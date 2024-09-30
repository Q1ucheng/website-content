# 数学建模中的LaTeX代码
> 一些已经编译好的LaTeX代码，可随时取用.

??? tip

    游戏结束，最难绷的一集！

## 1. 宏包的引用

```latex
\documentclass[12pt,a4paper,utf8]{article} % 文档类设置为article，字体大小为12pt，纸张尺寸为A4，编码为utf8
\usepackage{ctex} % 使用ctex宏包以支持中文
\usepackage{url} % 支持在文档中插入URL
\usepackage{booktabs} % 提供漂亮的表格线
\usepackage{makecell}% 允许在表格中使用更多的命令和选项
\usepackage{tabularx} % 提供可自动调整宽度的表格
\usepackage{amssymb}% 提供额外的数学符号
\usepackage{amsmath} % 提供数学公式和环境

\usepackage{setspace} % 控制行距
\usepackage{graphicx} % 支持插入图像
\usepackage{array,caption} % 提供更多的表格控制选项
\usepackage[labelfont=bf]{caption} % 设置标题的字体为粗体

\usepackage{tabu}                     % 表格插入
\usepackage{multirow}                 % 一般用以设计表格，将所行合并
\usepackage{multicol}                 % 合并多列
\usepackage{multirow}                % 合并多行
\usepackage{float}                    % 图片浮动
\usepackage{makecell} 

\usepackage[colorlinks,
linkcolor=blue,      
anchorcolor=blue,  
citecolor=blue,        
]{hyperref}

% \documentclass{article}
\usepackage{listings}  % 导入代码列表宏包

\usepackage{xcolor} % 导入颜色宏包

%New colors defined below
\definecolor{codegreen}{rgb}{0,0.6,0} % 代码中的注释颜色
\definecolor{codegray}{rgb}{0.5,0.5,0.5} % 代码中的行号和注释颜色
\definecolor{codepurple}{rgb}{0.58,0,0.82} % 代码中的关键字颜色
\definecolor{backcolour}{rgb}{0.95,0.95,0.92} % 代码的背景颜色

%Code listing style named "mystyle"
\lstdefinestyle{mystyle}{
	backgroundcolor=\color{backcolour},  % 设置代码的背景颜色
    commentstyle=\color{codegreen},  % 设置代码中注释的颜色
    keywordstyle=\color{magenta},  % 设置代码中关键字的颜色
    numberstyle=\tiny\color{codegray},  % 设置代码中行号的颜色
    stringstyle=\color{codepurple},  % 设置代码中字符串的颜色
    basicstyle=\ttfamily\footnotesize,  % 设置代码的基本样式为等宽字体、小号字体
    breakatwhitespace=false,  % 控制代码在空白处是否换行
    breaklines=true,  % 控制长代码是否自动换行
    captionpos=b,  % 设置代码标题的位置为底部
    keepspaces=true,  % 保留代码中的空格
    numbers=left,  % 设置行号显示在代码的左侧
    numbersep=5pt,  % 设置行号与代码之间的间距
    showspaces=false,  % 控制是否显示代码中的空格
    showstringspaces=false,  % 控制是否显示代码中字符串之间的空格
    showtabs=false,  % 控制是否显示代码中的制表符
    tabsize=2  % 设置制表符的大小为2个空格
}

% 设置代码列表的样式为 "mystyle"
\lstset{style=mystyle}
```

## 2. 三线表
```latex
	% Written especially for 朱宇欣
    \begin{table}[!htp]
		\centering
		\setlength{\tabcolsep}{16mm}
		\caption{本文所用符号的相关说明与解释}\label{Tab:1}
		\begin{tabular}{cc}
			\toprule[1.5pt]
			%\makebox[0.3\textwidth][c]{符号}	&  \makebox[0.4\textwidth][c]{意义} \\
			符号 & 意义 \\ 
			\midrule
			$x_{i1}$ & 一个品类在第i天的平均成本 \\
			$x_{i2}$ & 一个品类在第i天的平均利润率 \\  
			$y_i$    & 一个品类的销量 \\
			$\alpha$ & 平均成本相关系数 \\
			$\beta$  & 平均利润率相关系数 \\
			$\gamma$ & 线性拟合常量 \\
			\bottomrule[1.5pt]
		\end{tabular}
	\end{table}

```

## 3. 图片的插入

```latex
% 单个图的插入
\begin{figure}[!htbp]
		\centering
		\includegraphics[width=.6\textwidth]{图片名称}
	\end{figure}


% 图片并列
\begin{figure}[htbp]
		\centering
		\begin{minipage}[t]{0.48\textwidth}
			\centering
			\includegraphics[width=6cm]{图片名称}
			\caption{图片标题}
		\end{minipage}
		\begin{minipage}[t]{0.48\textwidth}
			\centering
			\includegraphics[width=6cm]{图片名称}
			\caption{图片标题}
		\end{minipage}
	\end{figure}
```
## 4. 一些零碎的语句
```latex
\textbf{} % 文字加粗
```

## 4. 附录相关
```latex
	%附录
	\appendix
	\section{主程序--python 源程序}
\begin{lstlisting}[language=Python, caption=附录名称]

...

\end{lstlisting}
```
