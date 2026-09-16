# Learning Parts

### Erdos-Renyi model:
- __Expected Edges__: Has a probability $p$ that all edges independently uses to form an edge with:
    - then $\langle m\rangle = p\cdot n(n-1)/2$ edges; if we isolate for $p$ we get $p = 2\langle m\rangle/[n(n-1)]$. This is exactly the __density__!
- __Degree Distribution__: Follows binomial distribution; if large and sparse, then follows _Poisson_ with mean $\langle k\rangle$ (average degree); when $\langle k\rangle$ is large, then it follows approximately a _normal_.
- __Distances__: Average distance grows with $\log n$.
- __Clustering__: because neighbours link with same probability, $p$, clustering is very low.

__Watts–Strogatz__: means the network between a __lattice__ and __random__ based on the _q_ parameter that swaps links with shortcuts!

__Barabási–Albert__: means a network based on _growth_ and is called _scale-free_ as well! The growth is $$\Pi(k_i) = \frac{k_i}{\sum_jk_j}$$

__Overview__: ![Table](Table.png)

#### Giant Connected Components
- Start appearing at $p = 1/|V|$ or eqiuvalently $p = 1/n$. In fact, it grows quickly after that, which mimics real networks!


##### 2.1
1. Why did the founders of the field study random networks when they had no data? Name two reasons. And why do we still keep the model around now that we have all the data in the world?
    - First, it has properties that are easily verifiable, and second you could expand the networks without having to gather data; you could analyze them for n->infinity. We keep this model around, because it still has nice properties that are good for understanding or making baselines, but also highlights the differences that make real networks, well, real! Also, the giant components are also present in the random graph model, just like in real life.
2. The giant component appears at $\langle k\rangle=1$. Explain the intuition: why exactly one? (Think about what happens to a fragment when its nodes have, on average, more than one link each versus less than one.) What does the network look like on either side of the transition, and at what $\langle k\rangle$ does the last isolated node typically vanish?
    - Because, if it is below $\langle k\rangle < 1$, then we have on average less than 1 (so 0) links to other nodes in the network. If we take the limit of infinity nodes, then the fraction of nodes with any links would be 0! Conversely, if it is above 1, we start seeing more and more nodes in the giant components, and the fraction of the nodes in it will go towards 1 as the average degree increases!.It seems to disappear at around 4 or 5 average degree. This is related to $\langle k\rangle = \ln n$
3. Sketcings
4. A random network with the Marvel network's n and m has, on average, essentially no isolated nodes (the expected number is n $e^{−⟨k⟩}\approx0.02$). The real network has 17. Which of the two facts is the more informative, and what does the real network's 17 isolates tell you that its $\langle k\rangle$ does not?
    - If I understand the question correctly, then I think the most informative one is the real on, because the the real one is a real network, so it is more informative. The 17 isolates tell us, that the random network is not conforming to reality, that there will be heavy tails in the distribution of degrees!
5. $G(n,p)$ with $n=6$ and $p=0.2$: expected number of links? Expected degree? Probability that a given node is isolated? Now the expected number of links for $n=300$, $p=0.03$ - check it against the Marvel $m$.
    - Links: $p\cdot n(n-1)/2 = 0.2\cdot 6\cdot 5/2 = 0.2\cdot 30 / 2 = 0.2\cdot 15 = 3$.  
    Expected degree is then $p(n-1) = 0.2\cdot 5=1$.  
    The probability that a node is isolated is that it chooses none of the connections to others so $(1-0.2)^5 = 0.32$.  
    Expected number of links for 300 and 0.03: $p\cdot n(n-1)/2 = 0.03\cdot 300\cdot 299/2 = 1345.5$. This is very close the real one!


## Small Worlds
Taking one step, you reach $\langle k\rangle$ nodes, then $\langle k\rangle^2$ nodes in two steps; so in few steps, you can reach quite far in a network, $d$ steps then $\langle k\rangle^d$. Whole network covered when $n \approx \langle k\rangle^d$. Distance grows then with $d = \ln n / \ln \langle k\rangle$.


## Clustering
Clustering covers when nodes share edges with one another. "_Friend of my friend, is my friend_". __local clustering coefficient__ for node $i$ with degree $k_i$; $e_i$ counts how many of neighbours are connected with each other as well:
$$ C_i = \frac{e_i}{k_i(k_i - 1)/2} = \frac{2e_i}{k_i(k_i - 1)} $$

$C_i = 1$ if we have _clique_ and $c_i = 0$ if no one of ones neighbours know another. 

The network's average clustering coefficient $C$ is the mean of $C_i$​ over all nodes.

23rd September, Guest Lecture, Pioneer Center (social connection lecture)

