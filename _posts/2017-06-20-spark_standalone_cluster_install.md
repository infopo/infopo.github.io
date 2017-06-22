---
layout: post
title: Standalone Mode Cluster 설치
category: Spark
---

노트북(데스크탑)과 싱글보드 컴퓨터(오렌지파이) 3대를 이용해 클러스터를 구성하는 과정을 보여드리겠습니다. 물론, 노트북(데스크탑)을 이용하지 않고 싱글보드 컴퓨터만으로도 클러스터를 구성할 수도 있습니다.

## 싱글보드 컴퓨터에 대한 선행 작업: `resize`, `update`, `upgrade`, `vim`, 고정ip, `sudoers`

우선, 랜선이 연결된 오렌지파이의 ip주소를 알아야 합니다. 그러기 위해서 공유기 모뎀의 기본게이트웨이 주소를 웹브라우저에 입력하여 설정화면에 접속을 합니다(172.30.1.254, 192.168.0.1, 192.168.219.1 등등). 여기서 유무선 단말정보와 같은 화면에서 접속 경과 시간으로 오렌지파이의 ip주소를 찾아내야 합니다(아직 더 나은 방법을 찾지 못해 이 방법을 사용하고 있습니다.).

찾아냈다면 우분투가 설치된 노트북(데스크탑)에서 오렌지파이에 원격접속을 하겠습니다. 터미널을 열고 아래 명령어를 입력합니다. 입력을 하면 비밀번호를 입력하라고 할 텐데, 기본 비밀번호는 orangepi입니다.
```
$ ssh orangepi@오렌지파이의_ip주소 -p 22
```

<br>

이제부터 선행작업을 시작하겠습니다. 연결할 오렌지파이의 개수만큼 이 과정을 반복하면 되겠습니다. 먼저, `resize`입니다. 오렌지파이 설치 후 `df -h`를 해보면 micro sd 카드만큼의 용량이 인식되지 않기 때문입니다(라즈베리파이의 경우는 이 명령어가 인식되지 않습니다.).
```
$ sudo fs_resize
```

<br>

다음으로는 host 추가입니다. 오렌지파이에서 설치 이후 `sudo: unable to resolve host OrangePI`라는 메세지가 계속 뜨는데 이 메세지가 안 뜨게 하기 위해서는 `/etc/hosts`로 들어가 `localhost`뒤에 `OrangePI`를 추가해줍니다.
```
127.0.0.1 localhost OrangePI
```

<br>

이제 `update`와 `upgrade`를 하도록 하겠습니다. 시간이 조금 걸릴 수 있습니다.
```
$ sudo apt-get update
$ sudo apt-get -y upgrade
```

<br>

`vim`을 설치할 차례인데, 만약 `vim`이 불편하다고 생각이 들면 설치하지 않고, 이미 설치가 된 `nano`를 이용해도 상관없습니다.
```
$ sudo apt-get -y install vim
```

<br>

고정된 ip로 접속하도록 설정을 하겠습니다. 이 설정을 하지 않으면 오렌지파이를 껐다가 켤 때마다 웹 브라우저에 기본 게이트웨이 주소를 입력하고, 후에 설명할 ip관련 설정들을 계속 바꾸어 주어야 하는 불편함이 발생할 수도 있습니다.

`/etc/network/interfaces`에 들어가 아래의 내용을 입력합니다. address부분은 여러 대의 오렌지파이를 연결하는 것을 고려해 연속되는 주소로 설정해주는 것이 편리합니다.
```vim
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static

address xxx.xxx.xxx.xx  # 원하는 ip주소로
netmask 255.255.255.0 # netmask는 $ ifconfig에서 Mask부분에 해당합니다.
gateway xxx.xxx.xxx.xxx # $ route에서 default Gateway에서 확인 가능합니다.
```

그 다음, `/etc/resolv.conf`에 아래 내용을 추가합니다.
```vim
nameserver 8.8.8.8
```

이제 변경된 ip주소를 적용하도록 하겠습니다. 터미널에 `sudo /etc/init.d/networking restart`를 입력하고, `ssh`로 오렌지파이에 변경된 ip주소로 접속이 된다면 성공입니다.

