---
layout: post
title:  Central Limit Theorem and Law of Large Numbers!"
date:   2021-01-18 12:38:46 +0530
categories: statistics
---

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.dates as mdates

## This code requires sns >1.11.0
import seaborn as sns 

folder = 'Assignment3/'
np.random.seed(97)
```

## Q3 
<b>Illustrate the Law of Large Numbers and Central Limit Theorem for the $t_\nu$-distribution for different values of $\nu$. Use $\nu = 100$ </b>

### (a) Draw $M$ i.i.d random samples of length N from the $t_\nu$ distribution. $M = 500 ~\text{and}~ N = 10000$


```python
def generate_distribution(v=100):
    M = 500 
    N = 10000

    ##Checked on Exponential Distribution as well to check for implementation bug; 
    ##the results looked alright for exponential case as well.
    ## t_variables = [np.random.exponential(1, size=N) for _ in range(M)]

    ##Standard T distribution
    t_variables = [np.random.standard_t(v, size=N) for _ in range(M)]
    t_df = pd.DataFrame(t_variables)
    return t_df

#nu = 100
v = 100
t_df = generate_distribution(v)
t_df.shape ##each row corresponds to 1 draw of 10000 values from t-distribution
```




    (500, 10000)



### (b) For each sample $m = 1, ..., M$ compute the sample means for the first $n = 5, 10, 100, 500, 1000, 10000$ draws of the sample. 


```python
samples = [5, 10, 100, 500, 1000, 10000]

def sample_mean_create(t_df):
    sample_mean_df = pd.DataFrame()    
    for n in samples:
        sample_mean_df[n] = pd.Series(np.mean(r[1:n+1]) for r in t_df.itertuples())
    return sample_mean_df
```


```python
sample_mean_df = sample_mean_create(t_df)
display(sample_mean_df)
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>5</th>
      <th>10</th>
      <th>100</th>
      <th>500</th>
      <th>1000</th>
      <th>10000</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.914510</td>
      <td>-0.167780</td>
      <td>0.017331</td>
      <td>0.011185</td>
      <td>0.041914</td>
      <td>0.003841</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.014819</td>
      <td>0.240675</td>
      <td>0.014905</td>
      <td>0.003448</td>
      <td>0.013627</td>
      <td>0.009953</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.123534</td>
      <td>0.277000</td>
      <td>0.064362</td>
      <td>-0.069515</td>
      <td>-0.001274</td>
      <td>0.025583</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.047680</td>
      <td>0.310886</td>
      <td>0.183744</td>
      <td>0.078568</td>
      <td>0.055773</td>
      <td>0.010213</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.217392</td>
      <td>-0.248325</td>
      <td>0.024993</td>
      <td>0.081926</td>
      <td>0.039801</td>
      <td>0.004095</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>495</th>
      <td>0.518030</td>
      <td>0.744271</td>
      <td>0.025818</td>
      <td>0.029715</td>
      <td>0.022116</td>
      <td>-0.002505</td>
    </tr>
    <tr>
      <th>496</th>
      <td>0.702118</td>
      <td>0.452217</td>
      <td>0.260017</td>
      <td>0.075112</td>
      <td>0.061931</td>
      <td>0.021841</td>
    </tr>
    <tr>
      <th>497</th>
      <td>0.570883</td>
      <td>0.101392</td>
      <td>-0.097052</td>
      <td>-0.095220</td>
      <td>-0.074081</td>
      <td>-0.023038</td>
    </tr>
    <tr>
      <th>498</th>
      <td>-0.409794</td>
      <td>-0.184538</td>
      <td>0.106285</td>
      <td>0.065896</td>
      <td>0.020578</td>
      <td>-0.005990</td>
    </tr>
    <tr>
      <th>499</th>
      <td>0.438783</td>
      <td>0.125772</td>
      <td>-0.119980</td>
      <td>-0.041228</td>
      <td>0.003138</td>
      <td>0.003944</td>
    </tr>
  </tbody>
</table>
<p>500 rows × 6 columns</p>
</div>


### (c) For each $n$, compute the mean, standard deviation and variance of the sample means across the M samples.  


```python
def describe_sample_mean(df):
    details = sample_mean_df.describe() 
    details.loc["variance"] = details.loc["std"]**2
    details = details.loc[["mean", "std", "variance"]]
    display(details)
```


