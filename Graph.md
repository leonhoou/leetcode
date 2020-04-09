## 图：

存储方式：邻接矩阵、邻接表

广度优先搜索，深度优先搜索

```
#include <iostream>
#include <vector>
#include <queue>
#include <stack>
using namespace std;

/**
 * 图：
 * 存储方式：邻接矩阵，邻接表
 * 广度优先搜索，深度优先搜索
 */

class Graph {
public:
    Graph(int nodeNum): nodes(nodeNum), edges(nodeNum, vector<int>()) {}
    
    void addEdge(int s, int t) {
        this->edges[s].push_back(t);
    }
    
    // 搜索start到end的路径
    // 广度优先搜索
    void bfs(int start, int end) {
        if(start == end) return;
        // 我们不删掉已访问过的节点，为其设置一个标识位表示已访问
        vector<bool> visited(this->nodes, false);
        visited[start] = true;
        // 广度优先搜索需要存储每一层的节点呀
        queue<int> q;
        q.push(start);
        // 我们还需要一条记录start到end的路径
        // 我们只要记录每个节点的父节点即可
        vector<int> prev(this->nodes, -1);
        while(!q.empty()) {
            int parent = q.front(); q.pop();
            // 遍历他所有的子节点
            for(int i = 0; i < this->edges[parent].size(); ++i) {
                int child = this->edges[parent][i];
                // 可能有环，所以已经访问过的节点就不访问了
                if(!visited[child]) {
                    prev[child] = parent;
                    // 找到end节点了就倒序打印prev数组即可
                    if(child == end) {
                        print(prev, start, end);
                        return;
                    }
                    visited[child] = true;
                    q.push(child);
                }
            }
        }
        cout << "no found" << endl;
    }
    
    // 搜索start到end的路径
    // 广度优先搜索（递归）
    // 回溯思想：适合递归
    void dfsRecur(int start, int end) {
        vector<bool> visited(this->nodes, false);
        visited[start] = true;
        vector<int> prev(this->nodes, -1);
        bool found = false;
        
        dfsRecur(start, end, prev, visited, found);
        if(found) print(prev, start, end);
        else cout << "no found" << endl;
    }
    
    // 广度优先搜索（非递归）
    // 利用栈保存父节点
    void dfs(int start, int end) {
        if(start == end) return;
        vector<bool> visited(this->nodes, false);
        visited[start] = true;
        vector<int> prev(this->nodes, -1);
        
        stack<int> st;
        st.push(start);
        
        while(!st.empty()) {
            int parent = st.top(); st.pop();
            for(int i = 0; i < this->edges[parent].size(); ++i) {
                int child = this->edges[parent][i];
                if(!visited[child]) {
                    st.push(child);
                    prev[child] = parent;
                    visited[child] = true;
                    if(child == end) {
                        print(prev, start, end);
                        return;
                    }
                }
            }
        }
        cout << "no found" << endl;
    }
    
private:
    int nodes;
    vector<vector<int> > edges;
    
    // 递归打印 end<-start 的路径
    void print(vector<int> prev, int start, int end) {
        if (prev[end] != -1 && start != end) {
            print(prev, start, prev[end]);
        }
        cout << end << " ";
    }
    
    // 但是遍历过程中，如果碰到了就要提前停止
    void dfsRecur(int start, int end, vector<int>& prev, vector<bool>& visited, bool& found) {
//        if(found) return;
        visited[start] = true;
        if(start == end) {
            found = true;
            return;
        }
        // 遍历每一个子节点，并对每一个子节点进行深度搜索
        for(int i = 0; i < this->edges[start].size(); ++i) {
            int child = this->edges[start][i];
            if(!visited[child]) {
                prev[child] = start;
                // 再接着深度子节点
                dfsRecur(child, end, prev, visited, found);
            }
        }
    }
};

int main() {
    Graph* g = new Graph(5);
    g->addEdge(0, 1);
    g->addEdge(1, 2);
    g->addEdge(1, 3);
    g->addEdge(3, 4);
    g->addEdge(4, 2);
    g->dfs(0, 3);
}

```