<br>

마지막으로, `sudo`사용 권한을 주도록 하겠습니다. 곧 `sparkuser`라는 사용자를 추가할 것인데, 아래 내용을 추가하지 않으면 `sparkuser`에서 `sudo`명령어를 사용하지 못하는 경우가 발생할 수도 있습니다.

`sudo vi /etc/sudoers`를 입력하고, `sparkuser`로 시작하는 부분을 추가합니다.
```vim
# User privilege specification
root ALL=(ALL:ALL) ALL
sparkuser ALL=(ALL:ALL) ALL
```

오렌지파이에서 필요한 선행작업들이 끝났습니다. 본격적인 cluster 구성 작업을 시작하겠습니다.

<br>

## 1. 사용자, 그룹 추가

cluster 구성 작업은 크게 5단계로 이루어져 있는데, **1~3단계는 공통으로 실시해주어야 합니다.**

```
$ sudo addgroup spakrgroup
$ sudo adduser --ingroup sparkuser sparkuser

$ su - sparkuser
```

이제부터 `sparkuser`로 로그인된 상태로 작업을 진행합니다.


## 2. Java 설치

`openjdk-7-jdk`, `default-jdk`, `oracle-java8-installer` 등 설치가능한 다양한 java버전이 있지만, 여기서는 oracle홈페이지에서 다운받는 방법을 소개하겠습니다.

노트북(데스크탑)에서는 [Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html){:target="_blank"} 에서 Java Platform (JDK)를 클릭한 후 Linux x64	tar.gz를 다운 받으면 됩니다. 운영체제가 64비트인지 32비트인지 확인하고 싶다면, 터미널에 `uname -m`을 입력하면 됩니다. x86_64라면 64비트, i686같은 형태라면 32비트입니다.

오렌지파이의 경우는 보통 gui를 이용하지 않기 때문에, ftp프로그램을 통해 파일을 옮기던가 하는 방법을 사용할 수 있습니다. 여기서는 따로 ftp를 사용하지 않을 것이고, `wget`을 사용하겠습니다. 다시 위의 링크로 들어가 Java Platform (JDK)를 클릭한 후 이번에는 Linux ARM 32 Hard Float ABI의 다운로드 버튼에 마우스를 올리고 우클릭하여 링크 주소를 복사합니다. 이제 ssh를 통해 오렌지파이로 접속이 된 터미널에서 쿠키관련 설정을 추가하여 Java를 다운 받도록 합니다.
```
$ wget 복사한_Java_링크주소 --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"
```

<br>

다운 받은 파일을 압축해제하고, 위치를 옮기겠습니다.
```
$ tar -vxzf 다운받은_Java_파일
$ sudo mv 압축해제한_Java_파일 /usr/lib/jvm
```

<br>

`~/.bashrc`에 들어가 Java설정을 가장 아래줄 밑에 추가합니다.
```vim
export JAVA_HOME=/usr/lib/jvm/압축해제한_Java_파일
export PATH=$JAVA_HOME/bin:$PATH
```

저장종료하고 `source ~/.bashrc`를 통해 변경 내용을 적용합니다. `javac -version`을 통해 제대로 설치가 되었는지 확인할 수 있습니다.

## 3. Spark 설치

