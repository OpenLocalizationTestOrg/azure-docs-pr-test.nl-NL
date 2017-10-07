---
title: aaaCreate een webtaak .NET in Azure App Service | Microsoft Docs
description: Maak een app met meerdere lagen met ASP.NET MVC en Azure. Hallo front end wordt uitgevoerd in een web-app in Azure App Service en Hallo back-end wordt uitgevoerd als een webtaak. Hallo app gebruikmaakt van Entity Framework, SQL-Database en Azure storage-wachtrijen en blobs.
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Een .NET-webtaak maken in Azure App Service
Deze zelfstudie laat zien hoe toowrite code voor een eenvoudige ASP.NET MVC 5 toepassing met meerdere lagen die gebruikmaakt van Hallo [WebJobs SDK](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

doel van Hallo Hallo [WebJobs SDK](websites-webjobs-resources.md) is toosimplify Hallo code voor algemene taken die een webtaak schrijven, zoals beeldverwerking, wachtrijbewerkingen, RSS aggregatie, onderhouden van bestanden uitvoeren kunt en e-mailberichten verzenden. Hallo WebJobs SDK bevat ingebouwde functies voor het werken met Azure Storage en Service Bus, voor het plannen van taken en het afhandelen van fouten en voor veel andere veelvoorkomende scenario's. Bovendien heeft toobe extensible ontworpen en er is een [open-source-opslagplaats voor uitbreidingen](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Hallo-voorbeeldtoepassing is een bulletinboard voor advertenties. Gebruikers kunnen uploaden afbeeldingen voor advertenties en een back-end-proces Hallo installatiekopieën toothumbnails geconverteerd. pagina ad Hallo toont Hallo miniaturen en Hallo ad detailpagina toont Hallo-afbeelding. Hier volgt een schermafbeelding:

![Advertentielijst](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

Deze voorbeeldtoepassing werkt met [Azure wachtrijen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) en [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). Hallo zelfstudie laat zien hoe Hallo toodeploy toepassing te[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Vereisten
Hallo zelfstudie wordt ervan uitgegaan dat u weet hoe toowork met [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projecten in Visual Studio.

Hallo-zelfstudie oorspronkelijk is geschreven voor Visual Studio 2013, maar kan worden gebruikt met latere versies van Visual Studio. Als u van Visual Studio 2015 of 2017 gebruikmaakt, noteert u voordat u de toepassing hello lokaal uitvoeren, moet u de Hallo wijzigen `Data Source` deel van het SQL Server LocalDB-verbindingsreeks Hallo in Hallo Web.config en App.config-bestanden van `Data Source=(localdb)\v11.0` te`Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>Deze zelfstudie, moet u een Azure-account toocomplete hebben:
>
> * U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): U ontvangt tegoed dat u tootry uit betaalde Azure-services kunt en zelfs nadat ze zijn gebruikt, kunt u Hallo account houden en gratis Azure-services, zoals Websites gebruiken. Uw creditcard wordt nooit worden in rekening gebracht, tenzij u expliciet de instellingen wijzigen en vraag toobe in rekening gebracht.
> * U kunt [maandelijkse Azure-krediet voor Visual Studio-abonnees activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): uw abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.
>
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
>
>

## <a id="learn"></a>Wat u leert
Hallo-zelfstudie laat zien hoe toodo Hallo volgende taken:

* Computer klaarmaken voor het ontwikkelen van Azure inschakelen door het hello Azure SDK installeren (alleen voor Visual Studio 2013 en 2015 gebruikers).
* Maak een project-consoletoepassing die automatisch wordt geïmplementeerd als een webtaak Azure wanneer u de bijbehorende Hallo-webproject implementeert.
* Een WebJobs SDK back-end lokaal op de ontwikkelcomputer Hallo testen.
* Publiceer een toepassing met een API-back-end tooa web-app in App Service.
* Bestanden uploaden en op te slaan in hello Azure Blob-service.
* Hello Azure WebJobs SDK toowork gebruiken met Azure Storage-wachtrijen en blobs.

## <a id="contosoads"></a>Toepassingsarchitectuur
Hallo-voorbeeldtoepassing gebruikt Hallo [wachtrijgerichte werkpatroon](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff load Hallo CPU-intensief werk van het maken van miniatuurweergaven tooa back-end-proces.

Hallo app slaat de advertenties in een SQL-database, met behulp van Entity Framework Code First toocreate Hallo tabellen en toegang tot Hallo gegevens. Voor elke advertentie slaat Hallo database twee URL's: één voor de afbeelding Hallo en één voor Hallo miniatuur.

![Advertentietabel](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

Wanneer een gebruiker een installatiekopie, het Hallo-web-app uploadt, slaat Hallo-installatiekopie in een [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), en Hallo ad informatie opslaat in de database Hallo met een URL die toohello blob verwijst. AT Hallo dezelfde tijd, wordt een bericht tooan Azure-wachtrij geschreven. Hallo in een back-end-proces uitgevoerd als een webtaak Azure WebJobs SDK polls Hallo wachtrij voor nieuwe berichten. Wanneer een nieuw bericht wordt weergegeven, Hallo webtaak maakt een miniatuur voor de betreffende afbeelding en updates Hallo miniaturen URL databaseveld voor de advertentie. Hier volgt een diagram toont de wisselwerking tussen onderdelen van de toepassing hello Hallo:

![Architectuur van Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
Hallo zelfstudie instructies gelden tooAzure SDK voor .NET 2.7.1 of hoger.

## <a id="storage"></a>Een Azure Storage-account maken
Een Azure-opslagaccount biedt resources voor het opslaan van wachtrij en de blob-gegevens in de cloud Hallo. Dit wordt ook gebruikt door Hallo WebJobs SDK toostore-logboekgegevens voor Hallo-dashboard.

In een echte toepassing maakt u meestal afzonderlijke accounts voor toepassingsgegevens versus logboekgegevens en afzonderlijke accounts voor testgegevens versus productiegegevens. Voor deze zelfstudie gebruikt u slechts één account.

1. Open Hallo **Server Explorer** venster in Visual Studio.
2. Klik met de rechtermuisknop Hallo **Azure** knooppunt en klik vervolgens op **tooMicrosoft Azure-abonnement verbinden...** .
   
   ![Verbinding maken met tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Meld u aan met uw Azure-referenties.
4. Met de rechtermuisknop op **opslag** onder hello Azure knooppunt en klik vervolgens op **Storage-Account maken**.
   
   ![Storage-Account maken](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. In Hallo **Storage-Account maken** dialoogvenster, voer een naam voor het Hallo-opslagaccount.

    Hallo-naam moet uniek zijn (geen Azure storage-account kan Hallo hebben dezelfde naam). Als het Hallo-naam die u invoert, wordt al gebruikt, krijgt u een kans toochange deze.

    Hallo URL tooaccess uw storage-account worden *{name}*. core.windows.net.
6. Set Hallo **regio of Affiniteitsgroep** vervolgkeuzelijst toohello regio dichtstbijzijnde tooyou.

    Deze instelling bepaalt u welke Azure-datacenter fungeert als host voor uw opslagaccount. Voor deze zelfstudie won't uw keuze maakt geen merkbaar verschil. Voor een productie-web-app, wilt u echter uw webserver en uw storage-account toobe in Hallo dezelfde regio toominimize latentie en gegevens uitgaande kosten. Hallo-web-app (die u later maken) datacenter moet zo dicht mogelijk toohello browsers Hallo web-app openen in volgorde toominimize latentie.
7. Set Hallo **replicatie** vervolgkeuzelijst te**lokaal redundante**.

    Wanneer geo-replicatie is ingeschakeld voor een opslagaccount, is Hallo opgeslagen inhoud gerepliceerde tooa secundair datacenter tooenable failover toothat locatie in het geval van een noodgeval op Hallo primaire locatie. Geo-replicatie kan extra kosten met zich meebrengen. Voor test- en -accounts in het algemeen niet de bedoeling toopay voor geo-replicatie. Zie [Een opslagaccount maken, beheren of verwijderen](../storage/common/storage-create-storage-account.md) voor meer informatie.
8. Klik op **Create**.

    ![Nieuw opslagaccount](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>Hallo-toepassing downloaden
1. Downloaden en uitpakken Hallo [voltooide oplossing](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).
2. Start Visual Studio.
3. Van Hallo **bestand** in het menu **openen > Project/oplossing**, gaat u toowhere u Hallo oplossing gedownload en open het oplossingsbestand Hallo.
4. Druk op CTRL + SHIFT + B toobuild Hallo oplossing.

    Standaard herstelt Visual Studio automatisch Hallo NuGet-pakketinhoud die niet is opgenomen in Hallo *.zip* bestand. Als hello-pakketten niet worden hersteld, deze handmatig installeren door te gaan toohello **NuGet-pakketten beheren voor oplossing** dialoogvenster en te klikken op Hallo **herstellen** knop Hallo rechts bovenaan.
5. In **Solution Explorer**, zorg ervoor dat **ContosoAdsWeb** is geselecteerd als opstartproject Hallo.

## <a id="configurestorage"></a>Hallo toepassing toouse uw storage-account configureren
1. Open de toepassing hello *Web.config* bestand in Hallo ContosoAdsWeb-project.

    Hallo-bestand bevat een SQL-verbindingsreeks en een Azure-opslag-verbindingsreeks voor het werken met blobs en wachtrijen.

    Hallo SQL-verbindingsreeks verwijst tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.

    Hallo-verbindingsreeks voor opslag is een voorbeeld van tijdelijke aanduidingen voor Hallo storage account naam en toegangssleutel. U hebt deze vervangen met een verbindingsreeks met Hallo naam en sleutel van uw opslagaccount.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    Hallo-verbindingsreeks voor opslag is standaard de naam AzureWebJobsStorage omdat dat Hallo naam Hallo die webjobs SDK wordt gebruikt. Hallo dezelfde naam hier gebruikt wordt zodat u tooset slechts één gegevensbronwaarde in hello Azure-omgeving hebt.
2. In **Server Explorer**, met de rechtermuisknop op uw opslagaccount onder Hallo **opslag** knooppunt en klik vervolgens op **eigenschappen**.

    ![Klik op Eigenschappen van het Opslagaccount](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. In Hallo **eigenschappen** venster, klikt u op **Opslagaccountsleutels**, en klik vervolgens op Hallo weglatingsteken.

    ![Toegangscodes voor opslag](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Kopiëren Hallo **verbindingsreeks**.

    ![Opslag toegangscodes dialoogvenster](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Vervang Hallo verbindingsreeks voor opslag in Hallo *Web.config* bestand met de Hallo-verbindingsreeks die u zojuist hebt gekopieerd. Zorg ervoor dat u Alles selecteren binnen de aanhalingstekens Hallo maar niet inclusief de aanhalingstekens Hallo voordat u gaat plakken.
6. Open Hallo *App.config* bestand in Hallo ContosoAdsWebJob project.

    Dit bestand heeft twee storage-verbindingsreeksen, één voor toepassingsgegevens en één voor logboekregistratie. U kunt afzonderlijke storage-accounts voor toepassingsgegevens en logboekregistratie en kunt u [meerdere opslagaccounts voor gegevens](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). Voor deze zelfstudie maakt u een één opslagaccount gebruikt. Hallo-verbindingsreeksen hebben tijdelijke aanduidingen voor Hallo opslagaccountsleutels.

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    Standaard zoekt Hallo WebJobs SDK met de naam AzureWebJobsStorage en AzureWebJobsDashboard verbindingsreeksen. Als alternatief kunt u [Hallo verbindingsreeks opslaan, maar u wilt en geef dit door in expliciet toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Beide storage-verbindingsreeksen vervangen door Hallo-verbindingsreeks die u eerder hebt gekopieerd.
8. Sla uw wijzigingen op.

## <a id="run"></a>Hallo-toepassing lokaal uitvoeren
1. toostart hello web frontend toepassing hello, druk op CTRL + F5.

    Hallo standaardbrowser geopend toohello startpagina. (Hallo-webproject wordt uitgevoerd, omdat u deze hebt aangebracht Hallo opstartproject.)

    ![Contoso Ads-startpagina](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. toostart hello webtaak-back-end van de toepassing hello, met de rechtermuisknop op Hallo ContosoAdsWebJob project in **Solution Explorer**, en klik vervolgens op **Debug** > **nieuw exemplaar gestart** .

    Een toepassing consolevenster opent en toont berichtregistratie die aangeeft Hallo WebJobs SDK JobHost object toorun is begonnen.

    ![Toepassing consolevenster weergegeven die backend hello wordt uitgevoerd](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. Klik in uw browser **maken een advertentie**.
4. Voer enkele testgegevens, selecteert u een installatiekopie tooupload en klik vervolgens op **maken**.

    ![De pagina Create](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    Hallo app gaat toohello indexpagina, maar niet wordt weergegeven een miniatuur voor de nieuwe ad Hallo omdat die verwerking nog niet heeft plaatsgevonden.

    Ondertussen na een korte wachten logboekregistratie in een bericht in de toepassing consolevenster Hallo aangegeven dat een wachtrijbericht is ontvangen en is verwerkt.

    ![Toepassing consolevenster weergegeven dat er een wachtrijbericht is verwerkt](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. Nadat u logboekregistratie van berichten in de toepassing consolevenster Hallo Hallo ziet, Hallo Index pagina toosee Hallo miniatuur vernieuwen.

    ![De indexpagina](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Klik op **Details** voor uw afbeelding van ad toosee Hallo.

    ![De pagina Details](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

U hebt is Hallo toepassing uitvoeren op uw lokale computer en deze gebruik maakt van een SQL Server-database op de computer, maar werkt met wachtrijen en blobs in Hallo cloud. In de volgende sectie Hallo voert u de toepassing hello in de cloud Hallo, met behulp van een cloud-database, evenals cloud blobs en wachtrijen.  

## <a id="runincloud"></a>Hallo-toepassing uitvoeren in de cloud Hallo
U voert de volgende stappen toorun Hallo toepassing in de cloud Hallo Hallo:

* TooWeb Apps implementeren. Visual Studio maakt automatisch een nieuwe web-app in App Service en een exemplaar van SQL-Database.
* Hallo web app toouse uw Azure SQL database- en storage-account configureren.

Nadat u advertenties hebt gemaakt tijdens het uitvoeren van de cloud hello, bekijkt u Hallo WebJobs SDK dashboard toosee Hallo uitgebreide bewakingsfuncties toooffer heeft.

### <a name="deploy-tooweb-apps"></a>TooWeb Apps implementeren

1. Hallo-browser en Hallo-consolevenster toepassing sluiten.
2. Volg de stappen Hallo in Hallo [tooAzure met SQL Database publiceren](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sectie.
3. Nadat u de stappen voor het implementeren van Hallo hebt voltooid, kunt u doorgaan met de Hallo resterende taken in dit artikel.

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a>Hallo web app toouse uw Azure SQL database- en storage-account configureren
Er is een best practice bij beveiliging te[te voorkomen dat gevoelige informatie zoals verbindingsreeksen in bestanden die zijn opgeslagen in broncodeopslagplaatsen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). Azure biedt een manier toodo: u kunt de verbindingstekenreeks en andere instellingswaarden in hello Azure-omgeving instellen en ASP.NET-configuratie API's automatisch kunnen worden opgepikt deze waarden als Hallo-app wordt uitgevoerd in Azure. U kunt deze waarden instellen in Azure met behulp van **Server Explorer**, hello Azure-Portal Windows PowerShell of Hallo platformoverschrijdende opdrachtregelinterface. Zie voor meer informatie [tekenreeksen van toepassingen en verbindingsreeksen](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

In deze sectie gebruikt u **Server Explorer** tooset de waarden van verbindingsreeksen in Azure.

1. In **Server Explorer**, met de rechtermuisknop op uw web-app onder **Azure > App Service > {uw resourcegroep}**, en klik vervolgens op **weergave-instellingen**.

    Hallo **Azure-Web-App** venster wordt geopend op Hallo **configuratie** tabblad.
2. Hallo naam wijzigen van Hallo DefaultConnection toohello verbindingsreeksnaam u hebt gekozen als u Hallo SQL-database geconfigureerd in Hallo [tooAzure met SQL Database publiceren](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artikel.

    Deze verbindingsreeks Azure automatisch gemaakt wanneer u Hallo web-app met een bijbehorende database gemaakt, zodat het Hallo rechts gegevensbronwaarde al heeft. U kunt alleen Hallo naam-toowhat naar uw code zoekt wilt wijzigen.
3. Twee nieuwe verbindingsreeksen, met de naam AzureWebJobsStorage en AzureWebJobsDashboard toevoegen. Hallo databasetype te ingesteld**aangepaste**, en set Hallo verbinding tekenreeks waarde toohello dezelfde waarde die u hebt eerder voor Hallo gebruikt *Web.config* en *App.config* bestanden. (Zorg ervoor u Hallo hele verbindingsreeks, niet alleen Hallo-toegangssleutel, opneemt en Hallo aanhalingstekens zijn niet opgenomen.)

    Deze verbindingsreeksen worden gebruikt door Hallo WebJobs SDK, één voor toepassingsgegevens en één voor logboekregistratie. Als u eerder hebt gezien, wordt Hallo voor toepassingsgegevens worden ook gebruikt door Hallo web-front-code.
4. Klik op **Opslaan**.

    ![Verbindingsreeksen in Azure Portal](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. In **Server Explorer**, met de rechtermuisknop op het Hallo-web-app en klik vervolgens op **stoppen**.
6. Nadat het Hallo-web-app stopt, opnieuw met de rechtermuisknop op Hallo web-app en klik vervolgens op **Start**.

   Hallo webtaak wordt automatisch gestart wanneer u publiceren, maar stopt wanneer u een configuratiewijziging. toorestart, kunt u Hallo web-app te starten of opnieuw opstarten Hallo webtaak in Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Het is doorgaans aanbevolen toorestart Hallo web-app na een configuratiewijziging.
7. Hallo-browservenster met Hallo web-app-URL in de adresbalk vernieuwen.

    Hallo-startpagina wordt weergegeven.
8. Maken van een advertentie, net als wanneer u [Hallo toepassing lokaal uitgevoerd](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   Hallo indexpagina wordt weergegeven zonder een miniatuur in eerste instantie.
9. Vernieuw Hallo pagina na enkele seconden en hello miniatuur weergegeven.

   Als de miniatuur Hallo niet wordt weergegeven, wellicht u toowait een minuut voor Hallo webtaak toorestart. Als u na een tijdje u nog steeds ziet niet Hallo miniatuur bij het vernieuwen van Hallo pagina Hallo webtaak niet automatisch hebt gestart. In dat geval gaan toohello **App Services** blade in Hallo [Azure-portal](https://portal.azure.com/), zoek uw web-app en klik vervolgens op **Start**.

### <a name="view-hello-webjobs-sdk-dashboard"></a>Weergave Hallo WebJobs SDK-dashboard
1. In Hallo [Azure-portal](https://portal.azure.com/), selecteer Hallo **blade App Services**, Ga naar uw web-app en selecteer **WebJobs**.
3. Selecteer Hallo **logboeken** tabblad.

    ![Tabblad Logboeken](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    Een nieuw browsertabblad geopend toohello WebJobs SDK-dashboard. Hallo-dashboard ziet u dat Hallo webtaak wordt uitgevoerd en wordt een lijst met functies in uw code die Hallo die webjobs SDK wordt geactiveerd.
4. Klik op een Hallo functies toosee details over de uitvoering ervan.

    ![WebJobs SDK-dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK-dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    Hallo **Replay-functie** op deze pagina wordt knop Hallo WebJobs SDK framework toocall Hallo functie opnieuw, en geeft u een kans toochange Hallo doorgegeven toohello functie eerst.

> [!NOTE]
> Wanneer u klaar bent met testen, kunt u eventueel de Hallo web-app, storage-account en uw exemplaar van SQL-Database verwijderen. Hallo-web-app is gratis, maar Hallo storage-account voor SQL en database-exemplaar doorlopen kosten (zij, minimale vanwege toohello klein). Ook als u niets Hallo web-app die wordt uitgevoerd, kunt iedereen die uw URL vindt advertenties maken en weergeven. 
>
>

### <a name="delete-your-web-app"></a>Uw web-app verwijderen
Ga in de portal voor Hallo toohello **App Services** blade Zoek en selecteer uw web-app en klik vervolgens op **verwijderen**. Als u alleen wilt tootemporarily voorkomen dat anderen toegang hebben tot de web-app hello, klikt u op **stoppen** in plaats daarvan. In dat geval blijven de kosten tooaccrue voor Hallo SQL-Database en het Opslagaccount.

### <a name="delete-your-storage-account"></a>Uw storage-account verwijderen
toodelete uw storage-account, Zie [een opslagaccount verwijderen](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Uw database verwijderen
toodelete uw SQL database, Zie Hallo [REST-API van Azure SQL Database](https://docs.microsoft.com/rest/api/sql/) documentatie.

## <a id="create"></a>Hallo toepassing vanaf het begin maken
In deze sectie, doet u Hallo volgende taken:

* Een Visual Studio-oplossing maken met een webproject.
* Voeg een klasse bibliotheek-project voor Hallo gegevens toegang laag die wordt gedeeld tussen Hallo front-end en back-end.
* Voeg een project-consoletoepassing voor back-end van Hallo met WebJobs-implementatie is ingeschakeld.
* NuGet-pakketten toevoegen.
* Projectverwijzingen instellen.
* Kopieer toepassingsbestanden code en configuratie uit gedownload Hallo-toepassing die u in de vorige sectie Hallo Hallo-zelfstudie hebt gewerkt.
* Bekijk Hallo delen Hallo-code die werken met Azure blobs en wachtrijen en Hallo WebJobs SDK.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Een Visual Studio-oplossing maken met een webproject en class library-project
1. Kies in Visual Studio **bestand** > **nieuw** > **Project**.
2. In Hallo **nieuw Project** dialoogvenster kiezen **Visual C#** > **Web** > **ASP.NET-webtoepassing (.NET Framework)**.
3. Noem Hallo project ContosoAdsWeb en geef de naam Hallo oplossing ContosoAdsWebJobsSDK (Hallo oplossingsnaam wijzigen als u deze wilt opslaan in Hallo dezelfde map als Hallo gedownload oplossing), en klik vervolgens op **OK**.

    ![Nieuw project](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. In Hallo **nieuwe ASP.NET-webtoepassing** dialoogvenster Hallo MVC-sjabloon kiest en selecteert u **verificatie wijzigen**.

    ![Verificatie wijzigen](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. In Hallo **verificatie wijzigen** dialoogvenster kiezen **geen verificatie**, en klik vervolgens op **OK**.

    ![Geen verificatie](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. In Hallo **nieuwe ASP.NET-webtoepassing** dialoogvenster, klikt u op **OK**.

    Visual Studio maakt het Hallo-oplossing en Hallo-webproject.
7. In **Solution Explorer**, met de rechtermuisknop op het Hallo-oplossing (niet Hallo project) en kies **toevoegen** > **nieuw Project**.
8. In Hallo **Add New Project** dialoogvenster kiezen **Visual C#** > **Classic Windows Desktop** > **Class Library (.NET Framework)** sjabloon.  
9. Naam Hallo project *ContosoAdsCommon*, en klik vervolgens op **OK**.

    Dit project bevat Hallo Entity Framework-context en Hallo-gegevensmodel die beide Hallo front-end en back-end gebruikt. Als alternatief kan u Hallo EF-gerelateerde klassen definiëren in Hallo-webproject en uit Hallo webtaak project naar verwijzen. Maar vervolgens uw webtaak project een verwijzing tooweb assembly's, waarbij het niet nodig zou hebben.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Voeg een consoletoepassing-project met webtaken implementatie is ingeschakeld
1. Met de rechtermuisknop op het Hallo-webproject (geen Hallo oplossing of Hallo class library-project) en klik vervolgens op **toevoegen** > **nieuwe Azure webtaak Project**.

    ![Nieuwe Azure webtaak Project menuselectie](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. In Hallo **toevoegen Azure webtaak** dialoogvenster ContosoAdsWebJob invoeren als beide Hallo **projectnaam** en Hallo **naam van een webtaak**. Laat **webtaak uitvoeren modus** instellen te**continu uitvoeren**.
3. Klik op **OK**.

   Visual Studio maakt een consoletoepassing die is geconfigureerd toodeploy als een webtaak wanneer u Hallo-webproject implementeert. toodo dat het uitvoeren van Hallo taken te volgen nadat het Hallo-project maken:

   * Toegevoegd een *webtaak-publiceren settings.json* bestand in map Hallo webtaak project-eigenschappen.
   * Toegevoegd een *webjobs list.json* bestand in map Hallo web project-eigenschappen.
   * Hallo Microsoft.Web.WebJobs.Publish NuGet-pakket in Hallo webtaak project geïnstalleerd.

   Zie voor meer informatie over deze wijzigingen [hoe toodeploy WebJobs met behulp van Visual Studio](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>NuGet-pakketten toevoegen
Hallo nieuw project-sjabloon voor een webtaak project installeert automatisch Hallo WebJobs SDK NuGet-pakket [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) en de bijbehorende afhankelijkheden.

Een van de WebJobs SDK-afhankelijkheden die automatisch wordt geïnstalleerd in Hallo webtaak project is Hallo hello Azure Storage Client-bibliotheek (SCL). U moet echter tooadd het toohello web project toowork met blobs en wachtrijen.

1. Open Hallo **NuGet-pakketten beheren** dialoogvenster voor Hallo-oplossing.
2. Selecteer in het linkerdeelvenster Hallo **geïnstalleerde pakketten**.
3. Hallo zoeken *Azure Storage* van het pakket en klik vervolgens op **beheren**.
4. In Hallo **projecten selecteren** in, selecteer Hallo **ContosoAdsWeb** selectievakje en klik vervolgens op **OK**.

    Alle drie de projecten Hallo Entity Framework toowork met gegevens in SQL-Database gebruiken.
5. Selecteer in het linkerdeelvenster Hallo **Online**.
6. Hallo zoeken *EntityFramework* NuGet-pakket en installeer het in alle drie de projecten.

### <a name="set-project-references"></a>Projectverwijzingen instellen
Web- en webtaak projecten werken met Hallo SQL-database, zodat beide een verwijzing toohello ContosoAdsCommon project moeten.

1. In Hallo ingesteld project ContosoAdsWeb een verwijzing toohello ContosoAdsCommon project. (Met de rechtermuisknop op Hallo ContosoAdsWeb-project en klik vervolgens op **toevoegen** > **verwijzing**. 
2. In Hallo **Reference Manager** dialoogvenster, **projecten** > **oplossing** > **ContosoAdsCommon**, en klik vervolgens op **OK**.)
   
    Hallo webtaak project moet verwijzingen voor het werken met installatiekopieën en voor het openen van verbindingsreeksen.

4. Stel in Hallo ContosoAdsWebJob project een verwijzing te`System.Drawing` en `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Code-en configuratiebestanden toevoegen
Deze zelfstudie toont niet hoe te[maken van MVC-controllers en weergaven met steigers](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), hoe te[schrijven van code voor Entity Framework die geschikt is voor SQL Server-databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), of [Hallo basisprincipes van asynchrone programmering in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Zo, dat alle is blijft toodo code en configuratie bestanden kopiëren van de oplossing in de nieuwe oplossing Hallo Hallo gedownload. Nadat u dat doet, hello volgende secties weergeven en toegelicht belangrijke onderdelen van Hallo-code.

tooadd bestanden tooa project of een map, klik met de rechtermuisknop Hallo project of map en klikt u op **toevoegen** > **bestaand Item**. Selecteer Hallo bestanden wilt en klikt u op **toevoegen**. Als u wordt gevraagd of u wilt dat de bestaande bestanden tooreplace, klikt u op **Ja**.

1. Verwijder in project ContosoAdsCommon Hallo Hallo *Class1.cs* -bestand en in de plaats Hallo volgende bestanden uit Hallo gedownload project toevoegen.

   * *AD.cs*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. In het project ContosoAdsWeb Hallo toevoegen Hallo volgende bestanden uit Hallo gedownload project.

   * *Web.config*
   * *Global.asax.cs*  
   * In Hallo *domeincontrollers* map: *AdController.cs*
   * In Hallo *Views\Shared* map: *_Layout.cshtml* bestand
   * In Hallo *Views\Home* map: *Index.cshtml*
   * In Hallo *Views\Ad* map (Maak eerst Hallo map): vijf *.cshtml* bestanden
3. Voeg in Hallo ContosoAdsWebJob project Hallo volgende bestanden uit project Hallo gedownload.

   * *App.config* (Hallo type bestandsfilter ook wijzigen**alle bestanden**)
   * *Program.cs*
   * *Functions.cs*

Nu kunt u samenstellen, uitvoeren en implementeren van de toepassing hello volgens de instructies eerder in de zelfstudie Hallo. Voordat u dat doet, moet u echter Hallo webtaak die nog steeds worden uitgevoerd in Hallo eerste web-app geïmplementeerd stoppen. Anders die webtaak wordt verwerkt berichten in wachtrij plaatsen lokaal gemaakt of door Hallo-app in een nieuwe web-app wordt uitgevoerd, omdat alle gebruikt dezelfde Hallo storage-account.

## <a id="code"></a>Hallo toepassingscode bekijken
Hallo volgende secties wordt uitgelegd Hallo code verband tooworking Hello WebJobs SDK en Azure Storage-blobs en wachtrijen.

> [!NOTE]
> Ga voor Hallo code specifieke toohello WebJobs SDK toohello [Program.cs en Functions.cs](#programcs) secties.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
bestand van Hallo Ad.cs definieert een enum voor advertentiecategorieën en een POCO-entiteitsklasse voor advertentie-informatie.

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Hallo klasse contosoadscontext geeft aan dat Hallo Ad-klasse wordt gebruikt in een DbSet-verzameling Entity Framework wordt opgeslagen in een SQL-database.

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

Hallo-klasse heeft twee constructors. Hallo eerst wordt gebruikt door Hallo-webproject en specificeert Hallo-naam van een verbindingsreeks die is opgeslagen in Web.config Hallo of hello Azure runtime-omgeving. Hallo tweede constructor kunt u toopass in Hallo werkelijke verbindingsreeks. Deze is nodig voor Hallo webtaak project omdat het geen een Web.config-bestand. U eerder hebt gezien waar deze verbindingsreeks is opgeslagen en ziet u hoe Hallo-code Hallo verbindingsreeks ophaalt bij het instantiëren van Hallo DbContext-klasse.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon - BlobInformation.cs
Hallo `BlobInformation` klasse gebruikte toostore informatie over een blob installatiekopie in een wachtrijbericht is.

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Code die wordt aangeroepen vanuit Hallo `Application_Start` methode maakt u een *installatiekopieën* blob-container en een *installatiekopieën* als ze nog niet bestaan in de wachtrij. Dit zorgt ervoor dat wanneer u met behulp van een nieuw opslagaccount begint, Hallo vereiste blobcontainer en wachtrij automatisch worden gemaakt.

code haalt toegang toohello storage-account met behulp van de opslagverbindingsreeks uit Hallo HALLO hallo *Web.config* bestands- of Azure runtime-omgeving.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

Vervolgens wordt een verwijzing toohello *installatiekopieën* blob-container, Hallo container maakt als deze niet al bestaat en stelt deze voor de nieuwe container Hallo toegangsrechten. Standaard staan nieuwe containers alleen clients met storage-account referenties tooaccess blobs. Hallo-web-app moet blobs toobe openbare Hallo zodat deze afbeeldingen met URL's die punt toohello afbeeldingsblobs wijzen kan weergeven.

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

Vergelijkbare code wordt een verwijzing toohello *thumbnailrequest* wachtrij en een nieuwe wachtrij gemaakt. In dit geval is er geen machtigingswijziging nodig.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - _Layout.cshtml
Hallo *_Layout.cshtml* bestand Hallo app-naam stelt in Hallo koptekst en voettekst en maakt een menu-item 'Ads'.

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Hallo *Views\Home\Index.cshtml* bestand geeft categoriekoppelingen weer op Hallo-startpagina. Hallo-koppelingen geven de integerwaarde Hallo Hallo `Category` enum in een pagina querystring variabele toohello Ads Index.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
In Hallo *AdController.cs* bestand, Hallo constructor aanroepen Hallo `InitializeStorage` methode toocreate Azure Storage-clientbibliotheek objecten die een API leveren voor het werken met blobs en wachtrijen.

Vervolgens Hallo code een verwijzing toohello opgehaald *installatiekopieën* blobcontainer, zoals u eerder in gezien *Global.asax.cs*. Tijdens het uitvoeren, wordt standaard ingesteld [beleid voor opnieuw proberen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) geschikt is voor een web-app. Hallo standaard exponentieel uitstel-beleid voor opnieuw proberen kan vastlopen Hallo web-app langer dan een minuut herhaalde pogingen voor een tijdelijke fout. beleid voor opnieuw proberen Hallo hier opgegeven wacht drie seconden na elke poging up toothree pogingen.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Vergelijkbare code wordt een verwijzing toohello *installatiekopieën* wachtrij.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

De meeste Hallo controllercode is Typerend voor het werken met een Entity Framework-gegevensmodel met behulp van een DbContext-klasse. Een uitzondering is Hallo HttpPost `Create` methode, waarmee een bestand wordt geüpload en opgeslagen in blob-opslag. Hallo modelbinder levert een [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello methode-object.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Hallo gebruiker geselecteerd een bestand tooupload, Hallo code Hallo-bestand wordt geüpload, opgeslagen in een blob als Hallo Ad-databaserecord bijgewerkt met een URL die toohello blob verwijst.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

Hallo-code die uploaden Hallo heeft Hallo `UploadAndSaveBlobAsync` methode. Deze maakt een GUID-naam voor Hallo blob, uploads en slaat Hallo-bestand en retourneert een verwijzing toohello opgeslagen blob.

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

Na het Hallo HttpPost `Create` methode een blob uploadt en updates Hallo database, het maken van een wachtrij bericht tooinform Hallo back-endproces dat een afbeelding gereed voor conversie tooa miniatuur is.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

code voor Hallo HttpPost Hallo `Edit` methode is vergelijkbaar, behalve dat als Hallo gebruiker selecteert een nieuw afbeeldingsbestand, alle blobs die al bestaan voor deze advertentie moeten worden verwijderd.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Dit is Hallo code verwijderen van blobs wanneer u een advertentie verwijdert:

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml en Details.cshtml
Hallo *Index.cshtml* bestand bevat miniaturen Hello andere ad-gegevens:

        <img  src="@Html.Raw(item.ThumbnailURL)" />

Hallo *Details.cshtml* bestand Hallo-afbeelding wordt weergegeven:

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml en Edit.cshtml
Hallo *Create.cshtml* en *Edit.cshtml* bestanden formulier dat Hiermee controller tooget Hallo Hallo codering opgeven `HttpPostedFileBase` object.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

Een `<input>` element vertelt Hallo browser tooprovide een dialoogvenster voor bestandsselectie.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
Wanneer Hallo webtaak wordt gestart, hello `Main` methodeaanroepen Hallo WebJobs SDK `JobHost.RunAndBlock` methode toobegin uitvoering van de geactiveerde functies in de huidige thread Hallo.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail methode
Hallo WebJobs SDK roept deze methode wanneer er een wachtrijbericht wordt ontvangen. Hallo-methode maakt u een miniatuur en puts Hallo miniatuur-URL in het Hallo-database.

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* Hallo `QueueTrigger` kenmerk stuurt Hallo WebJobs SDK toocall deze methode wanneer een nieuw bericht wordt ontvangen op Hallo thumbnailrequest wachtrij.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    Hallo `BlobInformation` -object in de wachtrij het Hallo-bericht is automatisch gedeserialiseerde in Hallo `blobInfo` parameter. Wanneer Hallo-methode is voltooid, wordt de wachtrij het Hallo-bericht verwijderd. Als Hallo methode mislukt voordat wordt voltooid, wordt wachtrij het Hallo-bericht niet verwijderd. Nadat een 10 minuten lease is verlopen, is het Hallo-bericht uitgebrachte toobe opnieuw opgehaald en verwerkt. Deze reeks won't voor onbepaalde tijd worden herhaald als een bericht altijd een uitzondering veroorzaakt. Na 5 mislukte tooprocess een bericht pogingen, het Hallo-bericht is verplaatst tooa wachtrij met de naam {wachtrijnaam}-verontreinigd. maximum aantal pogingen Hallo kan worden geconfigureerd.
* Hallo twee `Blob` kenmerken Geef objecten die gebonden tooblobs zijn: één toohello bestaande installatiekopie blob en één tooa nieuwe miniaturen blob die Hallo-methode maakt.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    BLOB-namen afkomstig zijn van de eigenschappen van Hallo `BlobInformation` object in de wachtrij het Hallo-bericht ontvangen (`BlobName` en `BlobNameWithoutExtension`). tooget hello volledige functionaliteit van Hallo Storage-clientbibliotheek, kunt u Hallo `CloudBlockBlob` klasse toowork met blobs. Als u wilt dat tooreuse-code die is geschreven toowork met `Stream` objecten, kunt u Hallo `Stream` klasse.

Voor meer informatie over hoe toowrite functioneert die kenmerken van de WebJobs SDK gebruiken, raadpleegt u Hallo resources te volgen:

* [Hoe toouse Azure queue storage Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Hoe toouse Azure blob-opslag met Hallo WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Hoe toouse Azure table storage Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Hoe toouse Azure Service Bus met Hallo WebJobs SDK](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Als uw web-app wordt uitgevoerd op meerdere virtuele machines, meerdere WebJobs wordt tegelijkertijd worden uitgevoerd en in sommige gevallen kan dit resulteren in Hallo dezelfde gegevens meerdere keren wordt verwerkt. Dit is niet een probleem als u ingebouwde wachtrij hello, blob en Service Bus-triggers. Hallo SDK zorgt ervoor dat uw functies slechts één keer worden verwerkt voor elk bericht of blob.
> * Voor informatie over het correct afsluiten tooimplement, Zie [correct afsluiten](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * Hallo-code in Hallo `ConvertImageToThumbnailJPG` methode (niet weergegeven) maakt gebruik van klassen in Hallo `System.Drawing` naamruimte voor eenvoud. Hallo-klassen in deze naamruimte zijn echter bedoeld voor gebruik met Windows Forms. Ze worden niet ondersteund voor gebruik in een Windows- of ASP.NET-service. Zie [Afbeeldingen dynamisch genereren](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) en [Alles over het wijzigen van het formaat van afbeeldingen](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) voor meer informatie over opties voor de verwerking van afbeeldingen.
>
>

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u een eenvoudige toepassing met meerdere lagen die Hallo WebJobs SDK voor de verwerking van de back-end gebruikt gezien. Deze sectie vindt u enkele suggesties voor meer informatie over toepassingen met meerdere lagen ASP.NET en WebJobs.

### <a name="missing-features"></a>Ontbrekende functies
de toepassing Hello gehouden eenvoudige voor een zelfstudie aan de slag. In een echte toepassing die u wilt implementeren [afhankelijkheidsinjectie](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) en Hallo [opslagplaatsen en werkeenheden](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), gebruik [een interface voor logboekregistratie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), gebruiken[ EF Code First-migraties](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model wijzigingen en gebruik [EF-Verbindingstolerantie](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage tijdelijke netwerkfouten.

### <a name="scaling-webjobs"></a>Schalen WebJobs
WebJobs in Hallo context van een web-app uitgevoerd en zijn niet afzonderlijk worden schaalbaar. Als u een standaard web-app-exemplaar hebt, hebt u slechts één exemplaar van de achtergrondproces wordt uitgevoerd en sommige Hallo serverbronnen (CPU, geheugen, enzovoort) die anders beschikbaar tooserve webinhoud zijn zou wordt gebruikt.

Als verkeer hangt af van de tijd van de dag of week, en als back-end Hallo verwerken u moet toodo kunt wachten, uw toorun WebJobs kan worden gepland op tijden weinig verkeer. Als Hallo belasting nog steeds te hoog is voor deze oplossing wordt, kunt u back-end voor Hallo als een webtaak in een speciale afzonderlijke web-app uitvoeren daarvoor. U kunt uw back-end-web-app vervolgens onafhankelijk van elkaar schalen van uw frontend-web-app.

Zie voor meer informatie [WebJobs schalen](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Web-app time-out afsluiten-keuzelijsten voorkomen
toomake ervoor dat uw WebJobs worden altijd uitgevoerd en wordt uitgevoerd op alle exemplaren van uw web-app, hebt u tooenable Hallo [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) functie.

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a>Met behulp van Hallo WebJobs SDK buiten WebJobs
Een programma dat gebruikmaakt van Hallo WebJobs SDK biedt geen toorun in Azure in een webtaak. Lokaal kunt uitvoeren, en ook in andere omgevingen zoals een werkrol Cloudservice of een Windows-service kan worden uitgevoerd. U kunt echter alleen Hallo WebJobs SDK dashboard openen via een Azure-web-app. toouse Hallo-dashboard tooconnect Hallo web app toohello opslagaccount u hebt door het Hallo AzureWebJobsDashboard verbindingsreeks instellen op Hallo **configureren** tabblad van de klassieke portal Hallo. U kunt vervolgens toohello Dashboard krijgen met behulp van Hallo URL te volgen:

https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions

Zie voor meer informatie [ophalen van een dashboard voor lokale ontwikkeling Hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), maar houd er rekening mee dat er een oude naam van verbindingsreeks wordt weergegeven.

### <a name="more-webjobs-documentation"></a>Documentatie voor meer WebJobs
Zie voor meer informatie [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226).
