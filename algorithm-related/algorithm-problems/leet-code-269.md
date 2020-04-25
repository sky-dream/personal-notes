# leet code 269



There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

## Example 1:

```text
Input:
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]

Output: "wertf"
```

## Example 2:

```text
Input:
[
  "z",
  "x"
]

Output: "zx"
```

## Example 3:

```text
Input:
[
  "z",
  "x",
  "z"
] 

Output: "" 

Explanation: The order is invalid, so return "".
```

## Example 4:

```text
["ab","abc"]------------->"abc"
["abc","ab"]------------->""
```

## Note:

* You may assume all letters are in lowercase.
* If the order is invalid, return an empty string.
* There may be multiple valid order of letters, return any one of them is fine.

### Solution  of python code for 269

```python
# leetcode time     cost : 52 ms
# leetcode memory   cost : 13.8 MB 
# Time  Complexity: O(N)
# Space Complexity: O(N)
from typing import List
class Solution:
    def __init__(self):
      self.solutionNotFound = False
      
    def alienOrder(self, words: List[str]) -> str:
      # init the char mapping table
      dic = self.build_dict(words)
      print("char mapping dict: ",dic)
      # create adjacent list
      graph = self.build_adj(words, dic)
      print("adjacent list: ",graph)
      path = []
      # finish topo sort
      visited = [-1 for _ in range(len(dic))]
      for k,v in dic.items():
        if visited[v] is -1:
          state = self.dfs(v, graph, path, visited)
          if not state: return ""
      path.reverse()
      
      dictIndexToChar = {dic[k]:k for k in dic}
      ans = "".join([dictIndexToChar[i] for i in path])
      return ans if not self.solutionNotFound else ""

    def dfs(self, start, adj, path, visited):
      visited[start] = 1
      for next_node in adj[start]:
        # =1 means circle found
        if visited[next_node] == 1: 
          return False
        # =2 means this node checked before
        if visited[next_node] == 2: continue
        state = self.dfs(next_node, adj, path, visited)
        if not state: 
          return False
      visited[start] = 2
      path.append(start)
      #print(path,",current start is: ",start)
      return True
    
    def build_dict(self, words):
      dic = {}
      index = 0
      for word in words:
        for char in word:
          if char not in dic:
            dic[char] = index
            index += 1
      return dic

    def build_adj(self, words, dic):
      graph = {}
      for i in range(len(dic)):
        graph[i] = []
      
      for index in range( len(words)-1 ):
        w1,w2 = words[index],words[index+1]
        n1,n2 = len(w1),len(w2) 
        charOrderFound = False
        for j in range( max(n1,n2) ):
          c1 = w1[j] if j < n1 else None
          c2 = w2[j] if j < n2 else None
          if (c1) and (c2) and (c1 != c2) and (not charOrderFound):
            charOrderFound = True
            if dic[c2] not in graph[dic[c1]]:
              graph[dic[c1]].append(dic[c2])
          # used to handle case ["abc","ab"]
          if((c1 == c2) and ((j+1) == n2) and (n1>n2) and (not charOrderFound)):
            self.solutionNotFound = True
      return graph

def main():  
    words1,expect1 = ["wrt","wrf","er","ett","rftt"],"wertf"
    words2,expect2 = ["abc","ab"],""
    words3,expect3 = ["ab","abc"],"abc"
    words4,expect4 = ["ab","adc"],"abcd"
    words5,expect5 = ["za","zb","ca","cb"],"abzc"
    testCases = [(words1,expect1),(words2,expect2),(words3,expect3),(words4,expect4),(words5,expect5)]
    for input_strs,expectRes in testCases:
        obj = Solution()
        print("******************new test start,input is: ",input_strs,"********************")
        result = obj.alienOrder(input_strs)
        try:
            assert result == expectRes
            print("passed, result is follow expect:",result)
        except AssertionError as aError:
            print('failed, result >> ', result,"<< is wrong, ","expect is : "+ expectRes)
if __name__ =='__main__':
    main() 
```

