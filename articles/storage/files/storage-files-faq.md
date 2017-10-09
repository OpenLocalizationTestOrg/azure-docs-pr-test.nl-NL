---
title: Veelgestelde vragen over Azure File storage aaaFrequently | Microsoft Docs
description: Hier vindt u antwoorden op veelgestelde vragen over Azure File storage toofrequently.
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
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: d8a94fdc77e928dbc6996e1e635cd3527e0c67d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Veelgestelde vragen over Azure File storage

## <a name="general"></a>Algemeen
* **Q. Wat is Azure File storage?**  
   
    Azure File storage is een gedistribueerd bestandssysteem in Azure. Dit biedt een SMB-protocol-interface waarmee gebruikers toomount Hallo opslag als share met de systeemeigen op ondersteunde Azure virtuele Machine of op de lokale machine.

* **Q. Waarom is Azure File storage nuttig?**  
   
    Azure File storage biedt toegang tot gedeelde gegevens op meerdere VM's en platforms. Raadpleeg te[waarom Azure File storage is nuttig](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **Q. Wanneer gebruikt u Azure File-tegenover Azure Blob-tegenover Azure-schijf?**  
   
    Microsoft Azure biedt verschillende manieren toostore en toegang tot gegevens in Hallo cloud.  
   
    Azure File storage - biedt een interface SMB, clientbibliotheken en een REST-interface waarmee eenvoudig toegang vanaf elke locatie toostored bestanden.  
   
    Azure Blobs: beschikt over een REST-interface waarmee ongestructureerde gegevens toobe opgeslagen en gebruikt een grootschalige in blok-blobs en clientbibliotheken.  
   
    Azure Data schijven: beschikt over een REST-interface waarmee gegevens toobe permanent opgeslagen en is toegankelijk vanuit een gekoppelde virtuele harde schijf en clientbibliotheken.  
   
    Meer informatie over [gebruik wanneer toouse Azure Blobs, Azure-bestanden of Azure gegevensschijven](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)

