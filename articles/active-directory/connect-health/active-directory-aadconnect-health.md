---
title: aaaMonitor uw on-premises identity-infrastructuur in Hallo cloud.
description: Dit is hello Azure AD Connect Health-pagina waarop wordt beschreven wat en waarom u het kunt gebruiken.
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 82798ea6-5cd3-4f30-93ae-d56536f8d8e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 84d0b00ec800ba98094343731aa4e7317dfb0c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-on-premises-identity-infrastructure-and-synchronization-services-in-hello-cloud"></a>Controleer uw lokale identiteit infrastructuur- en synchronisatieregels services in de cloud Hallo
Azure Active Directory (Azure AD) Connect Health helpt u bij het controleren en inzicht in uw on-premises identiteits-infrastructuur en Hallo Synchronisatieservices. Hiermee kunt u toomaintain een betrouwbare verbinding tooOffice 365 en Microsoft Online Services door controlemogelijkheden te bieden voor uw belangrijkste identiteitsonderdelen, zoals Active Directory Federation Services (AD FS)-servers, Azure AD Connect-servers (ook bekend Als de synchronisatie-Engine), Active Directory-domeincontrollers, enzovoort. Ook kan Hallo belangrijkste gegevenspunten over deze componenten gemakkelijk toegankelijk is zodat u gebruik kunt ophalen en andere belangrijke insights toomake geïnformeerd beslissingen te nemen.

Hallo-informatie is opgenomen in het Hallo [portal Azure AD Connect Health](https://aka.ms/aadconnecthealth). U kunt waarschuwingen, bewaking van toepassingsprestaties gebruiksanalyse en andere informatie weergeven in hello Azure AD Connect Health-portal. Azure AD Connect Health kunt Hallo identiteitsonderdelen over de status van uw belangrijkste identiteitsonderdelen op één plek.

![Wat is Azure AD Connect Health?](./media/active-directory-aadconnect-health/aadconnecthealth2.png)

Hallo-functies in Azure AD Connect Health verhogen, zorgt Hallo portal voor één dashboard via Hallo gaat om identiteiten. Krijgt u een meer robuuste, in orde en geïntegreerde omgeving voor uw gebruikers tooincrease hun mogelijkheid tooget dingen doen.

## <a name="why-use-azure-ad-connect-health"></a>Waarom het handig is om Azure AD Connect Health te gebruiken
Wanneer u uw on-premises directory's met Azure AD integreert, zijn uw gebruikers productiever omdat er een algemene identiteit tooaccess zowel cloud en on-premises-resources. Deze integratie maakt echter Hallo uitdaging om ervoor te zorgen dat deze omgeving in orde is, zodat gebruikers op betrouwbare wijze toegang bronnen tot, zowel on-premises als in Hallo cloud vanaf elk apparaat. Azure AD Connect Health helpt u bij het controleren en inzicht in uw on-premises identity-infrastructuur die gebruikte tooaccess Office 365 of andere Azure AD-toepassingen. Het is net zo eenvoudig als het installeren van een agent op een van uw on-premises identiteitsservers.

## <a name="azure-ad-connect-health-for-ad-fsactive-directory-aadconnect-health-adfsmd"></a>[Azure AD Connect Health voor AD FS](active-directory-aadconnect-health-adfs.md)
Azure AD Connect Health voor AD FS biedt ondersteuning voor AD FS 2.0 in Windows Server 2008 R2, Windows Server 2012 en Windows Server 2012 R2. Het ondersteunt ook bewaking Hallo AD FS-proxy of webtoepassingsproxyservers die verificatie bieden ondersteuning voor toegang tot het extranet. Azure AD Connect Health voor AD FS biedt een eenvoudige en voordelige installatie Hallo Health Agent zonder Hallo volgende set kernfuncties:

* Controle met waarschuwingen tooknow wanneer AD FS en AD FS-proxyservers zich niet in orde
* E-mailmeldingen voor kritieke waarschuwingen
* Trends wat betreft prestatiegegevens, wat nuttig is voor de capaciteitsplanning van AD FS
* Gebruiksanalyse voor AD FS aanmeldingen met gegevensfuncties (apps, gebruikers, netwerklocatie, enzovoort), die nuttig toounderstand hoe AD FS wordt gebruikt
* Rapporten voor AD FS, zoals 50 belangrijkste gebruikers die aanmeldingspogingen ondernemen met een ongeldige gebruikersnaam/ongeldig wachtwoord, met het laatste IP-adres

Hallo biedt volgende video een overzicht van Azure AD Connect Health voor AD FS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health--Monitor-you-identity-bridge/player]
>
>

