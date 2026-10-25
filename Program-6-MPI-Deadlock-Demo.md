# Program 6: MPI Point-to-Point Communication and Deadlock Demonstration

## Source code as shown in the supplied document

```c
#include <stdio.h>
#include <mpi.h>

int main(int argc, char *argv[]) {
    int rank, data_send, data_recv;

    MPI_Init(&argc, &argv);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    data_send = rank;

    if (rank == 0) {
        MPI_Send(&data_send, 1, MPI_INT, 1, 0, MPI_COMM_WORLD);
        MPI_Recv(&data_recv, 1, MPI_INT, 1, 0, MPI_COMM_WORLD, MPI_STATUS_IGNORE);
    } else if (rank == 1) {
        MPI_Send(&data_send, 1, MPI_INT, 0, 0, MPI_COMM_WORLD);
        MPI_Recv(&data_recv, 1, MPI_INT, 0, 0, MPI_COMM_WORLD, MPI_STATUS_IGNORE);
    }

    printf("Process %d received message: %d\\n", rank, data_recv);
    MPI_Finalize();
    return 0;
}
```

## Sample output reported in the supplied document

```text
Process 1 received message: 0
Process 0 received message: 1
```

## Important note

The shown code calls blocking `MPI_Send` on both processes before either process calls `MPI_Recv`. Depending on the MPI implementation and message buffering, this can deadlock. The output above is what the document reports, but it is not guaranteed for this exact call order.

The document's title refers to avoiding deadlock by changing the call sequence, but the printed code does not include that change. This file preserves the source code as supplied rather than silently changing the program.
