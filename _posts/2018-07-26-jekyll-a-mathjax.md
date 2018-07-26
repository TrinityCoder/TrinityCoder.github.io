---
title:    Jekyll a matematické vzorce pomocí MathJax
date:     2018-07-26 13:30:00 +0200
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

Přičemž zdrojový kód této rovnice je:

```tex
\begin{equation}
  s(t) = s_0 + \int_{0}^{t} v(t) \text{ } \mathrm{d}t
\end{equation}
```

## 1) Přidání _MathJax_ configu do `<head>` elementu

Nejprve do HTML kódu webu, konkrétně do `<head>` elementu, přidejme
následující konfiguraci:

```html
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: {
      equationNumbers: {
        autoNumber: "AMS"
      }
    },
    tex2jax: {
      inlineMath: [ ['$','$'], ['\\(', '\\)'] ],
      displayMath: [ ['$$','$$'] ],
      processEscapes: true,
    }
  });
</script>
<script type="text/javascript" async
        src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```

Tato konfigurace - mimo jiné - říká například to, že inline matematické výrazy
hodláme uvozovat mezi znaky `$` (tj. mezi dolary; např. `$a = \sqrt{b}$`), případně
mezi `\(` a `\)`, např. `\(a = \sqrt{b}\)`. Samostatné matematické výrazy
(tj. ne ty vložené přímo do textu) pak budeme uvozovat znakem `$$`.

__Pozn.__ _Místo `$$` můžeme použít i jiná uvození matematických výrazů, např. `\begin{equation}`,
které jsem použil v úvodu článku. Více podrobností o zápisu matematických výrazů najdete
[v oficiální dokumentaci MathJaxu][4]._

__Doporučení__: Výše uvedený _MathJax_ config můžete uložit např.
do souboru `_includes/mathjax_support.html`, a na konec `<head>` elementu
vašeho HTML přidat něco na tento způsob:

{% raw %}
```js
{%- if page.use_math %}
  {% include mathjax_support.html %}
{%- endif %}
```
{% endraw %}

## 2) Vkládání _MathJax_ skriptu pouze do článků, kde jej hodláme použít

Následně v těch příspěvcích vašeho blogu, kde chcete _MathJax_ aktivovat,
jednoduše do [Front Matteru][5] přidejte `use_math: true`.

```yaml
---
title: blabla
author: Your Omnivor
# etc...
use_math: true
---
```

Takto zajistíte, že _MathJax_ skript bude vložen pouze do těch stránek,
ve kterých jej chcete používat.

## 3) To je vše - nyní lze _MathJax_ bez problémů používat

Nyní už jen stačí při psaní článku nezapomenou dát do [Front Matteru][5]
`use_math: true` a můžete zapisovat matematiku! Jako rozcestník pro další
informace o knihovně _MathJax_ a jejím použití doporučuji [oficiální dokumentaci][6].

[1]: https://cs.wikipedia.org/wiki/LaTeX
[2]: https://www.mathjax.org/
[3]: http://haixing-hu.github.io/programming/2013/09/20/how-to-use-mathjax-in-jekyll-generated-github-pages/
[4]: https://docs.mathjax.org/en/latest/start.html#tex-and-latex-input
[5]: https://jekyllrb.com/docs/frontmatter/
[6]: https://docs.mathjax.org/en/latest/index.html
