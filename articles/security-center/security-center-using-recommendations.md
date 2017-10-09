---
title: Azure Security Center aanbevelingen tooenhance beveiliging aaaUse | Microsoft Docs
description: " Meer informatie over hoe toouse beveiligingsbeleid en aanbevelingen in Azure Security Center toohelp een aanval op de beveiliging verhelpen. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: bd314350a5abfceea3e171f2e1b55afe4549c1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-security-center-recommendations-tooenhance-security"></a>Gebruik Azure Security Center aanbevelingen tooenhance beveiliging
Door een beveiligingsbeleid configureren en vervolgens implementeren Hallo aanbevelingen in Azure Security Center kunt u de kans op Hallo van een beveiligingsgebeurtenis aanzienlijke verkleinen. Dit artikel laat zien hoe toouse beveiligingsbeleid en aanbevelingen in Security Center toohelp een aanval op de beveiliging verhelpen.

> [!NOTE]
> In dit artikel is gebaseerd op Hallo rollen en concepten in Security Center Hallo [plannen en de operations guide](security-center-planning-and-operations-guide.md). Dit is een goed idee tooreview Hallo-handleiding voor planning voordat u doorgaat.
>
>

## <a name="managing-security-recommendations"></a>Aanbevelingen voor beveiliging beheren
Een beveiligingsbeleid bepaalt Hallo set besturingselementen die worden aanbevolen voor resources binnen de opgegeven abonnement of resourcegroep groep Hallo. In Security Center definieert u de beveiligingsvereisten van het bedrijf tooyour op basis van beleid. toolearn meer, Zie [instellen van beveiligingsbeleid in Security Center](security-center-policies.md).

Beveiligingsbeleid voor resourcegroepen worden overgenomen van het Hallo-abonnement.

![Beveiliging overname][1]

Als u aangepaste beleidsregels in bepaalde resourcegroepen nodig hebt, kunt u overname in de resourcegroep Hallo uitschakelen. toodisable, overname tooUnique ingesteld op de blade beveiligingsbeleid Hallo en Hallo-besturingselementen die Security Center aanbevelingen voor het bevat aanpassen.

Hebt u werkbelastingen waarvoor geen Hallo SQL Database Transparent Data Encryption (TDE)-beleid, bijvoorbeeld Hallo-beleid op abonnementsniveau Hallo uitschakelen en inschakelen alleen in Hallo resourcegroepen waar SQL TDE vereist is.

> [!NOTE]
> Als er een conflict tussen het beleid op abonnementsniveau en beleid op het niveau, voorrang Hallo beleid op het niveau.
>
>

Security Center analyseert de beveiligingsstatus Hallo van uw Azure-resources. Wanneer Beveiligingscentrum mogelijke beveiligingsproblemen identificeert, maakt deze aanbevelingen op basis van het Hallo-besturingselementen die zijn ingesteld in het Hallo-beveiligingsbeleid. Hallo aanbevelingen helpen u bij Hallo configuratieproces beveiligingsmechanismen Hallo nodig.

