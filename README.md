# classicalsearchalgorithm : There are variety of search algorithms like Depth First Search, Breadth First Search, Uniform Cost Search and A* Search that can be used to solve a variety of search related problems.

Generally search problems can be divided into two sections:

Uniformed Search

Informed Search

Uinformed Search strategies have no extra information available apart from that provided in problem definition. Such problems are proceeded only by generating successive states until they reach a given goal.

Let us consider example of Route Finding algorithm. Let’s divide the states into three sections- Explored State, Unexplored State and Frontier or latest current state. We define a function called Tree Search over the state space. We expand the path as we look at new actions and the result of new action i.e. new states. We add these results into frontier. Before this we check whether we have reached the goal state. If so, then we make a choice to remove the frontier. We find the state which is at the end of the path and if it is a goal state we are done. Tree Search represents a whole family of algorithms. The difference lies in the choice we make to expand the next item of the frontier. Which path to consider first?

First algorithm to consider is Breadth-First search. It always choose the path that is shortest possible from the frontier. Let’s suppose get a tie then we use some other strategy or randomly choose any path. But we can have repeated state in this process. Tree search super imposes certain paths while backtracking the solution. We always keep track of the frontier, which is at the beginning of the set of states which we haven’t explored yet. And behind that frontier is set of explored states and ahead is unexplored states. We keep track of explored states because if we see any state that has previously occurred we can simply remove that state because we have kept track of it.

So we modify that tree search function via a graph search function to avoid repeated paths. We initialize a set as explored set and add all the explored states to it. When we expand the path we don’t add a state if we have already seen that path before using the explored set.

Now if using this strategy we somehow reached the goal state, then we don’t just end it there. But the goal test isn’t applied when we add the path to the frontier but when we remove that path from the frontier. Also it might be not the optimal path to the goal. The general tree search or graph search does not surely know that it might be the shortest path available. We can introduce an optimization to the algorithm if we know that there is no shorter path that what we produced so that it checks the state as soon as they are added to the frontier. We can change the Breadth-First Routine accordingly and it is guaranteed to find the shortest path in number of steps if it exists. But if we consider the each path costs, then it turns out that it may find a path that is not optimal.

Second algorithm is called Uniform Cost Search. It is guaranteed to find the path with cheapest total cost. The difference is we choose path based on path cost instead of choosing based on shortest paths in terms of number of lengths. The task is finished once we pop the final goal state from the frontier set.

Third algorithm is called Depth First Search. In this algorithm we always expand the path that is longest, one with most links in it.

Breadth First Search, Uniform Cost Search will always find optimal paths while Depth First Search does not find the shortest or the optimal path. Also DFS is not a complete algorithm. Meaning, if there exists a goal will the algorithm be surely able to find the goal. In DFS, if there is a infinite path, the algorithm will keep going deeper and deeper without end. However, due to storage use cases we find depth first search more efficient. As we go down deeper in the tree we need to store the frontier in the memory. In BFS, if the depth of the tree is n, then we would require 2^n storage space. UCS will also need similar number of space. For DFS, the frontier at any point of time will have only n nodes and hence will require a much smaller storage space. If we keep track of explored states then it will probably loose the benefit but without it, it surely out performs the other two algorithms in terms of storage space.

Informed Search are algorithms where we have additional information about the states, so they can rank successors based on some fitness score until they reach a desired goal. The type of knowledge that can be useful is the estimate of the distance of between the start space and the goal. We use this estimate to find the goal faster. An algorithm called Greedy Best First Search does exactly this. It expands towards the paths first that look closest towards the goal. But the problem with this algorithm is that if there exists some obstacle in between the closest appearing path, it might choose the path that is longer instead of considering states that are closer from the goal. So we need an algorithm that combines both greedy and uniform cost search approach which is guaranteed to find the shortest path.

So the next algorithm that comes in line is A* search. Basically what the algorithm does is that at any state, it tries to minimize the sum of path cost to that state and expected distance to the goal state from that particular state. In this way it can keep the paths short and also be able to find the goal. In this way it finds the shortest path in the minimum number of ways possible. Now the second term in minimization is a heuristic like in case of route finding problem, it can be made as the estimated straight line distance between the goal and current state.

Some other problems that can be solved using search techniques are Pack man, Sliding blocks puzzle or 15 Puzzle problem.

Let us consider the 15 Puzzle problem. You can read more about the problem here. So we have a goal state or a configuration in this case we want to reach. We are given a random configuration of the board. We can have different heuristics that we can use for this problem.

First heuristic h1, let us consider number of misplaced boxes out of the 15 boxes present. Assume this value equal to h1. The second heuristic h2 equals the sum of the distance the each block will have to move to reach to the right distance. Now both of the heuristics are admissible.

Now if you think about it h2 is always greater than h1. This means, if A* search using h2 as a heuristic then it would certainly expand less number of paths than if we chose h1. To assure this statement let us consider another heuristic h3 that has precise cost at every node. Now using this heuristic we would expand the least number of nodes. On the other hand if there is a heuristic h4 that has cost equal to zero, then it would take the most number of nodes of all possible heuristics. Hence h2 will take less number of paths than h1 to reach the desired goal.

But in all these cases we had to provide our own heuristics. Although this algorithm may seem intelligent, some might argue that the real intelligence comes from the heuristics which we had given. So instead we should try to automatically come up with good heuristics.

For this matter in hand, we can come up with a program that can find good heuristics specified a problem and it’s goal. For example in the above sliding block problem if the problems says that we can move the block from A position to B position, given B is empty and is adjacent to A. So if we remove the first condition the B is empty then this is equivalent to heuristic h2, while if we remove second condition that is adjacent to A then it is heuristic h1. So both of the heuristics can be derived from the problem statement. Another good way to come up with a new heuristic would be that h = max{h1, h2}. And this will be also admissible and will be better than both algorithms since it has a greater value. The only demerit would be that we would need pay some extra cost to compute such definition and could take a longer to compute even if we expand less number of paths.

Okay. All said and done. Now if you want to implement the above algorithms instead of talking in terms of paths, we should rather talk in terms of nodes. A node is a data structure and for the above problems it has four fields, State at the end of a path, Action needed to get there, Total Cost, and the parent is the pointer to another node.

This creates a linked list of nodes representing the path for our problem. We have defined Frontiers and Explored list in above sections. These data structures will deal with nodes. In Frontier we pop the best element and subsequently add new ones. Hence we should try to implement it as a Priority Queue. Also we need to have a additional of a membership test. Is a new element in the frontier? This can be represented as a set which can be built from a hash table or a tree structure. In case of Explored set, we need to elements and check for membership which can be represented as a single set and can be done with hash tables or tree.

Finally, it is important to note that we can use these algorithms discussed above in cases where — The state space is fully observable, actions are known to us and are finite in number, result of choosing such actions should also be deterministic, and the state space should be static i.e. apart from the actions we take the state cannot change on its own.
There are many classical search algorithms that can be used to design intelligent agents to work on multitude of problems in search domain.
For reading more about the state of the art search algorithms check this link.

This blog post is an overview and my understanding from Udacity’s Artificial Intelligence Nanodegree’s Classical Search section.

Programming
AI
