# COMPSCI 4TB3 - Preconditions, Postconditions, Invariants


April 16th 2022

This project aims to extend the P0 language and add Preconditions, Postconditions and Invariants, ie., Hoare logic to it.

## Project Plan

### Group Members

This group consists of the following members: 

* Ankit Kapoor
* Jennifer Cheng (400118301)
* Shivam Taneja (400160537)

### Project Description

**Problem Description**

The task is to add procedure preconditions, procedure postconditions, and loop invariants to P0 in the style of Eiffel. 

A precondition ("require") is checked at procedure entry, a postcondition ("ensure") is checked at procedure exit, and a loop invariant is checked each time the loop body is entered and finished. In case a precondition, postcondition, or invariant does not hold, the program will be exited with appropriate error output. 

```
procedure quotrem(x, y: integer) → (q, r: integer)
    require x > 0 and y > 0
    ensure q × y + r = x and r < y
    q, r := 0, x
    invariant q × y + r = x ∧ r ≥ y
    while r ≥ y do
        r, q := r - y, q + 1
```

**Testing Implementation**

Testing this implementation would require that the following conditions are met for every execution of the program:

* Preconditions are met at each procedure entry - indicated with a `require` keyword
* Postconditions are met at each procedure exit - indicated with an `ensure` keyword
* Loop invariants are held throughout the execution of the loop - indicated with an `invariant` keyword

If at any point in time, the above conditions are violated, we are most likely going to exit the program. Alternate ways of handling
condition violations like throwing exceptions may be added in future implementations, but isn't a priority currently.

Concrete test cases would involve:

* Comparison of code with invariants and without to see how it impacts performance (efficiency) for similar code.
* Negative test cases to document behaviour when invariants are not held
* Edge cases such as no preconditions and/or postconditions and/or loop variants are applied.

### Resources

The following outlines the resources we plan to leverage for this project:
* [Programming by Contract - Eiffel](http://www.cs.unc.edu/~stotts/COMP204/contract.html)
* [Object Oriented Software Construction](https://en.wikipedia.org/wiki/Object-Oriented_Software_Construction)
* [Documentation of Eiffel](https://www.eiffel.org/)

The above resources refer to Bertrand Meyer, and his creation of the `Eiffel` programming language which introduced the above concept.

* [Program Logic for Certified Compilers](https://vst.cs.princeton.edu/download/PLCC-to-chapter-3.pdf) More information on Hoare logic
* [Bounds Checking](https://github.com/lambertjamesd/zen-lang/blob/master/doc/boundschecking.md)
Bounds checking normalizes all comparison equations so all ways of writing an equation look the same to the compiler.
* [The Design and Implementation of a Certifying Compiler](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.42.7948&rep=rep1&type=pdf) A design of a compiler that translates programs written in a variant of C, as well as a certifier for the compiler



### Division of Work
The following outlines how we plan on dividing up our work. We have 3 total team-members, and have allocated work to ensure everyone contributes an equal amount.


