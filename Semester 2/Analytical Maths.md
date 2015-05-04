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

**Rank**  
The rank of a matrix is a number relating to any matrix. The rank of A is the largest number of linearly independent rows of A.  
The rank of an upper triangular matrix is zero.  
The rank of a matrix in row echelon form is the number of non-zero rows.
