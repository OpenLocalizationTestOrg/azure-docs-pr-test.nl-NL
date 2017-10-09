---
title: aaaIntroduction tooAzure Security Center | Microsoft Docs
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
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a>Inleiding tooAzure Security Center
Meer informatie over Azure Security Center, de belangrijkste mogelijkheden van Azure Security Center en hoe Azure Security Center werkt.

> [!NOTE]
> Begin juni 2017 vanaf kan Security Center Hallo Microsoft Monitoring Agent toocollect gebruiken en opslaan van gegevens. Zie [Azure Security Center-Platform migratie](security-center-platform-migration.md) toolearn meer. Hallo-informatie in dit artikel beschrijft Security Center functionaliteit na de overgang toohello Microsoft Monitoring Agent.
>
>

## <a name="what-is-azure-security-center"></a>Wat is Azure Security Center?
 Security Center helpt u bij het detecteren, voorkomen van en reageren toothreats met verhoogde zichtbaarheid van en controle over Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

## <a name="key-capabilities"></a>Belangrijkste mogelijkheden
 Security Center biedt eenvoudig te gebruiken en effectieve bedreiging mogelijkheden voor preventie, detectie en reactie die zijn ingebouwd in tooAzure. De belangrijkste mogelijkheden zijn:

| Fase | Mogelijkheid |
| --- | --- |
| Voorkomen |Monitors Hallo beveiligingsstatus van uw Azure-resources |
| Voorkomen | Beleidsregels voor uw Azure-abonnementen op basis van de beveiligingsvereisten van uw bedrijf, Hallo soorten toepassingen gebruiken en de vertrouwelijkheid van uw gegevens Hallo definieert |
| Voorkomen | Maakt gebruik van beleid gebaseerde beveiliging aanbevelingen tooguide service-eigenaars via Hallo proces van implementatie van benodigde besturingselementen |
| Voorkomen | Beveiligingsservices en -toepassingen van Microsoft en partners worden snel geïmplementeerd |
| Detecteren |Automatisch verzameld en analyseert beveiligingsgegevens van uw Azure-resources, het Hallo-netwerk en partneroplossingen zoals antimalwareprogramma's en firewalls |
| Detecteren | Maakt gebruik van globale dreiging intelligence van Microsoft-producten en services, Microsoft Digital Crimes Unit (DCU), Hallo Hallo Microsoft Security Response Center (MSRC) en externe feeds |
| Detecteren | Er worden geavanceerde analyses toegepast, waaronder machine learning en gedragsanalyse |
| Reageren |Beveiligingsincidenten/-waarschuwingen worden met prioriteit geleverd |
| Reageren | Inzicht geboden in Hallo bron van het Hallo-aanval en betrokken resources |
| Reageren | Bevat informatie over toostop Hallo huidige aanval en toekomstige aanvallen te voorkomen |