#### 2.2
1) Node A's neighbors are {B, C, D}. Among them only B–C is linked. What is $C_A$​? Now add the link C–D: what is $C_A$​? Add B–D as well: what is it now?
    - In this case, we have that $C_A = \frac{1}{3\cdot 2/2} = \frac{1}{3}$ If we add the link C-D, then we increase it to $\frac{2}{3}$; if we add the last link between B and D, the graph is a clique and the clustering is 1
2) Take last week's edge list {A–B, A–C, A–D, B–C, C–D, D–E, E–F} (you drew it in exercise 1.5). Compute $C_i$ for all six nodes and the average $C$. Which nodes have $C_i​=0$ and why — is it the same reason for each?
    - For the graph we can calculate it, and get: $$ C_A = \frac{2}{3},\quad C_B = 1,\quad C_C = \frac{2}{3},\quad C_D = \frac{1}{3},\quad C_E = 0,\quad C_F = 0$$
    The reason for the two 0's is _not_ the same; 'f' can't form a clustering, but 'e' can, but it doesnt form it. The clustering for hte graph is the average:
    $$ C = \frac{\sum_i C_i}{6} = \frac{\frac{2}{3} + \frac{3}{3} + \frac{2}{3} + \frac{1}{3}}{6} = \frac{\frac{8}{3}}{6} = \frac{8}{18} = \frac{4}{9} \approx 0.44 $$
3) A node of degree 12 has $C_i​=0.5$. How many links exist among its neighbors? Now explain, in one sentence each, why (a) a hub in a social network usually has a lower $C_i$​ than a low-degree node, and (b) $C_i$​ is meaningless for a node of degree 1.
    - First, if $C_i = \frac{e_i}{k_i(k_i - 1)/2} = 0.5 = \frac{e_i}{12 \cdot 11)/2}$ then we isolate for $e_i$ and get $e_i = (0.5\cdot11\cdot12) = 33$.  
    __a)__ Hubs have lots of connections but not neccesarily in transitive relations, whereas low-degree nodes have higher chance of being in transitive relations.  
    __b)__ because with degree 1, it can't form a clustering
4) Marvel: $C\approx0.31$ but transitivity ≈0.18≈0.18. Which of the two is pulled down by the hubs, and why would the two numbers coincide in a network where every node had the same degree?
    - Hubs pull down the transitivity; transitivity doesn't exactly measure the local clustering, it simply counts trianges over triads, but hubs can have maaaany triads.

## Watts & Strogatz: perched between order and randomness
Both has Clustering And Small World Property. Random edges acts as _shortcuts_ when computing distances. A bit of randomness is nice and reflect reality.

__lattice__: every node is linked to its $l$ neighbours on either side. The paths in lattices are _long_ and grows with $n$ instead of $\log n$. Conversely, no chance is involved like the random model.

#### Idea 1: introduce random links
Can cut down the path lengths dramatically, _and_ it doesn't really affect the clustering coefficient that much. Choose some fraction $q$, of links, and re-wire them to random destinations.

#### Idea 2: $q$ is a dial
When $q=0$ we have full order, a __lattice__.  
When $q=1$ we have full random (but not the Erdos model! That is because minimum degree is the same as before!).

![Clustering And Distance](clustering_and_distance.png)

### Understanding Network Properties

![Caveman Cluster](caveman_cluster.png)

## The discovery of power laws
Heavy tails are sign of __hubs__! Highly connected nodes with interesting properties. Real networks _grow_, and it usually does so by _preferential attachment_! That means, new nodes attach to nodes with higher degree:

$$ \Pi(k_i) = \frac{k_i}{\sum_j k_j} $$
Above is the same as making a list of edge endpoints and picking uniformly at random from that. So 'A-B-C' graph would have $[a,b,b,c]$ as its list.

_Preferential attachment_ and above rule is enough to satisfy the power law for the _degree distribution_?; that is, the line for degree distribution $P(k)$ on the log-log axis fell on a straight line!

$$ P(k) = k^{-\lambda} $$

![alt text](DegreeDistLinear.png)
![alt text](DegreeDistLog.png)

So we expect it to be on a linear scale, if we have a "real" network!. When we use preferential attachkment, we see this.

#### 2.5
1. __The endpoint-list trick__: Take a four-node network with edges A–B, B–C, B–D, and C–D. Write down the flat list of all edge endpoints (every edge contributes both of its nodes). A newcomer picks one entry of that list uniformly at random (each list item with equal probability) and links to it. What is the probability that it links to B? To A? Now explain, in one sentence, why picking uniformly from this list is exactly the rule $\Pi(k_i​)=\frac{k_i}{\sum_j​ k_j}$​.
    - At the start, the list is $[a,b,b,c,c,d,d,a]$, and all share the same prob, that is $\frac{2}{8}$. It corresponds to picking uniformly, because for a node, it will have entries equal to the amount of degrees out of it. And each edge is counted for twice, so it ends up being over two times the amount of degrees. 
