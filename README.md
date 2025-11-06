# Muhamed-Sarajlic-Parallel-Programming-Assignments
******Assignment 5******
- implemented timestep.c and timestep_opt1/2/3
- added flags -fno-trapping-math and -fno-math-errno to Makefile


***Running make on timestep.c, output:***

student@itcenter-lab128:~/Desktop/Muhamed-Sarajlic-Parallel-Programming-Assignments$ make
gcc -g -O3 -fstrict-aliasing -ftree-vectorize -fopenmp-simd -march=native -mtune=native -mprefer-vector-width=256 -fopt-info-vec-optimized -fopt-info-vec-missed   -c -o main.o main.c
main.c:10:22: optimized: loop vectorized using 32 byte vectors
main.c:20:15: missed: statement clobbers memory: mymindt_6 = timestep (10000000, 9.800000000000000710542735760100185871124267578125e+0, 9.499999999999999555910790149937383830547332763671875e-1, &celltype, &H, &U, &V, &dx, &dy);
/usr/include/x86_64-linux-gnu/bits/stdio2.h:112:10: missed: statement clobbers memory: __printf_chk (1, "Minimum dt is %lf\n", mymindt_6);
gcc -g -O3 -fstrict-aliasing -ftree-vectorize -fopenmp-simd -march=native -mtune=native -mprefer-vector-width=256 -fopt-info-vec-optimized -fopt-info-vec-missed   -c -o timestep.o timestep.c
timestep.c:9:22: missed: couldn't vectorize loop
timestep.c:9:22: missed: not vectorized: control flow in loop.
timestep.c:11:25: missed: statement clobbers memory: wavespeed_46 = sqrt (_9);
gcc -g -O3 -fstrict-aliasing -ftree-vectorize -fopenmp-simd -march=native -mtune=native -mprefer-vector-width=256 -fopt-info-vec-optimized -fopt-info-vec-missed   -c -o timer.o timer.c
timer.c:9:5: missed: statement clobbers memory: clock_gettime (1, tstart_cpu_2(D));
timer.c:14:5: missed: statement clobbers memory: clock_gettime (1, &tstop_cpu);
gcc -g -O3 -fstrict-aliasing -ftree-vectorize -fopenmp-simd -march=native -mtune=native -mprefer-vector-width=256 -fopt-info-vec-optimized -fopt-info-vec-missed -o stream_triad main.o timestep.o timer.o -lm


***Running timestep_opt1.c, output:***
student@itcenter-lab128:~/Desktop/Muhamed-Sarajlic-Parallel-Programming-Assignments$ make
gcc -g -O3 -fno-trapping-math -fno-math-errno -fstrict-aliasing -ftree-vectorize -fopenmp-simd -march=native -mtune=native -mprefer-vector-width=256 -fopt-info-vec-optimized -fopt-info-vec-missed   -c -o timestep_opt1.o timestep_opt1.c
timestep_opt1.c:9:9: optimized: loop vectorized using 32 byte vectors
timestep_opt1.c:11:7: optimized: loop vectorized using 16 byte vectors
timestep_opt1.c:9:9: optimized: loop vectorized using 32 byte vectors
gcc -g -O3 -fno-trapping-math -fno-math-errno -fstrict-aliasing -ftree-vectorize -fopenmp-simd -march=native -mtune=native -mprefer-vector-width=256 -fopt-info-vec-optimized -fopt-info-vec-missed -o stream_triad main.o timestep_opt1.o timer.o -lm

***Running timestep_opt2.c, output:***
student@itcenter-lab128:~/Desktop/Muhamed-Sarajlic-Parallel-Programming-Assignments$ make
gcc -g -O3 -fno-trapping-math -fno-math-errno -fstrict-aliasing -ftree-vectorize -fopenmp-simd -march=native -mtune=native -mprefer-vector-width=256 -fopt-info-vec-optimized -fopt-info-vec-missed   -c -o timestep_opt2.o timestep_opt2.c
timestep_opt2.c:9:9: optimized: loop vectorized using 32 byte vectors
timestep_opt2.c:11:7: optimized: loop vectorized using 16 byte vectors
timestep_opt2.c:9:9: optimized: loop vectorized using 32 byte vectors
gcc -g -O3 -fno-trapping-math -fno-math-errno -fstrict-aliasing -ftree-vectorize -fopenmp-simd -march=native -mtune=native -mprefer-vector-width=256 -fopt-info-vec-optimized -fopt-info-vec-missed -o stream_triad main.o timestep_opt2.o timer.o -lm

***Running timestep_opt3.c, output:***
student@itcenter-lab128:~/Desktop/Muhamed-Sarajlic-Parallel-Programming-Assignments$ make
gcc -g -O3 -fno-trapping-math -fno-math-errno -fstrict-aliasing -ftree-vectorize -fopenmp-simd -march=native -mtune=native -mprefer-vector-width=256 -fopt-info-vec-optimized -fopt-info-vec-missed   -c -o timestep_opt3.o timestep_opt3.c
timestep_opt3.c:8:9: optimized: loop vectorized using 32 byte vectors
timestep_opt3.c:10:7: optimized: loop vectorized using 16 byte vectors
timestep_opt3.c:8:9: optimized: loop vectorized using 32 byte vectors
gcc -g -O3 -fno-trapping-math -fno-math-errno -fstrict-aliasing -ftree-vectorize -fopenmp-simd -march=native -mtune=native -mprefer-vector-width=256 -fopt-info-vec-optimized -fopt-info-vec-missed -o stream_triad main.o timestep_opt3.o timer.o -lm