### Solution  of java code for 269



```java
// leetcode time     cost : 29 ms
// leetcode memory   cost : 40.3 MB
import java.lang.Character;
import java.util.ArrayDeque;
import java.util.HashMap;
import java.util.Map;
import java.util.ArrayList;
import java.util.List;
import java.util.Queue;
//import java.util.Stack;
class Solution {
    // 基本情况处理，比如输入为空，或者输入的字符串只有一个
    public String alienOrder(String[] words) {
        if (words == null || words.length == 0)
            return null;
        if (words.length == 1) {
            return words[0];
        }
    
        // 构建有向图：定义一个邻接链表 adjList，也可以用邻接矩阵
        Map<Character, List<Character>> adjList = new HashMap<>();

        for (int i = 0; i < words.length - 1; i++) {
            String w1 = words[i], w2 = words[i + 1];
            int n1 = w1.length(), n2 = w2.length();
            boolean found = false;
            for (int j = 0; j < Math.max(w1.length(), w2.length()); j++) {
                Character c1 = j < n1 ? w1.charAt(j) : null;
                Character c2 = j < n2 ? w2.charAt(j) : null;

                if (c1 != null && !adjList.containsKey(c1)) {
                    adjList.put(c1, new ArrayList<Character>());
                }

                if (c2 != null && !adjList.containsKey(c2)) {
                    adjList.put(c2, new ArrayList<Character>());
                }

                if (c1 != null && c2 != null && c1 != c2 && !found) {
                    //一个char1 可能多次指向 char2, 同一起点和终点只统计一次 
                    if(!adjList.get(c1).contains(c2)){
                        adjList.get(c1).add(c2);
                    }
                    // 字符不等, 说明出现了大于的关系, 记录下来,后面不用看了
                    found = true;
                }
                // used to handle case ["abc","ab"]
                if(c1 == c2 && (j+1) == w2.length() && w1.length()>w2.length() && !found)
                    return ""; 
            }
        }
        System.out.println("adjList:  "+adjList.toString());

        StringBuilder strBuilder = new StringBuilder();
        // 拓补排序
        boolean sortResult = topologicalSort(adjList, strBuilder);
        if (sortResult){
            return strBuilder.toString();
        }
        else{
            return ""; 
        }
    
    } 
    // 拓补排序
    boolean topologicalSort(Map<Character, List<Character>> adjList,StringBuilder strBuilder) {
        Queue<Character> nodeHeader = new ArrayDeque<Character>();
        Map<Character, Integer> indegreeMap = new HashMap<>();
        //获取 indegree 入度表 
        for (Character key : adjList.keySet()) {
            if (!indegreeMap.containsKey(key)) {
                indegreeMap.put(key, 0);
            }
            
            for (Character c1 : adjList.get(key)) {
                if (!indegreeMap.containsKey(c1)) {
                    indegreeMap.put(c1, 1);
                }
                else{
                    int tmp = indegreeMap.get(c1);
                    indegreeMap.put(c1, tmp+1);
                }
            }
        }
        System.out.println("indegreeMap:  "+indegreeMap.toString());
        //把所有入度为0的字符节点加入到 Stack nodeHeader
        for (Character c1 : indegreeMap.keySet()){
            if (indegreeMap.get(c1)==0){
                nodeHeader.add(c1);
            }
        }
        //开始拓补排序
        while(!nodeHeader.isEmpty())
        {
            Character header=nodeHeader.poll(); // queue--poll(), stack---pop(),
            strBuilder.append(header);
            System.out.print("header: "+header+", ");
            
            for(Character c1 : adjList.get(header))
            {
                int tmp = indegreeMap.get(c1);
                if(tmp==1)//如果入度为1,那么header 是最后一个指向 c1的连接
                {
                    nodeHeader.add(c1);
                    indegreeMap.put(c1, 0);
                }
                else{
                    indegreeMap.put(c1, tmp-1);
                }
                //System.out.println(",dest is:  "+c1+", indegree value: "+tmp);
            }
        }
        // 如果拓扑排序遍历了所有的字符, 说明有可行解; 
        // 否则的话说明 1.不是有向无环图, 2.有环, 3.没有可行解
        if (adjList.keySet().size() == strBuilder.length()){
            return true;
        }
        else{
            return false;
        }
        
    }     
}

public class Alien_Dictionary {
    public static void main(String args[]) {
        String[] words= {"ab","abc"}; // #expect is "abc"
        Solution Solution_obj = new Solution();
        String result = Solution_obj.alienOrder(words);
        System.out.println("In java code,return value is :" + result);
    }
}
```

