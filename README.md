
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