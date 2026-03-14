# Collective Geometric Computation
## A First-Principles Theory of Artifact-Mediated Decision Inference in Sequential Human Systems

> A shared physical artifact, modified sequentially by uncoordinated agents,
> is a biological computer.
> Each agent is an approximate sampler from a Gibbs distribution.
> The energy function is the decision rule.
> Recovering the energy function from the artifact is the scientific objective.

---

## The Central Problem

A blank surface is placed in a shared space. One instruction is given:

> **Choose one shape and place it anywhere on the surface.**

Agents arrive one at a time. Each observes the surface, places a single shape, and leaves. No agent communicates with another. No agent knows the identity, sequence, or reasoning of any prior agent. No shared goal exists.

The surface fills. Structure appears.

The question this framework addresses is not descriptive — not *what pattern formed* — but generative and causal: **what decision rule, operating inside each agent, produced this structure?** And the deeper question beneath it: **what class of computational problem are these agents collectively solving?**

---

## What This Framework Is

Every prior approach in spatial point process modeling takes an observed pattern and asks: *what statistical structure characterizes this distribution?* The framework is descriptive. The agent is unobservable. The generative mechanism is inferred post hoc if at all.

This framework inverts the entire objective. The spatial configuration is not the thing to be characterized. It is the **evidence** — the compressed external record of a sequence of decisions made by deliberate cognitive agents. The target of inference is the decision rule those agents were following, recovered from the geometry they left behind.

This inversion has three structural consequences that separate the framework from all existing work:

**The intensity function is a decision rule, not a physical rate.** In all existing spatial and spatiotemporal point process literature, the conditional intensity $\lambda(q, \ell \mid X_t)$ measures how frequently events arise from a physical process. Here it measures the probability that a deliberate cognitive agent, reading the current configuration, selects shape $q$ and location $\ell$. This is not a terminological distinction. It changes the meaning of every estimated parameter, every goodness-of-fit criterion, and every simulation.

**The artifact is simultaneously record, stimulus, and coordination medium.** The shared surface is the complete history of all prior decisions, the perceptual input that structures the next decision, and the only channel through which uncoordinated strangers implicitly coordinate. No existing spatial model treats a physical object as all three of these simultaneously, because no existing spatial model concerns itself with agents coordinating through an artifact they are collectively constructing.

**Marks carry intrinsic geometry.** Every existing marked point process treats the mark as a dimensionless label — a type, a category, a scalar. This framework treats the mark as a geometric object with spatial extent, orientation, and symmetry structure that changes how it interacts with neighboring marks. A circle adjacent to a square is a structurally different spatial relationship than a square adjacent to a triangle. That difference enters the energy function.

---

## Formal Setup

### Domain

Let $\mathcal{S} = [0, W] \times [0, H] \subset \mathbb{R}^2$ be the bounded planar domain — the physical surface.

### Mark Space

Let $\mathcal{Q} = \{\circ, \square, \triangle\}$ be the finite categorical mark space of geometric primitives.

### Configuration Space

A **marked configuration** is a finite collection of spatially located typed events:

$$X = \{(q_i, \ell_i)\}_{i=1}^{n} \;\in\; \mathcal{N}_f(\mathcal{S} \times \mathcal{Q})$$

where $\mathcal{N}_f(\mathcal{S} \times \mathcal{Q})$ is the space of finite marked point configurations over $\mathcal{S} \times \mathcal{Q}$.

### The Construction Process

The artifact evolves as a **strictly additive, irreversible sequential process**:

$$X_0 = \emptyset \qquad X_{t+1} = X_t \cup \{(q_{t+1},\, \ell_{t+1})\}$$

No element is ever removed or relocated. Each agent contributes exactly one event. The configuration at time $n$ is the complete unalterable record of $n$ sequential decisions.

### The Shape Descriptor

Each placed mark is fully characterized by:

$$s = (q,\; \ell,\; r,\; \phi,\; \varepsilon)$$

