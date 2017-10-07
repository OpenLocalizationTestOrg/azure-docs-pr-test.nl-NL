---
title: aaaMonitoring en reageert tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit oplossing | Microsoft Docs
description: Dit document helpt u toouse Hallo threat intelligence optie beschikbaar in de OMS-beveiligings- en Audit toomonitor en toosecurity waarschuwingen reageren.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a>Bewaking en waarschuwingen in de beveiliging van Operations Management Suite en Audit oplossing toosecurity reageert
Dit document helpt u Hallo threat intelligence optie beschikbaar in de OMS-beveiligings- en Audit toomonitor gebruiken en waarschuwingen toosecurity reageren.

## <a name="what-is-oms"></a>Wat is OMS?
Microsoft Operations Management Suite (OMS) is van Microsoft-cloud-gebaseerde IT-beheeroplossing waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur. Lees voor meer informatie over OMS Hallo-artikel [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="threat-intelligence"></a>Informatie over bedreigingen
In een bedrijfsomgeving waar gebruikers ruime toegang toohello netwerk hebt en een verscheidenheid aan apparaten tooconnect toocorporate gegevens gebruiken, is het noodzakelijk actief uw resources bewaken en snel reageren toosecurity incidenten. Dit is name belangrijk vanuit Hallo beveiliging lifecycle perspectief omdat sommige cybersecurity bedreigingen kunnen niet verhogen waarschuwingen of verdachte activiteiten die kunnen worden geïdentificeerd door technische traditionele beveiligingsmechanismen. 

Met behulp van Hallo **dreigingen** optie beschikbaar in de OMS-beveiliging en controle, IT-beheerders kunnen identificeren bedreigingen van Hallo-omgeving, bijvoorbeeld, identificeren als een bepaalde computer deel uitmaakt van een [ botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection). Computers kunnen knooppunten in een botnet worden wanneer aanvallers vastlegt kwaadaardige software die heimelijk deze computer toohello opdracht en controle verbindt moet worden geïnstalleerd. Mogelijke bedreigingen die afkomstig zijn van ondergrondse communicatiekanalen, zoals kan ook worden aangegeven [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents). 

In volgorde toobuild gebruiken deze dreigingen OMS beveiligings- en Audit gegevens die afkomstig zijn uit meerdere bronnen binnen Microsoft. OMS beveiligings- en Audit zal gebruikmaken van deze gegevens tooidentify van mogelijke bedreigingen van uw omgeving.

Hallo dreigingen deelvenster bestaat door drie belangrijke opties:

* Servers met uitgaand schadelijk verkeer
* Typen gedetecteerde bedreigingen
* Bedreigingsinformatiekaart

> [!NOTE]
> Lees voor een overzicht van al deze opties [aan de slag met beveiliging van Operations Management Suite-oplossing van de Audit en](oms-security-getting-started.md).
> 
> 

### <a name="responding-toosecurity-alerts"></a>Reageert toosecurity waarschuwingen
Een van de stappen Hallo van een [beveiliging respons op incidenten](https://technet.microsoft.com/library/cc512623.aspx) proces tooidentify Hallo ernst van systemen dat Hallo inbreuk is. In deze fase moet u Hallo volgende taken uitvoeren:

* Hallo aard van de aanval Hallo bepalen
* Hallo aanvallen met zich mee van oorsprong bepalen
* Hallo bedoeling van Hallo aanval bepalen. Hallo-aanval die specifiek zijn gericht op een specifieke gegevens van de organisatie-tooacquire is of is willekeurige?
* Hallo systemen identificeren waarvoor is geknoeid
* Hallo-bestanden die zijn geopend en bepalen Hallo gevoeligheid van die bestanden identificeren

U kunt gebruikmaken van **dreigingen** informatie in de OMS-beveiligings- en Audit oplossing toohelp met deze taken. Voert u stappen hieronder tooaccess hello **dreigingen** opties:

1. In Hallo **Microsoft Operations Management Suite** hoofddashboard Klik **beveiligings- en Audit** tegel.
   
    ![Beveiliging en controle](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. In Hallo **beveiligings- en Audit** dashboard ziet u Hallo **dreigingen** opties in Hallo rechts, zoals hieronder wordt weergegeven:
   
    ![Threat intel](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

Deze drie tegels krijgt u een overzicht van de huidige bedreigingen Hallo. In Hallo **Server met uitgaand schadelijk verkeer** kunt u zich kunt tooidentify als er een computer die u controleren is wilt (binnen of buiten uw netwerk) die verzenden schadelijk verkeer toohello Internet. 

Hallo **gedetecteerd threat typen** tegel geeft een samenvatting weer van bedreigingen voor actueel 'in Hallo wilde"Hallo, als u op deze tegel klikt ziet u meer informatie over deze bedreigingen zoals u hierna ziet:

![Gedetecteerde bedreigingstypen](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

U kunt meer informatie over elke bedreiging uitpakken door erop te klikken. Hallo in het volgende voorbeeld ziet u meer informatie over Botnet:

![meer informatie over een bedreiging](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

Zoals beschreven in het begin van deze sectie hello, kan deze informatie nuttig zijn bij een aanvraag voor respons op incidenten. Het kan ook worden belangrijke tijdens een forensisch onderzoek hier moet u toofind Hallo bron Hallo aanval, welk systeem is geknoeid en Hallo tijdlijn. In dit rapport dat u enkele belangrijke details over Hallo-aanval zoals eenvoudig kunt herkennen: Hallo bron van de aanval hello, Hallo lokale IP waarmee is geknoeid en status van de huidige sessie van verbinding Hallo Hallo. 

Hallo **threat intelligence kaart** helpt u tooidentify Hallo huidige locaties hele Hallo wereld waarvoor schadelijk verkeer. Er zijn oranje (inkomend) en rood (uitgaand) pijlen in deze kaart die Hallo verkeer richting, identificeren als u in een van deze pijlen klikt, wordt het weergegeven Hallo type dreiging en Hallo verkeer richting zoals hieronder wordt weergegeven:

![kaart met gegevens van bedreigingen](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> Ziet u een demonstratie over het toouse deze mogelijkheid tijdens een respons op incidenten proces door bekijkt hello presentatie [datacenter beveiligingsrisico's verhelpen met begeleide onderzoek met Operations Management Suite](https://myignite.microsoft.com/videos/5000) geleverd bij Microsoft Ignite.
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a>Reageert toodistinct schadelijke IP geopend
In sommige scenario's ziet u mogelijk een potentieel schadelijke IP-adres dat is geopend vanaf een bewaakte computer:

![kaart met gegevens van bedreigingen](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Deze waarschuwing en anderen binnen dezelfde categorie Hallo, via de OMS-beveiliging worden gegenereerd door gebruik te [Microsoft dreigingen](https://youtu.be/O4WtxgUrDc8). Hallo dreigingen gegevens is verzameld door Microsoft evenals van toonaangevende leveranciers van threat intelligence aangeschaft. Deze gegevens vaak wordt bijgewerkt en aangepast bedreigingen toofast verplaatsen. Vanwege de aard van tooits, moet deze worden gecombineerd met andere bronnen van beveiligingsgegevens tijdens [onderzoeken](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) een beveiligingswaarschuwing. 

## <a name="customize-alerts-received-via-e-mail"></a>Meldingen ontvangen per e-mail aanpassen

U kunt aanpassen welke gebruikers in uw organisatie wordt gewaarschuwd wanneer er beveiligingswaarschuwingen worden geactiveerd door OMS-beveiliging. Deze optie is beschikbaar onder overzicht / instellingen bij Hallo OMS dashboard:

![E-mail](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a>Zie ook
In dit document, u leert hoe toouse hello **dreigingen** optie in OMS beveiligings- en Audit oplossing toorespond toosecurity waarschuwingen. toolearn meer informatie over OMS-beveiliging, Zie Hallo artikelen te volgen:

* [Overzicht van Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Aan de slag met beveiliging van Operations Management Suite en Audit-oplossing](oms-security-getting-started.md)
* [Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite ](oms-security-monitoring-resources.md)

