# Bubble sort
간단한 정렬법이다. 배열이 있고 첫번째 배열이 그 다음 배열보다 크면 Swap 하면서 가장 큰수를 가장 뒤에 위치시키고, 그 다음 loop에서 두번째로 큰수를 위치시켜서 
정렬하는 방식이다.
예 
배열 4 3 2 1 이 있으면
4 와 3 swap
#### 3 4 2 1
#### 3 2 4 1 
#### 3 2 1 4
#### 2 3 1 4
#### 2 1 3 4
#### 1 2 3 4

총 여섯번의 Swap이 일어났다.

## Code
### Java
<pre><code>
 static void countSwaps(int[] a) {
        int length = a.length;
        int swapCount = 0;
        for (int i = length - 1; i > 0; i--)
        {
            for (int j = 0; j < i; j++)
            {
                if (a[j] > a[j + 1])
                {
                    int temp = a[j];
                    a[j] = a[j + 1];
                    a[j + 1] = temp;
                    swapCount++;
                }
            }
        }

        System.out.println("Array is sorted in " + swapCount + " swaps.");
        System.out.println("First Element: " + a[0]);
        System.out.println("Last Element: " + a[length - 1]);

    }
</code></pre>