| Parameter | Meaning |
|---|---|
| $q \in \mathcal{Q}$ | categorical mark type |
| $\ell \in \mathcal{S}$ | centroid location |
| $r \in \mathbb{R}_+$ | characteristic scale |
| $\phi \in [0, 2\pi)$ | orientation angle |
| $\varepsilon$ | deviation from ideal geometric form |

---

## The Computational Complexity Foundation

Before deriving the decision model, it is necessary to establish the computational nature of the problem each agent faces.

When an agent observes configuration $X_t$ and selects action $(q, \ell)$, they are — implicitly, approximately, and without conscious deliberation — evaluating a compatibility function over all possible placements across all shape types. If the compatibility function is an energy defined over pairwise and higher-order spatial interactions, then the **exact** computation of the normalizing constant

$$\mathcal{Z}(X_t) = \sum_{q' \in \mathcal{Q}} \int_{\mathcal{S}} \exp(-\mathcal{H}(q', \ell' \mid X_t))\, d\ell'$$

is a **#P-hard problem** — it lives in the complexity class above NP under the assumption P $\neq$ NP. No polynomial-time algorithm can compute it exactly. The intractability is not an artifact of the parameterization. It is a fundamental property of any energy function over interacting spatial configurations.

This has a direct consequence for the interpretation of agent behavior: **agents who place shapes appropriately — respecting clustering, symmetry, spacing, and mark coherence — are approximately solving a computationally intractable problem.** They do so in seconds, without explicit computation, using perceptual and cognitive mechanisms that evolution developed for precisely this class of problem. The placement behavior is not a simple heuristic. It is biological approximate computation over an otherwise intractable distribution.

The inference problem inherits this structure. Recovering $\mathcal{H}$ from observed placements cannot use exact likelihood — the partition function $\mathcal{Z}$ appears in the likelihood and is #P-hard to evaluate. The entire inference pipeline is designed to operate in the regime where exact computation is impossible, which is the only regime in which the biological system being modeled also operates.

---

## Human Agents as Approximate Gibbs Samplers

The Gibbs distribution provides the natural probabilistic model for a decision-maker who evaluates the compatibility of an action with a current state via a real-valued energy function.

**Definition.** An agent is an **approximate Gibbs sampler** with respect to energy function $\mathcal{H}$ if, given field state $X_t$, the agent produces action $(q, \ell)$ with probability density approximately proportional to:

$$P(q, \ell \mid X_t) \;\propto\; \exp(-\mathcal{H}(q, \ell;\; X_t))$$

Low energy actions are preferred. High energy actions are suppressed. The temperature parameter is absorbed into the energy weights and is not separately identified.

**Why Gibbs?** The Gibbs distribution is the maximum entropy distribution over actions subject to the constraint that the expected energy is fixed. It is the unique distribution that encodes all information about agent preferences through the energy function and no other structure. It is therefore the minimally assumptive model consistent with the energy-based interpretation of agent behavior — it adds exactly as much structure as the energy function requires and nothing more.

**Why approximate?** Exact Gibbs sampling requires evaluating $\mathcal{Z}(X_t)$, which is #P-hard. Human agents produce samples from the distribution without computing the normalizer — they sample approximately, using perceptual shortcuts that approximate the Gibbs weighting without explicit calculation. The approximation quality varies across agents and configurations but the target distribution is always the Gibbs measure defined by $\mathcal{H}$.

---

## The Artifact as Biological Computer

The three roles of the artifact — record, stimulus, and coordination medium — are not merely descriptive. They constitute a specific computational architecture:

**The artifact as memory.** $X_t$ stores the complete decision history of the collective. No agent needs to remember prior decisions. No agent needs to know the sequence. No agent needs to know the identity of prior agents. The artifact is the external memory of the computation, written in geometry.

**The artifact as program.** The current configuration $X_t$ is also the input to each agent's decision process. It defines the energy landscape the agent samples from. The artifact does not merely record computation — it specifies the computation that will occur next. It is simultaneously state and instruction.

**The artifact as output.** The final configuration $X_n$ is the product of $n$ sequential approximate Gibbs samples from an energy function that was never written down, never negotiated, and never communicated. It is the output of a distributed computation performed by $n$ uncoordinated biological processors who share only a surface.

This architecture has a specific name in the study of social insects: **stigmergy** — indirect coordination through environmental modification first formalized by Grassé (1959) studying termite mound construction. This framework is the first application of stigmergy to a system where the environmental modifications are geometric primitives and the coordination medium is a two-dimensional surface subject to formal spatial statistical analysis.

The critical structural distinction from all prior stigmergy models: in insect stigmergy, the deposited substance is a physical chemical (pheromone, material). In this framework, the deposited substance is a geometric object with categorical identity, spatial extent, orientation, and symmetry structure. The mark is not a passive trace. It is an active geometric stimulus that imposes an energy structure on the decision landscape of every subsequent agent.

---

## Markov Structure and Sufficient Statistics

Agents observe only the current visible configuration. They have no access to the identity, sequence, or reasoning of prior agents. This motivates:

**The Markov assumption:**

$$P(X_{t+1} \mid X_0, X_1, \dots, X_t) = P(X_{t+1} \mid X_t)$$

**Justification from sufficient statistics.** The configuration $X_t$ is the complete spatial record of all prior actions. An agent reading the surface recovers — through perceptual processing of geometry — the aggregate signal of every preceding decision: local density, clustering, symmetry axes, empty regions, dominant mark types, spatial gradients. The current configuration encodes prior history through its geometry. It is therefore the natural sufficient statistic for predicting the next action, and the Markov assumption follows from this sufficiency rather than from an independence claim.

Under this assumption the construction process defines a **discrete-time Markov chain** on $\mathcal{N}_f(\mathcal{S} \times \mathcal{Q})$ with transition kernel:

$$K\bigl((q_{t+1}, \ell_{t+1}) \mid X_t\bigr) \;=\; \frac{\exp(-\mathcal{H}(q_{t+1}, \ell_{t+1};\; X_t))}{\mathcal{Z}(X_t)}$$

The chain is strictly growing — it never contracts — and irreversible. These properties distinguish it from equilibrium Gibbs processes and from all standard MCMC sampling frameworks, where the chain is ergodic and time-reversible. The construction process is non-ergodic by design: it is a record of history, not a stationary distribution.

---

## The Conditional Intensity as Decision Rule

The fundamental object of the framework is the conditional intensity function:

$$\lambda : \mathcal{Q} \times \mathcal{S} \times \mathcal{N}_f(\mathcal{S} \times \mathcal{Q}) \;\to\; \mathbb{R}_+$$

Given field state $X_t$, the probability that an agent selects shape $q$ and location $\ell$ is:

$$P(q, \ell \mid X_t)\, d\ell \;=\; \frac{\lambda(q, \ell \mid X_t)}{\mathcal{Z}(X_t)}\, d\ell$$

The distinction between this interpretation and all prior point process literature is precise and consequential:

In prior literature, $\lambda$ is a **rate** — it measures how frequently events of type $q$ arise near location $\ell$ per unit time, given prior event history. It is calibrated to natural or social processes in which the generating agent is unobservable (disease spread, seismic activity, crime).

Here, $\lambda$ is a **decision rule** — it measures the probability that a specific cognitive agent, deliberating over the current configuration, selects a specific action. The agent is directly observable (each action is recorded with identity, location, and ordering). The generative process is a sequence of deliberate decisions, not a physical rate.

This reinterpretation changes:
- What the model is for (causal recovery, not pattern characterization)
- What a good fit means (behavioral predictive validity, not distributional accuracy)
- What the estimated parameters mean (each $\beta_k$ is a behavioral tendency, not a statistical association)
- What simulation produces (synthetic behavioral trajectories, not synthetic event patterns)

---

## Gibbs Energy Representation

The conditional intensity admits a Gibbs representation derived from Besag's (1974) consistency theorem: a family of local conditional probability specifications that satisfies positivity and the Markov condition uniquely determines a globally consistent Gibbs distribution. Applied here:

$$\lambda(q, \ell \mid X_t) \;=\; \exp\!\bigl(-\mathcal{H}(q, \ell;\; X_t)\bigr)$$

where $\mathcal{H}$ is the **local interaction energy** — a real-valued function measuring the incompatibility of placing shape $q$ at location $\ell$ given the current configuration.

High $\mathcal{H}$ → high incompatibility → low placement probability.
Low $\mathcal{H}$ → high compatibility → high placement probability.

The energy formulation achieves a specific separation: **what is measured** (spatial features of the configuration) is separated from **how measurements combine** (the parameter weights). This separation is what makes inference tractable despite the #P-hardness of the exact partition function — pseudolikelihood methods work on ratios of local energies, not on the global normalizing constant.

---

## Energy Decomposition

The interaction energy decomposes as a weighted linear combination of spatial feature functions:

$$\mathcal{H}(q, \ell;\; X_t) \;=\; \sum_{k=1}^{K} \beta_k\, f_k(q, \ell;\; X_t)$$

Each $\beta_k \in \mathbb{R}$ is a signed parameter quantifying the strength and direction of one behavioral tendency. Negative $\beta_k$ means the feature attracts. Positive $\beta_k$ means it repels.

### Density Interaction

Attraction or inhibition relative to occupied regions:

$$f_{\text{density}}(q, \ell;\; X_t) = -\log\!\Bigl(1 + \sum_{(q_j, \ell_j) \in X_t} \kappa_h(\|\ell - \ell_j\|)\Bigr)$$

where $\kappa_h$ is an isotropic kernel with bandwidth $h$. Negative $\beta_{\text{density}}$ encodes clustering behavior. Positive encodes inhibition and regular spacing.

### Mark Homophily

Categorical attraction or repulsion between same-type marks:

$$f_{\text{match}}(q, \ell;\; X_t) = \sum_{(q_j, \ell_j) \in X_t} \mathbf{1}[q = q_j] \cdot \kappa_h(\|\ell - \ell_j\|)$$

Negative $\beta_{\text{match}}$ draws same-type shapes together (segregation). Positive disperses them (interleaving).

### Symmetry Completion

Preference for configurations of higher bilateral balance:

$$f_{\text{symmetry}}(q, \ell;\; X_t) = \Sigma\!\bigl(X_t \cup \{(q, \ell)\}\bigr) - \Sigma(X_t)$$

where $\Sigma(\cdot)$ is a bilateral symmetry functional over $\mathcal{S}$. Negative $\beta_{\text{symmetry}}$ encodes a tendency to complete perceived symmetry axes — an aesthetic-geometric heuristic with no analog in the natural event literature.

### Void Attraction

Preference for spatially unoccupied regions:

$$f_{\text{void}}(\ell;\; X_t) = V(\ell;\; X_t)$$

where $V(\ell; X_t)$ is the area of the Voronoi cell containing $\ell$ in the configuration $X_t$. Negative $\beta_{\text{void}}$ encodes space-filling behavior. The Voronoi formulation captures the negative-space dynamics of the decision — agents respond to where shapes are not, not only where they are.

### Boundary Interaction

Avoidance of or anchoring to the domain edge:

$$f_{\text{edge}}(\ell) = d(\ell,\; \partial\mathcal{S})$$

Positive $\beta_{\text{edge}}$ encodes interior preference. Negative encodes boundary anchoring.

### Scale Coherence

Tendency toward local size matching:

$$f_{\text{scale}}(q, \ell;\; X_t) = \sum_{(q_j, \ell_j) \in X_t} |r - r_j| \cdot \kappa_h(\|\ell - \ell_j\|)$$

where $r, r_j$ are the characteristic scales of placed shapes.

---

## Mark-Induced Spatial Anisotropy

The central structural novelty distinguishing this framework from all prior marked point process work is the treatment of marks as geometric objects rather than dimensionless labels.

Each mark type carries intrinsic symmetry structure:

**Circles $(\circ)$:** Continuous rotational symmetry group $SO(2)$. No preferred axis. Isotropic spatial footprint. Overlap geometry is direction-independent.

**Squares $(\square)$:** Discrete $C_4$ symmetry. Four preferred axes at $\phi, \phi + \pi/2, \phi + \pi, \phi + 3\pi/2$. Strong alignment tendency. Overlap geometry is axis-dependent — two squares share a face differently than they share a corner.

**Triangles $(\triangle)$:** $C_3$ symmetry broken by apex directionality. Single bilateral axis. Spatial relationships between triangles depend on whether apices point toward or away from each other.

This **mark-induced anisotropy** enters the interaction energy in two ways. First, feature functions that measure alignment and overlap must respect the symmetry structure of the marks involved — $f_{\text{match}}$ for two squares is not the same functional as $f_{\text{match}}$ for two circles. Second, the orientation parameter $\phi$ becomes a latent variable whose posterior must be integrated over when comparing configurations.

The full pairwise interaction between marks at $(q_i, \ell_i, r_i, \phi_i)$ and $(q_j, \ell_j, r_j, \phi_j)$ is:

$$\mathcal{H}_{\text{pair}} = g\!\bigl(\|\ell_i - \ell_j\|,\; |r_i - r_j|,\; \phi_i - \phi_j,\; q_i,\; q_j\bigr)$$

where $g$ is a function that must be specified differently for each pair type $(q_i, q_j) \in \mathcal{Q}^2$. There are $|\mathcal{Q}|^2 = 9$ distinct pairwise interaction functions. The isotropic approximation — treating all mark interactions as radially symmetric — discards the anisotropy and loses information about the alignment and orientation tendencies that are among the most cognitively significant features of human geometric placement behavior.

---

## Stigmergic Coordination Structure

The coordination mechanism in this system is structurally distinct from all other multi-agent models in the literature.

In **direct coordination** models (game theory, social networks, Schelling segregation), agents respond to each other's states, strategies, or positions. Remove the other agents and coordination dissolves.

In **broadcast coordination** models (cultural transmission, iterated learning), agents receive signals from a central or distributed source and align their behavior accordingly.

In this framework, agents **never interact**. No agent observes another agent. No signal is broadcast. No strategy is communicated. Coordination is mediated entirely through modifications to a shared physical object:

$$\text{agent}_t \;\to\; \text{reads } X_t \;\to\; \text{produces } (q_{t+1}, \ell_{t+1}) \;\to\; X_{t+1} = X_t \cup \{(q_{t+1}, \ell_{t+1})\}$$

This is stigmergy in the precise technical sense: indirect coordination through a modified environment. The shared surface is not a communication channel between agents — it is a computational state that each agent reads and modifies independently, without awareness of the other agents who read and modified it before.

Three properties of this coordination structure are unprecedented in the formal spatial statistics literature:

**Asymmetric information.** Each agent has complete information about the configuration at the time of their action and zero information about anything else — not prior agents' identities, not the instruction given to them, not the sequence of decisions.

**Irreversibility.** Every modification is permanent. The coordination medium accumulates decisions without forgetting any. The artifact is a monotone function of history.

**Emergent global structure without global information.** The final configuration $X_n$ reflects aggregate behavioral tendencies across $n$ agents, none of whom had access to those aggregate tendencies when making their decision. Global structure emerges from local stigmergic interaction, not from any agent's global intention.

---

## Evolutionary Grounding

The capacity for approximate Gibbs sampling over spatial configurations is not a recently acquired cognitive ability. The neural architecture for integrating spatial information, evaluating geometric compatibility, and producing placement decisions was substantially complete in anatomically modern humans 300,000 years before the present.

The developmental constraint preventing expression of this capacity at full theoretical resolution was not genomic. It was environmental: the absence of a shared surface, a controlled instruction set, a measurement system capable of recording actions with full observability, and an inference framework capable of recovering the energy function from the recorded actions.

All four constraints are simultaneously removed in the experimental design this framework specifies. The experiment does not create a new cognitive capacity. It creates, for the first time, the conditions under which an existing 300,000-year-old cognitive capacity can be formally characterized.

The specific capacity being characterized — the ability to evaluate spatial compatibility of geometric objects against a complex context — is one of the oldest and most evolutionarily conserved cognitive operations in the hominin lineage. Tool placement, nesting site selection, territorial marking, cache placement: all are instances of the same decision-theoretic problem this framework formalizes. The experiment brings this capacity into the laboratory under conditions of maximal observability.

---

## Parameter Estimation

Given observed action sequence $\{(q_t, \ell_t)\}_{t=1}^n$ with associated field states $\{X_{t-1}\}_{t=1}^n$, the parameters $\boldsymbol{\beta} = (\beta_1, \dots, \beta_K)$ are estimated by **maximum pseudolikelihood**:

$$\hat{\boldsymbol{\beta}} = \underset{\boldsymbol{\beta}}{\arg\max}\; \sum_{t=1}^{n} \Bigl[\log \lambda(q_t, \ell_t \mid X_{t-1};\; \boldsymbol{\beta}) - \log \mathcal{Z}(X_{t-1};\; \boldsymbol{\beta})\Bigr]$$

The partition function $\mathcal{Z}(X_{t-1}; \boldsymbol{\beta})$ is approximated by discretizing $\mathcal{S}$ into a fine grid and summing over grid points:

$$\mathcal{Z}(X_{t-1};\; \boldsymbol{\beta}) \approx \sum_{q' \in \mathcal{Q}} \sum_{j=1}^{J} \exp\!\bigl(-\mathcal{H}(q', \ell_j;\; X_{t-1};\; \boldsymbol{\beta})\bigr) \cdot \delta_{\mathcal{S}}$$

