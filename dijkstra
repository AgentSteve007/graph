#include <iostream>
#include <vector>
#include <queue>
#include <limits>
#include <unordered_map>

using namespace std;

// Структура для представления ребра графа
struct Edge {
    int to;      // Конечная вершина
    int weight;  // Вес ребра
};

using Graph = vector<vector<Edge>>;

void addEdge(Graph& graph, int from, int to, int weight) {
    graph[from].push_back({ to, weight });
    graph[to].push_back({ from, weight }); // Удалить эту строку, если граф направленный
}

// Функция для нахождения кратчайшего пути (алгоритм Дейкстры)
vector<int> dijkstra(const Graph& graph, int start, int target) {
    int n = graph.size();
    vector<int> distances(n, numeric_limits<int>::max()); 
    vector<int> previous(n, -1);                      
    distances[start] = 0;

    using Node = pair<int, int>;
    priority_queue<Node, vector<Node>, greater<Node>> pq;
    pq.push({ 0, start });

    while (!pq.empty()) {
        int currentDist = pq.top().first;
        int currentNode = pq.top().second;
        pq.pop();
        if (currentNode == target) break; 
        if (currentDist > distances[currentNode]) continue;
        for (const Edge& edge : graph[currentNode]) {
            int neighbor = edge.to;
            int newDist = currentDist + edge.weight;

            if (newDist < distances[neighbor]) {
                distances[neighbor] = newDist;
                previous[neighbor] = currentNode;
                pq.push({ newDist, neighbor });
            }
        }
    }
    vector<int> path;
    for (int at = target; at != -1; at = previous[at]) {
        path.push_back(at);
    }
    reverse(path.begin(), path.end());

    // Если путь не ведет к стартовой вершине, значит пути нет
    if (path.size() == 1 && path[0] != start) {
        return {};
    }
    return path;
}

int main() {
    int n, m;
    cout << "Введите количество складов (вершин графа): ";
    cin >> n;
    cout << "Введите количество маршрутов (ребер графа): ";
    cin >> m;

    Graph graph(n);

    cout << "Введите маршруты в формате: склад1 склад2 стоимость\n";
    for (int i = 0; i < m; ++i) {
        int u, v, w;
        cin >> u >> v >> w;
        addEdge(graph, u, v, w);
    }

    int start, target;
    cout << "Введите начальный и конечный склады: ";
    cin >> start >> target;

    vector<int> path = dijkstra(graph, start, target);

    if (path.empty()) {
        cout << "Путь между складами не найден.\n";
    }
    else {
        cout << "Самый дешевый путь: ";
        for (int v : path) {
            cout << v << " ";
        }
        cout << "\n";
    }

    return 0;
}
