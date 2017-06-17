---
layout: post
title: PySpark를 Jupyter에서 사용하기
category: Jupyter
---

Spark Standalone Mode를 기준으로 설명할 것이며, 사용할 파이썬 버전은 Python3입니다. `~/.bashrc`와 `/spark/conf/spark-env.sh`에 추가 설정을 해주면 됩니다.

## 설정

#### `~/.bashrc`

`SPARK_HOME`과 `PYSPARK_PYTHON`경로는 상이할 수 있습니다.
```vim
export SPARK_HOME=/home/sparkuser/spark
export PATH=$SPARK_HOME/bin:$PATH

export PYTHONPATH=$SPARK_HOME/python/:$PYTHONPATH
export PYTHONPATH=$SPARK_HOME/python/lib/py4j-0.10.4-src.zip:$PYTHONPATH

export PYSPARK_PYTHON=/usr/bin/python3
export PYSPARK_DRIVER_PYTHON=python3
```
`source`명령어로 변경내용을 적용합니다.

<br>

#### `/spark/conf/spark-env.sh`

```vim
PYSPARK_PYTHON=/usr/bin/python3
PYSPARK_DRIVER_PYTHON=python3
```

---

## 확인

`jupyter notebook`이나 `jupyter lab`을 실행하여 새로운 노트북을 생성합니다.(kernel은 python3)

셀에 아래 명령어를 입력합니다.
```python
from pyspark import SparkContext
from pyspark import SparkConf

conf = (SparkConf().setMaster('local[*]').setAppName('pyspark init'))
sc = SparkContext(conf=conf)
```

<br>

아래와 같은 결과가 뜨면 성공입니다.

```python
conf
```
> <pyspark.conf.SparkConf at 0x7f5cdf9ba748>


```python
sc
```
> <pyspark.context.SparkContext at 0x7f5cdf9ba908>
