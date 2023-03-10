## **문제 설명**

자연수 n이 매개변수로 주어집니다. n을 3진법 상에서 앞뒤로 뒤집은 후, 이를 다시 10진법으로 표현한 수를 return 하도록 solution 함수를 완성해주세요.

---

## 제한사항

- n은 1 이상 100,000,000 이하인 자연수입니다.

---

## 입출력 예

| n | result |
| --- | --- |
| 45 | 7 |
| 125 | 229 |

---

## 입출력 예 설명

**입출력 예 #1**

- 답을 도출하는 과정은 다음과 같습니다.

| n (10진법) | n (3진법) | 앞뒤 반전(3진법) | 10진법으로 표현 |
| --- | --- | --- | --- |
| 45 | 1200 | 0021 | 7 |
- 따라서 7을 return 해야 합니다.

**입출력 예 #2**

- 답을 도출하는 과정은 다음과 같습니다.

| n (10진법) | n (3진법) | 앞뒤 반전(3진법) | 10진법으로 표현 |
| --- | --- | --- | --- |
| 125 | 11122 | 22111 | 229 |
- 따라서 229를 return 해야 합니다.

## 풀이

- 이진법, 십진법 변환 알고리즘 참고

## 코드

```java
class Solution {
    private final int BASE_NUMBER = 3;
    
    public int solution(int n) {
        String resultNumber = getResultNumber(n, "");
        String reverseNumber = getReverseResultNumber(resultNumber);
        
        return getAnswer(n, reverseNumber);
    }
    
    private String getResultNumber(int n, String resultNumber) {
        if (n == 0) return resultNumber;
        
        resultNumber = getResultNumber(n / BASE_NUMBER, resultNumber);
        resultNumber += n % BASE_NUMBER;
        return resultNumber;
    }
    
    private String getReverseResultNumber(String resultNumber) {
        StringBuilder builder = new StringBuilder(resultNumber);
        
        return builder.reverse().toString();
    }
    
    private int getAnswer(int n, String reverseNumber) {
        int answer = 0;
        int numberForMultiple = 1;
        
        for (int i = reverseNumber.length() - 1; i >= 0; i--) {
            answer += (int)(reverseNumber.charAt(i) - '0') * numberForMultiple;
            numberForMultiple *= BASE_NUMBER;
        }
        
        return answer;
    }
}

테스트 1 〉	통과 (11.47ms, 77.1MB)
테스트 2 〉	통과 (13.63ms, 86.3MB)
테스트 3 〉	통과 (15.84ms, 73.8MB)
테스트 4 〉	통과 (23.28ms, 81MB)
테스트 5 〉	통과 (15.87ms, 84.8MB)
테스트 6 〉	통과 (9.73ms, 79.5MB)
테스트 7 〉	통과 (10.25ms, 83.5MB)
테스트 8 〉	통과 (10.98ms, 83.4MB)
테스트 9 〉	통과 (13.86ms, 76.2MB)
테스트 10 〉	통과 (10.06ms, 78.6MB)
```

- 조금 오래걸리는 느낌..?
- 생각해보니까 애초에 뒤집을 이유가 없을 것 같아서 다시 풀어보기로 했다.

## 최종 코드

```java
class Solution {
    private final int BASE_NUMBER = 3;
    
    public int solution(int n) {
        String reverseNumber = getReverseNumber(n, "");
        return getAnswer(n, reverseNumber);
    }
    
    private String getReverseNumber(int n, String reverseNumber) {
        while (n > 0) {
            reverseNumber += n % BASE_NUMBER;
            n /= BASE_NUMBER;
        }
        
        return reverseNumber;
    }
    
    private int getAnswer(int n, String reverseNumber) {
        int answer = 0;
        int numberForMultiple = 1;
        
        for (int i = reverseNumber.length() - 1; i >= 0; i--) {
            answer += (int)(reverseNumber.charAt(i) - '0') * numberForMultiple;
            numberForMultiple *= BASE_NUMBER;
        }
        
        return answer;
    }
}

테스트 1 〉	통과 (11.78ms, 78.9MB)
테스트 2 〉	통과 (12.96ms, 80MB)
테스트 3 〉	통과 (10.58ms, 79.6MB)
테스트 4 〉	통과 (10.16ms, 81.7MB)
테스트 5 〉	통과 (12.02ms, 83MB)
테스트 6 〉	통과 (8.68ms, 78.5MB)
테스트 7 〉	통과 (9.62ms, 79.7MB)
테스트 8 〉	통과 (11.70ms, 75MB)
테스트 9 〉	통과 (13.29ms, 85.9MB)
테스트 10 〉	통과 (8.60ms, 78MB)
```

- 훨씬 더 빠르다!
