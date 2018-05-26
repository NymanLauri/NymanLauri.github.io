---
layout: post
title:  "The Very First Post"
date:   2018-05-26
---

Greetings!

This is my first blog post for GSoC. First, I’ll briefly tell you about what I am planning on doing for my GSoC project.

My project concerns the Julia language. I will be implementing an eigenvalue problem solver for sparse matrices in Julia. During the GSoC program, my goal is to create a drop-in replacement for the current `eigs` function in pure Julia. The focus will be on nonsymmetric matrices, but if there is time, the implementation could be extended to cover symmetric matrices as well. As a part of this project, I will provide benchmarks comparing the performance of the new implementation of `eigs` versus the ARPACK’s implementation of `eigs` that is currently in use. The aim is to get this new method into the package `IterativeSolvers.jl`.

The project has started out quite nicely. I have worked on haampie's repository [`IRAM.jl`](https://github.com/haampie/IRAM.jl). The plan for the first week was to study the Implicitly Restarted Arnoldi Method and then start implementing it. Thus far, I have implemented a method `qr!` that computes the QR decomposition of a Hessenberg matrix using Givens rotations, and I’ve been working on getting the shifted QR algorithm to work with Givens rotations (currently named `restarted_arnoldi_2`). You can find my latest commits [here](https://github.com/NymanLauri/IRAM.jl/commits/restart-with-criterion).

I’ve had some school work to work on for these past two weeks, but I have managed to make modest progress with this coding project as well. I will keep you updated about my future progress. 

Until next time!