```python
describe_sample_mean(sample_mean_df)
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>5</th>
      <th>10</th>
      <th>100</th>
      <th>500</th>
      <th>1000</th>
      <th>10000</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mean</th>
      <td>0.032088</td>
      <td>0.025480</td>
      <td>0.004188</td>
      <td>-0.002063</td>
      <td>0.000263</td>
      <td>0.000254</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.443349</td>
      <td>0.325257</td>
      <td>0.095547</td>
      <td>0.043541</td>
      <td>0.031402</td>
      <td>0.009986</td>
    </tr>
    <tr>
      <th>variance</th>
      <td>0.196558</td>
      <td>0.105792</td>
      <td>0.009129</td>
      <td>0.001896</td>
      <td>0.000986</td>
      <td>0.000100</td>
    </tr>
  </tbody>
</table>
</div>


Theoretical mean is 0 and Theoretical variance is $\frac{100}{100-2} = 1.02$. And these values are consistent with what we see in the table above.

### (d) For each $n$, plot the distributions of the M sample Means.


```python
def plot_histograms_n(df, v, same_xaxis=False):
    f, axes = plt.subplots(3, 2, figsize=(15,15))
    axes = axes.ravel()
    for i, n in enumerate(samples):
        if same_xaxis:
            plt.setp(axes, xlim=(-1., 1.))
        sns.histplot(df[n], ax=axes[i], kde=True)
        axes[i].set_title("samples = %s"%n)
        axes[i].set(xlabel='')
    f.suptitle('degree of freedom = %s'%v)

plot_histograms_n(sample_mean_df, v)
```


    
![png](output_12_0.png)
    


One can observe that as we increase the number of samples, 

To compare X-axis in the above plot have similar range:


```python
plot_histograms_n(sample_mean_df, v, same_xaxis=True)
```


    
![png](output_14_0.png)
    


### (e) Describe how these simulations relate to the LLN and the CLT.

We can see from table of ques (c) is that as N increases, the mean of the sample is closer to the theoretical / true mean. This is consistent with the LLN. 

Similarly, if we see the distribution of the sample means, we see that they follow roughly normal distribution (more normal as n increases) and their mean is around the true mean $\mu=0$. Their variance is decreasing with n - this also follows from the fact that $\hat{\sigma}^2 = \frac{\sigma^2}{n}$. This observation is in line with CLT. 

### (f) Repeat the above for $\nu = 10, 5, 2, 1, 0.5$


```python
def experiment_nu(v, uniform_hist=True):
    t_df = generate_distribution(v)
    sample_mean_df = sample_mean_create(t_df)
    plot_histograms_n(sample_mean_df, v, uniform_hist)
```


```python
for v in [10, 5]:
    experiment_nu(v)
```


    
![png](output_18_0.png)
    



    
![png](output_18_1.png)
    



```python
for v in [2, 1]:
    experiment_nu(v, uniform_hist=False)
```


    
![png](output_19_0.png)
    



    
![png](output_19_1.png)
    



```python
#for v in [0.5]:
#    experiment_nu(v, uniform_hist=False)
#computer program crashed due to memory! the process here is very unstable! 
#because the variance is also undefined with this degree of freedom!
```

### (f) How does the value of $\nu$ affect the limiting?

With decreasing values of $\nu$ the variance of the process increases. So even with 10000 samples, the distribution of the sample mean was not coverging to a normal distribution. 

For $\nu = 1$ the CLT doesn't hold true at all, because the variance is $\infty$. This can be observed in the histogram plot as well.

For $\nu = 0.5$ my computer couldn't do the sampling even and erroring out with Memory error (taking up >8GB of RAM). It was happening mostly due to the variance being not defined at that range. 



```python

```

# MME vs MLE

MM estimator vs ML estimator.

(c) Set the true $\theta = 1$. Repeat the testing for n = 20, 100, 1000:


```python
theta = 1
n_range = [20, 100, 1000]

def plot_histograms_mm_mle(mm, mle, n):
    f, axes = plt.subplots(1, 2, figsize=(16, 8))
    axes = axes.ravel()
    if False:
        plt.setp(axes, xlim=(-1., 1.))
    sns.histplot(mm, ax=axes[0], kde=True)
    axes[0].set_title("MM")
    axes[0].set(xlabel='')
         
    sns.histplot(mle, ax=axes[1], kde=True)
    axes[1].set_title("MLE")
    axes[1].set(xlabel='')
         
    f.suptitle('n = %s'%n)
    
