= FairBasketball

== Motivation

Currently, certain shots in basketball are considered significantly less efficient than others.
E.g. shooting the furthest 2 pointer possible is the worst shot one can attempt.

This has led to a concentration of skills in the league, such as either being a 3-point expert or a paint (close to basket) expert. Making the game less varied makes it less interesting.

The purpose of this paper is to demonstrate new scoring rules that make every shot potentially equally efficient.

== Probabilities

Given any spot on the court, there is a probability of making the shot from there, which decreases as the distance to the hoop increases and decreases as the angle to the backboard increases.

The decrease via distance comes from increasing accumulated error as the ball flies longer.
The decrease via the angle comes from the decreased chances of using reflections from the backboard (purposefully or not) to make the basket.

Let's assume we have the probability given as

$ p(d, alpha) $

with

$ d_1 <= d_2 => p(d_2, alpha) <= p(d_1, alpha) $

and

$ alpha_1 <= alpha_2 => p(d, alpha_1) <= p(d, alpha_2) $

$alpha$ is measured as $0$ when the ball flies orthogonal to the backboard, increasing upto a quarter circle ($pi/2$) from the corner.

Left and right sides of the court will be considered symmetric, i.e. equal in probability.

Note that $p$ is of course skill dependent. All the obvervations and conclusions in this paper remain valid per skill level or considered for an average skill level or a maximal skill level.

== Fair = Equal Expectation

The expected value is calculated as the probability of making a shot times the _score_ $s$ from the shot:

$ E(d, alpha) = p(d, alpha) * S(d, alpha) $

Currently, $S$ is either 2 (inside the 3-point-line) or 3 (outside the 3-point-line), which makes $E$ variying across the court.

The problem we are trying to solve is that $E$ is decreases as we get further from the hoop until it suddenly jumps right after the 3-point-line and then decreases further. Which, rationally, leads to "dead zones" for shooting in basketball.

We want $E == E(d, alpha)$ to be constant across the court. We can arbitrarily set as $E == 1$

This is achieved by setting $S$ as follows:

$ S(d, alpha) = 1 / p(d, alpha) $

This means that a shot garners more points the more difficult it is.

== Data

To estimate $p$, we ideally want to have as much data as possible. E.g. choose a league and for every every shot attempt, record it's position ($d$, $alpha$) and whether it was successful or not.

== Modelling

From the data gathered, we could model $p$ as some kind of smooth function (polynomial, exponential, ...) to make calculations simpler.

== Technology

This idea might have occurred to people before. It is however very impractical to access $S$, the points rewarded to a successful shot, as it depends on the exact location of the shot. This would disrupt the game too much to be practical.

This idea can now be implemented using image object detection algorithms. A real time video feed from at least two sources, i.e. two cameras pointing at a court, can be run through object detection algorithms to find notice that a ball went through the hoop (successful shot) and rewind to find the player (and its position) that shot the ball.

$p$ and $S$ is be thus calculated immediately.

We could in fact show players a real time estimate of $S$ IF it made a shot from where the player with ball possession is standing on a live board.

== Implementation

The presented scoring rule could be easily implemented for virtual basketball (e.g. video games). A testing of a non-virtual version would require some committment from a team or league.
