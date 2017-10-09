---
title: een SQL Server-database tooSQL Server op een virtuele machine aaaMigrate | Microsoft Docs
description: Meer informatie over hoe een on-premises gebruiker toomigrate tooSQL Server in een virtuele machine van Azure-database.
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a>Migreren van een SQL Server-database tooSQL Server in een Azure VM

Er zijn een aantal methoden toomigrate een lokale SQL Server gebruiker database tooSQL Server in een Azure VM. Dit artikel wordt kort bespreken verschillende methoden en aanbevolen om de beste methode Hallo voor verschillende scenario's.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a>Wat zijn de primaire migratiemethoden Hallo?
Hallo primaire migratiemethoden zijn:

* Lokale back-up maken gebruik van compressie en handmatig kopiëren Hallo back-upbestand in hello Azure virtuele machine
* Maken en uitvoeren van een back-tooURL in hello Azure virtuele machine van Hallo-URL
* Ontkoppel en kopieer Hallo gegevens en logboekbestanden bestanden tooAzure blob-opslag en koppel vervolgens tooSQL Server in Azure VM van URL
* Converteren van lokale fysieke machine tooHyper-V-VHD en vervolgens implementeren als nieuwe virtuele machine via geüpload VHD uploaden tooAzure Blob-opslag
* Verzenden van de harde schijf met de Windows-Service voor importeren/exporteren
* Zo hebt u een AlwaysOn-implementatie van on-premises, gebruikt u Hallo [Azure Replica Wizard toevoegen](../classic/sql-onprem-availability.md) toocreate een replica in Azure en vervolgens failover, gebruikers toohello Azure database-exemplaar aan te wijzen
* SQL Server gebruiken [transactionele replicatie](https://msdn.microsoft.com/library/ms151176.aspx) tooconfigure hello Azure SQL Server-exemplaar als een abonnee en Schakel replicatie, wijzen gebruikers toohello Azure database-exemplaar uit

> [!TIP]
> Ook kunt u deze databases met dezelfde technieken toomove tussen VM's van SQL Server in Azure. Bijvoorbeeld: Er is geen ondersteunde manier tooupgrade een VM van de SQL Server-afbeelding van één versie /-editie tooanother. In dit geval moet u een nieuwe virtuele machine een SQL-Server maken met Hallo nieuwe versie /-editie en voert u een van Hallo migratie technieken in dit artikel toomove uw databases. 

## <a name="choosing-your-migration-method"></a>Uw migratiemethode kiezen
Voor optimale prestaties overdracht, migreren Hallo-databasebestanden in hello Azure-VM met een gecomprimeerde back-upbestand.

toominimize downtime tijdens het migratieproces Hallo-database, de optie AlwaysOn Hallo of Hallo transactionele replicatie-optie gebruiken.

Als het niet mogelijk toouse Hallo hierboven methoden, handmatig migreren van uw database. Met deze optie kunt u in het algemeen beginnen met een databaseback-up gevolgd door een kopie van Hallo databaseback-up naar Azure en voert u een database terugzetten. U kunt ook Hallo-databasebestanden zichzelf te kopiëren naar Azure en koppelt u ze. Er zijn verschillende methoden waarmee u deze handmatige verwerking van een database migreren naar een virtuele machine van Azure kunt uitvoeren.

> [!NOTE]
> Wanneer u tooSQL Server 2014 of SQL Server 2016 van oudere versies van SQL Server bijwerkt, moet u rekening houden of er wijzigingen nodig zijn. Het is raadzaam dat u alle afhankelijkheden op functies die niet wordt ondersteund door de nieuwe versie van SQL Server Hallo als onderdeel van uw migratieproject te houden. Zie voor meer informatie over scenario's en edities van Hallo ondersteund [tooSQL Server Upgrade](https://msdn.microsoft.com/library/bb677622.aspx).

Hallo volgende tabel geeft een lijst van elk van de primaire migratiemethoden Hallo en wordt beschreven wanneer Hallo gebruik van elke methode is het meest geschikt.

| Methode | De versie van de gegevensbron-database | De versie van de doel-database | De grootte van de back-beperking op de bron database | Opmerkingen |
| --- | --- | --- | --- | --- |
| [Lokale back-up maken gebruik van compressie en handmatig kopiëren Hallo back-upbestand in hello Azure virtuele machine](#backup-and-restore) |SQL Server 2005 of hoger |SQL Server 2005 of hoger |[De opslaglimiet van de Azure VM](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Dit is een zeer eenvoudige en uitgebreid geteste techniek voor het verplaatsen van databases op computers. |
| [Maken en uitvoeren van een back-tooURL in hello Azure virtuele machine van Hallo-URL](#backup-to-url-and-restore) |SQL Server 2012 SP1 CU2 of hoger |SQL Server 2012 SP1 CU2 of hoger |< 12,8 TB voor SQL Server 2016, anders < 1 TB | Deze methode is alleen een andere manier toomove Hallo back-upbestand toohello virtuele machine met behulp van Azure-opslag. |
| [Ontkoppel en kopieer Hallo gegevens en logboekbestanden bestanden tooAzure blob-opslag en koppel vervolgens tooSQL Server in Azure virtuele machine van de URL](#detach-and-attach-from-url) |SQL Server 2005 of hoger |SQL Server 2014 of hoger |[De opslaglimiet van de Azure VM](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Gebruik deze methode wanneer u van plan te bent[Bewaar deze bestanden hello Azure Blob storage-service met](https://msdn.microsoft.com/library/dn385720.aspx) en koppel deze tooSQL Server uitgevoerd in een virtuele machine van Azure, met name met zeer grote databases |
| [Convert on-premises machine tooHyper-V-VHD's, uploaden tooAzure Blob-opslag, en vervolgens een nieuwe virtuele machine met behulp van geüploade VHD implementeren](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 of hoger |SQL Server 2005 of hoger |[De opslaglimiet van de Azure VM](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Gebruiken wanneer [brengen van uw eigen SQL Server-licentie](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), bij het migreren van een database die u in een oudere versie van SQL Server wordt uitgevoerd of bij het migreren systeem en gebruikersdatabases samen als onderdeel van de migratie van de database is afhankelijk van andere Hallo gebruikersdatabases en/of systeemdatabases. |
| [Verzenden van de harde schijf met de Windows-Service voor importeren/exporteren](#ship-hard-drive) |SQL Server 2005 of hoger |SQL Server 2005 of hoger |[De opslaglimiet van de Azure VM](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Gebruik Hallo [Windows Import/Export-Service](../../../storage/common/storage-import-export-service.md) wanneer handmatige copy-methode is te langzaam, zoals met zeer grote databases |
| [Gebruik hello Azure Replica Wizard toevoegen](../classic/sql-onprem-availability.md) |SQL Server 2012 of hoger |SQL Server 2012 of hoger |[De opslaglimiet van de Azure VM](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Minimaliseert uitvaltijd, gebruik wanneer u een AlwaysOn-on-premises-implementatie |
| [Transactionele replicatie van SQL Server gebruiken](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 of hoger |SQL Server 2005 of hoger |[De opslaglimiet van de Azure VM](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Gebruik deze optie wanneer u toominimize uitvaltijd nodig en geen een AlwaysOn-on-premises-implementatie hoeft |

## <a name="backup-and-restore"></a>Back-ups en herstellen
Maak een back-up van de database met compressie Hallo back-toohello VM kopiëren en vervolgens Hallo-database te herstellen. Als uw back-upbestand groter dan 1 TB is, moet u het stripe omdat Hallo maximale grootte van een VM-schijf 1 TB is. Hallo volgende algemene stappen toomigrate een gebruikersdatabase die met deze handmatige methode gebruiken:

1. Voer een volledige back-tooan on-premises locatie.
2. Maken of een virtuele machine met de versie van SQL Server gewenst Hallo uploaden.
3. Het instellen van connectiviteit op basis van uw vereisten. Zie [verbinding maken met virtuele Machine van SQL Server op Azure (Resource Manager) tooa](virtual-machines-windows-sql-connect.md).
4. Kopieer de back-up bestand(en) tooyour VM met extern bureaublad, Windows Verkenner of Hallo opdracht kopiëren vanaf een opdrachtprompt.

## <a name="backup-toourl-and-restore"></a>TooURL back-up en herstel
In plaats van een back-up van het lokale bestand tooa, kunt u Hallo [back-tooURL](https://msdn.microsoft.com/library/dn435916.aspx) en herstel van URL toohello VM. Worden aanbevolen voor prestaties en vereist tooexceed Hallo groottebeperkingen per blob met SQL Server 2016 striped back-upsets worden ondersteund. Voor zeer grote databases Hallo gebruik van Hallo [Windows Import/Export-Service](../../../storage/common/storage-import-export-service.md) wordt aanbevolen.

## <a name="detach-and-attach-from-url"></a>Ontkoppel en koppelen van URL
Ontkoppel de database en logboekbestanden bestanden en dragen deze te[Azure Blob storage](https://msdn.microsoft.com/library/dn385720.aspx). Koppel vervolgens Hallo-database van Hallo-URL op de virtuele machine van Azure. Gebruik deze optie als u wilt dat Hallo fysieke database bestanden tooreside in Blob-opslag. Dit kan handig zijn voor zeer grote databases. Hallo volgende algemene stappen toomigrate een gebruikersdatabase die met deze handmatige methode gebruiken:

1. Loskoppelen van de databasebestanden Hallo van Hallo lokale database-exemplaar.
2. Hallo losgekoppeld databasebestanden kopiëren naar Azure blob storage met Hallo [AZCopy-opdrachtregelprogramma](../../../storage/common/storage-use-azcopy.md).
3. Hallo-databasebestanden uit hello Azure-URL toohello SQL Server-exemplaar in hello Azure VM toevoegen.

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a>TooVM converteren en tooURL uploaden en implementeren als een nieuwe virtuele machine
Gebruik deze methode toomigrate alle systeem- en -databases in een lokale SQL Server-exemplaar tooAzure virtuele machine. Hallo volgende algemene stappen toomigrate een volledige SQL Server-exemplaar met behulp van deze handmatige methode gebruiken:

1. Convert fysieke of virtuele machines tooHyper-V-VHD's met behulp van [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx).
2. VHD-bestanden tooAzure opslag uploaden via Hallo [cmdlet Add-AzureVHD](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).
3. Implementeer een nieuwe virtuele machine met behulp van Hallo VHD geüpload.

> [!NOTE]
> toomigrate een volledige toepassing, kunt u overwegen [Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>Verzenden van de harde schijf
Gebruik Hallo [Windows Import/Export-Service methode](../../../storage/common/storage-import-export-service.md) tootransfer grote hoeveelheden bestand gegevens tooAzure Blob-opslag in situaties waarbij uploaden via Hallo netwerk beperkend dure of niet haalbaar is is. Met deze service verzenden van een of meer harde schijven met deze gegevens tooan Azure-Datacenter, waar uw gegevens worden geüpload tooyour storage-account.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual Machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).

Zie voor instructies over het maken van een virtuele Machine van Azure SQL Server vanuit een vastgelegd beeld [Tips & trucs voor SQL Azure virtuele machines van de vastgelegde installatiekopieën klonen](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) op Hallo CSS SQL Server-Engineers-blog.

