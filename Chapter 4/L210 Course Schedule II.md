###210. Course Schedule II



题目:
<https://leetcode.com/problems/course-schedule-ii/>


难度:
Medium

思路：

### Python

```
# 本参考程序来自九章算法，由 @九章算法 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    # @param {int} numCourses a total of n courses
    # @param {int[][]} prerequisites a list of prerequisite pairs
    # @return {int[]} the course order
    def findOrder(self, numCourses, prerequisites):
        # Write your code here
        edges = {i: [] for i in xrange(numCourses)}
        degrees = [0 for i in xrange(numCourses)] 
        for i, j in prerequisites:
            edges[j].append(i)
            degrees[i] += 1
        import Queue
        queue = Queue.Queue(maxsize = numCourses)
        
        for i in xrange(numCourses):
            if degrees[i] == 0:
                queue.put(i)

        order = []
        while not queue.empty():
            node = queue.get()
            order.append(node)

            for x in edges[node]:
                degrees[x] -= 1
                if degrees[x] == 0:
                    queue.put(x)

        if len(order) == numCourses:
            return order
        return []
```



在207的基础上加了order，进击


```
class Solution(object):
    def findOrder(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: List[int]
        """
        degrees = [ 0 for i in range(numCourses)]
        childs = [[] for i in range(numCourses)]
        for front, tail in prerequisites:
        	degrees[front] += 1
        	childs[tail].append(front)


        courses = set(range(numCourses))
        flag = True
        order = []

        while flag and len(courses):
        	flag = False
        	removeList = []
        	for x in courses:
        		if degrees[x] == 0:
        			print x
        			for child in childs[x]:
        				degrees[child] -= 1
        			removeList.append(x)
        			order.append(x)
        			flag = True
        	for x in removeList:
        		courses.remove(x)

        if len(courses) == 0:
        	return order
        else:
        	return []

```
