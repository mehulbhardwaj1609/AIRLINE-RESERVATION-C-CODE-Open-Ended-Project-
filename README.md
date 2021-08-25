# AIRLINE-RESERVATION

ABOUT:

In Airline reservation system, Passengers generally has two prefrences 
while booking flight tickets. Sometimes it become difficult to find the 
flight which is cost efficient or time efficient. 
Our project is based on this, here we give two options one for cost 
efficient and second for time efficient. Passengers can choose anyone 
of them and can book flight tickets.The program will show the shortest 
path between source and destination city according to the prefrence the 
user choose.
First there will be 3 options:

1.Cities we travel. 
2.Book your flight.
3.Print your ticket.

Here passengers can search for the flight as per their requirements and 
book the flight. Then there will be an option to print the ticket, they can 
print it easily.


TECHNIQUE:

Greedy is an algorithmic paradigm that builds up a solution piece by piece, 
always choosing the next piece that offers the most obvious and immediate 
benefit. So the problems where choosing locally optimal also leads to global 
solution are best fit for Greedy.
A greedy algorithm is an algorithmic strategy that makes the best optimal 
choice at each small stage with the goal of this eventually leading to a globally 
optimum solution. This means that the algorithm picks the best solution at the 
moment without regard for consequences.


ALGORITHM:

Here we maintain two graphs, one graph contains vertices as cities and their 
weight represent the flight cost from the two vertices and the other graph 
contain the cities as vertices in which weight represents the duration of flight. 
We used dijkstra algorithm for both the cost adjacency matrix and the time 
adjacency matrix.As the dijkstra algorithm is single source all vertices 
algorithm, but we changed it to a single source and single destination algorithm.



Algorithm Dijkstra(G,s) 
//Dijkstra's algorithm for single source shortest paths.
//Input: A weighted connected graph G = (V,E) and its vertex s.
//Output: The length d, of a shortest path from s to v and its penultimate vertex 
Pv for every 
//vertex v in V
initialise(Q)
for every vertex v in V do

 dv <- ∞; Pv <- null
 Invert(Q,v,dv)
 dv<-0:
 Vt <-Φ
 for i<-0 to [V]-1 do
 U*<-DeleteMin(Q)
 Vt <-Vt U [a*]
 for every vertex u in V- Vt that is adjacent to U* do
 if du* + w(u*,u) <du
	  du <- du*+ w(u*,u); Pu <- u*
	    Decrease(Q,u,du)


TIME COMPLEXITY:

The main advantage of Dijkstra’s algorithm is its considerably low complexity, 
which is almost linear. However, when working with negative weights, 
Dijkstra’s algorithm can’t be used.Also, when working with dense graphs, 
where is close to , if we need to calculate the shortest path between any pair of 
nodes, using Dijkstra’s algorithm is not a good option.
The reason for this is that Dijkstra’s time complexity is . Since equals almost , 
the complexity becomes .
When we need to calculate the shortest path between every pair of nodes, we’ll 
need to call Dijkstra’s algorithm, starting from each node inside the graph. 
Therefore, the total complexity will become .
• The time efficiency of Dijkstra’s depends on the data structures 
representing an input graph.
• It is in θ(|V | 2 ) for graphs represented by their weight matrix.




