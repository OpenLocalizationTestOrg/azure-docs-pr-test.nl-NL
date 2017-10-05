---
title: 'Azure-portal: maken en beheren van een elastische pool SQL Database | Microsoft Docs'
description: Informatie over het gebruik van de Azure portal en de ingebouwde intelligentie SQL-Database om te beheren, controleren en het juiste formaat een schaalbare elastische pool te optimaliseren van databaseprestaties en kosten beheren.
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 4ffd1db31f42967dc7f07aa979898dddbb333641
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-the-azure-portal"></a>Maken en beheren van een elastische groep met de Azure-portal
In dit onderwerp wordt beschreven hoe u maken en beheren van schaalbare [elastische pools](sql-database-elastic-pool.md) met de Azure-portal. U kunt ook maken en beheren van een Azure elastische groep met [PowerShell](sql-database-elastic-pool-manage-powershell.md), de REST-API of [C#](sql-database-elastic-pool-manage-csharp.md). U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

## <a name="create-an-elastic-pool"></a>Elastische pool maken 

Er zijn twee manieren kunt u een elastische pool. U kunt dit zelf doen, als u weet welke instellingen u voor uw groep wilt gebruiken, of u kunt gebruikmaken van wat de service u aanraadt. SQL-Database beschikt over ingebouwde intelligentie die raadt aan om een elastische groep is ingesteld als het kostenefficiënte op basis van de gebruikstelemetrie van uw databases.

U kunt meerdere groepen maken op een server, maar u kunt geen databases van verschillende servers toevoegen aan dezelfde pool. 

> [!NOTE]
> Elastische pools zijn algemeen beschikbaar in alle Azure-regio's, behalve in West-India, waar deze zich momenteel in de previewfase bevinden.  Algemene beschikbaarheid van elastische pools in deze regio zal zo snel mogelijk plaatsvinden.
>

### <a name="step-1-create-an-elastic-pool"></a>Stap 1: Een elastische pool maken

Een elastische pool te maken van een bestaand **server** blade in de portal is de eenvoudigste manier om te verplaatsen van bestaande databases in een elastische pool.

> [!NOTE]
> U kunt ook een elastische pool maken door te zoeken naar **elastische SQL-groep** in de **Marketplace** of klikken op **+ toevoegen** in de **SQL elastische pools** blade bladeren. U bent een nieuwe of bestaande server via deze werkstroom van toepassingen opgeven.
>
>

1. In de [Azure-portal](http://portal.azure.com/), klikt u op **meer services**  **>**  **SQL-servers**, en klik vervolgens op de server waarop de databases die u wilt toevoegen aan een elastische pool.
2. Klik op **Nieuwe groep**.

    ![Voeg de groep toe aan een server](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **-OF-**

    Mogelijk ziet u een bericht weergegeven dat er aanbevolen elastische pools voor de server. Klik op het bericht om de groepen die worden aanbevolen op basis van de telemetrie van het databasegebruik te bekijken. Klik vervolgens op de categorie voor meer informatie en om de groep aan te passen. Zie [Aanbevelingen voor groepen begrijpen](#understand-elastic-pool-recommendations) verderop in dit onderwerp om te ontdekken hoe de aanbeveling tot stand is gekomen.

    ![aanbevolen groep](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. De **elastische pool** blade wordt weergegeven waarin u de instellingen voor uw groep opgeven. Als u hebt geklikt **nieuwe pool** in de vorige stap, de prijscategorie is **standaard** standaard en geen databases geselecteerd. U kunt een lege pool maken of een set bestaande databases van deze server opgeven die moeten worden verplaatst naar de pool. Als u een aanbevolen pool maakt, zijn de aanbevolen prijscategorie, de prestatie-instellingen en de lijst met databases vooraf ingevuld, maar u ze nog steeds wijzigen.

    ![Elastische groep configureren](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Kies een naam voor de elastische groep, of behoud de standaardnaam.

### <a name="step-2-choose-a-pricing-tier"></a>Stap 2: kies een prijscategorie

De prijscategorie van de pool bepaalt welke functies beschikbaar zijn voor de elastics in de groep en het maximale aantal edtu's (eDTU MAX) en opslag (GB) beschikbaar zijn voor elke database. Zie voor meer informatie de Servicecategorieën.

Klik op **Prijscategorie** om de prijscategorie van de pool te wijzigen. Klik op de gewenste prijscategorie en vervolgens op **Selecteren**.

> [!IMPORTANT]
> Nadat u de prijscategorie gekozen heeft en uw wijzigingen heeft opgeslagen door in de laatste stap op **OK** te klikken, kunt u de prijscategorie van de groep niet meer wijzigen. De prijscategorie voor een bestaande elastische pool niet wijzigen, een elastische pool maken in de gewenste prijscategorie en migreert de databases naar deze nieuwe pool.
>

![Een prijscategorie selecteren](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-the-pool"></a>Stap 3: configureer de groep

Zodra de prijscategorie is ingesteld, klikt u op pool configureren Hier voegt u databases, set groepen met edtu's en opslag (GB adresgroep) en waar u de min en max edtu's voor de elastics instellen in de groep.

1. Klik op **Groep configureren**
2. Selecteer de databases die u aan de groep wilt toevoegen. Deze stap is optioneel bij het maken van de groep. Databases kunnen ook worden toegevoegd wanneer de groep is gemaakt.
    Om databases toe te voegen klikt u op **Database toevoegen** en vervolgens op de databases die u wilt toevoegen. Klik als laatste op de knop **Selecteren**.

    ![Databases toevoegen](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    Als de gebruikstelemetrie van de databases waar u mee werkt genoeg is, worden de grafiek **Geschat eDTU- en GB-gebruik** en het staafdiagram **Werkelijk eDTU-gebruik** bijgewerkt zodat u betere beslissingen kunt nemen met betrekking tot de configuratie. De service kan ook een bericht weergeven met een aanbeveling zodat u de groep het juiste formaat kunt geven. Zie [Dynamische aanbevelingen](#understand-elastic-pool-recommendations).

3. Gebruik de bedieningselementen op de pagina **Groep configureren** om de instellingen te verkennen en uw groep te configureren. Zie [limieten elastische pools](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor meer informatie over de limieten van elke servicecategorie en Zie [prijs- en Prestatieoverwegingen voor elastische pools](sql-database-elastic-pool.md) voor gedetailleerde richtlijnen voor het juiste formaat een elastische pool. Zie voor meer informatie over de groepsinstellingen [eigenschappen van de elastische groep](sql-database-elastic-pool.md#database-properties-for-pooled-databases).

    ![Elastische groep configureren](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. Klik op **Selectere** in de blade **Groep configureren** nadat u de instellingen heeft gewijzigd.
5. Klik op **OK** om de groep te maken.

## <a name="understand-elastic-pool-recommendations"></a>Aanbevelingen voor elastische Pools begrijpen

De SQL Database-service beoordeelt de gebruiksgeschiedenis en beveelt een of meerdere groepen aan wanneer deze kosteneffectiever zijn dan het gebruik van individuele databases. Elke aanbeveling wordt geconfigureerd met een unieke subset van de databases van de server die het meest geschikt zijn voor de groep.

![aanbevolen groep](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

De aanbevelingen voor de groep bestaan uit:

- Een prijscategorie voor de pool (Basic, Standard, Premium of RS Premium)
- De juiste **eDTU’s voor de groep** (ook wel Max eDTU's per groep)
- De **eDTU MAX** en **eDTU Min** per database
- De lijst met aanbevolen databases voor de groep

> [!IMPORTANT]
> De service houdt rekening met de laatste 30 dagen telemetrie bij het aanbevelen van groepen. Voor een database te worden beschouwd als kandidaat voor een elastische pool, moet er ten minste 7 dagen bestaan. Databases die zich al in een elastische pool bevinden, worden niet aanbevolen voor een elastische pool.
>

De service beoordeelt wat de resource nodig heeft en hoe kosteneffectief het is om de individuele databases in elke servicecategorie te verplaatsen naar groepen van dezelfde categorie. Alle Standard databases op een server worden bijvoorbeeld beoordeeld op hoe ze in een Standard elastische groep passen. Dit betekent dat de service geen aanbevelingen doet voor het verplaatsen van databases naar een andere categorie, zoals het verplaatsen van een Standard database naar een Premium groep.

Nadat databases zijn toegevoegd aan de groep, worden aanbevelingen dynamisch gegenereerd op basis van het gebruik van de databases die u hebt geselecteerd. Deze aanbevelingen worden weergegeven in de eDTU- en GB-gebruiksgrafiek en in een banner aan de bovenkant van de **pool configureren** blade. Deze aanbevelingen zijn bedoeld om u te helpen bij het maken van een elastische pool die geoptimaliseerd is voor uw specifieke databases.

![dynamische aanbevelingen](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a>Beheren en controleren van een elastische pool

U kunt de Azure portal gebruiken om te controleren en beheren van een elastische groep en de databases in de pool. U kunt het gebruik van een elastische groep en de databases binnen die groep bewaken vanuit de portal. U kunt ook een aantal wijzigingen aanbrengen in uw elastische groep en alle wijzigingen tegelijk verzenden. Deze wijzigingen omvatten toevoegen of verwijderen van databases, elastische pool-instellingen wijzigen of database-instellingen wijzigen.

De volgende afbeelding toont een voorbeeld van de elastische groep. De weergave bevat:

*  De grafieken voor het brongebruik van de elastische groep en de databases die zijn opgenomen in de groep.
*  De **configureren** knop wijzigingen aanbrengen in de elastische groep van toepassingen.
*  De **database maken** knop waarmee een database wordt gemaakt en toegevoegd aan de huidige elastische groep.
*  Groot aantal databases beheren elastische taken die u helpen door te voeren van Transact-SQL-scripts op alle databases in een lijst.

![Toepassingen weergeven][2]

U kunt gaan naar een bepaalde groep om te zien van de bronnen beter worden benut. Standaard worden de toepassingen is geconfigureerd voor het weergeven van opslag en het eDTU-gebruik voor het afgelopen uur. De grafiek kan worden geconfigureerd voor andere metrische gegevens weergeven over verschillende tijdvensters.

1. Selecteer een elastische pool met werkt.
2. Onder **elastische Pool bewaking** is een grafiek met het label **Resourcegebruik**. Klik op de grafiek.

    ![Bewaking van de elastische groep][3]

    De **metriek** blade wordt geopend, waarin een gedetailleerde weergave van de opgegeven metrische gegevens via de opgegeven periode.   

    ![Blade met metrische gegevens][9]

### <a name="to-customize-the-chart-display"></a>De grafiekweergave aanpassen

U kunt de metrische blade om weer te geven van andere metrische gegevens zoals CPU-percentage, gegevens-IO-percentage en log-IO-percentage gebruikt en de grafiek bewerken.

1. Klik op de blade metrische **bewerken**.

    ![Klik op bewerken][6]

2. In de **grafiek bewerken** blade, selecteert u een tijdsbereik (voorbij vandaag de dag, uur of afgelopen week), of klik op **aangepaste** datumbereik selecteren in de afgelopen twee weken. Selecteer het grafiektype (staaf- of regel) en selecteer vervolgens de bronnen om te controleren.

   > [!Note]
   > Metrische gegevens met de dezelfde eenheid kunnen worden weergegeven in de grafiek op hetzelfde moment. Bijvoorbeeld, als u 'eDTU percentage' selecteert kunt vervolgens u alleen selecteren andere metrische gegevens met percentage als de maateenheid.
   >

    ![Klik op bewerken](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. Klik vervolgens op **OK**.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Beheren en controleren van de databases in een elastische pool

Afzonderlijke databases kunnen ook worden gecontroleerd voor potentiële problemen.

1. Onder **elastische Database bewaken**, er is een diagram waarin metrische gegevens voor vijf databases. Standaard het diagram toont de bovenste 5 databases in de groep door gemiddeld eDTU-gebruik in het afgelopen uur. Klik op de grafiek.

    ![Bewaking van de elastische groep][4]

2. De **Database Resourcegebruik** blade wordt weergegeven. Dit biedt een gedetailleerde weergave van het Databasegebruik in de groep. Het raster in het onderste gedeelte van de blade kunt u geen databases selecteren in de groep om het gebruik ervan in de grafiek (maximaal 5 databases) weer te geven. U kunt ook de metrische gegevens en het tijdstip venster wordt weergegeven in de grafiek door te klikken op **grafiek bewerken**.

    ![Gebruik van de databaseblade resource][8]

### <a name="to-customize-the-view"></a>De weergave aanpassen

1. In de **Resourcegebruik van de Database** blade, klikt u op **grafiek bewerken**.

    ![Klik op de grafiek bewerken](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. In de **bewerken** blade grafiek, selecteert u een tijdsbereik (voorbij uur of afgelopen 24 uur) of klik op **aangepaste** selecteren van een andere dag in de afgelopen twee weken om weer te geven.

    ![Klik op aangepast](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Klik op de **vergelijken databases door** dropdown selecteren van een andere waarde voor gebruik bij het vergelijken van databases.

    ![De grafiek bewerken](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="to-select-databases-to-monitor"></a>Databases bewaken selecteren

In de databaselijst in de **Database Resourcegebruik** blade kunt u bepaalde databases vinden door te zoeken door de pagina's in de lijst of typ in de naam van een database. Gebruik de selectievakjes om de database te selecteren.

![Zoeken naar databases bewaken][7]


## <a name="add-an-alert-to-an-elastic-pool-resource"></a>Een waarschuwing toevoegen aan een resource voor de elastische groep

U kunt regels toevoegen aan een elastische groep die e-mail verzenden naar personen of waarschuwing tekenreeksen met URL-eindpunten wanneer de elastische groep treffers een drempelwaarde voor overbenutting die u hebt ingesteld.

**Een waarschuwing toevoegen aan een resource:**

1. Klik op de **Resourcegebruik** grafiek te openen de **metriek** blade klikt u op **waarschuwing toevoegen**, en geef vervolgens de informatie in de **een waarschuwingsregeltoevoegen** blade (**Resource** wordt automatisch ingesteld tot worden de toepassingen waarmee u werkt).
2. Typ een **naam** en **beschrijving** die de waarschuwing u en de ontvangers identificeert.
3. Kies een **metriek** die u wilt een waarschuwing in de lijst.

    De grafiek wordt dynamisch Resourcegebruik voor deze metriek bij het kiezen van een drempelwaarde.

4. Kies een **voorwaarde** (groter dan maximaal, enzovoort) en een **drempelwaarde**.
5. Kies een **periode** tijdsperiode waarin de meetwaarde regel moet worden voldaan voordat de waarschuwing triggers.
6. Klik op **OK**.

Zie voor meer informatie [waarschuwingen van de SQL-Database maken in Azure portal](sql-database-insights-alerts-portal.md).

## <a name="move-a-database-into-an-elastic-pool"></a>Een database verplaatsen naar een elastische pool

U kunt toevoegen of verwijderen van databases uit een bestaande groep. De databases kunnen zich in andere toepassingen. U kunt echter alleen databases die zich op dezelfde logische server toevoegen.

1. In de blade voor de groep, onder **elastische databases** klikt u op **pool configureren**.

    ![Klik op pool configureren][1]

2. In de **pool configureren** blade, klikt u op **toevoegen aan groep**.

    ![Klik op toevoegen aan groep](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. In de **databases toevoegen** blade, selecteer de database of databases toevoegen aan de groep. Klik vervolgens op **Selecteer**.

    ![Selecteer de databases toevoegen](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    De **pool configureren** blade bevat nu de database die u hebt geselecteerd om te worden toegevoegd, klikt u met de status ingesteld op **in behandeling**.

    ![In behandeling pool-toevoegingen](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. In de **blade van de pool configureren**, klikt u op **opslaan**.

    ![Op Opslaan klikken](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>Een database verplaatst buiten een elastische pool

1. In de **pool configureren** blade, selecteer de database of databases verwijderen.

    ![databases weergeven](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. Klik op **verwijderen uit groep**.

    ![databases weergeven](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    De **pool configureren** blade bevat nu de database die u hebt geselecteerd om te worden verwijderd met de status ingesteld op **in behandeling**.

    ![voorbeeld database toevoegen en verwijderen](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. In de **blade van de pool configureren**, klikt u op **opslaan**.

    ![Op Opslaan klikken](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>Instellingen van de prestaties van een elastische groep wijzigen

Als u het Resourcegebruik van een elastische pool bewaken, ontdekt u dat bepaalde aanpassingen nodig zijn. De groep moet mogelijk een wijziging in de limieten van de prestaties of de opslag. Mogelijk wilt u de database-instellingen in de groep wijzigen. U kunt de installatie van de groep wijzigen op elk gewenst moment om op te halen van de beste balans van prestaties en kosten. Zie [wanneer moet een elastische pool worden gebruikt?](sql-database-elastic-pool.md) voor meer informatie.

De limieten voor edtu's of opslag per groep en edtu's per database wijzigen:

1. Open de **pool configureren** blade.

    Onder **elastische groepsinstellingen**, gebruik de schuifregelaar voor de Groepsinstellingen wijzigen.

    ![Resourcegebruik van de elastische groep](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Wanneer de instelling wordt gewijzigd, worden de weergave de geschatte maandelijkse kosten van de wijziging.

    ![Bijwerken van een elastische pool en nieuwe maandelijkse kosten](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>Latentie van bewerkingen van de elastische groep
* Doorgaans wijzigen van de edtu min's per database of max edtu's per database is voltooid in de 5 minuten of minder.
* Het wijzigen van de edtu's per groep, is afhankelijk van de totale hoeveelheid ruimte die wordt gebruikt door alle databases in de groep. Wijzigingen duren gemiddeld 90 minuten of minder per 100 GB. Bijvoorbeeld, als de totale ruimte gebruikt door alle databases in de pool is 200 GB, dan is de verwachte latentie voor het wijzigen van de groeps-eDTU per pool drie uur of minder.

## <a name="next-steps"></a>Volgende stappen

- Om te begrijpen wat een elastische groep is, Zie [elastische pool in SQL-Database](sql-database-elastic-pool.md).
- Zie voor instructies over het gebruik van elastische pools [prijs- en Prestatieoverwegingen voor elastische pools](sql-database-elastic-pool.md).
- Zie voor het gebruik van elastische taken Transact-SQL-scripts uitvoeren op een willekeurig aantal databases in de pool, [elastische taken overzicht](sql-database-elastic-jobs-overview.md).
- Om te vragen via een willekeurig aantal databases in de groep, Zie [elastische query overzicht](sql-database-elastic-query-overview.md).
- Zie voor transacties een willekeurig aantal databases in de pool [elastische transacties](sql-database-elastic-transactions-overview.md).


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
