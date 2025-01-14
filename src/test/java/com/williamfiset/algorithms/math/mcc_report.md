# Test Report for MCC
Source file:
> https://github.com/williamfiset/Algorithms/blob/master/src/main/java/com/williamfiset/algorithms/math/CompressedPrimeSieve.java

Function for testing: primeSieve()
This function do:
> Returns an array of longs with each bit indicating whether a number is prime or not. Use the isNotSet and setBit methods to toggle to bits for each number.

Function code:
```
  public static long[] primeSieve(int limit) {
    final int numChunks = (int) Math.ceil(limit / NUM_BITS);
    final int sqrtLimit = (int) Math.sqrt(limit);
    long[] chunks = new long[numChunks];
    chunks[0] = 1; // 1 as not prime
    for (int i = 3; i <= sqrtLimit; i += 2)
      if (isNotSet(chunks, i))
        for (int j = i * i; j <= limit; j += i)
          if (isNotSet(chunks, j)) {
            setBit(chunks, j);
          }
    return chunks;
  }
```
![alt text](https://drive.google.com/uc?id=12iKHCBtJjex9ZX0XL69J-nCZTHkXsq1y)

## Graphs

### Flow chart
![alt text](https://drive.google.com/uc?id=1DjkmdT-PoequO10YDOr8me2rv2Fyml_N)

### Control-flow graph
![alt text](https://drive.google.com/uc?id=1cLUdTxec5WJBWkyrNpk2vEmLs8Y0I8SY)
### MCC Coverage testcase
| Path                                                   | i <= sqrtLimit | isNotSet(chunk, i) | j <= limit | isNotSet(chunk,j) | Test case               | Expected output   | Actual output     | Result |
|--------------------------------------------------------|----------------|--------------------|------------|-------------------|-------------------------|-------------------|-------------------|--------|
| 1 -> 2-5 -> 6 -> 7 -> 6 -> 12-13                       | F              |                    |            |                   | limit = 8               | [1]               | [1]               | PASS   |
| 1 -> 2-5 -> 6 -> 7 -> 6 -> 12-13                       | T              | T                  |            |                   | limit = 9               | [17]              | [17]              | PASS   |
| 1 -> 2-5 -> 6 -> 7 -> 6 -> 12-13                       | T              | F                  |            |                   | limit = 100 (and i = 9) | [823970606298257] | [823970606298257] | PASS   |
| 1 -> 2-5 -> 6 -> 7 -> 6 -> 12-13                       |                | F                  |            |                   | limit = 8               | [1]               | [1]               | PASS   |
| 1 -> 2-5 -> 6 -> 7 ->8 -> 6-> 12-13                    | T              | T                  | F          |                   | Not happened            | [1]               | [1]               | PASS   |
| 1 -> 2-5 -> 6 -> 7 ->8 -> 6-> 12-13                    | T              | T                  | T          |                   | limit = 15              | [145]             | [145]             | PASS   |
| 1 -> 2-5 -> 6 -> 7 ->8 -> 9 -> 8 -> 6-> 12-13          | T              | T                  | T          | F                 | limit = 15 (and j = 12) | [145]             | [145]             | PASS   |
| 1 -> 2-5 -> 6 -> 7 ->8 -> 9 -> 10-11 -> 8 -> 6-> 12-13 | T              | T                  | T          | T                 | limit = 15              | [145]             | [145]             | PASS   |

