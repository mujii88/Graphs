
from typing import List, Tuple
import heapq

class Solution:
    def dijkstra(self, adj: List[List[Tuple[int, int]]], src: int) -> List[int]:
        result = [float('inf')] * len(adj)
        heap = []
        result[src] = 0
        heapq.heappush(heap, (0, src))

        while heap:
            distance, node = heapq.heappop(heap)

            for neighbor, weight in adj[node]:  # Unpacking correctly
                if distance + weight < result[neighbor]:  # Using correct weight
                    result[neighbor] = distance + weight
                    heapq.heappush(heap, (result[neighbor], neighbor))
        
        return result



from typing import List
import heapq

class Solution:
    def shortestPath(self, n: int, m: int, edges: List[List[int]]) -> List[int]:
        # Initialize adjacency list
        adj = {i: [] for i in range(1, n + 1)}
        for u, v, w in edges:
            adj[u].append((v, w))
            adj[v].append((u, w))
        
        # Distance array, parent array, and priority queue
        result = [float('inf')] * (n + 1)
        parent = [i for i in range(n + 1)]
        heap = []
        
        # Start from node 1
        result[1] = 0
        heapq.heappush(heap, (0, 1))
        
        while heap:
            dis, node = heapq.heappop(heap)
            
            
            # Explore neighbors
            for neighbor, weight in adj[node]:
                if dis + weight < result[neighbor]:
                    result[neighbor] = dis + weight
                    heapq.heappush(heap, (result[neighbor], neighbor))
                    parent[neighbor] = node
        
        # Check if the last node is unreachable
        if result[n] == float('inf'):
            return [-1]
        
        # Reconstruct the path
        path = []
        current = n
        while parent[current] != current:
            path.append(current)
            current = parent[current]
        path.append(1)
        path.append(result[n])
        
        
        # Reverse to get the path from 1 to n
        return path[::-1]