***Likwid is not worikng (access denied), so I followed instructions by assistant and used perf:***
1) Perf for opt1
student@itcenter-lab128:~/Desktop/Muhamed-Sarajlic-Parallel-Programming-Assignments$ sudo perf stat -e branch-misses,bus-cycles,cache-misses,cache-references,cpu-cycles,instructions ./stream_triad
Minimum dt is 0.016964

 Performance counter stats for './stream_triad':

            242332      branch-misses                                                         
          37496368      bus-cycles                                                            
           7055489      cache-misses                     #   75,68% of all cache refs         
           9322800      cache-references                                                      
        1237380182      cpu-cycles                                                            
         781632362      instructions                     #    0,63  insn per cycle            

       0,375440320 seconds time elapsed

       0,165996000 seconds user
       0,210995000 seconds sys

2) Perf for opt2
student@itcenter-lab128:~/Desktop/Muhamed-Sarajlic-Parallel-Programming-Assignments$ sudo perf stat -e branch-misses,bus-cycles,cache-misses,cache-references,cpu-cycles,instructions ./stream_triad
Minimum dt is 0.016964

 Performance counter stats for './stream_triad':

            305411      branch-misses                                                         
          42269232      bus-cycles                                                            
           7492562      cache-misses                     #   71,69% of all cache refs         
          10451182      cache-references                                                      
        1394884679      cpu-cycles                                                            
         801105489      instructions                     #    0,57  insn per cycle            

       0,457525938 seconds time elapsed

       0,172898000 seconds user
       0,251852000 seconds sys

3) Perf for opt3
student@itcenter-lab128:~/Desktop/Muhamed-Sarajlic-Parallel-Programming-Assignments$ sudo perf stat -e branch-misses,bus-cycles,cache-misses,cache-references,cpu-cycles,instructions ./stream_triad 
Minimum dt is 0.016964

 Performance counter stats for './stream_triad':

            307594      branch-misses                                                         
          42238213      bus-cycles                                                            
           7371856      cache-misses                     #   73,16% of all cache refs         
          10076372      cache-references                                                      
        1393861031      cpu-cycles                                                            
         807629400      instructions                     #    0,58  insn per cycle            

       0,426974814 seconds time elapsed

       0,165334000 seconds user
       0,258957000 seconds sys


***Iteration opt1***
- IPC = 0.63 --> its decent but not high, partial vectorization (not all loops use full SIMD width)
- Cache miss rate 75.68% --> high, memory access pattern is likely not optimized
- Exec time 0.375s --> fastest amont all 3 tests
- Partially vectorized 

***Iteration opt2***
- Higher CPU cycles and longer runtime 0.457s (slower than opt1)
- IPC 0.57 --> slightly less efficient per cycle
- Miss rate ~71% so memory access is a bit better
- Fully vectorized

***Iteration opt3***
- Similar to opt2 --> high cycle count and similar IPC (~0.58)
- Slightly better time (0.426s)
- Fully Vectorized


***What vector length instructions were used and which are the best?***

Vector length used for all iterations is 32 bytes or 256 bits, and that is the best match, because my processor’s maximum SIMD width is 256-bit (AVX) — this can be confirmed in the lscpu output, where the avx flag shows the CPU supports 256-bit SIMD instructions.

student@itcenter-lab128:~/Desktop/Muhamed-Sarajlic-Parallel-Programming-Assignments$ lscpu
Architecture:             x86_64
  CPU op-mode(s):         32-bit, 64-bit
  Address sizes:          36 bits physical, 48 bits virtual
  Byte Order:             Little Endian
CPU(s):                   4
  On-line CPU(s) list:    0-3
Vendor ID:                GenuineIntel
  Model name:             Intel(R) Core(TM) i3-2120 CPU @ 3.30GHz
    CPU family:           6
    Model:                42
    Thread(s) per core:   2
    Core(s) per socket:   2
    Socket(s):            1
    Stepping:             7
    CPU max MHz:          3300,0000
    CPU min MHz:          1600,0000
    BogoMIPS:             6585.23
    Flags:                fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse
                           sse2 ht tm pbe syscall nx rdtscp lm constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonst
                          op_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr pdcm pcid sse
                          4_1 sse4_2 popcnt tsc_deadline_timer xsave avx lahf_lm epb pti ssbd ibrs ibpb stibp tpr_shadow flexpr
                          iority ept vpid xsaveopt dtherm arat pln pts vnmi md_clear flush_l1d
Virtualization features:  
  Virtualization:         VT-x
Caches (sum of all):      
  L1d:                    64 KiB (2 instances)
  L1i:                    64 KiB (2 instances)
  L2:                     512 KiB (2 instances)
  L3:                     3 MiB (1 instance)
NUMA:                     
  NUMA node(s):           1
  NUMA node0 CPU(s):      0-3
Vulnerabilities:          
  Gather data sampling:   Not affected
  Itlb multihit:          KVM: Mitigation: VMX disabled
  L1tf:                   Mitigation; PTE Inversion; VMX conditional cache flushes, SMT vulnerable
  Mds:                    Mitigation; Clear CPU buffers; SMT vulnerable
  Meltdown:               Mitigation; PTI
  Mmio stale data:        Unknown: No mitigations
  Reg file data sampling: Not affected
  Retbleed:               Not affected
  Spec rstack overflow:   Not affected
  Spec store bypass:      Mitigation; Speculative Store Bypass disabled via prctl
  Spectre v1:             Mitigation; usercopy/swapgs barriers and __user pointer sanitization
  Spectre v2:             Mitigation; Retpolines; IBPB conditional; IBRS_FW; STIBP conditional; RSB filling; PBRSB-eIBRS Not af
                          fected; BHI Not affected
  Srbds:                  Not affected
  Tsx async abort:        Not affected