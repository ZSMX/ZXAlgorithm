###207. Course Schedule



题目:
<https://leetcode.com/problems/course-schedule/>

难度:
Medium

### Python

```
/**
* 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
* - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
* - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
* - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
* - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code
*/ 

public class Solution {
    /**
     * @param numCourses a total of n courses
     * @param prerequisites a list of prerequisite pairs
     * @return true if can finish all courses or false
     */
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // Write your code here
        List[] edges = new ArrayList[numCourses];
        int[] degree = new int[numCourses];
        
        for (int i = 0;i < numCourses; i++)
            edges[i] = new ArrayList<Integer>();
            
        for (int i = 0; i < prerequisites.length; i++) {
            degree[prerequisites[i][0]] ++ ;
            edges[prerequisites[i][1]].add(prerequisites[i][0]);
        }

        Queue queue = new LinkedList();
        for(int i = 0; i < degree.length; i++){
            if (degree[i] == 0) {
                queue.add(i);
            }
        }
        
        int count = 0;
        while(!queue.isEmpty()){
            int course = (int)queue.poll();
            count ++;
            int n = edges[course].size();
            for(int i = 0; i < n; i++){
                int pointer = (int)edges[course].get(i);
                degree[pointer]--;
                if (degree[pointer] == 0) {
                    queue.add(pointer);
                }
            }
        }
        
        return count == numCourses;
    }
}
```



思路：

就是考topological sort，用来判断directed graph是否有cycle

DFS 和 BFS都可以用来拓扑排序。

最简单的想法是每次取出indegree是0的node，然后把它和与之相关的edge都删了。一开始觉得这样的时间复杂度会很高，然后看到了这样写，参照：

<http://bookshadow.com/weblog/2015/05/07/leetcode-course-schedule/>

很聪明的写法

这里做了转成set以及添加removeList这样的操作是因为边list边做iterator这样的操作很危险




```
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        degrees = [ 0 for i in range(numCourses)]
        childs = [[] for i in range(numCourses)]
        for front, tail in prerequisites:
        	degrees[front] += 1
        	childs[tail].append(front)

        courses = set(range(numCourses))
        flag = True

        while flag and len(courses):
        	flag = False
        	removeList = []
        	for x in courses:
        		if degrees[x] == 0:
        			for child in childs[x]:
        				degrees[child] -= 1
        			removeList.append(x)
        			flag = True
        	for x in removeList:
        		courses.remove(x)
        return len(courses) == 0 

```

因为CLRS里面明确提到涂色法来处理DFS

搞了半天，写了一个涂色法，在超时的边缘。之所以超时边缘是因为每次都要去prerequisites里看，没有删减，不高效.

```
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        def dfs(i, colors, prerequisites):
        	colors[i] = 'G'
        	#print i, colors
        	for front, tail in prerequisites:
        		if tail == i:
        			if colors[front] == 'G':
        				return False
        			elif colors[front] == 'B':
        				continue
        			elif dfs(front, colors, prerequisites) == False:
        				return False
        	colors[i] = 'B'
        	return True

        colors = ['W' for i in range(numCourses)]
        for i in range(numCourses):
        	if colors[i] == 'W':
        		if dfs(i, colors, prerequisites) == False:
        			return False
        return True
```
