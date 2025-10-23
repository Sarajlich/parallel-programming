# Muhamed-Sarajlic-Parallel-Programming-Assignments

Makefile: 
- added TARGET_SRC = aosoa_mesurement.cpp 

aosoa_measurement.cpp:
- SoA_type* AoSoA = new SoA_type[num_blocks] --> creating array of length "num_blocks", where each element storess 3 arrays (R, G and B) of size V
- delete[] AoSoA --> deallocating the memory what was created with "new SoA_type[num_blocks]"

Spreadsheet link:
https://docs.google.com/spreadsheets/d/18bF3Dgd5wo2opXQJeE-q7iRfA2sv3hcyMeU9E4ZkT20/edit?usp=sharing

Spreadsheet:
- V --> vector length
- 1K, 10K, 100K, 1M, 10M --> each of these columns represent a different total array length (From 1000 up to 10 000 000), these check with values in Makefile variable LENGTHS
- Numbers in cells --> measured executing time in milliseconds for each combination of N (array length) and V (vector length)
- Chart --> visualization of how runtime changes with increasing vector length V for each total array size N