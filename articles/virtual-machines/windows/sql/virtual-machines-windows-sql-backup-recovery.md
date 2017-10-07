---
title: aaaBackup en herstel voor SQL Server | Microsoft Docs
description: Beschrijft de overwegingen voor back-up en herstel voor SQL Server-databases die zijn uitgevoerd op Azure Virtual Machines.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Back-up en herstel voor SQL Server in Azure Virtual Machines
## <a name="overview"></a>Overzicht
Azure-opslag onderhoudt 3 kopieën van elke virtuele machine van Azure schijf tooguarantee bescherming tegen gegevensverlies of fysieke gegevensbeschadiging. Dus in tegenstelling tot on-premises hoeft u geen tooworry over deze. Echter, u moet nog steeds back-up van uw SQL Server-databases tooprotect tegen toepassings- of -fouten (bijvoorbeeld verkeerde gegevens invoegen of verwijderen van een tabel) en kunnen toorestore wordt tooa tijdstip.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

U kunt voor SQL Server wordt uitgevoerd in Azure Virtual machines, met systeemeigen back-up en herstellen met behulp van gekoppelde schijven voor bestemming van back-upbestanden Hallo Hallo technieken. Er is echter een limiet toohello aantal schijven kunt u tooan virtuele machine van Azure, op basis van Hallo koppelen [grootte van virtuele machine van Hallo](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Er is ook Hallo overhead van schijf management tooconsider.

Beginnend met SQL Server 2014, kunt u back-up en herstel van tooMicrosoft Azure Blob-opslag. SQL Server 2016 biedt ook verbeteringen voor deze optie. Bovendien voor databasebestanden is opgeslagen in Microsoft Azure Blob storage, biedt SQL Server 2016 een optie voor bijna onmiddellijk uitgevoerde back-ups en snelle herstelacties met Azure momentopnamen. In dit artikel biedt een overzicht van deze opties en extra informatie kunt vinden op [SQL Server-back-up en herstel met Microsoft Azure Blob Storage-Service](https://msdn.microsoft.com/library/jj919148.aspx).

> [!NOTE]
> Zie voor een beschrijving van opties voor back-ups van zeer grote databases Hallo [NTFS-status en SQL Server-Database back-up strategieën voor Azure Virtual Machines](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx).
> 
> 

Hallo in de volgende secties bevatten informatie specifieke toohello verschillende versies van SQL Server wordt ondersteund in Azure een virtuele machine.

## <a name="sql-server-virtual-machines"></a>Virtuele Machines van SQL Server
Als uw exemplaar van SQL Server wordt uitgevoerd op een virtuele Machine van Azure, uw databasebestanden al zich bevinden op gegevensschijven met in Azure. Deze schijven bevinden zich in Azure Blob-opslag. Dus redenen Hallo voor back-ups van uw database en Hallo benaderingen dat u iets wijzigen uitvoeren. Houd rekening met de volgende Hallo. 

* U hoeft niet meer tooperform database back-ups tooprovide bescherming tegen hardware-of omdat Microsoft Azure deze beveiliging als onderdeel van Hallo Microsoft Azure-service biedt.
* U moet nog steeds tooperform database back-ups tooprovide beveiliging tegen gebruikersfouten of voor het archiveren of wettelijke redenen administratieve doeleinden.
* U kunt back-upbestand Hallo opslaan rechtstreeks in Azure. Zie voor meer informatie Hallo uit te voeren die richtlijnen te voor Hallo verschillende versies van SQL Server bieden.

## <a name="sql-server-2016"></a>SQL Server 2016
Biedt ondersteuning voor Microsoft SQL Server 2016 [back-up en herstel met Azure blobs](https://msdn.microsoft.com/library/jj919148.aspx) onderdelen gevonden in SQL Server 2014. Maar bevat ook Hallo volgende verbeteringen:

| Verbetering van de 2016 | Details |
| --- | --- |
| **Striping** |Wanneer een back-up tooMicrosoft Azure blob-opslag, ondersteunt SQL Server 2016 back-ups van toomultiple blobs tooenable back-ups van grote databases up tooa maximaal 12,8 TB. |
| **Back-up van de momentopname** |SQL Server-bestand Momentopnameback-up biedt via Hallo gebruik van Azure momentopnamen, bijna onmiddellijk uitgevoerde back-ups en snelle herstelbewerkingen voor databasebestanden opgeslagen met behulp van hello Azure Blob storage-service. Deze mogelijkheid kunt u toosimplify uw beleid voor back-up en herstel. Back-up van de momentopname van de bestanden ondersteunt ook punt in tijd terugzetten. Zie voor meer informatie [Momentopnameback-ups voor databasebestanden in Azure](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx). |
| **Back-upplanning beheerd** |SQL Server Managed Backup tooAzure ondersteunt nu het aangepaste schema's. Zie voor meer informatie [SQL Server Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx). |

Zie voor een zelfstudie van Hallo-mogelijkheden van SQL Server 2016 bij gebruik van Azure Blob storage [zelfstudie: Hallo Microsoft Azure Blob storage-service met SQL Server 2016 databases met](https://msdn.microsoft.com/library/dn466438.aspx).

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014 bevat Hallo volgende uitbreidingen:

1. **Back-up en herstel tooAzure**:
   
   * *SQL Server-back-up tooURL* heeft nu ondersteuning in SQL Server Management Studio. Hallo optie tooback up tooAzure is nu beschikbaar wanneer u back-up of herstel taak, of de wizard Onderhoudsplan in SQL Server Management Studio. Zie voor meer informatie [back-up van SQL Server-tooURL](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
   * *SQL Server Managed Backup tooAzure* zijn nieuwe functionaliteit waarmee geautomatiseerde back-beheer. Dit is vooral handig voor het automatiseren van back-beheer voor exemplaren van SQL Server 2014 uitgevoerd op een Azure-Machine. Zie voor meer informatie [SQL Server Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx).
   * *Automatische back-up* biedt extra automation tooautomatically inschakelen *SQL Server Managed Backup tooAzure* op alle bestaande en nieuwe databases voor een virtuele SQL Server-machine in Azure. Zie voor meer informatie [Automatische back-up voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).
   * Zie voor een overzicht van alle Hallo opties voor back-up van SQL Server 2014 tooAzure [SQL Server-back-up en herstel met Microsoft Azure Blob Storage-Service](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
2. **Versleuteling**: SQL Server 2014 ondersteunt de versleuteling van gegevens bij het maken van een back-up. Deze ondersteuning biedt voor verschillende algoritmen en Hallo osf gebruiken een certificaat of de asymmetrische sleutel. Zie voor meer informatie [back-Upversleuteling](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx).

## <a name="sql-server-2012"></a>SQL Server 2012
Zie voor gedetailleerde informatie over SQL Server-back-up en herstel in SQL Server 2012 [back-up en herstellen van SQL Server-Databases (SQL Server 2012)](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx).

U start in SQL Server 2012 SP1 cumulatieve Update 2, kunt u back-up tooand terugzetten vanuit hello Azure Blob Storage-service. Deze uitbreiding mag gebruikte tooback van SQL Server-databases op een SQL-Server uitgevoerd op een virtuele Machine van Azure of een lokaal exemplaar. Zie voor meer informatie [SQL Server-back-up en herstel met Azure Blob Storage-Service](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Dit zijn enkele Hallo voordelen van het gebruik van Azure Blob storage-service Hallo Hallo mogelijkheid toobypass Hallo 16 schijf limiet voor het gekoppelde schijven eenvoudig beheer, Hallo directe beschikbaarheid van Hallo back-upbestand tooanother exemplaar van SQL Server-exemplaar is uitgevoerd op een Azure de virtuele machine of een lokaal exemplaar voor hersteldoeleinden migratie of na noodgevallen. Zie voor een volledige lijst met voordelen toousing een Azure blob storage-service voor SQL Server-back-ups, Hallo *voordelen* in sectie [SQL Server-back-up en herstel met Azure Blob Storage-Service](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Zie voor aanbevolen werkwijzen besproken en informatie over probleemoplossing [back-up en herstellen van Best Practices (Azure Blob Storage-Service)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx).

## <a name="sql-server-2008"></a>SQL Server 2008
Zie voor SQL Server-back-up en herstel in SQL Server 2008 R2 [Backing up and Restoring Databases in SQL Server (SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx).

Zie voor SQL Server-back-up en herstel in SQL Server 2008 [Backing up and Restoring Databases in SQL Server (SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx).

## <a name="next-steps"></a>Volgende stappen
Als u van plan bent uw implementatie van SQL Server in een virtuele machine in Azure, vindt u richtlijnen inrichting in Hallo zelfstudie: [inrichten van een virtuele Machine van SQL Server op Azure met Azure Resource Manager](virtual-machines-windows-portal-sql-server-provision.md).

Hoewel back-up en herstel gebruikte toomigrate uw gegevens kan worden, zijn er mogelijk eenvoudiger gegevens migratie paden tooSQL Server op een virtuele machine in Azure. Zie voor een volledige beschrijving van de opties en aanbevelingen [migreren van een Database tooSQL Server op een Azure VM](virtual-machines-windows-migrate-sql.md).

Bekijk de andere [bronnen voor het uitvoeren van SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

