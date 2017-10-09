
* Hallo M-serie biedt Hallo hoogste vCPU count (omhoog too128 vcpu's) en de grootste geheugen (omhoog too2.0 TiB) van een virtuele machine in Hallo cloud.  Dit is ideaal voor zeer grote databases of andere toepassingen die zo kunnen profiteren van een groot aantal vCPU’s en grote hoeveelheden geheugen.

* Dv2-serie, D-reeks, G-serie, en Hallo DS/GS collega's zijn ideaal voor toepassingen die vraag sneller Vcpu, betere prestaties van de tijdelijke opslag, of hebben hogere geheugen eisen.  Ze bieden een krachtige combinatie voor vele toepassingen op bedrijfsniveau.

* D-reeks VM's zijn ontworpen toorun toepassingen die hoger rekencapaciteit en prestaties van de tijdelijke schijf. Virtuele machines uit de D-serie hebben snellere processors, een hogere geheugen-naar-vCPU-snelheid en een SSD (solid-state drive) voor tijdelijke opslag. Zie voor meer informatie Hallo aankondiging op hello Azure blog [nieuwe D-reeks voor de grootte van virtuele machines](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

* Dv2-serie, een vervolgcontrole op het vlak toohello oorspronkelijke D-reeks biedt een krachtige CPU. Hallo CPU Dv2-serie is ongeveer 35% sneller dan Hallo D-reeks CPU. Is gebaseerd op Hallo nieuwste 2,4 GHz Intel Xeon® E5-2673 v3-processor (Haswell), en met Hallo Intel Turbo versterking Technology 2.0, up too3.1 GHz kunt gaan. Hallo Dv2-serie heeft dezelfde configuraties voor geheugen en schijfruimte Hallo zoals Hallo D-reeks.


## <a name="esv3-series"></a>ESv3-serie

ACU: 160-190

ESv3-serie exemplaren zijn gebaseerd op Hallo 2.3 GHz Intel XEON® E5-2673 v4-processor (Broadwell) en kunnen bereiken 3.5GHz met Intel Turbo versterking technologie 2.0 en premium-opslag gebruiken. Ev3-exemplaren zijn ideaal voor geheugenintensieve bedrijfstoepassingen.


| Grootte             | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Max. aantal gegevensschijven | Maximale doorvoer voor schijven met caching en tijdelijke opslag: IOPS / MBps (cachegrootte in GiB) | Max. doorvoer voor schijf zonder caching: IOPS/MBps | Maximum aantal NIC's/verwachte netwerkprestaties (Mbps) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standard_E2s_v3  | 2      | 16          | 32             | 4              | 4,000 / 32 (50)                                                       | 3200 / 48                                | 2/gemiddeld                                   |
| Standard_E4s_v3  | 4      | 32          | 64             | 8              | 8,000 / 64 (100)                                                      | 6400 / 96                                | 2/gemiddeld                                   |
| Standard_E8s_v3  | 8      | 64          | 128            | 16             | 16,000 / 128 (200)                                                    | 12.800 / 192                              | 4/hoog                                       |
| Standard_E16s_v3 | 16     | 128         | 256            | 32             | 32,000 / 256 (400)                                                    | 25.600 / 384                              | 8/hoog                                       |
| Standard_E32s_v3 | 32     | 256         | 512            | 32             | 64,000 / 512 (800)                                                    | 51.200 / 768                              | 8/zeer hoog                             |
| Standard_E64s_v3 | 64     | 432         | 864            | 32             | 128,000/1024 (1600)                                                   | 80,000 / 1200                             | 8/zeer hoog                             |



## <a name="ev3-series"></a>Ev3-serie

ACU: 160 - 190 

Ev3-serie exemplaren zijn gebaseerd op Hallo 2.3 GHz Intel XEON® E5-2673 v4-processor (Broadwell) 3.5GHz met Intel Turbo versterking technologie 2.0 kan worden bereikt. Ev3-exemplaren zijn ideaal voor geheugenintensieve bedrijfstoepassingen.

Gegevensschijfopslag wordt apart van virtuele machines in rekening gebracht. toouse premium-opslag-schijven gebruiken Hallo ESv3 grootten. Hallo-prijzen en facturering meters voor ESv3 grootten zijn hetzelfde als Ev3-serie Hallo. 


| Grootte            | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Max. aantal gegevensschijven | Maximale tijdelijke opslagdoorvoer: IOPS / MBps lezen / MBps schrijven | Max. aantal NIC's/netwerkbandbreedte |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standard_E2_v3  | 2         | 16          | 50             | 4              | 3000/46/23                                               | 2/gemiddeld                 |
| Standard_E4_v3  | 4         | 32          | 100            | 8              | 6000/93/46                                               | 2/gemiddeld                 |
| Standard_E8_v3  | 8         | 64          | 200            | 16             | 12000/187/93                                             | 4/hoog                     |
| Standard_E16_v3 | 16        | 128         | 400            | 32             | 24000/375/187                                            | 8/hoog                     |
| Standard_E32_v3 | 32        | 256         | 800            | 32             | 48000/750/375                                            | 8/zeer hoog           |
| Standard_E64_v3 | 64        | 432         | 1600           | 32             | 96000/1000/500                                           | 8/zeer hoog           |


## <a name="m-series"></a>M-serie*

ACU: 160-180

| Grootte            | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Max. aantal gegevensschijven | Maximale doorvoer voor schijven met caching en tijdelijke opslag: IOPS / MBps (cachegrootte in GiB) | Max. doorvoer voor schijf zonder caching: IOPS/MBps | Maximum aantal NIC's/verwachte netwerkprestaties (Mbps) |
|-----------------|------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------|
| Standard_M64ms  | 64   | 1792        | 2048           | 32             | 80,000 / 800 (6348)       | 40.000 / 1,000                            | 8 / 16000          |
| Standard_M128s** | 128  | 2048        | 4096           | 64             | 160,000 / 1,600 (12,696) | 80.000 / 2000                            | 8 / 25000          |



*Virtuele machine uit de M-serie zijn uitgerust met Intel® Hyper-Threading-technologie

**Bij meer dan 64 vCPU’s is een van deze ondersteunde gastbesturingssystemen vereist: Windows Server 2016, Ubuntu 16.04 TNS, SLES 12 SP2, en Red Hat Enterprise Linux of CentOS 7.3 met LIS 4.2.1 

<br>

## <a name="gs-series"></a>GS-serie*

ACU: 180 - 240

| Grootte | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Max. aantal gegevensschijven | Maximale doorvoer voor schijven met caching en tijdelijke opslag: IOPS / MBps (cachegrootte in GiB) | Max. doorvoer voor schijf zonder caching: IOPS/MBps | Maximum aantal NIC's/verwachte netwerkprestaties (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_GS1 |2 |28 |56 |4 |10.000 / 100 (264) |5000 / 125 |2 / 2000 |
| Standard_GS2 |4 |56 |112 |8 |20.000 / 200 (528) |10.000 / 250 |2 / 4000 |
| Standard_GS3 |8 |112 |224 |16 |40.000 / 400 (1,056) |20.000 / 500 |4 / 8000 |
| Standard_GS4 |16 |224 |448 |32 |80.000 / 800 (2,112) |40.000 / 1,000 |8 / 6000 - 16000 &#8224; |
| Standard_GS5** |32 |448 |896 |64 |160.000 / 1600 (4,224) |80.000 / 2000 |8 / 20000 |

* Hallo maximale doorvoercapaciteit van de schijf (IOP's of MBps) mogelijk een GS-serie VM kan worden beperkt door Hallo nummer, grootte en striping Hallo een of meer schijven gekoppeld. Zie [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/storage/common/storage-premium-storage.md) (Premium Storage: opslag met hoge prestaties voor Azure VM-workloads) voor meer informatie. 

** Exemplaar is geïsoleerd toohardware toegewezen tooa één klant.


<br>

## <a name="g-series"></a>G-serie

ACU: 180 - 240

| Grootte         | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Maximale tijdelijke opslagdoorvoer: IOPS / MBps lezen / MBps schrijven | Maximumaantal gegevensschijven / doorvoer: IOPS | Maximum aantal NIC's/verwachte netwerkprestaties (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_G1  | 2         | 28          | 384            | 6000 / 93 / 46                                           | 4 / 4 x 500                       | 2 / 2000                     |
| Standard_G2  | 4         | 56          | 768            | 12.000 / 187 / 93                                         | 8 / 8 x 500                       | 2 / 4000                     |
| Standard_G3  | 8         | 112         | 1536          | 24.000 / 375 / 187                                        | 16 / 16 x 500                     | 4 / 8000                |
| Standard_G4  | 16        | 224         | 3072          | 48.000 / 750 / 375                                        | 32 / 32 x 500                     | 8 / 6000 - 16000 &#8224;          |
| Standard_G5* | 32        | 448         | 6144          | 96.000 / 1500 / 750                                       | 64 / 64 x 500                     | 8 / 20000           |

* Exemplaar is geïsoleerd toohardware toegewezen tooa één klant.
<br>


## <a name="dsv2-series"></a>DSv2-serie*

ACU: 210 - 250

| Grootte | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Max. aantal gegevensschijven | Maximale doorvoer voor schijven met caching en tijdelijke opslag: IOPS / MBps (cachegrootte in GiB) | Max. doorvoer voor schijf zonder caching: IOPS/MBps | Maximum aantal NIC's/verwachte netwerkprestaties (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11_v2 |2 |14 |28 |4 |8000 / 64 (72) |6400 / 96 |2 / 1500 |
| Standard_DS12_v2 |4 |28 |56 |8 |16.000 / 128 (144) |12.800 / 192 |4 / 3000 |
| Standard_DS13_v2 |8 |56 |112 |16 |32.000 / 256 (288) |25.600 / 384 |8 / 6000 |
| Standard_DS14_v2 |16 |112 |224 |32 |64.000 / 512 (576) |51.200 / 768 |8 / 6000 - 12000 &#8224; |
| Standard_DS15_v2** |20 |140 |280 |40 |80.000 / 640 (720) |64.000 / 960 |8 / 20000***

* Hallo maximale doorvoercapaciteit van de schijf (IOP's of MBps) mogelijk met een reeks DSv2 VM kan worden beperkt door Hallo nummer, grootte en striping Hallo een of meer schijven gekoppeld.  Zie [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/storage/common/storage-premium-storage.md) (Premium Storage: opslag met hoge prestaties voor Azure VM-workloads) voor meer informatie.

** Exemplaar is een geïsoleerde knooppunt dat wordt gegarandeerd dat de VM alleen een VM op onze knooppunt Intel Haswell Hallo.

***25000 Mbps met versneld netwerken.

<br>

## <a name="dv2-series"></a>Dv2-serie

ACU: 210 - 250

| Grootte              | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Maximale tijdelijke opslagdoorvoer: IOPS / MBps lezen / MBps schrijven | Maximumaantal gegevensschijven / doorvoer: IOPS | Maximum aantal NIC's/verwachte netwerkprestaties (Mbps) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11_v2   | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1500                     |
| Standard_D12_v2   | 4         | 28          | 200            | 12.000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 3000                     |
| Standard_D13_v2   | 8         | 56          | 400            | 24.000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 6000                     |
| Standard_D14_v2   | 16        | 112         | 800            | 48.000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000 - 12000 &#8224;          |
| Standard_D15_v2* | 20        | 140         | 1000          | 60.000 / 937 / 468                                        | 40 / 40 x 500                       | 8 / 20000** |

* Exemplaar is een geïsoleerde knooppunt dat wordt gegarandeerd dat de VM alleen een VM op onze knooppunt Intel Haswell Hallo.

**25000 Mbps met versneld netwerken.

<br>

## <a name="ds-series"></a>DS-serie*

ACU: 160

| Grootte | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Max. aantal gegevensschijven | Maximale doorvoer voor schijven met caching en tijdelijke opslag: IOPS / MBps (cachegrootte in GiB) | Max. doorvoer voor schijf zonder caching: IOPS/MBps | Maximum aantal NIC's/verwachte netwerkprestaties (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11 |2 |14 |28 |4 |8000 / 64 (72) |6400 / 64 |2 / 1000 |
| Standard_DS12 |4 |28 |56 |8 |16.000 / 128 (144) |12.800 / 128 |4 / 2000 |
| Standard_DS13 |8 |56 |112 |16 |32.000 / 256 (288) |25.600 / 256 |8 / 4000 |
| Standard_DS14 |16 |112 |224 |32 |64.000 / 512 (576) |51.200 / 512 |8 / 6000 - 8000 &#8224; |

* Hallo maximale doorvoercapaciteit van de schijf (IOP's of MBps) mogelijk met een DS-serie VM kan worden beperkt door Hallo nummer, grootte en striping Hallo een of meer schijven gekoppeld.  Zie [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/storage/common/storage-premium-storage.md) (Premium Storage: opslag met hoge prestaties voor Azure VM-workloads) voor meer informatie.


## <a name="d-series"></a>D-serie

ACU: 160

| Grootte         | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Maximale tijdelijke opslagdoorvoer: IOPS / MBps lezen / MBps schrijven | Maximumaantal gegevensschijven / doorvoer: IOPS | Maximum aantal NIC's/verwachte netwerkprestaties (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11 | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1000                     |
| Standard_D12 | 4         | 28          | 200            | 12.000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 2000                     |
| Standard_D13 | 8         | 56          | 400            | 24.000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 4000                     |
| Standard_D14 | 16        | 112         | 800            | 48.000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000 - 8000 &#8224;                |

<br>

