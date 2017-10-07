---
title: aaaHow toouse Azure-opslag voor SQL Server back-up en herstel | Microsoft Docs
description: Meer informatie over hoe tooback van SQL Server-tooAzure opslag. Legt uit Hallo voordelen van het back-ups van SQL-databases tooAzure opslag.
services: virtual-machines-windows
documentationcenter: 
author: MikeRayMSFT
manager: jhubbard
tags: azure-service-management
ms.assetid: 0db7667d-ef63-4e2b-bd4d-574802090f8b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: mikeray
ms.openlocfilehash: 67ebe8377be97df1312f8c1345e23576aabe0c4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-for-sql-server-backup-and-restore"></a>Azure Storage gebruiken voor SQL Server-back-up en herstel
## <a name="overview"></a>Overzicht
Beginnen met SQL Server 2012 SP1 CU2, kunt u nu schrijven SQL Server-back-ups rechtstreeks toohello Azure Blob storage-service. U kunt deze functionaliteit tooback up tooand herstel van hello Azure Blob-service gebruiken met een on-premises SQL Server database of SQL Server-database in Azure een virtuele machine. Back-toocloud biedt de voordelen van de beschikbaarheid, oneindig geogerepliceerde off-site opslag en eenvoudig van de migratie van gegevens tooand van Hallo cloud. Instructies voor BACKUP of RESTORE kunt u met behulp van Transact-SQL- of SMO uitgeven.

