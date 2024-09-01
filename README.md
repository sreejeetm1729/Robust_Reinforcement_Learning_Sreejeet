# Robust_Reinforcement_Learning
Recently, there has been a growing interest in understanding the non-asymptotic behavior of model-free reinforcement learning algorithms. Despite this focus, the performance of these algorithms in non-ideal settings, such as those with corrupted rewards, remains poorly understood. Addressing this gap, we examine the robustness of the well-known Q-learning algorithm under a strong-contamination attack model, where an adversary can arbitrarily perturb a small fraction of observed rewards. We first demonstrate that such attacks can lead to unbounded errors in the standard Q-learning algorithm. To counter this, we propose a novel robust synchronous Q-learning algorithm that leverages historical reward data to construct robust empirical Bellman operators at each time step. We further establish a finite-time convergence rate for our algorithm, which matches the best-known bounds for Q-learning in the absence of attacks, up to a small unavoidable error term \( O(\varepsilon) \) that scales with the adversarial corruption fraction \( \varepsilon \).

Test Case:  Consider the MDP depicted in the figure. In the absence of attacks, state 1 yields a reward of $d$ when taking action $a = L$ and a reward of $-d$ for action $a = R$, where $d > 0$. States 2 and 3 provide a reward of 1, while states 4 and 5 provide a reward of 0. Under a Huber attack model, the rewards in state $s = 1$ are perturbed: for the state-action pair $(1, L)$, the reward is $d$ with probability $1-\varepsilon$ and $-C$ with probability $\varepsilon$; for $(1, R)$, the reward is $-d$ with probability $1-\varepsilon$ and $C$ with probability $\varepsilon$. The corruption signal $C$ is defined as $\left((2-\varepsilon)d + \kappa\right) \varepsilon^{-1}$, where $\kappa > 0$ is a tunable parameter. The error norm $\lVert Q_t - Q^* \rVert_\infty$ is plotted for both the Vanilla Q-Learning Algorithm under corruption with $\varepsilon = 0.01$ (shown in \textcolor{red}{red}) and our proposed $\varepsilon$-Robust TD Learning Algorithm under the same corruption level (shown in \textcolor{blue}{blue}), highlighting the significant improvement of our approach.

This exactly aligns with our proven result :
\begin{tcolorbox}
\begin{theorem}\label{theorem:theoremmainresult} (\textbf{Robust Q-learning bound}) Suppose the corruption fraction satisfies $\varepsilon \in [0,1/16)$. Then, given any $\delta \in (0,1)$, the output of Algorithm~\ref{algo:algo2} with step-size $\alpha = \frac{\log T}{(1-\gamma)T}$  satisfies the following bound with probability at least $1-\delta$:
\begin{equation}
d_T \leq \frac{d_0}{T} + O\left( \frac{\R}{(1-\gamma)^{\frac{5}{2}}}  \frac{\log T}{\sqrt{T}} \sqrt{ \log \left(\frac{|\mathcal{S}||\mathcal{A}|T}{\delta}\right)} +  \frac{\R\sqrt{\varepsilon}}{1-\gamma}\right). 
\label{eqn:main_conv_bnd}
\nonumber
\end{equation}
\end{theorem}
\end{tcolorbox}