where $\delta_{\mathcal{S}}$ is the grid cell area and $J$ is the number of grid points.

Pseudolikelihood methods for spatial Gibbs processes were established by Besag (1977) and extended to marked processes by Baddeley, Rubak, and Turner (2015). Under mild regularity conditions — correct model specification, spatial coverage, sufficient sample size — $\hat{\boldsymbol{\beta}}$ is consistent and asymptotically normal.

### Identifiability Conditions

| Condition | Requirement |
|---|---|
| Sample size | $n \geq 30$ actions per experimental instance |
| Spatial coverage | actions distributed across $\mathcal{S}$, not concentrated |
| Mark diversity | all three mark types present in the sample |
| Field variation | configuration must evolve substantially across observation indices |
| Replication | multiple independent instances for out-of-sample validation |

### Model Selection

Competing energy specifications ranked by:

$$\text{AIC} = 2K - 2\hat{\ell} \qquad \text{BIC} = K\log n - 2\hat{\ell} \qquad \text{WAIC}$$

where $K$ is the number of free parameters and $\hat{\ell}$ is the maximized pseudolikelihood.

---

## Candidate Mechanisms

| Mechanism | Active Feature | Sign | Predicted Structure |
|---|---|---|---|
| Complete spatial randomness | none | — | uniform, unstructured |
| Aggregation | $f_{\text{density}}$ | $\beta < 0$ | clustered groups |
| Regular spacing | $f_{\text{density}}$ | $\beta > 0$ | inhibition lattice |
| Mark segregation | $f_{\text{match}}$ | $\beta < 0$ | same-type clusters |
| Mark interleaving | $f_{\text{match}}$ | $\beta > 0$ | alternating types |
| Symmetry completion | $f_{\text{symmetry}}$ | $\beta < 0$ | bilateral axes |
| Space-filling | $f_{\text{void}}$ | $\beta < 0$ | even spatial coverage |
| Boundary anchoring | $f_{\text{edge}}$ | $\beta < 0$ | peripheral concentration |
| Composite | multiple | signed | superposition of above |

