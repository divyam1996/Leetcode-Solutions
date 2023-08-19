class DisjointSet {
    vector<int> parent, size;
public:
    DisjointSet(int n) {
        parent.resize(n+1);
        size.resize(n+1);
        for (int i=0; i<=n; i++) {
            parent[i] = i;
            size[i] = 1;
        }
    }
    int findUPar(int node) {
        if (node == parent[node]) {
            return node;
        }
        return parent[node] = findUPar(parent[node]);
    }
    void unionBySize(int u, int v) {
        int ulp_u = findUPar(u);
        int ulp_v = findUPar(v);
        if (ulp_u == ulp_v) {
            return;
        }
        if (ulp_u < ulp_v) {
            parent[ulp_u] = ulp_v;
            size[ulp_u] += size[ulp_v];
        } else {
            parent[ulp_v] = ulp_u;
            size[ulp_v] += size[ulp_u];
        }
    }
};

class Solution {
    int kruskal(int n, vector<vector<int>>& edges, int skip, int prev = -1) {
        DisjointSet ds(n);
        int mst_weight = 0;
        if (prev != -1) {
            mst_weight += edges[prev][2];
            ds.unionBySize(edges[prev][0], edges[prev][1]);
        }
        for (int i=0; i<edges.size(); i++) {
            if (i == skip) {
                continue;
            }
            int u = edges[i][0];
            int v = edges[i][1];
            int wt = edges[i][2];
            if (ds.findUPar(u) == ds.findUPar(v)) {
                continue;
            }
            ds.unionBySize(u, v);
            mst_weight += wt;
        }
        for (int i=0; i<n; i++) {
            if (ds.findUPar(i) != ds.findUPar(0)) {
                return INT_MAX;
            }
        }
        return mst_weight;
    }
public:
    vector<vector<int>> findCriticalAndPseudoCriticalEdges(int n, vector<vector<int>>& edges) {
        for (int i=0; i<edges.size(); i++) {
            edges[i].push_back(i);
        }
        sort(edges.begin(), edges.end(), [](const vector<int>& a, const vector<int>& b) {
            return a[2] < b[2];
        });
        int original_mst = kruskal(n, edges, -1);
        vector<int> critical, non_critical;
        for (int i=0; i<edges.size(); i++) {
            if (original_mst < kruskal(n, edges, i)) {
                critical.push_back(edges[i][3]);
            } else if (original_mst == kruskal(n, edges, -1, i)) {
                non_critical.push_back(edges[i][3]);
            }
        }
        return {critical, non_critical};
    }
};