SQL Server 2016 introduceert nieuwe mogelijkheden; u kunt [back-up van de momentopname van de bestanden](http://msdn.microsoft.com/library/mt169363.aspx) tooperform bijna onmiddellijk uitgevoerde back-ups en zeer snelle herstelbewerkingen.

Dit onderwerp wordt uitgelegd waarom u toouse Azure-opslag voor SQL-back-ups kunt selecteren en vervolgens beschrijft Hallo componenten betrokken. U kunt Hallo resources die worden geleverd aan Hallo einde van Hallo artikel tooaccess scenario's en aanvullende informatie toostart met behulp van deze service met de back-ups van uw SQL Server gebruiken.

## <a name="benefits-of-using-hello-azure-blob-service-for-sql-server-backups"></a>Voordelen van Using hello Azure Blob-Service voor back-ups van SQL Server
Er zijn enkele uitdagingen die u geconfronteerd back-ups van SQL Server. Deze uitdagingen zijn onder andere opslagbeheer risico op uitval van opslag, toegang tot opslag toooff-site en de hardwareconfiguratie. Veel van deze uitdagingen worden aangepakt met behulp van hello Azure Blob store-service voor back-ups van SQL Server. Houd rekening met Hallo volgende voordelen:

* **Gebruiksgemak**: een handige, flexibele en eenvoudige tooaccess externe optie voor het opslaan van uw back-ups in Azure blobs kan worden. Externe opslag maken voor uw SQL Server back-ups kunnen net zo eenvoudig als het wijzigen van uw bestaande scripts/taken toouse hello **back-up tooURL** syntaxis. Externe opslag doorgaans moet ver genoeg van Hallo productie database locatie tooprevent een enkele noodgeval die mogelijk van invloed op een externe locatie Hallo zowel productie databaselocaties. Door te kiezen[geo-replicatie uw Azure blobs](../../../storage/common/storage-redundancy.md), hebt u een extra beschermingslaag in Hallo-gebeurtenis van een noodgeval die de hele regio Hallo kan beïnvloeden.
* **Back-archief**: hello Azure Blob Storage-service biedt een betere alternatieve toohello vaak gebruikt tape optie tooarchive back-ups. Tapeopslag mogelijk fysieke vervoer tooan off-site faciliteit en metingen tooprotect Hallo media. Uw back-ups opslaan in Azure Blob Storage biedt een momentopname, maximaal beschikbaar, en een duurzame optie archiveren.
* **Hardware beheerd**: Er is geen extra overhead van hardwarebeheer met Azure-services. Azure-services Hallo hardware beheren en leveren van geo-replicatie voor redundantie en bescherming tegen hardwarefouten.
* **Onbeperkte opslag**: doordat een directe back-tooAzure blobs die u hebt toegang toovirtually onbeperkte opslag. Back-ups van virtuele machine van Azure-schijf tooan heeft ook limieten op basis van de grootte van de machine. Er is een aantal van de toohello beperken van schijven kunt u virtuele Azure-machine voor back-ups tooan koppelen. Deze limiet is 16 schijven voor een extra groot exemplaar en minder voor kleinere exemplaren.
* **Back-up van beschikbaarheid**: back-ups opgeslagen in Azure blobs beschikbaar zijn vanaf elke locatie en op elk gewenst moment en eenvoudig kunnen worden geopend voor herstelacties tooeither een lokale SQL-Server of een andere SQL-Server in een Azure virtuele Machine wordt uitgevoerd zonder Hallo nodig Hallo VHD voor database koppelen/loskoppelen of te downloaden en te koppelen.
* **Kosten**: betaalt alleen voor Hallo-service die wordt gebruikt. Kan worden rendabele als een optie voor de externe en back-archief. Zie Hallo [Azure prijscategorie Rekenmachine](http://go.microsoft.com/fwlink/?LinkId=277060 "Prijscalculator"), en Hallo [prijzen van Azure artikel](http://go.microsoft.com/fwlink/?LinkId=277059 "prijzen artikel") voor meer informatie informatie.
* **Opslag-momentopnamen**: als de databasebestanden worden opgeslagen in een Azure-blob en u SQL Server 2016 gebruikt, kunt u [back-up van de momentopname van de bestanden](http://msdn.microsoft.com/library/mt169363.aspx) tooperform bijna onmiddellijk uitgevoerde back-ups en zeer snelle herstelbewerkingen.

Zie voor meer informatie [SQL Server-back-up en herstel met Azure Blob Storage-Service](http://go.microsoft.com/fwlink/?LinkId=271617).

Hallo na twee secties introduceren hello Azure Blob storage-service, inclusief Hallo vereist SQL Server-onderdelen. Het is belangrijk toounderstand Hallo onderdelen en hun interactie toosuccessfully gebruik back-up en herstel van hello Azure Blob storage-service.

## <a name="azure-blob-storage-service-components"></a>Azure Blob Storage-serviceonderdelen
Hallo worden volgende Azure onderdelen gebruikt wanneer een back-up toohello Azure Blob storage-service.

| Onderdeel | Beschrijving |
| --- | --- |
| **Storage-Account** |Hallo storage-account is Hallo startpunt voor alle storage-services. een Azure Blob Storage-service, tooaccess eerst maken een Azure Storage-account. Zie voor meer informatie over Azure Blob storage-service, [hoe toouse hello Azure Blob Storage-Service](https://azure.microsoft.com/develop/net/how-to-guides/blob-storage/) |
| **Container** |Een container is een groepering van een reeks blobs en kan een onbeperkt aantal Blobs bevatten. toowrite een back-tooan Azure Blob-service van SQL Server, hebt u ten minste Hallo root-container gemaakt. |
| **BLOB** |Een bestand van willekeurig type en de grootte. BLOBs kunnen worden opgevraagd met de volgende URL-indeling Hallo: **https://[storage account].blob.core.windows.net/[container]/[blob]**. Zie voor meer informatie over de pagina-Blobs [Understanding blok en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx) |

## <a name="sql-server-components"></a>SQL Server-onderdelen
Hallo worden volgende SQL Server-onderdelen gebruikt wanneer een back-up toohello Azure Blob storage-service.

| Onderdeel | Beschrijving |
| --- | --- |
| **URL** |De URL bevat een Uniform Resource Identifier (URI) tooa unieke back-upbestand. Hallo-URL is gebruikte tooprovide Hallo locatie en de naam van Hallo SQL Server-back-upbestand. Hallo-URL moet tooan Werkelijke blob, niet alleen een container verwijzen. Als Hallo blob niet bestaat, wordt deze gemaakt. Als een bestaande blob zijn die is opgegeven, back-up mislukt, tenzij Hallo > met indelingsoptie is opgegeven. Hallo Hieronder volgt een voorbeeld van Hallo URL u in de opdracht BACKUP Hallo geeft: **http[s]://[storageaccount].blob.core.windows.net/[container]/[FILENAME.bak]**. HTTPS wordt aanbevolen, maar niet vereist. |
| **Referentie** |Hallo-informatie die is vereist tooconnect en verifiëren van tooAzure Blob storage-service wordt opgeslagen als referentie.  In de volgorde voor SQL Server toowrite back-ups tooan Azure Blob of herstellen uit moet een SQL Server-referentie worden gemaakt. Zie voor meer informatie [referenties van het SQL Server](https://msdn.microsoft.com/library/ms189522.aspx). |

> [!NOTE]
> Als u toocopy kiest en uploaden van een back-upbestand toohello Azure Blob storage-service, moet u een pagina-blob-type gebruiken als uw opslagoptie als u van plan bent toouse dit bestand voor herstelbewerkingen. HERSTEL van een blok-blob-type mislukt met een fout opgetreden.
> 
> 

## <a name="next-steps"></a>Volgende stappen
1. Een Azure-account maken als u er nog geen hebt. Als u Azure evalueert, kunt u overwegen Hallo [gratis proefversie](https://azure.microsoft.com/free/).
2. Ga vervolgens via een Hallo zelfstudies waarin wordt beschreven hoe u een opslagaccount maken en het uitvoeren van een herstelpunt te volgen.
   
   * **SQL Server 2014**: [zelfstudie: SQL Server 2014 back-up en herstel tooMicrosoft Azure Blob Storage-Service](https://msdn.microsoft.com/library/jj720558\(v=sql.120\).aspx).
   * **SQL Server 2016**: [zelfstudie: Hallo Microsoft Azure Blob storage-service met SQL Server 2016-databases](https://msdn.microsoft.com/library/dn466438.aspx)
3. Bekijk de aanvullende documentatie beginnen met [SQL Server-back-up en herstel met Microsoft Azure Blob Storage-Service](https://msdn.microsoft.com/library/jj919148.aspx).

Als u problemen hebt, leest u Hallo onderwerp [SQL Server-back-up tooURL aanbevolen procedures en probleemoplossing](https://msdn.microsoft.com/library/jj919149.aspx).

Voor andere SQL-Server back-up en opties voor terugzetten, Zie [back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

