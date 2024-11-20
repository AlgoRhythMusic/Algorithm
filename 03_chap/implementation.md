## 구현이란?

> 머릿속에 있는 알고리즘을 소스코드로 바꾸는 과정

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_3 48 22](https://github.com/user-attachments/assets/110b7b59-0482-4591-afb5-540bb1a3860b)


특별한 방법을 요구하는 것이 아닌, 생각한 알고리즘을 코드로 구현할 수 있는 능력을 요구한다.

1. 문제를 읽고 문제 풀이 방법을 고민한다.
2. 풀이 방법을 프로그래밍 언어로 구현한다.

완전 탐색은 기본적으로 프로그래밍 언어를 잘 사용할 수 있어야 한다. 즉, 각 언어에서 제공하는 라이브러리를 잘 다루는 것으로부터 시작한다.

## 예제 4-1. 상하좌우

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2 25 59](https://github.com/user-attachments/assets/05fcb491-cbe9-4918-89cd-757b8a030334)

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_2 26 16](https://github.com/user-attachments/assets/e9e4d9d2-2b77-4a01-987e-2c119bf7219b)

```java
public class Main {

    static int N;
    static Queue<String> que = new LinkedList<>();

    // 상하좌우
    static String[] dirs = {"U", "D", "L", "R"};
    static int[] dx = {0, 0, -1, 1};
    static int[] dy = {-1, 1, 0, 0};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        for (String input : br.readLine().split(" ")) {
            que.offer(input);
        }

        int[] pos = answer();
        int x = pos[1] + 1;
        int y = pos[0] + 1;
        System.out.println(y + " " + x);
    }

    static int[] answer() {
        /**
         * (0, 0)에서 출발한다.
         * 상하좌우로 이동하되, 범위를 벗어나는 입력은 무시한다.
         */
        int x = 0, y = 0;
        while (!que.isEmpty()) {
            String dir = que.poll();
            int[] pos = moveDir(dir, x, y);
            x = pos[1];
            y = pos[0];
        }

        return new int[]{y, x};
    }

    static int[] moveDir(String dir, int x, int y) {
        int cx = x;
        int cy = y;
        for (int d = 0; d < dirs.length; d++) {
            if (dirs[d].equals(dir)) {
                cx += dx[d];
                cy += dy[d];
                break;
            }
        }

        // 범위를 벗어나지 않는 경우, 이동한 좌표를 반환한다.
        if (cx >= 0 && cx < N && cy >= 0 && cy < N) {
            return new int[]{cy, cx};
        }
        // 범위를 벗어나는 경우, 현재 좌표를 그대로 사용한다.
        return new int[]{y, x};
    }

    static boolean isContains(int h, int m, int s) {
        return ((h + "") + (m + "") + (s + "")).contains("3");
    }

}
```

## 예제 4-2. 시각

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_3 10 38](https://github.com/user-attachments/assets/87254b65-94bc-4804-a497-2f2517ff058d)

```java
public class Main {

    static int N;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt(); // N시 59분 59초
        System.out.println(answer());
    }

    static int answer() {
        int count = 0;
        for (int h = 0; h <= N; h++) {
            for (int m = 0; m <= 59; m++) {
                for (int s = 0; s <= 59; s++) {
                    // h시 m분 s초에 '3'이 포함된 경우
                    if (isContains3(h) || isContains3(m) || isContains3(s)) {
                        count++;
                    }
                }
            }
        }
        return count;
    }

    static boolean isContains3(int time) {
        return String.valueOf(time).contains("3");
    }
}
```

## 실전 문제

![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2024-11-21_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_3 29 36](https://github.com/user-attachments/assets/cfa7a10d-5cca-4409-81fb-a783f770356b)

### 비효율적인 코드

```java
public class Main {

    static int row, col;
    static final int SIZE = 8;

    static int[] dx = {-1, 1};
    static int[] dy = {-1, 1};
    static int count;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        char[] inputs = br.readLine().toCharArray();
        row = (inputs[1] - '0') - 1;
        col = inputs[0] - 'a';

        answer();
        System.out.println(count);
    }

    static void answer() {
        moveUp();
        moveDown();
        moveLeft();
        moveRight();
    }

    static void moveUp() {
        // 위로 2칸, 수평 1칸
        int y = row - 2;
        for (int d = 0; d < dx.length; d++) {
            int x = col + dx[d];
            if (isNotOutOfRange(x, y)) {
                count++;
            }
        }
    }

    static void moveDown() {
        // 아래로 2칸, 수평 1칸
        int y = row + 2;
        for (int d = 0; d < dx.length; d++) {
            int x = col + dx[d];
            if (isNotOutOfRange(x, y)) {
                count++;
            }
        }
    }

    static void moveLeft() {
        // 수직 1칸, 왼쪽 2칸
        int x = col - 2;
        for (int d = 0; d < dy.length; d++) {
            int y = row + dy[d];
            if (isNotOutOfRange(x, y)) {
                count++;
            }
        }
    }

    static void moveRight() {
        // 수직 1칸, 오른쪽 2칸
        int x = col + 2;
        for (int d = 0; d < dy.length; d++) {
            int y = row + dy[d];
            if (isNotOutOfRange(x, y)) {
                count++;
            }
        }
    }

    static boolean isNotOutOfRange(int x, int y) {
        return x >= 0 && x < SIZE && y >= 0 && y < SIZE;
    }
}
```

### 개선된 코드

- 나이트의 이동 경로를 모두 포함하는 리스트(dirs)를 사용한다.

```java
public class Main {

    static int row, col;
    static final int SIZE = 8;

    static int count;
    static List<int[]> dirs = List.of(
            new int[]{-2, -1}, new int[]{-2, 1},
            new int[]{2, -1}, new int[]{2, 1},
            new int[]{-1, -2}, new int[]{1, -2},
            new int[]{-1, 2}, new int[]{1, 2}
    );

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        char[] inputs = br.readLine().toCharArray();
        row = (inputs[1] - '0') - 1;
        col = inputs[0] - 'a';

        move();
        System.out.println(count);
    }

    static void move() {
        for (int[] moveDir : dirs) {
            int moveRow = row + moveDir[0];
            int moveCol = col + moveDir[1];
            if (isNotOutOfRange(moveCol, moveRow)) {
                count++;
            }
        }
    }

    static boolean isNotOutOfRange(int x, int y) {
        return x >= 0 && x < SIZE && y >= 0 && y < SIZE;
    }
}
```