---

## Simulation and Validation

Fitted parameters generate **synthetic collective trajectories** by sequential sampling from the estimated intensity:

$$X_0 = \emptyset, \qquad (q_{t+1}, \ell_{t+1}) \;\sim\; \frac{\exp(-\mathcal{H}(q, \ell;\; X_t;\; \hat{\boldsymbol{\beta}}))}{\mathcal{Z}(X_t;\; \hat{\boldsymbol{\beta}})}$$

Synthetic and observed fields are compared on spatial point process summary statistics:

| Statistic | Measures |
|---|---|
| $K(r) = \lambda^{-1}\,\mathbb{E}[\text{events within distance }r]$ | overall clustering / inhibition |
| $g(r) = K'(r)/2\pi r$ | pairwise distance structure |
| $G(r)$ nearest-neighbor distribution | local proximity |
| $M_{qq'}(r)$ mark connection function | same-type co-occurrence by distance |
| $\Sigma(X)$ symmetry index | bilateral balance |
| $\text{CV}(V)$ Voronoi area variation | spatial regularity |

The model that minimizes discrepancy between observed and simulated statistics — averaged across all statistics and replicated trajectories — identifies the most plausible behavioral mechanism.

---

## Experimental Design

### Staged Progression

Each level isolates one additional latent variable:

| Level | Task | Variable Isolated |
|---|---|---|
| 1 | Place a single shape | individual mark emission distribution |
| 2 | Place two shapes, same type | same-class relational geometry |
| 3 | Place two shapes, different types | cross-class integration strategy |
| 4 | Select from shape bank, place once | categorical choice without motor production |
| 5 | Sequential shared field, one shape per agent | collective transition kernel $K$ |

### Minimum Viable Implementation

**Materials:** Shape bank (circle, square, triangle templates) · One shared surface, initially blank · Coordinate recording system

**Instruction:**
> Choose one shape and place it anywhere on the surface.

**Record per action $t$:**
```
t        : order index
q_t      : shape type ∈ {circle, square, triangle}
ℓ_t      : placement coordinate (x, y)
X_{t-1}  : field state snapshot before action
```

**Estimation:**
$$\hat{\boldsymbol{\beta}} = \underset{\boldsymbol{\beta}}{\arg\max}\; \sum_t \log P(q_t, \ell_t \mid X_{t-1};\; \boldsymbol{\beta})$$

**Validate** via simulation and field statistic comparison.

---

## Position at the Research Frontier

The 2024–2025 literature on spatial and spatiotemporal point processes has expanded the expressive power of intensity models through neural Hawkes processes, score-matching pseudolikelihood estimators, and Transformer-based intensity functions. This expansion addresses one problem: fitting more complex rate functions to observational data from natural processes where the generating agent is unobservable.

It does not address the problem this framework targets: recovering an interpretable decision rule from a collective artifact produced by deliberate cognitive agents who are directly observable.

The distinction is structural. Every neural STPP approach models a physical rate. This framework models a decision rule — the probability that a specific cognitive agent, solving an approximate Gibbs sampling problem over a #P-hard energy landscape, selects a specific action given the current configuration. The two targets require different inference objectives, different validation criteria, and different experimental designs.

No existing paper in the marked spatial point process literature — including the current SOTA extensions — combines a behavioral causal interpretation of the intensity function with a controlled sequential experiment in which actions, ordering, and field states are recorded with full observability, and with a formal treatment of marks as geometric objects whose intrinsic symmetry structure enters the interaction energy.

The 2024–2025 frontier has not addressed this combination. That is the problem this framework addresses.

---

## Relationship to Prior Frameworks

| Framework | Connection | Structural Distinction |
|---|---|---|
| Besag (1974) | Gibbs–Markov local conditional specification | Besag addresses static spatial lattice systems; this framework addresses sequential behavioral decisions conditioned on an evolving visible geometric field |
| Ripley (1988); Møller & Waagepetersen (2004); Baddeley, Rubak & Turner (2015) | spatial point process inference machinery | Classical SPP addresses natural event patterns; this framework introduces a behavioral generative process where every event is a deliberate cognitive choice |
| Schelling (1971, 1978) | minimal local rules generating global spatial structure | Schelling models agent relocation; this framework models artifact accretion — agents append, never move |
| Kirby (2008) | sequential human update systems producing emergent structure | Kirby studies symbolic transmission through imitation chains; this framework studies spatial geometric accumulation through stigmergic placement |
| Grassé (1959) stigmergy | indirect coordination via environmental modification | Grassé addresses pheromone deposition by social insects; this framework addresses human aesthetic-geometric decision-making mediated by a shared geometric surface |
| Eckardt & Moradi (2024) | marked spatial point process inference, SOTA | Eckardt & Moradi characterizes observed patterns; this framework recovers the behavioral generative rule that produced them |
| Neural STPP literature (2024–2025) | flexible intensity estimation | Neural STPPs maximize expressive power at the cost of interpretability; this framework maximizes interpretability and causal identification at a well-characterized expressiveness cost |

---

## Theoretical Summary

The framework is formally described as:

$$\boxed{X_t = \{(q_i, \ell_i)\}_{i=1}^{t} \qquad (q_{t+1}, \ell_{t+1}) \;\sim\; \frac{\exp\!\Bigl(-\displaystyle\sum_k \beta_k f_k(q, \ell;\; X_t)\Bigr)}{\mathcal{Z}(X_t)}}$$

The object of inference is the energy decomposition $\{\beta_k, f_k\}_{k=1}^K$ that best accounts for the spatial and categorical structure of observed collective artifacts.

The energy decomposition is not a statistical description of a pattern. It is a behavioral causal model: a formal statement of the decision rule that governed the deliberate cognitive choices of uncoordinated agents producing a shared geometric object under a single minimal instruction.

Understanding the decomposition reveals how locally generated, individually bounded, computationally approximate decisions accumulate through irreversible stigmergic modification of a shared surface into global spatial structure — structure that no individual agent intended, planned, or could have produced alone.

---

## Conceptual Architecture

```
minimal instruction delivered to each agent
         ↓
agent observes current field  X_t
         ↓
agent solves approximate Gibbs sampling problem
over #P-hard energy landscape
         ↓
action (q_{t+1}, ℓ_{t+1}) drawn from λ(· | X_t)
         ↓
artifact updates:  X_{t+1} = X_t ∪ {(q_{t+1}, ℓ_{t+1})}
         ↓
next agent observes X_{t+1} as complete sufficient statistic
         ↓
collective artifact X_n = emergent spatial structure
         ↓
inference: recover energy decomposition {β_k, f_k} from trajectory
         ↓
simulation: generate synthetic fields from λ̂
         ↓
validation: compare observed and simulated spatial statistics
         ↓
identification: which decision rule governed the collective?
```

---

## Foundations

| Domain | Key Works |
|---|---|
| Markov processes | Markov (1906); Feller (1968); Norris (1998) |
| Spatial point processes | Cox & Isham (1980); Ripley (1988); Møller & Waagepetersen (2004); Baddeley, Rubak & Turner (2015) |
| Gibbs–Markov spatial interaction | Besag (1974, 1977); Cressie (1993) |
| Computational complexity | Cook (1971); Valiant (1979); #P-completeness of partition functions |
| Emergent spatial structure | Schelling (1971, 1978) |
| Stigmergy | Grassé (1959); Bonabeau et al. (1999) |
| Sequential human accumulation | Kirby (2008); Boyd & Richerson (1985) |
| Simulation-based inference | Metropolis et al. (1953); Robert & Casella (2004) |
| Evolutionary cognitive science | Klein (2009); Coolidge & Wynn (2009) |
| SOTA marked SPP | Eckardt & Moradi (2024); Mukherjee et al. (2025) |
