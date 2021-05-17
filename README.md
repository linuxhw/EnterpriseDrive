Reliability Test For Enterprise Hard Drives
===========================================

This is a project to estimate reliability of enterprise HDD/SSD drives by the analysis
of SMART reports from servers. The primary aim of the project is to find drives with
longest power-on hours (POH) and minimal number of errors, i.e. maximal MTBF (mean time
between failures).

Everyone can contribute to this report by installing [hw-probe](https://github.com/linuxhw/hw-probe) to
their [OpenVZ 7 or Virtuozzo 7](https://wiki.openvz.org/) servers:

    sudo -E hw-probe -all -upload

Total drives: 42893.

Contents
--------

1. [ About          ](#about)
2. [ HDD by Model   ](#hdd-by-model)
3. [ HDD by Family  ](#hdd-by-family)
4. [ HDD by Vendor  ](#hdd-by-vendor)
5. [ SSD by Model   ](#ssd-by-model)
6. [ SSD by Family  ](#ssd-by-family)
7. [ SSD by Vendor  ](#ssd-by-vendor)
8. [ NVMe by Model  ](#nvme-by-model)
9. [ NVMe by Vendor ](#nvme-by-vendor)

About
-----

The structure of the reports directory is the following:

    {KIND OF DRIVE}/{VENDOR}/{MODEL PREFIX}/{MODEL}/{DRIVE ID}

    ( e.g. HDD/Seagate/ST9500/ST9500620NS/B0744A84D66D )

Based on SMART data we determine most reliable drive models and vendors by the
following formula:

    MTBF = MAX( Power_On_Hours / ( 1 + Number_Of_Important_Errors ) ) / ( 365*24 )

    ( i.e. MTBF = "Years before/between errors" )

Number_Of_Important_Errors — number of important errors that can indicate a drive failure:

* Current_Pending_Sector
* ECC_Uncorr_Error_Count
* End-to-End_Error
* Offline_Uncorrectable
* Reallocated_Event_Count
* Reallocated_Sector_Ct
* Reported_Uncorrect
* Soft_Read_Error_Rate
* Spin_Retry_Count
* Total_Pending_Sectors
* Unc_Soft_Read_Err_Rate

One can estimate reliability of a hard drive (i.e. probability that the unit will work
for some time T without failure) by:

    Reliability(T) = exp(-T/MTBF)

The list of important SMART attributes is taken from recent studies of Google [1],
Backblaze [2] and Acronis [3]. If an attribute exceeds the value of 1000 then it's
counted as '1000 + log10(X - 999)'.

The list of tracked attributes and MTBF calculation method can be discussed. Please
suggest your ideas in "issues".

You can perform your own analysis of collected reports if needed.

* [1] Google, "Failure Trends in a Large Disk Drive Population" (https://research.google.com/archive/disk_failures.pdf)
* [2] Backblaze, "Hard Drive SMART Stats" (https://www.backblaze.com/blog/hard-drive-smart-stats/)
* [3] Acronis, "Acronis Drive Monitor: Disk Health Calculation" (https://kb.acronis.com/content/9264)

HDD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See complete list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| WDC       | WD740ADFD-00NLR5   | 74 GB  | 1       | 4525  | 0     | 12.40  |
| Hitachi   | HDS725050KLA360    | 500 GB | 1       | 4323  | 0     | 11.84  |
| Hitachi   | HDS721010KLA33R... | 1 TB   | 1       | 3863  | 0     | 10.58  |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 1       | 3845  | 0     | 10.54  |
| Seagate   | ST32500NSSUN250G   | 250 GB | 2       | 3676  | 0     | 10.07  |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 2       | 3570  | 0     | 9.78   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 6       | 3499  | 0     | 9.59   |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 3       | 3499  | 0     | 9.59   |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 15      | 3820  | 1     | 8.96   |
| Hitachi   | HUA722050CLA330    | 500 GB | 2       | 3101  | 0     | 8.50   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 15      | 3247  | 1     | 8.44   |
| Seagate   | ST3320620AS        | 320 GB | 3       | 4393  | 5     | 8.35   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 3       | 3004  | 0     | 8.23   |
| WDC       | WD5000AAKS-00V6A0  | 500 GB | 1       | 2965  | 0     | 8.12   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 1       | 2955  | 0     | 8.10   |
| HP        | GB0500EAFYL        | 500 GB | 2       | 2889  | 0     | 7.92   |
| Hitachi   | HUA722020ALA330... | 2 TB   | 1       | 2886  | 0     | 7.91   |
| Samsung   | HD250HJ            | 250 GB | 1       | 2882  | 0     | 7.90   |
| Seagate   | ST32000645NS       | 2 TB   | 81      | 3043  | 16    | 7.71   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 8       | 3220  | 1     | 7.69   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 62      | 2957  | 1     | 7.67   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 1       | 2778  | 0     | 7.61   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 1       | 2735  | 0     | 7.49   |
| Seagate   | ST3320620A         | 320 GB | 2       | 2728  | 0     | 7.47   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 1       | 2726  | 0     | 7.47   |
| WDC       | WD1002FBYS-50A6B1  | 1 TB   | 1       | 2722  | 0     | 7.46   |
| Hitachi   | HDS721050CLA360    | 500 GB | 2       | 2693  | 0     | 7.38   |
| WDC       | WD1600JD-75HBB0    | 160 GB | 1       | 2640  | 0     | 7.23   |
| Toshiba   | DT01ABA300         | 3 TB   | 1       | 2632  | 0     | 7.21   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 23      | 2668  | 1     | 7.11   |
| Samsung   | HD753LJ            | 752 GB | 1       | 2559  | 0     | 7.01   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 2       | 2547  | 0     | 6.98   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 14      | 2872  | 1     | 6.96   |
| Seagate   | ST3250620NS        | 250 GB | 4       | 2532  | 0     | 6.94   |
| HP        | GB0250EAFYK        | 250 GB | 2       | 2531  | 0     | 6.93   |
| WDC       | WD3200AAKS-61L9A0  | 320 GB | 1       | 2526  | 0     | 6.92   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 1       | 2526  | 0     | 6.92   |
| HP        | GB0500C4413        | 500 GB | 2       | 3306  | 1     | 6.90   |
| Hitachi   | HUA723020ALA640... | 2 TB   | 1       | 2500  | 0     | 6.85   |
| WDC       | WD2500AAJS-22L7A0  | 250 GB | 1       | 2473  | 0     | 6.78   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 2       | 2433  | 0     | 6.67   |
| Seagate   | ST32000646NS       | 2 TB   | 2       | 2424  | 0     | 6.64   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 1       | 2420  | 0     | 6.63   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 30      | 2774  | 70    | 6.62   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 1       | 2403  | 0     | 6.59   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 5       | 2756  | 1     | 6.58   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 2       | 2359  | 0     | 6.46   |
| Hitachi   | HUA722010CLA330... | 1 TB   | 1       | 2354  | 0     | 6.45   |
| Seagate   | ST3250410AS        | 250 GB | 2       | 2506  | 165   | 6.44   |
| Maxtor    | STM3250310AS       | 250 GB | 1       | 2347  | 0     | 6.43   |
| Hitachi   | HDS721010CLA330    | 1 TB   | 1       | 2342  | 0     | 6.42   |
| Seagate   | ST2000VX000-1CU164 | 2 TB   | 1       | 2335  | 0     | 6.40   |
| HP        | MB1000GCWCV        | 1 TB   | 3       | 2306  | 0     | 6.32   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 10      | 2752  | 3     | 6.22   |
| HP        | GB1000EAMYC        | 1 TB   | 1       | 2228  | 0     | 6.11   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 10      | 2868  | 9     | 6.05   |
| WDC       | WD1001FALS-00E8B0  | 1 TB   | 1       | 2171  | 0     | 5.95   |
| Seagate   | ST3000VX000-1CU166 | 3 TB   | 23      | 2408  | 2     | 5.91   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 29      | 2288  | 1     | 5.91   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 27      | 2244  | 1     | 5.88   |
| Seagate   | ST3320620NS        | 320 GB | 4       | 2189  | 1     | 5.81   |
| WDC       | WD7502AAEX-00Y9A0  | 752 GB | 4       | 2095  | 0     | 5.74   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 5       | 2538  | 2     | 5.73   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 2       | 2078  | 0     | 5.69   |
| Hitachi   | HDP725050GLA360    | 500 GB | 3       | 2075  | 0     | 5.69   |
| Seagate   | ST3400620AS        | 400 GB | 1       | 2060  | 0     | 5.65   |
| Seagate   | ST2000VX000-1ES164 | 2 TB   | 1       | 2043  | 0     | 5.60   |
| WDC       | WD1600AAJS-08L7A0  | 160 GB | 1       | 2027  | 0     | 5.56   |
| HGST      | HDS724040ALE640    | 4 TB   | 6       | 2027  | 0     | 5.55   |
| Seagate   | ST2000NM0033       | 2 TB   | 1       | 1988  | 0     | 5.45   |
| Seagate   | ST2000NC000-1CX164 | 2 TB   | 1       | 1954  | 0     | 5.36   |
| Maxtor    | 6V160E0            | 160 GB | 2       | 1932  | 0     | 5.29   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 2       | 1929  | 0     | 5.29   |
| Seagate   | ST3000VX006-1HH166 | 3 TB   | 2       | 1926  | 0     | 5.28   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 4       | 1922  | 0     | 5.27   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 27      | 2016  | 1     | 5.21   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 1       | 1875  | 0     | 5.14   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 6       | 2205  | 1     | 5.11   |
| WDC       | WD6001FSYZ-01SS7B0 | 6 TB   | 3       | 1838  | 0     | 5.04   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 8       | 2025  | 11    | 5.02   |
| WDC       | WD2001FFSX-68JNUN0 | 2 TB   | 2       | 1823  | 0     | 5.00   |
| WDC       | WD2004FBYZ-01YCBB0 | 2 TB   | 5       | 1814  | 0     | 4.97   |
| Seagate   | ST91000640NS       | 1 TB   | 29      | 1908  | 1     | 4.89   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 2       | 1783  | 0     | 4.89   |
| Hitachi   | HDT725032VLA360    | 320 GB | 5       | 3607  | 7     | 4.88   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 2       | 1780  | 0     | 4.88   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 2       | 1777  | 0     | 4.87   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 1       | 1777  | 0     | 4.87   |
| WDC       | WD2002FYPS-01U1B1  | 2 TB   | 17      | 2729  | 200   | 4.84   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 426     | 2133  | 108   | 4.83   |
| HP        | GB0160EAFJE        | 160 GB | 2       | 2819  | 513   | 4.82   |
| WDC       | WD10EZEX-22RKKA0   | 1 TB   | 4       | 2102  | 1     | 4.82   |
| WDC       | WD5000BHTZ-04JCPV0 | 500 GB | 1       | 1758  | 0     | 4.82   |
| Toshiba   | MK0502TSKB         | 500 GB | 1       | 1752  | 0     | 4.80   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 9       | 1942  | 1     | 4.79   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 4       | 2680  | 3     | 4.78   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 1742  | 0     | 4.77   |
| HGST      | HUS724020ALA640    | 2 TB   | 178     | 1821  | 12    | 4.77   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 4       | 2703  | 4     | 4.75   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 15      | 2202  | 3     | 4.74   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 21      | 1810  | 7     | 4.74   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 20      | 1856  | 19    | 4.74   |
| HGST      | HUS726060ALE614    | 6 TB   | 144     | 1825  | 11    | 4.72   |
| Seagate   | ST3500630AS        | 500 GB | 1       | 1720  | 0     | 4.71   |
| WDC       | WD2500AAJS-00B4A0  | 250 GB | 1       | 1718  | 0     | 4.71   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 31      | 1960  | 43    | 4.68   |
| WDC       | WD4001FFSX-68JNUN0 | 4 TB   | 12      | 2035  | 1     | 4.67   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 15      | 1692  | 0     | 4.64   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 7       | 1676  | 0     | 4.59   |
| WDC       | WD5003AZEX-00S3DA0 | 500 GB | 15      | 1654  | 0     | 4.53   |
| Seagate   | ST500NM0011 00W... | 500 GB | 2       | 1647  | 0     | 4.51   |
| WDC       | WD5003ABYX-23 0... | 500 GB | 2       | 1645  | 0     | 4.51   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 53      | 1979  | 47    | 4.50   |
| Samsung   | HD103UJ            | 1 TB   | 25      | 2856  | 150   | 4.50   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 5       | 2547  | 5     | 4.45   |
| Seagate   | ST3500630NS        | 500 GB | 9       | 1613  | 0     | 4.42   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 7       | 2359  | 1     | 4.40   |
| HGST      | HUS724040ALA640    | 4 TB   | 101     | 1692  | 3     | 4.37   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 3       | 1763  | 1     | 4.36   |
| HGST      | HDN724040ALE640    | 4 TB   | 21      | 1586  | 0     | 4.35   |
| Seagate   | ST33000651AS       | 3 TB   | 4       | 2291  | 10    | 4.33   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 14      | 1730  | 1     | 4.32   |
| Seagate   | ST33000650NS       | 3 TB   | 18      | 2411  | 69    | 4.31   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 20      | 1978  | 75    | 4.29   |
| Seagate   | ST9500620NS        | 500 GB | 27      | 1746  | 1     | 4.25   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 6       | 2173  | 2     | 4.22   |
| WDC       | WD5000AAKX-003CA0  | 500 GB | 3       | 2072  | 3     | 4.21   |
| Seagate   | ST2000NM0024-1H... | 2 TB   | 9       | 1537  | 0     | 4.21   |
| Seagate   | ST6000NM0024-1H... | 6 TB   | 1627    | 1782  | 17    | 4.21   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 1       | 1537  | 0     | 4.21   |
| WDC       | WD6402AAEX-00Y9A0  | 640 GB | 3       | 2286  | 677   | 4.21   |
| Toshiba   | HDWE160            | 6 TB   | 73      | 1608  | 1     | 4.19   |
| WDC       | WD20EARX-00MMMB0   | 2 TB   | 2       | 2514  | 2     | 4.14   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 8       | 1880  | 2     | 4.13   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 49      | 2011  | 25    | 4.10   |
| Hitachi   | HDT721050SLA360    | 500 GB | 1       | 1493  | 0     | 4.09   |
| WDC       | WD2003FYYS-05T8B0  | 2 TB   | 2       | 1487  | 0     | 4.08   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 3       | 1485  | 0     | 4.07   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 28      | 1483  | 0     | 4.07   |
| Seagate   | ST320DM000-1BC14C  | 320 GB | 2       | 1479  | 0     | 4.05   |
| WDC       | WD2500HHTZ-04N21V0 | 250 GB | 3       | 1473  | 0     | 4.04   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 1       | 1465  | 0     | 4.01   |
| WDC       | WD1000CHTZ-04JCPV1 | 1 TB   | 4       | 1464  | 0     | 4.01   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 1       | 1463  | 0     | 4.01   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 18      | 2882  | 291   | 4.00   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 3       | 1447  | 0     | 3.97   |
| HGST      | HUS724040ALE640    | 4 TB   | 16      | 1443  | 0     | 3.96   |
| Toshiba   | MK1002TSKB         | 1 TB   | 9       | 1438  | 0     | 3.94   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 16      | 1480  | 34    | 3.94   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 4       | 1433  | 0     | 3.93   |
| WDC       | WD2000FYYZ-01UL1B3 | 2 TB   | 1       | 1427  | 0     | 3.91   |
| Samsung   | SP0812C            | 80 GB  | 1       | 1426  | 0     | 3.91   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 8       | 1601  | 31    | 3.90   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 29      | 1622  | 212   | 3.89   |
| WDC       | WD3000HLHX-01JJPV0 | 304 GB | 2       | 1414  | 0     | 3.87   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 5       | 1802  | 22    | 3.86   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 35      | 1826  | 52    | 3.85   |
| WDC       | WD10EALX-089BA0    | 1 TB   | 7       | 1772  | 2     | 3.85   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 55      | 1442  | 4     | 3.85   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 11      | 1399  | 0     | 3.83   |
| WDC       | WD20EADS-65R6B1    | 2 TB   | 1       | 2788  | 1     | 3.82   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 10      | 2280  | 203   | 3.81   |
| HP        | MB1000GCEHH        | 1 TB   | 4       | 2760  | 578   | 3.80   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 3       | 1374  | 0     | 3.77   |
| WDC       | WD5000AUDX-61WNHY0 | 500 GB | 1       | 1373  | 0     | 3.76   |
| HGST      | HUS726030ALA610    | 3 TB   | 47      | 1391  | 1     | 3.76   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 1       | 1371  | 0     | 3.76   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 7       | 2160  | 401   | 3.75   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 6       | 2096  | 3     | 3.74   |
| WDC       | WD5002AALX-32Z3A0  | 500 GB | 7       | 1360  | 0     | 3.73   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 1       | 1356  | 0     | 3.72   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 114     | 1635  | 98    | 3.72   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 119     | 1591  | 7     | 3.69   |
| Seagate   | ST6000VX0001-1S... | 6 TB   | 2       | 1343  | 0     | 3.68   |
| Toshiba   | DT01ACA300         | 3 TB   | 68      | 1625  | 17    | 3.67   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 3       | 1328  | 0     | 3.64   |
| WDC       | WD4003FZEX-00Z4SA0 | 4 TB   | 14      | 1324  | 0     | 3.63   |
| HGST      | HUS724030ALA640    | 3 TB   | 37      | 1545  | 3     | 3.61   |
| WDC       | WD2003FYPS-02W0B1  | 2 TB   | 2       | 1312  | 0     | 3.60   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 288     | 1958  | 17    | 3.58   |
| Hitachi   | HDS721075KLA330    | 752 GB | 1       | 3894  | 2     | 3.56   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 11      | 1445  | 128   | 3.55   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 41      | 1462  | 9     | 3.54   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 2       | 2317  | 4     | 3.53   |
| WDC       | WD40PURX-64NZ6Y0   | 4 TB   | 4       | 1286  | 0     | 3.52   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 5       | 1281  | 0     | 3.51   |
| HGST      | HTE541010A9E680    | 1 TB   | 6       | 1275  | 0     | 3.49   |
| Toshiba   | MG04ACA600E        | 6 TB   | 758     | 1332  | 15    | 3.48   |
| WDC       | WD5003ABYX-01WERA0 | 500 GB | 20      | 1585  | 2     | 3.47   |
| WDC       | WD5000BPKX-22HPJT0 | 500 GB | 5       | 1483  | 2     | 3.46   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 7       | 2296  | 3     | 3.43   |
| WDC       | WD20NMVW-11W68S0   | 2 TB   | 1       | 1251  | 0     | 3.43   |
| Samsung   | HD103SI            | 1 TB   | 2       | 2961  | 506   | 3.40   |
| HGST      | HUH728080ALE600    | 8 TB   | 20      | 1241  | 0     | 3.40   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 10      | 1240  | 0     | 3.40   |
| WDC       | WD1003FBYX-50Y7B1  | 1 TB   | 3       | 1236  | 0     | 3.39   |
| WDC       | WD101KRYZ-01JPDB0  | 10 TB  | 1       | 1234  | 0     | 3.38   |
| HGST      | HDN726040ALE614    | 4 TB   | 21      | 1233  | 0     | 3.38   |
| WDC       | WD5000BMVW-11AJGS2 | 500 GB | 1       | 1228  | 0     | 3.37   |
| Seagate   | ST1000NM0011       | 1 TB   | 27      | 1658  | 81    | 3.36   |
| Seagate   | ST9250610NS        | 250 GB | 8       | 1228  | 0     | 3.36   |
| Samsung   | HD154UI            | 1.5 TB | 2       | 1850  | 1     | 3.36   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 17      | 1715  | 427   | 3.35   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 5       | 1497  | 1     | 3.35   |
| HGST      | HDN726060ALE614    | 6 TB   | 2       | 1214  | 0     | 3.33   |
| Maxtor    | STM3500630AS       | 500 GB | 2       | 1214  | 0     | 3.33   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 90      | 1528  | 97    | 3.32   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 2       | 1211  | 0     | 3.32   |
| WDC       | WD4000FYYZ-03UL1B3 | 4 TB   | 2       | 1208  | 0     | 3.31   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 3       | 1202  | 0     | 3.29   |
| Samsung   | HD161GJ            | 160 GB | 3       | 1200  | 0     | 3.29   |
| WDC       | WD100PURZ-85W86Y0  | 10 TB  | 1       | 1197  | 0     | 3.28   |
| Samsung   | HD103SJ            | 1 TB   | 23      | 2090  | 4     | 3.28   |
| Seagate   | ST3500514NS        | 500 GB | 4       | 1877  | 10    | 3.28   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 82      | 1301  | 15    | 3.28   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 15      | 1297  | 1     | 3.26   |
| MaxDig... | MD4000GBDS         | 4 TB   | 1       | 1187  | 0     | 3.25   |
| HPE       | MB0500GCEHE        | 500 GB | 5       | 1180  | 0     | 3.23   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 4       | 1176  | 0     | 3.22   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 19      | 1354  | 56    | 3.22   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 14      | 1271  | 144   | 3.21   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 23      | 1253  | 1     | 3.20   |
| Seagate   | ST2000VN0001-1S... | 2 TB   | 4       | 1167  | 0     | 3.20   |
| WDC       | WD10EZEX-00UD2A0   | 1 TB   | 1       | 1166  | 0     | 3.20   |
| Seagate   | ST500NM0011        | 500 GB | 9       | 1957  | 5     | 3.18   |
| WDC       | WD1004FBYZ-01YCBB1 | 1 TB   | 6       | 1161  | 0     | 3.18   |
| Hitachi   | HDT725050VLA360    | 500 GB | 1       | 1157  | 0     | 3.17   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 34      | 1709  | 29    | 3.15   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 42      | 1654  | 12    | 3.15   |
| HGST      | HDN724030ALE640    | 3 TB   | 7       | 1149  | 0     | 3.15   |
| HGST      | HUS726060ALE610    | 6 TB   | 21      | 1148  | 0     | 3.15   |
| Toshiba   | MG04ACA300E        | 3 TB   | 1       | 1147  | 0     | 3.14   |
| WDC       | WD10EALS-00Z8A0    | 1 TB   | 7       | 2354  | 5     | 3.14   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 2       | 1146  | 0     | 3.14   |
| WDC       | WD2000FYYZ-03UL1B2 | 2 TB   | 1       | 1145  | 0     | 3.14   |
| Seagate   | ST8000DM002-1YW112 | 8 TB   | 135     | 1208  | 2     | 3.13   |
| WDC       | WD3001FAEX-00MJRA0 | 3 TB   | 1       | 1140  | 0     | 3.13   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 3       | 1138  | 0     | 3.12   |
| HP        | MB2000EAZNL        | 2 TB   | 1       | 1132  | 0     | 3.10   |
| Hitachi   | HDS721050CLA362    | 500 GB | 6       | 1905  | 459   | 3.10   |
| Seagate   | ST8000DM005-2EH112 | 8 TB   | 215     | 1166  | 1     | 3.07   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 1       | 1117  | 0     | 3.06   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 1       | 1116  | 0     | 3.06   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 9       | 1283  | 128   | 3.05   |
| WDC       | WD5000BMVV-11GNWS0 | 500 GB | 1       | 1103  | 0     | 3.02   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 925     | 1188  | 17    | 3.02   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 4       | 1097  | 0     | 3.01   |
| HGST      | HUS726020ALE614    | 2 TB   | 74      | 1110  | 1     | 3.00   |
| WDC       | WD1003FBYX-12      | 1 TB   | 29      | 1169  | 1     | 2.99   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 27      | 1140  | 1     | 2.99   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 39      | 1414  | 2     | 2.98   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 14      | 1255  | 2     | 2.98   |
| Toshiba   | MG04ACA600EY       | 6 TB   | 2       | 1088  | 0     | 2.98   |
| WDC       | WD4000FYYZ-01UL1B2 | 4 TB   | 23      | 1758  | 55    | 2.97   |
| WDC       | WD5000BHTZ-04JCPV1 | 500 GB | 6       | 1084  | 0     | 2.97   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 16      | 1215  | 1     | 2.96   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 1       | 1075  | 0     | 2.95   |
| WDC       | WD5000BMVW-11AJGS4 | 500 GB | 1       | 1073  | 0     | 2.94   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 1       | 1071  | 0     | 2.93   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 9       | 1161  | 1     | 2.93   |
| WDC       | WD4002FYYZ-01B7CB0 | 4 TB   | 33      | 1124  | 1     | 2.92   |
| WDC       | WD2004FBYZ-01YCBB2 | 2 TB   | 1       | 1062  | 0     | 2.91   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 4       | 1488  | 1     | 2.89   |
| Toshiba   | MG04ACA200EY       | 2 TB   | 3       | 1049  | 0     | 2.87   |
| Toshiba   | DT01ACA100         | 1 TB   | 33      | 1231  | 36    | 2.87   |
| Toshiba   | HDWD120            | 2 TB   | 8       | 1042  | 0     | 2.86   |
| Toshiba   | MG03ACA100         | 1 TB   | 43      | 1062  | 3     | 2.85   |
| HGST      | HDN721010ALE604    | 10 TB  | 2       | 1041  | 0     | 2.85   |
| Seagate   | ST4000DX001-1CE168 | 4 TB   | 2       | 1038  | 0     | 2.85   |
| Seagate   | ST6000VX0023-2E... | 6 TB   | 17      | 1033  | 0     | 2.83   |
| Toshiba   | MQ01ABF050         | 500 GB | 1       | 1032  | 0     | 2.83   |
| Toshiba   | MG04ACA400N        | 4 TB   | 5       | 1318  | 2     | 2.82   |
| Seagate   | ST1000NM0018-2F... | 1 TB   | 36      | 1026  | 0     | 2.81   |
| WDC       | WD3000FYYZ-01UL1B2 | 3 TB   | 9       | 1621  | 3     | 2.80   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 16      | 1376  | 319   | 2.80   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 31      | 1755  | 33    | 2.78   |
| Seagate   | ST4000VX000-1F4168 | 4 TB   | 4       | 1014  | 0     | 2.78   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 4       | 1004  | 0     | 2.75   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 22      | 1740  | 17    | 2.75   |
| Seagate   | ST3250310AS        | 250 GB | 3       | 2149  | 209   | 2.74   |
| Seagate   | ST1000NX0423       | 1 TB   | 1       | 997   | 0     | 2.73   |
| Toshiba   | DT01ACA200         | 2 TB   | 274     | 1047  | 19    | 2.73   |
| HGST      | HUS726040ALA614    | 4 TB   | 9       | 995   | 0     | 2.73   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 35      | 1443  | 56    | 2.72   |
| Hitachi   | HDS721032CLA362    | 320 GB | 3       | 1673  | 571   | 2.72   |
| Samsung   | HD204UI            | 2 TB   | 3       | 1825  | 3     | 2.70   |
| HGST      | HUH728060ALE604    | 6 TB   | 14      | 1055  | 5     | 2.69   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 7       | 1333  | 2     | 2.69   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 5       | 980   | 0     | 2.69   |
| Seagate   | ST3500413AS        | 500 GB | 3       | 1572  | 22    | 2.68   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 8       | 974   | 0     | 2.67   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 5       | 2450  | 28    | 2.65   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 2       | 960   | 0     | 2.63   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 14      | 1200  | 16    | 2.63   |
| HGST      | HUH728080ALE604    | 8 TB   | 17      | 991   | 10    | 2.62   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 43      | 955   | 21    | 2.61   |
| Seagate   | ST8000NM0205-2F... | 8 TB   | 31      | 1007  | 66    | 2.61   |
| Fujitsu   | MHW2120BH          | 120 GB | 1       | 946   | 0     | 2.59   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 24      | 1623  | 65    | 2.59   |
| WDC       | WD8002FRYZ-01FF2B0 | 8 TB   | 14      | 978   | 1     | 2.59   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 4       | 941   | 0     | 2.58   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 5       | 1013  | 231   | 2.58   |
| Toshiba   | MG03ACA400         | 4 TB   | 23      | 1375  | 3     | 2.57   |
| WDC       | WD1502FAEX-007BA0  | 1.5 TB | 2       | 1480  | 5     | 2.57   |
| WDC       | WD1003FBYZ-010FB0  | 1 TB   | 60      | 994   | 1     | 2.57   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 6       | 1171  | 1     | 2.56   |
| WDC       | WD5003ABYX-01WERA1 | 500 GB | 17      | 1131  | 1     | 2.56   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 12      | 1077  | 1     | 2.56   |
| Toshiba   | MK2035GSS          | 200 GB | 1       | 927   | 0     | 2.54   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 1       | 915   | 0     | 2.51   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 2       | 1595  | 4     | 2.50   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 4       | 2285  | 260   | 2.48   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 27      | 1029  | 2     | 2.48   |
| HGST      | HUS722T1TALA600    | 1 TB   | 28      | 902   | 0     | 2.47   |
| HGST      | HUH721008ALE601    | 8 TB   | 6       | 901   | 0     | 2.47   |
| Hitachi   | HDP725025GLA380    | 250 GB | 2       | 4193  | 6     | 2.44   |
| HGST      | HUS726020ALE610    | 2 TB   | 7       | 886   | 0     | 2.43   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 7       | 1352  | 9     | 2.42   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 11      | 927   | 1     | 2.42   |
| HGST      | HUH721010ALN600    | 10 TB  | 16      | 882   | 0     | 2.42   |
| Toshiba   | MG04ACA400EY       | 4 TB   | 10      | 874   | 0     | 2.40   |
| Seagate   | ST32000644NS       | 2 TB   | 11      | 1402  | 8     | 2.39   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 3       | 873   | 0     | 2.39   |
| HGST      | HUS726040ALE610    | 4 TB   | 21      | 873   | 0     | 2.39   |
| WDC       | WD2003FYYS-27Y2P0  | 2 TB   | 2       | 1249  | 2     | 2.39   |
| HGST      | HUS726040ALE614    | 4 TB   | 13      | 941   | 3     | 2.39   |
| WDC       | WD4000FYYZ-01UL1B3 | 4 TB   | 18      | 1060  | 3     | 2.39   |
| WDC       | WD60PURZ-85ZUFY1   | 6 TB   | 2       | 871   | 0     | 2.39   |
| Seagate   | ST1000DX001-1NS162 | 1 TB   | 6       | 1607  | 219   | 2.38   |
| Toshiba   | DT01ACA050         | 500 GB | 18      | 1009  | 137   | 2.37   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 23      | 896   | 1     | 2.37   |
| HPE       | MM1000GFJTE        | 1 TB   | 4       | 862   | 0     | 2.36   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 28      | 1183  | 6     | 2.36   |
| Toshiba   | MG03ACA200         | 2 TB   | 7       | 920   | 288   | 2.35   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 10      | 856   | 0     | 2.35   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 4       | 1951  | 4     | 2.34   |
| HGST      | HUH721212ALN600    | 12 TB  | 11      | 854   | 0     | 2.34   |
| Seagate   | ST3400620NS        | 400 GB | 1       | 1695  | 1     | 2.32   |
| HGST      | HUS726020ALA610    | 2 TB   | 107     | 892   | 18    | 2.31   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 1       | 840   | 0     | 2.30   |
| Seagate   | ST10000NM0016-1... | 10 TB  | 1484    | 1246  | 56    | 2.30   |
| Seagate   | ST6000NM0235-2A... | 6 TB   | 9       | 837   | 0     | 2.29   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 6       | 1089  | 89    | 2.29   |
| Seagate   | ST3750640AS        | 752 GB | 1       | 2504  | 2     | 2.29   |
| HPE       | MB0500EBNCR        | 500 GB | 5       | 1525  | 18    | 2.26   |
| HGST      | HUS722T1TALA604    | 1 TB   | 111     | 834   | 11    | 2.25   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 2       | 821   | 0     | 2.25   |
| MediaMax  | WL2000GSA6472E     | 2 TB   | 1       | 817   | 0     | 2.24   |
| WDC       | WD2000F9YZ-09N20L1 | 2 TB   | 4       | 816   | 0     | 2.24   |
| WDC       | WD1005FBYZ-01YCBB2 | 1 TB   | 20      | 862   | 1     | 2.23   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 77      | 899   | 1     | 2.22   |
| WDC       | WD5002ABYS-18B1B0  | 500 GB | 1       | 808   | 0     | 2.22   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 3       | 804   | 0     | 2.21   |
| WDC       | WD50EFRX-68L0BN1   | 5 TB   | 6       | 1495  | 118   | 2.20   |
| HP        | MB2000GCEHK        | 2 TB   | 2       | 1625  | 1051  | 2.20   |
| Seagate   | ST380815AS         | 80 GB  | 4       | 800   | 0     | 2.19   |
| Samsung   | HD502HJ            | 500 GB | 2       | 800   | 0     | 2.19   |
| Seagate   | ST3120022A         | 120 GB | 1       | 3197  | 3     | 2.19   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 2       | 1368  | 3     | 2.19   |
| WDC       | WD2500AAJS-00VTA0  | 250 GB | 1       | 796   | 0     | 2.18   |
| Seagate   | ST31000NSSUN1.0T   | 1 TB   | 1       | 1574  | 1     | 2.16   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 10      | 785   | 0     | 2.15   |
| Seagate   | ST3500418AS        | 500 GB | 7       | 788   | 2     | 2.15   |
| WDC       | WD800JD-00HKA0     | 80 GB  | 1       | 776   | 0     | 2.13   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 22      | 835   | 3     | 2.13   |
| Seagate   | ST3250318AS        | 250 GB | 3       | 1339  | 17    | 2.12   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 39      | 800   | 28    | 2.10   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 42      | 790   | 3     | 2.09   |
| HPE       | MM2000GEFRA        | 2 TB   | 237     | 816   | 1     | 2.09   |
| HGST      | HUH721010ALE604    | 10 TB  | 106     | 760   | 0     | 2.08   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 15      | 759   | 0     | 2.08   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 8       | 758   | 0     | 2.08   |
| HGST      | HUS726040ALA610    | 4 TB   | 66      | 780   | 1     | 2.06   |
| Seagate   | ST10000DM0004-2... | 10 TB  | 7       | 872   | 52    | 2.04   |
| WDC       | WD4000F9YZ-09N20L0 | 4 TB   | 4       | 731   | 0     | 2.01   |
| Hitachi   | HTS723216L9SA60    | 160 GB | 1       | 727   | 0     | 1.99   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 3       | 937   | 1     | 1.99   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 140     | 744   | 6     | 1.99   |
| HGST      | HTS721010A9E630    | 1 TB   | 5       | 1393  | 605   | 1.98   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 197     | 744   | 3     | 1.98   |
| WDC       | WD2005FBYZ-01YCBB2 | 2 TB   | 40      | 723   | 0     | 1.98   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 6       | 722   | 0     | 1.98   |
| Hitachi   | HDE721050SLA330    | 500 GB | 2       | 3595  | 4     | 1.97   |
| Seagate   | ST500DM005 HD502HJ | 500 GB | 1       | 716   | 0     | 1.96   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 38      | 898   | 12    | 1.95   |
| Toshiba   | HDWD105            | 500 GB | 5       | 705   | 0     | 1.93   |
| HPE       | MM1000GBKAL        | 1 TB   | 18      | 909   | 1     | 1.92   |
| Seagate   | ST1000VN002-2EY102 | 1 TB   | 4       | 700   | 0     | 1.92   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 37      | 955   | 211   | 1.92   |
| Toshiba   | HDWA130            | 3 TB   | 1       | 699   | 0     | 1.92   |
| Seagate   | ST10000NE0004-1... | 10 TB  | 15      | 1123  | 372   | 1.91   |
| Toshiba   | HDWL120            | 2 TB   | 4       | 685   | 0     | 1.88   |
| HGST      | HUS726T6TALE6L4    | 6 TB   | 133     | 700   | 31    | 1.87   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 1       | 680   | 0     | 1.86   |
| Seagate   | ST4000NM000A-2H... | 4 TB   | 2       | 679   | 0     | 1.86   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 1       | 679   | 0     | 1.86   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 3       | 916   | 7     | 1.84   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 21      | 674   | 50    | 1.84   |
| HGST      | HUH721008ALE600    | 8 TB   | 39      | 671   | 0     | 1.84   |
| WDC       | WD15EARS-00MVWB0   | 1.5 TB | 4       | 2054  | 324   | 1.81   |
| Seagate   | ST2000VX003-1HH164 | 2 TB   | 3       | 652   | 0     | 1.79   |
| Seagate   | ST2000NM0125-1Y... | 2 TB   | 13      | 651   | 0     | 1.78   |
| Seagate   | ST2000NM0055-1V... | 2 TB   | 21      | 893   | 2     | 1.78   |
| HGST      | HUS722T2TALA604    | 2 TB   | 59      | 668   | 1     | 1.78   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 1       | 1944  | 2     | 1.78   |
| Seagate   | ST10000NM0196-2... | 10 TB  | 198     | 699   | 23    | 1.77   |
| Hitachi   | HDS723030ALA640... | 3 TB   | 2       | 975   | 1     | 1.77   |
| WDC       | WD121KRYZ-01W0RB0  | 12 TB  | 7       | 862   | 1     | 1.76   |
| Samsung   | HE103SJ            | 1 TB   | 1       | 637   | 0     | 1.75   |
| Toshiba   | MG04ACA200E        | 2 TB   | 10      | 637   | 0     | 1.75   |
| Seagate   | ST2000NM0011       | 2 TB   | 14      | 1478  | 94    | 1.74   |
| Seagate   | ST12000DM0007-2... | 12 TB  | 5       | 630   | 0     | 1.73   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 41      | 666   | 3     | 1.73   |
| WDC       | WD5000AZLX-35K2TA0 | 500 GB | 3       | 627   | 0     | 1.72   |
| WDC       | WD5000AZLX-08K2TA0 | 500 GB | 3       | 625   | 0     | 1.71   |
| WDC       | WD10JMVW-11AJGS3   | 1 TB   | 1       | 624   | 0     | 1.71   |
| WDC       | WD100EFAX-68LHPN0  | 10 TB  | 53      | 624   | 0     | 1.71   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 1       | 620   | 0     | 1.70   |
| HGST      | HUH721212ALN604    | 12 TB  | 2005    | 638   | 2     | 1.70   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 4       | 616   | 0     | 1.69   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 25      | 614   | 0     | 1.68   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 61      | 622   | 1     | 1.68   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 3       | 609   | 0     | 1.67   |
| WDC       | WD10EURX-63UY4Y0   | 1 TB   | 2       | 606   | 0     | 1.66   |
| HGST      | HUS726060ALA640    | 6 TB   | 44      | 607   | 1     | 1.66   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 70      | 624   | 74    | 1.65   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 95      | 649   | 2     | 1.64   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 17      | 651   | 2     | 1.63   |
| Hitachi   | HUS724040ALE640    | 4 TB   | 12      | 654   | 1     | 1.62   |
| HGST      | HUH728060ALE600    | 6 TB   | 1       | 589   | 0     | 1.61   |
| WDC       | WD4000FYYZ-01UL1B1 | 4 TB   | 9       | 1613  | 5     | 1.61   |
| Seagate   | ST3500312CS        | 500 GB | 4       | 723   | 3     | 1.58   |
| Seagate   | ST1000VX005-2EZ102 | 1 TB   | 3       | 574   | 0     | 1.57   |
| Toshiba   | MG05ACA800E        | 8 TB   | 662     | 600   | 1     | 1.57   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 20      | 569   | 0     | 1.56   |
| Seagate   | ST10000VN0004-1... | 10 TB  | 30      | 682   | 72    | 1.56   |
| HGST      | HUH721212ALE600    | 12 TB  | 50      | 568   | 0     | 1.56   |
| Seagate   | ST10000NM0156-2... | 10 TB  | 37      | 642   | 6     | 1.56   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 50      | 564   | 0     | 1.55   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 3       | 564   | 0     | 1.55   |
| HPE       | MB004000GWFWB      | 4 TB   | 15      | 564   | 0     | 1.55   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 110     | 622   | 5     | 1.54   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 4       | 1870  | 3     | 1.54   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 1       | 561   | 0     | 1.54   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 3       | 558   | 0     | 1.53   |
| WDC       | WD5000AAKS-65YGA0  | 500 GB | 1       | 556   | 0     | 1.52   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 1       | 2780  | 4     | 1.52   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 3       | 555   | 0     | 1.52   |
| WDC       | WD1003FBYX-01Y7B2  | 1 TB   | 1       | 555   | 0     | 1.52   |
| Seagate   | ST33000651NS       | 3 TB   | 1       | 552   | 0     | 1.51   |
| Seagate   | ST2000NM0018-2F... | 2 TB   | 1       | 552   | 0     | 1.51   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 34      | 568   | 30    | 1.51   |
| Seagate   | ST8000VX0022-2E... | 8 TB   | 4       | 755   | 9     | 1.51   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 3       | 549   | 0     | 1.50   |
| Toshiba   | MD04ACA400         | 4 TB   | 436     | 551   | 3     | 1.49   |
| WDC       | WD50EFRX-68MYMN1   | 5 TB   | 2       | 2167  | 4     | 1.49   |
| Toshiba   | MG04ACA400E        | 4 TB   | 54      | 538   | 41    | 1.46   |
| Seagate   | ST2000NX0253       | 2 TB   | 49      | 709   | 16    | 1.46   |
| Toshiba   | HDWT140            | 4 TB   | 2       | 530   | 0     | 1.45   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 13      | 529   | 0     | 1.45   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 156     | 537   | 1     | 1.45   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 3       | 524   | 0     | 1.44   |
| Seagate   | ST8000DM0004-1Z... | 8 TB   | 10      | 946   | 317   | 1.43   |
| Toshiba   | HDWD130            | 3 TB   | 8       | 541   | 2     | 1.43   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 15      | 646   | 133   | 1.43   |
| MediaMax  | WL4000GSA6472      | 4 TB   | 2       | 511   | 0     | 1.40   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 21      | 646   | 27    | 1.40   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 46      | 527   | 1     | 1.40   |
| WDC       | WD8003FRYZ-01JPDB1 | 8 TB   | 5       | 510   | 0     | 1.40   |
| Seagate   | ST14000VN0008-2... | 14 TB  | 12      | 508   | 0     | 1.39   |
| Toshiba   | HDWR21C            | 12 TB  | 5       | 501   | 0     | 1.37   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 17      | 498   | 0     | 1.37   |
| Toshiba   | HDWU130            | 3 TB   | 8       | 571   | 5     | 1.36   |
| HGST      | HTS725050A7E630    | 500 GB | 3       | 1084  | 1015  | 1.35   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 1       | 490   | 0     | 1.34   |
| Seagate   | ST2000NX0403       | 2 TB   | 7       | 488   | 0     | 1.34   |
| Seagate   | ST3750640NS        | 752 GB | 12      | 1304  | 737   | 1.32   |
| Samsung   | HD322GJ            | 320 GB | 1       | 477   | 0     | 1.31   |
| Seagate   | ST3000VX010-2E3166 | 3 TB   | 4       | 476   | 0     | 1.31   |
| Toshiba   | HDWN160            | 6 TB   | 10      | 567   | 3     | 1.31   |
| WDC       | WD8003FFBX-68B9AN0 | 8 TB   | 3       | 472   | 0     | 1.29   |
| WDC       | WD5000AZLX-22JKKA0 | 500 GB | 2       | 902   | 4     | 1.29   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 1       | 465   | 0     | 1.28   |
| Toshiba   | HDWE140            | 4 TB   | 42      | 469   | 43    | 1.25   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 1       | 452   | 0     | 1.24   |
| Seagate   | ST6000VX001-2BD186 | 6 TB   | 4       | 450   | 0     | 1.23   |
| HGST      | HUH721212ALE604    | 12 TB  | 175     | 453   | 1     | 1.23   |
| HGST      | HUH721010ALE600    | 10 TB  | 219     | 451   | 1     | 1.23   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 44      | 451   | 1     | 1.22   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 7       | 482   | 2     | 1.21   |
| Seagate   | ST31000524AS       | 1 TB   | 6       | 1718  | 657   | 1.21   |
| HGST      | HDN728080ALE604    | 8 TB   | 2       | 657   | 16    | 1.21   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 1       | 440   | 0     | 1.21   |
| Seagate   | ST2000NX0423       | 2 TB   | 60      | 439   | 0     | 1.20   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 27      | 439   | 0     | 1.20   |
| WDC       | WD1005FBYZ-01YCBB3 | 1 TB   | 1       | 438   | 0     | 1.20   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 1       | 434   | 0     | 1.19   |
| Seagate   | ST9500420ASG       | 500 GB | 4       | 674   | 10    | 1.19   |
| Samsung   | HD080HJ            | 80 GB  | 2       | 1964  | 841   | 1.17   |
| Seagate   | ST2000DX002-2DV164 | 2 TB   | 4       | 424   | 0     | 1.16   |
| Seagate   | ST1000NX0313       | 1 TB   | 32      | 1095  | 22    | 1.16   |
| WDC       | WD3000F9YZ-09N20L1 | 3 TB   | 1       | 419   | 0     | 1.15   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 2       | 1595  | 4     | 1.15   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 1       | 418   | 0     | 1.15   |
| HGST      | HUS726T4TALE6L4    | 4 TB   | 62      | 418   | 0     | 1.15   |
| Samsung   | HD501LJ            | 500 GB | 3       | 2138  | 676   | 1.14   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 5       | 551   | 4     | 1.13   |
| WDC       | WD3000FYYZ-01UL1B3 | 3 TB   | 5       | 411   | 0     | 1.13   |
| Seagate   | ST16000NE000-2R... | 16 TB  | 2       | 410   | 0     | 1.12   |
| WDC       | WD4000FYYZ-01UL1B0 | 4 TB   | 20      | 2132  | 231   | 1.11   |
| Toshiba   | MG07ACA12TEY       | 12 TB  | 7       | 401   | 0     | 1.10   |
| WDC       | WD1503FYYS-02W0B0  | 1.5 TB | 2       | 3213  | 7     | 1.10   |
| WDC       | WD1501FASS-00U0B0  | 1.5 TB | 1       | 3610  | 8     | 1.10   |
| Toshiba   | MG06ACA10TEY       | 10 TB  | 70      | 407   | 1     | 1.09   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 2       | 396   | 0     | 1.09   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 6       | 395   | 0     | 1.08   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 9       | 529   | 2     | 1.07   |
| WDC       | WD30PURZ-85GU6Y0   | 3 TB   | 1       | 390   | 0     | 1.07   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 164     | 1114  | 6     | 1.06   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 9       | 447   | 2     | 1.05   |
| HP        | MB2000GCWDA        | 2 TB   | 2       | 383   | 0     | 1.05   |
| Seagate   | ST12000NM0008-2... | 12 TB  | 163     | 387   | 4     | 1.05   |
| Seagate   | ST3250312AS        | 250 GB | 3       | 741   | 4     | 1.04   |
| Hitachi   | HTS542512K9SA00    | 120 GB | 1       | 1508  | 3     | 1.03   |
| Seagate   | ST6000NE0021-2E... | 6 TB   | 3       | 1114  | 144   | 1.03   |
| Seagate   | ST10000NM0568-2... | 10 TB  | 32      | 371   | 0     | 1.02   |
| Toshiba   | MG07ACA12TE        | 12 TB  | 84      | 378   | 1     | 1.02   |
| Toshiba   | HDWQ140            | 4 TB   | 11      | 370   | 0     | 1.02   |
| Toshiba   | HDWD110            | 1 TB   | 60      | 387   | 60    | 1.01   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 2       | 369   | 0     | 1.01   |
| Toshiba   | MG06ACA10TE        | 10 TB  | 102     | 371   | 1     | 1.01   |
| Seagate   | ST3250823AS        | 250 GB | 1       | 4725  | 12    | 1.00   |
| Seagate   | ST4000NM0033       | 4 TB   | 4       | 362   | 0     | 0.99   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 18      | 450   | 19    | 0.99   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 49      | 366   | 2     | 0.98   |
| Seagate   | ST4000NM0115-1Y... | 4 TB   | 87      | 357   | 0     | 0.98   |
| HGST      | HUH721008ALE604    | 8 TB   | 22      | 350   | 0     | 0.96   |
| Seagate   | ST10000DM0004-1... | 10 TB  | 7       | 349   | 0     | 0.96   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 131     | 348   | 5     | 0.95   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 1       | 1714  | 4     | 0.94   |
| WDC       | WD10EALS-002BA0    | 1 TB   | 2       | 2394  | 6     | 0.94   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 4       | 342   | 0     | 0.94   |
| Toshiba   | MG03ACA300         | 3 TB   | 2       | 606   | 6     | 0.93   |
| Seagate   | ST3500411SV        | 500 GB | 1       | 335   | 0     | 0.92   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 8       | 334   | 0     | 0.92   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 43      | 429   | 35    | 0.91   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 11      | 356   | 2     | 0.91   |
| WDC       | WD40EFAX-68JH4N0   | 4 TB   | 37      | 331   | 1     | 0.90   |
| WDC       | WD121KFBX-68EF5N0  | 12 TB  | 7       | 325   | 0     | 0.89   |
| Toshiba   | MG04ACA200N        | 2 TB   | 4       | 324   | 0     | 0.89   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 2       | 323   | 0     | 0.89   |
| Seagate   | ST10000VE0008-2... | 10 TB  | 4       | 321   | 0     | 0.88   |
| Seagate   | ST1000NX0443       | 1 TB   | 22      | 317   | 0     | 0.87   |
| Seagate   | ST10000VX0004-1... | 10 TB  | 18      | 317   | 0     | 0.87   |
| HGST      | HUS726T6TALE6L1    | 6 TB   | 12      | 314   | 0     | 0.86   |
| Seagate   | ST6000NM021A-2R... | 6 TB   | 81      | 321   | 13    | 0.86   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 1       | 1233  | 3     | 0.84   |
| Seagate   | ST12000NM0017-2... | 12 TB  | 2       | 307   | 0     | 0.84   |
| Seagate   | ST2000DM005-2CW102 | 2 TB   | 1       | 306   | 0     | 0.84   |
| WDC       | WD5000AZLX-00JKKA0 | 500 GB | 1       | 304   | 0     | 0.83   |
| WDC       | WD5000AZLX-00K2TA0 | 500 GB | 1       | 304   | 0     | 0.83   |
| WDC       | WD800BEVS-22RST0   | 80 GB  | 1       | 299   | 0     | 0.82   |
| Toshiba   | MK2002TSKB         | 2 TB   | 1       | 2695  | 8     | 0.82   |
| HPE       | MB8000GFECR        | 8 TB   | 55      | 296   | 0     | 0.81   |
| Hitachi   | HDS721050DLE630    | 500 GB | 4       | 774   | 420   | 0.81   |
| WDC       | WD20SPZX-00UA7T0   | 2 TB   | 5       | 296   | 0     | 0.81   |
| Seagate   | ST8000NM000A-2K... | 8 TB   | 29      | 299   | 1     | 0.80   |
| HPE       | MB0500EBZQA        | 500 GB | 1       | 2634  | 8     | 0.80   |
| WDC       | WUH721414ALE604    | 14 TB  | 1699    | 292   | 1     | 0.80   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 2       | 290   | 0     | 0.80   |
| Toshiba   | MG06ACA800E        | 8 TB   | 16      | 290   | 0     | 0.80   |
| Toshiba   | MG06ACA800EY       | 8 TB   | 15      | 288   | 0     | 0.79   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 25      | 287   | 0     | 0.79   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 2       | 286   | 0     | 0.78   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 4       | 317   | 1     | 0.78   |
| Seagate   | ST9750420AS        | 752 GB | 1       | 285   | 0     | 0.78   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 7       | 338   | 12    | 0.78   |
| HPE       | MB001000GWFGF      | 1 TB   | 1       | 283   | 0     | 0.78   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 83      | 286   | 20    | 0.77   |
| HGST      | HUS726T4TALA6L1    | 4 TB   | 69      | 282   | 1     | 0.77   |
| WDC       | WD4003FRYZ-01F0DB0 | 4 TB   | 27      | 275   | 0     | 0.75   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 2       | 1247  | 8     | 0.75   |
| Hitachi   | HDS721025CLA382    | 250 GB | 1       | 2454  | 8     | 0.75   |
| Seagate   | ST31000528AS       | 1 TB   | 4       | 742   | 351   | 0.74   |
| Maxtor    | STM3500320AS       | 500 GB | 2       | 459   | 617   | 0.74   |
| Toshiba   | MD04ACA50D         | 5 TB   | 1       | 268   | 0     | 0.74   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 4       | 1336  | 548   | 0.73   |
| Seagate   | ST31000524NS       | 1 TB   | 20      | 1063  | 107   | 0.72   |
| WDC       | WD5001AALS-00L3B2  | 500 GB | 2       | 3267  | 515   | 0.72   |
| Seagate   | ST3160815AS        | 160 GB | 3       | 2011  | 183   | 0.71   |
| Hitachi   | HTS545032B9A300    | 320 GB | 1       | 1024  | 3     | 0.70   |
| Seagate   | ST31000524NS 45... | 1 TB   | 2       | 682   | 2     | 0.70   |
| HPE       | MB012000GWDFE      | 12 TB  | 23      | 255   | 0     | 0.70   |
| WDC       | WD3000FYYZ-01UL1B1 | 3 TB   | 1       | 2286  | 8     | 0.70   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 18      | 252   | 0     | 0.69   |
| HPE       | MB008000GWRTC      | 8 TB   | 1       | 252   | 0     | 0.69   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 4       | 1168  | 697   | 0.69   |
| Toshiba   | MG06ACA600E        | 6 TB   | 9       | 251   | 0     | 0.69   |
| WDC       | WD3200AAKS-22B3A0  | 320 GB | 1       | 250   | 0     | 0.69   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 2       | 247   | 0     | 0.68   |
| WDC       | WD5000HHTZ-04N21V1 | 500 GB | 1       | 247   | 0     | 0.68   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 1       | 246   | 0     | 0.67   |
| WDC       | WD10TMVW-11ZSMS1   | 1 TB   | 1       | 492   | 1     | 0.67   |
| WDC       | WD10EADS-11P8B1    | 1 TB   | 1       | 2191  | 8     | 0.67   |
| WDC       | WD40EZAZ-00ZGHB0   | 4 TB   | 2       | 242   | 0     | 0.66   |
| WDC       | WD2003FYYS-70W0B0  | 2 TB   | 1       | 240   | 0     | 0.66   |
| Toshiba   | MQ01ACF050         | 500 GB | 5       | 380   | 2     | 0.66   |
| Seagate   | ST3320418AS        | 320 GB | 1       | 239   | 0     | 0.66   |
| Seagate   | ST10000NM0478-2... | 10 TB  | 15      | 261   | 2     | 0.65   |
| WDC       | WUH721414ALE6L4    | 14 TB  | 28      | 242   | 1     | 0.65   |
| WDC       | WD2005FBYZ-01YCBB3 | 2 TB   | 5       | 235   | 0     | 0.64   |
| WDC       | WD15NMVW-11W68S0   | 1.5 TB | 1       | 233   | 0     | 0.64   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 2       | 227   | 0     | 0.62   |
| HGST      | HUS728T8TALE6L0    | 8 TB   | 15      | 220   | 0     | 0.61   |
| Apple     | HDD HTS541010A9... | 1 TB   | 1       | 220   | 0     | 0.60   |
| Seagate   | ST32000542AS       | 2 TB   | 1       | 218   | 0     | 0.60   |
| Toshiba   | HDWR160            | 6 TB   | 1       | 210   | 0     | 0.58   |
| WDC       | WD1000DHTZ-04N21V0 | 1 TB   | 9       | 230   | 1     | 0.57   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 190     | 210   | 17    | 0.57   |
| Seagate   | ST1000NX0423 00... | 1 TB   | 1       | 207   | 0     | 0.57   |
| Samsung   | HD252HJ            | 250 GB | 1       | 2689  | 12    | 0.57   |
| Seagate   | ST16000NM001G-2... | 16 TB  | 50      | 206   | 0     | 0.57   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 51      | 218   | 21    | 0.56   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 1       | 1623  | 7     | 0.56   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 7       | 201   | 0     | 0.55   |
| HGST      | HUH721212ALE601    | 12 TB  | 49      | 200   | 0     | 0.55   |
| HP        | VB0250EAVER        | 250 GB | 3       | 322   | 204   | 0.54   |
| WDC       | WD101EFAX-68LDBN0  | 10 TB  | 10      | 196   | 0     | 0.54   |
| Seagate   | ST14000NM001G-2... | 14 TB  | 16      | 195   | 0     | 0.53   |
| Seagate   | ST3160812AS        | 160 GB | 1       | 194   | 0     | 0.53   |
| WDC       | WD6003FZBX-00GXAB0 | 6 TB   | 7       | 190   | 0     | 0.52   |
| HPE       | MB010000GWRTK      | 10 TB  | 24      | 190   | 0     | 0.52   |
| Toshiba   | MQ01ABB200         | 2 TB   | 1       | 1702  | 8     | 0.52   |
| WDC       | WD6003FRYZ-01F0DB0 | 6 TB   | 13      | 187   | 0     | 0.51   |
| HP        | MB1000EAMZE        | 1 TB   | 2       | 185   | 0     | 0.51   |
| Toshiba   | MG04ACA400NY       | 4 TB   | 2       | 181   | 0     | 0.50   |
| Seagate   | ST8000NE001-2M7101 | 8 TB   | 1       | 178   | 0     | 0.49   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 1       | 174   | 0     | 0.48   |
| Seagate   | ST1000NX0343       | 1 TB   | 2       | 1561  | 10    | 0.45   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 1       | 164   | 0     | 0.45   |
| Seagate   | ST8000VE000-2P6101 | 8 TB   | 1       | 159   | 0     | 0.44   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 4       | 158   | 0     | 0.43   |
| WDC       | WD102KFBX-68M95N0  | 10 TB  | 32      | 158   | 0     | 0.43   |
| Toshiba   | MQ01ACF032         | 320 GB | 1       | 151   | 0     | 0.41   |
| Maxtor    | STM3200827AS       | 200 GB | 1       | 1203  | 7     | 0.41   |
| Toshiba   | HDWN180            | 8 TB   | 1       | 146   | 0     | 0.40   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 17      | 144   | 0     | 0.40   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 4       | 1370  | 16    | 0.39   |
| Seagate   | ST1000NX0303       | 1 TB   | 3       | 615   | 4     | 0.39   |
| Apple     | HDD HTS545050A7... | 500 GB | 1       | 141   | 0     | 0.39   |
| HP        | MB2000EBZQC        | 2 TB   | 1       | 1269  | 8     | 0.39   |
| Seagate   | ST2000NM000A-2J... | 2 TB   | 1       | 139   | 0     | 0.38   |
| Seagate   | ST4000NM002A-2H... | 4 TB   | 50      | 139   | 0     | 0.38   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 4       | 137   | 0     | 0.38   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 3       | 701   | 44    | 0.37   |
| Hitachi   | HDT725025VLA380... | 250 GB | 1       | 135   | 0     | 0.37   |
| WDC       | WD6003FZBX-00K5WB0 | 6 TB   | 13      | 134   | 0     | 0.37   |
| WDC       | WD50EZRZ-00GZ5B1   | 5 TB   | 1       | 133   | 0     | 0.37   |
| Seagate   | ST18000NM000J-2... | 18 TB  | 11      | 130   | 0     | 0.36   |
| Seagate   | ST10000NM001G-2... | 10 TB  | 16      | 123   | 0     | 0.34   |
| Toshiba   | HDWR180            | 8 TB   | 3       | 122   | 0     | 0.34   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 3       | 120   | 0     | 0.33   |
| HP        | GB0750C4414        | 752 GB | 2       | 3668  | 152   | 0.33   |
| WDC       | WUS721010ALE6L4    | 10 TB  | 21      | 117   | 11    | 0.32   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 1       | 113   | 0     | 0.31   |
| Samsung   | HM641JI            | 640 GB | 1       | 112   | 0     | 0.31   |
| Hitachi   | HTS725016A9A364    | 160 GB | 2       | 1326  | 507   | 0.30   |
| Seagate   | ST12000NM001G-2... | 12 TB  | 10      | 107   | 0     | 0.30   |
| Hitachi   | HDS721010DLE630    | 1 TB   | 8       | 1591  | 1310  | 0.29   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 2       | 1727  | 16    | 0.29   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 2       | 507   | 4     | 0.28   |
| WDC       | WD10EURX-63C57Y0   | 1 TB   | 1       | 883   | 8     | 0.27   |
| WDC       | WD2003FYYS-05T9B0  | 2 TB   | 2       | 215   | 2     | 0.27   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 1       | 877   | 8     | 0.27   |
| WDC       | WUH721414ALE6L1    | 14 TB  | 8       | 95    | 0     | 0.26   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 1       | 807   | 8     | 0.25   |
| WDC       | WD10SMZW-11Y0TS0   | 1 TB   | 2       | 88    | 0     | 0.24   |
| WDC       | WD141KFGX-68FH9N0  | 14 TB  | 12      | 84    | 0     | 0.23   |
| WDC       | WD1600BEKT-00F3T0  | 160 GB | 2       | 1098  | 146   | 0.22   |
| WDC       | WD40EFAX-68JH4N1   | 4 TB   | 2       | 80    | 0     | 0.22   |
| WDC       | WD2500BEKT-60A25T1 | 250 GB | 1       | 399   | 4     | 0.22   |
| WDC       | WD4000F9YZ-76N20L1 | 4 TB   | 1       | 78    | 0     | 0.22   |
| WDC       | WUH721818ALE604    | 18 TB  | 222     | 74    | 0     | 0.21   |
| Seagate   | ST9500325AS        | 500 GB | 2       | 1360  | 69    | 0.20   |
| WDC       | WD20SPZX-75UA7T1   | 2 TB   | 2       | 71    | 0     | 0.20   |
| Seagate   | ST32000641AS       | 2 TB   | 1       | 2134  | 29    | 0.19   |
| Toshiba   | MQ01UBD050         | 500 GB | 1       | 69    | 0     | 0.19   |
| Seagate   | ST980811AS         | 80 GB  | 1       | 348   | 4     | 0.19   |
| Toshiba   | HDWG180            | 8 TB   | 8       | 67    | 0     | 0.19   |
| Toshiba   | MQ04ABF100         | 1 TB   | 2       | 197   | 1010  | 0.18   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 1       | 1641  | 24    | 0.18   |
| Toshiba   | MQ01UBD100         | 1 TB   | 2       | 76    | 8     | 0.18   |
| WDC       | WD5000LPLX-60ZNTT2 | 500 GB | 1       | 63    | 0     | 0.17   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 2       | 60    | 0     | 0.17   |
| Hitachi   | HTS725050A9A362    | 500 GB | 1       | 868   | 14    | 0.16   |
| HGST      | HUH728080ALN600    | 8 TB   | 2       | 96    | 2     | 0.16   |
| Hitachi   | HTS545016B9A300    | 160 GB | 1       | 55    | 0     | 0.15   |
| Hitachi   | HTS545025B9A300    | 250 GB | 1       | 219   | 3     | 0.15   |
| Toshiba   | MK1252GSX          | 120 GB | 1       | 54    | 0     | 0.15   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 1       | 54    | 0     | 0.15   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 6       | 52    | 0     | 0.14   |
| WDC       | WD3200AVVS-56L2B0  | 320 GB | 4       | 48    | 0     | 0.13   |
| Seagate   | ST31000340NS       | 1 TB   | 3       | 682   | 338   | 0.13   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 2       | 44    | 0     | 0.12   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 6       | 1924  | 905   | 0.12   |
| WDC       | WD20EZRX-19DC0B0   | 2 TB   | 1       | 1541  | 35    | 0.12   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 1       | 38    | 0     | 0.11   |
| Toshiba   | MQ04UBF100         | 1 TB   | 1       | 38    | 0     | 0.11   |
| Seagate   | ST3640323AS        | 640 GB | 1       | 960   | 24    | 0.11   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 1       | 1377  | 35    | 0.10   |
| WDC       | WUH721818ALE6L4    | 18 TB  | 33      | 37    | 0     | 0.10   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 1       | 2055  | 55    | 0.10   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 1       | 2330  | 66    | 0.10   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 2       | 33    | 0     | 0.09   |
| Toshiba   | HDWF180            | 8 TB   | 2       | 33    | 0     | 0.09   |
| Seagate   | ST5000NM0024-1H... | 5 TB   | 1       | 1636  | 49    | 0.09   |
| WDC       | WD30EFAX-68JH4N0   | 3 TB   | 2       | 127   | 4     | 0.09   |
| WDC       | WD62PURZ-85B3AY0   | 6 TB   | 3       | 31    | 0     | 0.09   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 4       | 30    | 0     | 0.08   |
| WDC       | WD4000FDYZ-27YA5B0 | 4 TB   | 5       | 711   | 115   | 0.08   |
| Apple     | HDD ST1000DM003    | 1 TB   | 1       | 254   | 8     | 0.08   |
| WDC       | WD1003FBYX-20Y7B0  | 1 TB   | 2       | 27    | 0     | 0.07   |
| HGST      | HTS541050A9E680    | 500 GB | 1       | 26    | 0     | 0.07   |
| HP        | VB0160EAVEQ        | 160 GB | 1       | 366   | 14    | 0.07   |
| HP        | MB1000EBZQB        | 1 TB   | 1       | 2073  | 86    | 0.07   |
| Seagate   | ST3000NM0005-1V... | 3 TB   | 1       | 22    | 0     | 0.06   |
| Toshiba   | MK5061GSY          | 500 GB | 1       | 20    | 0     | 0.06   |
| HP        | MB1000EBNCF        | 1 TB   | 1       | 1398  | 73    | 0.05   |
| Maxtor    | STM3160215AS       | 160 GB | 1       | 2568  | 142   | 0.05   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 1       | 17    | 0     | 0.05   |
| WDC       | WD80EFBX-68AZZN0   | 8 TB   | 1       | 16    | 0     | 0.04   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 1       | 3495  | 242   | 0.04   |
| Toshiba   | HDWR11A            | 10 TB  | 1       | 11    | 0     | 0.03   |
| WDC       | WD20SMZW-11JW8S1   | 2 TB   | 1       | 10    | 0     | 0.03   |
| Hitachi   | HDT722525DLA380    | 250 GB | 1       | 3559  | 368   | 0.03   |
| Seagate   | ST1000NC000-1CX162 | 1 TB   | 1       | 2088  | 224   | 0.03   |
| HGST      | HTS725050B7E630    | 500 GB | 4       | 8     | 0     | 0.02   |
| Seagate   | ST18000NE000-2Y... | 18 TB  | 1       | 8     | 0     | 0.02   |
| WDC       | WD10EVVS-63M5B0    | 1 TB   | 1       | 73    | 8     | 0.02   |
| Toshiba   | HDWL110            | 1 TB   | 1       | 8     | 0     | 0.02   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 1       | 6     | 0     | 0.02   |
| WDC       | WD20SMZW-11JW8S0   | 2 TB   | 1       | 5     | 0     | 0.01   |
| WDC       | WD60EZRX-00MVLB1   | 6 TB   | 1       | 1330  | 248   | 0.01   |
| WDC       | WD20SPZX-21UA7T0   | 2 TB   | 2       | 5     | 0     | 0.01   |
| Seagate   | ST31500341AS       | 1.5 TB | 1       | 2761  | 670   | 0.01   |
| Seagate   | ST3160211AS        | 160 GB | 1       | 1802  | 497   | 0.01   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 1       | 113   | 32    | 0.01   |
| HGST      | HTS541010A9E680    | 1 TB   | 1       | 888   | 259   | 0.01   |
| Samsung   | HD322HJ            | 320 GB | 1       | 3324  | 1015  | 0.01   |
| HP        | GJ0250EAGSQ        | 250 GB | 2       | 3080  | 1028  | 0.01   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 2       | 2     | 0     | 0.01   |
| WDC       | WD1600JS-75NCB2    | 160 GB | 1       | 2854  | 1502  | 0.01   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 1       | 649   | 384   | 0.00   |
| MediaMax  | WL4000GSA6472E     | 4.9 TB | 1       | 1617  | 1054  | 0.00   |
| WDC       | WD5000AADS-00M2B0  | 500 GB | 1       | 2968  | 2023  | 0.00   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 3       | 1309  | 1067  | 0.00   |
| Samsung   | SP2004C            | 200 GB | 1       | 1212  | 1105  | 0.00   |
| HGST      | HTS541075A9E680    | 752 GB | 1       | 1044  | 1026  | 0.00   |
| WDC       | WD2500BEVS-60UST0  | 250 GB | 1       | 400   | 413   | 0.00   |
| Seagate   | ST9120817AS        | 120 GB | 1       | 3408  | 3854  | 0.00   |
| HGST      | HTS725032A7E630    | 320 GB | 1       | 461   | 538   | 0.00   |
| Seagate   | ST3750330NS        | 752 GB | 1       | 22    | 26    | 0.00   |
| WDC       | WD2003FYPS-27Y2B0  | 2 TB   | 1       | 1747  | 2073  | 0.00   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 1       | 1638  | 2016  | 0.00   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 1       | 847   | 1060  | 0.00   |
| Toshiba   | MQ01ABD100         | 1 TB   | 2       | 655   | 1640  | 0.00   |
| HGST      | HTS545050A7E680    | 500 GB | 1       | 362   | 1023  | 0.00   |
| Seagate   | ST3250820AS        | 250 GB | 1       | 957   | 3053  | 0.00   |
| Seagate   | ST3500320NS        | 500 GB | 2       | 585   | 2573  | 0.00   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 1       | 332   | 1509  | 0.00   |
| Seagate   | ST1000LM010-9YH146 | 1 TB   | 1       | 61    | 1087  | 0.00   |

HDD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF   |
|-----------|------------------------|--------|---------|-------|-------|--------|
| WDC       | Raptor                 | 1      | 1       | 4525  | 0     | 12.40  |
| Hitachi   | Deskstar 7K500         | 1      | 1       | 4323  | 0     | 11.84  |
| Hitachi   | Sun Original           | 1      | 15      | 3820  | 1     | 8.96   |
| Hitachi   | Deskstar 7K1000        | 3      | 17      | 3322  | 1     | 8.27   |
| Samsung   | SpinPoint S250         | 1      | 1       | 2882  | 0     | 7.90   |
| Hitachi   | Deskstar 7K3000        | 4      | 71      | 2940  | 1     | 7.66   |
| Toshiba   | 3.5" DT01ABA Deskto... | 1      | 1       | 2632  | 0     | 7.21   |
| Hitachi   | Ultrastar A7K1000      | 1      | 23      | 2668  | 1     | 7.11   |
| Seagate   | Constellation ES.2 ... | 3      | 100     | 2905  | 25    | 7.03   |
| Seagate   | Constellation ES.2     | 1      | 2       | 2424  | 0     | 6.64   |
| WDC       | RE2                    | 1      | 5       | 2756  | 1     | 6.58   |
| HP        | Seagate Constellati... | 1      | 3       | 2306  | 0     | 6.32   |
| HP        | RE3                    | 1      | 1       | 2228  | 0     | 6.11   |
| WDC       | RE3                    | 12     | 61      | 2710  | 51    | 5.86   |
| Seagate   | NAS HDD                | 2      | 28      | 2213  | 2     | 5.67   |
| HGST      | Deskstar 7K4000        | 1      | 6       | 2027  | 0     | 5.55   |
| Maxtor    | DiamondMax 10 (SATA... | 1      | 2       | 1932  | 0     | 5.29   |
| HP        | Seagate Barracuda 7... | 1      | 2       | 2819  | 513   | 4.82   |
| Hitachi   | Ultrastar 7K3000       | 3      | 59      | 1828  | 3     | 4.79   |
| Hitachi   | Deskstar 7K2000        | 2      | 64      | 2208  | 48    | 4.78   |
| HGST      | Ultrastar 7K4000       | 4      | 332     | 1733  | 8     | 4.48   |
| Seagate   | Constellation.2 (SATA) | 3      | 64      | 1755  | 1     | 4.43   |
| WDC       | Caviar Black           | 22     | 230     | 1885  | 32    | 4.41   |
| Seagate   | Constellation ES.3     | 5      | 651     | 1957  | 104   | 4.41   |
| Seagate   | Surveillance           | 11     | 47      | 1767  | 2     | 4.39   |
| Hitachi   | Deskstar P7K500        | 2      | 5       | 2923  | 3     | 4.39   |
| WDC       | RE4-GP                 | 4      | 21      | 2450  | 261   | 4.35   |
| Seagate   | Enterprise NAS HDD     | 2      | 13      | 1703  | 1     | 4.30   |
| WDC       | Green                  | 12     | 58      | 1733  | 7     | 4.20   |
| Samsung   | SpinPoint F1 DT        | 5      | 31      | 2696  | 154   | 4.19   |
| Hitachi   | Ultrastar A7K2000      | 8      | 81      | 1993  | 55    | 4.10   |
| Hitachi   | Deskstar 7K1000.B      | 1      | 1       | 1493  | 0     | 4.09   |
| Seagate   | Barracuda ES           | 6      | 32      | 1816  | 277   | 4.03   |
| Seagate   | Barracuda 7200.10      | 10     | 21      | 2218  | 218   | 4.03   |
| Seagate   | SpinPoint M8 (AF)      | 1      | 1       | 1463  | 0     | 4.01   |
| Hitachi   | Deskstar T7K500        | 3      | 7       | 2761  | 5     | 3.99   |
| Samsung   | SpinPoint P80          | 1      | 1       | 1426  | 0     | 3.91   |
| HGST      | MegaScale 4000         | 1      | 8       | 1601  | 31    | 3.90   |
| Hitachi   | Deskstar 7K1000.C      | 7      | 32      | 2474  | 316   | 3.77   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 2      | 10      | 1564  | 1     | 3.63   |
| WDC       | Caviar Green           | 10     | 24      | 2210  | 256   | 3.62   |
| HGST      | Deskstar NAS           | 6      | 55      | 1328  | 1     | 3.62   |
| WDC       | Caviar Blue            | 20     | 29      | 2084  | 11    | 3.57   |
| Seagate   | Barracuda XT           | 2      | 5       | 2260  | 14    | 3.50   |
| Seagate   | Constellation CS       | 5      | 6       | 1868  | 42    | 3.45   |
| Samsung   | SpinPoint F2 EG        | 2      | 4       | 2405  | 253   | 3.38   |
| Seagate   | Barracuda 7200.14 (AF) | 15     | 188     | 1551  | 149   | 3.37   |
| Toshiba   | 3.5" MG04ACA Enterp... | 7      | 838     | 1265  | 16    | 3.31   |
| WDC       | RE4                    | 21     | 379     | 1444  | 9     | 3.29   |
| Maxtor    | DiamondMax 21          | 3      | 4       | 1836  | 36    | 3.28   |
| MaxDig... | Unknown                | 1      | 1       | 1187  | 0     | 3.25   |
| Seagate   | Archive HDD            | 1      | 19      | 1354  | 56    | 3.22   |
| Samsung   | SpinPoint F3           | 2      | 25      | 1987  | 4     | 3.19   |
| HGST      | Ultrastar 7K6000       | 11     | 529     | 1207  | 7     | 3.18   |
| WDC       | Black Mobile           | 6      | 22      | 1328  | 1     | 3.13   |
| Seagate   | Desktop HDD.15         | 3      | 150     | 1212  | 22    | 3.12   |
| Seagate   | Barracuda Pro          | 1      | 215     | 1166  | 1     | 3.07   |
| HP        | Proliant HardDrive     | 14     | 24      | 2233  | 290   | 3.05   |
| Seagate   | Enterprise Capacity... | 17     | 4724    | 1328  | 28    | 2.99   |
| Seagate   | SpinPoint M9T          | 1      | 16      | 1215  | 1     | 2.96   |
| WDC       | VelociRaptor           | 9      | 33      | 1185  | 1     | 2.92   |
| WDC       | Caviar SE              | 5      | 5       | 1634  | 301   | 2.91   |
| Toshiba   | X300                   | 7      | 127     | 1104  | 15    | 2.89   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 393     | 1160  | 25    | 2.89   |
| Seagate   | Constellation ES (S... | 3      | 50      | 1662  | 71    | 2.88   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 1       | 1032  | 0     | 2.83   |
| HGST      | Ultrastar He8          | 5      | 54      | 1060  | 5     | 2.82   |
| HPE       | WDC Enterprise         | 2      | 10      | 1353  | 9     | 2.75   |
| Samsung   | SpinPoint F4 EG (AF)   | 1      | 3       | 1825  | 3     | 2.70   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 4      | 75      | 1132  | 29    | 2.67   |
| Seagate   | Constellation ES       | 2      | 4       | 1164  | 1     | 2.61   |
| Fujitsu   | MHW BH                 | 1      | 1       | 946   | 0     | 2.59   |
| Toshiba   | S300                   | 2      | 3       | 937   | 0     | 2.57   |
| Toshiba   | 2.5" HDD               | 1      | 1       | 927   | 0     | 2.54   |
| Seagate   | Desktop SSHD           | 2      | 8       | 1465  | 164   | 2.50   |
| WDC       | RE                     | 18     | 199     | 1446  | 39    | 2.48   |
| WDC       | Red                    | 23     | 848     | 1336  | 9     | 2.44   |
| WDC       | Se                     | 7      | 27      | 1063  | 2     | 2.42   |
| HGST      | Travelstar 5K1000      | 4      | 9       | 1067  | 143   | 2.34   |
| Seagate   | Barracuda SpinPoint F3 | 2      | 5       | 1704  | 4     | 2.27   |
| WDC       | Gold                   | 17     | 331     | 852   | 8     | 2.26   |
| MediaMax  | WL2000                 | 1      | 1       | 817   | 0     | 2.24   |
| Seagate   | Skyhawk                | 5      | 29      | 835   | 2     | 2.21   |
| Seagate   | Barracuda 7200.7 an... | 1      | 1       | 3197  | 3     | 2.19   |
| WDC       | Black                  | 11     | 425     | 837   | 4     | 2.19   |
| WDC       | Blue                   | 50     | 240     | 954   | 19    | 2.18   |
| Seagate   | Sun Internal           | 1      | 1       | 1574  | 1     | 2.16   |
| HGST      | Ultrastar 7K2          | 3      | 198     | 794   | 7     | 2.14   |
| Hitachi   | Travelstar 7K320       | 1      | 1       | 727   | 0     | 1.99   |
| HGST      | Travelstar 7K1000      | 1      | 5       | 1393  | 605   | 1.98   |
| Seagate   | Terascale              | 1      | 6       | 722   | 0     | 1.98   |
| Seagate   | Exos X12               | 2      | 142     | 738   | 6     | 1.97   |
| HPE       | Proliant HardDrive     | 6      | 281     | 753   | 1     | 1.94   |
| HPE       | Seagate Constellati... | 1      | 18      | 909   | 1     | 1.92   |
| Seagate   | Mobile HDD             | 1      | 37      | 955   | 211   | 1.92   |
| Toshiba   | 3.5" HDD E300          | 1      | 1       | 699   | 0     | 1.92   |
| Seagate   | Seagate Enterprise     | 1      | 198     | 699   | 23    | 1.77   |
| Samsung   | SpinPoint F3 RE        | 1      | 1       | 637   | 0     | 1.75   |
| WDC       | Purple                 | 12     | 42      | 619   | 0     | 1.70   |
| Hitachi   | Deskstar E7K1000       | 2      | 6       | 2445  | 3     | 1.68   |
| HGST      | Ultrastar He6          | 1      | 44      | 607   | 1     | 1.66   |
| HGST      | Ultrastar DC HC520 ... | 5      | 2290    | 614   | 1     | 1.64   |
| Seagate   | Barracuda 7200.12      | 7      | 27      | 1111  | 203   | 1.61   |
| Seagate   | Exos 7E2               | 9      | 147     | 819   | 11    | 1.60   |
| Seagate   | Pipeline HD 5900.2     | 1      | 4       | 723   | 3     | 1.58   |
| Hitachi   | Ultrastar 7K4000       | 3      | 27      | 709   | 21    | 1.58   |
| Seagate   | IronWolf Pro           | 5      | 22      | 963   | 273   | 1.57   |
| Toshiba   | Toshiba Enterprise     | 5      | 680     | 599   | 1     | 1.56   |
| HGST      | Ultrastar He10         | 6      | 408     | 570   | 1     | 1.56   |
| WDC       | Red Pro                | 12     | 121     | 598   | 1     | 1.55   |
| Seagate   | Constellation ES (S... | 3      | 35      | 1263  | 65    | 1.54   |
| Seagate   | BarraCuda Pro          | 2      | 15      | 840   | 211   | 1.53   |
| Seagate   | Barracuda Compute      | 2      | 6       | 554   | 0     | 1.52   |
| Toshiba   | L200                   | 2      | 5       | 550   | 0     | 1.51   |
| Toshiba   | 3.5" MD04ACA Enterp... | 1      | 436     | 551   | 3     | 1.49   |
| Seagate   | Barracuda 3.5          | 3      | 99      | 536   | 12    | 1.41   |
| Seagate   | Barracuda 2.5 5400     | 4      | 109     | 581   | 33    | 1.40   |
| Toshiba   | V300                   | 1      | 8       | 571   | 5     | 1.36   |
| Samsung   | SpinPoint F4           | 1      | 1       | 477   | 0     | 1.31   |
| Toshiba   | P300                   | 4      | 81      | 486   | 45    | 1.29   |
| HGST      | Ultrastar DC HC310     | 5      | 407     | 462   | 12    | 1.25   |
| Seagate   | Exos 7E2000            | 2      | 67      | 444   | 0     | 1.22   |
| WDC       | Scorpio Black          | 4      | 5       | 1199  | 61    | 1.22   |
| Seagate   | Momentus 7200.4        | 1      | 4       | 674   | 10    | 1.19   |
| WDC       | Elements / My Passport | 11     | 16      | 446   | 1     | 1.18   |
| Samsung   | SpinPoint P80 SD       | 1      | 2       | 1964  | 841   | 1.17   |
| Seagate   | FireCuda 3.5           | 1      | 4       | 424   | 0     | 1.16   |
| Toshiba   | MG07ACA Enterprise ... | 3      | 137     | 429   | 1     | 1.15   |
| Samsung   | SpinPoint T166         | 1      | 3       | 2138  | 676   | 1.14   |
| Seagate   | Exos 7E8               | 8      | 224     | 426   | 17    | 1.10   |
| Seagate   | Barracuda Green (AF)   | 2      | 5       | 1252  | 439   | 1.08   |
| HGST      | Ultrastar DC HC320     | 2      | 59      | 392   | 1     | 1.06   |
| HP        | Constellation ES.3     | 1      | 2       | 383   | 0     | 1.05   |
| Hitachi   | Travelstar 5K250       | 1      | 1       | 1508  | 3     | 1.03   |
| Seagate   | Exos X14               | 3      | 210     | 375   | 3     | 1.02   |
| Toshiba   | 3.5" HDD N300          | 1      | 11      | 370   | 0     | 1.02   |
| HGST      | Travelstar Z7K500      | 2      | 4       | 928   | 896   | 1.01   |
| Seagate   | Barracuda 7200.8       | 1      | 1       | 4725  | 12    | 1.00   |
| Toshiba   | MG06ACA Enterprise ... | 5      | 212     | 366   | 1     | 0.99   |
| Seagate   | Barracuda Pro Compute  | 1      | 4       | 342   | 0     | 0.94   |
| MediaMax  | WL4000                 | 2      | 3       | 880   | 352   | 0.94   |
| Seagate   | IronWolf               | 12     | 409     | 341   | 20    | 0.91   |
| Seagate   | Laptop HDD             | 3      | 8       | 818   | 400   | 0.90   |
| WDC       | AV-GP                  | 5      | 9       | 415   | 2     | 0.88   |
| Seagate   | SkyHawk                | 3      | 23      | 311   | 0     | 0.85   |
| Seagate   | BarraCuda 3.5          | 6      | 89      | 347   | 20    | 0.83   |
| WDC       | Ultrastar DC HC530     | 2      | 1727    | 291   | 1     | 0.80   |
| Toshiba   | N300                   | 3      | 19      | 335   | 2     | 0.79   |
| Seagate   | Momentus 7200.5        | 1      | 1       | 285   | 0     | 0.78   |
| Maxtor    | DiamondMax 22          | 1      | 2       | 459   | 617   | 0.74   |
| WDC       | Blue Mobile            | 11     | 21      | 269   | 0     | 0.74   |
| Toshiba   | Toshiba Client HDD     | 1      | 1       | 268   | 0     | 0.74   |
| HPE       | Seagate Enterprise     | 3      | 80      | 293   | 1     | 0.72   |
| WDC       | Shrek LT 2.5           | 1      | 1       | 233   | 0     | 0.64   |
| WDC       | Scorpio Blue           | 4      | 5       | 463   | 85    | 0.62   |
| Toshiba   | 2.5" HDD MQ01ACF       | 2      | 6       | 342   | 2     | 0.62   |
| Apple     | Travelstar 5K1000      | 1      | 1       | 220   | 0     | 0.60   |
| Seagate   | Barracuda LP           | 1      | 1       | 218   | 0     | 0.60   |
| Seagate   | Exos X16               | 6      | 98      | 210   | 0     | 0.58   |
| HP        | 250GB SATA disk VB0... | 1      | 3       | 322   | 204   | 0.54   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 1       | 1702  | 8     | 0.52   |
| Hitachi   | Deskstar 7K1000.D      | 2      | 12      | 1318  | 1013  | 0.46   |
| Seagate   | FireCuda 2.5           | 1      | 4       | 158   | 0     | 0.43   |
| Maxtor    | DiamondMax 20          | 1      | 1       | 1203  | 7     | 0.41   |
| WDC       | Green Mobile           | 1      | 4       | 1370  | 16    | 0.39   |
| Apple     | HGST Travelstar Z5K500 | 1      | 1       | 141   | 0     | 0.39   |
| Seagate   | Exos X18               | 1      | 11      | 130   | 0     | 0.36   |
| Hitachi   | Travelstar 5K500.B     | 3      | 3       | 433   | 2     | 0.33   |
| WDC       | Ultrastar DC HC330     | 1      | 21      | 117   | 11    | 0.32   |
| Samsung   | SpinPoint M7E (AF)     | 1      | 1       | 112   | 0     | 0.31   |
| Seagate   | Barracuda 7200.9       | 2      | 2       | 998   | 249   | 0.27   |
| WDC       | Ultrastar DC HC500     | 1      | 8       | 95    | 0     | 0.26   |
| Hitachi   | Travelstar 7K500       | 2      | 3       | 1173  | 343   | 0.25   |
| Seagate   | Momentus 5400.6        | 1      | 2       | 1360  | 69    | 0.20   |
| WDC       | Ultrastar DC HC550     | 2      | 255     | 70    | 0     | 0.19   |
| Seagate   | Momentus 5400.3        | 1      | 1       | 348   | 4     | 0.19   |
| Toshiba   | 2.5" HDD MQ01UBD       | 2      | 3       | 74    | 6     | 0.18   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 2       | 197   | 1010  | 0.18   |
| Seagate   | Video 3.5 HDD          | 2      | 2       | 113   | 16    | 0.16   |
| Toshiba   | 2.5" HDD MK..52GSX     | 1      | 1       | 54    | 0     | 0.15   |
| WDC       | HGST Ultrastar He10    | 1      | 1       | 38    | 0     | 0.11   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 1       | 38    | 0     | 0.11   |
| Hitachi   | Travelstar 7K100       | 1      | 1       | 2330  | 66    | 0.10   |
| Apple     | Barracuda              | 1      | 1       | 254   | 8     | 0.08   |
| Seagate   | Barracuda ES.2         | 3      | 6       | 539   | 1031  | 0.07   |
| Seagate   | Barracuda 7200.11      | 2      | 2       | 1860  | 347   | 0.06   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 1      | 1       | 20    | 0     | 0.06   |
| WDC       | Red Plus               | 1      | 1       | 16    | 0     | 0.04   |
| Hitachi   | Deskstar T7K250        | 1      | 1       | 3559  | 368   | 0.03   |
| HGST      | Travelstar Z7K500.B    | 1      | 4       | 8     | 0     | 0.02   |
| Samsung   | SpinPoint P120         | 1      | 1       | 1212  | 1105  | 0.00   |
| Seagate   | Momentus 5400.4        | 1      | 1       | 3408  | 3854  | 0.00   |
| Hitachi   | Deskstar 5K3000        | 1      | 1       | 1638  | 2016  | 0.00   |
| Toshiba   | 2.5" HDD MQ01ABD       | 1      | 2       | 655   | 1640  | 0.00   |
| HGST      | Travelstar Z5K500      | 1      | 1       | 362   | 1023  | 0.00   |
| Seagate   | FreePlay               | 1      | 1       | 61    | 1087  | 0.00   |

HDD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| Hitachi     | 53     | 432     | 2263  | 79    | 4.98   |
| Samsung     | 18     | 74      | 2236  | 145   | 3.41   |
| MaxDigital  | 1      | 1       | 1187  | 0     | 3.25   |
| HP          | 19     | 35      | 2003  | 246   | 3.19   |
| Maxtor      | 6      | 9       | 1481  | 154   | 2.85   |
| Seagate     | 212    | 8407    | 1217  | 39    | 2.78   |
| Fujitsu     | 1      | 1       | 946   | 0     | 2.59   |
| Toshiba     | 66     | 3057    | 855   | 13    | 2.21   |
| HGST        | 59     | 4413    | 776   | 6     | 2.06   |
| WDC         | 318    | 5175    | 865   | 11    | 1.92   |
| HPE         | 12     | 389     | 681   | 1     | 1.71   |
| MediaMax    | 3      | 4       | 864   | 264   | 1.26   |
| Apple       | 3      | 3       | 205   | 3     | 0.36   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See complete list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Kingston  | SVP100S264G        | 64 GB  | 1       | 3150  | 0     | 8.63   |
| Samsung   | SSD 840 EVO        | 120 GB | 7       | 3036  | 0     | 8.32   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 3       | 2924  | 0     | 8.01   |
| Micron    | MTFDDAK512MAR-1... | 512 GB | 3       | 2720  | 0     | 7.45   |
| Samsung   | SSD 840 EVO        | 500 GB | 3       | 2714  | 0     | 7.44   |
| SATADOM   | D150SV             | 2 GB   | 1       | 2697  | 0     | 7.39   |
| OCZ       | VERTEX3            | 120 GB | 4       | 3462  | 1     | 7.22   |
| OCZ       | AGILITY3           | 240 GB | 1       | 2501  | 0     | 6.85   |
| SanDisk   | SDSSDP064G         | 64 GB  | 1       | 2475  | 0     | 6.78   |
| Samsung   | SSD 830 Series     | 256 GB | 1       | 2440  | 0     | 6.69   |
| OCZ       | VERTEX4            | 256 GB | 1       | 2437  | 0     | 6.68   |
| HP        | VK0480GDPVT        | 480 GB | 1       | 2425  | 0     | 6.65   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 1       | 2376  | 0     | 6.51   |
| Micron    | MTFDDAK128MAR-1... | 128 GB | 3       | 2373  | 0     | 6.50   |
| Apple     | SSD SM256E         | 256 GB | 2       | 2325  | 0     | 6.37   |
| HPE       | MK0800GCTZB        | 800 GB | 1       | 2321  | 0     | 6.36   |
| Intel     | SSDSA2CW120G3      | 120 GB | 40      | 2796  | 54    | 6.07   |
| Corsair   | Force 3 SSD        | 120 GB | 3       | 2182  | 0     | 5.98   |
| Intel     | SSDSC2BP240G4      | 240 GB | 9       | 2094  | 0     | 5.74   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 4       | 2048  | 0     | 5.61   |
| Samsung   | SSD 850 PRO        | 128 GB | 7       | 2047  | 0     | 5.61   |
| Transcend | TS128GSSD340       | 128 GB | 1       | 2033  | 0     | 5.57   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 1       | 2007  | 0     | 5.50   |
| Intel     | SSDSC2CW240A3      | 240 GB | 55      | 2137  | 1     | 5.49   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 4       | 1983  | 0     | 5.43   |
| Samsung   | SSD 840 EVO        | 250 GB | 6       | 2468  | 5     | 5.42   |
| Micron    | P400e-MTFDDAK40... | 400 GB | 3       | 1967  | 0     | 5.39   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 4       | 1959  | 0     | 5.37   |
| Samsung   | MZ7LM120HCFD-00003 | 120 GB | 4       | 1956  | 0     | 5.36   |
| Intel     | VR0120GEJXL        | 120 GB | 1       | 1950  | 0     | 5.34   |
| Samsung   | MZ7KM200HAGR00D3   | 200 GB | 2       | 1925  | 0     | 5.28   |
| Samsung   | MZ7WD480HAGM-00003 | 480 GB | 6       | 1924  | 0     | 5.27   |
| Intel     | SSDSC2CW480A3      | 400 GB | 12      | 2083  | 1     | 5.27   |
| Kingston  | SE50S3480G         | 480 GB | 5       | 1908  | 0     | 5.23   |
| Intel     | SSDSC2BA100G3      | 100 GB | 27      | 1937  | 1     | 5.21   |
| Samsung   | MZ7TD512HAGM-00000 | 512 GB | 4       | 2205  | 1     | 5.18   |
| Micron    | M500DC_MTFDDAK1... | 120 GB | 2       | 1890  | 0     | 5.18   |
| Samsung   | MZ7LM480HCHP-0E003 | 480 GB | 7       | 1873  | 0     | 5.13   |
| Samsung   | SSD 840 EVO        | 1 TB   | 19      | 2377  | 56    | 5.13   |
| Intel     | SSDSC2CW180A3      | 180 GB | 14      | 1940  | 1     | 5.13   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 1862  | 0     | 5.10   |
| ADATA     | SP600              | 128 GB | 1       | 1849  | 0     | 5.07   |
| Kingston  | SH103S3480G        | 480 GB | 1       | 1840  | 0     | 5.04   |
| Plextor   | PX-128M5S          | 128 GB | 1       | 1838  | 0     | 5.04   |
| OCZ       | TRION100           | 480 GB | 1       | 1833  | 0     | 5.02   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 12      | 1811  | 0     | 4.96   |
| Intel     | SSDSC2BB480G4      | 480 GB | 46      | 1910  | 23    | 4.89   |
| Samsung   | MZ7WD480HCGM-00003 | 480 GB | 23      | 1936  | 45    | 4.86   |
| Intel     | SSDSC2CT240A4      | 240 GB | 2       | 2646  | 1     | 4.84   |
| Intel     | SSDSA2BZ200G3      | 200 GB | 2       | 2332  | 1     | 4.78   |
| Intel     | SSDSC2BB800G4      | 800 GB | 7       | 1734  | 0     | 4.75   |
| Intel     | SSDSC2CT120A3      | 120 GB | 16      | 2640  | 2     | 4.75   |
| Crucial   | CT250MX200SSD1     | 250 GB | 11      | 1723  | 0     | 4.72   |
| Samsung   | MZ7WD240HAFV-000D2 | 240 GB | 7       | 2014  | 5     | 4.70   |
| SanDisk   | SDSSDHII960G       | 960 GB | 1       | 1708  | 0     | 4.68   |
| Intel     | SSDSC2BB120G4      | 120 GB | 17      | 1798  | 1     | 4.66   |
| Samsung   | MZ7WD120HCFV-00003 | 120 GB | 1       | 1689  | 0     | 4.63   |
| Samsung   | MZ7KM960HAHP-00005 | 800 GB | 1       | 1671  | 0     | 4.58   |
| Intel     | SSDSC2BB300H4      | 304 GB | 3       | 1663  | 0     | 4.56   |
| Samsung   | MZ7PD480HAGM-000D3 | 480 GB | 1       | 1653  | 0     | 4.53   |
| HPE       | MK0240GFDKQ        | 240 GB | 1       | 1650  | 0     | 4.52   |
| Toshiba   | THNSNJ960PCSZ      | 960 GB | 42      | 1676  | 1     | 4.50   |
| Samsung   | SSD 850 PRO        | 512 GB | 35      | 1631  | 0     | 4.47   |
| Intel     | SSDSC2BB160G4      | 160 GB | 57      | 1892  | 1     | 4.44   |
| Kingston  | SH103S3240G        | 240 GB | 2       | 2144  | 1     | 4.41   |
| Toshiba   | THNSNJ480PCSZ      | 480 GB | 1       | 1607  | 0     | 4.40   |
| Samsung   | SSD 850 PRO        | 256 GB | 37      | 1668  | 1     | 4.39   |
| Intel     | SSDSC2BB080G6      | 80 GB  | 1       | 1603  | 0     | 4.39   |
| Toshiba   | THNSN8480PCSE      | 480 GB | 1       | 1601  | 0     | 4.39   |
| HP        | VK0240GECQN        | 240 GB | 8       | 1590  | 0     | 4.36   |
| Intel     | SSDSC2BA400G3C     | 400 GB | 2       | 1590  | 0     | 4.36   |
| Samsung   | MZ7LM1T9HCJM-0E003 | 1.9 TB | 1       | 1573  | 0     | 4.31   |
| Intel     | SSDSC2BA400G3      | 400 GB | 5       | 1573  | 0     | 4.31   |
| HP        | VK0960GFDKK        | 960 GB | 1       | 1569  | 0     | 4.30   |
| Samsung   | MZ7GE960HMHP-00003 | 960 GB | 16      | 2053  | 131   | 4.30   |
| Intel     | SSDSC2BB012T6      | 1.2 TB | 5       | 1820  | 1     | 4.30   |
| HP        | VK0800GDJYA        | 800 GB | 31      | 1650  | 2     | 4.24   |
| Intel     | SSDSC2BB800G6      | 800 GB | 68      | 1655  | 15    | 4.23   |
| Kingston  | SKC300S37A120G     | 120 GB | 2       | 1538  | 0     | 4.22   |
| Samsung   | MZ7KM960HAHP-00005 | 960 GB | 47      | 1534  | 0     | 4.20   |
| Kingston  | SVP200S37A120G     | 120 GB | 1       | 1522  | 0     | 4.17   |
| Crucial   | CT512MX100SSD1     | 240 GB | 4       | 1899  | 1     | 4.16   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 1       | 1511  | 0     | 4.14   |
| Samsung   | MZ7LM480HCHP-00003 | 480 GB | 66      | 1511  | 0     | 4.14   |
| Samsung   | SSD 840 PRO Series | 128 GB | 17      | 1889  | 62    | 4.14   |
| Intel     | SSDSC2BW240A3      | 240 GB | 1       | 1489  | 0     | 4.08   |
| Kingston  | SUV300S37A120G     | 120 GB | 1       | 1471  | 0     | 4.03   |
| Intel     | SSDSC2BB016T6      | 1.6 TB | 13      | 1458  | 0     | 4.00   |
| Samsung   | MCBQE25G5MPQ-0VAD3 | 25 GB  | 1       | 1456  | 0     | 3.99   |
| Samsung   | MZ7KM480HAHP-00005 | 480 GB | 81      | 1450  | 0     | 3.97   |
| Intel     | SSDSC2BB120G6K     | 120 GB | 24      | 1449  | 0     | 3.97   |
| HPE       | MK001920GWCFB      | 1.9 TB | 1       | 1449  | 0     | 3.97   |
| Intel     | SSDSC2BB240G6      | 240 GB | 18      | 1449  | 0     | 3.97   |
| Intel     | SSDSC2BB120G6      | 120 GB | 4       | 1448  | 0     | 3.97   |
| Apacer    | AS510S             | 128 GB | 1       | 1444  | 0     | 3.96   |
| Samsung   | MZ7KM480HAHP-0E005 | 480 GB | 15      | 1440  | 0     | 3.95   |
| Samsung   | SSD 840 PRO Series | 512 GB | 10      | 1909  | 62    | 3.93   |
| Intel     | SSDSC2BB300G4      | 304 GB | 1       | 1428  | 0     | 3.91   |
| Kingston  | SH103S3120G        | 120 GB | 10      | 1523  | 1     | 3.86   |
| Crucial   | CT500MX200SSD1     | 500 GB | 14      | 1404  | 0     | 3.85   |
| Intel     | SSDSC2BA200G3      | 200 GB | 15      | 1532  | 1     | 3.85   |
| Intel     | SSDSC2BB240G4      | 240 GB | 40      | 1460  | 1     | 3.83   |
| SanDisk   | SD7UB2Q512G1022    | 512 GB | 7       | 1498  | 1     | 3.81   |
| Toshiba   | THNSN8240PCSE      | 240 GB | 2       | 1383  | 0     | 3.79   |
| SanDisk   | SDLF1CRM-017T-1HST | 1.7 TB | 4       | 1383  | 0     | 3.79   |
| SanDisk   | SDLF1DAR480G-1HHS  | 480 GB | 2       | 1382  | 0     | 3.79   |
| Lite-On   | PH3-CE120          | 120 GB | 2       | 1376  | 0     | 3.77   |
| Samsung   | MZ7KM240HAGR-00005 | 240 GB | 17      | 1368  | 0     | 3.75   |
| Kingston  | SV300S37A240G      | 240 GB | 100     | 1578  | 9     | 3.72   |
| Kingston  | SKC300S37A240G     | 240 GB | 12      | 1355  | 0     | 3.71   |
| Intel     | SSDSC2BB480G6      | 480 GB | 25      | 1353  | 0     | 3.71   |
| Lite-On   | PH4-CE120          | 120 GB | 1       | 1352  | 0     | 3.71   |
| SPCC      | SSD                | 240 GB | 1       | 1351  | 0     | 3.70   |
| Samsung   | MZ7KM1T9HAJM-000NU | 1.9 TB | 1       | 1342  | 0     | 3.68   |
| Intel     | SSDSC2BP480G4      | 480 GB | 1       | 1339  | 0     | 3.67   |
| ADATA     | SP900              | 256 GB | 2       | 2224  | 2     | 3.66   |
| Crucial   | CT750MX300SSD1     | 752 GB | 16      | 1532  | 1     | 3.66   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 1       | 1330  | 0     | 3.65   |
| Samsung   | MZ7KM120HAFD-00005 | 120 GB | 14      | 1330  | 0     | 3.65   |
| SanDisk   | X300 MSATA         | 256 GB | 1       | 1328  | 0     | 3.64   |
| Intel     | SSDSC2BB016T4      | 1.6 TB | 5       | 1519  | 1     | 3.63   |
| Samsung   | MZ7GE480HMHP-00003 | 480 GB | 12      | 1827  | 163   | 3.61   |
| Toshiba   | VX500              | 1 TB   | 6       | 1304  | 0     | 3.57   |
| Kingston  | SE50S37240G        | 240 GB | 1       | 1304  | 0     | 3.57   |
| Intel     | SSDSC2BB600G4      | 600 GB | 10      | 1300  | 0     | 3.56   |
| Samsung   | MZ7KM240HMHQ0D3    | 240 GB | 2       | 1295  | 0     | 3.55   |
| Kingston  | SKC400S37128G      | 128 GB | 4       | 1280  | 0     | 3.51   |
| Samsung   | SSD 850 PRO        | 1 TB   | 37      | 1865  | 6     | 3.47   |
| Samsung   | MZ7WD960HAGP-00003 | 960 GB | 3       | 1262  | 0     | 3.46   |
| Intel     | SSDSC2BX400G4      | 400 GB | 1       | 1252  | 0     | 3.43   |
| Samsung   | MZ7KM120HAFD-0E005 | 120 GB | 2       | 1246  | 0     | 3.41   |
| Kingston  | SUV300S37A240G     | 240 GB | 2       | 1245  | 0     | 3.41   |
| HPE       | MK0200GEYKC        | 200 GB | 21      | 1244  | 0     | 3.41   |
| SPCC      | SSD                | 120 GB | 1       | 1231  | 0     | 3.37   |
| Samsung   | SSD 850 EVO        | 120 GB | 14      | 1316  | 16    | 3.36   |
| Samsung   | MZ7LM960HCHP-00005 | 960 GB | 16      | 1226  | 0     | 3.36   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 14      | 1217  | 0     | 3.34   |
| Intel     | SSDSC2BB480H4      | 480 GB | 6       | 1449  | 1     | 3.33   |
| Samsung   | MZ7KM240HAGR-0E005 | 240 GB | 17      | 1567  | 22    | 3.32   |
| Samsung   | SSD 840 PRO Series | 256 GB | 19      | 2562  | 273   | 3.31   |
| Intel     | SSDSC2BA200G4      | 200 GB | 94      | 1207  | 0     | 3.31   |
| Samsung   | MZ7KM960HAHP-0E005 | 960 GB | 4       | 1204  | 0     | 3.30   |
| SanDisk   | Ultra II           | 960 GB | 12      | 1202  | 0     | 3.29   |
| Intel     | SSDSC2BB150G7      | 150 GB | 11      | 1193  | 0     | 3.27   |
| SanDisk   | SDLF1DAR-960G-1HA2 | 960 GB | 8       | 1193  | 0     | 3.27   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 1       | 1181  | 0     | 3.24   |
| OCZ       | VECTOR             | 128 GB | 1       | 2353  | 1     | 3.22   |
| Micron    | 5100_MTFDDAK240TCC | 240 GB | 6       | 1329  | 1     | 3.22   |
| HP        | VK0480GEQNB        | 480 GB | 1       | 1171  | 0     | 3.21   |
| SanDisk   | SD7UB2Q512G1122    | 512 GB | 6       | 1447  | 2     | 3.20   |
| Intel     | SSDSC2BA800G4      | 800 GB | 9       | 1163  | 0     | 3.19   |
| Samsung   | MZ7KM960HMJP0D3    | 960 GB | 120     | 1153  | 0     | 3.16   |
| Intel     | SSDSC2BB800G7R     | 800 GB | 40      | 1436  | 53    | 3.15   |
| Kingston  | SE50S3100G         | 100 GB | 3       | 1407  | 1     | 3.11   |
| Intel     | SSDSC2BX200G4      | 200 GB | 16      | 1131  | 0     | 3.10   |
| Kingston  | SE50S37100G        | 100 GB | 1       | 1126  | 0     | 3.09   |
| Samsung   | SSD 750 EVO        | 120 GB | 2       | 1125  | 0     | 3.08   |
| Samsung   | SSD 850 PRO        | 2 TB   | 3       | 1122  | 0     | 3.08   |
| SanDisk   | SD6SB1M064G1022I   | 64 GB  | 6       | 1119  | 0     | 3.07   |
| OCZ       | SABER1000          | 120 GB | 2       | 1113  | 0     | 3.05   |
| Intel     | SSDSC2BX100G4      | 100 GB | 2       | 1090  | 0     | 2.99   |
| Samsung   | MZ7LN512HMJP-00000 | 512 GB | 9       | 1267  | 5     | 2.96   |
| Crucial   | CT480BX200SSD1     | 480 GB | 1       | 1069  | 0     | 2.93   |
| SanDisk   | SDLF1CRR019T-1HHS  | 1.9 TB | 30      | 1078  | 34    | 2.93   |
| Samsung   | SSD 850 EVO        | 1 TB   | 178     | 1316  | 15    | 2.92   |
| Samsung   | SSD 850 EVO        | 2 TB   | 8       | 1056  | 0     | 2.89   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 1       | 1044  | 0     | 2.86   |
| Toshiba   | THNSNJ256GCSU      | 256 GB | 1       | 1036  | 0     | 2.84   |
| Intel     | SSDSC2KB960G7R     | 960 GB | 10      | 1035  | 0     | 2.84   |
| Patriot   | Blast              | 240 GB | 1       | 1030  | 0     | 2.82   |
| Intel     | SSDSC2BA400G4      | 400 GB | 20      | 1025  | 0     | 2.81   |
| SK hynix  | HFS500G32TND-N1A2A | 500 GB | 2       | 1024  | 0     | 2.81   |
| Samsung   | MZ7LM3T8HMLP-00005 | 3.8 TB | 1       | 1023  | 0     | 2.81   |
| Samsung   | MZ7LM1T9HCJM-00003 | 1.9 TB | 6       | 1022  | 0     | 2.80   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 2       | 1005  | 0     | 2.76   |
| OWC       | Mercury Accelsi... | 240 GB | 1       | 2002  | 1     | 2.74   |
| Intel     | SSDSC2BX800G4      | 800 GB | 2       | 1000  | 0     | 2.74   |
| Kingston  | SV300S37A120G      | 120 GB | 31      | 1521  | 9     | 2.72   |
| OCZ       | VERTEX3 MI         | 120 GB | 1       | 2968  | 2     | 2.71   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 4       | 987   | 0     | 2.71   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 2       | 980   | 0     | 2.69   |
| Samsung   | MZ7KM1T9HAJM-00005 | 1.9 TB | 45      | 980   | 0     | 2.69   |
| Kingston  | SHFS37A480G        | 480 GB | 3       | 1330  | 3     | 2.67   |
| Goodram   | SSD                | 240 GB | 4       | 962   | 0     | 2.64   |
| HP        | VK0240GDJXU        | 240 GB | 2       | 1452  | 1     | 2.62   |
| HPE       | LK0480GFJSK        | 480 GB | 1       | 956   | 0     | 2.62   |
| Samsung   | SSD 850 EVO        | 500 GB | 88      | 1016  | 35    | 2.62   |
| Samsung   | SSD 850 EVO        | 250 GB | 71      | 1041  | 34    | 2.60   |
| OCZ       | ARC100             | 480 GB | 4       | 1129  | 21    | 2.59   |
| Samsung   | MZ7LM240HCGR-00005 | 240 GB | 4       | 945   | 0     | 2.59   |
| Intel     | SSDSC2BA200G4C     | 200 GB | 5       | 945   | 0     | 2.59   |
| MyDigi... | SB2                | 128 GB | 6       | 945   | 0     | 2.59   |
| Intel     | SSDSC2BB240G7      | 240 GB | 21      | 934   | 0     | 2.56   |
| Micron    | 5100_MTFDDAK960TBY | 960 GB | 4       | 931   | 0     | 2.55   |
| Kingston  | SKC400S371T        | 1 TB   | 10      | 929   | 0     | 2.55   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 5       | 927   | 0     | 2.54   |
| Samsung   | SSD 840 Series     | 120 GB | 7       | 1862  | 86    | 2.54   |
| HP        | VK000240GWCFD      | 240 GB | 3       | 925   | 0     | 2.53   |
| Samsung   | MZ7LM960HCHP-00003 | 960 GB | 30      | 922   | 0     | 2.53   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 1       | 914   | 0     | 2.50   |
| Toshiba   | THNSN8960PCSE      | 960 GB | 31      | 929   | 1     | 2.49   |
| Kingston  | SKC400S37256G      | 256 GB | 1       | 902   | 0     | 2.47   |
| Kingston  | SKC400S37512G      | 512 GB | 3       | 900   | 0     | 2.47   |
| Samsung   | MZ7KM960HAHP-0Z005 | 960 GB | 1       | 895   | 0     | 2.45   |
| HP        | VK000240GWCNP      | 240 GB | 5       | 893   | 0     | 2.45   |
| Samsung   | MZ7LM480HCHP-00005 | 480 GB | 25      | 888   | 0     | 2.44   |
| SanDisk   | SDSSDH3250G        | 250 GB | 1       | 881   | 0     | 2.41   |
| Dell      | SSDSCKJB120G7R     | 120 GB | 5       | 1043  | 1     | 2.40   |
| HP        | VK000480GWJPE      | 480 GB | 1       | 876   | 0     | 2.40   |
| Samsung   | MZ7KM1T9HMJP-00005 | 1.9 TB | 76      | 872   | 0     | 2.39   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 59      | 866   | 13    | 2.36   |
| Samsung   | SSD 750 EVO        | 250 GB | 4       | 861   | 0     | 2.36   |
| Intel     | SSDSC2BX480G4      | 480 GB | 24      | 860   | 0     | 2.36   |
| Intel     | SSDSC2BB480G7      | 480 GB | 106     | 967   | 1     | 2.36   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 142     | 858   | 0     | 2.35   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 26      | 853   | 0     | 2.34   |
| Intel     | SSDSC2BX016T4      | 1.6 TB | 1       | 849   | 0     | 2.33   |
| Samsung   | SSD 840 Series     | 250 GB | 3       | 2451  | 358   | 2.32   |
| SanDisk   | Ultra II           | 480 GB | 15      | 871   | 1     | 2.31   |
| Intel     | SSDSC2MH120A2      | 120 GB | 2       | 842   | 0     | 2.31   |
| HP        | VK0960GFLKK        | 960 GB | 1       | 841   | 0     | 2.31   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 1       | 840   | 0     | 2.30   |
| Intel     | SSDSCKJB150G7      | 150 GB | 14      | 943   | 1     | 2.28   |
| SuperM... | SSD                | 64 GB  | 27      | 850   | 1     | 2.27   |
| Crucial   | CT525MX300SSD1     | 528 GB | 48      | 873   | 1     | 2.23   |
| Intel     | SSDSC2KG480G7      | 480 GB | 54      | 1022  | 2     | 2.23   |
| Intel     | SSDSA2CW160G3      | 160 GB | 1       | 1623  | 1     | 2.22   |
| XPG       | SX950U             | 120 GB | 2       | 806   | 0     | 2.21   |
| Micron    | M510DC_MTFDDAK4... | 480 GB | 2       | 805   | 0     | 2.21   |
| Crucial   | CT960M500SSD1      | 960 GB | 18      | 1769  | 7     | 2.19   |
| Crucial   | CT275MX300SSD1     | 275 GB | 39      | 994   | 1     | 2.18   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 10      | 790   | 0     | 2.17   |
| Intel     | SSDMCEAC120B3      | 120 GB | 1       | 788   | 0     | 2.16   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 2       | 782   | 0     | 2.14   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 1       | 782   | 0     | 2.14   |
| Kingston  | SV300S37A480G      | 480 GB | 11      | 1017  | 39    | 2.13   |
| Kingston  | SUV500240G         | 240 GB | 4       | 777   | 0     | 2.13   |
| Mushkin   | MKNSSDRE120GB      | 120 GB | 1       | 777   | 0     | 2.13   |
| ADATA     | SP600NS34          | 128 GB | 1       | 772   | 0     | 2.12   |
| SanDisk   | SDSSDA240G         | 240 GB | 2       | 768   | 0     | 2.11   |
| Crucial   | CT256MX100SSD1     | 256 GB | 4       | 1471  | 503   | 2.10   |
| Kingston  | SEDC400S37960G     | 960 GB | 9       | 762   | 0     | 2.09   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 11      | 762   | 0     | 2.09   |
| SanDisk   | SD7SB7S512G1122    | 512 GB | 1       | 762   | 0     | 2.09   |
| Samsung   | MZ7LM960HMJP-00005 | 960 GB | 259     | 906   | 9     | 2.09   |
| ADATA     | SU800              | 128 GB | 2       | 759   | 0     | 2.08   |
| Seagate   | XF1230-1A0480      | 480 GB | 12      | 747   | 0     | 2.05   |
| Toshiba   | THNSF8800CCSE      | 800 GB | 1       | 733   | 0     | 2.01   |
| Samsung   | SSD PM851a 2.5 7mm | 1 TB   | 1       | 732   | 0     | 2.01   |
| Intel     | SSDSC2BB016T7      | 1.6 TB | 61      | 1357  | 3     | 2.00   |
| Intel     | SSDSC2KG240G7      | 240 GB | 42      | 735   | 1     | 1.99   |
| Crucial   | CT500BX100SSD1     | 500 GB | 2       | 723   | 0     | 1.98   |
| Samsung   | MZ7LM960HMJP0D3    | 960 GB | 42      | 734   | 1     | 1.97   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 28      | 863   | 1     | 1.93   |
| Toshiba   | THNSNJ800PCSZ      | 800 GB | 4       | 700   | 0     | 1.92   |
| Toshiba   | THNSF8200CCSE      | 200 GB | 20      | 766   | 1     | 1.89   |
| HP        | VK000240GWJPD      | 240 GB | 1       | 686   | 0     | 1.88   |
| Samsung   | SSD 860 PRO        | 4 TB   | 14      | 685   | 0     | 1.88   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 1       | 678   | 0     | 1.86   |
| HP        | VK0480GEYJR        | 480 GB | 1       | 672   | 0     | 1.84   |
| Intel     | SSDSC2KG240G7R     | 240 GB | 25      | 721   | 83    | 1.84   |
| Kingston  | SHSS37A240G        | 240 GB | 3       | 661   | 0     | 1.81   |
| Micron    | 5100_MTFDDAK1T9TBY | 1.9 TB | 74      | 1138  | 20    | 1.80   |
| Intel     | SSDSC2BW120H6      | 120 GB | 4       | 811   | 3     | 1.80   |
| Intel     | SSDSC2BB480G7R     | 480 GB | 24      | 691   | 1     | 1.80   |
| Kingston  | SUV400S37120G      | 120 GB | 11      | 688   | 3     | 1.80   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 2       | 646   | 0     | 1.77   |
| Intel     | SSDSC2BW180A4      | 180 GB | 2       | 644   | 0     | 1.77   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 33      | 982   | 2     | 1.77   |
| Samsung   | SSD 860 PRO        | 256 GB | 45      | 641   | 0     | 1.76   |
| Samsung   | MZ7LM960HMJP-000MV | 960 GB | 4       | 641   | 0     | 1.76   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 11      | 777   | 2     | 1.73   |
| SuperM... | SSD                | 128 GB | 121     | 649   | 12    | 1.73   |
| Intel     | SSDSC2KB240G7      | 240 GB | 63      | 704   | 8     | 1.73   |
| Intel     | SSDSC2KG960G7      | 960 GB | 44      | 1000  | 4     | 1.73   |
| Micron    | 5200_MTFDDAK1T9TDC | 1.9 TB | 10      | 770   | 2     | 1.73   |
| Apacer    | AS330              | 240 GB | 1       | 627   | 0     | 1.72   |
| SATADOM   | SL 3IE3 V2         | 64 GB  | 3       | 625   | 0     | 1.71   |
| Micron    | 5100_MTFDDAK480TBY | 480 GB | 15      | 808   | 3     | 1.70   |
| Seagate   | XF1230-1A0240      | 240 GB | 10      | 621   | 0     | 1.70   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 32      | 960   | 62    | 1.70   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 1       | 620   | 0     | 1.70   |
| SK hynix  | SC300 2.5 7MM      | 256 GB | 1       | 618   | 0     | 1.69   |
| Intel     | SSDSC2BF120A4H     | 120 GB | 2       | 616   | 0     | 1.69   |
| Micron    | 5200_MTFDDAK3T8TDC | 3.8 TB | 21      | 613   | 0     | 1.68   |
| Toshiba   | THNSN81Q92CSE      | 1.9 TB | 7       | 612   | 0     | 1.68   |
| Micron    | 5100_MTFDDAK480TCC | 480 GB | 18      | 741   | 1     | 1.67   |
| Team      | T253X1960G         | 960 GB | 3       | 605   | 0     | 1.66   |
| WDC       | WDS100T2B0A        | 1 TB   | 7       | 602   | 0     | 1.65   |
| Transcend | TS256GSSD370       | 256 GB | 1       | 596   | 0     | 1.63   |
| SanDisk   | SDLF1CRR-019T-1HA1 | 1.9 TB | 10      | 633   | 1     | 1.62   |
| Seagate   | XF1230-1A0960      | 960 GB | 2       | 590   | 0     | 1.62   |
| Intel     | SSDSC2BA012T4      | 1.2 TB | 1       | 589   | 0     | 1.62   |
| Toshiba   | THNSF8240CCSE      | 240 GB | 10      | 589   | 0     | 1.62   |
| SuperM... | SSD                | 16 GB  | 27      | 588   | 0     | 1.61   |
| Team      | T2535T120G         | 120 GB | 2       | 583   | 0     | 1.60   |
| Phison    | SATA SSD           | 480 GB | 3       | 578   | 0     | 1.59   |
| Kingston  | SV300S37A60G       | 64 GB  | 3       | 1344  | 2     | 1.58   |
| HP        | VK000480GWSRR      | 480 GB | 4       | 572   | 0     | 1.57   |
| Samsung   | SSD 860 PRO        | 2 TB   | 139     | 572   | 0     | 1.57   |
| Samsung   | SSD 860 QVO        | 2 TB   | 25      | 570   | 0     | 1.56   |
| Samsung   | MZ7LM1T9HMJP-00005 | 1.9 TB | 100     | 791   | 9     | 1.56   |
| HP        | VK000240GWSRQ      | 240 GB | 13      | 566   | 0     | 1.55   |
| HPE       | MK000240GWEZF      | 240 GB | 10      | 565   | 0     | 1.55   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 5       | 564   | 0     | 1.55   |
| SK hynix  | SC311 SATA         | 1 TB   | 2       | 563   | 0     | 1.54   |
| Intel     | SSDSC2BB012T7      | 1.2 TB | 172     | 1004  | 3     | 1.54   |
| Samsung   | SSD 860 DCT 1.92TB | 1.9 TB | 16      | 557   | 0     | 1.53   |
| SATADOM   | SL 3SE             | 32 GB  | 3       | 556   | 0     | 1.52   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 21      | 555   | 0     | 1.52   |
| Micron    | 5200_MTFDDAK480TDC | 480 GB | 23      | 569   | 1     | 1.52   |
| Micron    | 5100_MTFDDAK960TCB | 960 GB | 126     | 814   | 2     | 1.52   |
| Seagate   | XA480ME10063       | 480 GB | 10      | 550   | 0     | 1.51   |
| Intel     | SSDSC2BW120A4      | 120 GB | 45      | 705   | 1     | 1.51   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 96      | 549   | 0     | 1.51   |
| Samsung   | MZ7LM1T9HMJP0D3    | 1.9 TB | 2       | 547   | 0     | 1.50   |
| HP        | VK0480GFLKH        | 480 GB | 2       | 547   | 0     | 1.50   |
| Kingston  | SM2280S3G2120G     | 120 GB | 1       | 547   | 0     | 1.50   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 3       | 543   | 0     | 1.49   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 7       | 542   | 0     | 1.49   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 2       | 542   | 0     | 1.49   |
| Micron    | 5200_MTFDDAK480TDN | 480 GB | 16      | 542   | 0     | 1.49   |
| SanDisk   | SDSSDHP256G        | 256 GB | 1       | 541   | 0     | 1.48   |
| Transcend | TSMSSSD01-240GP    | 240 GB | 4       | 540   | 0     | 1.48   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 2       | 538   | 0     | 1.47   |
| Innodisk  | 2.5" SATA SSD 3ME4 | 128 GB | 1       | 1074  | 1     | 1.47   |
| Samsung   | MZ7LH240HAHQ0D3    | 240 GB | 6       | 534   | 0     | 1.46   |
| Samsung   | MZNLN512HMJP-00000 | 512 GB | 11      | 531   | 0     | 1.46   |
| Intel     | SSDSC2KB480G8R     | 480 GB | 12      | 529   | 0     | 1.45   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 22      | 1144  | 4     | 1.43   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 3       | 512   | 0     | 1.40   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 29      | 541   | 1     | 1.40   |
| SanDisk   | SDSSDA480G         | 480 GB | 2       | 509   | 0     | 1.40   |
| HP        | VK0480GFDKH        | 480 GB | 6       | 509   | 0     | 1.40   |
| Samsung   | SSD 845DC PRO      | 800 GB | 4       | 2033  | 3     | 1.39   |
| Intel     | SSDSC2BB800G7      | 800 GB | 1       | 1015  | 1     | 1.39   |
| Crucial   | CT250BX100SSD1     | 250 GB | 1       | 507   | 0     | 1.39   |
| Plextor   | PX-256M6S+         | 256 GB | 2       | 505   | 0     | 1.39   |
| Micron    | 5200_MTFDDAK240TDN | 240 GB | 40      | 505   | 0     | 1.39   |
| HPE       | MK000960GWUGH      | 960 GB | 6       | 565   | 1     | 1.38   |
| Kingston  | SUV400S37240G      | 240 GB | 53      | 516   | 1     | 1.38   |
| Seagate   | ST120FN0021        | 120 GB | 1       | 502   | 0     | 1.38   |
| Samsung   | MZ7LM480HMHQ-00005 | 480 GB | 68      | 1047  | 30    | 1.36   |
| OCZ       | D2RSTK251E14-0400  | 400 GB | 2       | 495   | 0     | 1.36   |
| Intel     | SSDSC2KB960G7      | 960 GB | 159     | 1098  | 12    | 1.35   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 9       | 493   | 0     | 1.35   |
| Samsung   | SSD 860 EVO        | 2 TB   | 86      | 489   | 0     | 1.34   |
| Seagate   | XA1920LE10063      | 1.9 TB | 20      | 488   | 0     | 1.34   |
| Intel     | SSDSC2KB019T7      | 1.9 TB | 39      | 850   | 5     | 1.32   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 25      | 561   | 42    | 1.31   |
| Intel     | SSDSC2BF120A4H SED | 120 GB | 2       | 476   | 0     | 1.31   |
| Samsung   | SSD 860 PRO        | 1 TB   | 88      | 475   | 0     | 1.30   |
| Samsung   | SSD 850            | 120 GB | 2       | 474   | 0     | 1.30   |
| Patriot   | Burst              | 480 GB | 2       | 472   | 0     | 1.30   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 2       | 471   | 0     | 1.29   |
| Intel     | SSDSA2BW120G3      | 120 GB | 1       | 2358  | 4     | 1.29   |
| Intel     | SSDSC2BB960G7      | 960 GB | 17      | 750   | 2     | 1.29   |
| Intel     | SSDSC2KG960G8      | 960 GB | 94      | 538   | 1     | 1.29   |
| Kingston  | SA400S37120G       | 120 GB | 18      | 469   | 0     | 1.29   |
| Intel     | SSDSC2KG240G8      | 240 GB | 143     | 467   | 0     | 1.28   |
| Micron    | 5200_MTFDDAK960TDC | 960 GB | 44      | 477   | 1     | 1.28   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 1       | 465   | 0     | 1.28   |
| Intel     | SSDSC2CW120A3      | 120 GB | 33      | 2092  | 772   | 1.27   |
| Samsung   | MZ7LH480HAHQ0D3    | 480 GB | 2       | 464   | 0     | 1.27   |
| Micron    | MTFDDAK128MBF-1... | 128 GB | 13      | 464   | 0     | 1.27   |
| Kingston  | SUV500960G         | 960 GB | 6       | 464   | 0     | 1.27   |
| OWC       | Mercury Electra... | 250 GB | 2       | 462   | 0     | 1.27   |
| Kingston  | SUV500M8480G       | 480 GB | 1       | 459   | 0     | 1.26   |
| HP        | SSD M700           | 120 GB | 2       | 459   | 0     | 1.26   |
| SK hynix  | SC300 M.2 2280     | 256 GB | 1       | 459   | 0     | 1.26   |
| Samsung   | SSD 860 EVO        | 500 GB | 258     | 460   | 1     | 1.25   |
| SuperM... | SSD                | 32 GB  | 6       | 457   | 0     | 1.25   |
| Kingston  | SA400M8120G        | 120 GB | 3       | 457   | 0     | 1.25   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 4       | 456   | 0     | 1.25   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 16      | 487   | 1     | 1.25   |
| Samsung   | MZ7LM240HMHQ-00005 | 240 GB | 76      | 795   | 127   | 1.24   |
| Micron    | MTFDDAK480TDN      | 480 GB | 38      | 460   | 1     | 1.24   |
| Corsair   | Force LS SSD       | 64 GB  | 2       | 450   | 0     | 1.23   |
| Samsung   | MZ7KM480HMHQ-000MV | 480 GB | 37      | 449   | 0     | 1.23   |
| Intel     | SSDSC2BB480G7O     | 480 GB | 2       | 1493  | 5     | 1.23   |
| HPE       | MR000240GWFLU      | 240 GB | 2       | 447   | 0     | 1.23   |
| Crucial   | CT120BX500SSD1     | 120 GB | 38      | 446   | 0     | 1.22   |
| China     | SATA SSD           | 480 GB | 1       | 442   | 0     | 1.21   |
| Intel     | SSDSC2KG019T7R     | 1.9 TB | 15      | 699   | 3     | 1.21   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 1       | 440   | 0     | 1.21   |
| Goodram   | IR-SSDPR-S25A-120  | 120 GB | 7       | 439   | 0     | 1.21   |
| Micron    | 5200_MTFDDAK1T9TDD | 1.9 TB | 61      | 494   | 1     | 1.20   |
| Seagate   | XA960ME10063       | 960 GB | 2       | 435   | 0     | 1.19   |
| Samsung   | SSD 883 DCT 1.92TB | 1.9 TB | 185     | 435   | 1     | 1.19   |
| Samsung   | MZ7KH240HAHQ-00005 | 240 GB | 48      | 432   | 0     | 1.19   |
| PNY       | CS900 120GB SSD    | 120 GB | 2       | 431   | 0     | 1.18   |
| SanDisk   | SDLFOCAM-800G-1HA1 | 800 GB | 1       | 431   | 0     | 1.18   |
| Samsung   | MZ7LH1T9HMLT-00005 | 1.9 TB | 418     | 428   | 0     | 1.17   |
| WDC       | HBS3A1996A7E6B1    | 960 GB | 2       | 427   | 0     | 1.17   |
| Micron    | 5200_MTFDDAK960TDD | 960 GB | 94      | 446   | 1     | 1.17   |
| Samsung   | MZ7KH960HAJR-00005 | 960 GB | 51      | 426   | 0     | 1.17   |
| Seagate   | XA1920ME10063      | 1.9 TB | 29      | 423   | 0     | 1.16   |
| Intel     | SSDSC2BB800H4      | 800 GB | 6       | 423   | 0     | 1.16   |
| Intel     | SSDSC2KB240G8      | 240 GB | 605     | 439   | 2     | 1.16   |
| Samsung   | MZ7LH960HAJR-000AZ | 960 GB | 4       | 422   | 0     | 1.16   |
| HPE       | MK0400GEYKD        | 400 GB | 1       | 421   | 0     | 1.15   |
| Intel     | SSDSC2KB480G7      | 480 GB | 38      | 511   | 1     | 1.15   |
| PNY       | CS900 240GB SSD    | 240 GB | 1       | 418   | 0     | 1.15   |
| Kingston  | SEDC500R960G       | 960 GB | 1       | 418   | 0     | 1.15   |
| OCZ       | TRION100           | 120 GB | 1       | 417   | 0     | 1.14   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 1       | 416   | 0     | 1.14   |
| Samsung   | SSD 860 QVO        | 1 TB   | 42      | 411   | 0     | 1.13   |
| Gigabyte  | GP-GSTFS30512GTTD  | 512 GB | 2       | 410   | 0     | 1.13   |
| WDC       | WDS200T2B0A        | 2 TB   | 9       | 408   | 0     | 1.12   |
| Samsung   | SSD 883 DCT        | 480 GB | 2       | 407   | 0     | 1.12   |
| Goodram   | SSDPR-CX400-512    | 512 GB | 3       | 406   | 0     | 1.11   |
| Samsung   | SSD 883 DCT        | 960 GB | 14      | 406   | 0     | 1.11   |
| Samsung   | MZ7KH480HAHQ-00005 | 480 GB | 41      | 404   | 0     | 1.11   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 1       | 402   | 0     | 1.10   |
| Micron    | 5200_MTFDDAK960TDN | 960 GB | 2       | 401   | 0     | 1.10   |
| HP        | VK000480GWCNQ      | 480 GB | 1       | 399   | 0     | 1.09   |
| Micron    | 5200_MTFDDAK1T9TDN | 1.9 TB | 19      | 448   | 1     | 1.09   |
| Corsair   | Neutron SSD        | 128 GB | 1       | 1955  | 4     | 1.07   |
| Kingston  | SA400S37480G       | 480 GB | 28      | 615   | 14    | 1.06   |
| Samsung   | MZ7LH960HAJR0D3    | 960 GB | 16      | 385   | 0     | 1.06   |
| Toshiba   | THNSF8400CCSE      | 400 GB | 12      | 384   | 0     | 1.05   |
| Micron    | M500DC_MTFDDAK8... | 800 GB | 7       | 383   | 0     | 1.05   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 1       | 383   | 0     | 1.05   |
| HP        | SSD S700           | 500 GB | 7       | 437   | 1     | 1.04   |
| Micron    | 5100_MTFDDAV240TCB | 240 GB | 9       | 505   | 8     | 1.04   |
| Zheino    | CHN 25SATAS3 512   | 512 GB | 1       | 379   | 0     | 1.04   |
| SPCC      | SSD                | 1 TB   | 1       | 378   | 0     | 1.04   |
| Intel     | SSDSC2BW240A4      | 240 GB | 38      | 688   | 6     | 1.04   |
| Intel     | SSDSC2KB480G8      | 480 GB | 236     | 390   | 1     | 1.04   |
| Samsung   | SSD 860 EVO        | 1 TB   | 296     | 375   | 0     | 1.03   |
| SK hynix  | HFS250G32TND-N1A2A | 250 GB | 10      | 374   | 0     | 1.03   |
| Intel     | SSDSC2BW240H6      | 240 GB | 14      | 595   | 25    | 1.02   |
| Intel     | SSDSC2BW480H6      | 480 GB | 5       | 639   | 4     | 1.02   |
| Patriot   | P200               | 2 TB   | 5       | 371   | 0     | 1.02   |
| Crucial   | CT1000BX100SSD1    | 1 TB   | 1       | 370   | 0     | 1.02   |
| Samsung   | SSD 860 PRO        | 512 GB | 21      | 367   | 0     | 1.01   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 105     | 438   | 4     | 1.00   |
| Kingston  | SEDC500M960G       | 960 GB | 11      | 373   | 1     | 1.00   |
| KingDian  | S280               | 240 GB | 3       | 433   | 1     | 1.00   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 208     | 467   | 10    | 1.00   |
| Plextor   | PX-128S3C          | 128 GB | 1       | 363   | 0     | 1.00   |
| Samsung   | MZ7WD480HMHP-00003 | 480 GB | 6       | 1929  | 86    | 0.99   |
| Intel     | SSDSC2KB960G8      | 960 GB | 765     | 412   | 1     | 0.99   |
| Intel     | SSDSC2KG240G8R     | 240 GB | 1       | 361   | 0     | 0.99   |
| HP        | SSD S700           | 250 GB | 6       | 358   | 0     | 0.98   |
| ORTIAL    | SSD                | 1 TB   | 12      | 432   | 1     | 0.98   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 1       | 354   | 0     | 0.97   |
| Micron    | 5100_MTFDDAK1T9TCB | 1.9 TB | 3       | 1176  | 694   | 0.97   |
| SanDisk   | SSD PLUS           | 480 GB | 23      | 533   | 6     | 0.96   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 4       | 350   | 0     | 0.96   |
| Apacer    | AS340              | 480 GB | 1       | 348   | 0     | 0.96   |
| WDC       | WDS400T2B0A-00SM50 | 4 TB   | 4       | 394   | 1     | 0.95   |
| Intel     | SSDSCKKB240G8      | 240 GB | 17      | 345   | 0     | 0.95   |
| Samsung   | SSD 860 QVO        | 4 TB   | 6       | 342   | 0     | 0.94   |
| Micron    | 5300_MTFDDAK480TDS | 480 GB | 4       | 342   | 0     | 0.94   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 6       | 471   | 9     | 0.94   |
| Kingston  | SVP200S3120G       | 120 GB | 1       | 341   | 0     | 0.94   |
| HPE       | MK001920GWUGK      | 1.9 TB | 2       | 341   | 0     | 0.93   |
| ADATA     | SP550              | 120 GB | 1       | 337   | 0     | 0.93   |
| Samsung   | MZ7KH1T9HAJR-00005 | 1.9 TB | 97      | 340   | 1     | 0.92   |
| BIWIN     | SSD                | 256 GB | 1       | 332   | 0     | 0.91   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 33      | 337   | 1     | 0.91   |
| Seagate   | XA480LE10063       | 480 GB | 11      | 329   | 0     | 0.90   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 1       | 328   | 0     | 0.90   |
| Samsung   | SSD 860 EVO        | 250 GB | 105     | 327   | 0     | 0.90   |
| Intel     | SSDSC2KB480G7R     | 480 GB | 6       | 318   | 0     | 0.87   |
| SanDisk   | SDSSDA120G         | 120 GB | 3       | 317   | 0     | 0.87   |
| Micron    | 5300_MTFDDAK960TDS | 960 GB | 123     | 324   | 1     | 0.87   |
| ADATA     | SP580              | 120 GB | 2       | 990   | 505   | 0.86   |
| SanDisk   | pSSD               | 32 GB  | 1       | 314   | 0     | 0.86   |
| Mushkin   | MKNSSDRE960GB      | 960 GB | 5       | 509   | 2     | 0.85   |
| Intel     | SSDSC2KG019T8      | 1.9 TB | 167     | 348   | 1     | 0.83   |
| Micron    | MTFDDAV240TCB      | 240 GB | 13      | 312   | 1     | 0.83   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 20      | 328   | 1     | 0.82   |
| China     | 512GB QLC SATA SSD | 512 GB | 6       | 298   | 0     | 0.82   |
| Kingston  | SQ500S37480G       | 480 GB | 1       | 297   | 0     | 0.81   |
| Seagate   | XA240ME10003       | 240 GB | 2       | 296   | 0     | 0.81   |
| Intel     | SSDSC2KG480G8      | 480 GB | 218     | 325   | 1     | 0.81   |
| Micron    | 1300_MTFDDAK1T0TDL | 1 TB   | 9       | 315   | 1     | 0.79   |
| Lite-On   | L8H-128V2G-HP      | 128 GB | 2       | 286   | 0     | 0.79   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 3       | 285   | 0     | 0.78   |
| KingSpec  | MT-128             | 128 GB | 1       | 281   | 0     | 0.77   |
| China     | SH00R480GB         | 480 GB | 2       | 510   | 4     | 0.77   |
| Crucial   | CT240M500SSD1      | 240 GB | 11      | 1956  | 258   | 0.77   |
| HP        | VK001920GWSXK      | 1.9 TB | 35      | 279   | 0     | 0.77   |
| HPE       | MK000480GWXFF      | 480 GB | 9       | 279   | 0     | 0.76   |
| Samsung   | MZ7LH960HAJR-00005 | 960 GB | 710     | 278   | 0     | 0.76   |
| SanDisk   | SSD PLUS           | 240 GB | 17      | 285   | 1     | 0.76   |
| Samsung   | MZ7LH480HAHQ-00005 | 480 GB | 42      | 270   | 0     | 0.74   |
| Patriot   | Burst              | 240 GB | 10      | 270   | 0     | 0.74   |
| Micron    | 5210_MTFDDAK1T9QDE | 1.9 TB | 4       | 269   | 0     | 0.74   |
| Intel     | SSDSC2BW256H6      | 256 GB | 1       | 268   | 0     | 0.74   |
| Samsung   | MZ7LM240HMHQ-00003 | 240 GB | 2       | 266   | 0     | 0.73   |
| Intel     | SSDSC2BW080A4      | 80 GB  | 1       | 1589  | 5     | 0.73   |
| Samsung   | MZ7KH480HAHQ0D3    | 480 GB | 17      | 263   | 0     | 0.72   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 8       | 262   | 0     | 0.72   |
| Toshiba   | THNSF8200CAME      | 200 GB | 3       | 261   | 0     | 0.72   |
| Micron    | M510DC_MTFDDAK9... | 960 GB | 1       | 1813  | 6     | 0.71   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 271     | 257   | 0     | 0.71   |
| SanDisk   | SSD PLUS           | 120 GB | 16      | 273   | 1     | 0.70   |
| SPCC      | SSD                | 512 GB | 6       | 253   | 0     | 0.69   |
| Toshiba   | THNSF81D60CSE      | 1.6 TB | 10      | 253   | 0     | 0.69   |
| Intel     | SSDSC2KB019T7R     | 1.9 TB | 20      | 326   | 2     | 0.69   |
| Samsung   | SSD 883 DCT 3.84TB | 3.8 TB | 102     | 253   | 0     | 0.69   |
| WDC       | WDS100T1R0A-68A4W0 | 1 TB   | 1       | 253   | 0     | 0.69   |
| Seagate   | XA960LE10063       | 960 GB | 83      | 252   | 0     | 0.69   |
| Micron    | 5100_MTFDDAK1T9TCC | 1.9 TB | 17      | 270   | 1     | 0.68   |
| Micron    | 5100_MTFDDAK480TCB | 480 GB | 18      | 745   | 99    | 0.68   |
| Crucial   | CT500MX500SSD1     | 500 GB | 97      | 302   | 3     | 0.68   |
| ADATA     | SP550              | 240 GB | 2       | 247   | 0     | 0.68   |
| Micron    | MTFDDAK960TCB      | 960 GB | 8       | 308   | 1     | 0.67   |
| Micron    | 5300_MTFDDAK1T9TDT | 1.9 TB | 94      | 255   | 1     | 0.67   |
| Micron    | MTFDDAV480TDS-1... | 480 GB | 1       | 243   | 0     | 0.67   |
| Kingston  | SHFS37A240G        | 240 GB | 1       | 242   | 0     | 0.66   |
| China     | SATA SSD           | 240 GB | 3       | 240   | 0     | 0.66   |
| KingSpec  | P4-960             | 960 GB | 2       | 239   | 0     | 0.66   |
| Samsung   | MZ7LH480HAHQ-000V3 | 480 GB | 5       | 239   | 0     | 0.66   |
| Gigabyte  | GP-GSTFS31480GNTD  | 480 GB | 1       | 238   | 0     | 0.65   |
| Kingston  | SEDC500R1920G      | 1.9 TB | 45      | 333   | 1     | 0.65   |
| HPE       | MK001920GWJPQ      | 1.9 TB | 18      | 425   | 6     | 0.64   |
| Micron    | 5300_MTFDDAK7T6TDS | 7.6 TB | 11      | 230   | 0     | 0.63   |
| HPE       | VR000240GXBBL      | 240 GB | 2       | 230   | 0     | 0.63   |
| Samsung   | MZ7WD960HMHP-00003 | 960 GB | 4       | 2013  | 41    | 0.63   |
| Transcend | TS480GSSD220S      | 480 GB | 4       | 320   | 2     | 0.63   |
| SanDisk   | SSD G5 BICS4       | 1 TB   | 5       | 252   | 1     | 0.63   |
| Transcend | TSMSSSD01-120GP    | 120 GB | 2       | 227   | 0     | 0.62   |
| Crucial   | CT240BX500SSD1     | 240 GB | 27      | 226   | 0     | 0.62   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 120     | 262   | 4     | 0.62   |
| Samsung   | SSD 883 DCT        | 240 GB | 25      | 225   | 0     | 0.62   |
| Micron    | 5100_MTFDDAK960TCC | 960 GB | 6       | 324   | 1     | 0.61   |
| Crucial   | CT960BX500SSD1     | 960 GB | 8       | 222   | 0     | 0.61   |
| Samsung   | MZ7LH7T6HMLA-00005 | 7.6 TB | 112     | 221   | 0     | 0.61   |
| SanDisk   | SDSA5GK-016G-1006  | 16 GB  | 1       | 219   | 0     | 0.60   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 1       | 219   | 0     | 0.60   |
| Kingston  | SEDC500M480G       | 480 GB | 6       | 217   | 0     | 0.60   |
| Micron    | 5300_MTFDDAK3T8TDS | 3.8 TB | 25      | 273   | 2     | 0.59   |
| Kingston  | SA400S37240G       | 240 GB | 49      | 214   | 0     | 0.59   |
| Patriot   | Burst              | 960 GB | 1       | 212   | 0     | 0.58   |
| Micron    | MTFDDAK480TDS-1... | 480 GB | 9       | 240   | 42    | 0.58   |
| Crucial   | CT120BX100SSD1     | 120 GB | 1       | 209   | 0     | 0.57   |
| Crucial   | CT1000BX500SSD1    | 1 TB   | 11      | 235   | 2     | 0.57   |
| Kingston  | SA400S37960G       | 960 GB | 5       | 207   | 0     | 0.57   |
| Crucial   | CT250MX500SSD1     | 250 GB | 58      | 222   | 1     | 0.55   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 1       | 2595  | 12    | 0.55   |
| Transcend | TS128GSSD370       | 128 GB | 2       | 198   | 0     | 0.54   |
| Intel     | SSDSC2KW128G8      | 128 GB | 9       | 211   | 2     | 0.54   |
| THU       | SSD 240G           | 240 GB | 1       | 197   | 0     | 0.54   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 1       | 786   | 3     | 0.54   |
| Samsung   | MZ7KM120HAFD-000FU | 120 GB | 1       | 195   | 0     | 0.54   |
| Dell      | SSDSCKKB240G8R     | 240 GB | 11      | 194   | 0     | 0.53   |
| Phison    | SATA SSD           | 64 GB  | 8       | 194   | 0     | 0.53   |
| Apacer    | AS340              | 960 GB | 42      | 306   | 21    | 0.53   |
| Samsung   | MZ7LH1T9HALT0D3    | 1.9 TB | 35      | 193   | 0     | 0.53   |
| HPE       | MK000960GXAXB      | 960 GB | 5       | 190   | 0     | 0.52   |
| HP        | VK000480GWTTA      | 480 GB | 6       | 188   | 0     | 0.52   |
| Crucial   | CT960BX200SSD1     | 960 GB | 1       | 181   | 0     | 0.50   |
| Toshiba   | KHK61RSE960G       | 960 GB | 62      | 179   | 0     | 0.49   |
| ADATA     | SU630              | 960 GB | 1       | 527   | 2     | 0.48   |
| Intel     | SSDSCKKI256G8      | 256 GB | 1       | 173   | 0     | 0.47   |
| HP        | VK000960GWTHB      | 960 GB | 3       | 172   | 0     | 0.47   |
| ADATA     | SU800              | 256 GB | 1       | 172   | 0     | 0.47   |
| SPCC      | SSD                | 480 GB | 2       | 168   | 0     | 0.46   |
| Samsung   | MZ7LM960HCHP-000MV | 960 GB | 6       | 168   | 0     | 0.46   |
| SK hynix  | SHGS31-1000GS-2    | 1 TB   | 12      | 162   | 0     | 0.45   |
| Micron    | 1100 SATA          | 256 GB | 1       | 162   | 0     | 0.45   |
| Intel     | SSDSC2KB960G8R     | 960 GB | 7       | 161   | 0     | 0.44   |
| SanDisk   | SDSSDH3 2T00       | 2 TB   | 6       | 161   | 0     | 0.44   |
| Phison    | SATA SSD           | 32 GB  | 1       | 161   | 0     | 0.44   |
| Kingston  | SEDC500M1920G      | 1.9 TB | 30      | 173   | 1     | 0.44   |
| Samsung   | SSD 750 EVO        | 500 GB | 1       | 157   | 0     | 0.43   |
| Intenso   | SSD                | 128 GB | 2       | 156   | 0     | 0.43   |
| Samsung   | MZ7LH3T8HMLT-00005 | 3.8 TB | 49      | 155   | 0     | 0.42   |
| HP        | VK000960GWTTB      | 960 GB | 10      | 154   | 0     | 0.42   |
| Micron    | 1100_MTFDDAK1T0TBN | 1 TB   | 3       | 1395  | 291   | 0.42   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 244     | 181   | 4     | 0.41   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 1       | 147   | 0     | 0.40   |
| PNY       | CS900 250GB SSD    | 250 GB | 4       | 147   | 0     | 0.40   |
| SPCC      | SSD                | 256 GB | 3       | 146   | 0     | 0.40   |
| ADATA     | SU800              | 2 TB   | 4       | 250   | 1     | 0.40   |
| Samsung   | MZ7KH960HAJR0D3    | 960 GB | 160     | 142   | 0     | 0.39   |
| Apacer    | 480GB SATA Flas... | 480 GB | 3       | 140   | 0     | 0.38   |
| Micron    | MTFDDAK480TDS      | 480 GB | 8       | 138   | 0     | 0.38   |
| Micron    | 1300_MTFDDAK512TDL | 512 GB | 116     | 138   | 0     | 0.38   |
| HP        | VK0480GEPQP        | 480 GB | 4       | 135   | 0     | 0.37   |
| Crucial   | CT240BX200SSD1     | 240 GB | 1       | 133   | 0     | 0.37   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 9       | 130   | 0     | 0.36   |
| ADATA     | SU750              | 512 GB | 4       | 129   | 0     | 0.35   |
| Intel     | SSDSC2KG038T8      | 3.8 TB | 6       | 162   | 1     | 0.34   |
| Intel     | SSDSC2KG960G8R     | 960 GB | 12      | 177   | 2     | 0.34   |
| Intel     | SSDSC2BF180A4      | 180 GB | 2       | 204   | 2     | 0.34   |
| Phison    | SATA SSD           | 960 GB | 4       | 123   | 0     | 0.34   |
| WDC       | WDS250G2B0A        | 250 GB | 2       | 118   | 0     | 0.33   |
| Micron    | 5300_MTFDDAK480TDT | 480 GB | 4       | 117   | 0     | 0.32   |
| Toshiba   | KHK61RSE1T92       | 1.9 TB | 3       | 116   | 0     | 0.32   |
| Kingston  | SEDC500R3840G      | 3.8 TB | 35      | 151   | 1     | 0.32   |
| ADATA     | SU650              | 120 GB | 4       | 116   | 0     | 0.32   |
| Micron    | MTFDDAK960TDS      | 960 GB | 6       | 115   | 0     | 0.32   |
| Intel     | SSDSC2KW256G8      | 256 GB | 23      | 115   | 0     | 0.32   |
| Intel     | SSDSC2BW120A3F     | 120 GB | 20      | 2070  | 968   | 0.31   |
| Intel     | SSDSC2BF240A4H     | 240 GB | 1       | 568   | 4     | 0.31   |
| Maxtor    | Z1 SSD             | 960 GB | 2       | 110   | 0     | 0.30   |
| Intel     | SSDSC2KB038T8      | 3.8 TB | 24      | 130   | 1     | 0.30   |
| Kingston  | SUV500M8240G       | 240 GB | 3       | 108   | 0     | 0.30   |
| Micron    | 5300_MTFDDAV240TDS | 240 GB | 6       | 107   | 0     | 0.30   |
| Crucial   | CT480BX500SSD1     | 480 GB | 20      | 106   | 0     | 0.29   |
| Crucial   | CT1024M550SSD1     | 1 TB   | 4       | 2340  | 231   | 0.29   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 1       | 2695  | 26    | 0.27   |
| Micron    | M500_MTFDDAK960MAV | 960 GB | 1       | 1991  | 19    | 0.27   |
| Micron    | 5300_MTFDDAK960TDT | 960 GB | 19      | 99    | 0     | 0.27   |
| Kingston  | SEDC500R480G       | 480 GB | 3       | 97    | 0     | 0.27   |
| SK hynix  | SC311 SATA         | 256 GB | 1       | 97    | 0     | 0.27   |
| Micron    | 5210_MTFDDAK3T8QDE | 3.8 TB | 37      | 101   | 1     | 0.26   |
| Patriot   | Burst              | 120 GB | 1       | 96    | 0     | 0.26   |
| Samsung   | SSD 870 QVO        | 8 TB   | 30      | 95    | 0     | 0.26   |
| Samsung   | SSD 860 EVO        | 4 TB   | 4       | 93    | 0     | 0.25   |
| WDC       | WDS200T1R0A-68A4W0 | 2 TB   | 15      | 91    | 0     | 0.25   |
| Intel     | SSDSC2KW512G8      | 512 GB | 4       | 131   | 4     | 0.25   |
| Samsung   | MZ7KH3T8HALS-00005 | 3.8 TB | 2       | 88    | 0     | 0.24   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 1       | 261   | 2     | 0.24   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 1       | 84    | 0     | 0.23   |
| Micron    | MTFDDAV256TDL      | 256 GB | 5       | 143   | 2     | 0.23   |
| SanDisk   | SDSSDH3512G        | 512 GB | 2       | 82    | 0     | 0.23   |
| Crucial   | CT250MX500SSD4     | 250 GB | 2       | 81    | 0     | 0.22   |
| Kingston  | SKC6001024G        | 1 TB   | 2       | 77    | 0     | 0.21   |
| ADATA     | SU800              | 1 TB   | 2       | 74    | 0     | 0.21   |
| Transcend | TS1TSSD370S        | 1 TB   | 1       | 296   | 3     | 0.20   |
| Intel     | SSDSC2BF240A4L     | 240 GB | 1       | 651   | 8     | 0.20   |
| Micron    | 5300_MTFDDAK3T8TDT | 3.8 TB | 9       | 71    | 0     | 0.20   |
| Smartbuy  | SSD                | 960 GB | 1       | 70    | 0     | 0.19   |
| HPE       | MK000480GWUGF      | 480 GB | 2       | 69    | 0     | 0.19   |
| Micron    | MTFDDAK1T0TDL      | 1 TB   | 20      | 70    | 1     | 0.19   |
| ADATA     | SU800              | 512 GB | 1       | 342   | 4     | 0.19   |
| Micron    | 5300_MTFDDAK1T9TDS | 1.9 TB | 34      | 67    | 0     | 0.19   |
| Transcend | TS128GSSD370S      | 128 GB | 6       | 65    | 0     | 0.18   |
| SanDisk   | SD7UB3Q256G1122    | 256 GB | 1       | 700   | 10    | 0.17   |
| Intel     | SSDSCKKW128G8      | 128 GB | 3       | 62    | 0     | 0.17   |
| SanDisk   | SSD PLUS           | 1 TB   | 1       | 124   | 1     | 0.17   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 1       | 57    | 0     | 0.16   |
| Seagate   | BarraCuda 120 S... | 500 GB | 2       | 56    | 0     | 0.16   |
| Micron    | MTFDDAK960TDT      | 960 GB | 8       | 55    | 0     | 0.15   |
| Micron    | MTFDDAV240TDU      | 240 GB | 6       | 55    | 0     | 0.15   |
| Samsung   | MZ7LH480HBHQ0D3    | 480 GB | 9       | 54    | 0     | 0.15   |
| Crucial   | CT120M500SSD1      | 120 GB | 2       | 2010  | 523   | 0.14   |
| SPCC      | SSD                | 128 GB | 1       | 50    | 0     | 0.14   |
| HPE       | VR000480GWFMD      | 480 GB | 1       | 49    | 0     | 0.14   |
| SATADOM   | ML 3MG2-P          | 248 GB | 1       | 47    | 0     | 0.13   |
| Maxtor    | Z1 SSD             | 240 GB | 1       | 44    | 0     | 0.12   |
| Samsung   | SSD 870 EVO        | 500 GB | 1       | 40    | 0     | 0.11   |
| China     | SATA SSD           | 120 GB | 3       | 40    | 0     | 0.11   |
| QUMO      | SSD                | 64 GB  | 2       | 47    | 608   | 0.10   |
| Kingston  | SKC6002048G        | 2 TB   | 1       | 37    | 0     | 0.10   |
| KingFast  | SSD                | 512 GB | 1       | 447   | 11    | 0.10   |
| Crucial   | CT512M550SSD1      | 512 GB | 2       | 592   | 16    | 0.10   |
| China     | OSSD120GBTSS2      | 120 GB | 1       | 624   | 18    | 0.09   |
| Intel     | SSDSC2BW480A4      | 480 GB | 3       | 514   | 24    | 0.09   |
| Transcend | TS1TSSD230S        | 1 TB   | 1       | 28    | 0     | 0.08   |
| HPE       | LK1600GEYMV        | 1.6 TB | 1       | 28    | 0     | 0.08   |
| Intel     | SSDSC2KI128G8      | 128 GB | 1       | 56    | 1     | 0.08   |
| Kingston  | SKC300S37A480G     | 480 GB | 1       | 27    | 0     | 0.08   |
| Kingston  | SEDC450R480G       | 480 GB | 1       | 24    | 0     | 0.07   |
| WDC       | WDS400T1R0A-68A4W0 | 4 TB   | 3       | 20    | 0     | 0.06   |
| Transcend | TS128GMTS800S      | 128 GB | 5       | 18    | 0     | 0.05   |
| Team      | T253X1480G         | 480 GB | 1       | 18    | 0     | 0.05   |
| Transcend | TS256GMTS800S      | 256 GB | 5       | 18    | 0     | 0.05   |
| V-GeN     | V-GEN12SM20AR10... | 1 TB   | 1       | 16    | 0     | 0.04   |
| HP        | VK000240GWEZB      | 240 GB | 8       | 15    | 0     | 0.04   |
| WDC       | WDS250G2B0B        | 250 GB | 2       | 14    | 0     | 0.04   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 1       | 14    | 0     | 0.04   |
| Kingston  | SKC600256G         | 256 GB | 1       | 13    | 0     | 0.04   |
| Crucial   | CT2000BX500SSD1    | 2 TB   | 2       | 12    | 0     | 0.03   |
| SATADOM   | SV 3ME3            | 64 GB  | 4       | 10    | 0     | 0.03   |
| Samsung   | MZNLH1T0HALB-00000 | 1 TB   | 8       | 10    | 0     | 0.03   |
| Intel     | SSDSC2KW240H6      | 240 GB | 1       | 190   | 19    | 0.03   |
| Micron    | 5300_MTFDDAK240TDT | 240 GB | 7       | 7     | 0     | 0.02   |
| Samsung   | SSD 870 QVO        | 1 TB   | 3       | 7     | 0     | 0.02   |
| Palit     | PH120 SSD          | 120 GB | 2       | 6     | 0     | 0.02   |
| Samsung   | SSD 870 EVO        | 4 TB   | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSC2KW120H6      | 120 GB | 1       | 6     | 0     | 0.02   |
| HP        | VK000480GWSXF      | 480 GB | 1       | 5     | 0     | 0.01   |
| Intel     | SSDSC2KF256H6 SATA | 256 GB | 1       | 169   | 42    | 0.01   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 4       | 3     | 0     | 0.01   |
| Lite-On   | CV1-8B128-HP       | 128 GB | 1       | 3     | 0     | 0.01   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 1       | 2994  | 1011  | 0.01   |
| Kingston  | SHPM2280P2H-480G   | 480 GB | 3       | 1138  | 743   | 0.01   |
| Intel     | SSDSC2BG200G4R     | 200 GB | 7       | 2153  | 1029  | 0.01   |
| Avant     | 120GB Client mSATA | 120 GB | 2       | 2045  | 1018  | 0.01   |
| ADATA     | SX900              | 512 GB | 2       | 2028  | 1019  | 0.01   |
| Transcend | TS2TSSD230S        | 2 TB   | 3       | 1     | 0     | 0.01   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 1       | 1920  | 1020  | 0.01   |
| Intel     | SSDSC2BX016T4R     | 1.6 TB | 32      | 1929  | 1029  | 0.01   |
| Intel     | SSDSC2BA200G3T     | 200 GB | 2       | 1883  | 1028  | 0.01   |
| Intel     | SSDSC2BB300G4T     | 304 GB | 2       | 1779  | 1028  | 0.00   |
| Intel     | SSDSC2BA200G3R     | 200 GB | 5       | 1729  | 1028  | 0.00   |
| Intel     | SSDSC2BW120A3      | 120 GB | 1       | 1687  | 1019  | 0.00   |
| Intel     | SSDSC2BX200G4R     | 200 GB | 21      | 1578  | 1028  | 0.00   |
| Intel     | SSDSC2BX400G4R     | 400 GB | 48      | 1421  | 1028  | 0.00   |
| Samsung   | MZ7GE240HMGR-00003 | 240 GB | 2       | 222   | 178   | 0.00   |
| Intel     | SSDSC1BG200G4R     | 200 GB | 33      | 1382  | 1028  | 0.00   |
| Micron    | MTFDDAK3T8TDS-1... | 3.8 TB | 2       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BB480G6R     | 480 GB | 1       | 1306  | 1028  | 0.00   |
| Kingston  | SHPM2280P2H-240G   | 240 GB | 1       | 1297  | 1022  | 0.00   |
| Intel     | SSDSC2BA100G3T     | 100 GB | 3       | 1191  | 1028  | 0.00   |
| Intel     | SSDSC2BA800G4R     | 800 GB | 71      | 1140  | 1028  | 0.00   |
| Crucial   | CT128MX100SSD1     | 128 GB | 1       | 1045  | 1061  | 0.00   |
| Intel     | SSDSC2BA200G4R     | 200 GB | 9       | 847   | 1027  | 0.00   |
| Intel     | SSDSC2BB800G4T     | 800 GB | 1       | 807   | 1027  | 0.00   |
| Intel     | SSDSC2KG960G8T     | 960 GB | 1       | 673   | 1026  | 0.00   |
| Intel     | SSDSC2BX800G4R     | 800 GB | 4       | 357   | 1027  | 0.00   |
| SanDisk   | SD8SBAT256G1122    | 256 GB | 2       | 297   | 921   | 0.00   |
| Intel     | SSDSC2KW480H6      | 480 GB | 1       | 115   | 393   | 0.00   |
| INDMEM    | SSD M.2 2260       | 128 GB | 1       | 0     | 0     | 0.00   |

SSD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF   |
|-----------|------------------------|--------|---------|-------|-------|--------|
| Kingston  | JMicron based SSDs     | 1      | 1       | 3150  | 0     | 8.63   |
| Intel     | X25-E SSDs             | 1      | 3       | 2924  | 0     | 8.01   |
| OCZ       | Indilinx Barefoot_2... | 1      | 1       | 2437  | 0     | 6.68   |
| Apple     | SD/SM/TS E/F/G SSDs    | 1      | 2       | 2325  | 0     | 6.37   |
| Micron    | RealSSD m4/C400/P400   | 4      | 11      | 2130  | 0     | 5.84   |
| Intel     | 320 Series SSDs        | 4      | 43      | 2715  | 50    | 5.78   |
| Transcend | JMicron/Maxiotek ba... | 1      | 1       | 2033  | 0     | 5.57   |
| OCZ       | SandForce Driven SSDs  | 4      | 8       | 2538  | 1     | 5.15   |
| ADATA     | JMicron/Maxiotek ba... | 1      | 1       | 1849  | 0     | 5.07   |
| Plextor   | M3/M5/M6 Series SSDs   | 1      | 1       | 1838  | 0     | 5.04   |
| Intel     | 710 Series SSDs        | 1      | 2       | 2332  | 1     | 4.78   |
| Intel     | 330/335 Series SSDs    | 3      | 19      | 2543  | 2     | 4.54   |
| Corsair   | SandForce Driven SSDs  | 2      | 5       | 1489  | 0     | 4.08   |
| ADATA     | SandForce Driven SSDs  | 1      | 2       | 2224  | 2     | 3.66   |
| Intel     | 520 Series SSDs        | 9      | 138     | 2081  | 340   | 3.58   |
| Toshiba   | OCZ                    | 1      | 6       | 1304  | 0     | 3.57   |
| Kingston  | SandForce Driven SSDs  | 18     | 189     | 1498  | 9     | 3.42   |
| SanDisk   | SanDisk based SSDs     | 5      | 16      | 1416  | 2     | 3.36   |
| OCZ       | OCZ/Toshiba Trion SSDs | 2      | 2       | 1125  | 0     | 3.08   |
| Intel     | 730 and DC S35x0/36... | 46     | 854     | 1378  | 204   | 2.93   |
| Toshiba   | HG6 Series SSD         | 1      | 1       | 1036  | 0     | 2.84   |
| SanDisk   | SATA Cloudspeed Max... | 5      | 54      | 1047  | 19    | 2.83   |
| OCZ       | Indilinx Barefoot 3... | 3      | 7       | 1300  | 12    | 2.81   |
| Intel     | Dell Certified Inte... | 3      | 78      | 1167  | 27    | 2.77   |
| OWC       | Unknown                | 1      | 1       | 2002  | 1     | 2.74   |
| Goodram   | Phison Driven OEM SSDs | 1      | 4       | 962   | 0     | 2.64   |
| Intel     | 3710 Series SSDs       | 1      | 5       | 945   | 0     | 2.59   |
| MyDigi... | Unknown                | 1      | 6       | 945   | 0     | 2.59   |
| Crucial   | BX/MX1/2/3/500, M5/... | 11     | 91      | 1346  | 36    | 2.56   |
| Toshiba   | HK4R Series SSD        | 4      | 41      | 913   | 1     | 2.46   |
| SATADOM   | Unknown                | 3      | 5       | 882   | 0     | 2.42   |
| Dell      | Certified Intel S35... | 1      | 5       | 1043  | 1     | 2.40   |
| Intel     | 510 Series SSDs        | 1      | 2       | 842   | 0     | 2.31   |
| XPG       | Unknown                | 1      | 2       | 806   | 0     | 2.21   |
| Intel     | 525 Series SSDs        | 1      | 1       | 788   | 0     | 2.16   |
| Lite-On   | Unknown                | 4      | 6       | 780   | 0     | 2.14   |
| Crucial   | MX1/2/300, M5/600, ... | 1      | 4       | 1471  | 503   | 2.10   |
| WDC       | Blue and Green SSDs    | 9      | 51      | 731   | 0     | 2.00   |
| Toshiba   | Unknown                | 12     | 170     | 705   | 1     | 1.89   |
| Seagate   | Nytro XF1230 SATA SSD  | 3      | 24      | 682   | 0     | 1.87   |
| HP        | Unknown                | 27     | 164     | 709   | 1     | 1.87   |
| SuperM... | Silicon Motion base... | 4      | 181     | 664   | 8     | 1.78   |
| Samsung   | Samsung based SSDs     | 127    | 5387    | 676   | 8     | 1.69   |
| HPE       | Unknown                | 17     | 84      | 659   | 2     | 1.68   |
| Crucial   | BX/MX1/2/3/500, M5/... | 9      | 250     | 827   | 13    | 1.68   |
| Intel     | S3520 Series SSDs      | 5      | 266     | 1069  | 3     | 1.67   |
| Crucial   | Silicon Motion base... | 5      | 6       | 600   | 0     | 1.65   |
| SanDisk   | Marvell based SanDi... | 16     | 123     | 645   | 2     | 1.62   |
| Kingston  | SSDNow UV400/500       | 2      | 10      | 589   | 0     | 1.62   |
| Micron    | BX/MX1/2/3/500, M5/... | 7      | 71      | 808   | 55    | 1.51   |
| Goodram   | Unknown                | 1      | 2       | 538   | 0     | 1.47   |
| Innodisk  | 3IE3/3ME3/3ME4 SSDs    | 1      | 1       | 1074  | 1     | 1.47   |
| Kingston  | SSDNow UV400           | 2      | 64      | 545   | 1     | 1.45   |
| Plextor   | M3/M5/M6/M7 Series ... | 1      | 2       | 505   | 0     | 1.39   |
| Team      | Unknown                | 3      | 6       | 500   | 0     | 1.37   |
| Apacer    | Unknown                | 3      | 5       | 498   | 0     | 1.37   |
| Micron    | 5100 Pro / 5200 SSDs   | 18     | 513     | 609   | 9     | 1.35   |
| SK hynix  | SATA SSDs              | 7      | 18      | 484   | 0     | 1.33   |
| Intel     | Unknown                | 15     | 121     | 1505  | 613   | 1.31   |
| Intel     | Dell Certified Inte... | 9      | 108     | 530   | 20    | 1.27   |
| OWC       | SandForce Driven SSDs  | 1      | 2       | 462   | 0     | 1.27   |
| Goodram   | Phison Driven SSDs     | 4      | 14      | 456   | 0     | 1.25   |
| SanDisk   | SandForce Driven SSDs  | 4      | 8       | 775   | 4     | 1.24   |
| Intel     | 53x and Pro 1500/25... | 11     | 117     | 677   | 6     | 1.22   |
| Micron    | MX1/2/300, M5/600, ... | 4      | 25      | 485   | 1     | 1.21   |
| Micron    | BX/MX1/2/3/500, M5/... | 2      | 14      | 573   | 2     | 1.20   |
| SanDisk   | SATA CS1K GEN1 ESS ... | 1      | 1       | 431   | 0     | 1.18   |
| PNY       | Phison Driven SSDs     | 2      | 3       | 427   | 0     | 1.17   |
| Gigabyte  | Unknown                | 1      | 2       | 410   | 0     | 1.13   |
| SPCC      | Unknown                | 5      | 11      | 408   | 0     | 1.12   |
| Intel     | S4510/S4610/S4500/S... | 19     | 2923    | 489   | 3     | 1.11   |
| Micron    | 5100 Pro / 5200 / 5... | 10     | 351     | 517   | 5     | 1.08   |
| Corsair   | Unknown                | 1      | 1       | 1955  | 4     | 1.07   |
| Zheino    | Unknown                | 1      | 1       | 379   | 0     | 1.04   |
| Patriot   | Silicon Motion base... | 1      | 5       | 371   | 0     | 1.02   |
| Samsung   | Unknown                | 15     | 457     | 379   | 1     | 1.00   |
| KingDian  | Silicon Motion base... | 1      | 3       | 433   | 1     | 1.00   |
| Plextor   | Unknown                | 1      | 1       | 363   | 0     | 1.00   |
| Patriot   | Phison Driven SSDs     | 3      | 13      | 360   | 0     | 0.99   |
| WDC       | Blue / Red / Green ... | 12     | 224     | 401   | 2     | 0.99   |
| ORTIAL    | Unknown                | 1      | 12      | 432   | 1     | 0.98   |
| Seagate   | Nytro SATA SSD         | 7      | 157     | 341   | 0     | 0.94   |
| BIWIN     | Unknown                | 1      | 1       | 332   | 0     | 0.91   |
| Kingston  | Phison Driven SSDs     | 20     | 265     | 376   | 2     | 0.90   |
| Mushkin   | Unknown                | 3      | 14      | 387   | 1     | 0.87   |
| Seagate   | Unknown                | 3      | 5       | 311   | 0     | 0.85   |
| Transcend | Unknown                | 3      | 9       | 291   | 0     | 0.80   |
| ADATA     | Silicon Motion base... | 5      | 10      | 315   | 1     | 0.79   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 2      | 7       | 274   | 0     | 0.75   |
| SanDisk   | Unknown                | 8      | 21      | 293   | 88    | 0.71   |
| WDC       | Unknown                | 3      | 9       | 277   | 1     | 0.70   |
| KingSpec  | Unknown                | 2      | 3       | 253   | 0     | 0.70   |
| Phison    | Driven OEM SSDs        | 4      | 16      | 246   | 0     | 0.68   |
| Kingston  | Unknown                | 7      | 13      | 593   | 250   | 0.63   |
| China     | Unknown                | 6      | 16      | 294   | 2     | 0.63   |
| Micron    | Unknown                | 23     | 451     | 229   | 1     | 0.61   |
| SPCC      | Phison Driven OEM SSDs | 2      | 4       | 204   | 0     | 0.56   |
| Intel     | X18-M/X25-M/X25-V G... | 1      | 1       | 2595  | 12    | 0.55   |
| Apacer    | AS340 SSDs             | 2      | 43      | 307   | 20    | 0.54   |
| THU       | Unknown                | 1      | 1       | 197   | 0     | 0.54   |
| Dell      | Certified Intel S4x... | 1      | 11      | 194   | 0     | 0.53   |
| Crucial   | MX500 SSDs             | 6      | 522     | 227   | 3     | 0.52   |
| ADATA     | Unknown                | 8      | 17      | 539   | 180   | 0.48   |
| Intel     | DC S3110 Series SSDs   | 1      | 1       | 173   | 0     | 0.47   |
| SK hynix  | Unknown                | 1      | 12      | 162   | 0     | 0.45   |
| Crucial   | SiliconMotion based... | 2      | 2       | 157   | 0     | 0.43   |
| Intenso   | Unknown                | 1      | 2       | 156   | 0     | 0.43   |
| Patriot   | Unknown                | 2      | 2       | 154   | 0     | 0.42   |
| PNY       | Unknown                | 1      | 4       | 147   | 0     | 0.40   |
| Intel     | 545s Series SSDs       | 4      | 39      | 134   | 1     | 0.35   |
| Transcend | Silicon Motion base... | 8      | 25      | 127   | 1     | 0.28   |
| Maxtor    | Unknown                | 2      | 3       | 88    | 0     | 0.24   |
| Smartbuy  | Unknown                | 1      | 1       | 70    | 0     | 0.19   |
| Gigabyte  | Phison Driven SSDs     | 3      | 6       | 51    | 0     | 0.14   |
| Kingston  | Silicon Motion base... | 3      | 4       | 51    | 0     | 0.14   |
| QUMO      | Unknown                | 1      | 2       | 47    | 608   | 0.10   |
| KingFast  | Unknown                | 1      | 1       | 447   | 11    | 0.10   |
| V-GeN     | Unknown                | 1      | 1       | 16    | 0     | 0.04   |
| Crucial   | Unknown                | 1      | 2       | 12    | 0     | 0.03   |
| Palit     | Unknown                | 1      | 2       | 6     | 0     | 0.02   |
| Intel     | 540 Series SSDs        | 3      | 3       | 104   | 138   | 0.02   |
| Crucial   | RealSSD m4/C400/P400   | 1      | 1       | 2994  | 1011  | 0.01   |
| Avant     | Unknown                | 1      | 2       | 2045  | 1018  | 0.01   |
| INDMEM    | Unknown                | 1      | 1       | 0     | 0     | 0.00   |

SSD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| Apple       | 1      | 2       | 2325  | 0     | 6.37   |
| OCZ         | 10     | 18      | 1894  | 5     | 4.10   |
| Corsair     | 3      | 6       | 1567  | 1     | 3.58   |
| MyDigita... | 1      | 6       | 945   | 0     | 2.59   |
| XPG         | 1      | 2       | 806   | 0     | 2.21   |
| Plextor     | 3      | 4       | 803   | 0     | 2.20   |
| Lite-On     | 4      | 6       | 780   | 0     | 2.14   |
| Toshiba     | 18     | 218     | 762   | 1     | 2.04   |
| SanDisk     | 39     | 223     | 768   | 14    | 1.93   |
| HP          | 27     | 164     | 709   | 1     | 1.87   |
| Kingston    | 53     | 546     | 796   | 10    | 1.85   |
| SuperMicro  | 4      | 181     | 664   | 8     | 1.78   |
| OWC         | 2      | 3       | 975   | 1     | 1.76   |
| HPE         | 17     | 84      | 659   | 2     | 1.68   |
| Intel       | 138    | 4724    | 800   | 66    | 1.64   |
| Samsung     | 142    | 5844    | 653   | 7     | 1.64   |
| Goodram     | 6      | 20      | 566   | 0     | 1.55   |
| Innodisk    | 1      | 1       | 1074  | 1     | 1.47   |
| SATADOM     | 5      | 12      | 527   | 0     | 1.45   |
| Team        | 3      | 6       | 500   | 0     | 1.37   |
| WDC         | 24     | 284     | 456   | 2     | 1.16   |
| Dell        | 2      | 16      | 460   | 1     | 1.12   |
| Micron      | 68     | 1436    | 486   | 8     | 1.09   |
| Crucial     | 36     | 878     | 524   | 13    | 1.07   |
| Seagate     | 13     | 186     | 384   | 0     | 1.05   |
| Zheino      | 1      | 1       | 379   | 0     | 1.04   |
| KingDian    | 1      | 3       | 433   | 1     | 1.00   |
| ORTIAL      | 1      | 12      | 432   | 1     | 0.98   |
| SK hynix    | 8      | 30      | 355   | 0     | 0.97   |
| SPCC        | 7      | 15      | 354   | 0     | 0.97   |
| ADATA       | 15     | 30      | 621   | 103   | 0.95   |
| Patriot     | 6      | 20      | 342   | 0     | 0.94   |
| BIWIN       | 1      | 1       | 332   | 0     | 0.91   |
| Mushkin     | 3      | 14      | 387   | 1     | 0.87   |
| PNY         | 3      | 7       | 267   | 0     | 0.73   |
| KingSpec    | 2      | 3       | 253   | 0     | 0.70   |
| Phison      | 4      | 16      | 246   | 0     | 0.68   |
| China       | 6      | 16      | 294   | 2     | 0.63   |
| Apacer      | 5      | 48      | 327   | 18    | 0.63   |
| Transcend   | 12     | 35      | 223   | 1     | 0.57   |
| THU         | 1      | 1       | 197   | 0     | 0.54   |
| Intenso     | 1      | 2       | 156   | 0     | 0.43   |
| Gigabyte    | 4      | 8       | 141   | 0     | 0.39   |
| Maxtor      | 2      | 3       | 88    | 0     | 0.24   |
| Smartbuy    | 1      | 1       | 70    | 0     | 0.19   |
| QUMO        | 1      | 2       | 47    | 608   | 0.10   |
| KingFast    | 1      | 1       | 447   | 11    | 0.10   |
| V-GeN       | 1      | 1       | 16    | 0     | 0.04   |
| Palit       | 1      | 2       | 6     | 0     | 0.02   |
| Avant       | 1      | 2       | 2045  | 1018  | 0.01   |
| INDMEM      | 1      | 1       | 0     | 0     | 0.00   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See complete list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Intel     | SSDPEDME020T4      | 2 TB   | 2       | 1696  | 0     | 4.65   |
| Dell      | Express Flash N... | 800 GB | 1       | 1668  | 0     | 4.57   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 1       | 1576  | 0     | 4.32   |
| Intel     | SSDPEDME020T4D ... | 2 TB   | 2       | 1549  | 0     | 4.24   |
| Intel     | SSDPEDME016T4S     | 1.6 TB | 2       | 1496  | 0     | 4.10   |
| Intel     | SSDPEDME400G4      | 400 GB | 19      | 1469  | 0     | 4.03   |
| Intel     | SSDPE2MX012T4      | 1.2 TB | 4       | 1433  | 0     | 3.93   |
| Dell      | Express Flash N... | 3.2 TB | 1       | 1428  | 0     | 3.91   |
| Intel     | SSDPEDME800G4      | 800 GB | 1       | 1416  | 0     | 3.88   |
| Intel     | SSDPEDMX400G4      | 400 GB | 10      | 1410  | 0     | 3.86   |
| Samsung   | SSD 950 PRO        | 512 GB | 6       | 1392  | 0     | 3.82   |
| Intel     | SSDPEDMD400G4      | 400 GB | 201     | 1333  | 0     | 3.65   |
| Samsung   | MZ1LV480HCHP-00003 | 480 GB | 2       | 1263  | 0     | 3.46   |
| Intel     | SSDPEDMD020T4D ... | 2 TB   | 5       | 1263  | 0     | 3.46   |
| Intel     | SSDPEDMX020T7      | 2 TB   | 46      | 1271  | 5     | 3.41   |
| Intel     | SSDPEDMD016T4      | 1.6 TB | 15      | 1203  | 0     | 3.30   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 3       | 1202  | 0     | 3.29   |
| Intel     | SSDPEDMW400G4      | 400 GB | 10      | 1175  | 0     | 3.22   |
| Intel     | SSDPEDME016T4      | 1.6 TB | 1       | 1170  | 0     | 3.21   |
| Intel     | SSDPEDMX012T7      | 1.2 TB | 2       | 1149  | 0     | 3.15   |
| Intel     | SSDPE2KE016T7      | 1.6 TB | 2       | 1133  | 0     | 3.11   |
| Intel     | SSDPEDMD800G4      | 800 GB | 261     | 1120  | 0     | 3.07   |
| Micron    | MTFDHAL1T2MCF-1... | 1.2 TB | 1       | 1120  | 0     | 3.07   |
| Intel     | SSDPE2MD400G4      | 400 GB | 10      | 1003  | 0     | 2.75   |
| Dell      | Express Flash N... | 2 TB   | 2       | 958   | 0     | 2.63   |
| Samsung   | SSD 960 PRO        | 2 TB   | 1       | 921   | 0     | 2.52   |
| Samsung   | MZPLL1T6HEHP-00003 | 1.6 TB | 87      | 916   | 12    | 2.48   |
| Toshiba   | THNSN5512GPU7      | 512 GB | 10      | 901   | 0     | 2.47   |
| Intel     | SSDPEDMD020T4      | 2 TB   | 1       | 897   | 0     | 2.46   |
| Intel     | SSDPE2MD400G4L     | 400 GB | 4       | 895   | 0     | 2.45   |
| Intel     | SSDPEK1W120GA      | 118 GB | 1       | 876   | 0     | 2.40   |
| Samsung   | SSD 960 EVO        | 500 GB | 5       | 827   | 0     | 2.27   |
| Dell      | Express Flash N... | 1.6 TB | 18      | 867   | 56    | 2.22   |
| Samsung   | SSD 960 PRO        | 1 TB   | 10      | 807   | 0     | 2.21   |
| Intel     | SSDPEDKX040T7      | 4 TB   | 45      | 823   | 23    | 2.16   |
| Intel     | SSDPE2KE076T8      | 7.6 TB | 2       | 778   | 0     | 2.13   |
| Intel     | SSDPEDMW800G4      | 800 GB | 7       | 774   | 0     | 2.12   |
| Intel     | SSDPE2MX012T7      | 1.2 TB | 17      | 770   | 0     | 2.11   |
| Intel     | SSDPE2MX450G7      | 450 GB | 24      | 768   | 0     | 2.10   |
| Intel     | VO0400KEFJB        | 400 GB | 4       | 743   | 0     | 2.04   |
| Huawei    | HWE36P43016M000N   | 1.6 TB | 2       | 741   | 0     | 2.03   |
| Kingston  | SKC1000960G        | 960 GB | 3       | 738   | 0     | 2.02   |
| Samsung   | MZQLW960HMJP-00003 | 960 GB | 13      | 1216  | 199   | 2.01   |
| Intel     | SSDPEKKW512G7      | 512 GB | 1       | 728   | 0     | 2.00   |
| Intel     | SSDPEKKW256G7      | 256 GB | 14      | 719   | 1     | 1.91   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 22      | 692   | 0     | 1.90   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 2       | 678   | 0     | 1.86   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 1       | 676   | 0     | 1.85   |
| Samsung   | MZPLL3T2HMLS-00003 | 3.2 TB | 6       | 667   | 0     | 1.83   |
| Intel     | SSDPE2KX040T8      | 4 TB   | 60      | 677   | 18    | 1.83   |
| Intel     | SSDPED1D480GA      | 480 GB | 52      | 650   | 0     | 1.78   |
| Samsung   | MZQLW1T9HMJP-00003 | 1.9 TB | 2       | 639   | 0     | 1.75   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 1       | 633   | 0     | 1.73   |
| Samsung   | MZWLL6T4HMLA-00005 | 6.4 TB | 2       | 629   | 0     | 1.72   |
| Intel     | SSDPE2KX020T7      | 2 TB   | 1       | 611   | 0     | 1.68   |
| Intel     | SSDPED1D280GA      | 280 GB | 21      | 659   | 1     | 1.66   |
| Samsung   | MZPLL6T4HMLA-00005 | 6.4 TB | 6       | 593   | 0     | 1.63   |
| Intel     | MT0800KEXUU        | 800 GB | 16      | 575   | 0     | 1.58   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 6       | 562   | 0     | 1.54   |
| Samsung   | MZPLL6T4HMLS-00003 | 6.4 TB | 16      | 555   | 0     | 1.52   |
| Intel     | SSDPE21K375GA      | 375 GB | 30      | 554   | 0     | 1.52   |
| Dell      | Express Flash N... | 1.6 TB | 4       | 554   | 0     | 1.52   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 1       | 540   | 0     | 1.48   |
| Dell      | Express Flash N... | 3.2 TB | 4       | 538   | 0     | 1.47   |
| Intel     | SSDPEDMD016T4K     | 1.6 TB | 2       | 530   | 0     | 1.45   |
| Dell      | Express Flash P... | 6.4 TB | 1       | 527   | 0     | 1.45   |
| Samsung   | MZWLL800HEHP-00003 | 800 GB | 14      | 678   | 2     | 1.44   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 16      | 517   | 0     | 1.42   |
| Intel     | SSDPE2ME012T4      | 1.2 TB | 4       | 516   | 0     | 1.41   |
| PNY       | CS3030 500GB SSD   | 500 GB | 2       | 496   | 0     | 1.36   |
| Samsung   | SSD 960 EVO        | 250 GB | 2       | 491   | 0     | 1.35   |
| Samsung   | SSD 960 PRO        | 512 GB | 1       | 489   | 0     | 1.34   |
| Samsung   | SSD 970 EVO        | 500 GB | 2       | 486   | 0     | 1.33   |
| Samsung   | MZPLL1T6HAJQ-00005 | 1.6 TB | 2       | 481   | 0     | 1.32   |
| Intel     | SSDPED1K375GA      | 375 GB | 77      | 480   | 0     | 1.32   |
| Intel     | SSDPE21D480GA      | 480 GB | 107     | 470   | 0     | 1.29   |
| Intel     | SSDPED1D960GAY     | 960 GB | 6       | 460   | 0     | 1.26   |
| Intel     | SSDPE2KX080T8      | 8 TB   | 14      | 460   | 0     | 1.26   |
| Intel     | SSDPED1K750GA      | 752 GB | 114     | 454   | 0     | 1.25   |
| Wester... | WUS3BA196C7P3E3    | 960 GB | 83      | 439   | 0     | 1.20   |
| Kingston  | SKC2000M81000G     | 1 TB   | 2       | 438   | 0     | 1.20   |
| Intel     | SSDPEDKE040T7      | 4 TB   | 1       | 435   | 0     | 1.19   |
| Samsung   | SSD 983 DCT        | 960 GB | 2       | 431   | 0     | 1.18   |
| Intel     | SSDPEKKA256G7      | 256 GB | 4       | 431   | 0     | 1.18   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 3       | 703   | 337   | 1.18   |
| Wester... | WUS3CA116C7P3E3    | 1.6 TB | 178     | 428   | 0     | 1.17   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 1       | 426   | 0     | 1.17   |
| Wester... | WUS3BA119C7P3E3    | 960 GB | 1       | 424   | 0     | 1.16   |
| Wester... | WUS3BA138C7P3E3    | 3.8 TB | 20      | 424   | 0     | 1.16   |
| Samsung   | MZWLL12THMLA-00005 | 12.... | 2       | 422   | 0     | 1.16   |
| Samsung   | MZPLL3T2HAJQ-00005 | 3.2 TB | 24      | 420   | 0     | 1.15   |
| Dell      | Express Flash P... | 800 GB | 8       | 381   | 0     | 1.04   |
| Intel     | SSDPEKKW512G8      | 512 GB | 9       | 367   | 0     | 1.01   |
| Samsung   | MZ1LB960HAJQ-00007 | 960 GB | 24      | 362   | 0     | 0.99   |
| Phison    | PCIe SSD           | 256 GB | 1       | 362   | 0     | 0.99   |
| Samsung   | MZPLL6T4HMLS-000MV | 6.4 TB | 4       | 357   | 0     | 0.98   |
| Samsung   | MZQLB3T8HALS-000AZ | 3.8 TB | 24      | 352   | 0     | 0.97   |
| Intel     | SSDPE2KE032T8      | 3.2 TB | 29      | 345   | 0     | 0.95   |
| Corsair   | Force MP600        | 1 TB   | 1       | 343   | 0     | 0.94   |
| WDC       | CL SN720 SDAQNT... | 1 TB   | 31      | 335   | 0     | 0.92   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 75      | 335   | 11    | 0.88   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 4       | 302   | 0     | 0.83   |
| Toshiba   | KXD51RUE960G       | 960 GB | 2       | 299   | 0     | 0.82   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 12      | 298   | 0     | 0.82   |
| Dell      | Express Flash N... | 1.6 TB | 111     | 297   | 0     | 0.81   |
| Intel     | SSDPEKKA512G8      | 512 GB | 23      | 294   | 0     | 0.81   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 17      | 287   | 0     | 0.79   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 2       | 282   | 0     | 0.77   |
| Intel     | SSDPE21K750GA      | 752 GB | 56      | 277   | 0     | 0.76   |
| Intel     | SSDPE2KX010T8      | 1 TB   | 125     | 273   | 0     | 0.75   |
| Wester... | WUS4BB096D7P3E3    | 960 GB | 443     | 273   | 0     | 0.75   |
| Micron    | 2200S NVMe         | 256 GB | 1       | 272   | 0     | 0.75   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 164     | 271   | 0     | 0.74   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 15      | 268   | 0     | 0.73   |
| Phison    | Sabrent Rocket Q   | 2 TB   | 1       | 265   | 0     | 0.73   |
| Samsung   | MZWLJ15THALA-00007 | 15.... | 2       | 262   | 0     | 0.72   |
| Samsung   | MZQLB3T8HALS-00007 | 3.8 TB | 92      | 265   | 1     | 0.71   |
| Dell      | Express Flash P... | 1.6 TB | 1       | 259   | 0     | 0.71   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 17      | 254   | 0     | 0.70   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 35      | 253   | 0     | 0.69   |
| Samsung   | SSD 970 PRO        | 512 GB | 75      | 249   | 0     | 0.68   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 406     | 247   | 0     | 0.68   |
| Wester... | WUS4CB016D7P3E3    | 1.6 TB | 152     | 246   | 0     | 0.68   |
| Intel     | SSDPEL1K100GA      | 100 GB | 11      | 239   | 0     | 0.66   |
| Crucial   | CT250P2SSD8        | 250 GB | 1       | 239   | 0     | 0.66   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 5       | 238   | 0     | 0.65   |
| Intel     | SSDPE2NU076T8      | 7.6 TB | 3       | 236   | 0     | 0.65   |
| Samsung   | MZQLW1T9HMJP-000AZ | 1.9 TB | 7       | 257   | 1     | 0.64   |
| Dell      | Express Flash P... | 1.6 TB | 4       | 233   | 0     | 0.64   |
| Kingston  | SEDC1000M1920G     | 1.9 TB | 2       | 230   | 0     | 0.63   |
| Samsung   | SSD 970 PRO        | 1 TB   | 35      | 230   | 0     | 0.63   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 4       | 229   | 0     | 0.63   |
| Samsung   | SSD 970 EVO        | 250 GB | 2       | 360   | 1     | 0.62   |
| Intel     | SSDPE21K100GA      | 100 GB | 5       | 224   | 0     | 0.62   |
| Intel     | SSDPE2ME400G4      | 400 GB | 7       | 223   | 0     | 0.61   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 6       | 223   | 0     | 0.61   |
| Intel     | EO000375KWJUC      | 375 GB | 2       | 221   | 0     | 0.61   |
| Samsung   | MZPJB480HMGC-0BW07 | 480 GB | 15      | 219   | 0     | 0.60   |
| Phison    | Viper M.2 VPN100   | 2 TB   | 7       | 217   | 0     | 0.60   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 515     | 214   | 1     | 0.59   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 1       | 211   | 0     | 0.58   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 19      | 204   | 0     | 0.56   |
| HP        | SSD EX950          | 2 TB   | 10      | 199   | 0     | 0.55   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 15      | 201   | 1     | 0.53   |
| Kingston  | SA2000M81000G      | 1 TB   | 4       | 192   | 0     | 0.53   |
| SK hynix  | PC601 NVMe         | 256 GB | 1       | 192   | 0     | 0.53   |
| Samsung   | VO001920KWVMT 1... | 1.9 TB | 36      | 191   | 0     | 0.53   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 1       | 191   | 0     | 0.52   |
| Micron    | 9300_MTFDHAL3T2TDR | 3.2 TB | 20      | 190   | 0     | 0.52   |
| Samsung   | MZWLL1T6HAJQ-00005 | 1.6 TB | 10      | 188   | 0     | 0.52   |
| Intel     | SSDPE2KX010T7      | 1 TB   | 8       | 186   | 0     | 0.51   |
| Intel     | SSDPECKE064T7ES    | 3.2 TB | 2       | 186   | 0     | 0.51   |
| Dell      | Express Flash P... | 1.6 TB | 12      | 182   | 0     | 0.50   |
| Samsung   | SSD 970 EVO        | 1 TB   | 5       | 324   | 3     | 0.48   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 2       | 173   | 0     | 0.48   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 28      | 173   | 0     | 0.48   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 8       | 170   | 0     | 0.47   |
| XPG       | SPECTRIX S40G      | 1 TB   | 1       | 168   | 0     | 0.46   |
| ADATA     | SX8200PNP          | 1 TB   | 1       | 164   | 0     | 0.45   |
| Intel     | SSDPE2KE016T8      | 1.6 TB | 27      | 164   | 0     | 0.45   |
| Samsung   | MZWLL1T6HEHP-00003 | 1.6 TB | 8       | 163   | 0     | 0.45   |
| Crucial   | CT500P1SSD8        | 500 GB | 2       | 163   | 0     | 0.45   |
| Wester... | WUS4BB038D7P3E3    | 3.8 TB | 13      | 162   | 0     | 0.44   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 6       | 161   | 0     | 0.44   |
| Toshiba   | KXD51RUE1T92       | 1.9 TB | 8       | 158   | 0     | 0.44   |
| Intel     | SSDPE2MD016T4      | 1.6 TB | 4       | 150   | 0     | 0.41   |
| Samsung   | MZQLB7T6HMLA-00007 | 7.6 TB | 64      | 150   | 0     | 0.41   |
| Seagate   | FireCuda 520 SS... | 500 GB | 10      | 147   | 0     | 0.40   |
| Micron    | 9300_MTFDHAL7T6TDP | 7.6 TB | 30      | 144   | 0     | 0.40   |
| HGST      | HUSMR7638BDP3Y1    | 3.8 TB | 24      | 135   | 0     | 0.37   |
| Dell      | Express Flash C... | 960 GB | 46      | 135   | 0     | 0.37   |
| Intel     | SSDPE2MD800G4      | 800 GB | 1       | 130   | 0     | 0.36   |
| Intel     | SSDPECME016T4      | 800 GB | 8       | 129   | 0     | 0.35   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 9       | 126   | 0     | 0.35   |
| Toshiba   | KXD51RUE3T84       | 3.8 TB | 1       | 118   | 0     | 0.32   |
| Wester... | WUS4BB019D7P3E1    | 1.9 TB | 193     | 117   | 0     | 0.32   |
| Wester... | WUS4BB076D7P3E1    | 7.6 TB | 12      | 114   | 0     | 0.31   |
| Kingston  | SKC2500M81000G     | 1 TB   | 4       | 113   | 0     | 0.31   |
| Kingston  | SA2000M8500G       | 500 GB | 4       | 111   | 0     | 0.31   |
| KIOXIA    | KCD6XLUL1T92       | 1.9 TB | 10      | 109   | 0     | 0.30   |
| Kingston  | SKC2500M8250G      | 250 GB | 4       | 109   | 0     | 0.30   |
| Huawei    | HWE52P431T6M002N   | 1.6 TB | 2       | 108   | 0     | 0.30   |
| Samsung   | MZ4LB3T8HALS-00003 | 3.8 TB | 6       | 107   | 0     | 0.29   |
| HP        | SSD EX950          | 512 GB | 6       | 106   | 0     | 0.29   |
| Samsung   | MZPLJ3T2HBJR-00007 | 3.2 TB | 2       | 103   | 0     | 0.28   |
| WDC       | PC SN530 NVMe      | 512 GB | 1       | 103   | 0     | 0.28   |
| Kingston  | SA2000M8250G       | 250 GB | 1       | 101   | 0     | 0.28   |
| Samsung   | MZ1LB1T9HALS-00007 | 1.9 TB | 3       | 99    | 0     | 0.27   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 8       | 98    | 0     | 0.27   |
| Wester... | WUS4BB096D7P3E1    | 960 GB | 200     | 97    | 0     | 0.27   |
| Samsung   | MZWLJ7T6HALA-00007 | 7.6 TB | 2       | 97    | 0     | 0.27   |
| Smartbuy  | m.2 PS5013T-2280T  | 128 GB | 1       | 95    | 0     | 0.26   |
| Samsung   | MZPLJ6T4HALA-00007 | 6.4 TB | 30      | 94    | 0     | 0.26   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 12      | 96    | 1     | 0.26   |
| Dell      | Express Flash P... | 1.6 TB | 4       | 92    | 0     | 0.25   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 52      | 89    | 0     | 0.24   |
| Samsung   | MT001600KWHAC 1... | 1.6 TB | 1       | 77    | 0     | 0.21   |
| Wester... | WUS4BB038D7P3E1    | 3.8 TB | 71      | 76    | 0     | 0.21   |
| SK hynix  | BC501 HFM512GDJ... | 512 GB | 1       | 73    | 0     | 0.20   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 28      | 71    | 0     | 0.20   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 3       | 71    | 0     | 0.20   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 22      | 67    | 0     | 0.19   |
| Micron    | 7300_MTFDHBE1T6TDG | 1.6 TB | 2       | 64    | 0     | 0.18   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 15      | 61    | 0     | 0.17   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 2       | 58    | 0     | 0.16   |
| Toshiba   | KXG60ZNV256G       | 256 GB | 23      | 54    | 0     | 0.15   |
| Toshiba   | KXG60PNV2T04       | 2 TB   | 6       | 53    | 0     | 0.15   |
| Kingston  | SKC2500M8500G      | 500 GB | 2       | 52    | 0     | 0.14   |
| Huawei    | HWE56P43800M005N   | 800 GB | 3       | 48    | 0     | 0.13   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 6       | 48    | 0     | 0.13   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 6       | 47    | 0     | 0.13   |
| Kingston  | SEDC1000M3840G     | 3.8 TB | 6       | 47    | 0     | 0.13   |
| SK hynix  | PC601 HFS256GD9... | 256 GB | 1       | 46    | 0     | 0.13   |
| ADATA     | SX8200PNP          | 2 TB   | 2       | 45    | 0     | 0.13   |
| Samsung   | MZPJB960HMGC-0BW07 | 960 GB | 11      | 45    | 0     | 0.12   |
| Patriot   | P300               | 256 GB | 2       | 44    | 0     | 0.12   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 3       | 43    | 0     | 0.12   |
| Intel     | MDTPED1K750GA      | 752 GB | 2       | 41    | 0     | 0.11   |
| Kingston  | SEDC1000M960G      | 960 GB | 2       | 35    | 0     | 0.10   |
| Silico... | NV900-1T           | 1 TB   | 1       | 30    | 0     | 0.08   |
| ADATA     | SX6000LNP          | 512 GB | 1       | 30    | 0     | 0.08   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 7       | 26    | 0     | 0.07   |
| Micron    | 7300_MTFDHBE960TDF | 960 GB | 4       | 25    | 0     | 0.07   |
| ADATA     | SX8200PNP          | 512 GB | 3       | 22    | 0     | 0.06   |
| Patriot   | P300               | 128 GB | 4       | 19    | 0     | 0.05   |
| Wester... | WUS4BB096D7P3E4    | 960 GB | 4       | 13    | 0     | 0.04   |
| Wester... | WUS4CB032D7P3E4    | 3.2 TB | 4       | 11    | 0     | 0.03   |
| Intel     | SSDPELKX010T8      | 1 TB   | 2       | 9     | 0     | 0.03   |
| Kingston  | SKC2500M82000G     | 2 TB   | 1       | 5     | 0     | 0.02   |
| Corsair   | MP400              | 1 TB   | 1       | 5     | 0     | 0.01   |
| KIOXIA    | KCD61LUL3T84       | 3.8 TB | 20      | 5     | 0     | 0.01   |
| Intel     | SSDPEKNW512G8      | 512 GB | 1       | 4     | 0     | 0.01   |
| ADATA     | SX6000NP           | 128 GB | 1       | 615   | 142   | 0.01   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | SSD 980            | 500 GB | 2       | 3     | 0     | 0.01   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 2       | 1     | 0     | 0.00   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 2       | 0     | 0     | 0.00   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF   |
|-------------|--------|---------|-------|-------|--------|
| Intel       | 69     | 1745    | 711   | 2     | 1.94   |
| SPCC        | 1      | 1       | 633   | 0     | 1.73   |
| PNY         | 1      | 2       | 496   | 0     | 1.36   |
| Dell        | 14     | 217     | 329   | 5     | 0.89   |
| WDC         | 12     | 165     | 293   | 5     | 0.79   |
| Toshiba     | 11     | 121     | 283   | 0     | 0.78   |
| Corsair     | 3      | 14      | 280   | 0     | 0.77   |
| Samsung     | 66     | 1768    | 287   | 3     | 0.77   |
| Huawei      | 3      | 7       | 263   | 0     | 0.72   |
| Western ... | 13     | 1374    | 241   | 0     | 0.66   |
| Phison      | 3      | 9       | 239   | 0     | 0.66   |
| Crucial     | 2      | 3       | 188   | 0     | 0.52   |
| Kingston    | 12     | 35      | 178   | 0     | 0.49   |
| Gigabyte    | 1      | 8       | 170   | 0     | 0.47   |
| XPG         | 1      | 1       | 168   | 0     | 0.46   |
| HP          | 2      | 16      | 164   | 0     | 0.45   |
| Seagate     | 1      | 10      | 147   | 0     | 0.40   |
| HGST        | 1      | 24      | 135   | 0     | 0.37   |
| Micron      | 8      | 125     | 122   | 0     | 0.34   |
| SK hynix    | 3      | 3       | 104   | 0     | 0.29   |
| Smartbuy    | 1      | 1       | 95    | 0     | 0.26   |
| ADATA       | 5      | 8       | 121   | 18    | 0.12   |
| KIOXIA      | 2      | 30      | 39    | 0     | 0.11   |
| Silicon ... | 1      | 1       | 30    | 0     | 0.08   |
| Patriot     | 2      | 6       | 28    | 0     | 0.08   |

