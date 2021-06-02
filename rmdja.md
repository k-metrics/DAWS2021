---
title: "無題の論文"
date: "2021-06-02"
author: "RMDJA太郎"
abstract: "`rmdja` パッケージは, `rmarkdown` および `bookdown` パッケージで自然なレイアウトの日本語文書を作成する際に必要な煩雑な設定を自動で行い, ユーザーの負担を軽減するために作成されたパッケージである."
output:
  rmdja::pdf_document2_ja:
    latex_engine: lualatex
documentclass: bxjsarticle
# documentclass: bxjsreport      # 章（chapter）のあるレポート用
classoption:
  - a4paper
  - 'number-of-lines=30'  # 1頁30行, ただし見出しは別
  - 'textwidth=40zw'      # 1行全角40字, ただしプロポーショナルフォントなので絶対ではない
bibliography: 
  - packages.bib
link-citations: false
---

\newpage



# イントロダクション {#introduction}

文書の作成には `rmarkdown` および `bookdown` パッケージ [@R-rmarkdown;@R-bookdown] が必要である. `citr`, `clipr` も執筆に役立つパッケージである.

第 \@ref(related-works) 節は先行研究のサーベイである.
第 \@ref(methodology) 節は今回提起する問題とその解決方法である.
第 \@ref(experiment) 節は実験内容である.
第 \@ref(conclusions) 節は結論である.

# 先行研究 {#related-works}

最も充実したドキュメントは開発メンバーの謝益輝 (Yihui) 氏らによる以下の3つである.

* "[R Markdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/)
* "[`bookdown`: Authoring Books and Technical Documents with R Markdown](https://bookdown.org/yihui/bookdown/)"
* "[R Markdown Cookbook](https://bookdown.org/yihui/rmarkdown-cookbook/)"


# 問題の定式化 {#methodology}

このサンプルを動かすには `knitr` [@R-knitr], `tidyverse` [@R-tidyverse] が必要である.

# 実験 {#experiment}

図 \@ref(fig:plot) が結果である.

(ref:ggplot-example-article) `ggplot2` を使用したデータのプロット


```{.r .numberLines .lineAnchors}
ggplot(
  mutate(mtcars, cyl = factor(cyl)),
  aes(x = mpg, y = wt, color = cyl)
) +
  geom_point() +
  labs(x = "マイル毎米ガロン", y = "重量 (1000ポンド)") +
  theme_bw(base_family = rmdja::get_default_font_family("lualatex")["serif"]) +
  scale_color_grey() +
  scale_fill_grey()
```

\begin{figure}

{\centering \includegraphics[width=1\linewidth,height=1\textheight,keepaspectratio]{rmdja_files/figure-latex/plot-1} 

}

\caption{(ref:ggplot-example-article)}(\#fig:plot)
\end{figure}

# 結論 {#conclusions}

表\@ref(tab:table-example)を見よ.


```{.r .numberLines .lineAnchors}
knitr::kable(head(mtcars[, 1:4]), booktabs = T, caption = "表の例", format = "pipe")
```



Table: (\#tab:table-example)表の例

|                  |  mpg| cyl| disp|  hp|
|:-----------------|----:|---:|----:|---:|
|Mazda RX4         | 21.0|   6|  160| 110|
|Mazda RX4 Wag     | 21.0|   6|  160| 110|
|Datsun 710        | 22.8|   4|  108|  93|
|Hornet 4 Drive    | 21.4|   6|  258| 110|
|Hornet Sportabout | 18.7|   8|  360| 175|
|Valiant           | 18.1|   6|  225| 105|

このファイルの出力例は以下のコマンドでコピーすることができます.


```{.r .numberLines .lineAnchors}
file.copy(system.file("resources/examples/templates/pdf_article_ja/", package = "rmdja"), "./", recursive = T)
```

<!-- 参考文献 -->
<!-- コメントはこのように HTMLの記法を使う. tex の % は使えない -->


