Point Pattern Analysis V
========================================================
author: Megan Coad and Alexis Polidoro
date: 
autosize: true

Key Points
========================================================
- Further understanding of null landscapes 
- understand what simulation envelopes are and why they are used 
- importance of defining a region 
- what edge effects are
- Issues with sample point patterns 


Motivation: Hypothesis Testing 
========================================================
- when making a decision whether the reject a null hypothesis, we determine the probability that we are making a mistake when doing so

Tests of hypothesis are developed following these general steps:

1. Identify a null hypothesis of interest, and if possible alternative hypotheses as well

2. Derive the expected value of the summary statistic of interest.

3. To make a decision whether to reject the null hypothesis, we need to know the _variance_ of the expected value under the null hypothesis.


<<<<<<< HEAD
Null Landscapes Revisited
========================================================
- A null landscape is a landscape produced by a random process
- A useful way of generating null landscapes for point patterns is by means of a Poisson process
- This function generates a null landscape given an intensity parameter and a window


Creating a Null Landscape 
=======

Recall: Creating a Null Landscape 
>>>>>>> 0b233e5f9ff92fd3559e4c4aa39ba26d715bb9fe
========================================================
Create the window:


```r
W <- pp1.ppp$window
```

Generate a null landscape:

```r
sim1 <- rpoispp(lambda = 81, win = W)
```

<<<<<<< HEAD
=======
***

>>>>>>> 0b233e5f9ff92fd3559e4c4aa39ba26d715bb9fe
The value of this function is a `ppp` object that can be analyzed:

![plot of chunk unnamed-chunk-4](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-4-1.png)


Creating a Null Landscape Contd. 
========================================================

<<<<<<< HEAD
Importantly, you can apply any of the techniques that you have seen so far, for instance, the $\hat{G}$-function:


Lets plot the empirical functions. To plot using `ggplot2` you can stack the two dataframes as follows (after adding a factor to indicate if it is the empirical function or a simulation):


Create a plot:

![plot of chunk unnamed-chunk-7](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-7-1.png)

- the empirical function is very, very similar to the simulated null landscape, But is this purely a coincidence? When we simulate a null landscape, there is the possibility, however improbable, that it will replicate some meaningful process purely by chance.
=======

Lets plot the empirical functions.


- the empirical function is very  similar to the simulated null landscape, But is this purely a coincidence? 
- When we simulate a null landscape, there is the possibility, however improbable, that it will replicate some meaningful process purely by chance.


***

![plot of chunk unnamed-chunk-7](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-7-1.png)
>>>>>>> 0b233e5f9ff92fd3559e4c4aa39ba26d715bb9fe


Null Landscape Contd. 
========================================================

To be sure, we can simulate and analyze a second null landscape:


Plot again:

![plot of chunk unnamed-chunk-9](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-9-1.png)

Simulation Envelopes 
========================================================
- the area covered by the $\hat{G}$-functions of the simulated landscapes above are an estimate of the variance. The set of functions estimated on the null landscapes are called _simulation envelopes_.
- The simulation provides a _pseudo-p-value_. If you generate 99 null landscapes, and the empirical pattern is still different, the probability that you are mistaken by rejecting the null hypothesis is at most 1%
<<<<<<< HEAD
- The package `spatstat` includes a function, called `envelope`, that can be used to generate simulation envelopes for several statistics used in point pattern analysis.


![plot of chunk unnamed-chunk-11](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-11-1.png)

- It is easy to see that in this case the empirical function falls within the simulation envelopes, and thus it is very unlikely to be different from the null landscapes.
=======



- the empirical function falls within the simulation envelopes, and thus it is very unlikely to be different from the null landscapes.

***

![plot of chunk unnamed-chunk-11](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-11-1.png)


>>>>>>> 0b233e5f9ff92fd3559e4c4aa39ba26d715bb9fe

Simulation Envelopes Contd. 
========================================================
- Now the empirical function lies outside of the simulation envelopes, which makes it very unlikely that it is similar to the null landscapes.


![plot of chunk unnamed-chunk-13](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-13-1.png)

Defining a Region: 
========================================================

- When defining the region (or window) for the analysis, care must be taken that it is reasonable from the perspective of the process under analysis
- Defining the region in an inappropriate way can easily lead to misleading results

<<<<<<< HEAD
This pattern was defined for a unit-square window. Lets apply the K-function to it:


![plot of chunk unnamed-chunk-15](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-15-1.png)

Based on this we would most likely conclude that the pattern is random.
=======


- Based on this we would most likely conclude that the pattern is random.

***

![plot of chunk unnamed-chunk-15](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-15-1.png)

>>>>>>> 0b233e5f9ff92fd3559e4c4aa39ba26d715bb9fe

Defining a Region Contd. 
========================================================

Lets now replace the unit-square window by a much larger window:


![plot of chunk unnamed-chunk-17](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-17-1.png)

The point pattern now looks clustered

Edge Effects 
========================================================
<<<<<<< HEAD
- If at all possible, the region should be selected in such a way that it is consistent with the underlying process. This is not always possible, either because the underlying process is not known, or because of limitations in data collection capabilities. 
=======
- the region should be selected in such a way that it is consistent with the underlying process. This is not always possible. 
>>>>>>> 0b233e5f9ff92fd3559e4c4aa39ba26d715bb9fe
- When this is the case, it is necessary to define a boundary that does not correspond necessarily with the extent of the process of interest
- When the extent of the process exceeds the window used in the analysis, the point pattern is observed only partially, and it is possible that the information of the location of events beyond the boundary may introduce some bias

Edge Effects Contd. 
==========================================================
<<<<<<< HEAD
Corrections are available in `spatstat` to deal with the possibility of edge effects. So far, we have used the argument `correction = "none"` when applying the functions. The following alternative corrections are implemented: "none", "rs", "km", "cs" and "best". Alternatively `correction = "all"` selects all options.
=======
So far, we have used the argument `correction = "none"` when applying the functions. The following alternative corrections are implemented: "none", "rs", "km", "cs" and "best". Alternatively `correction = "all"` selects all options.
>>>>>>> 0b233e5f9ff92fd3559e4c4aa39ba26d715bb9fe

These corrections are variations of weighting schemes. In other words, the statistic is weighted to give an unbiased estimator.

![plot of chunk unnamed-chunk-18](16-Point-Pattern-Analysis-V-Slides-figure/unnamed-chunk-18-1.png)


Sample Point Patterns
========================================================
- A _sampled_ point pattern, on the other hand, is a pattern where not all events have been recorded
- The bias introduced by sampled point patterns can be extremely serious, because the findings depend heavily of the observations that were recorded as well as those that were not recorded
- Clustered events could easily give the impression of a dispersed pattern, depending on what was observed.
- There are no good solutions to bias introduced by sampled point patterns