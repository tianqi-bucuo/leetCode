将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。  

比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：  

L   C   I   R  
E T O E S I I G  
E   D   H   N  
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。  

请你实现这个将字符串进行指定行数变换的函数：  

string convert(string s, int numRows);
```Java
class Solution {
    public String convert(String s, int numRows) {
        if(numRows == 1) return s;
        List<StringBuilder> l = new ArrayList<>();
        for(int i = 0;i <= Math.min(numRows, s.length());i++){
            l.add(new StringBuilder());
        }
        int cur = 0;Boolean flag = true;
        for(char c:s.toCharArray()){
            l.get(cur).append(c);
            if(flag ==true){
                cur++;
            }else{
                cur--;
            }
            if(cur == 0 || cur == numRows-1) flag = !flag;
        }
        StringBuilder res = new StringBuilder();
        for(StringBuilder str: l){
            res.append(str);
        }
        return res.toString();
    }
}
```
