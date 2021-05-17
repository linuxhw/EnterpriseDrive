Micron NVMe Drives
==================

This is a list of all tested Micron NVMe drive models and their MTBFs. See more
info on reliability test in the [README](https://github.com/linuxhw/EnterpriseDrive).

NVME by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Micron    | MTFDHAL1T2MCF-1... | 1.2 TB | 1       | 1120  | 0     | 3.07   |
| Micron    | 2200S NVMe         | 256 GB | 1       | 272   | 0     | 0.75   |
| Micron    | 9300_MTFDHAL3T2TDR | 3.2 TB | 20      | 190   | 0     | 0.52   |
| Micron    | 9300_MTFDHAL7T6TDP | 7.6 TB | 30      | 144   | 0     | 0.40   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 52      | 89    | 0     | 0.24   |
| Micron    | 7300_MTFDHBE1T6TDG | 1.6 TB | 2       | 64    | 0     | 0.18   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 15      | 61    | 0     | 0.17   |
| Micron    | 7300_MTFDHBE960TDF | 960 GB | 4       | 25    | 0     | 0.07   |