def describe_ml_mle(mm, mle, n):
    mm.name = 'MM Estimator'
    mle.name = 'MLE Estimator'
    df = pd.concat([mm, mle], axis=1)
    details = df.describe()
    details.loc["variance"] = details.loc["std"]**2
    details.loc["bias"] = details.loc["mean"] - theta
    details = details.loc[["mean", "std", "variance", "bias"]]
    print("for n = %s"%n)
    display(details)
    
def ml_mle_compare(n):
    samples = np.random.uniform(0, theta, size = (10000, n))
    sample_df = pd.DataFrame(samples)
    
    mm = 2 * sample_df.mean(axis=1)
    mle = sample_df.max(axis=1)
    plot_histograms_mm_mle(mm, mle, n)
    describe_ml_mle(mm, mle, n)
```


```python
n=20
ml_mle_compare(n)
```

    for n = 20
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MM Estimator</th>
      <th>MLE Estimator</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mean</th>
      <td>1.002949</td>
      <td>0.953376</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.129881</td>
      <td>0.045085</td>
    </tr>
    <tr>
      <th>variance</th>
      <td>0.016869</td>
      <td>0.002033</td>
    </tr>
    <tr>
      <th>bias</th>
      <td>0.002949</td>
      <td>-0.046624</td>
    </tr>
  </tbody>
</table>
</div>



    
![png](output_25_2.png)
    



```python
n=100
ml_mle_compare(n)
```

    for n = 100
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MM Estimator</th>
      <th>MLE Estimator</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mean</th>
      <td>0.999920</td>
      <td>0.989939</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.057335</td>
      <td>0.010047</td>
    </tr>
    <tr>
      <th>variance</th>
      <td>0.003287</td>
      <td>0.000101</td>
    </tr>
    <tr>
      <th>bias</th>
      <td>-0.000080</td>
      <td>-0.010061</td>
    </tr>
  </tbody>
</table>
</div>



    
![png](output_26_2.png)
    



```python
n=1000
ml_mle_compare(n)
```

    for n = 1000
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MM Estimator</th>
      <th>MLE Estimator</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mean</th>
      <td>0.999905</td>
      <td>9.990151e-01</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.018333</td>
      <td>9.736021e-04</td>
    </tr>
    <tr>
      <th>variance</th>
      <td>0.000336</td>
      <td>9.479011e-07</td>
    </tr>
    <tr>
      <th>bias</th>
      <td>-0.000095</td>
      <td>-9.848648e-04</td>
    </tr>
  </tbody>
</table>
</div>



    
![png](output_27_2.png)
    


### (d) For each $n$, compare the properties of the MLE and MM estimators in these simulations to their theoretical distributions.

MLE here looks like beta distribution, however the theoretical distribution should have been normal. 
MM estimator is normally distributed as per expectation.

### (e) Which properties of the estimators in the simulated data are expected, i.e. close to their theoretical properties, and which one are not? 

For MM estimator, we can directly interpret the results from CLT. The estimator is twice that of sample mean. So, as per CLT, the distribution follows a normal distribution - the mean of the distribution converges to 1 (the true mean) as n increases. Also, the variance of the distribution is decreasing as expected. The bias converges to 0 for high n. So, as expected, this is an unbiased estimator of theta. 

Similarly for MLE estimator, we can observe that it is biased. But as n increases, the mean converges to the true mean. However, I had expected that the asymptotic behaviour of MLE should be normally distributed. However that is not the case. It looks like an beta distribution.  

### (f) If the properties of the simulated estimators contradict the theoretical properties, the assumptions underlying the theoretical results must be violated. Which assumptions are violated in this case?

According to the chapter 8.8 in DGS textbook, and theorem 8.8.5; the asymptotic distribution is standard normal in case the 2nd and 3rd derivative of likelihood function must exist and satisfy certain regulatory conditions. The regularity conditions require that the MLE was obtained as a stationary point of the likelihood function and derivatives of the likelihood function at this point exist upto 3rd order. This assumption is violated in this case. 

(I had referred to https://stats.stackexchange.com/questions/435794/asymtotic-distribution-of-the-mle-of-a-uniform)


```python

```
