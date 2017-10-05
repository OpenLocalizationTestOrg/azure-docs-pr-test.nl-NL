---
title: Wat is Azure RemoteApp? | Microsoft Docs
description: Lees hoe u apps en resources op apparaten deelt via Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d4befefcaa0cacdde9cce3d8ad93ae8c4cad47f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-remoteapp"></a>Wat is Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp introduceert de functionaliteit van het on-premises Microsoft RemoteApp-programma, gesteund door Extern-bureaublad-services, in Azure. Met Azure RemoteApp kunt u vanaf een groot aantal verschillende gebruikersapparaten veilige externe toegang bieden tot toepassingen. Azure RemoteApp verzorgt in feite niet-permanente Terminal Server-sessies in de cloud, en u gaat deze gebruiken en delen met uw gebruikers.

Met Azure RemoteApp kunt u apps en resources delen met gebruikers op vrijwel elk apparaat. Uw apps worden gehost in de cloud. Dat betekent dat wij zorg dragen voor de hardware en schaling die nodig is om te voldoen aan de behoeften van gebruikers. U hoeft alleen de apps te uploaden die u wilt delen en ervoor te zorgen dat uw gebruikers deze apps gaan gebruiken. [Gebruikers kunnen hun eigen apparaten blijven gebruiken](remoteapp-clients.md) terwijl u alles beheert via de Azure-portal. U kunt er zelfs voor kiezen om uw bedrijfsreferenties te gebruiken, zodat u de veiligheid van apps en gegevens kunt verzekeren.

Lees verder voor meer informatie over Azure RemoteApp of [probeer het nu uit](https://azure.microsoft.com/services/remoteapp/) als we u al hebben overtuigd.

Hebt u vragen over Azure RemoteApp? Bekijk onze [veelgestelde vragen](remoteapp-faq.md).

Azure RemoteApp maakt deel uit van de [Microsoft Virtual Desktop Infrastructure](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx).

**Nieuw!** Wilt u meer informatie over Azure RemoteApp? Of wilt u Azure RemoteApp op schaal uitproberen? Neem deel aan ons wekelijks [webinar Vraag het de expert](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website).

## <a name="azure-remoteapp-collections"></a>Azure RemoteApp-verzamelingen
Er zijn twee soorten [Azure RemoteApp verzamelingen](remoteapp-collections.md):

* Een **cloudverzameling** wordt gehost in en slaat gegevens voor programma's op in de cloud. Gebruikers hebben toegang tot apps door zich aan te melden met hun Microsoft-account- of bedrijfsreferenties die zijn gesynchroniseerd of verenigd met Azure Active Directory.
  
    Kies een cloudverzameling als de toepassing die u wilt delen geen verbinding nodig heeft met resources in het particuliere netwerk van uw bedrijf (bijvoorbeeld via een VPN-apparaat). Als de toepassing resources gebruikt op internet, in OneDrive of Azure, kunt u een cloudverzameling gebruiken. Het is ook het snelst gemaakt.
* Een **hybride verzameling** wordt gehost in en slaat gegevens op in de Azure-cloud, maar biedt gebruikers ook toegang tot gegevens en resources die zijn opgeslagen in uw lokale netwerk. Gebruikers hebben toegang tot apps door zich aan te melden met hun bedrijfsreferenties die zijn gesynchroniseerd of verenigd met Azure Active Directory.
  
    Kies een hybride verzameling als u een verbinding nodig hebt met resources in het particuliere netwerk van uw bedrijf. Bijvoorbeeld, als de toepassing toegang moet hebben tot:
  
  * Bestandsservers op het intranet
  * Quicken
  * Databases achter een firewall
    
    Dit is doorgaans nuttiger voor grote bedrijven met veel resources in hun particuliere netwerken die niet naar de cloud kunnen worden verplaatst.

De verschillende verzamelingen hebben verschillende opties, waaronder netwerken. Zoek daarom uit [welke verzameling](remoteapp-collections.md) het meest geschikt is voor u. 

### <a name="updating-your-collection"></a>Een verzameling bijwerken
Een van de belangrijkste verschillen tussen een hybride verzameling en een cloudverzameling is de manier waarop software-updates worden afgehandeld. Met een cloudverzameling die gebruikmaakt van de vooraf geïnstalleerde installatiekopie van Office 365 ProPlus of Office 2013, hoeft u zich geen zorgen te maken over updates. De service onderhoudt zichzelf en de updates worden met vaste regelmatig uitgevoerd, zowel voor de apps als voor het besturingssysteem.

Voor hybride verzamelingen en voor cloudverzamelingen die gebruikmaken van een installatiekopie van een aangepaste sjabloon, zult u de installatiekopie en apps zelf moeten onderhouden. Voor installatiekopieën die lid zijn van een domein kunt u updates beheren met hulpprogramma's als Windows Update, Groepsbeleid of System Center.

Wanneer u de installatiekopie van een aangepaste sjabloon hebt bijgewerkt, uploadt u de nieuwe installatiekopie naar de Azure-cloud en werkt u vervolgens de verzameling bij voor het gebruik van de nieuwe installatiekopie. (U kunt dit doen vanaf de pagina **Snel starten** van Azure RemoteApp, of vanuit het Dashboard.)

Zie [Een verzameling bijwerken](remoteapp-update.md) voor meer informatie.

## <a name="supported-remoteapp-clients"></a>Ondersteunde RemoteApp-clients
Azure RemoteApp wordt ondersteund op de RemoteApp-client-apps voor Windows en Windows RT en op de Microsoft Remote Desktop-apps voor Mac, iOS en Android. Uw gebruikers kunnen deze apps op hun mobiele of desktopapparaten gebruiken om toegang te krijgen tot de nieuwe Azure RemoteApp-programma's.

Zie [Uw apps openen in Azure RemoteApp](remoteapp-clients.md) voor meer informatie over de clients.

## <a name="next-steps"></a>Volgende stappen
Aan de slag Probeer het nu! Deze artikelen helpen u op weg met Azure RemoteApp:

* [Wat voor verzameling hebt u nodig voor Azure RemoteApp?](remoteapp-collections.md)
* [Een installatiekopie maken voor Azure RemoteApp](remoteapp-imageoptions.md)
* [Een cloudverzameling maken van Azure RemoteApp](remoteapp-create-cloud-deployment.md)
* [Een hybride cloudverzameling maken van Azure RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Hoe werkt licentieverlening in Azure RemoteApp?](remoteapp-licensing.md)
* [Aanbevolen procedures voor het gebruik van Azure RemoteApp](remoteapp-bestpractices.md)
* [Veelgestelde vragen over Azure RemoteApp](remoteapp-faq.md)

### <a name="help-us-help-you"></a>Help ons u te helpen
Wist u dat u niet alleen dit artikel kunt beoordelen en opmerkingen kunt toevoegen, maar zelfs wijzigingen kunt aanbrengen in het artikel zelf? Ontbreekt er iets? Is er iets niet juist? Heb ik iets geschreven dat niet duidelijk is? Blader omhoog en klik op **Edit on GitHub** of **Edit** als u wijzigingen wilt aanbrengen. Deze worden eerst nagekeken en wanneer ze zijn goedgekeurd, worden uw wijzigingen en verbeteringen hier weergegeven.

