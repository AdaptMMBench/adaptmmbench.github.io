


\begin{table}[ht!]
  \centering
  \definecolor{softblue}{rgb}{0.93, 0.96, 1.0}
  \definecolor{softgreen}{rgb}{0.94, 0.98, 0.94}
  \definecolor{reasoningyellow}{rgb}{1.0, 0.98, 0.9}
  \definecolor{opensourcecyan}{rgb}{0.9, 0.98, 1.0}
  \definecolor{closedpurple}{rgb}{0.96, 0.94, 1.0}
  \definecolor{headergray}{rgb}{0.95, 0.95, 0.95}
  \definecolor{darkergray}{rgb}{0.35, 0.35, 0.35}

  % \caption{Detailed statistics of model decision quality on \bench. We report the confusion matrix components (TP, FP, TN, FN) and the Matthews Correlation Coefficient (MCC) to evaluate the meta-cognitive calibration of models. The best and second-best MCC scores within each category are highlighted in \colorbox{softblue}{blue} and \colorbox{softgreen}{green}, respectively.}
  \caption{{Evaluation of mode selection performance across models.} We report TP, FP, TN, FN, and the MCC to assess meta-cognitive calibration in adaptive reasoning mode. Best and second-best scores in each category are highlighted in \colorbox{softblue}{blue} and \colorbox{softgreen}{green}.}
  \label{tab:adaptive_results}
  \begin{adjustbox}{width=0.4\textwidth}
    \begin{tabular}{l | cccc | c}
      \toprule
      \textbf{Model}         & \textbf{TP} $\uparrow$ & \textbf{FP} $\downarrow$ & \textbf{TN} $\uparrow$ & \textbf{FN} $\downarrow$ & \textbf{MCC} $\uparrow$           \\
      \midrule
      \rowcolor{headergray} \multicolumn{6}{c}{\textit{Open-Source Models}} \\
      \midrule
      PixelReasoner          & 280                    & 196                      & 434                    & 390                      & 0.11                              \\
      Deepeyes               & 662                    & 638                      & 0                      & 0                        & 0.00                              \\
      Thyme                  & 20                     & 20                       & 655                    & 605                      & 0.01                              \\
      PyVision               & 540                    & 405                      & 231                    & 124                      & 0.20                              \\
      Deepeyes v2           & 623                    & 676                      & 1                      & 0                        & 0.03                              \\
      AdaptVision            & 385                    & 279                      & 375                    & 261                      & 0.17                              \\
      % \midrule
      % \rowcolor{opensourcecyan} \multicolumn{6}{c}{\textit{Open-Source General Models}} \\
      % \midrule
      Qwen3-vl-8B-Instruct   & 328                    & 381                      & 351                    & 240                      & 0.06                              \\
      Qwen3-vl-32B-Instruct  & 348                    & 646                      & 245                    & 61                       & 0.14                              \\
      Qwen3-vl-235B-Instruct & 286                    & 437                      & 487                    & 90                       & \cellcolor{softgreen}0.26         \\
      % \midrule
      % \rowcolor{closedpurple} \multicolumn{6}{c}{\textit{Closed-Source VLMs}} \\
      % \midrule
      \midrule
      \rowcolor{headergray} \multicolumn{6}{c}{\textit{Closed-Source Models}}   \\         
      \midrule
      GPT-5                  & 482                    & 392                      & 376                    & 50                       & \cellcolor{softblue}\textbf{0.41} \\
      Gemini-3-Pro           & 284                    & 703                      & 296                    & 17                       & 0.24                              \\
      \bottomrule
    \end{tabular}
  \end{adjustbox}
\end{table}



\begin{table}[h]
  \centering
  \definecolor{softblue}{rgb}{0.93, 0.96, 1.0}
  \definecolor{softgreen}{rgb}{0.94, 0.98, 0.94}
  \definecolor{headergray}{rgb}{0.95, 0.95, 0.95}
  \definecolor{darkergray}{rgb}{0.35, 0.35, 0.35}

  \caption{Comprehensive evaluation of reasoning process, including key step coverage (Key Step Cov.), tool effectiveness (Tool Effect.), and efficiency. This assesses the logical rigor of the reasoning paths alongside their computational efficiency.}
  \label{tab:process_results}
  \begin{adjustbox}{width=0.46\textwidth}
    \begin{tabular}{l cc | ccc}
      \toprule
      \multirow{2}{*}{\textbf{Model}} & \multirow{2}{*}{\shortstack{\textbf{Key Step} \\ \textbf{Cov.} (\%) $\uparrow$}} & \multirow{2}{*}{\shortstack{\textbf{Tool} \\ \textbf{Effect.} (\%) $\uparrow$}} & \multicolumn{3}{c}{\textbf{Efficiency}} \\ % 去掉了右侧竖线和 AEI
      \cmidrule(lr){4-6}
                                      &                                               &                    & Steps $\downarrow$ & Tools $\downarrow$ & Tokens $\downarrow$ \\
      \midrule
      PixelReasoner                   & 76.02                                         & 56.51              & \cellcolor{softgreen}{1.37}               & \cellcolor{softgreen}0.37                & 4229.00             \\
      Deepeyes                        & 75.56                                         & 50.99              & 2.00                & 1.68                & 7601.45             \\
      Thyme                           & 77.14                                         & 56.50              & \cellcolor{softblue}\textbf{{1.05}}   & \cellcolor{softblue}\textbf{0.06}      & 6708.47             \\
      PyVision                        & 77.43                                         & 62.02              & 2.76                & 1.76                & \cellcolor{softblue}\textbf{2481.00} \\
      Deepeyes v2                    & 75.14                                         & 56.79              & 2.09                & 1.09                & 6918.90             \\
      AdaptVision                     & 72.60                                         & 81.70              & 1.51                & 0.51   & \cellcolor{softgreen}4175.96             \\
      Qwen3-vl-8B                     & 78.40                                         & \cellcolor{softgreen}{91.62} & 1.76                & 1.20                & 8282.40             \\
      Qwen3-vl-32B                    & \cellcolor{softgreen}83.79                                         & \cellcolor{softblue}\textbf{92.98}    & 2.42                & 1.44                & 7725.99             \\
      Qwen3-vl-235B                   & \cellcolor{softblue}\textbf{84.83}                             & 89.64              & 2.04                & 1.04                & 7531.95             \\
      \bottomrule
    \end{tabular}
  \end{adjustbox}
\end{table}