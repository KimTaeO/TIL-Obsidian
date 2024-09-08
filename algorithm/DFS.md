DFS(Depth-First Search)란 그래프를 전체 탐색하기 위한 알고리즘 중 하나로 너비와 깊이중 깊이를 우선으로 탐색하는 알고리즘이다.

한 분기를 시작으로 다음 분기로 넘어가기 전까지 해당 분기를 전부 탐색하는 것이다

1. 시작점으로 잡은 노드를 **스택에 삽입** 후 **방문 처리**한다 
2. 스택 최상단 노드에 방문하지 않은 **인접 노드**가 있다면 **스택에 삽입** 후 **방문 처리**한다
3. **인접 노드**가 없다면 스택의 최상단 노드를 제거한다

2, 3의 동작을 모든 노드를 탐색하기 전까지 반복한다