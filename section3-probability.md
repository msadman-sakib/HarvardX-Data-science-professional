Section 3 - 1.1 Discreet Probability
================
M Sadman Sakib

First, set the seed. This is very important to reproduce the results in
this markdown.

``` r
set.seed(1986, sample.kind="Rounding")
```

    ## Warning in set.seed(1986, sample.kind = "Rounding"): non-uniform 'Rounding'
    ## sampler used

# We can use `mean()` function to calculate probabilities

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

Bonus:

-   `prop.table()` returns proportions.

# **Now, Combinations and Permutations**

## Introducing paste() and expand.grid()

``` r
# joining strings with paste
number <- "Three"
suit <- "Hearts"
paste(number, suit)
```

    ## [1] "Three Hearts"

``` r
# joining vectors element-wise with paste
paste(letters[1:5], as.character(1:5))
```

    ## [1] "a 1" "b 2" "c 3" "d 4" "e 5"

``` r
# generating combinations of 2 vectors with expand.grid
expand.grid(pants = c("blue", "black"), shirt = c("white", "grey", "plaid"))
```

    ##   pants shirt
    ## 1  blue white
    ## 2 black white
    ## 3  blue  grey
    ## 4 black  grey
    ## 5  blue plaid
    ## 6 black plaid

## Generating a deck of cards

``` r
suits <- c("Diamonds", "Clubs", "Hearts", "Spades")
numbers <- c("Ace", "Deuce", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King")
deck <- expand.grid(number = numbers, suit = suits)
deck <- paste(deck$number, deck$suit)

# probability of drawing a king
kings <- paste("King", suits)
mean(deck %in% kings)
```

    ## [1] 0.07692308

\#\#Permutations and combinations

``` r
library(gtools)
permutations(5,2)    # ways to choose 2 numbers in order from 1:5
```

    ##       [,1] [,2]
    ##  [1,]    1    2
    ##  [2,]    1    3
    ##  [3,]    1    4
    ##  [4,]    1    5
    ##  [5,]    2    1
    ##  [6,]    2    3
    ##  [7,]    2    4
    ##  [8,]    2    5
    ##  [9,]    3    1
    ## [10,]    3    2
    ## [11,]    3    4
    ## [12,]    3    5
    ## [13,]    4    1
    ## [14,]    4    2
    ## [15,]    4    3
    ## [16,]    4    5
    ## [17,]    5    1
    ## [18,]    5    2
    ## [19,]    5    3
    ## [20,]    5    4

``` r
all_phone_numbers <- permutations(10, 7, v = 0:9)
n <- nrow(all_phone_numbers)
index <- sample(n, 5)
all_phone_numbers[index,]
```

    ##      [,1] [,2] [,3] [,4] [,5] [,6] [,7]
    ## [1,]    4    8    2    7    0    3    1
    ## [2,]    2    0    8    7    3    4    6
    ## [3,]    6    0    9    3    7    2    1
    ## [4,]    3    2    8    4    7    1    6
    ## [5,]    5    9    8    7    3    6    0

``` r
permutations(3,2)    # order matters
```

    ##      [,1] [,2]
    ## [1,]    1    2
    ## [2,]    1    3
    ## [3,]    2    1
    ## [4,]    2    3
    ## [5,]    3    1
    ## [6,]    3    2

``` r
combinations(3,2)    # order does not matter
```

    ##      [,1] [,2]
    ## [1,]    1    2
    ## [2,]    1    3
    ## [3,]    2    3

## Probability of drawing a second king given that one king is drawn

``` r
hands <- permutations(52,2, v = deck)
first_card <- hands[,1]
second_card <- hands[,2]
sum(first_card %in% kings)
```

    ## [1] 204

``` r
sum(first_card %in% kings & second_card %in% kings) / sum(first_card %in% kings)
```

    ## [1] 0.05882353

## Probability of a natural 21 in blackjack

``` r
aces <- paste("Ace", suits)
facecard <- c("King", "Queen", "Jack", "Ten")
facecard <- expand.grid(number = facecard, suit = suits)
facecard <- paste(facecard$number, facecard$suit)

hands <- combinations(52, 2, v=deck) # all possible hands

# probability of a natural 21 given that the ace is listed first in `combinations`
mean(hands[,1] %in% aces & hands[,2] %in% facecard)
```

    ## [1] 0.04826546

``` r
# probability of a natural 21 checking for both ace first and ace second
mean((hands[,1] %in% aces & hands[,2] %in% facecard)|(hands[,2] %in% aces & hands[,1] %in% facecard))
```

    ## [1] 0.04826546

## Monte Carlo simulation of natural 21 in blackjack

``` r
# code for one hand of blackjack
hand <- sample(deck, 2)
hand
```

    ## [1] "Nine Hearts"   "Nine Diamonds"

``` r
# code for B=10,000 hands of blackjack
B <- 10000
results <- replicate(B, {
    hand <- sample(deck, 2)
    (hand[1] %in% aces & hand[2] %in% facecard) | (hand[2] %in% aces & hand[1] %in% facecard)
})
mean(results)
```

    ## [1] 0.0464
