---
title: aanbevolen procedures voor SQL Server in Azure aaaPerformance | Microsoft Docs
description: Bevat de aanbevolen procedures voor het optimaliseren van de prestaties van SQL Server in Microsoft Azure VM's.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a0c85092-2113-4982-b73a-4e80160bac36
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: jroth
ms.openlocfilehash: 42ec9fbeb2dec3a654b93bbd08d666369835ee73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-best-practices-for-sql-server-in-azure-virtual-machines"></a>Aanbevolen procedures voor prestaties voor SQL Server op virtuele machines van Azure

## <a name="overview"></a>Overzicht

Dit onderwerp bevat aanbevolen procedures voor het optimaliseren van de prestaties van SQL Server in Microsoft Azure Virtual machines. Tijdens het uitvoeren van SQL Server in Azure Virtual Machines, het is raadzaam dat u gebruiken blijven Hallo dezelfde databaseprestaties afstemmen van de opties die van toepassing tooSQL Server in on-premises server-omgeving. Hallo-prestaties van een relationele database in een openbare cloud is afhankelijk van veel factoren zoals de grootte van een virtuele machine en de configuratie van gegevensschijven Hallo HALLO hallo.

Bij het maken van SQL Server-installatiekopieën [Houd rekening met het inrichten van uw virtuele machines in Azure-portal Hallo](virtual-machines-windows-portal-sql-server-provision.md). SQL Server-VM's ingericht in Hallo Portal met Resource Manager implementeren alle deze best practices, met inbegrip van de opslagconfiguratie Hallo.

In dit artikel is gericht op het ophalen van Hallo *aanbevolen* prestaties voor SQL Server op Azure Virtual machines. Als uw werkbelasting minder zwaar worden belast, kunt u elke optimalisatie onderstaande mogelijk niet nodig. Houd rekening met uw prestatievereisten past en werkbelasting patronen als u deze aanbevelingen evalueren.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="quick-check-list"></a>Lijst met snelle controle

Hallo Hier volgt een lijst met snelle controle voor optimale prestaties van SQL Server op Azure Virtual Machines:

