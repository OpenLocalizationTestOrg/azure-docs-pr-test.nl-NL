---
title: Inleiding tot Azure Security Center | Microsoft Docs
description: Meer informatie over Azure Security Center, de belangrijkste mogelijkheden van Azure Security Center en hoe Azure Security Center werkt.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 8951167213da6ab5341c1ca420353ec625ef5424
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-security-center"></a>Inleiding tot Azure Security Center
Meer informatie over Azure Security Center, de belangrijkste mogelijkheden van Azure Security Center en hoe Azure Security Center werkt.

> [!NOTE]
> Vanaf begin juni 2017 zal Security Center de Microsoft Monitoring Agent gebruiken voor het verzamelen en opslaan van gegevens. Zie [Migratie van Azure Security Center-platform](security-center-platform-migration.md) voor meer informatie. De informatie in dit artikel beschrijft functionaliteit van Security Center na de overstap naar de Microsoft Monitoring Agent.
>
>

## <a name="what-is-azure-security-center"></a>Wat is Azure Security Center?
 Azure Security Center helpt u bij het detecteren, voorkomen van en reageren op bedreigingen dankzij een verhoogde zichtbaarheid van en controle over de beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

## <a name="key-capabilities"></a>Belangrijkste mogelijkheden
 Security Center biedt eenvoudige en effectieve preventie en detectie van bedreigingen en reactiemogelijkheden die zijn ingebouwd in Azure. De belangrijkste mogelijkheden zijn:

| Fase | Mogelijkheid |
| --- | --- |
| Voorkomen |De beveiligingsstatus van uw Azure-resources wordt gecontroleerd |
| Voorkomen | Wordt beleid gedefinieerd voor uw Azure-abonnementen op basis van beveiligingsvereisten van uw bedrijf, de typen toepassingen die u hebt gebruikt, en de vertrouwelijkheid van uw gegevens |
| Voorkomen | Er wordt gebruikgemaakt van beveiligingsaanbevelingen van het beleid om service-eigenaren te begeleiden bij de implementatie van benodigde besturingselementen |
| Voorkomen | Beveiligingsservices en -toepassingen van Microsoft en partners worden snel geïmplementeerd |
| Detecteren |Beveiligingsgegevens van uw Azure-resources, het netwerk en partneroplossingen zoals antimalwareprogramma's en firewalls worden automatisch verzameld en geanalyseerd |
| Detecteren | Maakt gebruik van globale dreiging intelligence van Microsoft-producten en services, de Microsoft Digital Crimes Unit (DCU), de Microsoft Security Response Center (MSRC) en externe feeds |
| Detecteren | Er worden geavanceerde analyses toegepast, waaronder machine learning en gedragsanalyse |
| Reageren |Beveiligingsincidenten/-waarschuwingen worden met prioriteit geleverd |
| Reageren | Er wordt inzicht geboden in de bron van de aanval en betrokken resources |
| Reageren | Er worden manieren voorgesteld om de huidige aanval te stoppen en toekomstige aanvallen te voorkomen |

## <a name="introductory-walkthrough"></a>Introductie

