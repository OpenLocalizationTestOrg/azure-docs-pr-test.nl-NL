---
title: Veelgestelde vragen over RemoteApp aaaAzure | Microsoft Docs
description: Meer informatie over antwoorden toohello meest Veelgestelde vragen over Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: swadhwa
editor: 
ms.assetid: bad66603-91f9-437f-8a70-236405d2a27f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: da981fea9e38b4e74694aeaba5f97c8ed897ccd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-faq"></a>Veelgestelde vragen over Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Hallo volgende vragen over Azure RemoteApp zijn gesteld. Hebt u nog andere vragen? Ga naar Hallo [RemoteApp-forums](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureRemoteApp) en laat ons weten wat tooknow, of u een opmerking vervolgkeuzelijst hieronder.

## <a name="cant-find-what-youre-looking-for-have-a-question-we-didnt-answer"></a>Kunt u niet vinden wat u zoekt? Hebt u een vraag die we niet hebben beantwoord?
Als u niet kunt Hallo informatie vinden moet u of u een extra vraag die we je niet die betrekking hebben op hier hebt, gaat u toohello [Azure RemoteApp-forum](http://aka.ms/araforum) en stel uw vraag er. We kunnen hier altijd meer antwoorden toevoegen.

## <a name="what-is-azure-remoteapp"></a>Wat is Azure RemoteApp?
* **Wat is Azure RemoteApp?** RemoteApp is dat een Azure-service kunt u tooapplications uit een groot aantal verschillende Gebruikersapparaten veilige externe toegang. Lees meer over [Azure RemoteApp](remoteapp-whatis.md).
* **Wat zijn de implementatieopties Hallo?** Er zijn twee soorten Azure RemoteApp-verzamelingen: cloud en hybride. Welke u nodig hebt, is afhankelijk van een aantal factoren, zoals of lidmaatschap van een domein vereist is. Deze beslissingen komen [hier](remoteapp-collections.md) aan bod.

## <a name="quick-tips-on-using-azure-remoteapp"></a>Snelle tips voor het gebruik van Azure RemoteApp
* **Hoe lang duurt het tot ik geen verbinding meer heb? Hoe lang ik inactief mag zijn voordat u mij Hallo opstarten geeft?** 4 uur. Als u of een van uw gebruikers gedurende 4 uur niet actief is, wordt u automatisch afgemeld bij Azure RemoteApp. Uitchecken Hallo andere standaardinstellingen in [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md).
* **Kan ik deze service gratis uitproberen?** Ja. Er is een gratis proefversie beschikbaar voor 30 dagen. Nadat Hallo proefperiode is afgelopen, kunt u overstappen tooa betaald account (die u kunt gebruiken in productie) of met behulp van Hallo-service stoppen. Start uw gratis proefversie door te gaan[portal.azure.com](http://portal.azure.com) -Maak een nieuw exemplaar van RemoteApp. Met de gratis proefversie hello, kunt u 2 exemplaren van RemoteApp met 10 gebruikers per exemplaar te maken. Deze proefversie is echter maar 30 dagen geldig.
  
  ## <a name="azure-remoteapp-subscription-details"></a>Informatie over Azure RemoteApp-abonnement
* **Wat zijn de Servicelimieten Hallo?** U kunt meer informatie over Hallo standaardinstellingen en Servicelimieten van Azure RemoteApp in [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md). Laat het ons weten als u meer vragen hebt.
* **Hoeveel gebruikers doen er toohave?** Er is een minimum van 20 gebruikers. Ik Herhaal dat toobe wissen super - Hallo MINIMUM 20 is. U wordt gefactureerd voor 20 gebruikers. 
* **Wat kost RemoteApp?** Deze informatie vindt u in [Azure RemoteApp-prijsinformatie](https://azure.microsoft.com/pricing/details/remoteapp/).
* **Is het ene type verzameling duurder dan het andere?** Ja, dat is mogelijk, maar dat is afhankelijk van de vereisten van de verzameling. Een hybride verzameling vereist een verbinding tussen Azure RemoteApp tooyour on-premises netwerk. Als u een bestaande VNET/Expresss Route gebruikt, zijn er geen extra kosten. Maar als u een nieuwe Azure VNET en een gateway of Express Route gebruikt, wordt u gefactureerd voor Hallo [VPN-gateway](https://azure.microsoft.com/pricing/details/vpn-gateway) of [Express Route](https://azure.microsoft.com/pricing/details/expressroute/). Deze kosten (gespecificeerd in Hallo koppelingen) is boven op uw maandelijkse Azure RemoteApp kosten.

## <a name="collections---whats-supported-which-should-you-use-and-others"></a>Verzamelingen: wat er wordt ondersteund, welke u moet gebruiken en andere informatie
* **Worden aangepaste LOB-toepassingen (Line-of-business) ondersteund?** Ja. maken van een aangepaste toepassing in Azure RemoteApp toouse een [aangepaste sjablooninstallatiekopie](remoteapp-create-custom-image.md), en upload het toohello RemoteApp-collectie.
* **Werkt mijn aangepaste LOB-toepassing in Azure RemoteApp?**  Hallo van de beste manier toofigure die uit tootest deze. Bekijk Hallo [RD Compatibility Center](http://www.rdcompatibility.com/compatibility/default.aspx).
* **Welke implementatiemethode (cloud of hybride) is voor mijn organisatie het meest geschikt?** Hybride verzamelingen bieden Hallo meest uitgebreide ervaring als u volledige integratie met eenmalige aanmelding (SSO wilt) en de veilige on-premises netwerkverbinding. Cloudverzamelingen bieden een flexibele en eenvoudige manier tooisolate uw implementatie met behulp van meerdere verificatiemethoden. Lees meer over Hallo [implementatieopties](remoteapp-whatis.md).
* **We hebben een SQL- of andere database on-premises of in Azure. Welk implementatietype moeten we dan gebruiken?** Dat is afhankelijk van waar de SQL- of back-enddatabase zich bevindt. Als het Hallo-database zich in een particulier netwerk bevindt, gebruikt u Hallo hybride verzameling. Als het Hallo-database is blootgestelde toohello Internet en kan clientcomputers verbindingen tooconnect tooit, kunt u Hallo cloudverzameling gebruiken.
* **Hoe zit het met stationstoewijzing, USB- en seriële poorten, delen via het Klembord en printeromleiding?** Al deze functies worden ondersteund in Azure RemoteApp. Klembord delen en printeromleiding zijn standaard ingeschakeld. Meer informatie over omleiding vindt u [hier](remoteapp-redirection.md). 

## <a name="template-images"></a>Sjablooninstallatiekopieën
* **Kan ik gebruiken een cloud of een bestaande virtuele machine als Hallo-sjabloon voor mijn RemoteApp-collectie?** Ja. U kunt een installatiekopie op basis van een Azure VM maken, gebruikt u een Hallo installatiekopieën die zijn opgenomen in uw abonnement of een aangepaste installatiekopie maken. Bekijk Hallo [RemoteApp-installatiekopie opties](remoteapp-imageoptions.md).

## <a name="network-options"></a>Netwerkopties
* **Hallo hybride verzameling vereist een VNET. Kunnen we ons bestaande VNET gebruiken?** U kunt als hello bestaande VNET een Azure VNET. Zie ' stap 1: uw virtueel netwerk instellen ' in hello [instructies voor hybride verzamelingen](remoteapp-create-hybrid-deployment.md) voor meer informatie.
* **Kan ik een VNET gebruiken met een cloudverzameling?** Dat kunt u inderdaad. Lees [Een cloudverzameling maken](remoteapp-create-cloud-deployment.md), met name stap 1, voor meer informatie.

## <a name="authentication-options"></a>Verificatieopties
* **Hoe zit het met verificatie? Welke methoden worden ondersteund?**  hello cloudverzameling biedt ondersteuning voor Microsoft-accounts en Azure Active Directory-accounts, de Office 365-accounts. Hallo hybride verzameling ondersteunt alleen Azure Active Directory-accounts die zijn gesynchroniseerd (met behulp van een hulpprogramma zoals [Azure Active Directory-synchronisatie](http://blogs.technet.com/b/ad/archive/2014/09/16/azure-active-directory-sync-is-now-ga.aspx)) van een Windows Server Active Directory-implementatie; in het bijzonder een gesynchroniseerd met de Hallo De synchronisatieoptie wachtwoord of gesynchroniseerd met Active Directory Federation Services (AD FS) Federatie geconfigureerd. U kunt ook [Multi-Factor Authentication (MFA)](https://azure.microsoft.com/services/multi-factor-authentication/) configureren.

> [!NOTE]
> Hello Azure Active Directory-gebruikers moeten uit Hallo-tenant die gekoppeld is aan uw abonnement. (U kunt bekijken en wijzigen van uw abonnement op Hallo **instellingen** tabblad in Hallo-portal. Zie [wijziging hello Azure Active Directory-tenant die wordt gebruikt door RemoteApp](remoteapp-changetenant.md) voor meer informatie.)
> 
> 

* **Waarom worden mijn Azure Active Directory-accounttoegang kan verlenen?**  hello Azure Active Directory-gebruikers moet vanuit Hallo-map die is gekoppeld aan uw abonnement. U kunt weergeven of wijzigen van de map op Hallo instellingen tabblad in Hallo-portal. Zie [wijziging hello Azure Active Directory-tenant die wordt gebruikt door RemoteApp](remoteapp-changetenant.md) voor meer informatie.

## <a name="clients---what-device-can-i-use-tooaccess-azure-remoteapp"></a>Clients - welk apparaat heb ik tooaccess Azure RemoteApp gebruiken?
U vindt goede clientinformatie, inclusief stappen voor het installeren van andere clients op Hallo [uw apps openen in Azure RemoteApp](remoteapp-clients.md).

* **Welke apparaten en besturingssystemen Hallo clienttoepassingen ondersteunen?**
  Eerste, Hallo computers en tablets: 
  
  * Windows 10 (client-preview)
  * Windows 8.1 en Windows 8
  * Windows 7 servicepack 1
  * Mac OS X
  * Windows RT
  * Android-tablets
  * iPads

    En Hallo telefoons:
  * iPhone
  * Android-telefoons
  * Windows Phone
    
    [Download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) nu een RemoteApp-client.
* **Biedt Azure RemoteApp ondersteuning voor Thin Clients?** Ja, hello volgende Windows Embedded thin clients worden ondersteund:
  
  * Windows Embedded Standard 7
  * Windows Embedded 8 Standard
  * Windows Embedded 8.1 Industry Pro
  * Windows 10 IoT Enterprise
* **Welke versie van Windows Server wordt ondersteund voor Hallo Remote Desktop Session Host (RDSH)?** Windows Server 2012 R2.

## <a name="support-and-feedback"></a>Ondersteuning en feedback
* **Wat is Hallo ondersteuningsplan voor RemoteApp?** Ondersteuning voor factuur- en abonnementbeheer wordt gratis aangeboden. Technische ondersteuning is beschikbaar via Hallo [Azure-serviceplannen](https://azure.microsoft.com/support/plans/). U kunt ook gratis communityondersteuning krijgen via ons [Azure-discussieforum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp). 
* **Hoe geef ik feedback?** Ga naar Hallo [Feedbackforum](https://feedback.azure.com/forums/247748-azure-remoteapp/).
* **Wie kan ik meer informatie over Azure RemoteApp toolearn praten?** In aanvulling tooour [discussieforum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp), dit is een goede plaats toopost vragen, u kunt deelnemen aan Hallo wekelijks [Hallo Experts webinar vraag](https://azureinfo.microsoft.com/US-Azure-WBNR-FY15-11Nov-AzureRemoteAppAskTheExperts-Registration-Page.html), waar allerlei zaken over RemoteApp aan bod komen.
* **Is er ook RemoteApp-documentatie?** We zijn blij dat u dat vraagt. Bovendien toohello help-inhoud in de portal help-sectie Hallo (Klik daarvoor op Hallo **?** op elke pagina van de portal Hallo) zijn Hallo volgende artikelen beschikbaar tooteach u alles over RemoteApp:
  
  * **Aan de slag:**
    * [Wat is RemoteApp?](remoteapp-whatis.md)
    * [Wat is er in Hallo RemoteApp-sjablooninstallatiekopieën?](remoteapp-images.md)
    * [Hoe werkt licentieverlening?](remoteapp-licensing.md)
    * [Hoe werken RemoteApp en Office samen?](remoteapp-o365.md)
    * [How does redirection work in RemoteApp](remoteapp-redirection.md)? (Hoe werkt omleiding in RemoteApp?)
  * **Implementeren:**
    * [Een aangepaste sjablooninstallatiekopie maken](remoteapp-create-custom-image.md)
    * [Een hybride verzameling maken](remoteapp-create-hybrid-deployment.md)
    * [Een cloudverzameling maken](remoteapp-create-cloud-deployment.md)
    * [Azure Active Directory configureren voor RemoteApp](remoteapp-ad.md)
    * [Een app publiceren in RemoteApp](remoteapp-publish.md)
  * **Beheren:**
    
    * [Gebruikers toevoegen](remoteapp-user.md)
    * [Aanbevolen procedures voor het configureren en gebruiken van RemoteApp](remoteapp-bestpractices.md)    
    
    Video's We hebben ook een aantal video's over RemoteApp. Sommige geven inleidende ([inleiding tooAzure RemoteApp](https://azure.microsoft.com/documentation/videos/cloud-cover-ep-150-azure-remote-app-with-thomas-willingham-and-nihar-namjoshi/)) terwijl andere u bij de implementatie helpen ([Cloud implementatie](https://www.youtube.com/watch?v=3NAv2iwZtGc&feature=youtu.be) en [hybride implementatie](https://www.youtube.com/watch?v=GCIMxPUvg0c&feature=youtu.be)). Bekijk ze allemaal.

### <a name="help-us-help-you"></a>Help ons u te helpen
Wist u dat in de toevoeging toorating in dit artikel en het toevoegen van opmerkingen omlaag hieronder, kunt u wijzigingen toohello artikel zelf? Ontbreekt er iets? Is er iets niet juist? Heb ik iets geschreven dat niet duidelijk is? Blader omhoog en klik op **Edit on GitHub** toomake wijzigingen - deze worden eerst nagekeken toous, en vervolgens wanneer uitgeschakeld op deze, ziet u uw wijzigingen en verbeteringen hier.

