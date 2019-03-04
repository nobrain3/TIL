# Sherlock and Anagrams

## 문제 설명
입력된 String의 부분 문자들의 동일한 짝을 구하는 계산. 순서는 상관없음
예를 들어 입력된 문자가 mom 이면 ([m],[m]) / ([m,o], [o,m]) 값은 2가 된다.

문제 수준은 midium 이었지만 나한테는 굉장히 어려운 문제였다. 결국 답을 보고 풀수 밖에 없었다.
이 문제는 우선 스트링으로 입력된 문자들을 하나 부터 계속 문자를 더하면서  hashmap에 저장했다.
순서는 상관없기 때문에 순서라 달라도 문자가 같으면 동일한 문자로 간주하기 위하여 문자를 오름차순 정렬하여 key 값으로 사용했다.
예를 들어. abba가 입력됐으면 앞에서 부터 순서데로 a, ab, bb, ba 여기서 ab와 ba는 같은 문자 이므로 같은 key 값에 value를 + 1 해준다.
이런식으로 그 그 다음 2번째 문자 부터 b, bb, ba 순으로 끝까지 저장한다.

그 다음에 hashMapdp 저장된 value 값을 리턴하여 value * (value - 1) / 2 계산을 통하여 총 동일한 count 값을 구하여 계속 더해준다.

예제 코드. java로 작성.
<pre><code>
public class Solution {

    // Complete the sherlockAndAnagrams function below.
    static int sherlockAndAnagrams(String s) {
        Map<String, Integer> wordMap = new HashMap<>();
        
        for (int i = 0; i < s.length(); i++)
        {
            for (int j = i + 1; j <= s.length(); j++)
            {
                //System.out.println("i::: " + i + " j::::"+ j);
                String subStr = s.substring(i, j);
                char[] subChar = subStr.toCharArray();
                //System.out.println(subStr);
                Arrays.sort(subChar);
                subStr = String.valueOf(subChar);
                //System.out.println(subStr);
                
                if (wordMap.containsKey(subStr) == true)
                    wordMap.put(subStr, wordMap.get(subStr) + 1);
                else
                    wordMap.put(subStr, 1);
            }
        }
        
        int resultValue = 0;
        for (Map.Entry<String, Integer> element : wordMap.entrySet())
        {
            if (element.getValue() > 1)
                resultValue += (element.getValue()) * (element.getValue() - 1) / 2;
        }
        //System.out.println(resultValue);
        return resultValue;
    }
    </code></pre>


c++ 작성 코드
<pre><code>

int sherlockAndAnagrams(string s) {
    vector<int> resultList;
    map<string, int> resultMap;
    for (int i = 0; i < s.size(); i++)
    {
        for (int j = 1; j + i - 1 <s.size(); j++)
        {
            string subS = s.substr(i, j);
            sort(subS.begin(), subS.end());
            resultMap[subS]++;
        }
    }

    long resultCount = 0;
    for (map<string, int>::iterator it= resultMap.begin(); it != resultMap.end(); ++it)
    {
        resultCount+= (long)(it->second) * (long)(it->second - 1) / 2;
    }

    return resultCount;
    
</pre></code>

## map 사용방식에 대해 java와 c++이 약간의 차이가 있다.
c++에 값을 insert  하거나 value 값을 업데이트 할때 resultMap[subS]++;로 사용가능.
java는 wordMap.containsKey(subStr) 리턴값으로 true/false를 구분하여 true면 wordMap.put(subStr, wordMap.get(subStr) + 1);
false면 wordMap.put(subStr, 1);