2) __Rich get richer, one step__: Suppose the newcomer-node E did link to B. Rewrite the list and compute B's probability of catching the next newcomer. Did it go up or down? Now suppose E had linked to A instead: what is A's share afterwards? Two sentences on why this feedback loop turns early luck into hubs.
    - In this case, we get $\Pi(k_b) = \frac{3}{10}$ which is higher than $1/4$! This is why when a node is added to an already popular node, it skews it even more towards that in the future!
3) __Kill the preference__: Change the rule to "pick an existing node uniformly at random." Write Π(ki)Π(ki​) for that rule in a network of NN nodes. Does degree matter at all? Then predict, without computing anything: after growing to 5,000 nodes under each rule, which network has the larger maximum degree, and what does each degree distribution look like on log–log axes (heavy tail or not)? One sentence each. 
    - First, the rule for preference has the highest maximum degree, because it skews the probability towards nodes with already high degree.
    - Second, the distribution of degrees for the uniform one has cut tails, dipping below the linear line, whereas the other would be looking like a line.
4) __Growth alone__: Compare the uniform-growth network with a random network G(n,m)G(n,m) that has the same nn and mm. Neither has any preference, yet they differ. Name two things that differ and say why. (Hints: in one of them the first nodes have had 5,000 rounds to collect links while the last ones had none; and think about how many connected components each has.)
    - One, the uniform growth network always adds a link, the random one might now; this is relelvant, because in uniform growth, you can't have isolated nodes; it is one giant component
    - Second, later nodes in the uniform growth one can't have more links than nodes that may come after it; that means the last node may only have 1 link, while the first one can have maaaany.

__complementary cumulative distribution__: $P(K>k)$ is the fraction of nodes with _at least_ degree $k$. It is by itself a power law, with exponent $\gamma - 1$.

It removes the need for binning.

#### 2.6


#### 2.7
1) Current degrees in a growing network: A: 5, B: 3, C: 1, D: 1. A newcomer makes one preferential-attachment link. Probability it goes to A? To D? Now the newcomer makes $m=2$ links (to two different nodes, first one preferentially, then again among the rest): probability that A gets one of them?
    - First question, it is $5/10 = 0.5$ due to weight by degree, and A has degree 5 out of the total 10.
    - Second question, we can figure it; either the first link happens to be on A, which was $1/2$, if that fails, which is equal chance, it then has a chance to be picked again, but this time the odds are a bit worse: $1/2 + 1/2\cdot 5/12 = 17/24 \approx 0.7083$.
2) After that newcomer has attached to A, the next newcomer arrives. Has A's chance of being chosen gone up or down, and by how much? Write one sentence connecting this to the phrase "rich get richer."
    - If it attached to A, then the chances in this case actually doesn't go up, as it becomes $6/12$. However, all others would have gone down, which relatively speaking means A stands stronger than the others for getting picked. I.e., the poor gets eaten.
3) Here are three degree distributions described in words. Name the model each one came from (random / Watts–Strogatz / Barabási–Albert / lattice) and say what would give it away on a plot: (a) every node has degree exactly 4; (b) a hump around 8, nothing above 20, and a bell shape on linear axes; (c) most nodes have degree 2 or 3, a few have 200.
    - a) This is the classic Lattice construction
    - b) A bell shape would signify a _random_ network! it also makes sense we would see very few above 20, if the average is 8!
    - c) This to me sounds exactly like the Barabase-Albert one, which has the power law; few with very high degree, many with low ones.
4) You double $⟨k⟩$ in a random network, keeping $n$. What happens to $C$? To the average distance? To the giant component? Now double $n$ keeping $⟨k⟩$ fixed: same three questions. Then, for Watts–Strogatz, what happens to $C$ and $⟨d⟩$ as $p$ goes from 0.001 to 0.01 — and which of the two moves first?
    - __Random Network (double ⟨k⟩)__: 
        - C: assumng a very large network, I believe it would go down, as the value $k_i$ in the denominator goes up, but $e_i$ does not neccesarily. It would flip at some point of doubling though.
        - Doubling the degree, would definitely have a positive impact on distances. If we are around $⟨k⟩=1$, then doubling has a large impact.
        - Giant Component? Grows larger!
    - __Random Network (double n)__:
        - C: It decreases.
        - Doubling the number of nodes, I see it has positive impact on the average distance, as links are formed independently, meaning more chances of adding to a component, and thus addind distance.
        - Doubling the number of nodes, I can suspect that it has a positive impact on the component size, since there are more chances of links forming.
    - __Watts-Strogatz (double ⟨k⟩)__:
        - C: Increases the clustering coefficient!
        - Doubling average degree, will impact distances negatively, i.e., they will become shorter! Since it has a lattice approach, adding to degree will allow longer jumps in 1 move.
        - Giant Component: unchanged, in WS it is all one big component anyways
    - __Watts-Strogatz (double n)__:
        - C: I am not sure it changes at all?
        - Double amount of nodes, _will_ affect the average distance as it is proportional to $n$.
        - It becomes twice as big.
