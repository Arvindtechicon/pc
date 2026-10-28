# Program 2: OpenMP Static Scheduling with Chunks of 2

## Source code

```c
#include <stdio.h>
#include <omp.h>

int main(void) {
    int n = 16, thread;
    printf("\\nEnter the number of tasks: ");
    scanf("%d", &n);
    printf("\\nEnter the number of threads: ");
    scanf("%d", &thread);

    omp_set_num_threads(thread);
    printf("\\n--------------------------------------\\n");

    #pragma omp parallel for schedule(static, 2)
    for (int i = 0; i < n; i++) {
        printf("Thread %d executes iteration %d\n", omp_get_thread_num(), i);
    }
    return 0;
}
```

## Sample input from the supplied document

```text
Enter the number of tasks: 24
Enter the number of threads: 12
```

## Sample output from the supplied document

Output order may vary.

```text
Thread 1 executes iteration 2
Thread 1 executes iteration 3
Thread 4 executes iteration 8
Thread 4 executes iteration 9
Thread 6 executes iteration 12
Thread 6 executes iteration 13
Thread 9 executes iteration 18
Thread 9 executes iteration 19
Thread 7 executes iteration 14
Thread 7 executes iteration 15
Thread 10 executes iteration 20
Thread 10 executes iteration 21
Thread 0 executes iteration 0
Thread 0 executes iteration 1
Thread 2 executes iteration 4
Thread 2 executes iteration 5
Thread 3 executes iteration 6
Thread 3 executes iteration 7
Thread 5 executes iteration 10
Thread 5 executes iteration 11
Thread 11 executes iteration 22
Thread 11 executes iteration 23
Thread 8 executes iteration 16
Thread 8 executes iteration 17
```
