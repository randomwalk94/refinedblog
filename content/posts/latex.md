+++
title = "LaTeX in HTML"
author = ["Kaushal Modi"]
date = 2018-02-02T18:58:00-05:00
tags = ["latex", "html", "hugo"]
categories = ["emacs", "org"]
draft = true
creator = "Emacs 27.0.50 (Org mode 9.1.13 + ox-hugo)"
mathjax = "t"
+++

<style>
  .ox-hugo-toc ul {
    list-style: none;
  }
</style>
<div class="ox-hugo-toc toc">
<div></div>

<div class="heading">Table of Contents</div>

- <span class="section-num">1</span> [Using MathJax](#using-mathjax)
- <span class="section-num">2</span> [Using HTML + CSS](#using-html-css)
    - [Define these macros in Org](#define-these-macros-in-org)
    - [CSS](#css)
    - [Use the Org macros](#use-the-org-macros)
- [References](#references)

</div>
<!--endtoc-->

Ever wondered how to show <span class="latex">L<sup>a</sup>T<sub>e</sub>X</span> in HTML or a [Hugo blog post](https://ox-hugo.scripter.co)
exported from Org?

<!--more-->

<span class="timestamp-wrapper"><span class="timestamp">&lt;2018-02-12 Mon&gt;</span></span>
: Add the MathJax method.

---

There are 2 ways to do this:

1.  Using MathJax -- \\(\LaTeX\\).
2.  Using HTML + CSS -- <span class="latex">L<sup>a</sup>T<sub>e</sub>X</span>.


## <span class="section-num">1</span> Using MathJax {#using-mathjax}

If you don't mind including the [MathJax script](https://gitlab.com/kaushalmodi/hugo-theme-refined/blob/master/layouts/partials/mathjax.html), it's as simple as
typing `$\LaTeX$` in Org, which results in \\(\LaTeX\\).

Similarly \\(\TeX\\) (`$\TeX$`) also works, though not `$\XeTeX$`.


## <span class="section-num">2</span> Using HTML + CSS {#using-html-css}

And here's another way if you don't want to include MathJax.


### Define these macros in Org {#define-these-macros-in-org}

```org
#+macro: tex @@html:<span class="tex">T<sub>e</sub>X</span>@@
#+macro: latex @@html:<span class="latex">L<sup>a</sup>T<sub>e</sub>X</span>@@
#+macro: xetex @@html:<span class="xetex">X<sub>&#398;</sub>T<sub>E</sub>X</span>@@
```

```go
import fmt

package main
```

```cpp
// my first program in C++
#include <iostream>

int main()
{
  std::cout << "Hello World!";
}
```

```python
:ef kmeans_display(X, label):
    K = np.amax(label) + 1
    X0 = X[label == 0, :]
    X1 = X[label == 1, :]
    X2 = X[label == 2, :]
    
    plt.plot(X0[:, 0], X0[:, 1], 'b^', markersize = 4, alpha = .8)
    plt.plot(X1[:, 0], X1[:, 1], 'go', markersize = 4, alpha = .8)
    plt.plot(X2[:, 0], X2[:, 1], 'rs', markersize = 4, alpha = .8)

    plt.axis('equal')
    plt.plot()
    plt.show()
    
kmeans_display(X, original_label)
```
### CSS {#css}

Add this CSS directly in the page within a `#+begin_export html` /
`#+end_export` block, or add that CSS your site's stylesheet.

```html
<style>
.tex, .latex, .tex sub, .latex sub, .xetex sub {
  font-size: 1em;
}

.tex sub, .latex sub, .latex sup, .xetex sub {
  text-transform: uppercase;
}

.tex sub, .latex sub, .xetex sub {
  vertical-align: -0.5ex;
  margin-left: -0.1667em;
  margin-right: -0.125em;
}

.latex sup {
  font-size: 0.85em;
  vertical-align: 0.15em;
  margin-left: -0.36em;
  margin-right: -0.15em;
}
</style>
```


### Use the Org macros {#use-the-org-macros}

```org
- {{{tex}}}
- {{{latex}}}
- {{{xetex}}}
```

Export that from Org to HTML or Hugo, and you get:

-   <span class="tex">T<sub>e</sub>X</span>
-   <span class="latex">L<sup>a</sup>T<sub>e</sub>X</span>
-   <span class="xetex">X<sub>&#398;</sub>T<sub>E</sub>X</span>


## References {#references}

-   [stackoverflow.com](https://stackoverflow.com/a/8160532/1219634)
-   [tess.oconnor.cx](http://tess.oconnor.cx/2007/08/tex-poshlet)
-   [hroy.eu](https://hroy.eu/tips/TeX/htmlAndCss/)

[//]: # "Exported with love from a post written in Org mode"
[//]: # "- https://github.com/kaushalmodi/ox-hugo"