## <a name="introductory-walkthrough"></a>Introductie

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie. Dit document is niet een stapsgewijze handleiding.
>
>

 Security Center is toegankelijk vanuit Hallo [Azure-portal](https://azure.microsoft.com/features/azure-portal/). [Meld u aan de portal toohello](https://portal.azure.com). Schuif onder Hallo portal hoofdmenu toohello **Security Center** optie of selecteer Hallo **Security Center** tegel dat u eerder toohello portaldashboard hebt vastgemaakt.

![Beveiligingstegel in Azure Portal][1]

Vanuit Security Center kunt u beveiligingsbeleid instellen, beveiligingsconfiguraties bewaken en beveiligingswaarschuwingen weergeven.

### <a name="security-policies"></a>Beveiligingsbeleid
U kunt beleid voor uw Azure-abonnementen op basis van de beveiligingsvereisten van het bedrijf tooyour definiëren. U kunt ook het beleid aanpassen toohello typen toepassingen die u gebruikt of toohello vertrouwelijkheid van Hallo gegevens in elk abonnement. Zo kunnen er voor resources die worden gebruikt voor ontwikkeling of tests, andere beveiligingsvereisten zijn dan voor resources die worden gebruikt voor productietoepassingen. Ook kan voor toepassingen met gereglementeerde gegevens, zoals PII, een hoger beveiligingsniveau vereist zijn.

> [!NOTE]
> toomodify een beveiligingsbeleid, moet u een abonnement beveiligingsbeheerder of Hallo eigenaar of bijdrager zijn. Zie toolearn meer informatie over de functies en de toegestane acties in Security Center [machtigingen in Azure Security Center](security-center-permissions.md).
>
>

Op Hallo **Security Center** blade, selecteer Hallo **beleid** tegel voor een lijst met uw abonnementen en resourcegroepen.   

![Blade Security Center][2]

Op Hallo **beveiligingsbeleid** blade, selecteert u een abonnement tooview Hallo beleidsdetails.

**Gegevensverzameling** schakelt u gegevensverzameling voor een beveiligingsbeleid. Het inschakelen biedt:

* Dagelijks scannen van alle virtuele machines (VM's) ondersteund voor het bewaken van de beveiliging en aanbevelingen.
* Verzameling van beveiligingsgebeurtenissen voor analyse en detectie van bedreigingen.

> [!NOTE]
> Gegevensverzameling is geconfigureerd op abonnementsniveau Hallo.
>
>

Selecteer **preventiebeleid** tooopen hello **preventiebeleid** blade. **Aanbevelingen weergeven voor** kunt u kiezen Hallo beveiligingsmechanismen die u wilt dat toomonitor en Hallo aanbevelingen die u toosee op basis van Hallo beveiligingsbehoeften van Hallo resources binnen Hallo-abonnement wilt.

### <a name="security-recommendations"></a>Aanbevelingen voor beveiliging
 Security Center analyseert de beveiligingsstatus Hallo van uw Azure-resources tooidentify mogelijke beveiligingsproblemen. Een lijst met aanbevelingen begeleidt u bij het Hallo-proces voor het configureren van benodigde besturingselementen. Voorbeelden zijn:

* Inrichting van antimalware toohelp identificeren en verwijderen van schadelijke software
* Network security groepen en regels toocontrol tooVMs verkeer configureren
* Inrichting van web application firewalls toohelp beschermen tegen aanvallen die zijn gericht op uw webtoepassingen
* Implementatie van ontbrekende systeemupdates
* Aanpassing van besturingssysteemconfiguraties die niet overeenkomen met de Hallo aanbevolen basislijnen

Klik op Hallo **aanbevelingen** tegel voor een lijst met aanbevelingen. Klik op elke aanbeveling tooview aanvullende informatie of tootake actie tooresolve Hallo probleem.

![Aanbevelingen voor beveiliging in Azure Security Center][5]

### <a name="security-state-of-azure-resources"></a>Beveiligingsstatus van de Azure-resources
Hallo **preventie** sectie van Hallo dashboard toont Hallo algehele beveiligingsstatus van Hallo omgeving per resourcetype, met inbegrip van virtuele machines, webtoepassingen en andere bronnen.   

Selecteer een resourcetype onder **preventie** tooview meer informatie, waaronder een lijst met alle mogelijke beveiligingsproblemen die zijn geïdentificeerd. (**Compute** is geselecteerd in Hallo in het volgende voorbeeld.)

![Tegel Status van resources][6]

### <a name="security-alerts"></a>Beveiligingswaarschuwingen
 Security Center automatisch verzamelt, analyseert en integreert logboekgegevens van uw Azure-resources, het Hallo-netwerk en partneroplossingen zoals antimalwareprogramma's en firewalls. Wanneer er dreigingen worden gedetecteerd, wordt een beveiligingswaarschuwing gemaakt. Voorbeelden zijn detectie van:

* Verdachte VM's die communiceren met bekende schadelijke IP-adressen
* Geavanceerde malware die is gedetecteerd met Windows Foutrapportage
* Beveiligingsaanvallen op virtuele machines
* Beveiligingswaarschuwingen van geïntegreerde antimalwareprogramma's en firewalls

Te klikken op Hallo **beveiligingswaarschuwingen** tegel geeft een lijst met waarschuwingen van prioriteit.

![Beveiligingswaarschuwingen][7]

Meer informatie over het Hallo-aanval en suggesties voor het selecteren van een waarschuwing bevat tooremediate deze.

![Details van beveiligingswaarschuwing][8]

### <a name="partner-solutions"></a>Partneroplossingen
Hallo **partneroplossingen** tegel kunt u in een oogopslag Hallo beveiligingsstatus van uw partneroplossingen bewaken die zijn geïntegreerd met uw Azure-abonnement. Security Center bevat waarschuwingen die afkomstig zijn van het Hallo-oplossingen.

Selecteer Hallo **partneroplossingen** tegel. Er wordt een blade met een lijst van alle verbonden partneroplossingen geopend.

![Partneroplossingen][9]

## <a name="get-started"></a>Aan de slag
tooget gestart met Security Center, moet u een abonnement tooMicrosoft Azure. Security Center wordt met uw Azure-abonnement ingeschakeld. Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).

 Security Center is toegankelijk vanuit Hallo [Azure-portal](https://azure.microsoft.com/features/azure-portal/). Zie Hallo [portaldocumentatie](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn meer.

[Aan de slag met Azure Security Center](security-center-get-started.md) leert u snel voor Hallo-beveiligingsbewaking en beleidsbeheer onderdelen van Security Center.

## <a name="next-steps"></a>Volgende stappen
In dit document zijn u geïntroduceerd tooSecurity Center, de belangrijkste mogelijkheden en hoe tooget gestart. toolearn Zie meer Hallo resources te volgen:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) : meer informatie hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) : Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) : meer informatie hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) : meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
- [Beveiliging van gegevens van Azure Security Center](security-center-data-security.md) -informatie over hoe gegevens worden beheerd en beveiligd in Security Center.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) : Hallo nieuwste Azure-beveiliging nieuws en informatie.

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
