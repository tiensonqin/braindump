+++
title = "Playing Atari with Deep RL"
author = ["Jethro Kuan"]
lastmod = 2020-07-17T00:55:43+08:00
draft = false
+++

## Playing Atari With Deep RL ([Mnih et al., n.d.](#orge8c8d98)) {#playing-atari-with-deep-rl--mnih-et-al-dot-n-dot-d-dot--orge8c8d98}

### Preprocessing Steps {#preprocessing-steps}

1.  Obtain raw pixels of size \\(210 \times 160\\)
2.  Grayscale and downsample to \\(110 \times 84\\)
3.  Crop representative \\(84 \times 84\\) region
4.  Stack the last 4 frames in history to form the \\(84 \times 84 \times
    4\\) input

### DQN {#dqn}

1.  Use of [Experience Replay]({{< relref "experience_replay" >}}) buffer
2.  Separate target network stabilizes optimization targets:

\begin{equation}
\delta = r_t + \gamma \mathrm{max}\_a Q(s\_{t+1}, a ; \theta') -
Q(s_t, a_t; \theta)
\end{equation}

The network parameterized with \\(\theta '\\) is a snapshot of the network
at some point in time, so the optimization target doesn't change so
rapidly.

1.  Clip \\(\delta\\) to \\(\left[1, -1\right]\\)

## Improving DQN {#improving-dqn}

- Double Q-learning reduces bias ([Van Hasselt, Guez, and Silver, n.d.](#org8a4647c))
- Average Q-learning reduces variance ([Anschel, Baram, and Shimkin, n.d.](#org7241430))
- [Hindsight Experience Replay]({{< relref "andrychowicz2017_hindsight_experience_replay" >}}) ([Andrychowicz et al., n.d.](#orgd6137a5))
- Distributional RL ([Dabney et al., n.d.](#org2f09943))

## References {#references}

- [Defeating the Deadly Triad: | random walks and lots of ♥s](https://davidsanwald.github.io/2016/12/11/Double-DQN-interfacing-OpenAi-Gym.html)

## Bibliography {#bibliography}

<a id="orgd6137a5"></a>Andrychowicz, Marcin, Filip Wolski, Alex Ray, Jonas Schneider, Rachel Fong, Peter Welinder, Bob McGrew, Josh Tobin, OpenAI Pieter Abbeel, and Wojciech Zaremba. n.d. “Hindsight Experience Replay.” In _Advances in Neural Information Processing Systems_, 5048–58.

<a id="org7241430"></a>Anschel, Oron, Nir Baram, and Nahum Shimkin. n.d. “Averaged-Dqn: Variance Reduction and Stabilization for Deep Reinforcement Learning.” In _Proceedings of the 34th International Conference on Machine Learning-Volume 70_, 176–85. JMLR. org.

<a id="org2f09943"></a>Dabney, Will, Mark Rowland, Marc G Bellemare, and Rémi Munos. n.d. “Distributional Reinforcement Learning with Quantile Regression.” In _Thirty-Second AAAI Conference on Artificial Intelligence_.

<a id="orge8c8d98"></a>Mnih, Volodymyr, Koray Kavukcuoglu, David Silver, Alex Graves, Ioannis Antonoglou, Daan Wierstra, and Martin Riedmiller. n.d. “Playing Atari with Deep Reinforcement Learning.”

<a id="org8a4647c"></a>Van Hasselt, Hado, Arthur Guez, and David Silver. n.d. “Deep Reinforcement Learning with Double Q-Learning.” In _Thirtieth AAAI Conference on Artificial Intelligence_.