### Solution  of cpp code for 269

```cpp
// leetcode time     cost : 4 ms
// leetcode memory   cost : 7 MB
#include<iostream>
#include<vector>
#include<queue>
#include<unordered_set>
using namespace std;

class Solution {
public:
    string alienOrder(vector<string>& words) {
        // 整体的思想就是拓扑排序
        // 我们抽象出来的关系是大于关系, 我们最后要看根据这个大于关系, 我们能不能生成一个合理的顺序
        // 特别坑爹地是, abc 和 ab是错误的直接返回", 因为abc的长度是3, 比ab的长度大, 所以必须在abc的后面

        int indegree[26], len=0; // 记录入度, 单词表涉及多少个字符
        for(int i=0;i<26; ++i)
            indegree[i]=-1; // 入度为-1 表示这个字符没有出现过
        
        for(int i=0;i<words.size(); ++i){ // 把出现的字符入度设为0
            for(int j=0; j<words[i].size(); ++j){
                indegree[words[i][j]-'a']=0;
            }              
        }
        
        for(int i=0;i<26; ++i) // 统计一共有多少个字符
            if(indegree[i]==0)
                ++len;

        vector<unordered_set<char>>  m(26,unordered_set<char>()); // 有向图的邻接表, 我们比较前后相邻的两个单词, 来获得字符之间的关系
            // 之所以用unordered_set<char>是因为可能多次出现比如a>b, 要防止反复地插入
        for(int i=0;i<words.size()-1; ++i){
            int j;
            for(j=0; j<words[i].size() && j<words[i+1].size(); ++j){
                if(words[i][j]==words[i+1][j]){ // 字符相等, 继续看
                    continue;
                }    
                else{ // 字符不等, 说明出现了大于的关系, 记录下来
                    m[words[i][j]-'a'].insert(words[i+1][j]);
                    break; // 后面不用看了
                }
            }
            // 这个就是为了克服abc和ab的问题, 也就是两个字符串前面的部分完全相等(所以在上面的循环结束后j==words[i+1].size()), 
            // 但是长的在前面, 短的在后面, 这样是错误的. 直接返回""
            if(j==words[i+1].size() && words[i].size()>words[i+1].size())
                return ""; 
        }

        // 接下来就是统计入度
        for(int i=0;i<26;++i){
            for(auto& c:m[i]){
                ++indegree[c-'a'];
            }          
        }
        queue<char> que;
        string res="";
        for(int i=0;i<26;++i){ // 把入度为0的结点加入到队列里
            if(indegree[i]==0){
                char c='a'+i;
                que.push(c);
            }    
        }

        while(!que.empty()){
            char c=que.front();
            res+=c; // 添加到字符串
            que.pop();
            for(auto s: m[c-'a']){ 
                --indegree[s-'a'];
                if(indegree[s-'a']==0) // 如果这个字符变成0了, 添加到队列里
                    que.push(s);
            }
        }

        if(res.size()!=len) // 如果拓扑排序遍历了所有的字符, 说明有可行解; 否则的话说明不是有向无环图, 有环, 没有可行解
            return "";
        else 
            return res;
    }
};

int main(){
    vector<string> words= {"ab","abc"};         //expect is "abc"
    Solution *obj = new Solution();
    string result = obj->alienOrder(words);
    cout << "In cpp code, result  is : [" << result << "]" << endl;
}
```

