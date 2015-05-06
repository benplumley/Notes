#CM10197 - Analytical Mathematics
##Prof Nicolai Vorobjov

**Determinant**  
The determinant is a number associated with a matrix. For a 2 by 2 matrix, it is calculated by subtracting the product of the trailing diagonal from the product of the leading diagonal.

**Cramer's Rule**  
Replacing the nth column of a matrix with the result vector and dividing the determinant of that matrix by the determinant of the original matrix gives a solution for the nth variable. Repeating this for all variables gives a solution to the system.

**Non-singularity**  
A square matrix A is called non-singular if there exists an inverse matrix A^-1 such that A*A^-1 is equal to the identity matrix. A system of equations AX = b can be solved by premulitplying both sides by A^-1.

**Operations on Determinants**  
Transposing a matrix doesn't change its determinant.  
Swapping two rows of a matrix changes the sign of the determinant.  
Multiplying a row by a constant multiplies the determinant by the same constant.  
If one row of a matrix is proportional to another, the determinant is zero.
If one row is multiplied by a constant and added to another row, the determinant doesn't change.

**Inductive Definition of Determinant**  
If A is an square n*n matrix, let Aij mean the matrix obtained by removing row i and column j from A. If n = 1, A contains only one element, its determinant. Assume that n > 1 and we have defined the determinant for square matrices of size n-1. Fix i between 1 and n. Then  
![](http://i.gyazo.com/eab194fc531873d8879ab41f801b8d5d.png)

**Row Echelon Form**  
A matrix is in row echelon form if all rows consisting of only zeroes are at the bottom of the matrix and each row has at least as many leading zeroes as the row above it.

**Guassian Elimination**  
The Gaussian elimination algorithm turns a square matrix into upper triangular form, and a non-square matrix into row echelon form.
1. Put all zero rows to the bottom.  
2. Move the row with the least first zeroes to the top. a_ij is the first non-zero element.  
3. For each non-zero element in column j, by multiplying row i by a constant and adding the rows, make column j all zeroes.  
4. Remove the top row and columns 0 through j. Repeat from step 1 until the matrix has just one element.  
5. Add the removed rows back in. This is now in upper triangular form. Its determinant is the product of the leading diagonal.

A matrix in upper triangular form in a system of equations can be solved easily for the last row, with the result from this substituted into the next row, and so on until all variables have values.

**Linear Dependence**  
A set of row vectors is linearly dependent if there exists a non-zero column vector such that the sum of the products of each row vector with the corresponding column cell is zero. A vector is zero if all of its items are zero.  
If no such column vector exists, the set is linearly independent.  
A set of row vectors is always linearly dependent if one of the vectors is zero.  

**Basis**  
There can only be be n linearly independent vectors in n-dimensional vector space. Any system of n+1 vectors is linearly dependent. A set of n linearly independent vectors in a vector space is called its basis.

The standard basis of n-dimensional real space is the set of n linearly independent row vectors  
![](http://i.gyazo.com/847034963aa2df0ee314be4aac26958c.png)

**Rank**  
The rank of a matrix is a number relating to any matrix. The rank of A is the largest number of linearly independent rows of A.  
The rank of an upper triangular matrix is zero.  
The rank of a matrix in row echelon form is the number of non-zero rows.

**Solving linear systems with Gaussian Elimination**  
To solve a system of linear equations, add the answer vector to the end of the matrix as a new column. Perform the Gaussian elimination algorithm until the matrix is in row echelon form. Take the answer vector back to the other side of the equality. Any rows containing only zeroes at this point can be removed. If a row of the matrix contains all zeroes but that position in the answer vector is not zero, the system has no solutions.

If there aren't enough simultaneous equations to find a unique solution, we can pick arbitrary values for the variables whose values can't be found. This will give a solution, but this is not the only solution. There are infinitely many.

Alternatively, we can keep the unknowns as variables and not give them values at all. The other variables become dependent on them.

**Affine Maps**  
A map from the plane to the plane is called an affine transformation or affine map. This represents a general solution to a system of equations. They can be written in the form X = BY+C. If and only if B is square and non-singular, the map is bijective.

**Spans**  
A span is a straight shape connecting the origin to a point. A span in the plane is written as span{(a, b)} which defines a line passing through (0, 0) and (a, b).

**Calculating a plane from points**  
Given three points in the vector space, (x1, y1, z1), (x2, y2, z2), (x3, y3, z3), the equation of the plane passing through all three is given by  
![](http://i.gyazo.com/64484ada44e6c062b90804120e450128.png)

A straight n-1 dimensional shape in n-dimensional space is known as a hyperplane.

**Intermediate Value Theorem**  
Intermediate value theorem says that a function f is continuous between two points a and b if for all t in the range there exists a c in the domain such that f(c) = t.

**Analytical Functions**  
Analytical functions are infinitely differentiable and can be expanded into a Taylor Series.

**Partial Differentiation**  
To differentiate a function with two variables *f(x, y)* we first fix *x=a* and calculate the gradient with *a* as a constant. Then substitute *a=x*. This is the partial derivative of f.

**Sum of a Series**  
The partial sum of a series, denoted by S_n, is the sum of its first n terms. The sum of the series is the limit of this partial sum as n tends to infinity.

**Convergence**  
If the sum converges, then the series converges to zero. The sum *converges absolutely* if the sum of the absolute values converges.

**Taylor Series**  
If f is an infinitely differentiable function from the interval (a, b) to the real numbers, and x_0 is a real number in (a, b), the Taylor Series of f is given by  
![](http://i.stack.imgur.com/MAMOg.png)

If x_0 is set to zero, the series is called the Maclaurin Series, which is given by this equivalent equation  
![](http://i.gyazo.com/e7061aa5d581fde6fa1c2f071ac015e9.png)

A function is analytic if its Taylor Series converges.

**Eigenvectors and Eigenvalues**  
For a vector x and real number b, Ax = bx is true if x is the eigenvector of A and b is the eigenvalue of A. In other words, for a matrix A there is a vector and a single number such that multiplying A by each gives the same result.

When the matrix transformation A is applied, points on the line through the origin and x stay on that line, and move along it by a factor of b.

**Finding Eigenvectors and Eigenvalues**  
Given concrete values for A, and that Ax - bx = 0  
(A - bI)x = 0 where I is the identity matrix with the same dimensions as A  
|A - bI| = 0 if an eigenvector exists  
Replace A with its values to get a quadratic in b; solve for eigenvalues.

Substitute found eigenvalues into (A - bI)x = 0 to get simultaneous equations in x; solve for eigenvectors.

**Rotation Matrix**  
A rotation matrix is any matrix of the form  
![](http://i.gyazo.com/956c4b4419b31b11a8a79133cfa15b26.png)