* **Q. Hoe ga ik aan de slag met Azure File storage?**  
   
    U kunt starten door het maken van een Azure-bestandsshare. U kunt Azure bestandsshares maken met Azure Portal, hello Azure Storage PowerShell-cmdlets, hello Azure Storage-clientbibliotheken of Hallo REST-API van Azure Storage. In deze zelfstudie leert u het:

    * [Meer informatie over hoe Azure File toocreate delen met behulp van Hallo Portal](storage-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Meer informatie over hoe Azure File toocreate delen met behulp van Powershell](storage-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Meer informatie over hoe Azure File toocreate delen met CLI](storage-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **Q. Welke replicaties worden ondersteund door Azure File storage?**  
   
    Azure File storage ondersteunt alleen LRS of GRS nu. We zullen toosupport RA-GRS maar is er nog geen tooshare tijdlijn.

## <a name="security-authentication-and-access-control"></a>Beveiliging, verificatie en toegangsbeheer

* **Q. Wat zijn verschillende manieren tooaccess bestanden in Azure File storage?**
    
    U kunt Hallo bestandsshare koppelen op uw lokale machine met behulp van SMB 3.0-protocol of gebruik hulpprogramma's zoals [Opslagverkenner](http://storageexplorer.com/) tooaccess bestanden in de bestandsshare. U kunt van uw toepassing opslagclientbibliotheken, REST-API's of Powershell tooaccess delen van bestanden in Azure File gebruiken.

* **Q. Hoe kan ik toegang tot tooa specifiek bestand met een webbrowser bieden?**
    
    Met SAS, kunt u tokens met specifieke machtigingen die geldig voor een opgegeven tijdsinterval zijn genereren. U kunt bijvoorbeeld een token genereren met alleen-lezentoegang tooa bepaald bestand voor een bepaalde periode. Iedereen die deze url bezit toegankelijk Hallo-bestand rechtstreeks via elke webbrowser wanneer deze geldig is. SAS-sleutels kunnen eenvoudig worden gegenereerd vanuit een gebruikersinterface zoals Opslagverkenner.

* **Q. Is het mogelijk toospecify alleen-lezen of alleen-schrijven machtigingen op mappen binnen Hallo share?**
    
    U hebt niet op dit niveau van controle over machtigingen als u Hallo bestandsshare via SMB koppelt. U kunt dit echter bereiken door het maken van een shared access signature (SAS) via Hallo REST-API of clientbibliotheken.  

* **Q. Hoe kan ik serverzijde versleuteling voor Azure File storage inschakelen?**

    [Serverversleuteling](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) voor Azure File storage is algemeen beschikbaar in alle regio's en openbare en nationale clouds. U kunt de SSE inschakelen voor het gebruik van Azure File storage [Azure-portal](https://portal.azure.com/),[API van Microsoft Azure Storage Resource Provider](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) of [Azure CLI ](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).
    
    Nadat de SSE op Azure File storage is ingeschakeld, wordt geen nieuwe gegevens toohello bestandsopslag geschreven in dit opslagaccount automatisch versleuteld. Deze functie is beschikbaar voor alle nieuwe gegevens tooexisting of nieuwe shares geschreven in een bestaande of nieuwe storage-account. Er zijn geen extra kosten verbonden aan het inschakelen van deze functie. Meer informatie over [hoe tooenable SSE op Azure File storage](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

* **Q. Wordt verificatie op basis van Active Directory ondersteund door Azure File storage?**
   
    Op dit moment wordt verificatie op basis van AD of ACL's nog niet ondersteund, maar deze mogelijkheid staat wel in onze lijst met functieaanvragen. Op dit moment zijn hello Azure opslagaccountsleutels gebruikte tooprovide verificatie toohello bestandsshare. We bieden een tijdelijke oplossing met shared access signatures (SAS) via Hallo REST-API of Hallo clientbibliotheken. Met SAS, kunt u tokens met specifieke machtigingen die geldig voor een opgegeven tijdsinterval zijn genereren. U kunt bijvoorbeeld een token genereren met alleen-lezentoegang tooa opgegeven bestand met de verloopdatum van 10 minuten. Iedereen die dit token beschikt wanneer deze geldig is heeft alleen-lezentoegang toothat bestand de 10 minuten.
   
    SAS wordt alleen ondersteund via Hallo REST-API of clientbibliotheken. Wanneer u Hallo bestandsshare via Hallo SMB-protocol koppelt, kunt u een SAS toodelegate toegang tooits inhoud niet gebruiken. 
    
* **Q. Wat zijn de beleidsregels voor naleving van Hallo gegevens voor Azure File storage ondersteund?**

   Azure File Storage wordt uitgevoerd boven dezelfde opslagarchitectuur Hallo als andere opslag in Azure Storage-services en is van toepassing hello dezelfde gegevens nalevingsbeleid. Meer informatie over de naleving van Azure Storage-gegevens, die u kunt downloaden en te verwijzen[Microsoft Azure Data Protection document](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Toegang tot on-Premises

* **Q.Do ik heb toouse Azure ExpressRoute tooconnect tooAzure opslag van bestanden van een lokale virtuele machine?**
   
    Nee. Als er geen ExpressRoute, u nog steeds toegang tot de bestandsshare Hallo van on-premises zolang 445 (TCP uitgaand) geopend voor toegang tot Internet poort. Echter, kunt u ExpressRoute met Azure File storage als u dit wilt.

* **Q. Hoe kan ik een Azure-bestandsshare op mijn lokale computer koppelen?** 
    
    U kunt Hallo bestandsshare koppelt via SMB-protocol Hallo zolang poort 445 (TCP uitgaand) geopend is en de client Hallo SMB 3.0-protocol ondersteunt (bijvoorbeeld, u Windows 10 of Windows Server 2012). Neem contact op met uw lokale ISP-provider toounblock Hallo poort. In tijdelijke hello, kunt u uw bestanden met weergeven [Opslagverkenner](../../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Facturering en prijzen
* **Q. , Hallo netwerkverkeer tussen een virtuele machine van Azure en een bestandsshare mee als externe bandbreedte die wordt verrekend toohello abonnement?**
   
    Als het Hallo-bestandsshare en de virtuele machine zich in Hallo dezelfde Azure-regio, hello verkeer tussen hen is gratis. Als ze zich in verschillende regio's, wordt verkeer tussen hen Hallo als externe bandbreedte in rekening gebracht.

## <a name="backup"></a>Back-up

* **Q. Hoe ik mijn Azure-bestandsshare back-up?**
    
    U kunt gebruikmaken van AzCopy, RoboCopy, of een 3rd partij back-hulpprogramma dat u kunt back-up een gekoppelde bestandsshare. We verwachten toohave Hallo mogelijkheid tootake momentopnamen van bestandsshares in Hallo nabije toekomst; u zult kunnen toouse delen van deze functie toobackup uw Azure-bestand.

## <a name="performance"></a>Prestaties

* **Q. Wat zijn de schaallimieten Hallo van Azure File storage?**
    Zie voor informatie over de schaalbaarheids- en prestatiedoelen van Azure File storage, [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#scalability-targets-for-blobs-queues-tables-and-files).

* **Q. Mijn prestaties waren slecht tijdens toounzip bestanden naar Azure File storage. Wat moet ik doen?**
    
    tootransfer grote aantallen bestanden naar Azure File storage, wordt aangeraden dat u AzCopy (Windows, Preview voor Linux/Unix) of Azure Powershell gebruiken als u deze hulpprogramma's zijn geoptimaliseerd voor netwerkoverdracht.

* **Q. Wat patches is vrijgegeven toofix prestatieproblemen met Azure File storage?**
    
    Hallo Windows team heeft onlangs een patch toofix een probleem met trage prestaties uitgebracht als Hallo klant Azure File storage vanuit Windows 8.1 of Windows Server 2012 R2 opent. Voor meer informatie gekoppeld uitchecken Hallo Neem KB-artikel [prestaties afnemen wanneer u Azure File storage vanuit Windows 8.1 of Server 2012 R2 opent](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Functies en -interoperabiliteit met andere services
* **Q. Is een 'bestandssharewitness' voor een failovercluster een Hallo gebruiksvoorbeelden voor Azure File storage?**
   
    Dit is momenteel niet ondersteund.

* **Q. Is er een naamswijziging in Hallo REST-API?**
   
    Momenteel niet.

* **Q. Zijn geneste shares, met andere woorden, een share onder een share?**
    
    Nee. Hallo-bestandsshare is Hallo virtuele stuurprogramma dat u koppelen kunt, dus geneste shares worden niet ondersteund.

* **Q. Azure File storage gebruiken met IBM MQ**
    
    IBM heeft een document tooguide IBM MQ-klanten uitgebracht bij het configureren van Azure File storage met hun service. Voor meer informatie raadpleegt [hoe toosetup IBM MQ Multi wachtrijbeheer met Microsoft Azure File Service-instantie](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).


## <a name="troubleshooting"></a>Problemen oplossen
* **Q. Hoe kan ik Azure File storage fouten oplossen?**
    
    U kunt te verwijzen[Azure File storage probleemoplossing artikel](storage-troubleshoot-windows-file-connection-problems.md) voor richtlijnen voor probleemoplossing voor end-to-end. 


## <a name="see-also"></a>Zie ook
Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.

### <a name="conceptual-articles-and-videos"></a>Conceptuele artikelen en video's
* [Azure File Storage: een naadloos SMB-bestandssysteem voor Windows en Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Hoe toouse Azure File storage met Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Hulpprogramma-ondersteuning voor File Storage
* [Hoe toouse AzCopy met Microsoft Azure Storage](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Hello Azure CLI gebruiken met Azure Storage](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Problemen met betrekking tot Azure File Storage oplossen](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a>Blogberichten
* [Azure File storage is now generally available (Azure File Storage is nu algemeen beschikbaar)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage (Een kijkje achter de schermen van Azure File Storage)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introducing Microsoft Azure File Service (Introductie van Microsoft Azure File-service)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migreren gegevens tooAzure File storage](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Naslaginformatie
* [Naslaginformatie over de Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Naslaginformatie over REST API voor bestandsservices](http://msdn.microsoft.com/library/azure/dn167006.aspx)
