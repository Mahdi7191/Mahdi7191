
# Advanced Code Samples for Heavy Tasks

This repository contains advanced and optimized code snippets suitable for heavy computational tasks, data processing, and performance-critical applications.

---

## 1. Python: Parallel Data Processing using multiprocessing

```python
import multiprocessing
import time

def worker(num):
    print(f"Worker {num} started")
    time.sleep(2)
    print(f"Worker {num} finished")
    return num * num

if __name__ == "__main__":
    with multiprocessing.Pool(processes=4) as pool:
        results = pool.map(worker, range(8))
    print("Results:", results)
```

---

## 2. Python: Efficient Large File Line Count with Generator

```python
def count_lines(filename):
    with open(filename, "r") as f:
        return sum(1 for _ in f)

print(count_lines("large_file.txt"))
```

---

## 3. C++: Dijkstra's Algorithm for Shortest Path in Graph

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

typedef pair<int, int> pii;

vector<int> dijkstra(int start, vector<vector<pii>>& graph) {
    int n = graph.size();
    vector<int> dist(n, numeric_limits<int>::max());
    dist[start] = 0;

    priority_queue<pii, vector<pii>, greater<pii>> pq;
    pq.push({0, start});

    while (!pq.empty()) {
        int cost = pq.top().first;
        int u = pq.top().second;
        pq.pop();

        if (cost > dist[u]) continue;

        for (auto& edge : graph[u]) {
            int v = edge.first;
            int w = edge.second;

            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }

    return dist;
}

int main() {
    int n = 5;
    vector<vector<pii>> graph(n);
    graph[0].push_back({1, 10});
    graph[0].push_back({3, 5});
    graph[1].push_back({2, 1});
    graph[3].push_back({1, 3});
    graph[3].push_back({2, 8});
    graph[3].push_back({4, 2});
    graph[4].push_back({2, 4});
    graph[4].push_back({0, 7});

    vector<int> dist = dijkstra(0, graph);

    for (int i = 0; i < n; i++) {
        cout << "Distance from 0 to " << i << " is " << dist[i] << endl;
    }

    return 0;
}
```

---

## 4. Python: Dynamic Programming - Longest Increasing Subsequence

```python
def length_of_LIS(nums):
    if not nums:
        return 0

    dp = [1] * len(nums)

    for i in range(len(nums)):
        for j in range(i):
            if nums[i] > nums[j]:
                dp[i] = max(dp[i], dp[j] + 1)

    return max(dp)

print(length_of_LIS([10, 9, 2, 5, 3, 7, 101, 18]))  # Output: 4
```

---

## 5. JavaScript: Web Worker for Heavy Computation

```javascript
// main.js
const worker = new Worker('worker.js');

worker.postMessage(1000000000);

worker.onmessage = function(event) {
  console.log('Result:', event.data);
};

// worker.js
self.onmessage = function(event) {
  let count = 0;
  for (let i = 0; i < event.data; i++) {
    count += i;
  }
  postMessage(count);
};
```
