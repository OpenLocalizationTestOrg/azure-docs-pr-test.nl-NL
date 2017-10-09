---
title: aaaDesign en implementeer een Oracle-database in Azure | Microsoft Docs
description: Ontwerpen en implementeren van een Oracle-database in uw Azure-omgeving.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a>Ontwerpen en implementeren van een Oracle-database in Azure

## <a name="assumptions"></a>Veronderstellingen

- U bent van plan een Oracle-database van de lokale tooAzure toomigrate.
- U hebt een goed begrip van Hallo verschillende metrische gegevens in rapporten voor Oracle AWR.
- U hebt een basislijn begrip van de prestaties van toepassingen en platforms te gebruiken.

## <a name="goals"></a>Doelstellingen

- Begrijpen hoe toooptimize uw Oracle-implementatie in Azure.
- Gebruik de opties voor een Oracle-database in een Azure-omgeving afstemmen van de prestaties.

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a>Hallo verschillen tussen een on-premises en Azure-implementatie 

Hieronder volgen enkele belangrijke dingen tookeep rekening moet houden bij waarnaar u migreert lokale toepassingen tooAzure. 

Een belangrijk verschil is dat de resources, zoals virtuele machines, schijven en virtuele netwerken in een Azure-implementatie moet worden gedeeld door andere clients. Resources kunnen bovendien worden beperkt op basis van Hallo vereisten. In plaats van te focussen op het voorkomen (MBTF) mislukt, wordt Azure meer gericht op functionerende hallo-fout (MTTR).

Hallo volgende tabel bevat enkele van Hallo verschillen tussen een lokale implementatie en een Azure-implementatie van een Oracle-database.

> 
> |  | **Lokale implementatie** | **Azure-implementatie** |
> | --- | --- | --- |
> | **Netwerken** |LAN/WAN  |SDN (software gedefinieerde netwerken)|
> | **Beveiligingsgroep** |Hulpprogramma's voor beperking van de IP/poort |[Netwerkbeveiligingsgroep (NSG)](https://azure.microsoft.com/blog/network-security-groups) |
> | **Herstelmogelijkheden** |MBTF (gemiddelde tijd tussen storingen) |MTTR (tussentijd toorecovery)|
> | **Gepland onderhoud** |Patchen of upgrades worden uitgevoerd|[Beschikbaarheidssets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patchen/upgrades worden beheerd door Azure) |
> | **Resource** |Toegewezen  |Gedeeld met andere clients|
> | **Regio 's** |Datacenters |[Regio paren](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | **Storage** |SAN of fysieke schijven |[Beheerde Azure-opslag](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | **Schalen** |Verticale schaal |Horizontaal schalen|


### <a name="requirements"></a>Vereisten

- Hallo database grootte en groei snelheid bepalen.
- Hallo IOPS vereisten, kunt u schatten op basis van Oracle AWR rapporten of andere hulpprogramma's voor Netwerkcontrole bepalen.

## <a name="configuration-options"></a>Configuratie-opties

Er zijn vier mogelijke gebieden dat kunt u de afstemmen tooimprove prestaties in een Azure-omgeving:

- Grootte van virtuele machine
- Netwerkdoorvoer
- Schijftypen en configuraties
- Schijf-cache-instellingen

### <a name="generate-an-awr-report"></a>Een AWR genereren

