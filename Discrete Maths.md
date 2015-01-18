#CM10196 - Discrete Mathematics
##Prof Nicolai Vorobjov

**1.1: Propositions**  
A proposition is a statement which is assumed to be either true or false. The content of the statement is not important; only its truth value.

**1.2: Logical Connectives**  
Propositions can be combined into more complex statements using logical connectives.

*Conjunction* is equivalent to a logical AND.

*Disjunction* is equivalent to a logical OR.

*Implication* is a logical if - then -, meaning it is true unless 1 implies 0.

*Negation* is a logical NOT, flipping a truth value to the opposite value.

**1.3: Boolean Formulae**  
Propositions are represented by variables and connected together by logical connectives to form *Boolean formulae*. The entire formula has a truth value which is calculated by applying the connectives to the truth values of the propositions that make it up.

**1.4: Tautologies**  
A boolean formula is called a *tautology* if the value of the formula is true for any combination of truth values in its propositions. It is represented by the identically equal to sign, meaning implies and is implied by.

**2.1: Commutativity**  
Conjunction and disjunction are *commutative*. A && B is equivalent to B && A, and A || B is equivalent to B || A.

**2.2: Associativity**  
Conjunction and disjunction are *associative*. (A && B) && C is equivalent to A && (B && C), and (A || B) || C is equivalent to A || (B || C).

**2.3: Distributivity**  
Conjunction and disjunction are *distributive*. (A && (B || C)) is equivalent to ((A && B) || (A && C)), and (A || (B && C)) is equivalent to ((A || B) && (A || C)).

**2.4: De Morgan's Laws**  
*De Morgan's Laws* state that ¬(X && Y) = (¬X || ¬Y), and ¬(X || Y) = (¬X && ¬Y).

**2.5: Laws of Logic**  
- X || ¬X  
- ¬¬X = X  
- ¬(X && ¬X)  
- ((¬X -> Y) && (¬X -> ¬Y)) -> X  
- (X -> Y) = (¬X || Y)  

Using these laws, commutativity, associativity, distributivity and de Morgan's, it is possible to represent any Boolean formula using only ¬ and one other connective.

**2.6: Direct and Inverse Theorems**  
Many theorems can be described using implication A -> B. This is the *direct theorem*. The proposition B -> A is known as the *inverse theorem*, and is not necessarily true if the direct theorem is true. The proposition ¬A -> ¬B is the *opposite theorem*. The proposition ¬B -> ¬A is the *opposite to inverse theorem*, and is true if and only if the direct theorem is true.

**2.7: Disjunctive Normal Form**  
A *literal* is a single variable, or a single variable negated with ¬. A *conjunctive term* is a series of literals joined by conjunctions. A formula is in *disjunctive normal form* if it is a string of conjunctive term joined by disjunctions, for example:  
(¬X && ¬Y) || (¬X && Y) || X

Any Boolean formula has an equivalent DNF formula.

**2.8: Conjunctive Normal Form**  
A *disjunctive term* is a string of literals joined by disjunctions, and a formula is in *conjunctive normal form* if it is a string of disjunctive terms joined by conjunctions, for example:  
(¬X || ¬Y) && (¬X || Y) && X

Any Boolean formula has an equivalent CNF formula.

**3.1: Sets**  
A set is a group of elements, often numbers. Useful sets include:
- **Z**, the integers  
- **R**, the real numbers  
- **Q**, the rational numbers  
- **N**, the natural numbers  

These sets are infinite. Sets can also be finite, in which case they can be defined by listing their elements between curly braces. A set can also contain no elements; this is the empty set.

**3.2: The Universal Quantifier**  
The *universal quantifier* is shorthand for saying "for all". It represents a string of conjunctions, meaning the whole proposition is true if and only if it is true for every member of the set.

**3.3: The Existential Quantifier**  
The *existential quantifier* is shorthand for saying "there exists". It represents a string of disjunctions, meaning the whole proposition is true if it is true for at least one member of the set.

**3.4: Universal and Existential Quantifiers in the same formula**  
A predicate containing several variables can be turned into a proposition (ie given a truth value) by adding the same number of quantifiers. These must be evaluated from right to left, so the rightmost quantifier is inside the most brackets in the expanded form and the leftmost is outside the brackets.

**3.5: Negation of Quantifiers**  
Because quantifiers represent strings of connectives, de Morgan's laws still apply. To negate a quantifier, the negation is moved to before the predicate and all quantifiers are flipped to the other quantifier.

