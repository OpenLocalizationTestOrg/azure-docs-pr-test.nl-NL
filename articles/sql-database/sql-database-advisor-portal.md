---
title: aaaApply prestaties aanbevelingen - Azure SQL Database | Microsoft Docs
description: U kunt hello Azure portal toofind prestaties aanbevelingen die u kunnen de prestaties van uw Azure SQL Database of toocorrect optimaliseren sommige probleem dat is aangetroffen in uw workload.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a>Zoeken en toepassen van aanbevelingen voor prestaties

U kunt hello Azure portal toofind prestaties aanbevelingen die u kunnen de prestaties van uw Azure SQL Database of toocorrect optimaliseren sommige probleem dat is aangetroffen in uw workload. **Prestaties aanbeveling** pagina in Azure-portal kunt u toofind Hallo bovenste aanbevelingen op basis van de potentiële impact. 

## <a name="viewing-recommendations"></a>Aanbevelingen weergeven

tooview en toepassen van aanbevelingen voor prestaties, u moet Hallo juist [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md) machtigingen in Azure. **Lezer**, **SQL DB Contributor** machtigingen zijn vereist tooview-aanbevelingen en **eigenaar**, **SQL DB Contributor** machtigingen zijn vereist tooexecute maatregelen; Maak of verwijder indexen en maken van een index te annuleren.

Hallo volgende stappen toofind prestaties aanbevelingen in Azure portal gebruiken:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Ga te**meer services** > **SQL-databases**, en selecteer uw database.
3. Navigeer te**prestaties aanbeveling** tooview beschikbaar aanbevelingen voor de geselecteerde database Hallo.

Aanbevelingen voor prestaties zijn shonw Hallo vergelijkbare toohello tabel een weergegeven op de volgende afbeelding Hallo:

![Aanbevelingen](./media/sql-database-advisor-portal/recommendations.png)

Aanbevelingen worden gesorteerd op de potentiële impact op de prestaties in Hallo categorieën te volgen:

| Impact | Beschrijving |
|:--- |:--- |
| Hoog |Aanbevelingen voor grote invloed leveren Hallo belangrijkste prestatie-invloed. |
| Middelgroot |Gemiddeld impact aanbevelingen moeten de prestaties verbeteren, maar niet aanzienlijk. |
| Laag |Lage impact aanbevelingen moeten zorgen voor betere prestaties dan zonder, maar mogelijk aanzienlijke verbeteringen niet. |


> [!NOTE]
> Azure SQL Database heeft toomonitor activiteiten ten minste een dag in volgorde tooidentify enkele aanbevelingen. Hello Azure SQL Database kunt gemakkelijker optimaliseren voor consistente querypatronen dan dit kunt doen voor willekeurige slechte bursts van activiteit. Als de aanbevelingen zijn niet beschikbaar corrently, Hallo **prestaties aanbeveling** pagina vindt u een bericht waarin wordt uitgelegd waarom.
> 

U kunt ook de status Hallo Hallo historische bewerkingen weergeven. Selecteer een aanbeveling of status toosee meer details.

Hier volgt een voorbeeld van een aanbeveling 'Index maken' in hello Azure-portal.

