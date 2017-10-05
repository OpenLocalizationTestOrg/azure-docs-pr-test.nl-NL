---
title: Azure DB die Cosmos-aanvragen en opslag bewaken | Microsoft Docs
description: Informatie over het bewaken van uw Azure DB die Cosmos-account voor prestatiegegevens, zoals aanvragen en serverfouten, en meetgegevens voor softwaregebruik, zoals opslagverbruik.
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
ms.openlocfilehash: 0ca652d31d6c50124f87916b4486d8279075f106
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Aanvragen, gebruik en opslag van Azure DB die Cosmos controleren
U kunt uw Azure DB die Cosmos-accounts in bewaken de [Azure-portal](https://portal.azure.com/). Beide maatstaven voor prestaties, zoals aanvragen en serverfouten en meetgegevens voor softwaregebruik, zoals opslagverbruik, zijn beschikbaar voor elk Azure DB die Cosmos-account.

Metrische gegevens kunnen worden gecontroleerd op de blade met het Account voor de nieuwe blade metrische gegevens of in de Azure-Monitor.

## <a name="view-performance-metrics-on-the-metrics-blade"></a>Weergave maatstaven voor prestaties op de blade metrische gegevens
1. In de [Azure-portal](https://portal.azure.com/), klikt u op **meer Services**, schuif naar **Databases**, klikt u op **Azure Cosmos DB**, en klik vervolgens op de naam van de Azure DB die Cosmos-account waarvan u wilt weergeven van maatstaven voor prestaties.
2. In het menu resource onder **bewaking**, klikt u op **metrische gegevens**.

De metrische gegevens blade wordt geopend en kunt u de verzameling om te controleren. U kunt bekijken van de beschikbaarheid, aanvragen, doorvoer en opslag metrische gegevens en deze vergelijken met de Azure Cosmos DB serviceovereenkomsten.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>De prestaties van metrische gegevens weergeven met behulp van Azure-bewaking
1. In de [Azure-portal](https://portal.azure.com/), klikt u op **Monitor** in de Snelbalk.
2. Klik in het menu resource **metrische gegevens**.
3. In de **Monitor - metrische gegevens** venster in de **esourcekalenders groep** vervolgkeuzelijst, selecteer de resourcegroep die zijn gekoppeld aan het Azure DB die Cosmos-account dat u wilt bewaken. 
4. In de **Resource** vervolgkeuzelijst, selecteer de database-account om te controleren.
5. In de lijst met **beschikbare metrische gegevens**, selecteert u de metrische gegevens om weer te geven. Gebruik de knop CTRL voor meervoudige selectie. 

    De metrische gegevens worden weergegeven op in de **tekenen** venster. 

## <a name="view-performance-metrics-on-the-account-blade"></a>Weergave maatstaven voor prestaties op de accountblade
1. In de [Azure-portal](https://portal.azure.com/), klikt u op **meer Services**, schuif naar **Databases**, klikt u op **Azure Cosmos DB**, en klik vervolgens op de naam van de Azure DB die Cosmos-account waarvan u wilt weergeven van maatstaven voor prestaties.
2. De **bewaking** lens wordt standaard de volgende tegels weergegeven:
   
   * Totaal aantal aanvragen voor de huidige dag.
   * Opslag gebruikt.
   
   Als wordt weergegeven in de tabel **geen gegevens beschikbaar** en u denkt dat er gegevens in uw database, raadpleegt u de [probleemoplossing](#troubleshooting) sectie.
   
   ![Schermopname van de bewaking lens waarin de aanvragen en het opslaggebruik](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. Klik op de **aanvragen** of **Gebruiksquotum** tegel Hiermee opent u een gedetailleerde **metriek** blade.
4. De **metriek** blade ziet u details over de metrische gegevens die u hebt geselecteerd.  Boven aan de blade wordt een grafiek van aanvragen per uur worden uitgezet en hieronder die tabel waarin de waarden van de aggregatie voor beperkte en totaal aantal aanvragen.  De metrische blade ziet u ook de lijst met waarschuwingen die zijn gedefinieerd, gefilterd op de metrische gegevens die worden weergegeven op de huidige metrische blade (op deze manier hebt u een aantal waarschuwingen, alleen ziet u de relevante waarden die hier wordt gepresenteerd).   
   
   ![Schermafbeelding van de metrische blade waaronder beperkt aanvragen](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-the-portal"></a>Prestaties metrische weergaven in de portal aanpassen
1. Voor het aanpassen van de metrische gegevens die worden weergegeven in een bepaalde grafiek, klikt u op de grafiek om te openen in de **metriek** blade en klik vervolgens op **grafiek bewerken**.  
   ![Schermopname van de besturingselementen metrische blade met grafiek bewerken gemarkeerd](./media/monitor-accounts/madocdb3.png)
2. Op de **grafiek bewerken** blade, er zijn opties voor het wijzigen van de metrische gegevens die worden weergegeven in de grafiek, evenals hun tijdsbereik.  
   ![Schermopname van de blade grafiek bewerken](./media/monitor-accounts/madocdb4.png)
3. Als u wilt wijzigen van de metrische gegevens weergegeven in het gedeelte, eenvoudig kunt selecteren of wissen van de van de beschikbare metrische prestatiegegevens en klik vervolgens op **OK** onderaan de blade.  
4. Als u wilt wijzigen van het tijdsbereik, kies een ander bereik (bijvoorbeeld **aangepaste**), en klik vervolgens op **OK** onderaan de blade.  
   
   ![Schermopname van het tijdsbereik deel van de grafiek bewerken-blade met het invoeren van een aangepaste periode](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-the-portal"></a>Side-by-side grafieken maken in de portal
De Azure Portal kunt u metrische side-by-side-grafieken maken.  

1. Eerst met de rechtermuisknop op de grafiek die u wilt kopiëren en selecteer **aanpassen**.
   
   ![Schermopname van de grafiek Totaal aantal aanvragen met de optie aanpassen gemarkeerd](./media/monitor-accounts/madocdb6.png)
2. Klik op **kloon** in het menu kopiëren van het onderdeel en klik vervolgens op **gedaan aanpassen**.
   
   ![Scherm maken van de grafiek Totaal aantal aanvragen met de kloon en opties voor aanpassen gemarkeerd uitgevoerd](./media/monitor-accounts/madocdb7.png)  

U mag dit onderdeel nu behandelen als andere metrische onderdeel aanpassen van de metrische gegevens en tijdbereik weergegeven in het gedeelte.  Dit doet, ziet u twee verschillende metrische gegevens grafiek side-by-side op hetzelfde moment.  
    ![Schermopname van de grafiek Totaal aantal aanvragen en de nieuwe totaal aantal aanvragen voorbij uur grafiek](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-the-portal"></a>Stel waarschuwingen in de portal
1. In de [Azure-portal](https://portal.azure.com/), klikt u op **meer Services**, klikt u op **Azure Cosmos DB**, en klik vervolgens op de naam van de Azure DB die Cosmos-account waarvoor u wil instellen om metrische prestatiewaarschuwingen.
2. Klik in het menu resource **waarschuwingsregels** om de regels voor waarschuwingen-blade te openen.  
   ![Schermopname van de waarschuwing regels geselecteerd](./media/monitor-accounts/madocdb10.5.png)
3. In de **waarschuwing regels** blade, klikt u op **waarschuwing toevoegen**.  
   ![Schermafbeelding van het tabblad regels voor waarschuwingen met de knop van het type waarschuwing toevoegen gemarkeerd](./media/monitor-accounts/madocdb11.png)
4. In de **een waarschuwingsregel toevoegen** blade opgeven:
   
   * De naam van de waarschuwingsregel die u instelt.
   * Een beschrijving van de nieuwe waarschuwingsregel.
   * De metrische gegevens voor de waarschuwingsregel.
   * De voorwaarde, drempelwaarde en periode om te bepalen wanneer de waarschuwing wordt geactiveerd. Bijvoorbeeld, een server aantal fouten groter is dan 5 in de afgelopen 15 minuten.
   * Hiermee wordt aangegeven of de servicebeheerder en coadministrators per e-mail verzonden worden wanneer de waarschuwing wordt geactiveerd.
   * Extra e-mailadressen voor meldingen van waarschuwingen.  
     ![Schermopname van de toevoegen een waarschuwingsregel-blade](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>Azure Cosmos DB via programmacode bewaken
De account niveau metrische gegevens beschikbaar zijn in de portal, zoals account opslag gebruik en totaal aantal aanvragen, zijn niet beschikbaar via de DocumentDB APIs. U kunt echter gebruiksgegevens op het niveau verzameling ophalen met behulp van de DocumentDB APIs. Voor het ophalen van gegevens te verzamelen niveau het volgende doen:

* De REST-API gebruiken [GET uitvoeren op de verzameling](https://msdn.microsoft.com/library/mt489073.aspx). De quota's en gebruik van informatie voor de verzameling wordt de x-ms-resource-quota- en x-ms--Resourcegebruik aangegeven in het antwoord geretourneerd.
* De .NET SDK, gebruikt de [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) methode retourneert een [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) die bevat een aantal eigenschappen van gebruik, zoals **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**, en meer.

Voor toegang tot aanvullende gegevens, gebruikt de [Azure Monitor SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights). Beschikbare metrische definities kunnen worden opgehaald door aan te roepen:

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

Query's voor het ophalen van afzonderlijke metrische gegevens gebruik de volgende notatie:

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

Zie voor meer informatie [bij het ophalen van metrische gegevens voor resources via de REST-API van Azure Monitor](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/). Houd er rekening mee dat de "Azure Inights" is gewijzigd 'Azure Monitor'.  Dit blogbericht verwijst naar de naam van de oudere.

## <a name="troubleshooting"></a>Problemen oplossen
Als uw bewaking tegels weergegeven de **geen gegevens beschikbaar** bericht en u onlangs aanvragen of gegevens toegevoegd aan de database, kunt u de tegel om de recente informatie over het gebruik weer te geven.

### <a name="edit-a-tile-to-refresh-current-data"></a>Bewerken van een tegel om huidige gegevens te vernieuwen
1. Klik op de grafiek te openen voor het aanpassen van de metrische gegevens die worden weergegeven in een bepaald deel de **metriek** blade en klik vervolgens op **grafiek bewerken**.  
   ![Schermopname van de besturingselementen metrische blade met grafiek bewerken gemarkeerd](./media/monitor-accounts/madocdb3.png)
2. Op de **grafiek bewerken** blade in de **tijdsbereik** sectie, klikt u op **voorbij uur**, en klik vervolgens op **OK**.  
   ![Schermopname van de blade grafiek bewerken met het afgelopen uur zijn geselecteerd](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. Uw tegel moet nu worden vernieuwd met uw huidige gegevens en informatie over het gebruik.  
   ![Schermopname van het bijgewerkte totaal aantal aanvragen in het verleden uur tegel](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over de capaciteitsplanning van Azure Cosmos DB, de [Azure Cosmos DB capaciteit planner Rekenmachine](https://www.documentdb.com/capacityplanner).

