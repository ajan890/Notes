# Week 1

## About the course

Instructor:   Jun Yin <br>
              Office: 6172 MS <br>
              Email: jyin@math.ucla.edu <br>
              OH: T/R 8-10pm Zoom <br>
              Midterm: Feb 10 <br>
              Final: March 20, 2023 8-11AM <br>
              
Find everything else in the syllabus.

<strong>Homework Grading:</strong>  The final grade used for the Homework category is determined by the formula: <br>

<img src="https://latex.codecogs.com/svg.image?{\color{Red}\text{Final&space;HW}&space;=&space;\text{min}(\text{HW},&space;1.5&space;\times&space;\text{Final&space;Exam})&space;}" title="https://latex.codecogs.com/svg.image?{\color{Red}\text{Final HW} = \text{min}(\text{HW}, 1.5 \times \text{Final Exam}) }" />

<strong>Ex. </strong> If the average homework grade is 92%, but the final exam grade is 60%, then the final homework grade used for the grade calculation will be 90%. <br>

<strong>Oral Exam </strong> If you do not attend class frequently, you would be required to take an oral exam (5-10 minutes) before the final.

## Probability

Consider the example questions: What is the probability that your first child is male? Or, what is the probability that it rains tomorrow? <br>

These are examples of <strong> applied probability</strong>, or cases of probability that apply to something in the real world.  For example, the first question may consider probabilities of genetic defects, and the second question may consider weather patterns from previous years.  This class does <strong> not </strong> cover applied probability.  Instead, it covers probability theory, or <em>pure probability</em>.  An example of this would be: If the chance of raining tomorrow is 20%, what is the chance of it not raining tomorrow? <br>

## Sets and Set Notation

A <strong>set</strong> is simply a group of objects.  <br>
* They are denoted using curly braces {}. <br>
* The set that contains the numbers 2 and 3 is {2, 3}. <br>
* {1, 2, 3, 4, 5} is the set that contains integers between 1 and 5 inclusive. <br>

### Symbols
  * ℕ - Natural Numbers (integers greater than 0) <br>
  * ℤ - Integers <br>
  * ℝ - Real Numbers <br>
  * Q - Rational Numbers <br>
  * ∈ - "In the set of" <br>
  * ⊂ - "Is a subset of," means the same as ⊆, but only ⊂ is used in this course.<br>
  * U - Union (The set that contains all the elements in at least one of the sets)<br>
  * ∩ - Intersection (The set that contains all the elements in both sets)<br>
  * A<sup>C</sup> - Complement (The set that contains all elements not in A)<br>
  * Φ - Empty Set (The set that contains nothing)<br>

### DeMorgan's Law
  > (A U B)<sup>C</sup> = A<sup>C</sup> ∩ B<sup>C</sup><br>
  > (A ∩ B)<sup>C</sup> = A<sup>C</sup> U B<sup>C</sup><br>

### Set Builder
* {x | x > 5, x ∈ ℕ} is the set that contains all integers greater than 5. <br>
  * This can also be written as {x ∈ ℕ : x > 5} <br>  (colon and line mean the same thing)

* {x + y : x is a prime & y is a prime} is the set of all numbers that can be written as the sum of two primes. <br>

### Sample Space

The <strong>Sample Space</strong> is a <strong>set</strong> which contains every possible outcome of an experiment.  It is not a <em>space</em>, it's just a name.<br>
* Sample space is denoted by "S".<br>
* Ex.<br>
  > For a coin toss, the sample space would be {Heads, Tails}.<br>
  > The sample space for two coin tosses would be {(H, H), (H, T), (T, H), (T, T)}<br>
  > The sample space for two dice throws would be {(1, 1), (1, 2), (1, 3), (1, 4), (1, 5), (1, 6), (2, 1), ...}, or better, written as {(a, b) : a, b ∈ \[\[1, 6]]}<br>
  > The two dice throws can also be written as S = \[\[1, 6]]<sup>2</sup><br>

### Probability in Sets

<strong>ℙ(A)</strong> denotes the probability that an outcome is in the subset.
* Suppose you toss a die.  S = \[\[1, 6]].
  * ℙ(S) = 1, since all outcomes from the dice toss would be a number in S.
  * ℙ(Φ) = 0, since none of the outcomes are in the empty set.
  * ℙ({2, 3, 5, 6}) = 0.66
          
