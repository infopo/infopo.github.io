---
layout: post
title: 정규분포 정리, plt.figure(), plt.subplots()
category: Python
---

## numpy 사용


```python
from numpy.random import normal
```

<br>

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

<br>

```python
# 정규분포를 따르지 않는 일반적인 난수
non_norm_height = np.random.randint(170, 180, 20)
```

<br>

```python
mu = 175
var = 4
height = np.random.normal(mu, var, 20)

def norm_dist():
    return [(1 / (np.sqrt(2*np.pi*var))) * np.exp(-((x-mu)**2)/(2*var)) for x in height]

dfh = pd.DataFrame({'height':height, 'prob':norm_dist()})
dfh.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>height</th>
      <th>prob</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>176.983865</td>
      <td>0.121961</td>
    </tr>
    <tr>
      <th>1</th>
      <td>174.511679</td>
      <td>0.193613</td>
    </tr>
    <tr>
      <th>2</th>
      <td>174.862678</td>
      <td>0.199002</td>
    </tr>
    <tr>
      <th>3</th>
      <td>171.629727</td>
      <td>0.048223</td>
    </tr>
    <tr>
      <th>4</th>
      <td>172.132686</td>
      <td>0.071378</td>
    </tr>
  </tbody>
</table>
</div>


<br>

```python
sum(dfh.prob)
```




    2.061306283935028


<br>

```python
# 아래에서는 plt. 에서 바로 subplots를 생성했다
# plt.figure()를 쓰면 각 plot의 크기를 설정할 수 있는 장점이 있다

fig = plt.figure()
subplot = fig.add_subplot(1, 1, 1)
#subplot.plot(dfh[0], dfh.index.values)
subplot.scatter(dfh.height, dfh.prob)
plt.show()
```


![png]({{ site.baseurl }} /images/normal_dist_sum_files/normal_dist_sum_6_0.png)

<br>

```python
fig, ax = plt.subplots(1, 1)
#ax.plot(dfh.height, dfh.prob)

#ax.scatter(non_norm_height, dfh.prob)
ax.scatter(dfh.height, dfh.prob)

plt.show()
```


![png]({{ site.baseurl }} /images/normal_dist_sum_files/normal_dist_sum_7_0.png)

<br>

## scipy 사용

[scipy.stats.norm document](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.norm.html){:target="_blank"}


```python
from scipy.stats import norm
```

<br>

```python
est = norm(loc=mu, scale=np.sqrt(var))
```

#### ppf


```python
# numpy.random.normal
np.sort(dfh.height)
```




    array([ 168.02512927,  169.91230429,  171.62972702,  171.77109022,
            172.13268612,  173.07751389,  174.15814035,  174.30578814,
            174.51167933,  174.57441716,  174.65568055,  174.86267802,
            175.7614779 ,  176.32476105,  176.98386498,  177.20176531,
            179.36408737,  180.60392868,  182.7560728 ,  183.27147727])


<br>

```python
# ppf -> Percent point function, numpy.linspace 사용
np.linspace(est.ppf(0.001), est.ppf(0.999), 20)
```




    array([ 168.81953539,  169.47011061,  170.12068583,  170.77126105,
            171.42183628,  172.0724115 ,  172.72298672,  173.37356194,
            174.02413717,  174.67471239,  175.32528761,  175.97586283,
            176.62643806,  177.27701328,  177.9275885 ,  178.57816372,
            179.22873895,  179.87931417,  180.52988939,  181.18046461])


<br>

```python
# ppf, arange 사용
np.arange(est.ppf(0.001), est.ppf(0.999))
```




    array([ 168.81953539,  169.81953539,  170.81953539,  171.81953539,
            172.81953539,  173.81953539,  174.81953539,  175.81953539,
            176.81953539,  177.81953539,  178.81953539,  179.81953539,
            180.81953539])


<br>

```python
# p=0.75일 때, x값(z값)?
est.ppf(0.75)
```




    176.34897950039218



#### cdf


```python
# x=175일 때, 누적확률은(p)?
est.cdf(175)
```




    0.5


<br>

```python
np.round(est.cdf(np.sort(dfh.height)), 3)
```




    array([ 0.001,  0.058,  0.098,  0.184,  0.277,  0.322,  0.349,  0.586,
            0.748,  0.762,  0.84 ,  0.845,  0.878,  0.889,  0.932,  0.94 ,
            0.961,  0.978,  0.987,  0.999])


<br>

```python
plt.plot(np.arange(20), np.sort(est.cdf(dfh.height)))
plt.show()
```


![png]({{ site.baseurl }} /images/normal_dist_sum_files/normal_dist_sum_20_0.png)


#### pdf


```python
# x값에 대한 정규분포함수값
# 이건 dfh.prob이랑 동일하다
est.pdf(dfh.height)
```




    array([ 0.00202438,  0.02668319,  0.12153708,  0.13312239,  0.05831459,
            0.18500726,  0.05978948,  0.10096717,  0.06601867,  0.15953317,
            0.17921847,  0.11911357,  0.09446537,  0.04225614,  0.15478825,
            0.01621514,  0.00147486,  0.08675775,  0.19478843,  0.16748473])

<br>


```python
dfh.prob
```




    0     0.002024
    1     0.026683
    2     0.121537
    3     0.133122
    4     0.058315
    5     0.185007
    6     0.059789
    7     0.100967
    8     0.066019
    9     0.159533
    10    0.179218
    11    0.119114
    12    0.094465
    13    0.042256
    14    0.154788
    15    0.016215
    16    0.001475
    17    0.086758
    18    0.194788
    19    0.167485
    Name: prob, dtype: float64



#### stats


```python
# Mean, Variance, Skew, Kurtosis

print (norm.stats(loc=175, scale=2, moments='mvsk'))
print (est.stats(moments='mvsk'))
```

    (array(175.0), array(4.0), array(0.0), array(0.0))
    (array(175.0), array(4.0), array(0.0), array(0.0))


#### rvs (Random variates)


```python
norm.rvs(175, 4, 10)
```




    array([ 169.94973808,  174.20345003,  171.65067103,  173.67808369,
            178.15750573,  179.18391464,  173.96181439,  175.48923808,
            180.02436536,  178.45060004])


<br>

```python
np.random.normal(175, 4, 10)
```




    array([ 169.24431896,  169.14127749,  168.69309429,  171.63411788,
            173.52711404,  173.23052814,  179.08513392,  176.95025606,
            181.92236243,  172.34384902])
