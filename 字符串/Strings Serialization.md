设计一个将字符串列表编码为字符串的算法。 已经编码的字符串之后会通过网络发送同时也会被解码回到原始的字符串列表。
请实现 encode 和 decode

***

自己实现一个字符串的编解码

```Java
public class Solution {
    /**
     * @param strs a list of strings
     * @return encodes a list of strings to a single string.
     */
    public String encode(List<String> strs) {
        // Write your code here
        StringBuilder result = new StringBuilder();
        for(String str : strs){
            result.append(String.valueOf(str.length()) + "$");
            result.append(str);
        }
        return result.toString();
    }

    /**
     * @param str a string
     * @return dcodes a single string to a list of strings
     */
    public List<String> decode(String str) {
        // Write your code here
        List<String> result = new LinkedList<String>();
        int start = 0;
        while(start < str.length()){
            int idx = str.indexOf('$', start);
            int size = Integer.parseInt(str.substring(start, idx));
            result.add(str.substring(idx + 1, idx + size + 1));
            start = idx + size + 1;
        }
        return result;
    }
}
```