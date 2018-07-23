
# Effect Size 

### SWBATs

* Illustrate a clear understanding of the terms "Effect" and "Effect Size" in a statistical context.
* Compare and contrast p-value and effect size for identifying significance of results.
* Calculate simple (unstandardized) effect size using Python and SciPy
* Interpret results of simple effect size and identify shortcomings of this approach
* Calculate standardized effect size using Cohen's d statistic
* Visualize and Interpret the $d$ value as size of effect


### Introduction to Effect Size

'Effect size' is used to quantify the *size of the difference* between two groups under observation. Effect sizes are easy to calculate, understand and apply to any measured outcome and is this approach is applicable to a multitude of study domains. It is highly valuable towards quantifying the *effectiveness of a particular intervention, relative to some comparison*. Measuring effect size allows scientists to go beyond the obvious and simplistic, *'Does it work or not?'* to the far more sophisticated, *'How well does it work in a range of contexts?'*. 

[More on effect size](https://www.slideshare.net/gaetanlion/effect-size-presentation)



#### P-value vs. Effect Size

Effect size measurement places its emphasis on the effect size only, unlike statistical significance which combines effect size and sample size, thus promoting a more scientific approach towards knowledge accumulation. Effect size is therefore routinely used towards **Meta-Analysis** i.e. for combining and comparing estimates from different studies conducted on different samples. 

By increasing sample size, you can show there is a statistically significant difference between two Means. However, **Statistically significant does not imply “significant.**.

>**P value** = probability sample Means are the same.

>(1 – P) or **Confidence Level** = probability sample Means are different.

>**Effect Size** = how different sample Means are


In light of this, it is possible to achieve highly significant p-values for effect sizes that have no practical significance. In contrast, study designs with low power can produce non-significant p-values for effect sizes of great practical importance.

[Further details on p-value vs. effect size calculation](http://www.win-vector.com/blog/2017/09/remember-p-values-are-not-effect-sizes/)

### Why do data scientists need to know about 'Effect Size'?

Consider the experiment conducted by Dowson (2000) to investigate time of day effects on children learning: do children learn better in the morning or afternoon? A group of 38 children were included in the experiment. Half were randomly allocated to listen to a story and answer questions about it at 9am, the other half to hear exactly the same story and answer the same questions at 3pm. Their comprehension was measured by the number of questions answered correctly out of 20.

The average score was 15.2 for the morning group and 17.9 for the afternoon group, giving a difference of 2.7. 
**How big a difference is this? **

If the results were measured on a standard scale, such as GCSE grades, interpreting the difference would not be a problem. If the average difference was, say, half a grade or a full grade, most people would have a fair idea of the educational significance of the effect of reading a story at different times of day. However, in many experiments there is no familiar scale available on which to record the outcomes i.e. student comprehension in this case. The experimenter often has to invent a scale or to use (or adapt) an already existing one - but generally most people would be unfimilar with interpretation of this scaler.

In data analytics domain, effect size calculation serves three primary goals:

* Communicate **practical significance** of results. An effect might be statistically significant, but does it matter in practical scenarios ?

* Effect size calculation and interpretation allows you to draw **Meta-Analytical** conclusions. This allows you to group together a number of existing studies, calculate the meta-analytic effect size and get the best estimate of the tur effect size of the population. 

* Perform **Power Analysis** , which help determine the number of particicpants (sample size) that a study would require to achieve a certain probability of finding a true effect - if there is one. 


## Calculating effect size in Python 

### Using SciPy for measuring effect size

SciPy (pronounced “Sigh Pie”) is open-source software for mathematics, science, and engineering. The SciPy package contains various toolboxes dedicated to common issues in scientific computing. Its different submodules correspond to different applications, such as interpolation, integration, optimization, image processing, statistics, special functions, etc. For our experiment we would use `scipy.stats` package which contains statistical tools and probabilistic descriptions of random processes. Detailed documentation of SciPy is available [here](https://docs.scipy.org/doc/scipy/reference/index.html). 


```python
# Import necessary modules 
from __future__ import print_function, division
import numpy as np

# Import SciPy stats and matplotlib for calculating and visualising effect size
import scipy.stats
import matplotlib.pyplot as pyplot

%matplotlib inline

# seed the random number generator so we all get the same results
np.random.seed(10)
```

### Example: 
To explore statistics that quantify effect size, let's first look at the difference in height between men and women in USA, based on the mean and standard deviation for male and female heights as given in (BRFSS) Behavioral Risk Factor Surveillance System.

>**Males Height**  (Mean = 178 , Standard Deviation = 7.7)

>**Female Height** (Mean = 163 , Standard Deviation = 7.3)

We can use `scipy.stats.norm()` to represent the height distributions by passing mean and standard deviation values as arguments for creating normal distribution. 


```python
#Mean height and sd for males
male_mean = None
male_sd = None

# Generate a normal distribution for male heights using scipy.stats.norm()
male_height = None
```

 The result `male_height` is a SciPy `rv` object which represents a **normal continuous random variable**. 


```python
male_height
```




    <scipy.stats._distn_infrastructure.rv_frozen at 0x1143cb0b8>



Use the mean and standard deviation for female height and repeat calculations shown above to calculate `female_height` as an `rv` object.


```python
female_mean = None
female_sd = None
female_height = None
```

###  Evaluate Probability Density Function (PDF)

A continuous random variable, as calculated above, takes on an uncountably infinite number of possible values. 

For a **discrete** random variable X that takes on a finite or infinite number of possible values, we determine P(X = x) for all of the possible values of X, and call it the probability mass function (PMF). 

For **continuous** random variables, as in the case of heights, the probability that X takes on any particular value x is 0. That is, finding P(X = x) for a continuous random variable X is not going to work. Instead, we'll need to find the probability that X falls in some interval (a, b) i.e. we'll need to find **P(a < X < b)** using a **probability density function(PDF)**. 


The following function evaluates the normal (Gaussian) probability density function within 4 standard deviations of the mean. The function ingests an rv object and returns a pair of NumPy arrays.


```python
def evaluate_PDF(rv, x=4):
    '''Input: a random variable object, standard deviation
       output : x and y values for the normal distribution
       '''
    
    # Identify the mean and standard deviation of random variable 
    mean = None
    std = None

    # Use numpy to calculate evenly spaced numbers over the specified interval (4 sd) and generate 100 samples.
    xs = None
    
    # Calculate the peak of normal distribution i.e. probability density. 
    ys = None

    return xs, ys # Return calculated values
```

Let's use the function above to caculate xs and ys for male and female heights (pass the `rv` object as an argument) and plot the resulting xs and ys for both distributions to visualise the effect size.


```python
# Male height
xs, ys = None
#pyplot.plot(xs, ys, label='male', linewidth=4, color='#beaed4') 

#Female height 
xs, ys = None
# Plot female distribution
# Label the plot
```


![png](output_15_0.png)


Let's assume for the sake of simplicity that these are the true distributions for the population. As you studied earlier, in real life we never observe the true population distribution.  We generally have to work with a random sample. Let's try to work out how different these two groups are with respect to height by calculating un-standardized and standardized effect sizes.



## Un-standardized or Simple Effect Size Calculation

An unstandradized effect size simply tries to find the different between two groups by calculating the difference between distribution means. Here is how we can do it in python. 

We can use `rvs` method from `scipy.stats` to generate 1000 random samples from the population distributions.  Note that these are totally random and representative samples, with no measurement error.

following our assumption of a true distribution. 

Visit [this link](https://docs.scipy.org/doc/scipy-1.0.0/reference/tutorial/stats.html) for more details on `sciPy.stats`. 


```python
male_sample = None
```

The resulting samples are numPy arrays, so we can now easily calculate mean and sd of random samples. 


```python
mean_male = None 
std_male = None

# (177.88791390576085, 7.222274730410271)
```

The sample mean is close to the population mean, but not exact, as expected.

Let's perform above calculation for female heights to calculate mean and sd of random samples from `female_height` `rv` object**


```python
# Solution
female_sample = None
mean2, std2 = None, None

# (162.91903182040372, 7.261850929417819)
```

And the results are similar for the female sample.

Now, there are many ways to describe the magnitude of the difference between these distributions. An obvious one is the difference in the means. 

Now we calculate the difference in means of both distributions identified above.**


```python
difference_in_means =None 

# in cm
# 15.041607291585223
```

This shows that on average, men are around 15 centimeters taller. For some applications, that would be a good way to describe the difference, but there are caveats:

* Without knowing more about the distributions (like the standard deviations or Spread of the distribution) it's hard to interpret whether a difference like 15 cm is a **big difference** or not.

* The magnitude of the difference depends on the units of measure, making it hard to compare across different studies that may be conducted with different units of measurement.

There are a number of ways to quantify the difference between distributions.  A simple option is to express the difference as a percentage of the mean.


Let's figure out what is the relative difference in means of two populations, scaled by mean of male heights and  expressed as a percentage. 


```python
relative_difference = None


#  8.414783082614122
```




    8.414783082614122



But a problem with relative differences is that you have to choose which mean to express them relative to. try above with female height.


```python
relative_difference = None

# 9.18792722869745
```




    9.236689246642001



### Overlap threshold

As you can see above, there is still difference in results when we express the relative difference, relative to male height and female height. Perhaps we can look for amount of overlap between the two distributions.  To define overlap, we choose a threshold between the two means.  The simple threshold is the midpoint between the means:


```python
# Calculate the midpoint between means
simple_thresh = None
# 170.36711025996823
```




    170.36711025996823



A better, but slightly more complicated threshold is the place where the PDFs cross.


```python
thresh = (std1 * mean2 + std2 * mean1) / (std1 + std2)
thresh
```




    170.42334559337462



In this example, there's not much difference between the two thresholds.
Now we can count how many men are below the threshold:


```python
male_below_thresh = None
#  154
```




    154



Simiularly, we can calculate how many women are above calculated threshold


```python
female_above_thresh = None
#  150
```

![auc](auc.png)

The "overlap" (shaded region above) is the total **AUC (Area Under the Curves)**. We can use this to identify the sample that end up on the wrong side of the threshold. We can calculate the amount of overlap as shown below. 


```python
# Calculate the overlap 
overlap =None
# 0.304
```

Or in more practical terms, you might report the fraction of people who would be misclassified if you tried to use height to guess sex:


```python
misclassification_rate = None
# 0.152
```




    0.152



### Probability of superiority (Non-parametric)

Another "non-parametric" way to quantify the difference between distributions is what's called **"probability of superiority"**, which is the probability that *"a randomly-chosen man is taller than a randomly-chosen woman"*, which makes perfect sense.

> Question: If we choose a male and a female sample at random, what is the probability that males are taller than females ? 


```python
# Python zip() The zip() function take iterables (can be zero or more), 
# makes iterator that aggregates elements based on the iterables passed, 
# and returns an iterator of tuples.

# 0.932
```




    0.932



> Question: If we choose a female and a male sample at random, what is the probability that female are smaller than males in height? Is it different/same as above? **


```python

# 0.932
```




    0.932



Overlap (or misclassification rate) as shown above, and "probability of superiority" have two good properties:

* As probabilities, they don't depend on units of measure, so they are comparable between studies.

* They are expressed in operational terms, so a reader has a sense of what practical effect the difference makes.

There is one other common way to express the difference between distributions i.e. the difference in means, standardized by dividing by the standard deviation.



Here's a function that encapsulates the code we have already seen for computing overlap and probability of superiority.


```python
def overlap_superiority(group1, group2, n=1000):
    """Estimates overlap and superiority based on a sample.
    
    group1: scipy.stats rv object
    group2: scipy.stats rv object
    n: sample size
    """

    # Get a sample of size n from both groups
    group1_sample = None
    group2_sample = None
    
    # Identify the threshold between samples
    thresh = None

    # Calculate no. of values above and below for group 1 and group 2 respectively
    above = None
    below = None
    
    # Calculate the overlap
    overlap = None
    
    # Calculate probability of superiority
    superiority = None

    return overlap, superiority
```


```python
# uncomment below and run 
# overlap_superiority(male_height, female_height, n=1000)

# 170.5
# (0.325, 0.921)
```

### Standardized effect size

When analysts generally talk about effect sizes, they refer to some method of calculating a *standadized* effect size. The standardized effect size statistic would divide effect size by some standardizer i.e. standard deviation :

>**Effect Size / Standardiser**

When interpreting, this statistic would be in terms of standard deviations e.g. The mean height of males in USA is 1.4 standard deviations higher than mean female heights etc.The effect size measure we will be learning about in this lesson is Cohen’s d. This measure expresses the size of an effect as a number standard deviations, similar to a z-score in statistics.

### Cohen's $d$

Cohen’s D is one of the most common ways to measure effect size.  As an effect size, Cohen's d is typically used to represent the magnitude of differences between two (or more) groups on a given variable, with larger values representing a greater differentiation between the two groups on that variable. 

Cohen’s d is similar to the unpaired t test t value. It relies on Standard Deviations instead of Standard Errors

The basic formula to calculate Cohen’s $d$ is:

> ** $d$ = effect size (difference of means) / pooled standard deviation **

The denominator is the **standardiser**, and it is important to select the most appropriate one for a given dataset. The pooled standard deviation is the average spread of all data points around their group mean (not the overall mean). 

> **Exercise: Write a Python function that takes in two `rv` objects i.e. male and female heights in this case and returns Cohen's d statistic using the formula *mean(1) - mean(2)/sd(pooled)* **


```python
# Solution

def Cohen_d(group1, group2):

    # Compute Cohen's d.

    # group1: Series or NumPy array
    # group2: Series or NumPy array

    # returns a floating point number 

    diff = None

    n1, n2 = None, None
    var1 = None
    var2 = None

    # Calculate the pooled threshold as shown earlier
    pooled_var = None
    
    # Calculate Cohen's d statistic
    d = None
    
    return d
```

Computing the denominator is a little complicated; in fact, people have proposed several ways to do it.  [Here](https://scientificallysound.org/2017/07/13/cohens-d-standardiser/) is a brief description on using standardisers while calculating Cohen's $d$ for standard effect sizes.  

This implementation uses the "pooled standard deviation", which is a weighted average of the standard deviations of the two groups.

And here's the result for the difference in height between men and women.


```python
# Cohen_d(male_sample, female_sample)
# 2.0669285200851877
```




    2.0669285200851877



### Interpreting $d$
Most people don't have a good sense of how big $d=2.0$ is. If you are having trouble visualizing what the result of Cohen’s D means, use these general “rule of thumb” guidelines (which Cohen said should be used cautiously):

>**Small effect = 0.2**

>**Medium Effect = 0.5**

>**Large Effect = 0.8**

Here is as excellent online visualisation tool developed by [Kristoffer Magnusson](http://rpsychologist.com/so) to help interpret the results of cohen's $d$ statistic. 

Inspired from the above illustratoin, following function that takes Cohen's $d$, plots normal distributions with the given effect size, and prints their overlap and superiority.


```python
def plot_pdfs(cohen_d=2):
    """Plot PDFs for distributions that differ by some number of stds.
    
    cohen_d: number of standard deviations between the means
    """
    group1 = scipy.stats.norm(0, 1)
    group2 = scipy.stats.norm(cohen_d, 1)
    xs, ys = evaluate_PDF(group1)
    pyplot.fill_between(xs, ys, label='Group1', color='#ff2289', alpha=0.7)

    xs, ys = evaluate_PDF(group2)
    pyplot.fill_between(xs, ys, label='Group2', color='#376cb0', alpha=0.7)
    
    o, s = overlap_superiority(group1, group2)
    print('overlap', o)
    print('superiority', s)
```

Here's an example that demonstrates the function:


```python
#plot_pdfs(5)
# Try changing the d value and observe the effect on the outcome below
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-6-f74cd74a513c> in <module>()
    ----> 1 plot_pdfs(5)
          2 # Try changing the d value and observe the effect on the outcome below
    

    <ipython-input-5-11e922de96f8> in plot_pdfs(cohen_d)
          6     group1 = scipy.stats.norm(0, 1)
          7     group2 = scipy.stats.norm(cohen_d, 1)
    ----> 8     xs, ys = evaluate_PDF(group1)
          9     pyplot.fill_between(xs, ys, label='Group1', color='#ff2289', alpha=0.7)
         10 
    

    NameError: name 'evaluate_PDF' is not defined


Cohen's $d$ has a few nice properties:

* Because mean and standard deviation have the same units, their ratio is dimensionless, so we can compare $d$ across different studies.

* In fields that commonly use $d$, people are calibrated to know what values should be considered big, surprising, or important.

* Given $d$ (and the assumption that the distributions are normal), you can compute overlap, superiority, and related statistics.

## Summary and Conclusion

In this lesson, we highlighted the importance of calculating and interpreting effect size in Python as a measure of observing real world difference between two groups. You learnt about simple (unstandardized) effect size calculation as difference of means, as well as standardization of this calculation with standard deviation as a standardizer. You also learnt what is Cohen's d statistic and how to use it for pratical purposes. The best way to report effect size often depends on the audience, goals and subjects of study.  There is often a tradeoff between summary statistics that have good technical properties and statistics that are meaningful to a general audience.
