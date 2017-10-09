---
title: aaaOptimize uw Active Directory-omgeving met Azure Log Analytics | Microsoft Docs
description: U kunt Active Directory Assessment oplossing tooassess Hallo risico en status van uw server-omgevingen met regelmatige tussenpozen hello gebruiken.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a>Optimalisatie van uw Active Directory-omgeving met Hallo beoordeling van Active Directory-oplossing in Log Analytics

![Symbool van AD-evaluatie](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

U kunt Active Directory Assessment oplossing tooassess Hallo risico en status van uw server-omgevingen met regelmatige tussenpozen hello gebruiken. In dit artikel helpt u bij het installeren en gebruiken van Hallo oplossing zodat u corrigerende maatregelen op mogelijke problemen kunt uitvoeren.

Deze oplossing biedt een geprioriteerde lijst met aanbevelingen voor specifieke tooyour geïmplementeerde serverinfrastructuur. Hallo aanbevelingen worden onderverdeeld in vier focus gebieden waarmee u snel inzicht Hallo risico en actie ondernemen.

Hallo aanbevelingen zijn gebaseerd op Hallo kennis en ervaring door Microsoft engineers van duizenden klant bezoeken. Elke aanbeveling bevat richtlijnen over waarom een probleem tooyou mogelijk belang en hoe tooimplement Hallo voorgestelde wijzigingen.

U kunt focusgebieden die belangrijkste tooyour organisatie en bijhouden van uw progressie ten opzichte van een omgeving met risico gratis en goed wordt uitgevoerd.

Nadat u Hallo oplossing hebt toegevoegd en een beoordeling voltooid, samenvattende is informatie voor focusgebieden wordt weergegeven op Hallo **AD Assessment** dashboard voor Hallo-infrastructuur in uw omgeving. Hallo volgende secties wordt beschreven hoe toouse informatie over Hallo Hallo **AD Assessment** dashboard, waar u kunt weergeven en vervolgens te aanbevolen acties voor de infrastructuur van de Active Directory-server.

![afbeelding van de beoordeling van de SQL-tegel](./media/log-analytics-ad-assessment/ad-tile.png)

![afbeelding van de beoordeling van de SQL-dashboard](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a>Installeren en configureren van Hallo-oplossing
Hallo informatie tooinstall na gebruik en oplossingen voor Hallo configureren.

* Agents moeten worden geïnstalleerd op domeincontrollers die lid van Hallo domein toobe geëvalueerd zijn.
* Hallo Active Directory Assessment oplossing vereist een ondersteunde versie van .NET Framework 4 (4.5.2 of hoger) op elke computer die een OMS-agent is geïnstalleerd.
* Toevoegen van Hallo Active Directory-Assessment oplossing tooyour OMS-werkruimte van [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).  Er is geen verdere configuratie nodig.

  > [!NOTE]
  > Nadat u Hallo oplossing hebt toegevoegd, Hallo AdvisorAssessment.exe bestand tooservers waarop agents zijn toegevoegd. Configuratiegegevens lezen en vervolgens verzonden toohello OMS-service in de cloud Hallo voor verwerking. Logica is toegepaste toohello ontvangen gegevens en Hallo cloudservice registreert Hallo-gegevens.
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a>Active Directory Assessment verzameling Gegevensdetails

Active Directory-Assessment verzamelt gegevens van Hallo de volgende bronnen gebruikt Hallo-agents die u hebt ingeschakeld:

- Register-collectors
- LDAP-collectors
- .NET framework
- Gebeurtenis logboekverzamelaars
- Active Directory Service interfaces (ADSI)
- Windows Powershell
- Bestand gegevens collectors
- Windows Management Instrumentation (WMI)
- DCDIAG hulpprogramma API
- API voor File Replication Service (NTFRS)
- Aangepaste C#-code


Hallo volgende tabel ziet u de methoden van de collectie voor agents, of Operations Manager (SCOM) is vereist, en hoe vaak gegevens worden verzameld door een agent.

| Platform | Directe Agent | SCOM-agents | Azure Storage | SCOM vereist? | SCOM-agent gegevens die worden verzonden via de beheergroep | Frequentie van de verzameling |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |7 dagen |

## <a name="understanding-how-recommendations-are-prioritized"></a>Begrijpen hoe de aanbevelingen zijn geplaatst
Elke aanbeveling krijgt een weging-waarde die Hallo relatieve belang van Hallo aanbeveling aangeeft. Alleen Hallo 10 belangrijkste aanbevelingen worden weergegeven.

### <a name="how-weights-are-calculated"></a>Hoe gewichten worden berekend
Wegingen zijn statistische waarden op basis van de drie belangrijkste factoren:

* Hallo *kans* problemen zorgt ervoor dat een probleem dat is aangetroffen. Een grotere kans gelijkstaat tooa groter algemene score voor Hallo aanbeveling.
* Hallo *impact* van Hallo probleem van uw organisatie als dit leidt een probleem tot. Een hogere impact gelijkstaat tooa groter algemene score voor Hallo aanbeveling.
* Hallo *inspanning* tooimplement Hallo aanbeveling vereist. Een hogere inspanning gelijkstaat tooa kleinere totale score voor Hallo aanbeveling.

Hallo weging voor elke aanbeveling wordt uitgedrukt als percentage van totale score Hallo beschikbaar voor elke focusgebied. Bijvoorbeeld, als een aanbeveling in Hallo beveiliging en naleving focusgebied heeft een score van 5%, verhoogd implementatie van deze aanbeveling uw algemene beveiliging en naleving score door 5%.

### <a name="focus-areas"></a>Focusgebieden
**Beveiliging en naleving** -focus ziet u hier aanbevelingen voor potentiële beveiligingsrisico's en schendingen, bedrijfsbeleid en aan technische, juridische en wettelijke vereisten.

**Beschikbaarheid en zakelijke continuïteit** -focus ziet u hier aanbevelingen voor de beschikbaarheid van de service, de tolerantie van uw infrastructuur en de bescherming van zakelijke.

**Prestaties en schaalbaarheid** -focus ziet u hier aanbevelingen toohelp van uw organisatie IT-infrastructuur toenemen, zorg ervoor dat uw IT-omgeving voldoet aan de huidige prestatievereisten en kunnen toorespond toochanging infrastructuur nodig.

**Een upgrade uitvoert, migratie en implementatie van** - focus ziet u hier aanbevelingen toohelp u een upgrade uitvoert, migreren en implementeren van Active Directory tooyour bestaande infrastructuur.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Moet u zijn gericht tooscore 100% in elk focusgebied?
Dat hoeft niet. Hallo aanbevelingen zijn gebaseerd op Hallo kennis en ervaring opgedaan door Microsoft engineers in duizenden klant bezoeken. Er is geen infrastructuren van twee servers zijn echter dezelfde Hallo en specifieke aanbevelingen mogelijk meer of minder relevante tooyou. Enkele aanbevelingen voor beveiliging worden minder relevant als uw virtuele machines niet blootgestelde toohello Internet. Enkele aanbevelingen beschikbaarheid mogelijk minder relevant zijn voor services die de ad-hoc gegevensverzameling met lage prioriteit en rapportage bieden. Problemen die belangrijke tooa volwassen bedrijven mogelijk minder belangrijke tooa opstarten. U mogelijk wilt tooidentify welke focusgebieden uw prioriteiten zijn en bekijk hoe uw scores gedurende een bepaalde periode wijzigen.

Elke aanbeveling bevat richtlijnen over waarom het belangrijk is. U moet deze richtlijnen tooevaluate of implementeren van Hallo aanbeveling geschikt is voor u is, gezien Hallo aard van uw IT-services en Hallo zakelijke behoeften van uw organisatie.

## <a name="use-assessment-focus-area-recommendations"></a>Gebruik assessment focus gebied aanbevelingen
Voordat u een oplossing voor evaluatie in OMS gebruiken kunt, moet u Hallo oplossing geïnstalleerd hebben. tooread meer informatie over het installeren van oplossingen, Zie [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md). Nadat deze is geïnstalleerd, kunt u Hallo overzicht van aanbevelingen bekijken met behulp van Hallo Assessment tegel op de overzichtspagina Hallo in OMS.

Weergave Hallo samengevat beoordelingen van compatibiliteit voor uw infrastructuur en inzoomen in aanbevelingen.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>tooview aanbevelingen voor een focus gebied en corrigerende actie ondernemen
1. Op Hallo **overzicht** pagina, klikt u op Hallo **Assessment** tegel voor uw serverinfrastructuur.
2. Op Hallo **Assessment** pagina, Hallo samenvattingsinformatie in een Hallo focus gebied blades controleren en klik op een tooview aanbevelingen voor het desbetreffende focusgebied.
3. U kunt op elk van de Hallo focus gebiedspagina's kunt Hallo prioriteit aanbevelingen voor uw omgeving weergeven. Klik op een aanbeveling onder **objecten van invloed op een** tooview om details over waarom het Hallo-aanbeveling wordt gemaakt.  
    ![afbeelding van Assessment aanbevelingen](./media/log-analytics-ad-assessment/ad-focus.png)
4. U kunt ondernemen corrigerende maatregelen voorgesteld in **voorgestelde acties**. Hallo-item is opgelost, hoger beoordelingen records die acties aanbevolen zijn uitgevoerd als uw score naleving wordt verhoogd. Gecorrigeerde items worden weergegeven als **doorgegeven objecten**.

## <a name="ignore-recommendations"></a>Aanbevelingen negeren
Als u de aanbevelingen die u tooignore wilt hebt, kunt u een tekstbestand dat OMS tooprevent aanbevelingen worden weergegeven in de resultaten van de beoordeling wordt gebruikt.

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>tooidentify aanbevelingen die u worden genegeerd
1. Meld u in de werkruimte tooyour en logboek zoekopdracht openen. Gebruik hello query toolist aanbevelingen die zijn mislukt voor computers in uw omgeving.

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query zou Wijzig toohello volgende.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   Hier volgt een schermopname die laat zien Hallo logboek zoekquery: ![aanbevelingen is mislukt](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)
2. Kies de aanbevelingen die u tooignore wilt. U in de volgende procedure Hallo Hallo waarden gebruikt voor RecommendationId.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate en het gebruik van een tekstbestand IgnoreRecommendations.txt
1. Maak een bestand met de naam IgnoreRecommendations.txt.
2. Plakken of typ elke RecommendationId voor elke aanbeveling dat u logboekanalyse tooignore op een afzonderlijke regel wilt en vervolgens opslaan en Hallo-bestand sluiten.
3. Hallo-bestand in de volgende map op elke computer waar u OMS tooignore aanbevelingen Hallo plaatsen.
   * Op computers met Microsoft Monitoring Agent (rechtstreeks of via de Operations Manager verbonden) - Hallo *SystemDrive*: \Program Files\Microsoft Agent\Agent bewaking
   * Op Hallo Operations Manager-beheerserver - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify dat aanbevelingen worden genegeerd
Nadat Hallo volgende geplande evaluatie wordt uitgevoerd, wordt standaard elke 7 dagen Hallo opgegeven aanbevelingen zijn gemarkeerd *genegeerd* en worden niet weergegeven op Hallo assessment dashboard.

1. Kunt u Hallo logboek zoeken query's toolist na alle Hallo genegeerd aanbevelingen.

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query zou Wijzig toohello volgende.
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. Als u later besluit dat u wilt dat de aanbevelingen toosee genegeerd, IgnoreRecommendations.txt bestanden verwijderen of u kunt RecommendationIDs verwijderen uit deze.

## <a name="ad-assessment-solutions-faq"></a>AD-evaluatie oplossingen Veelgestelde vragen
*Hoe vaak wordt een evaluatie uitgevoerd?*

* Hallo beoordeling wordt uitgevoerd om de zeven dagen.

*Is er een manier tooconfigure hoe vaak Hallo beoordeling wordt uitgevoerd?*

* Momenteel niet.

*Als een andere server wordt gedetecteerd nadat ik een evaluatie-oplossing hebt toegevoegd, wordt deze gecontroleerd?*

* Ja, zodra deze is gedetecteerd. deze wordt beoordeeld van vervolgens, elke 7 dagen.

*Als een server buiten werking wordt gesteld, wanneer deze verwijderd uit Hallo assessment?*

* Als een server komt niet met het verzenden van gegevens voor drie weken, wordt deze verwijderd.

*Wat is de naam Hallo van Hallo-proces dat het verzamelen van gegevens Hallo?*

* AdvisorAssessment.exe

*Hoe lang duurt het voor gegevens toobe verzameld?*

* Hallo werkelijke gegevensverzameling op Hallo server duurt ongeveer 1 uur. Kan het langer duren op servers die een groot aantal Active Directory-servers hebt.

*Is er een manier tooconfigure wanneer gegevens worden verzameld?*

* Momenteel niet.

*Waarom alleen Hallo top 10 aanbevelingen worden weergegeven?*

* In plaats van zodat u overweldigend uitputtende lijst met taken, is het raadzaam dat u zich richten op Hallo prioriteit aanbevelingen eerst adressering. Nadat u deze oplossen, wordt extra aanbevelingen beschikbaar worden. Als u liever toosee Hallo gedetailleerde lijst, kunt u alle aanbevelingen logboek zoekactie kunt weergeven.

*Is er een manier tooignore een aanbeveling?*

* Ja, Zie [aanbevelingen negeren](#ignore-recommendations) sectie hierboven.

## <a name="next-steps"></a>Volgende stappen
* Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde gegevens voor de Nalevingsbeoordeling van AD en aanbevelingen.