## <a name="azure-ad-connect-health-for-syncactive-directory-aadconnect-health-syncmd"></a>[Azure AD Connect Health for Sync](active-directory-aadconnect-health-sync.md)
Azure AD Connect Health voor synchroniseren bewaakt en bevat informatie over Hallo synchronisaties die worden uitgevoerd tussen uw lokale Active Directory en Azure AD. Azure AD Connect Health voor synchroniseren biedt Hallo volgende set kernfuncties:

* Bewaking met tooknow waarschuwingen wanneer een Azure AD Connect-server, is ook wel bekend als Hallo synchronisatie-Engine niet in orde
* E-mailmeldingen voor kritieke waarschuwingen
* Operationele synchronisatie-inzichten, inclusief latentiegrafieken voor synchronisatiebewerkingen en trends in verschillende bewerkingen zoals toevoegingen, updates en verwijderingen
* Snelle weergave informatie over synchronisatie-eigenschappen en de laatste geslaagde tooAzure AD exporteren
* Voor rapporten over synchronisatiefouten op objectniveau \(is Azure AD Premium niet vereist\)

Hallo biedt volgende video een overzicht van Azure AD Connect Health voor synchroniseren.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Health-Monitoring-the-sync-engine/player]
>
>

## <a name="azure-ad-connect-health-for-ad-dsactive-directory-aadconnect-health-addsmd"></a>[Azure AD Connect Health voor AD DS](active-directory-aadconnect-health-adds.md)
Azure AD Connect Health voor Active Directory Domain Services biedt bewaking voor domeincontrollers die zijn geïnstalleerd in Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 en Windows Server 2016. Hallo Health Agent-installatie kunt u toomonitor uw on-premises AD DS-omgeving van Hallo cloud. Azure AD Connect Health voor AD DS biedt Hallo volgende set kernfuncties:

* Bewaking van waarschuwingen toodetect wanneer domeincontrollers niet in orde worden en e-mailmeldingen voor kritieke waarschuwingen
* Hallo-domeincontrollers dashboard, dat een overzicht van Hallo health en operationele status van uw domeincontrollers biedt
* Hallo replicatiestatus dashboard die de meest recente replicatiegegevens Hallo en koppelingen tootroubleshooting handleidingen wanneer er fouten zijn gedetecteerd
* Snel toegang vanaf elke locatie tooperformance gegevens grafieken van populaire prestatiemeteritems die nodig zijn voor het oplossen van problemen en monitoring

Hallo biedt volgende video een overzicht van Azure AD Connect Health voor AD DS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health-monitors-on-premises-AD-Domain-Services/player]
>
>

## <a name="get-started-with-azure-ad-connect-health"></a>Aan de slag met Azure AD Connect Health
tooget de slag met Azure AD Connect Health, gebruik Hallo stappen te volgen:

