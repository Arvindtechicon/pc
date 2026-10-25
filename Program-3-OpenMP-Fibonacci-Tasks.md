# Program 3: OpenMP Fibonacci Using Tasks

## Source code

```c
#include <stdio.h>
#include <omp.h>
#include <time.h>

long int ser_fib(long int n) {
    if (n < 2) return n;
    long int x = ser_fib(n - 1);
    long int y = ser_fib(n - 2);
    return x + y;
}

long int fib(long int n) {
    if (n < 2) return n;
    long int x, y;

    #pragma omp task shared(x)
    x = fib(n - 1);

    #pragma omp task shared(y)
    y = fib(n - 2);

    #pragma omp taskwait
    return x + y;
}

int main(void) {
    long int n = 10, result;
    clock_t start, end;
    double cpu_time;

    printf("\\nEnter the value of n: ");
    scanf("%ld", &n);

    start = clock();
    #pragma omp parallel
    {
        #pragma omp single
        result = fib(n);
    }
    end = clock();
    cpu_time = (double)(end - start) / CLOCKS_PER_SEC;
    printf("Fibonacci(%ld) = %ld\\n", n, result);
    printf("The time used to execute the program in parallel mode = %f\\n", cpu_time);

    start = clock();
    result = ser_fib(n);
    end = clock();
    cpu_time = (double)(end - start) / CLOCKS_PER_SEC;
    printf("Fibonacci(%ld) = %ld\\n", n, result);
    printf("The time used to execute the program in sequential mode = %f\\n", cpu_time);
    return 0;
}
```

## Sample output from the supplied document

Input: `32`

```text
Fibonacci(32) = 2178309
The time used to execute the program in parallel mode = 3.370000
Fibonacci(32) = 2178309
The time used to execute the program in sequential mode = 0.157000
```

**Note:** This recursive task version may be inefficient because it creates many small tasks and performs exponential recursive work. Timing values vary by system.
