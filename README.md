Reliability Test For Enterprise Hard Drives
===========================================

This is a project to estimate reliability of enterprise HDD/SSD drives by the analysis
of SMART reports from servers. The primary aim of the project is to find drives with
longest power-on hours (POH) and minimal number of errors, i.e. maximal MTBF (mean time
between failures).

Everyone can contribute to this report by installing [hw-probe](https://github.com/linuxhw/hw-probe) to
their [OpenVZ 7 or Virtuozzo 7](https://wiki.openvz.org/) servers:

    sudo -E hw-probe -all -upload

Total drives: 51186.

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

See full list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| WDC       | WD740ADFD-00NLR5   | 74 GB  | 1       | 4658  | 0     | 12.76  |
| Hitachi   | HDS725050KLA360    | 500 GB | 1       | 4456  | 0     | 12.21  |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 1       | 3899  | 0     | 10.68  |
| Hitachi   | HDS721010KLA33R... | 1 TB   | 1       | 3863  | 0     | 10.58  |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 2       | 3719  | 0     | 10.19  |
| Seagate   | ST32500NSSUN250G   | 250 GB | 2       | 3676  | 0     | 10.07  |
| Maxtor    | STM3250310AS       | 250 GB | 2       | 3651  | 0     | 10.00  |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 3       | 3596  | 0     | 9.85   |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 16      | 3909  | 1     | 9.25   |
| Hitachi   | HUA722050CLA330    | 500 GB | 2       | 3243  | 0     | 8.89   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 3       | 3147  | 0     | 8.62   |
| Seagate   | ST3320620AS        | 320 GB | 3       | 4439  | 5     | 8.48   |
| HP        | GB0500EAFYL        | 500 GB | 2       | 2973  | 0     | 8.15   |
| WDC       | WD5000AAKS-00V6A0  | 500 GB | 1       | 2965  | 0     | 8.12   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 1       | 2955  | 0     | 8.10   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 16      | 3343  | 16    | 8.08   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 4       | 2929  | 0     | 8.03   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 8       | 3346  | 1     | 7.99   |
| Hitachi   | HUA722020ALA330... | 2 TB   | 1       | 2886  | 0     | 7.91   |
| Samsung   | HD250HJ            | 250 GB | 1       | 2882  | 0     | 7.90   |
| Seagate   | ST32000645NS       | 2 TB   | 88      | 3111  | 15    | 7.89   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 1       | 2878  | 0     | 7.89   |
| Hitachi   | HDS721050CLA360    | 500 GB | 2       | 2828  | 0     | 7.75   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 1       | 2827  | 0     | 7.75   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 81      | 3052  | 1     | 7.75   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 8       | 3041  | 22    | 7.73   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 1       | 2778  | 0     | 7.61   |
| Seagate   | ST3320620A         | 320 GB | 2       | 2728  | 0     | 7.47   |
| WDC       | WD1002FBYS-50A6B1  | 1 TB   | 1       | 2722  | 0     | 7.46   |
| Toshiba   | DT01ABA300         | 3 TB   | 1       | 2720  | 0     | 7.45   |
| Hitachi   | HUA723020ALA640... | 2 TB   | 1       | 2643  | 0     | 7.24   |
| WDC       | WD1600JD-75HBB0    | 160 GB | 1       | 2640  | 0     | 7.23   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 23      | 2692  | 1     | 7.17   |
| Hitachi   | HUA722010CLA330... | 1 TB   | 1       | 2591  | 0     | 7.10   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 6       | 2982  | 1     | 7.07   |
| WDC       | WD2500AAJS-22L7A0  | 250 GB | 1       | 2570  | 0     | 7.04   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 1       | 2562  | 0     | 7.02   |
| Samsung   | HD753LJ            | 752 GB | 1       | 2559  | 0     | 7.01   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 2       | 2547  | 0     | 6.98   |
| Seagate   | ST3250620NS        | 250 GB | 4       | 2532  | 0     | 6.94   |
| HP        | GB0250EAFYK        | 250 GB | 2       | 2531  | 0     | 6.93   |
| WDC       | WD3200AAKS-61L9A0  | 320 GB | 1       | 2526  | 0     | 6.92   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 1       | 2526  | 0     | 6.92   |
| HP        | GB0500C4413        | 500 GB | 2       | 3306  | 1     | 6.90   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 16      | 2827  | 2     | 6.88   |
| Seagate   | ST2000VX000-1CU164 | 2 TB   | 1       | 2477  | 0     | 6.79   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 34      | 2875  | 62    | 6.77   |
| WDC       | WD5000AACS-00G8B1  | 500 GB | 2       | 4300  | 3     | 6.73   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 2       | 2433  | 0     | 6.67   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 5       | 2785  | 1     | 6.66   |
| Seagate   | ST32000646NS       | 2 TB   | 2       | 2424  | 0     | 6.64   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 1       | 2403  | 0     | 6.59   |
| Seagate   | ST3250410AS        | 250 GB | 4       | 3449  | 85    | 6.55   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 2       | 2359  | 0     | 6.46   |
| HP        | MB1000GCWCV        | 1 TB   | 3       | 2355  | 0     | 6.45   |
| Hitachi   | HDS721010CLA330    | 1 TB   | 1       | 2342  | 0     | 6.42   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 1       | 2335  | 0     | 6.40   |
| HGST      | HUS724020ALE640    | 2 TB   | 1       | 2280  | 0     | 6.25   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 29      | 2406  | 1     | 6.22   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 30      | 2342  | 1     | 6.17   |
| WDC       | WD7502AAEX-00Y9A0  | 752 GB | 4       | 2242  | 0     | 6.14   |
| HP        | GB1000EAMYC        | 1 TB   | 1       | 2228  | 0     | 6.11   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 3       | 2222  | 0     | 6.09   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 10      | 2883  | 9     | 6.05   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 6       | 2569  | 2     | 5.96   |
| WDC       | WD1001FALS-00E8B0  | 1 TB   | 1       | 2171  | 0     | 5.95   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 11      | 2849  | 3     | 5.89   |
| HGST      | HDS724040ALE640    | 4 TB   | 6       | 2140  | 0     | 5.86   |
| Seagate   | ST3000VX000-1CU166 | 3 TB   | 26      | 2459  | 4     | 5.82   |
| Seagate   | ST3320620NS        | 320 GB | 4       | 2189  | 1     | 5.81   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 32      | 2203  | 1     | 5.78   |
| Seagate   | ST2000NC000-1CX164 | 2 TB   | 1       | 2101  | 0     | 5.76   |
| Hitachi   | HDP725050GLA360    | 500 GB | 3       | 2095  | 0     | 5.74   |
| Seagate   | ST3000VX006-1HH166 | 3 TB   | 2       | 2069  | 0     | 5.67   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 2       | 2067  | 0     | 5.67   |
| Seagate   | ST3400620AS        | 400 GB | 1       | 2060  | 0     | 5.65   |
| Toshiba   | MD04ACA500         | 5 TB   | 2       | 2046  | 0     | 5.61   |
| Seagate   | ST2000VX000-1ES164 | 2 TB   | 1       | 2043  | 0     | 5.60   |
| WDC       | WD1600AAJS-08L7A0  | 160 GB | 1       | 2027  | 0     | 5.56   |
| WDC       | WD6001FSYZ-01SS7B0 | 6 TB   | 3       | 1989  | 0     | 5.45   |
| Seagate   | ST2000NM0033       | 2 TB   | 1       | 1988  | 0     | 5.45   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 4       | 1958  | 0     | 5.37   |
| Maxtor    | 6V160E0            | 160 GB | 2       | 1932  | 0     | 5.29   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 2       | 1929  | 0     | 5.29   |
| WDC       | WD2004FBYZ-01YCBB0 | 2 TB   | 5       | 1902  | 0     | 5.21   |
| WDC       | WD2001FFSX-68JNUN0 | 2 TB   | 2       | 1899  | 0     | 5.20   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 8       | 2103  | 11    | 5.19   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 4       | 1888  | 0     | 5.17   |
| WDC       | WD10EZEX-22RKKA0   | 1 TB   | 4       | 2248  | 1     | 5.15   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 1877  | 0     | 5.14   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 9       | 2087  | 1     | 5.14   |
| Seagate   | ST91000640NS       | 1 TB   | 33      | 1990  | 1     | 5.14   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 437     | 2259  | 106   | 5.09   |
| HGST      | HUS724020ALA640    | 2 TB   | 205     | 1921  | 10    | 5.08   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 17      | 2335  | 2     | 5.01   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 2       | 1825  | 0     | 5.00   |
| WDC       | WD2500AAJS-00B4A0  | 250 GB | 1       | 1814  | 0     | 4.97   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 4       | 2789  | 4     | 4.96   |
| WDC       | WD2002FYPS-01U1B1  | 2 TB   | 17      | 2794  | 201   | 4.96   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 22      | 1885  | 7     | 4.96   |
| HGST      | HUS726060ALE614    | 6 TB   | 147     | 1949  | 11    | 4.94   |
| Hitachi   | HDT725032VLA360    | 320 GB | 5       | 3607  | 7     | 4.88   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 33      | 2086  | 42    | 4.87   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 2       | 1777  | 0     | 4.87   |
| HP        | GB0160EAFJE        | 160 GB | 2       | 2903  | 513   | 4.82   |
| WDC       | WD5000BHTZ-04JCPV0 | 500 GB | 1       | 1758  | 0     | 4.82   |
| Toshiba   | MK0502TSKB         | 500 GB | 1       | 1752  | 0     | 4.80   |
| Toshiba   | MK1002TSKB         | 1 TB   | 10      | 1749  | 0     | 4.79   |
| WDC       | WD20EADS-00R6B0    | 2 TB   | 2       | 3212  | 6     | 4.77   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 7       | 1733  | 0     | 4.75   |
| Seagate   | ST3500630AS        | 500 GB | 1       | 1720  | 0     | 4.71   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 15      | 1710  | 0     | 4.69   |
| WDC       | WD4001FFSX-68JNUN0 | 4 TB   | 12      | 2048  | 1     | 4.67   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 20      | 1939  | 20    | 4.67   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 7       | 2089  | 1     | 4.66   |
| Samsung   | HD103UJ            | 1 TB   | 26      | 2880  | 144   | 4.60   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 59      | 1989  | 42    | 4.60   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 17      | 1760  | 15    | 4.59   |
| Toshiba   | HDWE160            | 6 TB   | 74      | 1747  | 1     | 4.56   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 7       | 2404  | 1     | 4.53   |
| Seagate   | ST500NM0011 00W... | 500 GB | 2       | 1647  | 0     | 4.51   |
| WDC       | WD5003ABYX-23 0... | 500 GB | 2       | 1645  | 0     | 4.51   |
| Seagate   | ST2000NM0024-1H... | 2 TB   | 9       | 1645  | 0     | 4.51   |
| WDC       | WD5003AZEX-00S3DA0 | 500 GB | 16      | 1644  | 0     | 4.51   |
| Seagate   | ST3500630NS        | 500 GB | 9       | 1643  | 0     | 4.50   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 6       | 2294  | 2     | 4.47   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 1       | 1630  | 0     | 4.47   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 5       | 2547  | 5     | 4.45   |
| HGST      | HDN724040ALE640    | 4 TB   | 22      | 1721  | 92    | 4.44   |
| Seagate   | ST33000651AS       | 3 TB   | 4       | 2329  | 10    | 4.44   |
| WDC       | WD6402AAEX-00Y9A0  | 640 GB | 3       | 2411  | 677   | 4.43   |
| Hitachi   | HDT721050SLA360    | 500 GB | 1       | 1617  | 0     | 4.43   |
| Seagate   | ST9500620NS        | 500 GB | 27      | 1811  | 1     | 4.41   |
| WDC       | WD20EARX-00MMMB0   | 2 TB   | 2       | 2666  | 2     | 4.39   |
| Seagate   | ST6000NM0024-1H... | 6 TB   | 1675    | 1889  | 18    | 4.38   |
| WDC       | WD5000AAKX-003CA0  | 500 GB | 3       | 2165  | 3     | 4.36   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 23      | 2185  | 67    | 4.34   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 3       | 1583  | 0     | 4.34   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 4       | 1581  | 0     | 4.33   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 55      | 2120  | 25    | 4.29   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 16      | 1885  | 2     | 4.28   |
| WDC       | WD1500HLHX-01JJPV0 | 150 GB | 1       | 1552  | 0     | 4.25   |
| WDC       | WD1000CHTZ-04JCPV1 | 1 TB   | 4       | 1542  | 0     | 4.22   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 1       | 1518  | 0     | 4.16   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 30      | 1508  | 0     | 4.13   |
| HGST      | HUS726030ALA610    | 3 TB   | 47      | 1529  | 1     | 4.13   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 13      | 1504  | 0     | 4.12   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 7       | 1796  | 16    | 4.12   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 56      | 1578  | 6     | 4.10   |
| Seagate   | ST6000VX0001-1S... | 6 TB   | 2       | 1493  | 0     | 4.09   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 4       | 2749  | 4     | 4.09   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 29      | 1695  | 211   | 4.09   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 15      | 1779  | 2     | 4.08   |
| WDC       | WD2003FYYS-05T8B0  | 2 TB   | 2       | 1487  | 0     | 4.08   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 3       | 1485  | 0     | 4.07   |
| WDC       | WD10EALX-089BA0    | 1 TB   | 7       | 1879  | 2     | 4.06   |
| Seagate   | ST320DM000-1BC14C  | 320 GB | 2       | 1479  | 0     | 4.05   |
| WDC       | WD2500HHTZ-04N21V0 | 250 GB | 3       | 1473  | 0     | 4.04   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 136     | 1741  | 83    | 4.03   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 36      | 1951  | 50    | 4.03   |
| WDC       | WD5000HHTZ-04N21V0 | 500 GB | 1       | 1468  | 0     | 4.02   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 1       | 1465  | 0     | 4.01   |
| HP        | MB1000GCEHH        | 1 TB   | 4       | 2908  | 578   | 4.00   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 6       | 1954  | 1     | 4.00   |
| WDC       | WD2003FYPS-02W0B1  | 2 TB   | 2       | 1454  | 0     | 3.99   |
| Seagate   | ST33000650NS       | 3 TB   | 19      | 2306  | 68    | 3.97   |
| WDC       | WD5000AZLX-07K2TA0 | 500 GB | 1       | 1444  | 0     | 3.96   |
| HGST      | HUS724040ALA640    | 4 TB   | 139     | 1524  | 2     | 3.95   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 10      | 2351  | 203   | 3.93   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 19      | 2820  | 396   | 3.93   |
| WDC       | WD4003FZEX-00Z4SA0 | 4 TB   | 14      | 1431  | 0     | 3.92   |
| Toshiba   | DT01ACA300         | 3 TB   | 77      | 1717  | 21    | 3.92   |
| WDC       | WD2000FYYZ-01UL1B3 | 2 TB   | 1       | 1427  | 0     | 3.91   |
| Samsung   | SP0812C            | 80 GB  | 1       | 1426  | 0     | 3.91   |
| WDC       | WD5002AALX-32Z3A0  | 500 GB | 7       | 1425  | 0     | 3.91   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 4       | 1417  | 0     | 3.88   |
| HGST      | HTE541010A9E680    | 1 TB   | 6       | 1414  | 0     | 3.87   |
| WDC       | WD20EADS-65R6B1    | 2 TB   | 1       | 2788  | 1     | 3.82   |
| WDC       | WD40PURX-64NZ6Y0   | 4 TB   | 4       | 1394  | 0     | 3.82   |
| HGST      | HUS724030ALA640    | 3 TB   | 37      | 1636  | 71    | 3.82   |
| HGST      | HUS724040ALE640    | 4 TB   | 22      | 1390  | 0     | 3.81   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 17      | 1519  | 219   | 3.81   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 8       | 1609  | 44    | 3.80   |
| WDC       | WD101KRYZ-01JPDB0  | 10 TB  | 1       | 1384  | 0     | 3.79   |
| HGST      | HUH728080ALE600    | 8 TB   | 20      | 1382  | 0     | 3.79   |
| WDC       | WD5000BMVW-11AJGS2 | 500 GB | 2       | 1375  | 0     | 3.77   |
| Seagate   | ST9250610NS        | 250 GB | 8       | 1375  | 0     | 3.77   |
| WDC       | WD5000AUDX-61WNHY0 | 500 GB | 1       | 1373  | 0     | 3.76   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 7       | 2160  | 401   | 3.75   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 4       | 1494  | 1     | 3.75   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 6       | 2120  | 3     | 3.74   |
| Toshiba   | MG04ACA600E        | 6 TB   | 766     | 1435  | 15    | 3.73   |
| WDC       | WD4000FYYZ-03UL1B3 | 4 TB   | 2       | 1360  | 0     | 3.73   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 1       | 1356  | 0     | 3.72   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 2       | 1353  | 0     | 3.71   |
| WDC       | WD100PURZ-85W86Y0  | 10 TB  | 1       | 1347  | 0     | 3.69   |
| WDC       | WD1003FBYX-50Y7B1  | 1 TB   | 3       | 1335  | 0     | 3.66   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 123     | 1599  | 7     | 3.64   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 3       | 1328  | 0     | 3.64   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 288     | 2022  | 17    | 3.63   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 42      | 1495  | 8     | 3.63   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 6       | 1320  | 0     | 3.62   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 18      | 1585  | 88    | 3.61   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 2       | 1315  | 0     | 3.60   |
| HGST      | HDN724030ALE640    | 3 TB   | 7       | 1299  | 0     | 3.56   |
| Hitachi   | HDS721075KLA330    | 752 GB | 1       | 3894  | 2     | 3.56   |
| WDC       | WD2000FYYZ-03UL1B2 | 2 TB   | 1       | 1292  | 0     | 3.54   |
| HGST      | HDN726060ALE614    | 6 TB   | 2       | 1289  | 0     | 3.53   |
| HGST      | HDN726040ALE614    | 4 TB   | 23      | 1287  | 0     | 3.53   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 2       | 2317  | 4     | 3.53   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 95      | 1621  | 104   | 3.52   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 10      | 1374  | 1     | 3.50   |
| WDC       | WD5003ABYX-01WERA0 | 500 GB | 20      | 1598  | 2     | 3.50   |
| Toshiba   | MG04ACA200EY       | 2 TB   | 7       | 1270  | 0     | 3.48   |
| Toshiba   | DT01ACA100         | 1 TB   | 37      | 1415  | 28    | 3.48   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 1       | 1262  | 0     | 3.46   |
| WDC       | WD5000BPKX-22HPJT0 | 500 GB | 5       | 1483  | 2     | 3.46   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 17      | 1781  | 428   | 3.46   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 1       | 1260  | 0     | 3.45   |
| Samsung   | HD154UI            | 1.5 TB | 2       | 1879  | 1     | 3.44   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 7       | 2296  | 3     | 3.43   |
| WDC       | WD20NMVW-11W68S0   | 2 TB   | 1       | 1251  | 0     | 3.43   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 89      | 1361  | 14    | 3.42   |
| Seagate   | ST1000NM0011       | 1 TB   | 27      | 1693  | 81    | 3.42   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 24      | 1333  | 1     | 3.41   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 15      | 1348  | 1     | 3.39   |
| Toshiba   | MG04ACA600EY       | 6 TB   | 2       | 1236  | 0     | 3.39   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 45      | 1572  | 2     | 3.37   |
| Toshiba   | MG03ACA100         | 1 TB   | 49      | 1238  | 2     | 3.34   |
| Samsung   | HD103SJ            | 1 TB   | 23      | 2119  | 4     | 3.34   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 19      | 1405  | 56    | 3.34   |
| Maxtor    | STM3500630AS       | 500 GB | 2       | 1214  | 0     | 3.33   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 1       | 1213  | 0     | 3.32   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 928     | 1313  | 20    | 3.32   |
| HGST      | HUS726060ALE610    | 6 TB   | 23      | 1203  | 0     | 3.30   |
| Samsung   | HD161GJ            | 160 GB | 3       | 1200  | 0     | 3.29   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 15      | 1304  | 150   | 3.28   |
| WDC       | WD2004FBYZ-01YCBB2 | 2 TB   | 1       | 1197  | 0     | 3.28   |
| Seagate   | ST8000DM005-2EH112 | 8 TB   | 215     | 1259  | 1     | 3.27   |
| HGST      | HDN721010ALE604    | 10 TB  | 2       | 1188  | 0     | 3.26   |
| MaxDig... | MD4000GBDS         | 4 TB   | 1       | 1187  | 0     | 3.25   |
| Seagate   | ST6000VX0023-2E... | 6 TB   | 17      | 1187  | 0     | 3.25   |
| WDC       | WD4002FYYZ-01B7CB0 | 4 TB   | 51      | 1332  | 3     | 3.25   |
| HGST      | HUS726020ALE614    | 2 TB   | 78      | 1212  | 1     | 3.24   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 16      | 1315  | 1     | 3.24   |
| WDC       | WD1004FBYZ-01YCBB1 | 1 TB   | 7       | 1179  | 0     | 3.23   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 2       | 1179  | 0     | 3.23   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 34      | 1748  | 29    | 3.23   |
| Toshiba   | MQ01ABF050         | 500 GB | 1       | 1175  | 0     | 3.22   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 14      | 1355  | 2     | 3.22   |
| Seagate   | ST2000VN0001-1S... | 2 TB   | 4       | 1167  | 0     | 3.20   |
| WDC       | WD10EZEX-00UD2A0   | 1 TB   | 1       | 1166  | 0     | 3.20   |
| Seagate   | ST500NM0011        | 500 GB | 9       | 1964  | 5     | 3.19   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 7       | 1162  | 0     | 3.19   |
| Hitachi   | HDT725050VLA360    | 500 GB | 1       | 1157  | 0     | 3.17   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 4       | 1156  | 0     | 3.17   |
| HGST      | HUS722T1TALA600    | 1 TB   | 29      | 1154  | 0     | 3.16   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 43      | 1690  | 12    | 3.15   |
| Seagate   | ST4000VX000-1F4168 | 4 TB   | 4       | 1150  | 0     | 3.15   |
| Seagate   | ST8000DM002-1YW112 | 8 TB   | 135     | 1214  | 2     | 3.15   |
| Toshiba   | MG04ACA300E        | 3 TB   | 1       | 1147  | 0     | 3.14   |
| WDC       | WD10EALS-00Z8A0    | 1 TB   | 7       | 2354  | 5     | 3.14   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 2       | 1146  | 0     | 3.14   |
| HGST      | HUS726020ALE610    | 2 TB   | 11      | 1145  | 0     | 3.14   |
| Seagate   | ST1000NM0018-2F... | 1 TB   | 36      | 1168  | 1     | 3.14   |
| WDC       | WD3001FAEX-00MJRA0 | 3 TB   | 1       | 1140  | 0     | 3.13   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 27      | 1188  | 1     | 3.12   |
| WDC       | WD2500BHTZ-04JCPV1 | 250 GB | 2       | 1137  | 0     | 3.12   |
| HGST      | HUH728060ALE600    | 6 TB   | 3       | 1136  | 0     | 3.11   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 7       | 1997  | 2     | 3.11   |
| Seagate   | ST3160318AS        | 160 GB | 1       | 2266  | 1     | 3.11   |
| Hitachi   | HDS721050CLA362    | 500 GB | 6       | 1905  | 459   | 3.10   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 10      | 1212  | 1     | 3.10   |
| WDC       | WD5000BMVW-11AJGS4 | 500 GB | 3       | 1129  | 0     | 3.10   |
| WDC       | WD3000HLHX-01JJPV0 | 304 GB | 6       | 1421  | 2     | 3.06   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 8       | 1419  | 2     | 3.05   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 11      | 1396  | 105   | 3.02   |
| WDC       | WD5000BMVV-11GNWS0 | 500 GB | 1       | 1103  | 0     | 3.02   |
| WDC       | WD1003FBYX-12      | 1 TB   | 29      | 1172  | 1     | 3.00   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 35      | 1872  | 30    | 2.98   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 8       | 1133  | 144   | 2.98   |
| WDC       | WD5000BHTZ-04JCPV1 | 500 GB | 6       | 1084  | 0     | 2.97   |
| WDC       | WD3000FYYZ-01UL1B2 | 3 TB   | 9       | 1718  | 3     | 2.95   |
| Toshiba   | DT01ACA200         | 2 TB   | 287     | 1125  | 18    | 2.95   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 3       | 2428  | 732   | 2.95   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 1       | 1075  | 0     | 2.95   |
| HPE       | MB0500GCEHE        | 500 GB | 6       | 1073  | 0     | 2.94   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 45      | 1072  | 20    | 2.94   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 4       | 1065  | 0     | 2.92   |
| HGST      | HUS726040ALA614    | 4 TB   | 19      | 1193  | 4     | 2.92   |
| WDC       | WD5000HHTZ-04N21V1 | 500 GB | 3       | 1064  | 0     | 2.92   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 35      | 1539  | 57    | 2.91   |
| Seagate   | ST8000NM0205-2F... | 8 TB   | 31      | 1151  | 66    | 2.89   |
| HGST      | HUH721008ALE601    | 8 TB   | 6       | 1050  | 0     | 2.88   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 5       | 1580  | 1     | 2.88   |
| WDC       | WD1003FBYZ-010FB0  | 1 TB   | 62      | 1112  | 1     | 2.87   |
| Seagate   | ST3250310AS        | 250 GB | 3       | 2192  | 209   | 2.86   |
| Seagate   | ST4000DX001-1CE168 | 4 TB   | 2       | 1038  | 0     | 2.85   |
| WDC       | WD5003ABYX-01WERA1 | 500 GB | 18      | 1224  | 1     | 2.83   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 22      | 1065  | 1     | 2.83   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 5       | 2518  | 28    | 2.79   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 4       | 1014  | 0     | 2.78   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 40      | 1439  | 17    | 2.77   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 2       | 1112  | 1     | 2.74   |
| Seagate   | ST1000NX0423       | 1 TB   | 1       | 997   | 0     | 2.73   |
| Toshiba   | MG03ACA400         | 4 TB   | 24      | 1455  | 3     | 2.73   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 27      | 1847  | 20    | 2.73   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 5       | 993   | 0     | 2.72   |
| Toshiba   | HDWD120            | 2 TB   | 9       | 993   | 0     | 2.72   |
| Hitachi   | HDS721032CLA362    | 320 GB | 3       | 1673  | 571   | 2.72   |
| WDC       | WD1502FAEX-007BA0  | 1.5 TB | 2       | 1534  | 5     | 2.72   |
| HGST      | HUS726040ALE610    | 4 TB   | 23      | 990   | 0     | 2.71   |
| Samsung   | HD204UI            | 2 TB   | 3       | 1876  | 3     | 2.71   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 16      | 1437  | 459   | 2.71   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 24      | 1688  | 65    | 2.71   |
| HGST      | HUS726040ALE614    | 4 TB   | 13      | 1068  | 3     | 2.71   |
| Seagate   | ST6000NM0235-2A... | 6 TB   | 9       | 984   | 0     | 2.70   |
| HGST      | HUH728080ALE604    | 8 TB   | 17      | 1020  | 10    | 2.69   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 5       | 980   | 0     | 2.69   |
| Seagate   | ST3500413AS        | 500 GB | 3       | 1621  | 22    | 2.68   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 1       | 977   | 0     | 2.68   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 8       | 976   | 0     | 2.67   |
| WDC       | WD4000FYYZ-01UL1B2 | 4 TB   | 25      | 1902  | 89    | 2.67   |
| Seagate   | ST750LX003-1AC154  | 752 GB | 1       | 2921  | 2     | 2.67   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 18      | 1175  | 13    | 2.67   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 6       | 1230  | 1     | 2.66   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 2       | 1651  | 4     | 2.66   |
| WDC       | WD8002FRYZ-01FF2B0 | 8 TB   | 14      | 999   | 1     | 2.65   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 13      | 1171  | 49    | 2.62   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 10      | 953   | 0     | 2.61   |
| MediaMax  | WL2000GSA6472E     | 2 TB   | 1       | 948   | 0     | 2.60   |
| HGST      | HTE721010A9E630    | 1 TB   | 2       | 1767  | 8     | 2.59   |
| Fujitsu   | MHW2120BH          | 120 GB | 1       | 946   | 0     | 2.59   |
| WDC       | WD2003FYYS-27Y2P0  | 2 TB   | 2       | 1374  | 2     | 2.59   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 4       | 2324  | 260   | 2.59   |
| Seagate   | ST380815AS         | 80 GB  | 5       | 944   | 0     | 2.59   |
| Toshiba   | MG04ACA400EY       | 4 TB   | 12      | 940   | 0     | 2.58   |
| WDC       | WD2500AAJS-00VTA0  | 250 GB | 1       | 934   | 0     | 2.56   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 3       | 934   | 0     | 2.56   |
| Toshiba   | MG04ACA400N        | 4 TB   | 6       | 1201  | 2     | 2.55   |
| Toshiba   | MK2035GSS          | 200 GB | 1       | 927   | 0     | 2.54   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 10      | 924   | 0     | 2.53   |
| Seagate   | ST1000DX001-1NS162 | 1 TB   | 6       | 1689  | 219   | 2.53   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 3       | 1242  | 339   | 2.53   |
| MediaMax  | WL500GSA3272       | 500 GB | 1       | 920   | 0     | 2.52   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 23      | 957   | 1     | 2.51   |
| Seagate   | ST32000644NS       | 2 TB   | 11      | 1525  | 11    | 2.51   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 79      | 1007  | 1     | 2.50   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 2       | 911   | 0     | 2.50   |
| HGST      | HUS722T1TALA604    | 1 TB   | 124     | 923   | 10    | 2.50   |
| Toshiba   | HDWD105            | 500 GB | 5       | 907   | 0     | 2.49   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 6       | 906   | 0     | 2.48   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 14      | 1086  | 1     | 2.47   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 31      | 1019  | 2     | 2.45   |
| HGST      | HUH721212ALN600    | 12 TB  | 11      | 1003  | 17    | 2.45   |
| Hitachi   | HDP725025GLA380    | 250 GB | 2       | 4193  | 6     | 2.44   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 48      | 1137  | 10    | 2.43   |
| WDC       | WD2000F9YZ-09N20L1 | 2 TB   | 4       | 886   | 0     | 2.43   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 11      | 927   | 1     | 2.42   |
| HGST      | HUH721010ALN600    | 10 TB  | 16      | 882   | 0     | 2.42   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 8       | 1482  | 8     | 2.41   |
| HGST      | HUS726020ALA610    | 2 TB   | 133     | 936   | 19    | 2.39   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 8       | 871   | 0     | 2.39   |
| WDC       | WD1005FBYZ-01YCBB2 | 1 TB   | 21      | 920   | 1     | 2.39   |
| Samsung   | HD103SI            | 1 TB   | 3       | 3325  | 806   | 2.38   |
| HGST      | HUH721010ALE604    | 10 TB  | 111     | 869   | 0     | 2.38   |
| Toshiba   | DT01ACA050         | 500 GB | 19      | 1005  | 129   | 2.36   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 5       | 1753  | 7     | 2.36   |
| HPE       | MM1000GFJTE        | 1 TB   | 4       | 862   | 0     | 2.36   |
| Seagate   | ST10000NM0016-1... | 10 TB  | 1507    | 1335  | 66    | 2.36   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 4       | 1986  | 4     | 2.35   |
| Toshiba   | MG03ACA200         | 2 TB   | 7       | 920   | 288   | 2.35   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 140     | 870   | 7     | 2.33   |
| Seagate   | ST3400620NS        | 400 GB | 1       | 1695  | 1     | 2.32   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 3       | 846   | 0     | 2.32   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 45      | 873   | 3     | 2.31   |
| HGST      | HUS726040ALA610    | 4 TB   | 68      | 863   | 1     | 2.29   |
| Seagate   | ST3750640AS        | 752 GB | 1       | 2504  | 2     | 2.29   |
| WDC       | WD50EFRX-68L0BN1   | 5 TB   | 6       | 1538  | 118   | 2.27   |
| HPE       | MB0500EBNCR        | 500 GB | 5       | 1525  | 18    | 2.26   |
| Seagate   | ST1000VN002-2EY102 | 1 TB   | 4       | 817   | 0     | 2.24   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 16      | 813   | 0     | 2.23   |
| Seagate   | ST3250318AS        | 250 GB | 3       | 1375  | 17    | 2.22   |
| WDC       | WD5002ABYS-18B1B0  | 500 GB | 1       | 808   | 0     | 2.22   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 40      | 840   | 27    | 2.21   |
| HP        | MB2000GCEHK        | 2 TB   | 2       | 1625  | 1051  | 2.20   |
| Samsung   | HD502HJ            | 500 GB | 2       | 800   | 0     | 2.19   |
| Seagate   | ST2000NM0125-1Y... | 2 TB   | 13      | 800   | 0     | 2.19   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 1       | 799   | 0     | 2.19   |
| Seagate   | ST3120022A         | 120 GB | 1       | 3197  | 3     | 2.19   |
| HPE       | MM1000GBKAL        | 1 TB   | 21      | 1099  | 1     | 2.19   |
| HGST      | HUH728060ALE604    | 6 TB   | 14      | 1198  | 20    | 2.18   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 207     | 816   | 3     | 2.18   |
| Toshiba   | HDWL120            | 2 TB   | 4       | 793   | 0     | 2.17   |
| Seagate   | ST10000NM0196-2... | 10 TB  | 198     | 869   | 37    | 2.17   |
| Seagate   | ST31000NSSUN1.0T   | 1 TB   | 1       | 1574  | 1     | 2.16   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 2       | 1354  | 3     | 2.15   |
| Seagate   | ST3500418AS        | 500 GB | 7       | 789   | 2     | 2.15   |
| WDC       | WD800JD-00HKA0     | 80 GB  | 1       | 776   | 0     | 2.13   |
| WDC       | WD4000F9YZ-09N20L0 | 4 TB   | 4       | 775   | 0     | 2.12   |
| HPE       | MM2000GEFRA        | 2 TB   | 241     | 824   | 1     | 2.11   |
| WDC       | WD2005FBYZ-01YCBB2 | 2 TB   | 40      | 770   | 0     | 2.11   |
| HGST      | HUS726060ALA640    | 6 TB   | 46      | 779   | 1     | 2.11   |
| WDC       | WD4000FYYZ-01UL1B3 | 4 TB   | 23      | 1115  | 16    | 2.11   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 3       | 979   | 1     | 2.10   |
| Seagate   | ST3500312CS        | 500 GB | 10      | 964   | 2     | 2.10   |
| Hitachi   | HUS724040ALE640    | 4 TB   | 22      | 797   | 1     | 2.08   |
| HGST      | HTS721010A9E630    | 1 TB   | 5       | 1455  | 605   | 2.07   |
| HGST      | HUH721008ALE600    | 8 TB   | 46      | 752   | 0     | 2.06   |
| Hitachi   | HDE721050SLA330    | 500 GB | 2       | 3732  | 4     | 2.05   |
| HGST      | HUH721212ALN604    | 12 TB  | 2050    | 770   | 2     | 2.03   |
| WDC       | WD5000AZLX-08K2TA0 | 500 GB | 3       | 733   | 0     | 2.01   |
| Hitachi   | HTS723216L9SA60    | 160 GB | 1       | 727   | 0     | 1.99   |
| WDC       | WD100EFAX-68LHPN0  | 10 TB  | 53      | 733   | 1     | 1.99   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 127     | 791   | 14    | 1.99   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 6       | 722   | 0     | 1.98   |
| Seagate   | ST500DM005 HD502HJ | 500 GB | 1       | 716   | 0     | 1.96   |
| Seagate   | ST2000NM0018-2F... | 2 TB   | 1       | 716   | 0     | 1.96   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 3       | 715   | 0     | 1.96   |
| Seagate   | ST12000DM0007-2... | 12 TB  | 5       | 712   | 0     | 1.95   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 38      | 963   | 210   | 1.93   |
| Seagate   | ST33000651NS       | 3 TB   | 1       | 704   | 0     | 1.93   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 3       | 1027  | 4     | 1.92   |
| Seagate   | ST10000DM0004-2... | 10 TB  | 7       | 990   | 87    | 1.92   |
| Toshiba   | HDWA130            | 3 TB   | 1       | 699   | 0     | 1.92   |
| HGST      | HUS726T6TALE6L4    | 6 TB   | 191     | 710   | 22    | 1.91   |
| WDC       | WD30PURZ-85GU6Y0   | 3 TB   | 2       | 696   | 0     | 1.91   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 27      | 697   | 39    | 1.91   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 173     | 715   | 6     | 1.91   |
| WDC       | WD1003FBYX-01Y7B2  | 1 TB   | 1       | 695   | 0     | 1.91   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 65      | 698   | 1     | 1.89   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 20      | 688   | 0     | 1.89   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 7       | 970   | 21    | 1.88   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 57      | 683   | 0     | 1.87   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 1       | 680   | 0     | 1.86   |
| Seagate   | ST10000NE0004-1... | 10 TB  | 15      | 1217  | 373   | 1.86   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 1       | 679   | 0     | 1.86   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 73      | 696   | 72    | 1.85   |
| Seagate   | ST1000VX005-2EZ102 | 1 TB   | 3       | 672   | 0     | 1.84   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 101     | 734   | 12    | 1.84   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 3       | 668   | 0     | 1.83   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 1       | 667   | 0     | 1.83   |
| Toshiba   | MD04ACA400         | 4 TB   | 440     | 681   | 3     | 1.83   |
| Seagate   | ST10000NM0156-2... | 10 TB  | 37      | 743   | 6     | 1.83   |
| WDC       | WD5000AZLX-35K2TA0 | 500 GB | 3       | 664   | 0     | 1.82   |
| WDC       | WD15EARS-00MVWB0   | 1.5 TB | 4       | 2054  | 324   | 1.81   |
| Seagate   | ST2000NM0055-1V... | 2 TB   | 21      | 900   | 2     | 1.79   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 17      | 712   | 2     | 1.79   |
| Seagate   | ST14000VN0008-2... | 14 TB  | 12      | 653   | 0     | 1.79   |
| Seagate   | ST2000VX003-1HH164 | 2 TB   | 3       | 652   | 0     | 1.79   |
| Seagate   | ST10000VN0004-1... | 10 TB  | 30      | 808   | 110   | 1.78   |
| Toshiba   | MG05ACA800E        | 8 TB   | 666     | 683   | 1     | 1.78   |
| MediaMax  | WL4000GSA6472      | 4 TB   | 2       | 649   | 0     | 1.78   |
| Toshiba   | HDWR21C            | 12 TB  | 5       | 649   | 0     | 1.78   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 1       | 1944  | 2     | 1.78   |
| Seagate   | ST2000NX0253       | 2 TB   | 49      | 832   | 16    | 1.77   |
| Hitachi   | HDS723030ALA640... | 3 TB   | 2       | 975   | 1     | 1.77   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 46      | 662   | 1     | 1.76   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 6       | 1354  | 366   | 1.75   |
| Samsung   | HE103SJ            | 1 TB   | 1       | 637   | 0     | 1.75   |
| Toshiba   | HDWT140            | 4 TB   | 2       | 634   | 0     | 1.74   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 47      | 665   | 18    | 1.73   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 13      | 627   | 0     | 1.72   |
| HP        | MB2000EAZNL        | 2 TB   | 2       | 809   | 2     | 1.72   |
| Toshiba   | HDWU130            | 3 TB   | 8       | 715   | 8     | 1.71   |
| WDC       | WD10JMVW-11AJGS3   | 1 TB   | 1       | 624   | 0     | 1.71   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 8       | 657   | 1     | 1.71   |
| Seagate   | ST12000NM0017-2... | 12 TB  | 2       | 621   | 0     | 1.70   |
| WDC       | WD8003FFBX-68B9AN0 | 8 TB   | 3       | 616   | 0     | 1.69   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 4       | 1982  | 3     | 1.69   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 5       | 614   | 0     | 1.68   |
| WDC       | WD3200AAJS-08L7A0  | 320 GB | 1       | 612   | 0     | 1.68   |
| WDC       | WD121KRYZ-01W0RB0  | 12 TB  | 8       | 812   | 1     | 1.68   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 3       | 609   | 0     | 1.67   |
| HGST      | HUS722T2TALA604    | 2 TB   | 84      | 621   | 1     | 1.66   |
| WDC       | WD10EURX-63UY4Y0   | 1 TB   | 2       | 606   | 0     | 1.66   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 29      | 841   | 22    | 1.66   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 40      | 621   | 29    | 1.65   |
| Toshiba   | HDWD130            | 3 TB   | 8       | 621   | 2     | 1.65   |
| Seagate   | ST3000VX010-2E3166 | 3 TB   | 5       | 595   | 0     | 1.63   |
| Seagate   | ST6000VX001-2BD186 | 6 TB   | 4       | 595   | 0     | 1.63   |
| HGST      | HUH721212ALE604    | 12 TB  | 175     | 598   | 1     | 1.62   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 15      | 717   | 133   | 1.62   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 3       | 583   | 0     | 1.60   |
| WDC       | WD4000FYYZ-01UL1B1 | 4 TB   | 10      | 1633  | 5     | 1.60   |
| Seagate   | ST2000NX0403       | 2 TB   | 7       | 611   | 1     | 1.60   |
| Seagate   | ST2000NX0423       | 2 TB   | 60      | 587   | 1     | 1.59   |
| Toshiba   | HDWE140            | 4 TB   | 42      | 595   | 43    | 1.58   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 1       | 2881  | 4     | 1.58   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 33      | 573   | 0     | 1.57   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 3       | 564   | 0     | 1.55   |
| HPE       | MB004000GWFWB      | 4 TB   | 15      | 564   | 0     | 1.55   |
| HGST      | HUH721212ALE600    | 12 TB  | 64      | 559   | 0     | 1.53   |
| WDC       | WD5000AAKS-65YGA0  | 500 GB | 1       | 556   | 0     | 1.52   |
| Seagate   | ST8000VX0022-2E... | 8 TB   | 4       | 758   | 9     | 1.52   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 19      | 553   | 0     | 1.52   |
| WDC       | WD2003FYYS-05T9B0  | 2 TB   | 4       | 609   | 1     | 1.51   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 3       | 549   | 0     | 1.50   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 1       | 545   | 0     | 1.49   |
| WDC       | WD50EFRX-68MYMN1   | 5 TB   | 2       | 2167  | 4     | 1.49   |
| Toshiba   | HDWN160            | 6 TB   | 10      | 640   | 3     | 1.47   |
| HGST      | HUH721010ALE600    | 10 TB  | 219     | 539   | 1     | 1.47   |
| Seagate   | ST8000DM0004-1Z... | 8 TB   | 10      | 956   | 317   | 1.46   |
| HGST      | HUS726T4TALE6L4    | 4 TB   | 62      | 531   | 0     | 1.46   |
| HGST      | HTS725050A7E630    | 500 GB | 3       | 1123  | 1015  | 1.46   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 2       | 877   | 509   | 1.45   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 35      | 527   | 0     | 1.45   |
| WDC       | WD5000AZLX-22JKKA0 | 500 GB | 3       | 840   | 2     | 1.45   |
| Toshiba   | MG04ACA400E        | 4 TB   | 69      | 532   | 32    | 1.44   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 1       | 523   | 0     | 1.43   |
| Seagate   | ST2000NM0011       | 2 TB   | 14      | 1590  | 143   | 1.43   |
| Toshiba   | MG06ACA10TEY       | 10 TB  | 70      | 541   | 1     | 1.43   |
| Seagate   | ST12000NM0008-2... | 12 TB  | 163     | 521   | 4     | 1.41   |
| Seagate   | ST16000NE000-2R... | 16 TB  | 2       | 511   | 0     | 1.40   |
| WDC       | WD8003FRYZ-01JPDB1 | 8 TB   | 5       | 510   | 0     | 1.40   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 49      | 507   | 1     | 1.38   |
| WDC       | WD3000FYYZ-01UL1B3 | 3 TB   | 5       | 499   | 0     | 1.37   |
| HGST      | HDN728080ALE604    | 8 TB   | 2       | 766   | 16    | 1.36   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 1       | 490   | 0     | 1.34   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 2       | 483   | 0     | 1.32   |
| Seagate   | ST1000NM0011 81... | 1 TB   | 1       | 2394  | 4     | 1.31   |
| WDC       | WD60PURZ-85ZUFY1   | 6 TB   | 6       | 477   | 0     | 1.31   |
| Samsung   | HD322GJ            | 320 GB | 1       | 477   | 0     | 1.31   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 182     | 1159  | 6     | 1.31   |
| Seagate   | ST3750640NS        | 752 GB | 13      | 1262  | 802   | 1.29   |
| Seagate   | ST10000NM0568-2... | 10 TB  | 32      | 468   | 0     | 1.28   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 1       | 465   | 0     | 1.28   |
| Seagate   | ST2000DM005-2CW102 | 2 TB   | 1       | 459   | 0     | 1.26   |
| Seagate   | ST3500514NS        | 500 GB | 4       | 1140  | 10    | 1.26   |
| Seagate   | ST1000NX0313       | 1 TB   | 32      | 1167  | 23    | 1.25   |
| WDC       | WD3200AAKS-00SBA0  | 320 GB | 1       | 2733  | 5     | 1.25   |
| WDC       | WD40EFAX-68JH4N0   | 4 TB   | 38      | 464   | 1     | 1.24   |
| WDC       | WD121KFBX-68EF5N0  | 12 TB  | 7       | 451   | 0     | 1.24   |
| HGST      | HUH721008ALE604    | 8 TB   | 22      | 445   | 0     | 1.22   |
| Seagate   | ST4000NM0115-1Y... | 4 TB   | 87      | 453   | 1     | 1.22   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 8       | 445   | 0     | 1.22   |
| WDC       | WD3200AAJS-40VWA1  | 320 GB | 1       | 443   | 0     | 1.21   |
| Seagate   | ST10000NM0146-2... | 10 TB  | 1       | 441   | 0     | 1.21   |
| Toshiba   | MG07ACA12TEY       | 12 TB  | 52      | 449   | 2     | 1.21   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 1       | 440   | 0     | 1.21   |
| WDC       | WD1005FBYZ-01YCBB3 | 1 TB   | 1       | 438   | 0     | 1.20   |
| Seagate   | ST31000524AS       | 1 TB   | 6       | 1739  | 759   | 1.20   |
| HGST      | HUS726T6TALE6L1    | 6 TB   | 12      | 436   | 0     | 1.20   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 1       | 434   | 0     | 1.19   |
| HPE       | MB001000GWFGF      | 1 TB   | 1       | 431   | 0     | 1.18   |
| Toshiba   | MG06ACA800EY       | 8 TB   | 15      | 430   | 0     | 1.18   |
| Samsung   | HD080HJ            | 80 GB  | 2       | 1964  | 841   | 1.17   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 2       | 1646  | 4     | 1.16   |
| Seagate   | ST2000DX002-2DV164 | 2 TB   | 4       | 424   | 0     | 1.16   |
| Toshiba   | HDWD110            | 1 TB   | 74      | 440   | 49    | 1.16   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 63      | 463   | 22    | 1.16   |
| Toshiba   | MG06ACA10TE        | 10 TB  | 123     | 427   | 1     | 1.16   |
| Seagate   | ST10000VE0008-2... | 10 TB  | 4       | 422   | 0     | 1.16   |
| WDC       | WD3000F9YZ-09N20L1 | 3 TB   | 1       | 419   | 0     | 1.15   |
| WDC       | WD1501FASS-00U0B0  | 1.5 TB | 1       | 3755  | 8     | 1.14   |
| Toshiba   | MG03ACA300         | 3 TB   | 2       | 750   | 6     | 1.14   |
| Toshiba   | MD04ACA50D         | 5 TB   | 1       | 416   | 0     | 1.14   |
| Toshiba   | MG04ACA200N        | 2 TB   | 4       | 458   | 1     | 1.14   |
| Samsung   | HD501LJ            | 500 GB | 3       | 2183  | 676   | 1.14   |
| Seagate   | ST3250312AS        | 250 GB | 3       | 777   | 4     | 1.14   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 137     | 415   | 5     | 1.13   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 14      | 551   | 2     | 1.13   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 20      | 496   | 18    | 1.12   |
| Toshiba   | MG04ACA200E        | 2 TB   | 34      | 406   | 0     | 1.11   |
| WDC       | WD1503FYYS-02W0B0  | 1.5 TB | 2       | 3213  | 7     | 1.10   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 25      | 400   | 0     | 1.10   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 4       | 398   | 0     | 1.09   |
| Toshiba   | HDWQ140            | 4 TB   | 11      | 395   | 0     | 1.08   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 2       | 392   | 0     | 1.08   |
| WDC       | WD5000AZLX-00JKKA0 | 500 GB | 2       | 392   | 0     | 1.08   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 4       | 442   | 1     | 1.07   |
| WDC       | WD4003FRYZ-01F0DB0 | 4 TB   | 29      | 391   | 0     | 1.07   |
| WDC       | WD40EZAZ-00ZGHB0   | 4 TB   | 2       | 388   | 0     | 1.06   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 11      | 506   | 99    | 1.06   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 7       | 386   | 0     | 1.06   |
| HP        | MB2000GCWDA        | 2 TB   | 2       | 383   | 0     | 1.05   |
| Seagate   | ST6000NM021A-2R... | 6 TB   | 84      | 401   | 13    | 1.05   |
| Hitachi   | HTS542512K9SA00    | 120 GB | 1       | 1508  | 3     | 1.03   |
| Seagate   | ST6000NE0021-2E... | 6 TB   | 3       | 1114  | 144   | 1.03   |
| WDC       | WUH721414ALE604    | 14 TB  | 1998    | 376   | 1     | 1.03   |
| HGST      | HUS728T8TALE6L0    | 8 TB   | 15      | 370   | 0     | 1.01   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 2       | 369   | 0     | 1.01   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 2       | 367   | 0     | 1.01   |
| Toshiba   | HDWR160            | 6 TB   | 1       | 364   | 0     | 1.00   |
| Toshiba   | MG06ACA600E        | 6 TB   | 10      | 363   | 0     | 1.00   |
| Seagate   | ST3250823AS        | 250 GB | 1       | 4725  | 12    | 1.00   |
| Seagate   | ST4000NM0033       | 4 TB   | 4       | 362   | 0     | 0.99   |
| Toshiba   | MG07ACA12TE        | 12 TB  | 104     | 374   | 1     | 0.99   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 2       | 361   | 0     | 0.99   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 44      | 473   | 34    | 0.99   |
| WDC       | WD5000AZLX-00K2TA0 | 500 GB | 1       | 358   | 0     | 0.98   |
| WDC       | WD2005FBYZ-01YCBB3 | 2 TB   | 5       | 351   | 0     | 0.96   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 6       | 699   | 185   | 0.94   |
| Seagate   | ST14000NM001G-2... | 14 TB  | 16      | 343   | 0     | 0.94   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 1       | 1714  | 4     | 0.94   |
| WDC       | WD10EALS-002BA0    | 1 TB   | 2       | 2394  | 6     | 0.94   |
| WDC       | WD6003FZBX-00GXAB0 | 6 TB   | 7       | 337   | 0     | 0.92   |
| WDC       | WD20SPZX-00UA7T0   | 2 TB   | 5       | 336   | 0     | 0.92   |
| Seagate   | ST3500411SV        | 500 GB | 1       | 335   | 0     | 0.92   |
| HGST      | HUS726T4TALA6L1    | 4 TB   | 79      | 340   | 1     | 0.91   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 3       | 330   | 0     | 0.91   |
| Hitachi   | HDS721050DLE630    | 500 GB | 4       | 808   | 420   | 0.90   |
| HPE       | MB8000GFECR        | 8 TB   | 56      | 353   | 28    | 0.90   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 14      | 350   | 2     | 0.90   |
| WDC       | WD4000FYYZ-01UL1B0 | 4 TB   | 20      | 2195  | 175   | 0.90   |
| Maxtor    | STM3500320AS       | 500 GB | 2       | 514   | 617   | 0.89   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 2       | 323   | 0     | 0.89   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 85      | 337   | 80    | 0.89   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 5       | 320   | 0     | 0.88   |
| Seagate   | ST8000NE001-2M7101 | 8 TB   | 1       | 317   | 0     | 0.87   |
| Seagate   | ST10000VX0004-1... | 10 TB  | 18      | 317   | 0     | 0.87   |
| Seagate   | ST10000NM0478-2... | 10 TB  | 28      | 336   | 4     | 0.87   |
| Toshiba   | MK2002TSKB         | 2 TB   | 1       | 2835  | 8     | 0.86   |
| Toshiba   | MQ01ACF050         | 500 GB | 5       | 500   | 2     | 0.86   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 196     | 325   | 31    | 0.85   |
| HPE       | MB0500EBZQA        | 500 GB | 1       | 2783  | 8     | 0.85   |
| Seagate   | ST8000VE000-2P6101 | 8 TB   | 1       | 307   | 0     | 0.84   |
| Seagate   | ST31000528AS       | 1 TB   | 4       | 777   | 351   | 0.84   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 7       | 359   | 12    | 0.84   |
| WDC       | WD7500BPVT-22HXZT3 | 752 GB | 1       | 301   | 0     | 0.83   |
| WDC       | WD800BEVS-22RST0   | 80 GB  | 1       | 299   | 0     | 0.82   |
| WDC       | WD101EFAX-68LDBN0  | 10 TB  | 10      | 299   | 0     | 0.82   |
| Seagate   | ST9500420ASG       | 500 GB | 4       | 713   | 19    | 0.81   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 9       | 295   | 0     | 0.81   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 4       | 295   | 0     | 0.81   |
| Seagate   | ST8000VX004-2M1101 | 8 TB   | 5       | 295   | 416   | 0.79   |
| Seagate   | ST9750420AS        | 752 GB | 1       | 285   | 0     | 0.78   |
| Seagate   | ST1000NX0443       | 1 TB   | 22      | 281   | 0     | 0.77   |
| Seagate   | ST31000524NS       | 1 TB   | 20      | 1090  | 107   | 0.77   |
| Seagate   | ST2000NM000A-2J... | 2 TB   | 1       | 281   | 0     | 0.77   |
| WDC       | WD6003FZBX-00K5WB0 | 6 TB   | 13      | 281   | 0     | 0.77   |
| HPE       | MB012000GWDFE      | 12 TB  | 35      | 281   | 0     | 0.77   |
| Seagate   | ST18000NM000J-2... | 18 TB  | 11      | 276   | 0     | 0.76   |
| Seagate   | ST10000DM0004-1... | 10 TB  | 7       | 482   | 453   | 0.76   |
| WDC       | WD1200JS-00NCB1    | 120 GB | 1       | 3027  | 10    | 0.75   |
| Seagate   | ST16000NM001G-2... | 16 TB  | 57      | 273   | 0     | 0.75   |
| Hitachi   | HDS721025CLA382    | 250 GB | 1       | 2454  | 8     | 0.75   |
| WDC       | WD5001AALS-00L3B2  | 500 GB | 2       | 3341  | 515   | 0.74   |
| WDC       | WD3000FYYZ-01UL1B1 | 3 TB   | 1       | 2435  | 8     | 0.74   |
| Seagate   | ST32000542AS       | 2 TB   | 1       | 264   | 0     | 0.73   |
| Seagate   | ST12000NM0248-2... | 12 TB  | 2       | 263   | 0     | 0.72   |
| WDC       | WD102KFBX-68M95N0  | 10 TB  | 32      | 262   | 0     | 0.72   |
| Seagate   | ST4000NM000A-2H... | 4 TB   | 10      | 301   | 1     | 0.71   |
| Seagate   | ST3160815AS        | 160 GB | 3       | 2011  | 183   | 0.71   |
| WDC       | WUS721010ALE6L4    | 10 TB  | 21      | 257   | 11    | 0.70   |
| Hitachi   | HTS545032B9A300    | 320 GB | 1       | 1024  | 3     | 0.70   |
| Seagate   | ST31000524NS 45... | 1 TB   | 2       | 682   | 2     | 0.70   |
| Toshiba   | MG04ACA400NY       | 4 TB   | 3       | 252   | 0     | 0.69   |
| HPE       | MB008000GWRTC      | 8 TB   | 1       | 252   | 0     | 0.69   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 4       | 1203  | 697   | 0.69   |
| WDC       | WD3200AAKS-22B3A0  | 320 GB | 1       | 250   | 0     | 0.69   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 25      | 247   | 0     | 0.68   |
| WDC       | WD1000DHTZ-04N21V0 | 1 TB   | 11      | 328   | 1     | 0.68   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 1       | 246   | 0     | 0.67   |
| WDC       | WD10TMVW-11ZSMS1   | 1 TB   | 1       | 492   | 1     | 0.67   |
| HP        | VB0250EAVER        | 250 GB | 3       | 418   | 205   | 0.67   |
| WDC       | WD10EADS-11P8B1    | 1 TB   | 1       | 2191  | 8     | 0.67   |
| WDC       | WD2003FYYS-70W0B0  | 2 TB   | 1       | 240   | 0     | 0.66   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 1       | 239   | 0     | 0.66   |
| Seagate   | ST3320418AS        | 320 GB | 1       | 239   | 0     | 0.66   |
| Toshiba   | HDWG11A            | 10 TB  | 1       | 235   | 0     | 0.65   |
| WDC       | WD15NMVW-11W68S0   | 1.5 TB | 1       | 233   | 0     | 0.64   |
| Seagate   | ST8000NM000A-2K... | 8 TB   | 51      | 240   | 1     | 0.63   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 2       | 227   | 0     | 0.62   |
| WDC       | WD141KFGX-68FH9N0  | 14 TB  | 12      | 224   | 0     | 0.62   |
| HGST      | HUH721212ALE601    | 12 TB  | 49      | 221   | 0     | 0.61   |
| Apple     | HDD HTS541010A9... | 1 TB   | 1       | 220   | 0     | 0.60   |
| Samsung   | HD252HJ            | 250 GB | 1       | 2827  | 12    | 0.60   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 74      | 249   | 32    | 0.59   |
| Toshiba   | MG04ACA200NY       | 2 TB   | 4       | 215   | 0     | 0.59   |
| Seagate   | ST3160812AS        | 160 GB | 1       | 211   | 0     | 0.58   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 27      | 210   | 0     | 0.58   |
| Seagate   | ST1000NX0423 00... | 1 TB   | 1       | 207   | 0     | 0.57   |
| WDC       | WD6003FRYZ-01F0DB0 | 6 TB   | 27      | 204   | 0     | 0.56   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 1       | 1623  | 7     | 0.56   |
| Toshiba   | MK1252GSX          | 120 GB | 1       | 199   | 0     | 0.55   |
| Seagate   | ST10000NM001G-2... | 10 TB  | 36      | 198   | 0     | 0.54   |
| Toshiba   | HDWG180            | 8 TB   | 8       | 197   | 0     | 0.54   |
| Seagate   | ST12000NM0128-2... | 12 TB  | 18      | 197   | 1     | 0.53   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 2       | 191   | 0     | 0.52   |
| HPE       | MB010000GWRTK      | 10 TB  | 24      | 190   | 0     | 0.52   |
| Toshiba   | MQ01ABB200         | 2 TB   | 1       | 1702  | 8     | 0.52   |
| HP        | MB1000EAMZE        | 1 TB   | 2       | 185   | 0     | 0.51   |
| WDC       | WD62PURZ-85B3AY0   | 6 TB   | 3       | 182   | 0     | 0.50   |
| WDC       | WUH721414ALE6L1    | 14 TB  | 8       | 169   | 0     | 0.46   |
| WDC       | WUH721414ALE6L4    | 14 TB  | 94      | 168   | 1     | 0.46   |
| Seagate   | ST3000NM0005-1V... | 3 TB   | 1       | 166   | 0     | 0.46   |
| Seagate   | ST1000NX0343       | 1 TB   | 2       | 1561  | 10    | 0.45   |
| Toshiba   | HDWL110            | 1 TB   | 1       | 163   | 0     | 0.45   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 1       | 162   | 0     | 0.44   |
| Toshiba   | MQ04UBF100         | 1 TB   | 4       | 161   | 0     | 0.44   |
| Seagate   | ST1000NX0303       | 1 TB   | 3       | 650   | 4     | 0.42   |
| Toshiba   | MQ01ACF032         | 320 GB | 1       | 151   | 0     | 0.41   |
| Maxtor    | STM3200827AS       | 200 GB | 1       | 1203  | 7     | 0.41   |
| WDC       | WD20SPZX-21UA7T0   | 2 TB   | 2       | 150   | 0     | 0.41   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 4       | 1441  | 15    | 0.40   |
| Toshiba   | HDWN180            | 8 TB   | 1       | 146   | 0     | 0.40   |
| WDC       | WD20SPZX-75UA7T1   | 2 TB   | 2       | 143   | 0     | 0.39   |
| Seagate   | ST4000NM002A-2H... | 4 TB   | 65      | 143   | 0     | 0.39   |
| WDC       | WD50EZRZ-00GZ5B1   | 5 TB   | 1       | 141   | 0     | 0.39   |
| Apple     | HDD HTS545050A7... | 500 GB | 1       | 141   | 0     | 0.39   |
| HP        | MB2000EBZQC        | 2 TB   | 1       | 1269  | 8     | 0.39   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 4       | 137   | 0     | 0.38   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 3       | 750   | 44    | 0.37   |
| Seagate   | ST6000VN001-2BB186 | 6 TB   | 8       | 136   | 0     | 0.37   |
| Hitachi   | HDT725025VLA380... | 250 GB | 1       | 135   | 0     | 0.37   |
| Samsung   | HM641JI            | 640 GB | 1       | 132   | 0     | 0.36   |
| Seagate   | ST12000NM001G-2... | 12 TB  | 43      | 132   | 0     | 0.36   |
| Hitachi   | HDS721010DLE630    | 1 TB   | 8       | 1613  | 1436  | 0.34   |
| WDC       | WD20PURZ-85AKKY0   | 2 TB   | 1       | 121   | 0     | 0.33   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 3       | 1796  | 15    | 0.33   |
| HP        | GB0750C4414        | 752 GB | 2       | 3668  | 152   | 0.33   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 19      | 118   | 0     | 0.32   |
| Toshiba   | MQ01ABD100         | 1 TB   | 3       | 553   | 1093  | 0.32   |
| WDC       | WD10EURX-63C57Y0   | 1 TB   | 1       | 1027  | 8     | 0.31   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 1       | 113   | 0     | 0.31   |
| Hitachi   | HTS725016A9A364    | 160 GB | 2       | 1326  | 507   | 0.30   |
| Toshiba   | MG06ACA800E        | 8 TB   | 86      | 108   | 0     | 0.30   |
| WDC       | WD30EFAX-68JH4N0   | 3 TB   | 2       | 249   | 4     | 0.30   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 1       | 952   | 8     | 0.29   |
| Toshiba   | HDWR180            | 8 TB   | 9       | 104   | 0     | 0.29   |
| WDC       | WD1003FBYX-20Y7B0  | 1 TB   | 2       | 102   | 0     | 0.28   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 2       | 507   | 4     | 0.28   |
| WDC       | WD40EFAX-68JH4N1   | 4 TB   | 4       | 100   | 0     | 0.28   |
| WDC       | WD20EZAZ-00L9GB0   | 2 TB   | 3       | 91    | 0     | 0.25   |
| WDC       | WD3200AVVS-56L2B0  | 320 GB | 4       | 91    | 0     | 0.25   |
| Toshiba   | MG08ACA16TEY       | 16 TB  | 4       | 90    | 0     | 0.25   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 1       | 807   | 8     | 0.25   |
| WDC       | WD10SMZW-11Y0TS0   | 1 TB   | 2       | 88    | 0     | 0.24   |
| WDC       | WUH721818ALE604    | 18 TB  | 759     | 87    | 1     | 0.24   |
| Seagate   | ST8000NM012A-2K... | 8 TB   | 73      | 86    | 0     | 0.24   |
| HPE       | MB008000GWJRT      | 8 TB   | 4       | 83    | 0     | 0.23   |
| WDC       | WD20EFAX-68B2RN1   | 2 TB   | 4       | 82    | 0     | 0.23   |
| WDC       | WD1600BEKT-00F3T0  | 160 GB | 2       | 1098  | 146   | 0.22   |
| WDC       | WD2500BEKT-60A25T1 | 250 GB | 1       | 399   | 4     | 0.22   |
| WDC       | WD4000F9YZ-76N20L1 | 4 TB   | 1       | 76    | 0     | 0.21   |
| Seagate   | ST9500325AS        | 500 GB | 2       | 1360  | 69    | 0.20   |
| Seagate   | ST32000641AS       | 2 TB   | 1       | 2235  | 29    | 0.20   |
| Seagate   | ST9160412AS        | 160 GB | 1       | 73    | 0     | 0.20   |
| WDC       | WUH721818ALE6L4    | 18 TB  | 201     | 72    | 0     | 0.20   |
| WDC       | WD102KRYZ-01A5AB0  | 10 TB  | 1       | 70    | 0     | 0.19   |
| Toshiba   | MQ01UBD050         | 500 GB | 1       | 69    | 0     | 0.19   |
| Seagate   | ST980811AS         | 80 GB  | 1       | 348   | 4     | 0.19   |
| Toshiba   | MQ01UBD100         | 1 TB   | 2       | 142   | 8     | 0.19   |
| Toshiba   | MQ04ABF100         | 1 TB   | 2       | 267   | 1010  | 0.18   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 1       | 1641  | 24    | 0.18   |
| WDC       | WD5000LPLX-60ZNTT2 | 500 GB | 1       | 63    | 0     | 0.17   |
| Toshiba   | HDWD240            | 4 TB   | 3       | 61    | 0     | 0.17   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 2       | 60    | 0     | 0.17   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 1       | 60    | 0     | 0.16   |
| Hitachi   | HTS725050A9A362    | 500 GB | 1       | 868   | 14    | 0.16   |
| HGST      | HUH728080ALN600    | 8 TB   | 2       | 96    | 2     | 0.16   |
| WDC       | WD102PURZ-85BXPY0  | 10 TB  | 10      | 56    | 0     | 0.15   |
| Hitachi   | HTS545016B9A300    | 160 GB | 1       | 55    | 0     | 0.15   |
| Hitachi   | HTS545025B9A300    | 250 GB | 1       | 219   | 3     | 0.15   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 1       | 54    | 0     | 0.15   |
| WDC       | WD60EFAX-68JH4N1   | 6 TB   | 2       | 51    | 0     | 0.14   |
| HPE       | MB006000GWKGR      | 6 TB   | 1       | 51    | 0     | 0.14   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 1       | 49    | 0     | 0.14   |
| Seagate   | ST12000NM003G-2... | 12 TB  | 4       | 49    | 0     | 0.14   |
| WDC       | WD80EFBX-68AZZN0   | 8 TB   | 3       | 46    | 0     | 0.13   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 2       | 44    | 0     | 0.12   |
| Seagate   | ST31000340NS       | 1 TB   | 3       | 730   | 354   | 0.12   |
| WDC       | WD20EZRX-19DC0B0   | 2 TB   | 1       | 1541  | 35    | 0.12   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 6       | 1993  | 1022  | 0.12   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 1       | 1522  | 35    | 0.12   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 1       | 38    | 0     | 0.11   |
| Seagate   | ST3640323AS        | 640 GB | 1       | 960   | 24    | 0.11   |
| WDC       | WUH721816ALE6L4    | 16 TB  | 20      | 36    | 0     | 0.10   |
| HPE       | MB006000GWWQT      | 6 TB   | 1       | 36    | 0     | 0.10   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 1       | 2330  | 66    | 0.10   |
| HP        | VB0160EAVEQ        | 160 GB | 1       | 513   | 14    | 0.09   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 2       | 33    | 0     | 0.09   |
| Toshiba   | MG08ACA16TE        | 16 TB  | 6       | 33    | 0     | 0.09   |
| Toshiba   | HDWF180            | 8 TB   | 2       | 33    | 0     | 0.09   |
| Seagate   | ST5000NM0024-1H... | 5 TB   | 1       | 1636  | 49    | 0.09   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 1       | 2202  | 67    | 0.09   |
| Seagate   | ST16000NM003G-2... | 16 TB  | 4       | 30    | 0     | 0.08   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 4       | 30    | 0     | 0.08   |
| WDC       | WD4000FDYZ-27YA5B0 | 4 TB   | 5       | 711   | 115   | 0.08   |
| WDC       | WD10EZEX-00BBHA0   | 1 TB   | 2       | 28    | 0     | 0.08   |
| Apple     | HDD ST1000DM003    | 1 TB   | 1       | 254   | 8     | 0.08   |
| HGST      | HTS541050A9E680    | 500 GB | 1       | 26    | 0     | 0.07   |
| Seagate   | ST6000NM002A-2K... | 6 TB   | 1       | 25    | 0     | 0.07   |
| Toshiba   | MG08ACA16TA        | 16 TB  | 35      | 23    | 0     | 0.07   |
| HP        | MB1000EBZQB        | 1 TB   | 1       | 2073  | 86    | 0.07   |
| Toshiba   | MK5061GSY          | 500 GB | 1       | 22    | 0     | 0.06   |
| HP        | MB1000EBNCF        | 1 TB   | 1       | 1398  | 73    | 0.05   |
| Maxtor    | STM3160215AS       | 160 GB | 1       | 2646  | 142   | 0.05   |
| Seagate   | ST16000NM005G-2... | 16 TB  | 6       | 18    | 0     | 0.05   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 1       | 17    | 0     | 0.05   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 1       | 3625  | 242   | 0.04   |
| WDC       | WD60EZRX-00MVLB1   | 6 TB   | 1       | 1373  | 105   | 0.04   |
| Toshiba   | HDWR11A            | 10 TB  | 1       | 11    | 0     | 0.03   |
| Seagate   | ST16000VN001-2R... | 16 TB  | 1       | 10    | 0     | 0.03   |
| WDC       | WD20SMZW-11JW8S1   | 2 TB   | 1       | 10    | 0     | 0.03   |
| Seagate   | ST1000NC000-1CX162 | 1 TB   | 1       | 2229  | 224   | 0.03   |
| Seagate   | ST3160813AS        | 160 GB | 1       | 1350  | 139   | 0.03   |
| Hitachi   | HDT722525DLA380    | 250 GB | 1       | 3645  | 398   | 0.03   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 2       | 8     | 0     | 0.02   |
| HGST      | HTS725050B7E630    | 500 GB | 4       | 8     | 0     | 0.02   |
| Seagate   | ST18000NE000-2Y... | 18 TB  | 1       | 8     | 0     | 0.02   |
| WDC       | WD10EVVS-63M5B0    | 1 TB   | 1       | 73    | 8     | 0.02   |
| Seagate   | ST9320325AS        | 320 GB | 1       | 348   | 42    | 0.02   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 1       | 960   | 118   | 0.02   |
| Toshiba   | MG08ADA800E        | 8 TB   | 5       | 7     | 0     | 0.02   |
| Seagate   | ST16000NM001J-2... | 16 TB  | 1       | 6     | 0     | 0.02   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 1       | 6     | 0     | 0.02   |
| Seagate   | ST2000DM001-1E6164 | 2 TB   | 1       | 6     | 0     | 0.02   |
| Samsung   | HD502HI            | 500 GB | 3       | 3726  | 807   | 0.02   |
| WDC       | WD20SMZW-11JW8S0   | 2 TB   | 1       | 5     | 0     | 0.01   |
| Seagate   | ST3750330NS        | 752 GB | 1       | 170   | 36    | 0.01   |
| Seagate   | ST31500341AS       | 1.5 TB | 1       | 2761  | 670   | 0.01   |
| WDC       | WD101EFBX-68B0AN0  | 10 TB  | 1       | 3     | 0     | 0.01   |
| Seagate   | ST3160211AS        | 160 GB | 1       | 1802  | 497   | 0.01   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 1       | 113   | 32    | 0.01   |
| Samsung   | HD322HJ            | 320 GB | 1       | 3471  | 1015  | 0.01   |
| HGST      | HTS541010A9E680    | 1 TB   | 1       | 888   | 259   | 0.01   |
| HP        | GJ0250EAGSQ        | 250 GB | 2       | 3080  | 1028  | 0.01   |
| Seagate   | ST31000524NS 43... | 1 TB   | 1       | 2718  | 1138  | 0.01   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 2       | 1527  | 699   | 0.01   |
| Seagate   | ST3000VN007-2AH16M | 3 TB   | 3       | 1     | 0     | 0.01   |
| WDC       | WD1600JS-75NCB2    | 160 GB | 1       | 2854  | 1502  | 0.01   |
| MediaMax  | WL4000GSA6472E     | 4.9 TB | 1       | 1617  | 1054  | 0.00   |
| WDC       | WD5000AADS-00M2B0  | 500 GB | 1       | 2968  | 2023  | 0.00   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 3       | 1335  | 1067  | 0.00   |
| HGST      | HTS541075A9E680    | 752 GB | 1       | 1224  | 1027  | 0.00   |
| Samsung   | SP2004C            | 200 GB | 1       | 1212  | 1105  | 0.00   |
| WDC       | WD2500BEVS-60UST0  | 250 GB | 1       | 400   | 413   | 0.00   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 1       | 998   | 1060  | 0.00   |
| Seagate   | ST9120817AS        | 120 GB | 1       | 3408  | 3854  | 0.00   |
| HGST      | HTS725032A7E630    | 320 GB | 1       | 461   | 538   | 0.00   |
| WDC       | WD2003FYPS-27Y2B0  | 2 TB   | 1       | 1747  | 2073  | 0.00   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 1       | 1638  | 2016  | 0.00   |
| Seagate   | ST3200827AS        | 200 GB | 1       | 1371  | 2268  | 0.00   |
| WDC       | WD10JMVW-11S5XS0   | 1 TB   | 1       | 540   | 1016  | 0.00   |
| HGST      | HTS545050A7E680    | 500 GB | 1       | 362   | 1023  | 0.00   |
| Seagate   | ST3250820AS        | 250 GB | 1       | 957   | 3053  | 0.00   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 1       | 449   | 1509  | 0.00   |
| Seagate   | ST3500320NS        | 500 GB | 2       | 585   | 2573  | 0.00   |
| Seagate   | ST9160821AS        | 160 GB | 1       | 262   | 1011  | 0.00   |
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
| WDC       | Raptor                 | 1      | 1       | 4658  | 0     | 12.76  |
| Hitachi   | Deskstar 7K500         | 1      | 1       | 4456  | 0     | 12.21  |
| Hitachi   | Sun Original           | 1      | 16      | 3909  | 1     | 9.25   |
| Hitachi   | Deskstar 7K1000        | 3      | 18      | 3403  | 15    | 7.97   |
| Samsung   | SpinPoint S250         | 1      | 1       | 2882  | 0     | 7.90   |
| Hitachi   | Deskstar 7K3000        | 5      | 98      | 3000  | 3     | 7.58   |
| Toshiba   | 3.5" DT01ABA Deskto... | 1      | 1       | 2720  | 0     | 7.45   |
| Hitachi   | Ultrastar A7K1000      | 1      | 23      | 2692  | 1     | 7.17   |
| Seagate   | Constellation ES.2 ... | 3      | 108     | 2947  | 24    | 7.14   |
| WDC       | RE2                    | 1      | 5       | 2785  | 1     | 6.66   |
| Seagate   | Constellation ES.2     | 1      | 2       | 2424  | 0     | 6.64   |
| HP        | Seagate Constellati... | 1      | 3       | 2355  | 0     | 6.45   |
| HP        | RE3                    | 1      | 1       | 2228  | 0     | 6.11   |
| WDC       | RE3                    | 12     | 63      | 2744  | 50    | 5.97   |
| Seagate   | NAS HDD                | 3      | 33      | 2301  | 2     | 5.96   |
| HGST      | Deskstar 7K4000        | 1      | 6       | 2140  | 0     | 5.86   |
| Maxtor    | DiamondMax 21          | 3      | 5       | 2475  | 29    | 5.34   |
| Maxtor    | DiamondMax 10 (SATA... | 1      | 2       | 1932  | 0     | 5.29   |
| Hitachi   | Ultrastar 7K3000       | 3      | 67      | 1963  | 3     | 5.19   |
| Hitachi   | Deskstar 7K2000        | 2      | 68      | 2311  | 45    | 5.00   |
| HP        | Seagate Barracuda 7... | 1      | 2       | 2903  | 513   | 4.82   |
| Seagate   | Constellation.2 (SATA) | 3      | 68      | 1847  | 1     | 4.69   |
| Seagate   | Surveillance           | 11     | 50      | 1874  | 2     | 4.66   |
| Seagate   | Constellation ES.3     | 5      | 692     | 2067  | 100   | 4.64   |
| HGST      | MegaScale 4000         | 1      | 17      | 1760  | 15    | 4.59   |
| Seagate   | Enterprise NAS HDD     | 2      | 13      | 1804  | 1     | 4.55   |
| WDC       | Caviar Black           | 22     | 242     | 1947  | 31    | 4.52   |
| HGST      | Ultrastar 7K4000       | 5      | 404     | 1730  | 13    | 4.51   |
| WDC       | RE4-GP                 | 4      | 21      | 2516  | 261   | 4.49   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 2      | 11      | 1848  | 1     | 4.44   |
| Hitachi   | Deskstar 7K1000.B      | 1      | 1       | 1617  | 0     | 4.43   |
| Hitachi   | Deskstar P7K500        | 2      | 5       | 2934  | 3     | 4.42   |
| Samsung   | SpinPoint F1 DT        | 5      | 32      | 2729  | 149   | 4.29   |
| Seagate   | Barracuda 7200.10      | 10     | 24      | 2381  | 191   | 4.29   |
| Hitachi   | Ultrastar A7K2000      | 8      | 91      | 2108  | 51    | 4.26   |
| WDC       | Green                  | 12     | 62      | 1783  | 5     | 4.26   |
| Seagate   | Constellation CS       | 5      | 7       | 2022  | 36    | 4.06   |
| Hitachi   | Deskstar T7K500        | 3      | 7       | 2761  | 5     | 3.99   |
| Seagate   | Barracuda ES           | 6      | 33      | 1791  | 316   | 3.96   |
| Samsung   | SpinPoint P80          | 1      | 1       | 1426  | 0     | 3.91   |
| HGST      | Deskstar NAS           | 6      | 58      | 1432  | 36    | 3.79   |
| WDC       | Caviar Green           | 12     | 29      | 2409  | 212   | 3.76   |
| Seagate   | Barracuda XT           | 2      | 5       | 2310  | 14    | 3.59   |
| Hitachi   | Deskstar 7K1000.C      | 8      | 35      | 2414  | 386   | 3.55   |
| WDC       | Black Mobile           | 6      | 30      | 1495  | 1     | 3.52   |
| Toshiba   | 3.5" MG04ACA Enterp... | 7      | 891     | 1317  | 16    | 3.43   |
| Seagate   | Barracuda 7200.14 (AF) | 16     | 198     | 1606  | 185   | 3.40   |
| WDC       | VelociRaptor           | 13     | 49      | 1374  | 1     | 3.39   |
| WDC       | RE4                    | 21     | 397     | 1502  | 9     | 3.36   |
| HGST      | Ultrastar 7K6000       | 11     | 582     | 1288  | 8     | 3.35   |
| Seagate   | Archive HDD            | 1      | 19      | 1405  | 56    | 3.34   |
| WDC       | Caviar Blue            | 24     | 33      | 1976  | 10    | 3.32   |
| Seagate   | Barracuda Pro          | 1      | 215     | 1259  | 1     | 3.27   |
| MaxDig... | Unknown                | 1      | 1       | 1187  | 0     | 3.25   |
| Samsung   | SpinPoint F3           | 2      | 25      | 2013  | 4     | 3.25   |
| Seagate   | SpinPoint M9T          | 1      | 16      | 1315  | 1     | 3.24   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 1       | 1175  | 0     | 3.22   |
| Seagate   | Desktop HDD.15         | 4      | 155     | 1239  | 23    | 3.19   |
| Seagate   | Enterprise Capacity... | 18     | 4860    | 1431  | 33    | 3.17   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 420     | 1254  | 25    | 3.15   |
| Toshiba   | X300                   | 7      | 134     | 1186  | 14    | 3.11   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 4      | 82      | 1263  | 27    | 3.03   |
| HP        | Proliant HardDrive     | 14     | 25      | 2205  | 279   | 3.01   |
| HGST      | Ultrastar He8          | 5      | 56      | 1167  | 8     | 2.89   |
| Seagate   | Constellation ES (S... | 3      | 50      | 1713  | 85    | 2.82   |
| Toshiba   | S300                   | 2      | 3       | 1006  | 0     | 2.76   |
| Samsung   | SpinPoint F4 EG (AF)   | 1      | 3       | 1876  | 3     | 2.71   |
| Seagate   | Momentus XT (AF)       | 1      | 1       | 2921  | 2     | 2.67   |
| HPE       | WDC Enterprise         | 2      | 11      | 1278  | 8     | 2.63   |
| Seagate   | Desktop SSHD           | 2      | 8       | 1527  | 164   | 2.61   |
| MediaMax  | WL2000                 | 1      | 1       | 948   | 0     | 2.60   |
| HGST      | Travelstar 5K1000      | 4      | 9       | 1180  | 143   | 2.59   |
| Fujitsu   | MHW BH                 | 1      | 1       | 946   | 0     | 2.59   |
| WDC       | Se                     | 7      | 27      | 1131  | 2     | 2.59   |
| WDC       | Red                    | 26     | 907     | 1400  | 9     | 2.58   |
| WDC       | Caviar SE              | 6      | 6       | 1866  | 252   | 2.55   |
| WDC       | RE                     | 18     | 225     | 1542  | 38    | 2.55   |
| Toshiba   | 2.5" HDD               | 1      | 1       | 927   | 0     | 2.54   |
| MediaMax  | WL500                  | 1      | 1       | 920   | 0     | 2.52   |
| WDC       | Black                  | 11     | 448     | 921   | 4     | 2.41   |
| WDC       | Gold                   | 18     | 387     | 918   | 7     | 2.39   |
| Seagate   | Exos X12               | 2      | 142     | 866   | 7     | 2.32   |
| HGST      | Ultrastar 7K2          | 3      | 237     | 844   | 6     | 2.28   |
| Seagate   | Barracuda SpinPoint F3 | 2      | 5       | 1732  | 4     | 2.28   |
| Seagate   | Skyhawk                | 6      | 35      | 848   | 61    | 2.26   |
| WDC       | Blue                   | 55     | 288     | 979   | 24    | 2.25   |
| HGST      | Travelstar 7K1000      | 2      | 7       | 1544  | 434   | 2.22   |
| Seagate   | Barracuda 7200.7 an... | 1      | 1       | 3197  | 3     | 2.19   |
| HPE       | Seagate Constellati... | 1      | 21      | 1099  | 1     | 2.19   |
| Seagate   | Seagate Enterprise     | 1      | 198     | 869   | 37    | 2.17   |
| Seagate   | Sun Internal           | 1      | 1       | 1574  | 1     | 2.16   |
| HGST      | Ultrastar He6          | 1      | 46      | 779   | 1     | 2.11   |
| Seagate   | Pipeline HD 5900.2     | 1      | 10      | 964   | 2     | 2.10   |
| Hitachi   | Travelstar 7K320       | 1      | 1       | 727   | 0     | 1.99   |
| Seagate   | Terascale              | 1      | 6       | 722   | 0     | 1.98   |
| HGST      | Ultrastar DC HC520 ... | 5      | 2349    | 741   | 2     | 1.96   |
| Seagate   | Constellation ES       | 4      | 6       | 1628  | 191   | 1.96   |
| Hitachi   | Ultrastar 7K4000       | 3      | 49      | 826   | 14    | 1.95   |
| Seagate   | SpinPoint M8 (AF)      | 1      | 3       | 1027  | 4     | 1.92   |
| Toshiba   | 3.5" HDD E300          | 1      | 1       | 699   | 0     | 1.92   |
| HPE       | Proliant HardDrive     | 9      | 303     | 731   | 1     | 1.89   |
| Seagate   | Mobile HDD             | 2      | 39      | 940   | 204   | 1.89   |
| Seagate   | Barracuda 3.5          | 2      | 54      | 713   | 20    | 1.87   |
| Toshiba   | 3.5" MD04ACA Enterp... | 2      | 442     | 687   | 3     | 1.85   |
| Toshiba   | L200                   | 2      | 5       | 667   | 0     | 1.83   |
| HGST      | Ultrastar He10         | 6      | 420     | 665   | 1     | 1.82   |
| Hitachi   | Deskstar E7K1000       | 2      | 6       | 2565  | 3     | 1.81   |
| Seagate   | Exos 7E2               | 9      | 147     | 907   | 11    | 1.80   |
| WDC       | Red Pro                | 12     | 136     | 695   | 3     | 1.79   |
| Toshiba   | MG05ACA Enterprise ... | 1      | 666     | 683   | 1     | 1.78   |
| Samsung   | SpinPoint F2 EG        | 3      | 8       | 3114  | 605   | 1.76   |
| Samsung   | SpinPoint F3 RE        | 1      | 1       | 637   | 0     | 1.75   |
| HGST      | Ultrastar HC310/320    | 3      | 302     | 641   | 14    | 1.73   |
| Seagate   | Barracuda Compute      | 2      | 6       | 632   | 0     | 1.73   |
| Toshiba   | V300                   | 1      | 8       | 715   | 8     | 1.71   |
| Seagate   | Barracuda 7200.12      | 8      | 28      | 1175  | 218   | 1.70   |
| Seagate   | Barracuda Green (AF)   | 2      | 8       | 1234  | 402   | 1.68   |
| Seagate   | Exos 7E2000            | 2      | 67      | 590   | 1     | 1.59   |
| Seagate   | IronWolf Pro           | 5      | 22      | 1043  | 274   | 1.58   |
| Seagate   | Barracuda 2.5 5400     | 4      | 116     | 622   | 37    | 1.50   |
| WDC       | Purple                 | 14     | 61      | 537   | 0     | 1.47   |
| WDC       | Elements / My Passport | 12     | 20      | 575   | 51    | 1.47   |
| Seagate   | BarraCuda Pro          | 1      | 10      | 956   | 317   | 1.46   |
| Toshiba   | MG04ACA Enterprise HDD | 4      | 17      | 627   | 1     | 1.43   |
| Toshiba   | P300                   | 5      | 99      | 517   | 37    | 1.38   |
| Seagate   | Constellation ES (S... | 3      | 35      | 1232  | 66    | 1.37   |
| Samsung   | SpinPoint F4           | 1      | 1       | 477   | 0     | 1.31   |
| Seagate   | Exos X14               | 5      | 243     | 467   | 3     | 1.26   |
| Seagate   | BarraCuda 3.5 (CMR)    | 2      | 12      | 578   | 264   | 1.25   |
| Toshiba   | MG07ACA Enterprise ... | 3      | 202     | 459   | 1     | 1.22   |
| MediaMax  | WL4000                 | 2      | 3       | 972   | 352   | 1.19   |
| Samsung   | SpinPoint P80 SD       | 1      | 2       | 1964  | 841   | 1.17   |
| Seagate   | FireCuda 3.5           | 1      | 4       | 424   | 0     | 1.16   |
| Toshiba   | Toshiba Client HDD     | 1      | 1       | 416   | 0     | 1.14   |
| Samsung   | SpinPoint T166         | 1      | 3       | 2183  | 676   | 1.14   |
| WDC       | Scorpio Black          | 4      | 6       | 1074  | 51    | 1.12   |
| HGST      | Travelstar Z7K500      | 2      | 4       | 958   | 896   | 1.09   |
| Seagate   | Barracuda Pro Compute  | 1      | 4       | 398   | 0     | 1.09   |
| Seagate   | IronWolf               | 15     | 456     | 416   | 38    | 1.08   |
| HGST      | Ultrastar DC HC310     | 3      | 228     | 390   | 3     | 1.06   |
| HP        | Constellation ES.3     | 1      | 2       | 383   | 0     | 1.05   |
| Hitachi   | Travelstar 5K250       | 1      | 1       | 1508  | 3     | 1.03   |
| Toshiba   | N300 NAS HDD           | 5      | 31      | 410   | 1     | 1.03   |
| HGST      | Ultrastar DC HC320     | 1      | 15      | 370   | 0     | 1.01   |
| WDC       | Ultrastar DC HC530     | 2      | 2092    | 367   | 1     | 1.00   |
| Seagate   | Barracuda 7200.8       | 1      | 1       | 4725  | 12    | 1.00   |
| Toshiba   | MG06ACA Enterprise ... | 5      | 304     | 361   | 1     | 0.97   |
| Seagate   | BarraCuda 3.5          | 7      | 172     | 406   | 34    | 0.94   |
| Seagate   | Exos 7E8               | 10     | 354     | 378   | 11    | 0.94   |
| WDC       | AV-GP                  | 5      | 9       | 450   | 2     | 0.94   |
| Seagate   | SkyHawk                | 3      | 23      | 334   | 0     | 0.92   |
| WDC       | Blue Mobile            | 12     | 24      | 330   | 0     | 0.91   |
| Maxtor    | DiamondMax 22          | 1      | 2       | 514   | 617   | 0.89   |
| Seagate   | Laptop HDD             | 3      | 9       | 758   | 356   | 0.86   |
| Toshiba   | Toshiba Enterprise     | 1      | 7       | 359   | 12    | 0.84   |
| Seagate   | FireCuda 2.5           | 1      | 4       | 295   | 0     | 0.81   |
| HPE       | Seagate Enterprise     | 3      | 81      | 335   | 19    | 0.79   |
| Toshiba   | 2.5" HDD MQ01ACF       | 2      | 6       | 442   | 2     | 0.79   |
| Seagate   | Momentus 7200.5        | 1      | 1       | 285   | 0     | 0.78   |
| Seagate   | Barracuda LP           | 1      | 1       | 264   | 0     | 0.73   |
| WDC       | Ultrastar DC HC330     | 1      | 21      | 257   | 11    | 0.70   |
| Seagate   | Exos X18               | 2      | 12      | 253   | 0     | 0.69   |
| Seagate   | Momentus 7200.4        | 2      | 5       | 585   | 15    | 0.69   |
| HP        | 250GB SATA disk VB0... | 1      | 3       | 418   | 205   | 0.67   |
| WDC       | Scorpio Blue           | 5      | 6       | 448   | 71    | 0.66   |
| WDC       | Shrek LT 2.5           | 1      | 1       | 233   | 0     | 0.64   |
| Seagate   | Exos X16               | 9      | 172     | 225   | 0     | 0.62   |
| Apple     | Travelstar 5K1000      | 1      | 1       | 220   | 0     | 0.60   |
| Toshiba   | 2.5" HDD MK..52GSX     | 1      | 1       | 199   | 0     | 0.55   |
| Hitachi   | Deskstar 7K1000.D      | 2      | 12      | 1345  | 1097  | 0.53   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 1       | 1702  | 8     | 0.52   |
| WDC       | Ultrastar DC HC500     | 1      | 8       | 169   | 0     | 0.46   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 4       | 161   | 0     | 0.44   |
| Maxtor    | DiamondMax 20          | 1      | 1       | 1203  | 7     | 0.41   |
| WDC       | Green Mobile           | 1      | 4       | 1441  | 15    | 0.40   |
| Apple     | HGST Travelstar Z5K500 | 1      | 1       | 141   | 0     | 0.39   |
| Samsung   | SpinPoint M7E (AF)     | 1      | 1       | 132   | 0     | 0.36   |
| Hitachi   | Travelstar 5K500.B     | 3      | 3       | 433   | 2     | 0.33   |
| Toshiba   | 2.5" HDD MQ01ABD       | 1      | 3       | 553   | 1093  | 0.32   |
| Hitachi   | Travelstar 7K500       | 2      | 3       | 1173  | 343   | 0.25   |
| WDC       | Ultrastar DC HC550     | 3      | 980     | 83    | 1     | 0.23   |
| Seagate   | Barracuda 7200.9       | 3      | 3       | 1128  | 922   | 0.20   |
| Toshiba   | 2.5" HDD MQ01UBD       | 2      | 3       | 118   | 6     | 0.19   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 2       | 267   | 1010  | 0.18   |
| Seagate   | Video 3.5 HDD          | 2      | 2       | 113   | 16    | 0.16   |
| Seagate   | Momentus 5400.6        | 2      | 3       | 1023  | 60    | 0.14   |
| WDC       | HGST Ultrastar He10    | 1      | 1       | 38    | 0     | 0.11   |
| WDC       | Red Plus               | 2      | 4       | 35    | 0     | 0.10   |
| Seagate   | Momentus 5400.3        | 2      | 2       | 305   | 508   | 0.10   |
| Hitachi   | Travelstar 7K100       | 1      | 1       | 2330  | 66    | 0.10   |
| Toshiba   | MG08ACA Enterprise ... | 3      | 45      | 31    | 0     | 0.09   |
| Apple     | Barracuda              | 1      | 1       | 254   | 8     | 0.08   |
| Seagate   | Barracuda ES.2         | 3      | 6       | 588   | 1041  | 0.06   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 1      | 1       | 22    | 0     | 0.06   |
| Seagate   | Barracuda 7200.11      | 3      | 3       | 1690  | 278   | 0.05   |
| Hitachi   | Deskstar T7K250        | 1      | 1       | 3645  | 398   | 0.03   |
| HGST      | Travelstar Z7K500.B    | 1      | 4       | 8     | 0     | 0.02   |
| Toshiba   | MG08                   | 1      | 5       | 7     | 0     | 0.02   |
| Samsung   | SpinPoint P120         | 1      | 1       | 1212  | 1105  | 0.00   |
| Seagate   | Momentus 5400.4        | 1      | 1       | 3408  | 3854  | 0.00   |
| Hitachi   | Deskstar 5K3000        | 1      | 1       | 1638  | 2016  | 0.00   |
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
| Hitachi     | 55     | 508     | 2306  | 78    | 5.08   |
| Maxtor      | 6      | 10      | 1847  | 139   | 3.95   |
| Samsung     | 19     | 79      | 2347  | 184   | 3.31   |
| MaxDigital  | 1      | 1       | 1187  | 0     | 3.25   |
| HP          | 19     | 36      | 2007  | 239   | 3.18   |
| Seagate     | 239    | 8990    | 1280  | 44    | 2.88   |
| Fujitsu     | 1      | 1       | 946   | 0     | 2.59   |
| HGST        | 61     | 4745    | 887   | 7     | 2.34   |
| Toshiba     | 74     | 3398    | 897   | 12    | 2.33   |
| WDC         | 345    | 6593    | 819   | 9     | 1.84   |
| MediaMax    | 4      | 5       | 957   | 211   | 1.74   |
| HPE         | 15     | 416     | 687   | 5     | 1.71   |
| Apple       | 3      | 3       | 205   | 3     | 0.36   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

See full list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Intel     | SSDSA2CW300G3      | 304 GB | 1       | 3503  | 0     | 9.60   |
| Kingston  | SVP100S264G        | 64 GB  | 1       | 3150  | 0     | 8.63   |
| Samsung   | SSD 840 EVO        | 120 GB | 7       | 3119  | 0     | 8.55   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 1       | 3117  | 0     | 8.54   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 3       | 2924  | 0     | 8.01   |
| Samsung   | SSD 840 EVO        | 500 GB | 10      | 3120  | 1     | 7.89   |
| Micron    | MTFDDAK512MAR-1... | 512 GB | 3       | 2870  | 0     | 7.86   |
| SATADOM   | D150SV             | 2 GB   | 1       | 2697  | 0     | 7.39   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 1       | 2611  | 0     | 7.15   |
| Samsung   | MZ-5EA1000-0D3     | 100 GB | 1       | 2597  | 0     | 7.12   |
| OCZ       | AGILITY3           | 240 GB | 1       | 2501  | 0     | 6.85   |
| SanDisk   | SDSSDP064G         | 64 GB  | 1       | 2475  | 0     | 6.78   |
| Samsung   | SSD 830 Series     | 256 GB | 1       | 2440  | 0     | 6.69   |
| OCZ       | VERTEX4            | 256 GB | 1       | 2437  | 0     | 6.68   |
| HP        | VK0480GDPVT        | 480 GB | 1       | 2425  | 0     | 6.65   |
| Micron    | MTFDDAK128MAR-1... | 128 GB | 3       | 2373  | 0     | 6.50   |
| Apple     | SSD SM256E         | 256 GB | 2       | 2325  | 0     | 6.37   |
| HPE       | MK0800GCTZB        | 800 GB | 1       | 2321  | 0     | 6.36   |
| Samsung   | SSD 830 Series     | 512 GB | 12      | 3084  | 253   | 6.33   |
| Intel     | SSDSC2BP240G4      | 240 GB | 11      | 2269  | 0     | 6.22   |
| Intel     | SSDSA2CW120G3      | 120 GB | 41      | 2813  | 53    | 6.15   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 4       | 2197  | 0     | 6.02   |
| Corsair   | Force 3 SSD        | 120 GB | 3       | 2182  | 0     | 5.98   |
| Transcend | TS128GSSD340       | 128 GB | 1       | 2182  | 0     | 5.98   |
| OCZ       | VERTEX3            | 120 GB | 5       | 3677  | 5     | 5.94   |
| Samsung   | SSD 850 PRO        | 128 GB | 7       | 2133  | 0     | 5.85   |
| Intel     | VR0120GEJXL        | 120 GB | 3       | 2118  | 0     | 5.80   |
| Samsung   | MZ7LM120HCFD-00003 | 120 GB | 4       | 2104  | 0     | 5.77   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 4       | 2067  | 0     | 5.66   |
| Samsung   | MZ7KM200HAGR00D3   | 200 GB | 2       | 2062  | 0     | 5.65   |
| Intel     | SSDSC2CW240A3      | 240 GB | 55      | 2171  | 1     | 5.56   |
| Samsung   | MZ7WD480HAGM-00003 | 480 GB | 7       | 2020  | 0     | 5.54   |
| Samsung   | MZ7LM480HCHP-0E003 | 480 GB | 7       | 2019  | 0     | 5.53   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 1       | 2007  | 0     | 5.50   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 2006  | 0     | 5.50   |
| ADATA     | SP600              | 128 GB | 1       | 2000  | 0     | 5.48   |
| Micron    | P400e-MTFDDAK40... | 400 GB | 3       | 1995  | 0     | 5.47   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 4       | 1983  | 0     | 5.43   |
| Plextor   | PX-128M5S          | 128 GB | 1       | 1971  | 0     | 5.40   |
| Samsung   | MZ7TD512HAGM-00000 | 512 GB | 4       | 2275  | 1     | 5.33   |
| Kingston  | SH103S3480G        | 480 GB | 1       | 1943  | 0     | 5.32   |
| Intel     | SSDSA2BZ200G3      | 200 GB | 2       | 2530  | 1     | 5.32   |
| Kingston  | SE50S3480G         | 480 GB | 5       | 1933  | 0     | 5.30   |
| Intel     | SSDSC2CW480A3      | 400 GB | 12      | 2083  | 1     | 5.27   |
| Intel     | SSDSC2BA100G3      | 100 GB | 28      | 2021  | 1     | 5.23   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 2       | 1898  | 0     | 5.20   |
| Micron    | M500DC_MTFDDAK1... | 120 GB | 2       | 1890  | 0     | 5.18   |
| Intel     | SSDSC2BB800G4      | 800 GB | 7       | 1882  | 0     | 5.16   |
| Intel     | SSDSC2CW180A3      | 180 GB | 14      | 1940  | 1     | 5.13   |
| Micron    | MTFDDAK256MAR-1... | 256 GB | 3       | 2481  | 1     | 5.13   |
| Intel     | SSDSC2BB480G4      | 480 GB | 55      | 1977  | 19    | 5.12   |
| Samsung   | SSD 840 EVO        | 1 TB   | 21      | 2369  | 57    | 5.05   |
| Samsung   | MZ7WD480HCGM-00003 | 480 GB | 23      | 1999  | 45    | 5.03   |
| OCZ       | TRION100           | 480 GB | 1       | 1833  | 0     | 5.02   |
| Samsung   | MZ7WD120HCFV-00003 | 120 GB | 1       | 1832  | 0     | 5.02   |
| Crucial   | CT250MX200SSD1     | 250 GB | 11      | 1827  | 0     | 5.01   |
| Samsung   | MZ7KM960HAHP-00005 | 800 GB | 1       | 1822  | 0     | 4.99   |
| Kingston  | SUV300S37A120G     | 120 GB | 1       | 1816  | 0     | 4.98   |
| Intel     | SSDSC2BX012T4      | 1.2 TB | 4       | 1807  | 0     | 4.95   |
| HPE       | MK0240GFDKQ        | 240 GB | 1       | 1803  | 0     | 4.94   |
| Samsung   | MZ7LM1T9HCJM-0E003 | 1.9 TB | 2       | 1785  | 0     | 4.89   |
| Samsung   | MZ7WD240HAFV-000D2 | 240 GB | 7       | 2083  | 5     | 4.88   |
| Intel     | SSDSC2BB120G4      | 120 GB | 17      | 1885  | 1     | 4.88   |
| Samsung   | MZ7LM960HCHP-0E003 | 960 GB | 4       | 1778  | 0     | 4.87   |
| Intel     | SSDSC2CT120A3      | 120 GB | 16      | 2688  | 2     | 4.85   |
| Intel     | SSDSC2CT240A4      | 240 GB | 2       | 2646  | 1     | 4.84   |
| Toshiba   | THNSNJ480PCSZ      | 480 GB | 1       | 1755  | 0     | 4.81   |
| Toshiba   | THNSNJ960PCSZ      | 960 GB | 42      | 1789  | 1     | 4.80   |
| Toshiba   | THNSN8480PCSE      | 480 GB | 1       | 1751  | 0     | 4.80   |
| Intel     | SSDSC2BA400G3C     | 400 GB | 2       | 1733  | 0     | 4.75   |
| Samsung   | SSD 840 EVO        | 250 GB | 7       | 2673  | 7     | 4.74   |
| Samsung   | SSD 850 PRO        | 512 GB | 42      | 1766  | 1     | 4.70   |
| HP        | VK0960GFDKK        | 960 GB | 1       | 1713  | 0     | 4.69   |
| SanDisk   | SDSSDHII960G       | 960 GB | 1       | 1708  | 0     | 4.68   |
| Samsung   | SSD 850 PRO        | 1 TB   | 47      | 2322  | 5     | 4.68   |
| HP        | VK0240GECQN        | 240 GB | 8       | 1701  | 0     | 4.66   |
| Intel     | SSDSC2BB160G4      | 160 GB | 57      | 2007  | 1     | 4.64   |
| Samsung   | MZ7KM960HAHP-00005 | 960 GB | 66      | 1681  | 0     | 4.61   |
| Samsung   | SSD 850 PRO        | 256 GB | 37      | 1734  | 1     | 4.58   |
| Intel     | SSDSC2BB300H4      | 304 GB | 3       | 1663  | 0     | 4.56   |
| Intel     | SSDSC2BA400G3      | 400 GB | 5       | 1660  | 0     | 4.55   |
| Samsung   | MZ7LM480HCHP-00003 | 480 GB | 74      | 1656  | 0     | 4.54   |
| Kingston  | SKC300S37A120G     | 120 GB | 2       | 1656  | 0     | 4.54   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 1       | 1655  | 0     | 4.54   |
| Samsung   | MZ7PD480HAGM-000D3 | 480 GB | 1       | 1653  | 0     | 4.53   |
| HP        | VK0800GDJYA        | 800 GB | 31      | 1754  | 2     | 4.50   |
| Intel     | SSDSC2BB800G6      | 800 GB | 68      | 1732  | 15    | 4.43   |
| Kingston  | SH103S3240G        | 240 GB | 2       | 2144  | 1     | 4.41   |
| Crucial   | CT512MX100SSD1     | 240 GB | 4       | 2010  | 1     | 4.40   |
| Intel     | SSDSC2BB080G6      | 80 GB  | 1       | 1603  | 0     | 4.39   |
| HPE       | MK001920GWCFB      | 1.9 TB | 1       | 1602  | 0     | 4.39   |
| Samsung   | MZ7GE960HMHP-00003 | 960 GB | 16      | 2115  | 142   | 4.38   |
| Intel     | SSDSC2BB012T6      | 1.2 TB | 5       | 1850  | 1     | 4.38   |
| Intel     | SSDSC2BB120G6      | 120 GB | 6       | 1593  | 0     | 4.37   |
| Intel     | SSDSC2BB120G6K     | 120 GB | 24      | 1581  | 0     | 4.33   |
| Samsung   | SSD 840 PRO Series | 128 GB | 17      | 1967  | 77    | 4.31   |
| Intel     | SSDSC2BB300G4      | 304 GB | 1       | 1568  | 0     | 4.30   |
| Intel     | SSDSC2BB240G6      | 240 GB | 19      | 1563  | 0     | 4.28   |
| Intel     | SSDSC2BB016T6      | 1.6 TB | 13      | 1560  | 0     | 4.27   |
| Samsung   | MZ7KM480HAHP-00005 | 480 GB | 82      | 1552  | 0     | 4.25   |
| Intel     | SSDSC2BA200G3      | 200 GB | 15      | 1662  | 1     | 4.17   |
| Kingston  | SVP200S37A120G     | 120 GB | 1       | 1522  | 0     | 4.17   |
| Intel     | SSDSC2BX400G4      | 400 GB | 3       | 1520  | 0     | 4.17   |
| SanDisk   | SDLF1DAR480G-1HHS  | 480 GB | 2       | 1517  | 0     | 4.16   |
| Intel     | SSDSC2BB240G4      | 240 GB | 43      | 1570  | 1     | 4.15   |
| Samsung   | MZ7KM480HAHP-0E005 | 480 GB | 15      | 1498  | 0     | 4.11   |
| Intel     | SSDSC2BW240A3      | 240 GB | 1       | 1489  | 0     | 4.08   |
| SanDisk   | X300 MSATA         | 256 GB | 1       | 1486  | 0     | 4.07   |
| Samsung   | MZ7KM240HAGR-00005 | 240 GB | 19      | 1479  | 0     | 4.05   |
| Samsung   | MZ7KM120HAFD-00005 | 120 GB | 14      | 1476  | 0     | 4.05   |
| Toshiba   | THNSN8240PCSE      | 240 GB | 2       | 1471  | 0     | 4.03   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 23      | 1469  | 0     | 4.03   |
| Intel     | SSDSA2BW600G3D     | 600 GB | 2       | 2200  | 1     | 4.02   |
| Samsung   | MZ7LM1T9HCJM00D3   | 1.9 TB | 4       | 1466  | 0     | 4.02   |
| Samsung   | SSD 840 Series     | 250 GB | 4       | 2709  | 269   | 4.01   |
| Samsung   | MCBQE25G5MPQ-0VAD3 | 25 GB  | 1       | 1456  | 0     | 3.99   |
| Samsung   | SSD 840 PRO Series | 512 GB | 10      | 1941  | 62    | 3.98   |
| Kingston  | SE50S37240G        | 240 GB | 1       | 1450  | 0     | 3.97   |
| Intel     | SSDSC2BB480H4      | 480 GB | 9       | 1611  | 1     | 3.97   |
| Apacer    | AS510S             | 128 GB | 1       | 1444  | 0     | 3.96   |
| Toshiba   | VX500              | 1 TB   | 6       | 1443  | 0     | 3.95   |
| Kingston  | SH103S3120G        | 120 GB | 10      | 1568  | 1     | 3.95   |
| Intel     | SSDSC2BB016T4      | 1.6 TB | 5       | 1634  | 1     | 3.94   |
| Kingston  | SKC300S37A240G     | 240 GB | 12      | 1436  | 0     | 3.93   |
| Crucial   | CT500MX200SSD1     | 500 GB | 16      | 1434  | 0     | 3.93   |
| ADATA     | SP900              | 256 GB | 2       | 2368  | 2     | 3.89   |
| Samsung   | MZ7KM120HAFD-0E005 | 120 GB | 2       | 1394  | 0     | 3.82   |
| SanDisk   | SD7UB2Q512G1022    | 512 GB | 7       | 1498  | 1     | 3.81   |
| Intel     | SSDSC2BB480G6      | 480 GB | 33      | 1384  | 0     | 3.79   |
| SanDisk   | SDLF1CRM-017T-1HST | 1.7 TB | 4       | 1383  | 0     | 3.79   |
| Kingston  | SV300S37A240G      | 240 GB | 101     | 1601  | 9     | 3.78   |
| Intel     | SSDSC2BB600G4      | 600 GB | 11      | 1378  | 0     | 3.78   |
| Lite-On   | PH3-CE120          | 120 GB | 2       | 1376  | 0     | 3.77   |
| Samsung   | MZ7LM120HCFD-00005 | 120 GB | 1       | 1375  | 0     | 3.77   |
| HPE       | MK0200GEYKC        | 200 GB | 21      | 1370  | 0     | 3.75   |
| Crucial   | CT750MX300SSD1     | 752 GB | 16      | 1569  | 1     | 3.74   |
| Lite-On   | PH4-CE120          | 120 GB | 1       | 1352  | 0     | 3.71   |
| SPCC      | SSD                | 240 GB | 1       | 1351  | 0     | 3.70   |
| Samsung   | MZ7KM1T9HAJM-000NU | 1.9 TB | 1       | 1342  | 0     | 3.68   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 14      | 1339  | 0     | 3.67   |
| Intel     | SSDSC2BP480G4      | 480 GB | 1       | 1339  | 0     | 3.67   |
| SanDisk   | SDLF1DAR-960G-1HA2 | 960 GB | 9       | 1339  | 0     | 3.67   |
| Intel     | SSDSC2BX200G4      | 200 GB | 18      | 1334  | 0     | 3.66   |
| Samsung   | MZ7LM960HCHP-00005 | 960 GB | 16      | 1333  | 0     | 3.65   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 1       | 1330  | 0     | 3.65   |
| OCZ       | SABER1000          | 120 GB | 2       | 1309  | 0     | 3.59   |
| Samsung   | SSD 850 EVO        | 120 GB | 15      | 1391  | 15    | 3.58   |
| Samsung   | MZ7KM960HAHP-0E005 | 960 GB | 4       | 1302  | 0     | 3.57   |
| Intel     | SSDSC2BA200G4      | 200 GB | 111     | 1297  | 0     | 3.55   |
| Samsung   | MZ7KM240HMHQ0D3    | 240 GB | 2       | 1295  | 0     | 3.55   |
| Samsung   | MZ7KM960HMJP0D3    | 960 GB | 120     | 1289  | 0     | 3.53   |
| Kingston  | SE50S37100G        | 100 GB | 1       | 1285  | 0     | 3.52   |
| Micron    | 5100_MTFDDAK240TCC | 240 GB | 6       | 1452  | 1     | 3.51   |
| Kingston  | SKC400S37128G      | 128 GB | 4       | 1280  | 0     | 3.51   |
| Intel     | SSDSC2BB150G7      | 150 GB | 12      | 1279  | 0     | 3.51   |
| Samsung   | MZ7LN512HMJP-00000 | 512 GB | 13      | 1414  | 3     | 3.49   |
| Samsung   | MZ7WD960HAGP-00003 | 960 GB | 3       | 1262  | 0     | 3.46   |
| Samsung   | MZ7GE480HMHP-00003 | 480 GB | 12      | 1956  | 165   | 3.45   |
| Kingston  | SE50S3100G         | 100 GB | 3       | 1552  | 1     | 3.43   |
| Kingston  | SUV300S37A240G     | 240 GB | 2       | 1245  | 0     | 3.41   |
| Intel     | SSDSC2BB800G7R     | 800 GB | 40      | 1574  | 53    | 3.41   |
| Crucial   | CT480BX200SSD1     | 480 GB | 1       | 1240  | 0     | 3.40   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 2       | 1239  | 0     | 3.39   |
| SanDisk   | Ultra II           | 960 GB | 12      | 1236  | 0     | 3.39   |
| SPCC      | SSD                | 120 GB | 1       | 1231  | 0     | 3.37   |
| Samsung   | SSD 850 PRO        | 2 TB   | 3       | 1223  | 0     | 3.35   |
| Samsung   | SSD 840 PRO Series | 256 GB | 19      | 2627  | 274   | 3.34   |
| HP        | VK0480GEQNB        | 480 GB | 1       | 1199  | 0     | 3.28   |
| Samsung   | SSD 850 EVO        | 500 GB | 118     | 1266  | 27    | 3.28   |
| SanDisk   | SDLF1CRR019T-1HHS  | 1.9 TB | 30      | 1208  | 34    | 3.28   |
| Samsung   | SSD 750 EVO        | 120 GB | 2       | 1196  | 0     | 3.28   |
| Intel     | SSDSC2BA800G4      | 800 GB | 12      | 1185  | 0     | 3.25   |
| Intel     | SSDSC2KB960G7R     | 960 GB | 10      | 1183  | 0     | 3.24   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 1       | 1181  | 0     | 3.24   |
| OCZ       | VECTOR             | 128 GB | 1       | 2353  | 1     | 3.22   |
| Samsung   | MZ7LM3T8HMLP-00005 | 3.8 TB | 1       | 1176  | 0     | 3.22   |
| Samsung   | MZ7KM1T9HAJM-00005 | 1.9 TB | 50      | 1174  | 0     | 3.22   |
| SanDisk   | SD7UB2Q512G1122    | 512 GB | 6       | 1465  | 2     | 3.21   |
| Samsung   | SSD 850 EVO        | 2 TB   | 8       | 1163  | 0     | 3.19   |
| SK hynix  | HFS500G32TND-N1A2A | 500 GB | 2       | 1146  | 0     | 3.14   |
| Intel     | SSDSC2BX800G4      | 800 GB | 2       | 1142  | 0     | 3.13   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 2       | 1123  | 0     | 3.08   |
| Samsung   | MZ7KM240HAGR-0E005 | 240 GB | 17      | 1671  | 23    | 3.07   |
| Intel     | SSDSC2BA400G4      | 400 GB | 20      | 1120  | 0     | 3.07   |
| SanDisk   | SD6SB1M064G1022I   | 64 GB  | 6       | 1119  | 0     | 3.07   |
| HPE       | LK0480GFJSK        | 480 GB | 1       | 1103  | 0     | 3.02   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 4       | 1101  | 0     | 3.02   |
| Intel     | SSDSC2BA200G4C     | 200 GB | 5       | 1092  | 0     | 2.99   |
| Intel     | SSDSC2BX100G4      | 100 GB | 2       | 1090  | 0     | 2.99   |
| Samsung   | SSD 850 EVO        | 1 TB   | 196     | 1421  | 58    | 2.96   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 2       | 1077  | 0     | 2.95   |
| SanDisk   | SDSSDA960G         | 960 GB | 1       | 1074  | 0     | 2.94   |
| Samsung   | MZ7LM480HCHP-00005 | 480 GB | 25      | 1069  | 0     | 2.93   |
| Intel     | SSDSC2BB240G7      | 240 GB | 21      | 1067  | 0     | 2.92   |
| Toshiba   | THNSN8960PCSE      | 960 GB | 32      | 1066  | 1     | 2.87   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 1       | 1044  | 0     | 2.86   |
| Micron    | 5100_MTFDDAK960TBY | 960 GB | 4       | 1044  | 0     | 2.86   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 5       | 1041  | 0     | 2.85   |
| Samsung   | MZ7LM1T9HCJM-00003 | 1.9 TB | 7       | 1040  | 0     | 2.85   |
| Toshiba   | THNSNJ256GCSU      | 256 GB | 1       | 1036  | 0     | 2.84   |
| Patriot   | Blast              | 240 GB | 1       | 1030  | 0     | 2.82   |
| Samsung   | SSD 850 EVO        | 250 GB | 82      | 1139  | 35    | 2.81   |
| Kingston  | SKC400S37512G      | 512 GB | 5       | 1022  | 0     | 2.80   |
| Samsung   | MZ7LM240HCGR-00005 | 240 GB | 4       | 1018  | 0     | 2.79   |
| Samsung   | MZ7KM960HAHP-0Z005 | 960 GB | 1       | 1004  | 0     | 2.75   |
| Dell      | SSDSCKJB120G7R     | 120 GB | 5       | 1193  | 1     | 2.75   |
| OWC       | Mercury Accelsi... | 240 GB | 1       | 2002  | 1     | 2.74   |
| OCZ       | VERTEX3 MI         | 120 GB | 1       | 2968  | 2     | 2.71   |
| Samsung   | MZ7LM960HCHP-00003 | 960 GB | 31      | 987   | 0     | 2.70   |
| Kingston  | SV300S37A120G      | 120 GB | 38      | 1460  | 9     | 2.70   |
| Kingston  | SHFS37A480G        | 480 GB | 3       | 1378  | 3     | 2.69   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 61      | 977   | 13    | 2.66   |
| Samsung   | MZ7KM1T9HMJP-00005 | 1.9 TB | 81      | 963   | 0     | 2.64   |
| Goodram   | SSD                | 240 GB | 4       | 962   | 0     | 2.64   |
| Intel     | SSDSCKJB150G7      | 150 GB | 14      | 1088  | 1     | 2.63   |
| HP        | VK0240GDJXU        | 240 GB | 2       | 1452  | 1     | 2.62   |
| OCZ       | ARC100             | 480 GB | 4       | 1129  | 21    | 2.59   |
| Kingston  | SKC400S371T        | 1 TB   | 10      | 945   | 0     | 2.59   |
| MyDigi... | SB2                | 128 GB | 6       | 945   | 0     | 2.59   |
| Samsung   | SSD 750 EVO        | 250 GB | 4       | 933   | 0     | 2.56   |
| Intel     | SSDSC2BB480G7      | 480 GB | 107     | 1075  | 1     | 2.55   |
| Samsung   | SSD 840 Series     | 120 GB | 7       | 1862  | 86    | 2.54   |
| HP        | VK000240GWCFD      | 240 GB | 3       | 925   | 0     | 2.53   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 1       | 914   | 0     | 2.50   |
| HP        | VK000480GWJPE      | 480 GB | 1       | 909   | 0     | 2.49   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 151     | 908   | 0     | 2.49   |
| SuperM... | SSD                | 64 GB  | 27      | 930   | 1     | 2.48   |
| Intel     | SSDSC2KG480G7      | 480 GB | 54      | 1131  | 2     | 2.48   |
| Kingston  | SKC400S37256G      | 256 GB | 1       | 902   | 0     | 2.47   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 27      | 898   | 0     | 2.46   |
| Toshiba   | THNSF8800CCSE      | 800 GB | 1       | 896   | 0     | 2.46   |
| HP        | VK000240GWCNP      | 240 GB | 5       | 893   | 0     | 2.45   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 2       | 881   | 0     | 2.41   |
| SanDisk   | SDSSDH3250G        | 250 GB | 1       | 881   | 0     | 2.41   |
| Intel     | SSDSC2BX480G4      | 480 GB | 24      | 871   | 0     | 2.39   |
| Samsung   | MZ7LM960HMJP0D3    | 960 GB | 42      | 903   | 1     | 2.38   |
| Crucial   | CT960M500SSD1      | 960 GB | 18      | 1863  | 7     | 2.37   |
| Seagate   | XF1230-1A0480      | 480 GB | 14      | 864   | 0     | 2.37   |
| SanDisk   | Ultra II           | 480 GB | 15      | 892   | 1     | 2.36   |
| Micron    | M510DC_MTFDDAK4... | 480 GB | 3       | 854   | 0     | 2.34   |
| Intel     | SSDSC2BX016T4      | 1.6 TB | 1       | 849   | 0     | 2.33   |
| Mushkin   | MKNSSDRE120GB      | 120 GB | 1       | 846   | 0     | 2.32   |
| Team      | T2535T120G         | 120 GB | 2       | 846   | 0     | 2.32   |
| Samsung   | MZ7LM960HMJP-00005 | 960 GB | 293     | 1062  | 20    | 2.31   |
| Intel     | SSDSC2MH120A2      | 120 GB | 2       | 842   | 0     | 2.31   |
| HP        | VK0960GFLKK        | 960 GB | 1       | 841   | 0     | 2.31   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 1       | 840   | 0     | 2.30   |
| ADATA     | SU800              | 128 GB | 2       | 836   | 0     | 2.29   |
| Crucial   | CT275MX300SSD1     | 275 GB | 40      | 1026  | 1     | 2.28   |
| Toshiba   | THNSF8200CCSE      | 200 GB | 20      | 914   | 1     | 2.27   |
| Intel     | SSDSC2KG240G7R     | 240 GB | 25      | 877   | 83    | 2.25   |
| AMD       | R3SL120G           | 120 GB | 2       | 812   | 0     | 2.23   |
| Intel     | SSDSA2CW160G3      | 160 GB | 1       | 1623  | 1     | 2.22   |
| Crucial   | CT525MX300SSD1     | 528 GB | 49      | 892   | 1     | 2.22   |
| Intel     | SSDSC2KG240G7      | 240 GB | 42      | 815   | 1     | 2.21   |
| XPG       | SX950U             | 120 GB | 2       | 806   | 0     | 2.21   |
| Apacer    | AS330              | 240 GB | 1       | 799   | 0     | 2.19   |
| Kingston  | SEDC400S37960G     | 960 GB | 9       | 791   | 0     | 2.17   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 10      | 790   | 0     | 2.17   |
| Intel     | SSDMCEAC120B3      | 120 GB | 1       | 788   | 0     | 2.16   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 11      | 787   | 0     | 2.16   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 1       | 782   | 0     | 2.14   |
| Team      | T253X1960G         | 960 GB | 3       | 780   | 0     | 2.14   |
| OWC       | Mercury Electra... | 250 GB | 2       | 774   | 0     | 2.12   |
| Intel     | SSDSC2BB016T7      | 1.6 TB | 61      | 1477  | 4     | 2.12   |
| ADATA     | SP600NS34          | 128 GB | 1       | 772   | 0     | 2.12   |
| SanDisk   | SDSSDA240G         | 240 GB | 2       | 768   | 0     | 2.11   |
| Crucial   | CT256MX100SSD1     | 256 GB | 4       | 1508  | 503   | 2.10   |
| Samsung   | SSD 860 EVO        | 4 TB   | 11      | 766   | 0     | 2.10   |
| SanDisk   | SD7SB7S512G1122    | 512 GB | 1       | 762   | 0     | 2.09   |
| Samsung   | SSD 860 PRO        | 256 GB | 56      | 761   | 0     | 2.09   |
| Samsung   | MZ7GE240HMGR-00003 | 240 GB | 3       | 907   | 119   | 2.08   |
| Samsung   | SSD 860 PRO        | 4 TB   | 14      | 755   | 0     | 2.07   |
| Intel     | SSDSC2BA012T4      | 1.2 TB | 1       | 745   | 0     | 2.04   |
| Intel     | SSDSC2KB240G7      | 240 GB | 64      | 830   | 8     | 2.04   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 28      | 960   | 2     | 2.04   |
| SanDisk   | SDSSDH31000G       | 1 TB   | 1       | 743   | 0     | 2.04   |
| Seagate   | XF1230-1A0240      | 240 GB | 10      | 740   | 0     | 2.03   |
| Toshiba   | TR150              | 960 GB | 1       | 1473  | 1     | 2.02   |
| Toshiba   | THNSF8240CCSE      | 240 GB | 10      | 736   | 0     | 2.02   |
| Micron    | 5100_MTFDDAK1T9TBY | 1.9 TB | 74      | 1272  | 20    | 2.01   |
| Seagate   | XF1230-1A0960      | 960 GB | 2       | 734   | 0     | 2.01   |
| Samsung   | SSD PM851a 2.5 7mm | 1 TB   | 1       | 732   | 0     | 2.01   |
| Micron    | 5100_MTFDDAK480TCC | 480 GB | 18      | 876   | 1     | 2.01   |
| Kingston  | SV300S37A480G      | 480 GB | 11      | 1097  | 39    | 2.01   |
| WDC       | WDS100T2B0A        | 1 TB   | 9       | 730   | 0     | 2.00   |
| Samsung   | MZ7KH3T8HALS-00005 | 3.8 TB | 7       | 727   | 0     | 1.99   |
| Crucial   | CT500BX100SSD1     | 500 GB | 2       | 723   | 0     | 1.98   |
| Intel     | SSDSC2KG960G7      | 960 GB | 46      | 1150  | 4     | 1.98   |
| HP        | VK000480GWSRR      | 480 GB | 4       | 720   | 0     | 1.97   |
| Toshiba   | THNSN81Q92CSE      | 1.9 TB | 7       | 719   | 0     | 1.97   |
| HP        | VK0480GEYJR        | 480 GB | 1       | 715   | 0     | 1.96   |
| Samsung   | SSD 860 DCT 1.92TB | 1.9 TB | 18      | 711   | 0     | 1.95   |
| Intel     | SSDSC2BB480G7R     | 480 GB | 24      | 747   | 1     | 1.95   |
| Micron    | 5200_MTFDDAK1T9TDC | 1.9 TB | 10      | 873   | 2     | 1.94   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 36      | 1032  | 2     | 1.93   |
| Samsung   | SSD 860 PRO        | 2 TB   | 141     | 703   | 0     | 1.93   |
| SuperM... | SSD                | 128 GB | 131     | 721   | 11    | 1.92   |
| Toshiba   | THNSNJ800PCSZ      | 800 GB | 4       | 700   | 0     | 1.92   |
| Samsung   | SSD 860 QVO        | 2 TB   | 25      | 691   | 0     | 1.89   |
| HP        | VK000240GWJPD      | 240 GB | 1       | 686   | 0     | 1.88   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 6       | 682   | 0     | 1.87   |
| Kingston  | SUV500240G         | 240 GB | 4       | 678   | 0     | 1.86   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 1       | 678   | 0     | 1.86   |
| Plextor   | PH6-CE120-L1       | 120 GB | 1       | 674   | 0     | 1.85   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 5       | 666   | 0     | 1.83   |
| Kingston  | SHSS37A240G        | 240 GB | 3       | 661   | 0     | 1.81   |
| Samsung   | MZNLN512HMJP-00000 | 512 GB | 11      | 661   | 0     | 1.81   |
| Intel     | SSDSC2BW120H6      | 120 GB | 4       | 814   | 3     | 1.80   |
| HPE       | MK000240GWEZF      | 240 GB | 10      | 651   | 0     | 1.79   |
| Intel     | SSDSC2BF120A4H     | 120 GB | 2       | 647   | 0     | 1.77   |
| Intel     | SSDSC2BW180A4      | 180 GB | 2       | 644   | 0     | 1.77   |
| Micron    | 5200_MTFDDAK240TDN | 240 GB | 40      | 642   | 0     | 1.76   |
| SuperM... | SSD                | 16 GB  | 29      | 641   | 0     | 1.76   |
| Samsung   | MZ7LM960HMJP-000MV | 960 GB | 4       | 641   | 0     | 1.76   |
| HP        | VK000240GWSRQ      | 240 GB | 15      | 633   | 0     | 1.74   |
| Kingston  | SUV400S37120G      | 120 GB | 12      | 662   | 3     | 1.73   |
| Micron    | 5100_MTFDDAK960TCB | 960 GB | 128     | 960   | 3     | 1.73   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 11      | 777   | 2     | 1.73   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 31      | 728   | 34    | 1.73   |
| HPE       | MK000960GWUGH      | 960 GB | 6       | 704   | 1     | 1.71   |
| Micron    | 5200_MTFDDAK480TDN | 480 GB | 17      | 625   | 0     | 1.71   |
| Micron    | 5100_MTFDDAK480TBY | 480 GB | 15      | 808   | 3     | 1.70   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 1       | 620   | 0     | 1.70   |
| SK hynix  | SC300 2.5 7MM      | 256 GB | 1       | 618   | 0     | 1.69   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 38      | 989   | 53    | 1.69   |
| Kingston  | SA400M8120G        | 120 GB | 3       | 616   | 0     | 1.69   |
| Micron    | 5200_MTFDDAK480TDC | 480 GB | 27      | 623   | 1     | 1.68   |
| SanDisk   | SDLF1CRR-019T-1HA1 | 1.9 TB | 10      | 650   | 1     | 1.67   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 31      | 642   | 1     | 1.67   |
| Kingston  | SUV500M8480G       | 480 GB | 1       | 608   | 0     | 1.67   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 9       | 606   | 0     | 1.66   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 96      | 603   | 0     | 1.65   |
| Samsung   | SSD 860 EVO        | 2 TB   | 102     | 600   | 0     | 1.65   |
| Transcend | TS256GSSD370       | 256 GB | 1       | 596   | 0     | 1.63   |
| Micron    | MTFDDAK480TDN      | 480 GB | 38      | 604   | 1     | 1.62   |
| Kingston  | SM2280S3G2120G     | 120 GB | 1       | 592   | 0     | 1.62   |
| Intel     | SSDSC2BB012T7      | 1.2 TB | 172     | 1087  | 3     | 1.62   |
| Micron    | M500DC_MTFDDAK8... | 800 GB | 27      | 601   | 1     | 1.62   |
| HPE       | MR000240GWFLU      | 240 GB | 2       | 588   | 0     | 1.61   |
| Samsung   | SSD 883 DCT 1.92TB | 1.9 TB | 203     | 589   | 1     | 1.61   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 2       | 585   | 0     | 1.60   |
| Micron    | 5200_MTFDDAK1T9TDD | 1.9 TB | 68      | 645   | 1     | 1.60   |
| Intel     | SSDSC2BB800G7      | 800 GB | 1       | 1164  | 1     | 1.59   |
| Samsung   | SSD 860 PRO        | 1 TB   | 100     | 579   | 0     | 1.59   |
| Phison    | SATA SSD           | 480 GB | 3       | 578   | 0     | 1.59   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 3       | 577   | 0     | 1.58   |
| Kingston  | SV300S37A60G       | 64 GB  | 3       | 1344  | 2     | 1.58   |
| SanDisk   | SDLFOCAM-800G-1HA1 | 800 GB | 1       | 577   | 0     | 1.58   |
| WDC       | HBS3A1996A7E6B1    | 960 GB | 2       | 577   | 0     | 1.58   |
| WDC       | WDS200T2B0A        | 2 TB   | 9       | 575   | 0     | 1.58   |
| Intel     | SSDSC2BB480G7O     | 480 GB | 3       | 1550  | 4     | 1.57   |
| Transcend | TSMSSSD01-240GP    | 240 GB | 4       | 572   | 0     | 1.57   |
| Samsung   | MZ7LH960HAJR-000AZ | 960 GB | 4       | 571   | 0     | 1.57   |
| Samsung   | MZ7LM1T9HMJP-00005 | 1.9 TB | 106     | 895   | 10    | 1.56   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 7       | 569   | 0     | 1.56   |
| Seagate   | XA480ME10063       | 480 GB | 10      | 564   | 0     | 1.55   |
| SK hynix  | SC311 SATA         | 1 TB   | 2       | 563   | 0     | 1.54   |
| Samsung   | SSD 883 DCT        | 960 GB | 30      | 563   | 0     | 1.54   |
| Intel     | SSDSC2BW120A4      | 120 GB | 45      | 715   | 1     | 1.53   |
| SATADOM   | SL 3SE             | 32 GB  | 3       | 556   | 0     | 1.52   |
| Seagate   | XA1920LE10063      | 1.9 TB | 20      | 549   | 0     | 1.51   |
| Micron    | 5200_MTFDDAK3T8TDC | 3.8 TB | 29      | 566   | 1     | 1.50   |
| Samsung   | MZ7LM1T9HMJP0D3    | 1.9 TB | 2       | 547   | 0     | 1.50   |
| HP        | VK0480GFLKH        | 480 GB | 2       | 547   | 0     | 1.50   |
| Kingston  | SUV400S37240G      | 240 GB | 53      | 563   | 1     | 1.50   |
| Samsung   | MZ7LM480HMHQ-00005 | 480 GB | 68      | 1120  | 30    | 1.50   |
| Intel     | SSDSC2KB019T7      | 1.9 TB | 65      | 866   | 4     | 1.49   |
| Samsung   | SSD 845DC PRO      | 800 GB | 4       | 2179  | 3     | 1.49   |
| PNY       | CS900 120GB SSD    | 120 GB | 2       | 543   | 0     | 1.49   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 2       | 542   | 0     | 1.49   |
| SanDisk   | SDSSDHP256G        | 256 GB | 1       | 541   | 0     | 1.48   |
| Samsung   | MZ7KM480HMHQ-000MV | 480 GB | 37      | 539   | 0     | 1.48   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 23      | 539   | 0     | 1.48   |
| Samsung   | SSD 860 EVO        | 500 GB | 284     | 540   | 1     | 1.47   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 2       | 538   | 0     | 1.47   |
| Innodisk  | 2.5" SATA SSD 3ME4 | 128 GB | 1       | 1074  | 1     | 1.47   |
| Micron    | 5200_MTFDDAK960TDD | 960 GB | 133     | 560   | 1     | 1.47   |
| Seagate   | XA960ME10063       | 960 GB | 2       | 535   | 0     | 1.47   |
| Samsung   | MZ7LH240HAHQ0D3    | 240 GB | 6       | 534   | 0     | 1.46   |
| Micron    | 5200_MTFDDAK960TDC | 960 GB | 45      | 567   | 1     | 1.46   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 22      | 1227  | 22    | 1.45   |
| Intel     | SSDSC2KB960G7      | 960 GB | 175     | 1188  | 12    | 1.45   |
| Plextor   | PX-256M6S+         | 256 GB | 2       | 527   | 0     | 1.44   |
| Micron    | MTFDDAK128MBF-1... | 128 GB | 13      | 526   | 0     | 1.44   |
| Intel     | SSDSC2KG019T7R     | 1.9 TB | 15      | 820   | 3     | 1.44   |
| Samsung   | MZ7LM240HMHQ-00005 | 240 GB | 77      | 888   | 134   | 1.44   |
| Seagate   | XA1920ME10063      | 1.9 TB | 35      | 523   | 0     | 1.44   |
| Seagate   | XA240ME10003       | 240 GB | 3       | 522   | 0     | 1.43   |
| Intel     | SSDSC2BW240A4      | 240 GB | 44      | 853   | 6     | 1.42   |
| Kingston  | SUV500960G         | 960 GB | 8       | 518   | 0     | 1.42   |
| Samsung   | MZ7LH960HAJR0D3    | 960 GB | 20      | 512   | 0     | 1.40   |
| Samsung   | MZ7KH240HAHQ-00005 | 240 GB | 54      | 512   | 0     | 1.40   |
| Patriot   | P200               | 2 TB   | 5       | 510   | 0     | 1.40   |
| SanDisk   | SDSSDA480G         | 480 GB | 2       | 509   | 0     | 1.40   |
| HP        | VK0480GFDKH        | 480 GB | 6       | 509   | 0     | 1.40   |
| Samsung   | MZ7KH960HAJR-00005 | 960 GB | 57      | 508   | 0     | 1.39   |
| Toshiba   | THNSF8400CCSE      | 400 GB | 12      | 508   | 0     | 1.39   |
| Intel     | SSDSC2KG240G8R     | 240 GB | 1       | 508   | 0     | 1.39   |
| Crucial   | CT250BX100SSD1     | 250 GB | 1       | 507   | 0     | 1.39   |
| Goodram   | IR-SSDPR-S25A-120  | 120 GB | 7       | 507   | 0     | 1.39   |
| Intel     | SSDSC2KG240G8      | 240 GB | 168     | 503   | 0     | 1.38   |
| Seagate   | ST120FN0021        | 120 GB | 1       | 502   | 0     | 1.38   |
| Samsung   | MZ7LH1T9HMLT-00005 | 1.9 TB | 472     | 501   | 0     | 1.37   |
| Zheino    | CHN 25SATAS3 512   | 512 GB | 1       | 497   | 0     | 1.36   |
| Intel     | SSDSC2BF120A4H SED | 120 GB | 2       | 497   | 0     | 1.36   |
| Intel     | SSDSC2KB480G7      | 480 GB | 41      | 587   | 1     | 1.36   |
| Intel     | SSDSC2KB240G8      | 240 GB | 688     | 516   | 2     | 1.36   |
| Micron    | MTFDDAK960TCB      | 960 GB | 12      | 617   | 1     | 1.36   |
| OCZ       | D2RSTK251E14-0400  | 400 GB | 2       | 495   | 0     | 1.36   |
| Kingston  | SA400S37120G       | 120 GB | 42      | 522   | 1     | 1.35   |
| Plextor   | PX-128S3C          | 128 GB | 1       | 490   | 0     | 1.34   |
| HP        | SSD S700           | 500 GB | 7       | 545   | 1     | 1.34   |
| Micron    | 5200_MTFDDAK1T9TDN | 1.9 TB | 19      | 554   | 1     | 1.34   |
| HPE       | MK001920GWUGK      | 1.9 TB | 2       | 488   | 0     | 1.34   |
| Intel     | SSDSC2KB480G8      | 480 GB | 268     | 499   | 1     | 1.33   |
| SATADOM   | SL 3IE3 V2         | 64 GB  | 4       | 485   | 0     | 1.33   |
| Intel     | SSDSC2BB960G7      | 960 GB | 34      | 909   | 2     | 1.33   |
| Samsung   | SSD 860 QVO        | 1 TB   | 47      | 476   | 0     | 1.30   |
| Samsung   | MZ7LH480HAHQ0D3    | 480 GB | 2       | 475   | 0     | 1.30   |
| Samsung   | SSD 850            | 120 GB | 2       | 474   | 0     | 1.30   |
| Intel     | SSDSC2BB800H4      | 800 GB | 6       | 473   | 0     | 1.30   |
| Patriot   | Burst              | 480 GB | 2       | 472   | 0     | 1.30   |
| Intel     | SSDSA2BW120G3      | 120 GB | 1       | 2358  | 4     | 1.29   |
| Samsung   | SSD 860 EVO        | 1 TB   | 347     | 468   | 1     | 1.28   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 1       | 465   | 0     | 1.28   |
| Intel     | SSDSC2KB960G8      | 960 GB | 803     | 528   | 1     | 1.26   |
| Crucial   | CT120BX500SSD1     | 120 GB | 38      | 460   | 0     | 1.26   |
| HP        | SSD M700           | 120 GB | 2       | 459   | 0     | 1.26   |
| SK hynix  | SC300 M.2 2280     | 256 GB | 1       | 459   | 0     | 1.26   |
| Kingston  | SEDC500M960G       | 960 GB | 14      | 476   | 1     | 1.25   |
| SuperM... | SSD                | 32 GB  | 6       | 457   | 0     | 1.25   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 4       | 456   | 0     | 1.25   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 16      | 487   | 1     | 1.25   |
| Intel     | SSDSCKKB240G8      | 240 GB | 17      | 453   | 0     | 1.24   |
| Kingston  | SA400S37480G       | 480 GB | 32      | 704   | 12    | 1.24   |
| Corsair   | Force LS SSD       | 64 GB  | 2       | 450   | 0     | 1.23   |
| Toshiba   | THNSF8200CAME      | 200 GB | 3       | 447   | 0     | 1.23   |
| Goodram   | SSDPR-CX400-512    | 512 GB | 3       | 446   | 0     | 1.22   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 1       | 440   | 0     | 1.21   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 236     | 559   | 9     | 1.20   |
| Micron    | 1100_MTFDDAK1T0TBN | 1 TB   | 6       | 1224  | 146   | 1.20   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 6       | 589   | 9     | 1.20   |
| HP        | VK000480GWCNQ      | 480 GB | 1       | 433   | 0     | 1.19   |
| Samsung   | MZ7KH1T9HAJR-00005 | 1.9 TB | 109     | 433   | 1     | 1.18   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 3       | 425   | 0     | 1.17   |
| Samsung   | SSD 860 EVO        | 250 GB | 113     | 426   | 1     | 1.16   |
| Patriot   | Burst              | 960 GB | 1       | 423   | 0     | 1.16   |
| HP        | VK001920GWSXK      | 1.9 TB | 35      | 422   | 0     | 1.16   |
| Patriot   | Burst              | 120 GB | 1       | 421   | 0     | 1.16   |
| China     | SATA SSD           | 256 GB | 2       | 421   | 0     | 1.15   |
| HPE       | MK0400GEYKD        | 400 GB | 1       | 421   | 0     | 1.15   |
| Micron    | 5210_MTFDDAK1T9QDE | 1.9 TB | 4       | 419   | 0     | 1.15   |
| PNY       | CS900 240GB SSD    | 240 GB | 1       | 418   | 0     | 1.15   |
| Kingston  | SEDC500R960G       | 960 GB | 1       | 418   | 0     | 1.15   |
| OCZ       | TRION100           | 120 GB | 1       | 417   | 0     | 1.14   |
| Samsung   | SSD 860 QVO        | 4 TB   | 6       | 417   | 0     | 1.14   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 1       | 416   | 0     | 1.14   |
| Micron    | 5300_MTFDDAK960TDS | 960 GB | 139     | 426   | 1     | 1.14   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 114     | 493   | 3     | 1.14   |
| Samsung   | MZ7LM240HMHQ-00003 | 240 GB | 2       | 411   | 0     | 1.13   |
| Gigabyte  | GP-GSTFS30512GTTD  | 512 GB | 2       | 410   | 0     | 1.13   |
| KingDian  | S280               | 240 GB | 3       | 476   | 1     | 1.12   |
| Intel     | SSDSC2KG960G8      | 960 GB | 146     | 464   | 1     | 1.11   |
| Micron    | 5100_MTFDDAK1T9TCB | 1.9 TB | 3       | 1328  | 694   | 1.11   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 4       | 404   | 0     | 1.11   |
| Intel     | SSDSC2CW120A3      | 120 GB | 34      | 2108  | 810   | 1.11   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 1       | 402   | 0     | 1.10   |
| Micron    | 5200_MTFDDAK960TDN | 960 GB | 2       | 401   | 0     | 1.10   |
| Crucial   | CT1000BX100SSD1    | 1 TB   | 1       | 400   | 0     | 1.10   |
| Samsung   | MZ7KH480HAHQ0D3    | 480 GB | 17      | 399   | 0     | 1.10   |
| Micron    | MTFDDAV240TCB      | 240 GB | 13      | 407   | 1     | 1.09   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 33      | 403   | 1     | 1.08   |
| Micron    | MTFDDAV480TDS-1... | 480 GB | 1       | 393   | 0     | 1.08   |
| HP        | SSD S700           | 250 GB | 6       | 392   | 0     | 1.08   |
| Corsair   | Neutron SSD        | 128 GB | 1       | 1955  | 4     | 1.07   |
| Samsung   | MZ7LH960HAJR-00005 | 960 GB | 838     | 390   | 0     | 1.07   |
| Samsung   | MZ7LH480HAHQ-000V3 | 480 GB | 5       | 390   | 0     | 1.07   |
| Micron    | 5100_MTFDDAK1T9TCC | 1.9 TB | 17      | 422   | 1     | 1.07   |
| Intel     | SSDSC2KB480G8R     | 480 GB | 18      | 386   | 0     | 1.06   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 3       | 382   | 0     | 1.05   |
| SPCC      | SSD                | 1 TB   | 1       | 378   | 0     | 1.04   |
| Micron    | 1300_MTFDDAK1T0TDL | 1 TB   | 9       | 414   | 1     | 1.03   |
| Intel     | SSDSC2BW240H6      | 240 GB | 14      | 605   | 25    | 1.03   |
| Micron    | 5100_MTFDDAV240TCB | 240 GB | 12      | 500   | 19    | 1.03   |
| SK hynix  | HFS250G32TND-N1A2A | 250 GB | 10      | 374   | 0     | 1.03   |
| Intel     | SSDSC2BW480H6      | 480 GB | 5       | 639   | 4     | 1.02   |
| Seagate   | XA480LE10063       | 480 GB | 14      | 367   | 0     | 1.01   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 21      | 394   | 1     | 1.01   |
| Intel     | SSDSC2KB480G7R     | 480 GB | 6       | 367   | 0     | 1.01   |
| Samsung   | MZ7WD480HMHP-00003 | 480 GB | 6       | 1987  | 86    | 1.00   |
| ORTIAL    | SSD                | 1 TB   | 12      | 455   | 2     | 1.00   |
| SanDisk   | SSD PLUS           | 480 GB | 23      | 545   | 6     | 1.00   |
| Samsung   | SSD 883 DCT        | 240 GB | 28      | 357   | 0     | 0.98   |
| WDC       | WDS400T2B0A-00SM50 | 4 TB   | 4       | 478   | 1     | 0.98   |
| Samsung   | MZ7LH480HAHQ-00005 | 480 GB | 66      | 352   | 0     | 0.96   |
| China     | 512GB QLC SATA SSD | 512 GB | 6       | 350   | 0     | 0.96   |
| Apacer    | AS340              | 480 GB | 1       | 348   | 0     | 0.96   |
| Micron    | MTFDDAK480TDS-1... | 480 GB | 9       | 392   | 79    | 0.95   |
| Seagate   | XA960LE10063       | 960 GB | 98      | 346   | 0     | 0.95   |
| Micron    | 5100_MTFDDAK960TCC | 960 GB | 9       | 422   | 1     | 0.95   |
| Intel     | SSDSC2KG019T8      | 1.9 TB | 214     | 392   | 1     | 0.94   |
| Kingston  | SVP200S3120G       | 120 GB | 1       | 341   | 0     | 0.94   |
| Samsung   | MZ7KH480HAHQ-00005 | 480 GB | 81      | 340   | 0     | 0.93   |
| Intel     | SSDSC2KG480G8      | 480 GB | 239     | 376   | 1     | 0.93   |
| HPE       | MK000960GXAXB      | 960 GB | 5       | 339   | 0     | 0.93   |
| Samsung   | SSD 883 DCT 3.84TB | 3.8 TB | 138     | 338   | 0     | 0.93   |
| Samsung   | MZ7LH1T9HALT0D3    | 1.9 TB | 35      | 338   | 0     | 0.93   |
| Lite-On   | L8H-128V2G-HP      | 128 GB | 2       | 335   | 0     | 0.92   |
| BIWIN     | SSD                | 256 GB | 1       | 332   | 0     | 0.91   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 1       | 328   | 0     | 0.90   |
| Patriot   | Burst              | 240 GB | 10      | 327   | 0     | 0.90   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 376     | 321   | 0     | 0.88   |
| Samsung   | MZ7LH7T6HMLA-00005 | 7.6 TB | 125     | 320   | 0     | 0.88   |
| SanDisk   | SDSSDA120G         | 120 GB | 3       | 317   | 0     | 0.87   |
| Micron    | 5300_MTFDDAK1T9TDT | 1.9 TB | 109     | 330   | 1     | 0.87   |
| Crucial   | CT240BX500SSD1     | 240 GB | 30      | 316   | 0     | 0.87   |
| ADATA     | SP580              | 120 GB | 2       | 990   | 505   | 0.86   |
| SanDisk   | pSSD               | 32 GB  | 1       | 314   | 0     | 0.86   |
| Mushkin   | MKNSSDRE960GB      | 960 GB | 5       | 514   | 2     | 0.85   |
| HPE       | MK000480GWXFF      | 480 GB | 13      | 311   | 0     | 0.85   |
| HPE       | MK001920GWJPQ      | 1.9 TB | 18      | 555   | 6     | 0.85   |
| Mushkin   | MKNSSDRE500GB      | 500 GB | 1       | 308   | 0     | 0.84   |
| Dell      | SSDSCKKB240G8R     | 240 GB | 12      | 306   | 0     | 0.84   |
| Maxtor    | Z1 SSD             | 240 GB | 1       | 302   | 0     | 0.83   |
| Micron    | 5100_MTFDDAK480TCB | 480 GB | 24      | 961   | 140   | 0.83   |
| Intel     | SSDSC2KB019T7R     | 1.9 TB | 23      | 417   | 2     | 0.82   |
| Kingston  | SQ500S37480G       | 480 GB | 1       | 297   | 0     | 0.81   |
| ADATA     | SP550              | 240 GB | 2       | 295   | 0     | 0.81   |
| Crucial   | CT960BX500SSD1     | 960 GB | 8       | 295   | 0     | 0.81   |
| SPCC      | SSD                | 512 GB | 6       | 294   | 0     | 0.81   |
| SanDisk   | SSD G5 BICS4       | 1 TB   | 5       | 322   | 1     | 0.80   |
| Crucial   | CT240M500SSD1      | 240 GB | 11      | 1997  | 258   | 0.79   |
| Samsung   | MZ7KH960HAJR0D3    | 960 GB | 160     | 287   | 0     | 0.79   |
| Transcend | TS128GSSD370       | 128 GB | 3       | 286   | 0     | 0.79   |
| Kingston  | SA400S37960G       | 960 GB | 8       | 286   | 0     | 0.78   |
| KingSpec  | MT-128             | 128 GB | 1       | 281   | 0     | 0.77   |
| China     | SH00R480GB         | 480 GB | 2       | 510   | 4     | 0.77   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 9       | 279   | 0     | 0.76   |
| Samsung   | SSD 883 DCT        | 480 GB | 7       | 278   | 0     | 0.76   |
| Kingston  | SEDC500R1920G      | 1.9 TB | 45      | 373   | 1     | 0.75   |
| Intel     | SSDSC2BW120A3F     | 120 GB | 20      | 2107  | 917   | 0.75   |
| SanDisk   | SSD PLUS           | 240 GB | 19      | 283   | 1     | 0.74   |
| Intel     | SSDSC2BW256H6      | 256 GB | 1       | 268   | 0     | 0.74   |
| Intel     | SSDSCKJB240G7      | 240 GB | 3       | 267   | 0     | 0.73   |
| Micron    | MTFDDAK480TDS      | 480 GB | 8       | 267   | 0     | 0.73   |
| Intel     | SSDSC2KB960G8R     | 960 GB | 7       | 267   | 0     | 0.73   |
| Crucial   | CT500MX500SSD1     | 500 GB | 121     | 327   | 3     | 0.73   |
| Intel     | SSDSC2BW080A4      | 80 GB  | 1       | 1589  | 5     | 0.73   |
| Micron    | 1100 SATA          | 256 GB | 1       | 264   | 0     | 0.72   |
| HPE       | VR000240GXBBL      | 240 GB | 2       | 264   | 0     | 0.72   |
| ADATA     | SP550              | 120 GB | 3       | 446   | 166   | 0.72   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 8       | 262   | 0     | 0.72   |
| Kingston  | SEDC500R480G       | 480 GB | 9       | 259   | 0     | 0.71   |
| Kingston  | SEDC500M1920G      | 1.9 TB | 36      | 280   | 1     | 0.70   |
| Toshiba   | THNSF81D60CSE      | 1.6 TB | 10      | 253   | 0     | 0.69   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 132     | 303   | 4     | 0.69   |
| Kingston  | SHFS37A240G        | 240 GB | 1       | 248   | 0     | 0.68   |
| Intel     | SSDSC2KG019T7      | 1.9 TB | 1       | 243   | 0     | 0.67   |
| KingSpec  | P4-960             | 960 GB | 2       | 239   | 0     | 0.66   |
| Toshiba   | KHK61RSE960G       | 960 GB | 67      | 239   | 0     | 0.66   |
| SanDisk   | SSD PLUS           | 120 GB | 24      | 260   | 1     | 0.65   |
| Micron    | 5300_MTFDDAV240TDS | 240 GB | 6       | 238   | 0     | 0.65   |
| Crucial   | CT250MX500SSD1     | 250 GB | 61      | 259   | 1     | 0.65   |
| Gigabyte  | GP-GSTFS31480GNTD  | 480 GB | 1       | 238   | 0     | 0.65   |
| Samsung   | SSD 860 PRO        | 512 GB | 64      | 237   | 0     | 0.65   |
| Kingston  | SEDC500M480G       | 480 GB | 10      | 255   | 1     | 0.64   |
| Toshiba   | THNSFJ256GDNU      | 256 GB | 1       | 232   | 0     | 0.64   |
| Kingston  | SA400S37240G       | 240 GB | 66      | 233   | 1     | 0.64   |
| Micron    | 5300_MTFDDAK7T6TDS | 7.6 TB | 11      | 230   | 0     | 0.63   |
| Phison    | SATA SSD           | 960 GB | 4       | 230   | 0     | 0.63   |
| Transcend | TS480GSSD220S      | 480 GB | 4       | 320   | 2     | 0.63   |
| Transcend | TSMSSSD01-120GP    | 120 GB | 2       | 227   | 0     | 0.62   |
| ADATA     | SU630              | 960 GB | 1       | 676   | 2     | 0.62   |
| HP        | VK000960GWTTB      | 960 GB | 11      | 225   | 0     | 0.62   |
| Samsung   | SSD 870 QVO        | 8 TB   | 35      | 223   | 0     | 0.61   |
| Crucial   | CT1000BX500SSD1    | 1 TB   | 20      | 236   | 1     | 0.60   |
| SanDisk   | SDSA5GK-016G-1006  | 16 GB  | 1       | 219   | 0     | 0.60   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 1       | 219   | 0     | 0.60   |
| Phison    | SATA SSD           | 64 GB  | 9       | 218   | 0     | 0.60   |
| Micron    | M510DC_MTFDDAK9... | 960 GB | 1       | 1953  | 8     | 0.59   |
| Micron    | 5300_MTFDDAK3T8TDS | 3.8 TB | 29      | 265   | 2     | 0.59   |
| Apacer    | AS340              | 960 GB | 43      | 322   | 20    | 0.59   |
| WDC       | WDS200T1R0A-68A4W0 | 2 TB   | 15      | 209   | 0     | 0.58   |
| Crucial   | CT120BX100SSD1     | 120 GB | 1       | 209   | 0     | 0.57   |
| Samsung   | MZ7LH3T8HMLT-00005 | 3.8 TB | 63      | 206   | 0     | 0.57   |
| Intel     | SSDSC2KW128G8      | 128 GB | 9       | 219   | 2     | 0.57   |
| Samsung   | MZ7WD960HMHP-00003 | 960 GB | 4       | 2167  | 43    | 0.55   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 1       | 2595  | 12    | 0.55   |
| Micron    | MTFDDAV240TDU      | 240 GB | 6       | 199   | 0     | 0.55   |
| THU       | SSD 240G           | 240 GB | 1       | 197   | 0     | 0.54   |
| Micron    | MTFDDAK960TDT      | 960 GB | 8       | 196   | 0     | 0.54   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 1       | 786   | 3     | 0.54   |
| Samsung   | MZ7KM120HAFD-000FU | 120 GB | 1       | 195   | 0     | 0.54   |
| Micron    | 5300_MTFDDAK480TDT | 480 GB | 4       | 194   | 0     | 0.53   |
| Micron    | 5300_MTFDDAK480TDS | 480 GB | 13      | 194   | 0     | 0.53   |
| Samsung   | MZ7LM960HCHP-000MV | 960 GB | 6       | 192   | 0     | 0.53   |
| Samsung   | MZ7LH480HBHQ0D3    | 480 GB | 9       | 189   | 0     | 0.52   |
| HP        | VK000480GWTTA      | 480 GB | 6       | 188   | 0     | 0.52   |
| SanDisk   | SDSSDH3 2T00       | 2 TB   | 6       | 209   | 1     | 0.51   |
| Intel     | SSDSC2KG960G8R     | 960 GB | 16      | 245   | 2     | 0.51   |
| Intel     | SSDSC2KG038T8      | 3.8 TB | 10      | 227   | 1     | 0.51   |
| Kingston  | SEDC450R480G       | 480 GB | 1       | 182   | 0     | 0.50   |
| Crucial   | CT960BX200SSD1     | 960 GB | 1       | 181   | 0     | 0.50   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 1       | 181   | 0     | 0.50   |
| China     | SATA SSD           | 240 GB | 5       | 180   | 0     | 0.49   |
| Intel     | SSDSC2KB038T8      | 3.8 TB | 24      | 233   | 1     | 0.49   |
| SPCC      | SSD                | 256 GB | 3       | 178   | 0     | 0.49   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 3       | 177   | 0     | 0.49   |
| WDC       | WDS250G2B0A        | 250 GB | 2       | 176   | 0     | 0.48   |
| SK hynix  | SHGS31-1000GS-2    | 1 TB   | 23      | 175   | 0     | 0.48   |
| Intel     | SSDSCKKI256G8      | 256 GB | 1       | 173   | 0     | 0.47   |
| Maxtor    | Z1 SSD             | 960 GB | 2       | 172   | 0     | 0.47   |
| HP        | VK000960GWTHB      | 960 GB | 3       | 172   | 0     | 0.47   |
| ADATA     | SU800              | 256 GB | 1       | 172   | 0     | 0.47   |
| Samsung   | MZNLH1T0HALB-00000 | 1 TB   | 10      | 167   | 0     | 0.46   |
| Kingston  | SEDC400S37480G     | 480 GB | 1       | 166   | 0     | 0.46   |
| China     | SATA SSD           | 480 GB | 3       | 166   | 0     | 0.46   |
| Samsung   | SSD 870 EVO        | 4 TB   | 2       | 165   | 0     | 0.45   |
| ADATA     | SU750              | 512 GB | 4       | 163   | 0     | 0.45   |
| Phison    | SATA SSD           | 32 GB  | 1       | 161   | 0     | 0.44   |
| Micron    | MTFDDAK960TDS      | 960 GB | 16      | 160   | 0     | 0.44   |
| Apacer    | 480GB SATA Flas... | 480 GB | 3       | 157   | 0     | 0.43   |
| Samsung   | SSD 750 EVO        | 500 GB | 1       | 157   | 0     | 0.43   |
| Intenso   | SSD                | 128 GB | 2       | 156   | 0     | 0.43   |
| HPE       | VR000480GWFMD      | 480 GB | 1       | 154   | 0     | 0.42   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 327     | 183   | 3     | 0.42   |
| Micron    | 5300_MTFDDAK960TDT | 960 GB | 36      | 151   | 0     | 0.41   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 1       | 147   | 0     | 0.40   |
| SanDisk   | SSD PLUS           | 1 TB   | 1       | 294   | 1     | 0.40   |
| Intel     | SSDSC2BF180A4      | 180 GB | 2       | 243   | 2     | 0.40   |
| ADATA     | SU800              | 2 TB   | 4       | 250   | 1     | 0.40   |
| ADATA     | SU650              | 120 GB | 4       | 146   | 0     | 0.40   |
| Micron    | 5210_MTFDDAK3T8QDE | 3.8 TB | 67      | 148   | 3     | 0.38   |
| Micron    | 1300_MTFDDAK512TDL | 512 GB | 116     | 138   | 0     | 0.38   |
| Team      | T253X6001T         | 1 TB   | 4       | 137   | 0     | 0.38   |
| Kingston  | SEDC500R3840G      | 3.8 TB | 36      | 173   | 1     | 0.38   |
| Samsung   | SSD 870 EVO        | 250 GB | 2       | 136   | 0     | 0.37   |
| Kingston  | SKC6001024G        | 1 TB   | 2       | 136   | 0     | 0.37   |
| HP        | VK0480GEPQP        | 480 GB | 4       | 135   | 0     | 0.37   |
| Crucial   | CT240BX200SSD1     | 240 GB | 1       | 133   | 0     | 0.37   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 1       | 125   | 0     | 0.34   |
| Crucial   | CT480BX500SSD1     | 480 GB | 24      | 125   | 0     | 0.34   |
| Intel     | SSDSC2BF240A4H     | 240 GB | 1       | 622   | 4     | 0.34   |
| WDC       | WDS100T1R0A-68A4W0 | 1 TB   | 3       | 120   | 0     | 0.33   |
| Toshiba   | KHK61RSE1T92       | 1.9 TB | 33      | 119   | 0     | 0.33   |
| Micron    | 5300_MTFDDAK1T9TDS | 1.9 TB | 48      | 118   | 0     | 0.33   |
| Team      | T253X1480G         | 480 GB | 1       | 118   | 0     | 0.33   |
| Intel     | SSDSC2KW256G8      | 256 GB | 24      | 142   | 6     | 0.32   |
| Crucial   | CT250MX500SSD4     | 250 GB | 4       | 117   | 0     | 0.32   |
| Micron    | MTFDDAK1T9TDD      | 1.9 TB | 3       | 116   | 0     | 0.32   |
| Crucial   | CT1024M550SSD1     | 1 TB   | 5       | 2364  | 188   | 0.30   |
| WDC       | WDS400T1R0A-68A4W0 | 4 TB   | 3       | 110   | 0     | 0.30   |
| PNY       | CS900 250GB SSD    | 250 GB | 10      | 109   | 0     | 0.30   |
| WDC       | WDS250G2B0B        | 250 GB | 2       | 108   | 0     | 0.30   |
| Kingston  | SUV500M8240G       | 240 GB | 3       | 108   | 0     | 0.30   |
| Patriot   | P210               | 1 TB   | 4       | 107   | 0     | 0.30   |
| Samsung   | SSD 860 DCT        | 960 GB | 2       | 106   | 0     | 0.29   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 1       | 2863  | 26    | 0.29   |
| Intel     | SSDSCKKW128G8      | 128 GB | 3       | 103   | 0     | 0.28   |
| Intel     | SSDSC2KG019T8R     | 1.9 TB | 25      | 100   | 0     | 0.27   |
| Micron    | MTFDDAK960TDD      | 960 GB | 14      | 99    | 0     | 0.27   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 1       | 99    | 0     | 0.27   |
| SK hynix  | SC311 SATA         | 256 GB | 1       | 97    | 0     | 0.27   |
| Micron    | MTFDDAK960TDS-1... | 960 GB | 2       | 95    | 0     | 0.26   |
| Micron    | 5300_MTFDDAK3T8TDT | 3.8 TB | 16      | 122   | 3     | 0.26   |
| Intel     | SSDSC2KW512G8      | 512 GB | 6       | 123   | 3     | 0.26   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 1       | 261   | 2     | 0.24   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 1       | 84    | 0     | 0.23   |
| Micron    | MTFDDAV256TDL      | 256 GB | 5       | 143   | 2     | 0.23   |
| SanDisk   | SDSSDH3512G        | 512 GB | 2       | 82    | 0     | 0.23   |
| SATADOM   | SH Type D 3TE7     | 120 GB | 5       | 75    | 0     | 0.21   |
| Samsung   | SSD 870 QVO        | 1 TB   | 16      | 75    | 0     | 0.21   |
| ADATA     | SU800              | 1 TB   | 2       | 74    | 0     | 0.21   |
| Kingston  | SEDC500M3840G      | 3.8 TB | 6       | 89    | 1     | 0.20   |
| Transcend | TS1TSSD370S        | 1 TB   | 1       | 296   | 3     | 0.20   |
| Phison    | SATA SSD           | 1 TB   | 6       | 72    | 0     | 0.20   |
| Intel     | SSDSCKKB960G8      | 960 GB | 1       | 72    | 0     | 0.20   |
| Smartbuy  | SSD                | 960 GB | 1       | 70    | 0     | 0.19   |
| HPE       | MK000480GWUGF      | 480 GB | 2       | 69    | 0     | 0.19   |
| Samsung   | SSD 870 EVO        | 500 GB | 8       | 69    | 0     | 0.19   |
| Micron    | MTFDDAK1T0TDL      | 1 TB   | 21      | 70    | 1     | 0.19   |
| ADATA     | SU800              | 512 GB | 1       | 342   | 4     | 0.19   |
| Transcend | TS128GSSD370S      | 128 GB | 7       | 66    | 0     | 0.18   |
| Micron    | MTFDDAK480TDT      | 480 GB | 10      | 66    | 0     | 0.18   |
| SanDisk   | SD7UB3Q256G1122    | 256 GB | 1       | 700   | 10    | 0.17   |
| V-GeN     | V-GEN12SM20AR10... | 1 TB   | 1       | 190   | 2     | 0.17   |
| Micron    | C400-MTFDDAC512MAM | 512 GB | 4       | 679   | 802   | 0.17   |
| Kingston  | SKC6002048G        | 2 TB   | 1       | 117   | 1     | 0.16   |
| Micron    | MTFDDAK512TBN      | 512 GB | 3       | 58    | 0     | 0.16   |
| Intel     | SSDSC2BF240A4L     | 240 GB | 1       | 740   | 12    | 0.16   |
| Seagate   | BarraCuda 120 S... | 500 GB | 2       | 56    | 0     | 0.16   |
| HPE       | MK001920GWTTL      | 1.9 TB | 1       | 56    | 0     | 0.15   |
| SATADOM   | SL 3TE7            | 120 GB | 2       | 55    | 0     | 0.15   |
| ADATA     | SU630 1.9TB        | 1.9 TB | 2       | 54    | 0     | 0.15   |
| China     | SATA SSD           | 1 TB   | 13      | 52    | 0     | 0.14   |
| KIOXIA... | SATA SSD           | 240 GB | 8       | 51    | 0     | 0.14   |
| Crucial   | CT120M500SSD1      | 120 GB | 2       | 2010  | 523   | 0.14   |
| SPCC      | SSD                | 128 GB | 1       | 50    | 0     | 0.14   |
| WDC       | WDS500G1R0A-68A4W0 | 500 GB | 1       | 49    | 0     | 0.13   |
| Intel     | SSDSC2BB480G7K     | 480 GB | 1       | 48    | 0     | 0.13   |
| SATADOM   | ML 3MG2-P          | 248 GB | 1       | 47    | 0     | 0.13   |
| Transcend | TS2TSSD230S        | 2 TB   | 2       | 46    | 0     | 0.13   |
| Team      | T253A3001T         | 1 TB   | 30      | 46    | 0     | 0.13   |
| Samsung   | SSD 870 EVO        | 2 TB   | 44      | 46    | 1     | 0.12   |
| Crucial   | CT512M550SSD1      | 512 GB | 2       | 740   | 16    | 0.12   |
| Samsung   | SSD 870 EVO        | 1 TB   | 45      | 42    | 1     | 0.12   |
| China     | SATA SSD           | 120 GB | 3       | 40    | 0     | 0.11   |
| QUMO      | SSD                | 64 GB  | 2       | 47    | 608   | 0.10   |
| KingFast  | SSD                | 512 GB | 1       | 447   | 11    | 0.10   |
| China     | OSSD120GBTSS2      | 120 GB | 1       | 700   | 18    | 0.10   |
| SPCC      | SSD                | 480 GB | 2       | 311   | 518   | 0.10   |
| Crucial   | CT2000BX500SSD1    | 2 TB   | 12      | 34    | 0     | 0.09   |
| Intel     | SSDSC2BW480A4      | 480 GB | 3       | 514   | 24    | 0.09   |
| Transcend | TS256GMTS800S      | 256 GB | 5       | 31    | 0     | 0.09   |
| Patriot   | P210               | 2 TB   | 2       | 31    | 0     | 0.09   |
| Synology  | SAT5200-480G       | 480 GB | 12      | 31    | 0     | 0.09   |
| Intenso   | AP-SSD-A1-256      | 256 GB | 1       | 29    | 0     | 0.08   |
| Transcend | TS1TSSD230S        | 1 TB   | 1       | 28    | 0     | 0.08   |
| HPE       | LK1600GEYMV        | 1.6 TB | 1       | 28    | 0     | 0.08   |
| Intel     | SSDSC2KI128G8      | 128 GB | 1       | 56    | 1     | 0.08   |
| Kingston  | SKC300S37A480G     | 480 GB | 1       | 27    | 0     | 0.08   |
| Intel     | SSDSC2KB240GZ      | 240 GB | 5       | 24    | 0     | 0.07   |
| Transcend | TS128GMTS800S      | 128 GB | 5       | 18    | 0     | 0.05   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 6       | 15    | 0     | 0.04   |
| HP        | VK000240GWEZB      | 240 GB | 8       | 15    | 0     | 0.04   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 1       | 14    | 0     | 0.04   |
| Intel     | SSDSC2BA400G3I ... | 400 GB | 2       | 13    | 0     | 0.04   |
| SATADOM   | SV 3ME3            | 64 GB  | 4       | 10    | 0     | 0.03   |
| Netac     | SSD                | 64 GB  | 1       | 10    | 0     | 0.03   |
| Kingston  | SKC600256G         | 256 GB | 27      | 10    | 0     | 0.03   |
| Kingston  | SEDC450R1920G      | 1.9 TB | 4       | 8     | 0     | 0.02   |
| Micron    | 5300_MTFDDAK240TDT | 240 GB | 7       | 7     | 0     | 0.02   |
| Intel     | SSDSC2KW240H6      | 240 GB | 1       | 201   | 27    | 0.02   |
| Palit     | PH120 SSD          | 120 GB | 2       | 6     | 0     | 0.02   |
| Intel     | SSDSC2KW120H6      | 120 GB | 1       | 6     | 0     | 0.02   |
| HP        | VK000480GWSXF      | 480 GB | 1       | 5     | 0     | 0.01   |
| Intel     | SSDSC2KF256H6 SATA | 256 GB | 1       | 169   | 42    | 0.01   |
| Lite-On   | CV1-8B128-HP       | 128 GB | 1       | 3     | 0     | 0.01   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 1       | 3129  | 1011  | 0.01   |
| Kingston  | SHPM2280P2H-480G   | 480 GB | 3       | 1138  | 743   | 0.01   |
| Intel     | SSDSC2BG200G4R     | 200 GB | 7       | 2303  | 1029  | 0.01   |
| Intel     | SSDSC2BA200G3R     | 200 GB | 21      | 2279  | 1029  | 0.01   |
| Micron    | M500_MTFDDAK960MAV | 960 GB | 1       | 2162  | 1032  | 0.01   |
| Avant     | 120GB Client mSATA | 120 GB | 2       | 2045  | 1018  | 0.01   |
| ADATA     | SX900              | 512 GB | 2       | 2028  | 1019  | 0.01   |
| Intel     | SSDSC2BX016T4R     | 1.6 TB | 32      | 2003  | 1029  | 0.01   |
| Intel     | SSDSC1BG400G4R     | 400 GB | 16      | 1975  | 1028  | 0.01   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 1       | 1920  | 1020  | 0.01   |
| Intel     | SSDSC2BB300G4T     | 304 GB | 2       | 1925  | 1028  | 0.01   |
| Intel     | SSDSC2BA200G3T     | 200 GB | 4       | 1733  | 1028  | 0.00   |
| Intel     | SSDSC2BX200G4R     | 200 GB | 21      | 1707  | 1028  | 0.00   |
| Intel     | SSDSC2BW120A3      | 120 GB | 1       | 1687  | 1019  | 0.00   |
| Intel     | SSDSC1BG200G4R     | 200 GB | 33      | 1528  | 1028  | 0.00   |
| Intel     | SSDSC2BB480G6R     | 480 GB | 1       | 1446  | 1028  | 0.00   |
| Intel     | SSDSC2BX400G4R     | 400 GB | 78      | 1361  | 1028  | 0.00   |
| Micron    | MTFDDAK3T8TDS-1... | 3.8 TB | 2       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BA100G3T     | 100 GB | 3       | 1336  | 1028  | 0.00   |
| Kingston  | SHPM2280P2H-240G   | 240 GB | 1       | 1297  | 1022  | 0.00   |
| Intel     | SSDSC2BA800G4R     | 800 GB | 71      | 1243  | 1042  | 0.00   |
| Intel     | SSDSC2BA200G4R     | 200 GB | 12      | 1078  | 1027  | 0.00   |
| Crucial   | CT128MX100SSD1     | 128 GB | 1       | 1045  | 1061  | 0.00   |
| Intel     | SSDSC2KG960G8T     | 960 GB | 1       | 822   | 1026  | 0.00   |
| Intel     | SSDSC2BB800G4T     | 800 GB | 1       | 807   | 1027  | 0.00   |
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
| Transcend | JMicron/Maxiotek ba... | 1      | 1       | 2182  | 0     | 5.98   |
| Intel     | 320 Series SSDs        | 7      | 48      | 2672  | 45    | 5.75   |
| ADATA     | JMicron/Maxiotek ba... | 1      | 1       | 2000  | 0     | 5.48   |
| Plextor   | M3/M5/M6 Series SSDs   | 1      | 1       | 1971  | 0     | 5.40   |
| Intel     | 710 Series SSDs        | 1      | 2       | 2530  | 1     | 5.32   |
| Crucial   | RealSSD m4/C400        | 1      | 2       | 1898  | 0     | 5.20   |
| OCZ       | SandForce Driven SSDs  | 4      | 9       | 2760  | 3     | 4.67   |
| Intel     | 330/335 Series SSDs    | 3      | 19      | 2583  | 2     | 4.62   |
| Micron    | RealSSD m4/C400/P400   | 6      | 18      | 1891  | 179   | 4.53   |
| Crucial   | RealSSD m4/C400/P400   | 2      | 2       | 3123  | 506   | 4.27   |
| Corsair   | SandForce Driven SSDs  | 2      | 5       | 1489  | 0     | 4.08   |
| Toshiba   | OCZ                    | 1      | 6       | 1443  | 0     | 3.95   |
| ADATA     | SandForce Driven SSDs  | 1      | 2       | 2368  | 2     | 3.89   |
| Intel     | 520 Series SSDs        | 9      | 139     | 2104  | 345   | 3.62   |
| Kingston  | SandForce Driven SSDs  | 18     | 197     | 1518  | 9     | 3.45   |
| SanDisk   | SanDisk based SSDs     | 5      | 16      | 1423  | 2     | 3.36   |
| SanDisk   | SATA Cloudspeed Max... | 5      | 55      | 1152  | 19    | 3.12   |
| OCZ       | OCZ/Toshiba Trion SSDs | 2      | 2       | 1125  | 0     | 3.08   |
| Apacer    | Unknown                | 2      | 2       | 1122  | 0     | 3.07   |
| Intel     | 730 and DC S35x0/36... | 50     | 980     | 1478  | 232   | 3.01   |
| Intel     | Dell Certified Inte... | 3      | 78      | 1277  | 27    | 3.01   |
| Intel     | 3710 Series SSDs       | 1      | 5       | 1092  | 0     | 2.99   |
| OCZ       | Indilinx Barefoot 3... | 3      | 7       | 1356  | 12    | 2.97   |
| Toshiba   | HK4R Series SSD        | 4      | 42      | 1043  | 1     | 2.82   |
| Dell      | Certified Intel S35... | 1      | 5       | 1193  | 1     | 2.75   |
| OWC       | Unknown                | 1      | 1       | 2002  | 1     | 2.74   |
| Goodram   | Phison Driven OEM SSDs | 1      | 4       | 962   | 0     | 2.64   |
| MyDigi... | Unknown                | 1      | 6       | 945   | 0     | 2.59   |
| Crucial   | BX/MX1/2/3/500, M5/... | 11     | 134     | 1198  | 18    | 2.44   |
| Intel     | 510 Series SSDs        | 1      | 2       | 842   | 0     | 2.31   |
| AMD       | Silicon Motion base... | 1      | 2       | 812   | 0     | 2.23   |
| XPG       | Unknown                | 1      | 2       | 806   | 0     | 2.21   |
| Seagate   | Nytro XF1230 SATA SSD  | 3      | 26      | 806   | 0     | 2.21   |
| Lite-On   | Unknown                | 4      | 6       | 796   | 0     | 2.18   |
| Intel     | 525 Series SSDs        | 1      | 1       | 788   | 0     | 2.16   |
| OWC       | SandForce Driven SSDs  | 1      | 2       | 774   | 0     | 2.12   |
| WDC       | Blue and Green SSDs    | 9      | 52      | 768   | 0     | 2.11   |
| Crucial   | MX1/2/300, M5/600, ... | 1      | 4       | 1508  | 503   | 2.10   |
| HP        | Unknown                | 27     | 167     | 780   | 1     | 2.06   |
| Toshiba   | OCZ/Toshiba Trion SSDs | 1      | 1       | 1473  | 1     | 2.02   |
| SuperM... | Silicon Motion base... | 4      | 193     | 730   | 8     | 1.96   |
| Samsung   | Samsung based SSDs     | 133    | 6236    | 765   | 10    | 1.91   |
| HPE       | Unknown                | 18     | 89      | 736   | 2     | 1.87   |
| Toshiba   | Unknown                | 12     | 205     | 683   | 1     | 1.83   |
| Micron    | BX/MX1/2/3/500, M5/... | 5      | 73      | 906   | 42    | 1.78   |
| Toshiba   | HG6 Series SSD         | 2      | 2       | 634   | 0     | 1.74   |
| Crucial   | Silicon Motion base... | 5      | 6       | 634   | 0     | 1.74   |
| Intel     | S3520 Series SSDs      | 7      | 288     | 1141  | 3     | 1.73   |
| Crucial   | BX/MX1/2/3/500, M5/... | 9      | 242     | 865   | 18    | 1.72   |
| Plextor   | Unknown                | 2      | 2       | 582   | 0     | 1.60   |
| SanDisk   | SATA CS1K GEN1 ESS ... | 1      | 1       | 577   | 0     | 1.58   |
| Kingston  | SSDNow UV400           | 2      | 65      | 581   | 1     | 1.54   |
| Micron    | 5100 Pro / 5200 SSDs   | 19     | 592     | 697   | 10    | 1.53   |
| Micron    | BX/MX1/2/3/500, M5/... | 5      | 68      | 674   | 29    | 1.52   |
| SanDisk   | Marvell based SanDi... | 19     | 145     | 602   | 2     | 1.51   |
| Goodram   | Unknown                | 1      | 2       | 538   | 0     | 1.47   |
| Innodisk  | 3IE3/3ME3/3ME4 SSDs    | 1      | 1       | 1074  | 1     | 1.47   |
| Micron    | MX1/2/300, M5/600, ... | 3      | 20      | 557   | 1     | 1.46   |
| Plextor   | M3/M5/M6/M7 Series ... | 1      | 2       | 527   | 0     | 1.44   |
| Patriot   | Silicon Motion base... | 1      | 5       | 510   | 0     | 1.40   |
| Goodram   | Phison Driven SSDs     | 4      | 14      | 506   | 0     | 1.39   |
| PNY       | Phison Driven SSDs     | 2      | 3       | 502   | 0     | 1.38   |
| Zheino    | Unknown                | 1      | 1       | 497   | 0     | 1.36   |
| SK hynix  | SATA SSDs              | 7      | 18      | 497   | 0     | 1.36   |
| Intel     | 53x and Pro 1500/25... | 11     | 123     | 743   | 6     | 1.36   |
| Kingston  | SSDNow UV400/500       | 4      | 16      | 487   | 0     | 1.33   |
| Intel     | S4510/S4610/S4500/S... | 21     | 3303    | 568   | 3     | 1.30   |
| Micron    | 5100 Pro / 5200 / 5... | 13     | 420     | 572   | 5     | 1.24   |
| SanDisk   | SandForce Driven SSDs  | 4      | 8       | 796   | 4     | 1.24   |
| Intel     | Dell Certified Inte... | 10     | 146     | 504   | 15    | 1.20   |
| Samsung   | Unknown                | 18     | 617     | 442   | 1     | 1.18   |
| SanDisk   | Unknown                | 8      | 12      | 473   | 154   | 1.16   |
| Seagate   | Nytro SATA SSD         | 7      | 182     | 421   | 0     | 1.15   |
| WDC       | Blue / Red / Green ... | 13     | 241     | 462   | 2     | 1.15   |
| Gigabyte  | Unknown                | 1      | 2       | 410   | 0     | 1.13   |
| SATADOM   | Unknown                | 5      | 12      | 408   | 0     | 1.12   |
| KingDian  | Silicon Motion base... | 1      | 3       | 476   | 1     | 1.12   |
| SPCC      | Unknown                | 5      | 11      | 456   | 95    | 1.11   |
| Patriot   | Phison Driven SSDs     | 3      | 13      | 404   | 0     | 1.11   |
| Corsair   | Unknown                | 1      | 1       | 1955  | 4     | 1.07   |
| Intel     | Unknown                | 15     | 131     | 1634  | 691   | 1.07   |
| Kingston  | Phison Driven SSDs     | 24     | 349     | 412   | 2     | 1.00   |
| ORTIAL    | Unknown                | 1      | 12      | 455   | 2     | 1.00   |
| Seagate   | Unknown                | 3      | 5       | 357   | 0     | 0.98   |
| Transcend | Unknown                | 3      | 8       | 354   | 0     | 0.97   |
| BIWIN     | Unknown                | 1      | 1       | 332   | 0     | 0.91   |
| WDC       | Unknown                | 3      | 9       | 377   | 1     | 0.89   |
| Mushkin   | Unknown                | 3      | 14      | 394   | 1     | 0.88   |
| ADATA     | Silicon Motion base... | 5      | 12      | 377   | 42    | 0.85   |
| Mushkin   | Silicon Motion base... | 1      | 1       | 308   | 0     | 0.84   |
| Dell      | Certified Intel S4x... | 1      | 12      | 306   | 0     | 0.84   |
| KingSpec  | Unknown                | 2      | 3       | 253   | 0     | 0.70   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 2      | 8       | 248   | 0     | 0.68   |
| Micron    | Unknown                | 21     | 484     | 252   | 2     | 0.67   |
| SPCC      | Phison Driven OEM SSDs | 2      | 4       | 228   | 0     | 0.63   |
| Phison    | Driven OEM SSDs        | 5      | 23      | 226   | 0     | 0.62   |
| Micron    | Client SSDs            | 3      | 39      | 231   | 1     | 0.61   |
| Apacer    | AS340 SSDs             | 2      | 44      | 323   | 20    | 0.60   |
| Maxtor    | Unknown                | 2      | 3       | 215   | 0     | 0.59   |
| Crucial   | MX500 SSDs             | 6      | 648     | 241   | 3     | 0.55   |
| Intel     | X18-M/X25-M/X25-V G... | 1      | 1       | 2595  | 12    | 0.55   |
| THU       | Unknown                | 1      | 1       | 197   | 0     | 0.54   |
| SK hynix  | Unknown                | 1      | 23      | 175   | 0     | 0.48   |
| ADATA     | Unknown                | 9      | 19      | 503   | 161   | 0.48   |
| Intel     | DC S3110 Series SSDs   | 1      | 1       | 173   | 0     | 0.47   |
| Patriot   | Unknown                | 4      | 8       | 167   | 0     | 0.46   |
| China     | Unknown                | 8      | 35      | 196   | 1     | 0.45   |
| Apacer    | SSDs                   | 1      | 3       | 157   | 0     | 0.43   |
| Crucial   | SiliconMotion based... | 2      | 2       | 157   | 0     | 0.43   |
| Team      | Unknown                | 5      | 40      | 152   | 0     | 0.42   |
| Kingston  | Unknown                | 4      | 6       | 933   | 542   | 0.41   |
| Intel     | 545s Series SSDs       | 4      | 42      | 153   | 4     | 0.36   |
| Transcend | Silicon Motion base... | 8      | 27      | 140   | 1     | 0.32   |
| Intenso   | Unknown                | 2      | 3       | 114   | 0     | 0.31   |
| PNY       | Unknown                | 1      | 10      | 109   | 0     | 0.30   |
| Smartbuy  | Unknown                | 1      | 1       | 70    | 0     | 0.19   |
| Gigabyte  | Phison Driven SSDs     | 3      | 8       | 63    | 0     | 0.17   |
| V-GeN     | Unknown                | 1      | 1       | 190   | 2     | 0.17   |
| KIOXIA... | Unknown                | 1      | 8       | 51    | 0     | 0.14   |
| QUMO      | Unknown                | 1      | 2       | 47    | 608   | 0.10   |
| KingFast  | Unknown                | 1      | 1       | 447   | 11    | 0.10   |
| Crucial   | Client SSDs            | 1      | 12      | 34    | 0     | 0.09   |
| Synology  | Unknown                | 1      | 12      | 31    | 0     | 0.09   |
| Kingston  | Silicon Motion base... | 3      | 30      | 22    | 1     | 0.06   |
| Netac     | Unknown                | 1      | 1       | 10    | 0     | 0.03   |
| Palit     | Unknown                | 1      | 2       | 6     | 0     | 0.02   |
| Intel     | 540 Series SSDs        | 3      | 3       | 108   | 140   | 0.01   |
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
| OCZ         | 10     | 19      | 2054  | 6     | 3.98   |
| Corsair     | 3      | 6       | 1567  | 1     | 3.58   |
| MyDigita... | 1      | 6       | 945   | 0     | 2.59   |
| OWC         | 2      | 3       | 1184  | 1     | 2.33   |
| Plextor     | 4      | 5       | 838   | 0     | 2.30   |
| AMD         | 1      | 2       | 812   | 0     | 2.23   |
| XPG         | 1      | 2       | 806   | 0     | 2.21   |
| Lite-On     | 4      | 6       | 796   | 0     | 2.18   |
| HP          | 27     | 167     | 780   | 1     | 2.06   |
| Toshiba     | 20     | 256     | 763   | 1     | 2.04   |
| SanDisk     | 42     | 237     | 785   | 13    | 1.98   |
| SuperMicro  | 4      | 193     | 730   | 8     | 1.96   |
| HPE         | 18     | 89      | 736   | 2     | 1.87   |
| Samsung     | 151    | 6853    | 736   | 9     | 1.85   |
| Intel       | 150    | 5315    | 872   | 72    | 1.77   |
| Kingston    | 56     | 664     | 750   | 9     | 1.75   |
| Goodram     | 6      | 20      | 600   | 0     | 1.65   |
| Innodisk    | 1      | 1       | 1074  | 1     | 1.47   |
| Dell        | 2      | 17      | 567   | 1     | 1.40   |
| Zheino      | 1      | 1       | 497   | 0     | 1.36   |
| WDC         | 25     | 302     | 512   | 2     | 1.30   |
| Seagate     | 13     | 213     | 466   | 0     | 1.28   |
| Micron      | 75     | 1714    | 549   | 10    | 1.24   |
| KingDian    | 1      | 3       | 476   | 1     | 1.12   |
| Crucial     | 38     | 1052    | 520   | 11    | 1.09   |
| ORTIAL      | 1      | 12      | 455   | 2     | 1.00   |
| SPCC        | 7      | 15      | 396   | 70    | 0.98   |
| Patriot     | 8      | 26      | 351   | 0     | 0.96   |
| ADATA       | 16     | 34      | 613   | 105   | 0.96   |
| SATADOM     | 7      | 20      | 344   | 0     | 0.94   |
| BIWIN       | 1      | 1       | 332   | 0     | 0.91   |
| Mushkin     | 4      | 15      | 388   | 1     | 0.88   |
| SK hynix    | 8      | 41      | 317   | 0     | 0.87   |
| KingSpec    | 2      | 3       | 253   | 0     | 0.70   |
| Apacer      | 5      | 49      | 345   | 18    | 0.69   |
| Transcend   | 12     | 36      | 244   | 1     | 0.63   |
| Phison      | 5      | 23      | 226   | 0     | 0.62   |
| Maxtor      | 2      | 3       | 215   | 0     | 0.59   |
| PNY         | 3      | 13      | 200   | 0     | 0.55   |
| THU         | 1      | 1       | 197   | 0     | 0.54   |
| China       | 8      | 35      | 196   | 1     | 0.45   |
| Team        | 5      | 40      | 152   | 0     | 0.42   |
| Gigabyte    | 4      | 10      | 133   | 0     | 0.36   |
| Intenso     | 2      | 3       | 114   | 0     | 0.31   |
| Smartbuy    | 1      | 1       | 70    | 0     | 0.19   |
| V-GeN       | 1      | 1       | 190   | 2     | 0.17   |
| KIOXIA-E... | 1      | 8       | 51    | 0     | 0.14   |
| QUMO        | 1      | 2       | 47    | 608   | 0.10   |
| KingFast    | 1      | 1       | 447   | 11    | 0.10   |
| Synology    | 1      | 12      | 31    | 0     | 0.09   |
| Netac       | 1      | 1       | 10    | 0     | 0.03   |
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

See full list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF   |
|-----------|--------------------|--------|---------|-------|-------|--------|
| Dell      | Express Flash N... | 800 GB | 1       | 1865  | 0     | 5.11   |
| Intel     | SSDPEDME016T4      | 1.6 TB | 1       | 1754  | 0     | 4.81   |
| Intel     | SSDPEDME020T4      | 2 TB   | 2       | 1696  | 0     | 4.65   |
| Intel     | SSDPEDME020T4D ... | 2 TB   | 2       | 1608  | 0     | 4.41   |
| Intel     | SSDPEDME400G4      | 400 GB | 19      | 1600  | 0     | 4.38   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 1       | 1576  | 0     | 4.32   |
| Intel     | SSDPE2MX012T4      | 1.2 TB | 4       | 1433  | 0     | 3.93   |
| Intel     | SSDPEDMX400G4      | 400 GB | 10      | 1432  | 0     | 3.93   |
| Dell      | Express Flash N... | 3.2 TB | 1       | 1428  | 0     | 3.91   |
| Intel     | SSDPEDME800G4      | 800 GB | 1       | 1416  | 0     | 3.88   |
| Samsung   | SSD 950 PRO        | 512 GB | 6       | 1392  | 0     | 3.82   |
| Intel     | SSDPEDMD400G4      | 400 GB | 210     | 1359  | 0     | 3.73   |
| Intel     | SSDPEDMD020T4D ... | 2 TB   | 5       | 1323  | 0     | 3.62   |
| Intel     | SSDPEDMD016T4      | 1.6 TB | 17      | 1319  | 0     | 3.62   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 3       | 1281  | 0     | 3.51   |
| Intel     | SSDPE2KE016T7      | 1.6 TB | 2       | 1280  | 0     | 3.51   |
| Samsung   | MZ1LV480HCHP-00003 | 480 GB | 2       | 1263  | 0     | 3.46   |
| Intel     | SSDPEDMX020T7      | 2 TB   | 46      | 1287  | 5     | 3.46   |
| Intel     | SSDPEDMW400G4      | 400 GB | 10      | 1229  | 0     | 3.37   |
| Intel     | SSDPEDMX012T7      | 1.2 TB | 3       | 1228  | 0     | 3.36   |
| Intel     | SSDPEDMD800G4      | 800 GB | 270     | 1189  | 0     | 3.26   |
| Intel     | SSDPE2KE020T7      | 2 TB   | 1       | 1180  | 0     | 3.23   |
| Intel     | SSDPE2MD400G4      | 400 GB | 11      | 1156  | 0     | 3.17   |
| Dell      | Express Flash N... | 2 TB   | 14      | 1155  | 0     | 3.16   |
| Intel     | SSDPE2ME020T4      | 2 TB   | 2       | 1134  | 0     | 3.11   |
| Micron    | MTFDHAL1T2MCF-1... | 1.2 TB | 1       | 1120  | 0     | 3.07   |
| Intel     | SSDPEK1W120GA      | 118 GB | 1       | 1054  | 0     | 2.89   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 2       | 1041  | 0     | 2.85   |
| Intel     | SSDPEDME016T4S     | 1.6 TB | 4       | 1035  | 0     | 2.84   |
| Toshiba   | THNSN5512GPU7      | 512 GB | 14      | 1021  | 0     | 2.80   |
| Samsung   | MZPLL1T6HEHP-00003 | 1.6 TB | 87      | 1007  | 12    | 2.70   |
| Intel     | SSDPE2MX012T7      | 1.2 TB | 19      | 953   | 0     | 2.61   |
| Samsung   | SSD 960 EVO        | 500 GB | 6       | 922   | 0     | 2.53   |
| Samsung   | SSD 960 PRO        | 2 TB   | 1       | 921   | 0     | 2.52   |
| Intel     | SSDPEDMD020T4      | 2 TB   | 1       | 897   | 0     | 2.46   |
| Intel     | SSDPE2MD400G4L     | 400 GB | 4       | 895   | 0     | 2.45   |
| Dell      | Express Flash N... | 1.6 TB | 19      | 920   | 54    | 2.37   |
| Intel     | SSDPEDKX040T7      | 4 TB   | 45      | 890   | 23    | 2.33   |
| Samsung   | SSD 960 PRO        | 1 TB   | 10      | 845   | 0     | 2.32   |
| Intel     | SSDPE2ME012T4      | 1.2 TB | 7       | 828   | 0     | 2.27   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 1       | 824   | 0     | 2.26   |
| Intel     | SSDPEKKW256G7      | 256 GB | 17      | 836   | 1     | 2.24   |
| Intel     | SSDPE2MX450G7      | 450 GB | 44      | 812   | 0     | 2.23   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 1       | 789   | 0     | 2.16   |
| Intel     | SSDPE2KE076T8      | 7.6 TB | 2       | 778   | 0     | 2.13   |
| Intel     | SSDPEDMW800G4      | 800 GB | 7       | 774   | 0     | 2.12   |
| Intel     | SSDPE21K375GA      | 375 GB | 30      | 773   | 0     | 2.12   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 25      | 770   | 0     | 2.11   |
| Intel     | SSDPEDMD016T4K     | 1.6 TB | 2       | 764   | 0     | 2.09   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 2       | 759   | 0     | 2.08   |
| Intel     | SSDPE2KX040T8      | 4 TB   | 60      | 762   | 18    | 2.05   |
| Intel     | VO0400KEFJB        | 400 GB | 4       | 743   | 0     | 2.04   |
| Huawei    | HWE36P43016M000N   | 1.6 TB | 2       | 741   | 0     | 2.03   |
| Kingston  | SKC1000960G        | 960 GB | 3       | 738   | 0     | 2.02   |
| Intel     | SSDPEKKW512G7      | 512 GB | 1       | 728   | 0     | 2.00   |
| Samsung   | MZPLL3T2HMLS-00003 | 3.2 TB | 6       | 715   | 0     | 1.96   |
| Intel     | MT0800KEXUU        | 800 GB | 18      | 713   | 0     | 1.95   |
| Intel     | SSDPED1D480GA      | 480 GB | 52      | 710   | 0     | 1.95   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 5       | 858   | 202   | 1.90   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 6       | 685   | 0     | 1.88   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 1       | 673   | 0     | 1.84   |
| Intel     | SSDPED1D280GA      | 280 GB | 21      | 720   | 1     | 1.83   |
| Samsung   | MZPLL6T4HMLA-00005 | 6.4 TB | 6       | 658   | 0     | 1.81   |
| Samsung   | MZQLW1T9HMJP-00003 | 1.9 TB | 2       | 639   | 0     | 1.75   |
| Samsung   | MZQLW960HMJP-00003 | 960 GB | 18      | 992   | 144   | 1.74   |
| Dell      | Express Flash N... | 1.6 TB | 4       | 631   | 0     | 1.73   |
| Samsung   | MZWLL6T4HMLA-00005 | 6.4 TB | 2       | 629   | 0     | 1.72   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 18      | 614   | 0     | 1.68   |
| Intel     | SSDPE2KX020T7      | 2 TB   | 1       | 611   | 0     | 1.68   |
| Intel     | SSDPEDKE040T7      | 4 TB   | 1       | 604   | 0     | 1.66   |
| Samsung   | MZPLL6T4HMLS-00003 | 6.4 TB | 16      | 603   | 0     | 1.65   |
| Samsung   | SSD 983 DCT        | 960 GB | 2       | 591   | 0     | 1.62   |
| PNY       | CS3030 500GB SSD   | 500 GB | 2       | 589   | 0     | 1.62   |
| Samsung   | SSD 970 EVO        | 500 GB | 2       | 588   | 0     | 1.61   |
| Intel     | SSDPEL1D380GA      | 384 GB | 6       | 562   | 0     | 1.54   |
| Intel     | SSDPEKKA256G7      | 256 GB | 4       | 557   | 0     | 1.53   |
| Intel     | SSDPE2KX080T8      | 8 TB   | 14      | 556   | 0     | 1.53   |
| Intel     | SSDPEKKW256G8      | 256 GB | 1       | 548   | 0     | 1.50   |
| Dell      | Express Flash N... | 3.2 TB | 4       | 538   | 0     | 1.47   |
| Intel     | SSDPED1K375GA      | 375 GB | 77      | 535   | 0     | 1.47   |
| Corsair   | Force MP600        | 1 TB   | 1       | 531   | 0     | 1.46   |
| Dell      | Express Flash P... | 6.4 TB | 1       | 527   | 0     | 1.45   |
| Kingston  | SKC2000M81000G     | 1 TB   | 2       | 518   | 0     | 1.42   |
| Dell      | Express Flash P... | 800 GB | 8       | 517   | 0     | 1.42   |
| WDC       | WUS3BA196C7P3E3    | 960 GB | 83      | 513   | 0     | 1.41   |
| WDC       | WUS3BA138C7P3E3    | 3.8 TB | 20      | 503   | 0     | 1.38   |
| Samsung   | SSD 960 EVO        | 250 GB | 2       | 495   | 0     | 1.36   |
| Smartbuy  | m.2 PS5013T-2280T  | 128 GB | 1       | 493   | 0     | 1.35   |
| Intel     | SSDPE21D480GA      | 480 GB | 107     | 491   | 0     | 1.35   |
| Samsung   | MZQLB3T8HALS-000AZ | 3.8 TB | 24      | 484   | 0     | 1.33   |
| WDC       | WUS3CA116C7P3E3    | 1.6 TB | 178     | 479   | 0     | 1.31   |
| Samsung   | MZWLL800HEHP-00003 | 800 GB | 14      | 757   | 4     | 1.30   |
| Samsung   | MZPLL3T2HAJQ-00005 | 3.2 TB | 24      | 474   | 0     | 1.30   |
| Toshiba   | KXD51RUE960G       | 960 GB | 4       | 466   | 0     | 1.28   |
| Samsung   | MZPLL6T4HMLS-000MV | 6.4 TB | 4       | 465   | 0     | 1.27   |
| Intel     | SSDPED1D960GAY     | 960 GB | 6       | 460   | 0     | 1.26   |
| Intel     | SSDPED1K750GA      | 752 GB | 135     | 456   | 0     | 1.25   |
| Samsung   | MZ1LB960HAJQ-00007 | 960 GB | 28      | 447   | 0     | 1.23   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 164     | 439   | 0     | 1.21   |
| Wester... | WUS3BA196C7P3E3    | 960 GB | 83      | 439   | 0     | 1.20   |
| Intel     | SSDPE21K750GA      | 752 GB | 66      | 430   | 0     | 1.18   |
| Samsung   | MZWLJ15THALA-00007 | 15.... | 2       | 429   | 0     | 1.18   |
| Wester... | WUS3CA116C7P3E3    | 1.6 TB | 178     | 428   | 0     | 1.17   |
| Wester... | WUS3BA119C7P3E3    | 960 GB | 1       | 424   | 0     | 1.16   |
| Wester... | WUS3BA138C7P3E3    | 3.8 TB | 20      | 424   | 0     | 1.16   |
| Samsung   | MZWLL12THMLA-00005 | 12.... | 2       | 422   | 0     | 1.16   |
| Samsung   | MZWLL1T6HAJQ-00005 | 1.6 TB | 10      | 420   | 0     | 1.15   |
| Dell      | Express Flash N... | 1.6 TB | 115     | 407   | 0     | 1.12   |
| Samsung   | MZQLW1T9HMJP-000AZ | 1.9 TB | 7       | 435   | 1     | 1.11   |
| Intel     | SSDPE2KX040T7      | 4 TB   | 4       | 405   | 0     | 1.11   |
| Intel     | SSDPE2KE032T8      | 3.2 TB | 29      | 404   | 0     | 1.11   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 12      | 391   | 0     | 1.07   |
| Intel     | SSDPE21K100GA      | 100 GB | 5       | 387   | 0     | 1.06   |
| Intel     | SSDPE2KX010T8      | 1 TB   | 133     | 384   | 0     | 1.05   |
| WDC       | CL SN720 SDAQNT... | 1 TB   | 46      | 383   | 0     | 1.05   |
| WDC       | WUS4CB016D7P3E3    | 1.6 TB | 152     | 375   | 0     | 1.03   |
| Intel     | SSDPEL1K100GA      | 100 GB | 11      | 368   | 0     | 1.01   |
| Intel     | SSDPEKKW512G8      | 512 GB | 9       | 367   | 0     | 1.01   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 96      | 375   | 9     | 0.99   |
| Samsung   | SSD 960 PRO        | 512 GB | 2       | 362   | 0     | 0.99   |
| Phison    | PCIe SSD           | 256 GB | 1       | 362   | 0     | 0.99   |
| WDC       | WUS4BB096D7P3E3    | 960 GB | 534     | 361   | 0     | 0.99   |
| Samsung   | MZPLL1T6HAJQ-00005 | 1.6 TB | 3       | 357   | 0     | 0.98   |
| Intel     | SSDPEKKA512G8      | 512 GB | 23      | 352   | 0     | 0.97   |
| Intel     | SSDPE2MD016T4      | 1.6 TB | 4       | 349   | 0     | 0.96   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 5       | 344   | 0     | 0.95   |
| ADATA     | SX8200PNP          | 1 TB   | 1       | 341   | 0     | 0.94   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 27      | 359   | 1     | 0.93   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 3       | 333   | 0     | 0.91   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 470     | 333   | 0     | 0.91   |
| Micron    | 2200S NVMe         | 256 GB | 1       | 333   | 0     | 0.91   |
| HP        | SSD EX950          | 2 TB   | 10      | 332   | 0     | 0.91   |
| Phison    | Viper M.2 VPN100   | 2 TB   | 7       | 330   | 0     | 0.91   |
| Dell      | Express Flash P... | 1.6 TB | 4       | 327   | 0     | 0.90   |
| Crucial   | CT250P2SSD8        | 250 GB | 1       | 326   | 0     | 0.89   |
| Samsung   | VO001920KWVMT 1... | 1.9 TB | 36      | 320   | 0     | 0.88   |
| Samsung   | MZWLL1T6HEHP-00003 | 1.6 TB | 8       | 318   | 0     | 0.87   |
| Samsung   | SSD 970 PRO        | 1 TB   | 38      | 316   | 0     | 0.87   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 2       | 312   | 0     | 0.85   |
| Samsung   | MZPJB480HMGC-0BW07 | 480 GB | 15      | 310   | 0     | 0.85   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 4       | 309   | 0     | 0.85   |
| Kingston  | SEDC1000M1920G     | 1.9 TB | 2       | 307   | 0     | 0.84   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 27      | 306   | 1     | 0.82   |
| Samsung   | MZQLB3T8HALS-00007 | 3.8 TB | 124     | 304   | 1     | 0.82   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 15      | 296   | 0     | 0.81   |
| HGST      | HUSMR7638BDP3Y1    | 3.8 TB | 24      | 290   | 0     | 0.80   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 38      | 289   | 0     | 0.79   |
| Seagate   | FireCuda 520 SS... | 500 GB | 10      | 287   | 0     | 0.79   |
| Intel     | SSDPE2ME400G4      | 400 GB | 7       | 285   | 0     | 0.78   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 1       | 282   | 0     | 0.77   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 45      | 279   | 0     | 0.77   |
| Dell      | Express Flash P... | 1.6 TB | 12      | 277   | 0     | 0.76   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 668     | 276   | 1     | 0.76   |
| Intel     | SSDPECKE064T7ES    | 3.2 TB | 2       | 273   | 0     | 0.75   |
| Wester... | WUS4BB096D7P3E3    | 960 GB | 443     | 273   | 0     | 0.75   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 2       | 270   | 0     | 0.74   |
| Samsung   | SSD 970 PRO        | 512 GB | 83      | 266   | 0     | 0.73   |
| ADATA     | SX8200PNP          | 256 GB | 2       | 264   | 0     | 0.72   |
| Dell      | Express Flash P... | 1.6 TB | 1       | 259   | 0     | 0.71   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 10      | 254   | 0     | 0.70   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 23      | 252   | 0     | 0.69   |
| Wester... | WUS4CB016D7P3E3    | 1.6 TB | 152     | 246   | 0     | 0.68   |
| Micron    | 9300_MTFDHAL3T2TDR | 3.2 TB | 30      | 245   | 0     | 0.67   |
| Intel     | EO000375KWJUC      | 375 GB | 2       | 242   | 0     | 0.66   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 6       | 239   | 0     | 0.66   |
| Intel     | SSDPE2NU076T8      | 7.6 TB | 3       | 236   | 0     | 0.65   |
| Toshiba   | KXD51RUE3T84       | 3.8 TB | 1       | 234   | 0     | 0.64   |
| Samsung   | SSD 970 EVO        | 250 GB | 2       | 360   | 1     | 0.62   |
| Samsung   | MZWLJ7T6HALA-00007 | 7.6 TB | 2       | 226   | 0     | 0.62   |
| Intel     | SSDPE2NV076T8      | 7.6 TB | 2       | 223   | 0     | 0.61   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 2       | 216   | 0     | 0.59   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 12      | 225   | 1     | 0.58   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 8       | 210   | 0     | 0.58   |
| WDC       | WUS4BB038D7P3E1    | 3.8 TB | 71      | 198   | 0     | 0.54   |
| WDC       | WUS4BB038D7P3E3    | 3.8 TB | 37      | 197   | 0     | 0.54   |
| Patriot   | P300               | 256 GB | 2       | 196   | 0     | 0.54   |
| Toshiba   | KXD51RUE1T92       | 1.9 TB | 10      | 194   | 0     | 0.53   |
| SK hynix  | PC601 NVMe         | 256 GB | 1       | 192   | 0     | 0.53   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 20      | 192   | 0     | 0.53   |
| WDC       | WUS4BB076D7P3E1    | 7.6 TB | 12      | 191   | 0     | 0.53   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 1       | 191   | 0     | 0.52   |
| Intel     | SSDPE2KX010T7      | 1 TB   | 8       | 186   | 0     | 0.51   |
| Kingston  | SEDC1000M3840G     | 3.8 TB | 6       | 183   | 0     | 0.50   |
| HP        | SSD EX950          | 512 GB | 7       | 183   | 0     | 0.50   |
| Samsung   | MZQLB7T6HMLA-00007 | 7.6 TB | 106     | 182   | 0     | 0.50   |
| Silico... | NVME SSD           | 512 GB | 1       | 177   | 0     | 0.49   |
| Intel     | SSDPECME016T4      | 800 GB | 8       | 175   | 0     | 0.48   |
| Samsung   | MZPLJ6T4HALA-00007 | 6.4 TB | 37      | 174   | 0     | 0.48   |
| Intel     | SSDPE2KE016T8      | 1.6 TB | 28      | 174   | 0     | 0.48   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 45      | 169   | 0     | 0.46   |
| XPG       | SPECTRIX S40G      | 1 TB   | 1       | 168   | 0     | 0.46   |
| Micron    | 9300_MTFDHAL7T6TDP | 7.6 TB | 33      | 166   | 0     | 0.46   |
| WDC       | WUS4BB096D7P3E1    | 960 GB | 365     | 165   | 0     | 0.45   |
| Crucial   | CT500P1SSD8        | 500 GB | 2       | 163   | 0     | 0.45   |
| Patriot   | P300               | 128 GB | 4       | 163   | 0     | 0.45   |
| Wester... | WUS4BB038D7P3E3    | 3.8 TB | 13      | 162   | 0     | 0.44   |
| Samsung   | MZPJB960HMGC-0BW07 | 960 GB | 11      | 161   | 0     | 0.44   |
| Kingston  | SKC2500M8250G      | 250 GB | 5       | 161   | 0     | 0.44   |
| Samsung   | MZ1LB1T9HALS-00007 | 1.9 TB | 3       | 158   | 0     | 0.43   |
| Samsung   | MZPLJ3T2HBJR-00007 | 3.2 TB | 4       | 157   | 0     | 0.43   |
| Kingston  | SA2000M81000G      | 1 TB   | 8       | 154   | 0     | 0.42   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 3       | 153   | 0     | 0.42   |
| Toshiba   | KXG60PNV2T04       | 2 TB   | 8       | 146   | 0     | 0.40   |
| WDC       | WUS4BB019D7P3E1    | 1.9 TB | 465     | 144   | 0     | 0.40   |
| Dell      | Express Flash C... | 960 GB | 97      | 142   | 0     | 0.39   |
| Samsung   | MZ4LB3T8HALS-00003 | 3.8 TB | 6       | 140   | 0     | 0.38   |
| Intel     | SSDPE2MD800G4      | 800 GB | 1       | 130   | 0     | 0.36   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 17      | 128   | 0     | 0.35   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 2       | 126   | 0     | 0.35   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 58      | 125   | 0     | 0.34   |
| Kingston  | SKC2500M81000G     | 1 TB   | 8       | 122   | 0     | 0.34   |
| Wester... | WUS4BB019D7P3E1    | 1.9 TB | 193     | 117   | 0     | 0.32   |
| Samsung   | SSD 970 EVO        | 1 TB   | 7       | 339   | 2     | 0.32   |
| Micron    | 7300_MTFDHBE960TDF | 960 GB | 4       | 115   | 0     | 0.32   |
| Wester... | WUS4BB076D7P3E1    | 7.6 TB | 12      | 114   | 0     | 0.31   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 8       | 113   | 0     | 0.31   |
| Kingston  | SA2000M8500G       | 500 GB | 4       | 111   | 0     | 0.31   |
| ADATA     | SX8200PNP          | 512 GB | 5       | 111   | 0     | 0.30   |
| KIOXIA    | KCD6XLUL1T92       | 1.9 TB | 10      | 109   | 0     | 0.30   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 22      | 108   | 0     | 0.30   |
| Huawei    | HWE52P431T6M002N   | 1.6 TB | 2       | 108   | 0     | 0.30   |
| Dell      | Ent NVMe P5600 ... | 1.6 TB | 8       | 108   | 0     | 0.30   |
| WDC       | WUS3BA119C7P3E3    | 1.9 TB | 7       | 107   | 0     | 0.29   |
| WDC       | PC SN530 NVMe      | 512 GB | 1       | 103   | 0     | 0.28   |
| Kingston  | SA2000M8250G       | 250 GB | 1       | 101   | 0     | 0.28   |
| Kingston  | SEDC1000M960G      | 960 GB | 2       | 100   | 0     | 0.27   |
| Wester... | WUS4BB096D7P3E1    | 960 GB | 200     | 97    | 0     | 0.27   |
| Samsung   | MZQL2960HCJR-00A07 | 960 GB | 2       | 96    | 0     | 0.26   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 44      | 95    | 0     | 0.26   |
| Dell      | Express Flash P... | 1.6 TB | 4       | 92    | 0     | 0.25   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 18      | 89    | 0     | 0.25   |
| Samsung   | MZPLJ3T2HBJR-000H3 | 3.2 TB | 6       | 87    | 0     | 0.24   |
| Toshiba   | KXG60ZNV256G       | 256 GB | 55      | 86    | 0     | 0.24   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 14      | 84    | 0     | 0.23   |
| SK hynix  | VO000960KXAVL      | 960 GB | 2       | 80    | 0     | 0.22   |
| Samsung   | MZQLB1T9HAJR-000AZ | 1.9 TB | 4       | 80    | 0     | 0.22   |
| Samsung   | MT001600KWHAC 1... | 1.6 TB | 1       | 77    | 0     | 0.21   |
| Wester... | WUS4BB038D7P3E1    | 3.8 TB | 71      | 76    | 0     | 0.21   |
| SK hynix  | BC501 HFM512GDJ... | 512 GB | 1       | 73    | 0     | 0.20   |
| WDC       | WUS4BB019D7P3E3    | 1.9 TB | 54      | 69    | 0     | 0.19   |
| Intel     | SSDPEKNW512G8      | 512 GB | 4       | 69    | 0     | 0.19   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 15      | 69    | 0     | 0.19   |
| Micron    | 7300_MTFDHBE1T6TDG | 1.6 TB | 2       | 64    | 0     | 0.18   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 6       | 62    | 0     | 0.17   |
| Samsung   | MZPLJ1T6HBJR-000H3 | 1.6 TB | 8       | 56    | 0     | 0.15   |
| Dell      | Ent NVMe AGN RI... | 3.8 TB | 180     | 54    | 0     | 0.15   |
| Corsair   | MP400              | 1 TB   | 20      | 53    | 0     | 0.15   |
| Samsung   | SSD 980            | 500 GB | 3       | 51    | 0     | 0.14   |
| Huawei    | HWE56P43800M005N   | 800 GB | 3       | 48    | 0     | 0.13   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 47    | 0     | 0.13   |
| SK hynix  | PC601 HFS256GD9... | 256 GB | 1       | 46    | 0     | 0.13   |
| ADATA     | SX8200PNP          | 2 TB   | 2       | 45    | 0     | 0.13   |
| Team      | TM8FP6128G         | 128 GB | 1       | 45    | 0     | 0.13   |
| WDC       | WUS4BB096D7P3E4    | 960 GB | 4       | 43    | 0     | 0.12   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 3       | 43    | 0     | 0.12   |
| Samsung   | MZQL23T8HCLS-00... | 3.8 TB | 1       | 43    | 0     | 0.12   |
| Intel     | MDTPED1K750GA      | 752 GB | 2       | 41    | 0     | 0.11   |
| Dell      | Express Flash N... | 6.4 TB | 4       | 39    | 0     | 0.11   |
| Samsung   | SSD 980 PRO        | 250 GB | 2       | 37    | 0     | 0.10   |
| Kingston  | SKC2500M8500G      | 500 GB | 3       | 35    | 0     | 0.10   |
| Micron    | 7300_MTFDHBE6T4TDG | 6.4 TB | 24      | 34    | 0     | 0.09   |
| Silico... | NV900-1T           | 1 TB   | 1       | 30    | 0     | 0.08   |
| ADATA     | SX6000LNP          | 512 GB | 1       | 30    | 0     | 0.08   |
| Samsung   | MZVL21T0HCLR-00B00 | 1 TB   | 6       | 28    | 0     | 0.08   |
| Toshiba   | KXG6AZNV512G       | 512 GB | 12      | 27    | 0     | 0.07   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 1       | 24    | 0     | 0.07   |
| WDC       | WUS4BB038D7P3E4    | 3.8 TB | 6       | 24    | 0     | 0.07   |
| ADATA     | SX6000PNP          | 256 GB | 2       | 22    | 0     | 0.06   |
| Micron    | MTFDHBA1T0TDV-1... | 1 TB   | 1       | 21    | 0     | 0.06   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 4       | 17    | 0     | 0.05   |
| Intel     | SSDPF2KX076TZ      | 7.6 TB | 5       | 15    | 0     | 0.04   |
| Wester... | WUS4BB096D7P3E4    | 960 GB | 4       | 13    | 0     | 0.04   |
| Wester... | WUS4CB032D7P3E4    | 3.2 TB | 4       | 11    | 0     | 0.03   |
| WDC       | WUS4CB032D7P3E4    | 3.2 TB | 5       | 9     | 0     | 0.03   |
| Intel     | SSDPELKX010T8      | 1 TB   | 2       | 9     | 0     | 0.03   |
| SK hynix  | BC501A NVMe        | 128 GB | 3       | 7     | 0     | 0.02   |
| KIOXIA    | KCD61LUL3T84       | 3.8 TB | 20      | 5     | 0     | 0.01   |
| Crucial   | CT500P5SSD8        | 500 GB | 5       | 4     | 0     | 0.01   |
| ADATA     | SX6000NP           | 128 GB | 1       | 615   | 142   | 0.01   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 1       | 4     | 0     | 0.01   |
| Micron    | 7300_MTFDHBG1T9TDF | 1.9 TB | 8       | 3     | 0     | 0.01   |
| Kingston  | SKC2500M82000G     | 2 TB   | 2       | 3     | 0     | 0.01   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 3       | 2     | 0     | 0.01   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 2       | 1     | 0     | 0.00   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 980            | 250 GB | 4       | 0     | 0     | 0.00   |
| Samsung   | SSD 980            | 1 TB   | 2       | 0     | 0     | 0.00   |

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
| SPCC        | 1      | 1       | 789   | 0     | 2.16   |
| Intel       | 76     | 1871    | 777   | 2     | 2.12   |
| PNY         | 1      | 2       | 589   | 0     | 1.62   |
| Smartbuy    | 1      | 1       | 493   | 0     | 1.35   |
| Phison      | 3      | 11      | 334   | 0     | 0.92   |
| Samsung     | 76     | 2212    | 334   | 3     | 0.90   |
| HGST        | 1      | 24      | 290   | 0     | 0.80   |
| Seagate     | 1      | 10      | 287   | 0     | 0.79   |
| Toshiba     | 12     | 213     | 281   | 0     | 0.77   |
| WDC         | 29     | 2210    | 278   | 1     | 0.76   |
| HP          | 2      | 17      | 271   | 0     | 0.74   |
| Huawei      | 3      | 7       | 263   | 0     | 0.72   |
| Dell        | 17     | 477     | 258   | 3     | 0.70   |
| Gigabyte    | 1      | 10      | 254   | 0     | 0.70   |
| Western ... | 13     | 1374    | 241   | 0     | 0.66   |
| Kingston    | 12     | 46      | 192   | 0     | 0.53   |
| Corsair     | 3      | 33      | 190   | 0     | 0.52   |
| Patriot     | 2      | 6       | 174   | 0     | 0.48   |
| XPG         | 1      | 1       | 168   | 0     | 0.46   |
| Micron      | 11     | 180     | 137   | 0     | 0.38   |
| ADATA       | 7      | 14      | 157   | 11    | 0.31   |
| Silicon ... | 2      | 2       | 103   | 0     | 0.28   |
| Crucial     | 4      | 12      | 62    | 0     | 0.17   |
| SK hynix    | 5      | 8       | 61    | 0     | 0.17   |
| Team        | 1      | 1       | 45    | 0     | 0.13   |
| KIOXIA      | 2      | 30      | 39    | 0     | 0.11   |

