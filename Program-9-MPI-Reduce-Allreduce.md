# Program 9: MPI_Reduce and MPI_Allreduce

## Source code

```c
#include <stdio.h>
#include <mpi.h>

int main(int argc, char **argv) {
    int rank, value, sum, max;

    MPI_Init(&argc, &argv);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);

    value = rank + 1;

    MPI_Reduce(&value, &sum, 1, MPI_INT, MPI_SUM, 0, MPI_COMM_WORLD);
    if (rank == 0)
        printf("Sum using Reduce: %d\\n", sum);

    MPI_Allreduce(&value, &max, 1, MPI_INT, MPI_MAX, MPI_COMM_WORLD);
    printf("Max using Allreduce (rank %d): %d\\n", rank, max);

    MPI_Finalize();
    return 0;
}
```

## Sample output from the supplied document

```text
Sum using Reduce: 10
Max using Allreduce (rank 0): 4
Max using Allreduce (rank 1): 4
Max using Allreduce (rank 2): 4
Max using Allreduce (rank 3): 4
```

Run with four MPI processes to match the sample output.

**Note:** The document mentions `MPI_MIN` and `MPI_PROD` in its title note, but the printed code only demonstrates `MPI_SUM` and `MPI_MAX`.
