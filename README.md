# Parallel Computing Lab (BCS702)

Programs 1–9 transcribed from the supplied lab document. Each program has its own Markdown file with the source code and sample output.

## Programs

1. [OpenMP Sequential and Parallel Merge Sort](Program-1-OpenMP-Merge-Sort.md)
2. [OpenMP Static Scheduling with Chunks of 2](Program-2-OpenMP-Static-Scheduling.md)
3. [OpenMP Fibonacci Using Tasks](Program-3-OpenMP-Fibonacci-Tasks.md)
4. [Prime Numbers Using OpenMP](Program-4-OpenMP-Prime-Numbers.md)
5. [MPI_Send and MPI_Recv](Program-5-MPI-Send-Recv.md)
6. [MPI Point-to-Point Communication and Deadlock Demonstration](Program-6-MPI-Deadlock-Demo.md)
7. [MPI_Bcast Broadcast Operation](Program-7-MPI-Bcast.md)
8. [MPI_Scatter and MPI_Gather](Program-8-MPI-Scatter-Gather.md)
9. [MPI_Reduce and MPI_Allreduce](Program-9-MPI-Reduce-Allreduce.md)

## Notes

- These are Markdown files, so source code is shown in fenced code blocks for easy copying.
- OpenMP programs require a C compiler with OpenMP support.
- MPI programs require an MPI implementation such as MPICH or Open MPI.
- Sample outputs are transcribed from the supplied document. Timing values and process output order can vary between systems.
- Program 6's blocking send/receive sequence may deadlock on some MPI implementations, as noted in the source document.
- Program 8's source uses arrays sized for four processes; run it with exactly four MPI processes.
- Program 9's source demonstrates `MPI_SUM` and `MPI_MAX`. It does not implement `MPI_MIN` or `MPI_PROD`, despite the title note in the source document.
