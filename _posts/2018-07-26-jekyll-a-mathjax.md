---
title:    Jekyll a matematické vzorce pomocí MathJax
date:     2018-07-26 8:00:00 +0200
tags:     [o-blogu, mathjax, jekyll]
use_math: true
---
Chcete-li do článků na svém Jekyll blogu psát matematické výrazy
(podobně jako např. v [_LaTeXu_][1]), jedna z přímočarých možností
je zprovoznit si [_MathJax_][2]. Já jsem se řídil primárně podle článku:

- [How to use MathJax in Jekyll generated Github pages _(haixing-hu.github.io)_][3],

nicméně několik detailů jsem musel pozměnit, než mi to začlo fungovat.
Pojďme tedy na to! Nejprve ukázka, jak bude výsledek našeho snažení vypadat:

\begin{equation}
  s(t) = s_0 + \int_{0}^{t} v(t) \text{ } \mathrm{d}t
\end{equation}

[1]: https://cs.wikipedia.org/wiki/LaTeX
[2]: https://www.mathjax.org/
[3]: http://haixing-hu.github.io/programming/2013/09/20/how-to-use-mathjax-in-jekyll-generated-github-pages/
