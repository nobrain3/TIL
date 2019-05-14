# Stack
 - 한쪽끝에서 자료를 넣고 빼는 자료구조
 - LIFO(Last in first out) 구조 가장 나중에 삽입 된것이 가장 먼저 빠진다.
 - push : 스택에 자료를 넣는다.
 - pop : 스택의 가장 위에 있는 자료를 뺀다.
 - top : 스택의 가장 위 자료를 리턴.
 - empty : 스택이 비어있는지 여부를 확인.
 - size : 스택에 저장되어 있는 자료의 개수를 리턴.
 
 ## 스택 구현.
 ### BackJoon 10828 문제 
 https://www.acmicpc.net/problem/10828
 
 정수를 저장하는 스택을 구현한 다음, 입력으로 주어지는 명령을 처리하는 프로그램을 작성하시오.

명령은 총 다섯 가지이다.

- push X: 정수 X를 스택에 넣는 연산이다.
- pop: 스택에서 가장 위에 있는 정수를 빼고, 그 수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다.
- size: 스택에 들어있는 정수의 개수를 출력한다.
- empty: 스택이 비어있으면 1, 아니면 0을 출력한다.
- top: 스택의 가장 위에 있는 정수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다.

c++ 
<pre><code>
#include <iostream>
#include <vector>
#include <cstring>
using namespace std;

class Stack {
private:
    vector<int> stack;
    
public:
    
    void push(int num)
    {
        stack.push_back(num);
    }
    
    int pop()
    {
        int num = -1;
        if (stack.size() > 0){
            num = stack.back();
            stack.pop_back();
        }
        return num;
    }
    
    int size()
    {
        return stack.size();
    }
    
    int empty()
    {
        if (stack.size() == 0)
            return 1;
        else
            return 0;
    }
    
    int top()
    {
        if (stack.size() <= 0)
            return -1;
        else
            return stack.back();
    }
};

int main(int argc, const char * argv[]) {
    int count = 0;
    cin>>count;
    
    Stack stack;
    
    for (int i = 0; i < count; i ++)
    {
        char str[6];
        cin>>str;
        
        if (strncmp(str, "push", sizeof("push")) == 0)
        {
            int num = 0;
            cin>>num;
            stack.push(num);
        } else if (strncmp(str, "pop", sizeof("pop")) == 0)
        {
            cout<<stack.pop()<<endl;
        } else if (strncmp(str, "size", sizeof("size")) == 0)
        {
            cout<<stack.size()<<endl;
        } else if (strncmp(str, "empty", sizeof("empty")) == 0)
        {
            cout<<stack.empty()<<endl;
        } else
        {
            cout<<stack.top()<<endl;
        }
    }
    return 0;
}
</code></pre>