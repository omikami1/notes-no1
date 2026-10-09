```tikz
\usepackage{circuitikz}
\begin{document}
\begin{circuitikz}[american]
    \node[nand port] (and1) at (0,0) {};
    \node[or port] (or1) at (2,0) {};
    \draw (and1.out) -- (or1.in 1);
    \draw (or1.out) -- ++(1,0);
\end{circuitikz}
\end{document}
```