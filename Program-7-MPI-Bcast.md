# Program 7: MPI_Bcast Broadcast Operation

## Source code

```c
#include <stdio.h>
#include <mpi.h>

int main(int argc, char **argv) {
    int rank, data = 0;

    MPI_Init(&argc, &argv);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);

    if (rank == 0)
        data = 100;

    MPI_Bcast(&data, 1, MPI_INT, 0, MPI_COMM_WORLD);
    printf("Process %d received data: %d\\n", rank, data);

    MPI_Finalize();
    return 0;
}
```

## Sample output from the supplied document

```text
Process 0 received data: 100
Process 1 received data: 100
Process 2 received data: 100
Process 3 received data: 100
```

Run with four MPI processes to match the sample output. Output line order may vary.
