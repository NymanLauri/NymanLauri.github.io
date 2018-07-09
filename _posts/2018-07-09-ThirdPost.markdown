---
layout: post
title:  "Week 9 Blog Post"
date:   2018-07-09
---

We are 8 weeks into the coding period and the project is starting to look good! The current state of the project can be found [here](https://github.com/NymanLauri/IRAM.jl). 

There have been some changes in the project outline as well. Let’s start with the project outline.

# Project outline

At the time that I posted the previous blog post, the project outline looked as follows: 

1) IRAM for real and complex arithmetics with QR iterations through Givens rotations. __DONE__

2) Finding multiple eigenpairs which requires locking of converged Ritz vectors. __DONE__

3) Adding search targets for eigenvalues.

4) Adding support for generalized eigenvalue problems.

Since the last blog post, there have been changes in the project outline. Namely, implementing search targets has been removed. This is because a practical design is to have the user invert the problem so that the largest eigenvalue is the desired one. Hence, instead of implementing search targets, the time interval July 1 - 14 in the project schedule is spent on making the implementation fully native which includes native Julia implementations for the `schurfact!` call and the `eigvals` call. Furthermore, JuliaCon occupies the week 6 August - 12 August which was not taken into account in the original project schedule. Hence, the project  should be paced so that it is done by 6 August. Current schedule is therefore:

__1 - 14 July:__ Make implementation fully native.

__15 July - 6 August:__ Add support for generalized eigenvalue problems, write documentation, tests and benchmarking.

# Progress since last post

__Fully native code__

The `eigvals` call has been made fully native. This native implementation currently assumes that the matrix is in upper triangular form, which requires that the `schurfact!` call be made fully native as well. In making these fully native, an implementation for [`eigvals!`](https://github.com/andreasnoack/LinearAlgebra.jl/blob/master/src/eigenGeneral.jl#L227) and [`schurfact!`](https://github.com/andreasnoack/LinearAlgebra.jl/blob/master/src/eigenGeneral.jl#L80) by Andreas Noack have been consulted. The Schur factorization works with Wilkinson single and double shifts. These native Julia versions are located in [`eigvals.jl`](https://github.com/NymanLauri/IRAM.jl/blob/master/src/eigvals.jl). Currently, there are some bugs with with the double shift ([`double_shift_schur!`](https://github.com/NymanLauri/IRAM.jl/blob/master/src/eigvals.jl#L293)). Fixing these is the next step.

__Double shift__

In `implicit_restart!`, the arnoldi procedure is restarted by shrinking the Krylov subspace by shifting away unwanted eigenvalues. If our matrix is real and the eigenvalue we want to shift happens to be complex, then we can combine two shifts that are the unwanted eigenvalue and its complex conjugate in order to stay in real arithmetic. This is implemented in [`double_shift!`](https://github.com/NymanLauri/IRAM.jl/blob/master/src/implicit_restart.jl#L110).

Instead of using Householder reflections in `double_shift!`, two Givens rotations are combined to yield the same effect. 

__Implicit QR steps__

The QR steps in `double_shift!` and `single_shift!` are now done implicitly. This was done to make it easier to implement double shift for conjugate eigenvalues. With implicit QR shifts, both single and double shifts are implemented with “bulge chasing” and hence work in a similar manner.

__Using partial Schur decomposition__

To improve stability, the implementation now uses partial schur decomposition, and brings the locked part of the Hessenberg matrix into upper triangular form. The function [`restarted_arnoldi`](https://github.com/NymanLauri/IRAM.jl/blob/master/src/run.jl#L5) currently returns the partial Schur decomposition of the converged part of the Hessenberg matrix from which the eigenvalues and eigenvectors of the original matrix can be computed.

# Next steps

The next steps in this projects are:

* Finish making the implementation fully native.

* Add support for generalized eigenvalue problems.

After these, the project is nearly finished!
