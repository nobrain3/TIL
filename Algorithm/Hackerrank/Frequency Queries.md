# Frequency Queries

## 문제 개요
n개의 2차원 배열이 주어지고 그 2차원 배열의 원소는 다시 길이 2개의 배열이 주어진다.
배열의 첫번째 값은 1, 2, 3이 들어오는데
1 : 원소의 값을 삽입한다.
2 : 원소에 해당 되는 값을 삭제한다.
3 : 삽입/삭제 작업이 완료된 리스트에 값의 빈도가 원소만큼 있으면 1을 출력 아니면 0을 출력한다.

<pre><code>
Operation   Array   Output
(1,1)       [1]
(2,2)       [1]
(3,2)                   0
(1,1)       [1,1]
(1,1)       [1,1,1]
(2,1)       [1,1]
(3,2)                   1
</code></pre>

처음에 HashMap<Integer, Integer> 로 키값은 원소르 들어온 값 Value 값은 빈도수로 해서 빈도수가 0이면 맵에서 삭제하면서
3이 들어오면 HashMap의 containsValue() 함수를 사용하여 해당 원소 값과 동일한 Value 값이 있으면 1을 아니면 0을 List<Interger>형 배열에 삽입해주도록 했는데.
특정 Case에서 계속 타임아웃 문제가 났다. 원인은 HashMap의  containsValue() 함수에서 오버헤드가 심해서 타임아웃이 나는 것이었다. 
생각해보면 map에 key값으로 찾는게 아닌 Value를 찾으려면 잘못하면 O(n)까지 나오니 map을 사용할 이유가 없는 것 같다.
이 문제 해결을 위해 빈도수를 저장하는 Map 을 하나더 만들었다. 값이 추가되거나 삭제될때 첫번째 resultMap의 value 값을 이용하여 frequency map에서 해당 값을
찾아서 +/- 해주면서 이 문제를 해결할 수 있었다.

## Code
### Java
<pre><code>

    // Complete the freqQuery function below.
    static List<Integer> freqQuery(int[][]queries) {
        Map<Integer, Integer> resultMap = new HashMap<>();
        Map<Integer, Integer> frequencyMap = new HashMap();
       
        List<Integer> resultList = new ArrayList<>();
        for (int i = 0; i < queries.length; i ++)
        {
            int curOperator = queries[i][0];
            int curValue = queries[i][1];
            int curValueCount = 0;
            switch(curOperator)
            {
                case 1:
                    curValueCount = resultMap.getOrDefault(curValue, 0) + 1;
                    resultMap.put(curValue, curValueCount);
                    frequencyMap.put(curValueCount, frequencyMap.getOrDefault(curValueCount, 0) + 1);
                    if (curValueCount - 1 > 0)
                        frequencyMap.put(curValueCount - 1 , frequencyMap.getOrDefault(curValueCount - 1, 1) - 1);
                    break;

                case 2:
                    curValueCount = resultMap.getOrDefault(curValue, -1);
                    int count = curValueCount - 1;
                    if (count <= 0) {
                        resultMap.remove(curValue);
                        if (curValueCount != -1)
                            frequencyMap.put(1, frequencyMap.getOrDefault(1, 1)  -1);
                    } else {
                        resultMap.put(curValue, resultMap.getOrDefault(curValue, 1) - 1); 
                        frequencyMap.put(curValueCount, frequencyMap.getOrDefault(curValueCount, 1)  - 1);
                        frequencyMap.put(curValueCount - 1, frequencyMap.getOrDefault(curValueCount - 1, 0)  + 1);
                    }
                    break;
                
                case 3:
                    int resultNum = 0;
                    //if (resultMap.containsValue(curValue))
                      //   resultNum = 1;

                      if (frequencyMap.getOrDefault(curValue, 0) != 0)
                        resultNum = 1;
                    
                
                    resultList.add(resultNum);
                    break;
            }
        }
        
        return resultList;
    }

</code></pre>

### C++
<pre><code>

// Complete the freqQuery function below.
vector<int> freqQuery(vector<vector<int>> queries) {
    map<int, int> resultMap;
    map<int, int> frequencyMap;

    vector<int> resultList;

    for (int i = 0; i < queries.size(); i ++)
    {
        int curOperator = queries[i][0];
        int curValue = queries[i][1];
        int curValueCount = 0;
        switch(curOperator) 
        {        
            case 1:
                curValueCount = resultMap[curValue] + 1;
                resultMap[curValue] = curValueCount;
                frequencyMap[curValueCount]++;
                if (curValueCount - 1 > 0)
                    frequencyMap[curValueCount - 1]--;
                break;
            
            case 2:
            {
                curValueCount = resultMap[curValue];
                int count = resultMap[curValue] - 1;
                if (count <= 0) {
                    resultMap.erase(curValue);
                    if (curValueCount == 1)
                        frequencyMap[1]--;
                }
                else {
                    resultMap[curValue]--;
                    frequencyMap[curValueCount]--;
                    frequencyMap[curValueCount - 1]++;
                }
                break;
            }
            case 3:
            {
                int resultNum = 0;
                if (frequencyMap[curValue] != 0)
                    resultNum = 1;
                                
                resultList.push_back(resultNum);
                break;
            }
            default:
                break;
        }
    }

    return resultList;

}

</code></pre>
