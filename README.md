# BTC Network Simulation

Part of the Networked Society research done for Honors at the TU/e. This simulates the construction of the network as closely as possible. 

We chose to model the dynamics of the network as a discrete stochastic process. In particular, we consider some reasonable timestep, say $\Delta t$, and for each step, one of the following occurs:
\begin{itemize}
    \item A new client enters the network,
    \item A connected client leaves the network.
\end{itemize}
Our underlying network is represented by a time varying directed graph $B: T \rightarrow G$ with $T = \{ n \Delta t : n \in \mathbb{N} \}$ and $G$ the space of all directed graphs. For convenience, we denote by $V(t)$ and $ E(t)$ the nodes and edges of our network $B(t)$. Although edges are directional, they act bidirectional from a communication perspective; that is the directionality only encodes the which node initiated the connection. In addition, each node $V(t)$ has a variety of attributes. In particular, one attribute represents the natting state of the node:
$$nat: V(t) \rightarrow \{ true, false \}.$$
Now, to the dynamics, we assume that $B(0) = (V(0), E(0)) = G$ where $G$ is a complete directed graph with $10$ nodes and now, for each ensuing timestep $\Delta t$, some action will be performed:
\begin{itemize}
    \item A node joins the network,
    \item A node exists the network.
\end{itemize}
These actions are never both performed and the action chosen is based on a probability. In particular, the probability that the exiting action is performed is given by $p: T \rightarrow [0,1]$ with:
$$p(t) = \min\bigg\{\dfrac{|V(t)| - 10}{2n}, \dfrac{1}{2}\bigg\}.$$
The probability of joining at time $t \in T$ is given by $1 - p(t)$. So, essentially, each timestep a coin flip with the described probabilities is performed to determine the action performed. 

We, now, define the actions in detail. We make the following assumptions on the attachment strategy of a new node, say $v$, at timestep $t + \Delta t \in T$: 
\begin{itemize}
    \item The new node $v$ can initiate connections to any node in $A = nat^{-1}(true) \subset V(t)$,
    \item $v$ is natted with probability $q$; that is $nat(v) = true$ with probability $q$.
    \item If natted, it chooses $l$ nodes to connect to uniformly from $A$,
    \item Otherwise, it chooses $8$ nodes to connect to uniformly from $A$,\footnote{Filip investigated to what extent this assumption holds true by collecting data of the various DNS seeds (see his report for details)}
\end{itemize}
These assumptions while simplification of the, previously, discussed node behaviour represented to us the most important characteristics of the peer's connection policies.

The exiting strategy of a node $v \in V(t)$ at time $t + \Delta t \in T$ is assumed to adhere to:
\begin{itemize}
    \item All nodes $u \in \{ u \in V(t) : (u,v) \in E(t) \}$ rewire the lost connection $(u,v)$ to $(u,v')$ with $v' \in A = nat^{-1}(true) \subset V(t + \Delta t)$.
\end{itemize}
This ensures the nodes in the network maintain their required number of outgoing connections.

All in all, there are two main parameters that can be varied in the model $q$ and $l$. In a sense, $q$ and $l$ were designed to represent the cost of a node to participate in a network. If more nodes are natted, this represents and easier barrier to entry in the network. Similarly, the lower $l$ is the less bandwidth requirements there are on a node joining the network. So, although varying $q$ to be low and $l$ to be high may be desirable from a network structure perspective, we, also, needed to evaluate the extent to which we can push these parameters to those extremes.

Please add any relevant literature to the following google drive:
https://drive.google.com/drive/folders/1c-1Q7H5glX_qCQP6j0OeZEPpo7nTZPWS?usp=sharing
