---
title: aaaMonitor Azure Cosmos DB aanvragen en opslag | Microsoft Docs
description: Meer informatie over hoe toomonitor uw Cosmos Azure DB administratief prestatiegegevens, zoals aanvragen en serverfouten, en meetgegevens voor softwaregebruik, zoals opslagverbruik.
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: aea029d10717236a573a080dab9d06d87f97f318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Aanvragen, gebruik en opslag van Azure DB die Cosmos controleren
U kunt uw Azure DB die Cosmos-accounts in Hallo bewaken [Azure-portal](https://portal.azure.com/). Beide maatstaven voor prestaties, zoals aanvragen en serverfouten en meetgegevens voor softwaregebruik, zoals opslagverbruik, zijn beschikbaar voor elk Azure DB die Cosmos-account.

Metrische gegevens kunnen worden gecontroleerd op Hallo accountblade nieuwe metrische gegevens blade hello, of in de Azure-Monitor.

## <a name="view-performance-metrics-on-hello-metrics-blade"></a>Weergave maatstaven voor prestaties op Hallo metrische gegevens blade
1. In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **meer Services**, te schuiven**Databases**, klikt u op **Azure Cosmos DB**, en klik op de naam Hallo Hallo Azure DB Cosmos-account waarvoor u maatstaven voor prestaties tooview wilt.
2. In het menu Hallo resource onder **bewaking**, klikt u op **metrische gegevens**.

Hallo metrische gegevens blade wordt geopend en u Hallo verzameling tooreview kunt selecteren. U kunt metrische gegevens voor beschikbaarheid, aanvragen, doorvoer en opslag bekijken en deze vergelijken met de toohello Azure Cosmos DB Sla's.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>De prestaties van metrische gegevens weergeven met behulp van Azure-bewaking
1. In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **Monitor** op Hallo Snelbalk.
2. Hallo resource menu en klik op **metrische gegevens**.
3. In Hallo **Monitor - metrische gegevens** in Hallo venster **esourcekalenders groep** vervolgkeuzelijst, selecteer Hallo resourcegroep hello Azure DB die Cosmos-account dat u toomonitor wilt gekoppeld. 
4. In Hallo **Resource** vervolgkeuzelijst, selecteer Hallo database account toomonitor.
5. In de lijst met Hallo **beschikbare metrische gegevens**, Hallo metrische gegevens toodisplay selecteren. Gebruik Hallo CTRL knop toomulti selecteren. 

    De metrische gegevens worden weergegeven op in Hallo **tekenen** venster. 

## <a name="view-performance-metrics-on-hello-account-blade"></a>De prestaties van metrische gegevens weergeven over blade Hallo-account
1. In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **meer Services**, te schuiven**Databases**, klikt u op **Azure Cosmos DB**, en klik op de naam Hallo Hallo Azure DB Cosmos-account waarvoor u maatstaven voor prestaties tooview wilt.
2. Hallo **bewaking** lens Hallo tegels standaard na wordt weergegeven:
   
   * Totaal aantal aanvragen voor de huidige dag Hallo.
   * Opslag gebruikt.
   
   Als wordt weergegeven in de tabel **geen gegevens beschikbaar** en u denkt dat er gegevens in uw database, raadpleegt u Hallo [probleemoplossing](#troubleshooting) sectie.
   
   ![Schermopname van Hallo bewaking lens waarin Hallo aanvragen en Hallo opslaggebruik](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. Te klikken op Hallo **aanvragen** of **Gebruiksquotum** tegel Hiermee opent u een gedetailleerde **metriek** blade.
4. Hallo **metriek** blade ziet u details over Hallo metrische gegevens die u hebt geselecteerd.  Op Hallo bovenaan de blade Hallo is wordt een grafiek van aanvragen uitgezet per uur en hieronder die tabel waarin de waarden van de aggregatie voor beperkte en totaal aantal aanvragen.  Hallo metrische blade toont ook Hallo lijst met waarschuwingen die zijn gedefinieerd, gefilterde toohello metrische gegevens die worden weergegeven op de huidige metrische blade Hallo (op deze manier hebt u een aantal waarschuwingen, alleen ziet u Hallo relevante waarden die hier wordt gepresenteerd).   
   
   ![Schermafbeelding van metrische Hallo-blade waaronder beperkt aanvragen](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-hello-portal"></a>Metrische prestatieweergaven in Hallo portal aanpassen
1. toocustomize hello metrische gegevens die worden weergegeven in een bepaalde grafiek, klikt u op Hallo grafiek tooopen in Hallo **metriek** blade en klik vervolgens op **grafiek bewerken**.  
   ![Schermopname van Hallo metrische blade besturingselementen, met grafiek bewerken gemarkeerd](./media/monitor-accounts/madocdb3.png)
2. Op Hallo **grafiek bewerken** blade, er zijn opties toomodify Hallo metrische gegevens die worden weergegeven in de grafiek hello, evenals hun tijdsbereik.  
   ![Schermopname van Hallo grafiek bewerken blade](./media/monitor-accounts/madocdb4.png)
3. toochange hello metrische gegevens weergegeven in Hallo-deel eenvoudig kunt selecteren of wissen Hallo beschikbaar prestatiewaarden en klik vervolgens op **OK** Hallo Hallo blade onderaan in.  
4. toochange hello tijdbereik, kiest u een ander bereik (bijvoorbeeld **aangepaste**), en klik vervolgens op **OK** Hallo Hallo blade onderaan in.  
   
   ![Schermopname van Hallo tijdsbereik deel van Hallo grafiek bewerken blade weergeeft hoe tooenter een aangepaste periode](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-hello-portal"></a>Side-by-side grafieken maken in Hallo-portal
Hello Azure Portal kunt u toocreate side-by-side metrische grafieken.  

1. Eerst met de rechtermuisknop op Hallo grafiek gewenste toocopy en selecteer **aanpassen**.
   
   ![Schermopname van Hallo totaal aantal aanvragen grafiek met de optie aanpassen Hallo gemarkeerd](./media/monitor-accounts/madocdb6.png)
2. Klik op **kloon** op Hallo van menu toocopy Hallo onderdeel en klik vervolgens op **gedaan aanpassen**.
   
   ![Scherm geschoten van Hallo totaal aantal aanvragen grafiek Hello kloon en opties voor aanpassen gemarkeerd uitgevoerd](./media/monitor-accounts/madocdb7.png)  

U mag dit deel nu behandelen als andere metrische onderdeel Hallo metrische gegevens en tijdbereik weergegeven in Hallo deel aanpassen.  Dit doet, ziet u twee verschillende metrische gegevens grafiek side-by-side op Hallo hetzelfde moment.  
    ![Schermopname van het Hallo-totaal aantal aanvragen grafiek en nieuwe totaal aantal aanvragen dat uit het verleden uur grafiek Hallo](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-hello-portal"></a>Stel waarschuwingen in Hallo-portal
1. In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **meer Services**, klikt u op **Azure Cosmos DB**, en klik vervolgens op Hallo-naam van hello Azure Cosmos DB account waarvoor u toosetup wilt metrische prestatiewaarschuwingen.
2. Hallo resource menu en klik op **waarschuwingsregels** tooopen Hallo waarschuwingsregels blade.  
   ![Schermopname van het Hallo waarschuwing regels geselecteerd](./media/monitor-accounts/madocdb10.5.png)
3. In Hallo **waarschuwing regels** blade, klikt u op **waarschuwing toevoegen**.  
   ![Schermopname van Hallo waarschuwingsregels blade Hallo waarschuwing toevoegen knop gemarkeerd](./media/monitor-accounts/madocdb11.png)
4. In Hallo **een waarschuwingsregel toevoegen** blade opgeven:
   
   * Hallo-naam van de waarschuwingsregel Hallo die u instelt.
   * Een beschrijving van de nieuwe waarschuwingsregel Hallo.
   * Hallo metrische gegevens voor de waarschuwingsregel Hallo.
   * Hallo voorwaarde drempelwaarde en periode om te bepalen wanneer Hallo waarschuwing wordt geactiveerd. Bijvoorbeeld, een server aantal fouten groter is dan 5 via Hallo afgelopen 15 minuten.
   * Hiermee wordt aangegeven of Hallo servicebeheerder en coadministrators worden per e-mail verzonden wanneer het Hallo-waarschuwing wordt geactiveerd.
   * Extra e-mailadressen voor meldingen van waarschuwingen.  
     ![Schermopname van het Hallo toevoegen een blade waarschuwingsregel](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>Azure Cosmos DB via programmacode bewaken
Hallo account niveau meetgegevens beschikbaar zijn in de portal hello, zoals opslag account gebruik en totaal aantal aanvragen zijn niet beschikbaar via Hallo DocumentDB APIs. U kunt echter gebruiksgegevens op niveau van de verzameling Hallo ophalen met behulp van Hallo DocumentDB APIs. de niveau Verzamelingsgegevens tooretrieve, Hallo te volgen:

* toouse hello REST API, [GET uitvoeren op Hallo verzameling](https://msdn.microsoft.com/library/mt489073.aspx). Hallo quota en het gebruik informatie voor de verzameling van Hallo wordt Hallo x-ms-resource-quota en x-ms--Resourcegebruik kopteksten in Hallo antwoord geretourneerd.
* toouse hello .NET SDK gebruiken Hallo [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) methode retourneert een [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) die bevat een aantal eigenschappen van gebruik, zoals  **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**, en meer.

aanvullende gegevens tooaccess, gebruik Hallo [Azure Monitor SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights). Beschikbare metrische definities kunnen worden opgehaald door aan te roepen:

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

Query's tooretrieve afzonderlijke metrische gegevens gebruik Hallo volgende indeling:

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

Zie voor meer informatie [bij het ophalen van metrische gegevens voor resources via hello Azure Monitor REST-API](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/). Houd er rekening mee dat de "Azure Inights" is gewijzigd 'Azure Monitor'.  Dit blogbericht verwijst toohello oudere naam.

## <a name="troubleshooting"></a>Problemen oplossen
Als uw bewaking tegels weergegeven Hallo **geen gegevens beschikbaar** bericht en u onlangs aanvragen of gegevens toohello-database toegevoegd, kunt u Hallo tegel tooreflect Hallo recente informatie over het gebruik.

### <a name="edit-a-tile-toorefresh-current-data"></a>Een tegel toorefresh huidige gegevens bewerken
1. toocustomize hello metrische gegevens die worden weergegeven in een bepaald gedeelte, klikt u op Hallo grafiek tooopen hello **metriek** blade en klik vervolgens op **grafiek bewerken**.  
   ![Schermopname van Hallo metrische blade besturingselementen, met grafiek bewerken gemarkeerd](./media/monitor-accounts/madocdb3.png)
2. Op Hallo **grafiek bewerken** blade in Hallo **tijdsbereik** sectie, klikt u op **voorbij uur**, en klik vervolgens op **OK**.  
   ![Schermopname van Hallo grafiek bewerken blade met het afgelopen uur zijn geselecteerd](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. Uw tegel moet nu worden vernieuwd met uw huidige gegevens en informatie over het gebruik.  
   ![Schermopname van Hallo bijgewerkt totaal aantal aanvragen in het verleden uur tegel](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Azure Cosmos DB plannen van capaciteit, Zie Hallo [Azure Cosmos DB capaciteit planner Rekenmachine](https://www.documentdb.com/capacityplanner).