> [!NOTE]
> In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie. Dit document is niet een stapsgewijze handleiding.
>
>

 Security Center is toegankelijk via [Azure Portal](https://azure.microsoft.com/features/azure-portal/). [Aanmelden bij de portal](https://portal.azure.com). Schuif onder het portal hoofdmenu naar de **Security Center** optie of Selecteer de **Security Center** tegel die u eerder aan het portaldashboard hebt vastgemaakt.

![Beveiligingstegel in Azure Portal][1]

Vanuit Security Center kunt u beveiligingsbeleid instellen, beveiligingsconfiguraties bewaken en beveiligingswaarschuwingen weergeven.

### <a name="security-policies"></a>Beveiligingsbeleid
U kunt beleid definiëren voor uw Azure-abonnementen volgens de vereisten van de beveiliging van uw bedrijf. Vervolgens kunt u het beleid aanpassen aan de typen toepassingen die u gebruikt, of de vertrouwelijkheid van de gegevens in elk abonnement. Zo kunnen er voor resources die worden gebruikt voor ontwikkeling of tests, andere beveiligingsvereisten zijn dan voor resources die worden gebruikt voor productietoepassingen. Ook kan voor toepassingen met gereglementeerde gegevens, zoals PII, een hoger beveiligingsniveau vereist zijn.

> [!NOTE]
> Als u wilt een beveiligingsbeleid wijzigen, moet u een beveiligingsbeheerder of eigenaar of bijdrager van het abonnement. Voor meer informatie over rollen en toegestane acties in Security Center, Zie [machtigingen in Azure Security Center](security-center-permissions.md).
>
>

Selecteer op de blade **Security Center** de tegel **Beleid** voor een lijst met uw abonnementen en resourcegroepen.   

![Blade Security Center][2]

Op de **beveiligingsbeleid** blade, selecteert u een abonnement om details van het beleid weer te geven.

**Gegevensverzameling** schakelt u gegevensverzameling voor een beveiligingsbeleid. Het inschakelen biedt:

* Dagelijks scannen van alle virtuele machines (VM's) ondersteund voor het bewaken van de beveiliging en aanbevelingen.
* Verzameling van beveiligingsgebeurtenissen voor analyse en detectie van bedreigingen.

> [!NOTE]
> Gegevensverzameling is geconfigureerd op het abonnementsniveau.
>
>

Selecteer **preventiebeleid** openen de **preventiebeleid** blade. **Aanbevelingen weergeven voor** kunt u ervoor kiest de beveiligingsmechanismen die u wilt bewaken en de aanbevelingen die u wilt weergeven op basis van de beveiligingsvereisten van de resources in het abonnement.

### <a name="security-recommendations"></a>Aanbevelingen voor beveiliging
 Security Center analyseert de beveiligingsstatus van uw Azure-resources om mogelijke beveiligingsproblemen op te sporen. Een lijst met aanbevelingen begeleidt u bij het configureren van benodigde besturingselementen. Voorbeelden zijn:

* Inrichting van antimalware om schadelijke software te identificeren en te verwijderen
* Netwerkbeveiligingsgroepen en regels voor het verkeer voor beheer voor virtuele machines configureren
* Inrichten van Web Application Firewalls om te beschermen tegen aanvallen die zijn gericht op uw webtoepassingen
* Implementatie van ontbrekende systeemupdates
* Aanpassing van besturingssysteemconfiguraties die niet overeenkomen met de aanbevolen basislijnen

Klik op de tegel **Aanbevelingen** voor een lijst met aanbevelingen. Klik op elke aanbeveling om extra informatie weer te geven of te doen om het probleem te verhelpen.

![Aanbevelingen voor beveiliging in Azure Security Center][5]

### <a name="security-state-of-azure-resources"></a>Beveiligingsstatus van de Azure-resources
De **preventie** gedeelte van het dashboard ziet u de algehele beveiligingsstatus van de omgeving per resourcetype, met inbegrip van virtuele machines, webtoepassingen en andere bronnen.   

Selecteer een resourcetype onder **preventie** voor meer informatie, waaronder een lijst met alle mogelijke beveiligingsproblemen die zijn geïdentificeerd. (**Compute** is geselecteerd in het onderstaande voorbeeld.)

![Tegel Status van resources][6]

### <a name="security-alerts"></a>Beveiligingswaarschuwingen
 Security Center verzamelt, analyseert en integreert automatisch logboekgegevens van uw Azure-resources, het netwerk en partneroplossingen zoals antimalwareprogramma's en firewalls. Wanneer er dreigingen worden gedetecteerd, wordt een beveiligingswaarschuwing gemaakt. Voorbeelden zijn detectie van:

* Verdachte VM's die communiceren met bekende schadelijke IP-adressen
* Geavanceerde malware die is gedetecteerd met Windows Foutrapportage
* Beveiligingsaanvallen op virtuele machines
* Beveiligingswaarschuwingen van geïntegreerde antimalwareprogramma's en firewalls

Als u op de tegel **Beveiligingswaarschuwingen** klikt, wordt een lijst waarschuwingen met prioriteit weergegeven.

![Beveiligingswaarschuwingen][7]

Als u een waarschuwing selecteert, ziet u meer informatie over de aanval en suggesties voor herstel.

![Details van beveiligingswaarschuwing][8]

### <a name="partner-solutions"></a>Partneroplossingen
De **partneroplossingen** tegel kunt u controleren in één oogopslag de beveiligingsstatus van uw partneroplossingen die zijn geïntegreerd met uw Azure-abonnement. Security Center bevat waarschuwingen die van de oplossingen afkomstig zijn.

Selecteer de tegel **Partneroplossingen**. Er wordt een blade met een lijst van alle verbonden partneroplossingen geopend.

![Partneroplossingen][9]

## <a name="get-started"></a>Aan de slag
Om te beginnen met Security Center, moet u een abonnement op Microsoft Azure. Security Center wordt met uw Azure-abonnement ingeschakeld. Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).

 Security Center is toegankelijk via [Azure Portal](https://azure.microsoft.com/features/azure-portal/). Zie de [portaldocumentatie](https://azure.microsoft.com/documentation/services/azure-portal/) voor meer informatie.

In [Aan de slag met Azure Security Center](security-center-get-started.md) leert u snel de onderdelen van Security Center voor de bewaking van de beveiliging en het beheer van het beleid kennen.

## <a name="next-steps"></a>Volgende stappen
Dit document is een inleiding tot Security Center, de belangrijkste mogelijkheden hiervan en hoe u met Security Center aan de slag gaat. Zie de volgende bronnen voor meer informatie:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) : informatie over het beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen configureren.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) : Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md): meer informatie over het bewaken van de status van uw Azure-resources.
* [Het beheren van en reageren op beveiligingswaarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) : informatie over het beheren van en reageren op beveiligingswaarschuwingen.
* [Partneroplossingen controleren met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt controleren.
- [Beveiliging van gegevens van Azure Security Center](security-center-data-security.md) -informatie over hoe gegevens worden beheerd en beveiligd in Security Center.
* [Azure Security Center FAQ](security-center-faq.md): raadpleeg veelgestelde vragen over het gebruik van de service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) — Lees het laatste nieuws van de Azure-beveiliging en de informatie.

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