[Download Apache Spark](http://spark.apache.org/downloads.html){:target="_blank"}에서 2.1.0, Pre-built for Hadoop 2.7 and later로 놓고 다운을 받습니다. 오렌지파이의 경우는 Java설치처럼 링크 주소를 복사하여 `wget`으로 다운을 받으면 됩니다.

압축해제를 합니다.
```
$ tar -vxzf 다운받은_Spark파일
```

<br>

`/home/sparkuser`로 압축해제한_Spark파일을 옮기고, 해당 디렉토리로 이동합니다.
```
$ sudo mv 압축해제한_Spark파일 /home/sparkuser
$ cd /home/sparkuser
```

<br>

사용자와 그룹을 바꾸겠습니다. 그리고 나서 `ll`명령어로 바뀌었는지 확인합니다.
```
$ sudo chown -R sparkuser:sparkgroup 압축해제한_Spark파일
```

<br>

압축해제한_Spark파일에 링크를 걸겠습니다.
```
$ ln -s 압축해제한_Spark파일 spark
```

<br>

`~/.bashrc`에서 `SPARK_HOME`설정을 합니다. `JAVA_HOME` 밑에 추가하면 됩니다.
```vim
export SPARK_HOME=/home/sparkuser/spark
export PATH=$SPARK_HOME/bin:$PATH
```

저장종료하고 `source ~/.bashrc`로 변경 내용을 적용합니다. `spark-shell --version`이 spark관련 내용을 출력하면 정상적으로 설치가 된 것입니다.

## 네트워크 설정

이제부터 네트워크 설정을 할 것입니다. master로 사용할 노트북(데스크탑), slave로 사용할 오렌지파이에 대한 설정이 상이하므로 주의해야 합니다. master와 slave를 구분해 아래의 내용들을 추가합니다.

- `/etc/hosts` (master, slave)
```vim
xxx.xxx.xxx.70      # master ip주소
xxx.xxx.xxx.101     # slave1 ip주소
xxx.xxx.xxx.102     # slave2 ip주소
xxx.xxx.xxx.103     # slave3 ip주소
```

- `/etc/hosts.allow` (master)
```vim
sshd:xxx.xxx.xxx.70    # master ip주소
```

- `/etc/ssh/sshd_config` (master)
```vim
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```

- `mkdir ~/.ssh` (master, slave)

- keygen (master)  

    ```
    $ ssh-keygen -t rsa -P ""
    $ cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys

    # slave ip에 해당하는 머신에 모두 실시해야 합니다.
    $ scp ~/.ssh/authorized_keys xxx.xxx.xxx.101:/home/sparkuser/.ssh/.
    $ scp ~/.ssh/authorized_keys xxx.xxx.xxx.102:/home/sparkuser/.ssh/.
    $ scp ~/.ssh/authorized_keys xxx.xxx.xxx.103:/home/sparkuser/.ssh/.
    ```

- `/spark/conf`로 이동해 `slaves.template`와 `spark-env.sh.template`의 파일명을 변경합니다. (master)  

    ```
    $ sudo mv spark-env.sh.template spark-env.sh
    $ sudo mv slaves.template slaves
    ```

- `spark-env.sh` (master, 필요에 따라 slave에도 추가)  
    ```vim
    SPARK_LOCAL_IP=xxx.xxx.xxx.70 # master ip
    SPARK_MASTER_HOST=xxx.xxx.xxx.70 # master ip
    SPARK_MASTER_PORT=7077
    SPARK_MASTER_WEBUI_PORT=8089  # tomcat 기본 포트가 8080이므로 변경합니다.

    # master, slave 다르게 설정가능합니다. 설정하지 않으면 가용한 모든 메모리를 사용합니다. :8089에서 확인 가능합니다.
    SPARK_WORKER_MEMORY=1g

    # master, slave 다르게 설정가능합니다. 설정하지마 않으면 가용한 코어를 모두 사용합니다. :8089에서 확인 가능합니다.
    SPARK_WORKER_CORES=4
    ```

- `slaves` (master)
    ```vim
    localhost  # master도 worker로 쓰고 싶다면 추가합니다
    xxx.xxx.xxx.101
    xxx.xxx.xxx.102
    xxx.xxx.xxx.103
    ```

## 5. 실행 및 확인

모든 설치과정이 끝났고, 이제 실행을 하여 확인을 하겠습니다. 우선 master로 설정한 머신에서 `$SPARK_HOME/sbin/start-all.sh`로 Spark를 실행합니다.

master에서 `$ jps`를 실행하면 아래와 같은 결과가 뜨고(수치는 다를 수 있습니다.),

> 25874 Worker  
25795 Master  
25962 Jps  

slave에서 같은 멸령어를 실행하면 아래와 같이 뜹니다(slave에서는 실행하는 것이 없습니다. master와 마찬가지로 수치는 다를 수 있습니다.).

> 3008 Jps
2977 Worker

이제 웹브라우저에서 xxx.xxx.xxx.70:8089를 입력하여 web UI를 확인하겠습니다.

![]({{ base.url }}/images/spark1.png)

`/spark/conf/slaves`에서 master도 worker에 추가했으므로 총 4개의 worker가 보입니다. 또한, Cores, Memory부분은 master머신의 경우 `/spark/conf/spark-env.sh`에서 4, 1g로 설정했기 때문에 저렇게 보이며, 나머지 slave의 경우 따로 설정을 하지 않았기 때문에 오렌지파이에서 가용한 만큼 표시를 하고 있습니다. 그리고 아직까지 Spark로 작업을 하지 않았으므로 Running Applications, Completed Applications에 아무런 내용이 없습니다.

간단한 예제들을 통해 Spark를 실행해보겠습니다(실행 전 반드시 `jps`를 입력해 Master, Worker가 출력되는지 확인해야 합니다.).

1. `spark-submit` 사용
터미널에서 Spark프로그램을 실행할 수 있는 `spark-submit`입니다. 아래 예제는 Spark에 내장된 예제로써, pi의 값을 출력합니다. 실행이 되면 로그 사이에 Pi is roughly 3.140835704178521와 유사한 메세지를 찾을 수 있습니다.
```
$ $SPARK_HOME/bin/spark-submit --class org.apache.spark.examples.SparkPi --master spark://MASTER_IP_입력:7077 /home/sparkuser/spark/examples/jars/spark-examples_2.11-2.1.0.jar
```

2. `spark-shell` 사용
Spark 프로그램을 실행하는 방법입니다.
```
$ $SPARK_HOME/bin/spark-shell --master spark://MASTER_IP_입력:7077
```
실행이 되었다면 아래와 같은 화면이 보일 것입니다.
```scala
Spark context available as 'sc' (master = spark://MASTER_IP:7077, app id = app-20170622221837-0001).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.1.0
      /_/

Using Scala version 2.11.8 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_111)
Type in expressions to have them evaluated.
Type :help for more information.

scala>
```
아래는 1~10000사이의 숫자 중에서 10보다 작은 수만 출력하는 예제입니다.
```scala
scala> val data = 1 to 10000
scala> val distData = sc.parallelize(data)
scala> distData.filter(_ < 10).collect()
```

3. `pyspark` 사용
`spark-shell`과 비슷하게 Python을 Spark에서 사용할 수 있습니다. 실행은 아래와 같습니다.
```
$ $SPARK_HOME/bin/pyspark --master spark://MASTER_IP_입력:7077
```
실행 직후 화면입니다.
```python
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /__ / .__/\_,_/_/ /_/\_\   version 2.1.0
      /_/

Using Python version 3.5.2 (default, Nov 17 2016 17:05:23)
SparkSession available as 'spark'.
>>>
```

```python
>>> rdd1 = sc.parallelize(range(1, 11))
>>> result = rdd1.collect()
>>> result
```

4. `jupyter notebook` 활용
`jupyter notebook`에서 `pyspark`를 실행해보겠습니다. 이를 위해 몇 가지 설정을 추가해줘야 합니다. [PySpark를 Jupyter에서 사용하기](https://jongwoo315.github.io/09-jupyter_add_pyspark/){:target="_blank"}를 참고하시면 됩니다. 추가 후, `$SPARK_HOME/sbin/stop-all.sh`로 Spark를 멈춘 후 `$SPARK_HOME/sbin/start-all.sh`로 다시 시작합니다. 그리고 `jupyter notebook`을 실행합니다.

```python
from pyspark import SparkConf, SparkContext, SQLContext
config = SparkConf().setMaster('spark://MASTER_IP_입력:7077').setAppName('pyspark_from_jupyter')

sc1 = SparkContext(conf = config)
sc1
```

```python
rawData = sc1.textFile('/home/sparkuser/spark/README.md')
print ('%s \n' % (rawData.first()))
print (rawData.count())
```

Spark를 실행할 수 있는 4가지 방법을 알아보았습니다. 그 결과를 web UI에서도 확인을 할 수 있습니다.

![]({{ base.url }}/images/spark2.png)

만약, 작업 도중이라면 http://MASTER_IP:4040/에서 현재 작업 진행상황을 볼 수도 있습니다. 다만, 작업이 완료되면 접근이 불가합니다.
