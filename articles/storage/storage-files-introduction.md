---
title: aaaIntroduction tooAzure File storage | Microsoft Docs
description: Een overzicht van Azure File storage, een service waarmee u toocreate en gebruik netwerkbestand deelt in Hallo Hallo industrie-initiatief met Microsoft-Cloud.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: a0a6a80a2ccd9742aa470bdd02ff375387a1629b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Inleiding tooAzure File storage
Azure File storage biedt bestandsshares netwerk in Hallo cloud met behulp van industriestandaard Hallo [Protocol Server Message Block (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) en [Common Internet File System (CIFS)](https://technet.microsoft.com/library/cc939973.aspx). Azure-bestandsshares kunnen gelijktijdig worden gekoppeld door clients zoals on-premises implementaties van Windows, Mac OS, Linux of door virtuele Azure-machines. Een opslagaccounts voor algemeen gebruik biedt u toegang tot tooAzure opslag van bestanden en andere services zoals Blobs, virtuele machine van Azure-schijven, wachtrijen onder één account.



## <a name="videos"></a>Video's
| Inleiding tot Azure File storage (27 minuten) | Azure File Storage-zelfstudie (5 minuten)  |
|-|-|
| [![Screencap van Hallo Introducing Azure File storage video - Klik tooplay.](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Screencap van hello Azure File storage zelfstudie - Klik tooplay.](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Waarom Azure File Storage handig is
Azure File storage kunt u tooreplace Server, Windows, Linux, of NAS-bestandsservers gehost lokaal of in de cloud Hallo met een besturingssysteem vrije cloud-bestand delen. Dit heeft Hallo volgende voordelen:

* **Gedeelde toegang**. Azure support Hallo bedrijfstak standaard SMB-protocol, wat betekent dat u naadloos door uw lokale bestandsshares Azure-bestandsshares vervangen kunt zonder dat u toepassingscompatibiliteit voor bestandsshares. Wordt kunnen tooshare een bestandssysteem over meerdere machines, is-toepassingen/exemplaren een belangrijk voordeel ten met Azure File storage voor toepassingen die shareability moeten. 
* **Volledig beheerd**. Azure-bestandsshares kunnen worden gemaakt zonder Hallo nodig toomanage hardware of een besturingssysteem. Dit betekent dat u hebt geen toodeal met patchen Hallo serverbesturingssysteem met essentiële upgrades of defecte harde schijven vervangen.
* **Scripts en hulpprogramma’s**. PowerShell-cmdlets en Azure CLI mag gebruikte toocreate koppelen en beheren van bestandsshares voor opslag als onderdeel van Hallo beheer van Azure-toepassingen. U kunt maken en beheren met Azure Portal en Azure storage Explorer Azure-bestandsshares. 
* **Flexibiliteit**. Azure File storage is uit Hallo gemalen up toobe altijd beschikbaar gemaakt. Lokale bestandsshares vervangen met Azure File storage betekent dat u niet langer toowake up toodeal met lokale stroomstoringen of netwerkproblemen. 
* **Vertrouwde programmeerbaarheid**. Toepassingen die worden uitgevoerd in Azure toegang tot gegevens in de share Hallo via bestand [system I/O APIs](https://msdn.microsoft.com/library/system.io.file.aspx). Ontwikkelaars kunnen daarom gebruikmaken van hun bestaande code en vaardigheden toomigrate bestaande toepassingen. Bovendien tooSystem i/o-API's, kunt u [clientbibliotheken van Azure Storage](https://msdn.microsoft.com/library/azure/dn261237.aspx) of Hallo [REST-API van Azure Storage](/rest/api/storageservices/file-service-rest-api).

Azure-bestandsshares kunnen worden gebruikt voor het volgende:

* **Ter vervanging van lokale bestandsservers**:  
    Azure File storage kan worden gebruikt toocompletely vervangen bestandsshares op de bestandsservers traditionele on-premises of NAS-apparaten. Populaire besturingssystemen, zoals Windows, Mac OS- en Linux kunt gemakkelijk een Azure-bestandsshare koppelen waar ze ook in Hallo wereld zijn.

* **'Lift- en shift'-toepassingen**:  
    Azure File storage kunt u gemakkelijk te 'lift- en verschuiven' toepassingen toohello cloud die gebruikmaken van lokale bestand tooshare gegevens tussen onderdelen van de toepassing hello deelt. dit gebeuren toomake elke virtuele machine maakt verbinding toohello bestandsshare en vervolgens het kan bestanden lezen en schrijven net zoals het zou tegen een lokaal bestand delen.

* **Cloudontwikkeling vereenvoudigen**:  
    Azure File storage kan worden gebruikt in een aantal verschillende manieren toosimplify ontwikkelingsprojecten van nieuwe cloud.
    * **Gedeelde toepassingsinstellingen**:  
        Een algemene patroon voor gedistribueerde toepassingen is toohave configuratiebestanden op een centrale locatie waar ze toegankelijk zijn vanuit veel andere VM's. Dergelijke configuratiebestanden kunnen nu worden opgeslagen op een Azure-bestandsshare en worden gelezen door alle exemplaren van een toepassing. Deze instellingen kunnen ook worden beheerd via de REST-interface hello, waarmee u wereldwijd toegang krijgt toohello configuratiebestanden.

    * **Diagnostische gegevens delen**:  
        Een Azure-bestandsshare kan ook worden gebruikt toosave diagnostische bestanden zoals Logboeken, meetgegevens en crashdumps. Deze updates via SMB Hallo en REST-interface kunt toepassingen toobuild of gebruikmaken van tal van hulpprogramma's voor analyse voor het verwerken en analyseren van Hallo diagnostische gegevens.

    * **Ontwikkelen/testen/fouten opsporen**:  
        Wanneer ontwikkelaars of beheerders op VM's in de cloud Hallo werkt, moeten ze vaak een set hulpprogramma's of hulpprogramma's. Het installeren en distribueren van deze hulpprogramma's op elke virtuele machine waar ze nodig zijn, kan een tijdrovend proces zijn. Met Azure File storage, kan een ontwikkelaar of beheerder opslaan hun favoriete tools op een bestandsshare, wat kan eenvoudig verbonden toofrom een virtuele machine.
        
## <a name="how-does-it-work"></a>Hoe werkt het?
Het beheren van Azure-bestandsshares is veel eenvoudiger dan het beheren van bestandsshares op locatie. Hallo volgende diagram illustreert hello Azure File storage management-constructs:

![Bestandsstructuur](../../includes/media/storage-file-concepts-include/files-concepts.png)

* **Storage-Account**: alle toegang tot tooAzure opslag wordt gedaan via een opslagaccount. Zie Schaalbaarheids- en prestatiedoelen in Azure Storage voor meer informatie over opslagaccountcapaciteit.
* **Share**: een File Storage-share is een SMB-bestandsshare in Azure. Alle mappen en bestanden moeten worden gemaakt in een bovenliggende share. Een account kan een onbeperkt aantal shares bevatten en een bestandsshare kan een onbeperkt aantal bestanden toohello 5 TB totale capaciteit van de bestandsshare Hallo opslaan.
* **Map**: een optionele hiërarchie van mappen.
* **Bestand**: een bestand in Hallo-share. Een bestand mogelijk up too1 TB groot zijn.
* **URL-indeling**: bestanden kunnen worden opgevraagd met Hallo URL-indeling te volgen:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```
## <a name="next-steps"></a>Volgende stappen
* [Azure-bestandsshare maken](storage-file-how-to-create-file-share.md)
* [Verbinding maken en koppelen in Windows](storage-file-how-to-use-files-windows.md)
* [Verbinding maken en koppelen in Linux](storage-how-to-use-files-linux.md)
* [Verbinding maken en koppelen in macOS](storage-file-how-to-use-files-mac.md)
* [Veelgestelde vragen](storage-files-faq.md)
* [Problemen oplossen](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Conceptuele artikelen en video's
* [Azure File Storage: een naadloos SMB-bestandssysteem voor Windows en Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Hulpprogramma-ondersteuning voor Azure File Storage
* [Azure PowerShell gebruiken met Azure Storage](storage-powershell-guide-full.md)
* [Hoe toouse AzCopy met Microsoft Azure Storage](storage-use-azcopy.md)
* [Hello Azure CLI gebruiken met Azure Storage](storage-azure-cli.md#create-and-manage-file-shares)

### <a name="blog-posts"></a>Blogberichten
* [Azure File storage is now generally available (Azure File Storage is nu algemeen beschikbaar)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage (Een kijkje achter de schermen van Azure File Storage)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introducing Microsoft Azure File Service (Introductie van Microsoft Azure File-service)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migreren gegevens tooAzure bestand](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Naslaginformatie
* [Naslaginformatie over de Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Naslaginformatie over REST API voor bestandsservices](http://msdn.microsoft.com/library/azure/dn167006.aspx)