Als u een bestaande een Oracle-database en toomigrate tooAzure van plan bent, hebt u verschillende mogelijkheden. U kunt uitvoeren Hallo Oracle AWR rapport tooget Hallo metrische gegevens (IOP's, Mbps, GiBs, enzovoort). Kies vervolgens Hallo die VM op basis van Hallo metrische gegevens die u hebt verzameld. Of u kunt contact opnemen met uw team tooget vergelijkbare informatie over de infrastructuur.

U kunt uw rapport AWR uitvoeren tijdens normale en piekuren werkbelastingen, zodat u kunt vergelijken. Op basis van deze rapporten, kunt u virtuele machines op basis van gemiddelde werkbelasting Hallo of de maximale werkbelasting Hallo Hallo groot.

Hieronder volgt een voorbeeld van hoe u een rapport AWR toogenerate:

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a>De belangrijkste metrische gegevens

Hieronder vindt u Hallo metrische gegevens die u van Hallo AWR rapport verkrijgen kunt:

- Totaal aantal kernen
- CPU-kloksnelheid
- Totale geheugen in GB
- CPU-gebruik
- Overdrachtssnelheid piek
- Het aantal i/o-wijzigingen (lezen/schrijven)
- Opnieuw logboek snelheid (MBPs)
- Netwerkdoorvoer
- Netwerk latentie snelheid (laag/hoog)
- Databasegrootte in GB
- Bytes ontvangen via SQL * Net van / tooclient

### <a name="virtual-machine-size"></a>Grootte van virtuele machine

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a>1. Schatting maken van VM-grootte op basis van CPU, geheugen en i/o-gebruik van Hallo AWR rapport

Wat die u mogelijk bekijkt is hello bovenste vijf is een time-out opgetreden voor gebeurtenissen die aangeven waar knelpunten in het systeem Hallo zijn.

Bijvoorbeeld in Hallo diagram te volgen, Hallo log-bestand synchronisatie wordt Hallo boven. Hiermee wordt aangegeven Hallo aantal wacht die vereist zijn voordat Hallo LGWR Hallo buffer toohello opnieuw logboek logboekbestand worden geschreven. Deze resultaten blijkt dat beter presterende opslag of schijven vereist zijn. Hallo diagram toont bovendien ook Hallo aantal CPU (kernen) en Hallo en de hoeveelheid geheugen.

![Schermafbeelding van pagina Hallo AWR-rapport](./media/oracle-design/cpu_memory_info.png)

Hallo toont volgende diagram Hallo totale i/o lezen en schrijven. Er zijn 59 lezen en 247.3 GB tijdens Hallo van Hallo rapport geschreven.

![Schermafbeelding van pagina Hallo AWR-rapport](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a>2. Kies een virtuele machine

Op basis van het Hallo-informatie die u hebt verzameld van Hallo AWR rapport, is de volgende stap Hallo toochoose een virtuele machine met een vergelijkbare grootte die voldoet aan uw. U vindt een lijst met beschikbare virtuele machines in Hallo artikel [geoptimaliseerd voor geheugen](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a>3. Hallo VM sizing stemmen met een vergelijkbare VM-reeks op basis van Hallo ACU

Nadat u hebt gekozen Hallo VM, betaalt u aandacht toohello ACU voor Hallo VM. U kunt een andere virtuele machine op basis van Hallo ACU-waarde die beter aansluit bij uw behoeften. Zie voor meer informatie [Azure compute eenheid](https://docs.microsoft.com/azure/virtual-machines/windows/acu).

![Schermafbeelding van Hallo ACU eenheden-pagina](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a>Netwerkdoorvoer

Hallo volgende diagram ziet u Hallo relatie tussen de doorvoer en IOP's:

![Schermopname van doorvoer](./media/oracle-design/throughput.png)

de totale netwerkdoorvoer Hallo geschat op basis van de volgende informatie Hallo:
- SQL * Net verkeer
- MBps x het aantal servers (uitgaande stream zoals Oracle Data Guard)
- Andere factoren, zoals toepassing replicatie

![Schermopname van Hallo SQL * Net doorvoer](./media/oracle-design/sqlnet_info.png)

Op basis van de vereisten van uw netwerkbandbreedte, zijn er verschillende gatewaytypen voor toochoose van. Het gaat hierbij om basic, VpnGw en Azure ExpressRoute. Zie voor meer informatie, Hallo [VPN-gateway pagina met prijzen](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).

**Aanbevelingen**

- Netwerklatentie is hoger dan tooan on-premises implementatie. Netwerk ronde reizen kan aanzienlijk verminderen, de prestaties verbeteren.
- tooreduce retourbewerkingen, consolideren toepassingen met hoge transacties of 'chatty' apps op Hallo dezelfde virtuele machine.

### <a name="disk-types-and-configurations"></a>Schijftypen en configuraties

- *Standaard OS schijven*: deze schijftypen bieden permanente gegevens en opslaan in cache. Ze zijn geoptimaliseerd voor OS toegang bij het opstarten en zijn niet bedoeld voor transactionele of datawarehouse-werkbelastingen (analytische).

- *Schijven zonder begeleiding*: met deze schijftypen die u beheert Hallo storage-accounts die Hallo virtuele harde schijf (VHD)-bestanden die overeenkomen met tooyour VM schijven opslaan. VHD-bestanden worden opgeslagen als pagina-blobs in Azure storage-accounts.

- *Schijven die worden beheerd*: Azure beheert Hallo storage-accounts die u voor uw VM-schijven gebruikt. U geeft Hallo schijftype (premium of standaard) en Hallo grootte van Hallo-schijf die u nodig hebt. Azure maakt en beheert de Hallo schijf voor u.

- *Premium-opslag-schijven*: deze schijftypen geschikt zijn voor productieworkloads. Premium-opslag ondersteunt het VM-schijven die kunnen worden gekoppeld toospecific grootte-serie VM's, zoals Active Directory, DSv2 GS en F-serie virtuele machines. Hallo premium schijf is voorzien van verschillende grootte en kunt u kiezen tussen schijven variërend van 32 GB too4, 096 GB. De grootte van elke schijf heeft zijn eigen prestatiespecificaties. Afhankelijk van uw toepassing, kunt u een of meer schijven tooyour VM koppelen.

Wanneer u een nieuwe beheerde schijf vanuit Hallo portal maakt, kunt u Hallo **accounttype** Hallo type schijf dat u wilt toouse. Houd er rekening mee dat niet alle beschikbare schijven in de vervolgkeuzelijst Hallo worden weergegeven. Nadat u een bepaalde VM-grootte hebt gekozen, ziet u Hallo menu alleen Hallo beschikbaar premium-opslag SKU's die zijn gebaseerd op deze VM-grootte.

![Schermafbeelding van pagina met Hallo-beheerde schijven](./media/oracle-design/premium_disk01.png)

Zie voor meer informatie [beheerde schijven voor virtuele machines en hoge prestaties Premium-opslag](https://docs.microsoft.com/azure/storage/storage-premium-storage).

Nadat u uw opslag op een virtuele machine hebt geconfigureerd, kunt u tooload test Hallo schijven hebben voordat u een database maakt. Doorvoer latentie doelen weten Hallo i/o-snelheid in termen van de latentie en de doorvoer kan u helpen bepalen als Hallo VM's Hallo ondersteunen worden verwacht.

Er zijn een aantal hulpprogramma's voor de toepassing werklast testen, zoals Oracle Orion Sysbench en Fio.

Hallo load test opnieuw uitgevoerd nadat u een Oracle-database hebt geïmplementeerd. Start de werkbelasting van uw normale en piekuren en Hallo resultaten weergeven Hallo van basislijn van uw omgeving.

Belangrijker toosize Hallo opslag op basis van Hallo IOPS snelheid in plaats van Hallo opslaggrootte mogelijk. Bijvoorbeeld als Hallo vereist IOPS 5.000 is, maar hoeft u alleen 200 GB, u mogelijk alsnog Hallo P30 klasse premium schijf ook al beschikt u over meer dan 200 GB aan opslagruimte.

Hallo IOPS snelheid kan worden verkregen van Hallo AWR rapport. Dit wordt bepaald door Hallo opnieuw logboek, fysieke leesbewerkingen en snelheid van schrijfbewerkingen.

![Schermafbeelding van pagina Hallo AWR-rapport](./media/oracle-design/awr_report.png)

Hallo opnieuw grootte is bijvoorbeeld 12,200,000 bytes per seconde, wat gelijk too11.63 MBPs.
Hallo IOPS is 12.200.000 / 2,358 = 5,174.

Nadat u een duidelijk beeld van Hallo i/o-vereisten hebt, kunt u een combinatie van stations die het beste geschikt toomeet zijn deze vereisten.

**Aanbevelingen**

- Voor gegevens tabelruimte, verdeeld over Hallo i/o-werkbelasting een aantal schijven met behulp van beheerde opslaggroep of Oracle ASM.
- Als Hallo i/o-blokgrootte voor lees-intensieve en write-intensieve bewerkingen toeneemt, kunt u meer gegevensschijven toevoegen.
- Hallo blokgrootte voor grote opeenvolgende processen verhogen.
- Gebruik gegevens compressie tooreduce i/o (voor gegevens en indexen).
- Afzonderlijke opnieuw Logboeken, systeem en temps en ongedaan maken van TS op afzonderlijke gegevensschijven.
- Niet alle toepassingsbestanden op standaard OS-schijven (/ dev/sda) plaatsen. Deze schijven worden niet geoptimaliseerd voor snelle VM opstarttijden, en ze bieden geen goede prestaties voor uw toepassing.

### <a name="disk-cache-settings"></a>Schijf-cache-instellingen

Er zijn drie opties voor hostcaching:

- *Alleen-lezen*: alle aanvragen in cache zijn opgeslagen voor toekomstige leesbewerkingen. Alle schrijfbewerkingen worden persistent rechtstreeks tooAzure Blob-opslag.

- *Lezen / schrijven*: dit is een 'read-ahead' algoritme. Hallo leest en schrijft in cache zijn opgeslagen voor toekomstige leesbewerkingen. Niet-write-through schrijfbewerkingen zijn eerst toohello lokale cache bewaard. Schrijfbewerkingen zijn persistente tooAzure opslag voor SQL Server, omdat deze write-through gebruikt. Het bevat ook Hallo laagste schijf latentie voor lichte werkbelasting.

- *Geen* (uitgeschakeld): deze optie gebruikt, kunt u Hallo cache overslaan. Alle Hallo-gegevens worden overgebracht toodisk en persistent tooAzure opslag. Deze methode kunt u Hallo hoogste i/o-snelheid voor i/o-intensieve werkbelastingen. Tootake 'transactiekosten' moet u ook rekening.

**Aanbevelingen**

toomaximize hello doorvoer, het is raadzaam dat u met begint **geen** voor hostcaching. Voor Premium-opslag, houd er rekening mee moet u Hallo 'barrières"uitschakelen wanneer u Hallo bestandssysteem Hello koppelt **ReadOnly** of **geen** opties. Hallo /etc/fstab bestand bijwerken met Hallo UUID toohello schijven.

Zie voor meer informatie [Premium-opslag voor virtuele Linux-machines](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).

![Schermafbeelding van pagina met Hallo-beheerde schijven](./media/oracle-design/premium_disk02.png)

- Voor OS-schijven, gebruikt u de standaard **lezen/schrijven** opslaan in cache.
- Gebruik voor het systeem, TEMP en ongedaan maken **geen** voor opslaan in cache.
- Gebruik voor gegevens, **geen** voor opslaan in cache. Maar als de database alleen-lezen of lees-intensieve is, gebruikt u **alleen-lezen** opslaan in cache.

Nadat de instelling van de schijf gegevens zijn opgeslagen, kunt u Hallo host cache-instelling niet wijzigen, tenzij u het Hallo-station op Hallo OS niveau ontkoppelen en koppel deze het vervolgens opnieuw nadat u hebt aangebracht Hallo wijzigen.


## <a name="security"></a>Beveiliging

Nadat u hebt ingesteld en geconfigureerd van uw Azure-omgeving, de volgende stap Hallo toosecure is uw netwerk. Hier volgen enkele aanbevelingen:

- *NSG-beleid*: NSG worden gedefinieerd met een subnet of NIC. Het is eenvoudiger toocontrol toegang op Hallo subnetniveau voor beveiliging en werking routering voor dingen zoals firewalls, toepassing.

- *Jumpbox*: voor een beter beveiligde toegang beheerders moeten niet rechtstreeks toegang toohello toepassingsservice of database. Een jumpbox wordt gebruikt als een medium tussen Hallo beheerder machine en de Azure-resources.
![Schermafbeelding van pagina met Hallo Jumpbox-topologie](./media/oracle-design/jumpbox.png)

    Hallo beheerder machine moet IP beperkte toegang toohello jumpbox alleen aanbieden. Hallo jumpbox moet hebben toegang toohello toepassing en -database.

- *Particulier netwerk* (subnetten): We raden u aan Hallo toepassings-service en de database op afzonderlijke subnetten, zodat betere controle kan worden ingesteld door het NSG-beleid.


## <a name="additional-reading"></a>Aanvullende bronnen

- [Oracle ASM configureren](configure-oracle-asm.md)
- [Oracle Data Guard configureren](configure-oracle-dataguard.md)
- [Oracle Golden Gate configureren](configure-oracle-golden-gate.md)
- [Oracle back-up en herstel](oracle-backup-recovery.md)

## <a name="next-steps"></a>Volgende stappen

- [Zelfstudie: Een maximaal beschikbare virtuele machines maken](../../linux/create-cli-complete.md)
- [VM-implementatie Azure CLI voorbeelden verkennen](../../linux/cli-samples.md)
