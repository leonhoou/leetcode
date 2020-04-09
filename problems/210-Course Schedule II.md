## Course Schedule II

[LeetCode 210](https://leetcode.com/problems/course-schedule-ii/)

思想：拓扑排序

一个有向无环图，要求输出所有节点的一个线性序列。

要求：

1. 每个顶点出现且只出现一次；

2. 每个定点若存在一条从顶点 A 到顶点 B 的路径，那么在序列中顶点 A 出现在顶点 B 的前面。

## 解法一：BFS

这是一个通俗写法，耗时的地方在修改入度时要遍历每一个边，

改进：空间换时间，记录以该节点指向其他节点的一个结构。

```
class Solution {
public:
    // 拓扑排序：必须是有向无环图
    // 广度优先遍历：遍历每一层入度为0的节点
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> res;
        if(numCourses < 1 || prerequisites.size() < 1) {
            return res;
        }
        // 初始化每一个节点的入度为0
        vector<int> nodeInDegree(numCourses, 0);
        // 遍历所有的边，修改每一个节点的入度
        int nodeIdx = 0;
        for(auto prerequisite : prerequisites) {
            nodeIdx = prerequisite[0];
            nodeInDegree[nodeIdx] ++;
        }
        queue<int> q;
        // 入度为0的节点入队列
        for(int i = 0; i < numCourses; ++i) {
            if(nodeInDegree[i] == 0) {
                q.push(i);
            }
        }
        while(!q.empty()) {
            int first = q.front();
            res.push_back(first);
            q.pop();
            // 耗时的地方在这里
            // 入度为0的点输出了，修改与该节点有边的节点的入度减一
            for(auto prerequisite : prerequisites) {
                nodeIdx = prerequisite[0];
                if(prerequisite[1] == first) {
                    nodeInDegree[nodeIdx] --;
                }
                // 如果该节点的入度为0了，就入队
                if(nodeInDegree[nodeIdx] == 0) {
                    q.push(nodeIdx);
                }
            }
        }
        return res;
    }
};
```

```
class Solution {
public:
    // 这是我写的一个通俗写法，耗时的地方在修改入度时要遍历每一个边
    // 改进：空间换时间，记录以该节点指向其他节点的一个结构
    // 拓扑排序：必须是有向无环图
    // 广度优先遍历：遍历每一层入度为0的节点
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> res;
        vector<vector<int> > graph(numCourses, vector<int>());
        vector<int> inDegree(numCourses, 0);
        
        // 每个节点指向哪些节点
        for(auto prerequisite : prerequisites) {
            graph[prerequisite[1]].push_back(prerequisite[0]);
            inDegree[prerequisite[0]] ++;
        }
        
        queue<int> q;
        for(int i = 0; i < numCourses; ++i)
            if(inDegree[i] == 0)
                q.push(i);
        while(!q.empty()) {
            int first = q.front(); 
            q.pop();
            res.push_back(first);
            for(auto out : graph[first]) {
                inDegree[out] --;
                if(inDegree[out] == 0)
                    q.push(out);
            }
        }
        // 可能存在环，存在环的元素就无法输出了
        if(res.size() == numCourses)
            return res;
        return vector<int>();
    }
};
```

## 解法二：DFS

一步一步来，这是考虑无环的状况的深度优先搜索

```
class Solution {
public:
    // 深度优先搜索
    // 沿这一条路径一直走，遍历节点的所有邻接节点往下递归走
    // 前置节点肯定要放在后置节点的前面
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> res;
        vector<vector<int> > graph(numCourses, vector<int>());
        // 邻接矩阵存储图
        for(auto prerequisite : prerequisites) {
            graph[prerequisite[1]].push_back(prerequisite[0]);
        }
        vector<bool> visited(numCourses, false);
        for(int i = 0; i < numCourses; ++i) {
            dfs(graph, res, visited, i);
        }
        reverse(res.begin(), res.end());
        return res;
    }
    
    void dfs(vector<vector<int> >& graph, vector<int>& res, vector<bool>& visited, int start) {
        if(visited[start]) return;
        visited[start] = true;
        for(int i = 0; i < graph[start].size(); ++i) {
            dfs(graph, res, visited, graph[start][i]);
        }
        // 前置节点肯定要放在后置节点的前面，所以要先添加父节点
        res.push_back(start);
    }
};
```
