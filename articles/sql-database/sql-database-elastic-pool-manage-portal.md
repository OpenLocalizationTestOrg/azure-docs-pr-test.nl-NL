---
title: 'Azure-portal: maken en beheren van een elastische pool SQL Database | Microsoft Docs'
description: Ontdek hoe toouse hello Azure-portal en SQL-Database ingebouwde intelligentie toomanage, bewaken en de prestaties van een schaalbare elastische pool toooptimize-database het juiste formaat en kosten beheren.
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
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a>Maken en beheren van een elastische groep met hello Azure-portal
Dit onderwerp leest u hoe toocreate en beheren van schaalbare [elastische pools](sql-database-elastic-pool.md) Hello Azure-portal. U kunt ook maken en beheren van een Azure elastische groep met [PowerShell](sql-database-elastic-pool-manage-powershell.md), Hallo REST-API of [C#](sql-database-elastic-pool-manage-csharp.md). U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

## <a name="create-an-elastic-pool"></a>Elastische pool maken 

Er zijn twee manieren kunt u een elastische pool. U kunt dit doen vanaf het begin als u Hallo groep instellingen u wilt weet, of met een aanbeveling van Hallo-service. SQL-Database beschikt over ingebouwde intelligentie die raadt aan om een elastische groep is ingesteld als het kostenefficiënte op basis van Hallo voorbij gebruik telemetrie van uw databases.

U kunt meerdere groepen maken op een server, maar u kunt geen databases van verschillende servers toevoegen in Hallo dezelfde groep. 

> [!NOTE]
> Elastische pools zijn algemeen beschikbaar in alle Azure-regio's, behalve in West-India, waar deze zich momenteel in de previewfase bevinden.  Algemene beschikbaarheid van elastische pools in deze regio zal zo snel mogelijk plaatsvinden.
>

### <a name="step-1-create-an-elastic-pool"></a>Stap 1: Een elastische pool maken

Een elastische pool te maken van een bestaand **server** blade in de portal Hallo Hallo gemakkelijkste manier toomove bestaande databases in een elastische groep is.

> [!NOTE]
> U kunt ook een elastische pool maken door te zoeken naar **elastische SQL-groep** in Hallo **Marketplace** of klikken op **+ toevoegen** in Hallo **SQL elastische pools**blade bladeren. U zijn kunt toospecify een nieuwe of bestaande server via deze werkstroom van toepassingen.
>
>

1. In Hallo [Azure-portal](http://portal.azure.com/), klikt u op **meer services**  **>**  **SQL-servers**, en klik vervolgens op Hallo-server die Hallo bevat databases die u wilt dat tooadd tooan elastische pool.
2. Klik op **Nieuwe groep**.

    ![Groep tooa server toevoegen](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **-OF-**

    Mogelijk ziet u een bericht weergegeven dat er aanbevolen elastische pools voor Hallo-server. Hallo-bericht toosee Hallo aanbevolen pools voor op basis van historische database gebruik telemetrie, klikt u op en klikt u op Hallo laag toosee voor meer informatie en Hallo groep aanpassen. Zie [aanbevelingen voor Pools begrijpen](#understand-elastic-pool-recommendations) verderop in dit onderwerp voor hoe Hallo aanbeveling wordt gesteld.

    ![aanbevolen groep](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. Hallo **elastische pool** blade wordt weergegeven waarin u Hallo-instellingen opgeven voor uw toepassingen. Als u hebt geklikt **nieuwe pool** in de vorige stap Hallo Hallo prijscategorie is **standaard** standaard en geen databases geselecteerd. U kunt een lege groep maken of een set van bestaande databases van die server toomove in Hallo van toepassingen opgeven. Als u een aanbevolen pool maakt, Hallo aanbevolen prijscategorie, prestatie-instellingen en lijst met databases vooraf worden ingevuld, maar u kunt ze nog steeds wijzigen.

    ![Elastische groep configureren](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Geef een naam voor de elastische groep Hallo of laat het veld als Hallo standaard.

### <a name="step-2-choose-a-pricing-tier"></a>Stap 2: kies een prijscategorie

Hallo bepaalt prijscategorie van pool Hallo functies beschikbaar toohello elastics in Hallo pool en Hallo maximumaantal edtu's (eDTU MAX) en opslag (GB) beschikbare tooeach database. Zie voor meer informatie de Servicecategorieën.

toochange hello prijscategorie voor Hallo-groep, klikt u op **prijscategorie**, klikt u op de prijscategorie die u wilt en klik vervolgens op Hallo **Selecteer**.

> [!IMPORTANT]
> Nadat u Hallo prijscategorie kiezen en uw wijzigingen door te klikken op **OK** in de laatste stap hello, niet meer kunnen toochange Hallo prijscategorie van Hallo van toepassingen. toochange Hallo prijscategorie voor een bestaande elastische pool, een elastische pool maken in de gewenste prijscategorie Hallo en Hallo databases toothis nieuwe toepassingen te migreren.
>

![Een prijscategorie selecteren](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a>Stap 3: Hallo pool configureren

Klik na het instellen van Hallo prijscategorie pool configureren Hier voegt u databases, set groepen met edtu's en opslag (GB adresgroep) en waar u Hallo min en max Edtu voor Hallo elastics instellen in de groep Hallo.

1. Klik op **Groep configureren**
2. Hallo-databases u tooadd toohello toepassingen wilt selecteren. Deze stap is optioneel bij het maken van Hallo van toepassingen. Databases kunnen worden toegevoegd nadat Hallo-groep is gemaakt.
    tooadd databases, klik met de **database toevoegen**, klikt u op Hallo databases wilt tooadd en klik vervolgens op Hallo **Selecteer** knop.

    ![Databases toevoegen](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    Hallo-databases waarmee u samenwerkt hebt voldoende gebruikstelemetrie, Hallo **geschat eDTU- en GB-gebruik** grafiek en Hallo **werkelijk eDTU-gebruik** staafdiagram update toohelp maken van configuratie beslissingen te nemen. Bovendien Hallo-service kan bieden u een aanbeveling bericht toohelp u het juiste formaat Hallo van toepassingen. Zie [Dynamische aanbevelingen](#understand-elastic-pool-recommendations).

3. Hallo-opties op Hallo gebruiken **pool configureren** pagina tooexplore instellingen en uw pool te configureren. Zie [limieten elastische pools](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) voor meer informatie over de limieten van elke servicecategorie en Zie [prijs- en Prestatieoverwegingen voor elastische pools](sql-database-elastic-pool.md) voor gedetailleerde richtlijnen voor het juiste formaat een elastische pool. Zie voor meer informatie over de groepsinstellingen [eigenschappen van de elastische groep](sql-database-elastic-pool.md#database-properties-for-pooled-databases).

    ![Elastische groep configureren](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. Klik op **Selecteer** in Hallo **Pool configureren** blade na het wijzigen van instellingen.
5. Klik op **OK** toocreate Hallo van toepassingen.

## <a name="understand-elastic-pool-recommendations"></a>Aanbevelingen voor elastische Pools begrijpen

Hallo SQL Database-service beoordeelt de gebruiksgeschiedenis en beveelt een of meer groepen wanneer deze kosteneffectiever zijn dan het gebruik van individuele databases. Elke aanbeveling wordt geconfigureerd met een unieke subset van Hallo-server-databases die het meest Hallo van toepassingen geschikt.

![aanbevolen groep](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

Hallo groep aanbeveling omvat:

- Een prijscategorie voor Hallo pool (Basic, Standard, Premium of RS Premium)
- De juiste **eDTU’s voor de groep** (ook wel Max eDTU's per groep)
- Hallo **eDTU MAX** en **eDTU Min** per database
- Hallo-lijst met aanbevolen databases voor Hallo van toepassingen

> [!IMPORTANT]
> Hallo service wordt rekening gehouden Hallo afgelopen 30 dagen telemetrie bij het aanbevelen van pools. Voor een database toobe beschouwd als kandidaat voor een elastische pool, moet er ten minste 7 dagen bestaan. Databases die zich al in een elastische pool bevinden, worden niet aanbevolen voor een elastische pool.
>

Hallo service beoordeelt resourcebehoeften en kosteneffectiviteit zwevend Hallo één databases in elke servicelaag naar pools van Hallo dezelfde laag. Alle Standard databases op een server worden bijvoorbeeld beoordeeld op hoe ze in een Standard elastische groep passen. Dit betekent dat het Hallo-service maakt geen cross-aanbevelingen zoals het verplaatsen van een Standard database naar een Premium pool.

Na het toevoegen van databases toohello groep worden aanbevelingen dynamisch gegenereerd op basis van historisch gebruik Hallo Hallo-databases die u hebt geselecteerd. Deze aanbevelingen worden weergegeven in Hallo eDTU- en GB-gebruiksgrafiek en in een banner boven Hallo Hallo **pool configureren** blade. Deze aanbevelingen zijn bedoeld tooassist u bij het maken van een elastische pool geoptimaliseerd voor uw specifieke databases.

![dynamische aanbevelingen](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a>Beheren en controleren van een elastische pool

U kunt hello Azure portal toomonitor gebruiken en een elastische pool en het Hallo-databases in de groep Hallo beheren. Vanuit de portal Hallo kunt u gebruik van een elastische pool en het Hallo-databases binnen die groep Hallo bewaken. U kunt ook een aantal wijzigingen tooyour elastische pool en dienen alle wijzigingen op Hallo dezelfde tijd. Deze wijzigingen omvatten toevoegen of verwijderen van databases, elastische pool-instellingen wijzigen of database-instellingen wijzigen.

Hallo volgende afbeelding toont een voorbeeld van de elastische groep. Hallo-weergave bevat:

*  De grafieken voor het brongebruik van Hallo elastische pool en Hallo-databases die zijn opgenomen in de groep Hallo.
*  Hallo **configureren** groep knop toomake toohello elastische pool wordt gewijzigd.
*  Hallo **database maken** knop waarmee een database wordt gemaakt en de huidige elastische pool toohello toegevoegd.
*  Groot aantal databases beheren elastische taken die u helpen door te voeren van Transact-SQL-scripts op alle databases in een lijst.

![Toepassingen weergeven][2]

Het Resourcegebruik, kunt u tooa bepaalde toepassingen toosee gaan. Hallo-groep is standaard geconfigureerde tooshow opslag en het eDTU-gebruik voor Hallo afgelopen uur. Hallo-grafiek kunt geconfigureerde tooshow andere metrische gegevens worden via verschillende tijdvensters.

1. Selecteer een elastische pool toowork met.
2. Onder **elastische Pool bewaking** is een grafiek met het label **Resourcegebruik**. Klik op Hallo-grafiek.

    ![Bewaking van de elastische groep][3]

    Hallo **metriek** blade wordt geopend, waarin een gedetailleerde weergave van Hallo metrische gegevens opgegeven via de opgegeven tijdvenster Hallo.   

    ![Blade met metrische gegevens][9]

### <a name="toocustomize-hello-chart-display"></a>grafiekweergave van toocustomize Hallo

U kunt Hallo grafiek en Hallo metrische blade toodisplay bewerken andere metrische gegevens zoals CPU-percentage, gegevens-IO-percentage en log-IO-percentage gebruikt.

1. Klik op Hallo metrische blade **bewerken**.

    ![Klik op bewerken][6]

2. In Hallo **grafiek bewerken** blade, selecteert u een tijdsbereik (voorbij vandaag de dag, uur of afgelopen week), of klik op **aangepaste** tooselect een datumbereik in Hallo afgelopen twee weken. Hallo grafiektype (staaf- of regel) selecteren en selecteer vervolgens Hallo resources toomonitor.

   > [!Note]
   > Alleen metrische gegevens met dezelfde eenheid kan worden weergegeven in Hallo Hallo grafiek op Hallo dezelfde tijd. Bijvoorbeeld, als u 'eDTU percentage' selecteert kunt vervolgens u alleen selecteren andere metrische gegevens met percentage als eenheid Hallo.
   >

    ![Klik op bewerken](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. Klik vervolgens op **OK**.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Beheren en controleren van de databases in een elastische pool

Afzonderlijke databases kunnen ook worden gecontroleerd voor potentiële problemen.

1. Onder **elastische Database bewaken**, er is een diagram waarin metrische gegevens voor vijf databases. Standaard Hallo diagram toont Hallo bovenste 5 databases in de groep Hallo door gemiddeld eDTU-gebruik in Hallo afgelopen uur. Klik op Hallo-grafiek.

    ![Bewaking van de elastische groep][4]

2. Hallo **Database Resourcegebruik** blade wordt weergegeven. Dit biedt een gedetailleerde weergave van het Databasegebruik Hallo in Hallo van toepassingen. Hallo raster Hallo onder in de blade Hallo gebruikt, kunt u geen databases in Hallo groep toodisplay het gebruik ervan in de grafiek hello (omhoog too5 databases). U kunt ook aanpassen Hallo metrische gegevens en het tijdstip venster wordt weergegeven in de grafiek Hallo door te klikken op **grafiek bewerken**.

    ![Gebruik van de databaseblade resource][8]

### <a name="toocustomize-hello-view"></a>toocustomize hello weergeven

1. In Hallo **Resourcegebruik van de Database** blade, klikt u op **grafiek bewerken**.

    ![Klik op de grafiek bewerken](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. In Hallo **bewerken** blade grafiek, selecteert u een tijdsbereik (voorbij uur of afgelopen 24 uur) of klik op **aangepaste** tooselect een andere dag in Hallo voorbij toodisplay 2 weken.

    ![Klik op aangepast](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Klik op Hallo **vergelijken databases door** dropdown tooselect verschillende metrische toouse bij het vergelijken van databases.

    ![Hallo grafiek bewerken](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect databases toomonitor

In de lijst met de Hallo database in Hallo **Database Resourcegebruik** blade kunt u bepaalde databases vinden door te zoeken door Hallo pagina's in de lijst Hallo of door in het Hallo-naam van een database te typen. Hallo selectievakje tooselect Hallo database gebruiken.

![Zoeken naar databases toomonitor][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Een elastische pool waarschuwing tooan resource toevoegen

Regels tooan elastische groep die e-mail verzenden toopeople of waarschuwing tekenreeksen tooURL eindpunten wanneer Hallo elastische pool treffers een drempelwaarde voor overbenutting die u hebt ingesteld, kunt u toevoegen.

**een waarschuwing tooany resource tooadd:**

1. Klik op Hallo **Resourcegebruik** grafiek tooopen Hallo **metriek** blade klikt u op **waarschuwing toevoegen**, en vult u de informatie in Hallo Hallo **een waarschuwing toevoegen regel** blade (**Resource** automatisch ingesteld toobe Hallo toepassingen waarmee u werkt).
2. Typ een **naam** en **beschrijving** die Hallo waarschuwing tooyou en Hallo ontvangers identificeert.
3. Kies een **metriek** dat u wilt dat tooalert uit Hallo-lijst.

    Hallo diagram toont dynamisch Resourcegebruik voor die metrische toohelp die u kiest een drempelwaarde.

4. Kies een **voorwaarde** (groter dan maximaal, enzovoort) en een **drempelwaarde**.
5. Kies een **periode** hoelang Hallo metriek regel moet worden voldaan voordat de waarschuwing Hallo-triggers.
6. Klik op **OK**.

Zie voor meer informatie [waarschuwingen van de SQL-Database maken in Azure portal](sql-database-insights-alerts-portal.md).

## <a name="move-a-database-into-an-elastic-pool"></a>Een database verplaatsen naar een elastische pool

U kunt toevoegen of verwijderen van databases uit een bestaande groep. Hallo-databases kunnen zich in andere toepassingen. U kunt echter alleen toevoegen databases die zijn op Hallo dezelfde logische server.

1. Hallo-blade voor Hallo-toepassingen onder **elastische databases** klikt u op **pool configureren**.

    ![Klik op pool configureren][1]

2. In Hallo **pool configureren** blade, klikt u op **toopool toevoegen**.

    ![Klik op toevoegen toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. In Hallo **databases toevoegen** blade, selecteer Hallo database of databases tooadd toohello van toepassingen. Klik vervolgens op **Selecteer**.

    ![Selecteer de databases tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    Hallo **pool configureren** blade nu een lijst met toobe toegevoegd met de status ervan instellen te geselecteerde database Hallo**in behandeling**.

    ![In behandeling pool-toevoegingen](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. In Hallo **blade van de pool configureren**, klikt u op **opslaan**.

    ![Op Opslaan klikken](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>Een database verplaatst buiten een elastische pool

1. In Hallo **pool configureren** blade, selecteer Hallo database of databases tooremove.

    ![databases weergeven](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. Klik op **verwijderen uit groep**.

    ![databases weergeven](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    Hallo **pool configureren** blade nu een lijst met toobe verwijderd met de status ervan instellen te geselecteerde database Hallo**in behandeling**.

    ![voorbeeld database toevoegen en verwijderen](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. In Hallo **blade van de pool configureren**, klikt u op **opslaan**.

    ![Op Opslaan klikken](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>Instellingen van de prestaties van een elastische groep wijzigen

Tijdens het controleren van Resourcegebruik Hallo van een pool voor elastische ontdekt u dat bepaalde aanpassingen nodig zijn. Hallo-groep moet mogelijk een wijziging in Hallo prestaties of de opslag limieten. Mogelijk wilt u toochange Hallo database-instellingen in Hallo van toepassingen. U kunt setup Hallo van Hallo van toepassingen die op elk moment tooget Hallo beste balans van prestaties en kosten wijzigen. Zie [wanneer moet een elastische pool worden gebruikt?](sql-database-elastic-pool.md) voor meer informatie.

toochange hello edtu's of opslag limieten per groep van toepassingen en edtu's per database:

1. Open Hallo **pool configureren** blade.

    Onder **elastische groepsinstellingen**, ofwel groepsinstellingen schuifregelaar toochange hello gebruiken.

    ![Resourcegebruik van de elastische groep](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Wanneer Hallo-instelling wordt gewijzigd, ziet u Hallo weergave Hallo Geschatte maandelijkse kosten van Hallo wijzigen.

    ![Bijwerken van een elastische pool en nieuwe maandelijkse kosten](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>Latentie van bewerkingen van de elastische groep
* Hallo min edtu's per database of max edtu's per database doorgaans wijzigen is voltooid in de 5 minuten of minder.
* Hallo edtu's per groep wijzigen hangt af van de totale hoeveelheid ruimte die wordt gebruikt door alle databases in de groep Hallo Hallo. Wijzigingen duren gemiddeld 90 minuten of minder per 100 GB. Bijvoorbeeld, als de totale ruimte hello worden gebruikt door alle databases in de groep Hallo is 200 GB en vervolgens Hallo verwachte latentie voor het wijzigen van Hallo groeps-eDTU per pool is drie uur of minder.

## <a name="next-steps"></a>Volgende stappen

- welke een elastische groep is, Zie toounderstand [elastische pool in SQL-Database](sql-database-elastic-pool.md).
- Zie voor instructies over het gebruik van elastische pools [prijs- en Prestatieoverwegingen voor elastische pools](sql-database-elastic-pool.md).
- toouse elastische taken toorun Transact-SQL-scripts uitvoeren op een willekeurig aantal databases in de groep hello, Zie [elastische taken overzicht](sql-database-elastic-jobs-overview.md).
- tooquery via een willekeurig aantal databases in de groep hello, Zie [elastische query overzicht](sql-database-elastic-query-overview.md).
- Zie voor transacties een willekeurig aantal databases in de groep hello, [elastische transacties](sql-database-elastic-transactions-overview.md).


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
