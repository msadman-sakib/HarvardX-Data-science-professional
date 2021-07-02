Section 3 - 1.1 Discreet Probability
================

First, set the seed. This is very important to reproduce the results in
this markdown.

``` r
set.seed(1986, sample.kind="Rounding")
```

    ## Warning in set.seed(1986, sample.kind = "Rounding"): non-uniform 'Rounding'
    ## sampler used

# 1. we can use `mean()` function to calculate probabilities

For example, say we have 2 red and 3 blue beads in an urn.

``` r
beads <- rep(c("red", "blue"), times = c(2,3))
beads
```

    ## [1] "red"  "red"  "blue" "blue" "blue"

*Q: What is the probability to pick out blue beads?*

``` r
mean(beads == "blue")
```

    ## [1] 0.6

Therefore, mean() of a logical vector(beads == “blue”) is giving out the
probability of picking up a blue bead from the urn.

### Assessment:

**Probability of cyan**

1- One ball will be drawn at random from a box containing: 3 cyan balls,
5 magenta balls, and 7 yellow balls. Calculate probability of picking
and not picking cyan balls.

``` r
beads <- rep(c("cyan", "magenta", "yellow"), times = c(3,5,7))
beads
```

    ##  [1] "cyan"    "cyan"    "cyan"    "magenta" "magenta" "magenta" "magenta"
    ##  [8] "magenta" "yellow"  "yellow"  "yellow"  "yellow"  "yellow"  "yellow" 
    ## [15] "yellow"

``` r
A = mean(beads =="cyan")
B = mean(beads !="cyan")
paste0("probabiliy of picking cyan:", A)
```

    ## [1] "probabiliy of picking cyan:0.2"

``` r
paste0("probability of not picking cyan:", B)
```

    ## [1] "probability of not picking cyan:0.8"

2- Instead of taking just one draw, consider taking two draws. You take
the second draw without returning the first draw to the box.

We call this **sampling without replacement**. What is the probability
that the first draw is cyan and that the second draw is not cyan?

*A:* need to multiply correctly of those two probabilities above.

``` r
first.draw.cyan = 3/(3+5+7)
second.draw.not.cyan = 1 - (2/(2+5+7))
probability = first.draw.cyan * second.draw.not.cyan
paste0("probability (without replacement):",probability)
```

    ## [1] "probability (without replacement):0.171428571428571"

3- Now repeat the experiment, but this time, after taking the first draw
and recording the color, return it back to the box and shake the box. We
call this sampling with replacement.

What is the probability that the first draw is cyan and that the second
draw is not cyan?

``` r
first.draw.cyan = 3/(3+5+7)
second.draw.not.cyan = 1 - (3/(3+5+7))
probability = first.draw.cyan * second.draw.not.cyan
paste0("probability (with replacement):",probability)
```

    ## [1] "probability (with replacement):0.16"

After this, did similar exercise on Datacamp.