**4.1: Equal Sets and Subsets**  
Two sets are *equal* if they contain the same elements. Specifically, A = B if A c B and B c A, where c means "is a subset of".

**4.2: Union of sets**  
The *union* of two sets is the set of all elements that appear in one or the other, and is written as A u B.

**4.3: Intersection of sets**  
The *intersection* of two sets is the set of all elements that appear in both sets, and is written as A n B.

**4.4: Properties of union and intersection**  
As with the logical connectives, union and intersection are commutative, associative and distributive.

**4.5: Difference of sets**  
The *difference* of two sets A and B is written A \ B, meaning the set of all things in A which are not in B. The *complement* of a set is the difference between the universe (U) and the set. Hence the complement of A is U \ A, which is written as A'. De Morgan's laws apply to complement in the same way they applied to negation.

**4.6: Cartesian Product of sets**  
The *cartesian product* of sets A and B is written as A x B, and consists of all pairs of elements where the first element is from A and the second from B.

**4.7: Cardinality**  
The *cardinality* of a set is the number of elements that set contains. It is written as |A|.

|A u B| = |A| + |B| - |A n B|

|A x B| = |A| * |B|

**4.8: Sets of sets**  
Sets can also contain sets as their elements, and this is true recursively. A set containing the empty set is not empty, its cardinality is 1.

**4.9: Power set**  
The *power set* of A is the set of all subsets of A, which includes the empty set and A. It is written as 2^A. The cardinality of the power set 2^A is 2^|A|.

**5.1: Proof by induction of a sum**  
The *base case* is typically the case where the sum starts (ie 1 in a sum from 1 <= n). By substituting 1 in both sides, it can be proved that the formula is true for the base case.

The *inductive hypothesis* is the replacement of n with k, and an assumption that the formula is true for n=k.

The *inductive step* is the replacement of n = k+1. The left hand side is calculated, using the assumed truth from the hypothesis. This is simplified until it can be written as the right hand side with n = k+1. The formula is true for n=1, and proven true for n=k+1 if assumed true for n=k, therefore it is true for all n by induction.

**5.2: Proof by induction of divisiblity**  
The method is the same as for a sum.

**5.3: Maps**  
A *map* from A to B is a rule that, when given one element from A, returns one element from B. All elements from A must give exactly one result from B.

**5.4: Surjective Maps**  
A map is *surjective* if all elements in B are mapped to, ie all elements in B have a preimage.

**5.5: Injective Maps**  
A map is *surjective* if no two arguments in A map to the same image in B - every element in B has a unique preimage.

**5.6: Bijective and Inverse Maps**  
A map is *bijective* if it is both surjective and injective. This requires there to be the same number of elements in A and B.

The *inverse* of a map is the map which takes the images as arguments and returns the correct preimages. Only bijective maps can have an inverse.

**6.1: Composition of Maps**  
The *composition* of maps *f* and *g* is written as *g* o *f*, and means g's transformation applied to f's transformation of an input. *g* o *f*(x) = g(f(x)).

The composition of two injective maps is injective, and likewise with surjective and bijective maps.

**6.2: Inverse and Identity Maps**  
The composition of a map and its inverse is the *identity map*. The identity map's output for any input is that input.

**6.3: Map as a Subset of Cartesian Product**  
A map f from A to B is a subset of A x B. For any input in A there is a unique output in B such that (input, output) is in f.

**6.4: Relations**  
A *relation* is the subset of the cartesian product of the domain and range. It is the same as a map, with the condition removed that each image is unique. For x in A and y in B, the elements x and y can be said to be in the relation by writing x*y.

It is *reflexive* if x*x is in the relation.

It is *symmetric* if x*y implies y*x.

It is *transitive* if x*y and y*z implies x*z.

**6.5: Equivalence Relations**  


**6.6: Partitions into Equivalence Classes**  


**7.1: Rational Numbers**  


**7.2: Arithmetic Operations on Rational Numbers**  


**7.3: Cauchy Sequences**  


**7.4: Arithmetic of Cauchy Sequences**  


**7.5: Null Sequences**  


**7.6: Equivalence Relations for Cauchy Sequences**  


**8.1: Arithmetic Operations on Real Numbers**  


**8.2: Partial and Total Orders**  


**8.3: Maximal and Minimal Elements**  


**8.4: Strict Partial Order**  


**8.5: Orders on Rational and Real Numbers**  
