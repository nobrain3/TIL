# 문자열 비교
## C++
<pre><code>
string a = "I am string one! ;)" 
string b = "string if (a.compare(b) == 0) 
{ // 두 문자열이 같을 때 
} else if (a.compare(b) < 0) { 
// a가 b보다 사전순으로 앞일 때 
} else if (a.compare(b) > 0) { 
// a가 b보다 사전순으로 뒤일 때 
}
</code></pre>

출처: https://makerj.tistory.com/127 [CheatSheet]

## JAVA
s1.compareTo(s2)
if s1 > s2, it returns positive number  
if s1 < s2, it returns negative number  
if s1 == s2, it returns 0  