![Index maken](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a>Toepassen van aanbevelingen
Azure SQL Database hebt u volledige controle over hoe aanbevelingen worden ingeschakeld met behulp van een Hallo na drie opties: 

* Afzonderlijke aanbevelingen één toepassing tegelijk.
* Schakel Hallo automatische afstemmen tooautomatically toepassen van aanbevelingen.
* een aanbeveling tooimplement uitgevoerd handmatig Hallo aanbevolen T-SQL-script op uw database.

Selecteer elke aanbeveling tooview de details en klik op **script weergeven** tooreview Hallo meer informatie over hoe Hallo aanbeveling wordt gemaakt.

Hallo-database blijft online tijdens het Hallo-aanbeveling wordt toegepast--een database met behulp van de prestaties aanbeveling of automatische afstemming nooit offline neemt.

### <a name="apply-an-individual-recommendation"></a>Een afzonderlijke aanbeveling toepassen
U kunt bekijken en aanbevelingen een tegelijk accepteren.

1. Op Hallo **aanbevelingen** blade, selecteert u een aanbeveling.
2. Op Hallo **Details** Klik op de blade **toepassen** knop.
   
    ![Aanbeveling toepassen](./media/sql-database-advisor-portal/apply.png)

Geselecteerde aanbeveling wordt toegepast op Hallo-database.

### <a name="removing-recommendations-from-hello-list"></a>Aanbevelingen verwijderen uit lijst Hallo
Als uw lijst met aanbevelingen items bevat die u tooremove uit Hallo-lijst wilt, kunt u Hallo aanbeveling negeren:

1. Een aanbeveling selecteren in lijst met Hallo **aanbevelingen** tooopen Hallo details.
2. Klik op **negeren** op Hallo **Details** blade.

Indien gewenst, kunt u toevoegen verwijderde items terug toohello **aanbevelingen** lijst:

1. Op Hallo **aanbevelingen** Klik op de blade **weergave verwijderd**.
2. Selecteer een verwijderde item van Hallo lijst tooview de details ervan.
3. Klik desgewenst op **ongedaan negeren** tooadd Hallo index back toohello primaire lijst met **aanbevelingen**.


### <a name="enable-automatic-tuning"></a>Automatisch instellen inschakelen
U kunt automatisch hello Azure SQL Database tooimplement aanbevelingen instellen. Aanbevelingen beschikbaar komen ze automatisch worden toegepast. Als met alle aanbevelingen die worden beheerd door Hallo worden service als Hallo prestatieresultaat negatief Hallo aanbeveling is, teruggedraaid.

1. Op Hallo **aanbevelingen** blade, klikt u op **automatiseren**:
   
    ![Advisor-instellingen](./media/sql-database-advisor-portal/settings.png)
2. Selecteer de acties die tooautomate:
   
    ![Aanbevolen indexen](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a>Handmatig Hallo aanbevolen T-SQL-script uitvoeren
Selecteer elke aanbeveling en klik op **script weergeven**. Dit script uitvoeren op uw database toomanually Hallo aanbeveling toepassen.

*Indexen die handmatig worden uitgevoerd wordt niet gecontroleerd en gevalideerd voor prestatie-invloed Hallo service* zodat het wordt aangeraden dat u deze indexen na het maken van tooverify controleren ze bieden betere prestaties en aan te passen of verwijder ze als nodig. Zie voor meer informatie over het maken van indexen [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).

### <a name="canceling-recommendations"></a>Aanbevelingen annuleren
Aanbevelingen die zich in een **in behandeling**, **controleren**, of **geslaagd** status kan worden geannuleerd. Aanbevelingen met de status van **Executing** kan niet worden geannuleerd.

1. Selecteer een aanbeveling in Hallo **afstemmen geschiedenis** gebied tooopen hello **aanbevelingen details** blade.
2. Klik op **annuleren** tooabort Hallo proces van het toepassen van Hallo aanbeveling.

## <a name="monitoring-operations"></a>Bewakingsbewerkingen
Toepassen van een aanbeveling kan niet direct gebeuren. Hallo-portal biedt gegevens met betrekking tot het Hallo-status van de aanbeveling. Hallo volgen mogelijke statussen van een index worden weergegeven in:

| Status | Beschrijving |
|:--- |:--- |
| In behandeling |Aanbeveling opdracht is ontvangen en is gepland voor uitvoering toepassen. |
| Uitvoeren |Hallo-aanbeveling wordt toegepast. |
| Controleren |Aanbeveling is toegepast en Hallo service meet Hallo voordelen. |
| Geslaagd |Aanbeveling is toegepast en voordelen zijn gemeten. |
| Fout |Er is een fout opgetreden tijdens het Hallo Hallo aanbeveling toe te passen. Dit kan een tijdelijk probleem of mogelijk een tabel met schema wijzigen toohello en Hallo-script is niet meer geldig. |
| Herstellen van instellingen |Hallo aanbeveling werd toegepast, maar heeft vastgesteld dat is niet zodat en automatisch wordt omgezet. |
| Teruggedraaid |Hallo-aanbeveling is hersteld. |

Klik op een in-process-aanbeveling van Hallo lijst toosee meer informatie:

![Aanbevolen indexen](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a>Herstellen van een aanbeveling
Als u Hallo prestaties aanbevelingen tooapply Hallo aanbeveling gebruikt wordt (wat betekent dat u handmatig niet Hallo T-SQL-script hebt uitgevoerd) automatisch overgeschakeld deze als het Hallo prestaties impact toobe negatieve gevonden. Als voor de gewenste gewoon toorevert of andere reden een aanbeveling kunt u doen Hallo volgende:

1. Selecteer een toegepaste aanbeveling in Hallo **afstemmen geschiedenis** gebied.
2. Klik op **Revert** op Hallo **gegevens over de aanbeveling** blade.

![Aanbevolen indexen](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a>Bewaking van prestatie-invloed van de indexaanbevelingen
Nadat de aanbevelingen zijn geïmplementeerd (momenteel index-bewerkingen en aanbevelingen voor query's alleen voorzien) kunt u **Query Insights** op Hallo aanbeveling details blade tooopen [Query Inzichten](sql-database-query-performance.md) en Zie Hallo prestatie-invloed van de meest gebruikte query's.

![Prestatie-invloed van monitor](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a>Samenvatting
Azure SQL-Database bevat aanbevelingen voor het verbeteren van de prestaties van de SQL-database. Dankzij de T-SQL-scripts, evenals afzonderlijke en volledig-automatische, krijgt u een handig hulp bij het optimaliseren van uw database en uiteindelijk queryprestaties te verbeteren.

## <a name="next-steps"></a>Volgende stappen
Uw aanbevelingen controleren en doorgaan tooapply ze toorefine prestaties. Database-werkbelastingen zijn dynamisch en continu wijzigen. Azure SQL-Database wordt voortgezet toomonitor en doet aanbevelingen die potentieel prestaties van uw database kunnen verbeteren. 

* Zie [automatische afstemming](sql-database-automatic-tuning.md) toolearn informatie over Hallo automatische afstemming in Azure SQL Database.
* Zie [prestaties aanbevelingen](sql-database-advisor.md) voor een overzicht van Azure SQL Database prestaties aanbevelingen.
* Zie [inzichten voor queryprestaties](sql-database-query-performance.md) toolearn over het weergeven van Hallo prestatie-invloed van de meest gebruikte query's.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Query Store](https://msdn.microsoft.com/library/dn817826.aspx)
* [INDEX MAKEN](https://msdn.microsoft.com/library/ms188783.aspx)
* [Toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md)

