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

### 269 solution code of java



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

### 269 solution code of cpp

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

