<!-- A-series - compute-intensive instances, H-series -->

Hallo A8-A11 en H-serie grootten zijn ook wel bekend als *rekenintensieve exemplaren*. Hallo-hardware waarop deze formaten is ontworpen en geoptimaliseerd voor rekenintensieve en netwerk-intensieve toepassingen, met inbegrip van high-performance computing (HPC)-toepassingen, modellering en simulaties cluster. A8-A11 reeks Hallo Intel Xeon E5-2670 @ 2.6 GHZ en Hallo H-serie Intel Xeon E5-2667 v3 @ 3,2 GHz gebruikt. 

Virtuele machines in Azure H-serie zijn Hallo volgende generatie high performance computing-virtuele machines die zijn gericht op het hoge einde behoeften, zoals moleculaire modellering en computational fluid dynamics. Deze 8 en 16 vCPU VM's zijn gebaseerd op Hallo Intel Haswell E5 2667 V3 processortechnologie met DDR4 geheugen en voor op SSD gebaseerd tijdelijke opslag. 

Bovendien toohello aanzienlijk CPU-kracht, biedt Hallo H-serie diverse opties voor lage latentie RDMA netwerken met FDR InfiniBand en verschillende configuraties toosupport geheugen intensieve rekenkundige geheugenvereisten.



## <a name="h-series"></a>H-serie

ACU: 290-300

| Grootte | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | Max. aantal gegevensschijven | Max. doorvoer schijf: IOPS | Max. aantal NIC's |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |56 |1000 |16 |16 x 500 |2  |
| Standard_H16 |16 |112 |2000 |32 |32 x 500 |4 |
| Standard_H8m |8 |112 |1000 |16 |16 x 500 |2  |
| Standard_H16m |16 |224 |2000 |32 |32 x 500 |4  |
| Standard_H16r* |16 |112 |2000 |32 |32 x 500 |4  |
| Standard_H16mr* |16 |224 |2000 |32 |32 x 500 |4 |

*Toegewezen RDMA-back-endnetwerk is ingeschakeld voor MPI-toepassingen via FDR InfiniBand-netwerk, dat zeer lage latentie en hoge bandbreedte biedt.

<br>



## <a name="a-series---compute-intensive-instances"></a>A-serie: rekenintensieve exemplaren

ACU: 225

| Grootte | vCPU | Geheugen: GiB | Tijdelijke opslag (HDD): GiB | Max. aantal gegevensschijven | Max. doorvoer gegevensschijf: IOPS | Max. aantal NIC's|
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8* |8 |56 |382 |16 |16 x 500 |2 |
| Standard_A9* |16 |112 |382 |16 |16 x 500 |4 |
| Standard_A10 |8 |56 |382 |16 |16 x 500 |2  |
| Standard_A11 |16 |112 |382 |16 |16 x 500 |4 |

*Toegewezen RDMA-back-endnetwerk is ingeschakeld voor MPI-toepassingen via FDR InfiniBand-netwerk, dat zeer lage latentie en hoge bandbreedte biedt.

<br>



