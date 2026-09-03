# Graphs introduction

Graph: $n$ nodes, $m$ edges  
Node degree: $k_n = $#edges from/to node   
Average degree $\langle k\rangle = 2m/n$  
Max edges = $n(n-1)/2$  
Network density = $2m/[n(n-1)]$  

Path: edges that join two nodes
Distance: the _shortest_ path(s)

Undirected: adjacency matrix is _symmetric_.
Simple network: max 1 edge between pairs, no self loops (diagonal 0 in adj matrix)

## 1.1 - Did you really read it?
1. **List three real networks and state the nodes and the edges for each. Then, for each: directed or undirected? Weighted or unweighted? What question would force you to add weights?** 
    1. Wikipedia Network. The nodes are different articles, the edges are then different links between said articles. It is a _directed_ but _unweighted_ network. It may be able to be _weighted_ if you count the amount of links to the same page it has, but it would be a really sparse one.
    2. Scientific Articles. The nodes could be authors, edges then co-authors and the weight on it then how many papers they co-authed together. It would be _undirected_ but _weighted_. In this case, the weight is how many co-authed papers.
    3. Same as above, but we switch it around to be articles as nodes, and links would be citations. Now _directed_ but _unweighted_.

2. **Pick a network you personally care about — a fourth one. What are its nodes and edges? Roughly how large is it? Can it actually be mapped (is the data available), and does it change over time? Is something flowing or spreading on it? Why do you care?**
    - I personally really like database networks. In a sense, if you have a database, it can be visualized as a network, where each node would be a table, and each edge is then a connection to another table through foreign keys. It would require _node features_ and _edge features_ to be complete, but it is cool. It would change over time, as it is constantly changing, and may get new tables. 
3. **The representation question we just discussed: describe one system that can be cast as a network in two genuinely different ways (different node choice, not just different data). Ask a question each representation answers that the other cannot.**
    - I already touched upon this, but I see the example was already shown. I will choose another.

## 1.2
I asked about what nodes/edges are, node features, edge features, and how often and why it could change.
- Node examples: Users, Orders, Order_Items, Products, and Payments
- Edge examples: Foreign-key relationships connecting tables.
- Node features: 
    - Scale: Row count (cardinality) and total disk footprint (MB/GB).
    - Activity: Read vs. write traffic (QPS), average update frequency.
    - Structure: Column count, primary key data type, index count.
- Edge features:
    - Relationship cardinality: 1:1, 1:N, or N:M (via junction table).
    - Constraint logic: Cascade behavior (ON DELETE CASCADE, SET NULL, RESTRICT).
    - Join frequency / cost: How often query optimizer executes joins over this foreign key, join selectivity, and presence of a supporting index on the foreign key column.
- Why it can change:
    - **Schema Evolution** (Infrequent, e.g., weekly or monthly releases):
    - **Operational Drift** (Continuous, e.g., real-time to hourly): Node Volume Shift: An active marketing campaign balloons the row counts, Edge Weight / Traffic Shift: Read/write bottlenecks and join volumes migrate across edges.
- What looks like:
    - **Adding a feature:**: adding new features.
    - **Denormalization / Splitting:**: changing nodes as one may split.
    - **System Bottlenecks:** bottlenecks and latencies.

**Grade every answer against a source you trust. Report the score as a fraction, and classify the failures: plainly wrong, subtly wrong, or confidently unverifiable?**
- A graph database is already a thing, so it is already heavily verifiable the starting parts. Node features and edge features I find less verifiable, for example the join frequency and costs. That can change, depending on te joins.

**One paragraph: given that error profile, what would you let this tool do unsupervised, and what would you always verify? Keep the paragraph.**
- I would always verify most input, but just reading through it glance-style, but I would probably let a tool unsupervised.


## 1.3 - Toolbox shakedown
I would probably not have thought or found out if it had a small mistake in the edge _directions_ if it were directed, not if it had left single edges out. I would probably also trust the agent to use the built-in parts of `networkx`.

# Power Binning
Sometimes you want to bin your degree distributions, as it is heavy tailed (few nodes with many, many edges, but many nodes with few). If you used equally sized binning, some would be super sparse, and others much more volume. If we use _power binning_, we start with small binning sizes, and then increase it.

## 1.4
1. I think the one who creates links intention is to write a link into the page, this will increase both the in-degree at the point of writing, but an out-degree somewhere. So in this case, in-degree has a much higher ceiling, as it is a count of how many pointers there are to it, where as out-degrees are deliberate actions. It takes effort to increase from some actor

## 1.7
1. **Flip through force, circle A–Z, circle by degree and random. For each of the following, does it change when the layout changes? The number of nodes; the number of edges; Spider-Man's degree; how far apart two characters sit on the screen; the network distance (Part 5) between the same two characters. Sort the five into data and decoration.**
    - The number of nodes, nor number of edges, does not change; Nothing changes but the visual layout really.
2. **In circle A–Z, two characters sit right next to each other on the rim. What, if anything, does that tell you about whether they are connected? Now switch to circle by degree: what does this layout let you read off that A–Z does not — and what is the only piece of information any circle layout adds to the drawing?**
    - It really does not tell about something. Circle degree does, however, as it changes the layout to be based on degree; two character next to each other has similar degrees! Any layout only adds
3. **In the force layout, pick two nodes that sit close together. Give two different reasons they might be close — one that is about the network, one that is not. Then hover a hub: are its neighbours all near it? What does that tell you about how much to trust "close on screen"?**
    - One reason they might be close, due to the network, is that they have similar degree. Because they have similar degree, they are close. High degree --> center, less --> edge. However, it does not mean close nodes are closer together, as it simply is an act of force. 
4. **Is the random layout wrong? Think of something it is good for (hint: it is the drawing you would get if position carried no information at all — a baseline). What does force show you that random cannot, and what does it tempt you to over-read?**
    - Random layout is not wrong at all, it just not does carry much information we can glean from it. Force shows degree more easily as a relative: more towards center --> higher degree. 
5. **Turn the community colours on and off in each layout. Which layout makes the communities easiest to see, which hides them completely, and why does the colour survive every layout while the visual grouping does not? Finish with a three-sentence critique of one layout as a data visualization: what it makes visible, what it hides, and one wrong conclusion a reader might draw from it.**
    - Only really circle by community makes it easy to gleam any community. I want to critique the "A-Z grouping"; it seems to hide any community and sense of degree (though it does show on node size), it hides community, and it may give the reader a wrong conclusiong about exactly the community part. On a positive note, it may actually be a heuristic.