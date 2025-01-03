Reliability Test For Enterprise Hard Drives
-------------------------------------------

This is a project to estimate reliability of enterprise HDD/SSD drives by the analysis
of SMART reports from servers. The primary aim of the project is to find drives with
longest power-on hours (POH) and minimal number of errors, i.e. maximal MTBF (mean time
between failures).

Everyone can contribute to this report by installing [hw-probe](https://github.com/linuxhw/hw-probe) to
their [OpenVZ](https://wiki.openvz.org/) servers:

    sudo -E hw-probe -all -upload

This is a report for enterprise drives. Report for consumer drives: [SMART](https://github.com/linuxhw/SMART)

Total drives: 65082.

Contents
--------

1. [ About          ](#about)
2. [ HDD by Model   ](#hdd-by-model)
3. [ HDD by Vendor  ](#hdd-by-vendor)
4. [ SSD by Model   ](#ssd-by-model)
5. [ SSD by Vendor  ](#ssd-by-vendor)
6. [ NVMe by Model  ](#nvme-by-model)
7. [ NVMe by Vendor ](#nvme-by-vendor)

About
-----

The structure of the reports directory is the following:

    {KIND OF DRIVE}/{VENDOR}/{MODEL PREFIX}/{MODEL}/{DRIVE ID}

    ( e.g. HDD/Seagate/ST9500/ST9500620NS/B0744A84D66D )

Based on SMART data we determine most reliable drive models and vendors by the
following formula:

    MTBF = Power_On_Hours / ( 1 + Number_Of_Important_Errors ) / ( 365*24 )

    ( i.e. MTBF = "Years before/between errors" )

Number_Of_Important_Errors - number of important errors that can indicate a drive failure:

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

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested HDD samples in the Appendix 1 ([All_HDD.md](/All_HDD.md)).

See top 1000 of tested HDD models in the [Top1000_HDD.md](/Top1000_HDD.md).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| WDC       | WD1002FBYS-01A6B0  | 1 TB   | 2       | 3814  | 0     | 10.45  |
| Maxtor    | STM3250310AS       | 250 GB | 2       | 3810  | 0     | 10.44  |
| Seagate   | ST32500NSSUN250G   | 250 GB | 2       | 3676  | 0     | 10.07  |
| WDC       | WD2502ABYS-01B7A0  | 256 GB | 3       | 3659  | 0     | 10.03  |
| Hitachi   | HUA7210SASUN1.0T   | 1 TB   | 18      | 3987  | 1     | 9.62   |
| WDC       | WD1001FALS-00Y6A0  | 1 TB   | 3       | 3237  | 0     | 8.87   |
| HP        | MB1000GCEEK        | 1 TB   | 4       | 3173  | 0     | 8.69   |
| Seagate   | ST3320620AS        | 320 GB | 3       | 4466  | 5     | 8.55   |
| WDC       | WD1500HLFS-01G6U4  | 150 GB | 4       | 3016  | 0     | 8.26   |
| WDC       | WD1002FBYS-05A6B0  | 1 TB   | 8       | 3444  | 1     | 8.24   |
| Hitachi   | HDS721010KLA330    | 1 TB   | 16      | 3401  | 16    | 8.23   |
| HP        | GB0500EAFYL        | 500 GB | 2       | 2973  | 0     | 8.15   |
| Hitachi   | HDS721050CLA360    | 500 GB | 2       | 2828  | 0     | 7.75   |
| Hitachi   | HDS723030ALA640    | 3 TB   | 8       | 3043  | 22    | 7.73   |
| Hitachi   | HDS723020BLA642    | 2 TB   | 93      | 3139  | 16    | 7.69   |
| Seagate   | ST3320620A         | 320 GB | 2       | 2728  | 0     | 7.47   |
| Hitachi   | HUA721010KLA330    | 1 TB   | 23      | 2801  | 1     | 7.44   |
| WDC       | WD1002FBYS-02A6B0  | 1 TB   | 17      | 2925  | 2     | 7.19   |
| Samsung   | HD502HJ            | 500 GB | 4       | 2564  | 0     | 7.03   |
| WDC       | WD5003ABYX-01WERA2 | 500 GB | 2       | 2547  | 0     | 6.98   |
| Seagate   | ST3250620NS        | 250 GB | 4       | 2532  | 0     | 6.94   |
| HP        | GB0250EAFYK        | 250 GB | 2       | 2531  | 0     | 6.93   |
| HP        | GB0500C4413        | 500 GB | 2       | 3306  | 1     | 6.90   |
| WDC       | WD5000AACS-00G8B1  | 500 GB | 2       | 4393  | 3     | 6.87   |
| HP        | MB1000GDUNU        | 1 TB   | 2       | 2503  | 0     | 6.86   |
| HP        | MB2000EBUCF        | 2 TB   | 2       | 2458  | 0     | 6.74   |
| WDC       | WD7500AYYS-01RCA0  | 752 GB | 5       | 2803  | 1     | 6.71   |
| Hitachi   | HUA722050CLA330    | 500 GB | 3       | 2440  | 0     | 6.69   |
| WDC       | WD6400AAKS-41H2B0  | 640 GB | 2       | 2433  | 0     | 6.67   |
| Seagate   | ST4000VN000-1H4168 | 4 TB   | 33      | 2556  | 1     | 6.66   |
| Seagate   | ST32000646NS       | 2 TB   | 2       | 2424  | 0     | 6.64   |
| Seagate   | ST3250410AS        | 250 GB | 4       | 3467  | 85    | 6.60   |
| HP        | MB1000GCWCV        | 1 TB   | 3       | 2387  | 0     | 6.54   |
| Hitachi   | HDS722020ALA330    | 2 TB   | 36      | 2753  | 58    | 6.49   |
| WDC       | WD7501AALS-00J7B0  | 752 GB | 2       | 2359  | 0     | 6.46   |
| WDC       | WD7502AAEX-00Y9A0  | 752 GB | 4       | 2329  | 0     | 6.38   |
| Hitachi   | HDS723020BLE640    | 2 TB   | 10      | 3101  | 3     | 6.33   |
| HGST      | HDS724040ALE640    | 4 TB   | 7       | 2281  | 0     | 6.25   |
| Seagate   | ST1000NC001-1DY162 | 1 TB   | 3       | 2254  | 0     | 6.18   |
| WDC       | WD30EZRX-00SPEB0   | 3 TB   | 6       | 2652  | 2     | 6.17   |
| WDC       | WD5002AALX-00J37A0 | 500 GB | 13      | 2804  | 3     | 6.09   |
| WDC       | WD1002FBYS-18W8B0  | 1 TB   | 10      | 2892  | 9     | 6.05   |
| WDC       | WD6001FSYZ-01SS7B0 | 6 TB   | 3       | 2201  | 0     | 6.03   |
| Seagate   | ST3000VX000-1CU166 | 3 TB   | 27      | 2613  | 5     | 5.97   |
| WDC       | WD5003AZEX-00K1GA0 | 500 GB | 43      | 2300  | 1     | 5.94   |
| Hitachi   | HDP725050GLA360    | 500 GB | 3       | 2156  | 0     | 5.91   |
| HGST      | HUS724020ALA640    | 2 TB   | 267     | 2223  | 9     | 5.90   |
| Toshiba   | MD04ACA500         | 5 TB   | 2       | 2148  | 0     | 5.89   |
| Seagate   | ST6000DM001-1XY17Z | 6 TB   | 4       | 2125  | 0     | 5.82   |
| Seagate   | ST3320620NS        | 320 GB | 4       | 2189  | 1     | 5.81   |
| Hitachi   | HUA723030ALA640    | 3 TB   | 42      | 2236  | 1     | 5.78   |
| Seagate   | ST2000VX000-1ES164 | 2 TB   | 2       | 2105  | 0     | 5.77   |
| Seagate   | ST2000VN000-1HJ164 | 2 TB   | 2       | 2067  | 0     | 5.67   |
| WDC       | WD3000HLFS-01G6U4  | 304 GB | 2       | 3664  | 16    | 5.58   |
| Seagate   | ST1000VX000-1CU162 | 1 TB   | 5       | 2014  | 0     | 5.52   |
| Seagate   | ST4000VN0001-1S... | 4 TB   | 9       | 2235  | 1     | 5.51   |
| WDC       | WD2004FBYZ-01YCBB0 | 2 TB   | 5       | 2002  | 0     | 5.49   |
| Seagate   | ST750LX003-1AC154  | 752 GB | 2       | 3002  | 1     | 5.48   |
| WDC       | WD2502ABYS-18B7A0  | 250 GB | 2       | 1995  | 0     | 5.47   |
| WDC       | WD20EARX-00PASB0   | 2 TB   | 4       | 1982  | 0     | 5.43   |
| Seagate   | ST91000640NS       | 1 TB   | 44      | 2173  | 2     | 5.36   |
| WDC       | WD10EZEX-22RKKA0   | 1 TB   | 4       | 2345  | 1     | 5.36   |
| Seagate   | ST4000NM0033-9Z... | 4 TB   | 458     | 2390  | 121   | 5.33   |
| Maxtor    | 6V160E0            | 160 GB | 2       | 1932  | 0     | 5.29   |
| Seagate   | ST500DM002-1BC142  | 500 GB | 2       | 1929  | 0     | 5.29   |
| HGST      | HUS726060ALE614    | 6 TB   | 149     | 2130  | 13    | 5.23   |
| WDC       | WD30EFRX-68AX9N0   | 3 TB   | 20      | 2576  | 3     | 5.23   |
| Hitachi   | HDS5C3020ALA632    | 2 TB   | 2       | 2729  | 1008  | 5.23   |
| WDC       | WD30EZRX-00DC0B0   | 3 TB   | 8       | 2115  | 11    | 5.22   |
| WDC       | WD10EZEX-75ZF5A0   | 1 TB   | 2       | 1898  | 0     | 5.20   |
| WDC       | WD20EFRX-68AX9N0   | 2 TB   | 4       | 2862  | 4     | 5.12   |
| Hitachi   | HUA723020ALA640    | 2 TB   | 22      | 1925  | 7     | 5.07   |
| HGST      | HUH728080ALE604    | 8 TB   | 62      | 1892  | 5     | 5.05   |
| Toshiba   | HDWE160            | 6 TB   | 74      | 1949  | 2     | 5.02   |
| WDC       | WD1002FAEX-007BA0  | 1 TB   | 2       | 1821  | 0     | 4.99   |
| WDC       | WD2001FFSX-68JNUN0 | 2 TB   | 3       | 2178  | 1     | 4.98   |
| WDC       | WD2002FYPS-01U1B1  | 2 TB   | 17      | 2931  | 208   | 4.97   |
| Toshiba   | MQ01UBD050         | 500 GB | 12      | 1889  | 1     | 4.94   |
| Hitachi   | HDT725032VLA360    | 320 GB | 5       | 3663  | 7     | 4.90   |
| Seagate   | ST2000NM0024-1H... | 2 TB   | 9       | 1786  | 0     | 4.89   |
| HGST      | HMS5C4040BLE640    | 4 TB   | 19      | 1854  | 13    | 4.88   |
| WDC       | WD1002FBYS-18W8B1  | 1 TB   | 7       | 2645  | 1     | 4.87   |
| WDC       | WD20EZRX-00DC0B0   | 2 TB   | 7       | 1768  | 0     | 4.84   |
| WDC       | WD1002FAEX-00Z3A0  | 1 TB   | 37      | 2081  | 37    | 4.83   |
| HP        | GB0160EAFJE        | 160 GB | 2       | 2937  | 513   | 4.82   |
| Hitachi   | HUA722010CLA330    | 1 TB   | 66      | 2247  | 21    | 4.81   |
| Toshiba   | MK1002TSKB         | 1 TB   | 12      | 1751  | 0     | 4.80   |
| Seagate   | ST3000DM001-1CH166 | 3 TB   | 20      | 1981  | 22    | 4.77   |
| WDC       | WD20EADS-00R6B0    | 2 TB   | 2       | 3219  | 6     | 4.75   |
| Seagate   | ST3000VX000-1ES166 | 3 TB   | 3       | 1727  | 0     | 4.73   |
| HGST      | HUS726030ALA610    | 3 TB   | 47      | 1745  | 1     | 4.71   |
| Seagate   | ST6000NM0004-1F... | 6 TB   | 12      | 1708  | 0     | 4.68   |
| WDC       | WD4001FFSX-68JNUN0 | 4 TB   | 12      | 2048  | 1     | 4.68   |
| WDC       | WD2002FAEX-007BA0  | 2 TB   | 62      | 2015  | 40    | 4.67   |
| Seagate   | MM0500GBKAK        | 500 GB | 2       | 1702  | 0     | 4.66   |
| Samsung   | HD103UJ            | 1 TB   | 26      | 2912  | 144   | 4.64   |
| Seagate   | ST6000NM0024-1H... | 6 TB   | 1697    | 2053  | 19    | 4.59   |
| WDC       | WD20EARX-00MMMB0   | 2 TB   | 2       | 2762  | 2     | 4.55   |
| Seagate   | ST3500630NS        | 500 GB | 9       | 1654  | 0     | 4.53   |
| WDC       | WD20EARS-00MVWB0   | 2 TB   | 7       | 2143  | 1     | 4.52   |
| WDC       | WD40PURX-64NZ6Y0   | 4 TB   | 4       | 1648  | 0     | 4.52   |
| WDC       | WD1000CHTZ-04JCPV1 | 1 TB   | 4       | 1647  | 0     | 4.51   |
| Seagate   | ST500NM0011 00W... | 500 GB | 2       | 1647  | 0     | 4.51   |
| WDC       | WD5003ABYX-23 0... | 500 GB | 2       | 1645  | 0     | 4.51   |
| Seagate   | ST33000651AS       | 3 TB   | 4       | 2352  | 10    | 4.50   |
| HGST      | HTE541010A9E680    | 1 TB   | 6       | 1631  | 0     | 4.47   |
| WDC       | WD5000AAKX-003CA0  | 500 GB | 3       | 2229  | 3     | 4.45   |
| Hitachi   | HUA722010ALA330    | 1 TB   | 5       | 2547  | 5     | 4.45   |
| WDC       | WD7500BPKX-00HPJT0 | 752 GB | 16      | 1948  | 2     | 4.44   |
| WDC       | WD5003ABYZ-011FA0  | 500 GB | 19      | 1676  | 41    | 4.43   |
| WDC       | WD6402AAEX-00Y9A0  | 640 GB | 3       | 2411  | 677   | 4.43   |
| HGST      | HDN724030ALE640    | 3 TB   | 8       | 1613  | 0     | 4.42   |
| HGST      | HDN724040ALE640    | 4 TB   | 22      | 1798  | 92    | 4.42   |
| Seagate   | ST3000NM0033-9Z... | 3 TB   | 25      | 2237  | 185   | 4.39   |
| WDC       | WD101KRYZ-01JPDB0  | 10 TB  | 2       | 1590  | 0     | 4.36   |
| HGST      | HUH728080ALE601    | 8 TB   | 39      | 1582  | 0     | 4.34   |
| HGST      | HUS724040ALA640    | 4 TB   | 150     | 1684  | 2     | 4.33   |
| WDC       | WD1000DHTZ-04N21V1 | 1 TB   | 7       | 2185  | 2     | 4.33   |
| HGST      | HUH728080ALE600    | 8 TB   | 20      | 1577  | 0     | 4.32   |
| WDC       | WD2004FBYZ-01YCBB2 | 2 TB   | 2       | 1571  | 0     | 4.31   |
| WDC       | WD4000FYYZ-03UL1B3 | 4 TB   | 2       | 1571  | 0     | 4.31   |
| WDC       | WD2003FYPS-02W0B1  | 2 TB   | 2       | 1563  | 0     | 4.28   |
| WDC       | WD2003FYYS-02W0B1  | 2 TB   | 36      | 2048  | 50    | 4.25   |
| WDC       | WD10EZEX-00RKKA0   | 1 TB   | 7       | 1828  | 16    | 4.21   |
| Hitachi   | HUA722020ALA330    | 2 TB   | 6       | 2058  | 2     | 4.19   |
| Seagate   | ST2000DM001-1ER164 | 2 TB   | 29      | 1737  | 211   | 4.19   |
| Hitachi   | HUA723020ALA641    | 2 TB   | 14      | 1527  | 0     | 4.19   |
| WDC       | WD4002FFWX-68TZ4N0 | 4 TB   | 5       | 1523  | 0     | 4.17   |
| WDC       | WD4003FZEX-00Z4SA0 | 4 TB   | 16      | 1521  | 0     | 4.17   |
| Seagate   | ST1000NM0033-9Z... | 1 TB   | 155     | 1809  | 82    | 4.16   |
| Toshiba   | DT01ACA300         | 3 TB   | 80      | 1795  | 22    | 4.15   |
| Toshiba   | MG04ACA400N        | 4 TB   | 29      | 1733  | 2     | 4.14   |
| Seagate   | ST1000DM003-1ER162 | 1 TB   | 33      | 1505  | 0     | 4.13   |
| WDC       | WD30EFRX-68EUZN0   | 3 TB   | 55      | 1853  | 1     | 4.12   |
| WDC       | WD6002FRYZ-01WD5B0 | 6 TB   | 69      | 1597  | 30    | 4.12   |
| Seagate   | ST9250610NS        | 250 GB | 10      | 1643  | 1     | 4.11   |
| Seagate   | ST6000VX0001-1S... | 6 TB   | 4       | 1500  | 0     | 4.11   |
| WDC       | WD2003FYYS-05T8B0  | 2 TB   | 2       | 1487  | 0     | 4.08   |
| Seagate   | ST500NM0011        | 500 GB | 11      | 2167  | 4     | 4.06   |
| Seagate   | ST320DM000-1BC14C  | 320 GB | 2       | 1479  | 0     | 4.05   |
| WDC       | WD2500HHTZ-04N21V0 | 250 GB | 3       | 1473  | 0     | 4.04   |
| Toshiba   | MG04ACA600E        | 6 TB   | 778     | 1575  | 18    | 4.04   |
| WDC       | WD6002FFWX-68TZ4N0 | 6 TB   | 9       | 1809  | 42    | 4.03   |
| HGST      | HUS724040ALE640    | 4 TB   | 22      | 1457  | 0     | 3.99   |
| WDC       | WD5000AAKX-75U6AA0 | 500 GB | 4       | 1451  | 0     | 3.98   |
| WDC       | WD5002AALX-32Z3A0  | 500 GB | 8       | 1449  | 0     | 3.97   |
| WDC       | WD10EALX-089BA0    | 1 TB   | 7       | 1914  | 2     | 3.97   |
| WDC       | WD5000AZLX-00CL5A0 | 500 GB | 2       | 1448  | 0     | 3.97   |
| Hitachi   | HDS721010CLA332    | 1 TB   | 19      | 2874  | 401   | 3.94   |
| HGST      | HUS724030ALA640    | 3 TB   | 41      | 1779  | 68    | 3.94   |
| WDC       | WD30EZRX-00D8PB0   | 3 TB   | 16      | 1707  | 1     | 3.90   |
| HGST      | HUS726020ALE614    | 2 TB   | 81      | 1469  | 26    | 3.89   |
| Toshiba   | MK2002TSKB         | 2 TB   | 3       | 2317  | 4     | 3.88   |
| HGST      | HDN726040ALE614    | 4 TB   | 23      | 1411  | 0     | 3.87   |
| Seagate   | ST4000DX001-1CE168 | 4 TB   | 2       | 1411  | 0     | 3.87   |
| Seagate   | ST3000VX006-1HH166 | 3 TB   | 4       | 1407  | 0     | 3.86   |
| Seagate   | ST4000DM000-1F2168 | 4 TB   | 34      | 2049  | 142   | 3.85   |
| Seagate   | ST4000NM0024-1H... | 4 TB   | 21      | 1638  | 76    | 3.82   |
| HGST      | HDN726060ALE614    | 6 TB   | 2       | 1392  | 0     | 3.81   |
| Toshiba   | MG03ACA100         | 1 TB   | 58      | 1394  | 2     | 3.78   |
| WDC       | WD5001AALS-00E3A0  | 500 GB | 6       | 2162  | 3     | 3.78   |
| Seagate   | ST8000NM0055-1R... | 8 TB   | 949     | 1510  | 23    | 3.76   |
| WDC       | WD5000BMVW-11AJGS2 | 500 GB | 2       | 1372  | 0     | 3.76   |
| Seagate   | ST6000VN0041-2E... | 6 TB   | 10      | 1474  | 1     | 3.76   |
| WDC       | WD1002FBYS-18A6B0  | 1 TB   | 7       | 2160  | 401   | 3.75   |
| WDC       | WD1003FBYX-50Y7B1  | 1 TB   | 3       | 1368  | 0     | 3.75   |
| WDC       | WD1003FBYX-01Y7B1  | 1 TB   | 129     | 1624  | 7     | 3.72   |
| WDC       | WD2500BHTZ-04JCPV1 | 250 GB | 2       | 1354  | 0     | 3.71   |
| WDC       | WD40EFRX-68WT0N0   | 4 TB   | 290     | 2130  | 18    | 3.70   |
| HGST      | HUS726040ALE614    | 4 TB   | 28      | 1907  | 11    | 3.70   |
| WDC       | WD1002FAEX-00Y9A0  | 1 TB   | 44      | 1560  | 8     | 3.69   |
| HP        | MB1000GCEHH        | 1 TB   | 5       | 3106  | 464   | 3.69   |
| Seagate   | ST8000DM005-2EH112 | 8 TB   | 217     | 1431  | 1     | 3.67   |
| Seagate   | ST1000NM0018-2F... | 1 TB   | 36      | 1366  | 1     | 3.67   |
| WDC       | WD2004FBYZ-01YCBB1 | 2 TB   | 25      | 1415  | 1     | 3.66   |
| Toshiba   | DT01ACA100         | 1 TB   | 40      | 1532  | 26    | 3.65   |
| Toshiba   | MG04ACA600EY       | 6 TB   | 2       | 1330  | 0     | 3.65   |
| Seagate   | ST33000650NS       | 3 TB   | 25      | 2246  | 60    | 3.63   |
| HGST      | HDN721010ALE604    | 10 TB  | 2       | 1317  | 0     | 3.61   |
| WDC       | WD10EZRX-00L4HB0   | 1 TB   | 6       | 1316  | 0     | 3.61   |
| WDC       | WD5003AZEX-00S3DA0 | 500 GB | 24      | 1316  | 0     | 3.61   |
| Seagate   | ST1000VX000-1ES162 | 1 TB   | 2       | 1315  | 0     | 3.60   |
| Seagate   | ST6000VX0023-2E... | 6 TB   | 17      | 1389  | 4     | 3.60   |
| Toshiba   | MK1661GSYG         | 160 GB | 8       | 1313  | 0     | 3.60   |
| Seagate   | ST1000DM003-1CH162 | 1 TB   | 22      | 1448  | 307   | 3.59   |
| Seagate   | ST8000DM002-1YW112 | 8 TB   | 142     | 1433  | 13    | 3.58   |
| Hitachi   | HDS721010CLA330    | 1 TB   | 2       | 2113  | 3     | 3.58   |
| Seagate   | ST2000NM0033-9Z... | 2 TB   | 97      | 1704  | 124   | 3.57   |
| WDC       | WD5003ABYX-01WERA0 | 500 GB | 20      | 1619  | 2     | 3.56   |
| Hitachi   | HUA722010CLA630    | 1 TB   | 14      | 1703  | 83    | 3.54   |
| HGST      | HUS722T1TALA600    | 1 TB   | 31      | 1288  | 0     | 3.53   |
| Hitachi   | HUA722020ALA331    | 2 TB   | 10      | 2391  | 203   | 3.53   |
| WDC       | WD1001FALS-00J7B0  | 1 TB   | 2       | 2317  | 4     | 3.53   |
| Seagate   | ST9500620NS        | 500 GB | 27      | 1465  | 1     | 3.51   |
| WDC       | WD1003FZEX-00MK2A0 | 1 TB   | 96      | 1390  | 13    | 3.50   |
| Hitachi   | HDS723030BLE640    | 3 TB   | 5       | 1896  | 166   | 3.49   |
| WDC       | WD101KRYZ-01JPDB1  | 10 TB  | 13      | 1378  | 89    | 3.49   |
| Toshiba   | MG04ACA200EY       | 2 TB   | 11      | 1376  | 1     | 3.47   |
| WDC       | WD5000BPKX-22HPJT0 | 500 GB | 5       | 1483  | 2     | 3.46   |
| WDC       | WD10EFRX-68JCSN0   | 1 TB   | 7       | 2296  | 3     | 3.43   |
| Seagate   | ST8000NM0205-2F... | 8 TB   | 31      | 1361  | 66    | 3.43   |
| WDC       | WD82PURZ-85TEUY0   | 8 TB   | 19      | 1250  | 0     | 3.43   |
| WDC       | WD6002FRYZ-01WD5B1 | 6 TB   | 45      | 1250  | 20    | 3.42   |
| WDC       | WD1002F9YZ-09H1JL1 | 1 TB   | 14      | 1445  | 2     | 3.42   |
| WDC       | WD1004FBYZ-01YCBB1 | 1 TB   | 7       | 1248  | 0     | 3.42   |
| Seagate   | ST2000LM003 HN-... | 2 TB   | 16      | 1381  | 1     | 3.42   |
| WDC       | WD10EZEX-00BN5A0   | 1 TB   | 8       | 1242  | 0     | 3.41   |
| WDC       | WD30PURX-64P6ZY0   | 3 TB   | 2       | 1237  | 0     | 3.39   |
| WDC       | WD4002FYYZ-01B7CB0 | 4 TB   | 65      | 1458  | 7     | 3.38   |
| HGST      | HUH728060ALE600    | 6 TB   | 3       | 1231  | 0     | 3.37   |
| Samsung   | HD103SJ            | 1 TB   | 23      | 2135  | 4     | 3.37   |
| Hitachi   | HDS722020ALA330... | 2 TB   | 34      | 1804  | 29    | 3.34   |
| Maxtor    | STM3500630AS       | 500 GB | 2       | 1214  | 0     | 3.33   |
| WDC       | WD10JFCX-68N6GN0   | 1 TB   | 27      | 1263  | 1     | 3.33   |
| WDC       | WD4000FYYZ-01UL1B2 | 4 TB   | 29      | 2036  | 95    | 3.32   |
| Samsung   | HD154UI            | 1.5 TB | 6       | 3422  | 188   | 3.32   |
| WDC       | WD5000AAKX-221CA1  | 500 GB | 2       | 1201  | 0     | 3.29   |
| Samsung   | HD161GJ            | 160 GB | 3       | 1200  | 0     | 3.29   |
| WDC       | WD4004FZWX-00GBGB0 | 4 TB   | 22      | 1337  | 6     | 3.28   |
| Seagate   | ST6000NM0235-2A... | 6 TB   | 9       | 1196  | 0     | 3.28   |
| HGST      | HUS726020ALE610    | 2 TB   | 11      | 1195  | 0     | 3.28   |
| WDC       | WD20EZRX-00D8PB0   | 2 TB   | 10      | 1277  | 1     | 3.27   |
| Seagate   | ST4000VX000-1F4168 | 4 TB   | 4       | 1182  | 0     | 3.24   |
| WDC       | WD1003FBYZ-010FB0  | 1 TB   | 69      | 1232  | 1     | 3.22   |
| Seagate   | ST2000VN0001-1S... | 2 TB   | 4       | 1167  | 0     | 3.20   |
| HPE       | MB0500GCEHE        | 500 GB | 6       | 1160  | 0     | 3.18   |
| WDC       | WD5000BMVW-11AJGS4 | 500 GB | 4       | 1157  | 0     | 3.17   |
| WDC       | WD5000AAKX-60U6AA0 | 500 GB | 5       | 1426  | 204   | 3.17   |
| WDC       | WD10EALS-00Z8A0    | 1 TB   | 7       | 2354  | 5     | 3.14   |
| WDC       | WD5000LPLX-00ZNTT0 | 500 GB | 2       | 1146  | 0     | 3.14   |
| HGST      | HUH721008ALE601    | 8 TB   | 6       | 1139  | 0     | 3.12   |
| WDC       | WD3000HLHX-01JJPV0 | 304 GB | 6       | 1452  | 2     | 3.11   |
| Hitachi   | HDS721050CLA362    | 500 GB | 6       | 1905  | 459   | 3.10   |
| WDC       | WD10JPLX-00MBPT0   | 1 TB   | 4       | 1130  | 0     | 3.10   |
| Seagate   | ST1000NM0011       | 1 TB   | 30      | 1707  | 77    | 3.09   |
| WDC       | WD40EZRZ-00WN9B0   | 4 TB   | 20      | 1326  | 12    | 3.09   |
| WDC       | WD5000HHTZ-04N21V1 | 500 GB | 3       | 1128  | 0     | 3.09   |
| WDC       | WD5003ABYX-18WERA0 | 500 GB | 17      | 1352  | 1     | 3.09   |
| Seagate   | ST3250310AS        | 250 GB | 3       | 2275  | 209   | 3.08   |
| Toshiba   | DT01ACA200         | 2 TB   | 294     | 1179  | 18    | 3.08   |
| HGST      | HUS726060ALE610    | 6 TB   | 34      | 1123  | 0     | 3.08   |
| HGST      | HUS726040ALA614    | 4 TB   | 20      | 1253  | 4     | 3.08   |
| Seagate   | ST2000DL003-9VT166 | 2 TB   | 8       | 1655  | 274   | 3.07   |
| Seagate   | ST1000NM0055-1V... | 1 TB   | 43      | 1234  | 1     | 3.05   |
| HGST      | HUS726040ALE610    | 4 TB   | 24      | 1112  | 0     | 3.05   |
| WDC       | WD3000FYYZ-01UL1B2 | 3 TB   | 10      | 1724  | 3     | 3.05   |
| WDC       | WD30EFRX-68N32N0   | 3 TB   | 4       | 1105  | 0     | 3.03   |
| WDC       | WD1003FBYX-12      | 1 TB   | 29      | 1177  | 1     | 3.01   |
| WDC       | WD1003FBYX-01Y7B0  | 1 TB   | 45      | 1738  | 12    | 3.00   |
| WDC       | WD2003FYYS-27Y2P0  | 2 TB   | 2       | 1602  | 2     | 3.00   |
| WDC       | WD10EZEX-60WN4A0   | 1 TB   | 2       | 1094  | 0     | 3.00   |
| WDC       | WD5000AAKX-083CA1  | 500 GB | 2       | 1775  | 4     | 3.00   |
| WDC       | WD80EFZX-68UW8N0   | 8 TB   | 23      | 1089  | 0     | 2.98   |
| WDC       | WD5000BHTZ-04JCPV1 | 500 GB | 6       | 1084  | 0     | 2.97   |
| WDC       | WD40EFRX-68N32N0   | 4 TB   | 88      | 1194  | 1     | 2.96   |
| Seagate   | ST1000DM003-9YN162 | 1 TB   | 3       | 2428  | 732   | 2.95   |
| Seagate   | ST12000VN0007-2... | 12 TB  | 8       | 1075  | 0     | 2.95   |
| Toshiba   | MG03ACA400         | 4 TB   | 24      | 1587  | 3     | 2.94   |
| Seagate   | ST1000LM048-2E7172 | 1 TB   | 11      | 1072  | 0     | 2.94   |
| WDC       | WD2000FYYZ-01UL1B1 | 2 TB   | 42      | 1964  | 26    | 2.92   |
| WDC       | WD2003FYYS-02W0B0  | 2 TB   | 9       | 1607  | 7     | 2.91   |
| WDC       | WD5000AADS-00S9B0  | 500 GB | 6       | 2396  | 5     | 2.90   |
| WDC       | WD10EFRX-68PJCN0   | 1 TB   | 5       | 1056  | 0     | 2.89   |
| Seagate   | ST3000DM001-1ER166 | 3 TB   | 16      | 1500  | 459   | 2.88   |
| Seagate   | ST500DM002-1BD142  | 500 GB | 47      | 1495  | 46    | 2.87   |
| Toshiba   | MG03ACA200         | 2 TB   | 9       | 1285  | 224   | 2.86   |
| Toshiba   | MG04ACA400EY       | 4 TB   | 14      | 1045  | 0     | 2.86   |
| HGST      | HUH721010ALE604    | 10 TB  | 114     | 1055  | 1     | 2.86   |
| WDC       | WD10EALX-009BA0    | 1 TB   | 25      | 1783  | 68    | 2.86   |
| WDC       | WD5003ABYX-01WERA1 | 500 GB | 18      | 1236  | 1     | 2.86   |
| Hitachi   | HUS724030ALE641    | 3 TB   | 13      | 1279  | 49    | 2.85   |
| Toshiba   | HDWD120            | 2 TB   | 10      | 1035  | 0     | 2.84   |
| WDC       | WD2000FYYZ-01UL1B2 | 2 TB   | 46      | 1556  | 29    | 2.83   |
| WDC       | WD5002ABYS-02B1B0  | 500 GB | 5       | 2535  | 28    | 2.83   |
| Seagate   | ST8000AS0002-1N... | 8 TB   | 22      | 1572  | 110   | 2.81   |
| Seagate   | ST12000NM0007-2... | 12 TB  | 140     | 1077  | 12    | 2.81   |
| WDC       | WD1003FBYX-18Y7B0  | 1 TB   | 7       | 2023  | 15    | 2.81   |
| Seagate   | ST2000DM001-1CH164 | 2 TB   | 20      | 1661  | 834   | 2.80   |
| HGST      | HUS722T1TALA604    | 1 TB   | 126     | 1031  | 10    | 2.79   |
| WDC       | WD7500BPKT-75PK4T0 | 752 GB | 2       | 1112  | 1     | 2.74   |
| WDC       | WD5000AAKX-08ERMA0 | 500 GB | 4       | 1311  | 19    | 2.74   |
| HGST      | HTE721010A9E630    | 1 TB   | 2       | 1867  | 8     | 2.74   |
| WDC       | WD8002FRYZ-01FF2B0 | 8 TB   | 14      | 1029  | 1     | 2.73   |
| WDC       | WD5003AZEX-00MK2A0 | 500 GB | 11      | 995   | 0     | 2.73   |
| Samsung   | HD204UI            | 2 TB   | 3       | 1908  | 3     | 2.72   |
| WDC       | WD10EZEX-60M2NA0   | 1 TB   | 3       | 1324  | 339   | 2.72   |
| Hitachi   | HDS721032CLA362    | 320 GB | 3       | 1673  | 571   | 2.72   |
| WDC       | WD2000F9YZ-09N20L1 | 2 TB   | 4       | 991   | 0     | 2.72   |
| WDC       | WD1502FAEX-007BA0  | 1.5 TB | 2       | 1534  | 5     | 2.72   |
| Seagate   | ST1000DM003-1SB10C | 1 TB   | 6       | 1257  | 1     | 2.71   |
| Samsung   | HD322HJ            | 320 GB | 2       | 2738  | 508   | 2.71   |
| Seagate   | ST2000DM001-9YN164 | 2 TB   | 4       | 2351  | 260   | 2.67   |
| WDC       | WD3003FZEX-00Z4SA0 | 3 TB   | 8       | 972   | 0     | 2.66   |
| WDC       | WD5000AAKX-001CA0  | 500 GB | 6       | 1588  | 1     | 2.66   |
| Hitachi   | HDP725025GLA380    | 250 GB | 2       | 4565  | 6     | 2.65   |
| Seagate   | ST1000DX001-1NS162 | 1 TB   | 6       | 1744  | 219   | 2.64   |
| Toshiba   | HDWD105            | 500 GB | 5       | 964   | 0     | 2.64   |
| WDC       | WD10EZEX-75WN4A0   | 1 TB   | 7       | 986   | 42    | 2.63   |
| WDC       | WD10EZEX-22MFCA0   | 1 TB   | 2       | 958   | 0     | 2.63   |
| Toshiba   | DT01ACA050         | 500 GB | 22      | 1082  | 111   | 2.62   |
| WDC       | WD2003FZEX-00Z4SA0 | 2 TB   | 16      | 1110  | 1     | 2.60   |
| Seagate   | ST380815AS         | 80 GB  | 5       | 944   | 0     | 2.59   |
| WDC       | WD4002FYYZ-01B7CB1 | 4 TB   | 48      | 996   | 4     | 2.56   |
| Seagate   | ST3500413AS        | 500 GB | 6       | 1417  | 180   | 2.56   |
| WDC       | WD60EFRX-68MYMN1   | 6 TB   | 34      | 2045  | 22    | 2.55   |
| Seagate   | ST2000NM0125-1Y... | 2 TB   | 13      | 930   | 0     | 2.55   |
| WDC       | WD20EFRX-68EUZN0   | 2 TB   | 51      | 1222  | 10    | 2.54   |
| WDC       | WD10EARS-00Y5B1    | 1 TB   | 5       | 1709  | 557   | 2.54   |
| Seagate   | ST10000NM0196-2... | 10 TB  | 210     | 1028  | 42    | 2.53   |
| WDC       | WD5000AAKX-00ERMA0 | 500 GB | 10      | 1178  | 2     | 2.53   |
| WDC       | WD1005FBYZ-01YCBB2 | 1 TB   | 23      | 968   | 1     | 2.52   |
| HGST      | HUH721212ALN604    | 12 TB  | 2142    | 967   | 2     | 2.52   |
| HGST      | HUS726020ALA610    | 2 TB   | 155     | 976   | 16    | 2.52   |
| Seagate   | ST12000DM0007-2... | 12 TB  | 5       | 919   | 0     | 2.52   |
| Seagate   | ST6000VN0033-2E... | 6 TB   | 3       | 917   | 0     | 2.51   |
| HGST      | HUS726040ALA610    | 4 TB   | 82      | 940   | 1     | 2.50   |
| HGST      | HUS726060ALA640    | 6 TB   | 46      | 952   | 1     | 2.47   |
| WDC       | WD10EZEX-21M2NA0   | 1 TB   | 2       | 899   | 0     | 2.46   |
| Seagate   | ST10000VN0004-2... | 10 TB  | 4       | 1178  | 10    | 2.46   |
| Toshiba   | HDWT140            | 4 TB   | 2       | 890   | 0     | 2.44   |
| WDC       | WD2000FYYZ-05UL1B0 | 2 TB   | 11      | 927   | 1     | 2.42   |
| HPE       | MM1000GBKAL        | 1 TB   | 21      | 1253  | 56    | 2.42   |
| HGST      | HUH721010ALN600    | 10 TB  | 16      | 882   | 0     | 2.42   |
| WDC       | WD5000AAKX-08U6AA0 | 500 GB | 6       | 879   | 0     | 2.41   |
| WDC       | WD100EFAX-68LHPN0  | 10 TB  | 53      | 893   | 1     | 2.40   |
| WDC       | WD5003AZEX-00K3CA0 | 500 GB | 3       | 874   | 0     | 2.40   |
| WDC       | WD40EZRZ-22GXCB0   | 4 TB   | 16      | 871   | 0     | 2.39   |
| Seagate   | ST3160811AS        | 160 GB | 2       | 1240  | 5     | 2.38   |
| Samsung   | HD103SI            | 1 TB   | 3       | 3356  | 806   | 2.38   |
| Toshiba   | HDWR21C            | 12 TB  | 5       | 868   | 0     | 2.38   |
| Hitachi   | HUS724040ALE640    | 4 TB   | 29      | 946   | 1     | 2.36   |
| Seagate   | ST1000DM005 HD1... | 1 TB   | 4       | 2010  | 4     | 2.36   |
| HPE       | MM1000GFJTE        | 1 TB   | 4       | 862   | 0     | 2.36   |
| Seagate   | ST10000NM0016-1... | 10 TB  | 1567    | 1472  | 88    | 2.36   |
| WDC       | WD1003FZEX-00K3CA0 | 1 TB   | 208     | 887   | 3     | 2.35   |
| HGST      | HUH728060ALE604    | 6 TB   | 14      | 1278  | 28    | 2.34   |
| Seagate   | ST2000DM006-2DM164 | 2 TB   | 42      | 884   | 26    | 2.34   |
| HGST      | HUS726T4TALN6L4    | 4 TB   | 20      | 911   | 2     | 2.33   |
| Seagate   | ST4000NM0035-1V... | 4 TB   | 197     | 928   | 16    | 2.33   |
| WDC       | WD1005FBYZ-01YCBB1 | 1 TB   | 3       | 1063  | 1     | 2.33   |
| WDC       | WD50EFRX-68L0BN1   | 5 TB   | 6       | 1559  | 118   | 2.32   |
| Seagate   | ST10000DM0004-2... | 10 TB  | 7       | 1130  | 87    | 2.31   |
| Toshiba   | MG04ACA400E        | 4 TB   | 94      | 871   | 29    | 2.29   |
| WDC       | WD4000FYYZ-01UL1B3 | 4 TB   | 24      | 1218  | 17    | 2.28   |
| Toshiba   | MG04ACA400NY       | 4 TB   | 5       | 832   | 0     | 2.28   |
| WDC       | WD2005FBYZ-01YCBB2 | 2 TB   | 43      | 840   | 44    | 2.26   |
| Seagate   | ST3300831AS        | 304 GB | 2       | 1236  | 1     | 2.26   |
| HPE       | MB0500EBNCR        | 500 GB | 5       | 1520  | 18    | 2.26   |
| Seagate   | ST1000VN002-2EY102 | 1 TB   | 4       | 823   | 0     | 2.26   |
| HGST      | HUS722T2TALA604    | 2 TB   | 88      | 837   | 1     | 2.25   |
| WDC       | WD10EZRX-00D8PB0   | 1 TB   | 3       | 818   | 0     | 2.24   |
| Seagate   | ST1000NM0008-2F... | 1 TB   | 63      | 814   | 0     | 2.23   |
| Seagate   | ST1000VX005-2EZ102 | 1 TB   | 3       | 811   | 0     | 2.22   |
| WDC       | WD4005FZBX-00K5WB0 | 4 TB   | 10      | 810   | 0     | 2.22   |
| Toshiba   | MG05ACA800E        | 8 TB   | 677     | 850   | 4     | 2.22   |
| WDC       | WD2003FZEX-00SRLA0 | 2 TB   | 69      | 819   | 1     | 2.22   |
| HGST      | HUS726T6TALE6L4    | 6 TB   | 199     | 821   | 21    | 2.22   |
| HP        | MB2000GCEHK        | 2 TB   | 2       | 1625  | 1051  | 2.20   |
| HP        | MB2000GCWDA        | 2 TB   | 2       | 802   | 0     | 2.20   |
| Seagate   | ST14000VN0008-2... | 14 TB  | 12      | 868   | 2     | 2.19   |
| WDC       | WD30PURZ-85GU6Y0   | 3 TB   | 2       | 796   | 0     | 2.18   |
| Seagate   | ST2000NX0423       | 2 TB   | 60      | 803   | 1     | 2.18   |
| WDC       | WD5000AZLX-08K2TA0 | 500 GB | 5       | 790   | 0     | 2.17   |
| HGST      | HUH721212ALE604    | 12 TB  | 183     | 792   | 1     | 2.15   |
| WDC       | WD2000F9YZ-09N20L0 | 2 TB   | 2       | 1354  | 3     | 2.15   |
| Seagate   | ST3500418AS        | 500 GB | 7       | 789   | 2     | 2.15   |
| Seagate   | ST2000NM0008-2F... | 2 TB   | 74      | 805   | 71    | 2.14   |
| Seagate   | ST8000VN0022-2E... | 8 TB   | 27      | 781   | 39    | 2.14   |
| Seagate   | ST1000DM003-1SB102 | 1 TB   | 9       | 999   | 16    | 2.13   |
| Seagate   | ST1000LM024 HN-... | 1 TB   | 3       | 1172  | 4     | 2.12   |
| WDC       | WD40EZRZ-75GXCB0   | 4 TB   | 3       | 771   | 0     | 2.11   |
| Seagate   | ST16000NE000-2R... | 16 TB  | 2       | 769   | 0     | 2.11   |
| Seagate   | ST4000NM0115-1Y... | 4 TB   | 87      | 780   | 1     | 2.11   |
| Toshiba   | MD04ACA400         | 4 TB   | 452     | 782   | 3     | 2.10   |
| HGST      | HUH721212ALN600    | 12 TB  | 12      | 1080  | 22    | 2.09   |
| Seagate   | ST10000VN0004-1... | 10 TB  | 36      | 991   | 107   | 2.09   |
| WDC       | WD10EZEX-00WN4A0   | 1 TB   | 9       | 763   | 0     | 2.09   |
| Hitachi   | HDE721050SLA330    | 500 GB | 2       | 3797  | 4     | 2.08   |
| Seagate   | ST6000DM003-2CY186 | 6 TB   | 3       | 750   | 0     | 2.06   |
| MediaMax  | WL4000GSA6472      | 4 TB   | 2       | 747   | 0     | 2.05   |
| Seagate   | ST32000645NS       | 2 TB   | 88      | 797   | 15    | 2.01   |
| Seagate   | ST3500312CS        | 500 GB | 10      | 1001  | 3     | 2.01   |
| WDC       | WD10EZEX-60ZF5A0   | 1 TB   | 6       | 1860  | 13    | 2.00   |
| Seagate   | ST4000NC001-1FS168 | 4 TB   | 6       | 722   | 0     | 1.98   |
| WDC       | WD10EFRX-68FYTN0   | 1 TB   | 24      | 947   | 2     | 1.98   |
| WDC       | WD8003FFBX-68B9AN0 | 8 TB   | 3       | 719   | 0     | 1.97   |
| WDC       | WD5000AZLX-35K2TA0 | 500 GB | 3       | 717   | 0     | 1.97   |
| HPE       | MM2000GEFRA        | 2 TB   | 266     | 767   | 1     | 1.96   |
| Toshiba   | HDWU130            | 3 TB   | 8       | 800   | 8     | 1.94   |
| HGST      | HUH721010ALE600    | 10 TB  | 220     | 717   | 1     | 1.94   |
| Seagate   | ST2000LM007-1R8174 | 2 TB   | 39      | 1006  | 222   | 1.94   |
| Seagate   | ST4000LM024-2AN17V | 4 TB   | 50      | 759   | 18    | 1.93   |
| WDC       | WD5000LPCX-24VHAT0 | 500 GB | 4       | 704   | 0     | 1.93   |
| Seagate   | ST12000NM0017-2... | 12 TB  | 2       | 704   | 0     | 1.93   |
| Seagate   | ST10000NM0156-2... | 10 TB  | 37      | 780   | 6     | 1.92   |
| WDC       | WD2002FFSX-68PF8N0 | 2 TB   | 13      | 696   | 0     | 1.91   |
| Toshiba   | MG06ACA10TEY       | 10 TB  | 72      | 718   | 1     | 1.89   |
| Seagate   | ST10000NM0086-2... | 10 TB  | 110     | 786   | 20    | 1.88   |
| Seagate   | ST4000NM0245-1Z... | 4 TB   | 32      | 948   | 20    | 1.88   |
| HGST      | HTS721010A9E630    | 1 TB   | 7       | 1273  | 721   | 1.87   |
| Toshiba   | HDWE140            | 4 TB   | 43      | 698   | 42    | 1.86   |
| WDC       | WD4000F9YZ-09N20L0 | 4 TB   | 5       | 668   | 0     | 1.83   |
| Seagate   | ST2000LM015-2E8174 | 2 TB   | 18      | 802   | 111   | 1.83   |
| WDC       | WD40EZRZ-00GXCB0   | 4 TB   | 49      | 702   | 24    | 1.82   |
| Seagate   | ST6000NM0115-1Y... | 6 TB   | 174     | 721   | 11    | 1.82   |
| WDC       | WD30EZRZ-00Z5HB0   | 3 TB   | 8       | 695   | 1     | 1.81   |
| Seagate   | ST9500420ASG       | 500 GB | 6       | 1420  | 184   | 1.81   |
| WDC       | WD15EARS-00MVWB0   | 1.5 TB | 4       | 2054  | 324   | 1.81   |
| Seagate   | ST2000NX0253       | 2 TB   | 49      | 857   | 16    | 1.80   |
| Toshiba   | MQ01ACF050         | 500 GB | 6       | 876   | 2     | 1.80   |
| Seagate   | ST2000VX003-1HH164 | 2 TB   | 3       | 652   | 0     | 1.79   |
| Toshiba   | MG07ACA12TEY       | 12 TB  | 52      | 662   | 2     | 1.78   |
| WDC       | WD80EFAX-68KNBN0   | 8 TB   | 6       | 648   | 0     | 1.78   |
| Hitachi   | HDE721010SLA330    | 1 TB   | 4       | 2029  | 3     | 1.78   |
| Hitachi   | HDS723030ALA640... | 3 TB   | 2       | 975   | 1     | 1.77   |
| Western   | WUH721818ALE6L4    | 18 TB  | 2       | 643   | 0     | 1.76   |
| HGST      | HUS726T4TALE6L4    | 4 TB   | 70      | 645   | 1     | 1.74   |
| WDC       | WD40EFAX-68JH4N0   | 4 TB   | 39      | 663   | 1     | 1.73   |
| Seagate   | ST10000NM0568-2... | 10 TB  | 36      | 653   | 6     | 1.73   |
| Seagate   | ST2000NM0055-1V... | 2 TB   | 22      | 866   | 1     | 1.73   |
| Seagate   | ST1000DL002-9TT153 | 1 TB   | 2       | 1021  | 509   | 1.72   |
| WDC       | WD121KRYZ-01W0RB0  | 12 TB  | 9       | 818   | 1     | 1.72   |
| WDC       | WD4000FYYZ-01UL1B1 | 4 TB   | 10      | 1743  | 5     | 1.72   |
| WDC       | WD3000FYYZ-01UL1B3 | 3 TB   | 5       | 624   | 0     | 1.71   |
| HP        | MB2000EAZNL        | 2 TB   | 2       | 800   | 2     | 1.71   |
| Toshiba   | MG07ACA14TE        | 14 TB  | 88      | 637   | 1     | 1.69   |
| Seagate   | ST3250318AS        | 250 GB | 4       | 1245  | 19    | 1.69   |
| Toshiba   | HDWD130            | 3 TB   | 9       | 630   | 2     | 1.68   |
| Seagate   | ST3000DM007-1WY10G | 3 TB   | 3       | 612   | 0     | 1.68   |
| Seagate   | ST4000LM016-1N2170 | 4 TB   | 3       | 609   | 0     | 1.67   |
| WDC       | WD5000AZLX-22JKKA0 | 500 GB | 3       | 953   | 3     | 1.66   |
| WDC       | WD10EURX-63UY4Y0   | 1 TB   | 2       | 606   | 0     | 1.66   |
| WDC       | WD4003FFBX-68MU3N0 | 4 TB   | 37      | 601   | 0     | 1.65   |
| Seagate   | ST8000DM0004-1Z... | 8 TB   | 10      | 1045  | 317   | 1.65   |
| HGST      | HUH721008ALE600    | 8 TB   | 70      | 600   | 0     | 1.64   |
| Seagate   | ST12000NM0008-2... | 12 TB  | 165     | 605   | 4     | 1.64   |
| WDC       | WD10EZEX-08WN4A0   | 1 TB   | 38      | 624   | 2     | 1.63   |
| Seagate   | ST3500514NS        | 500 GB | 4       | 1274  | 10    | 1.62   |
| WDC       | WD121KFBX-68EF5N0  | 12 TB  | 7       | 586   | 0     | 1.61   |
| HGST      | HUS728T8TALE6L0    | 8 TB   | 15      | 585   | 0     | 1.60   |
| Seagate   | ST1000NX0423       | 1 TB   | 3       | 835   | 12    | 1.60   |
| Seagate   | ST3000VX010-2E3166 | 3 TB   | 5       | 691   | 4     | 1.60   |
| Toshiba   | HDWL120            | 2 TB   | 12      | 668   | 1     | 1.59   |
| Seagate   | ST10000NE0004-1... | 10 TB  | 15      | 1277  | 376   | 1.58   |
| Toshiba   | HDWN160            | 6 TB   | 11      | 685   | 2     | 1.57   |
| HGST      | HUH721008ALE604    | 8 TB   | 22      | 572   | 0     | 1.57   |
| Toshiba   | MG06ACA10TE        | 10 TB  | 176     | 579   | 1     | 1.56   |
| Toshiba   | MG06ACA600E        | 6 TB   | 10      | 569   | 0     | 1.56   |
| WDC       | WUH721414ALE604    | 14 TB  | 2111    | 576   | 1     | 1.56   |
| Seagate   | ST32000644NS       | 2 TB   | 12      | 998   | 21    | 1.55   |
| WDC       | WD10EZRZ-00HTKB0   | 1 TB   | 3       | 564   | 0     | 1.55   |
| HPE       | MB004000GWFWB      | 4 TB   | 15      | 564   | 0     | 1.55   |
| WDC       | WD60PURZ-85ZUFY1   | 6 TB   | 6       | 563   | 0     | 1.54   |
| WDC       | WD4003FRYZ-01F0DB0 | 4 TB   | 29      | 562   | 0     | 1.54   |
| Seagate   | ST8000VX0022-2E... | 8 TB   | 4       | 758   | 9     | 1.52   |
| WDC       | WD101EFAX-68LDBN0  | 10 TB  | 10      | 553   | 0     | 1.52   |
| Seagate   | ST8000DM004-2CX188 | 8 TB   | 20      | 646   | 18    | 1.51   |
| HGST      | HTS725050A7E630    | 500 GB | 6       | 844   | 508   | 1.50   |
| WDC       | WD60EFRX-68L0BN1   | 6 TB   | 193     | 1222  | 7     | 1.50   |
| WDC       | WD2003FYYS-05T9B0  | 2 TB   | 4       | 604   | 1     | 1.50   |
| WDC       | WD50EFRX-68MYMN1   | 5 TB   | 2       | 2167  | 4     | 1.49   |
| HGST      | HDN728080ALE604    | 8 TB   | 2       | 850   | 16    | 1.48   |
| Seagate   | ST2000NM0011       | 2 TB   | 15      | 1638  | 136   | 1.48   |
| Seagate   | ST10000VE0008-2... | 10 TB  | 4       | 538   | 0     | 1.48   |
| Seagate   | ST10000VN0008-2... | 10 TB  | 25      | 529   | 0     | 1.45   |
| Hitachi   | HUS724040ALE641    | 4 TB   | 17      | 686   | 61    | 1.44   |
| Seagate   | ST2000LX001-1RG174 | 2 TB   | 4       | 518   | 0     | 1.42   |
| HPE       | MB012000GWDFE      | 12 TB  | 36      | 523   | 1     | 1.40   |
| WDC       | WD8003FRYZ-01JPDB1 | 8 TB   | 5       | 510   | 0     | 1.40   |
| Toshiba   | MG03ACA300         | 3 TB   | 2       | 919   | 6     | 1.39   |
| HGST      | HUS726T4TALA6L4    | 4 TB   | 143     | 514   | 5     | 1.38   |
| HGST      | HUS728T8TALE6L4    | 8 TB   | 83      | 507   | 1     | 1.38   |
| WDC       | WUH722020ALE604    | 20 TB  | 106     | 500   | 0     | 1.37   |
| Seagate   | ST3750640NS        | 752 GB | 13      | 1310  | 859   | 1.37   |
| WDC       | WUH722020BLE604    | 20 TB  | 54      | 500   | 0     | 1.37   |
| Seagate   | ST320LT007-9ZV142  | 320 GB | 2       | 498   | 0     | 1.37   |
| WDC       | WD10JPVX-08JC3T5   | 1 TB   | 2       | 490   | 0     | 1.34   |
| HGST      | HUH721212ALE600    | 12 TB  | 125     | 487   | 0     | 1.33   |
| WDC       | WD10EZEX-75WN4A1   | 1 TB   | 2       | 486   | 0     | 1.33   |
| WDC       | WD40EZAZ-00ZGHB0   | 4 TB   | 2       | 483   | 0     | 1.32   |
| WDC       | WD5000LPVX-22V0TT0 | 500 GB | 4       | 480   | 0     | 1.32   |
| Seagate   | ST1000NX0313       | 1 TB   | 60      | 984   | 14    | 1.31   |
| WDC       | WD60EFAX-68SHWN0   | 6 TB   | 4       | 578   | 1     | 1.31   |
| Seagate   | ST4000NM000A-2H... | 4 TB   | 46      | 495   | 1     | 1.28   |
| Toshiba   | HDWD110            | 1 TB   | 89      | 478   | 41    | 1.27   |
| Seagate   | ST500LT012-1DG142  | 500 GB | 6       | 463   | 0     | 1.27   |
| Toshiba   | MG04ACA200E        | 2 TB   | 38      | 445   | 0     | 1.22   |
| WDC       | WD141KFGX-68FH9N0  | 14 TB  | 12      | 443   | 0     | 1.21   |
| Toshiba   | MG07ACA12TE        | 12 TB  | 139     | 451   | 1     | 1.21   |
| Seagate   | ST2000DM008-2UB102 | 2 TB   | 5       | 438   | 0     | 1.20   |
| Seagate   | ST1000DM010-2EP102 | 1 TB   | 76      | 538   | 36    | 1.20   |
| WDC       | WD5000AAKS-00UU3A0 | 500 GB | 2       | 1740  | 4     | 1.19   |
| HGST      | HUS726T4TALA6L1    | 4 TB   | 84      | 447   | 1     | 1.19   |
| Toshiba   | HDWQ140            | 4 TB   | 11      | 434   | 0     | 1.19   |
| WDC       | WD6003FZBX-00GXAB0 | 6 TB   | 7       | 428   | 0     | 1.17   |
| Samsung   | HD080HJ            | 80 GB  | 2       | 1964  | 841   | 1.17   |
| Seagate   | ST8000VN004-2M2101 | 8 TB   | 203     | 453   | 52    | 1.17   |
| Seagate   | ST2000DX002-2DV164 | 2 TB   | 4       | 424   | 0     | 1.16   |
| WDC       | WD60EZRZ-00GZ5B1   | 6 TB   | 2       | 424   | 0     | 1.16   |
| Seagate   | ST1000NM0011 99... | 1 TB   | 2       | 1210  | 3     | 1.16   |
| Toshiba   | MG04ACA200N        | 2 TB   | 5       | 467   | 1     | 1.16   |

HDD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| Hitachi     | 37     | 552     | 2372  | 76    | 5.25   |
| Maxtor      | 4      | 8       | 1884  | 155   | 5.03   |
| HP          | 17     | 41      | 2288  | 208   | 4.16   |
| Samsung     | 11     | 78      | 2594  | 187   | 3.63   |
| Seagate     | 212    | 10297   | 1289  | 48    | 2.82   |
| HGST        | 58     | 5287    | 1061  | 7     | 2.77   |
| Toshiba     | 66     | 3890    | 979   | 12    | 2.52   |
| MediaMax    | 1      | 2       | 747   | 0     | 2.05   |
| Western     | 1      | 2       | 643   | 0     | 1.76   |
| WDC         | 270    | 9234    | 765   | 7     | 1.76   |
| HPE         | 11     | 492     | 637   | 7     | 1.60   |

SSD by Model
------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested SSD samples in the Appendix 2 ([All_SSD.md](/All_SSD.md)).

See top 1000 of tested SSD models in the [Top1000_SSD.md](/Top1000_SSD.md).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Intel     | SSDSA2SH032G1GN    | 32 GB  | 3       | 3167  | 0     | 8.68   |
| Micron    | MTFDDAK512MAR-1... | 512 GB | 3       | 3088  | 0     | 8.46   |
| Intel     | SSDSC2BX012T4      | 1.2 TB | 4       | 2821  | 0     | 7.73   |
| Samsung   | SSD 840 EVO        | 120 GB | 11      | 2574  | 0     | 7.05   |
| Apple     | SSD SM256E         | 256 GB | 2       | 2543  | 0     | 6.97   |
| Micron    | MTFDDAK128MAR-1... | 128 GB | 3       | 2373  | 0     | 6.50   |
| Intel     | VR0120GEJXL        | 120 GB | 3       | 2370  | 0     | 6.49   |
| Samsung   | SSD 840 EVO        | 500 GB | 13      | 3101  | 237   | 6.48   |
| Intel     | SSDSC2BP240G4      | 240 GB | 11      | 2343  | 0     | 6.42   |
| Intel     | SSDSA2CW120G3      | 120 GB | 41      | 2901  | 53    | 6.34   |
| Samsung   | MZ7LM120HCFD-00003 | 120 GB | 4       | 2312  | 0     | 6.34   |
| Samsung   | SSD 830 Series     | 512 GB | 12      | 3084  | 253   | 6.33   |
| Intel     | SSDSC2CW240A3      | 240 GB | 55      | 2463  | 1     | 6.32   |
| Samsung   | MZ7LM240HCGR-00003 | 240 GB | 4       | 2292  | 0     | 6.28   |
| Samsung   | MZ7LM480HCHP-0E003 | 480 GB | 7       | 2231  | 0     | 6.11   |
| Intel     | SSDSC2BA100G3      | 100 GB | 28      | 2321  | 1     | 6.05   |
| Intel     | SSDSC2BB080G4      | 80 GB  | 4       | 2192  | 0     | 6.01   |
| Toshiba   | THNSNJ120PCSZ      | 120 GB | 2       | 2176  | 0     | 5.96   |
| Micron    | P400e-MTFDDAK40... | 400 GB | 3       | 2157  | 0     | 5.91   |
| Samsung   | SSD 850 PRO        | 128 GB | 7       | 2133  | 0     | 5.85   |
| Samsung   | SSD 850 PRO        | 1 TB   | 92      | 2609  | 5     | 5.80   |
| Intel     | SSDSC2BB800G4      | 800 GB | 7       | 2082  | 0     | 5.71   |
| Samsung   | MZ7KM200HAGR00D3   | 200 GB | 2       | 2082  | 0     | 5.71   |
| Samsung   | MZ7WD480HAGM-00003 | 480 GB | 9       | 2063  | 0     | 5.65   |
| Crucial   | M4-CT128M4SSD2     | 128 GB | 2       | 2008  | 0     | 5.50   |
| Intel     | SSDSC2BB300G4      | 304 GB | 18      | 1985  | 0     | 5.44   |
| Micron    | MTFDDAK128MAM-1J1  | 128 GB | 4       | 1983  | 0     | 5.43   |
| Micron    | MTFDDAK256MAR-1... | 256 GB | 3       | 2622  | 1     | 5.43   |
| OCZ       | VERTEX3            | 120 GB | 6       | 3237  | 4     | 5.43   |
| Samsung   | MZ7TD512HAGM-00000 | 512 GB | 4       | 2299  | 1     | 5.40   |
| Intel     | SSDSC2CW480A3      | 400 GB | 12      | 2122  | 1     | 5.38   |
| Kingston  | SE50S3480G         | 480 GB | 5       | 1952  | 0     | 5.35   |
| Intel     | SSDSA2BZ200G3      | 200 GB | 2       | 2530  | 1     | 5.32   |
| Intel     | SSDSC2BA400G3C     | 400 GB | 2       | 1937  | 0     | 5.31   |
| Intel     | SSDSC2BB480G4      | 480 GB | 60      | 2091  | 17    | 5.27   |
| Kingston  | SKC300S37A120G     | 120 GB | 2       | 1914  | 0     | 5.25   |
| Toshiba   | THNSNJ960PCSZ      | 960 GB | 42      | 1953  | 1     | 5.24   |
| Crucial   | CT250MX200SSD1     | 250 GB | 11      | 1911  | 0     | 5.24   |
| Intel     | SSDSC2CW180A3      | 180 GB | 14      | 1974  | 1     | 5.22   |
| Samsung   | MZ7WD480HCGM-00003 | 480 GB | 26      | 2050  | 70    | 5.19   |
| Micron    | M500DC_MTFDDAK1... | 120 GB | 2       | 1890  | 0     | 5.18   |
| Samsung   | MZ7LM1T9HCJM-0E003 | 1.9 TB | 2       | 1890  | 0     | 5.18   |
| Intel     | SSDSC2BB120G4      | 120 GB | 18      | 1984  | 1     | 5.15   |
| Intel     | SSDSC2BB160G4      | 160 GB | 61      | 2202  | 1     | 5.14   |
| Samsung   | MZ7LM3T8HCJM-0E003 | 3.8 TB | 9       | 1875  | 0     | 5.14   |
| Intel     | SSDSC2BA400G4      | 400 GB | 39      | 1911  | 1     | 5.10   |
| HP        | VK0240GECQN        | 240 GB | 8       | 1861  | 0     | 5.10   |
| Intel     | MK1200GEYKF        | 1.2 TB | 2       | 1852  | 0     | 5.07   |
| Samsung   | SSD 840 EVO        | 1 TB   | 26      | 2493  | 48    | 5.06   |
| SanDisk   | SDSSDXPS240G       | 240 GB | 2       | 1816  | 0     | 4.98   |
| HP        | VK0800GDJYA        | 800 GB | 32      | 1982  | 2     | 4.97   |
| Corsair   | Force 3 SSD        | 120 GB | 4       | 2396  | 1     | 4.96   |
| Intel     | SSDSC2CT120A3      | 120 GB | 16      | 2741  | 2     | 4.93   |
| Kingston  | SEDC400S371600G    | 1.6 TB | 2       | 1794  | 0     | 4.92   |
| Samsung   | MZ7WD240HAFV-000D2 | 240 GB | 7       | 2083  | 5     | 4.88   |
| Samsung   | MZ7KM960HAHP-00005 | 960 GB | 73      | 1776  | 0     | 4.87   |
| Intel     | SSDSC2BA200G3      | 200 GB | 20      | 2020  | 1     | 4.86   |
| Intel     | SSDSC2CT240A4      | 240 GB | 2       | 2646  | 1     | 4.84   |
| Intel     | SSDSC2BB120G6K     | 120 GB | 24      | 1755  | 0     | 4.81   |
| Samsung   | SSD 840 PRO Series | 128 GB | 16      | 2104  | 70    | 4.80   |
| Samsung   | MZ7LM1T9HCJM00D3   | 1.9 TB | 4       | 1744  | 0     | 4.78   |
| SanDisk   | SDLF1DAR-960G-1HA2 | 960 GB | 12      | 1744  | 0     | 4.78   |
| Intel     | SSDSC2BB240G6      | 240 GB | 21      | 1744  | 0     | 4.78   |
| SanDisk   | SDLF1DAR480G-1HHS  | 480 GB | 2       | 1734  | 0     | 4.75   |
| Intel     | SSDSC2BB800G6      | 800 GB | 68      | 1847  | 15    | 4.73   |
| Samsung   | MZ7LM480HCHP-00003 | 480 GB | 81      | 1788  | 3     | 4.72   |
| Toshiba   | THNSN8240PCSE      | 240 GB | 2       | 1717  | 0     | 4.70   |
| Samsung   | SSD 840 EVO        | 250 GB | 10      | 2674  | 5     | 4.69   |
| Samsung   | SSD 850 PRO        | 256 GB | 42      | 1765  | 1     | 4.68   |
| Intel     | SSDSC2BB016T6      | 1.6 TB | 13      | 1701  | 0     | 4.66   |
| Samsung   | MZ7KM480HAHP-00005 | 480 GB | 92      | 1694  | 0     | 4.64   |
| Crucial   | CT512MX100SSD1     | 240 GB | 4       | 2113  | 1     | 4.64   |
| Intel     | SSDSC2BA400G3      | 400 GB | 7       | 1826  | 1     | 4.63   |
| Intel     | SSDSC2BB120G6      | 120 GB | 7       | 1685  | 0     | 4.62   |
| Intel     | SSDSC2BX400G4      | 400 GB | 3       | 1684  | 0     | 4.61   |
| Samsung   | MZ7WD960HAGP-00003 | 960 GB | 3       | 1681  | 0     | 4.61   |
| Intel     | SSDSC2BB012T6      | 1.2 TB | 18      | 1792  | 1     | 4.59   |
| HP        | VK000960GWEZD      | 960 GB | 5       | 1925  | 1     | 4.57   |
| Intel     | SSDSC2BB300H4      | 304 GB | 3       | 1663  | 0     | 4.56   |
| Samsung   | SSD 850 PRO        | 512 GB | 63      | 1693  | 1     | 4.53   |
| Samsung   | MZ7WD240HCFV-00003 | 240 GB | 7       | 1653  | 0     | 4.53   |
| Toshiba   | VX500              | 1 TB   | 6       | 1649  | 0     | 4.52   |
| Micron    | M600_MTFDDAK256MBF | 256 GB | 2       | 1641  | 0     | 4.50   |
| Intel     | SSDSC2BB240G4      | 240 GB | 45      | 1712  | 1     | 4.48   |
| Samsung   | MZ7LM960HCHP-00005 | 960 GB | 24      | 1633  | 0     | 4.48   |
| Intel     | SSDSC2BB600G4      | 600 GB | 23      | 1729  | 1     | 4.47   |
| Samsung   | MZ7GE960HMHP-00003 | 960 GB | 24      | 2270  | 109   | 4.42   |
| Samsung   | MZ7KM120HAFD-00005 | 120 GB | 15      | 1612  | 0     | 4.42   |
| Samsung   | MZ7LM960HCHP-0E003 | 960 GB | 5       | 1611  | 0     | 4.42   |
| Samsung   | MZ7KM240HAGR-00005 | 240 GB | 24      | 1639  | 1     | 4.41   |
| Kingston  | SH103S3240G        | 240 GB | 2       | 2144  | 1     | 4.41   |
| Samsung   | MZ7KM120HAFD-0E005 | 120 GB | 2       | 1602  | 0     | 4.39   |
| Intel     | SSDSC2BX200G4      | 200 GB | 20      | 1599  | 0     | 4.38   |
| Kingston  | SKC300S37A240G     | 240 GB | 12      | 1573  | 0     | 4.31   |
| HPE       | MK0200GEYKC        | 200 GB | 21      | 1554  | 0     | 4.26   |
| Crucial   | CT500MX200SSD1     | 500 GB | 18      | 1553  | 0     | 4.26   |
| Samsung   | MZ7KM480HAHP-0E005 | 480 GB | 15      | 1537  | 0     | 4.21   |
| Intel     | SSDSC2BB120G7R     | 120 GB | 14      | 1527  | 0     | 4.19   |
| Intel     | SSDSC2BB480H4      | 480 GB | 9       | 1708  | 1     | 4.19   |
| Crucial   | CT750MX300SSD1     | 752 GB | 16      | 1769  | 1     | 4.18   |
| OCZ       | SABER1000          | 120 GB | 2       | 1522  | 0     | 4.17   |
| Intel     | SSDSC2BX800G4      | 800 GB | 4       | 1516  | 0     | 4.15   |
| Samsung   | SSD 840 Series     | 250 GB | 4       | 2752  | 269   | 4.12   |
| Intel     | SSDSC2BB480G6      | 480 GB | 43      | 1505  | 0     | 4.12   |
| ADATA     | SP900              | 256 GB | 2       | 2463  | 2     | 4.05   |
| Intel     | SSDSA2BW600G3D     | 600 GB | 2       | 2213  | 1     | 4.04   |
| Samsung   | SSD 840 PRO Series | 512 GB | 10      | 1984  | 64    | 4.04   |
| Intel     | SSDSC2BA200G4      | 200 GB | 156     | 1495  | 7     | 4.04   |
| Samsung   | MZ7KM960HMJP0D3    | 960 GB | 128     | 1472  | 0     | 4.03   |
| Kingston  | SH103S3120G        | 120 GB | 10      | 1601  | 1     | 4.02   |
| Crucial   | CT1024MX200SSD1    | 1 TB   | 26      | 1474  | 1     | 4.01   |
| SanDisk   | SDLF1CRR019T-1HHS  | 1.9 TB | 30      | 1485  | 34    | 3.95   |
| HPE       | MK0400GEYKD        | 400 GB | 3       | 1419  | 0     | 3.89   |
| Intel     | SSDSC2BA800G4      | 800 GB | 17      | 1415  | 0     | 3.88   |
| Kingston  | SE50S3100G         | 100 GB | 3       | 1763  | 1     | 3.87   |
| Intel     | SSDSC2BB800G7R     | 800 GB | 40      | 1767  | 53    | 3.85   |
| Kingston  | SKC400S37128G      | 128 GB | 4       | 1403  | 0     | 3.85   |
| Samsung   | MZ7LM480HMHQ-00003 | 480 GB | 8       | 1400  | 0     | 3.84   |
| Micron    | 5100_MTFDDAK240TCC | 240 GB | 6       | 1579  | 1     | 3.82   |
| SanDisk   | SD7UB2Q512G1022    | 512 GB | 7       | 1498  | 1     | 3.81   |
| Samsung   | MZ7LN512HMJP-00000 | 512 GB | 15      | 1515  | 3     | 3.80   |
| Intel     | SSDSC2BB016T4      | 1.6 TB | 5       | 1807  | 1     | 3.80   |
| SanDisk   | SDLF1CRM-017T-1HST | 1.7 TB | 4       | 1383  | 0     | 3.79   |
| Samsung   | SSD 850 EVO        | 120 GB | 15      | 1465  | 15    | 3.79   |
| Lite-On   | PH3-CE120          | 120 GB | 2       | 1376  | 0     | 3.77   |
| Kingston  | SV300S37A240G      | 240 GB | 103     | 1587  | 9     | 3.75   |
| Samsung   | SSD 850 PRO        | 2 TB   | 3       | 1359  | 0     | 3.72   |
| Samsung   | MZ7KM960HAHP-0E005 | 960 GB | 4       | 1348  | 0     | 3.70   |
| Samsung   | MZ7KM1T9HAJM-00005 | 1.9 TB | 55      | 1346  | 0     | 3.69   |
| Toshiba   | THNSN8960PCSE      | 960 GB | 36      | 1357  | 1     | 3.67   |
| Intel     | SSDSC2KB960G7R     | 960 GB | 10      | 1398  | 1     | 3.64   |
| Samsung   | SSD 840 PRO Series | 256 GB | 21      | 2635  | 251   | 3.62   |
| Samsung   | SSD 750 EVO        | 120 GB | 2       | 1304  | 0     | 3.57   |
| SanDisk   | Ultra II           | 960 GB | 12      | 1299  | 0     | 3.56   |
| Samsung   | MZ7KM240HMHQ0D3    | 240 GB | 2       | 1295  | 0     | 3.55   |
| Samsung   | MZ7GE480HMHP-00003 | 480 GB | 12      | 1995  | 165   | 3.53   |
| SK hynix  | HFS500G32TND-N1A2A | 500 GB | 2       | 1270  | 0     | 3.48   |
| Samsung   | SSD 860 EVO M.2    | 1 TB   | 4       | 1263  | 0     | 3.46   |
| Intel     | SSDSC2BA200G4C     | 200 GB | 5       | 1260  | 0     | 3.45   |
| Samsung   | MZ7LM3T8HMLP-00005 | 3.8 TB | 7       | 1247  | 0     | 3.42   |
| Intel     | SSDSC2BB150G7      | 150 GB | 16      | 1302  | 1     | 3.42   |
| Samsung   | SSD 850 EVO        | 2 TB   | 20      | 1432  | 22    | 3.42   |
| Kingston  | SUV300S37A240G     | 240 GB | 2       | 1245  | 0     | 3.41   |
| Intel     | SSDSC2BB480G7      | 480 GB | 119     | 1447  | 1     | 3.41   |
| Samsung   | SSD 850 EVO        | 500 GB | 128     | 1306  | 25    | 3.40   |
| Samsung   | MZ7LM480HCHP-00005 | 480 GB | 29      | 1229  | 0     | 3.37   |
| Samsung   | MZ7KM240HAGR-0E005 | 240 GB | 17      | 1822  | 23    | 3.37   |
| Samsung   | SSD 860 EVO M.2    | 2 TB   | 2       | 1225  | 0     | 3.36   |
| Intel     | SSDSC2BX480G4      | 480 GB | 41      | 1222  | 0     | 3.35   |
| SATADOM   | ML 3MG-P           | 32 GB  | 2       | 1215  | 0     | 3.33   |
| Dell      | SSDSCKJB120G7R     | 120 GB | 6       | 1375  | 1     | 3.25   |
| Samsung   | SSD 850 EVO M.2    | 250 GB | 2       | 1186  | 0     | 3.25   |
| Intel     | SSDSC2KB480G7K     | 480 GB | 4       | 1186  | 0     | 3.25   |
| Kingston  | SEDC400S37480G     | 480 GB | 2       | 1175  | 0     | 3.22   |
| HP        | VK003840GWSXL      | 3.8 TB | 47      | 1484  | 1     | 3.20   |
| Samsung   | SSD 850 EVO M.2    | 500 GB | 5       | 1168  | 0     | 3.20   |
| Samsung   | SSD 850 EVO        | 1 TB   | 206     | 1509  | 67    | 3.18   |
| Samsung   | MZ7LM240HCGR-00005 | 240 GB | 4       | 1125  | 0     | 3.08   |
| SanDisk   | SDLF1DAR-480G-1HA1 | 480 GB | 39      | 1124  | 0     | 3.08   |
| Samsung   | MZ7GE240HMGR-00003 | 240 GB | 4       | 1234  | 89    | 3.08   |
| Superm... | SSD                | 32 GB  | 16      | 1121  | 0     | 3.07   |
| SanDisk   | SDSSDH31000G       | 1 TB   | 13      | 1292  | 8     | 3.07   |
| HP        | VK000240GWSRQ      | 240 GB | 40      | 1120  | 0     | 3.07   |
| SanDisk   | SD6SB1M064G1022I   | 64 GB  | 6       | 1119  | 0     | 3.07   |
| Micron    | 5100_MTFDDAK960TBY | 960 GB | 4       | 1115  | 0     | 3.05   |
| Samsung   | MZ7KM240HMHQ-00005 | 240 GB | 65      | 1115  | 12    | 3.04   |
| Samsung   | MZ7KM1T9HMJP-00005 | 1.9 TB | 86      | 1103  | 0     | 3.02   |
| Superm... | SSD                | 64 GB  | 27      | 1116  | 1     | 2.99   |
| Intel     | SSDSC2BX100G4      | 100 GB | 2       | 1090  | 0     | 2.99   |
| Intel     | SSDSCKJB150G7      | 150 GB | 14      | 1238  | 1     | 2.98   |
| Samsung   | MZ7LM960HCHP-00003 | 960 GB | 33      | 1083  | 0     | 2.97   |
| Micron    | M510DC_MTFDDAK9... | 960 GB | 2       | 1985  | 4     | 2.94   |
| Samsung   | MZ7LM1T9HCJM-00003 | 1.9 TB | 7       | 1070  | 0     | 2.93   |
| Intel     | SSDSC2KG480G7      | 480 GB | 54      | 1372  | 2     | 2.91   |
| HPE       | LK0480GFJSK        | 480 GB | 5       | 1059  | 0     | 2.90   |
| SanDisk   | SD7UB2Q512G1122    | 512 GB | 8       | 1550  | 10    | 2.85   |
| Kingston  | SKC400S371T        | 1 TB   | 10      | 1037  | 0     | 2.84   |
| Samsung   | SSD 850 EVO        | 250 GB | 97      | 1165  | 40    | 2.83   |
| Kingston  | SV300S37A120G      | 120 GB | 41      | 1516  | 25    | 2.83   |
| Samsung   | MZ7LM960HMJP0D3    | 960 GB | 46      | 1073  | 1     | 2.83   |
| Toshiba   | THNSF8200CCSE      | 200 GB | 20      | 1129  | 1     | 2.82   |
| Intel     | SSDSC2BB480G7O     | 480 GB | 5       | 1624  | 3     | 2.82   |
| Samsung   | MZ7KM480HMHQ-00005 | 480 GB | 169     | 1023  | 0     | 2.80   |
| Kingston  | SKC400S37512G      | 512 GB | 5       | 1022  | 0     | 2.80   |
| Intel     | SSDSC2BA012T4      | 1.2 TB | 2       | 1019  | 0     | 2.79   |
| Kingston  | SV300S37A60G       | 64 GB  | 5       | 1678  | 2     | 2.79   |
| Micron    | MTFDDAK960TDD      | 960 GB | 14      | 1144  | 2     | 2.77   |
| Goodram   | SSD                | 240 GB | 4       | 1006  | 0     | 2.76   |
| Kingston  | SEDC400S37960G     | 960 GB | 10      | 996   | 0     | 2.73   |
| HP        | VK000240GWCNP      | 240 GB | 6       | 988   | 0     | 2.71   |
| Intel     | SSDSC2BB240G7      | 240 GB | 34      | 1010  | 1     | 2.69   |
| Samsung   | SSD 750 EVO        | 250 GB | 4       | 979   | 0     | 2.68   |
| Intel     | SSDSC2KG240G7R     | 240 GB | 26      | 1045  | 80    | 2.65   |
| Micron    | 5100_MTFDDAK480TCC | 480 GB | 21      | 1101  | 1     | 2.65   |
| Kingston  | SHFS37A480G        | 480 GB | 3       | 1412  | 4     | 2.65   |
| WDC       | WDS100T1B0A-00H9H0 | 1 TB   | 27      | 960   | 0     | 2.63   |
| HP        | VK0240GDJXU        | 240 GB | 2       | 1452  | 1     | 2.62   |
| Toshiba   | THNSF8240CCSE      | 240 GB | 10      | 952   | 0     | 2.61   |
| Samsung   | MZ7KH3T8HALS-00005 | 3.8 TB | 7       | 947   | 0     | 2.60   |
| OCZ       | ARC100             | 480 GB | 4       | 1129  | 21    | 2.59   |
| Samsung   | MZ7LM960HMJP-00005 | 960 GB | 343     | 1295  | 26    | 2.59   |
| MyDigi... | SB2                | 128 GB | 6       | 945   | 0     | 2.59   |
| HP        | VK003840GXAWP      | 3.8 TB | 24      | 1183  | 1     | 2.56   |
| Team      | T2535T120G         | 120 GB | 2       | 933   | 0     | 2.56   |
| HP        | VK000480GWSRR      | 480 GB | 4       | 932   | 0     | 2.56   |
| Samsung   | MZ7LH1T9HMLT0D3    | 1.9 TB | 35      | 930   | 0     | 2.55   |
| SanDisk   | SD8SB8U256G1122    | 256 GB | 5       | 929   | 0     | 2.55   |
| Samsung   | SSD 840 Series     | 120 GB | 7       | 1862  | 86    | 2.54   |
| HP        | VK000240GWCFD      | 240 GB | 3       | 925   | 0     | 2.53   |
| Plextor   | PH6-CE240          | 240 GB | 2       | 909   | 0     | 2.49   |
| Samsung   | SSD 860 DCT        | 960 GB | 5       | 906   | 0     | 2.48   |
| HP        | SSD M700           | 120 GB | 3       | 902   | 0     | 2.47   |
| Kingston  | SUV500240G         | 240 GB | 5       | 899   | 0     | 2.47   |
| Crucial   | CT960M500SSD1      | 960 GB | 18      | 1909  | 7     | 2.46   |
| Samsung   | MZNLN512HMJP-00000 | 512 GB | 11      | 891   | 0     | 2.44   |
| Intel     | SSDSC2KG240G7      | 240 GB | 46      | 907   | 1     | 2.44   |
| Micron    | M510DC_MTFDDAK4... | 480 GB | 3       | 888   | 0     | 2.43   |
| Samsung   | SSD 860 PRO        | 256 GB | 57      | 887   | 0     | 2.43   |
| SanDisk   | SSD PLUS 240 GB    | 240 GB | 11      | 885   | 0     | 2.43   |
| SanDisk   | Ultra II           | 480 GB | 15      | 914   | 1     | 2.43   |
| WDC       | WDS500G1B0A-00H9H0 | 500 GB | 2       | 881   | 0     | 2.41   |
| Seagate   | XF1230-1A0480      | 480 GB | 14      | 878   | 0     | 2.41   |
| Intel     | SSDSC2BB016T7      | 1.6 TB | 61      | 1699  | 4     | 2.40   |
| Samsung   | SSD 860 EVO        | 4 TB   | 11      | 875   | 0     | 2.40   |
| Samsung   | SSD 860 DCT 1.92TB | 1.9 TB | 20      | 868   | 0     | 2.38   |
| WDC       | WDS100T2B0A        | 1 TB   | 9       | 856   | 0     | 2.35   |
| SATADOM   | SL 3IE3 V2         | 64 GB  | 7       | 854   | 0     | 2.34   |
| Seagate   | XF1230-1A0240      | 240 GB | 10      | 853   | 0     | 2.34   |
| Micron    | 5100_MTFDDAK240TCB | 240 GB | 29      | 1094  | 2     | 2.33   |
| Samsung   | SSD 860 PRO        | 4 TB   | 14      | 847   | 0     | 2.32   |
| Crucial   | CT275MX300SSD1     | 275 GB | 40      | 1042  | 1     | 2.31   |
| Intel     | SSDSC2MH120A2      | 120 GB | 2       | 842   | 0     | 2.31   |
| Seagate   | XF1230-1A0960      | 960 GB | 2       | 833   | 0     | 2.28   |
| Team      | T253X1960G         | 960 GB | 3       | 830   | 0     | 2.28   |
| Intel     | SSDSC2KG960G7      | 960 GB | 46      | 1308  | 4     | 2.27   |
| Intel     | SSDSC2KB240G7      | 240 GB | 70      | 914   | 7     | 2.26   |
| Superm... | SSD                | 128 GB | 134     | 840   | 11    | 2.25   |
| OWC       | Mercury Electra... | 250 GB | 2       | 818   | 0     | 2.24   |
| AMD       | R3SL120G           | 120 GB | 2       | 812   | 0     | 2.23   |
| Toshiba   | THNSN81Q92CSE      | 1.9 TB | 7       | 812   | 0     | 2.23   |
| Micron    | 5100_MTFDDAK1T9TBY | 1.9 TB | 74      | 1422  | 20    | 2.22   |
| XPG       | SX950U             | 120 GB | 2       | 806   | 0     | 2.21   |
| Crucial   | CT525MX300SSD1     | 528 GB | 49      | 916   | 1     | 2.21   |
| Micron    | 5300_MTFDDAK480TDT | 480 GB | 7       | 802   | 0     | 2.20   |
| Samsung   | SSD 883 DCT 1.92TB | 1.9 TB | 236     | 806   | 1     | 2.20   |
| Micron    | 5300_MTFDDAK960TDS | 960 GB | 180     | 825   | 1     | 2.18   |
| Micron    | MTFDDAK480TDN      | 480 GB | 40      | 808   | 1     | 2.17   |
| Micron    | 1300_MTFDDAK256TDL | 256 GB | 31      | 839   | 1     | 2.17   |
| Samsung   | SSD 860 PRO        | 2 TB   | 158     | 791   | 1     | 2.17   |
| WDC       | WDS240G1G0A-00SS50 | 240 GB | 10      | 790   | 0     | 2.17   |
| Samsung   | SSD 883 DCT        | 960 GB | 43      | 789   | 0     | 2.16   |
| WDC       | HBS3A1996A7E6B1    | 960 GB | 2       | 788   | 0     | 2.16   |
| HPE       | MR000240GWFLU      | 240 GB | 2       | 785   | 0     | 2.15   |
| HPE       | MK000240GWEZF      | 240 GB | 10      | 785   | 0     | 2.15   |
| Samsung   | MZ7KH240HAHQ-00005 | 240 GB | 85      | 784   | 0     | 2.15   |
| Intel     | SSDSC2BW120H6      | 120 GB | 5       | 905   | 3     | 2.13   |
| Samsung   | SSD 850 EVO mSATA  | 250 GB | 6       | 775   | 0     | 2.12   |
| SanDisk   | SDSSDA240G         | 240 GB | 2       | 768   | 0     | 2.11   |
| Samsung   | MZ7LM1T9HMJP-00005 | 1.9 TB | 113     | 1215  | 19    | 2.10   |
| Crucial   | CT256MX100SSD1     | 256 GB | 4       | 1560  | 503   | 2.10   |
| Micron    | 5200_MTFDDAK1T9TDC | 1.9 TB | 10      | 955   | 2     | 2.10   |
| Goodram   | IR-SSDPR-S25A-240  | 240 GB | 3       | 762   | 0     | 2.09   |
| Samsung   | SSD 860 EVO M.2    | 500 GB | 9       | 760   | 0     | 2.08   |
| Micron    | 5200_MTFDDAK3T8TDC | 3.8 TB | 31      | 779   | 1     | 2.08   |
| WDC       | WDS200T2B0A        | 2 TB   | 9       | 755   | 0     | 2.07   |
| Micron    | 5200_MTFDDAK240TDN | 240 GB | 40      | 753   | 0     | 2.06   |
| Intel     | SSDSCKKB240G8      | 240 GB | 19      | 809   | 1     | 2.06   |
| Crucial   | CT1050MX300SSD1    | 1 TB   | 38      | 1137  | 3     | 2.06   |
| Patriot   | Burst Elite        | 240 GB | 2       | 748   | 0     | 2.05   |
| Seagate   | XA1920ME10063      | 1.9 TB | 36      | 742   | 0     | 2.03   |
| Intel     | SSDSC2BB480G7R     | 480 GB | 26      | 774   | 1     | 2.03   |
| Samsung   | MZ7LN256HCHP-000L7 | 256 GB | 2       | 740   | 0     | 2.03   |
| Samsung   | SSD 860 EVO        | 2 TB   | 159     | 739   | 0     | 2.03   |
| SanDisk   | SDSSDH32000G       | 2 TB   | 2       | 736   | 0     | 2.02   |
| Micron    | 5200_MTFDDAK960TDD | 960 GB | 174     | 760   | 1     | 2.02   |
| Micron    | 5100_MTFDDAK960TCB | 960 GB | 131     | 1207  | 4     | 2.01   |
| Intel     | SSDSC2BF120A4H     | 120 GB | 2       | 734   | 0     | 2.01   |
| Micron    | 5200_MTFDDAK1T9TDD | 1.9 TB | 71      | 801   | 1     | 2.01   |
| Samsung   | MZ7LH960HAJR-000AZ | 960 GB | 4       | 731   | 0     | 2.01   |
| Samsung   | SSD 860 QVO        | 2 TB   | 29      | 728   | 0     | 2.00   |
| Micron    | 1100_MTFDDAK512TBN | 512 GB | 44      | 1221  | 47    | 1.99   |
| Crucial   | CT500BX100SSD1     | 500 GB | 2       | 723   | 0     | 1.98   |
| Superm... | SSD                | 16 GB  | 29      | 718   | 0     | 1.97   |
| Kingston  | SV300S37A480G      | 480 GB | 11      | 1169  | 39    | 1.96   |
| Micron    | 5300_MTFDDAK1T9TDT | 1.9 TB | 109     | 769   | 1     | 1.96   |
| HPE       | MK000960GWUGH      | 960 GB | 6       | 806   | 1     | 1.96   |
| Kingston  | SA400M8120G        | 120 GB | 3       | 714   | 0     | 1.96   |
| HPE       | MK001920GWUGK      | 1.9 TB | 2       | 708   | 0     | 1.94   |
| Intel     | SSDSC2KG240G8      | 240 GB | 210     | 710   | 1     | 1.94   |
| Micron    | M500DC_MTFDDAK8... | 800 GB | 27      | 718   | 1     | 1.93   |
| Patriot   | Burst              | 480 GB | 9       | 826   | 1     | 1.93   |
| Transcend | TSMSSSD01-240GP    | 240 GB | 4       | 702   | 0     | 1.92   |
| Toshiba   | THNSNJ800PCSZ      | 800 GB | 4       | 700   | 0     | 1.92   |
| Toshiba   | THNSF8400CCSE      | 400 GB | 12      | 688   | 0     | 1.89   |
| Samsung   | MZ7KM960HMJP-00005 | 960 GB | 99      | 684   | 0     | 1.87   |
| Micron    | 5200_MTFDDAK480TDN | 480 GB | 21      | 676   | 0     | 1.85   |
| Micron    | 5200_MTFDDAK960TDC | 960 GB | 48      | 712   | 1     | 1.85   |
| Samsung   | MZ7KM480HMHQ-000MV | 480 GB | 37      | 675   | 0     | 1.85   |
| Samsung   | MZ7LH960HAJR0D3    | 960 GB | 20      | 672   | 0     | 1.84   |
| Samsung   | MZ7KH960HAJR-00005 | 960 GB | 67      | 669   | 0     | 1.84   |
| Kingston  | SHSS37A240G        | 240 GB | 3       | 661   | 0     | 1.81   |
| Intel     | SSDSCKJB240G7      | 240 GB | 5       | 656   | 0     | 1.80   |
| Micron    | 5200_MTFDDAK480TDC | 480 GB | 31      | 667   | 1     | 1.80   |
| Samsung   | MZ7LM1T9HMJP0D3    | 1.9 TB | 2       | 656   | 0     | 1.80   |
| Intel     | SSDSC2KB480G8R     | 480 GB | 19      | 694   | 1     | 1.79   |
| Intel     | SSDSC2BB012T7      | 1.2 TB | 173     | 1202  | 4     | 1.79   |
| Samsung   | SSD 860 PRO        | 1 TB   | 113     | 650   | 0     | 1.78   |
| Kingston  | SUV400S37120G      | 120 GB | 12      | 680   | 3     | 1.78   |
| Dell      | SSDSCKKB240G8R     | 240 GB | 16      | 648   | 0     | 1.78   |
| Intel     | SSDSC2BW180A4      | 180 GB | 2       | 644   | 0     | 1.77   |
| Corsair   | Force LS SSD       | 64 GB  | 4       | 643   | 0     | 1.76   |
| Samsung   | MZ7LM960HMJP-000MV | 960 GB | 4       | 641   | 0     | 1.76   |
| HP        | VK001920GWSXK      | 1.9 TB | 35      | 638   | 0     | 1.75   |
| Intel     | SSDSC2CW120A3      | 120 GB | 34      | 2170  | 720   | 1.75   |
| Seagate   | XA1920LE10063      | 1.9 TB | 20      | 637   | 0     | 1.75   |
| Micron    | 5210_MTFDDAK1T9QDE | 1.9 TB | 4       | 637   | 0     | 1.75   |
| WDC       | WDS500G2B0A-00SM50 | 500 GB | 5       | 634   | 0     | 1.74   |
| Samsung   | MZ7LN128HCHP-000H1 | 128 GB | 2       | 633   | 0     | 1.74   |
| Seagate   | XA960ME10063       | 960 GB | 4       | 632   | 0     | 1.73   |
| SanDisk   | SSD PLUS 480 GB    | 480 GB | 11      | 777   | 2     | 1.73   |
| Micron    | 5200_MTFDDAK960TDN | 960 GB | 4       | 630   | 0     | 1.73   |
| Micron    | 5100_MTFDDAK480TBY | 480 GB | 15      | 808   | 3     | 1.70   |
| Intel     | SSDSC2KB480G7      | 480 GB | 46      | 738   | 1     | 1.70   |
| Samsung   | MZ7L3960HBLT-00A07 | 960 GB | 65      | 618   | 0     | 1.69   |
| Samsung   | MZ7LM480HMHQ-00005 | 480 GB | 73      | 1242  | 28    | 1.69   |
| Intel     | SSDSC2KB960G8      | 960 GB | 921     | 715   | 1     | 1.69   |
| Intel     | SSDSC2BW120A4      | 120 GB | 47      | 771   | 1     | 1.68   |
| Goodram   | IR-SSDPR-S25A-120  | 120 GB | 7       | 612   | 0     | 1.68   |
| SanDisk   | SDLF1CRR-019T-1HA1 | 1.9 TB | 10      | 650   | 1     | 1.67   |
| WDC       | WDS120G1G0A-00SS50 | 120 GB | 7       | 605   | 0     | 1.66   |
| Intel     | SSDSC2KB019T7      | 1.9 TB | 65      | 1082  | 5     | 1.66   |
| Intel     | SSDSC2KB240G8      | 240 GB | 821     | 627   | 2     | 1.65   |
| Intel     | SSDSC2KB480G8      | 480 GB | 312     | 617   | 1     | 1.65   |
| Samsung   | MZ7KH1T9HAJR-00005 | 1.9 TB | 117     | 605   | 1     | 1.65   |
| Samsung   | MZ7LH480HAHQ-000V3 | 480 GB | 5       | 599   | 0     | 1.64   |
| Micron    | MTFDDAV240TCB      | 240 GB | 14      | 606   | 1     | 1.64   |
| Goodram   | SSDPR-CX400-512    | 512 GB | 3       | 596   | 0     | 1.63   |
| Micron    | 1100_MTFDDAK256TBN | 256 GB | 36      | 670   | 29    | 1.61   |
| Seagate   | BarraCuda SSD Z... | 250 GB | 2       | 585   | 0     | 1.60   |
| Micron    | MTFDDAK960TDS      | 960 GB | 22      | 619   | 1     | 1.60   |
| Plextor   | PX-256M6S+         | 256 GB | 2       | 584   | 0     | 1.60   |
| Seagate   | XA480ME10063       | 480 GB | 13      | 584   | 0     | 1.60   |
| Intel     | SSDSC2KG019T7R     | 1.9 TB | 15      | 959   | 3     | 1.60   |
| Micron    | 5300_MTFDDAK480TDS | 480 GB | 63      | 578   | 0     | 1.59   |
| Phison    | SATA SSD           | 480 GB | 3       | 578   | 0     | 1.59   |
| Samsung   | SSD 860 EVO        | 500 GB | 291     | 580   | 1     | 1.58   |
| Samsung   | SSD 883 DCT 3.84TB | 3.8 TB | 165     | 578   | 3     | 1.57   |
| Samsung   | MZ7LM240HMHQ-00005 | 240 GB | 79      | 1000  | 138   | 1.57   |
| Kingston  | SEDC500M960G       | 960 GB | 15      | 596   | 1     | 1.57   |
| Samsung   | SSD 860 EVO        | 250 GB | 119     | 574   | 2     | 1.57   |
| Intel     | SSDSC2KB960G7      | 960 GB | 176     | 1363  | 12    | 1.56   |
| Samsung   | SSD 845DC PRO      | 800 GB | 4       | 2276  | 3     | 1.56   |
| ADATA     | SU800              | 128 GB | 4       | 868   | 4     | 1.55   |
| Micron    | 5100_MTFDDAK1T9TCC | 1.9 TB | 17      | 640   | 1     | 1.55   |
| SK hynix  | SC311 SATA         | 1 TB   | 2       | 563   | 0     | 1.54   |
| Samsung   | SSD 860 EVO        | 1 TB   | 472     | 562   | 1     | 1.54   |
| WDC       | WDS250G2B0A-00SM50 | 250 GB | 23      | 559   | 0     | 1.53   |
| SATADOM   | SL 3SE             | 32 GB  | 3       | 556   | 0     | 1.52   |
| HPE       | MK000960GXAXB      | 960 GB | 5       | 552   | 0     | 1.51   |
| Intel     | SSDSC2BF120A4H SED | 120 GB | 2       | 552   | 0     | 1.51   |
| Intel     | SSDSC2BB960G7      | 960 GB | 34      | 1075  | 3     | 1.51   |
| Kingston  | SUV400S37240G      | 240 GB | 53      | 565   | 1     | 1.50   |
| HP        | VK0480GFLKH        | 480 GB | 2       | 547   | 0     | 1.50   |
| Micron    | 5200_MTFDDAK1T9TDN | 1.9 TB | 19      | 631   | 1     | 1.50   |
| HP        | SSD S700           | 500 GB | 7       | 600   | 1     | 1.49   |
| PNY       | CS900 120GB SSD    | 120 GB | 2       | 543   | 0     | 1.49   |
| ADATA     | SU650              | 240 GB | 8       | 541   | 0     | 1.48   |
| Crucial   | CT2050MX300SSD1    | 2 TB   | 22      | 1266  | 22    | 1.48   |
| Crucial   | CT120BX500SSD1     | 120 GB | 38      | 539   | 0     | 1.48   |
| Goodram   | SSDPR-CX300-120    | 120 GB | 2       | 538   | 0     | 1.47   |
| Samsung   | SSD 860 QVO        | 1 TB   | 58      | 537   | 0     | 1.47   |
| Samsung   | MZ7LH240HAHQ0D3    | 240 GB | 6       | 534   | 0     | 1.46   |
| Intel     | SSDSC2BA400G3E     | 400 GB | 2       | 528   | 0     | 1.45   |
| Micron    | MTFDDAK128MBF-1... | 128 GB | 13      | 526   | 0     | 1.44   |
| Intel     | SSDSC2BW240A4      | 240 GB | 44      | 861   | 7     | 1.43   |
| Toshiba   | THNSF8200CAME      | 200 GB | 3       | 521   | 0     | 1.43   |
| Seagate   | XA480LE10063       | 480 GB | 14      | 520   | 0     | 1.43   |
| SPCC      | SSD                | 1 TB   | 2       | 517   | 0     | 1.42   |
| Micron    | MTFDDAK960TCB      | 960 GB | 12      | 642   | 1     | 1.41   |
| Samsung   | MZ7LM240HMHQ-00003 | 240 GB | 2       | 513   | 0     | 1.41   |
| Micron    | MTFDDAK1T9TCB-1... | 1.9 TB | 12      | 511   | 0     | 1.40   |
| Patriot   | P200               | 2 TB   | 5       | 510   | 0     | 1.40   |
| SanDisk   | SDSSDA480G         | 480 GB | 2       | 509   | 0     | 1.40   |
| HP        | VK0480GFDKH        | 480 GB | 6       | 509   | 0     | 1.40   |
| Samsung   | MZ7LH7T6HMLA-00005 | 7.6 TB | 125     | 509   | 0     | 1.40   |
| Seagate   | XA960LE10063       | 960 GB | 110     | 509   | 0     | 1.39   |
| Samsung   | MZ7KH960HAJR0D3    | 960 GB | 163     | 508   | 0     | 1.39   |
| Intel     | SSDSC2BB800H4      | 800 GB | 6       | 504   | 0     | 1.38   |
| Intel     | SSDSC2BB120G7K     | 120 GB | 8       | 618   | 1     | 1.37   |
| PNY       | CS900 240GB SSD    | 240 GB | 2       | 497   | 0     | 1.36   |
| Kingston  | SA400S37120G       | 120 GB | 54      | 520   | 1     | 1.36   |
| OCZ       | D2RSTK251E14-0400  | 400 GB | 2       | 495   | 0     | 1.36   |
| WDC       | WDS100T2B0A-00SM50 | 1 TB   | 116     | 589   | 4     | 1.35   |
| Intel     | SSDSCKKW128G8      | 128 GB | 3       | 493   | 0     | 1.35   |
| Samsung   | MZ7LH1T9HALT0D3    | 1.9 TB | 45      | 482   | 0     | 1.32   |
| Samsung   | MZ7KH480HAHQ-00005 | 480 GB | 83      | 482   | 0     | 1.32   |
| Micron    | 5100_MTFDDAK1T9TCB | 1.9 TB | 3       | 1499  | 694   | 1.32   |
| Samsung   | SSD 860 EVO mSATA  | 250 GB | 3       | 481   | 0     | 1.32   |
| HP        | VK001600GWCNT      | 1.6 TB | 12      | 616   | 2     | 1.32   |
| Micron    | 5300_MTFDDAK240TDS | 240 GB | 10      | 477   | 0     | 1.31   |
| WDC       | WDS250G2B0A        | 250 GB | 2       | 476   | 0     | 1.31   |
| Samsung   | MZ7LH480HAHQ0D3    | 480 GB | 2       | 475   | 0     | 1.30   |
| Samsung   | SSD 850            | 120 GB | 2       | 474   | 0     | 1.30   |
| Samsung   | MZ7LH960HAJR-00005 | 960 GB | 1149    | 473   | 0     | 1.30   |
| Samsung   | MZ7LH1T9HMLT-00005 | 1.9 TB | 788     | 473   | 0     | 1.30   |
| QUMO      | Q3DT-512GSCY       | 512 GB | 4       | 472   | 0     | 1.30   |
| Micron    | 1300_MTFDDAK1T0TDL | 1 TB   | 10      | 527   | 1     | 1.29   |
| Micron    | 5100_MTFDDAV240TCB | 240 GB | 13      | 637   | 22    | 1.29   |
| Lite-On   | L8H-128V2G-HP      | 128 GB | 2       | 469   | 0     | 1.29   |
| SPCC      | SSD                | 256 GB | 3       | 469   | 0     | 1.29   |
| Samsung   | SSD 860 QVO        | 4 TB   | 6       | 464   | 0     | 1.27   |
| Intel     | SSDSC2KG960G8      | 960 GB | 225     | 508   | 1     | 1.27   |
| Samsung   | MZ7KH480HAHQ0D3    | 480 GB | 23      | 461   | 0     | 1.26   |
| Intel     | SSDSC2KG019T8      | 1.9 TB | 235     | 542   | 1     | 1.26   |
| Micron    | 1100_MTFDDAK1T0TBN | 1 TB   | 6       | 1358  | 147   | 1.25   |
| WDC       | WDS400T2B0A-00SM50 | 4 TB   | 4       | 735   | 1     | 1.25   |
| Samsung   | SSD 840 EVO 250... | 250 GB | 4       | 456   | 0     | 1.25   |
| Micron    | 1100_MTFDDAK2T0TBN | 2 TB   | 16      | 487   | 1     | 1.25   |
| Samsung   | SSD 883 DCT        | 240 GB | 42      | 453   | 0     | 1.24   |
| Samsung   | SSD 883 DCT        | 480 GB | 7       | 446   | 0     | 1.22   |
| Micron    | MTFDDAK480TDS      | 480 GB | 8       | 444   | 0     | 1.22   |
| Kingston  | SA400S37480G       | 480 GB | 35      | 699   | 12    | 1.22   |
| WDC       | WDS240G2G0A-00JH30 | 240 GB | 21      | 488   | 1     | 1.21   |
| Samsung   | MZ7L3480HBLT-00A07 | 480 GB | 31      | 464   | 1     | 1.21   |
| Intel     | SSDSC2KB480G7R     | 480 GB | 6       | 438   | 0     | 1.20   |
| Intel     | SSDSC2KB038T7      | 3.8 TB | 25      | 733   | 9     | 1.20   |
| Samsung   | MZ7LH240HAHQ-00005 | 240 GB | 503     | 437   | 0     | 1.20   |
| Intel     | SSDSC2KG480G8      | 480 GB | 284     | 487   | 1     | 1.20   |
| Kingston  | SEDC450R960G       | 960 GB | 3       | 435   | 0     | 1.19   |
| Samsung   | SSD 870 QVO        | 8 TB   | 35      | 435   | 0     | 1.19   |
| Micron    | 5300_MTFDDAK960TDT | 960 GB | 40      | 440   | 1     | 1.19   |
| Intel     | SSDSC2KB019T8      | 1.9 TB | 457     | 555   | 5     | 1.19   |
| Micron    | 5300_MTFDDAK3T8TDS | 3.8 TB | 135     | 452   | 1     | 1.18   |
| Kingston  | SUV500960G         | 960 GB | 8       | 425   | 0     | 1.17   |
| SanDisk   | SDSSDH3 1T00       | 1 TB   | 3       | 425   | 0     | 1.17   |
| Micron    | 5100_MTFDDAK960TCC | 960 GB | 9       | 520   | 1     | 1.17   |
| HP        | SSD S700           | 250 GB | 6       | 423   | 0     | 1.16   |
| Intel     | SSDSC2KB960G8R     | 960 GB | 7       | 420   | 0     | 1.15   |
| Crucial   | CT960BX500SSD1     | 960 GB | 8       | 418   | 0     | 1.15   |
| Intel     | SSDSC2KB019T7R     | 1.9 TB | 23      | 612   | 3     | 1.15   |
| WDC       | WDS480G2G0B-00EPW0 | 480 GB | 6       | 725   | 10    | 1.14   |
| Micron    | MTFDDAK960TDT      | 960 GB | 8       | 413   | 0     | 1.13   |
| Samsung   | MZ7LH480HAHQ-00005 | 480 GB | 139     | 410   | 0     | 1.13   |
| Gigaby... | GP-GSTFS30512GTTD  | 512 GB | 2       | 410   | 0     | 1.13   |
| KingDian  | S280               | 240 GB | 3       | 476   | 1     | 1.12   |
| SanDisk   | SSD G5 BICS4       | 1 TB   | 5       | 448   | 1     | 1.11   |
| Patriot   | Burst              | 960 GB | 3       | 403   | 0     | 1.10   |
| SPCC      | SSD                | 512 GB | 6       | 402   | 0     | 1.10   |
| SuperM... | SSD                | 128 GB | 2       | 402   | 0     | 1.10   |
| Micron    | 5300_MTFDDAK3T8TDT | 3.8 TB | 86      | 425   | 2     | 1.10   |
| SanDisk   | SSD PLUS           | 480 GB | 24      | 574   | 6     | 1.10   |
| Samsung   | MZ7LH3T8HALT0D3    | 3.8 TB | 8       | 397   | 0     | 1.09   |
| SK hynix  | HFS3T8G32FEH-7410A | 3.8 TB | 8       | 395   | 0     | 1.08   |
| Samsung   | SSD 860 PRO        | 512 GB | 67      | 393   | 0     | 1.08   |
| WDC       | WDS200T2B0A-00SM50 | 2 TB   | 45      | 399   | 1     | 1.07   |
| Kingston  | SEDC500R480G       | 480 GB | 11      | 387   | 0     | 1.06   |
| Seagate   | BarraCuda 120 S... | 1 TB   | 3       | 387   | 0     | 1.06   |
| Micron    | 5300_MTFDDAV240TDS | 240 GB | 8       | 385   | 0     | 1.06   |
| Samsung   | MZ7KM480HMHQ0D3    | 480 GB | 3       | 382   | 0     | 1.05   |
| Micron    | MTFDDAK480TDS-1... | 480 GB | 13      | 429   | 78    | 1.05   |
| Micron    | 5210_MTFDDAK3T8QDE | 3.8 TB | 113     | 426   | 3     | 1.05   |
| Samsung   | SSD 870 QVO        | 2 TB   | 6       | 382   | 0     | 1.05   |
| Intel     | SSDSC2BW240H6      | 240 GB | 14      | 610   | 25    | 1.04   |
| SK hynix  | HFS250G32TND-N1A2A | 250 GB | 10      | 374   | 0     | 1.03   |
| Intel     | SSDSC2KG960G8R     | 960 GB | 19      | 482   | 2     | 1.02   |
| Intel     | SSDSC2BW480H6      | 480 GB | 5       | 639   | 4     | 1.02   |
| Kingston  | SEDC500M1920G      | 1.9 TB | 44      | 406   | 1     | 1.01   |
| HPE       | MK000480GWCEV      | 480 GB | 2       | 364   | 0     | 1.00   |
| Kingston  | SA400S37960G       | 960 GB | 8       | 364   | 0     | 1.00   |
| HPE       | MK000480GWXFF      | 480 GB | 21      | 363   | 0     | 1.00   |
| ORTIAL    | SSD                | 1 TB   | 12      | 455   | 2     | 1.00   |
| Intel     | SSDSC2KG019T8L     | 1.9 TB | 6       | 489   | 2     | 0.99   |
| Seagate   | XA240ME10003       | 240 GB | 5       | 361   | 0     | 0.99   |
| Micron    | 5300_MTFDDAV240TDU | 240 GB | 3       | 357   | 0     | 0.98   |
| Hikvision | HS-SSD-C100 960G   | 960 GB | 2       | 356   | 0     | 0.98   |
| Micron    | MTFDDAV240TDU      | 240 GB | 6       | 355   | 0     | 0.97   |
| Samsung   | MZ7LM960HMJP-00003 | 960 GB | 2       | 678   | 12    | 0.97   |
| Toshiba   | KHK61RSE1T92       | 1.9 TB | 33      | 351   | 0     | 0.96   |
| Samsung   | MZ7WD480HMHP-00003 | 480 GB | 8       | 1956  | 66    | 0.96   |
| China     | 512GB QLC SATA SSD | 512 GB | 6       | 350   | 0     | 0.96   |
| Toshiba   | KHK61RSE960G       | 960 GB | 67      | 348   | 0     | 0.95   |
| WDC       | WDS200T1R0A-68A4W0 | 2 TB   | 24      | 358   | 1     | 0.95   |
| Patriot   | Burst Elite        | 480 GB | 2       | 343   | 0     | 0.94   |
| ADATA     | SP550              | 120 GB | 3       | 521   | 166   | 0.93   |
| Samsung   | MZNLH1T0HALB-00000 | 1 TB   | 12      | 336   | 0     | 0.92   |
| HP        | VK000960GWTTB      | 960 GB | 11      | 330   | 0     | 0.91   |
| HPE       | MK001920GWJPQ      | 1.9 TB | 18      | 640   | 7     | 0.91   |
| Patriot   | Burst              | 240 GB | 10      | 327   | 0     | 0.90   |
| Samsung   | MZ7LH3T8HMLT0D3    | 3.8 TB | 40      | 325   | 0     | 0.89   |
| SK hynix  | SHGS31-1000GS-2    | 1 TB   | 23      | 323   | 0     | 0.89   |
| Micron    | MTFDDAK1T9TDD      | 1.9 TB | 3       | 322   | 0     | 0.88   |
| Crucial   | CT500MX500SSD1     | 500 GB | 160     | 389   | 3     | 0.88   |
| Intel     | SSDSC2KG960GZ      | 960 GB | 12      | 320   | 0     | 0.88   |
| SanDisk   | SSD PLUS           | 240 GB | 19      | 335   | 1     | 0.88   |
| SanDisk   | SDSSDA120G         | 120 GB | 3       | 317   | 0     | 0.87   |
| ADATA     | SP580              | 120 GB | 2       | 1271  | 505   | 0.86   |
| Micron    | MTFDDAK960TDS-1... | 960 GB | 2       | 313   | 0     | 0.86   |
| Samsung   | MZ7LH480HBHQ0D3    | 480 GB | 19      | 313   | 0     | 0.86   |
| Mushkin   | MKNSSDRE960GB      | 960 GB | 5       | 514   | 2     | 0.85   |
| Intel     | SSDSC2KG038T8      | 3.8 TB | 42      | 341   | 1     | 0.85   |
| Crucial   | CT1000MX500SSD4    | 1 TB   | 3       | 306   | 0     | 0.84   |

SSD by Vendor
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| Apple       | 1      | 2       | 2543  | 0     | 6.97   |
| OCZ         | 4      | 14      | 1998  | 8     | 3.86   |
| Corsair     | 2      | 8       | 1520  | 1     | 3.36   |
| MyDigita... | 1      | 6       | 945   | 0     | 2.59   |
| Toshiba     | 14     | 254     | 931   | 1     | 2.51   |
| HP          | 25     | 306     | 981   | 1     | 2.41   |
| SanDisk     | 29     | 286     | 927   | 12    | 2.38   |
| Supermicro  | 4      | 206     | 881   | 7     | 2.37   |
| OWC         | 1      | 2       | 818   | 0     | 2.24   |
| XPG         | 1      | 2       | 806   | 0     | 2.21   |
| Dell        | 2      | 22      | 846   | 1     | 2.18   |
| Plextor     | 2      | 4       | 746   | 0     | 2.05   |
| Samsung     | 157    | 9293    | 782   | 8     | 1.97   |
| Intel       | 139    | 6660    | 957   | 70    | 1.97   |
| Goodram     | 5      | 19      | 708   | 0     | 1.94   |
| Lite-On     | 3      | 6       | 703   | 0     | 1.93   |
| Kingston    | 45     | 839     | 671   | 7     | 1.57   |
| HPE         | 15     | 147     | 612   | 1     | 1.56   |
| Micron      | 79     | 2415    | 652   | 8     | 1.52   |
| Seagate     | 18     | 267     | 737   | 131   | 1.46   |
| WDC         | 23     | 353     | 552   | 3     | 1.36   |
| Patriot     | 8      | 37      | 471   | 1     | 1.21   |
| SATADOM     | 6      | 30      | 416   | 0     | 1.14   |
| KingDian    | 1      | 3       | 476   | 1     | 1.12   |
| SuperMicro  | 1      | 2       | 402   | 0     | 1.10   |
| Crucial     | 31     | 1334    | 505   | 8     | 1.07   |
| AMD         | 3      | 6       | 365   | 0     | 1.00   |
| ORTIAL      | 1      | 12      | 455   | 2     | 1.00   |
| SK hynix    | 7      | 53      | 437   | 9     | 0.99   |
| Hikvision   | 1      | 2       | 356   | 0     | 0.98   |
| SPCC        | 5      | 15      | 381   | 8     | 0.91   |
| QUMO        | 2      | 7       | 301   | 1     | 0.81   |
| PNY         | 4      | 16      | 290   | 0     | 0.80   |
| Mushkin     | 2      | 13      | 359   | 1     | 0.77   |
| ADATA       | 17     | 61      | 468   | 143   | 0.73   |
| DEXP        | 2      | 14      | 260   | 0     | 0.71   |
| Synology    | 1      | 12      | 240   | 0     | 0.66   |
| KingSpec    | 1      | 2       | 239   | 0     | 0.66   |
| Gigabyte... | 2      | 12      | 239   | 0     | 0.66   |
| SNR         | 1      | 3       | 237   | 0     | 0.65   |
| SaiChi      | 1      | 6       | 232   | 0     | 0.64   |
| Phison      | 4      | 22      | 229   | 0     | 0.63   |
| Apacer      | 2      | 49      | 325   | 19    | 0.59   |
| China       | 11     | 85      | 212   | 2     | 0.56   |
| Team        | 4      | 40      | 203   | 0     | 0.56   |
| Maxtor      | 1      | 2       | 203   | 0     | 0.56   |
| Transcend   | 11     | 50      | 151   | 2     | 0.38   |
| Intenso     | 2      | 4       | 110   | 0     | 0.30   |
| KIOXIA-E... | 1      | 8       | 90    | 0     | 0.25   |
| Qumo        | 1      | 2       | 47    | 608   | 0.10   |
| GS Nanotech | 2      | 5       | 26    | 0     | 0.07   |
| Palit       | 1      | 2       | 6     | 0     | 0.02   |
| Foxline     | 1      | 2       | 4     | 0     | 0.01   |
| Avant       | 1      | 2       | 2045  | 1018  | 0.01   |

NVME by Model
-------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

See full list of tested NVMe samples in the Appendix 5 ([All_NVMe.md](/All_NVMe.md)).

See top 1000 of tested NVMe models in the [Top1000_NVMe.md](/Top1000_NVMe.md).

| MFG       | Model              | Size   | Samples | Days  | Err   | MTBF |
|-----------|--------------------|--------|---------|-------|-------|------|
| Intel     | SSDPEDMX400G4      | 400 GB | 10      | 2795  | 0     | 7.66   |
| Intel     | SSDPE2MX012T4      | 1.2 TB | 4       | 1977  | 0     | 5.42   |
| Intel     | SSDPEDME020T4      | 2 TB   | 2       | 1913  | 0     | 5.24   |
| Intel     | SSDPEDME020T4D ... | 2 TB   | 2       | 1790  | 0     | 4.90   |
| Intel     | SSDPEDME016T4S     | 1.6 TB | 17      | 1716  | 0     | 4.70   |
| Intel     | SSDPEDME400G4      | 400 GB | 19      | 1695  | 0     | 4.65   |
| Intel     | SSDPE2KX020T8L     | 962 GB | 20      | 1555  | 0     | 4.26   |
| Intel     | SSDPEDMD020T4D ... | 2 TB   | 5       | 1486  | 0     | 4.07   |
| Intel     | SSDPE2KE016T7      | 1.6 TB | 2       | 1483  | 0     | 4.06   |
| Intel     | SSDPEDMD400G4      | 400 GB | 211     | 1477  | 0     | 4.05   |
| Intel     | SSDPEDMD016T4      | 1.6 TB | 17      | 1400  | 0     | 3.84   |
| Samsung   | MZ1LV480HCHP-00003 | 480 GB | 2       | 1399  | 0     | 3.84   |
| Intel     | SSDPE21K375GAL     | 375 GB | 10      | 1363  | 0     | 3.74   |
| Intel     | SSDPEDMX020T7      | 2 TB   | 46      | 1375  | 5     | 3.70   |
| Samsung   | MZVPV512HDGL-00000 | 512 GB | 3       | 1347  | 0     | 3.69   |
| Intel     | SSDPEDMD800G4      | 800 GB | 276     | 1340  | 0     | 3.67   |
| Intel     | SSDPEDMX012T7      | 1.2 TB | 3       | 1300  | 0     | 3.56   |
| Intel     | SSDPEDMW400G4      | 400 GB | 10      | 1271  | 0     | 3.48   |
| Intel     | SSDPE2KE020T7      | 2 TB   | 2       | 1270  | 0     | 3.48   |
| Samsung   | SSD 950 PRO        | 512 GB | 8       | 1201  | 0     | 3.29   |
| Dell      | Express Flash N... | 2 TB   | 14      | 1184  | 0     | 3.25   |
| Samsung   | MZVLW512HMJP-000H1 | 512 GB | 2       | 1148  | 0     | 3.15   |
| Intel     | SSDPE2ME020T4      | 2 TB   | 2       | 1134  | 0     | 3.11   |
| Dell      | Express Flash N... | 1.6 TB | 19      | 1180  | 54    | 3.08   |
| Toshiba   | THNSN5512GPU7      | 512 GB | 15      | 1100  | 0     | 3.01   |
| Samsung   | MZPLL1T6HEHP-00003 | 1.6 TB | 88      | 1114  | 12    | 2.99   |
| Intel     | SSDPE2MX012T7      | 1.2 TB | 19      | 1067  | 0     | 2.92   |
| Intel     | SSDPE2MD400G4      | 400 GB | 13      | 1061  | 0     | 2.91   |
| Toshiba   | KXG50ZNV256G       | 256 GB | 2       | 1038  | 0     | 2.85   |
| Intel     | SSDPEDKX040T7      | 4 TB   | 45      | 1035  | 23    | 2.72   |
| Samsung   | MZWLL6T4HMLA-00005 | 6.4 TB | 2       | 989   | 0     | 2.71   |
| Intel     | SSDPE2KX040T8      | 4 TB   | 65      | 991   | 16    | 2.67   |
| Intel     | SSDPEDKE020T7      | 2 TB   | 28      | 973   | 0     | 2.67   |
| Intel     | SSDPE2MX450G7      | 450 GB | 46      | 954   | 0     | 2.61   |
| Samsung   | SSD 960 PRO        | 1 TB   | 10      | 901   | 0     | 2.47   |
| Intel     | SSDPE2MD400G4L     | 400 GB | 4       | 895   | 0     | 2.45   |
| Intel     | SSDPEKKW256G7      | 256 GB | 17      | 911   | 1     | 2.44   |
| Dell      | Express Flash N... | 1.6 TB | 4       | 890   | 0     | 2.44   |
| Samsung   | MZPLL3T2HMLS-00003 | 3.2 TB | 6       | 887   | 0     | 2.43   |
| Kingston  | SKC1000960G        | 960 GB | 3       | 886   | 0     | 2.43   |
| Intel     | SSDPE2ME012T4      | 1.2 TB | 8       | 881   | 0     | 2.41   |
| Intel     | SSDPEDMD016T4K     | 1.6 TB | 2       | 881   | 0     | 2.41   |
| Intel     | SSDPED1D280GA      | 280 GB | 21      | 952   | 1     | 2.39   |
| PNY       | CS3030 500GB SSD   | 500 GB | 2       | 851   | 0     | 2.33   |
| Intel     | SSDPE21K375GA      | 375 GB | 38      | 840   | 0     | 2.30   |
| Intel     | SSDPED1D480GA      | 480 GB | 52      | 835   | 0     | 2.29   |
| Intel     | SSDPEDMW800G4      | 800 GB | 7       | 825   | 0     | 2.26   |
| Samsung   | SSD 960 EVO        | 500 GB | 10      | 830   | 8     | 2.24   |
| Samsung   | MZPLL6T4HMLA-00005 | 6.4 TB | 6       | 817   | 0     | 2.24   |
| Intel     | SSDPE21D480GA      | 480 GB | 107     | 791   | 0     | 2.17   |
| Toshiba   | KXG50ZNV1T02       | 1 TB   | 6       | 781   | 0     | 2.14   |
| Samsung   | MZWLL12THMLA-00005 | 12.... | 2       | 780   | 0     | 2.14   |
| Intel     | SSDPE2KE076T8      | 7.6 TB | 2       | 778   | 0     | 2.13   |
| Toshiba   | KXG50ZNV512G       | 512 GB | 21      | 770   | 0     | 2.11   |
| Intel     | MT0800KEXUU        | 800 GB | 18      | 765   | 0     | 2.10   |
| Intel     | SSDPEKKW128G8      | 128 GB | 3       | 752   | 0     | 2.06   |
| Intel     | VO0400KEFJB        | 400 GB | 4       | 743   | 0     | 2.04   |
| Samsung   | MZPLL6T4HMLS-00003 | 6.4 TB | 16      | 742   | 0     | 2.04   |
| HUAWEI    | HWE36P43016M000N   | 1.6 TB | 2       | 741   | 0     | 2.03   |
| Samsung   | MZVKW512HMJP-00000 | 512 GB | 5       | 932   | 202   | 2.01   |
| Dell      | Express Flash P... | 800 GB | 8       | 731   | 0     | 2.00   |
| Dell      | Express Flash P... | 1.6 TB | 8       | 724   | 0     | 1.99   |
| Samsung   | MZPLL6T4HMLS-000MV | 6.4 TB | 4       | 717   | 0     | 1.97   |
| WDC       | WUS3CA116C7P3E3    | 1.6 TB | 178     | 713   | 0     | 1.95   |
| WDC       | WUS3BA196C7P3E3    | 960 GB | 83      | 706   | 0     | 1.94   |
| Samsung   | MZQLW960HMJP-00003 | 960 GB | 20      | 1027  | 130   | 1.88   |
| Kingston  | SKC2000M81000G     | 1 TB   | 2       | 668   | 0     | 1.83   |
| Samsung   | MZPLL1T6HAJQ-00005 | 1.6 TB | 6       | 659   | 0     | 1.81   |
| Samsung   | MZQLW1T9HMJP-00003 | 1.9 TB | 5       | 658   | 0     | 1.81   |
| Intel     | SSDPED1K375GA      | 375 GB | 77      | 651   | 0     | 1.78   |
| Intel     | SSDPEKKA256G7      | 256 GB | 4       | 630   | 0     | 1.73   |
| Samsung   | MZ1LB960HAJQ-00007 | 960 GB | 43      | 626   | 0     | 1.72   |
| Samsung   | MZWLJ15THALA-00007 | 15.... | 2       | 622   | 0     | 1.71   |
| Samsung   | MZPLL3T2HAJQ-00005 | 3.2 TB | 24      | 620   | 0     | 1.70   |
| Samsung   | SSD 960 EVO        | 250 GB | 4       | 594   | 0     | 1.63   |
| Intel     | SSDPED1K750GA      | 752 GB | 152     | 593   | 0     | 1.63   |
| Dell      | Express Flash N... | 1.6 TB | 118     | 586   | 0     | 1.61   |
| Samsung   | MZWLL800HEHP-00003 | 800 GB | 14      | 864   | 4     | 1.60   |
| Intel     | SSDPEL1D380GA      | 384 GB | 6       | 579   | 0     | 1.59   |
| Intel     | SSDPE21K750GA      | 752 GB | 66      | 578   | 0     | 1.58   |
| WDC       | WUS3BA138C7P3E3    | 3.8 TB | 28      | 569   | 0     | 1.56   |
| Dell      | Express Flash P... | 1.6 TB | 5       | 569   | 0     | 1.56   |
| Phison    | Viper M.2 VPN100   | 2 TB   | 9       | 564   | 0     | 1.55   |
| Samsung   | SSD 970 EVO        | 500 GB | 3       | 563   | 0     | 1.54   |
| Intel     | SSDPE2KX020T8      | 2 TB   | 168     | 559   | 0     | 1.53   |
| Samsung   | MZQLB3T8HALS-000AZ | 3.8 TB | 24      | 556   | 0     | 1.52   |
| Micron    | 9300_MTFDHAL3T8TDP | 3.8 TB | 2       | 552   | 0     | 1.51   |
| Intel     | SSDPEL1K100GA      | 100 GB | 11      | 548   | 0     | 1.50   |
| Samsung   | SSD 983 DCT        | 960 GB | 6       | 544   | 0     | 1.49   |
| Samsung   | MZQLW1T9HMJP-000AZ | 1.9 TB | 7       | 591   | 1     | 1.49   |
| Micron    | 7300_MTFDHBE960TDF | 960 GB | 6       | 539   | 0     | 1.48   |
| Dell      | Express Flash N... | 3.2 TB | 4       | 538   | 0     | 1.47   |
| Samsung   | VO001920KWVMT 1... | 1.9 TB | 36      | 537   | 0     | 1.47   |
| Dell      | Express Flash P... | 1.6 TB | 4       | 537   | 0     | 1.47   |
| Intel     | SSDPE21K100GA      | 100 GB | 5       | 527   | 0     | 1.45   |
| Samsung   | MZ1L2960HCJR-00A07 | 960 GB | 22      | 526   | 0     | 1.44   |
| Corsair   | Force MP510 1.9TB  | 1.9 TB | 12      | 521   | 0     | 1.43   |
| Intel     | SSDPEKKA512G8      | 512 GB | 23      | 515   | 0     | 1.41   |
| HGST      | HUSMR7638BDP3Y1    | 3.8 TB | 24      | 504   | 0     | 1.38   |
| Samsung   | MZWLJ7T6HALA-00007 | 7.6 TB | 2       | 502   | 0     | 1.38   |
| Intel     | SSDPE2ME400G4      | 400 GB | 7       | 501   | 0     | 1.38   |
| Samsung   | MZWLL1T6HAJQ-00005 | 1.6 TB | 10      | 501   | 0     | 1.37   |
| WDC       | WUS4CB016D7P3E3    | 1.6 TB | 152     | 500   | 0     | 1.37   |
| WDC       | WDS250G3X0C-00SJG0 | 250 GB | 4       | 494   | 0     | 1.36   |
| Dell      | Express Flash P... | 1.6 TB | 12      | 492   | 0     | 1.35   |
| Toshiba   | KXD51RUE960G       | 960 GB | 10      | 485   | 0     | 1.33   |
| Intel     | SSDPE2KX010T8      | 1 TB   | 168     | 484   | 0     | 1.33   |
| Intel     | SSDPE2KE016T8      | 1.6 TB | 37      | 480   | 0     | 1.32   |
| Corsair   | Force MP600        | 1 TB   | 3       | 475   | 0     | 1.30   |
| WDC       | WUS4BB096D7P3E3    | 960 GB | 553     | 474   | 0     | 1.30   |
| Intel     | SSDPE2MD016T4      | 1.6 TB | 4       | 471   | 0     | 1.29   |
| ADATA     | SX8200PNP          | 256 GB | 2       | 463   | 0     | 1.27   |
| Intel     | SSDPED1D960GAY     | 960 GB | 6       | 460   | 0     | 1.26   |
| WDC       | PC SN720 SDAPNT... | 256 GB | 15      | 454   | 0     | 1.25   |
| Samsung   | MZPLJ12THALA-00007 | 12.... | 12      | 448   | 0     | 1.23   |
| WDC       | CL SN720 SDAQNT... | 1 TB   | 51      | 447   | 0     | 1.23   |
| Intel     | SSDPE2KX080T8      | 8 TB   | 21      | 444   | 0     | 1.22   |
| Samsung   | MZ4LB3T8HALS-00003 | 3.8 TB | 6       | 443   | 0     | 1.22   |
| Wester... | WUS3BA196C7P3E3    | 960 GB | 83      | 439   | 0     | 1.20   |
| Samsung   | MZWLL1T6HEHP-00003 | 1.6 TB | 8       | 436   | 0     | 1.20   |
| Seagate   | FireCuda 520 SS... | 500 GB | 10      | 428   | 0     | 1.17   |
| Wester... | WUS3CA116C7P3E3    | 1.6 TB | 178     | 428   | 0     | 1.17   |
| Dell      | Ent NVMe AGN MU... | 1.6 TB | 12      | 428   | 0     | 1.17   |
| Intel     | SSDPEKNW020T8      | 2 TB   | 5       | 427   | 0     | 1.17   |
| Wester... | WUS3BA138C7P3E3    | 3.8 TB | 20      | 424   | 0     | 1.16   |
| Intel     | SSDPECKE064T7ES    | 3.2 TB | 2       | 422   | 0     | 1.16   |
| WDC       | WUS4BB038D7P3E3    | 3.8 TB | 37      | 421   | 0     | 1.15   |
| Samsung   | MZVLQ512HALU-00000 | 512 GB | 2       | 417   | 0     | 1.14   |
| Samsung   | SSD 960 PRO        | 512 GB | 3       | 416   | 0     | 1.14   |
| Samsung   | MZQL23T8HCLS-00... | 1.9 TB | 2       | 405   | 0     | 1.11   |
| HP        | SSD EX950          | 2 TB   | 10      | 403   | 0     | 1.10   |
| Samsung   | SSD 970 PRO        | 1 TB   | 39      | 396   | 0     | 1.09   |
| Samsung   | MZPJB480HMGC-0BW07 | 480 GB | 16      | 395   | 0     | 1.08   |
| Samsung   | MZ1LB3T8HMLA-00007 | 3.8 TB | 12      | 417   | 1     | 1.08   |
| Toshiba   | KXG60ZNV1T02       | 1 TB   | 50      | 390   | 0     | 1.07   |
| Samsung   | MZVLB512HAJQ-00000 | 512 GB | 29      | 393   | 1     | 1.03   |
| WDC       | WDS250G2B0C-00PXH0 | 250 GB | 3       | 371   | 0     | 1.02   |
| Samsung   | MZQLB960HAJR-00007 | 960 GB | 682     | 369   | 0     | 1.01   |
| Kingston  | SEDC1000M1920G     | 1.9 TB | 2       | 364   | 0     | 1.00   |
| WDC       | WDS500G3XHC-00SJG0 | 500 GB | 6       | 361   | 0     | 0.99   |
| Kingston  | SEDC1000M3840G     | 3.8 TB | 7       | 351   | 0     | 0.96   |
| Phison    | Sabrent Rocket Q   | 1 TB   | 6       | 349   | 0     | 0.96   |
| Samsung   | MZ1LB1T9HALS-00007 | 1.9 TB | 7       | 347   | 0     | 0.95   |
| Samsung   | MZVLB1T0HALR-00000 | 1 TB   | 33      | 350   | 1     | 0.94   |
| WDC       | CL SN720 SDAQNT... | 512 GB | 152     | 351   | 6     | 0.94   |
| Kingston  | SEDC1000M960G      | 960 GB | 2       | 340   | 0     | 0.93   |
| Samsung   | MZQL23T8HCLS-00... | 1.2 TB | 2       | 338   | 0     | 0.93   |
| Samsung   | MZQLB1T9HAJR-00007 | 1.9 TB | 951     | 335   | 1     | 0.92   |
| Samsung   | SSD 970 PRO        | 512 GB | 84      | 333   | 0     | 0.91   |
| Samsung   | MZPLJ1T6HBJR-000H3 | 1.6 TB | 8       | 333   | 0     | 0.91   |
| Intel     | SSDPE2KX040T7      | 4 TB   | 5       | 331   | 0     | 0.91   |
| WDC       | WDS500G3X0C-00SJG0 | 500 GB | 27      | 330   | 0     | 0.90   |
| Samsung   | MZSLW1T0HMLH-000L1 | 1 TB   | 2       | 328   | 0     | 0.90   |
| Kingston  | SEDC1500M3840G     | 3.8 TB | 22      | 326   | 0     | 0.90   |
| Samsung   | MZQLB3T8HALS-00007 | 3.8 TB | 182     | 329   | 1     | 0.89   |
| Samsung   | MZQL23T8HCLS-00A07 | 368 GB | 2       | 321   | 0     | 0.88   |
| Intel     | SSDPE2NV076T8      | 7.6 TB | 6       | 319   | 0     | 0.88   |
| Gigaby... | GP-GSM2NE3100TNTD  | 1 TB   | 10      | 312   | 0     | 0.86   |
| Goodram   | SSDPR-PX500-01T-80 | 1 TB   | 2       | 312   | 0     | 0.86   |
| Samsung   | MZQLB7T6HMLA-00007 | 7.6 TB | 118     | 323   | 1     | 0.85   |
| WDC       | WUS4BB019D7P3E1    | 1.9 TB | 477     | 306   | 0     | 0.84   |
| Micron    | 9300_MTFDHAL3T2TDR | 3.2 TB | 39      | 304   | 0     | 0.83   |
| Samsung   | MZQL23T8HCLS-00... | 3.8 TB | 99      | 303   | 0     | 0.83   |
| Samsung   | MZPJB960HMGC-0BW07 | 960 GB | 12      | 301   | 0     | 0.83   |
| Toshiba   | KXD51RUE1T92       | 1.9 TB | 11      | 293   | 0     | 0.80   |
| Kingston  | SKC3000S1024G      | 1 TB   | 4       | 287   | 0     | 0.79   |
| Intel     | SSDPE2KE032T8      | 3.2 TB | 85      | 285   | 0     | 0.78   |
| Toshiba   | KXG60ZNV512G       | 512 GB | 63      | 284   | 0     | 0.78   |
| WDC       | WUS4BB096D7P3E1    | 960 GB | 488     | 283   | 0     | 0.78   |
| Samsung   | MZPLJ3T2HBJR-000H3 | 3.2 TB | 6       | 278   | 0     | 0.76   |
| Wester... | WUS4BB096D7P3E3    | 960 GB | 443     | 273   | 0     | 0.75   |
| Kingston  | SKC2500M8250G      | 250 GB | 5       | 271   | 0     | 0.74   |
| Intel     | SSDPEKKW010T8      | 1 TB   | 2       | 270   | 0     | 0.74   |
| Intel     | SSDPECME016T4      | 800 GB | 8       | 267   | 0     | 0.73   |
| Intel     | SSDPEKNW010T8      | 1 TB   | 8       | 267   | 0     | 0.73   |
| Samsung   | SSD 970 EVO        | 250 GB | 3       | 387   | 1     | 0.72   |
| Kingston  | SA2000M81000G      | 1 TB   | 8       | 261   | 0     | 0.72   |
| Corsair   | Force MP600        | 500 GB | 4       | 253   | 0     | 0.69   |
| Smartbuy  | m.2 PS5013-2280T   | 512 GB | 3       | 252   | 0     | 0.69   |
| Samsung   | MZQL2960HCJR-00A07 | 960 GB | 124     | 247   | 0     | 0.68   |
| Wester... | WUS4CB016D7P3E3    | 1.6 TB | 152     | 246   | 0     | 0.68   |
| Toshiba   | KXG60PNV2T04       | 2 TB   | 8       | 244   | 0     | 0.67   |
| WDC       | WUS4BB038D7P3E1    | 3.8 TB | 163     | 244   | 0     | 0.67   |
| ADATA     | SX8200PNP          | 1 TB   | 2       | 243   | 0     | 0.67   |
| HP        | SSD EX950          | 512 GB | 7       | 242   | 0     | 0.67   |
| Intel     | EO000375KWJUC      | 375 GB | 2       | 242   | 0     | 0.66   |
| Crucial   | CT500P5SSD8        | 500 GB | 5       | 240   | 0     | 0.66   |
| Samsung   | MZVLB256HAHQ-00000 | 256 GB | 14      | 237   | 0     | 0.65   |
| Intel     | SSDPE2NU076T8      | 7.6 TB | 3       | 236   | 0     | 0.65   |
| Corsair   | MP400              | 1 TB   | 20      | 230   | 0     | 0.63   |
| Samsung   | MZPLJ1T6HBJR-00007 | 1.6 TB | 4       | 228   | 0     | 0.62   |
| Dell      | Ent NVMe AGN RI... | 3.8 TB | 204     | 227   | 0     | 0.62   |
| Samsung   | MZPLJ6T4HALA-00007 | 6.4 TB | 41      | 224   | 0     | 0.61   |
| Micron    | 9300_MTFDHAL7T6TDP | 7.6 TB | 51      | 219   | 0     | 0.60   |
| Samsung   | MZ1L21T9HCLS-00A07 | 480 GB | 6       | 212   | 0     | 0.58   |
| Samsung   | SSD 970 EVO        | 1 TB   | 9       | 416   | 2     | 0.57   |
| Patriot   | P300               | 256 GB | 2       | 208   | 0     | 0.57   |
| WDC       | WDS100T3X0C-00SJG0 | 1 TB   | 94      | 204   | 0     | 0.56   |
| Samsung   | SSD 970 EVO Plus   | 1 TB   | 80      | 204   | 0     | 0.56   |
| Dell      | Ent NVMe CM6 RI... | 1.9 TB | 24      | 203   | 0     | 0.56   |
| Kingston  | SKC2500M81000G     | 1 TB   | 9       | 202   | 0     | 0.55   |
| Dell      | Ent NVMe AGN RI... | 7.6 TB | 72      | 201   | 0     | 0.55   |
| Samsung   | MZ1L21T9HCLS-00A07 | 472 GB | 4       | 200   | 0     | 0.55   |
| Toshiba   | KXG6AZNV512G       | 512 GB | 21      | 199   | 0     | 0.55   |
| Intel     | MDTPED1K750GA      | 752 GB | 7       | 199   | 0     | 0.55   |
| WDC       | WUS4BB038D7P3E4    | 3.8 TB | 18      | 197   | 0     | 0.54   |
| SK hynix  | SHGP31-1000GM-2    | 1 TB   | 5       | 196   | 0     | 0.54   |
| Micron    | 2200_MTFDHBA512TCK | 512 GB | 69      | 195   | 0     | 0.53   |
| Samsung   | MZQLB1T9HAJR-000AZ | 1.9 TB | 4       | 189   | 0     | 0.52   |
| Dell      | Express Flash C... | 960 GB | 132     | 187   | 0     | 0.51   |
| Intel     | SSDPE2KX010T7      | 1 TB   | 8       | 186   | 0     | 0.51   |
| Samsung   | MZ1L21T9HCLS-00A07 | 1.9 TB | 2       | 186   | 0     | 0.51   |
| Samsung   | SSD 970 EVO Plus   | 500 GB | 27      | 185   | 0     | 0.51   |
| Micron    | 7300_MTFDHBE6T4TDG | 6.4 TB | 24      | 182   | 0     | 0.50   |
| Intel     | SSDPF2KX019T1      | 1.9 TB | 10      | 180   | 0     | 0.50   |
| Intel     | SSDPF2KX076TZ      | 7.6 TB | 5       | 178   | 0     | 0.49   |
| Samsung   | SSD 970 EVO Plus   | 250 GB | 35      | 169   | 0     | 0.47   |
| Micron    | 7300_MTFDHBE3T8TDF | 3.8 TB | 26      | 168   | 0     | 0.46   |
| Patriot   | P300               | 128 GB | 4       | 166   | 0     | 0.45   |
| Crucial   | CT500P1SSD8        | 500 GB | 2       | 163   | 0     | 0.45   |
| Wester... | WUS4BB038D7P3E3    | 3.8 TB | 13      | 162   | 0     | 0.44   |
| Intel     | SSDPEKKW512G8      | 512 GB | 23      | 161   | 0     | 0.44   |
| Samsung   | MZVLB512HBJQ-00000 | 512 GB | 25      | 160   | 0     | 0.44   |
| WDC       | PC SN520 SDAPNU... | 128 GB | 2       | 157   | 0     | 0.43   |
| Samsung   | MZQL21T9HCJR-00... | 1.9 TB | 53      | 156   | 0     | 0.43   |
| Samsung   | MZPLJ1T6HBJR-00007 | 736 GB | 10      | 153   | 0     | 0.42   |
| Corsair   | MP600 PRO          | 2 TB   | 2       | 150   | 0     | 0.41   |
| Samsung   | MZVLB1T0HBLR-00000 | 1 TB   | 56      | 149   | 0     | 0.41   |
| WDC       | WUS4BB019D7P3E3    | 1.9 TB | 54      | 148   | 0     | 0.41   |
| Intel     | SSDPF2NV153TZ      | 15.... | 2       | 146   | 0     | 0.40   |
| Dell      | Ent NVMe P5600 ... | 1.6 TB | 39      | 143   | 0     | 0.39   |
| Samsung   | SSD 980            | 500 GB | 5       | 140   | 0     | 0.39   |
| Micron    | 7300_MTFDHBG3T8TDF | 3.8 TB | 8       | 137   | 0     | 0.38   |
| Intel     | SSDPF2KX076T1      | 3.8 TB | 30      | 136   | 0     | 0.37   |
| Toshiba   | KXG60ZNV256G       | 256 GB | 156     | 136   | 1     | 0.37   |
| Samsung   | MZPLJ3T2HBJR-00007 | 3.2 TB | 57      | 133   | 0     | 0.37   |
| WDC       | WUS3BA119C7P3E3    | 1.9 TB | 8       | 132   | 0     | 0.36   |
| Intel     | SSDPEKNW512G8      | 512 GB | 6       | 170   | 169   | 0.36   |
| WDC       | WUS4BB076D7P3E1    | 7.6 TB | 57      | 130   | 0     | 0.36   |
| XPG       | SPECTRIX S40G      | 4 TB   | 4       | 166   | 4     | 0.35   |
| Wester... | WUS4BB019D7P3E1    | 1.9 TB | 193     | 117   | 0     | 0.32   |
| ADATA     | SX8200PNP          | 512 GB | 5       | 117   | 0     | 0.32   |
| Micron    | 7300_MTFDHBG1T9TDF | 1.9 TB | 13      | 117   | 0     | 0.32   |
| Wester... | WUS4BB076D7P3E1    | 7.6 TB | 12      | 114   | 0     | 0.31   |
| Micron    | 2200_MTFDHBA256TCK | 256 GB | 18      | 114   | 0     | 0.31   |
| Kingston  | SA2000M8500G       | 500 GB | 4       | 111   | 0     | 0.31   |
| Micron    | MTFDHBA480TDF      | 480 GB | 8       | 110   | 0     | 0.30   |
| Micron    | 7300_MTFDHBA480TDF | 480 GB | 2       | 110   | 0     | 0.30   |
| Micron    | 7300_MTFDHBE7T6TDF | 7.6 TB | 5       | 109   | 0     | 0.30   |
| KIOXIA    | KCD6XLUL1T92       | 1.9 TB | 10      | 109   | 0     | 0.30   |
| HUAWEI    | HWE52P431T6M002N   | 1.6 TB | 2       | 108   | 0     | 0.30   |
| Kingston  | SEDC1000BM8240G    | 240 GB | 11      | 107   | 0     | 0.29   |
| Samsung   | MZVLB256HBHQ-00000 | 256 GB | 6       | 107   | 0     | 0.29   |
| Phison    | PCIe SSD           | 4 TB   | 7       | 105   | 0     | 0.29   |
| Samsung   | MZQL27T6HBLA-00A07 | 7.6 TB | 35      | 98    | 0     | 0.27   |
| Crucial   | CT1000P5SSD8       | 1 TB   | 4       | 98    | 0     | 0.27   |
| Wester... | WUS4BB096D7P3E1    | 960 GB | 200     | 97    | 0     | 0.27   |
| ADATA     | SX8200PNP          | 2 TB   | 3       | 96    | 0     | 0.26   |
| Transcend | TS2TMTE220S        | 2 TB   | 2       | 94    | 0     | 0.26   |
| ADATA     | SX6000LNP          | 1 TB   | 3       | 85    | 0     | 0.23   |
| Samsung   | SSD 983 DCT M.2    | 960 GB | 5       | 84    | 0     | 0.23   |
| Crucial   | CT1000P2SSD8       | 1 TB   | 3       | 81    | 0     | 0.22   |
| Samsung   | SSD 980 PRO        | 250 GB | 4       | 81    | 0     | 0.22   |
| SK hynix  | VO000960KXAVL      | 960 GB | 2       | 80    | 0     | 0.22   |
| Wester... | WUS4BB038D7P3E1    | 3.8 TB | 71      | 76    | 0     | 0.21   |
| ADATA     | SX6000PNP          | 256 GB | 2       | 74    | 0     | 0.20   |
| Micron    | 7300_MTFDHBE1T6TDG | 1.6 TB | 2       | 64    | 0     | 0.18   |
| ADATA     | LEGEND 900         | 2 TB   | 3       | 63    | 0     | 0.17   |
| Dell      | Express Flash N... | 6.4 TB | 4       | 63    | 0     | 0.17   |
| Micron    | 7400_MTFDKCB1T9TDZ | 1.9 TB | 5       | 61    | 0     | 0.17   |
| Samsung   | MZVL21T0HCLR-00B00 | 1 TB   | 10      | 60    | 0     | 0.17   |
| HP        | SSD FX900 Plus M.2 | 1 TB   | 6       | 59    | 0     | 0.16   |
| SanDisk   | WD Red SN700       | 500 GB | 3       | 59    | 0     | 0.16   |
| Transcend | TS512GMTE110S      | 512 GB | 4       | 57    | 0     | 0.16   |
| WDC       | WUS4CB032D7P3E4    | 3.2 TB | 5       | 54    | 0     | 0.15   |
| Samsung   | MZVLB256HAHQ-000L7 | 256 GB | 5       | 54    | 0     | 0.15   |
| Kingston  | SKC2500M8500G      | 500 GB | 4       | 53    | 0     | 0.15   |
| HUAWEI    | HWE56P43800M005N   | 800 GB | 3       | 48    | 0     | 0.13   |
| Kingston  | SKC2500M82000G     | 2 TB   | 3       | 44    | 0     | 0.12   |
| WDC       | WUS4BB096D7P3E4    | 960 GB | 4       | 43    | 0     | 0.12   |
| Gigabyte  | GP-GSM2NE3256GNTD  | 256 GB | 3       | 42    | 0     | 0.12   |
| Dell      | Ent NVMe AGN RI... | 1.9 TB | 3       | 41    | 0     | 0.11   |
| Samsung   | MZVLW256HEHP-000L7 | 256 GB | 2       | 41    | 0     | 0.11   |
| WDC       | WUS4BB076D7P3E3    | 7.6 TB | 124     | 35    | 0     | 0.10   |
| SanDisk   | WD_BLACK SN750 SE  | 1 TB   | 24      | 32    | 0     | 0.09   |
| Samsung   | SSD 970 EVO Plus   | 2 TB   | 60      | 29    | 0     | 0.08   |
| Intel     | SSDPELKX010T8      | 1 TB   | 3       | 26    | 0     | 0.07   |
| ADATA     | SX6000PNP          | 512 GB | 2       | 24    | 0     | 0.07   |
| SK hynix  | BC501A NVMe        | 128 GB | 3       | 21    | 0     | 0.06   |
| Crucial   | CT1000P5PSSD8      | 1 TB   | 3       | 20    | 0     | 0.06   |
| HP        | SSD EX900          | 1 TB   | 2       | 20    | 0     | 0.06   |
| Samsung   | SSD 980            | 250 GB | 6       | 19    | 0     | 0.05   |
| Wester... | WUS4BB096D7P3E4    | 960 GB | 4       | 13    | 0     | 0.04   |
| Wester... | WUS4CB032D7P3E4    | 3.2 TB | 4       | 11    | 0     | 0.03   |
| Samsung   | MZVL2512HCJQ-00B07 | 512 GB | 8       | 11    | 0     | 0.03   |
| Dell      | Ent NVMe v2 AGN... | 1.9 TB | 6       | 11    | 0     | 0.03   |
| Samsung   | MZQLB960HAJR-000AZ | 960 GB | 11      | 10    | 0     | 0.03   |
| Intel     | SSDPE2KE064T8      | 6.4 TB | 90      | 9     | 0     | 0.03   |
| GS Nan... | GS SSD U.2 DC      | 960 GB | 2       | 9     | 0     | 0.03   |
| Kingston  | SEDC1000BM8960G    | 960 GB | 7       | 8     | 0     | 0.02   |
| Netac     | NVMe SSD           | 256 GB | 3       | 5     | 0     | 0.01   |
| KIOXIA    | KCD61LUL3T84       | 3.8 TB | 20      | 5     | 0     | 0.01   |
| Kingston  | SEDC1000BM8480G    | 480 GB | 2       | 4     | 0     | 0.01   |
| Samsung   | MZVLB256HBHQ-000L7 | 256 GB | 3       | 4     | 0     | 0.01   |
| Samsung   | SSD 980 PRO        | 1 TB   | 2       | 3     | 0     | 0.01   |
| Samsung   | MZVLW128HEGR-00000 | 128 GB | 2       | 1     | 0     | 0.00   |
| Samsung   | SSD 980            | 1 TB   | 2       | 0     | 0     | 0.00   |

NVME by Vendor
--------------

Please take all columns into account when reading the table. Pay attention on the
number of tested samples and power-on days. Simultaneous high values of both MTBF
and errors are possible if only rare drives in the subset encounter errors.

Days - avg. days per sample,
Err  - avg. errors per sample,
MTBF - avg. MTBF in years per sample.

| MFG         | Models | Samples | Days  | Err   | MTBF |
|-------------|--------|---------|-------|-------|------|
| PNY         | 1      | 2       | 851   | 0     | 2.33   |
| Intel       | 72     | 2222    | 841   | 2     | 2.30   |
| HGST        | 1      | 24      | 504   | 0     | 1.38   |
| Seagate     | 1      | 10      | 428   | 0     | 1.17   |
| WDC         | 25     | 2783    | 367   | 1     | 1.00   |
| Phison      | 3      | 22      | 359   | 0     | 0.99   |
| Samsung     | 88     | 3429    | 359   | 2     | 0.97   |
| Dell        | 19     | 692     | 344   | 2     | 0.94   |
| Corsair     | 5      | 41      | 331   | 0     | 0.91   |
| Gigabyte... | 1      | 10      | 312   | 0     | 0.86   |
| Goodram     | 1      | 2       | 312   | 0     | 0.86   |
| Toshiba     | 11     | 363     | 309   | 1     | 0.85   |
| HUAWEI      | 3      | 7       | 263   | 0     | 0.72   |
| Smartbuy    | 1      | 3       | 252   | 0     | 0.69   |
| Kingston    | 16     | 95      | 247   | 0     | 0.68   |
| HP          | 4      | 25      | 245   | 0     | 0.67   |
| Western ... | 12     | 1373    | 241   | 0     | 0.66   |
| Micron      | 15     | 278     | 202   | 0     | 0.56   |
| Patriot     | 2      | 6       | 180   | 0     | 0.49   |
| ADATA       | 8      | 22      | 133   | 0     | 0.37   |
| Crucial     | 5      | 17      | 130   | 0     | 0.36   |
| XPG         | 1      | 4       | 166   | 4     | 0.35   |
| SK hynix    | 3      | 10      | 120   | 0     | 0.33   |
| Transcend   | 2      | 6       | 69    | 0     | 0.19   |
| Gigabyte    | 1      | 3       | 42    | 0     | 0.12   |
| KIOXIA      | 2      | 30      | 39    | 0     | 0.11   |
| SanDisk     | 2      | 27      | 35    | 0     | 0.10   |
| GS Nanotech | 1      | 2       | 9     | 0     | 0.03   |
| Netac       | 1      | 3       | 5     | 0     | 0.01   |