| Onderwerp | Optimalisaties |
| --- | --- |
| [VM-grootte](#vm-size-guidance) |[DS3](../../virtual-machines-windows-sizes-memory.md) of hoger voor SQL Enterprise edition.<br/><br/>[DS2](../../virtual-machines-windows-sizes-memory.md) of hoger voor SQL Standard- en Web-edities. |
| [Storage](#storage-guidance) |Gebruik [Premium-opslag](../../../storage/common/storage-premium-storage.md). Standard-opslag wordt alleen aanbevolen voor ontwikkelen en testen.<br/><br/>Hallo houden [opslagaccount](../../../storage/common/storage-create-storage-account.md) en SQL Server VM in Hallo dezelfde regio.<br/><br/>Schakel Azure [geografisch redundante opslag](../../../storage/common/storage-redundancy.md) (geo-replicatie) op Hallo storage-account. |
| [Schijven](#disks-guidance) |Gebruik een minimum van 2 [P30 schijven](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) (1 voor logboekbestanden, 1 voor gegevensbestanden en TempDB).<br/><br/>Vermijd het gebruik van besturingssysteem of tijdelijke schijven voor database-opslag of registratie.<br/><br/>Schakel lees-caching op Hallo een of meer schijven Hallo gegevensbestanden en TempDB te hosten.<br/><br/>Schakel niet opslaan in cache op een of meer schijven die als host fungeert voor het logboekbestand Hallo.<br/><br/>Belangrijk: Stop Hallo SQL Server-service als het Hallo-cache-instellingen wijzigen voor een virtuele machine van Azure-schijf.<br/><br/>Stripe meerdere Azure gegevens schijven tooget verhoogd i/o-doorvoer.<br/><br/>Formatteren met grootten gedocumenteerde toewijzing. |
| [I/O 'S](#io-guidance) |Database pagina compressie inschakelen.<br/><br/>Schakel directe bestand de initialisatie van de gegevensbestanden worden opgeslagen.<br/><br/>Beperk of autogrow op Hallo database uitschakelen.<br/><br/>Autoshrink op Hallo-database niet uitschakelen.<br/><br/>Verplaats alle databases toodata schijven, met inbegrip van systeemdatabases.<br/><br/>SQL Server fout logboek- en traceringsbestanden bestand mappen toodata schijven verplaatsen.<br/><br/>Het instellen van standaardbestandslocaties voor back-up en -database.<br/><br/>Schakel vergrendelde pagina's.<br/><br/>SQL Server prestaties correcties toepassen. |
| [Specifieke functies](#feature-specific-guidance) |Back-ups rechtstreeks tooblob opslag. |

Voor meer informatie over *hoe* en *waarom* toomake deze optimalisaties Controleer Hallo details en richtlijnen in de volgende secties.

## <a name="vm-size-guidance"></a>Richtlijnen voor VM-grootte

Voor gevoelige toepassingen prestaties, wordt aanbevolen dat u de volgende Hallo [grootten voor virtuele machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json):

* **SQL Server Enterprise Edition**: DS3 of hoger
* **SQL Server Standard en Web-edities**: DS2 of hoger

## <a name="storage-guidance"></a>Richtlijnen voor opslag

DS-serie (samen met DSv2-serie en GS-serie) VMs ondersteuning [Premium-opslag](../../../storage/common/storage-premium-storage.md). Premium-opslag wordt aanbevolen voor alle productieworkloads.

> [!WARNING]
> Standard-opslag heeft verschillende latenties en bandbreedte en wordt alleen aanbevolen voor ontwikkel-/ testwerkbelastingen. Productieworkloads moeten Premium-opslag gebruiken.

Bovendien wordt aangeraden dat u uw Azure storage-account in Hallo maken hetzelfde Datacenter als uw SQL Server virtuele machines tooreduce overdracht vertragingen. Wanneer u een opslagaccount maakt, uitschakelen geo-replicatie zoals consistent schrijven volgorde over meerdere schijven kan niet worden gegarandeerd. Overweeg in plaats daarvan het configureren van een SQL Server-technologie disaster recovery tussen twee Azure-datacenters. Zie voor meer informatie [hoge beschikbaarheid en herstel na noodgevallen voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="disks-guidance"></a>Schijven richtlijnen

Er zijn drie belangrijkste schijftypen op een virtuele machine van Azure:

* **Besturingssysteemschijf**: wanneer u een virtuele Machine in Azure maakt, ten minste één schijf zal worden gekoppeld aan Hallo platform (aangeduid als Hallo **C** station) toohello VM voor de schijf van uw besturingssysteem. Deze schijf is een VHD die is opgeslagen als een pagina-blob in de opslag.
* **Tijdelijke schijf**: Azure Virtual Machines bevatten een andere schijf met de naam van de tijdelijke schijf hello (aangeduid als Hallo **D**: station). Dit is een schijf op Hallo-knooppunt dat kan worden gebruikt voor scratchruimte.
* **Gegevensschijven**: U kunt ook extra schijven tooyour virtuele machine als gegevensschijven koppelen en deze in de opslag worden opgeslagen als pagina-blobs.

Hallo beschrijven volgende secties aanbevelingen voor het gebruik van deze andere schijven.

### <a name="operating-system-disk"></a>Besturingssysteemschijf

De schijf van een besturingssysteem is een VHD die u kunt opstarten en koppelen als een versie van een besturingssysteem en wordt aangeduid als **C** station.

Standaardwaarde cachebeleid op Hallo besturingssysteemschijf is **lezen/schrijven**. Voor gevoelige toepassingen prestaties, is het raadzaam dat u gegevensschijven in plaats van de besturingssysteemschijf Hallo. Zie sectie Hallo op gegevensschijven hieronder.

### <a name="temporary-disk"></a>Tijdelijke schijf

station voor tijdelijke opslag, aangeduid als Hallo Hallo **D**: schijf, is niet persistent gemaakte tooAzure blob-opslag. Sla niet uw Gebruikersdatabasebestanden of gebruiker transactielogboekbestanden op Hallo **D**: station.

Voor D-reeks, Dv2-serie en G-serie virtuele machines is tijdelijk Hallo-station op deze virtuele machines op SSD gebaseerd. Als uw werkbelasting intensief gebruik van TempDB (bijvoorbeeld voor tijdelijke objecten of complexe joins maakt) TempDB op Hallo opslaan **D** station kan leiden tot hogere TempDB-doorvoer en lagere latentie van TempDB.

Voor virtuele machines die ondersteuning bieden voor Premium-opslag (DS-serie, DSv2-serie en GS-serie), wordt u aangeraden TempDB opslaan op een schijf die ondersteuning biedt voor Premium-opslag met lees-caching is ingeschakeld. Er is een uitzondering toothis aanbeveling; Als het gebruik van uw TempDB schrijven-intensieve is, kunt u betere prestaties bereiken door te TempDB op Hallo lokaal opslaan **D** station, dat ook SSD op basis van de grootte van deze machine.

### <a name="data-disks"></a>Gegevensschijven

* **Gegevensschijven gebruiken voor gegevens en logboekbestanden**: ten minste 2 Premium-opslag gebruiken [P30 schijven](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) waar één schijf bevat Hallo-logboekbestanden en Hallo andere Hallo gegevens en bestanden van TempDB. Elke schijf Premium-opslag biedt een aantal IOPs en bandbreedte (MB/s), afhankelijk van de grootte, zoals beschreven in het volgende artikel Hallo: [Premium-opslag voor schijven met behulp van](../../../storage/common/storage-premium-storage.md).

* **Striping schijf**: voor een meer doorvoer, kunt u extra gegevensschijven toevoegen en gebruiken van Striping van de schijf. toodetermine hello aantal gegevensschijven, moet u tooanalyze Hallo aantal IOPS en bandbreedte die is vereist voor uw logboekbestanden, en voor uw gegevens en bestanden van TempDB. U ziet dat andere VM-grootten verschillende beperkingen hebben op Hallo aantal IOPs en bandbreedte die wordt ondersteund, raadpleegt u Hallo tabellen op IOP's per [VM-grootte](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Gebruik Hallo richtlijnen te volgen:

  * Gebruik voor Windows 8/Windows Server 2012 of later, [opslagruimten](https://technet.microsoft.com/library/hh831739.aspx) Hello richtlijnen te volgen:

      1. Set Hallo interleave (stripe-grootte) too64 KB (65536 bytes) voor OLTP-werkbelastingen en 256 KB (262144 bytes) voor datawarehousescenario werkbelastingen tooavoid invloed op de prestaties vanwege toopartition uitlijning van gegevenstypen. Dit moet worden ingesteld met PowerShell.
      1. Aantal kolommen ingesteld = het aantal fysieke schijven. PowerShell gebruiken bij het configureren van meer dan 8 schijven (geen Server Manager UI). 

    Bijvoorbeeld, Hallo na PowerShell maakt u een nieuwe opslaggroep met Hallo interleave grootte too64 KB en Hallo aantal kolommen too2:

    ```powershell
    $PoolCount = Get-PhysicalDisk -CanPool $True
    $PhysicalDisks = Get-PhysicalDisk | Where-Object {$_.FriendlyName -like "*2" -or $_.FriendlyName -like "*3"}

    New-StoragePool -FriendlyName "DataFiles" -StorageSubsystemFriendlyName "Storage Spaces*" -PhysicalDisks $PhysicalDisks | New-VirtualDisk -FriendlyName "DataFiles" -Interleave 65536 -NumberOfColumns 2 -ResiliencySettingName simple –UseMaximumSize |Initialize-Disk -PartitionStyle GPT -PassThru |New-Partition -AssignDriveLetter -UseMaximumSize |Format-Volume -FileSystem NTFS -NewFileSystemLabel "DataDisks" -AllocationUnitSize 65536 -Confirm:$false 
    ```

  * Voor Windows 2008 R2 of eerder, kunt u dynamische schijven (OS striped volumes) en Hallo stripe-grootte is altijd 64 KB. Houd er rekening mee dat deze optie is afgeschaft vanaf Windows 8 of Windows Server 2012. Zie voor informatie Hallo ondersteuningsverklaring op [Virtual Disk-Service in een overgang tooWindows Storage Management API](https://msdn.microsoft.com/library/windows/desktop/hh848071.aspx).

  * Als uw werkbelasting geen logboek intensieve is en niet toegewezen IOP's hoeft, kunt u slechts één opslaggroep kunt configureren. Anders maakt u twee opslaggroepen, één voor Hallo-logboekbestanden en een andere opslaggroep voor Hallo gegevensbestand(en) en TempDB. Het aantal schijven die zijn gekoppeld aan elke opslaggroep op basis van de load-verwachtingen Hallo bepalen. Houd er rekening mee dat andere VM-grootten toestaan verschillend aantal gegevensschijven gekoppeld. Zie voor meer informatie [grootten voor virtuele Machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

  * Als u geen Premium-opslag (ontwikkelen en testen scenario's) gebruikt, Hallo aanbeveling is tooadd Hallo maximum aantal gegevensschijven dat wordt ondersteund door uw [VM-grootte](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en schijf-Striping gebruiken.

* **Cachebeleid**: gegevensschijven voor de Premium-opslag, inschakelen Lees-caching op Hallo gegevensschijven gegevensbestanden en TempDB alleen hosten. Als u geen Premium-opslag gebruikt, niet is ingeschakeld eventuele cachegebruik op eventuele gegevensschijven. Zie voor instructies over het configureren van de schijfcache, Hallo volgende onderwerpen: [Set AzureOSDisk](https://msdn.microsoft.com/library/azure/jj152847) en [Set AzureDataDisk](https://msdn.microsoft.com/library/azure/jj152851.aspx).

  > [!WARNING]
  > Hallo SQL Server-service stoppen bij het wijzigen van de cache-instelling Hallo van Azure VM schijven tooavoid Hallo mogelijkheid van een beschadiging van de database.

* **Clustergrootte van NTFS**: bij het opmaken van de gegevensschijf hello wordt aanbevolen dat u een clustergrootte van 64 KB voor gegevens en logboekbestanden, evenals TempDB.

* **Best practices voor schijf**: wanneer een gegevensschijf verwijderen of wijzigen van de cache typt, Hallo SQL Server-service stoppen tijdens het Hallo wijzigen. Wanneer Hallo cache-instellingen zijn gewijzigd op Hallo OS-schijf Azure Hallo VM stopt, cachetype hello wordt gewijzigd en Hallo VM opnieuw wordt opgestart. Wanneer Hallo cache-instellingen van een gegevensschijf worden gewijzigd, Hallo VM niet is gestopt, maar Hallo gegevensschijf wordt losgekoppeld van Hallo VM tijdens Hallo wijzigen en klik vervolgens opnieuw.

  > [!WARNING]
  > Fout toostop Hallo SQL Server-service tijdens deze bewerkingen kan leiden tot beschadiging van de database.

## <a name="io-guidance"></a>I/o-richtlijnen

* Hallo de beste resultaten met Premium-opslag bereikt wanneer u uw toepassing en aanvragen parallelize. Premium-opslag is bedoeld voor scenario's waarin Hallo i/o-wachtrijdiepte groter is dan 1, daarom u weinig of geen prestatieverbeteringen voor seriële aanvragen single thread ziet (zelfs als ze zich intensieve opslag). Dit kan bijvoorbeeld van Hallo single thread-testresultaten van prestaties analyseprogramma's, zoals SQLIO invloed.

* Overweeg het gebruik van [database pagina compressie](https://msdn.microsoft.com/library/cc280449.aspx) zoals kunt verbeteren de prestaties van i/o-intensieve werkbelastingen. Hallo gegevenscompressie mogelijk echter Hallo CPU-verbruik op Hallo-databaseserver te verhogen.

* Overweeg in te schakelen instant file initialisatie tooreduce Hallo tijd die nodig zijn voor toewijzing van de eerste bestand. tootake profiteren van de initialisatie van de directe bestanden, u Hallo serviceaccount van SQL Server (MSSQLSERVER) met SE_MANAGE_VOLUME_NAME verlenen en toe te voegen toohello **volumeonderhoudstaken uitvoeren** beveiligingsbeleid. Als u van een SQL Server-platforminstallatiekopie voor Azure gebruikmaakt, Hallo standaard serviceaccount (NT Service\MSSQLSERVER) toohello is niet toegevoegd **volumeonderhoudstaken uitvoeren** beveiligingsbeleid. Initialisatie van de directe bestanden met andere woorden, niet is ingeschakeld in een installatiekopie van SQL Server-Azure-platform. Na het toevoegen van Hallo SQL Server-service-account toohello **volumeonderhoudstaken uitvoeren** beveiligingsbeleid, Hallo SQL Server-service opnieuw. Er zijn beveiligingsoverwegingen voor het gebruik van deze functie. Zie voor meer informatie [initialiseren van de Database-bestand](https://msdn.microsoft.com/library/ms175935.aspx).

* **autogrow** wordt beschouwd als toobe enkel geval van nood voor onverwachte groei. Beheert de groei van uw gegevens en logboekbestanden op dagelijks met autogrow niet. Als het autogrow wordt gebruikt, moet u vooraf Hallo-bestand met Hallo grootte schakeloptie groeien.

* Zorg ervoor dat **autoshrink** is uitgeschakeld tooavoid onnodige overhead die prestaties negatief kan beïnvloeden.

* Verplaats alle databases toodata schijven, met inbegrip van systeemdatabases. Zie voor meer informatie [systeemdatabases verplaatsen](https://msdn.microsoft.com/library/ms345408.aspx).

* SQL Server fout logboek- en traceringsbestanden bestand mappen toodata schijven verplaatsen. Dit is mogelijk in SQL Server Configuration Manager met de rechtermuisknop op uw SQL Server-exemplaar eigenschappen te selecteren. Hallo instellingen voor foutpagina logboek- en traceringsbestanden bestand kunnen worden gewijzigd in Hallo **opstartparameters** tabblad Hallo geheugendump is opgegeven in Hallo **Geavanceerd** tabblad Hallo volgende Schermafbeelding toont waar toolook voor Hallo fout logboek starten van de parameter.

    ![Schermafbeelding van de SQL-foutenlogboek](./media/virtual-machines-windows-sql-performance/sql_server_error_log_location.png)

* Het instellen van standaardbestandslocaties voor back-up en -database. Hallo aanbevelingen in dit onderwerp gebruiken en Hallo wijzigingen aanbrengen in het eigenschappenvenster Hallo-Server. Zie voor instructies [weergeven of wijzigen Hallo standaard locaties voor gegevens en logboekbestanden (SQL Server Management Studio)](https://msdn.microsoft.com/library/dd206993.aspx). Hallo volgende Schermafbeelding toont waar toomake deze wijzigingen.

    ![Logboekbestanden voor SQL-gegevens en back-up](./media/virtual-machines-windows-sql-performance/sql_server_default_data_log_backup_locations.png)
* Pagina's tooreduce i/o en eventuele activiteiten Paginering inschakelen is vergrendeld. Zie voor meer informatie [inschakelen Hallo pagina's in de optie geheugen (Windows) vergrendelen](https://msdn.microsoft.com/library/ms190730.aspx).

* Als u SQL Server 2012 uitvoert, installeert u Service Pack 1 Cumulative Update 10. Deze update bevat Hallo-oplossing voor slechte prestaties in i/o tijdens het uitvoeren van select into-instructie van de tijdelijke tabel in SQL Server 2012. Zie voor meer informatie, dit [knowledge base-artikel](http://support.microsoft.com/kb/2958012).

* Overweeg het comprimeren van gegevensbestanden bij de overdracht / out van Azure.

## <a name="feature-specific-guidance"></a>Functie voor specifieke aanwijzingen

Sommige implementaties mogelijk extra prestatievoordelen met behulp van meer geavanceerde configuratie technieken bereiken. Hallo hieronder gemarkeerd sommige SQL Server-functies waarmee u kunnen betere prestaties tooachieve:

* **Back-up tooAzure opslag**: bij het uitvoeren van back-ups voor SQL Server op Azure virtuele machines, kunt u [back-up van SQL Server-tooURL](https://msdn.microsoft.com/library/dn435916.aspx). Deze functie is beschikbaar vanaf met SQL Server 2012 SP1 CU2 en aanbevolen voor back-ups van gegevensschijven toohello gekoppeld. Wanneer u back-up/herstel naar/van de Azure-opslag, volgt u Hallo aanbevelingen op [SQL Server-back-tooURL aanbevolen procedures en probleemoplossing en terugzetten van back-ups die zijn opgeslagen in Azure Storage](https://msdn.microsoft.com/library/jj919149.aspx). U kunt ook deze back-ups met automatiseren [automatische back-up voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).

    Eerdere tooSQL Server 2012, kunt u [back-up van SQL Server-tooAzure hulpprogramma](https://www.microsoft.com/download/details.aspx?id=40740). Dit hulpprogramma kunt u de back-doorvoer tooincrease met meerdere back-stripe-doelen.

* **SQL Server-gegevensbestanden in Azure**: deze nieuwe functie [SQL Server-gegevensbestanden in Azure](https://msdn.microsoft.com/library/dn385720.aspx), is beschikbaar vanaf SQL Server 2014. Met SQL Server met gegevensbestanden in Azure, ziet u vergelijkbare prestatiekenmerken als het gebruik van Azure gegevensschijven.

## <a name="next-steps"></a>Volgende stappen

Zie voor aanbevolen procedures voor beveiliging, [beveiligingsoverwegingen voor het SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-security.md).

Zie de andere virtuele Machine van SQL Server-onderwerpen op [SQL Server op Azure Virtual Machines Overview](virtual-machines-windows-sql-server-iaas-overview.md).
