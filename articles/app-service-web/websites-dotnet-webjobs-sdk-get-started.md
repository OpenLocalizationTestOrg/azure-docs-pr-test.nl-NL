---
title: Maken van een webtaak .NET in Azure App Service | Microsoft Docs
description: Maak een app met meerdere lagen met ASP.NET MVC en Azure. De front-end wordt in een web-app in Azure App Service en de vorige einde wordt uitgevoerd als een webtaak wordt uitgevoerd. De app gebruikmaakt van Entity Framework, SQL-Database en Azure storage-wachtrijen en blobs.
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
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Een .NET-webtaak maken in Azure App Service
Deze zelfstudie laat zien hoe u code schrijven voor een eenvoudige ASP.NET MVC 5 toepassing met meerdere lagen die gebruikmaakt van de [WebJobs SDK](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Het doel van de [WebJobs SDK](websites-webjobs-resources.md) te vereenvoudigen, de code voor algemene taken die een webtaak schrijven, zoals beeldverwerking, wachtrijbewerkingen, RSS aggregatie, onderhouden van bestanden uitvoeren kunt en e-mailberichten verzenden. De WebJobs SDK bevat ingebouwde functies voor het werken met Azure Storage en Service Bus, voor het plannen van taken en het afhandelen van fouten en voor veel andere veelvoorkomende scenario's. Bovendien kan worden uitgebreid ontworpen en er is een [open-source-opslagplaats voor uitbreidingen](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

De voorbeeldtoepassing is een bulletinboard voor advertenties. Gebruikers kunnen uploaden afbeeldingen voor advertenties en een back-end-proces de afbeeldingen worden geconverteerd naar miniatuurweergaven. De pagina van de lijst met ad toont de miniaturen en de detailpagina ad ziet u de afbeelding. Hier volgt een schermafbeelding:

![Advertentielijst](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

Deze voorbeeldtoepassing werkt met [Azure wachtrijen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) en [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). De zelfstudie laat zien hoe de toepassing implementeren naar [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Vereisten
De zelfstudie wordt ervan uitgegaan dat u hoe weet werken met [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projecten in Visual Studio.

De zelfstudie oorspronkelijk is geschreven voor Visual Studio 2013, maar kan worden gebruikt met latere versies van Visual Studio. Als u van Visual Studio 2015 of 2017 gebruikmaakt, noteert u dat voordat u de toepassing lokaal uitvoeren, moet u de `Data Source` deel uit van de SQL Server LocalDB-verbindingsreeks in de Web.config en App.config bestanden van `Data Source=(localdb)\v11.0` naar `Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>U hebt een Azure-account om deze zelfstudie te voltooien:
>
> * U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): U ontvangt tegoed dat u gebruiken kunt om betaalde Azure-services te proberen en zelfs nadat ze zijn gebruikt, kunt u het account houden en gratis Azure-services, zoals Websites gebruiken. Er wordt nooit iets op uw creditcard in rekening gebracht, tenzij u expliciet de instellingen wijzigt en vraagt of de kosten op uw creditcard in rekening kunnen worden gebracht.
> * U kunt [maandelijkse Azure-krediet voor Visual Studio-abonnees activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): uw abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.
>
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
>
>

## <a id="learn"></a>Wat u leert
De zelfstudie laat zien hoe de volgende taken uitvoeren:

* Computer klaarmaken voor het ontwikkelen van Azure inschakelen door het installeren van de Azure-SDK (alleen voor Visual Studio 2013 en 2015 gebruikers).
* Maak een project-consoletoepassing die automatisch wordt geïmplementeerd als een webtaak Azure wanneer u het bijbehorende webproject implementeert.
* Test een WebJobs SDK back-end lokaal op de ontwikkelcomputer.
* Publiceer een toepassing met een back-end voor API in een WebApp in App Service.
* Bestanden uploaden en op te slaan in de Azure Blob-service.
* Gebruik de Azure WebJobs SDK werken met Azure Storage-wachtrijen en blobs.

## <a id="contosoads"></a>Toepassingsarchitectuur
De voorbeeldtoepassing gebruikt de [wachtrijgerichte werkpatroon](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) naar tijdens stillegging het CPU-intensief werk van het maken van miniatuurweergaven voor een back-end-proces.

De app slaat de advertenties met behulp van Entity Framework Code First op in een SQL-database om de tabellen te maken en toegang te krijgen tot de gegevens. Voor elke advertentie slaat de database twee URL's: één voor de afbeelding op volledige grootte en één voor de miniatuur.

![Advertentietabel](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

Wanneer een gebruiker een afbeelding uploadt de web-app slaat de afbeelding in een [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), slaat de Advertentiegegevens worden opgeslagen in de database met een URL die naar de blob verwijst. Tegelijkertijd schrijft de front-end een bericht naar een Azure-wachtrij. In een back-end-proces als een Azure-webtaak wordt uitgevoerd, controleert de WebJobs SDK of de wachtrij voor nieuwe berichten. Wanneer een nieuw bericht wordt weergegeven, wordt de webtaak wordt gemaakt van een miniatuur voor de betreffende afbeelding en de miniatuur databaseveld URL voor de advertentie-updates. Hier volgt een diagram toont de wisselwerking tussen de onderdelen van de toepassing:

![Architectuur van Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
De zelfstudie instructies gelden voor de Azure SDK voor .NET 2.7.1 of hoger.

## <a id="storage"></a>Een Azure Storage-account maken
Een Azure-opslagaccount biedt resources voor het opslaan van wachtrij- en blobgegevens in de cloud. Dit wordt ook gebruikt door de WebJobs SDK voor het opslaan van gegevens van de logboekregistratie voor het dashboard.

In een echte toepassing maakt u meestal afzonderlijke accounts voor toepassingsgegevens versus logboekgegevens en afzonderlijke accounts voor testgegevens versus productiegegevens. Voor deze zelfstudie gebruikt u slechts één account.

1. Open de **Server Explorer** venster in Visual Studio.
2. Met de rechtermuisknop op de **Azure** knooppunt en klik vervolgens op **verbinding maken met Microsoft Azure-abonnement...** .
   
   ![Verbinding maken met Azure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Meld u aan met uw Azure-referenties.
4. Met de rechtermuisknop op **opslag** onder de Azure-knooppunt en klik vervolgens op **Storage-Account maken**.
   
   ![Storage-Account maken](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. In de **Storage-Account maken** dialoogvenster, voer een naam voor het opslagaccount.

    De naam moet uniek zijn (geen Azure storage-account kan dezelfde naam hebben). Als de naam die u invoert, al gebruikt wordt, krijgt u een kans om dit te wijzigen.

    De URL voor toegang tot uw storage-account *{name}*. core.windows.net.
6. Stel de **regio of Affiniteitsgroep** vervolgkeuzelijst voor de regio die het dichtst bij u.

    Deze instelling bepaalt u welke Azure-datacenter fungeert als host voor uw opslagaccount. Voor deze zelfstudie won't uw keuze maakt geen merkbaar verschil. Voor een productie-web-app wilt u echter uw storage-account zich in dezelfde regio kosten voor uitgaande gegevens en de latentie te minimaliseren en de webserver. De web-app (die u later maken) datacenter moet zo dicht mogelijk bij de toegang tot de web-app om te minimaliseren latentie browsers.
7. Stel de vervolgkeuzelijst **Replicatie** in op **Lokaal redundant**.

    Wanneer geo-replicatie is ingeschakeld voor een opslagaccount, wordt de opgeslagen inhoud gerepliceerd naar een secundair datacenter om failover naar die locatie mogelijk te maken in het geval van een noodgeval op de primaire locatie. Geo-replicatie kan extra kosten met zich meebrengen. Voor test- en ontwikkelingsaccounts wilt u in het algemeen niet betalen voor geo-replicatie. Zie [Een opslagaccount maken, beheren of verwijderen](../storage/common/storage-create-storage-account.md) voor meer informatie.
8. Klik op **Create**.

    ![Nieuw opslagaccount](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>De toepassing downloaden
1. Download de [voltooide oplossing](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb) en pak deze uit.
2. Start Visual Studio.
3. Van de **bestand** in het menu **openen > Project/oplossing**, gaat u naar waar u de oplossing gedownload en open het oplossingsbestand.
4. Druk op CTRL + SHIFT + B om de oplossing te bouwen.

    Standaard herstelt Visual Studio automatisch de inhoud van het NuGet-pakket, dat niet is opgenomen in het *.zip*-bestand. Als de pakketten niet worden hersteld, deze handmatig installeren door te gaan naar de **NuGet-pakketten beheren voor oplossing** dialoogvenster en te klikken op de **herstellen** knop in de rechterbovenhoek.
5. In **Solution Explorer**, zorg ervoor dat **ContosoAdsWeb** is geselecteerd als opstartproject.

## <a id="configurestorage"></a>De toepassing configureren voor uw storage-account gebruiken
1. Open de toepassing *Web.config* bestand in het project ContosoAdsWeb.

    Het bestand bevat een SQL-verbindingsreeks en de verbindingsreeks van een Azure-opslag voor het werken met blobs en wachtrijen.

    De SQL-verbindingsreeks verwijst naar een [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.

    De verbindingsreeks voor opslag is een voorbeeld van tijdelijke aanduidingen voor de storage-account naam en toegangssleutel. U hebt deze vervangen met een verbindingsreeks met de naam en sleutel van uw opslagaccount.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    De verbindingsreeks voor opslag is standaard de naam AzureWebJobsStorage omdat dat de naam van die de WebJobs SDK wordt gebruikt. Dezelfde naam wordt hier gebruikt, hoeft u slechts één gegevensbronwaarde in de Azure-omgeving instellen.
2. In **Server Explorer**, met de rechtermuisknop op uw opslagaccount onder de **opslag** knooppunt en klik vervolgens op **eigenschappen**.

    ![Klik op Eigenschappen van het Opslagaccount](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. In de **eigenschappen** venster, klikt u op **Opslagaccountsleutels**, en klik vervolgens op het weglatingsteken.

    ![Toegangscodes voor opslag](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Kopieer de **verbindingsreeks**.

    ![Opslag toegangscodes dialoogvenster](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Vervang de verbindingsreeks voor opslag in de *Web.config* bestand met de verbindingsreeks die u zojuist hebt gekopieerd. Zorg ervoor dat u Alles selecteren binnen de aanhalingstekens, maar niet inclusief de aanhalingstekens voordat u gaat plakken.
6. Open de *App.config* bestand in het project ContosoAdsWebJob.

    Dit bestand heeft twee storage-verbindingsreeksen, één voor toepassingsgegevens en één voor logboekregistratie. U kunt afzonderlijke storage-accounts voor toepassingsgegevens en logboekregistratie en kunt u [meerdere opslagaccounts voor gegevens](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). Voor deze zelfstudie maakt u een één opslagaccount gebruikt. De verbindingsreeksen hebben tijdelijke aanduidingen voor de opslagaccountsleutels.

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

    Standaard zoekt de WebJobs SDK met de naam AzureWebJobsStorage en AzureWebJobsDashboard verbindingsreeksen. Als alternatief kunt u [store de verbinding string, maar u wilt en geef dit in expliciet aan de `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Beide storage-verbindingsreeksen vervangen door de verbindingsreeks die u eerder hebt gekopieerd.
8. Sla uw wijzigingen op.

## <a id="run"></a>De toepassing lokaal uitvoeren
1. Druk op CTRL + F5 voor het starten van de front-end webserver van de toepassing.

    De standaardbrowser geopend met de startpagina. (Het webproject wordt uitgevoerd omdat u opstartproject hebt aangebracht.)

    ![Contoso Ads-startpagina](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. Voor het starten van de webtaak back-end van de toepassing met de rechtermuisknop op het project ContosoAdsWebJob in **Solution Explorer**, en klik vervolgens op **Debug** > **nieuw exemplaar gestart**.

    Een toepassing consolevenster opent en toont logboekregistratie-berichten die aangeven dat het object WebJobs SDK JobHost is gestart om uit te voeren.

    ![Toepassing consolevenster weergegeven dat de back-end wordt uitgevoerd](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. Klik in uw browser **maken een advertentie**.
4. Voer enkele testgegevens, selecteert u een installatiekopie uploaden en klik vervolgens op **maken**.

    ![De pagina Create](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    De app gaat naar de indexpagina, maar geeft voor de nieuwe advertentie geen miniatuur weer omdat de betreffende bewerking nog niet heeft plaatsgevonden.

    Ondertussen na een korte wachten logboekregistratie in een bericht in het consolevenster van de toepassing aangegeven dat een wachtrijbericht is ontvangen en is verwerkt.

    ![Toepassing consolevenster weergegeven dat er een wachtrijbericht is verwerkt](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. Nadat u de logboekregistratie van berichten in het consolevenster van de toepassing ziet, vernieuwt u de indexpagina om te zien van de miniatuur.

    ![De indexpagina](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Klik op **Details** voor uw advertentie om de afbeelding op volledige grootte te bekijken.

    ![De pagina Details](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

U hebt uitvoert, de toepassing op uw lokale computer, en deze gebruik maakt van een SQL Server-database op de computer, maar werkt met wachtrijen en blobs in de cloud. In de volgende sectie voert u de toepassing in de cloud, met behulp van een cloud-database, evenals cloud blobs en wachtrijen.  

## <a id="runincloud"></a>De toepassing uitvoert in de cloud
U voert de volgende stappen uit voor het uitvoeren van de toepassing in de cloud:

* Implementeer op Web-Apps. Visual Studio maakt automatisch een nieuwe web-app in App Service en een exemplaar van SQL-Database.
* De web-app voor het gebruik van uw Azure SQL database- en storage-account configureren.

Nadat u advertenties hebt gemaakt tijdens het uitvoeren van de cloud, bekijkt u het WebJobs SDK dashboard overzicht van de uitgebreide bewakingsfuncties niet optimaal.

### <a name="deploy-to-web-apps"></a>Implementeren voor Web-Apps

1. Sluit de browser en het consolevenster van de toepassing.
2. Volg de stappen in de [publiceren naar Azure met SQL-Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sectie.
3. Nadat u de stappen voor de implementatie hebt voltooid, kunt u doorgaan met de resterende taken in dit artikel.

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a>De web-app voor het gebruik van uw Azure SQL database- en storage-account configureren
Het is een best practice bij beveiliging naar [te voorkomen dat gevoelige informatie zoals verbindingsreeksen in bestanden die zijn opgeslagen in broncodeopslagplaatsen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). Azure biedt een manier om u te doen: u kunt de verbindingstekenreeks en andere instellingswaarden instellen in de Azure-omgeving en ASP.NET-configuratie API's automatisch kunnen worden opgepikt deze waarden als de app wordt uitgevoerd in Azure. U kunt deze waarden instellen in Azure met behulp van **Server Explorer**, de Azure Portal, Windows PowerShell of de platformoverschrijdende opdrachtregelinterface. Zie voor meer informatie [tekenreeksen van toepassingen en verbindingsreeksen](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

In deze sectie gebruikt u **Server Explorer** verbinding tekenreekswaarden instellen in Azure.

1. In **Server Explorer**, met de rechtermuisknop op uw web-app onder **Azure > App Service > {uw resourcegroep}**, en klik vervolgens op **weergave-instellingen**.

    De **Azure-Web-App** venster wordt geopend op de **configuratie** tabblad.
2. Wijzig de naam van de verbindingsreeks DefaultConnection in de naam die u hebt gekozen bij het instellen van de SQL-database in de [publiceren naar Azure met SQL-Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artikel.

    Deze verbindingsreeks Azure automatisch gemaakt wanneer u de web-app met een bijbehorende database gemaakt, zodat deze de waarde voor de juiste verbinding al heeft. Alleen de naam wijzigt u op wat uw code zoekt.
3. Twee nieuwe verbindingsreeksen, met de naam AzureWebJobsStorage en AzureWebJobsDashboard toevoegen. Het databasetype instellen op **aangepaste**, en stel de waarde voor de verbinding op dezelfde waarde die u eerder hebt gebruikt voor de *Web.config* en *App.config* bestanden. (Zorg ervoor dat u de volledige verbindingsreeks, niet alleen de toegangssleutel opneemt en de aanhalingstekens zijn niet opgenomen.)

    Deze verbindingsreeksen worden gebruikt door de WebJobs SDK, één voor toepassingsgegevens en één voor logboekregistratie. Als u eerder hebt gezien, wordt voor toepassingsgegevens wordt ook gebruikt door de web-front-code.
4. Klik op **Opslaan**.

    ![Verbindingsreeksen in Azure Portal](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. In **Server Explorer**, met de rechtermuisknop op de web-app en klik vervolgens op **stoppen**.
6. Nadat de web-app stopt, opnieuw met de rechtermuisknop op de web-app en klik vervolgens op **Start**.

   De webtaak wordt automatisch gestart wanneer u publiceren, maar stopt wanneer u een configuratiewijziging. Om deze opnieuw starten, kunt u de web-app starten of opnieuw opstarten van de webtaak in de [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Het is doorgaans aanbevolen na een wijziging in de configuratie opnieuw opstarten van de web-app.
7. Vernieuw het browservenster met de web-app-URL in de adresbalk.

    De startpagina wordt weergegeven.
8. Maken van een advertentie, net als wanneer u [de toepassing lokaal uitgevoerd](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   De indexpagina toont zonder een miniatuur in eerste instantie.
9. Vernieuw de pagina na enkele seconden en de miniatuur weergegeven.

   Als de miniatuur niet wordt weergegeven, moet u wellicht wachten totdat een minuut of doet voor de webtaak op te starten. Als u na een tijdje nog steeds niet wordt weergegeven de miniatuur wanneer u de pagina vernieuwt, kan de webtaak niet automatisch hebt gestart. In dat geval gaat u naar de **App Services** blade in de [Azure-portal](https://portal.azure.com/), zoek uw web-app en klik vervolgens op **Start**.

### <a name="view-the-webjobs-sdk-dashboard"></a>De WebJobs SDK-dashboard weergeven
1. In de [Azure-portal](https://portal.azure.com/), selecteer de **blade App Services**, Ga naar uw web-app en selecteer **WebJobs**.
3. Selecteer de **logboeken** tabblad.

    ![Tabblad Logboeken](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    Een nieuw browsertabblad geopend met de WebJobs SDK-dashboard. Het dashboard ziet u dat de webtaak wordt uitgevoerd en wordt een lijst met functies in uw code waarmee de WebJobs SDK is geactiveerd.
4. Klik op een van de functies voor informatie over de uitvoering ervan.

    ![WebJobs SDK-dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK-dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    De **Replay-functie** knop op deze pagina zorgt ervoor dat de WebJobs SDK framework Roep de functie opnieuw, en geeft u een kans om de gegevens doorgegeven aan de functie eerst te wijzigen.

> [!NOTE]
> Wanneer u klaar bent met testen, kunt u eventueel de web-app, storage-account en uw exemplaar van SQL-Database verwijderen. De web-app is gratis, maar het SQL-storage-account en de database-exemplaar doorlopen kosten (zij, minimale vanwege de grootte klein). Ook als u de web-app actief laat, kunt iedereen die uw URL vindt advertenties maken en weergeven. 
>
>

### <a name="delete-your-web-app"></a>Uw web-app verwijderen
In de portal, gaat u naar de **App Services** blade Zoek en selecteer uw web-app en klik vervolgens op **verwijderen**. Als u alleen tijdelijk voorkomen dat anderen toegang hebben tot de web-app, klikt u op wilt **stoppen** in plaats daarvan. In dat geval blijven de kosten doorlopen voor het SQL-Database en Storage-account.

### <a name="delete-your-storage-account"></a>Uw storage-account verwijderen
Zie het verwijderen van uw opslagaccount [een opslagaccount verwijderen](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Uw database verwijderen
Zie het verwijderen van de SQL-database de [REST-API van Azure SQL Database](https://docs.microsoft.com/rest/api/sql/) documentatie.

## <a id="create"></a>De toepassing vanaf het begin maken
In deze sectie, doet u de volgende taken:

* Een Visual Studio-oplossing maken met een webproject.
* Voeg een klasse bibliotheek-project voor de data access-laag die wordt gedeeld tussen de front-end en back-end.
* Voeg een consoletoepassing-project voor de back-end met WebJobs-implementatie is ingeschakeld.
* NuGet-pakketten toevoegen.
* Projectverwijzingen instellen.
* Kopieer toepassingsbestanden code en configuratie van de gedownloade toepassing die u in de vorige sectie van de zelfstudie hebt gewerkt.
* Bekijk de onderdelen van de code die met Azure blobs en wachtrijen en de WebJobs SDK werken.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Een Visual Studio-oplossing maken met een webproject en class library-project
1. Kies in Visual Studio **bestand** > **nieuw** > **Project**.
2. In de **nieuw Project** dialoogvenster kiezen **Visual C#** > **Web** > **ASP.NET-webtoepassing (.NET Framework)**.
3. Noem het project ContosoAdsWeb, de naam van de oplossing ContosoAdsWebJobsSDK (wijzigen de oplossing als u deze wilt opslaan in dezelfde map als de gedownloade oplossing naam) en klik vervolgens op **OK**.

    ![Nieuw project](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. In de **nieuwe ASP.NET-webtoepassing** dialoogvenster, kies de MVC-sjabloon en selecteer **verificatie wijzigen**.

    ![Verificatie wijzigen](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. In de **verificatie wijzigen** dialoogvenster kiezen **geen verificatie**, en klik vervolgens op **OK**.

    ![Geen verificatie](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. In de **nieuwe ASP.NET-webtoepassing** dialoogvenster, klikt u op **OK**.

    Visual Studio maakt de oplossing en het webproject.
7. In **Solution Explorer**, met de rechtermuisknop op de oplossing (niet op het project) en kies **toevoegen** > **nieuw Project**.
8. In de **Add New Project** dialoogvenster kiezen **Visual C#** > **Classic Windows Desktop** > **Class Library (.NET Framework)** sjabloon.  
9. Geef het project de naam *ContosoAdsCommon* en klik vervolgens op **OK**.

    Dit project bevat de Entity Framework-context en het bijbehorende gegevensmodel die door de front-end- en back-end worden gebruikt. Als alternatief kan u de EF-gerelateerde klassen definiëren in het webproject en uit het project webtaak naar verwijzen. Maar vervolgens uw webtaak project een verwijzing naar webassembly's, die niet noodzakelijk zou hebben.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Voeg een consoletoepassing-project met webtaken implementatie is ingeschakeld
1. Met de rechtermuisknop op het webproject (niet de oplossing of de klasse library-project) en klik vervolgens op **toevoegen** > **nieuwe Azure webtaak Project**.

    ![Nieuwe Azure webtaak Project menuselectie](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. In de **toevoegen Azure webtaak** dialoogvenster ContosoAdsWebJob invoeren als zowel de **projectnaam** en de **naam van een webtaak**. Laat **webtaak uitvoeren modus** ingesteld op **continu uitvoeren**.
3. Klik op **OK**.

   Visual Studio maakt een consoletoepassing die is geconfigureerd om te implementeren als een webtaak wanneer u het webproject implementeren. Als u wilt dat deze de volgende taken uitgevoerd na het maken van het project:

   * Toegevoegd een *webtaak-publiceren settings.json* bestand in de eigenschappen van webtaak projectmap.
   * Toegevoegd een *webjobs list.json* bestand in de map web project eigenschappen.
   * Het Microsoft.Web.WebJobs.Publish NuGet-pakket in het project webtaak geïnstalleerd.

   Zie voor meer informatie over deze wijzigingen [WebJobs implementeren met behulp van Visual Studio](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>NuGet-pakketten toevoegen
De sjabloon nieuw project voor een webtaak project installeert automatisch de WebJobs SDK NuGet-pakket [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) en de bijbehorende afhankelijkheden.

Een van de WebJobs SDK-afhankelijkheden die automatisch wordt geïnstalleerd in het project webtaak is de Azure Storage Client-bibliotheek (SCL). U moet echter toe te voegen aan het webproject werken met blobs en wachtrijen.

1. Open de **NuGet-pakketten beheren** dialoogvenster voor de oplossing.
2. Selecteer in het linkerdeelvenster **geïnstalleerde pakketten**.
3. Zoek de *Azure Storage* van het pakket en klik vervolgens op **beheren**.
4. In de **projecten selecteren** Selecteer de **ContosoAdsWeb** selectievakje en klik vervolgens op **OK**.

    Alle drie de projecten gebruiken de Entity Framework werkt met gegevens in SQL-Database.
5. Selecteer in het linkerdeelvenster **Online**.
6. Zoek het NuGet pakket *EntityFramework* op en installeer het in alle drie de projecten.

### <a name="set-project-references"></a>Projectverwijzingen instellen
Web- en webtaak projecten werken met de SQL-database, zodat beide een verwijzing naar het project ContosoAdsCommon moeten.

1. Stel in het project ContosoAdsWeb een verwijzing in naar het project ContosoAdsCommon. (Met de rechtermuisknop op het project ContosoAdsWeb en klik vervolgens op **toevoegen** > **verwijzing**. 
2. In de **Reference Manager** dialoogvenster, **projecten** > **oplossing** > **ContosoAdsCommon**, en klik vervolgens op **OK**.)
   
    Het project webtaak moet verwijzingen voor het werken met installatiekopieën en voor het openen van verbindingsreeksen.

4. In het project ContosoAdsWebJob, stelt u een verwijzing naar `System.Drawing` en `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Code-en configuratiebestanden toevoegen
Deze zelfstudie wordt niet weergegeven hoe [maken van MVC-controllers en weergaven met steigers](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), hoe naar [schrijven van code voor Entity Framework die geschikt is voor SQL Server-databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), of [de basisbeginselen van asynchrone programmering in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Dus alles wat blijft te doen is de code en configuratie bestanden kopiëren vanuit de gedownloade oplossing naar de nieuwe oplossing. Nadat u dat doet, wordt de volgende secties weergeven en uitgelegd van de belangrijkste onderdelen van de code.

Als u bestanden wilt toevoegen aan een project of map, klikt u met de rechtermuisknop op het project of de map en klikt u vervolgens op **Add** > **Existing Item**. Selecteer de bestanden die u wilt en klikt u op **toevoegen**. Als u wordt gevraagd of u de bestaande bestanden wilt vervangen, klikt u op **Yes**.

1. Verwijder in het project ContosoAdsCommon het *Class1.cs* bestands- en toevoegen in plaats daarvan de volgende bestanden uit het gedownloade project.

   * *AD.cs*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. Voeg in het project ContosoAdsWeb de volgende bestanden uit het gedownloade project toe.

   * *Web.config*
   * *Global.asax.cs*  
   * In de *domeincontrollers* map: *AdController.cs*
   * In de *Views\Shared* map: *_Layout.cshtml* bestand
   * In de *Views\Home* map: *Index.cshtml*
   * In de *Views\Ad* map (Maak eerst de map): vijf *.cshtml* bestanden
3. Voeg de volgende bestanden uit het gedownloade project in het project ContosoAdsWebJob.

   * *App.config* (wijzigen van het type bestandsfilter **alle bestanden**)
   * *Program.cs*
   * *Functions.cs*

U kunt nu samenstellen, uitvoeren en de toepassing implementeren volgens de instructies eerder in de zelfstudie. Voordat u dat doet, moet u echter de webtaak die nog steeds worden uitgevoerd in de eerste web-app die u hebt geïmplementeerd om te stoppen. Anders verwerkt die webtaak Wachtrijberichten lokaal of door de app in een nieuwe web-app wordt uitgevoerd, omdat alles met behulp van hetzelfde opslagaccount is gemaakt.

## <a id="code"></a>De toepassingscode bekijken
De volgende secties worden de code voor het werken met de WebJobs SDK en Azure Storage-blobs en wachtrijen.

> [!NOTE]
> Voor de code die specifiek zijn voor de WebJobs SDK, gaat u naar de [Program.cs en Functions.cs](#programcs) secties.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
Het bestand Ad.cs definieert een enum voor advertentiecategorieën en een POCO-entiteitsklasse voor advertentie-informatie.

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
De klasse contosoadscontext geeft aan dat de Ad-klasse wordt gebruikt in een DbSet-verzameling Entity Framework wordt opgeslagen in een SQL-database.

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

De klasse heeft twee constructors. De eerste wordt gebruikt door het webproject en specificeert de naam van een verbindingsreeks die is opgeslagen in het Web.config-bestand of de Azure-runtime-omgeving. Met de tweede constructor kunt u de werkelijke verbindingsreeks doorgeven. Deze is nodig voor het project webtaak omdat het geen een Web.config-bestand. U weet al waar deze verbindingsreeks is opgeslagen. Later ziet u hoe de code de verbindingsreeks ophaalt bij het instantiëren van de DbContext-klasse.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon - BlobInformation.cs
De `BlobInformation` klasse wordt gebruikt voor het opslaan van informatie over een blob installatiekopie in een wachtrijbericht.

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
Code die wordt aangeroepen vanuit de `Application_Start`-methode maakt een blobcontainer met *afbeeldingen* en een wachtrij met *afbeeldingen* als deze nog niet bestaan. Dit zorgt ervoor dat wanneer u met behulp van een nieuw opslagaccount begint, de vereiste blobcontainer en wachtrij automatisch worden gemaakt.

De code krijgt toegang tot het opslagaccount met behulp van de verbindingsreeks voor opslag van de *Web.config* bestands- of Azure runtime-omgeving.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

Vervolgens wordt het een verwijzing naar de *installatiekopieën* blob-container, maakt u de container als deze niet al bestaat en stelt deze voor de nieuwe container toegangsrechten. Standaard staan nieuwe containers alleen clients met opslagaccountreferenties voor toegang tot blobs. De web-app moet de blobs openbaar zodat deze afbeeldingen met URL's die naar de afbeeldingsblobs wijzen verwijzen kan weergeven.

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

Vergelijkbare code wordt een verwijzing naar de *thumbnailrequest* wachtrij en een nieuwe wachtrij gemaakt. In dit geval is er geen machtigingswijziging nodig.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - _Layout.cshtml
Het bestand *_Layout.cshtml* stelt de naam van de app in de kop- en voettekst in en maakt een menu-item 'Ads'.

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Het bestand *Views\Home\Index.cshtml* geeft categoriekoppelingen weer op de startpagina. De koppelingen geven de integerwaarde van de `Category`-enum door in een queryreeksvariabele naar de pagina Ads Index.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
In het bestand *AdController.cs* roept de constructor de `InitializeStorage`-methode aan voor het maken van Azure Storage Client-bibliotheekobjecten die een API leveren voor het werken met blobs en wachtrijen.

Vervolgens haalt de code een verwijzing naar de *installatiekopieën* blobcontainer, zoals u eerder in gezien *Global.asax.cs*. Tijdens het uitvoeren, wordt standaard ingesteld [beleid voor opnieuw proberen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) geschikt is voor een web-app. Toepassing van het standaardbeleid voor opnieuw proberen met exponentieel uitstel kan ertoe leiden dat de web-app bij een tijdelijke fout langer dan een minuut blijft hangen vanwege herhaalde pogingen om het opnieuw te proberen. Het beleid dat hier is opgegeven, schrijft voor dat er na elke poging drie seconden wordt gewacht en dat het aantal pogingen maximaal drie bedraagt.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Door vergelijkbare code wordt een verwijzing naar de *afbeeldingen* wachtrij opgehaald.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

Het grootste deel van de controllercode is typerend voor het werken met een Entity Framework-gegevensmodel met behulp van een DbContext-klasse. Een uitzondering is de HttpPost `Create`-methode, waarmee een bestand wordt geüpload en opgeslagen in blobopslag. De modelbinder levert een [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx)-object aan de methode.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Als de gebruiker een bestand heeft geselecteerd om te uploaden, wordt het door de code geüpload en opgeslagen in een blob. Tegelijkertijd wordt het Ad-databaserecord bijgewerkt met een URL die naar de blob verwijst.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

De code die het uploaden uitvoert, bevindt zich in de `UploadAndSaveBlobAsync`-methode. Deze maakt een GUID-naam voor de blob, uploadt het bestand en slaat dit op, en retourneert een verwijzing naar de opgeslagen blob.

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

Nadat de HttpPost `Create` methode een blob uploadt en de database bijwerkt, maakt deze een wachtrijbericht om te informeren over de back-endproces dat een afbeelding gereed voor conversie naar een miniatuur is.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

De code voor de HttpPost `Edit` methode is vergelijkbaar, behalve dat als de gebruiker selecteert een nieuw afbeeldingsbestand, alle blobs die al bestaan voor deze advertentie moeten worden verwijderd.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Hier volgt de code die verwijderen van blobs wanneer u een advertentie verwijdert:

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
De *Index.cshtml* bestand miniaturen met de ad-gegevens worden weergegeven:

        <img  src="@Html.Raw(item.ThumbnailURL)" />

De *Details.cshtml* bestand de afbeelding wordt weergegeven:

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml en Edit.cshtml
De bestanden *Create.cshtml* en *Edit.cshtml* specificeren formuliercodering waarmee de controller het `HttpPostedFileBase`-object kan ophalen.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

Een `<input>`-element vertelt de browser dat deze een dialoogvenster voor bestandsselectie moet aanleveren.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
Wanneer de webtaak wordt gestart, wordt de `Main` methode roept de WebJobs SDK `JobHost.RunAndBlock` methode om te beginnen met het uitvoeren van functies in de huidige thread geactiveerd.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail methode
De WebJobs SDK roept deze methode wanneer er een wachtrijbericht wordt ontvangen. De methode een miniatuur gemaakt en plaatst de miniatuur-URL in de database.

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
            // be instantiated and disposed within the function.
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

* De `QueueTrigger` kenmerk de WebJobs SDK deze methode niet aanroepen wanneer een nieuw bericht wordt ontvangen op de thumbnailrequest wachtrij stuurt.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    De `BlobInformation` -object in bericht in de wachtrij is automatisch gedeserialiseerde in de `blobInfo` parameter. Wanneer de methode is voltooid, wordt het bericht van de wachtrij verwijderd. Als de methode is mislukt voordat wordt voltooid, wordt het bericht van de wachtrij niet verwijderd. Nadat een lease 10 minuten is verstreken, wordt het bericht beschikbaar voor het opnieuw worden opgepikt en verwerkt. Deze reeks won't voor onbepaalde tijd worden herhaald als een bericht altijd een uitzondering veroorzaakt. Na 5 mislukte pogingen een bericht te verwerken, het bericht is verplaatst naar een wachtrij met de naam {wachtrijnaam}-verontreinigd. Het maximum aantal pogingen kan worden geconfigureerd.
* De twee `Blob` kenmerken Geef objecten die zijn gekoppeld aan BLOB's: een voor de bestaande installatiekopie blob en één met een nieuwe miniatuur blob die de methode wordt gemaakt.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    BLOB-namen afkomstig zijn van de eigenschappen van de `BlobInformation` object in bericht in de wachtrij ontvangen (`BlobName` en `BlobNameWithoutExtension`). Als u de volledige functionaliteit van de Storage-clientbibliotheek, kunt u de `CloudBlockBlob` klasse werken met blobs. Als u gebruiken als code die is geschreven wilt naar het werken met `Stream` objecten, kunt u de `Stream` klasse.

Zie de volgende bronnen voor meer informatie over het schrijven van functies die WebJobs SDK kenmerken gebruiken:

* [Azure Queue Storage gebruiken met de WebJobs-SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Het gebruik van Azure Blob Storage met de WebJobs-SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Azure Table Storage gebruiken met de WebJobs-SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Azure Service Bus gebruiken met de WebJobs-SDK](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Als uw web-app wordt uitgevoerd op meerdere virtuele machines, meerdere WebJobs wordt tegelijkertijd worden uitgevoerd en in sommige scenario's die dit kan leiden tot dezelfde gegevens meerdere keren wordt verwerkt. Dit is niet een probleem als u de ingebouwde wachtrij, blobs en Service Bus-triggers. De SDK zorgt ervoor dat uw functies slechts één keer worden verwerkt voor elk bericht of blob.
> * Zie voor meer informatie over het correct afsluiten implementeren [correct afsluiten](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * De code in de `ConvertImageToThumbnailJPG` methode (niet weergegeven) maakt gebruik van klassen in de `System.Drawing` naamruimte voor eenvoud. De klassen in deze naamruimte zijn echter bedoeld voor gebruik met Windows Forms. Ze worden niet ondersteund voor gebruik in een Windows- of ASP.NET-service. Zie [Afbeeldingen dynamisch genereren](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) en [Alles over het wijzigen van het formaat van afbeeldingen](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) voor meer informatie over opties voor de verwerking van afbeeldingen.
>
>

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u een eenvoudige toepassing met meerdere lagen die gebruikmaakt van de WebJobs SDK voor de verwerking van de back-end gezien. Deze sectie vindt u enkele suggesties voor meer informatie over toepassingen met meerdere lagen ASP.NET en WebJobs.

### <a name="missing-features"></a>Ontbrekende functies
De toepassing heeft gehouden eenvoudige voor een zelfstudie aan de slag. In een echte toepassing die u wilt implementeren [afhankelijkheidsinjectie](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) en de [opslagplaatsen en werkeenheden](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), gebruik [een interface voor logboekregistratie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), gebruik [EF Code First-migraties](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) voor het beheren van wijzigingen in het gegevensmodel en gebruik [EF-Verbindingstolerantie](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) voor het beheren van tijdelijke netwerkfouten.

### <a name="scaling-webjobs"></a>Schalen WebJobs
WebJobs uitgevoerd in de context van een web-app en zijn niet afzonderlijk worden schaalbaar. Als u een standaard web-app-exemplaar hebt, hebt u slechts één exemplaar van de achtergrondproces wordt uitgevoerd en het gebruik van een aantal van de server-resources (CPU, geheugen, enzovoort) die anders beschikbaar zijn zou voor het leveren van webinhoud.

Als het verkeer door de tijd van de dag of week varieert, en als de back-end-verwerking die u wilt kunt wachten, kunt u uw WebJobs om uit te voeren op tijdstippen met weinig verkeer kan plannen. Als de belasting nog steeds te hoog is voor deze oplossing wordt, kunt u de back-end uitvoeren als een webtaak in een speciale afzonderlijke web-app voor dat doel. U kunt uw back-end-web-app vervolgens onafhankelijk van elkaar schalen van uw frontend-web-app.

Zie voor meer informatie [WebJobs schalen](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Web-app time-out afsluiten-keuzelijsten voorkomen
Om te controleren of uw WebJobs altijd worden uitgevoerd en u hebt uitgevoerd op alle exemplaren van uw web-app, zodat de [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) functie.

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a>Met behulp van de WebJobs SDK buiten WebJobs
Een programma dat gebruikmaakt van de WebJobs SDK beschikt niet over in Azure in een webtaak uit te voeren. Lokaal kunt uitvoeren, en ook in andere omgevingen zoals een werkrol Cloudservice of een Windows-service kan worden uitgevoerd. Echter, u kunt alleen toegang tot het dashboard WebJobs SDK via een Azure-web-app. Gebruik het dashboard dat u hebt verbinding maken met de web-app van het opslagaccount dat u de verbindingsreeks AzureWebJobsDashboard door in te stellen de **configureren** tabblad van de klassieke portal. U kunt vervolgens naar het Dashboard krijgen met behulp van de volgende URL:

https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions

Zie voor meer informatie [ophalen van een dashboard voor lokale ontwikkeling met de WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), maar houd er rekening mee dat er een oude naam van verbindingsreeks wordt weergegeven.

### <a name="more-webjobs-documentation"></a>Documentatie voor meer WebJobs
Zie voor meer informatie [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226).
