---
title: Wat is er nieuw in Azure RemoteApp? | Microsoft Docs
description: Meer informatie over wijzigingen en verbeteringen aangebracht in Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 40f1ba79-80f1-47bd-bf39-f86c03e2306a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aff2e0fc60432b87ed85183fb45eee6e6d8aa5ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-azure-remoteapp"></a>Wat is er nieuw in Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Een van de voordelen van Azure RemoteApp is dat we altijd proberen te verbeteren. Elke keer dat we doen, aankondigen we deze wijzigingen hier.

## <a name="future-updates"></a>Toekomstige updates
Hey - wist u dat het team van Azure RemoteApp boekt maandelijkse updates van de RDS-blog? U vindt niet alleen wat is er gewijzigd in Azure RemoteApp, maar ook andere informatie over het gebruik van RDS. Bekijk de blog [Blog van extern bureaublad-Services](https://blogs.msdn.microsoft.com/rds/), voor meer informatie. Bijvoorbeeld, een paar weken geleden, ze geboekt een vermelding over [op te heffen en verschuiving van werkbelastingen met Azure RemoteApp- en Azure AD](https://blogs.msdn.microsoft.com/rds/2016/01/19/lift-and-shift-your-workloads-with-azure-remoteapp-and-azure-ad-domain-services/).

## <a name="september-2015"></a>September 2015
* Toegevoegde Infopath op de installatiekopie van Microsoft Office 365-sjabloon en de galerie. Als u delen, Infopath wilt, zorg er dan voor dat uw verzamelingen bijwerken met de meest recente afbeelding.
* Client-updates:
  * Windows-client bijgewerkt zodat gebruikers feedback, met name om verbindingsproblemen delen.
  * iOS-client is bijgewerkt om op te lossen foutberichten en oplossen van problemen waar uw referenties verlopen eerder dan verwacht.
* We proberen op de ondersteuning van Office 2016 getest. Zodra dat voltooid, zoekt u bijgewerkte afbeeldingen.
* Een nieuw artikel gepubliceerd over de [verschillen tussen cloud en hybride verzamelingen](remoteapp-collections.md) -dit helpt u het verzamelingtype die geschikt is voor uw apps - alleen in de cloud, cloud + VNET of hybride kiezen.
* Willen delen met Azure RemoteApp QuickBooks, maar niet zeker weet wat de stappen? Bekijk [van Eric nieuw artikel](remoteapp-quickbooks.md) dat u precies wat te doen.

## <a name="august-2015"></a>Augustus 2015
Grote wijzigingen hebben plaatsgevonden in augustus - Hier volgen de belangrijkste eigenschappen:

* U kunt nu een Azure-VNET met een cloudverzameling gebruiken! Bekijk de [instructies voor het maken van cloud](remoteapp-create-cloud-deployment.md) voor de nieuwe stappen.
* Maakte het mogelijk is het toevoegen van apps naar de ** Start ** menu voor de Windows-RemoteApp-client. Apps worden weergegeven in de lijst met toepassingen en u kunt vastmaken aan de ** Start ** menu van Windows.
* Een nieuwe installatiekopie aan de virtuele machine van Azure-galerie - Windows Server Remote Desktop Session Host met Microsoft Office 365 ProPlus toegevoegd.
* De Mac-client, zodat apps met modaal windows stopt bevriezing vast.
* Beschreven hoe u kunt uw [Office 365 ProPlus-abonnement](remoteapp-officesubscription.md) met Azure RemoteApp.
* U kunt gedetailleerde [apps en gegevens beveiligen](remoteapp-secure.md) in uw Azure RemoteApp-verzameling.

## <a name="july-2015"></a>Juli 2015
Juli instellen de fase voor wijzigingen binnenkort in augustus, zodat er niet veel praten over nu, voornamelijk doc updates. Hier volgen de meest recente wijzigingen:

* Toegevoegd een **ondersteunen** tabblad naar de portal, zodat u eenvoudiger toegang krijgen Ondersteuningsbronnen, zoals de forums tot.
* De informatie over probleemoplossing voor het maken van een hybride verzameling gewerkt. Bekijk [nieuwste en beste](remoteapp-hybridtrouble.md) voor het oplossen van tips zoals het identificeren van de juiste poorten configureren voor uw VNET.
* Beschreven hoe [gebruikersgegevens](remoteapp-upd.md) wordt gemaakt en opgeslagen in Azure RemoteApp.
* Beschreven hoe naar [vergrendelen apps](remoteapp-secure.md).
* Gepubliceerd de [Azure RemoteApp-cmdlets](https://msdn.microsoft.com/library/mt428031.aspx).
* En ten slotte we een conversatie met sommige Azure RemoteApp-gebruikers over terminologie gestart. Zoek naar wijzigingen in de manier waarop die we naar de andere verzameling opties verwijzen.

## <a name="june-2015"></a>Juni 2015
Zo veel wijzigingen! Het team is bezet in juni:

* De Azure RemoteApp is opnieuw ontworpen zodat [startpagina](https://www.remoteapp.windowsazure.com/) -uitchecken!
* De software in de beschikbare installatiekopieën bijgewerkt als onderdeel van uw abonnement.
* Verbeteringen in hybride verzamelingen, met inbegrip van geforceerde tunneling ondersteuning en IP-subnetgrootte controleren voordat u probeert te maken van de verzameling gemaakt.
* Gedetecteerd die het * jokerteken werkt niet voor webcam. In plaats daarvan moet u de exemplaar-ID of GUID opgeven. We je bijwerken de omleiding van informatie te brengen met.
* Het geworden zodat u aangepaste antivirussoftware aan uw installatiekopie toevoegen kunt wanneer u de installatiekopie van een sjabloon van de Azure-galerie maken.

Wij hebben meer wijzigingen zodat we weer met een andere update snel uit te rollen in juli.

## <a name="may-2015"></a>Mei 2015
Er zijn een aantal toevoegingen (en maanden) omdat we eerst gemaakt in dit onderwerp, zodat deze lijst iets cheats en vanaf het begin van maart via mogelijk. Bekijk deze nieuwe functies:

* Alles automatiseren - Azure RemoteApp heeft nu [cmdlets in de Azure PowerShell-module](remoteapp-tutorial-arawithpowershell.md).
* [Een Azure RemoteApp-installatiekopie maken van een virtuele machine van Azure](remoteapp-image-on-azurevm.md). Zorgt ervoor dat uw aangepaste installatiekopie uploaden naar Azure veel sneller.
* Een Azure-VNET gebruiken in plaats van een RemoteApp VNET verbinding maken met uw zakelijke netwerkbronnen Azure. We hebben bijgewerkt de [instructies voor hybride verzamelingen](remoteapp-create-hybrid-deployment.md) u stapsgewijs door het maken van een Azure VNET (dit is stap 1).
* Bekijk spreken van VNETs [de nieuwe richtlijnen](remoteapp-vnetsizing.md) rond VNET grootte limieten en beperkingen.
* En spreken limieten - net wat zijn de [Servicelimieten en standaardinstellingen](../azure-subscription-service-limits.md)?

Wilt u meer informatie over Azure RemoteApp? De RemoteApp-team is uitgaand van kracht op Ignite enkele weken geleden. Het uitchecken van Eric de video [de basisprincipes van Microsoft Azure RemoteApp-Management en beheer](http://channel9.msdn.com/Events/Ignite/2015/BRK3868).

Voor een overzicht van Azure RemoteApp in de praktijk nodig? Bekijk de [een app uitvoeren op elk apparaat overal](remoteapp-anyapp.md) zelfstudie - dit wordt beschreven hoe u Access delen met uw gebruikers, waaronder delen van bestanden van de database. We hebben ook een zelfstudie op [waardoor Office 365](remoteapp-tutorial-o365anywhere.md) dezelfde op elk apparaat uitvoeren.

Bedankt voor ons bevalt - back van de volgende maand met meer updates.

### <a name="help-us-help-you"></a>Help ons u te helpen
Wist u dat u niet alleen dit artikel kunt beoordelen en opmerkingen kunt toevoegen, maar zelfs wijzigingen kunt aanbrengen in het artikel zelf? Ontbreekt er iets? Is er iets niet juist? Heb ik iets geschreven dat niet duidelijk is? Blader omhoog en klik op **Edit on GitHub** als u wijzigingen wilt aanbrengen. Deze worden eerst nagekeken en wanneer ze zijn goedgekeurd, worden uw wijzigingen en verbeteringen hier weergegeven.