5) Fill in a 3 × 3 table: rows = random / Watts–Strogatz / Barabási–Albert; columns = clustering, distances, hubs. In each cell: does the model get the real world right or wrong, and what ingredient is responsible?
    - ![Table](Table.png)

## Shuffling VS null models
We used the random model as a "baseline". As a picture of what the network would be with "nothing interesting going on".

When we use a model like that to determine for example how much more a real network has clustering, it is a __null model__.

The _null model_ needs to have the correct baseline, that is, if for centrality, we need to maintain the degree distribution of nodes. Two ways for this example:
- __Edge Swapping__: Pick two links A-B and C-D; swap such that it is A-C and B-D; repeat 1000 times. Node degree kept, links shuffled
- __Configuration Models__: This is a version of the random network, but where we force it to have a specific degree distribution. In practice it's done by giving every node as many "stubs" as its real degree, then pairing stubs up uniformly at random.

Example of _edge swapping_ on the Marvel network
> So: the random network has a clustering of 0.04. A random network with hubs has a clustering of 0.15. But the real network has C=0.32. So now we know that it's not just the hubs!

### Null Model and Statistical Test
Do above once, and you 1 number. Repeat it many times, and you can get a distribution of the values you seek. LLN says it must follow a normal distribution. Find mean and standard deviation, work out the Z-score; find p-value.

#### 2.8
Three short analyzes first, each with a flaw in the choice of baseline. For each, name the flaw and the null model that would fix it:
1) "The Marvel network's average distance (2.7) is no shorter than a random network's (2.8), so it is not a small world."
    - First, it _is_ a small world; secondly, we need to verify that the clustering is above chance; we would do a Null model check with edge-swapping, preserving the degree distribution.
2) "39% of links in the directed Marvel network are reciprocated (A links to B and B to A). In a random directed network with the same density only 3% would be, so reciprocity is 13× higher than chance."
    - The simple baseline only preserved overall density, but hubs have massive amount of in and out edges; this is not reflected, we need a edge-swap model to preserve this!
3) For the above, here are some better ones:
    - Marvel's average clustering is about 0.32, compared with 0.155 under degree-preserving edge swaps and 0.112 under the simplified configuration model, so it remains significantly higher than nulls that preserve its degree structure. 
    - For reciprocity, the right null is a directed degree-preserving swap model that keeps every node's in-degree and out-degree fixed; the 13x comparison against a density-only null is not trustworthy because hubs can create reciprocal pairs, so survival must be tested against this stronger baseline. 
    - Therefore, heavy-tailed degrees alone do not explain Marvel's clustering, while any reciprocity left after directed degree-preserving swaps would indicate structure beyond the effects of hubs.

## A null model in action: friendship paradox
_"your friends have more friends than you do"_ is true for many networks, and is known as degree sampling bias. Hubs have many connections, so of course they would skew the average.

#### 2.9
1) State the paradox precisely: which two averages are being compared, and why is the comparison biased by construction? Then, in one line of algebra: if degrees have mean $\langle k\rangle$ and variance $\sigma^2$, the mean degree of a random neighbor is $\langle k\rangle + \sigma^2/\langle k\rangle$. Use that to explain why the paradox is strongest in scale-free networks and weakest — but not absent — in random ones.
    - We compare the average node degree $\frac{2m}{n}$ to the average degree amongst a nodes neighbours; this is a sampling bias.
    - In the linear algebra one, the term $\sigma^2/\langle k\rangle$ grows as is bounded by 0; so it can only add. Therefore, in random where $\sigma^2 \approx \langle k\rangle$ it equals around 1 and vanishes somewhat, whereas in scale-free ones, with very heavy tails, it explodes!
2) __Null-model it__: run the same sampling on a degree-preserving shuffle of the Marvel network. The effect survives — explain why this null cannot kill it, and what that tells you about which network property the paradox really depends on. Then think one step further: could properties beyond the degree sequence (assortativity — do hubs link to hubs? — clustering, communities) make the paradox stronger or weaker? Reason first; test one of them if you can.