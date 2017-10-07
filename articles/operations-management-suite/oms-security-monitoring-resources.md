---
title: Bronnen voor beveiliging van Operations Management Suite en Audit oplossing aaaMonitoring | Microsoft Docs
description: Dit document helpt u toouse OMS-beveiliging en Audit mogelijkheden toomonitor uw resources en beveiligingsproblemen identificeren.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a>Bewaking van bronnen voor beveiliging van Operations Management Suite en Audit-oplossing
Dit document helpt u bij het gebruik van OMS beveiligings- en Audit mogelijkheden toomonitor uw resources en beveiligingsproblemen identificeren.

## <a name="what-is-oms"></a>Wat is OMS?
Microsoft Operations Management Suite (OMS) is van Microsoft-cloud-gebaseerde IT-beheeroplossing waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur. Lees voor meer informatie over OMS Hallo-artikel [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="monitoring-resources"></a>Bewaking van resources
Indien mogelijk is, zult u tooprevent beveiligingsincidenten gebeurt in de eerste plaats Hallo. Het is echter onmogelijk tooprevent alle beveiligingsincidenten. Wanneer een beveiligingsincident voordoet, moet u tooensure dat de gevolgen ervan wordt geminimaliseerd.  Er zijn drie essentiële aanbevelingen die gebruikt toominimize worden kunnen Hallo nummer en de invloed van beveiligingsincidenten Hallo:

* Evalueer regelmatig beveiligingslekken in uw omgeving.
* Controleer regelmatig alle computersystemen en netwerk apparaten tooensure die ze alle van de meest recente patches Hallo geïnstalleerd hebben.
* Controleer regelmatig alle logboeken en mechanismen voor logboekregistratie, met inbegrip van gebeurtenislogboeken besturingssysteem, toepassingen en inbraakdetectie detectie het systeemlogboek in Logboeken.

OMS beveiligings- en Audit oplossing kan IT tooactively bewaken van alle resources die kunnen helpen minimaliseren Hallo impact van beveiligingsincidenten. OMS beveiligings- en Audit heeft security-domeinen die kunnen worden gebruikt voor het bewaken van resources. Hallo beveiligingsdomeinen snelle toegang biedt opties voor tooa, voor beveiliging bewaking Hallo volgende domeinen worden behandeld in meer informatie:

* evaluatie van schadelijke software
* Update-evaluatie
* Identiteit en toegang

> [!NOTE]
> Lees voor een overzicht van al deze opties [aan de slag met beveiliging van Operations Management Suite-oplossing van de Audit en](oms-security-getting-started.md).
> 
> 

### <a name="monitoring-system-protection"></a>Bewaking van de systeembeveiliging
In een ingrijpende diepte benadering, elke laag van beveiliging is belangrijk voor Hallo algehele beveiligingsstatus van uw asset. Computers met gedetecteerd bedreigingen en computers met onvoldoende beveiliging worden weergegeven in Hallo evaluatie van schadelijke software tegel onder beveiligingsdomeinen. Door Hallo informatie op Hallo evaluatie van schadelijke software, kunt u een plan tooapply beveiliging toohello servers nodig identificeren. tooaccess deze optie Volg Hallo stappen hieronder:

1. In Hallo **Microsoft Operations Management Suite** hoofddashboard Klik **beveiligings- en Audit** tegel.
   
    ![Beveiliging en controle](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. In Hallo **beveiligings- en Audit** dashboard, klikt u op **Antimalware Assessment** onder **beveiligingsdomeinen**. Hallo **Antimalware Assessment** dashboard wordt weergegeven zoals hieronder wordt weergegeven:

![evaluatie van schadelijke software](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

U kunt Hallo **evaluatie van schadelijke software** dashboard tooidentify Hallo beveiligingsproblemen te volgen:

* **Actieve bedreigingen**: computers die in verkeerde handen en actieve bedreigingen in Hallo systeem hebben.
* **Bedreigingen hersteld**: computers die zijn aangetast maar Hallo bedreigingen zijn hersteld.
* **Handtekening is verouderd**: computers waarvoor bescherming tegen schadelijke software is ingeschakeld maar Hallo handtekening is verouderd.
* **Er is geen real-timebeveiliging**: computers die geen antimalware geïnstalleerd hebben.

### <a name="monitoring-updates"></a>updates controleren
Toepassen van de meest recente beveiligingsupdates Hallo is een best practice bij beveiliging en deze moet worden opgenomen in de beheerstrategie voor update. Microsoft Monitoring Agent-service (HealthService.exe) inleest update van bewaakte computers en stuurt vervolgens deze bijgewerkte informatie toohello OMS-service in de cloud Hallo voor verwerking. Hallo Microsoft Monitoring Agent-service is geconfigureerd als een automatische-service en deze altijd in Hallo doelcomputer moet worden uitgevoerd.

![updates controleren](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

Logica is toegepaste toohello-gegevens voor de update en Hallo cloudservice registreert Hallo-gegevens. Als ontbrekende updates worden gevonden, worden weergegeven op Hallo **Updates** dashboard. Kunt u Hallo **Updates** dashboard toowork met ontbrekende updates en ontwikkelen van een plan tooapply ze toohello-servers die ze nodig hebt. Hallo stappen hieronder tooaccess hello **Updates** dashboard:

1. In Hallo **Microsoft Operations Management Suite** hoofddashboard Klik **beveiligings- en Audit** tegel.
2. In Hallo **beveiligings- en Audit** dashboard, klikt u op **Update-evaluatie** onder **beveiligingsdomeinen**. Hallo Update dashboard wordt weergegeven zoals hieronder wordt weergegeven:

![Update-evaluatie](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

In dit dashboard kunt u een update assessment toounderstand Hallo huidige status van uw computers en het adres Hallo meest kritieke bedreigingen uitvoeren. Met behulp van Hallo **essentiële of beveiligingsupdates** tegel, IT-beheerders zijn kunnen tooaccess gedetailleerde informatie over het Hallo-updates die ontbreken zoals hieronder wordt weergegeven:

![zoekresultaat](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

Dit rapport bevatten belangrijke informatie die kan worden gebruikt tooidentify Hallo type bedreiging dit systeem is kwetsbaar voor, waaronder Hallo Microsoft KB-artikelen die zijn gekoppeld aan het Hallo-beveiligingsupdate en MS-Bulletin met meer details over Hallo Hallo beveiligingsprobleem.

### <a name="monitoring-identity-and-access"></a>Bewaking van identiteits- en toegangsbeheer
Met gebruikers die overal werken met behulp van verschillende apparaten en toegang tot een enorme hoeveelheid cloud en on-premises apps, is het noodzakelijk dat hun referenties worden beveiligd. Credential theft aanvallen zijn waarbij een aanvaller in eerste instantie toegang tot tooa reguliere van de gebruiker referenties tooaccess een systeem in Hallo-netwerk krijgt. In veel gevallen deze initiële aanval is alleen een manier tooget toegang toohello-netwerk, Hallo einddoel is toodiscover bevoegdheid accounts. 

Aanvallers blijft in Hallo-netwerk met behulp van gratis tooling tooextract referenties van Hallo sessies van andere accounts is aangemeld. Afhankelijk van de systeemconfiguratie hello, kunnen deze referenties worden geëxtraheerd in Hallo vorm van hashes, tickets of zelfs ongecodeerde wachtwoorden.  

> [!NOTE]
> computers die rechtstreeks zijn blootgesteld toohello die Internet ziet veel mislukt probeert die probeer toologin met alle soorten bekende gebruikersnamen (bijvoorbeeld Administrator). In de meeste gevallen is het OK als Hallo bekende gebruikersnamen niet worden gebruikt en als Hallo wachtwoord sterk genoeg is.
> 
> 

Het is mogelijk tooidentify voordat ze een account met bevoegdheden inbreuk deze indringers. U kunt gebruikmaken van **OMS beveiligings- en Audit oplossing** toomonitor identiteits- en toegangsbeheer. Hallo stappen hieronder tooaccess hello **identiteits- en toegangsbeheer** dashboard:

1. In Hallo **Microsoft Operations Management Suite** hoofddashboard klikt u op beveiliging en Audit tegel.
2. In Hallo **beveiligings- en Audit** dashboard, klikt u op **identiteits- en toegangsbeheer** onder **beveiligingsdomeinen**. Hallo **identiteits- en toegangsbeheer** dashboard wordt weergegeven zoals hieronder wordt weergegeven:

![identiteit en toegang](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

Als onderdeel van uw strategie voor regelmatige controle, moet u de bewaking van de identiteit opnemen. IT-beheerder moet eruitzien als er een specifieke geldige gebruikersnaam met veel pogingen. Dit kan erop wijzen dat een aanvaller die Hallo echte gebruikersnaam verkregen en probeer het toobrute geweld of een automatische hulpprogramma dat gebruikmaakt van vastgelegde wachtwoord verlopen.

Dit dashboard inschakelen IT tooquickly identificeren mogelijke bedreigingen gerelateerde tooidentity en toegang toocompany van resources. Is bijzonder belangrijk tooalso potentiële trends herkennen, bijvoorbeeld in tegel Hallo aanmeldingen gedurende een periode, kunt u zien over tijdsperiode hoe vaak een mislukte aanmeldingspoging is uitgevoerd. In dit geval Hallo computer **bestandsserver** 35 aanmeldingspogingen ontvangen. U vindt meer informatie over deze computer door erop te klikken. 

![meer informatie](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

Hallo-rapport gegenereerd voor deze computer brengt waardevolle informatie over dit patroon. Opgemerkt dat Hallo **ACCOUNT** kolom geeft u het gebruikersaccount dat gebruikt tootry tooaccess is Hallo Hallo systeem hello **TIMEGENERATED** kolom biedt u Hallo tijdsinterval in welke Hallo poging is gedaan en Hallo **LOGONTYPENAME** kolom biedt Hallo van locatie waar deze poging is gedaan. Als deze pogingen zijn lokaal in Hallo systeem uitgevoerd door een programma, Hallo **proces** kolom Hallo procesnaam zou worden weergegeven. U hebt al Hallo procesnaam beschikbaar in scenario's waarbij Hallo aanmeldingspoging afkomstig is van een programma, en nu u kunt verder onderzoek verrichten in het doelsysteem Hallo.

## <a name="see-also"></a>Zie ook
In dit document, u leert hoe toouse OMS beveiligings- en Audit oplossing toomonitor uw resources. toolearn meer informatie over OMS-beveiliging, Zie Hallo artikelen te volgen:

* [Overzicht van Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Aan de slag met beveiliging van Operations Management Suite en Audit-oplossing](oms-security-getting-started.md)
* [Bewaking en reageren tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit-oplossing](oms-security-responding-alerts.md)

