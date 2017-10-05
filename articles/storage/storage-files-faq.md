---
title: Veelgestelde vragen over Azure File storage | Microsoft Docs
description: Hier vindt u antwoorden op veelgestelde vragen over Azure File storage.
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
ms.openlocfilehash: cb2134502a585c4f9772e594f635c10f1841e46f
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Veelgestelde vragen over Azure File storage

## <a name="general"></a>Algemeen
* **Q. Wat is Azure File storage?**  
   
    Azure File storage is een gedistribueerd bestandssysteem in Azure. Dit biedt een SMB-protocol-interface waarmee gebruikers kunnen de opslag koppelen als share met de systeemeigen op ondersteunde Azure virtuele Machine of op de lokale machine.

* **Q. Waarom is Azure File storage nuttig?**  
   
    Azure File storage biedt toegang tot gedeelde gegevens op meerdere VM's en platforms. Raadpleeg [waarom Azure File storage is nuttig](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **Q. Wanneer gebruikt u Azure File-tegenover Azure Blob-tegenover Azure-schijf?**  
   
    Microsoft Azure biedt verschillende manieren opslaan en gebruiken van gegevens in de cloud.  
   
    Azure File storage - biedt een SMB-interface, clientbibliotheken, en een REST-interface eenvoudig waarmee openen vanaf een willekeurige plaats opgeslagen bestanden.  
   
    Azure Blobs: beschikt over een REST-interface waarmee ongestructureerde gegevens kunnen worden opgeslagen en gebruikt een grootschalige in blok-blobs en clientbibliotheken.  
   
    Azure Data schijven: beschikt over een REST-interface waarmee gegevens naar permanent worden opgeslagen en is toegankelijk vanuit een gekoppelde virtuele harde schijf en clientbibliotheken.  
   
    Meer informatie over [beslissen wanneer u Azure Blobs, Azure-bestanden of Azure gegevensschijven gebruiken](storage-decide-blobs-files-disks.md)

