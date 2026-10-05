# Fibonacci Formula -- Using matrices and eigenvectors

The method here is to write

$$
\begin{pmatrix}
F_{n+1}\\
F_{n+2}
\end{pmatrix}
= 
\begin{pmatrix}
0 & 1\\
1 & 1
\end{pmatrix}
\begin{pmatrix}
F_n\\
F_{n+1}
\end{pmatrix}
$$

Then find two eigenvectors and eigenvalues of $A = \begin{pmatrix} 0 & 1\\ 1 & 1\end{pmatrix}$.  Then $A^n\begin{pmatrix}1\\1\end{pmatrix} = c_1 \phi^n \vec{v}_1 + c_2 \psi^n \vec{v}_2$.
