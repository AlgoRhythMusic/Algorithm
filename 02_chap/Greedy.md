## 그리디란?

현재 상황에서 지금 당장 좋은 것만을 고르는 방법

→ 가장 좋아보이는 것을 선택하며, 현재의 선택이 나중에 미칠 영향에 대해서는 고려하지 않는다.
<br/>

## 예제 3-1. 거스름돈

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-18_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9 22 58](https://github.com/user-attachments/assets/5d99f239-7510-4777-8c2c-fc6c1478188c)

- 시간 복잡도 : O(K)
    - 동전의 개수가 K일 때, 시간 복잡도는 O(K)이다.
    - 동전의 개수만큼만 계산하면 되기 때문이다.

```java
public class Main {

    static int[] coins = {10, 500, 100, 50}; // 화폐 단위

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in); // 남은 돈을 입력한다.
        int money = sc.nextInt();

        // 화폐 단위가 가장 큰 것부터 계산하기 위해 정렬한다.
        Arrays.sort(coins);

        // 거슬러줘야 할 동전의 최소 개수를 구한다.
        int result = 0;
        for (int i = 0; i < coins.length; i++) {
            // 최소 동전이어야 하므로, 화폐 단위가 가장 큰 것부터 선택한다.
            // ex. 남은 돈이 1260원일 때, 현재 상황에서 최선의 방법은 500원 2개를 거슬러주는 것이다.
            int coin = coins[coins.length - 1 - i];
            result += money / coin;
            money %= coin;
        }

        System.out.println("최소 동전 개수 : " + result);
    }
}
```

## 예제3-2. 거스름돈2

그러나 그리디 알고리즘은 최적의 해를 보장하지 않는다.

따라서 다음 문제에서 그리디 알고리즘을 사용하면 오답을 유발한다.

> 문제 : 거슬러 줘야할 돈으로 800원이 주어졌을 때, 화폐 단위는 500, 400, 100원이 존재한다. 이때, 거슬러 줄 수 있는 최소 동전 개수를 구하라.

```java
public class Main {

    static int[] coins = {500, 400, 100}; // 화폐 단위

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in); // 남은 돈을 입력한다.
        int money = sc.nextInt();

        // 화폐 단위가 가장 큰 것부터 계산하기 위해 정렬한다.
        Arrays.sort(coins);

        // 거슬러줘야 할 동전의 최소 개수를 구한다.
        int result = 0;
        for (int i = 0; i < coins.length; i++) {
            // 최소 동전이어야 하므로, 화폐 단위가 가장 큰 것부터 선택한다.
            // ex. 남은 돈이 1260원일 때, 현재 상황에서 최선의 방법은 500원 2개를 거슬러주는 것이다.
            int coin = coins[coins.length - 1 - i];
            result += money / coin;
            money %= coin;
        }

        System.out.println("최소 동전 개수 : " + result);
    }
}
```

문제를 그리디 알고리즘으로 풀게되면 최소 동전 개수로 4를 반환한다. 이는 (500, 100, 100, 100)을 반환하기 때문이다. 그러나 최적의 답은 (400, 400)이다. 

그리디 알고리즘이 틀린 이유는 현재 상황에서 최적의 방법만 생각할 뿐, 현재 선택으로 인해 다음 상황에서 발생할 문제를 고려하지 않기 때문이다. 

예를 들어, 800원에서 500원을 거슬러주면 300원이 남는다. 이때, 400원으로는 거슬러 줄 수 없기 때문에 100원 3개를 선택하게 된다. 그러나 처음부터 500원이 아닌 400원을 선택했다면 400원 2개로 거슬러 줄 수 있다.

```java
입력 : 800

출력 : 4
정답 : 2
```
<br/>

## 문제를 대하는 태도

- 다양한 아이디어를 고려한다.
- 예제 3-1을 예로 들자면, 10원짜리부터 사용한다면 최적의 해를 구할 수 있는가? 를 먼저 생각한다.
    - 10원부터 사용하는 것이 최적의 해가 아님을 인정하고 또 다른 방법을 생각한다.
    - 최종적으로는 가장 큰 화폐 단위인 500원부터 거슬러주기 시작하여 가장 작은 10원짜리까지 차례대로 거슬러준다면 최적의 해가 될 수 있음을 판단하게 된다.
- 그러나 예제3-2의 경우 예제3-1의 방법이 최적의 해를 보장하지 않는다.
    - 이 경우에는 그리디 알고리즘을 사용할 수 없겠구나! 라고 판단한다.
    - 다이나믹 프로그래밍(DP), 완전 탐색 등을 사용할 수 있을 것이다.
<br/>

## 실전 문제 - 큰 수의 법칙

### 문제 설명
![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-18_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_10 06 15](https://github.com/user-attachments/assets/beab05aa-ff2f-490d-ae10-faf8cf2fa58c)

### 코드

1. 입력받은 숫자들(numbers)를 오름차순 정렬한다.
    1. N - 1번 인덱스에 가장 큰 값이 저장된다.
2. 특정 숫자를 최대 K번 연속으로 사용할 수 있으므로, 가장 큰 값을 K 번 사용한다.
3. K번 사용 후, 다른 숫자를 사용하되 N - 2번 인덱스에 저장된 값이 가장 크므로 해당 값을 사용한다.
4. 3번 이후에 다시 N - 1번 인덱스를 K번 연속하여 사용한다.

```java
public class Main {

    static int N, M, K;
    static int[] numbers;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] inputs = br.readLine().split(" ");
        N = Integer.parseInt(inputs[0]); // 숫자 개수
        M = Integer.parseInt(inputs[1]); // 더할 수 있는 최대 횟수
        K = Integer.parseInt(inputs[2]); // 같은 인덱스를 연속하여 사용할 수 있는 개수

        numbers = new int[N];
        inputs = br.readLine().split(" ");
        for (int i = 0; i < N; i++) {
            numbers[i] = Integer.parseInt(inputs[i]);
        }

        Arrays.sort(numbers);

        int count = 0;
        int sum = 0;
        for (int i = 0; i < M; i++) {
            if (count == K) {
                sum += numbers[N - 2];
                count = 0;
            } else {
                sum += numbers[N - 1];
                count++;
            }
        }

        System.out.println("최대 값 : " + sum);
    }
}
```

```java
입력 : 
5 8 3
2 4 5 4 6

출력 : 46
정답 : 46
```
<br/>

그러나 위 코드는 M이 100억(10_000_000_000)이라면 시간 초과가 발생한다.

보통 1초에 1억번의 계산을 할 수 있으므로, 100억번의 계산은 엄청난 시간을 사용하게 된다.

이 문제는 K개의 가장 큰 수와 1개의 다음으로 가장 큰 수를 반복해서 사용한다. → (K + 1)개의 숫자를 반복하여 계산한다. 그렇다면 반복문을 사용하지 않고 (K + 1)개의 숫자를 M번 이하로 미리 계산하면 된다.

즉, repeatCount만큼 미리 (K + 1)개의 숫자를 미리 더하고, 나머지 횟수를 가장 큰 수를 더하면 된다.

```java
public class Main {

    static int N, K;
    static long M;
    static int[] numbers;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] inputs = br.readLine().split(" ");
        N = Integer.parseInt(inputs[0]); // 숫자 개수
        M = Long.parseLong(inputs[1]); // 더할 수 있는 최대 횟수
        K = Integer.parseInt(inputs[2]); // 같은 인덱스를 연속하여 사용할 수 있는 개수

        numbers = new int[N];
        inputs = br.readLine().split(" ");
        for (int i = 0; i < N; i++) {
            numbers[i] = Integer.parseInt(inputs[i]);
        }

        Arrays.sort(numbers);

        long sum = 0;
        int repeat = 0; // 반복해서 더해지는 수열
        // K개의 가장 큰 수 + 다음으로 가장 큰 수
        for (int i = 0; i < K; i++) {
            repeat += numbers[N - 1];
        }
        repeat += numbers[N - 2];

        long repeatCount = M / (K + 1);
        sum += repeat * repeatCount; // M번 반복해서 더하는 것이 아닌, 반복해서 더해지는 수열을 미리 계산
        for (int i = 0; i < M % repeatCount; i++) {
            sum += numbers[N - 1]; // 가장 큰 수를 남은 횟수만큼 더하면 된다.
        }

        System.out.println("최대 값 : " + sum);

    }
}
```

```java
입력 : 
4 10000000000 10
2 4 5 4

출력 : 49090909091
```
<br/>

## 실전 문제 - 숫자 카드 게임

### 문제 설명

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-18_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_10 49 26](https://github.com/user-attachments/assets/4b0e51b4-5000-4516-b087-d4b57abe15f9)

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-18_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_10 49 57](https://github.com/user-attachments/assets/1632cf94-1bab-44ad-aad9-2a104b5357c0)

### 코드

1. 각 행에서 가장 작은 값을 구한다.
    1. tmp = Math.min()
2. 그 중에서 가장 큰 값을 구한다.
    1. result = Math.max()

```java
public class Main {

    static int N, M;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] inputs = br.readLine().split(" ");
        N = Integer.parseInt(inputs[0]);
        M = Integer.parseInt(inputs[1]);

        int result = 0; // 각 행에서 가장 작은 값 중에서 가장 큰 값
        for (int i = 0; i < N; i++) {
            int tmp = Integer.MAX_VALUE;
            for (String input : br.readLine().split(" ")) {
		            // 행에서 가장 작은 값을 찾는다.
                tmp = Math.min(tmp, Integer.parseInt(input));
            }
            // 가장 큰 수를 갱신한다.
            result = Math.max(result, tmp);
        }

        System.out.println("정답 : " + result);
    }
}
```
<br/>

## 실전 문제 - 1이 될 때까지

### 문제 설명

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-18_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11 04 47](https://github.com/user-attachments/assets/8d821212-570e-4dfe-b945-fb1a0f26c100)


### 코드

- N이 K로 나누어진다면(나머지 = 0) K로 나눈 값을 저장한다.
- N이 K로 나누어지지 않는다면(나머지 ≠ 0) 1을 뺀 값을 저장한다.
- 두 과정 모두 연산 횟수 + 1을 한다.

```java
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int K = sc.nextInt();

        int count = 0;
        while (N != 1) {
            if (N % K == 0) { // K로 나누어질 때
                N /= K;
            } else {
                N--;
            }
            count++;
        }

        System.out.println(count);
    }
}
```
<br/>

그러나 위 방법은 N이 매우 클 때, 시간 초과가 발생한다. 

연산 횟수를 최소화하기 위해서, 반복문을 수행할 때마다 N이 K로 나누어지도록 만들어준다.

```java
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        long N = sc.nextInt(); // ex) 30
        int K = sc.nextInt(); // ex) 11

        long count = 0;
        while (N >= K) {
            // **1. (N - 1) 연산 최소화**
            // N이 K로 나누어지지 않을 때, 한 번에 빼기 연산을 수행해 N을 K로 나누어 떨어지는 값으로 만든다.
            // 예시: N = 30, K = 11
            // 30을 11로 나누면 나머지는 8. 따라서, 30 -> 22로 만들기 위해 (N - 1)을 8번 반복하지 않고,
            // 한 번에 8을 빼서 N을 22로 만든다.
            long target = (N / K) * K; // N을 K로 나누어떨어지는 가장 가까운 값으로 만든다.
            count += (N - target); // N을 target(target은 N이 K로 나누어지기 위한 가장 가까운 값)으로 만들기 위해 필요한 (N - 1) 연산 횟수를 더한다.
            N = target; // K로 나누어떨어지는 N 값을 갱신한다.

            // **2. 나누기 연산**
            if (N < K) {
                break; // N이 K보다 작으면 더 이상 K로 나눌 수 없으므로 루프를 종료한다.
            }
            N /= K; // K로 나누기
            count++; // 나누기 연산 1회 수행
        }

        // **3. N < K && N > 1인 경우**
        // N == 1을 만들기 위해 (N - 1) 연산을 반복한다.
        // 예시: N = 2 -> 1을 만들기 위해 1번 빼야 한다.
        System.out.println(count + (N - 1));
    }
}
```
