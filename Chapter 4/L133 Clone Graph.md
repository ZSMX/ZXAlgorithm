###133. Clone Graph


题目:
<https://leetcode.com/problems/clone-graph/>


难度:
Medium

### Python

```
# 本参考程序来自九章算法，由 @令狐冲 提供。版权所有，转发请注明出处。
# - 九章算法致力于帮助更多中国人找到好的工作，教师团队均来自硅谷和国内的一线大公司在职工程师。
# - 现有的面试培训课程包括：九章算法班，系统设计班，算法强化班，Java入门与基础算法班，Android 项目实战班，
# - Big Data 项目实战班，算法面试高频题班, 动态规划专题班
# - 更多详情请见官方网站：http://www.jiuzhang.com/?source=code


class Solution:
    def cloneGraph(self, node):
        root = node
        if node is None:
            return node
            
        # use bfs algorithm to traverse the graph and get all nodes.
        nodes = self.getNodes(node)
        
        # copy nodes, store the old->new mapping information in a hash map
        mapping = {}
        for node in nodes:
            mapping[node] = UndirectedGraphNode(node.label)
        
        # copy neighbors(edges)
        for node in nodes:
            new_node = mapping[node]
            for neighbor in node.neighbors:
                new_neighbor = mapping[neighbor]
                new_node.neighbors.append(new_neighbor)
        
        return mapping[root]
        
    def getNodes(self, node):
        q = collections.deque([node])
        result = set([node])
        while q:
            head = q.popleft()
            for neighbor in head.neighbors:
                if neighbor not in result:
                    result.add(neighbor)
                    q.append(neighbor)
        return result
```



思路：

DFS或者BFS把graph traverse一遍，边traverse边复制。因为nodes are labeled uniquely，这就是方便的地方，但是注意node可能重复和有self-loop.

所以先建立新的root node，然后有一个dict把node label和node一一对应。

用stack来存储原本的graph root node，对原本的graph做DFS，这个时候，如果这个node的neighbor是已经出现过，那么我们就是去修改原本的existNode，让它指向存在的neighbor，否则创建新的，再把它们联系起来，谷歌了一下，别人写的比我更简单。anyway，先AC。



`if cur.label in createdNodes:`多余。




```
class Solution(object):
    def cloneGraph(self, node):
        """
        :type node: UndirectedGraphNode
        :rtype: UndirectedGraphNode
        """
        if node == None: return None

        root = UndirectedGraphNode(node.label)
        # must 1 to 1
        createdNodes = {}
        createdNodes[root.label] = root 

        stack = []
        stack.append(node)

        while stack:
        	cur = stack.pop()
        	if cur.label in createdNodes:
        		existNode = createdNodes[cur.label]
        		for neighbor in cur.neighbors:
        			if neighbor.label in createdNodes:
        				existNeighbor = createdNodes[neighbor.label]
        				existNode.neighbors.append(existNeighbor)
        			else:
        				newNode = UndirectedGraphNode(neighbor.label)
        				existNode.neighbors.append(newNode)
        				createdNodes[neighbor.label] = newNode
        				stack.append(neighbor)
        return root
```



看了别人的代码，貌似比我又写的简洁。



