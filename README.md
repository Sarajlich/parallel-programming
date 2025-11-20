# Muhamed-Sarajlic-Parallel-Programming-Assignments

***Code:***

- MPI_Allgather:
used to to gather lolcal array size from all processes
this allowed the process to know how many elements each rank will recieve and where their data begins in the global array

- MPI_Scatterv:
distributing chunks of global array from 0 to all ranks

- MPI_Reduce:
collecting all partial sums and computing final sum

- Calculating local array size (ensuring that leftovers are properly distributed):
int base = ncells / nprocs;
int rem  = ncells % nprocs;
int nsize = base + (rank < rem ? 1 : 0);
int start = rank * base + (rank < rem ? rank : rem);

- a_local (ensuring that MPI processes allocates memory for its portion of global array):
double *a_local = (double *)malloc(nsize * sizeof(double));
if (a_local == NULL) {
    fprintf(stderr, "Rank %d: failed to allocate a_local\n", rank);
    MPI_Abort(comm, 1);
}



***Screenshots:***

![Run with 2 processes](images/ss_np2.png)
- global array is at rank 0
- both partial sums are combined with MPI_Reduce
- total sum is 50,005,000.00
- scatter and reduce timings are very small

![Run with 4 processes](images/ss_np4.png)
- timing increases a bit due to more processes communication
- result is still 50005000.00

![Run with 8 processes - part 1](images/ss_np8p1.png)
![Run with 8 processes - part 2](images/ss_np8p2.png)
- 8 processes means that each process will recieve 1250 elements
- scatter timing is a bit higher
- computing time decreases (each rank is processing less elements)