Huidige beleid aanbevelingen in Security Center focus op het, systeemupdates, configuratie van het besturingssysteem, netwerk-beveiligingsgroepen op subnetten en virtuele machines (VM's), SQL Database Auditing, SQL Database TDE en web application firewalls. Zie voor de meest recente dekking Hallo met Security Center aanbevelingen, [aanbevelingen voor beveiliging in Security Center beheren](security-center-recommendations.md).

## <a name="scenario"></a>Scenario
Dit scenario wordt beschreven hoe toouse Security Center toohelp Hallo kans op een aanzienlijke veiligheidsincident verminderen door Security Center aanbevelingen bewaken en actie ondernemen. Hallo scenario gebruikt Hallo fictieve bedrijf Contoso, en functies die zijn gepresenteerd in Security Center Hallo [plannen en de operations guide](security-center-planning-and-operations-guide.md#security-roles-and-access-controls). Hallo rollen vertegenwoordigen individuen en teams die van Security Center tooperform verschillende beveiligingstaken gebruikmaken mogelijk. Hallo-rollen zijn:

![Scenario-functies][2]

Contoso onlangs gemigreerd enkele van hun tooAzure van lokale resources. Contoso wil tooimplement en beheren van beveiliging die hun beveiligingslek tooa aanval op de beveiliging van hun bronnen in de cloud Hallo verminderen.

## <a name="recommended-solution"></a>Aanbevolen oplossing
Een oplossing is toouse Security Center tooprevent en beveiligingsproblemen detecteren. Contoso heeft tooSecurity Center openen via hun Azure-abonnement. Hallo [gratis laag](security-center-pricing.md) van Security Center wordt automatisch ingeschakeld op alle Azure-abonnementen en verzamelen van gegevens is ingeschakeld op alle VM's in het abonnement.

David in de Contoso IT-beveiliging, configureert u een **beveiligingsbeleid** met Security Center. Security Center analyseert de beveiligingsstatus Hallo van Contoso Azure-resources. Wanneer het Beveiligingscentrum identificeert mogelijke beveiligingsproblemen, maakt deze **aanbevelingen** op basis van het Hallo-besturingselementen die zijn ingesteld in het Hallo-beveiligingsbeleid.

Jeff, de eigenaar van een cloud-werkbelasting is verantwoordelijk voor het implementeren en onderhouden van bescherming in overeenstemming met het beveiligingsbeleid van Contoso. Jeff kunt Hallo aanbevelingen die zijn gemaakt door Security Center tooapply beveiligingen bewaken. Hallo aanbevelingen leiden Jeff door Hallo configuratieproces beveiligingsmechanismen Hallo nodig.

In volgorde voor Jeff tooimplement en zorgen voor beveiliging en beveiligingsproblemen, moet hij elimineren:

- Beveiligingsaanbevelingen voor de monitor geleverd door Security Center
- Aanbevelingen voor beveiliging evalueren en te bepalen of hij moet toepassen of verwijderen
- Aanbevelingen voor beveiliging toepassen

Laten we volgen van Jeff stappen toosee hoe gebruikt hij Security Center aanbevelingen tooguide hem door Hallo configuratieproces besturingselementen tooeliminate beveiligingsproblemen.

## <a name="how-tooimplement-this-solution"></a>Hoe tooimplement deze oplossing
Jeff meldt zich aan te[Azure-portal](https://azure.microsoft.com/features/azure-portal/) en wordt geopend Hallo Security Center-console. Als onderdeel van zijn dagelijks bewakingsactiviteiten controleert hij toosee u of er aanbevelingen voor beveiliging zijn door Hallo volgende stappen uit te voeren:

1. Jeroen selecteert Hallo **aanbevelingen** tegel tooopen hello **aanbevelingen** blade.
   ![Selecteer Hallo aanbevelingen tegel][3]
2. Jeff bekijkt hello lijst met aanbevelingen. Hij ziet dat Security Center Hallo lijst met aanbevelingen in volgorde van prioriteit van de hoogste prioriteit toolowest prioriteit is opgegeven. Hij besluit tooaddress een hoge prioriteit aanbeveling op Hallo-lijst. Hij selecteert **Endpoint Protection installeren** op Hallo **aanbevelingen** blade.
3. Hallo **Endpoint Protection installeren** blade wordt geopend met een lijst van virtuele machines zonder antimalware is ingeschakeld. Jeff bekijkt hello lijst met VM's, selecteert u alle virtuele machines en vervolgens selecteert **installeren op 3 VM's**.
   ![Eindpuntbeveiliging installeren][4]
4. Hallo **Selecteer Endpoint Protection** blade geopend met Jeff met twee antimalware-oplossingen. Jeroen selecteert Hallo **Microsoft Antimalware** oplossing.
5. Meer informatie over de anti-malwareoplossing hello wordt weergegeven. Jeroen selecteert **maken**.
   ![Microsoft antimalware][5]
6. Jeff Hallo vereiste configuratie-instellingen op Hallo ingevoerd **installeren** blade en selecteert **OK**.

[Microsoft Antimalware](../security/azure-security-antimalware.md) is nu actief op Hallo VMs geselecteerd.

Jeff blijft toomove via Hallo hoge prioriteit en gemiddelde prioriteit aanbevelingen voor het nemen van beslissingen over de uitvoering. Jeff verwijst naar Hallo [aanbevelingen voor beveiliging beheren](security-center-recommendations.md) artikel toounderstand Hallo aanbevelingen en elk biedt als hij van toepassing is.

Jeff leert die [Microsoft Security Response Center (MSRC)](../security/azure-security-response-center.md) voert selecteert u beveiliging hello Azure-netwerk en infrastructuur bewaken en threat intelligence en misbruik klachten ontvangt van een derde partij. Als Jeff biedt informatie over contact op met de beveiliging voor Contoso Azure-abonnement, contactpersonen van Microsoft Contoso als Hallo MSRC klantgegevens die Contoso detecteert is geopend door een onrechtmatig of niet-geautoriseerde partij. Laten we volgt Jeff als hij is van toepassing hello **contact op met informatie over de beveiliging bieden** aanbeveling (een aanbeveling met de ernst van gemiddeld in Hallo lijst met de bovenstaande aanbevelingen).

1. Jeff selecteert **contact op met informatie over de beveiliging bieden** op Hallo **aanbevelingen** blade die wordt geopend Hallo **contact op met informatie over de beveiliging bieden** blade.
2. Jeroen selecteert hello Azure-abonnement tooprovide contactgegevens op. Een tweede **contact op met informatie over de beveiliging bieden** blade wordt geopend.
   ![Neem contact op met informatie over de beveiliging][6]
3. Op Hallo tweede **contact op met informatie over de beveiliging bieden** blade Jeff invoert:

  - Hallo beveiliging e-mailadres adressen gescheiden door komma's (Er is geen limiet toohello getal met e-mailadressen die hij kunt invoeren)
  - een beveiliging Neem contact op met telefoonnummer

4. Jeff ook Hiermee schakelt u de optie Hallo **Stuur mij e-mails over waarschuwingen** tooreceive e-mailberichten over waarschuwingen met hoog dreigingsniveau.
5. Jeroen selecteert **OK** tooapply Hallo beveiliging Neem contact op met de informatie tooContoso abonnement.

Tot slot Jeff bekijkt hello met lage prioriteit aanbeveling **herstellen OS beveiligingslekken** en bepaalt deze aanbeveling is niet van toepassing. Hij toodismiss Hallo aanbeveling. Jeroen selecteert Hallo drie punten die worden weergegeven toohello rechts en selecteert **sluiten**.
   ![Aanbeveling negeren][7]

## <a name="conclusion"></a>Conclusie
Bewaking van de aanbevelingen in Security Center kunt u beveiligingsproblemen elimineren voordat een aanval plaatsvindt. Door het implementeren en onderhouden van beveiligingen aan het beveiligingsbeleid in Security Center kunt u voorkomen dat een beveiligingsincident voordoet.

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
