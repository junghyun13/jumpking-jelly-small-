# jumpking-jelly-small-
# python
입력의 첫 번째 줄에는 게임 구역의 크기 N (2 ≤ N ≤ 3)이 주어지고 입력의 두 번째 줄부터 마지막 줄까지 게임판의 구역(맵)이 주어진다.게임판의 승리 지점(오른쪽 맨 아래 칸)에는 -1이 쓰여있고, 나머지 칸에는 0 이상 100 이하의 정수가 쓰여있고 쩰리’가 끝 점에 도달할 수 있는지를 출력하는 프로그램을 작성해보자!
규칙
1-‘쩰리’는 가로와 세로의 칸 수가 같은 정사각형의 구역 내부에서만 움직일 수 있다. ‘쩰리’가 정사각형 구역의 외부로 나가는 경우엔 바닥으로 떨어져 즉시 게임에서 패배하게 된다.
2-‘쩰리’의 출발점은 항상 정사각형의 가장 왼쪽, 가장 위의 칸이다. 다른 출발점에서는 출발하지 않는다.
3-‘쩰리’가 이동 가능한 방향은 오른쪽과 아래 뿐이다. 위쪽과 왼쪽으로는 이동할 수 없다.
4-‘쩰리’가 가장 오른쪽, 가장 아래 칸에 도달하는 순간, 그 즉시 ‘쩰리’의 승리로 게임은 종료된다.
5-‘쩰리’가 한 번에 이동할 수 있는 칸의 수는, 현재 밟고 있는 칸에 쓰여 있는 수 만큼이다. 칸에 쓰여 있는 수 초과나 그 미만으로 이동할 수 없다.

BFS(너비우선탐색) 알고리즘을 이용해보자!


from collections import deque
n=int(input())
place=[list(map(int,input().split())) for _ in range(n)]
visit=[[False]*n for _ in range(n)] #방문을 초기화 
dx=[1,0] #오른쪽
dy=[0,1] #아래 
def bfs(x,y):
  data=deque()
  data.append([x,y])
  while data:
    x,y=data.popleft() #popleft(): deque앞(왼쪽)값 삭제후반환
    a=place[x][y] #현재위치
    if place[x][y]==-1: #도작지점 도달시 
      return True
    for i in range(2): #i=0,1
      nx=x+a*dx[i]
      ny=y+a*dy[i]
      if nx<0 or nx>=n or ny<0 or ny>=n: #정해진범위를 벗어남
        continue
      if not visit[nx][ny]: #방문하지 않음 
        visit[nx][ny]=True #방문 
        data.append([nx,ny]) #아직 -1에 도달이 안됨, 담고 반복
if bfs(0,0):
  print("성공")
else:
  print("실패")
