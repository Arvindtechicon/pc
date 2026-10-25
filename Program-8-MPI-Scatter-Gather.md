# Program 8: MPI_Scatter and MPI_Gather

## Source code

```c
#include <stdio.h>
#include <mpi.h>

int main(int argc, char **argv) {
    int rank, size;
    int send_data[4] = {10, 20, 30, 40};
    int recv_data;

    MPI_Init(&argc, &argv);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    MPI_Comm_size(MPI_COMM_WORLD, &size);

    MPI_Scatter(send_data, 1, MPI_INT, &recv_data, 1, MPI_INT, 0, MPI_COMM_WORLD);
    printf("Process %d received: %d\\n", rank, recv_data);

    recv_data += 1;
    MPI_Gather(&recv_data, 1, MPI_INT, send_data, 1, MPI_INT, 0, MPI_COMM_WORLD);

    if (rank == 0) {
        printf("Gathered data: ");
        for (int i = 0; i < size; i++)
            printf("%d ", send_data[i]);
        printf("\\n");
    }

    MPI_Finalize();
    return 0;
}
```

## Sample output from the supplied document

```text
Process 0 received: 10
Process 1 received: 20
Process 2 received: 30
Process 3 received: 40
Gathered data: 11 21 31 41
```

**Important:** Run with exactly four MPI processes. The source arrays are sized for four values.
