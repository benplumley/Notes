#CM10197 - Analytical Mathematics
##Prof Nicolai Vorobjov

**Determinant**  
The determinant is a number associated with a matrix. For a 2 by 2 matrix, it is calculated by subtracting the product of the trailing diagonal from the product of the leading diagonal.

**Cramer's Rule**  
Replacing the nth column of a matrix with the result vector and dividing the determinant of that matrix by the determinant of the original matrix gives a solution for the nth variable. Repeating this for all variables gives a solution to the system.

**Non-singularity**  
A square matrix A is called non-singular if there exists an inverse matrix A^-1 such that A*A^-1 is equal to the identity matrix. A system of equations AX = b can be solved by premulitplying both sides by A^-1.

**Inductive Definition of Determinant**  
If A is an square n*n matrix, let Aij mean the matrix obtained by removing row i and column j from A. If n = 1, A contains only one element, its determinant. Assume that n > 1 and we have defined the determinant for square matrices of size n-1. Fix i between 1 and n. Then ![](http://i.gyazo.com/eab194fc531873d8879ab41f801b8d5d.png)
