# Program 4: Find Prime Numbers from 1 to n Using OpenMP

## Source code

```c
#include <stdio.h>
#include <omp.h>
#include <time.h>

int is_prime(int n) {
    if (n < 2) return 0;
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0) return 0;
    return 1;
}

int main(void) {
    long n = 10000000;
    clock_t start, end;
    double cpu_time;

    printf("\\nThe range of numbers is 1 to %ld\\n", n);
    printf("\\n--------------------------------------\\n");

    start = clock();
    for (int i = 1; i <= n; i++)
        is_prime(i);
    end = clock();
    cpu_time = (double)(end - start) / CLOCKS_PER_SEC;
    printf("Time to compute prime numbers serially: %f\\n", cpu_time);

    start = clock();
    #pragma omp parallel for
    for (int i = 1; i <= n; i++)
        is_prime(i);
    end = clock();
    cpu_time = (double)(end - start) / CLOCKS_PER_SEC;
    printf("Time to compute prime numbers Parallel: %f\\n", cpu_time);
    return 0;
}
```

## Sample outputs from the supplied document

### Output 1 (`n = 10,000,000`)

```text
Time to compute prime numbers serially: 2.403000
Time to compute prime numbers Parallel: 0.491000
```

### Output 2 (`n = 1,000,000`)

```text
Time to compute prime numbers serially: 0.095000
Time to compute prime numbers Parallel: 0.025000
```

### Output 3 (`n = 100,000`)

```text
Time to compute prime numbers serially: 0.006000
Time to compute prime numbers Parallel: 0.000000
```

**Note:** The source initializes `n` to `10000000`. The smaller cases require changing `n`. The program calls `is_prime` but does not print the prime numbers themselves.
