---
layout: post
title:  "Week 5 Blog Post"
date:   2018-06-13
---

# First words

It has been a while since I wrote the previous blog post, and quite a lot has happened in the meantime. Now, we are 5 weeks into the coding period, so I will walk you through the progress that I have made during this time.

# IRAM for one eigenpair

Last time I posted I was working on the Implicitly Restarted Arnoldi Method that finds one eigenpair, and in particular getting it to work with Givens rotations. This is now done. Currently, you can find the implementation [here](https://github.com/NymanLauri/IRAM.jl/blob/master/src/factorization.jl#L113).


# IRAM for multiple eigenpairs

After finishing the IRAM for finding one eigenpair, the next step was extending this to find multiple eigenpairs through the locking of Ritz vectors ([PR #7](https://github.com/haampie/IRAM.jl/pull/7)). Currently, this is implemented in the method [`restarted_arnoldi.jl`](https://github.com/NymanLauri/IRAM.jl/blob/locked-restart/src/factorization.jl#L145).

# Issues that were encountered

As with any project, there are always some issues along the way. Here I have listed the two largest issues/concerns that both relate to the locking of Ritz vectors:

* Understanding the locking procedure took more time than anticipated. Despite this, I'm still keeping up with the proposed schedule.

* Unwanted Ritz vectors might get locked. Hence, purging still needs to be implemented. Purging refers to the act of removing unwanted Ritz vectors from the locked Ritz vectors. This is not yet implemented.

# A quick overview of the current state of the project

1) IRAM for real and complex arithmetics with QR iterations through Givens rotations. __DONE__

2) Finding multiple eigenpairs which requires locking of converged Ritz vectors. __DONE__

3) Adding search targets for eigenvalues.

4) Adding support for generalized eigenvalue problems.

__Stretch goal:__ Finding eigenvalues of symmetric matrices using Lanczos method.

# Next steps

* Adding search targets for eigenvalues (e.g. largest magnitude, largest real part, smallest imaginary part).

* Currently, the Schur form of the locked part of the Hessenberg matrix during the IRA-procedure is computed calling `schur`. This seems a bit excessive, and I will try to get rid of this function call by incorporating the computation of the Schur form into the IRA-procedure itself.

I'll keep you updated about my future progress. Until next time!
