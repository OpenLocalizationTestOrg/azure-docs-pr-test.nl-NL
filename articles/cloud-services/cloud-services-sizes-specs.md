---
title: aaaVirtual machine grootten voor Azure-cloudservices | Microsoft Docs
description: Een lijst met grootten van de andere virtuele machines hello (en -id's) voor Azure cloud service-web- en werkrollen rollen.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1127c23e-106a-47c1-a2e9-40e6dda640f6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 93d91a67afc352f3d18c31e0dd5cf976bf46350c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-cloud-services"></a>Grootten voor Cloudservices
Dit onderwerp beschrijft de beschikbare grootten Hallo en opties voor Cloudservice rolexemplaren (webrollen en werkrollen). Het bevat ook implementatie overwegingen toobe bij het plannen van toouse deze resources. Is een ID die u in plaats van elke grootte uw [servicedefinitiebestand](cloud-services-model-and-package.md#csdef). Prijzen voor elke grootte beschikbaar zijn op Hallo [Cloud Services-prijzen](https://azure.microsoft.com/pricing/details/cloud-services/) pagina.

> [!NOTE]
> toosee gerelateerde Azure-limieten, Zie [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md)
>
>

## <a name="sizes-for-web-and-worker-role-instances"></a>Grootten voor web- en werkrollen rolinstanties
Er zijn meerdere standaard grootten toochoose uit op Azure. Enkele overwegingen voor een aantal van deze grootten zijn:

* D-reeks VM's zijn ontworpen toorun toepassingen die hoger rekencapaciteit en prestaties van de tijdelijke schijf. D-reeks virtuele machines bieden snellere processors, een hogere ratio van geheugen-core- en een SSD-station (SSD) voor de tijdelijke schijf Hallo. Zie voor meer informatie Hallo aankondiging op hello Azure blog [nieuwe D-reeks voor de grootte van virtuele machines](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).
* Dv2-serie, een vervolgcontrole op het vlak toohello oorspronkelijke D-reeks biedt een krachtige CPU. Hallo CPU Dv2-serie is ongeveer 35% sneller dan Hallo D-reeks CPU. Is gebaseerd op Hallo nieuwste 2,4 GHz Intel Xeon® E5-2673 v3-processor (Haswell), en met Hallo Intel Turbo versterking Technology 2.0, up too3.1 GHz kunt gaan. Hallo Dv2-serie heeft dezelfde configuraties voor geheugen en schijfruimte Hallo zoals Hallo D-reeks.
* G-serie VMs Hallo bieden de meeste geheugen en uitgevoerd op hosts met Intel Xeon E5 V3-familie processor een.
* Hallo A-serie virtuele machines kan worden geïmplementeerd op verschillende hardwaretypen en processors. Hallo-grootte is beperkt, op basis van hardware hello, consistente processorprestaties toooffer voor Hallo met een exemplaar, ongeacht deze is geïmplementeerd op Hallo-hardware. toodetermine hello fysieke hardware waarop deze grootte is geïmplementeerd, query Hallo virtuele hardware uit binnen Hallo virtuele Machine.
* Hallo A0 grootte is te veel geabonneerde op Hallo fysieke hardware. Voor deze specifieke grootte alleen andere implementaties van de klant kunnen invloed hebben op prestaties van Hallo van uw workload uitgevoerd. Hallo relatieve prestaties worden hieronder beschreven als basislijn Hallo verwacht, onderwerp tooan geschatte variabiliteit van 15 procent.

Hallo-grootte van Hallo virtuele machine beïnvloedt Hallo prijzen. Hallo grootte zijn ook van invloed op de verwerking, geheugen en opslag capaciteit Hallo van Hallo virtuele machine. Opslagkosten zijn berekend afzonderlijk op basis van de gebruikte pagina's in Hallo storage-account. Zie voor meer informatie [Cloud Services Pricing Details](https://azure.microsoft.com/pricing/details/cloud-services/) en [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/).

Hallo na overwegingen kan helpen een grootte kiezen:

* Hallo A8-A11 en H-serie grootten zijn ook wel bekend als *rekenintensieve exemplaren*. Hallo-hardware waarop deze formaten is ontworpen en geoptimaliseerd voor rekenintensieve en netwerk-intensieve toepassingen, met inbegrip van high-performance computing (HPC)-toepassingen, modellering en simulaties cluster. A8-A11 reeks Hallo Intel Xeon E5-2670 @ 2.6 GHZ en Hallo H-serie Intel Xeon E5-2667 v3 @ 3,2 GHz gebruikt. Zie voor gedetailleerde informatie en overwegingen over het gebruik van deze formaten [hoge prestaties compute-VM-grootten](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Dv2-serie, D-reeks, G-serie zijn ideaal voor toepassingen die snellere CPU's, betere lokale schijf van de prestaties of hebben hogere geheugen eisen. Ze bieden een krachtige combinatie voor vele toepassingen op bedrijfsniveau.
* Enkele van de fysieke hosts Hallo in Azure-datacenters mogelijk geen ondersteuning voor grotere van virtuele machine, zoals A5 – A11. Als gevolg hiervan kunnen er Hallo foutbericht **mislukt tooconfigure virtuele machine {machine name}** of **mislukt toocreate virtuele machine {machine name}** wanneer het formaat van een bestaande virtuele machine tooa nieuwe grootte. maken van een nieuwe virtuele machine in een virtueel netwerk gemaakt vóór 16 April 2013; of het toevoegen van een nieuwe virtuele machine tooan bestaande cloudservice. Zie [fout: 'Mislukt tooconfigure virtuele machine'](https://social.msdn.microsoft.com/Forums/9693f56c-fcd3-4d42-850e-5e3b56c7d6be/error-failed-to-configure-virtual-machine-with-a5-a6-or-a7-vm-size?forum=WAVirtualMachinesforWindows) op Hallo ondersteuningsforum voor tijdelijke oplossingen voor elk implementatiescenario.
* Uw abonnement mogelijk ook het aantal kernen dat u in een bepaalde grootte families implementeren kunt Hallo beperken. een quotum tooincrease contact op met ondersteuning van Azure.

## <a name="performance-considerations"></a>Prestatieoverwegingen
We hebben gemaakt Hallo concept van hello Azure Compute-eenheid (ACU) tooprovide een manier om computerprestaties (CPU) in Azure-SKU's en tooidentify die SKU hoogstwaarschijnlijk toosatisfy is vergelijken de prestaties van uw behoeften.  ACU is momenteel gestandaardiseerd op 100 voor een kleine virtuele machine (Standard_A1). Alle andere SKU's geven vervolgens weer hoeveel sneller die SKU een standaardbenchmark ongeveer kan uitvoeren.

> [!IMPORTANT]
> Hallo ACU is alleen een richtlijn. Hallo-resultaten voor uw workload kunnen variëren.
>
>

<br>

| SKU-familie | ACU/kern |
| --- | --- |
| [ExtraSmall](#a-series) |50 |
| [Klein zijn](#a-series) |100 |
| [A5-7](#a-series) |100 |
| [Standard_A1-8v2](#av2-series) |100 |
| [Standard_A2m-8mv2](#av2-series) |100 |
| [A8-A11](#a-series) |225* |
| [D1-14](#d-series) |160 |
| [D1-15v2](#dv2-series) |210 - 250* |
| [G1-5](#g-series) |180 - 240* |
| [H](#h-series) |290 - 300* |

ACUs gemarkeerd met een * Intel® Turbo technologie tooincrease CPU frequentie gebruiken en een krachtige prestaties leveren. Hallo hoeveelheid Hallo versterking kan variëren op basis van VM-grootte hello, werkbelasting en andere werkbelastingen die worden uitgevoerd op Hallo dezelfde host.

## <a name="size-tables"></a>Groottetabellen
Hallo volgende tabellen bevatten Hallo grootten en Hallo capaciteiten die ze bieden.

* De opslagcapaciteit wordt weergegeven in GiB-eenheden of 1024^3 bytes. Wanneer het vergelijken van schijven gemeten in GB (1000 ^ 3 bytes) toodisks gemeten in GiB (1024 ^ 3) onthouden capaciteit getallen die zijn opgegeven in GiB lijkt kleiner. 1023 GiB is bijvoorbeeld gelijk aan 1098,4 GB
* De schijfdoorvoer wordt gemeten in I/O-bewerkingen per seconde (IOPS) en MBps, waarbij MBps = 10^6 bytes per seconde.
* Gegevensschijven kunnen in de modus met of zonder caching werken. Voor gegevens in de cache schijfbewerking, Hallo host-cachemodus te ingesteld**ReadOnly** of **ReadWrite**. Voor schijfbewerking uncached gegevens, Hallo host-cachemodus te ingesteld**geen**.
* Maximale netwerkbandbreedte is Hallo geaggregeerde Maximumbandbreedte toegewezen en toegewezen per VM-type. de maximale bandbreedte Hallo biedt richtlijnen voor het selecteren van Hallo rechts VM type tooensure voldoende netwerkcapaciteit zijn beschikbaar. Wanneer u verplaatst tussen de laag, Gemiddeld, hoog en zeer hoge, neemt Hallo doorvoer toe. De werkelijke netwerkprestaties zijn afhankelijk van talloze factoren, waaronder de netwerk- en toepassingsbelastingen en de instellingen van het toepassingsnetwerk.

## <a name="a-series"></a>A-serie
| Grootte            | CPU-kernen | Geheugen: GiB  | Lokale HDD: GiB       | Max. aantal NIC's/netwerkbandbreedte |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| ExtraSmall      | 1         | 0,768        | 20                   | 1/laag |
| Klein           | 1         | 1,75         | 225                  | 1/gemiddeld |
| Middelgroot          | 2         | 3,5 GB       | 490                  | 1/gemiddeld |
| Groot           | 4         | 7            | 1000                 | 2/hoog |
| Zijn      | 8         | 14           | 2040                 | 4/hoog |
| A5              | 2         | 14           | 490                  | 1/gemiddeld |
| A6              | 4         | 28           | 1000                 | 2/hoog |
| A7              | 8         | 56           | 2040                 | 4/hoog |

## <a name="a-series---compute-intensive-instances"></a>A-serie: rekenintensieve exemplaren
Zie voor informatie en overwegingen over het gebruik van deze formaten [hoge prestaties compute-VM-grootten](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

| Grootte            | CPU-kernen | Geheugen: GiB  | Lokale HDD: GiB       | Max. aantal NIC's/netwerkbandbreedte |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| A8 *             |8          | 56           | 1817                 | 2/hoog |
| A9 *             |16         | 112          | 1817                 | 4/zeer hoog |
| A10             |8          | 56           | 1817                 | 2/hoog |
| A11             |16         | 112          | 1817                 | 4/zeer hoog |

\*RDMA-compatibele

## <a name="av2-series"></a>Av2-serie

| Grootte            | CPU-kernen | Geheugen: GiB  | Lokale SSD: GiB       | Max. aantal NIC's/netwerkbandbreedte |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_A1_v2  | 1         | 2            | 10                   | 1/gemiddeld                 |
| Standard_A2_v2  | 2         | 4            | 20                   | 2/gemiddeld                 |
| Standard_A4_v2  | 4         | 8            | 40                   | 4/hoog                     |
| Standard_A8_v2  | 8         | 16           | 80                   | 8/hoog                     |
| Standard_A2m_v2 | 2         | 16           | 20                   | 2/gemiddeld                 |
| Standard_A4m_v2 | 4         | 32           | 40                   | 4/hoog                     |
| Standard_A8m_v2 | 8         | 64           | 80                   | 8/hoog                     |


## <a name="d-series"></a>D-serie
| Grootte            | CPU-kernen | Geheugen: GiB  | Lokale SSD: GiB       | Max. aantal NIC's/netwerkbandbreedte |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1     | 1         | 3,5          | 50                   | 1/gemiddeld |
| Standard_D2     | 2         | 7            | 100                  | 2/hoog |
| Standard_D3     | 4         | 14           | 200                  | 4/hoog |
| Standard_D4     | 8         | 28           | 400                  | 8/hoog |
| Standard_D11    | 2         | 14           | 100                  | 2/hoog |
| Standard_D12    | 4         | 28           | 200                  | 4/hoog |
| Standard_D13    | 8         | 56           | 400                  | 8/hoog |
| Standard_D14    | 16        | 112          | 800                  | 8/zeer hoog |

## <a name="dv2-series"></a>Dv2-serie
| Grootte            | CPU-kernen | Geheugen: GiB  | Lokale SSD: GiB       | Max. aantal NIC's/netwerkbandbreedte |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1_v2  | 1         | 3,5          | 50                   | 1/gemiddeld |
| Standard_D2_v2  | 2         | 7            | 100                  | 2/hoog |
| Standard_D3_v2  | 4         | 14           | 200                  | 4/hoog |
| Standard_D4_v2  | 8         | 28           | 400                  | 8/hoog |
| Standard_D5_v2  | 16        | 56           | 800                  | 8/zeer hoog |
| Standard_D11_v2 | 2         | 14           | 100                  | 2/hoog |
| Standard_D12_v2 | 4         | 28           | 200                  | 4/hoog |
| Standard_D13_v2 | 8         | 56           | 400                  | 8/hoog |
| Standard_D14_v2 | 16        | 112          | 800                  | 8/zeer hoog |
| Standard_D15_v2 | 20        | 140          | 1000                | 8/zeer hoog |

## <a name="g-series"></a>G-serie
| Grootte            | CPU-kernen | Geheugen: GiB  | Lokale SSD: GiB       | Max. aantal NIC's/netwerkbandbreedte |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_G1     | 2         | 28           | 384                  |1/hoog |
| Standard_G2     | 4         | 56           | 768                  |2/hoog |
| Standard_G3     | 8         | 112          | 1536                |4/zeer hoog |
| Standard_G4     | 16        | 224          | 3072                |8/zeer hoog |
| Standard_G5     | 32        | 448          | 6144                |8/zeer hoog |

## <a name="h-series"></a>H-serie
Virtuele machines in Azure H-serie zijn Hallo volgende generatie high performance computing-virtuele machines die zijn gericht op het hoge einde behoeften, zoals moleculaire modellering en computational fluid dynamics. Deze 8 en 16-core virtuele machines zijn gebouwd op Hallo Intel Haswell E5 2667 V3 processortechnologie met DDR4 geheugen en lokale opslag voor op SSD gebaseerd.

Bovendien toohello aanzienlijk CPU-kracht, biedt Hallo H-serie diverse opties voor lage latentie RDMA netwerken met FDR InfiniBand en verschillende configuraties toosupport geheugen intensieve rekenkundige geheugenvereisten.

| Grootte            | CPU-kernen | Geheugen: GiB  | Lokale SSD: GiB       | Max. aantal NIC's/netwerkbandbreedte |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_H8     | 8         | 56           | 1000                 | 8/hoog |
| Standard_H16    | 16        | 112          | 2000                 | 8/zeer hoog |
| Standard_H8m    | 8         | 112          | 1000                 | 8/hoog |
| Standard_H16m   | 16        | 224          | 2000                 | 8/zeer hoog |
| Standard_H16r*  | 16        | 112          | 2000                 | 8/zeer hoog |
| Standard_H16mr* | 16        | 224          | 2000                 | 8/zeer hoog |

\*RDMA-compatibele

## <a name="configure-sizes-for-cloud-services"></a>Grootten voor Cloud-Services configureren
U kunt Hallo de grootte van de virtuele Machine van een rolexemplaar opgeven als onderdeel van de ServiceModel Hallo beschreven door Hallo [servicedefinitiebestand](cloud-services-model-and-package.md#csdef). Hallo-grootte van Hallo rol bepaalt Hallo aantal CPU-kernen, Hallo geheugencapaciteit en Hallo lokale systeem bestandsgrootte op die met een exemplaar van tooa is toegewezen. Kies de grootte van de rol Hallo op basis van de vereisten van uw toepassing.

Hier volgt een voorbeeld voor het instellen van Hallo rol grootte toobe [Standard_D2](#general-purpose-d) voor een exemplaar van de Webrol:

```xml
<WorkerRole name="Worker1" vmsize="Standard_D2">
...
</WorkerRole>
```

## <a name="changing-hello-size-of-an-existing-role"></a>Hallo-grootte van een bestaande rol wijzigen

Als Hallo aard van uw werkbelasting wordt gewijzigd of nieuwe VM-grootten beschikbaar, wilt u wellicht toochange Hallo grootte van uw rol. toodo zodat u moet Hallo VM-grootte in het servicedefinitiebestand wijzigen (zoals hierboven) opnieuw inpakken van uw Cloud-Service en implementeren. Het is niet mogelijk toochange VM-grootten rechtstreeks vanuit het Hallo-portal of PowerShell.

>[!TIP]
> U kunt andere VM-grootten toouse voor uw rol in verschillende omgevingen (bv. Test tegenover productie). Eenzijdige toodo dit toocreate is meerdere service-definitie (.csdef)-bestanden in uw project en maak vervolgens andere cloud servicepakketten per omgeving tijdens uw geautomatiseerde opbouw met Hallo CSPack hulpprogramma. toolearn meer informatie over het Hallo-elementen van een cloud services-pakket en hoe toocreate die ze zien [wat is er Hallo cloud services-model en hoe ik dit pakket?](cloud-services-model-and-package.md)
>
>

## <a name="get-a-list-of-sizes"></a>Een lijst met grootten
U kunt PowerShell of REST-API tooget een lijst met grootten hello gebruiken. Hallo REST-API wordt beschreven [hier](https://msdn.microsoft.com/library/azure/dn469422.aspx). Hallo is volgende code een PowerShell-opdracht met alle Hallo grootten momenteel beschikbaar is voor uw Cloud-Service.

```powershell
Get-AzureRoleSize | where SupportedByWebWorkerRoles -eq $true | select InstanceSize
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie: [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md) (Limieten van Azure-abonnementen en -services, quota en beperkingen).
* Meer informatie [over hoge prestaties compute VM-grootten](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor HPC-workloads.