* **Q. Hoe ga ik aan de slag met Azure File storage?**  
   
    U kunt starten door het maken van een Azure-bestandsshare. U kunt Azure bestandsshares maken met Azure Portal, de Azure Storage PowerShell-cmdlets, de clientbibliotheken van Azure Storage of de REST-API van Azure Storage. In deze zelfstudie leert u het:

    * [Informatie over het maken van Azure-bestandsshare met behulp van de Portal](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Informatie over het maken van bestandsshare in Azure met behulp van Powershell](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Informatie over het maken van bestandsshare in Azure met CLI](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **Q. Welke replicaties worden ondersteund door Azure File storage?**  
   
    Azure File storage ondersteunt alleen LRS of GRS nu. We willen RA-GRS ook gaan ondersteunen, maar we kunnen nog niet zeggen op welke termijn dit gaat gebeuren.

## <a name="security-authentication-and-access-control"></a>Beveiliging, verificatie en toegangsbeheer

* **Q. Wat zijn verschillende manieren toegang krijgen tot bestanden in Azure File storage?**
    
    U kunt de bestandsshare koppelen op uw lokale machine met behulp van SMB 3.0-protocol of gebruik hulpprogramma's zoals [Opslagverkenner](http://storageexplorer.com/) toegang krijgen tot bestanden in de bestandsshare. U kunt van uw toepassing opslagclientbibliotheken REST-API's of Powershell toegang tot uw bestanden in Azure-bestandsshare.

* **Q. Hoe kan ik toegang bieden tot een specifiek bestand met een webbrowser?**
    
    Met SAS, kunt u tokens met specifieke machtigingen die geldig voor een opgegeven tijdsinterval zijn genereren. U kunt bijvoorbeeld een token genereren met alleen-lezen toegang tot een bepaald bestand voor een bepaalde periode. Iedereen die deze url heeft toegang tot het bestand rechtstreeks via elke webbrowser wanneer deze geldig is. SAS-sleutels kunnen eenvoudig worden gegenereerd vanuit een gebruikersinterface zoals Opslagverkenner.

* **Q. Is het mogelijk om op te geven alleen-lezen of alleen-schrijven machtigingen op de mappen in de share?**
    
    Dit niveau van controle over machtigingen is niet mogelijk wanneer u de bestandsshare koppelt via SMB. U kunt dit echter wel bereiken door een Shared Access Signature (SAS) te maken via de REST API of clientbibliotheken.  

* **Q. Hoe kan ik serverzijde versleuteling voor Azure File storage inschakelen?**

    [Serverversleuteling](storage-service-encryption.md) voor Azure File storage is algemeen beschikbaar in alle regio's en openbare en nationale clouds. U kunt de SSE inschakelen voor het gebruik van Azure File storage [Azure-portal](https://portal.azure.com/),[API van Microsoft Azure Storage Resource Provider](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) of [Azure CLI ](storage-azure-cli.md).
    
    Nadat de SSE op Azure File storage is ingeschakeld, wordt geen nieuwe gegevens geschreven naar de opslag van bestanden in dit opslagaccount automatisch versleuteld. Deze functie is beschikbaar voor alle nieuwe gegevens die worden geschreven naar bestaande of nieuwe shares in een bestaand of nieuw opslagaccount. Er zijn geen extra kosten verbonden aan het inschakelen van deze functie. Meer informatie over [SSE op Azure File storage inschakelen](storage-service-encryption.md).

* **Q. Wordt verificatie op basis van Active Directory ondersteund door Azure File storage?**
   
    Op dit moment wordt verificatie op basis van AD of ACL's nog niet ondersteund, maar deze mogelijkheid staat wel in onze lijst met functieaanvragen. Op dit moment worden Azure Storage-accountsleutels gebruikt voor verificatie naar de bestandsshare. We bieden een tijdelijke oplossing met Shared Access Signatures (SAS) via de REST API of de clientbibliotheken. Met SAS, kunt u tokens met specifieke machtigingen die geldig voor een opgegeven tijdsinterval zijn genereren. U kunt bijvoorbeeld een token met alleen-lezen toegang tot een bepaald bestand 10 minuten verloopdatum genereren. Iedereen die dit token beschikt wanneer deze geldig is heeft alleen-lezen toegang tot dit bestand die 10 minuten.
   
    SAS wordt alleen ondersteund via de REST API of clientbibliotheken. Wanneer u de bestandsshare via het SMB-protocol koppelt, kunt u een SAS niet gebruiken voor toegang tot de inhoud ervan te delegeren. 
    
* **Q. Wat zijn de gegevens nalevingsbeleid voor Azure File storage ondersteund?**

   Azure File Storage wordt uitgevoerd boven op de dezelfde opslagarchitectuur als andere storage-services in Azure Storage en past de beleidsregels voor naleving van dezelfde gegevens. Meer informatie over de naleving van Azure Storage-gegevens, die u kunt downloaden en verwijzen naar [Microsoft Azure Data Protection document](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Toegang tot on-Premises

* **Q.Do heb ik Azure ExpressRoute gebruiken vanaf een lokale virtuele machine verbinding maken met Azure File storage?**
   
    Nee. Als u niet over ExpressRoute beschikt, hebt u nog steeds toegang tot de bestandsshare vanaf een on-premises computer, zolang poort 445 (TCP uitgaand) is geopend voor internettoegang. Echter, kunt u ExpressRoute met Azure File storage als u dit wilt.

* **Q. Hoe kan ik een Azure-bestandsshare op mijn lokale computer koppelen?** 
    
    U kunt de bestandsshare koppelt via het SMB-protocol, zolang poort 445 (TCP uitgaand) geopend is en de client het SMB 3.0-protocol ondersteunt (bijvoorbeeld, u Windows 10 of Windows Server 2012). Neem contact op met uw lokale ISP-provider om de poort te deblokkeren. In de tussentijd kunt u uw bestanden met weergeven [Opslagverkenner](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Facturering en prijzen
* **Q. Telt het netwerkverkeer tussen een virtuele machine van Azure en een bestandsshare mee als externe bandbreedte die wordt verrekend met het abonnement?**
   
    Als de bestandsshare en de virtuele machine zich in dezelfde Azure-regio, wordt het verkeer tussen hen is gratis. Als ze zich in verschillende regio's, wordt het verkeer tussen hen als externe bandbreedte in rekening gebracht.

## <a name="backup"></a>Back-up

* **Q. Hoe ik mijn Azure-bestandsshare back-up?**
    
    U kunt gebruikmaken van AzCopy, RoboCopy, of een 3rd partij back-hulpprogramma dat u kunt back-up een gekoppelde bestandsshare. We verwachten dat de mogelijkheid aan momentopnamen van bestandsshares in de nabije toekomst; u kunt zich met deze functie kunt u back-up van uw Azure-bestandsshare.

## <a name="performance"></a>Prestaties

* **Q. Wat zijn de schaallimieten van Azure File storage?**
    Zie voor informatie over de schaalbaarheids- en prestatiedoelen van Azure File storage, [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).

* **Q. Mijn prestaties waren slecht tijdens het uitpakken van bestanden naar Azure File storage. Wat moet ik doen?**
    
    Om grote aantallen bestanden overdragen naar Azure File storage, is het raadzaam dat u AzCopy (Windows, Preview voor Linux/Unix) of Azure Powershell gebruiken als u deze hulpprogramma's zijn geoptimaliseerd voor netwerkoverdracht.

* **Q. Wat patches heeft is beschikbaar voor het oplossen van prestatieproblemen met Azure File storage?**
    
    Het Windows-team heeft onlangs een patch een probleem met trage prestaties wanneer de klant Azure File storage vanuit Windows 8.1 of Windows Server 2012 R2 opent uitgebracht. Voor meer informatie, Controleer of het bijbehorende KB-artikel [prestaties afnemen wanneer u Azure File storage vanuit Windows 8.1 of Server 2012 R2 opent](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Functies en -interoperabiliteit met andere services
* **Q. Is een 'bestandssharewitness' voor een failovercluster een van de gebruiksvoorbeelden voor Azure File storage?**
   
    Dit is momenteel niet ondersteund.

* **Q. Is er een naamswijziging in de REST-API?**
   
    Momenteel niet.

* **Q. Zijn geneste shares, met andere woorden, een share onder een share?**
    
    Nee. De bestandsshare is het virtuele stuurprogramma dat u kunt koppelen. Geneste shares worden dus niet ondersteund.

* **Q. Azure File storage gebruiken met IBM MQ**
    
    IBM heeft een document IBM MQ-klanten te helpen bij het configureren van Azure File storage met hun service uitgebracht. Voor meer informatie raadpleegt u [How to setup IBM MQ Multi instance queue manager with Microsoft Azure File Service](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service) (IBM MQ-wachtrijbeheer voor meerdere instanties instellen met Microsoft Azure File-service.


## <a name="troubleshooting"></a>Problemen oplossen
* **Q. Hoe kan ik Azure File storage fouten oplossen?**
    
    U kunt verwijzen naar [Azure File storage probleemoplossing artikel](storage-troubleshoot-file-connection-problems.md) voor richtlijnen voor probleemoplossing voor end-to-end. 


## <a name="see-also"></a>Zie ook
Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.

### <a name="conceptual-articles-and-videos"></a>Conceptuele artikelen en video's
* [Azure File Storage: een naadloos SMB-bestandssysteem voor Windows en Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Azure File Storage gebruiken met Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Hulpprogramma-ondersteuning voor File Storage
* [Azure PowerShell gebruiken met Azure Storage](storage-powershell-guide-full.md)
* [AzCopy gebruiken met Microsoft Azure Storage](storage-use-azcopy.md)
* [De Azure CLI gebruiken met Azure Storage](storage-azure-cli.md)
* [Problemen met betrekking tot Azure File Storage oplossen](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a>Blogberichten
* [Azure File storage is now generally available (Azure File Storage is nu algemeen beschikbaar)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage (Een kijkje achter de schermen van Azure File Storage)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introducing Microsoft Azure File Service (Introductie van Microsoft Azure File-service)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migreren van gegevens naar Azure File storage](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Naslaginformatie
* [Naslaginformatie over de Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Naslaginformatie over REST API voor bestandsservices](http://msdn.microsoft.com/library/azure/dn167006.aspx)
