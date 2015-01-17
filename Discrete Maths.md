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
