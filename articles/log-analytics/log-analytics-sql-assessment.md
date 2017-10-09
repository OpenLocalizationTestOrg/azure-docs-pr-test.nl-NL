---
title: aaaOptimize uw SQL Server-omgeving met Azure Log Analytics | Microsoft Docs
description: U kunt met Azure Log Analytics Hallo SQL Assessment oplossing tooassess Hallo risico en status van uw SQL server-omgevingen met regelmatige tussenpozen.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a>Optimalisatie van uw SQL Server-omgeving met Hallo beoordeling van de SQL-oplossing in Log Analytics

![Symbool van de SQL-evaluatie](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

U kunt Hallo SQL Assessment oplossing tooassess Hallo risico en status van uw server-omgevingen met regelmatige tussenpozen. Dit artikel helpt u bij het installeren van Hallo oplossing zodat u corrigerende maatregelen op mogelijke problemen kunt uitvoeren.

Deze oplossing biedt een geprioriteerde lijst met aanbevelingen voor specifieke tooyour geïmplementeerde serverinfrastructuur. Hallo aanbevelingen worden onderverdeeld in zes focus gebieden waarmee u snel inzicht Hallo risico en herstelacties uitvoeren.

Hallo aanbevelingen zijn gebaseerd op Hallo kennis en ervaring door Microsoft engineers van duizenden klant bezoeken. Elke aanbeveling bevat richtlijnen over waarom een probleem tooyou mogelijk belang en hoe tooimplement Hallo voorgestelde wijzigingen.

U kunt focusgebieden die belangrijkste tooyour organisatie en bijhouden van uw progressie ten opzichte van een omgeving met risico gratis en goed wordt uitgevoerd.

Nadat u Hallo oplossing hebt toegevoegd en een beoordeling voltooid, samenvattende is informatie voor focusgebieden wordt weergegeven op Hallo **SQL Assessment** dashboard voor Hallo-infrastructuur in uw omgeving. Hallo volgende secties wordt beschreven hoe toouse informatie over Hallo Hallo **SQL Assessment** dashboard, waar u kunt weergeven en vervolgens te aanbevolen acties voor de infrastructuur van de SQL-server.

![afbeelding van de beoordeling van de SQL-tegel](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![afbeelding van de beoordeling van de SQL-dashboard](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a>Installeren en configureren van Hallo-oplossing
SQL-evaluatie werkt met alle ondersteunde versies van SQL Server voor Hallo Standard-, Developer- en Enterprise-edities.

Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.

* Agents moeten worden geïnstalleerd op servers die SQL Server geïnstalleerd hebt.
* Hallo SQL oplossing vereist een ondersteunde versie van .NET Framework 4 is geïnstalleerd op elke computer die een OMS-agent heeft.
* In volgorde tooinstall Hallo oplossing Hallo gebruiker moet een beheerder of bijdrager toohello Azure-abonnement als Azure-portal met behulp van Hallo. Hallo-gebruiker moet bovendien een lid van Hallo OMS werkruimte Inzender of administrator-rol in Hallo OMS-portal.
* Als u Operations Manager-agent Hallo met SQL Assessment, moet u een account van Operations Manager Run-As toouse. Zie [Operations Manager run as-accounts voor OMS](#operations-manager-run-as-accounts-for-oms) hieronder voor meer informatie.

  > [!NOTE]
  > Hallo MMA agent biedt geen ondersteuning voor Operations Manager Run-As accounts.
  >
  >
* Hallo SQL Assessment oplossing tooyour OMS-werkruimte met behulp van Hallo proces dat wordt beschreven in toevoegen [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md). Er is geen verdere configuratie nodig.

> [!NOTE]
> Nadat u Hallo oplossing hebt toegevoegd, Hallo AdvisorAssessment.exe bestand tooservers waarop agents zijn toegevoegd. Configuratiegegevens lezen en vervolgens verzonden toohello OMS-service in de cloud Hallo voor verwerking. Logica is toegepaste toohello ontvangen gegevens en Hallo cloudservice registreert Hallo-gegevens.

## <a name="sql-assessment-data-collection-details"></a>De verzameling Gegevensdetails SQL-evaluatie
SQL-evaluatie verzamelt gegevens van WMI, registergegevens, prestatiegegevens en resultaten SQL Server dynamische Beheerweergave weergeven met behulp van Hallo-agents die u hebt ingeschakeld.

Hallo volgende tabel ziet u de methoden van de collectie voor agents, of Operations Manager (SCOM) is vereist, en hoe vaak gegevens worden verzameld door een agent.

| Platform | Directe Agent | SCOM-agents | Azure Storage | SCOM vereist? | SCOM-agent gegevens die worden verzonden via de beheergroep | Frequentie van de verzameling |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  | &#8226; |7 dagen |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Operations Manager run as-accounts voor OMS
Log Analytics in OMS gebruikt Hallo Operations Manager-agent en management groep toocollect en verzenden van gegevens toohello OMS-service. OMS builds van management packs voor werkbelastingen tooprovide toevoegen waarde-services. Elke werkbelasting vereist werklastspecifiek bevoegdheden toorun management packs in een andere beveiligingscontext, zoals een domeinaccount. Referentiegegevens tooprovide moet u een Operations Manager Run As-account voor configureren.

Gebruik Hallo na informatie tooset Hallo Operations Manager run as-account voor SQL-evaluatie.

### <a name="set-hello-run-as-account-for-sql-assessment"></a>Hallo Run As-account voor SQL beoordeling instellen
 Als u al Hallo management pack voor SQL Server gebruikt, moet u de Run As-account gebruiken.

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a>tooconfigure hello SQL Run As-account in Hallo Operations-console
> [!NOTE]
> Als u hello OMS directe agent in plaats van de SCOM-agents hello, Hallo management pack altijd in de beveiligingscontext Hallo Hallo lokale systeemaccount wordt uitgevoerd. Overslaan stappen 1-5 hieronder en Voer Hallo ofwel T-SQL- of Powershell-voorbeeld NT AUTHORITY\SYSTEM als Hallo gebruikersnaam opgeven.
>
>

1. Open Hallo Operations-console in Operations Manager en klik vervolgens op **beheer**.
2. Onder **Run As-configuratie**, klikt u op **profielen**, en open **OMS SQL Assessment Run As-profiel**.
3. Op Hallo **Run As-Accounts** pagina, klikt u op **toevoegen**.
4. Selecteer een Windows Run As-account met Hallo-referenties die nodig zijn voor SQL Server, of klik op **nieuw** toocreate een.

   > [!NOTE]
   > Hallo Run As-accounttype moet Windows. Hallo Run As-account moet ook deel uitmaken van de lokale groep Administrators op alle Windows-Servers die als host fungeert voor SQL Server-exemplaren.
   >
   >
5. Klik op **Opslaan**.
6. Wijzigen en vervolgens Hallo T-SQL-voorbeeld te volgen op elke SQL Server-exemplaar toogrant minimale machtigingen vereist tooRun tooperform As-Account voor SQL-evaluatie wordt uitgevoerd. Echter, u hoeft niet toodo dit als een Run As-Account al deel uit van Hallo serverrol sysadmin voor SQL Server-exemplaren maakt.

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a>tooconfigure hello SQL Run As-account met behulp van Windows PowerShell
Open een PowerShell-venster en Voer Hallo script volgen nadat u deze met uw gegevens hebt bijgewerkt:

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a>Begrijpen hoe de aanbevelingen zijn geplaatst
Elke aanbeveling krijgt een weging-waarde die Hallo relatieve belang van Hallo aanbeveling aangeeft. Alleen Hallo tien belangrijkste aanbevelingen worden weergegeven.

### <a name="how-weights-are-calculated"></a>Hoe gewichten worden berekend
Wegingen zijn statistische waarden op basis van de drie belangrijkste factoren:

* Hallo *kans* dat er een probleem vastgesteld problemen tot leidt. Een grotere kans gelijkstaat tooa groter algemene score voor Hallo aanbeveling.
* Hallo *impact* van Hallo probleem van uw organisatie als dit leidt een probleem tot. Een hogere impact gelijkstaat tooa groter algemene score voor Hallo aanbeveling.
* Hallo *inspanning* tooimplement Hallo aanbeveling vereist. Een hogere inspanning gelijkstaat tooa kleinere totale score voor Hallo aanbeveling.

Hallo weging voor elke aanbeveling wordt uitgedrukt als percentage van totale score Hallo beschikbaar voor elke focusgebied. Bijvoorbeeld, als een aanbeveling in Hallo beveiliging en naleving focusgebied heeft een score van 5%, wordt implementatie van deze aanbeveling verhoogd, uw algemene beveiliging en naleving score door 5%.

### <a name="focus-areas"></a>Focusgebieden
**Beveiliging en naleving** -focus ziet u hier aanbevelingen voor potentiële beveiligingsrisico's en schendingen, bedrijfsbeleid en aan technische, juridische en wettelijke vereisten.

**Beschikbaarheid en zakelijke continuïteit** -focus ziet u hier aanbevelingen voor de beschikbaarheid van de service, de tolerantie van uw infrastructuur en de bescherming van zakelijke.

**Prestaties en schaalbaarheid** -focus ziet u hier aanbevelingen toohelp van uw organisatie IT-infrastructuur toenemen, zorg ervoor dat uw IT-omgeving voldoet aan de huidige prestatievereisten en kunnen toorespond toochanging infrastructuur nodig.

**Een upgrade uitvoert, migratie en implementatie van** - focus ziet u hier aanbevelingen toohelp u een upgrade uitvoert, migreren en implementeren van SQL Server tooyour bestaande infrastructuur.

**Bewerkingen en bewaking** - focus ziet u hier aanbevelingen toohelp stroomlijnen uw IT-team implementeren preventief onderhoud en prestaties.

**Wijzigings- en Configuratiebeheer** -focus ziet u hier aanbevelingen toohelp beveiligen dagelijkse taken, zorg ervoor dat wijzigingen geen negatieve invloed zijn op uw infrastructuur, controleprocedures wijzigen, en tootrack instellen en controleren basissysteemconfiguraties.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Moet u zijn gericht tooscore 100% in elk focusgebied?
Dat hoeft niet. Hallo aanbevelingen zijn gebaseerd op Hallo kennis en ervaring opgedaan door Microsoft engineers in duizenden klant bezoeken. Er is geen infrastructuren van twee servers zijn echter dezelfde Hallo en specifieke aanbevelingen mogelijk meer of minder relevante tooyou. Enkele aanbevelingen voor beveiliging worden minder relevant als uw virtuele machines niet blootgestelde toohello Internet. Enkele aanbevelingen beschikbaarheid mogelijk minder relevant zijn voor services die de ad-hoc gegevensverzameling met lage prioriteit en rapportage bieden. Problemen die belangrijke tooa volwassen bedrijven mogelijk minder belangrijke tooa opstarten. U mogelijk wilt tooidentify welke focusgebieden uw prioriteiten zijn en bekijk hoe uw scores gedurende een bepaalde periode wijzigen.

Elke aanbeveling bevat richtlijnen over waarom het belangrijk is. U moet deze richtlijnen tooevaluate of implementeren van Hallo aanbeveling geschikt is voor u is, gezien Hallo aard van uw IT-services en Hallo zakelijke behoeften van uw organisatie.

## <a name="use-assessment-focus-area-recommendations"></a>Gebruik assessment focus gebied aanbevelingen
Voordat u een oplossing voor evaluatie in OMS gebruiken kunt, moet u Hallo oplossing geïnstalleerd hebben. tooread meer informatie over het installeren van oplossingen, Zie [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md). Nadat deze is geïnstalleerd, kunt u Hallo overzicht van aanbevelingen bekijken met behulp van Hallo SQL Assessment tegel op de overzichtspagina Hallo in OMS.

Weergave Hallo samengevat beoordelingen van compatibiliteit voor uw infrastructuur en inzoomen in aanbevelingen.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>tooview aanbevelingen voor een focus gebied en corrigerende actie ondernemen
1. Op Hallo **overzicht** pagina, klikt u op Hallo **SQL Assessment** tegel.
2. Op Hallo **SQL Assessment** pagina, Hallo samenvattingsinformatie in een Hallo focus gebied blades controleren en klik op een tooview aanbevelingen voor het desbetreffende focusgebied.
3. U kunt op elk van de Hallo focus gebiedspagina's kunt Hallo prioriteit aanbevelingen voor uw omgeving weergeven. Klik op een aanbeveling onder **objecten van invloed op een** tooview om details over waarom het Hallo-aanbeveling wordt gemaakt.  
    ![afbeelding van SQL-evaluatie aanbevelingen](./media/log-analytics-sql-assessment/sql-assess-focus.png)
4. U kunt ondernemen corrigerende maatregelen voorgesteld in **voorgestelde acties**. Wanneer het Hallo-item is opgelost, record hoger beoordelingen die aanbevolen acties zijn uitgevoerd en de naleving-score wordt verhoogd. Gecorrigeerde items worden weergegeven als **doorgegeven objecten**.

## <a name="ignore-recommendations"></a>Aanbevelingen negeren
Als u de aanbevelingen die u tooignore wilt hebt, kunt u een tekstbestand dat OMS tooprevent aanbevelingen worden weergegeven in de resultaten van de beoordeling wordt gebruikt.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>tooidentify aanbevelingen die u worden genegeerd
1. Meld u in de werkruimte tooyour en logboek zoekopdracht openen. Gebruik hello query toolist aanbevelingen die zijn mislukt voor computers in uw omgeving.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   Hier volgt een schermopname die laat zien Hallo logboek zoekquery: ![aanbevelingen is mislukt](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)
2. Kies de aanbevelingen die u tooignore wilt. U in de volgende procedure Hallo Hallo waarden gebruikt voor RecommendationId.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate en het gebruik van een tekstbestand IgnoreRecommendations.txt
1. Maak een bestand met de naam IgnoreRecommendations.txt.
2. Plakken of typ elke RecommendationId voor elke aanbeveling dat u OMS tooignore op een afzonderlijke regel wilt en vervolgens opslaan en Hallo-bestand sluiten.
3. Hallo-bestand in de volgende map op elke computer waar u OMS tooignore aanbevelingen Hallo plaatsen.
   * Op computers met Microsoft Monitoring Agent (rechtstreeks of via de Operations Manager verbonden) - Hallo *SystemDrive*: \Program Files\Microsoft Agent\Agent bewaking
   * Op Hallo Operations Manager-beheerserver - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify dat aanbevelingen worden genegeerd
1. Nadat het Hallo volgende geplande evaluatie wordt uitgevoerd, wordt standaard elke 7 dagen opgegeven Hallo aanbevelingen zijn gemarkeerd genegeerd en worden niet weergegeven op Hallo assessment dashboard.
2. Kunt u Hallo logboek zoeken query's toolist na alle Hallo genegeerd aanbevelingen.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. Als u later besluit dat u wilt dat de aanbevelingen toosee genegeerd, IgnoreRecommendations.txt bestanden verwijderen of u kunt RecommendationIDs verwijderen uit deze.

## <a name="sql-assessment-solution-faq"></a>SQL-evaluatie oplossing Veelgestelde vragen
*Hoe vaak wordt een evaluatie uitgevoerd?*

* Hallo beoordeling wordt uitgevoerd om de zeven dagen.

*Is er een manier tooconfigure hoe vaak Hallo beoordeling wordt uitgevoerd?*

* Momenteel niet.

*Als een andere server wordt gedetecteerd nadat ik Hallo SQL assessment oplossing hebt toegevoegd, wordt deze gecontroleerd?*

* Ja, zodra deze is gedetecteerd. deze wordt beoordeeld van vervolgens, elke 7 dagen.

*Als een server buiten werking wordt gesteld, wanneer deze verwijderd uit Hallo assessment?*

* Als een server komt niet met het verzenden van gegevens voor drie weken, wordt deze verwijderd.

*Wat is de naam Hallo van Hallo-proces dat het verzamelen van gegevens Hallo?*

* AdvisorAssessment.exe

*Hoe lang duurt het voor gegevens toobe verzameld?*

* Hallo werkelijke gegevensverzameling op Hallo server duurt ongeveer 1 uur. Kan het langer duren op servers met een groot aantal SQL-exemplaren of -databases.

*Welk type gegevens worden verzameld?*

* Hallo volgende typen gegevens zijn verzameld:
  * WMI
  * Register
  * Prestatiemeteritems
  * SQL dynamische beheerweergaven (DMV).

*Is er een manier tooconfigure wanneer gegevens worden verzameld?*

* Momenteel niet.

*Waarom heb ik tooconfigure uitvoeren als-Account?*

* Voor SQL Server, worden een klein aantal SQL-query's uitgevoerd. Zodat ze toorun, een Run As-Account met VIEW SERVER STATE machtigingen tooSQL moet worden gebruikt.  Bovendien zijn in de volgorde tooquery WMI, lokale beheerdersreferenties zijn vereist.

*Waarom alleen Hallo top 10 aanbevelingen worden weergegeven?*

* In plaats van zodat u overweldigend uitputtende lijst met taken, is het raadzaam dat u zich richten op Hallo prioriteit aanbevelingen eerst adressering. Nadat u deze oplossen, wordt extra aanbevelingen beschikbaar worden. Als u liever toosee Hallo gedetailleerde lijst, kunt u alle aanbevelingen Hallo OMS logboek zoekactie kunt weergeven.

*Is er een manier tooignore een aanbeveling?*

* Ja, Zie [aanbevelingen negeren](#ignore-recommendations) sectie hierboven.

## <a name="next-steps"></a>Volgende stappen
* [Zoeken in een logboek](log-analytics-log-searches.md) tooview gedetailleerde gegevens voor de Nalevingsbeoordeling van de SQL- en aanbevelingen.
