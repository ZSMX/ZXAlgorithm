### 200. Number of Islands 


题目:
<https://leetcode.com/problems/number-of-islands/>

难度:
Medium

### Python

```
# 本参考程序来自九章算法，由 @令狐冲 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


from collections import deque

class Solution:
    """
    @param grid: a boolean 2D matrix
    @return: an integer
    """
    def numIslands(self, grid):
        if not grid or not grid[0]:
            return 0
            
        islands = 0
        visited = set()
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] and (i, j) not in visited:
                    self.bfs(grid, i, j, visited)
                    islands += 1
                    
        return islands                    
    
    def bfs(self, grid, x, y, visited):
        queue = deque([(x, y)])
        visited.add((x, y))
        while queue:
            x, y = queue.popleft()
            for delta_x, delta_y in [(1, 0), (0, -1), (-1, 0), (0, 1)]:
                next_x = x + delta_x
                next_y = y + delta_y
                if not self.is_valid(grid, next_x, next_y, visited):
                    continue
                queue.append((next_x, next_y))
                visited.add((next_x, next_y))

    def is_valid(self, grid, x, y, visited):
        n, m = len(grid), len(grid[0])
        if not (0 <= x < n and 0 <= y < m):
            return False
        if (x, y) in visited:
            return False
        return grid[x][y]
    
# LeetCode 的用户请用下面的代码，因为 LeetCode 上的输入是 2D string array 而不是 boolean array
# from collections import deque

# class Solution:
#     """
#     @param grid: a boolean 2D matrix
#     @return: an integer
#     """
#     def numIslands(self, grid):
#         if not grid or not grid[0]:
#             return 0
        
#         islands = 0
#         for i in range(len(grid)):
#             for j in range(len(grid[0])):
#                 if grid[i][j] == '1':
#                     self.bfs(grid, i, j)
#                     islands += 1
                    
#         return islands                    
    
#     def bfs(self, grid, x, y):
#         queue = deque([(x, y)])
#         grid[x][y] = '0'
#         while queue:
#             x, y = queue.popleft()
#             for delta_x, delta_y in [(1, 0), (0, -1), (-1, 0), (0, 1)]:
#                 next_x = x + delta_x
#                 next_y = y + delta_y
#                 if not self.is_valid(grid, next_x, next_y):
#                     continue
#                 queue.append((next_x, next_y))
#                 grid[next_x][next_y] = '0'
                
#     def is_valid(self, grid, x, y):
#         n, m = len(grid), len(grid[0])
#         return 0 <= x < n and 0 <= y < m and grid[x][y] == '1'
```




思路：


一开始：
numberOfIslands = 0
islandArea = []


然后遇到（x,y） = 1的状况，更新numberOfIslands，并且把（x,y）放入islandArea，然后用BFS或者DFS查找岛屿范围，全部更如islandArea，做loop

以上就是基本思路


然后超时|||, 小改之后AC


```

class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        self.grid = grid[:]

        self.row = len(self.grid)
        self.col = len(self.grid[0]) if self.row else 0
        self.visited = [[0 for i in range(self.col)]for j in range(self.row)]


        self.numberOfIslands = 0

        for i in range(self.row):
        	for j in range(self.col):
        		if self.grid[i][j] == '1' and self.visited[i][j] == 0:
        				self.findArea(i,j)
        				self.numberOfIslands += 1

        return self.numberOfIslands

    def findArea(self, i, j):
    	s = []
    	s.append((i,j))
    	while s:
    		(x,y) = s.pop()
    		self.visited[x][y] = 1
    		if self.legal(x-1,y):
    			s.append((x-1,y))
    		if self.legal(x+1,y):
    			s.append((x+1,y))
    		if self.legal(x,y-1):
    			s.append((x,y-1))
    		if self.legal(x,y+1):
    			s.append((x,y+1))

    def legal(self,x,y):
    	return x>= 0 and x < self.row and y >= 0 and y < self.col and self.grid[x][y] == '1' and self.visited[x][y] == 0
a = Solution()
print a.numIslands(["11000","11000","00100","00011"])

```


看了别人的代码，写的真美 ╮(╯_╰)╭ 啊

```
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        def dfs(gird, used, row, col, x, y):
            if gird[x][y] == '0' or used[x][y]:
                return 
            used[x][y] = True

            if x!= 0:
                dfs(grid, used, row,col, x-1,y)
            if x!= row -1 :
                dfs(grid, used, row,col, x+1, y)
            if y!= 0:
                dfs(grid, used, row,col, x, y-1)
            if y!= col - 1:
                dfs(grid, used, row,col, x, y+1)


        row = len(grid)
        col = len(grid[0]) if row else 0

        used = [[0 for i in xrange(col)] for i in xrange(row)]

        count = 0
        for i in xrange(row):
            for j in xrange(col):
                if grid[i][j] == '1' and not used[i][j]:
                    dfs(grid,used,row,col,i,j)
                    count += 1
        return count
```

厉害的解法：Sink and count the islands.
```python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        def sink(i, j):
            if 0 <= i < len(grid) and 0 <= j < len(grid[0]) and grid[i][j] == '1':
                grid[i][j] = '0'
                map(sink, (i+1, i-1, i, i), (j, j, j+1, j-1))
                return 1
            return 0
        return sum(sink(i, j) for i in range(len(grid)) for j in range(len(grid[0])))
```

