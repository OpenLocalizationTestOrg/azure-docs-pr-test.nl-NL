---
title: aaaOptimize uw System Center Operations Manager-omgeving met Azure Log Analytics | Microsoft Docs
description: U kunt System Center Operations Manager Assessment oplossing tooassess Hallo risico en status van uw server-omgevingen met regelmatige tussenpozen hello gebruiken.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a>Uw omgeving met System Center Operations Manager (Preview) oplossing Hallo optimaliseren

![System Center Operations Manager Assessment symbool](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

U kunt System Center Operations Manager Assessment oplossing tooassess Hallo risico en status van de System Center Operations Manager server-omgevingen met regelmatige tussenpozen hello gebruiken. In dit artikel helpt u bij het installeren, configureren en Hallo oplossing gebruiken zodat u corrigerende maatregelen op mogelijke problemen kunt uitvoeren.

Deze oplossing biedt een geprioriteerde lijst met aanbevelingen voor specifieke tooyour geïmplementeerde serverinfrastructuur. Hallo aanbevelingen worden onderverdeeld in vier focus gebieden waarmee u snel inzicht Hallo risico en herstelacties uitvoeren.

Hallo aanbevelingen zijn gebaseerd op Hallo kennis en ervaring door Microsoft engineers van duizenden klant bezoeken. Elke aanbeveling bevat richtlijnen over waarom een probleem tooyou mogelijk belang en hoe tooimplement Hallo voorgestelde wijzigingen.

U kunt focusgebieden die belangrijkste tooyour organisatie en bijhouden van uw progressie ten opzichte van een omgeving met risico gratis en goed wordt uitgevoerd.

Nadat u Hallo oplossing hebt toegevoegd en een beoordeling voltooid, samenvattende is informatie voor focusgebieden wordt weergegeven op Hallo **System Center Operations Manager Assessment** dashboard voor uw infrastructuur. Hallo volgende secties wordt beschreven hoe toouse informatie over Hallo Hallo **System Center Operations Manager Assessment** dashboard, waar u kunt weergeven en vervolgens te aanbevolen acties voor uw SCOM-infrastructuur.

![System Center Operations Manager-oplossing tegel](./media/log-analytics-scom-assessment/scom-tile.png)

![System Center Operations Manager Assessment dashboard](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a>Installeren en configureren van Hallo-oplossing

Hallo-oplossing werkt met Microsoft System Operations Manager 2012 R2 en 2012 SP1.

Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.

 - Voordat u een oplossing voor evaluatie in OMS gebruiken kunt, moet u Hallo oplossing geïnstalleerd hebben. Hallo-oplossing van installeren [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) of door de instructies te volgen Hallo in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).

 - Na het toevoegen van Hallo oplossing toohello werkruimte weer Hallo System Center Operations Manager Assessment tegel op Hallo dashboard bericht met de Hallo aanvullende configuratie vereist. Klik op de tegel Hallo en volg Hallo configuratiestappen vermeld in het Hallo-pagina

 ![Dashboardtegel voor System Center Operations Manager](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 Configuratie van System Center Operations Manager Hallo kan worden gedaan via Hallo script door Hallo stappen uit te voeren die worden vermeld in de configuratiepagina Hallo van Hallo-oplossing in OMS.

 In plaats daarvan tooconfigure Hallo assessment via SCOM-Console, volg Hallo onderstaande stappen voor het Hallo dezelfde volgorde
1. [Hallo Run As-account voor System Center Operations Manager beoordeling instellen](#operations-manager-run-as-accounts-for-oms)  
2. [Hallo System Center Operations Manager Assessment regel configureren](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a>System Center Operations Manager assessment Gegevensdetails-verzameling

Hallo beoordeling van de System Center Operations Manager verzamelt gegevens van WMI, registergegevens, gegevens van EventLog, Operations Manager-gegevens via Windows PowerShell, SQL-query's, bestand informatie verzamelen met behulp van Hallo-server die u hebt ingeschakeld.

Hallo volgende tabel ziet u de methoden van de collectie voor System Center Operations Manager beoordeling en hoe vaak gegevens worden verzameld door een agent.

| Platform | Directe Agent | SCOM-agents | Azure Storage | SCOM vereist? | SCOM-agent gegevens die worden verzonden via de beheergroep | Frequentie van de verzameling |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | | | | &#8226; | | zeven dagen |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Operations Manager run as-accounts voor OMS

OMS bouwt voort op management packs voor werkbelastingen tooprovide toevoegen waarde-services. Elke werkbelasting vereist werklastspecifiek bevoegdheden toorun management packs in een andere beveiligingscontext, zoals een domeinaccount. Configureer een Manager Operations die Run As-account tooprovide referentie-informatie.

Gebruik Hallo tooset hello Operations Manager-run as-account voor System Center Operations Manager Assessment informatie te volgen.

### <a name="set-hello-run-as-account"></a>Set Hallo Run As-account

1. Ga in de Operations Manager-Console hello, toohello **beheer** tabblad.
2. Onder Hallo **Run As-configuratie**, klikt u op **Accounts**.
3. Hallo Run As-Account, volgen via Hallo Wizard voor het maken van een Windows-account maken. Hallo account toouse is Hallo een geïdentificeerd en dat alle vereiste onderdelen Hallo hieronder:

    >[!NOTE]
    Hallo Run As-account moet voldoen aan de volgende vereisten:
    - De lid van een domein van Hallo lokale groep Administrators op alle servers in het Hallo-omgeving (alle Operations Manager-functies - beheerserver, Operations Manager-Database, datawarehouse, rapportage, -webconsole, -Gateway)
    - Bewerking Manager beheerdersrol voor Hallo beheergroep wordt beoordeeld
    - Hallo uitvoeren [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) toogrant gedetailleerde machtigingen toohello account voor SQL-instance die wordt gebruikt door Operations Manager.
      Opmerking: Als dit account al sysadmin-rechten heeft, gaat u verder Hallo script worden uitgevoerd.

4. Onder **Distributiebeveiliging**, selecteer **veiliger**.
5. Geef Hallo beheerserver waar Hallo-account is gedistribueerd.
3. Ga terug toohello Run As-configuratie en klikt u op **profielen**.
4. Zoeken naar Hallo *SCOM Assessment profiel*.
5. Hallo profiel moeten worden ingevoerd: *Microsoft System Center Advisor SCOM Assessment Run As-profiel*.
6. Met de rechtermuisknop op en de eigenschappen ervan bijwerken en toevoegen van Hallo recent gemaakte Run As-Account u in stap 3 hebt gemaakt.

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a>SQL-script toogrant gedetailleerde machtigingen toohello Run As-account

Hallo volgende SQL-script toogrant vereist machtigingen toohello Run As-account op Hallo SQL-exemplaar gebruikt door Operations Manager worden uitgevoerd.

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a>Hallo assessment regel configureren

Hallo System Center Operations Manager Assessment van oplossing management pack bevat een regel met naam *Microsoft System Center Advisor SCOM Assessment Assessment regel uitvoeren*. Deze regel is verantwoordelijk voor het uitvoeren van Hallo assessment. tooenable regel Hallo en configureer Hallo frequentie, gebruik Hallo onderstaande procedures.

Microsoft System Center Advisor SCOM Assessment Assessment regel uitvoeren Hallo is standaard uitgeschakeld. toorun hello assessment, moet u Hallo-regel op een beheerserver inschakelen. Gebruik hello stappen te volgen.

#### <a name="enable-hello-rule-for-a-specific-management-server"></a>Hallo-regel voor een specifieke beheerserver inschakelen

1. In Hallo **ontwerpen** werkruimte van Hallo Operations Manager-console, zoekt u de regel Hallo *Microsoft System Center Advisor SCOM Assessment Assessment regel uitvoeren* in Hallo **regels** deelvenster.
2. In de zoekresultaten Hallo Hallo selecteren waarin tekst hello *Type: beheerserver*.
3. Met de rechtermuisknop op het Hallo-regel en klik vervolgens op **overschrijft** > **voor een specifiek object van klasse: beheerserver**.
4.  Selecteer in de Hallo beschikbare lijst met beheerservers, Hallo-beheerserver waarop Hallo regel moet worden uitgevoerd.
5.  Zorg ervoor dat u de waarde te wijzigen**True** voor Hallo **ingeschakeld** parameterwaarde.  
    ![parameter overschrijven](./media/log-analytics-scom-assessment/rule.png)

Configureer Hallo frequentie van Hallo uitgevoerd met behulp van de volgende procedure Hallo terwijl u nog steeds in dit venster.

#### <a name="configure-hello-run-frequency"></a>Configureer de frequentie Hallo uitvoeren

Hallo assessment is standaardinterval voor Hallo geconfigureerde toorun elke 10.080 minuten (of zeven dagen). U kunt onderdrukken Hallo waarde tooa minimumwaarde van 1440 minuten (of één dag). Hallo-waarde vertegenwoordigt Hallo minimaal tijdsverschil tussen opeenvolgende beoordeling wordt uitgevoerd. toooverride hello-interval, gebruik Hallo onderstaande stappen.

1. In Hallo **ontwerpen** werkruimte van Hallo Operations Manager-console, zoekt u de regel Hallo *Microsoft System Center Advisor SCOM Assessment Assessment regel uitvoeren* in Hallo **regels** deelvenster.
2. In de zoekresultaten Hallo Hallo selecteren waarin tekst hello *Type: beheerserver*.
3. Met de rechtermuisknop op het Hallo-regel en klik vervolgens op **onderdrukking Hallo regel** > **voor alle objecten van klasse: beheerserver**.
4. Wijziging Hallo **Interval** parameter waarde tooyour gewenst de waarde voor interval. In onderstaande Hallo voorbeeld, Hallo waarde wordt ingesteld too1440 minuten (één dag).  
    ![de parameter interval](./media/log-analytics-scom-assessment/interval.png)  
    Als het Hallo-waarde is tooless dan 1440 minuten ingesteld, klikt u vervolgens Hallo regel wordt uitgevoerd met een interval van één dag. In dit voorbeeld Hallo regel Hallo intervalwaarde worden genegeerd en wordt uitgevoerd met een frequentie van één dag.


## <a name="understanding-how-recommendations-are-prioritized"></a>Begrijpen hoe de aanbevelingen zijn geplaatst

Elke aanbeveling krijgt een weging-waarde die Hallo relatieve belang van Hallo aanbeveling aangeeft. Alleen Hallo 10 belangrijkste aanbevelingen worden weergegeven.

### <a name="how-weights-are-calculated"></a>Hoe gewichten worden berekend

Wegingen zijn statistische waarden op basis van de drie belangrijkste factoren:

- Hallo *kans* dat er een probleem vastgesteld problemen tot leidt. Een grotere kans gelijkstaat tooa groter algemene score voor Hallo aanbeveling.
- Hallo *impact* van Hallo probleem van uw organisatie als dit leidt een probleem tot. Een hogere impact gelijkstaat tooa groter algemene score voor Hallo aanbeveling.
- Hallo *inspanning* tooimplement Hallo aanbeveling vereist. Een hogere inspanning gelijkstaat tooa kleinere totale score voor Hallo aanbeveling.

Hallo weging voor elke aanbeveling wordt uitgedrukt als percentage van totale score Hallo beschikbaar voor elke focusgebied. Bijvoorbeeld, als een aanbeveling in Hallo beschikbaarheid en zakelijke continuïteit focusgebied heeft een score van 5%, verhoogd implementatie van deze aanbeveling uw algemene beschikbaarheid en zakelijke continuïteit score door 5%.

### <a name="focus-areas"></a>Focusgebieden

**Beschikbaarheid en zakelijke continuïteit** -focus ziet u hier aanbevelingen voor de beschikbaarheid van de service, de tolerantie van uw infrastructuur en de bescherming van zakelijke.

**Prestaties en schaalbaarheid** -focus ziet u hier aanbevelingen toohelp van uw organisatie IT-infrastructuur toenemen, zorg ervoor dat uw IT-omgeving voldoet aan de huidige prestatievereisten en kunnen toorespond toochanging infrastructuur nodig.

**Upgrade-, migratie- en implementatie** - focus ziet u hier aanbevelingen toohelp u een upgrade uitvoert, migreren en implementeren van SQL Server tooyour bestaande infrastructuur.

**Bewerkingen en bewaking** - focus ziet u hier aanbevelingen toohelp stroomlijnen uw IT-team implementeren preventief onderhoud en prestaties.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Moet u zijn gericht tooscore 100% in elk focusgebied?

Dat hoeft niet. Hallo aanbevelingen zijn gebaseerd op Hallo kennis en ervaring opgedaan door Microsoft engineers in duizenden klant bezoeken. Er is geen infrastructuren van twee servers zijn echter dezelfde Hallo en specifieke aanbevelingen mogelijk meer of minder relevante tooyou. Enkele aanbevelingen voor beveiliging worden minder relevant als uw virtuele machines niet blootgestelde toohello Internet. Enkele aanbevelingen beschikbaarheid mogelijk minder relevant zijn voor services die de ad-hoc gegevensverzameling met lage prioriteit en rapportage bieden. Problemen die belangrijke tooa volwassen bedrijven mogelijk minder belangrijke tooa opstarten. U mogelijk wilt tooidentify welke focusgebieden uw prioriteiten zijn en bekijk hoe uw scores gedurende een bepaalde periode wijzigen.

Elke aanbeveling bevat richtlijnen over waarom het belangrijk is. Gebruik deze richtlijnen tooevaluate of implementeren van Hallo aanbeveling geschikt is voor u is, gezien Hallo aard van uw IT-services en Hallo zakelijke behoeften van uw organisatie.

## <a name="use-assessment-focus-area-recommendations"></a>Gebruik assessment focus gebied aanbevelingen

Voordat u een oplossing voor evaluatie in OMS gebruiken kunt, moet u Hallo oplossing geïnstalleerd hebben. tooread meer informatie over het installeren van oplossingen, Zie [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md). Nadat deze is geïnstalleerd, kunt u Hallo samenvatting van aanbevelingen weergeven met behulp van System Center Operations Manager Assessment-tegel Hallo op de overzichtspagina Hallo in OMS.

Weergave Hallo samengevat beoordelingen van compatibiliteit voor uw infrastructuur en inzoomen in aanbevelingen.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>tooview aanbevelingen voor een focus gebied en corrigerende actie ondernemen

1. Op Hallo **overzicht** pagina, klikt u op Hallo **System Center Operations Manager Assessment** tegel.
2. Op Hallo **System Center Operations Manager Assessment** pagina, Hallo samenvattingsinformatie in een Hallo focus gebied blades controleren en klik op een tooview aanbevelingen voor het desbetreffende focusgebied.
3. U kunt op elk van de Hallo focus gebiedspagina's kunt Hallo prioriteit aanbevelingen voor uw omgeving weergeven. Klik op een aanbeveling onder **objecten van invloed op een** tooview om details over waarom het Hallo-aanbeveling wordt gemaakt.  
    ![focusgebied](./media/log-analytics-scom-assessment/focus-area.png)
4. U kunt ondernemen corrigerende maatregelen voorgesteld in **voorgestelde acties**. Wanneer het Hallo-item is opgelost, record hoger beoordelingen die aanbevolen acties zijn uitgevoerd en de naleving-score wordt verhoogd. Gecorrigeerde items worden weergegeven als **doorgegeven objecten**.

## <a name="ignore-recommendations"></a>Aanbevelingen negeren

Als u de aanbevelingen die u tooignore wilt hebt, kunt u een tekstbestand met OMS tooprevent aanbevelingen worden weergegeven in de resultaten van uw beoordeling.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a>tooidentify aanbevelingen die u tooignore wilt

1. Meld u in de werkruimte tooyour en logboek zoekopdracht openen. Gebruik hello query toolist aanbevelingen die zijn mislukt voor computers in uw omgeving.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    Hier volgt een schermopname die laat zien Hallo logboek zoekopdracht:  
    ![zoeken in logboeken](./media/log-analytics-scom-assessment/scom-log-search.png)

2. Kies de aanbevelingen die u tooignore wilt. U in de volgende procedure Hallo Hallo waarden gebruikt voor RecommendationId.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate en het gebruik van een tekstbestand IgnoreRecommendations.txt

1. Maak een bestand met de naam IgnoreRecommendations.txt.
2. Plakken of typ elke RecommendationId voor elke aanbeveling dat u OMS tooignore op een afzonderlijke regel wilt en vervolgens opslaan en Hallo-bestand sluiten.
3. Hallo-bestand in de volgende map op elke computer waar u OMS tooignore aanbevelingen Hallo plaatsen.
4. Op Hallo Operations Manager-beheerserver - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify dat aanbevelingen worden genegeerd

1. Nadat het Hallo volgende geplande evaluatie wordt uitgevoerd, wordt standaard elke zeven dagen opgegeven Hallo aanbevelingen zijn gemarkeerd genegeerd en worden niet weergegeven op Hallo assessment dashboard.
2. Kunt u Hallo logboek zoeken query's toolist na alle Hallo genegeerd aanbevelingen.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. Als u later besluit dat u wilt dat de aanbevelingen toosee genegeerd, IgnoreRecommendations.txt bestanden verwijderen of u kunt RecommendationIDs verwijderen uit deze.

## <a name="system-center-operations-manager-assessment-solution-faq"></a>Veelgestelde vragen voor System Center Operations Manager Assessment-oplossing

*Ik heb Hallo assessment oplossing toomy OMS-werkruimte hebt toegevoegd. Maar Hallo aanbevelingen niet weergegeven. Waarom niet?* Na het toevoegen van Hallo oplossing gebruiken Hallo stappen weergave Hallo aanbevelingen op Hallo OMS dashboard te volgen.  

- [Hallo Run As-account voor System Center Operations Manager beoordeling instellen](#operations-manager-run-as-accounts-for-oms)  
- [Hallo System Center Operations Manager Assessment regel configureren](#configure-the-assessment-rule)


*Is er een manier tooconfigure hoe vaak Hallo beoordeling wordt uitgevoerd?* Ja. Zie [configureren Hallo run frequentie](#configure-the-run-frequency).

*Als een andere server wordt gedetecteerd nadat ik Hallo System Center Operations Manager Assessment oplossing hebt toegevoegd, wordt deze gecontroleerd?* Ja, na de detectie, deze wordt gecontroleerd van vervolgens aan--standaard elke zeven dagen.

*Wat is de naam Hallo van Hallo-proces dat het verzamelen van gegevens Hallo?* AdvisorAssessment.exe

*Waar wordt Hallo AdvisorAssessment.exe proces uitgevoerd?* AdvisorAssessment.exe wordt uitgevoerd onder Hallo Health-service van de beheerserver Hallo waar Hallo assessment regel is ingeschakeld. Met dit proces, is detectie van uw hele omgeving via externe gegevensverzameling bereikt.

*Hoe lang duurt het voor het verzamelen van gegevens?* Verzamelen van gegevens op de server Hallo duurt ongeveer één uur. Kan het langer duren in omgevingen met veel Operations Manager-exemplaren of -databases.

*Wat gebeurt er als ik hello-interval van Hallo assessment tooless dan 1440 minuten instellen?*  hello beoordeling is vooraf geconfigureerd toorun maximaal eenmaal per dag. Als u waarde Hallo-tooa intervalwaarde maximaal 1440 minuten overschrijven, gebruikt Hallo assessment 1440 minuten als Hallo intervalwaarde.

*Hoe tooknow als er vereiste fouten?* Als Hallo assessment uitgevoerd en er geen resultaten, is het waarschijnlijk dat sommige van de vereisten voor beoordeling Hallo Hallo is mislukt. U kunt query's uitvoeren: `Type=Operation Solution=SCOMAssessment` en `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` in logboek zoeken toosee Hallo vereisten is mislukt.

*Er is een `Failed tooconnect toohello SQL Instance (….).` bericht vereiste storingen in. Wat is Hallo probleem?* AdvisorAssessment.exe, Hallo-proces dat gegevens verzamelt, wordt uitgevoerd onder Hallo Health-service van Hallo-beheerserver. Als onderdeel van de assessment hello probeert Hallo proces tooconnect toohello SQL Server waarin Hallo Operations Manager-database aanwezig is. Deze fout kan optreden wanneer firewallregels Hallo verbinding toohello SQL Server-exemplaar blokkeren.

*Welk type gegevens worden verzameld?*  hello volgende typen gegevens worden verzameld: - gegevens van WMI - gegevens - gegevens van EventLog - Operations Manager registergegevens via Windows PowerShell, SQL-query's en bestanden verzamelen van informatie.

*Waarom heb ik tooconfigure uitvoeren als-Account?* Voor een Operations Manager-server worden verschillende SQL-query's uitgevoerd. Zodat ze toorun, moet u een Run As-Account gebruiken met de vereiste machtigingen beschikt. Bovendien zijn lokale beheerdersreferenties vereist tooquery WMI.

*Waarom alleen Hallo top 10 aanbevelingen worden weergegeven?* In plaats van geeft u een uitgebreide en overweldigend lijst van taken, is het raadzaam dat u zich richten op Hallo prioriteit aanbevelingen eerst adressering. Nadat u deze oplossen, wordt extra aanbevelingen beschikbaar worden. Als u liever toosee Hallo gedetailleerde lijst, kunt u alle aanbevelingen logboek zoekactie kunt weergeven.

*Is er een manier tooignore een aanbeveling?* Ja, Zie Hallo [aanbevelingen negeren](#Ignore-recommendations).


## <a name="next-steps"></a>Volgende stappen

- [Zoeken in een logboek](log-analytics-log-searches.md) tooview gedetailleerde gegevens voor System Center Operations Manager Assessment en aanbevelingen.
