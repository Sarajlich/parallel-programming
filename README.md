# Muhamed-Sarajlic-Parallel-Programming-Assignments

Code
    - implemented from book chapter Long Double, Kahan, Knuth and Pairwise methods
    - in main.c i added generic test functions for each summation method (Long Double, Kahan, Knuth, Paiwise) so we can see the differecne and compare methods
    - tests different algorithms for summing large arrays of numbers
    - in the makefile I added "-lm" to allow use of powe and log2

Why some techniques work better
    - Long Double --> reduces error but still limited
    - Pairwise --> adds number in tree structure, reduces error growth
    - Kahan --> tracking error in correction variable, improves accuracy a lot with small overhead
    - Knuth --> similar to Kahan, but even more accurate

Global sum problem in in parallelization
    - large sums are computed by dividing the array among processors, then results are combined
    - floating point arithmetics are not associative (x + y) + z != x + (y + z)
    - problem is that parallel calculation is changing the order of additions, this means that result may not match true sum
    - the problem gets worse as the problem size gets larger because the addition of the last value becomes a smaller and smaller part of the overall sum
    - even worst case is adding floating-poin numbers that are almost identical but with different signs (subtracting two nearly equal numbers leaves only few digits, are the rest is filled with numerical noise, making the resuls inaccurate)
    