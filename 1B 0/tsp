#include <iostream>
#include <vector>
#include <bits/stdc++.h>

using namespace std;

int findMinEdge(const vector<vector<int>>& graph, int node, int n) {
    int min_cost = INT_MAX;
    for (int i = 0; i < n; i++) {
        if (graph[node][i] != 0 && graph[node][i] < min_cost)
            min_cost = graph[node][i];
    }
    return min_cost;
}

int calculateInitialBound(const vector<vector<int>>& graph, int n) {
    int bound = 0;
    for (int i = 0; i < n; i++) {
        bound += (findMinEdge(graph, i, n) + findMinEdge(graph, i, n)) / 2;
    }
    return bound;
}

void solveTSP(const vector<vector<int>>& graph, vector<bool>& visited, vector<int>& currentPath,
              int currentBound, int currentCost, int level, int n, vector<int>& bestPath, int& minCost) {
    
    if (level == n) {
        int lastToFirstCost = graph[currentPath[level - 1]][currentPath[0]];
        if (lastToFirstCost != 0 && (currentCost + lastToFirstCost < minCost)) {
            bestPath = currentPath;
            bestPath.push_back(currentPath[0]);  
            minCost = currentCost + lastToFirstCost;
        }
        return;
    }

    for (int i = 0; i < n; i++) {
        if (graph[currentPath[level - 1]][i] != 0 && !visited[i]) {
            int tempBound = currentBound;
            currentCost += graph[currentPath[level - 1]][i];

            currentBound -= (findMinEdge(graph, currentPath[level - 1], n) + findMinEdge(graph, i, n)) / 2;

            if (currentBound + currentCost < minCost) {
                currentPath[level] = i;
                visited[i] = true;

                solveTSP(graph, visited, currentPath, currentBound, currentCost, level + 1, n, bestPath, minCost);
            }

            currentCost -= graph[currentPath[level - 1]][i];
            currentBound = tempBound;
            visited[i] = false;
        }
    }
}

void travellingSalesmanProblem(const vector<vector<int>>& graph, int n) {
    vector<int> currentPath(n); 
    vector<int> bestPath;       
    vector<bool> visited(n, false); 

    int currentBound = calculateInitialBound(graph, n);  
    int currentCost = 0;    
    int minCost = INT_MAX;  

    currentPath[0] = 0;    
    visited[0] = true;      

    solveTSP(graph, visited, currentPath, currentBound, currentCost, 1, n, bestPath, minCost);

    cout << "Minimum cost: " << minCost << endl;
    cout << "Path: ";
    for (int i = 0; i < bestPath.size(); i++) {
        cout << bestPath[i] << " ";
    }
    cout << endl;
}

int main() {
    int n;
    cout<<"Enter number of cities:";
    cin>>n;
    vector<vector<int>>graph(n,vector<int>(n));
    cout<<"Enter a "<<n<<" x "<<n<<" matrix:"<<endl;
    for(int i=0; i<n; i++)
    {
        for(int j=0; j<n; j++)
        {
            cin>>graph[i][j];
        }
    }

    travellingSalesmanProblem(graph, n);

    return 0;
}
