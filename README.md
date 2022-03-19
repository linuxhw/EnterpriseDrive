Reliability Test For Enterprise Hard Drives
===========================================

This is a project to estimate reliability of enterprise HDD/SSD drives by the analysis
of SMART reports from servers. The primary aim of the project is to find drives with
longest power-on hours (POH) and minimal number of errors, i.e. maximal MTBF (mean time
between failures).

Everyone can contribute to this report by installing [hw-probe](https://github.com/linuxhw/hw-probe) to
their [OpenVZ 7](https://wiki.openvz.org/) servers:

    sudo -E hw-probe -all -upload

Total drives: 58564.

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

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| WDC       | WD740ADFD-00NLR5   | 74 GB  | 1       | 4658  | 0     | 12.76  |
| Hitachi   | HDS725050KLA360    | 500 GB | 1       | 4610  | 0     | 12.63  |
| WDC       | WD5000AAKS-00A7B2  | 500 GB | 1       | 3899  | 0     | 10.68  |
| Hitachi   | HDS721010KLA33R... | 1 TB   | 1       | 3863  | 0     | 10.58  |
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 2       | 3814  | 0     | 10.45  |
| WDC       | WD5000AAKS-22A7B0  | 500 GB | 1       | 3793  | 0     | 10.39  |
| Maxtor    | STM3250310AS       | 250 GB | 2       | 3760  | 0     | 10.30  |
| Seagate   | ST32500NSSUN250G   | 250 GB | 2       | 3676  | 0     | 10.07  |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 3       | 3659  | 0     | 10.03  |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 18      | 3987  | 1     | 9.62   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 3       | 3237  | 0     | 8.87   |
| Seagate   | ST3320620AS        | 320 GB | 3       | 4466  | 5     | 8.55   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 4       | 3016  | 0     | 8.26   |
| WDC       | WD5000AAKS-00E4A0  | 500 GB | 1       | 3014  | 0     | 8.26   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 16      | 3401  | 16    | 8.23   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 8       | 3433  | 1     | 8.20   |
| HP        | GB0500EAFYL        | 500 GB | 2       | 2973  | 0     | 8.15   |
| WDC       | WD5000AAKS-00V6A0  | 500 GB | 1       | 2965  | 0     | 8.12   |
| WDC       | WD10EACS-00ZJB0    | 1 TB   | 1       | 2955  | 0     | 8.10   |
| Hitachi   | HUA722020ALA330... | 2 TB   | 1       | 2886  | 0     | 7.91   |
| Samsung   | HD250HJ            | 250 GB | 1       | 2882  | 0     | 7.90   |
| WDC       | WD10EZRX-00A8LB0   | 1 TB   | 1       | 2874  | 0     | 7.87   |
| Toshiba   | DT01ABA300         | 3 TB   | 1       | 2857  | 0     | 7.83   |
| Hitachi   | HDS721050CLA360    | 500 GB | 2       | 2828  | 0     | 7.75   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 8       | 3043  | 22    | 7.73   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 92      | 3158  | 16    | 7.73   |
| WDC       | WD10EARS-00MVWB0   | 1 TB   | 1       | 2778  | 0     | 7.61   |
| Hitachi   | HUA723020ALA640... | 2 TB   | 1       | 2743  | 0     | 7.52   |
| Seagate   | ST3320620A         | 320 GB | 2       | 2728  | 0     | 7.47   |
| WDC       | WD1002FBYS-50A6B1  | 1 TB   | 1       | 2722  | 0     | 7.46   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 23      | 2795  | 1     | 7.43   |
| WDC       | WD10EALX-759BA1    | 1 TB   | 1       | 2664  | 0     | 7.30   |
| HPE       | MB0500GCEHF        | 500 GB | 1       | 2651  | 0     | 7.26   |
| WDC       | WD1600JD-75HBB0    | 160 GB | 1       | 2640  | 0     | 7.23   |
| Hitachi   | HUA722010CLA330... | 1 TB   | 1       | 2619  | 0     | 7.18   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 17      | 2916  | 2     | 7.17   |
| Seagate   | ST2000VX000-1CU164 | 2 TB   | 1       | 2579  | 0     | 7.07   |
| WDC       | WD2500AAJS-22L7A0  | 250 GB | 1       | 2570  | 0     | 7.04   |
| Samsung   | HD502HJ            | 500 GB | 4       | 2564  | 0     | 7.03   |
| Samsung   | HD753LJ            | 752 GB | 1       | 2559  | 0     | 7.01   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 2       | 2547  | 0     | 6.98   |
| Seagate   | ST3250620NS        | 250 GB | 4       | 2532  | 0     | 6.94   |
| HP        | GB0250EAFYK        | 250 GB | 2       | 2531  | 0     | 6.93   |
| WDC       | WD3200AAKS-61L9A0  | 320 GB | 1       | 2526  | 0     | 6.92   |
| WDC       | WD10EADS-00L5B1    | 1 TB   | 1       | 2526  | 0     | 6.92   |
| HP        | GB0500C4413        | 500 GB | 2       | 3306  | 1     | 6.90   |
| WDC       | WD5000AACS-00G8B1  | 500 GB | 2       | 4393  | 3     | 6.87   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 34      | 2895  | 61    | 6.82   |
| HP        | MB2000EBUCF        | 2 TB   | 2       | 2458  | 0     | 6.74   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 5       | 2803  | 1     | 6.71   |
| Hitachi   | HUA722050CLA330    | 500 GB | 3       | 2440  | 0     | 6.69   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 2       | 2433  | 0     | 6.67   |
| Seagate   | ST32000646NS       | 2 TB   | 2       | 2424  | 0     | 6.64   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 32      | 2508  | 1     | 6.63   |
| Seagate   | ST3250410AS        | 250 GB | 4       | 3467  | 85    | 6.60   |
| WDC       | WD1500HLFS-01G6U0  | 150 GB | 1       | 2403  | 0     | 6.59   |
| HP        | MB1000GCWCV        | 1 TB   | 3       | 2387  | 0     | 6.54   |
| HGST      | HUS724020ALE640    | 2 TB   | 1       | 2373  | 0     | 6.50   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 2       | 2359  | 0     | 6.46   |
| Hitachi   | HDS721010CLA330    | 1 TB   | 1       | 2342  | 0     | 6.42   |
| WDC       | WD7502AAEX-00Y9A0  | 752 GB | 4       | 2329  | 0     | 6.38   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 10      | 3101  | 3     | 6.33   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 3       | 2254  | 0     | 6.18   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 6       | 2652  | 2     | 6.17   |
| HGST      | HDS724040ALE640    | 4 TB   | 7       | 2243  | 0     | 6.15   |
| HP        | GB1000EAMYC        | 1 TB   | 1       | 2228  | 0     | 6.11   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 13      | 2789  | 3     | 6.06   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 10      | 2892  | 9     | 6.05   |
| Seagate   | ST2000NC000-1CX164 | 2 TB   | 1       | 2192  | 0     | 6.01   |
| WDC       | WD5000AAKS-22V1A0  | 500 GB | 1       | 2188  | 0     | 6.00   |
| WDC       | WD1001FALS-00E8B0  | 1 TB   | 1       | 2171  | 0     | 5.95   |
| Hitachi   | HDP725050GLA360    | 500 GB | 3       | 2156  | 0     | 5.91   |
| WDC       | WD6001FSYZ-01SS7B0 | 6 TB   | 3       | 2150  | 0     | 5.89   |
| Toshiba   | MD04ACA500         | 5 TB   | 2       | 2148  | 0     | 5.89   |
| Seagate   | ST3000VX000-1CU166 | 3 TB   | 27      | 2572  | 5     | 5.87   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 42      | 2269  | 1     | 5.84   |
| Seagate   | ST3320620NS        | 320 GB | 4       | 2189  | 1     | 5.81   |
| Seagate   | ST2000VX000-1ES164 | 2 TB   | 2       | 2105  | 0     | 5.77   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 42      | 2220  | 1     | 5.74   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 2       | 2067  | 0     | 5.67   |
| Seagate   | ST3400620AS        | 400 GB | 1       | 2060  | 0     | 5.65   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 4       | 2053  | 0     | 5.63   |
| WDC       | WD3000HLFS-01G6U4  | 304 GB | 2       | 3664  | 16    | 5.58   |
| WDC       | WD1600AAJS-08L7A0  | 160 GB | 1       | 2027  | 0     | 5.56   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 5       | 2014  | 0     | 5.52   |
| HGST      | HUS724020ALA640    | 2 TB   | 231     | 2084  | 10    | 5.49   |
| Seagate   | ST750LX003-1AC154  | 752 GB | 2       | 3002  | 1     | 5.48   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 2       | 1995  | 0     | 5.47   |
| Seagate   | ST2000NM0033       | 2 TB   | 1       | 1988  | 0     | 5.45   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 4       | 1982  | 0     | 5.43   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 9       | 2204  | 1     | 5.43   |
| HP        | MB1000GDUNU        | 1 TB   | 1       | 1969  | 0     | 5.40   |
| WDC       | WD2004FBYZ-01YCBB0 | 2 TB   | 5       | 1966  | 0     | 5.39   |
| WDC       | WD10EZEX-22RKKA0   | 1 TB   | 4       | 2345  | 1     | 5.36   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 442     | 2387  | 115   | 5.34   |
| Maxtor    | 6V160E0            | 160 GB | 2       | 1932  | 0     | 5.29   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 2       | 1929  | 0     | 5.29   |
| Seagate   | ST91000640NS       | 1 TB   | 44      | 2126  | 2     | 5.24   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 2       | 2729  | 1008  | 5.23   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 8       | 2115  | 11    | 5.22   |
| HGST      | HUS726060ALE614    | 6 TB   | 148     | 2076  | 12    | 5.17   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 4       | 2862  | 4     | 5.12   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 2       | 1864  | 0     | 5.11   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 22      | 1919  | 7     | 5.05   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 18      | 2470  | 3     | 5.01   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 2       | 1821  | 0     | 4.99   |
| WDC       | WD2002FYPS-01U1B1  | 2 TB   | 17      | 2931  | 208   | 4.97   |
| WDC       | WD2500AAJS-00B4A0  | 250 GB | 1       | 1814  | 0     | 4.97   |
| HGST      | HUH728080ALE604    | 8 TB   | 62      | 1852  | 5     | 4.94   |
| Toshiba   | MQ01UBD050         | 500 GB | 12      | 1889  | 1     | 4.94   |
| Hitachi   | HDT725032VLA360    | 320 GB | 5       | 3663  | 7     | 4.90   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 15      | 1775  | 0     | 4.87   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 7       | 1767  | 0     | 4.84   |
| Toshiba   | HDWE160            | 6 TB   | 74      | 1880  | 2     | 4.84   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 19      | 1839  | 13    | 4.83   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 37      | 2079  | 37    | 4.82   |
| HP        | GB0160EAFJE        | 160 GB | 2       | 2937  | 513   | 4.82   |
| WDC       | WD5000BHTZ-04JCPV0 | 500 GB | 1       | 1758  | 0     | 4.82   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 7       | 2607  | 1     | 4.81   |
| Toshiba   | MK0502TSKB         | 500 GB | 1       | 1752  | 0     | 4.80   |
| Seagate   | ST2000NM0024-1H... | 2 TB   | 9       | 1744  | 0     | 4.78   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 20      | 1981  | 22    | 4.77   |
| WDC       | WD20EADS-00R6B0    | 2 TB   | 2       | 3219  | 6     | 4.75   |
| WDC       | WD10EZEX-22BN5A0   | 1 TB   | 1       | 1730  | 0     | 4.74   |
| Toshiba   | MK1002TSKB         | 1 TB   | 12      | 1723  | 0     | 4.72   |
| Seagate   | ST3500630AS        | 500 GB | 1       | 1720  | 0     | 4.71   |
| Seagate   | ST6000NM0004-1F... | 6 TB   | 12      | 1708  | 0     | 4.68   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 3       | 1707  | 0     | 4.68   |
| WDC       | WD4001FFSX-68JNUN0 | 4 TB   | 12      | 2048  | 1     | 4.68   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 62      | 2015  | 40    | 4.66   |
| Samsung   | HD103UJ            | 1 TB   | 26      | 2912  | 144   | 4.64   |
| Seagate   | ST6000NM0024-1H... | 6 TB   | 1694    | 2020  | 19    | 4.58   |
| HGST      | HUH728080ALE601    | 8 TB   | 19      | 1662  | 0     | 4.55   |
| WDC       | WD20EARX-00MMMB0   | 2 TB   | 2       | 2762  | 2     | 4.55   |
| Seagate   | ST3500630NS        | 500 GB | 9       | 1654  | 0     | 4.53   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 7       | 2143  | 1     | 4.52   |
| WDC       | WD1500HLHX-01JJPV0 | 150 GB | 1       | 1647  | 0     | 4.51   |
| Seagate   | ST500NM0011 00W... | 500 GB | 2       | 1647  | 0     | 4.51   |
| WDC       | WD5003ABYX-23 0... | 500 GB | 2       | 1645  | 0     | 4.51   |
| Seagate   | ST33000651AS       | 3 TB   | 4       | 2352  | 10    | 4.50   |
| HGST      | HUS726030ALA610    | 3 TB   | 47      | 1665  | 1     | 4.50   |
| WDC       | WD2001FFSX-68JNUN0 | 2 TB   | 3       | 1996  | 1     | 4.47   |
| Seagate   | ST3000NC002-1DY166 | 3 TB   | 1       | 1627  | 0     | 4.46   |
| WDC       | WD5000AAKX-003CA0  | 500 GB | 3       | 2229  | 3     | 4.45   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 5       | 2547  | 5     | 4.45   |
| WDC       | WD6402AAEX-00Y9A0  | 640 GB | 3       | 2411  | 677   | 4.43   |
| Hitachi   | HDT721050SLA360    | 500 GB | 1       | 1617  | 0     | 4.43   |
| HGST      | HDN724040ALE640    | 4 TB   | 22      | 1798  | 92    | 4.42   |
| WDC       | WD1000CHTZ-04JCPV1 | 1 TB   | 4       | 1611  | 0     | 4.42   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 57      | 2156  | 25    | 4.42   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 16      | 1927  | 2     | 4.39   |
| WDC       | WD40PURX-64NZ6Y0   | 4 TB   | 4       | 1589  | 0     | 4.35   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 25      | 2222  | 185   | 4.35   |
| WDC       | WD5000HHTZ-04N21V0 | 500 GB | 1       | 1567  | 0     | 4.29   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 7       | 2160  | 2     | 4.28   |
| HGST      | HTE541010A9E680    | 1 TB   | 6       | 1563  | 0     | 4.28   |
| HGST      | HDN724030ALE640    | 3 TB   | 8       | 1558  | 0     | 4.27   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 7       | 1828  | 16    | 4.21   |
| WDC       | WD101KRYZ-01JPDB0  | 10 TB  | 1       | 1534  | 0     | 4.20   |
| HP        | MB1000GCEHH        | 1 TB   | 4       | 3041  | 578   | 4.20   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 36      | 2027  | 50    | 4.20   |
| WDC       | WD2003FYPS-02W0B1  | 2 TB   | 2       | 1531  | 0     | 4.20   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 29      | 1737  | 211   | 4.19   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 14      | 1527  | 0     | 4.19   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 5       | 1523  | 0     | 4.17   |
| HGST      | HUH728080ALE600    | 8 TB   | 20      | 1521  | 0     | 4.17   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 152     | 1815  | 83    | 4.16   |
| WDC       | WD4000FYYZ-03UL1B3 | 4 TB   | 2       | 1511  | 0     | 4.14   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 6       | 2038  | 2     | 4.14   |
| HGST      | HUS724040ALA640    | 4 TB   | 149     | 1602  | 2     | 4.13   |
| WDC       | WD4003FZEX-00Z4SA0 | 4 TB   | 16      | 1504  | 0     | 4.12   |
| Seagate   | ST6000VX0001-1S... | 6 TB   | 4       | 1500  | 0     | 4.11   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 4       | 2800  | 4     | 4.10   |
| WDC       | WD100PURZ-85W86Y0  | 10 TB  | 1       | 1497  | 0     | 4.10   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 33      | 1496  | 0     | 4.10   |
| Toshiba   | DT01ACA300         | 3 TB   | 78      | 1782  | 22    | 4.09   |
| WDC       | WD2003FYYS-05T8B0  | 2 TB   | 2       | 1487  | 0     | 4.08   |
| Seagate   | ST320DM000-1BC14C  | 320 GB | 2       | 1479  | 0     | 4.05   |
| Seagate   | ST1000LM014-1EJ164 | 1 TB   | 1       | 1479  | 0     | 4.05   |
| WDC       | WD5000AZLX-07K2TA0 | 500 GB | 1       | 1475  | 0     | 4.04   |
| WDC       | WD2500HHTZ-04N21V0 | 250 GB | 3       | 1473  | 0     | 4.04   |
| Seagate   | ST500NM0011        | 500 GB | 11      | 2153  | 4     | 4.03   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 69      | 1538  | 8     | 4.02   |
| WDC       | WD800JD-60LUA0     | 80 GB  | 1       | 1465  | 0     | 4.01   |
| Seagate   | ST9250610NS        | 250 GB | 10      | 1593  | 1     | 3.98   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 4       | 1451  | 0     | 3.98   |
| WDC       | WD5002AALX-32Z3A0  | 500 GB | 8       | 1449  | 0     | 3.97   |
| Toshiba   | MG04ACA600E        | 6 TB   | 778     | 1541  | 16    | 3.97   |
| WDC       | WD10EALX-089BA0    | 1 TB   | 7       | 1914  | 2     | 3.97   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 2       | 1448  | 0     | 3.97   |
| HGST      | HUS724040ALE640    | 4 TB   | 22      | 1444  | 0     | 3.96   |
| WDC       | WD2000FYYZ-03UL1B2 | 2 TB   | 1       | 1440  | 0     | 3.95   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 19      | 2869  | 392   | 3.94   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 52      | 1775  | 1     | 3.94   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 4       | 1556  | 1     | 3.91   |
| WDC       | WD2000FYYZ-01UL1B3 | 2 TB   | 1       | 1427  | 0     | 3.91   |
| Samsung   | SP0812C            | 80 GB  | 1       | 1426  | 0     | 3.91   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 16      | 1707  | 1     | 3.90   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 9       | 1755  | 42    | 3.89   |
| Toshiba   | MK2002TSKB         | 2 TB   | 3       | 2317  | 4     | 3.88   |
| Toshiba   | MK2035GSS          | 200 GB | 1       | 1412  | 0     | 3.87   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 21      | 1638  | 76    | 3.82   |
| WDC       | WD20EADS-65R6B1    | 2 TB   | 1       | 2788  | 1     | 3.82   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 32      | 1982  | 137   | 3.82   |
| HGST      | HUS724030ALA640    | 3 TB   | 39      | 1685  | 71    | 3.81   |
| HGST      | HDN726040ALE614    | 4 TB   | 23      | 1379  | 0     | 3.78   |
| Seagate   | ST3000VX006-1HH166 | 3 TB   | 4       | 1378  | 0     | 3.78   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 6       | 2152  | 3     | 3.77   |
| WDC       | WD5000AUDX-61WNHY0 | 500 GB | 1       | 1373  | 0     | 3.76   |
| WDC       | WD5000BMVW-11AJGS2 | 500 GB | 2       | 1372  | 0     | 3.76   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 7       | 2160  | 401   | 3.75   |
| WDC       | WD1003FBYX-50Y7B1  | 1 TB   | 3       | 1368  | 0     | 3.75   |
| Seagate   | ST9500620NS        | 500 GB | 27      | 1548  | 1     | 3.75   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 10      | 1467  | 1     | 3.74   |
| HGST      | HDN726060ALE614    | 6 TB   | 2       | 1358  | 0     | 3.72   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 24      | 1439  | 1     | 3.72   |
| WDC       | WD10EZEX-00MFCA0   | 1 TB   | 1       | 1356  | 0     | 3.72   |
| WDC       | WD1600AAJS-00YZCA0 | 160 GB | 1       | 1356  | 0     | 3.72   |
| WDC       | WD10EZEX-21WN4A0   | 1 TB   | 1       | 1355  | 0     | 3.71   |
| WDC       | WD2004FBYZ-01YCBB2 | 2 TB   | 1       | 1350  | 0     | 3.70   |
| Seagate   | ST33000650NS       | 3 TB   | 24      | 2310  | 63    | 3.70   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 44      | 1559  | 8     | 3.69   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 288     | 2111  | 18    | 3.69   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 128     | 1610  | 7     | 3.67   |
| Toshiba   | DT01ACA100         | 1 TB   | 39      | 1545  | 27    | 3.67   |
| Toshiba   | MG04ACA600EY       | 6 TB   | 2       | 1330  | 0     | 3.65   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 3       | 1328  | 0     | 3.64   |
| Toshiba   | MQ01ABF050         | 500 GB | 1       | 1320  | 0     | 3.62   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 20      | 1430  | 186   | 3.62   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 6       | 1316  | 0     | 3.61   |
| WDC       | WD5003AZEX-00S3DA0 | 500 GB | 24      | 1316  | 0     | 3.61   |
| WDC       | WD10SPZX-00Z10T0   | 1 TB   | 1       | 1315  | 0     | 3.60   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 2       | 1315  | 0     | 3.60   |
| Toshiba   | MK1661GSYG         | 160 GB | 8       | 1313  | 0     | 3.60   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 942     | 1437  | 22    | 3.59   |
| Hitachi   | HDS721075KLA330    | 752 GB | 1       | 3894  | 2     | 3.56   |
| Seagate   | ST8000DM005-2EH112 | 8 TB   | 216     | 1381  | 1     | 3.56   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 97      | 1691  | 124   | 3.54   |
| WDC       | WD5003ABYX-01WERA0 | 500 GB | 20      | 1611  | 2     | 3.54   |
| HGST      | HDN721010ALE604    | 10 TB  | 2       | 1290  | 0     | 3.54   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 10      | 2391  | 203   | 3.53   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 2       | 2317  | 4     | 3.53   |
| WDC       | WD2500BHTZ-04JCPV1 | 250 GB | 2       | 1279  | 0     | 3.51   |
| Toshiba   | MG03ACA100         | 1 TB   | 53      | 1296  | 2     | 3.51   |
| Seagate   | ST1000NM0018-2F... | 1 TB   | 36      | 1298  | 1     | 3.49   |
| HGST      | HUS726020ALE614    | 2 TB   | 79      | 1319  | 26    | 3.48   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 96      | 1379  | 13    | 3.47   |
| Toshiba   | MG04ACA200EY       | 2 TB   | 11      | 1376  | 1     | 3.47   |
| WDC       | WD5000BPKX-22HPJT0 | 500 GB | 5       | 1483  | 2     | 3.46   |
| Seagate   | ST6000VX0023-2E... | 6 TB   | 17      | 1336  | 4     | 3.45   |
| Seagate   | ST8000DM002-1YW112 | 8 TB   | 137     | 1376  | 13    | 3.45   |
| Hitachi   | HDS723030BLE640    | 3 TB   | 5       | 1872  | 51    | 3.45   |
| HGST      | HUS722T1TALA600    | 1 TB   | 30      | 1253  | 0     | 3.43   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 7       | 2296  | 3     | 3.43   |
| WDC       | WD20NMVW-11W68S0   | 2 TB   | 1       | 1251  | 0     | 3.43   |
| WDC       | WD1004FBYZ-01YCBB1 | 1 TB   | 7       | 1248  | 0     | 3.42   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 16      | 1381  | 1     | 3.42   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 5       | 1245  | 0     | 3.41   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 14      | 1435  | 2     | 3.40   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 12      | 1510  | 96    | 3.39   |
| HGST      | HUS726060ALE610    | 6 TB   | 30      | 1236  | 0     | 3.39   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 8       | 1231  | 0     | 3.38   |
| HGST      | HUH728060ALE600    | 6 TB   | 3       | 1231  | 0     | 3.37   |
| Samsung   | HD103SJ            | 1 TB   | 23      | 2135  | 4     | 3.37   |
| WDC       | WD4002FYYZ-01B7CB0 | 4 TB   | 62      | 1436  | 6     | 3.36   |
| Toshiba   | MQ01ABD050         | 500 GB | 1       | 1222  | 0     | 3.35   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 10      | 1252  | 116   | 3.33   |
| Maxtor    | STM3500630AS       | 500 GB | 2       | 1214  | 0     | 3.33   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 34      | 1789  | 29    | 3.31   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 2       | 1201  | 0     | 3.29   |
| Samsung   | HD161GJ            | 160 GB | 3       | 1200  | 0     | 3.29   |
| Seagate   | ST8000NM0205-2F... | 8 TB   | 31      | 1300  | 66    | 3.27   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 27      | 1239  | 1     | 3.26   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 10      | 1272  | 1     | 3.26   |
| HGST      | HUS726020ALE610    | 2 TB   | 11      | 1189  | 0     | 3.26   |
| MaxDig... | MD4000GBDS         | 4 TB   | 1       | 1187  | 0     | 3.25   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 45      | 1187  | 20    | 3.25   |
| Seagate   | ST4000VX000-1F4168 | 4 TB   | 4       | 1182  | 0     | 3.24   |
| Seagate   | ST3160318AS        | 160 GB | 1       | 2359  | 1     | 3.23   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 22      | 1272  | 5     | 3.21   |
| Seagate   | ST2000VN0001-1S... | 2 TB   | 4       | 1167  | 0     | 3.20   |
| WDC       | WD10EZEX-00UD2A0   | 1 TB   | 1       | 1166  | 0     | 3.20   |
| WDC       | WD5000BMVW-11AJGS4 | 500 GB | 4       | 1157  | 0     | 3.17   |
| Hitachi   | HDT725050VLA360    | 500 GB | 1       | 1157  | 0     | 3.17   |
| WDC       | WD1003FBYZ-010FB0  | 1 TB   | 65      | 1215  | 1     | 3.16   |
| Toshiba   | MG04ACA300E        | 3 TB   | 1       | 1147  | 0     | 3.14   |
| HGST      | HUS726040ALA614    | 4 TB   | 19      | 1284  | 4     | 3.14   |
| WDC       | WD10EALS-00Z8A0    | 1 TB   | 7       | 2354  | 5     | 3.14   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 2       | 1146  | 0     | 3.14   |
| WDC       | WD3001FAEX-00MJRA0 | 3 TB   | 1       | 1140  | 0     | 3.13   |
| HPE       | MB0500GCEHE        | 500 GB | 6       | 1139  | 0     | 3.12   |
| HGST      | HUH721008ALE601    | 8 TB   | 6       | 1139  | 0     | 3.12   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 45      | 1737  | 11    | 3.11   |
| WDC       | WD3000HLHX-01JJPV0 | 304 GB | 6       | 1452  | 2     | 3.11   |
| Hitachi   | HDS721050CLA362    | 500 GB | 6       | 1905  | 459   | 3.10   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 4       | 1130  | 0     | 3.10   |
| Seagate   | ST1000NM0011       | 1 TB   | 30      | 1705  | 77    | 3.09   |
| WDC       | WD5000HHTZ-04N21V1 | 500 GB | 3       | 1128  | 0     | 3.09   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 17      | 1352  | 1     | 3.09   |
| Toshiba   | DT01ACA200         | 2 TB   | 294     | 1178  | 18    | 3.08   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 22      | 1565  | 96    | 3.08   |
| Seagate   | ST3500413AS        | 500 GB | 5       | 1525  | 14    | 3.07   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 8       | 1646  | 274   | 3.04   |
| Seagate   | ST3250310AS        | 250 GB | 3       | 2258  | 209   | 3.04   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 4       | 1105  | 0     | 3.03   |
| WDC       | WD5000BMVV-11GNWS0 | 500 GB | 1       | 1103  | 0     | 3.02   |
| WDC       | WD1003FBYX-12      | 1 TB   | 29      | 1177  | 1     | 3.01   |
| WDC       | WD3000FYYZ-01UL1B2 | 3 TB   | 9       | 1778  | 3     | 3.01   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 2       | 1094  | 0     | 3.00   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 42      | 1195  | 1     | 2.99   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 42      | 1576  | 49    | 2.99   |
| WDC       | WD5000BHTZ-04JCPV1 | 500 GB | 6       | 1084  | 0     | 2.97   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 18      | 1793  | 927   | 2.97   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 3       | 2428  | 732   | 2.95   |
| WDC       | WD101KFBX-68R56N0  | 10 TB  | 1       | 1075  | 0     | 2.95   |
| WDC       | WD800AAJS-00PSA0   | 80 GB  | 1       | 1072  | 0     | 2.94   |
| HGST      | HUS726040ALE610    | 4 TB   | 23      | 1071  | 0     | 2.94   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 42      | 1964  | 26    | 2.92   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 10      | 1065  | 0     | 2.92   |
| Seagate   | ST6000NM0235-2A... | 6 TB   | 9       | 1065  | 0     | 2.92   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 2       | 1745  | 4     | 2.91   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 24      | 1832  | 71    | 2.91   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 23      | 1058  | 0     | 2.90   |
| WDC       | WD2003FYYS-27Y2P0  | 2 TB   | 2       | 1542  | 2     | 2.90   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 5       | 1588  | 1     | 2.90   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 9       | 1600  | 7     | 2.90   |
| MediaMax  | WL2000GSA6472E     | 2 TB   | 1       | 1053  | 0     | 2.89   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 16      | 1500  | 459   | 2.88   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 87      | 1163  | 1     | 2.88   |
| Seagate   | ST31000NSSUN1.0T   | 1 TB   | 1       | 2095  | 1     | 2.87   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 18      | 1262  | 13    | 2.87   |
| HGST      | HUS726040ALE614    | 4 TB   | 14      | 1127  | 3     | 2.87   |
| Toshiba   | MG04ACA400EY       | 4 TB   | 14      | 1045  | 0     | 2.86   |
| Toshiba   | MG03ACA200         | 2 TB   | 9       | 1280  | 224   | 2.86   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 5       | 1043  | 0     | 2.86   |
| Toshiba   | MG03ACA400         | 4 TB   | 24      | 1532  | 3     | 2.86   |
| WDC       | WD5003ABYX-01WERA1 | 500 GB | 18      | 1236  | 1     | 2.86   |
| WDC       | WD4000FYYZ-01UL1B2 | 4 TB   | 27      | 1925  | 102   | 2.85   |
| Seagate   | ST4000DX001-1CE168 | 4 TB   | 2       | 1038  | 0     | 2.85   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 46      | 1553  | 28    | 2.85   |
| Toshiba   | HDWD120            | 2 TB   | 10      | 1035  | 0     | 2.84   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 5       | 2535  | 28    | 2.83   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 13      | 1265  | 49    | 2.82   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 8       | 1025  | 0     | 2.81   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 7       | 2023  | 15    | 2.81   |
| MediaMax  | WL500GSA3272       | 500 GB | 1       | 1018  | 0     | 2.79   |
| HGST      | HUH721010ALE604    | 10 TB  | 111     | 1013  | 0     | 2.78   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 2       | 1112  | 1     | 2.74   |
| HGST      | HTE721010A9E630    | 1 TB   | 2       | 1867  | 8     | 2.74   |
| HGST      | HUS722T1TALA604    | 1 TB   | 124     | 1010  | 10    | 2.74   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 11      | 995   | 0     | 2.73   |
| Samsung   | HD204UI            | 2 TB   | 3       | 1908  | 3     | 2.72   |
| Hitachi   | HDS721032CLA362    | 320 GB | 3       | 1673  | 571   | 2.72   |
| WDC       | WD1502FAEX-007BA0  | 1.5 TB | 2       | 1534  | 5     | 2.72   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 6       | 1257  | 1     | 2.71   |
| Samsung   | HD322HJ            | 320 GB | 2       | 2738  | 508   | 2.71   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 140     | 1037  | 10    | 2.71   |
| WDC       | WD8002FRYZ-01FF2B0 | 8 TB   | 14      | 1020  | 1     | 2.71   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 4       | 2351  | 260   | 2.67   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 8       | 972   | 0     | 2.66   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 3       | 1301  | 339   | 2.66   |
| Seagate   | ST1000DX001-1NS162 | 1 TB   | 6       | 1744  | 219   | 2.64   |
| Toshiba   | HDWD105            | 500 GB | 5       | 964   | 0     | 2.64   |
| Toshiba   | MG04ACA400N        | 4 TB   | 6       | 1254  | 3     | 2.64   |
| WDC       | WD2000F9YZ-09N20L1 | 2 TB   | 4       | 962   | 0     | 2.64   |
| WDC       | WD2500AAJS-00VTA0  | 250 GB | 1       | 962   | 0     | 2.64   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 2       | 958   | 0     | 2.63   |
| Fujitsu   | MHW2120BH          | 120 GB | 1       | 946   | 0     | 2.59   |
| Seagate   | ST380815AS         | 80 GB  | 5       | 944   | 0     | 2.59   |
| Hitachi   | HDP725025GLA380    | 250 GB | 2       | 4427  | 6     | 2.58   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 7       | 935   | 0     | 2.56   |
| HGST      | HUH721212ALN600    | 12 TB  | 12      | 1036  | 21    | 2.56   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 33      | 2042  | 22    | 2.56   |
| Seagate   | ST2000NM0125-1Y... | 2 TB   | 13      | 926   | 0     | 2.54   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 51      | 1219  | 10    | 2.54   |
| HGST      | HUS726020ALA610    | 2 TB   | 155     | 981   | 16    | 2.54   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 10      | 1172  | 2     | 2.52   |
| WDC       | WD1005FBYZ-01YCBB2 | 1 TB   | 23      | 968   | 1     | 2.52   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 3       | 917   | 0     | 2.51   |
| HGST      | HUS726040ALA610    | 4 TB   | 73      | 942   | 1     | 2.50   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 15      | 1071  | 1     | 2.46   |
| Toshiba   | DT01ACA050         | 500 GB | 19      | 1035  | 129   | 2.43   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 11      | 927   | 1     | 2.42   |
| HGST      | HUH721010ALN600    | 10 TB  | 16      | 882   | 0     | 2.42   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 48      | 939   | 3     | 2.41   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 6       | 879   | 0     | 2.41   |
| Seagate   | ST10000NM0196-2... | 10 TB  | 210     | 961   | 40    | 2.40   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 3       | 874   | 0     | 2.40   |
| HGST      | HUH721212ALN604    | 12 TB  | 2122    | 912   | 2     | 2.39   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 16      | 871   | 0     | 2.39   |
| Seagate   | ST3160811AS        | 160 GB | 2       | 1240  | 5     | 2.38   |
| Samsung   | HD103SI            | 1 TB   | 3       | 3356  | 806   | 2.38   |
| Seagate   | ST2000NM0018-2F... | 2 TB   | 1       | 868   | 0     | 2.38   |
| Seagate   | ST10000NM0016-1... | 10 TB  | 1548    | 1441  | 83    | 2.38   |
| HPE       | MM1000GBKAL        | 1 TB   | 21      | 1205  | 2     | 2.37   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 4       | 2010  | 4     | 2.36   |
| HPE       | MM1000GFJTE        | 1 TB   | 4       | 862   | 0     | 2.36   |
| Seagate   | ST12000DM0007-2... | 12 TB  | 5       | 860   | 0     | 2.36   |
| HGST      | HUH728060ALE604    | 6 TB   | 14      | 1278  | 28    | 2.34   |
| HGST      | HUS726060ALA640    | 6 TB   | 46      | 895   | 1     | 2.33   |
| Seagate   | ST3400620NS        | 400 GB | 1       | 1695  | 1     | 2.32   |
| WDC       | WD50EFRX-68L0BN1   | 5 TB   | 6       | 1559  | 118   | 2.32   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 208     | 874   | 3     | 2.31   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 41      | 875   | 26    | 2.31   |
| Seagate   | ST10000VN0004-2... | 10 TB  | 4       | 1106  | 10    | 2.31   |
| HGST      | HUH721008ALE600    | 8 TB   | 48      | 842   | 0     | 2.31   |
| WDC       | WD100EFAX-68LHPN0  | 10 TB  | 53      | 858   | 1     | 2.30   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 2       | 837   | 0     | 2.29   |
| Seagate   | ST3750640AS        | 752 GB | 1       | 2504  | 2     | 2.29   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 3       | 1043  | 1     | 2.28   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 61      | 831   | 0     | 2.28   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 191     | 894   | 17    | 2.28   |
| Hitachi   | HUS724040ALE640    | 4 TB   | 29      | 905   | 1     | 2.26   |
| Toshiba   | HDWT140            | 4 TB   | 2       | 824   | 0     | 2.26   |
| Seagate   | ST3300831AS        | 304 GB | 2       | 1236  | 1     | 2.26   |
| HPE       | MB0500EBNCR        | 500 GB | 5       | 1520  | 18    | 2.26   |
| Seagate   | ST1000VN002-2EY102 | 1 TB   | 4       | 823   | 0     | 2.26   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 3       | 818   | 0     | 2.24   |
| WDC       | WD2005FBYZ-01YCBB2 | 2 TB   | 43      | 831   | 44    | 2.24   |
| Seagate   | ST3250318AS        | 250 GB | 3       | 1375  | 17    | 2.22   |
| Seagate   | ST14000VN0008-2... | 14 TB  | 12      | 809   | 0     | 2.22   |
| WDC       | WD4000FYYZ-01UL1B3 | 4 TB   | 24      | 1190  | 17    | 2.22   |
| WDC       | WD5002ABYS-18B1B0  | 500 GB | 1       | 808   | 0     | 2.22   |
| WDC       | WD4000F9YZ-09N20L0 | 4 TB   | 4       | 805   | 0     | 2.21   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 139     | 875   | 14    | 2.20   |
| HP        | MB2000GCEHK        | 2 TB   | 2       | 1625  | 1051  | 2.20   |
| HP        | MB2000GCWDA        | 2 TB   | 2       | 802   | 0     | 2.20   |
| Toshiba   | HDWR21C            | 12 TB  | 5       | 801   | 0     | 2.20   |
| Seagate   | ST33000651NS       | 3 TB   | 1       | 801   | 0     | 2.20   |
| Seagate   | ST500DM009-2F110A  | 500 GB | 1       | 799   | 0     | 2.19   |
| Seagate   | ST3120022A         | 120 GB | 1       | 3197  | 3     | 2.19   |
| WDC       | WD30PURZ-85GU6Y0   | 3 TB   | 2       | 796   | 0     | 2.18   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 20      | 851   | 1     | 2.18   |
| Seagate   | ST10000DM0004-2... | 10 TB  | 7       | 1084  | 87    | 2.18   |
| WDC       | WD10EZEX-75M2NA0   | 1 TB   | 1       | 792   | 0     | 2.17   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 2       | 1354  | 3     | 2.15   |
| Seagate   | ST3500418AS        | 500 GB | 7       | 789   | 2     | 2.15   |
| HGST      | HUS726T6TALE6L4    | 6 TB   | 197     | 793   | 21    | 2.14   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 9       | 999   | 16    | 2.13   |
| WDC       | WD800JD-00HKA0     | 80 GB  | 1       | 776   | 0     | 2.13   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 3       | 771   | 0     | 2.11   |
| Seagate   | ST1000VX005-2EZ102 | 1 TB   | 3       | 770   | 0     | 2.11   |
| Toshiba   | MG05ACA800E        | 8 TB   | 677     | 808   | 4     | 2.11   |
| Toshiba   | MD04ACA400         | 4 TB   | 452     | 780   | 3     | 2.09   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 67      | 771   | 1     | 2.09   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 3       | 760   | 0     | 2.08   |
| Hitachi   | HDE721050SLA330    | 500 GB | 2       | 3797  | 4     | 2.08   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 19      | 864   | 2     | 2.07   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 3       | 1127  | 4     | 2.07   |
| Samsung   | HD154UI            | 1.5 TB | 5       | 3410  | 226   | 2.07   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 73      | 776   | 72    | 2.06   |
| HGST      | HUS722T2TALA604    | 2 TB   | 85      | 768   | 1     | 2.06   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 3       | 750   | 0     | 2.06   |
| MediaMax  | WL4000GSA6472      | 4 TB   | 2       | 747   | 0     | 2.05   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 19      | 738   | 0     | 2.02   |
| WDC       | WD5000AZLX-08K2TA0 | 500 GB | 5       | 737   | 0     | 2.02   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 27      | 736   | 39    | 2.01   |
| Seagate   | ST3500312CS        | 500 GB | 10      | 1001  | 3     | 2.01   |
| Seagate   | ST10000VN0004-1... | 10 TB  | 36      | 952   | 107   | 2.01   |
| HGST      | HUH721212ALE604    | 12 TB  | 175     | 734   | 1     | 2.00   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 6       | 1860  | 13    | 2.00   |
| Hitachi   | HTS723216L9SA60    | 160 GB | 1       | 727   | 0     | 1.99   |
| Seagate   | ST2000NX0423       | 2 TB   | 60      | 735   | 1     | 1.99   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 6       | 722   | 0     | 1.98   |
| WDC       | WD8003FFBX-68B9AN0 | 8 TB   | 3       | 719   | 0     | 1.97   |
| Seagate   | ST500DM005 HD502HJ | 500 GB | 1       | 716   | 0     | 1.96   |
| HPE       | MM2000GEFRA        | 2 TB   | 266     | 759   | 1     | 1.95   |
| Toshiba   | HDWU130            | 3 TB   | 8       | 800   | 8     | 1.94   |
| WDC       | WD3200AAJS-08L7A0  | 320 GB | 1       | 707   | 0     | 1.94   |
| Seagate   | ST12000NM0017-2... | 12 TB  | 2       | 704   | 0     | 1.93   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 50      | 757   | 18    | 1.93   |
| WDC       | WD1003FBYX-01Y7B2  | 1 TB   | 1       | 703   | 0     | 1.93   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 39      | 1000  | 222   | 1.92   |
| Toshiba   | HDWA130            | 3 TB   | 1       | 699   | 0     | 1.92   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 13      | 696   | 0     | 1.91   |
| Seagate   | ST16000NE000-2R... | 16 TB  | 2       | 694   | 0     | 1.90   |
| WDC       | WD5000AZLX-35K2TA0 | 500 GB | 3       | 694   | 0     | 1.90   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 106     | 790   | 21    | 1.89   |
| Seagate   | ST10000NE0004-1... | 10 TB  | 15      | 1257  | 373   | 1.88   |
| Seagate   | ST32000645NS       | 2 TB   | 88      | 745   | 15    | 1.88   |
| WDC       | WD5000AAKX-22ERMA0 | 500 GB | 1       | 680   | 0     | 1.86   |
| WDC       | WD2002FYPS-02W3B0  | 2 TB   | 1       | 679   | 0     | 1.86   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 32      | 941   | 20    | 1.86   |
| Seagate   | ST2000NX0403       | 2 TB   | 7       | 716   | 1     | 1.86   |
| Toshiba   | HDWE140            | 4 TB   | 43      | 697   | 42    | 1.85   |
| Seagate   | ST10000NM0156-2... | 10 TB  | 37      | 754   | 6     | 1.85   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 1       | 673   | 0     | 1.85   |
| Toshiba   | MG04ACA400E        | 4 TB   | 82      | 687   | 27    | 1.84   |
| HGST      | HUH721010ALE600    | 10 TB  | 220     | 672   | 1     | 1.82   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 17      | 799   | 117   | 1.82   |
| HGST      | HTS721010A9E630    | 1 TB   | 7       | 1244  | 721   | 1.82   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 8       | 695   | 1     | 1.81   |
| Seagate   | ST9500420ASG       | 500 GB | 6       | 1420  | 184   | 1.81   |
| WDC       | WD15EARS-00MVWB0   | 1.5 TB | 4       | 2054  | 324   | 1.81   |
| Seagate   | ST2000NX0253       | 2 TB   | 49      | 849   | 16    | 1.80   |
| Toshiba   | HDWD130            | 3 TB   | 8       | 673   | 2     | 1.79   |
| Seagate   | ST2000VX003-1HH164 | 2 TB   | 3       | 652   | 0     | 1.79   |
| WDC       | WD2500AAJS-08L7A0  | 250 GB | 1       | 1944  | 2     | 1.78   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 4       | 2029  | 3     | 1.78   |
| Hitachi   | HDS723030ALA640... | 3 TB   | 2       | 975   | 1     | 1.77   |
| Toshiba   | MG06ACA10TEY       | 10 TB  | 72      | 656   | 1     | 1.75   |
| Samsung   | HE103SJ            | 1 TB   | 1       | 637   | 0     | 1.75   |
| Seagate   | ST10000NM0146-2... | 10 TB  | 1       | 635   | 0     | 1.74   |
| Toshiba   | MQ01ACF050         | 500 GB | 6       | 834   | 2     | 1.73   |
| Seagate   | ST2000NM0055-1V... | 2 TB   | 22      | 866   | 1     | 1.73   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 6       | 627   | 0     | 1.72   |
| HP        | MB2000EAZNL        | 2 TB   | 2       | 800   | 2     | 1.71   |
| WDC       | WD10JMVW-11AJGS3   | 1 TB   | 1       | 624   | 0     | 1.71   |
| WDC       | WD4000FYYZ-01UL1B1 | 4 TB   | 10      | 1725  | 5     | 1.69   |
| Toshiba   | MG06ACA800EY       | 8 TB   | 27      | 649   | 4     | 1.69   |
| WDC       | WD5000AAKS-00V1A0  | 500 GB | 1       | 3066  | 4     | 1.68   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 3       | 611   | 0     | 1.67   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 3       | 609   | 0     | 1.67   |
| HGST      | HUS726T4TALE6L4    | 4 TB   | 63      | 609   | 0     | 1.67   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 2       | 1000  | 509   | 1.66   |
| WDC       | WD10EURX-63UY4Y0   | 1 TB   | 2       | 606   | 0     | 1.66   |
| HPE       | MB010000GWRTK      | 10 TB  | 24      | 638   | 51    | 1.66   |
| Seagate   | ST10000NM0568-2... | 10 TB  | 36      | 605   | 0     | 1.66   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 46      | 644   | 26    | 1.66   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 62      | 632   | 1     | 1.66   |
| WDC       | WD121KRYZ-01W0RB0  | 12 TB  | 9       | 789   | 1     | 1.65   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 37      | 601   | 0     | 1.65   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 38      | 624   | 2     | 1.63   |
| WDC       | WD3000FYYZ-01UL1B3 | 3 TB   | 5       | 591   | 0     | 1.62   |
| HPE       | MB001000GWFGF      | 1 TB   | 1       | 589   | 0     | 1.62   |
| Seagate   | ST8000DM0004-1Z... | 8 TB   | 10      | 1026  | 317   | 1.61   |
| Toshiba   | MG07ACA12TEY       | 12 TB  | 52      | 600   | 2     | 1.61   |
| Seagate   | ST3000VX010-2E3166 | 3 TB   | 5       | 691   | 4     | 1.60   |
| Seagate   | ST12000NM0008-2... | 12 TB  | 165     | 590   | 4     | 1.60   |
| WDC       | WD5000AZLX-22JKKA0 | 500 GB | 3       | 923   | 3     | 1.58   |
| WDC       | WD40EFAX-68JH4N0   | 4 TB   | 38      | 600   | 1     | 1.58   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 3       | 577   | 0     | 1.58   |
| Seagate   | ST3500514NS        | 500 GB | 4       | 1257  | 10    | 1.58   |
| Seagate   | ST1000NX0423       | 1 TB   | 3       | 817   | 12    | 1.58   |
| Seagate   | ST4000NM0115-1Y... | 4 TB   | 87      | 584   | 1     | 1.57   |
| Seagate   | ST32000644NS       | 2 TB   | 12      | 978   | 17    | 1.55   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 3       | 564   | 0     | 1.55   |
| HPE       | MB004000GWFWB      | 4 TB   | 15      | 564   | 0     | 1.55   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 8       | 563   | 0     | 1.54   |
| WDC       | WD5000AAKS-65YGA0  | 500 GB | 1       | 556   | 0     | 1.52   |
| Seagate   | ST8000VX0022-2E... | 8 TB   | 4       | 758   | 9     | 1.52   |
| Seagate   | ST2000DM005-2CW102 | 2 TB   | 1       | 552   | 0     | 1.51   |
| Toshiba   | HDWN160            | 6 TB   | 11      | 658   | 2     | 1.51   |
| HGST      | HTS725050A7E630    | 500 GB | 6       | 844   | 508   | 1.50   |
| WDC       | WD2003FYYS-05T9B0  | 2 TB   | 4       | 604   | 1     | 1.50   |
| WDC       | WD121KFBX-68EF5N0  | 12 TB  | 7       | 543   | 0     | 1.49   |
| WDC       | WD50EFRX-68MYMN1   | 5 TB   | 2       | 2167  | 4     | 1.49   |
| HGST      | HDN728080ALE604    | 8 TB   | 2       | 850   | 16    | 1.48   |
| WDC       | WD60PURZ-85ZUFY1   | 6 TB   | 6       | 541   | 0     | 1.48   |
| Seagate   | ST10000VE0008-2... | 10 TB  | 4       | 538   | 0     | 1.48   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 20      | 629   | 18    | 1.47   |
| HGST      | HUH721008ALE604    | 8 TB   | 22      | 535   | 0     | 1.47   |
| WDC       | WUH721414ALE604    | 14 TB  | 2053    | 532   | 1     | 1.44   |
| WDC       | WD4003FRYZ-01F0DB0 | 4 TB   | 29      | 524   | 0     | 1.44   |
| Toshiba   | HDWL120            | 2 TB   | 12      | 605   | 1     | 1.44   |
| HGST      | HUS728T8TALE6L0    | 8 TB   | 15      | 523   | 0     | 1.43   |
| Seagate   | ST2000NM0011       | 2 TB   | 15      | 1602  | 136   | 1.43   |
| Toshiba   | MQ01ABF032         | 320 GB | 1       | 519   | 0     | 1.42   |
| Seagate   | ST32000542AS       | 2 TB   | 1       | 518   | 0     | 1.42   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 188     | 1200  | 7     | 1.41   |
| Toshiba   | MG06ACA10TE        | 10 TB  | 165     | 519   | 1     | 1.40   |
| WDC       | WD8003FRYZ-01JPDB1 | 8 TB   | 5       | 510   | 0     | 1.40   |
| WDC       | WD5003ABYX-50WERA1 | 500 GB | 1       | 508   | 0     | 1.39   |
| Toshiba   | MD04ACA50D         | 5 TB   | 1       | 504   | 0     | 1.38   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 25      | 500   | 0     | 1.37   |
| Toshiba   | MG06ACA600E        | 6 TB   | 10      | 499   | 0     | 1.37   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 2       | 498   | 0     | 1.37   |
| Toshiba   | MG03ACA300         | 3 TB   | 2       | 899   | 6     | 1.36   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 17      | 635   | 2     | 1.35   |
| WDC       | WD101EFAX-68LDBN0  | 10 TB  | 10      | 488   | 0     | 1.34   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 2       | 487   | 0     | 1.34   |
| WDC       | WD3200AAJS-40VWA1  | 320 GB | 1       | 487   | 0     | 1.33   |
| Seagate   | ST3750640NS        | 752 GB | 13      | 1289  | 859   | 1.33   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 2       | 486   | 0     | 1.33   |
| WDC       | WD40EZAZ-00ZGHB0   | 4 TB   | 2       | 483   | 0     | 1.32   |
| Seagate   | ST31000524AS       | 1 TB   | 7       | 1614  | 844   | 1.32   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 5       | 479   | 0     | 1.31   |
| Seagate   | ST1000NM0011 81... | 1 TB   | 1       | 2394  | 4     | 1.31   |
| Samsung   | HD322GJ            | 320 GB | 1       | 477   | 0     | 1.31   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 141     | 485   | 5     | 1.31   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 4       | 560   | 1     | 1.30   |
| Seagate   | ST1000NX0313       | 1 TB   | 32      | 1235  | 24    | 1.29   |
| WDC       | WD3200AAKS-00SBA0  | 320 GB | 1       | 2793  | 5     | 1.28   |
| WDC       | WD10JMVW-11AJGS4   | 1 TB   | 1       | 465   | 0     | 1.28   |
| Toshiba   | MG07ACA12TE        | 12 TB  | 114     | 474   | 1     | 1.26   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 69      | 461   | 1     | 1.25   |
| Seagate   | ST6000VX001-2BD186 | 6 TB   | 7       | 455   | 0     | 1.25   |
| Toshiba   | HDWR160            | 6 TB   | 1       | 454   | 0     | 1.25   |
| Toshiba   | HDWD110            | 1 TB   | 85      | 466   | 43    | 1.24   |
| HPE       | MB012000GWDFE      | 12 TB  | 36      | 461   | 1     | 1.23   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 4       | 449   | 0     | 1.23   |
| Toshiba   | MG04ACA200E        | 2 TB   | 38      | 445   | 0     | 1.22   |
| Seagate   | ST6000NM021A-2R... | 6 TB   | 87      | 463   | 13    | 1.21   |
| WDC       | WD20PURX-64P6ZY0   | 2 TB   | 1       | 440   | 0     | 1.21   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 74      | 543   | 37    | 1.21   |
| WDC       | WD1005FBYZ-01YCBB3 | 1 TB   | 1       | 438   | 0     | 1.20   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 2       | 1740  | 4     | 1.19   |
| WDC       | WD800JD-60LSA5     | 80 GB  | 1       | 434   | 0     | 1.19   |
| Toshiba   | HDWQ140            | 4 TB   | 11      | 434   | 0     | 1.19   |
| HGST      | HUH721212ALE600    | 12 TB  | 125     | 428   | 0     | 1.17   |
| WDC       | WD6003FZBX-00GXAB0 | 6 TB   | 7       | 428   | 0     | 1.17   |
| WDC       | WD1501FASS-00U0B0  | 1.5 TB | 1       | 3850  | 8     | 1.17   |
| Samsung   | HD080HJ            | 80 GB  | 2       | 1964  | 841   | 1.17   |
| Seagate   | ST2000DX002-2DV164 | 2 TB   | 4       | 424   | 0     | 1.16   |
| Seagate   | ST1000NM0011 99... | 1 TB   | 2       | 1210  | 3     | 1.16   |
| WDC       | WD3000F9YZ-09N20L1 | 3 TB   | 1       | 419   | 0     | 1.15   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 203     | 442   | 52    | 1.14   |
| Samsung   | HD501LJ            | 500 GB | 3       | 2183  | 676   | 1.14   |
| Seagate   | ST3250312AS        | 250 GB | 3       | 777   | 4     | 1.14   |
| WDC       | WD5000LPCX-00VHAT0 | 500 GB | 2       | 414   | 0     | 1.14   |
| Seagate   | ST8000NE001-2M7101 | 8 TB   | 1       | 413   | 0     | 1.13   |
| HGST      | HUS726T4TALA6L1    | 4 TB   | 84      | 424   | 1     | 1.13   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 2       | 412   | 0     | 1.13   |
| Toshiba   | MG04ACA200N        | 2 TB   | 5       | 455   | 1     | 1.13   |
| WDC       | WD20EZRZ-00Z5HB0   | 2 TB   | 11      | 524   | 99    | 1.11   |
| Seagate   | ST8000VE000-2P6101 | 8 TB   | 1       | 402   | 0     | 1.10   |
| WDC       | WD1503FYYS-02W0B0  | 1.5 TB | 2       | 3213  | 7     | 1.10   |
| WDC       | WD6003FFBX-68MU3N0 | 6 TB   | 9       | 400   | 0     | 1.10   |
| WDC       | WD20PURZ-85GU6Y0   | 2 TB   | 7       | 400   | 0     | 1.10   |
| Toshiba   | MQ01ABB200         | 2 TB   | 2       | 1156  | 4     | 1.10   |
| HPE       | MB8000GFECR        | 8 TB   | 56      | 425   | 28    | 1.09   |
| Seagate   | ST1000LM049-2GH172 | 1 TB   | 4       | 398   | 0     | 1.09   |
| WDC       | WD2005FBYZ-01YCBB3 | 2 TB   | 5       | 391   | 0     | 1.07   |
| WDC       | WD141KFGX-68FH9N0  | 14 TB  | 12      | 383   | 0     | 1.05   |
| WDC       | WD20EZAZ-00GGJB0   | 2 TB   | 5       | 381   | 0     | 1.04   |
| Toshiba   | HDWG180            | 8 TB   | 8       | 380   | 0     | 1.04   |
| Seagate   | ST5000LM000-2AN170 | 5 TB   | 44      | 543   | 65    | 1.04   |
| Hitachi   | HTS542512K9SA00    | 120 GB | 1       | 1508  | 3     | 1.03   |
| Seagate   | ST6000NE0021-2E... | 6 TB   | 3       | 1114  | 144   | 1.03   |
| Seagate   | ST4000VN008-2DR166 | 4 TB   | 85      | 391   | 79    | 1.03   |
| Seagate   | ST12000NM0248-2... | 12 TB  | 2       | 373   | 0     | 1.02   |
| WDC       | WD6003FZBX-00K5WB0 | 6 TB   | 13      | 371   | 0     | 1.02   |
| Maxtor    | STM3500320AS       | 500 GB | 2       | 561   | 617   | 1.02   |
| Toshiba   | MG04ACA400NY       | 4 TB   | 3       | 370   | 0     | 1.02   |
| WDC       | WD3200BPVT-22JJ5T0 | 320 GB | 2       | 369   | 0     | 1.01   |
| WDC       | WD20SPZX-00UA7T0   | 2 TB   | 5       | 367   | 0     | 1.01   |
| Seagate   | ST3250823AS        | 250 GB | 1       | 4725  | 12    | 1.00   |
| Seagate   | ST4000NM0033       | 4 TB   | 4       | 362   | 0     | 0.99   |
| WDC       | WD2500AAKX-083CA1  | 250 GB | 1       | 360   | 0     | 0.99   |
| Seagate   | ST10000VE0008-2... | 10 TB  | 2       | 359   | 0     | 0.98   |
| WDC       | WD5000AZLX-00K2TA0 | 500 GB | 1       | 358   | 0     | 0.98   |
| Seagate   | ST4000DM004-2CV104 | 4 TB   | 16      | 373   | 1     | 0.97   |
| WDC       | WD102KRYZ-01A5AB0  | 10 TB  | 4       | 497   | 81    | 0.97   |
| Toshiba   | MG04ACA100NY       | 1 TB   | 7       | 403   | 12    | 0.96   |
| Toshiba   | HDWG11A            | 10 TB  | 1       | 346   | 0     | 0.95   |
| WDC       | WD102KFBX-68M95N0  | 10 TB  | 47      | 346   | 0     | 0.95   |
| Seagate   | ST3000DM008-2DM166 | 3 TB   | 6       | 714   | 185   | 0.94   |
| WDC       | WD3000F9YZ-09N20L0 | 3 TB   | 1       | 1714  | 4     | 0.94   |
| WDC       | WD10EALS-002BA0    | 1 TB   | 2       | 2394  | 6     | 0.94   |
| Seagate   | ST31000528AS       | 1 TB   | 4       | 812   | 351   | 0.94   |
| WDC       | WUH721414ALE6L4    | 14 TB  | 206     | 342   | 1     | 0.93   |
| Seagate   | ST4000NM000A-2H... | 4 TB   | 10      | 387   | 1     | 0.93   |
| Seagate   | ST3500411SV        | 500 GB | 1       | 335   | 0     | 0.92   |
| WDC       | WD5000AZLX-00JKKA0 | 500 GB | 3       | 335   | 0     | 0.92   |
| Seagate   | ST18000NM000J-2... | 18 TB  | 13      | 334   | 0     | 0.92   |
| Hitachi   | HDS721050DLE630    | 500 GB | 4       | 808   | 420   | 0.90   |
| WDC       | WD4000FYYZ-01UL1B0 | 4 TB   | 20      | 2264  | 177   | 0.89   |
| WDC       | WD5000LPLX-08ZNTT0 | 500 GB | 2       | 323   | 0     | 0.89   |
| WDC       | WD62PURZ-85B3AY0   | 6 TB   | 3       | 323   | 0     | 0.89   |
| HPE       | MB0500EBZQA        | 500 GB | 1       | 2879  | 8     | 0.88   |
| Seagate   | ST12000NM0128-2... | 12 TB  | 18      | 326   | 1     | 0.87   |
| Seagate   | ST10000VX0004-1... | 10 TB  | 18      | 317   | 0     | 0.87   |
| Seagate   | ST2000DM008-2FR102 | 2 TB   | 75      | 348   | 49    | 0.86   |
| Toshiba   | MG04ACA200NY       | 2 TB   | 4       | 313   | 0     | 0.86   |
| WDC       | WUS721010ALE6L4    | 10 TB  | 26      | 312   | 9     | 0.85   |
| WDC       | WD6003FRYZ-01F0DB0 | 6 TB   | 32      | 309   | 0     | 0.85   |
| Seagate   | ST8000VX004-2M1101 | 8 TB   | 6       | 331   | 389   | 0.84   |
| Seagate   | ST14000NM001G-2... | 14 TB  | 27      | 321   | 11    | 0.83   |
| WDC       | WD20SPZX-21UA7T0   | 2 TB   | 2       | 302   | 0     | 0.83   |
| WDC       | WD7500BPVT-22HXZT3 | 752 GB | 1       | 301   | 0     | 0.83   |
| WDC       | WD800BEVS-22RST0   | 80 GB  | 1       | 299   | 0     | 0.82   |
| Toshiba   | HDWL110            | 1 TB   | 1       | 298   | 0     | 0.82   |
| Seagate   | ST31000524NS       | 1 TB   | 20      | 1104  | 107   | 0.80   |
| Seagate   | ST6000VN001-2BB186 | 6 TB   | 8       | 292   | 0     | 0.80   |
| Seagate   | ST10000DM0004-1... | 10 TB  | 7       | 498   | 491   | 0.79   |
| Seagate   | ST10000NM0478-2... | 10 TB  | 49      | 295   | 2     | 0.78   |
| Seagate   | ST9750420AS        | 752 GB | 1       | 285   | 0     | 0.78   |
| WDC       | WD5000AAKX-603CA0  | 500 GB | 1       | 284   | 0     | 0.78   |
| WDC       | WD5001AALS-00L3B2  | 500 GB | 2       | 3429  | 515   | 0.77   |
| Seagate   | ST1000NX0443       | 1 TB   | 22      | 281   | 0     | 0.77   |
| Seagate   | ST8000NM000A-2K... | 8 TB   | 53      | 306   | 1     | 0.77   |
| WDC       | WD3000FYYZ-01UL1B1 | 3 TB   | 1       | 2529  | 8     | 0.77   |
| Seagate   | ST1000LM035-1RK172 | 1 TB   | 2       | 279   | 0     | 0.77   |
| HGST      | HUS726T6TALE6L1    | 6 TB   | 27      | 277   | 0     | 0.76   |
| HP        | VB0250EAVER        | 250 GB | 3       | 480   | 205   | 0.76   |
| HGST      | HUH721212ALE601    | 12 TB  | 53      | 276   | 0     | 0.76   |
| Seagate   | ST2000VN004-2E4164 | 2 TB   | 26      | 276   | 0     | 0.76   |
| Hitachi   | HDS721025CLA382    | 250 GB | 1       | 2454  | 8     | 0.75   |
| WDC       | WD8004FRYZ-01VAEB0 | 8 TB   | 39      | 260   | 0     | 0.71   |
| WDC       | WD40EZRX-00SPEB0   | 4 TB   | 3       | 399   | 36    | 0.71   |
| Seagate   | ST3160815AS        | 160 GB | 3       | 2011  | 183   | 0.71   |
| WDC       | WD1000DHTZ-04N21V0 | 1 TB   | 11      | 337   | 1     | 0.70   |
| Hitachi   | HTS545032B9A300    | 320 GB | 1       | 1024  | 3     | 0.70   |
| Seagate   | ST31000524NS 45... | 1 TB   | 2       | 682   | 2     | 0.70   |
| Seagate   | ST8000NM012A-2K... | 8 TB   | 74      | 260   | 1     | 0.70   |
| Seagate   | ST16000NM001G-2... | 16 TB  | 109     | 252   | 0     | 0.69   |
| HPE       | MB008000GWRTC      | 8 TB   | 1       | 252   | 0     | 0.69   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 4       | 1229  | 697   | 0.69   |
| Seagate   | ST4000VX007-2DT166 | 4 TB   | 2       | 250   | 0     | 0.69   |
| WDC       | WD3200AAKS-22B3A0  | 320 GB | 1       | 250   | 0     | 0.69   |
| WDC       | WD1001FALS-00J7B1  | 1 TB   | 1       | 246   | 0     | 0.67   |
| WDC       | WD10TMVW-11ZSMS1   | 1 TB   | 1       | 492   | 1     | 0.67   |
| Toshiba   | HDWR180            | 8 TB   | 9       | 244   | 0     | 0.67   |
| WDC       | WD10EADS-11P8B1    | 1 TB   | 1       | 2191  | 8     | 0.67   |
| Seagate   | ST10000NM001G-2... | 10 TB  | 62      | 241   | 0     | 0.66   |
| WDC       | WD2003FYYS-70W0B0  | 2 TB   | 1       | 240   | 0     | 0.66   |
| WDC       | WUH721414ALE6L1    | 14 TB  | 8       | 239   | 0     | 0.66   |
| Seagate   | ST3320418AS        | 320 GB | 1       | 239   | 0     | 0.66   |
| Toshiba   | MQ01ABD100         | 1 TB   | 5       | 525   | 859   | 0.65   |
| Seagate   | ST4000NM002A-2H... | 4 TB   | 96      | 238   | 0     | 0.65   |
| HPE       | MB008000GWJRT      | 8 TB   | 4       | 237   | 0     | 0.65   |
| Seagate   | ST5000LM000-2U8170 | 5 TB   | 2       | 234   | 0     | 0.64   |
| Toshiba   | MQ04UBF100         | 1 TB   | 4       | 234   | 0     | 0.64   |
| WDC       | WD15NMVW-11W68S0   | 1.5 TB | 1       | 233   | 0     | 0.64   |
| Seagate   | ST12000NM001G-2... | 12 TB  | 52      | 234   | 1     | 0.64   |
| Seagate   | ST3000NM0005-1V... | 3 TB   | 3       | 230   | 0     | 0.63   |
| Samsung   | HD252HJ            | 250 GB | 1       | 2983  | 12    | 0.63   |
| WDC       | WD5000AZRZ-00HTKB0 | 500 GB | 2       | 227   | 0     | 0.62   |
| Apple     | HDD HTS541010A9... | 1 TB   | 1       | 220   | 0     | 0.60   |
| WDC       | WD20SPZX-75UA7T1   | 2 TB   | 2       | 219   | 0     | 0.60   |
| WDC       | WD20PURZ-85AKKY0   | 2 TB   | 1       | 216   | 0     | 0.59   |
| Seagate   | ST3160812AS        | 160 GB | 1       | 211   | 0     | 0.58   |
| Seagate   | ST1000NX0423 00... | 1 TB   | 1       | 207   | 0     | 0.57   |
| Toshiba   | MG06ACA800E        | 8 TB   | 123     | 207   | 0     | 0.57   |
| WDC       | WD3200LPVX-22V0TT0 | 320 GB | 1       | 205   | 0     | 0.56   |
| WDC       | WD5000AZLX-75K2TA0 | 500 GB | 1       | 202   | 0     | 0.56   |
| WDC       | WD7500BPKT-00PK4T0 | 752 GB | 1       | 1623  | 7     | 0.56   |
| Toshiba   | MG08ADA800E        | 8 TB   | 5       | 201   | 0     | 0.55   |
| Toshiba   | MK1252GSX          | 120 GB | 1       | 199   | 0     | 0.55   |
| HGST      | HTS541010A9E680    | 1 TB   | 2       | 639   | 130   | 0.54   |
| WDC       | WD10JPVX-22JC3T0   | 1 TB   | 2       | 191   | 0     | 0.52   |
| HP        | MB1000EAMZE        | 1 TB   | 2       | 185   | 0     | 0.51   |
| WDC       | WUH721818ALE604    | 18 TB  | 1653    | 175   | 1     | 0.48   |
| WDC       | WD20NPVX-00EA4T0   | 2 TB   | 4       | 1499  | 12    | 0.48   |
| WDC       | WD20EFAX-68B2RN1   | 2 TB   | 4       | 173   | 0     | 0.48   |
| WDC       | WD1200JS-00NCB1    | 120 GB | 1       | 3117  | 17    | 0.47   |
| WDC       | WD20EZAZ-00L9GB0   | 2 TB   | 3       | 172   | 0     | 0.47   |
| Seagate   | ST1000NX0343       | 1 TB   | 2       | 1629  | 10    | 0.46   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 35      | 168   | 0     | 0.46   |
| Toshiba   | MG08ACA16TA        | 16 TB  | 35      | 162   | 0     | 0.45   |
| Seagate   | ST16000VN001-2R... | 16 TB  | 1       | 162   | 0     | 0.45   |
| WDC       | WD30EFAX-68JH4N0   | 3 TB   | 2       | 300   | 4     | 0.44   |
| WDC       | WD1003FBYX-05Y7B0  | 1 TB   | 4       | 523   | 2     | 0.43   |
| Seagate   | ST16000NM005G-2... | 16 TB  | 12      | 156   | 0     | 0.43   |
| Seagate   | ST1000NX0303       | 1 TB   | 3       | 650   | 4     | 0.42   |
| WDC       | WD80EFBX-68AZZN0   | 8 TB   | 6       | 153   | 0     | 0.42   |
| Toshiba   | MQ01ACF032         | 320 GB | 1       | 151   | 0     | 0.41   |
| Maxtor    | STM3200827AS       | 200 GB | 1       | 1203  | 7     | 0.41   |
| WDC       | WD1003FBYX-20Y7B0  | 1 TB   | 2       | 149   | 0     | 0.41   |
| WDC       | WD2500BEVT-00ZCT0  | 250 GB | 2       | 147   | 0     | 0.40   |
| Toshiba   | HDWN180            | 8 TB   | 1       | 146   | 0     | 0.40   |
| WDC       | WD1600AAJS-22L7A0  | 160 GB | 2       | 1307  | 8     | 0.40   |
| WDC       | WD50EZRZ-00GZ5B1   | 5 TB   | 1       | 141   | 0     | 0.39   |
| Apple     | HDD HTS545050A7... | 500 GB | 1       | 141   | 0     | 0.39   |
| HP        | MB2000EBZQC        | 2 TB   | 1       | 1269  | 8     | 0.39   |
| Samsung   | HM641JI            | 640 GB | 1       | 141   | 0     | 0.39   |
| HP        | MB1000EBNCF        | 1 TB   | 2       | 1616  | 40    | 0.39   |
| WDC       | WD40NMZW-11GX6S1   | 4 TB   | 4       | 137   | 0     | 0.38   |
| Toshiba   | HDWD240            | 4 TB   | 6       | 136   | 0     | 0.37   |
| Hitachi   | HDT725025VLA380... | 250 GB | 1       | 135   | 0     | 0.37   |
| WDC       | WUH721818ALE6L4    | 18 TB  | 517     | 127   | 1     | 0.35   |
| WDC       | WD10EURX-63C57Y0   | 1 TB   | 1       | 1110  | 8     | 0.34   |
| Hitachi   | HDS721010DLE630    | 1 TB   | 8       | 1613  | 1436  | 0.34   |
| WDC       | WD101EFBX-68B0AN0  | 10 TB  | 5       | 122   | 0     | 0.34   |
| Seagate   | ST10000NM0086 0... | 10 TB  | 4       | 121   | 0     | 0.33   |
| WDC       | WD2001FASS-00W2B0  | 2 TB   | 3       | 1833  | 15    | 0.33   |
| WDC       | WD10JPVT-00A1YT0   | 1 TB   | 1       | 1081  | 8     | 0.33   |
| HP        | GB0750C4414        | 752 GB | 2       | 3668  | 152   | 0.33   |
| Seagate   | ST6000NM002A-2K... | 6 TB   | 1       | 118   | 0     | 0.32   |
| WDC       | WD60EFZX-68B3FN0   | 6 TB   | 5       | 116   | 0     | 0.32   |
| Seagate   | ST1000VM002-1CT162 | 1 TB   | 1       | 113   | 0     | 0.31   |
| Samsung   | HN-M500MBB         | 500 GB | 1       | 112   | 0     | 0.31   |
| Toshiba   | MG08ACA16TE        | 16 TB  | 27      | 111   | 0     | 0.31   |
| Hitachi   | HTS725016A9A364    | 160 GB | 2       | 1326  | 507   | 0.30   |
| Seagate   | ST16000NM000J-2... | 16 TB  | 80      | 105   | 0     | 0.29   |
| Seagate   | ST2000NM000A-2J... | 2 TB   | 7       | 103   | 0     | 0.28   |
| WDC       | WD40EFAX-68JH4N1   | 4 TB   | 25      | 102   | 0     | 0.28   |
| Seagate   | ST250DM000-1BD141  | 250 GB | 4       | 1076  | 536   | 0.28   |
| WDC       | WD2500AAKX-00ERMA0 | 250 GB | 2       | 507   | 4     | 0.28   |
| Seagate   | ST12000NM003G-2... | 12 TB  | 4       | 97    | 0     | 0.27   |
| WDC       | WD102PURZ-85BXPY0  | 10 TB  | 10      | 97    | 0     | 0.27   |
| WDC       | WD181KRYZ-01AGBB0  | 18 TB  | 1       | 96    | 0     | 0.26   |
| WDC       | WD3200AVVS-56L2B0  | 320 GB | 4       | 91    | 0     | 0.25   |
| WDC       | WD10SMZW-11Y0TS0   | 1 TB   | 2       | 88    | 0     | 0.24   |
| WDC       | WD10EZEX-00BBHA0   | 1 TB   | 3       | 88    | 0     | 0.24   |
| Hitachi   | HTS725050A9A362    | 500 GB | 1       | 1241  | 14    | 0.23   |
| WDC       | WUH721816ALE6L4    | 16 TB  | 30      | 82    | 0     | 0.23   |
| WDC       | WD1600BEKT-00F3T0  | 160 GB | 2       | 1098  | 146   | 0.22   |
| WDC       | WD2500BEKT-60A25T1 | 250 GB | 1       | 399   | 4     | 0.22   |
| WDC       | WD10SDRW-11A0XS0   | 1 TB   | 1       | 76    | 0     | 0.21   |
| Seagate   | ST4000NM000A       | 4 TB   | 1       | 74    | 0     | 0.20   |
| Seagate   | ST32000641AS       | 2 TB   | 1       | 2235  | 29    | 0.20   |
| Seagate   | ST9160412AS        | 160 GB | 1       | 73    | 0     | 0.20   |
| Seagate   | ST9500325AS        | 500 GB | 5       | 636   | 32    | 0.20   |
| Toshiba   | MQ01UBD100         | 1 TB   | 2       | 190   | 8     | 0.20   |
| WDC       | WD4000F9YZ-76N20L1 | 4 TB   | 1       | 71    | 0     | 0.20   |
| WDC       | WD101FZBX-00ATAA0  | 10 TB  | 3       | 71    | 0     | 0.20   |
| Seagate   | ST980811AS         | 80 GB  | 1       | 348   | 4     | 0.19   |
| WDC       | WD60EFAX-68JH4N1   | 6 TB   | 11      | 91    | 1     | 0.19   |
| Toshiba   | MQ04ABF100         | 1 TB   | 2       | 306   | 1010  | 0.18   |
| Hitachi   | HUA723030ALA641    | 3 TB   | 1       | 65    | 0     | 0.18   |
| Seagate   | ST2000NC001-1DY164 | 2 TB   | 1       | 1641  | 24    | 0.18   |
| WDC       | WD5000LPLX-60ZNTT2 | 500 GB | 1       | 63    | 0     | 0.17   |
| HPE       | MB014000GWTFF      | 14 TB  | 55      | 61    | 0     | 0.17   |
| WDC       | WD50NDZW-11MR8S1   | 5 TB   | 2       | 60    | 0     | 0.17   |
| WDC       | WD60PURX-64T0ZY0   | 6 TB   | 2       | 524   | 8     | 0.16   |
| HGST      | HUH728080ALN600    | 8 TB   | 2       | 96    | 2     | 0.16   |
| Toshiba   | MG09ACA18TE        | 18 TB  | 22      | 58    | 1     | 0.16   |
| Hitachi   | HTS545016B9A300    | 160 GB | 1       | 55    | 0     | 0.15   |
| Hitachi   | HTS545025B9A300    | 250 GB | 1       | 219   | 3     | 0.15   |
| WDC       | WD20NMVW-11EDZS7   | 2 TB   | 1       | 54    | 0     | 0.15   |
| Seagate   | ST16000NM003G-2... | 16 TB  | 14      | 53    | 0     | 0.15   |
| WDC       | WD10JPCX-24UE4T0   | 1 TB   | 2       | 52    | 0     | 0.14   |
| WDC       | WD5000AAKS-00TMA0  | 500 GB | 1       | 49    | 0     | 0.14   |
| Seagate   | ST3000VN007-2AH16M | 3 TB   | 3       | 48    | 0     | 0.13   |
| WDC       | WD40EFZX-68AWUN0   | 4 TB   | 4       | 48    | 0     | 0.13   |
| WDC       | WD40EZAZ-00SF3B0   | 4 TB   | 4       | 46    | 0     | 0.13   |
| Seagate   | ST1000NM000A-2J... | 1 TB   | 2       | 44    | 0     | 0.12   |
| Toshiba   | MG08ACA16TEY       | 16 TB  | 24      | 44    | 0     | 0.12   |
| WDC       | WD10SPZX-21Z10T0   | 1 TB   | 2       | 44    | 0     | 0.12   |
| HGST      | HUS722T2TALA600    | 2 TB   | 1       | 44    | 0     | 0.12   |
| WDC       | WD20EZRX-19DC0B0   | 2 TB   | 1       | 1541  | 35    | 0.12   |
| Seagate   | ST3000DM001-9YN166 | 3 TB   | 6       | 2026  | 1022  | 0.12   |
| Seagate   | ST8000VN0002-1Z... | 8 TB   | 1       | 1535  | 35    | 0.12   |
| Seagate   | ST31000340NS       | 1 TB   | 3       | 748   | 1009  | 0.11   |
| Samsung   | HM640JJ            | 640 GB | 1       | 373   | 8     | 0.11   |
| Seagate   | ST16000NM001J-2... | 16 TB  | 51      | 40    | 0     | 0.11   |
| WDC       | WD80EMAZ-00WJTA0   | 8 TB   | 1       | 38    | 0     | 0.11   |
| Seagate   | ST3640323AS        | 640 GB | 1       | 960   | 24    | 0.11   |
| HP        | VB0160EAVEQ        | 160 GB | 1       | 545   | 14    | 0.10   |
| HPE       | MB006000GWWQT      | 6 TB   | 1       | 36    | 0     | 0.10   |
| Hitachi   | HTS721060G9SA00    | 64 GB  | 1       | 2330  | 66    | 0.10   |
| WDC       | WD2502ABYS-02B7A0  | 256 GB | 1       | 2349  | 67    | 0.09   |
| WDC       | WD40PURZ-85TTDY0   | 4 TB   | 2       | 33    | 0     | 0.09   |
| Toshiba   | HDWF180            | 8 TB   | 2       | 33    | 0     | 0.09   |
| Seagate   | ST5000NM0024-1H... | 5 TB   | 1       | 1636  | 49    | 0.09   |
| WDC       | WD20EFAX-68FB5N0   | 2 TB   | 4       | 30    | 0     | 0.08   |
| WDC       | WD4000FDYZ-27YA5B0 | 4 TB   | 5       | 711   | 115   | 0.08   |
| Apple     | HDD ST1000DM003    | 1 TB   | 1       | 254   | 8     | 0.08   |
| WDC       | WD5000LPLX-60ZNTT1 | 500 GB | 10      | 29    | 1     | 0.07   |
| HGST      | HTS541050A9E680    | 500 GB | 1       | 26    | 0     | 0.07   |
| HP        | MB1000EBZQB        | 1 TB   | 1       | 2073  | 86    | 0.07   |
| WDC       | WD20SDRW-11VUUS0   | 2 TB   | 1       | 23    | 0     | 0.06   |
| Toshiba   | MQ04ABB400         | 4 TB   | 3       | 20    | 0     | 0.06   |
| Seagate   | ST16000VE000-2L... | 16 TB  | 1       | 19    | 0     | 0.05   |
| Maxtor    | STM3160215AS       | 160 GB | 1       | 2646  | 142   | 0.05   |
| WDC       | WD20EZBX-00AYRA0   | 2 TB   | 3       | 17    | 0     | 0.05   |
| WDC       | WD3200AAKS-00L9A0  | 320 GB | 1       | 3625  | 242   | 0.04   |
| Toshiba   | MK5061GSY          | 500 GB | 2       | 13    | 0     | 0.04   |
| WDC       | WD60EZRX-00MVLB1   | 6 TB   | 1       | 1376  | 105   | 0.04   |
| Seagate   | ST20000NM007D-3... | 20 TB  | 4       | 12    | 0     | 0.04   |
| Toshiba   | HDWR11A            | 10 TB  | 1       | 11    | 0     | 0.03   |
| WDC       | WD20SMZW-11JW8S1   | 2 TB   | 1       | 10    | 0     | 0.03   |
| Seagate   | ST1000NC000-1CX162 | 1 TB   | 1       | 2331  | 224   | 0.03   |
| Hitachi   | HTS543216L9SA02    | 160 GB | 1       | 130   | 12    | 0.03   |
| Seagate   | ST12000VN0008-2... | 12 TB  | 3       | 9     | 0     | 0.03   |
| Seagate   | ST3160813AS        | 160 GB | 1       | 1350  | 139   | 0.03   |
| WDC       | WD5000AZLX-60K2TA0 | 500 GB | 2       | 8     | 0     | 0.02   |
| Hitachi   | HDS721010CLA632    | 1 TB   | 1       | 1059  | 124   | 0.02   |
| HGST      | HTS725050B7E630    | 500 GB | 4       | 8     | 0     | 0.02   |
| Seagate   | ST18000NE000-2Y... | 18 TB  | 1       | 8     | 0     | 0.02   |
| WDC       | WD10EVVS-63M5B0    | 1 TB   | 1       | 73    | 8     | 0.02   |
| Seagate   | ST9320325AS        | 320 GB | 1       | 348   | 42    | 0.02   |
| Seagate   | ST3750330NS        | 752 GB | 1       | 258   | 36    | 0.02   |
| Hitachi   | HDT722525DLA380    | 250 GB | 1       | 3853  | 579   | 0.02   |
| WDC       | WD40PURX-64GVNY0   | 4 TB   | 1       | 6     | 0     | 0.02   |
| Seagate   | ST2000DM001-1E6164 | 2 TB   | 1       | 6     | 0     | 0.02   |
| WDC       | WD10EADS-00M2B0    | 1 TB   | 1       | 315   | 51    | 0.02   |
| Samsung   | HD502HI            | 500 GB | 3       | 3790  | 810   | 0.02   |
| WDC       | WD20SMZW-11JW8S0   | 2 TB   | 1       | 5     | 0     | 0.01   |
| Seagate   | ST31500341AS       | 1.5 TB | 1       | 2761  | 670   | 0.01   |
| Seagate   | ST3160211AS        | 160 GB | 1       | 1802  | 497   | 0.01   |
| Seagate   | ST1000VM002-1ET162 | 1 TB   | 1       | 113   | 32    | 0.01   |
| HP        | GJ0250EAGSQ        | 250 GB | 2       | 3080  | 1028  | 0.01   |
| Seagate   | ST31000524NS 43... | 1 TB   | 1       | 2718  | 1138  | 0.01   |
| Hitachi   | HDS721010CLA630    | 1 TB   | 2       | 1533  | 699   | 0.01   |
| WDC       | WD1600JS-75NCB2    | 160 GB | 1       | 2854  | 1502  | 0.01   |
| MediaMax  | WL4000GSA6472E     | 4.9 TB | 1       | 1617  | 1054  | 0.00   |
| WDC       | WD5000AADS-00M2B0  | 500 GB | 1       | 2968  | 2023  | 0.00   |
| HGST      | HTS541075A9E680    | 752 GB | 1       | 1376  | 1027  | 0.00   |
| Seagate   | ST500LT012-9WS142  | 500 GB | 3       | 1335  | 1067  | 0.00   |
| Samsung   | SP2004C            | 200 GB | 1       | 1212  | 1105  | 0.00   |
| Seagate   | ST4000DM000-2AE166 | 4 TB   | 1       | 1104  | 1060  | 0.00   |
| WDC       | WD2500BEVS-60UST0  | 250 GB | 1       | 400   | 413   | 0.00   |
| Seagate   | ST9120817AS        | 120 GB | 1       | 3408  | 3854  | 0.00   |
| HGST      | HTS725032A7E630    | 320 GB | 1       | 461   | 538   | 0.00   |
| WDC       | WD2003FYPS-27Y2B0  | 2 TB   | 1       | 1747  | 2073  | 0.00   |
| Seagate   | ST1000LM010-9YH146 | 1 TB   | 2       | 32    | 545   | 0.00   |
| Seagate   | ST3200827AS        | 200 GB | 1       | 1453  | 2271  | 0.00   |
| Seagate   | ST3500410AS        | 500 GB | 1       | 642   | 1085  | 0.00   |
| MaxDig... | MD15000-ALDW-RO    | 1.5 TB | 1       | 549   | 1015  | 0.00   |
| WDC       | WD10JMVW-11S5XS0   | 1 TB   | 1       | 540   | 1016  | 0.00   |
| HGST      | HTS545050A7E680    | 500 GB | 1       | 362   | 1023  | 0.00   |
| Seagate   | ST3250820AS        | 250 GB | 1       | 957   | 3053  | 0.00   |
| WDC       | WD2500AAKX-001CA0  | 250 GB | 1       | 449   | 1509  | 0.00   |
| Seagate   | ST3500320NS        | 500 GB | 2       | 585   | 2573  | 0.00   |
| Seagate   | ST9160821AS        | 160 GB | 1       | 262   | 1011  | 0.00   |
| Seagate   | ST3320820SCE       | 320 GB | 1       | 235   | 1047  | 0.00   |
| HPE       | MB006000GWKGR      | 6 TB   | 1       | 0     | 0     | 0.00   |

HDD by Family
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| WDC       | Raptor                 | 1      | 1       | 4658  | 0     | 12.76  |
| Hitachi   | Deskstar 7K500         | 1      | 1       | 4610  | 0     | 12.63  |
| Hitachi   | Sun Original           | 1      | 18      | 3987  | 1     | 9.62   |
| Hitachi   | Deskstar 7K1000        | 3      | 18      | 3454  | 15    | 8.11   |
| Samsung   | SpinPoint S250         | 1      | 1       | 2882  | 0     | 7.90   |
| Toshiba   | 3.5" DT01ABA Deskto... | 1      | 1       | 2857  | 0     | 7.83   |
| Hitachi   | Ultrastar A7K1000      | 1      | 23      | 2795  | 1     | 7.43   |
| Hitachi   | Deskstar 7K3000        | 6      | 118     | 3050  | 16    | 7.33   |
| WDC       | RE2                    | 1      | 5       | 2803  | 1     | 6.71   |
| Seagate   | Constellation ES.2     | 1      | 2       | 2424  | 0     | 6.64   |
| HP        | Seagate Constellati... | 1      | 3       | 2387  | 0     | 6.54   |
| Seagate   | NAS HDD                | 3      | 35      | 2455  | 2     | 6.39   |
| WDC       | RE3                    | 12     | 64      | 2820  | 49    | 6.15   |
| HGST      | Deskstar 7K4000        | 1      | 7       | 2243  | 0     | 6.15   |
| HP        | RE3                    | 1      | 1       | 2228  | 0     | 6.11   |
| Seagate   | Momentus XT (AF)       | 1      | 2       | 3002  | 1     | 5.48   |
| Maxtor    | DiamondMax 21          | 3      | 5       | 2519  | 29    | 5.46   |
| Maxtor    | DiamondMax 10 (SATA... | 1      | 2       | 1932  | 0     | 5.29   |
| Hitachi   | Deskstar 5K3000        | 1      | 2       | 2729  | 1008  | 5.23   |
| Hitachi   | Ultrastar 7K3000       | 4      | 79      | 1986  | 2     | 5.20   |
| Hitachi   | Deskstar 7K2000        | 2      | 68      | 2342  | 45    | 5.06   |
| Seagate   | Surveillance           | 10     | 52      | 2050  | 3     | 5.00   |
| HGST      | MegaScale 4000         | 1      | 19      | 1839  | 13    | 4.83   |
| HP        | Seagate Barracuda 7... | 1      | 2       | 2937  | 513   | 4.82   |
| Seagate   | Constellation ES.3     | 5      | 717     | 2165  | 112   | 4.81   |
| HGST      | Ultrastar 7K4000       | 5      | 442     | 1855  | 12    | 4.81   |
| Seagate   | Enterprise NAS HDD     | 2      | 13      | 1885  | 1     | 4.74   |
| Seagate   | Constellation.2 (SATA) | 3      | 81      | 1868  | 1     | 4.59   |
| Hitachi   | Deskstar P7K500        | 2      | 5       | 3065  | 3     | 4.58   |
| Toshiba   | 3.5" HDD MK.002TSKB    | 2      | 15      | 1842  | 1     | 4.55   |
| WDC       | RE4-GP                 | 4      | 21      | 2634  | 267   | 4.51   |
| WDC       | Caviar Black           | 22     | 276     | 1930  | 27    | 4.51   |
| Hitachi   | Deskstar 7K1000.B      | 1      | 1       | 1617  | 0     | 4.43   |
| Samsung   | SpinPoint F1 DT        | 5      | 33      | 2737  | 145   | 4.35   |
| HGST      | Ultrastar He8          | 6      | 120     | 1655  | 6     | 4.33   |
| Seagate   | Barracuda 7200.10      | 10     | 24      | 2395  | 191   | 4.33   |
| Hitachi   | Ultrastar A7K2000      | 8      | 95      | 2134  | 49    | 4.31   |
| Toshiba   | 2.5" HDD MQ01UBD       | 2      | 14      | 1646  | 2     | 4.26   |
| Seagate   | Constellation CS       | 5      | 7       | 2079  | 36    | 4.17   |
| WDC       | Green                  | 13     | 68      | 1706  | 6     | 4.07   |
| Seagate   | Laptop SSHD            | 1      | 1       | 1479  | 0     | 4.05   |
| Hitachi   | Deskstar T7K500        | 3      | 7       | 2801  | 5     | 4.01   |
| HGST      | Deskstar NAS           | 6      | 59      | 1538  | 35    | 4.00   |
| Seagate   | Barracuda ES           | 6      | 33      | 1805  | 339   | 3.99   |
| Samsung   | SpinPoint F3           | 2      | 27      | 2199  | 3     | 3.92   |
| Samsung   | SpinPoint P80          | 1      | 1       | 1426  | 0     | 3.91   |
| Toshiba   | 2.5" HDD               | 1      | 1       | 1412  | 0     | 3.87   |
| Toshiba   | 3.5" MG04ACA Enterp... | 7      | 926     | 1410  | 16    | 3.64   |
| Seagate   | Barracuda XT           | 2      | 5       | 2329  | 14    | 3.64   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 1       | 1320  | 0     | 3.62   |
| WDC       | Caviar Green           | 13     | 30      | 2369  | 207   | 3.62   |
| Toshiba   | 2.5" HDD MK..61GSY     | 1      | 8       | 1313  | 0     | 3.60   |
| WDC       | Caviar Blue            | 26     | 36      | 2052  | 9     | 3.56   |
| Seagate   | Barracuda Pro          | 1      | 216     | 1381  | 1     | 3.56   |
| Hitachi   | Deskstar 7K1000.C      | 8      | 35      | 2444  | 384   | 3.56   |
| WDC       | VelociRaptor           | 14     | 52      | 1493  | 2     | 3.55   |
| Seagate   | Desktop HDD.15         | 4      | 174     | 1502  | 42    | 3.55   |
| HGST      | Ultrastar 7K6000       | 11     | 619     | 1361  | 11    | 3.51   |
| Seagate   | SpinPoint M9T          | 1      | 16      | 1381  | 1     | 3.42   |
| WDC       | RE4                    | 23     | 415     | 1528  | 9     | 3.40   |
| Toshiba   | X300                   | 7      | 135     | 1302  | 14    | 3.38   |
| Seagate   | Barracuda 7200.14 (AF) | 16     | 215     | 1614  | 224   | 3.37   |
| Seagate   | Enterprise Capacity... | 19     | 5002    | 1544  | 39    | 3.32   |
| Toshiba   | 3.5" HDD DT01ACA       | 4      | 430     | 1315  | 24    | 3.29   |
| HP        | Proliant HardDrive     | 15     | 28      | 2232  | 249   | 3.23   |
| Toshiba   | 3.5" MG03ACAxxx(Y) ... | 4      | 88      | 1349  | 25    | 3.21   |
| Toshiba   | S300                   | 2      | 3       | 1133  | 0     | 3.11   |
| Seagate   | Archive HDD            | 1      | 22      | 1565  | 96    | 3.08   |
| MediaMax  | WL2000                 | 1      | 1       | 1053  | 0     | 2.89   |
| Seagate   | Sun Internal           | 1      | 1       | 2095  | 1     | 2.87   |
| Seagate   | Constellation ES (S... | 3      | 56      | 1766  | 78    | 2.83   |
| MediaMax  | WL500                  | 1      | 1       | 1018  | 0     | 2.79   |
| Seagate   | Barracuda Green (AF)   | 2      | 10      | 1517  | 321   | 2.77   |
| HPE       | WDC Enterprise         | 2      | 11      | 1312  | 8     | 2.73   |
| WDC       | Se                     | 7      | 27      | 1188  | 2     | 2.73   |
| Samsung   | SpinPoint F4 EG (AF)   | 1      | 3       | 1908  | 3     | 2.72   |
| WDC       | Black Mobile           | 7      | 40      | 1151  | 1     | 2.72   |
| Seagate   | Exos X12               | 2      | 142     | 1032  | 10    | 2.70   |
| Seagate   | Desktop SSHD           | 2      | 8       | 1567  | 164   | 2.70   |
| HGST      | Travelstar 5K1000      | 4      | 10      | 1206  | 129   | 2.69   |
| WDC       | RE                     | 18     | 241     | 1629  | 41    | 2.66   |
| WDC       | Red                    | 27     | 976     | 1446  | 9     | 2.66   |
| Fujitsu   | MHW BH                 | 1      | 1       | 946   | 0     | 2.59   |
| HGST      | Ultrastar 7K2          | 4      | 240     | 951   | 6     | 2.57   |
| WDC       | Black                  | 12     | 464     | 982   | 4     | 2.56   |
| WDC       | Gold                   | 19     | 443     | 976   | 12    | 2.51   |
| WDC       | Caviar SE              | 6      | 6       | 1881  | 254   | 2.51   |
| Seagate   | Seagate Enterprise     | 1      | 210     | 961   | 40    | 2.40   |
| HPE       | Seagate Constellati... | 1      | 21      | 1205  | 2     | 2.37   |
| HGST      | Ultrastar He6          | 1      | 46      | 895   | 1     | 2.33   |
| Seagate   | Barracuda SpinPoint F3 | 2      | 5       | 1751  | 4     | 2.28   |
| HGST      | Ultrastar DC HC520 ... | 5      | 2487    | 863   | 2     | 2.27   |
| Seagate   | Constellation ES.2 ... | 3      | 113     | 1078  | 25    | 2.27   |
| WDC       | Blue                   | 61     | 322     | 989   | 22    | 2.26   |
| HP        | Constellation ES.3     | 1      | 2       | 802   | 0     | 2.20   |
| Seagate   | Barracuda 7200.7 an... | 1      | 1       | 3197  | 3     | 2.19   |
| HGST      | Ultrastar He10         | 6      | 423     | 788   | 1     | 2.15   |
| Seagate   | Skyhawk                | 7      | 44      | 845   | 56    | 2.14   |
| Hitachi   | Ultrastar 7K4000       | 3      | 59      | 907   | 12    | 2.12   |
| Toshiba   | 3.5" MD04ACA Enterp... | 2      | 454     | 786   | 3     | 2.11   |
| Toshiba   | MG05ACA Enterprise ... | 1      | 677     | 808   | 4     | 2.11   |
| Seagate   | SpinPoint M8 (AF)      | 1      | 3       | 1127  | 4     | 2.07   |
| HGST      | Travelstar 7K1000      | 2      | 9       | 1383  | 562   | 2.02   |
| Seagate   | Pipeline HD 5900.2     | 1      | 10      | 1001  | 3     | 2.01   |
| Hitachi   | Travelstar 7K320       | 1      | 1       | 727   | 0     | 1.99   |
| Seagate   | Exos 7E2000            | 2      | 67      | 733   | 1     | 1.98   |
| Seagate   | Terascale              | 1      | 6       | 722   | 0     | 1.98   |
| Toshiba   | V300                   | 1      | 8       | 800   | 8     | 1.94   |
| Seagate   | Barracuda 3.5          | 2      | 57      | 735   | 19    | 1.94   |
| Toshiba   | 3.5" HDD E300          | 1      | 1       | 699   | 0     | 1.92   |
| Seagate   | Exos 7E2               | 9      | 149     | 958   | 11    | 1.89   |
| WDC       | Red Pro                | 12     | 158     | 739   | 3     | 1.88   |
| Hitachi   | Deskstar E7K1000       | 2      | 6       | 2618  | 3     | 1.88   |
| Seagate   | Mobile HDD             | 2      | 41      | 965   | 211   | 1.86   |
| HGST      | Ultrastar HC310/320    | 3      | 329     | 688   | 13    | 1.86   |
| Seagate   | Barracuda 7200.8       | 2      | 3       | 2399  | 5     | 1.84   |
| Seagate   | Barracuda Compute      | 2      | 6       | 663   | 0     | 1.82   |
| Seagate   | Barracuda 7200.12      | 9      | 32      | 1169  | 267   | 1.79   |
| Seagate   | Constellation ES       | 5      | 8       | 1524  | 144   | 1.76   |
| Samsung   | SpinPoint F3 RE        | 1      | 1       | 637   | 0     | 1.75   |
| WDC       | Purple                 | 15     | 63      | 641   | 1     | 1.72   |
| Seagate   | Barracuda 2.5 5400     | 5      | 123     | 703   | 46    | 1.65   |
| Seagate   | IronWolf Pro           | 5      | 22      | 1091  | 274   | 1.65   |
| MaxDig... | Unknown                | 2      | 2       | 868   | 508   | 1.63   |
| Seagate   | BarraCuda Pro          | 1      | 10      | 1026  | 317   | 1.61   |
| HPE       | Proliant HardDrive     | 11     | 385     | 619   | 1     | 1.60   |
| Samsung   | SpinPoint F2 EG        | 3      | 11      | 3499  | 543   | 1.59   |
| Seagate   | Momentus 7200.4        | 2      | 7       | 1227  | 157   | 1.58   |
| WDC       | Elements / My Passport | 12     | 21      | 607   | 49    | 1.56   |
| Toshiba   | MG04ACA Enterprise HDD | 4      | 18      | 676   | 1     | 1.55   |
| Toshiba   | 2.5" HDD MQ01ACF       | 2      | 7       | 736   | 2     | 1.54   |
| Toshiba   | MG07ACA Enterprise ... | 3      | 228     | 546   | 1     | 1.45   |
| Seagate   | BarraCuda 3.5 (CMR)    | 2      | 12      | 648   | 287   | 1.44   |
| HGST      | Ultrastar DC HC320     | 1      | 15      | 523   | 0     | 1.43   |
| Toshiba   | P300                   | 5      | 114     | 535   | 32    | 1.43   |
| Toshiba   | 2.5" HDD MQ01ABF       | 1      | 1       | 519   | 0     | 1.42   |
| Seagate   | Barracuda LP           | 1      | 1       | 518   | 0     | 1.42   |
| Seagate   | Exos X14               | 5      | 270     | 519   | 3     | 1.40   |
| WDC       | Ultrastar DC HC530     | 2      | 2259    | 515   | 1     | 1.40   |
| Toshiba   | L200                   | 2      | 13      | 581   | 1     | 1.39   |
| Toshiba   | Toshiba Client HDD     | 1      | 1       | 504   | 0     | 1.38   |
| MediaMax  | WL4000                 | 2      | 3       | 1037  | 352   | 1.37   |
| Seagate   | Momentus Thin          | 1      | 2       | 498   | 0     | 1.37   |
| Samsung   | SpinPoint F4           | 1      | 1       | 477   | 0     | 1.31   |
| Seagate   | IronWolf               | 17     | 493     | 504   | 45    | 1.29   |
| HGST      | Travelstar Z7K500      | 2      | 7       | 789   | 512   | 1.29   |
| HPE       | Seagate Enterprise     | 3      | 81      | 518   | 35    | 1.26   |
| Seagate   | FireCuda 2.5           | 1      | 4       | 449   | 0     | 1.23   |
| Toshiba   | N300 NAS HDD           | 5      | 32      | 485   | 1     | 1.23   |
| Toshiba   | MG06ACA Enterprise ... | 5      | 397     | 456   | 1     | 1.23   |
| HGST      | Ultrastar DC HC310     | 3      | 252     | 442   | 3     | 1.19   |
| Samsung   | SpinPoint P80 SD       | 1      | 2       | 1964  | 841   | 1.17   |
| Seagate   | FireCuda 3.5           | 1      | 4       | 424   | 0     | 1.16   |
| Seagate   | Exos 7E8               | 12     | 403     | 455   | 10    | 1.14   |
| Seagate   | Constellation ES (S... | 3      | 36      | 1079  | 67    | 1.14   |
| Samsung   | SpinPoint T166         | 1      | 3       | 2183  | 676   | 1.14   |
| Seagate   | BarraCuda 3.5          | 7      | 184     | 501   | 46    | 1.13   |
| WDC       | Blue Mobile            | 12     | 26      | 407   | 0     | 1.12   |
| WDC       | Scorpio Black          | 4      | 6       | 1074  | 51    | 1.12   |
| Toshiba   | 2.5" HDD MQ01ABD       | 2      | 6       | 641   | 716   | 1.10   |
| Toshiba   | 2.5" HDD MQ01ABB       | 1      | 2       | 1156  | 4     | 1.10   |
| Seagate   | Barracuda Pro Compute  | 1      | 4       | 398   | 0     | 1.09   |
| Seagate   | Barracuda 7200.9       | 4      | 5       | 1189  | 556   | 1.07   |
| Seagate   | Laptop HDD             | 3      | 11      | 748   | 291   | 1.05   |
| Hitachi   | Travelstar 5K250       | 1      | 1       | 1508  | 3     | 1.03   |
| Maxtor    | DiamondMax 22          | 1      | 2       | 561   | 617   | 1.02   |
| Seagate   | SkyHawk                | 4      | 25      | 359   | 0     | 0.98   |
| Toshiba   | Toshiba Enterprise     | 1      | 7       | 403   | 12    | 0.96   |
| WDC       | AV-GP                  | 5      | 9       | 459   | 2     | 0.94   |
| WDC       | Ultrastar DC HC330     | 1      | 26      | 312   | 9     | 0.85   |
| Seagate   | Momentus 7200.5        | 1      | 1       | 285   | 0     | 0.78   |
| HP        | 250GB SATA disk VB0... | 1      | 3       | 480   | 205   | 0.76   |
| Seagate   | Exos X16               | 9      | 288     | 256   | 1     | 0.70   |
| WDC       | Ultrastar DC HC500     | 1      | 8       | 239   | 0     | 0.66   |
| Toshiba   | 2.5" HDD MQ04UBF       | 1      | 4       | 234   | 0     | 0.64   |
| WDC       | Shrek LT 2.5           | 1      | 1       | 233   | 0     | 0.64   |
| Apple     | Travelstar 5K1000      | 1      | 1       | 220   | 0     | 0.60   |
| Toshiba   | MG08                   | 1      | 5       | 201   | 0     | 0.55   |
| Toshiba   | 2.5" HDD MK..52GSX     | 1      | 1       | 199   | 0     | 0.55   |
| Hitachi   | Deskstar 7K1000.D      | 2      | 12      | 1345  | 1097  | 0.53   |
| WDC       | Scorpio Blue           | 7      | 10      | 322   | 43    | 0.51   |
| WDC       | Green Mobile           | 1      | 4       | 1499  | 12    | 0.48   |
| WDC       | Ultrastar DC HC550     | 3      | 2200    | 163   | 1     | 0.45   |
| Maxtor    | DiamondMax 20          | 1      | 1       | 1203  | 7     | 0.41   |
| Apple     | HGST Travelstar Z5K500 | 1      | 1       | 141   | 0     | 0.39   |
| Samsung   | SpinPoint M7E (AF)     | 1      | 1       | 141   | 0     | 0.39   |
| Hitachi   | Travelstar 5K500.B     | 3      | 3       | 433   | 2     | 0.33   |
| Seagate   | Exos X10               | 1      | 4       | 121   | 0     | 0.33   |
| WDC       | Red Plus               | 3      | 15      | 115   | 0     | 0.32   |
| Toshiba   | MG08ACA Enterprise ... | 3      | 86      | 113   | 0     | 0.31   |
| Samsung   | SpinPoint M8 (AF)      | 1      | 1       | 112   | 0     | 0.31   |
| Seagate   | Exos X18               | 3      | 144     | 102   | 0     | 0.28   |
| Hitachi   | Travelstar 7K500       | 2      | 3       | 1298  | 343   | 0.28   |
| WDC       | IU CB500               | 1      | 1       | 76    | 0     | 0.21   |
| Toshiba   | 2.5" HDD MQ04ABF       | 1      | 2       | 306   | 1010  | 0.18   |
| Seagate   | Momentus 5400.6        | 2      | 6       | 588   | 34    | 0.17   |
| Seagate   | Video 3.5 HDD          | 2      | 2       | 113   | 16    | 0.16   |
| Toshiba   | MG09                   | 1      | 22      | 58    | 1     | 0.16   |
| Samsung   | SpinPoint MP5          | 1      | 1       | 373   | 8     | 0.11   |
| WDC       | HGST Ultrastar He10    | 1      | 1       | 38    | 0     | 0.11   |
| Seagate   | Momentus 5400.3        | 2      | 2       | 305   | 508   | 0.10   |
| Hitachi   | Travelstar 7K100       | 1      | 1       | 2330  | 66    | 0.10   |
| Apple     | Barracuda              | 1      | 1       | 254   | 8     | 0.08   |
| WDC       | Internal Use HDD       | 1      | 1       | 23    | 0     | 0.06   |
| Seagate   | Barracuda ES.2         | 3      | 6       | 612   | 1368  | 0.06   |
| Toshiba   | 2.5" HDD MQ04ABB       | 1      | 3       | 20    | 0     | 0.06   |
| Seagate   | SkyHawk AI             | 1      | 1       | 19    | 0     | 0.05   |
| Seagate   | Barracuda 7200.11      | 3      | 3       | 1690  | 278   | 0.05   |
| Toshiba   | 2.5" HDD MK..61GSY[N]  | 1      | 2       | 13    | 0     | 0.04   |
| Seagate   | Exos X20               | 1      | 4       | 12    | 0     | 0.04   |
| Hitachi   | Travelstar 5K320       | 1      | 1       | 130   | 12    | 0.03   |
| HGST      | Travelstar Z7K500.B    | 1      | 4       | 8     | 0     | 0.02   |
| Hitachi   | Deskstar T7K250        | 1      | 1       | 3853  | 579   | 0.02   |
| Samsung   | SpinPoint P120         | 1      | 1       | 1212  | 1105  | 0.00   |
| Seagate   | Momentus 5400.4        | 1      | 1       | 3408  | 3854  | 0.00   |
| Seagate   | FreePlay               | 1      | 2       | 32    | 545   | 0.00   |
| HGST      | Travelstar Z5K500      | 1      | 1       | 362   | 1023  | 0.00   |
| Seagate   | DB35.3                 | 1      | 1       | 235   | 1047  | 0.00   |

HDD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| Hitachi     | 58     | 558     | 2345  | 74    | 5.14   |
| Maxtor      | 6      | 10      | 1878  | 139   | 4.03   |
| Samsung     | 21     | 87      | 2433  | 180   | 3.41   |
| HP          | 20     | 39      | 2072  | 221   | 3.40   |
| Seagate     | 257    | 9670    | 1317  | 49    | 2.90   |
| HGST        | 63     | 5089    | 1007  | 7     | 2.64   |
| Fujitsu     | 1      | 1       | 946   | 0     | 2.59   |
| Toshiba     | 79     | 3713    | 964   | 12    | 2.49   |
| MediaMax    | 4      | 5       | 1036  | 211   | 1.96   |
| WDC         | 368    | 8296    | 795   | 8     | 1.81   |
| MaxDigital  | 2      | 2       | 868   | 508   | 1.63   |
| HPE         | 17     | 498     | 642   | 7     | 1.60   |
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

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Intel     | SSDSA2CW080G3      | 80 GB  | 1       | 3625  | 0     | 9.93   |
| Intel     | SSDSA2CW300G3      | 304 GB | 1       | 3503  | 0     | 9.60   |
| Crucial   | M4-CT256M4SSD2     | 256 GB | 1       | 3154  | 0     | 8.64   |
| Kingston  | SVP100S264G        | 64 GB  | 1       | 3150  | 0     | 8.63   |
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 3       | 3069  | 0     | 8.41   |
| Micron    | MTFDDAK512MAR-1... | 512 GB | 3       | 3013  | 0     | 8.26   |
| Samsung   | MZ7TE256HMHP-00000 | 256 GB | 1       | 2910  | 0     | 7.97   |
| Samsung   | MZ7TE128HMGR-00004 | 128 GB | 1       | 2803  | 0     | 7.68   |
| Samsung   | SSD 840 EVO        | 120 GB | 10      | 2753  | 0     | 7.54   |
| SATADOM   | D150SV             | 2 GB   | 1       | 2697  | 0     | 7.39   |
| Samsung   | MZ-5EA1000-0D3     | 100 GB | 1       | 2597  | 0     | 7.12   |
| Apple     | SSD SM256E         | 256 GB | 2       | 2543  | 0     | 6.97   |
| OCZ       | AGILITY3           | 240 GB | 1       | 2501  | 0     | 6.85   |
| Samsung   | SSD 830 Series     | 256 GB | 1       | 2440  | 0     | 6.69   |
| OCZ       | VERTEX4            | 256 GB | 1       | 2437  | 0     | 6.68   |
| HP        | VK0480GDPVT        | 480 GB | 1       | 2425  | 0     | 6.65   |
| Micron    | MTFDDAK128MAR-1... | 128 GB | 3       | 2373  | 0     | 6.50   |
| Intel     | SSDSC2BP240G4      | 240 GB | 11      | 2343  | 0     | 6.42   |
| HPE       | MK0800GCTZB        | 800 GB | 1       | 2321  | 0     | 6.36   |
| Intel     | VR0120GEJXL        | 120 GB | 3       | 2320  | 0     | 6.36   |
| Samsung   | SSD 830 Series     | 512 GB | 12      | 3084  | 253   | 6.33   |
| Intel     | SSDSC2CW240A3      | 240 GB | 55      | 2461  | 1     | 6.31   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 4       | 2292  | 0     | 6.28   |
| Intel     | SSDSA2CW120G3      | 120 GB | 41      | 2877  | 53    | 6.28   |
| Transcend | TS128GSSD340       | 128 GB | 1       | 2277  | 0     | 6.24   |
| Samsung   | SSD 840 EVO        | 500 GB | 12      | 3026  | 257   | 6.11   |
| Samsung   | MZ7LM120HCFD-00003 | 120 GB | 4       | 2221  | 0     | 6.09   |
| Corsair   | Force 3 SSD        | 120 GB | 3       | 2217  | 0     | 6.08   |
| Intel     | SSDSC2BA100G3      | 100 GB | 28      | 2294  | 1     | 5.98   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 2156  | 0     | 5.91   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 4       | 2155  | 0     | 5.90   |
| Samsung   | MZ7LM480HCHP-0E003 | 480 GB | 7       | 2153  | 0     | 5.90   |
| ADATA     | SP600              | 128 GB | 1       | 2142  | 0     | 5.87   |
| Kingston  | SH103S3480G        | 480 GB | 1       | 2135  | 0     | 5.85   |
| Samsung   | SSD 850 PRO        | 128 GB | 7       | 2133  | 0     | 5.85   |
| Micron    | P400e-MTFDDAK40... | 400 GB | 3       | 2107  | 0     | 5.77   |
| Samsung   | MZ7KM200HAGR00D3   | 200 GB | 2       | 2082  | 0     | 5.71   |
| Samsung   | MZ7WD480HAGM-00003 | 480 GB | 9       | 2063  | 0     | 5.65   |
| Plextor   | PX-128M5S          | 128 GB | 1       | 2039  | 0     | 5.59   |
| Intel     | SSDSC2BB800G4      | 800 GB | 7       | 2030  | 0     | 5.56   |
| Samsung   | SSD 850 PRO        | 1 TB   | 73      | 2628  | 5     | 5.55   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 2       | 2008  | 0     | 5.50   |
| Intel     | SSDSC2BW180A3L     | 180 GB | 1       | 2007  | 0     | 5.50   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 4       | 1983  | 0     | 5.43   |
| Micron    | MTFDDAK256MAR-1... | 256 GB | 3       | 2622  | 1     | 5.43   |
| OCZ       | VERTEX3            | 120 GB | 6       | 3237  | 4     | 5.43   |
| Samsung   | MZ7WD120HCFV-00003 | 120 GB | 1       | 1974  | 0     | 5.41   |
| Samsung   | MZ7TD512HAGM-00000 | 512 GB | 4       | 2299  | 1     | 5.40   |
| Intel     | SSDSC2BX012T4      | 1.2 TB | 4       | 1957  | 0     | 5.36   |
| Intel     | SSDSC2CW480A3      | 400 GB | 12      | 2112  | 1     | 5.35   |
| Kingston  | SE50S3480G         | 480 GB | 5       | 1952  | 0     | 5.35   |
| HPE       | MK0240GFDKQ        | 240 GB | 1       | 1942  | 0     | 5.32   |
| Intel     | SSDSA2BZ200G3      | 200 GB | 2       | 2530  | 1     | 5.32   |
| Samsung   | MZ7KM960HAHP-00005 | 800 GB | 1       | 1928  | 0     | 5.28   |
| Samsung   | MZ7LM960HCHP-0E003 | 960 GB | 4       | 1917  | 0     | 5.25   |
| Intel     | SSDSC2CW180A3      | 180 GB | 14      | 1974  | 1     | 5.22   |
| Crucial   | CT250MX200SSD1     | 250 GB | 11      | 1900  | 0     | 5.21   |
| Samsung   | MZ7WD480HCGM-00003 | 480 GB | 26      | 2042  | 70    | 5.19   |
| Intel     | SSDSC2BB480G4      | 480 GB | 60      | 2053  | 17    | 5.18   |
| Micron    | M500DC_MTFDDAK1... | 120 GB | 2       | 1890  | 0     | 5.18   |
| Intel     | SSDSC2BB120G4      | 120 GB | 18      | 1971  | 1     | 5.12   |
| Toshiba   | THNSNJ960PCSZ      | 960 GB | 42      | 1901  | 1     | 5.10   |
| Toshiba   | THNSN8480PCSE      | 480 GB | 1       | 1861  | 0     | 5.10   |
| Toshiba   | THNSNJ480PCSZ      | 480 GB | 1       | 1860  | 0     | 5.10   |
| Samsung   | MZ7LM1T9HCJM-0E003 | 1.9 TB | 2       | 1860  | 0     | 5.10   |
| HP        | VK0960GFDKK        | 960 GB | 1       | 1854  | 0     | 5.08   |
| Samsung   | SSD 840 EVO        | 1 TB   | 26      | 2493  | 48    | 5.06   |
| Kingston  | SKC300S37A120G     | 120 GB | 2       | 1843  | 0     | 5.05   |
| Intel     | SSDSC2BB160G4      | 160 GB | 61      | 2150  | 1     | 5.02   |
| OCZ       | TRION100           | 480 GB | 1       | 1833  | 0     | 5.02   |
| Intel     | SSDSC2BA400G3C     | 400 GB | 2       | 1804  | 0     | 4.94   |
| HP        | VK0240GECQN        | 240 GB | 8       | 1803  | 0     | 4.94   |
| Intel     | SSDSC2CT120A3      | 120 GB | 16      | 2735  | 2     | 4.92   |
| Intel     | SSDSC2BB300G4      | 304 GB | 9       | 1792  | 0     | 4.91   |
| Kingston  | SUV300S37A120G     | 120 GB | 1       | 1787  | 0     | 4.90   |
| Samsung   | MZ7WD240HAFV-000D2 | 240 GB | 7       | 2083  | 5     | 4.88   |
| Intel     | SSDSC2CT240A4      | 240 GB | 2       | 2646  | 1     | 4.84   |
| Intel     | SSDSC2CT080A4      | 80 GB  | 1       | 1758  | 0     | 4.82   |
| HP        | VK0800GDJYA        | 800 GB | 31      | 1924  | 2     | 4.81   |
| HPE       | MK001920GWCFB      | 1.9 TB | 1       | 1747  | 0     | 4.79   |
| Intel     | SSDSC2BW240A3      | 240 GB | 1       | 1743  | 0     | 4.78   |
| Samsung   | MZ7KM960HAHP-00005 | 960 GB | 73      | 1742  | 0     | 4.77   |
| Intel     | SSDSC2BB120G6K     | 120 GB | 24      | 1722  | 0     | 4.72   |
| Samsung   | MZ7LM480HCHP-00003 | 480 GB | 78      | 1744  | 3     | 4.71   |
| Samsung   | SSD 840 EVO        | 250 GB | 10      | 2674  | 5     | 4.69   |
| SanDisk   | SDSSDHII960G       | 960 GB | 1       | 1708  | 0     | 4.68   |
| Samsung   | SSD 850 PRO        | 256 GB | 42      | 1758  | 1     | 4.66   |
| SanDisk   | SDLF1DAR-960G-1HA2 | 960 GB | 12      | 1694  | 0     | 4.64   |
| Intel     | SSDSC2BB800G6      | 800 GB | 68      | 1812  | 15    | 4.64   |
| Intel     | SSDSC2BB120G6      | 120 GB | 7       | 1684  | 0     | 4.61   |
| Samsung   | MZ7WD960HAGP-00003 | 960 GB | 3       | 1681  | 0     | 4.61   |
| Crucial   | CT512MX100SSD1     | 240 GB | 4       | 2098  | 1     | 4.60   |
| Toshiba   | THNSN8240PCSE      | 240 GB | 2       | 1676  | 0     | 4.59   |
| Samsung   | MZ7LM1T9HCJM00D3   | 1.9 TB | 4       | 1672  | 0     | 4.58   |
| Intel     | SSDSC2BB012T6      | 1.2 TB | 18      | 1788  | 1     | 4.57   |
| Intel     | SSDSC2BB300H4      | 304 GB | 3       | 1663  | 0     | 4.56   |
| SanDisk   | SDLF1DAR480G-1HHS  | 480 GB | 2       | 1660  | 0     | 4.55   |
| Intel     | SSDSC2BB016T6      | 1.6 TB | 13      | 1658  | 0     | 4.54   |
| Samsung   | MZ7KM480HAHP-00005 | 480 GB | 92      | 1657  | 0     | 4.54   |
| Samsung   | MZ7PD480HAGM-000D3 | 480 GB | 1       | 1653  | 0     | 4.53   |
| Intel     | SSDSC2BB240G6      | 240 GB | 20      | 1652  | 0     | 4.53   |
| Kingston  | SE50S37480G        | 480 GB | 1       | 1648  | 0     | 4.52   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 7       | 1637  | 0     | 4.49   |
| Intel     | SSDSC2BX400G4      | 400 GB | 3       | 1636  | 0     | 4.48   |
| Intel     | SSDSC2BA400G3      | 400 GB | 7       | 1768  | 1     | 4.48   |
| Intel     | SSDSC2BA200G3      | 200 GB | 17      | 1906  | 1     | 4.45   |
| Samsung   | SSD 840 PRO Series | 128 GB | 17      | 2053  | 108   | 4.43   |
| Samsung   | MZ7GE960HMHP-00003 | 960 GB | 24      | 2270  | 109   | 4.42   |
| Intel     | SSDSC2BB240G4      | 240 GB | 45      | 1686  | 1     | 4.41   |
| Kingston  | SH103S3240G        | 240 GB | 2       | 2144  | 1     | 4.41   |
| Intel     | SSDSC2BB080G6      | 80 GB  | 1       | 1603  | 0     | 4.39   |
| Samsung   | SSD 850 PRO        | 512 GB | 55      | 1647  | 1     | 4.39   |
| Samsung   | MZ7LM960HCHP-00005 | 960 GB | 24      | 1595  | 0     | 4.37   |
| Kingston  | SE50S37240G        | 240 GB | 1       | 1588  | 0     | 4.35   |
| Toshiba   | VX500              | 1 TB   | 6       | 1579  | 0     | 4.33   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 2       | 1578  | 0     | 4.33   |
| SanDisk   | SSD i110           | 64 GB  | 1       | 1561  | 0     | 4.28   |
| Samsung   | MZ7KM240HAGR-00005 | 240 GB | 23      | 1586  | 1     | 4.26   |
| Samsung   | MZ7KM120HAFD-00005 | 120 GB | 15      | 1550  | 0     | 4.25   |
| Samsung   | MZ7KM480HAHP-0E005 | 480 GB | 15      | 1537  | 0     | 4.21   |
| Kingston  | SKC300S37A240G     | 240 GB | 12      | 1536  | 0     | 4.21   |
| Intel     | SSDSC2BB480H4      | 480 GB | 9       | 1708  | 1     | 4.19   |
| Crucial   | CT750MX300SSD1     | 752 GB | 16      | 1769  | 1     | 4.18   |
| Kingston  | SVP200S37A120G     | 120 GB | 1       | 1522  | 0     | 4.17   |
| OCZ       | SABER1000          | 120 GB | 2       | 1522  | 0     | 4.17   |
| Samsung   | MZ7KM120HAFD-0E005 | 120 GB | 2       | 1517  | 0     | 4.16   |
| Samsung   | SSD 840 Series     | 250 GB | 4       | 2752  | 269   | 4.12   |
| SanDisk   | X300 MSATA         | 256 GB | 1       | 1502  | 0     | 4.12   |
| HPE       | MK0200GEYKC        | 200 GB | 21      | 1496  | 0     | 4.10   |
| Intel     | SSDSC2BB480G6      | 480 GB | 42      | 1488  | 0     | 4.08   |
| ADATA     | SP900              | 256 GB | 2       | 2463  | 2     | 4.05   |
| Intel     | SSDSA2BW600G3D     | 600 GB | 2       | 2213  | 1     | 4.04   |
| Intel     | SSDSC2BX200G4      | 200 GB | 18      | 1471  | 0     | 4.03   |
| Samsung   | SSD 840 PRO Series | 512 GB | 10      | 1967  | 63    | 4.02   |
| Kingston  | SH103S3120G        | 120 GB | 10      | 1601  | 1     | 4.02   |
| Crucial   | CT500MX200SSD1     | 500 GB | 16      | 1465  | 0     | 4.01   |
| Samsung   | MZ7LM120HCFD-00005 | 120 GB | 1       | 1464  | 0     | 4.01   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 14      | 1464  | 0     | 4.01   |
| Samsung   | MCBQE25G5MPQ-0VAD3 | 25 GB  | 1       | 1456  | 0     | 3.99   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 26      | 1445  | 0     | 3.96   |
| Apacer    | AS510S             | 128 GB | 1       | 1444  | 0     | 3.96   |
| SPCC      | SSD                | 120 GB | 1       | 1444  | 0     | 3.96   |
| Intel     | SSDSC2BA200G4      | 200 GB | 130     | 1426  | 0     | 3.91   |
| Kingston  | SE50S37100G        | 100 GB | 1       | 1425  | 0     | 3.90   |
| Samsung   | MZ7KM960HMJP0D3    | 960 GB | 120     | 1413  | 0     | 3.87   |
| Kingston  | SKC400S37128G      | 128 GB | 4       | 1403  | 0     | 3.85   |
| Intel     | SSDSC2BB600G4      | 600 GB | 11      | 1396  | 0     | 3.83   |
| SanDisk   | SD7UB2Q512G1022    | 512 GB | 7       | 1498  | 1     | 3.81   |
| Crucial   | CT480BX200SSD1     | 480 GB | 1       | 1389  | 0     | 3.81   |
| Micron    | 5100_MTFDDAK240TCC | 240 GB | 6       | 1572  | 1     | 3.80   |
| SanDisk   | SDLF1CRM-017T-1HST | 1.7 TB | 4       | 1383  | 0     | 3.79   |
| Lite-On   | PH3-CE120          | 120 GB | 2       | 1376  | 0     | 3.77   |
| SanDisk   | SDLF1CRR019T-1HHS  | 1.9 TB | 30      | 1412  | 34    | 3.76   |
| Intel     | SSDSC2BA800G4      | 800 GB | 17      | 1367  | 0     | 3.75   |
| Kingston  | SV300S37A240G      | 240 GB | 103     | 1583  | 9     | 3.74   |
| Samsung   | SSD 850 EVO        | 120 GB | 15      | 1444  | 15    | 3.73   |
| Kingston  | SE50S3100G         | 100 GB | 3       | 1693  | 1     | 3.72   |
| Intel     | SSDSC2BB800G7R     | 800 GB | 40      | 1704  | 53    | 3.71   |
| Lite-On   | PH4-CE120          | 120 GB | 1       | 1352  | 0     | 3.71   |
| SPCC      | SSD                | 240 GB | 1       | 1351  | 0     | 3.70   |
| Samsung   | MZ7KM960HAHP-0E005 | 960 GB | 4       | 1348  | 0     | 3.70   |
| Samsung   | MZ7LN512HMJP-00000 | 512 GB | 13      | 1494  | 3     | 3.69   |
| Samsung   | MZ7KM1T9HAJM-000NU | 1.9 TB | 1       | 1342  | 0     | 3.68   |
| Intel     | SSDSC2BP480G4      | 480 GB | 1       | 1339  | 0     | 3.67   |
| Intel     | SSDSC2BB016T4      | 1.6 TB | 5       | 1751  | 1     | 3.66   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 1       | 1330  | 0     | 3.65   |
| Samsung   | SSD 850 PRO        | 2 TB   | 3       | 1318  | 0     | 3.61   |
| Samsung   | MZ7KM1T9HAJM-00005 | 1.9 TB | 55      | 1305  | 0     | 3.58   |
| Samsung   | MZ7KM240HMHQ0D3    | 240 GB | 2       | 1295  | 0     | 3.55   |
| SanDisk   | Ultra II           | 960 GB | 12      | 1293  | 0     | 3.54   |
| Samsung   | MZ7GE480HMHP-00003 | 480 GB | 12      | 1995  | 165   | 3.53   |
| Samsung   | SSD 840 PRO Series | 256 GB | 19      | 2731  | 277   | 3.50   |
| SK hynix  | HFS500G32TND-N1A2A | 500 GB | 2       | 1270  | 0     | 3.48   |
| Intel     | SSDSC2KB960G7R     | 960 GB | 10      | 1335  | 1     | 3.48   |
| Samsung   | SSD 750 EVO        | 120 GB | 2       | 1266  | 0     | 3.47   |
| Micron    | M510DC_MTFDDAK2... | 240 GB | 1       | 1264  | 0     | 3.46   |
| Samsung   | SSD 850 EVO        | 500 GB | 126     | 1315  | 26    | 3.43   |
| Kingston  | SUV300S37A240G     | 240 GB | 2       | 1245  | 0     | 3.41   |
| Intel     | SSDSC2BX800G4      | 800 GB | 2       | 1244  | 0     | 3.41   |
| Samsung   | SSD 850 EVO        | 2 TB   | 20      | 1419  | 7     | 3.40   |
| Intel     | SSDSC2BA200G4C     | 200 GB | 5       | 1236  | 0     | 3.39   |
| Intel     | SSDSC2BA400G4      | 400 GB | 20      | 1226  | 0     | 3.36   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 2       | 1225  | 0     | 3.36   |
| SATADOM   | ML 3MG-P           | 32 GB  | 2       | 1215  | 0     | 3.33   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 4       | 1207  | 0     | 3.31   |
| HP        | VK0480GEQNB        | 480 GB | 1       | 1199  | 0     | 3.28   |
| Samsung   | MZ7KM240HAGR-0E005 | 240 GB | 17      | 1770  | 23    | 3.27   |
| WDC       | WDS250G1B0A-00H9H0 | 250 GB | 1       | 1181  | 0     | 3.24   |
| Toshiba   | THNSN8960PCSE      | 960 GB | 32      | 1197  | 1     | 3.23   |
| OCZ       | VECTOR             | 128 GB | 1       | 2353  | 1     | 3.22   |
| Intel     | SSDSC2BB150G7      | 150 GB | 15      | 1228  | 1     | 3.21   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 5       | 1161  | 0     | 3.18   |
| Intel     | SSDSC2BB240G7      | 240 GB | 21      | 1159  | 0     | 3.18   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 2       | 1152  | 0     | 3.16   |
| Samsung   | MZ7LM480HCHP-00005 | 480 GB | 26      | 1149  | 0     | 3.15   |
| Samsung   | SSD 850 EVO        | 1 TB   | 206     | 1491  | 67    | 3.15   |
| Dell      | SSDSCKJB120G7R     | 120 GB | 5       | 1346  | 1     | 3.10   |
| Samsung   | MZ7GE240HMGR-00003 | 240 GB | 4       | 1234  | 89    | 3.08   |
| SuperM... | SSD                | 32 GB  | 16      | 1121  | 0     | 3.07   |
| Kingston  | SEDC400S37480G     | 480 GB | 2       | 1121  | 0     | 3.07   |
| SanDisk   | SDSSDH31000G       | 1 TB   | 13      | 1292  | 8     | 3.07   |
| SanDisk   | SD6SB1M064G1022I   | 64 GB  | 6       | 1119  | 0     | 3.07   |
| Micron    | 5100_MTFDDAK960TBY | 960 GB | 4       | 1115  | 0     | 3.05   |
| Samsung   | MZ7TE256HMHP-00004 | 256 GB | 1       | 1108  | 0     | 3.04   |
| Intel     | SSDSC2BX100G4      | 100 GB | 2       | 1090  | 0     | 2.99   |
| Samsung   | MZ7LM240HCGR-00005 | 240 GB | 4       | 1079  | 0     | 2.96   |
| SanDisk   | SDSSDA960G         | 960 GB | 1       | 1074  | 0     | 2.94   |
| Micron    | M510DC_MTFDDAK9... | 960 GB | 2       | 1985  | 4     | 2.94   |
| Samsung   | MZ7KM1T9HMJP-00005 | 1.9 TB | 86      | 1067  | 0     | 2.93   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 64      | 1070  | 12    | 2.92   |
| Intel     | SSDSCKJB150G7      | 150 GB | 14      | 1210  | 1     | 2.92   |
| Samsung   | MZ7LM1T9HCJM-00003 | 1.9 TB | 7       | 1061  | 0     | 2.91   |
| SanDisk   | SDLF1DAR-480G-1HA1 | 480 GB | 39      | 1057  | 0     | 2.90   |
| Samsung   | MZ7LM960HCHP-00003 | 960 GB | 32      | 1050  | 0     | 2.88   |
| Samsung   | SSD PM830 2.5" 7mm | 256 GB | 1       | 1044  | 0     | 2.86   |
| Toshiba   | THNSF8800CCSE      | 800 GB | 1       | 1042  | 0     | 2.86   |
| SanDisk   | SD7UB2Q512G1122    | 512 GB | 8       | 1531  | 10    | 2.85   |
| Toshiba   | THNSNJ256GCSU      | 256 GB | 1       | 1036  | 0     | 2.84   |
| Samsung   | SSD 850 EVO        | 250 GB | 92      | 1169  | 42    | 2.83   |
| Patriot   | Blast              | 240 GB | 1       | 1030  | 0     | 2.82   |
| Intel     | SSDSC2BB480G7O     | 480 GB | 5       | 1624  | 3     | 2.82   |
| Intel     | SSDSC2KG480G7      | 480 GB | 54      | 1308  | 2     | 2.81   |
| Intel     | SSDSC2BB480G7      | 480 GB | 107     | 1182  | 1     | 2.80   |
| Kingston  | SKC400S37512G      | 512 GB | 5       | 1022  | 0     | 2.80   |
| Kingston  | SV300S37A60G       | 64 GB  | 5       | 1678  | 2     | 2.79   |
| Kingston  | SV300S37A120G      | 120 GB | 39      | 1506  | 26    | 2.77   |
| Goodram   | SSD                | 240 GB | 4       | 1006  | 0     | 2.76   |
| Samsung   | MZ7KM960HAHP-0Z005 | 960 GB | 1       | 1004  | 0     | 2.75   |
| Intel     | SSDSC1BG200G4      | 200 GB | 1       | 1001  | 0     | 2.74   |
| OWC       | Mercury Accelsi... | 240 GB | 1       | 2002  | 1     | 2.74   |
| SuperM... | SSD                | 64 GB  | 27      | 1022  | 1     | 2.73   |
| Samsung   | MZ7LM960HMJP0D3    | 960 GB | 44      | 1030  | 1     | 2.71   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 164     | 990   | 0     | 2.71   |
| OCZ       | VERTEX3 MI         | 120 GB | 1       | 2968  | 2     | 2.71   |
| Samsung   | SSD 750 EVO        | 250 GB | 4       | 979   | 0     | 2.68   |
| Kingston  | SKC400S371T        | 1 TB   | 10      | 978   | 0     | 2.68   |
| HP        | VK000240GWCNP      | 240 GB | 6       | 978   | 0     | 2.68   |
| Kingston  | SHFS37A480G        | 480 GB | 3       | 1412  | 4     | 2.65   |
| Toshiba   | THNSF8200CCSE      | 200 GB | 20      | 1058  | 1     | 2.64   |
| HP        | VK0240GDJXU        | 240 GB | 2       | 1452  | 1     | 2.62   |
| Mushkin   | MKNSSDRE120GB      | 120 GB | 1       | 949   | 0     | 2.60   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 27      | 949   | 0     | 2.60   |
| OCZ       | ARC100             | 480 GB | 4       | 1129  | 21    | 2.59   |
| MyDigi... | SB2                | 128 GB | 6       | 945   | 0     | 2.59   |
| HPE       | MK0400GEYKD        | 400 GB | 1       | 941   | 0     | 2.58   |
| HP        | VK0480GEYJR        | 480 GB | 1       | 938   | 0     | 2.57   |
| Intel     | SSDSC2KG240G7      | 240 GB | 42      | 943   | 1     | 2.56   |
| Team      | T2535T120G         | 120 GB | 2       | 933   | 0     | 2.56   |
| Samsung   | SSD 840 Series     | 120 GB | 7       | 1862  | 86    | 2.54   |
| HP        | VK000240GWCFD      | 240 GB | 3       | 925   | 0     | 2.53   |
| Intel     | SSDSC2KG240G7R     | 240 GB | 26      | 994   | 81    | 2.53   |
| Kingston  | SEDC400S37960G     | 960 GB | 10      | 918   | 0     | 2.52   |
| Intel     | SSDSA2BW160G3L     | 160 GB | 1       | 914   | 0     | 2.50   |
| HP        | VK000480GWJPE      | 480 GB | 1       | 909   | 0     | 2.49   |
| ADATA     | SU800              | 128 GB | 2       | 907   | 0     | 2.49   |
| HP        | VK0300GDUQV        | 304 GB | 1       | 903   | 0     | 2.48   |
| Kingston  | SKC400S37256G      | 256 GB | 1       | 902   | 0     | 2.47   |
| Samsung   | MZ7LM960HMJP-00005 | 960 GB | 337     | 1233  | 26    | 2.47   |
| Crucial   | CT960M500SSD1      | 960 GB | 18      | 1909  | 7     | 2.46   |
| Micron    | M510DC_MTFDDAK4... | 480 GB | 3       | 888   | 0     | 2.43   |
| Intel     | SSDSC2BA012T4      | 1.2 TB | 1       | 887   | 0     | 2.43   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 11      | 885   | 0     | 2.43   |
| SanDisk   | Ultra II           | 480 GB | 15      | 910   | 1     | 2.41   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 2       | 881   | 0     | 2.41   |
| SanDisk   | SDSSDH3250G        | 250 GB | 1       | 881   | 0     | 2.41   |
| Seagate   | XF1230-1A0480      | 480 GB | 14      | 878   | 0     | 2.41   |
| Intel     | SSDSC2BX480G4      | 480 GB | 24      | 876   | 0     | 2.40   |
| Samsung   | MZ7KH3T8HALS-00005 | 3.8 TB | 7       | 872   | 0     | 2.39   |
| Toshiba   | THNSF8240CCSE      | 240 GB | 10      | 872   | 0     | 2.39   |
| HP        | VK000480GWSRR      | 480 GB | 4       | 864   | 0     | 2.37   |
| Samsung   | SSD 860 PRO        | 256 GB | 57      | 854   | 0     | 2.34   |
| Intel     | SSDSC2BB016T7      | 1.6 TB | 61      | 1641  | 4     | 2.33   |
| Intel     | SSDSC2BX016T4      | 1.6 TB | 1       | 849   | 0     | 2.33   |
| Seagate   | XF1230-1A0240      | 240 GB | 10      | 845   | 0     | 2.32   |
| Micron    | 5100_MTFDDAK480TCC | 480 GB | 18      | 997   | 1     | 2.31   |
| Intel     | SSDSC2MH120A2      | 120 GB | 2       | 842   | 0     | 2.31   |
| Crucial   | CT275MX300SSD1     | 275 GB | 40      | 1039  | 1     | 2.31   |
| HP        | VK0960GFLKK        | 960 GB | 1       | 841   | 0     | 2.31   |
| Samsung   | SSD 860 EVO        | 4 TB   | 11      | 840   | 0     | 2.30   |
| Samsung   | MZ7LN256HMJP-00000 | 256 GB | 1       | 840   | 0     | 2.30   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 5       | 836   | 0     | 2.29   |
| Seagate   | XF1230-1A0960      | 960 GB | 2       | 833   | 0     | 2.28   |
| Intel     | SSDSC2KB240G7      | 240 GB | 64      | 928   | 8     | 2.28   |
| SATADOM   | SL 3IE3 V2         | 64 GB  | 7       | 832   | 0     | 2.28   |
| Team      | T253X1960G         | 960 GB | 3       | 830   | 0     | 2.28   |
| Kingston  | SUV500240G         | 240 GB | 4       | 826   | 0     | 2.26   |
| Crucial   | CT525MX300SSD1     | 528 GB | 49      | 909   | 1     | 2.25   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 29      | 1058  | 2     | 2.25   |
| Samsung   | MZNLN512HMJP-00000 | 512 GB | 11      | 820   | 0     | 2.25   |
| OWC       | Mercury Electra... | 250 GB | 2       | 818   | 0     | 2.24   |
| Samsung   | SSD 860 PRO        | 4 TB   | 14      | 815   | 0     | 2.23   |
| AMD       | R3SL120G           | 120 GB | 2       | 812   | 0     | 2.23   |
| Intel     | SSDSA2CW160G3      | 160 GB | 1       | 1623  | 1     | 2.22   |
| XPG       | SX950U             | 120 GB | 2       | 806   | 0     | 2.21   |
| Samsung   | SSD 860 DCT 1.92TB | 1.9 TB | 19      | 804   | 0     | 2.20   |
| Intel     | SSDSC2KG960G7      | 960 GB | 46      | 1272  | 4     | 2.19   |
| Samsung   | MZ7LM1T9HMJP-00005 | 1.9 TB | 106     | 1175  | 13    | 2.19   |
| WDC       | WDS100T2B0A        | 1 TB   | 9       | 797   | 0     | 2.18   |
| Apacer    | AS330              | 240 GB | 1       | 796   | 0     | 2.18   |
| SuperM... | SSD                | 128 GB | 134     | 815   | 11    | 2.18   |
| Toshiba   | THNSN81Q92CSE      | 1.9 TB | 7       | 795   | 0     | 2.18   |
| Micron    | 5100_MTFDDAK1T9TBY | 1.9 TB | 74      | 1388  | 20    | 2.17   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 10      | 790   | 0     | 2.17   |
| Intel     | SSDMCEAC120B3      | 120 GB | 1       | 788   | 0     | 2.16   |
| Micron    | M600_MTFDDAK1T0MBF | 1 TB   | 1       | 782   | 0     | 2.14   |
| Kingston  | SM2280S3G2120G     | 120 GB | 1       | 779   | 0     | 2.14   |
| Intel     | SSDSC2BW120H6      | 120 GB | 5       | 905   | 3     | 2.13   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 6       | 775   | 0     | 2.12   |
| ADATA     | SP600NS34          | 128 GB | 1       | 772   | 0     | 2.12   |
| SanDisk   | SDSSDA240G         | 240 GB | 2       | 768   | 0     | 2.11   |
| Crucial   | CT256MX100SSD1     | 256 GB | 4       | 1545  | 503   | 2.10   |
| Kingston  | SUV500M8480G       | 480 GB | 1       | 764   | 0     | 2.09   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 3       | 762   | 0     | 2.09   |
| Samsung   | SSD 860 QVO        | 2 TB   | 26      | 762   | 0     | 2.09   |
| SanDisk   | SD7SB7S512G1122    | 512 GB | 1       | 762   | 0     | 2.09   |
| Micron    | 5200_MTFDDAK1T9TDC | 1.9 TB | 10      | 940   | 2     | 2.08   |
| HP        | SSD M700           | 120 GB | 3       | 751   | 0     | 2.06   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 37      | 1110  | 3     | 2.05   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 31      | 784   | 1     | 2.04   |
| Samsung   | SSD 860 PRO        | 2 TB   | 157     | 740   | 0     | 2.03   |
| Micron    | 5200_MTFDDAK480TDN | 480 GB | 17      | 739   | 0     | 2.03   |
| HPE       | MR000240GWFLU      | 240 GB | 2       | 737   | 0     | 2.02   |
| SanDisk   | SDSSDH32000G       | 2 TB   | 2       | 736   | 0     | 2.02   |
| Toshiba   | TR150              | 960 GB | 1       | 1473  | 1     | 2.02   |
| Micron    | 5200_MTFDDAK240TDN | 240 GB | 40      | 735   | 0     | 2.02   |
| Samsung   | SSD PM851a 2.5 7mm | 1 TB   | 1       | 732   | 0     | 2.01   |
| HPE       | MK000240GWEZF      | 240 GB | 10      | 732   | 0     | 2.01   |
| Samsung   | SSD 883 DCT 1.92TB | 1.9 TB | 228     | 732   | 1     | 1.99   |
| Samsung   | SSD 860 EVO        | 2 TB   | 157     | 727   | 0     | 1.99   |
| Crucial   | CT500BX100SSD1     | 500 GB | 2       | 723   | 0     | 1.98   |
| WDC       | HBS3A1996A7E6B1    | 960 GB | 2       | 720   | 0     | 1.97   |
| Micron    | MTFDDAK480TDN      | 480 GB | 38      | 733   | 1     | 1.97   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 9       | 718   | 0     | 1.97   |
| HPE       | MK000960GWUGH      | 960 GB | 6       | 806   | 1     | 1.96   |
| Intel     | SSDSC2BB480G7R     | 480 GB | 24      | 752   | 1     | 1.96   |
| Kingston  | SA400M8120G        | 120 GB | 3       | 714   | 0     | 1.96   |
| Micron    | 5100_MTFDDAK960TCB | 960 GB | 128     | 1120  | 4     | 1.96   |
| Intel     | SSDSC2BF120A4H     | 120 GB | 2       | 711   | 0     | 1.95   |
| SuperM... | SSD                | 16 GB  | 29      | 708   | 0     | 1.94   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 42      | 1094  | 48    | 1.93   |
| Toshiba   | THNSNJ800PCSZ      | 800 GB | 4       | 700   | 0     | 1.92   |
| Samsung   | MZ7LM3T8HMLP-00005 | 3.8 TB | 2       | 697   | 0     | 1.91   |
| Micron    | 5200_MTFDDAK3T8TDC | 3.8 TB | 31      | 715   | 1     | 1.91   |
| Samsung   | MZ7LH960HAJR-000AZ | 960 GB | 4       | 694   | 0     | 1.90   |
| WDC       | WDS200T2B0A        | 2 TB   | 9       | 693   | 0     | 1.90   |
| Micron    | M500DC_MTFDDAK8... | 800 GB | 27      | 703   | 1     | 1.89   |
| HP        | VK000240GWJPD      | 240 GB | 1       | 686   | 0     | 1.88   |
| Samsung   | SSD 883 DCT        | 960 GB | 39      | 679   | 0     | 1.86   |
| Samsung   | MZ7LN256HCHP-000H1 | 256 GB | 1       | 678   | 0     | 1.86   |
| Plextor   | PH6-CE120-L1       | 120 GB | 1       | 674   | 0     | 1.85   |
| SanDisk   | SDLFOCAM-800G-1HA1 | 800 GB | 1       | 670   | 0     | 1.84   |
| Micron    | 5200_MTFDDAK1T9TDD | 1.9 TB | 68      | 738   | 1     | 1.84   |
| Intel     | SSDSC2KG240G8R     | 240 GB | 1       | 664   | 0     | 1.82   |
| Kingston  | SHSS37A240G        | 240 GB | 3       | 661   | 0     | 1.81   |
| Transcend | TSMSSSD01-240GP    | 240 GB | 4       | 661   | 0     | 1.81   |
| Intel     | SSDSC2BB800G7      | 800 GB | 1       | 1320  | 1     | 1.81   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 98      | 657   | 0     | 1.80   |
| Samsung   | MZ7LM1T9HMJP0D3    | 1.9 TB | 2       | 656   | 0     | 1.80   |
| Micron    | 5200_MTFDDAK960TDD | 960 GB | 156     | 675   | 1     | 1.78   |
| Micron    | 5200_MTFDDAK480TDC | 480 GB | 27      | 659   | 1     | 1.78   |
| Intel     | SSDSCKKB240G8      | 240 GB | 17      | 645   | 0     | 1.77   |
| Kingston  | SUV400S37120G      | 120 GB | 12      | 674   | 3     | 1.77   |
| Intel     | SSDSC2BW180A4      | 180 GB | 2       | 644   | 0     | 1.77   |
| Samsung   | MZ7LM960HMJP-000MV | 960 GB | 4       | 641   | 0     | 1.76   |
| Samsung   | MZ7KH960HAJR-00005 | 960 GB | 57      | 640   | 0     | 1.76   |
| HPE       | MK001920GWUGK      | 1.9 TB | 2       | 633   | 0     | 1.74   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 11      | 777   | 2     | 1.73   |
| Toshiba   | THNSF8400CCSE      | 400 GB | 12      | 631   | 0     | 1.73   |
| Micron    | 5200_MTFDDAK960TDN | 960 GB | 4       | 630   | 0     | 1.73   |
| Intel     | SSDSC2BB012T7      | 1.2 TB | 173     | 1160  | 3     | 1.73   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 1       | 629   | 0     | 1.72   |
| Samsung   | MZ7KM480HMHQ-000MV | 480 GB | 37      | 626   | 0     | 1.72   |
| Transcend | TS256GSSD370       | 256 GB | 1       | 624   | 0     | 1.71   |
| Seagate   | XA1920ME10063      | 1.9 TB | 35      | 624   | 0     | 1.71   |
| Micron    | 5100_MTFDDAK480TBY | 480 GB | 15      | 808   | 3     | 1.70   |
| SK hynix  | HFS120G32TND-N1A2A | 120 GB | 1       | 620   | 0     | 1.70   |
| SK hynix  | SC300 2.5 7MM      | 256 GB | 1       | 618   | 0     | 1.69   |
| Intel     | SSDSCKJB240G7      | 240 GB | 5       | 616   | 0     | 1.69   |
| SanDisk   | SDSSDHP256G        | 256 GB | 1       | 613   | 0     | 1.68   |
| Intel     | SSDSC2BW120A4      | 120 GB | 47      | 769   | 1     | 1.68   |
| Micron    | 5200_MTFDDAK960TDC | 960 GB | 47      | 649   | 1     | 1.68   |
| Goodram   | IR-SSDPR-S25A-120  | 120 GB | 7       | 612   | 0     | 1.68   |
| SanDisk   | SDLF1CRR-019T-1HA1 | 1.9 TB | 10      | 650   | 1     | 1.67   |
| Intel     | SSDSC2KB038T7      | 3.8 TB | 18      | 901   | 2     | 1.67   |
| Intel     | SSDSC2KB480G8      | 480 GB | 273     | 621   | 1     | 1.66   |
| Seagate   | XA1920LE10063      | 1.9 TB | 20      | 607   | 0     | 1.66   |
| Seagate   | XA960ME10063       | 960 GB | 4       | 600   | 0     | 1.64   |
| Samsung   | SSD 860 PRO        | 1 TB   | 111     | 599   | 0     | 1.64   |
| Samsung   | MZ7LH960HAJR0D3    | 960 GB | 20      | 597   | 0     | 1.64   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 5       | 597   | 0     | 1.64   |
| Intel     | SSDSC2KG019T7R     | 1.9 TB | 15      | 914   | 3     | 1.64   |
| Goodram   | SSDPR-CX400-512    | 512 GB | 3       | 596   | 0     | 1.63   |
| Samsung   | MZ7LM480HMHQ-00005 | 480 GB | 73      | 1204  | 28    | 1.62   |
| Intel     | SSDSC2KG240G8      | 240 GB | 184     | 590   | 1     | 1.61   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 2       | 585   | 0     | 1.60   |
| Plextor   | PX-256M6S+         | 256 GB | 2       | 584   | 0     | 1.60   |
| Intel     | SSDSC2KB019T7      | 1.9 TB | 65      | 1017  | 4     | 1.60   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 7       | 583   | 0     | 1.60   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 36      | 664   | 29    | 1.59   |
| Seagate   | XA480ME10063       | 480 GB | 10      | 579   | 0     | 1.59   |
| Phison    | SATA SSD           | 480 GB | 3       | 578   | 0     | 1.59   |
| Samsung   | SSD 860 EVO        | 500 GB | 291     | 578   | 1     | 1.58   |
| Intel     | SSDSC2KB240G8      | 240 GB | 780     | 596   | 2     | 1.57   |
| HP        | VK001920GWSXK      | 1.9 TB | 35      | 571   | 0     | 1.57   |
| Samsung   | SSD 845DC PRO      | 800 GB | 4       | 2276  | 3     | 1.56   |
| Kingston  | SV300S37A480G      | 480 GB | 11      | 1156  | 40    | 1.55   |
| Intel     | SSDSC2CW120A3      | 120 GB | 34      | 2166  | 749   | 1.55   |
| SK hynix  | SC311 SATA         | 1 TB   | 2       | 563   | 0     | 1.54   |
| Micron    | 5210_MTFDDAK1T9QDE | 1.9 TB | 4       | 562   | 0     | 1.54   |
| Kingston  | SA400S37120G       | 120 GB | 46      | 589   | 1     | 1.54   |
| Samsung   | MZ7LM240HMHQ-00005 | 240 GB | 79      | 953   | 136   | 1.53   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 23      | 559   | 0     | 1.53   |
| Intel     | SSDSC2KB480G7      | 480 GB | 43      | 680   | 1     | 1.53   |
| SATADOM   | SL 3SE             | 32 GB  | 3       | 556   | 0     | 1.52   |
| Samsung   | MZ7KH240HAHQ-00005 | 240 GB | 66      | 554   | 0     | 1.52   |
| Micron    | MTFDDAV480TDS-1... | 480 GB | 1       | 551   | 0     | 1.51   |
| Intel     | SSDSC2BB960G7      | 960 GB | 33      | 1031  | 2     | 1.51   |
| Kingston  | SUV400S37240G      | 240 GB | 53      | 565   | 1     | 1.50   |
| Intel     | SSDSC2KB960G7      | 960 GB | 175     | 1308  | 12    | 1.50   |
| HP        | VK0480GFLKH        | 480 GB | 2       | 547   | 0     | 1.50   |
| Micron    | 5200_MTFDDAK1T9TDN | 1.9 TB | 19      | 627   | 1     | 1.50   |
| Plextor   | PX-128S3C          | 128 GB | 1       | 544   | 0     | 1.49   |
| Samsung   | MZ7LH480HAHQ-000V3 | 480 GB | 5       | 544   | 0     | 1.49   |
| PNY       | CS900 120GB SSD    | 120 GB | 2       | 543   | 0     | 1.49   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 2       | 542   | 0     | 1.49   |
| Samsung   | MZ7KH1T9HAJR-00005 | 1.9 TB | 117     | 541   | 1     | 1.47   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 2       | 538   | 0     | 1.47   |
| Innodisk  | 2.5" SATA SSD 3ME4 | 128 GB | 1       | 1074  | 1     | 1.47   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 22      | 1252  | 22    | 1.47   |
| Intel     | SSDSC2BF120A4H SED | 120 GB | 2       | 535   | 0     | 1.47   |
| Samsung   | SSD 860 EVO        | 250 GB | 119     | 537   | 2     | 1.46   |
| Samsung   | MZ7LH240HAHQ0D3    | 240 GB | 6       | 534   | 0     | 1.46   |
| Samsung   | SSD 860 QVO        | 1 TB   | 58      | 530   | 0     | 1.45   |
| HP        | VK000240GWSRQ      | 240 GB | 23      | 529   | 0     | 1.45   |
| Crucial   | CT120BX500SSD1     | 120 GB | 38      | 528   | 0     | 1.45   |
| Samsung   | SSD 860 EVO        | 1 TB   | 457     | 529   | 1     | 1.45   |
| Micron    | MTFDDAK128MBF-1... | 128 GB | 13      | 526   | 0     | 1.44   |
| PNY       | CS900 480GB SSD    | 480 GB | 1       | 524   | 0     | 1.44   |
| Intel     | SSDSC2BW240A4      | 240 GB | 44      | 861   | 7     | 1.43   |
| Kingston  | SEDC500M960G       | 960 GB | 14      | 547   | 1     | 1.43   |
| Intel     | SSDSC2KB960G8      | 960 GB | 862     | 605   | 1     | 1.43   |
| SPCC      | SSD                | 1 TB   | 2       | 517   | 0     | 1.42   |
| Micron    | MTFDDAK960TCB      | 960 GB | 12      | 642   | 1     | 1.41   |
| Samsung   | MZ7LM240HMHQ-00003 | 240 GB | 2       | 513   | 0     | 1.41   |
| Patriot   | P200               | 2 TB   | 5       | 510   | 0     | 1.40   |
| SanDisk   | SDSSDA480G         | 480 GB | 2       | 509   | 0     | 1.40   |
| HP        | VK0480GFDKH        | 480 GB | 6       | 509   | 0     | 1.40   |
| Micron    | 5300_MTFDDAK960TDS | 960 GB | 156     | 522   | 1     | 1.39   |
| Crucial   | CT250BX100SSD1     | 250 GB | 1       | 507   | 0     | 1.39   |
| Intel     | SSDSC2BB800H4      | 800 GB | 6       | 504   | 0     | 1.38   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 34      | 513   | 1     | 1.38   |
| Seagate   | ST120FN0021        | 120 GB | 1       | 502   | 0     | 1.38   |
| Samsung   | MZ7KH480HAHQ0D3    | 480 GB | 17      | 499   | 0     | 1.37   |
| Micron    | 5100_MTFDDAK1T9TCC | 1.9 TB | 17      | 565   | 1     | 1.37   |
| Samsung   | SSD 883 DCT 3.84TB | 3.8 TB | 155     | 498   | 0     | 1.36   |
| Zheino    | CHN 25SATAS3 512   | 512 GB | 1       | 497   | 0     | 1.36   |
| Toshiba   | THNSF8200CAME      | 200 GB | 3       | 497   | 0     | 1.36   |
| OCZ       | D2RSTK251E14-0400  | 400 GB | 2       | 495   | 0     | 1.36   |
| HP        | SSD S700           | 500 GB | 7       | 547   | 1     | 1.35   |
| HPE       | MK000960GXAXB      | 960 GB | 5       | 490   | 0     | 1.34   |
| Micron    | MTFDDAK480TDS-1... | 480 GB | 9       | 546   | 113   | 1.33   |
| Seagate   | XA480LE10063       | 480 GB | 14      | 486   | 0     | 1.33   |
| Micron    | MTFDDAV240TCB      | 240 GB | 13      | 496   | 1     | 1.33   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 116     | 566   | 4     | 1.31   |
| Patriot   | Burst              | 120 GB | 1       | 476   | 0     | 1.30   |
| Micron    | 5300_MTFDDAK1T9TDT | 1.9 TB | 109     | 505   | 1     | 1.30   |
| Samsung   | MZ7LH480HAHQ0D3    | 480 GB | 2       | 475   | 0     | 1.30   |
| Samsung   | SSD 850            | 120 GB | 2       | 474   | 0     | 1.30   |
| Samsung   | MZ7LH1T9HMLT-00005 | 1.9 TB | 658     | 473   | 0     | 1.30   |
| Patriot   | Burst              | 480 GB | 2       | 472   | 0     | 1.30   |
| Intel     | SSDSA2BW120G3      | 120 GB | 1       | 2358  | 4     | 1.29   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 6       | 647   | 9     | 1.28   |
| Goodram   | SSDPR-CX400-256    | 256 GB | 1       | 465   | 0     | 1.28   |
| Samsung   | SSD 860 QVO        | 4 TB   | 6       | 464   | 0     | 1.27   |
| Samsung   | MZ7LH1T9HALT0D3    | 1.9 TB | 37      | 463   | 0     | 1.27   |
| HPE       | LK0480GFJSK        | 480 GB | 3       | 461   | 0     | 1.26   |
| Micron    | 1100 SATA          | 256 GB | 1       | 459   | 0     | 1.26   |
| SK hynix  | SC300 M.2 2280     | 256 GB | 1       | 459   | 0     | 1.26   |
| Micron    | 5100_MTFDDAK1T9TCB | 1.9 TB | 3       | 1471  | 694   | 1.26   |
| Samsung   | MZ7LH7T6HMLA-00005 | 7.6 TB | 125     | 458   | 0     | 1.26   |
| Micron    | 1100_MTFDDAK1T0TBN | 1 TB   | 6       | 1338  | 147   | 1.25   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 4       | 456   | 0     | 1.25   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 16      | 487   | 1     | 1.25   |
| Samsung   | MZ7KH480HAHQ-00005 | 480 GB | 83      | 450   | 0     | 1.24   |
| Corsair   | Force LS SSD       | 64 GB  | 2       | 450   | 0     | 1.23   |
| Kingston  | SA400S37480G       | 480 GB | 34      | 707   | 12    | 1.23   |
| Seagate   | XA960LE10063       | 960 GB | 110     | 447   | 0     | 1.22   |
| China     | SATA SSD           | 480 GB | 6       | 445   | 0     | 1.22   |
| Samsung   | MZ7KH960HAJR0D3    | 960 GB | 161     | 440   | 0     | 1.21   |
| WDC       | WDS100T2G0A-00JH30 | 1 TB   | 1       | 440   | 0     | 1.21   |
| Micron    | 5100_MTFDDAV240TCB | 240 GB | 13      | 591   | 22    | 1.19   |
| WDC       | WDS250G2B0A        | 250 GB | 2       | 433   | 0     | 1.19   |
| HP        | VK000480GWCNQ      | 480 GB | 1       | 433   | 0     | 1.19   |
| Crucial   | CT1000BX100SSD1    | 1 TB   | 1       | 432   | 0     | 1.19   |
| Micron    | 1300_MTFDDAK1T0TDL | 1 TB   | 10      | 483   | 1     | 1.18   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 296     | 554   | 8     | 1.17   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 9       | 427   | 0     | 1.17   |
| Intel     | SSDSC2KB480G8R     | 480 GB | 18      | 436   | 1     | 1.17   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 21      | 471   | 1     | 1.17   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 3       | 425   | 0     | 1.17   |
| Intel     | SSDSC2KG019T8      | 1.9 TB | 224     | 499   | 1     | 1.16   |
| HP        | SSD S700           | 250 GB | 6       | 423   | 0     | 1.16   |
| THU       | SSD 240G           | 240 GB | 1       | 422   | 0     | 1.16   |
| PNY       | CS900 240GB SSD    | 240 GB | 1       | 418   | 0     | 1.15   |
| Maxtor    | Z1 SSD             | 240 GB | 1       | 418   | 0     | 1.15   |
| Kingston  | SEDC500R960G       | 960 GB | 1       | 418   | 0     | 1.15   |
| Intel     | SSDSC2KB480G7R     | 480 GB | 6       | 418   | 0     | 1.15   |
| Samsung   | MZ7LH480HAHQ-00005 | 480 GB | 76      | 418   | 0     | 1.15   |
| OCZ       | TRION100           | 120 GB | 1       | 417   | 0     | 1.14   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 433     | 417   | 0     | 1.14   |
| SanDisk   | SD6SB1M128G1022I   | 128 GB | 1       | 416   | 0     | 1.14   |
| Intel     | SSDSC2KG960G8      | 960 GB | 198     | 463   | 1     | 1.14   |
| Samsung   | SSD 883 DCT        | 480 GB | 7       | 414   | 0     | 1.13   |
| Samsung   | MZ7LH960HAJR-00005 | 960 GB | 1112    | 412   | 0     | 1.13   |
| Gigabyte  | GP-GSTFS30512GTTD  | 512 GB | 2       | 410   | 0     | 1.13   |
| KingDian  | S280               | 240 GB | 3       | 476   | 1     | 1.12   |
| SanDisk   | SSD G5 BICS4       | 1 TB   | 5       | 448   | 1     | 1.11   |
| Patriot   | Burst              | 960 GB | 3       | 403   | 0     | 1.10   |
| Micron    | 5100_MTFDDAK960TCC | 960 GB | 9       | 493   | 1     | 1.10   |
| SPCC      | SSD                | 512 GB | 6       | 402   | 0     | 1.10   |
| WDC       | WDS240G2G0B-00EPW0 | 240 GB | 1       | 402   | 0     | 1.10   |
| Intel     | SSDSC2KB019T7R     | 1.9 TB | 23      | 551   | 2     | 1.10   |
| SanDisk   | SSD PLUS           | 480 GB | 24      | 574   | 6     | 1.10   |
| Dell      | SSDSCKKB240G8R     | 240 GB | 13      | 397   | 0     | 1.09   |
| Kingston  | SUV500960G         | 960 GB | 8       | 394   | 0     | 1.08   |
| SPCC      | SSD                | 256 GB | 3       | 392   | 0     | 1.08   |
| Corsair   | Neutron SSD        | 128 GB | 1       | 1955  | 4     | 1.07   |
| WDC       | WDS400T2B0A-00SM50 | 4 TB   | 4       | 606   | 1     | 1.07   |
| Intel     | SSDSC2KG480G8      | 480 GB | 276     | 433   | 1     | 1.06   |
| Seagate   | BarraCuda 120 S... | 1 TB   | 3       | 387   | 0     | 1.06   |
| Lite-On   | L8H-128V2G-HP      | 128 GB | 2       | 385   | 0     | 1.06   |
| Micron    | MTFDDAK480TDS      | 480 GB | 8       | 384   | 0     | 1.05   |
| Samsung   | SSD 883 DCT        | 240 GB | 42      | 382   | 0     | 1.05   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 3       | 382   | 0     | 1.05   |
| Samsung   | SSD 870 QVO        | 2 TB   | 6       | 382   | 0     | 1.05   |
| Intel     | SSDSC2BW240H6      | 240 GB | 14      | 610   | 25    | 1.04   |
| Intel     | SSDSC2KB960G8R     | 960 GB | 7       | 375   | 0     | 1.03   |
| SK hynix  | HFS250G32TND-N1A2A | 250 GB | 10      | 374   | 0     | 1.03   |
| Crucial   | CT960BX500SSD1     | 960 GB | 8       | 373   | 0     | 1.02   |
| Intel     | SSDSC2BW480H6      | 480 GB | 5       | 639   | 4     | 1.02   |
| Samsung   | SSD 870 QVO        | 8 TB   | 35      | 372   | 0     | 1.02   |
| Kingston  | SA400S37960G       | 960 GB | 8       | 364   | 0     | 1.00   |
| ORTIAL    | SSD                | 1 TB   | 12      | 455   | 2     | 1.00   |
| Seagate   | XA240ME10003       | 240 GB | 5       | 361   | 0     | 0.99   |
| Samsung   | MZ7WD480HMHP-00003 | 480 GB | 8       | 1956  | 66    | 0.96   |
| China     | 512GB QLC SATA SSD | 512 GB | 6       | 350   | 0     | 0.96   |
| HPE       | VR000480GWFMD      | 480 GB | 1       | 349   | 0     | 0.96   |
| Apacer    | AS340              | 480 GB | 1       | 348   | 0     | 0.96   |
| Kingston  | SEDC500R480G       | 480 GB | 11      | 343   | 0     | 0.94   |
| Kingston  | SVP200S3120G       | 120 GB | 1       | 341   | 0     | 0.94   |
| Samsung   | SSD 860 PRO        | 512 GB | 66      | 337   | 0     | 0.92   |
| Toshiba   | THNSFJ256GDNU      | 256 GB | 1       | 337   | 0     | 0.92   |
| Intel     | SSDSC2KG019T7      | 1.9 TB | 1       | 335   | 0     | 0.92   |
| Micron    | MTFDDAK960TDT      | 960 GB | 8       | 334   | 0     | 0.92   |
| HPE       | MK000480GWXFF      | 480 GB | 19      | 333   | 0     | 0.91   |
| BIWIN     | SSD                | 256 GB | 1       | 332   | 0     | 0.91   |
| HPE       | MK001920GWJPQ      | 1.9 TB | 18      | 640   | 7     | 0.91   |
| Kingston  | SEDC500M1920G      | 1.9 TB | 44      | 363   | 1     | 0.90   |
| Samsung   | SSD 860 EVO M.2    | 250 GB | 1       | 328   | 0     | 0.90   |
| SanDisk   | SD8SN8U256G1002    | 256 GB | 1       | 327   | 0     | 0.90   |
| Patriot   | Burst              | 240 GB | 10      | 327   | 0     | 0.90   |
| Crucial   | CT500MX500SSD1     | 500 GB | 158     | 391   | 3     | 0.89   |
| Samsung   | MZ7LM960HMJP-00003 | 960 GB | 2       | 614   | 12    | 0.88   |
| SanDisk   | SSD PLUS           | 240 GB | 19      | 335   | 1     | 0.88   |
| SanDisk   | SDSSDA120G         | 120 GB | 3       | 317   | 0     | 0.87   |
| ADATA     | SP580              | 120 GB | 2       | 1178  | 506   | 0.86   |
| SanDisk   | pSSD               | 32 GB  | 1       | 314   | 0     | 0.86   |
| ADATA     | SP550              | 120 GB | 3       | 497   | 166   | 0.86   |
| Toshiba   | KHK61RSE960G       | 960 GB | 67      | 312   | 0     | 0.86   |
| Mushkin   | MKNSSDRE960GB      | 960 GB | 5       | 514   | 2     | 0.85   |
| Micron    | 5300_MTFDDAV240TDS | 240 GB | 8       | 309   | 0     | 0.85   |
| Mushkin   | MKNSSDRE500GB      | 500 GB | 1       | 308   | 0     | 0.84   |
| China     | SATA SSD           | 240 GB | 6       | 305   | 0     | 0.84   |
| Micron    | MTFDDAV240TDU      | 240 GB | 6       | 303   | 0     | 0.83   |
| ADATA     | SP550              | 240 GB | 2       | 301   | 0     | 0.83   |
| HP        | VK000960GWTTB      | 960 GB | 11      | 300   | 0     | 0.82   |
| SK hynix  | SHGS31-1000GS-2    | 1 TB   | 23      | 299   | 0     | 0.82   |
| Transcend | TS128GSSD370       | 128 GB | 3       | 299   | 0     | 0.82   |
| Kingston  | SQ500S37480G       | 480 GB | 1       | 297   | 0     | 0.81   |
| Toshiba   | KHK61RSE1T92       | 1.9 TB | 33      | 295   | 0     | 0.81   |
| Samsung   | SSD 870 EVO        | 250 GB | 2       | 292   | 0     | 0.80   |
| Crucial   | CT2000MX500SSD1    | 2 TB   | 144     | 366   | 7     | 0.79   |
| Crucial   | CT240M500SSD1      | 240 GB | 11      | 2033  | 259   | 0.79   |
| Micron    | 5100_MTFDDAK480TCB | 480 GB | 28      | 1077  | 179   | 0.79   |
| Intel     | SSDSC2KG960G8R     | 960 GB | 17      | 352   | 2     | 0.77   |
| KingSpec  | MT-128             | 128 GB | 1       | 281   | 0     | 0.77   |
| China     | SH00R480GB         | 480 GB | 2       | 510   | 4     | 0.77   |
| Kingston  | SEDC500R1920G      | 1.9 TB | 49      | 378   | 1     | 0.77   |
| Micron    | MTFDDAK960TDS      | 960 GB | 16      | 290   | 1     | 0.77   |
| Samsung   | SSD 860 DCT        | 960 GB | 2       | 277   | 0     | 0.76   |
| Micron    | 5300_MTFDDAK960TDT | 960 GB | 36      | 283   | 1     | 0.76   |
| Intel     | SSDSC2BW120A3F     | 120 GB | 20      | 2125  | 917   | 0.75   |
| Micron    | 5300_MTFDDAK480TDT | 480 GB | 4       | 270   | 0     | 0.74   |
| Intel     | SSDSC2BW256H6      | 256 GB | 1       | 268   | 0     | 0.74   |
| Crucial   | CT240BX500SSD1     | 240 GB | 44      | 267   | 0     | 0.73   |
| Intel     | SSDSC2BW080A4      | 80 GB  | 1       | 1589  | 5     | 0.73   |
| HPE       | VR000240GXBBL      | 240 GB | 2       | 264   | 0     | 0.72   |
| Mushkin   | MKNSSDSR500GB      | 500 GB | 8       | 262   | 0     | 0.72   |
| WDC       | WDS200T1R0A-68A4W0 | 2 TB   | 22      | 261   | 0     | 0.72   |
| Samsung   | MZNLH1T0HALB-00000 | 1 TB   | 12      | 261   | 0     | 0.72   |
| Crucial   | CT250MX500SSD1     | 250 GB | 62      | 275   | 1     | 0.70   |
| Toshiba   | THNSF81D60CSE      | 1.6 TB | 10      | 253   | 0     | 0.69   |
| SanDisk   | SDSSDH3 2T00       | 2 TB   | 8       | 273   | 1     | 0.69   |
| Samsung   | MZ7LH480HBHQ0D3    | 480 GB | 19      | 251   | 0     | 0.69   |
| Micron    | MTFDDAK960TDD      | 960 GB | 14      | 251   | 0     | 0.69   |
| Samsung   | MZ7LH3T8HMLT0D3    | 3.8 TB | 40      | 251   | 0     | 0.69   |
| Micron    | MTFDDAK1T9TDD      | 1.9 TB | 3       | 250   | 0     | 0.69   |
| Kingston  | SHFS37A240G        | 240 GB | 1       | 248   | 0     | 0.68   |
| PNY       | CS900 250GB SSD    | 250 GB | 10      | 247   | 0     | 0.68   |
| SanDisk   | SSD PLUS           | 120 GB | 24      | 268   | 1     | 0.68   |
| WDC       | WDS100T1R0A-68A4W0 | 1 TB   | 3       | 244   | 0     | 0.67   |
| Intel     | SSDSC2CT060A3      | 64 GB  | 1       | 969   | 3     | 0.66   |
| Intel     | SSDSC2KG038T8      | 3.8 TB | 10      | 359   | 2     | 0.66   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 3       | 239   | 0     | 0.66   |
| KingSpec  | P4-960             | 960 GB | 2       | 239   | 0     | 0.66   |
| Micron    | MTFDDAK960TDS-1... | 960 GB | 2       | 238   | 0     | 0.65   |
| Gigabyte  | GP-GSTFS31480GNTD  | 480 GB | 1       | 238   | 0     | 0.65   |
| Intel     | SSDSC2KW128G8      | 128 GB | 10      | 249   | 1     | 0.65   |
| ADATA     | SU750              | 512 GB | 4       | 235   | 0     | 0.65   |
| ADATA     | SU630              | 960 GB | 1       | 705   | 2     | 0.64   |
| Kingston  | SEDC500M480G       | 480 GB | 17      | 258   | 1     | 0.64   |
| Samsung   | MZ7LH3T8HMLT-00005 | 3.8 TB | 94      | 232   | 0     | 0.64   |
| Apacer    | AS340              | 960 GB | 43      | 356   | 21    | 0.63   |
| China     | SATA SSD           | 960 GB | 4       | 230   | 0     | 0.63   |
| Phison    | SATA SSD           | 960 GB | 4       | 230   | 0     | 0.63   |
| Intel     | SSDSC2KG019T8R     | 1.9 TB | 31      | 236   | 1     | 0.63   |
| China     | SATA SSD           | 64 GB  | 9       | 229   | 0     | 0.63   |
| Team      | T253X1480G         | 480 GB | 1       | 229   | 0     | 0.63   |
| Transcend | TS480GSSD220S      | 480 GB | 4       | 320   | 2     | 0.63   |
| Transcend | TSMSSSD01-120GP    | 120 GB | 2       | 227   | 0     | 0.62   |
| ADATA     | SU720              | 2 TB   | 2       | 225   | 0     | 0.62   |
| SanDisk   | SSD PLUS           | 1 TB   | 1       | 443   | 1     | 0.61   |
| Micron    | 5210_MTFDDAK3T8QDE | 3.8 TB | 82      | 230   | 3     | 0.60   |
| SanDisk   | SDSA5GK-016G-1006  | 16 GB  | 1       | 219   | 0     | 0.60   |
| Micron    | MTFDDAK256MAM-1K1  | 256 GB | 1       | 219   | 0     | 0.60   |
| Phison    | SATA SSD           | 64 GB  | 9       | 218   | 0     | 0.60   |
| China     | SATA SSD           | 256 GB | 4       | 214   | 0     | 0.59   |
| Micron    | MTFDDAK480TDT      | 480 GB | 10      | 214   | 0     | 0.59   |
| Micron    | 5300_MTFDDAK480TDS | 480 GB | 22      | 213   | 0     | 0.58   |
| Samsung   | MZ7LM960HCHP-000MV | 960 GB | 6       | 210   | 0     | 0.58   |
| Crucial   | CT120BX100SSD1     | 120 GB | 1       | 209   | 0     | 0.57   |
| HPE       | MK001920GWSSE      | 1.9 TB | 8       | 209   | 0     | 0.57   |
| Kingston  | SEDC450R480G       | 480 GB | 1       | 208   | 0     | 0.57   |
| Maxtor    | Z1 SSD             | 960 GB | 2       | 203   | 0     | 0.56   |
| Samsung   | MZ7KM120HAFD-000FU | 120 GB | 1       | 195   | 0     | 0.54   |
| Crucial   | CT1000MX500SSD1    | 1 TB   | 451     | 223   | 3     | 0.53   |
| SanDisk   | SDSSDH3 250G       | 250 GB | 1       | 193   | 0     | 0.53   |
| Micron    | 5300_MTFDDAK7T6TDS | 7.6 TB | 21      | 193   | 0     | 0.53   |
| SATADOM   | SH Type D 3TE7     | 120 GB | 6       | 189   | 0     | 0.52   |
| Intel     | SSDSC2BF180A4      | 180 GB | 2       | 314   | 2     | 0.52   |
| Gigabyte  | GP-GSTFS31120GNTD  | 120 GB | 10      | 189   | 0     | 0.52   |
| Lite-On   | CV8-CE512-11 SATA  | 512 GB | 1       | 189   | 0     | 0.52   |
| WDC       | WDS400T1R0A-68A4W0 | 4 TB   | 6       | 189   | 0     | 0.52   |
| HP        | VK000480GWTTA      | 480 GB | 6       | 188   | 0     | 0.52   |
| Kingston  | SA400S37240G       | 240 GB | 124     | 187   | 5     | 0.51   |
| Samsung   | MZ7WD960HMHP-00003 | 960 GB | 4       | 2284  | 44    | 0.50   |
| Crucial   | CT960BX200SSD1     | 960 GB | 1       | 181   | 0     | 0.50   |
| Gigabyte  | GP-GSTFS31240GNTD  | 240 GB | 1       | 181   | 0     | 0.50   |
| Crucial   | CT1000BX500SSD1    | 1 TB   | 31      | 206   | 1     | 0.49   |
| Intel     | SSDSCKKI256G8      | 256 GB | 1       | 173   | 0     | 0.47   |
| HP        | VK000960GWTHB      | 960 GB | 3       | 172   | 0     | 0.47   |
| ADATA     | SU800              | 256 GB | 1       | 172   | 0     | 0.47   |
| Samsung   | SSD 870 QVO        | 1 TB   | 18      | 170   | 0     | 0.47   |
| Team      | T253X6001T         | 1 TB   | 4       | 163   | 0     | 0.45   |
| Micron    | 5300_MTFDDAK3T8TDS | 3.8 TB | 48      | 193   | 1     | 0.45   |
| Phison    | SATA SSD           | 32 GB  | 1       | 161   | 0     | 0.44   |
| Intel     | SSDSC2KB038T8      | 3.8 TB | 68      | 188   | 1     | 0.44   |
| Apacer    | 480GB SATA Flas... | 480 GB | 3       | 157   | 0     | 0.43   |
| Samsung   | SSD 750 EVO        | 500 GB | 1       | 157   | 0     | 0.43   |
| Intenso   | SSD                | 128 GB | 2       | 156   | 0     | 0.43   |
| Synology  | SAT5200-480G       | 480 GB | 12      | 154   | 0     | 0.42   |
| Patriot   | P210               | 1 TB   | 4       | 151   | 0     | 0.42   |
| Intel     | SSDSC2BA400G3I ... | 400 GB | 2       | 150   | 0     | 0.41   |
| HPE       | MK001920GWTTL      | 1.9 TB | 1       | 148   | 0     | 0.41   |
| WDC       | WDS250G2B0B-00YS70 | 250 GB | 1       | 147   | 0     | 0.40   |
| ADATA     | SU630 1.9TB        | 1.9 TB | 2       | 147   | 0     | 0.40   |
| ADATA     | SU800              | 2 TB   | 4       | 250   | 1     | 0.40   |
| ADATA     | SU650              | 120 GB | 4       | 146   | 0     | 0.40   |
| China     | SATA SSD           | 1 TB   | 21      | 145   | 0     | 0.40   |
| Intel     | SSDSA2M080G2GC     | 80 GB  | 2       | 1656  | 9     | 0.40   |
| Intel     | SSDSC2KB240GZ      | 240 GB | 6       | 144   | 0     | 0.39   |
| China     | SATA SSD           | 16 GB  | 1       | 144   | 0     | 0.39   |
| Intel     | SSDSC2BB480G7K     | 480 GB | 1       | 141   | 0     | 0.39   |
| Kingston  | SEDC500R3840G      | 3.8 TB | 42      | 174   | 1     | 0.39   |
| WDC       | WDS250G2B0B        | 250 GB | 2       | 141   | 0     | 0.39   |
| WDC       | WDS500G1R0A-68A4W0 | 500 GB | 4       | 140   | 0     | 0.38   |
| Crucial   | CT250MX500SSD4     | 250 GB | 4       | 138   | 0     | 0.38   |
| Micron    | 1300_MTFDDAK512TDL | 512 GB | 116     | 138   | 0     | 0.38   |
| Kingston  | SKC6001024G        | 1 TB   | 2       | 136   | 0     | 0.37   |
| HP        | VK0480GEPQP        | 480 GB | 4       | 135   | 0     | 0.37   |
| Crucial   | CT240BX200SSD1     | 240 GB | 1       | 133   | 0     | 0.37   |
| HP        | VK001920GWJPH      | 1.9 TB | 4       | 245   | 8     | 0.36   |
| Intel     | SSDSC2BF240A4H     | 240 GB | 1       | 659   | 4     | 0.36   |
| Crucial   | CT480BX500SSD1     | 480 GB | 34      | 131   | 0     | 0.36   |
| Micron    | 5300_MTFDDAK1T9TDS | 1.9 TB | 105     | 126   | 0     | 0.35   |
| Intel     | SSDSA2CT040G3      | 40 GB  | 1       | 125   | 0     | 0.34   |
| Micron    | 5300_MTFDDAK3T8TDT | 3.8 TB | 55      | 145   | 3     | 0.34   |
| Intel     | SSDSC2KW256G8      | 256 GB | 24      | 149   | 6     | 0.34   |
| Intel     | SSDSC2KW512G8      | 512 GB | 6       | 152   | 3     | 0.33   |
| Innodisk  | DEMSR-64GM41BC1... | 64 GB  | 1       | 601   | 4     | 0.33   |
| Samsung   | MZ7LN1T0HAJQ-00000 | 1 TB   | 2       | 119   | 0     | 0.33   |
| China     | SATA SSD           | 32 GB  | 2       | 118   | 0     | 0.33   |
| Kingston  | SEDC500M3840G      | 3.8 TB | 13      | 168   | 1     | 0.32   |
| Crucial   | CT1024M550SSD1     | 1 TB   | 5       | 2458  | 188   | 0.32   |
| Intel     | SSDSCKKW128G8      | 128 GB | 3       | 112   | 0     | 0.31   |
| Samsung   | SSD 870 EVO        | 1 TB   | 82      | 136   | 2     | 0.31   |
| Netac     | SSD                | 64 GB  | 1       | 111   | 0     | 0.31   |
| Kingston  | SUV500M8240G       | 240 GB | 3       | 108   | 0     | 0.30   |
| SanDisk   | SDSSDX480GG25      | 480 GB | 1       | 2911  | 26    | 0.30   |
| Seagate   | XA240LE10003       | 240 GB | 10      | 103   | 0     | 0.28   |
| Intel     | SSDSCKKB960G8      | 960 GB | 3       | 131   | 2     | 0.27   |
| HPE       | MK000960GWSSD      | 960 GB | 40      | 98    | 0     | 0.27   |
| Kingston  | SUV500M8120G       | 120 GB | 1       | 97    | 0     | 0.27   |
| Kingston  | SKC6002048G        | 2 TB   | 1       | 190   | 1     | 0.26   |
| SK hynix  | SC311 SATA         | 256 GB | 2       | 95    | 0     | 0.26   |
| KIOXIA... | SATA SSD           | 240 GB | 8       | 90    | 0     | 0.25   |
| SATADOM   | SL 3TE7            | 120 GB | 6       | 88    | 0     | 0.24   |
| Team      | T253A3001T         | 1 TB   | 31      | 88    | 0     | 0.24   |
| SanDisk   | SD8SB8U128G1122    | 128 GB | 1       | 261   | 2     | 0.24   |
| WDC       | WDS100T2B0B-00YS70 | 1 TB   | 1       | 84    | 0     | 0.23   |
| Samsung   | SSD 870 EVO        | 2 TB   | 63      | 110   | 3     | 0.23   |
| Micron    | MTFDDAV256TDL      | 256 GB | 5       | 143   | 2     | 0.23   |
| SanDisk   | SDSSDH3512G        | 512 GB | 2       | 82    | 0     | 0.23   |
| Seagate   | BarraCuda 120 S... | 250 GB | 1       | 81    | 0     | 0.22   |
| Micron    | MTFDDAK1T0TDL      | 1 TB   | 25      | 82    | 1     | 0.22   |
| Samsung   | SSD 870 EVO        | 500 GB | 15      | 119   | 10    | 0.22   |
| SanDisk   | SDSSDP064G         | 64 GB  | 1       | 2694  | 33    | 0.22   |
| Patriot   | P210               | 2 TB   | 2       | 79    | 0     | 0.22   |
| ADATA     | SU800              | 1 TB   | 2       | 74    | 0     | 0.21   |
| Transcend | TS1TSSD370S        | 1 TB   | 1       | 296   | 3     | 0.20   |
| Phison    | SATA SSD           | 1 TB   | 6       | 72    | 0     | 0.20   |
| Kingston  | SEDC450R1920G      | 1.9 TB | 10      | 72    | 0     | 0.20   |
| Intenso   | AP-SSD-A1-256      | 256 GB | 1       | 71    | 0     | 0.20   |
| Smartbuy  | SSD                | 960 GB | 1       | 70    | 0     | 0.19   |
| HPE       | MK000480GWUGF      | 480 GB | 2       | 69    | 0     | 0.19   |
| ADATA     | SU800              | 512 GB | 1       | 342   | 4     | 0.19   |
| Micron    | C400-MTFDDAC512MAM | 512 GB | 4       | 689   | 802   | 0.18   |
| SanDisk   | SD7UB3Q256G1122    | 256 GB | 1       | 700   | 10    | 0.17   |
| Transcend | TS128GSSD370S      | 128 GB | 8       | 63    | 0     | 0.17   |
| V-GeN     | V-GEN12SM20AR10... | 1 TB   | 1       | 190   | 2     | 0.17   |
| Micron    | MTFDDAK512TBN      | 512 GB | 3       | 58    | 0     | 0.16   |
| Samsung   | MZ7LH1T9HMLT0D3    | 1.9 TB | 15      | 57    | 0     | 0.16   |
| Transcend | TS2TSSD230S        | 2 TB   | 2       | 56    | 0     | 0.16   |
| Seagate   | BarraCuda 120 S... | 500 GB | 2       | 56    | 0     | 0.16   |
| Samsung   | MZ7L3240HCHQ-00A07 | 240 GB | 1       | 56    | 0     | 0.15   |
| Samsung   | MZ7L33T8HBNA-00... | 3.8 TB | 5       | 56    | 0     | 0.15   |
| Samsung   | SSD 870 EVO        | 4 TB   | 11      | 82    | 7     | 0.15   |
| Crucial   | CT120M500SSD1      | 120 GB | 2       | 2010  | 523   | 0.14   |
| SPCC      | SSD                | 128 GB | 1       | 50    | 0     | 0.14   |
| Samsung   | MZ7L31T9HBLT-00... | 1.9 TB | 3       | 49    | 0     | 0.14   |
| SATADOM   | ML 3MG2-P          | 248 GB | 1       | 47    | 0     | 0.13   |
| SPCC      | SSD                | 480 GB | 2       | 408   | 60    | 0.13   |
| Intel     | SSDSC2BF240A4L     | 240 GB | 1       | 803   | 16    | 0.13   |
| Crucial   | CT512M550SSD1      | 512 GB | 2       | 835   | 17    | 0.13   |
| PNY       | CS900 1TB SSD      | 1 TB   | 2       | 45    | 0     | 0.12   |
| China     | OSSD120GBTSS2      | 120 GB | 1       | 843   | 18    | 0.12   |
| SPCC      | SSD                | 2 TB   | 1       | 43    | 0     | 0.12   |
| China     | SATA SSD           | 120 GB | 3       | 40    | 0     | 0.11   |
| Kingston  | SEDC450R3840G      | 3.8 TB | 4       | 40    | 0     | 0.11   |
| ADATA     | SX900              | 128 GB | 4       | 397   | 766   | 0.11   |
| HP        | VK001920GXCGP      | 1.9 TB | 12      | 38    | 0     | 0.11   |
| Transcend | TS256GMTS800S      | 256 GB | 7       | 38    | 0     | 0.10   |
| Intel     | SSDSC2KG076T8      | 7.6 TB | 1       | 37    | 0     | 0.10   |
| QUMO      | SSD                | 64 GB  | 2       | 47    | 608   | 0.10   |
| KingFast  | SSD                | 512 GB | 1       | 447   | 11    | 0.10   |
| Intel     | SSDSC2KB019TZ      | 1.9 TB | 2       | 36    | 0     | 0.10   |
| Crucial   | CT2000BX500SSD1    | 2 TB   | 12      | 34    | 0     | 0.09   |
| Samsung   | MZ7L33T8HBLT-00... | 3.8 TB | 1       | 33    | 0     | 0.09   |
| ADATA     | SU630              | 240 GB | 3       | 32    | 0     | 0.09   |
| Intel     | SSDSC2BW480A4      | 480 GB | 3       | 667   | 28    | 0.09   |
| Kingston  | SKC600256G         | 256 GB | 27      | 32    | 0     | 0.09   |
| Transcend | TS1TSSD230S        | 1 TB   | 1       | 28    | 0     | 0.08   |
| HPE       | LK1600GEYMV        | 1.6 TB | 1       | 28    | 0     | 0.08   |
| Intel     | SSDSC2KI128G8      | 128 GB | 1       | 56    | 1     | 0.08   |
| Kingston  | SKC300S37A480G     | 480 GB | 1       | 27    | 0     | 0.08   |
| Transcend | TS128GMTS800S      | 128 GB | 5       | 18    | 0     | 0.05   |
| Intel     | SSDSC2KB019T8R     | 1.9 TB | 2       | 16    | 0     | 0.05   |
| HP        | VK000240GWEZB      | 240 GB | 8       | 15    | 0     | 0.04   |
| SanDisk   | SD8SB8U-128G-1006  | 128 GB | 1       | 14    | 0     | 0.04   |
| SanDisk   | SSD PLUS           | 2 TB   | 1       | 12    | 0     | 0.04   |
| WDC       | WDS500G1R0B-68A4Z0 | 500 GB | 3       | 12    | 0     | 0.03   |
| SATADOM   | SV 3ME3            | 64 GB  | 4       | 10    | 0     | 0.03   |
| Micron    | 5300_MTFDDAK240TDT | 240 GB | 7       | 7     | 0     | 0.02   |
| Palit     | PH120 SSD          | 120 GB | 2       | 6     | 0     | 0.02   |
| Intel     | SSDSC2KW120H6      | 120 GB | 1       | 6     | 0     | 0.02   |
| Intel     | SSDSC2KW240H6      | 240 GB | 1       | 209   | 30    | 0.02   |
| Crucial   | CT4000MX500SSD1    | 4 TB   | 4       | 6     | 0     | 0.02   |
| Patriot   | Burst Elite        | 240 GB | 1       | 6     | 0     | 0.02   |
| HP        | VK000480GWSXF      | 480 GB | 1       | 5     | 0     | 0.01   |
| SanDisk   | 64G SSD            | 64 GB  | 2       | 5     | 0     | 0.01   |
| Intel     | SSDSC2KF256H6 SATA | 256 GB | 1       | 169   | 42    | 0.01   |
| Crucial   | M4-CT256M4SSD1     | 256 GB | 1       | 3225  | 1011  | 0.01   |
| Lite-On   | CV1-8B128-HP       | 128 GB | 1       | 3     | 0     | 0.01   |
| Kingston  | SHPM2280P2H-480G   | 480 GB | 3       | 1138  | 743   | 0.01   |
| Intel     | SSDSC2BA200G3R     | 200 GB | 26      | 2392  | 1029  | 0.01   |
| Micron    | M500_MTFDDAK960MAV | 960 GB | 1       | 2296  | 1032  | 0.01   |
| Intel     | SSDSC2BG200G4R     | 200 GB | 10      | 2281  | 1029  | 0.01   |
| Intel     | SSDSC2CW060A3      | 64 GB  | 1       | 2105  | 1019  | 0.01   |
| Intel     | SSDSC2BX016T4R     | 1.6 TB | 32      | 2074  | 1029  | 0.01   |
| Avant     | 120GB Client mSATA | 120 GB | 2       | 2045  | 1018  | 0.01   |
| ADATA     | SX900              | 512 GB | 2       | 2028  | 1019  | 0.01   |
| Intel     | SSDSC1BG400G4R     | 400 GB | 16      | 1975  | 1028  | 0.01   |
| Intel     | SSDSC2BA200G3T     | 200 GB | 5       | 1840  | 1028  | 0.00   |
| Intel     | SSDSC1NB080G4R     | 80 GB  | 1       | 1816  | 1028  | 0.00   |
| Intel     | SSDSC2BX200G4R     | 200 GB | 28      | 1800  | 1028  | 0.00   |
| Intel     | SSDSC2BB300G4T     | 304 GB | 55      | 1750  | 1028  | 0.00   |
| Intel     | SSDSC2BW120A3      | 120 GB | 1       | 1687  | 1019  | 0.00   |
| Intel     | SSDSC1BG200G4R     | 200 GB | 33      | 1658  | 1028  | 0.00   |
| Intel     | SSDSC2BB480G6R     | 480 GB | 1       | 1593  | 1028  | 0.00   |
| Intel     | SSDSC2BX400G4R     | 400 GB | 78      | 1491  | 1028  | 0.00   |
| Intel     | SSDSC2BA100G3T     | 100 GB | 3       | 1477  | 1028  | 0.00   |
| Micron    | MTFDDAK3T8TDS-1... | 3.8 TB | 2       | 1     | 0     | 0.00   |
| Intel     | SSDSC2BA800G4R     | 800 GB | 71      | 1337  | 1042  | 0.00   |
| Kingston  | SHPM2280P2H-240G   | 240 GB | 1       | 1297  | 1022  | 0.00   |
| Intel     | SSDSC2BA200G4R     | 200 GB | 13      | 1198  | 1028  | 0.00   |
| Crucial   | CT128MX100SSD1     | 128 GB | 1       | 1045  | 1061  | 0.00   |
| Intel     | SSDSC2KG960G8T     | 960 GB | 1       | 975   | 1026  | 0.00   |
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

| MFG       | Family                 | Models | Samples | Days  | Err   | MTBF |
|-----------|------------------------|--------|---------|-------|-------|------|
| Kingston  | JMicron based SSDs     | 1      | 1       | 3150  | 0     | 8.63   |
| Intel     | X25-E SSDs             | 1      | 3       | 3069  | 0     | 8.41   |
| Apple     | SD/SM/TS E/F/G SSDs    | 1      | 2       | 2543  | 0     | 6.97   |
| OCZ       | Indilinx Barefoot_2... | 1      | 1       | 2437  | 0     | 6.68   |
| Transcend | JMicron/Maxiotek ba... | 1      | 1       | 2277  | 0     | 6.24   |
| Intel     | 320 Series SSDs        | 8      | 49      | 2746  | 44    | 5.95   |
| ADATA     | JMicron/Maxiotek ba... | 1      | 1       | 2142  | 0     | 5.87   |
| Plextor   | M3/M5/M6 Series SSDs   | 1      | 1       | 2039  | 0     | 5.59   |
| Crucial   | RealSSD m4/C400        | 1      | 2       | 2008  | 0     | 5.50   |
| Intel     | 710 Series SSDs        | 1      | 2       | 2530  | 1     | 5.32   |
| Intel     | 330/335 Series SSDs    | 3      | 19      | 2632  | 2     | 4.68   |
| Micron    | RealSSD m4/C400/P400   | 6      | 18      | 1941  | 179   | 4.64   |
| OCZ       | SandForce Driven SSDs  | 4      | 10      | 2588  | 3     | 4.48   |
| Toshiba   | OCZ                    | 1      | 6       | 1579  | 0     | 4.33   |
| Crucial   | RealSSD m4/C400/P400   | 2      | 2       | 3189  | 506   | 4.33   |
| Corsair   | SandForce Driven SSDs  | 2      | 5       | 1510  | 0     | 4.14   |
| ADATA     | SandForce Driven SSDs  | 1      | 2       | 2463  | 2     | 4.05   |
| Intel     | 520 Series SSDs        | 9      | 139     | 2245  | 330   | 4.05   |
| Kingston  | SandForce Driven SSDs  | 19     | 203     | 1544  | 12    | 3.47   |
| Intel     | 3710 Series SSDs       | 1      | 5       | 1236  | 0     | 3.39   |
| SanDisk   | SATA Cloudspeed Max... | 6      | 97      | 1230  | 11    | 3.32   |
| Intel     | Dell Certified Inte... | 3      | 78      | 1368  | 27    | 3.22   |
| Toshiba   | HK4R Series SSD        | 4      | 42      | 1168  | 1     | 3.16   |
| OCZ       | Indilinx Barefoot 3... | 3      | 7       | 1416  | 12    | 3.13   |
| Dell      | Certified Intel S35... | 1      | 5       | 1346  | 1     | 3.10   |
| Intel     | 730 and DC S35x0/36... | 51     | 1123    | 1602  | 265   | 3.10   |
| OCZ       | OCZ/Toshiba Trion SSDs | 2      | 2       | 1125  | 0     | 3.08   |
| Apacer    | Unknown                | 2      | 2       | 1120  | 0     | 3.07   |
| SanDisk   | SanDisk based SSDs     | 5      | 18      | 1469  | 7     | 2.82   |
| Goodram   | Phison Driven OEM SSDs | 1      | 4       | 1006  | 0     | 2.76   |
| OWC       | Unknown                | 1      | 1       | 2002  | 1     | 2.74   |
| MyDigi... | Unknown                | 1      | 6       | 945   | 0     | 2.59   |
| Seagate   | Nytro XF1230 SATA SSD  | 3      | 26      | 862   | 0     | 2.36   |
| Intel     | 510 Series SSDs        | 1      | 2       | 842   | 0     | 2.31   |
| SuperM... | Silicon Motion base... | 4      | 206     | 851   | 7     | 2.29   |
| OWC       | SandForce Driven SSDs  | 1      | 2       | 818   | 0     | 2.24   |
| AMD       | Silicon Motion base... | 1      | 2       | 812   | 0     | 2.23   |
| XPG       | Unknown                | 1      | 2       | 806   | 0     | 2.21   |
| WDC       | Blue and Green SSDs    | 9      | 52      | 797   | 0     | 2.19   |
| Intel     | 525 Series SSDs        | 1      | 1       | 788   | 0     | 2.16   |
| Toshiba   | Unknown                | 12     | 205     | 790   | 1     | 2.12   |
| Crucial   | MX1/2/300, M5/600, ... | 1      | 4       | 1545  | 503   | 2.10   |
| Micron    | BX/MX1/2/3/500, M5/... | 3      | 45      | 1115  | 45    | 2.06   |
| HP        | Unknown                | 30     | 194     | 779   | 1     | 2.04   |
| Samsung   | Samsung based SSDs     | 144    | 7366    | 815   | 10    | 2.03   |
| Toshiba   | OCZ/Toshiba Trion SSDs | 1      | 1       | 1473  | 1     | 2.02   |
| Crucial   | BX/MX1/2/3/500, M5/... | 14     | 250     | 905   | 10    | 1.99   |
| Lite-On   | Unknown                | 5      | 7       | 724   | 0     | 1.98   |
| Intel     | S3520 Series SSDs      | 7      | 292     | 1243  | 3     | 1.90   |
| Toshiba   | HG6 Series SSD         | 2      | 2       | 686   | 0     | 1.88   |
| SanDisk   | SATA CS1K GEN1 ESS ... | 1      | 1       | 670   | 0     | 1.84   |
| Micron    | 5100 Pro / 5200 SSDs   | 16     | 438     | 840   | 6     | 1.82   |
| Crucial   | Silicon Motion base... | 5      | 6       | 664   | 0     | 1.82   |
| Micron    | BX/MX1/2/3/500, M5/... | 10     | 119     | 764   | 25    | 1.76   |
| Goodram   | Phison Driven SSDs     | 4      | 14      | 630   | 0     | 1.73   |
| SanDisk   | Marvell based SanDi... | 20     | 162     | 691   | 2     | 1.72   |
| Plextor   | Unknown                | 2      | 2       | 609   | 0     | 1.67   |
| Plextor   | M3/M5/M6/M7 Series ... | 1      | 2       | 584   | 0     | 1.60   |
| Kingston  | SSDNow UV400           | 2      | 65      | 585   | 1     | 1.55   |
| Goodram   | Unknown                | 1      | 2       | 538   | 0     | 1.47   |
| Micron    | MX1/2/300, M5/600, ... | 3      | 20      | 562   | 1     | 1.47   |
| Innodisk  | 3IE3/3ME3/3ME4 SSDs    | 1      | 1       | 1074  | 1     | 1.47   |
| SATADOM   | Innodisk 3IE3/3ME3/... | 2      | 11      | 533   | 0     | 1.46   |
| Intel     | S4510/S4610/S4500/S... | 22     | 3700    | 635   | 3     | 1.45   |
| Intel     | 53x and Pro 1500/25... | 11     | 126     | 777   | 6     | 1.45   |
| HPE       | Unknown                | 20     | 145     | 564   | 1     | 1.43   |
| Samsung   | Unknown                | 19     | 756     | 532   | 1     | 1.42   |
| Intel     | Dell Certified Inte... | 11     | 156     | 593   | 15    | 1.41   |
| Patriot   | Silicon Motion base... | 1      | 5       | 510   | 0     | 1.40   |
| PNY       | Phison Driven SSDs     | 3      | 4       | 507   | 0     | 1.39   |
| Crucial   | BX/MX1/2/3/500, M5/... | 7      | 323     | 713   | 15    | 1.36   |
| Zheino    | Unknown                | 1      | 1       | 497   | 0     | 1.36   |
| SK hynix  | SATA SSDs              | 7      | 19      | 489   | 0     | 1.34   |
| Seagate   | Nytro SATA SSD         | 8      | 208     | 485   | 0     | 1.33   |
| Micron    | 5100 Pro / 5200 / 5... | 17     | 734     | 595   | 10    | 1.32   |
| WDC       | Blue / Red / Green ... | 14     | 258     | 521   | 2     | 1.29   |
| SanDisk   | SandForce Driven SSDs  | 4      | 8       | 802   | 4     | 1.24   |
| SPCC      | Unknown                | 6      | 12      | 510   | 10    | 1.23   |
| Kingston  | SSDNow UV400/500       | 5      | 17      | 449   | 0     | 1.23   |
| SATADOM   | Unknown                | 6      | 19      | 448   | 0     | 1.23   |
| SPCC      | Phison Driven OEM SSDs | 2      | 5       | 442   | 0     | 1.21   |
| THU       | Unknown                | 1      | 1       | 422   | 0     | 1.16   |
| SanDisk   | Unknown                | 12     | 17      | 453   | 109   | 1.15   |
| Intel     | Unknown                | 18     | 139     | 1682  | 674   | 1.13   |
| Gigabyte  | Unknown                | 1      | 2       | 410   | 0     | 1.13   |
| KingDian  | Silicon Motion base... | 1      | 3       | 476   | 1     | 1.12   |
| Patriot   | Phison Driven SSDs     | 4      | 16      | 403   | 0     | 1.11   |
| Transcend | Unknown                | 3      | 8       | 401   | 0     | 1.10   |
| Dell      | Certified Intel S4x... | 1      | 13      | 397   | 0     | 1.09   |
| Corsair   | Unknown                | 1      | 1       | 1955  | 4     | 1.07   |
| ORTIAL    | Unknown                | 1      | 12      | 455   | 2     | 1.00   |
| Kingston  | Phison Driven SSDs     | 25     | 459     | 392   | 3     | 0.96   |
| WDC       | Unknown                | 3      | 12      | 416   | 1     | 0.94   |
| Seagate   | Unknown                | 5      | 9       | 336   | 0     | 0.92   |
| ADATA     | Silicon Motion base... | 5      | 12      | 403   | 42    | 0.92   |
| BIWIN     | Unknown                | 1      | 1       | 332   | 0     | 0.91   |
| Mushkin   | Unknown                | 3      | 14      | 401   | 1     | 0.90   |
| Micron    | Unknown                | 19     | 518     | 323   | 3     | 0.85   |
| Mushkin   | Silicon Motion base... | 1      | 1       | 308   | 0     | 0.84   |
| SK hynix  | Unknown                | 1      | 23      | 299   | 0     | 0.82   |
| Maxtor    | Unknown                | 2      | 3       | 275   | 0     | 0.75   |
| KingSpec  | Unknown                | 2      | 3       | 253   | 0     | 0.70   |
| Apacer    | AS340 SSDs             | 2      | 44      | 356   | 21    | 0.64   |
| China     | Unknown                | 5      | 16      | 309   | 2     | 0.63   |
| Phison    | Driven OEM SSDs        | 5      | 23      | 226   | 0     | 0.62   |
| China     | Phison Driven OEM SSDs | 7      | 49      | 223   | 0     | 0.61   |
| Crucial   | MX500 SSDs             | 5      | 664     | 258   | 3     | 0.61   |
| Micron    | Client SSDs            | 3      | 43      | 223   | 1     | 0.59   |
| PNY       | Unknown                | 2      | 12      | 213   | 0     | 0.59   |
| Team      | Unknown                | 5      | 41      | 194   | 0     | 0.53   |
| Gigabyte  | Phison Driven SSDs     | 3      | 12      | 192   | 0     | 0.53   |
| Kingston  | Unknown                | 4      | 6       | 964   | 542   | 0.50   |
| Intel     | DC S3110 Series SSDs   | 1      | 1       | 173   | 0     | 0.47   |
| ADATA     | Unknown                | 12     | 28      | 449   | 219   | 0.44   |
| Apacer    | SSDs                   | 1      | 3       | 157   | 0     | 0.43   |
| Crucial   | SiliconMotion based... | 2      | 2       | 157   | 0     | 0.43   |
| Patriot   | Unknown                | 4      | 8       | 156   | 0     | 0.43   |
| Synology  | Unknown                | 1      | 12      | 154   | 0     | 0.42   |
| Intel     | 545s Series SSDs       | 4      | 43      | 170   | 4     | 0.41   |
| Intel     | X18-M/X25-M/X25-V G... | 1      | 2       | 1656  | 9     | 0.40   |
| Intenso   | Unknown                | 2      | 3       | 127   | 0     | 0.35   |
| Innodisk  | Unknown                | 1      | 1       | 601   | 4     | 0.33   |
| Transcend | Silicon Motion base... | 8      | 30      | 133   | 1     | 0.31   |
| Netac     | Unknown                | 1      | 1       | 111   | 0     | 0.31   |
| KIOXIA... | Unknown                | 1      | 8       | 90    | 0     | 0.25   |
| Smartbuy  | Unknown                | 1      | 1       | 70    | 0     | 0.19   |
| V-GeN     | Unknown                | 1      | 1       | 190   | 2     | 0.17   |
| Kingston  | Silicon Motion base... | 3      | 30      | 44    | 1     | 0.11   |
| QUMO      | Unknown                | 1      | 2       | 47    | 608   | 0.10   |
| KingFast  | Unknown                | 1      | 1       | 447   | 11    | 0.10   |
| Crucial   | Client SSDs            | 1      | 12      | 34    | 0     | 0.09   |
| Palit     | Unknown                | 1      | 2       | 6     | 0     | 0.02   |
| Crucial   | Unknown                | 1      | 4       | 6     | 0     | 0.02   |
| Intel     | 540 Series SSDs        | 3      | 3       | 110   | 141   | 0.01   |
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

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| Apple       | 1      | 2       | 2543  | 0     | 6.97   |
| OCZ         | 10     | 20      | 2024  | 6     | 3.98   |
| Corsair     | 3      | 6       | 1585  | 1     | 3.63   |
| MyDigita... | 1      | 6       | 945   | 0     | 2.59   |
| Plextor     | 4      | 5       | 885   | 0     | 2.43   |
| OWC         | 2      | 3       | 1212  | 1     | 2.41   |
| Toshiba     | 20     | 256     | 872   | 1     | 2.34   |
| SuperMicro  | 4      | 206     | 851   | 7     | 2.29   |
| SanDisk     | 48     | 303     | 899   | 11    | 2.26   |
| AMD         | 1      | 2       | 812   | 0     | 2.23   |
| XPG         | 1      | 2       | 806   | 0     | 2.21   |
| HP          | 30     | 194     | 779   | 1     | 2.04   |
| Lite-On     | 5      | 7       | 724   | 0     | 1.98   |
| Samsung     | 163    | 8122    | 789   | 9     | 1.98   |
| Intel       | 157    | 5883    | 947   | 78    | 1.91   |
| Goodram     | 6      | 20      | 696   | 0     | 1.91   |
| Dell        | 2      | 18      | 660   | 1     | 1.65   |
| Kingston    | 59     | 781     | 703   | 9     | 1.64   |
| HPE         | 20     | 145     | 564   | 1     | 1.43   |
| Seagate     | 16     | 243     | 520   | 0     | 1.43   |
| WDC         | 26     | 322     | 562   | 2     | 1.42   |
| Micron      | 77     | 1935    | 604   | 10    | 1.37   |
| Zheino      | 1      | 1       | 497   | 0     | 1.36   |
| SATADOM     | 8      | 30      | 479   | 0     | 1.31   |
| SPCC        | 8      | 17      | 490   | 8     | 1.23   |
| THU         | 1      | 1       | 422   | 0     | 1.16   |
| KingDian    | 1      | 3       | 476   | 1     | 1.12   |
| Crucial     | 39     | 1269    | 512   | 10    | 1.09   |
| SK hynix    | 8      | 42      | 385   | 0     | 1.06   |
| ORTIAL      | 1      | 12      | 455   | 2     | 1.00   |
| Patriot     | 9      | 29      | 353   | 0     | 0.97   |
| BIWIN       | 1      | 1       | 332   | 0     | 0.91   |
| Innodisk    | 2      | 2       | 837   | 3     | 0.90   |
| Mushkin     | 4      | 15      | 395   | 1     | 0.90   |
| ADATA       | 19     | 43      | 569   | 154   | 0.87   |
| PNY         | 5      | 16      | 287   | 0     | 0.79   |
| Maxtor      | 2      | 3       | 275   | 0     | 0.75   |
| Apacer      | 5      | 49      | 375   | 19    | 0.73   |
| KingSpec    | 2      | 3       | 253   | 0     | 0.70   |
| Transcend   | 12     | 39      | 243   | 1     | 0.63   |
| Phison      | 5      | 23      | 226   | 0     | 0.62   |
| China       | 12     | 65      | 244   | 1     | 0.62   |
| Gigabyte    | 4      | 14      | 223   | 0     | 0.61   |
| Team        | 5      | 41      | 194   | 0     | 0.53   |
| Synology    | 1      | 12      | 154   | 0     | 0.42   |
| Intenso     | 2      | 3       | 127   | 0     | 0.35   |
| Netac       | 1      | 1       | 111   | 0     | 0.31   |
| KIOXIA-E... | 1      | 8       | 90    | 0     | 0.25   |
| Smartbuy    | 1      | 1       | 70    | 0     | 0.19   |
| V-GeN       | 1      | 1       | 190   | 2     | 0.17   |
| QUMO        | 1      | 2       | 47    | 608   | 0.10   |
| KingFast    | 1      | 1       | 447   | 11    | 0.10   |
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

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Intel     | SSDPEDME020T4      | 2 TB   | 2       | 1913  | 0     | 5.24   |
| Dell      | Express Flash N... | 800 GB | 1       | 1865  | 0     | 5.11   |
| Intel     | SSDPEDME020T4D ... | 2 TB   | 2       | 1790  | 0     | 4.90   |
| Intel     | SSDPEDME016T4      | 1.6 TB | 1       | 1754  | 0     | 4.81   |
| Intel     | SSDPEDME400G4      | 400 GB | 19      | 1693  | 0     | 4.64   |
| Dell      | Express Flash N... | 3.2 TB | 1       | 1646  | 0     | 4.51   |
| Intel     | SSDPEDMW012T4      | 1.2 TB | 1       | 1576  | 0     | 4.32   |
| Intel     | SSDPEDMD020T4D ... | 2 TB   | 5       | 1486  | 0     | 4.07   |
| Intel     | SSDPE2MX012T4      | 1.2 TB | 4       | 1433  | 0     | 3.93   |
| Intel     | SSDPEDMX400G4      | 400 GB | 10      | 1432  | 0     | 3.93   |
| Intel     | SSDPEDME800G4      | 800 GB | 1       | 1416  | 0     | 3.88   |
| Intel     | SSDPEDMD400G4      | 400 GB | 211     | 1405  | 0     | 3.85   |
| Intel     | SSDPEDME016T4S     | 1.6 TB | 8       | 1404  | 0     | 3.85   |
| Intel     | SSDPE2KE016T7      | 1.6 TB | 2       | 1402  | 0     | 3.84   |
| Intel     | SSDPEDMD016T4      | 1.6 TB | 17      | 1400  | 0     | 3.84   |
| Samsung   | MZ1LV480HCHP-00003 | 480 GB | 2       | 1399  | 0     | 3.84   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 3       | 1347  | 0     | 3.69   |
| Intel     | SSDPEDMX020T7      | 2 TB   | 46      | 1368  | 5     | 3.68   |
| Intel     | SSDPEDMD800G4      | 800 GB | 271     | 1308  | 0     | 3.59   |
| Intel     | SSDPEDMX012T7      | 1.2 TB | 3       | 1300  | 0     | 3.56   |
| Intel     | SSDPE2KE020T7      | 2 TB   | 2       | 1270  | 0     | 3.48   |
| Intel     | SSDPEDMW400G4      | 400 GB | 10      | 1242  | 0     | 3.40   |
| Samsung   | SSD 950 PRO        | 512 GB | 8       | 1201  | 0     | 3.29   |
| Dell      | Express Flash N... | 2 TB   | 14      | 1184  | 0     | 3.25   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 2       | 1148  | 0     | 3.15   |
| Intel     | SSDPE2ME020T4      | 2 TB   | 2       | 1134  | 0     | 3.11   |
| Micron    | MTFDHAL1T2MCF-1... | 1.2 TB | 1       | 1120  | 0     | 3.07   |
| Toshiba   | THNSN5512GPU7      | 512 GB | 15      | 1100  | 0     | 3.01   |
| Samsung   | MZPLL1T6HEHP-00003 | 1.6 TB | 88      | 1094  | 12    | 2.94   |
| Intel     | SSDPEK1W120GA      | 118 GB | 1       | 1054  | 0     | 2.89   |
| Intel     | SSDPE2MX012T7      | 1.2 TB | 19      | 1045  | 0     | 2.86   |
| Intel     | SSDPE2MD400G4      | 400 GB | 13      | 1030  | 0     | 2.82   |
| Dell      | Express Flash N... | 1.6 TB | 19      | 1086  | 54    | 2.82   |
| Samsung   | SSD 960 PRO        | 2 TB   | 1       | 1007  | 0     | 2.76   |
| Intel     | SSDPEDKX040T7      | 4 TB   | 45      | 1028  | 23    | 2.70   |
| Intel     | SSDPE2MX450G7      | 450 GB | 46      | 942   | 0     | 2.58   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 28      | 920   | 0     | 2.52   |
| Samsung   | MZWLL6T4HMLA-00005 | 6.4 TB | 2       | 901   | 0     | 2.47   |
| Samsung   | SSD 960 PRO        | 1 TB   | 10      | 899   | 0     | 2.46   |
| Intel     | SSDPEDMD020T4      | 2 TB   | 1       | 897   | 0     | 2.46   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 2       | 896   | 0     | 2.46   |
| Intel     | SSDPE2MD400G4L     | 400 GB | 4       | 895   | 0     | 2.45   |
| Intel     | SSDPEKKW256G7      | 256 GB | 17      | 911   | 1     | 2.44   |
| WDC       | PC SN720 SDAPNT... | 1 TB   | 1       | 892   | 0     | 2.44   |
| Samsung   | MZPLL3T2HMLS-00003 | 3.2 TB | 6       | 887   | 0     | 2.43   |
| Kingston  | SKC1000960G        | 960 GB | 3       | 886   | 0     | 2.43   |
| Intel     | SSDPE2ME012T4      | 1.2 TB | 8       | 881   | 0     | 2.41   |
| Intel     | SSDPE2KX040T8      | 4 TB   | 65      | 883   | 16    | 2.38   |
| SPCC      | M.2 PCIe SSD       | 1 TB   | 1       | 837   | 0     | 2.29   |
| Intel     | SSDPEDKE040T7      | 4 TB   | 1       | 821   | 0     | 2.25   |
| Samsung   | MZPLL6T4HMLA-00005 | 6.4 TB | 6       | 817   | 0     | 2.24   |
| PNY       | CS3030 500GB SSD   | 500 GB | 2       | 802   | 0     | 2.20   |
| Samsung   | SSD 960 EVO        | 500 GB | 10      | 806   | 8     | 2.17   |
| Intel     | SSDPED1D280GA      | 280 GB | 21      | 871   | 1     | 2.17   |
| Intel     | SSDPED1D480GA      | 480 GB | 52      | 785   | 0     | 2.15   |
| Dell      | Express Flash N... | 1.6 TB | 4       | 782   | 0     | 2.14   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 6       | 781   | 0     | 2.14   |
| Intel     | SSDPE2KE076T8      | 7.6 TB | 2       | 778   | 0     | 2.13   |
| Intel     | SSDPEDMW800G4      | 800 GB | 7       | 774   | 0     | 2.12   |
| Intel     | SSDPE21K375GA      | 375 GB | 30      | 773   | 0     | 2.12   |
| Intel     | SSDPEDMD016T4K     | 1.6 TB | 2       | 764   | 0     | 2.09   |
| Intel     | MT0800KEXUU        | 800 GB | 18      | 764   | 0     | 2.09   |
| Intel     | VO0400KEFJB        | 400 GB | 4       | 743   | 0     | 2.04   |
| Samsung   | MZPLL6T4HMLS-00003 | 6.4 TB | 16      | 742   | 0     | 2.04   |
| Huawei    | HWE36P43016M000N   | 1.6 TB | 2       | 741   | 0     | 2.03   |
| Intel     | SSDPEKKF256G8 NVMe | 256 GB | 1       | 739   | 0     | 2.03   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 5       | 932   | 202   | 2.01   |
| Intel     | SSDPEKKW512G7      | 512 GB | 1       | 728   | 0     | 2.00   |
| Intel     | SSDPE21D480GA      | 480 GB | 107     | 701   | 0     | 1.92   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 21      | 690   | 0     | 1.89   |
| Samsung   | MZQLW960HMJP-00003 | 960 GB | 20      | 1020  | 130   | 1.86   |
| Kingston  | SKC2000M81000G     | 1 TB   | 2       | 668   | 0     | 1.83   |
| WDC       | WUS3CA116C7P3E3    | 1.6 TB | 178     | 648   | 0     | 1.78   |
| Dell      | Express Flash P... | 1.6 TB | 1       | 639   | 0     | 1.75   |
| Intel     | SSDPE2KX080T8      | 8 TB   | 14      | 628   | 0     | 1.72   |
| Samsung   | MZWLL12THMLA-00005 | 12.... | 2       | 627   | 0     | 1.72   |
| Dell      | Express Flash P... | 800 GB | 8       | 626   | 0     | 1.72   |
| WDC       | WUS3BA196C7P3E3    | 960 GB | 83      | 623   | 0     | 1.71   |
| Samsung   | MZPLL3T2HAJQ-00005 | 3.2 TB | 24      | 620   | 0     | 1.70   |
| Intel     | SSDPEKKA256G7      | 256 GB | 4       | 618   | 0     | 1.70   |
| Intel     | SSDPED1K375GA      | 375 GB | 77      | 614   | 0     | 1.68   |
| Intel     | SSDPE2KX020T7      | 2 TB   | 1       | 611   | 0     | 1.68   |
| Samsung   | MZQLW1T9HMJP-00003 | 1.9 TB | 5       | 607   | 0     | 1.66   |
| Samsung   | MZ1LB960HAJQ-00007 | 960 GB | 39      | 597   | 0     | 1.64   |
| Samsung   | SSD 960 EVO        | 250 GB | 4       | 586   | 0     | 1.61   |
| Samsung   | MZPLL6T4HMLS-000MV | 6.4 TB | 4       | 584   | 0     | 1.60   |
| Samsung   | MZWLL800HEHP-00003 | 800 GB | 14      | 864   | 4     | 1.60   |
| Intel     | SSDPEL1D380GA      | 384 GB | 6       | 579   | 0     | 1.59   |
| Intel     | SSDPED1K750GA      | 752 GB | 150     | 572   | 0     | 1.57   |
| Micron    | 9300_MTFDHAL3T8TDP | 3.8 TB | 2       | 552   | 0     | 1.51   |
| Intel     | SSDPEKKW256G8      | 256 GB | 1       | 548   | 0     | 1.50   |
| Samsung   | MZPLL1T6HAJQ-00005 | 1.6 TB | 6       | 546   | 0     | 1.50   |
| Samsung   | SSD 983 DCT        | 960 GB | 6       | 544   | 0     | 1.49   |
| Dell      | Express Flash P... | 1.6 TB | 5       | 539   | 0     | 1.48   |
| Dell      | Express Flash N... | 3.2 TB | 4       | 538   | 0     | 1.47   |
| Samsung   | MZQLB3T8HALS-000AZ | 3.8 TB | 24      | 534   | 0     | 1.46   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 164     | 533   | 0     | 1.46   |
| Intel     | SSDPE21K750GA      | 752 GB | 66      | 532   | 0     | 1.46   |
| Samsung   | SSD 970 EVO        | 500 GB | 3       | 528   | 0     | 1.45   |
| Intel     | SSDPE21K100GA      | 100 GB | 5       | 527   | 0     | 1.45   |
| Dell      | Express Flash P... | 6.4 TB | 1       | 527   | 0     | 1.45   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 12      | 518   | 0     | 1.42   |
| WDC       | WUS3BA138C7P3E3    | 3.8 TB | 28      | 512   | 0     | 1.41   |
| Samsung   | MZQLW1T9HMJP-000AZ | 1.9 TB | 7       | 548   | 1     | 1.40   |
| Dell      | Express Flash N... | 1.6 TB | 115     | 501   | 0     | 1.37   |
| Intel     | SSDPEL1K100GA      | 100 GB | 11      | 494   | 0     | 1.36   |
| Smartbuy  | m.2 PS5013T-2280T  | 128 GB | 1       | 493   | 0     | 1.35   |
| Intel     | SSDPEKKA512G8      | 512 GB | 23      | 489   | 0     | 1.34   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 4       | 486   | 0     | 1.33   |
| Toshiba   | KXD51RUE960G       | 960 GB | 10      | 485   | 0     | 1.33   |
| Crucial   | CT250P2SSD8        | 250 GB | 1       | 484   | 0     | 1.33   |
| Samsung   | MZWLL1T6HAJQ-00005 | 1.6 TB | 10      | 483   | 0     | 1.32   |
| Intel     | SSDPE2ME400G4      | 400 GB | 7       | 483   | 0     | 1.32   |
| Corsair   | Force MP600        | 1 TB   | 3       | 475   | 0     | 1.30   |
| Intel     | SSDPE2MD016T4      | 1.6 TB | 4       | 471   | 0     | 1.29   |
| WDC       | WUS4CB016D7P3E3    | 1.6 TB | 152     | 468   | 0     | 1.28   |
| Dell      | Express Flash P... | 1.6 TB | 12      | 461   | 0     | 1.26   |
| Intel     | SSDPED1D960GAY     | 960 GB | 6       | 460   | 0     | 1.26   |
| Samsung   | MZWLJ15THALA-00007 | 15.... | 2       | 460   | 0     | 1.26   |
| Intel     | SSDPE2KX010T8      | 1 TB   | 142     | 454   | 0     | 1.24   |
| Samsung   | MZWLJ7T6HALA-00007 | 7.6 TB | 2       | 440   | 0     | 1.21   |
| Wester... | WUS3BA196C7P3E3    | 960 GB | 83      | 439   | 0     | 1.20   |
| Samsung   | MZWLL1T6HEHP-00003 | 1.6 TB | 8       | 436   | 0     | 1.20   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 15      | 431   | 0     | 1.18   |
| Seagate   | FireCuda 520 SS... | 500 GB | 10      | 428   | 0     | 1.17   |
| Wester... | WUS3CA116C7P3E3    | 1.6 TB | 178     | 428   | 0     | 1.17   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 5       | 427   | 0     | 1.17   |
| Samsung   | VO001920KWVMT 1... | 1.9 TB | 36      | 427   | 0     | 1.17   |
| Micron    | 2200S NVMe         | 256 GB | 1       | 426   | 0     | 1.17   |
| WDC       | CL SN720 SDAQNT... | 1 TB   | 51      | 425   | 0     | 1.16   |
| Wester... | WUS3BA119C7P3E3    | 960 GB | 1       | 424   | 0     | 1.16   |
| Wester... | WUS3BA138C7P3E3    | 3.8 TB | 20      | 424   | 0     | 1.16   |
| Intel     | SSDPE2KE032T8      | 3.2 TB | 29      | 424   | 0     | 1.16   |
| WDC       | WUS4BB096D7P3E3    | 960 GB | 553     | 423   | 0     | 1.16   |
| HGST      | HUSMR7638BDP3Y1    | 3.8 TB | 24      | 423   | 0     | 1.16   |
| Intel     | SSDPECKE064T7ES    | 3.2 TB | 2       | 422   | 0     | 1.16   |
| ADATA     | SX8200PNP          | 256 GB | 2       | 418   | 0     | 1.15   |
| Phison    | Viper M.2 VPN100   | 2 TB   | 7       | 417   | 0     | 1.14   |
| Samsung   | SSD 960 PRO        | 512 GB | 3       | 416   | 0     | 1.14   |
| HP        | SSD EX950          | 2 TB   | 10      | 403   | 0     | 1.10   |
| Samsung   | MZ4LB3T8HALS-00003 | 3.8 TB | 6       | 388   | 0     | 1.07   |
| WDC       | WUS4BB038D7P3E3    | 3.8 TB | 37      | 379   | 0     | 1.04   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 29      | 393   | 1     | 1.03   |
| Samsung   | SSD 970 PRO        | 1 TB   | 38      | 374   | 0     | 1.02   |
| Toshiba   | KXD51RUE3T84       | 3.8 TB | 1       | 369   | 0     | 1.01   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 46      | 369   | 0     | 1.01   |
| Intel     | SSDPEKKW512G8      | 512 GB | 9       | 367   | 0     | 1.01   |
| Kingston  | SEDC1000M1920G     | 1.9 TB | 2       | 364   | 0     | 1.00   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 6       | 361   | 0     | 0.99   |
| Samsung   | MZPJB480HMGC-0BW07 | 480 GB | 16      | 357   | 0     | 0.98   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 133     | 360   | 6     | 0.96   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 626     | 344   | 0     | 0.94   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 12      | 359   | 1     | 0.94   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 27      | 341   | 0     | 0.94   |
| Samsung   | MZ1LB1T9HALS-00007 | 1.9 TB | 7       | 335   | 0     | 0.92   |
| Intel     | SSDPE2KX040T7      | 4 TB   | 5       | 331   | 0     | 0.91   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 31      | 337   | 1     | 0.91   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 2       | 328   | 0     | 0.90   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 3       | 326   | 0     | 0.89   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 2       | 326   | 0     | 0.89   |
| Samsung   | MZVLW128HEGR-000L1 | 128 GB | 1       | 316   | 0     | 0.87   |
| Kingston  | SEDC1000M960G      | 960 GB | 2       | 314   | 0     | 0.86   |
| WDC       | PC SN530 NVMe      | 512 GB | 1       | 313   | 0     | 0.86   |
| Gigabyte  | GP-GSM2NE3100TNTD  | 1 TB   | 10      | 312   | 0     | 0.86   |
| Goodram   | SSDPR-PX500-01T-80 | 1 TB   | 2       | 312   | 0     | 0.86   |
| Samsung   | SSD 970 PRO        | 512 GB | 84      | 309   | 0     | 0.85   |
| Micron    | 9300_MTFDHAL3T2TDR | 3.2 TB | 36      | 308   | 0     | 0.84   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 5       | 306   | 0     | 0.84   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 900     | 305   | 1     | 0.84   |
| Toshiba   | KXD51RUE1T92       | 1.9 TB | 11      | 293   | 0     | 0.80   |
| Samsung   | MZQLB7T6HMLA-00007 | 7.6 TB | 111     | 301   | 1     | 0.79   |
| Samsung   | MZQLB3T8HALS-00007 | 3.8 TB | 180     | 289   | 1     | 0.78   |
| Wester... | WUS4BB096D7P3E3    | 960 GB | 443     | 273   | 0     | 0.75   |
| Kingston  | SKC2500M8250G      | 250 GB | 5       | 271   | 0     | 0.74   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 2       | 270   | 0     | 0.74   |
| Kingston  | SEDC1000BM8240G    | 240 GB | 2       | 268   | 0     | 0.74   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 8       | 267   | 0     | 0.73   |
| Samsung   | MZPLJ1T6HBJR-000H3 | 1.6 TB | 8       | 265   | 0     | 0.73   |
| Intel     | SSDPECME016T4      | 800 GB | 8       | 262   | 0     | 0.72   |
| Samsung   | MZPJB960HMGC-0BW07 | 960 GB | 12      | 261   | 0     | 0.72   |
| Kingston  | SEDC1000M3840G     | 3.8 TB | 7       | 261   | 0     | 0.72   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 59      | 256   | 0     | 0.70   |
| Intel     | SSDPE2NV076T8      | 7.6 TB | 6       | 255   | 0     | 0.70   |
| Wester... | WUS4CB016D7P3E3    | 1.6 TB | 152     | 246   | 0     | 0.68   |
| Toshiba   | KXG60PNV2T04       | 2 TB   | 8       | 244   | 0     | 0.67   |
| ADATA     | SX8200PNP          | 1 TB   | 2       | 243   | 0     | 0.67   |
| HP        | SSD EX950          | 512 GB | 7       | 242   | 0     | 0.67   |
| Intel     | EO000375KWJUC      | 375 GB | 2       | 242   | 0     | 0.66   |
| WDC       | WUS4BB019D7P3E1    | 1.9 TB | 474     | 241   | 0     | 0.66   |
| WDC       | WUS4BB096D7P3E1    | 960 GB | 487     | 241   | 0     | 0.66   |
| Intel     | SSDPE2NU076T8      | 7.6 TB | 3       | 236   | 0     | 0.65   |
| Samsung   | SSD 970 EVO        | 1 TB   | 8       | 468   | 2     | 0.64   |
| Patriot   | P300               | 128 GB | 4       | 226   | 0     | 0.62   |
| Dell      | Express Flash C... | 960 GB | 100     | 224   | 0     | 0.61   |
| Samsung   | MZPLJ6T4HALA-00007 | 6.4 TB | 41      | 224   | 0     | 0.61   |
| Team      | TM8FP6128G         | 128 GB | 1       | 214   | 0     | 0.59   |
| Kingston  | SA2000M81000G      | 1 TB   | 8       | 212   | 0     | 0.58   |
| Patriot   | P300               | 256 GB | 2       | 208   | 0     | 0.57   |
| Samsung   | SSD 970 EVO        | 250 GB | 3       | 327   | 1     | 0.55   |
| Kingston  | SKC2500M81000G     | 1 TB   | 9       | 202   | 0     | 0.55   |
| Micron    | 7300_MTFDHBE960TDF | 960 GB | 4       | 199   | 0     | 0.55   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 77      | 198   | 0     | 0.54   |
| SK hynix  | PC601 NVMe         | 256 GB | 1       | 192   | 0     | 0.53   |
| Samsung   | MZVLW256HEHP-000H1 | 256 GB | 1       | 191   | 0     | 0.52   |
| Micron    | 9300_MTFDHAL7T6TDP | 7.6 TB | 51      | 191   | 0     | 0.52   |
| Samsung   | MZQLB1T9HAJR-000AZ | 1.9 TB | 4       | 189   | 0     | 0.52   |
| Intel     | SSDPE2KX010T7      | 1 TB   | 8       | 186   | 0     | 0.51   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 14      | 185   | 0     | 0.51   |
| Intel     | SSDPE2KE016T8      | 1.6 TB | 29      | 184   | 0     | 0.51   |
| WDC       | WUS4BB038D7P3E1    | 3.8 TB | 154     | 183   | 0     | 0.50   |
| Corsair   | Force MP600        | 500 GB | 4       | 178   | 0     | 0.49   |
| Silico... | NVME SSD           | 512 GB | 1       | 177   | 0     | 0.49   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 27      | 177   | 0     | 0.49   |
| Dell      | Ent NVMe AGN RI... | 3.8 TB | 192     | 176   | 0     | 0.48   |
| WDC       | WDS500G2B0C-00PXH0 | 500 GB | 1       | 174   | 0     | 0.48   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 69      | 174   | 0     | 0.48   |
| Samsung   | MZPLJ3T2HBJR-000H3 | 3.2 TB | 6       | 170   | 0     | 0.47   |
| Samsung   | MZPLJ1T6HBJR-00007 | 1.6 TB | 4       | 170   | 0     | 0.47   |
| Intel     | SSDPEKNW512G8H     | 512 GB | 1       | 164   | 0     | 0.45   |
| WDC       | WUS4BB076D7P3E1    | 7.6 TB | 33      | 163   | 0     | 0.45   |
| Crucial   | CT500P1SSD8        | 500 GB | 2       | 163   | 0     | 0.45   |
| Corsair   | MP400              | 1 TB   | 20      | 162   | 0     | 0.45   |
| Wester... | WUS4BB038D7P3E3    | 3.8 TB | 13      | 162   | 0     | 0.44   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 25      | 160   | 0     | 0.44   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 2       | 157   | 0     | 0.43   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 80      | 150   | 0     | 0.41   |
| WDC       | WUS4BB038D7P3E4    | 3.8 TB | 18      | 148   | 0     | 0.41   |
| WDC       | WUS4BB019D7P3E3    | 1.9 TB | 54      | 146   | 0     | 0.40   |
| Kingston  | SA1000M8960G       | 960 GB | 1       | 146   | 0     | 0.40   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 54      | 143   | 0     | 0.39   |
| Micron    | 7300_MTFDHBE6T4TDG | 6.4 TB | 24      | 141   | 0     | 0.39   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 10      | 141   | 0     | 0.39   |
| Kingston  | SNVS500G           | 500 GB | 1       | 140   | 0     | 0.39   |
| Intel     | SSDPF2KX076TZ      | 7.6 TB | 5       | 140   | 0     | 0.38   |
| Dell      | Ent NVMe AGN RI... | 7.6 TB | 57      | 138   | 0     | 0.38   |
| Dell      | Ent NVMe CM6 RI... | 1.9 TB | 19      | 137   | 0     | 0.38   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 33      | 132   | 0     | 0.36   |
| Intel     | SSDPE2MD800G4      | 800 GB | 1       | 130   | 0     | 0.36   |
| XPG       | SPECTRIX S40G      | 4 TB   | 4       | 166   | 4     | 0.35   |
| WDC       | WUS3BA119C7P3E3    | 1.9 TB | 8       | 126   | 0     | 0.35   |
| Samsung   | MZQL21T9HCJR-00... | 1.9 TB | 6       | 119   | 0     | 0.33   |
| Wester... | WUS4BB019D7P3E1    | 1.9 TB | 193     | 117   | 0     | 0.32   |
| Intel     | MDTPED1K750GA      | 752 GB | 7       | 115   | 0     | 0.32   |
| Micron    | 7300_MTFDHBG3T8TDF | 3.8 TB | 8       | 115   | 0     | 0.32   |
| ADATA     | SX8200PNP          | 512 GB | 5       | 114   | 0     | 0.31   |
| Wester... | WUS4BB076D7P3E1    | 7.6 TB | 12      | 114   | 0     | 0.31   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 4       | 114   | 0     | 0.31   |
| Kingston  | SA2000M8500G       | 500 GB | 4       | 111   | 0     | 0.31   |
| KIOXIA    | KCD6XLUL1T92       | 1.9 TB | 10      | 109   | 0     | 0.30   |
| Huawei    | HWE52P431T6M002N   | 1.6 TB | 2       | 108   | 0     | 0.30   |
| Toshiba   | KXG6AZNV512G       | 512 GB | 20      | 107   | 0     | 0.29   |
| Phison    | PCIe SSD           | 4 TB   | 7       | 105   | 0     | 0.29   |
| Samsung   | MZPLJ3T2HBJR-00007 | 3.2 TB | 32      | 102   | 0     | 0.28   |
| Kingston  | SA2000M8250G       | 250 GB | 1       | 101   | 0     | 0.28   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 18      | 98    | 0     | 0.27   |
| Wester... | WUS4BB096D7P3E1    | 960 GB | 200     | 97    | 0     | 0.27   |
| Toshiba   | KXG60ZNV256G       | 256 GB | 151     | 96    | 0     | 0.26   |
| ADATA     | SX8200PNP          | 2 TB   | 3       | 96    | 0     | 0.26   |
| Dell      | Ent NVMe P5600 ... | 1.6 TB | 26      | 95    | 0     | 0.26   |
| Samsung   | MZQL27T6HBLA-00A07 | 7.6 TB | 15      | 94    | 0     | 0.26   |
| Transcend | TS2TMTE220S        | 2 TB   | 2       | 94    | 0     | 0.26   |
| Dell      | Express Flash P... | 1.6 TB | 4       | 92    | 0     | 0.25   |
| WDC       | WUS4BB076D7P3E3    | 7.6 TB | 4       | 90    | 0     | 0.25   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 6       | 90    | 0     | 0.25   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 87    | 0     | 0.24   |
| Samsung   | MZ1L2960HCJR-00A07 | 960 GB | 1       | 84    | 0     | 0.23   |
| SK hynix  | VO000960KXAVL      | 960 GB | 2       | 80    | 0     | 0.22   |
| Samsung   | SSD 980            | 500 GB | 4       | 79    | 0     | 0.22   |
| Samsung   | MT001600KWHAC 1... | 1.6 TB | 1       | 77    | 0     | 0.21   |
| Wester... | WUS4BB038D7P3E1    | 3.8 TB | 71      | 76    | 0     | 0.21   |
| Crucial   | CT500P5SSD8        | 500 GB | 5       | 74    | 0     | 0.20   |
| SK hynix  | BC501 HFM512GDJ... | 512 GB | 1       | 73    | 0     | 0.20   |
| Micron    | 7300_MTFDHBG1T9TDF | 1.9 TB | 13      | 71    | 0     | 0.20   |
| Samsung   | SSD 980 PRO        | 250 GB | 2       | 71    | 0     | 0.19   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 1       | 70    | 0     | 0.19   |
| ADATA     | SX6000PNP          | 256 GB | 2       | 70    | 0     | 0.19   |
| Samsung   | MZQL23T8HCLS-00... | 3.8 TB | 12      | 65    | 0     | 0.18   |
| Micron    | 7300_MTFDHBE1T6TDG | 1.6 TB | 2       | 64    | 0     | 0.18   |
| Dell      | Express Flash N... | 6.4 TB | 4       | 63    | 0     | 0.17   |
| Samsung   | SSD 983 DCT M.2    | 960 GB | 5       | 62    | 0     | 0.17   |
| Micron    | 7300_MTFDHBA480TDF | 480 GB | 2       | 58    | 0     | 0.16   |
| Micron    | MTFDHBA480TDF      | 480 GB | 8       | 57    | 0     | 0.16   |
| Intel     | SSDPEKNW512G8      | 512 GB | 5       | 101   | 203   | 0.15   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 5       | 54    | 0     | 0.15   |
| Kingston  | SKC2500M8500G      | 500 GB | 4       | 53    | 0     | 0.15   |
| Kingston  | SKC3000S1024G      | 1 TB   | 1       | 52    | 0     | 0.14   |
| Samsung   | MZVL21T0HCLR-00B00 | 1 TB   | 8       | 49    | 0     | 0.14   |
| Huawei    | HWE56P43800M005N   | 800 GB | 3       | 48    | 0     | 0.13   |
| Patriot   | M.2 P300           | 128 GB | 1       | 48    | 0     | 0.13   |
| SK hynix  | PC601 HFS256GD9... | 256 GB | 1       | 46    | 0     | 0.13   |
| Intel     | SSDPEKNU512GZ      | 512 GB | 1       | 46    | 0     | 0.13   |
| WDC       | WUS4CB032D7P3E4    | 3.2 TB | 5       | 45    | 0     | 0.12   |
| Kingston  | SKC2500M82000G     | 2 TB   | 3       | 44    | 0     | 0.12   |
| WDC       | WUS4BB096D7P3E4    | 960 GB | 4       | 43    | 0     | 0.12   |
| Transcend | TS512GMTE110S      | 512 GB | 1       | 43    | 0     | 0.12   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 4       | 42    | 0     | 0.12   |
| Samsung   | MZQL2960HCJR-00A07 | 960 GB | 32      | 41    | 0     | 0.11   |
| Samsung   | MZVLB256HBHQ-000L2 | 256 GB | 1       | 33    | 0     | 0.09   |
| Silico... | NV900-1T           | 1 TB   | 1       | 30    | 0     | 0.08   |
| ADATA     | SX6000LNP          | 512 GB | 1       | 30    | 0     | 0.08   |
| XPG       | GAMMIX S11 Pro     | 256 GB | 1       | 24    | 0     | 0.07   |
| Micron    | MTFDHBA1T0TDV-1... | 1 TB   | 1       | 21    | 0     | 0.06   |
| HP        | SSD EX900          | 1 TB   | 2       | 20    | 0     | 0.06   |
| SK hynix  | BC501A NVMe        | 128 GB | 3       | 14    | 0     | 0.04   |
| Wester... | WUS4BB096D7P3E4    | 960 GB | 4       | 13    | 0     | 0.04   |
| Wester... | WUS4CB032D7P3E4    | 3.2 TB | 4       | 11    | 0     | 0.03   |
| Samsung   | MZVL2512HCJQ-00B07 | 512 GB | 2       | 10    | 0     | 0.03   |
| Samsung   | MZQLB960HAJR-000AZ | 960 GB | 11      | 10    | 0     | 0.03   |
| SanDisk   | WD Red SN700       | 500 GB | 3       | 10    | 0     | 0.03   |
| Intel     | SSDPELKX010T8      | 1 TB   | 2       | 9     | 0     | 0.03   |
| Crucial   | CT1000P5PSSD8      | 1 TB   | 2       | 7     | 0     | 0.02   |
| Micron    | 7300_MTFDHBE3T8TDF | 3.8 TB | 2       | 6     | 0     | 0.02   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 3       | 6     | 0     | 0.02   |
| Kingston  | SNVS1000GB         | 1 TB   | 1       | 6     | 0     | 0.02   |
| KIOXIA    | KCD61LUL3T84       | 3.8 TB | 20      | 5     | 0     | 0.01   |
| ADATA     | SX6000NP           | 128 GB | 1       | 615   | 142   | 0.01   |
| WDC       | PC SN730 SDBQNT... | 256 GB | 1       | 4     | 0     | 0.01   |
| WDC       | PC SN520 SDAPNU... | 256 GB | 1       | 4     | 0     | 0.01   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 3       | 4     | 0     | 0.01   |
| Samsung   | SSD 980            | 250 GB | 4       | 1     | 0     | 0.00   |
| Micron    | 7400_MTFDKCB1T9TDZ | 1.9 TB | 5       | 1     | 0     | 0.00   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 2       | 1     | 0     | 0.00   |
| Samsung   | MZVLW1T0HMLH-000L7 | 1 TB   | 1       | 0     | 0     | 0.00   |
| Intel     | SSDPEKKF128G8      | 128 GB | 1       | 0     | 0     | 0.00   |
| Netac     | NVMe SSD           | 1 TB   | 1       | 0     | 0     | 0.00   |
| Samsung   | SSD 980            | 1 TB   | 2       | 0     | 0     | 0.00   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days — avg. days per sample,
Err  — avg. errors per sample,
MTBF — avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| Intel       | 79     | 1930    | 862   | 2     | 2.35   |
| SPCC        | 1      | 1       | 837   | 0     | 2.29   |
| PNY         | 1      | 2       | 802   | 0     | 2.20   |
| Smartbuy    | 1      | 1       | 493   | 0     | 1.35   |
| Seagate     | 1      | 10      | 428   | 0     | 1.17   |
| HGST        | 1      | 24      | 423   | 0     | 1.16   |
| Samsung     | 85     | 2906    | 351   | 2     | 0.94   |
| WDC         | 31     | 2599    | 339   | 1     | 0.93   |
| Dell        | 19     | 587     | 320   | 2     | 0.87   |
| Gigabyte    | 1      | 10      | 312   | 0     | 0.86   |
| Goodram     | 1      | 2       | 312   | 0     | 0.86   |
| HP          | 3      | 19      | 303   | 0     | 0.83   |
| Corsair     | 4      | 39      | 297   | 0     | 0.82   |
| Toshiba     | 12     | 350     | 276   | 0     | 0.76   |
| Phison      | 3      | 19      | 273   | 0     | 0.75   |
| Huawei      | 3      | 7       | 263   | 0     | 0.72   |
| Kingston    | 17     | 56      | 247   | 0     | 0.68   |
| Western ... | 13     | 1374    | 241   | 0     | 0.66   |
| Team        | 1      | 1       | 214   | 0     | 0.59   |
| Patriot     | 3      | 7       | 196   | 0     | 0.54   |
| Micron      | 17     | 247     | 178   | 0     | 0.49   |
| ADATA       | 7      | 16      | 185   | 9     | 0.40   |
| XPG         | 2      | 5       | 138   | 3     | 0.29   |
| Silicon ... | 2      | 2       | 103   | 0     | 0.28   |
| Crucial     | 6      | 17      | 81    | 0     | 0.22   |
| SK hynix    | 6      | 12      | 81    | 0     | 0.22   |
| Transcend   | 2      | 3       | 77    | 0     | 0.21   |
| KIOXIA      | 2      | 30      | 39    | 0     | 0.11   |
| SanDisk     | 1      | 3       | 10    | 0     | 0.03   |
| Netac       | 1      | 1       | 0     | 0     | 0.00   |

