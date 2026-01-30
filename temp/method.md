\subsection{Adaptive Mode Selection Evaluation}
Adaptive intelligence depends on a model’s ability to assess whether its current information is sufficient to solve a task. Consequently, the appropriateness of a reasoning mode should be evaluated independently of answer correctness.
Under this principle, the necessity of tool invocation is determined by the outcome of text-only reasoning. 
If a task can be solved using text reasoning alone, it is labeled as \textbf{Tool-Redundant}, indicating that visual tool invocation is unnecessary and may introduce noise. Conversely, tasks that cannot be solved via text-only reasoning are labeled as \textbf{Tool-Required}, indicating that visual tool invocation is necessary to obtain additional information. This categorization defines the mode selection labels used in our evaluation, as detailed in Fig.~\ref{fig:adaptive_evaluation}. Accordingly, tool invocation decisions are evaluated using a confusion matrix: TP denotes Tool-Required cases where the model invokes tools, FN denotes Tool-Required cases where the model does not invoke tools, TN denotes Tool-Redundant cases where the model selects text-only reasoning, and FP denotes Tool-Redundant cases where the model unnecessarily invokes tools.
\paragraph{Matthews Correlation Coefficient (MCC).}
In adaptive mode selection, the proportions of tool-redundant and tool-required cases are model-dependent, leading to varying degrees of class imbalance in the resulting confusion matrix. To ensure a robust evaluation, we adopt the MCC,
\begin{equation}
  \resizebox{0.9\columnwidth}{!}{$\displaystyle
      \text{MCC} =
      \frac{TP \cdot TN - FP \cdot FN}
      {\sqrt{(TP+FP)(TP+FN)(TN+FP)(TN+FN)} + \epsilon}.
    $}
  \label{equal:mcc}
\end{equation}
where $\epsilon$ is a small constant for numerical stability. MCC ranges from $[-1,1]$, with $1$ indicating perfect agreement with the optimal mode selection, $0$ denoting the chance-level performance, and $-1$ indicating complete misalignment.

\subsection{Reasoning Process Evaluation}

While MCC measures the quality of mode selection, it does not assess the validity of the reasoning process. Models may produce correct answers despite logical errors or improper tool usage. To address this limitation, we introduce three process-oriented metrics to evaluate reasoning coherence and tool execution fidelity.

A reasoning trajectory $\mathcal{R}$ is formalized as an interleaved sequence of reasoning steps and tool invocations:
\begin{equation}
  \mathcal{R} = \{(s_1, t_1), (s_2, t_2), \dots, s_n\},
\end{equation}
where $s_i$ is the reasoning at step $i$ and $t_i \in \mathcal{T}$ represents the corresponding tool invocation. The trajectory terminates at the final reasoning step $s_n$, and produces the answer.


\subsubsection{Key Steps Coverage}
Following the evaluation paradigm of \cite{jiang2025mme},
we assess whether a model’s reasoning chain $\{s_i\}_{i=1}^n$ covers the essential human-annotated key steps $K$ defined in Sec.~\ref{sec:data_formulation}. We employ GPT-5 as an evaluator to identify the presence of these key steps within the generated reasoning, and define the key step coverage as:
\begin{equation}
  \text{KCoverage}
  =
  \frac{1}{|K|}
  \max_j
  \prod_{i=1}^j
  \mathbb{I}\!\left[k_i \underset{\text{\tiny GPT-5}}{\in} \{s_1,\dots,s_n\}\right].
\end{equation}
This metric measures how far the model’s reasoning progresses along the key steps. Rather than penalizing skipped or compressed steps, KCoverage captures the maximum extent to which the reasoning aligns with the solution structure, allowing different reasoning styles and reflecting how close the model comes to a correct solution.



\subsubsection{Tool Execution Effectiveness}
To assess the precision of tool usage, we evaluate whether each tool invocation is semantically appropriate for its corresponding reasoning step and free of execution errors. The tool effectiveness is defined as:
\begin{equation}
  \text{Effect}_{\text{tool}}
  =
  \frac{1}{N_{\text{tool}}}
  \sum_{i=1}^{N_{\text{tool}}}
  \text{valid}_{\text{GPT-5}}(t_i \mid s_i),
\end{equation}
where $N_{\text{tool}}$ denotes the total number of tool invocations, $t_i \in \mathcal{T}$ is the tool invoked at step $i$, and $\text{valid}_{\text{GPT-5}}(\cdot) \in \{0,1\}$ is a semantic validity judgment provided by GPT-5.
