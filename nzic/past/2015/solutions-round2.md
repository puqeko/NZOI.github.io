---
title: 2015 Round 2 Solutions
layout: nzic_page
nzic_weight: -1
---

# NZIC 2015 Round 2 Solutions

There were 4 problems worth a total of 400 points.

## Missing Totals

_Author: Ben Anderson, Preparation: Edwin Flores_

This was a simple problem. For each line, take the difference and add it to the total cost if it is a positive price.

## Passport Control

_Original Idea: Ben Anderson, Author: Ronald Chan_

There are multiple ways to solve this problem. A naive approach would be to find the next eligible person in line and remove them from the array. However, this takes quadratic time and only gets 50%.

To solve this in linear time, there are two ways. The first way is to maintain 3 different queues/arrays, and for each desk, find the first person who would be in line. To do this, for each person, store their passport country, number, and also their initial place in line. That way, when checking the 3 queues, we can find which of the 3 people should be next.

The second way is to maintain a single array, and 3 pointers, representing the 3 types of desks. As we perform linear search for each desk, we also move its pointer, so that we know where we can resume the search next time. We should also keep track of the people who have already left the queue. When a desk is available, we start searching using its pointer for the first eligible person who has not already left the queue. Then we mark this person as having left the queue.

## Compositeness of Numberland

_Author: Ronald Chan_

It is reasonably easy to get some points on this problem, but relatively difficult to score full marks.

A simple way to solve the problem is to simply iterate through the numbers A to B, and using trial division, find its prime factors. However, this only scores 45% for a quadratic time algorithm.

Instead of this straight-forward method, another way is to find how many numbers between A and B is a multiple of each prime number. For any prime number, we can find the first and last multiple in the range A to B, and there are (max(0,B-i)/i - max(0,A-i-1)/i) of these (where / means integer division).

To speed up the algorithm, we need to use the Sieve of Erathosthenes to find all the prime numbers up to B/2\. To optimize, when sieving with a prime p, you only need to set integers to non-prime starting with p^2, and jumping 2p at a time.

While this is fast enough, it may be necessary to consider memory usage. To perform the sieve, we need an array with a size of 5 million, which fits into 32MB with 4 bytes per number. However, if we sieve up to 10 million, we need to use 1 byte booleans. If you are using an interpreted language, you may need to set individual bits in an integer to save memory.

## Location, Location, Location

_Author: Ronald Chan_

If you know how to do this problem, it is relatively easy to code. This is a type of shortest path problem, in which we might need the shortest path between many different pairs of vertices. This can be done using Floyd-Warshall, which takes O(N^3) time.

Once we have found the shortest path between all pairs of vertices, we can test if any pair of vertices might be the optimal locations for the 2 new branches. Since it takes O(N) time to test one pair of locations (for each intersection/vertex, we find the minimum distance to any of 3 branch locations), overall, this step takes O(N^3) time.

The O(N^3) time algorithm is fast enough to score full marks.

If you used Dijkstra of Bellman-Ford instead of Floyd-Warshall, then you would have scored only 20%, because they are too slow for the largest problems. The 2nd subtask can be solved using breadth-first search to find the shortest paths. The 4th subtask can be solved with depth-first search. Both bfs and dfs solves the single source shortest-path problems in O(E) time, where E is the number of edges, and in this case, this can be O(N^2), if N is the number of vertices, so they are as fast as Floyd-Warshall in the specific types of graphs in those subtasks.
