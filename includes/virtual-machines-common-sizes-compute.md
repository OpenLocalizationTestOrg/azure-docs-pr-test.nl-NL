<!-- F-series, Fs-series* -->

F-serie is gebaseerd op Hallo 2,4 GHz Intel Xeon® E5-2673 v3-processor (Haswell), die zo hoog 3.1 GHz Hello Intel Turbo versterking Technology 2.0 kloksnelheid kunt bereiken. Dit is dezelfde Hallo CPU-prestaties als Hallo Dv2-serie van virtuele machines.  Hallo F-serie is op een lagere prijs per uur, aanbevolen waarde van de Hallo prijs-prestaties van hello Azure portfolio op basis van hello Azure Compute-eenheid (ACU) per vCPU. 

Virtuele machines uit de F-serie vormen een uitstekende keuze voor workloads die snellere CPU's nodig hebben, maar niet zo veel geheugen of tijdelijke opslag per vCPU.  Werkbelastingen, zoals analytics, gaming-servers, webservers en batchverwerking profiteren van Hallo-waarde van Hallo F-serie.

Hallo Fs-serie biedt alle voordelen van Hallo Hallo F-serie, in de toevoeging tooPremium opslag.

## <a name="fs-series"></a>Fs-serie*

ACU: 210 - 250

| Grootte | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Max. aantal gegevensschijven | Maximale doorvoer voor schijven met caching en tijdelijke opslag: IOPS / MBps (cachegrootte in GiB) | Max. doorvoer voor schijf zonder caching: IOPS/MBps | Maximum aantal NIC's/verwachte netwerkprestaties (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_F1s |1 |2 |4 |2 |4000 / 32 (12) |3200 / 48 |2 / 750 |
| Standard_F2s |2 |4 |8 |4 |8000 / 64 (24) |6400 / 96 |2 / 1500 |
| Standard_F4s |4 |8 |16 |8 |16.000 / 128 (48) |12.800 / 192 |4 / 3000 |
| Standard_F8s |8 |16 |32 |16 |32.000 / 256 (96) |25.600 / 384 |8 / 6000 |
| Standard_F16s |16 |32 |64 |32 |64.000 / 512 (192) |51.200 / 768 |8 / 6000-12000 &#8224; |

MBps = 10^6 bytes per seconde en GiB = 1024^3 bytes.

* Hallo maximale doorvoercapaciteit van de schijf (IOP's of MBps) mogelijk met een reeks Fs VM kan worden beperkt door Hallo nummer, grootte en striping Hallo een of meer schijven gekoppeld.  Zie [Premium Storage: High-performance storage for Azure virtual machine workloads](../articles/storage/common/storage-premium-storage.md) (Premium Storage: opslag met hoge prestaties voor Azure VM-workloads) voor meer informatie.


<br>

## <a name="f-series"></a>F-serie

ACU: 210 - 250

| Grootte         | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Maximale tijdelijke opslagdoorvoer: IOPS / MBps lezen / MBps schrijven | Maximumaantal gegevensschijven / doorvoer: IOPS | Maximum aantal NIC's/verwachte netwerkprestaties (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_F1  | 1         | 2           | 16             | 3000 / 46 / 23                                           | 2 / 2 x 500                         | 2 / 750                 |
| Standard_F2  | 2         | 4           | 32             | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1500                     |
| Standard_F4  | 4         | 8           | 64             | 12.000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 3000                     |
| Standard_F8  | 8         | 16          | 128            | 24.000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 6000                     |
| Standard_F16 | 16        | 32          | 256            | 48.000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000 - 12000 &#8224;           |


<br>