1. [Installeer Azure AD Premium](../active-directory-get-started-premium.md) of [gebruik een proefversie](https://azure.microsoft.com/trial/get-started-active-directory/).
2. [Download en installeer Azure AD Connect Health-agents](#download-and-install-azure-ad-connect-health-agent) op uw servers voor identiteiten.
3. Weergave hello Azure AD Connect Health-dashboard [https://aka.ms/aadconnecthealth](https://aka.ms/aadconnecthealth).

> [!NOTE]
> Houd er rekening mee dat voordat u gegevens in uw Azure AD Connect Health dashboard ziet, u tooinstall hello Azure AD Connect Health-Agents op uw doelservers moet.
>
>

## <a name="download-and-install-azure-ad-connect-health-agent"></a>De Azure AD Connect Health-agent downloaden en installeren
* Zorg ervoor dat u [voldoen aan de eisen Hallo](active-directory-aadconnect-health-agent-install.md#requirements) voor Azure AD Connect Health.
* Aan de slag met Azure AD Connect Health voor AD FS
    * [Download de Azure AD Connect Health-agent voor AD FS.](http://go.microsoft.com/fwlink/?LinkID=518973)
    * [Zie de installatie-instructies Hallo](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs).
* Aan de slag met Azure AD Connect Health for Sync
    * [Download en installeer de nieuwste versie van Azure AD Connect Hallo](http://go.microsoft.com/fwlink/?linkid=615771). Hallo Health-Agent voor synchronisatie wordt geïnstalleerd als onderdeel van hello Azure AD Connect-installatie (versie 1.0.9125.0 of hoger).
* Aan de slag met Azure AD Connect Health voor AD DS
    * [Download de Azure AD Connect Health-agent voor AD DS](http://go.microsoft.com/fwlink/?LinkID=820540).
    * [Zie de installatie-instructies Hallo](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-ds).

## <a name="azure-ad-connect-health-portal"></a>Portal voor Azure AD Connect Health
Hello Azure AD Connect Health portal bevat weergaven van waarschuwingen, bewaking van de prestaties en gebruik analyseren. Hallo https://aka.ms/aadconnecthealth URL gaat u toohello hoofdblade van Azure AD Connect Health. Een blade kunt u zien als een venster. Op de hoofdblade hello, ziet u **Quick Start**, services in Azure AD Connect Health en extra configuratie-opties. Zie Hallo na de schermopname en korte beschrijvingen die Hallo schermafbeelding volgen. Nadat u Hallo agents hebt geïmplementeerd, identificeert Hallo health-service automatisch Hallo-services die Azure AD Connect Health worden gecontroleerd.

> [!NOTE]
> Zie voor informatie over licenties, Hallo [Azure AD Connect Veelgestelde vragen over](active-directory-aadconnect-health-faq.md) of Hallo [prijzen van Azure AD-pagina](https://aka.ms/aadpricing).
    
![Portal voor Azure AD Connect Health](./media/active-directory-aadconnect-health/portal4.png)

* **Snel starten**: wanneer u deze optie selecteert, Hallo **Quick Start** blade wordt geopend. U kunt hello Azure AD Connect Health-Agent downloaden door het selecteren van **ophalen extra**. U kunt ook documentatie bekijken en feedback geven.
* **Active Directory Federation Services**: deze optie geeft alle Hallo AD FS-services momenteel bewaking van Azure AD Connect Health. Wanneer u een exemplaar selecteert, geeft Hallo-blade die wordt geopend informatie over deze service-exemplaar. Deze informatie omvat een overzicht, eigenschappen, waarschuwingen, controle en gebruiksanalyses. Meer informatie over mogelijkheden Hallo [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).
* **Azure Active Directory Connect (Sync)**: deze optie verwijst u naar de Azure AD Connect-servers die momenteel door Azure AD Connect Health worden bewaakt. Wanneer u Hallo item selecteert, geeft Hallo-blade die wordt geopend informatie over uw Azure AD Connect-servers. Meer informatie over mogelijkheden Hallo [Using Azure AD Connect Health voor synchroniseren](active-directory-aadconnect-health-sync.md).
* **Active Directory Domain Services**: deze optie geeft alle Hallo AD DS-forests momenteel bewaking van Azure AD Connect Health. Wanneer u een forest selecteert, geeft Hallo-blade die wordt geopend informatie over dat forest. Deze informatie bevat een overzicht van essentiële informatie, Hallo domeincontrollers dashboard Hallo replicatiestatus dashboard, waarschuwingen en bewaking. Meer informatie over mogelijkheden Hallo [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).
* **Configureer**: in deze sectie bevat opties tooturn Hallo volgende in- of uitschakelen:

  - Automatische updates tooautomatically hello Azure AD Connect Health agent toohello meest recente updateversie: U wordt automatisch bijgewerkt toohello nieuwste versies van hello Azure AD Connect Health-Agent zijn wanneer deze beschikbaar. Deze optie is standaard ingeschakeld.
  - Microsoft access tooyour Azure AD-map van de gezondheid van gegevens voor het oplossen van problemen alleen toestaan: als deze optie is ingeschakeld, Microsoft ziet Hallo dezelfde gegevens die u ziet. Dit kan handig zijn bij het oplossen van problemen en het verlenen van hulp. Deze optie is standaard uitgeschakeld.

## <a name="related-links"></a>Verwante koppelingen
* [De Azure AD Connect Health-agent installeren](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health-bewerkingen](active-directory-aadconnect-health-operations.md)
* [Azure AD Connect Health gebruiken met AD FS](active-directory-aadconnect-health-adfs.md)
* [Azure AD Connect Health for Sync gebruiken](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health gebruiken met AD DS](active-directory-aadconnect-health-adds.md)
* [Veelgestelde vragen over Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Versiegeschiedenis van Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
