---
title: aaaGet slag met Azure Cloud Services en ASP.NET | Microsoft Docs
description: Meer informatie over hoe toocreate een app met meerdere lagen met ASP.NET MVC en Azure. Hallo-app wordt uitgevoerd in een cloudservice met de Webrol en een werkrol. De app maakt gebruik van Entity Framework, SQL Database, en wachtrijen en blobs van Azure Storage.
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>Aan de slag met Azure Cloud Services en ASP.NET

## <a name="overview"></a>Overzicht
Deze zelfstudie laat zien hoe toocreate een meerlaagse .NET-toepassing met een ASP.NET MVC-front-, en implementeert tooan [Azure-cloudservice](cloud-services-choose-me.md). toepassing gebruikt Hallo [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), Hallo [Azure Blob-service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), en Hallo [Azure Queue-service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern). U kunt [Hallo Visual Studio-project downloaden](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) van Hallo MSDN-Codegalerie.

Hallo-zelfstudie ziet u hoe toobuild en Voer Hallo toepassing lokaal door hoe toodeploy het tooAzure en uitvoeren in Hallo cloud, en hoe toobuild deze vanaf het begin. U kunt starten door gebouw vanaf het begin en vervolgens Hallo test en stappen daarna implementeren als u liever.

## <a name="contoso-ads-application"></a>Toepassing Contoso Ads
Hallo-toepassing is een bulletinboard voor advertenties. Gebruikers maken een advertentie door de tekst in te voeren en een afbeelding te uploaden. Zien ze een lijst met advertenties met miniatuurafbeeldingen en ze Hallo afbeelding kunnen zien wanneer ze een ad toosee Hallo details selecteren.

![Advertentielijst](./media/cloud-services-dotnet-get-started/list.png)

Hallo-toepassing hello gebruikt [wachtrijgerichte werkpatroon](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff load Hallo CPU-intensief werk van het maken van miniatuurweergaven tooa back-end-proces.

## <a name="alternative-architecture-websites-and-webjobs"></a>Alternatieve architectuur: Websites en WebJobs
Deze zelfstudie laat zien hoe toorun front-end- en back-end in een Azure cloud service. Een alternatief is toorun Hallo front-end in een [Azure-website](/services/web-sites/) en gebruik Hallo [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) functie (momenteel in preview) voor Hallo back-end. Zie voor een zelfstudie die gebruikmaakt van WebJobs [aan de slag met Azure WebJobs SDK Hallo](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md). Zie voor meer informatie over hoe toochoose Hallo services waar beste uw scenario past, [vergelijking van Azure Websites, Cloudservices en virtuele machines](../app-service-web/choose-web-site-cloud-service-vm.md).

## <a name="what-youll-learn"></a>Wat u leert
* Hoe tooenable computer klaarmaken voor het ontwikkelen van Azure door het installeren van hello Azure SDK.
* Hoe een Visual Studio toocreate cloud service-project met een ASP.NET MVC-Webrol en een werkrol.
* Hoe Hallo tootest cloudserviceproject lokaal hello Azure-opslagemulator gebruiken.
* Hoe toopublish Hallo cloud project tooan Azure-cloudservice en testen met behulp van een Azure storage-account.
* Hoe tooupload bestanden en deze opslaan op Hallo Azure Blob-service.
* Hoe toouse hello Azure Queue-service voor communicatie tussen lagen.

## <a name="prerequisites"></a>Vereisten
Hallo zelfstudie wordt ervan uitgegaan dat u begrijpt [basisconcepten van Azure-cloudservices](cloud-services-choose-me.md) zoals *Webrol* en *werkrol* terminologie.  Ook wordt ervan uitgegaan dat u weet hoe toowork met [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) of [webformulieren](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projecten in Visual Studio. Hallo-voorbeeldtoepassing gebruikt MVC, maar de meeste Hallo zelfstudie geldt ook tooWeb formulieren.

U kunt Hallo app lokaal zonder een Azure-abonnement uitvoeren, maar moet u één toodeploy Hallo toepassing toohello cloud. Als u geen account hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) of [zich aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).

Hallo zelfstudie instructies werken met een van de volgende producten Hallo:

* Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

Als u een van deze geen hebt, wordt Visual Studio kan worden automatisch geïnstalleerd wanneer u hello Azure SDK installeren.

## <a name="application-architecture"></a>Toepassingsarchitectuur
Hallo app slaat de advertenties in een SQL-database, met behulp van Entity Framework Code First toocreate Hallo tabellen en toegang tot Hallo gegevens. Voor elke advertentie Hallo Hallo database winkels twee URL's, één voor afbeelding op volledige grootte en één voor Hallo miniatuur.

![Advertentietabel](./media/cloud-services-dotnet-get-started/adtable.png)

Wanneer een gebruiker een afbeelding uploadt, front-uitgevoerd van Hallo in een Webrol slaat Hallo-installatiekopie in een [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), en Hallo ad informatie opslaat in de database Hallo met een URL die toohello blob verwijst. AT Hallo dezelfde tijd, wordt een bericht tooan Azure-wachtrij geschreven. Een back-end-proces dat periodiek wordt uitgevoerd in een werkrol Hallo wachtrij voor nieuwe berichten worden opgevraagd. Wanneer een nieuw bericht wordt weergegeven, Hallo werkrol een miniatuur voor de betreffende afbeelding gemaakt en updates Hallo miniaturen URL databaseveld voor de advertentie. Hallo volgende diagram toont de wisselwerking tussen onderdelen van de toepassing hello Hallo.

![Architectuur van Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a>Hallo voltooid oplossing downloaden en uitvoeren
1. Downloaden en uitpakken Hallo [voltooide oplossing](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).
2. Start Visual Studio.
3. Van Hallo **bestand** in het menu **Open Project**, gaat u toowhere u Hallo oplossing gedownload en open het oplossingsbestand Hallo.
4. Druk op CTRL + SHIFT + B toobuild Hallo oplossing.

    Standaard herstelt Visual Studio automatisch Hallo NuGet-pakketinhoud die niet is opgenomen in Hallo *.zip* bestand. Als hello-pakketten niet worden hersteld, deze handmatig installeren door te gaan toohello **NuGet-pakketten beheren voor oplossing** in het dialoogvenster en te klikken op Hallo **herstellen** knop Hallo rechts bovenaan.
5. In **Solution Explorer**, zorg ervoor dat **ContosoAdsCloudService** is geselecteerd als opstartproject Hallo.
6. Als u Visual Studio 2015 gebruikt of hoger, Hallo SQL Server-verbindingsreeks in de toepassing hello wijzigt *Web.config* bestand van het ContosoAdsWeb-project hello en in Hallo *ServiceConfiguration.Local.cscfg* -bestand van Hallo ContosoAdsCloudService-project. In elk geval kan ook '(localdb) \v11.0' wijzigen '(localdb) \MSSQLLocalDB'.
7. Druk op CTRL + F5 toorun Hallo toepassing.

    Wanneer u een cloudserviceproject lokaal uitvoert, roept Visual Studio automatisch hello Azure *rekenemulator* en Azure *opslagemulator*. Hallo compute emulator maakt gebruik van uw computer resources toosimulate Hallo-Webrol en omgevingen voor worker-rol. Hallo-opslagemulator maakt gebruik van een [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) toosimulate Azure cloud-opslag van de database.

    Hallo waarna eerste keer dat u een cloudserviceproject uitvoert een minuut Hallo emulators toostart up. Wanneer de emulator is opgestart, opent de standaardbrowser Hallo toohello toepassing-startpagina.

    ![Architectuur van Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. Klik op **Create an Ad**.
9. Voer enkele testgegevens in en selecteer een *.jpg* tooupload installatiekopie en klik vervolgens op **maken**.

    ![De pagina Create](./media/cloud-services-dotnet-get-started/create.png)

    Hallo app gaat toohello indexpagina, maar niet wordt weergegeven een miniatuur voor de nieuwe ad Hallo omdat die verwerking nog niet heeft plaatsgevonden.
10. Wacht even en vernieuw vervolgens Hallo Index pagina toosee Hallo miniatuur.

     ![De indexpagina](./media/cloud-services-dotnet-get-started/list.png)
11. Klik op **Details** voor uw afbeelding van ad toosee Hallo.

     ![De pagina Details](./media/cloud-services-dotnet-get-started/details.png)

U hebt de toepassing hello uitgevoerd volledig op uw lokale computer, zonder verbinding toohello cloud. Hallo-opslagemulator slaat Hallo wachtrij en blobgegevens in een SQL Server Express LocalDB-database en de toepassing hello Hallo ad-gegevens opslaat in een andere LocalDB-database. Entity Framework Code First automatisch gemaakte Hallo ad-database Hallo Hallo web-app heeft geprobeerd tooaccess eerst het.

In de volgende sectie Hallo configureert u Hallo oplossing toouse Azure-cloudbronnen voor wachtrijen, blobs en Hallo toepassingsdatabase wanneer deze wordt uitgevoerd in de cloud Hallo. Als u lokaal toocontinue toorun wilden maar gebruik van cloud- en databasebronnen, kunt u dat doen. Het is alleen een kwestie van het instellen van verbindingsreeksen, u ziet hoe toodo.

## <a name="deploy-hello-application-tooazure"></a>Hallo toepassing tooAzure implementeren
U voert de volgende stappen toorun Hallo toepassing in de cloud Hallo Hallo:

* Een Azure-cloudservice maken.
* Een Azure SQL-database maken.
* Een Azure-opslagaccount maken.
* Configureer Hallo oplossing toouse uw Azure SQL database als deze wordt uitgevoerd in Azure.
* Configureer Hallo oplossing toouse uw Azure storage-account wanneer deze wordt uitgevoerd in Azure.
* Hallo project tooyour Azure cloudservice implementeren.

### <a name="create-an-azure-cloud-service"></a>Een Azure-cloudservice maken
Een Azure-cloudservice is Hallo omgeving Hallo toepassing wordt uitgevoerd in.

1. Open in uw browser Hallo [Azure-portal](https://portal.azure.com).
2. Klik op **Nieuw > Berekenen > Cloudservice**.

3. Voer in Hallo DNS-naam-invoervak een URL-voorvoegsel voor Hallo-cloudservice.

    Deze URL heeft toobe uniek zijn.  U krijgt een foutmelding als Hallo voorvoegsel dat u kiest al in gebruik is.
4. Geef een nieuwe resourcegroep voor Hallo-service. Klik op **nieuw** en typ een naam in Hallo Resource groep invoervak, zoals CS_contososadsRG.

5. Hallo-regio waar u toodeploy Hallo toepassing kiezen.

    Dit veld geeft aan in welk datacenter uw cloudservice zal worden gehost. Voor een productietoepassing kiest u Hallo regio dichtstbijzijnde tooyour klanten. Voor deze zelfstudie kiest Hallo regio dichtstbijzijnde tooyou.
5. Klik op **Create**.

    In Hallo volgende afbeelding, een cloudservice met Hallo URL CSvccontosoads.cloudapp.net gemaakt.

    ![Nieuwe cloudservice](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>Een Azure SQL-database maken
Wanneer Hallo-app wordt uitgevoerd in de cloud hello, wordt een cloud-gebaseerde database gebruikt.

1. In Hallo [Azure-portal](https://portal.azure.com), klikt u op **Nieuw > Databases > SQL-Database**.
2. In Hallo **databasenaam** Voer *contosoads*.
3. In Hallo **resourcegroep**, klikt u op **gebruik bestaande** en selecteer Hallo resourcegroep gebruikt voor het Hallo-cloudservice.
4. Klik in het Hallo-installatiekopie, volgt op **Server - vereiste instellingen configureren** en **Maak een nieuwe server**.

    ![Tunnel toodatabase server](./media/cloud-services-dotnet-get-started/newdb.png)

    Als uw abonnement beschikt al over een server, kunt u ook die server selecteren uit de vervolgkeuzelijst Hallo.
5. In Hallo **servernaam** Voer *csvccontosodbserver*.

6. Geef een **Aanmeldingsnaam** en een **Wachtwoord** op voor de beheerder.

    Als u **Een nieuwe server maken** hebt geselecteerd, voert u hier geen bestaande naam en bestaand wachtwoord in. U invoert een nieuwe naam en het wachtwoord dat u nu toouse later definieert wanneer u Hallo database. Als u een server die u eerder hebt gemaakt, hebt geselecteerd, wordt u gevraagd voor Hallo wachtwoord toohello gebruiker met beheerdersrechten account die u al hebt gemaakt.
7. Kies dezelfde Hallo **locatie** die u hebt gekozen voor Hallo-cloudservice.

    Wanneer Hallo-cloudservice en de database zich in verschillende datacenters (verschillende regio's), de latentie toe en wordt u gefactureerd voor de bandbreedte buiten het datacenter Hallo. Bandbreedte binnen een datacenter is gratis.
8. Controleer **toestaan azure-services tooaccess server**.
9. Klik op **Selecteer** voor Hallo nieuwe server.

    ![Nieuwe SQL-databaseserver](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. Klik op **Create**.

### <a name="create-an-azure-storage-account"></a>Een Azure-opslagaccount maken
Een Azure-opslagaccount biedt resources voor het opslaan van wachtrij en de blob-gegevens in de cloud Hallo.

In een echte toepassing maakt u meestal afzonderlijke accounts voor toepassingsgegevens versus logboekgegevens, en afzonderlijke accounts voor testgegevens versus productiegegevens. Voor deze zelfstudie gebruikt u slechts één account.

1. In Hallo [Azure-portal](https://portal.azure.com), klikt u op **Nieuw > opslag > opslagaccount - blob, bestand, tabel, wachtrij**.
2. In Hallo **naam** Voer een URL-voorvoegsel.

    Dit voorvoegsel wordt samen met Hallo tekst onder Hallo vak worden Hallo unieke URL tooyour storage-account. Als het voorvoegsel dat u invoert Hallo is al door iemand anders gebruikt, hebt u toochoose een ander voorvoegsel.
3. Set Hallo **implementatiemodel** te*klassieke*.

4. Set Hallo **replicatie** vervolgkeuzelijst te**lokaal redundante opslag**.

    Wanneer geo-replicatie is ingeschakeld voor een opslagaccount, is Hallo opgeslagen inhoud gerepliceerde tooa secundair datacenter tooenable failover als er een noodgeval op de primaire locatie Hallo optreedt. Geo-replicatie kan extra kosten met zich meebrengen. Voor test- en -accounts in het algemeen niet de bedoeling toopay voor geo-replicatie. Zie [Een opslagaccount maken, beheren of verwijderen](../storage/common/storage-create-storage-account.md) voor meer informatie.

5. In Hallo **resourcegroep**, klikt u op **gebruik bestaande** en selecteer Hallo resourcegroep gebruikt voor het Hallo-cloudservice.
6. Set Hallo **locatie** vervolgkeuzelijst toohello dezelfde regio die u hebt gekozen voor Hallo-cloudservice.

    Wanneer Hallo cloud service- en storage-account zich in verschillende datacenters (verschillende regio's), de latentie toe en wordt u gefactureerd voor de bandbreedte buiten het datacenter Hallo. Bandbreedte binnen een datacenter is gratis.

    Azure-affiniteitsgroepen bieden een mechanisme toominimize Hallo afstand tussen resources in een datacenter, waardoor latentie kan verminderen. In deze zelfstudie worden geen affiniteitsgroepen gebruikt. Zie voor meer informatie [hoe tooCreate een affiniteit groepeert in Azure](http://msdn.microsoft.com/library/jj156209.aspx).
7. Klik op **Create**.

    ![Nieuw opslagaccount](./media/cloud-services-dotnet-get-started/newstorage.png)

    In afbeelding hello, een opslagaccount is gemaakt met Hallo URL `csvccontosoads.core.windows.net`.

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a>Hallo oplossing toouse configureren uw Azure SQL database als deze wordt uitgevoerd in Azure
Hallo-webproject hello werkrolproject elke heeft een eigen databaseverbindingsreeks en elk toopoint toohello Azure SQL-database moet bij het Hallo-app wordt uitgevoerd in Azure.

U gebruikt een [Web.config-transformatie](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) voor Hallo-Webrol en een cloud service-omgeving-instelling voor Hallo-werkrol.

> [!NOTE]
> In deze sectie en de volgende sectie hello slaat u referenties op in projectbestanden. [Sla gevoelige gegevens niet op in openbare broncodeopslagplaatsen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).
>
>

1. Open in het project ContosoAdsWeb Hallo Hallo *Web.Release.config* transformatiebestand voor de toepassing hello *Web.config* , verwijder Hallo Opmerkingenblok met een `<connectionStrings>` -element en plak Hallo code in plaats daarvan te volgen.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    Laat Hallo bestand geopend voor bewerken.
2. In Hallo [Azure-portal](https://portal.azure.com), klikt u op **SQL-Databases** in het linkerdeelvenster hello, klikt u op Hallo-database die u voor deze zelfstudie hebt gemaakt en klik vervolgens op **verbindingsreeksen weergeven**.

    ![Verbindingsreeksen weergeven](./media/cloud-services-dotnet-get-started/showcs.png)

    Hallo portal worden verbindingsreeksen met een tijdelijke aanduiding voor Hallo wachtwoord weergegeven.

    ![Verbindingsreeksen](./media/cloud-services-dotnet-get-started/connstrings.png)
3. In Hallo *Web.Release.config* transformatiebestand `{connectionstring}` en plak in de plaats Hallo ADO.NET-verbindingsreeks uit hello Azure-portal.
4. In de verbindingsreeks Hallo die u in Hallo geplakt *Web.Release.config* transformatiebestand, vervangen door `{your_password_here}` met Hallo wachtwoord die u hebt gemaakt voor Hallo nieuwe SQL-database.
5. Hallo-bestand opslaan.  
6. Selecteer en kopieer de verbindingsreeks Hallo (zonder Hallo aanhalingstekens rond) voor gebruik in de volgende stappen uit voor het configureren van het werkrolproject Hallo Hallo.
7. In **Solution Explorer**onder **rollen** hello cloudserviceproject met de rechtermuisknop op **ContosoAdsWorker** en klik vervolgens op **eigenschappen**.

    ![Roleigenschappen](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. Klik op Hallo **instellingen** tabblad.
9. Wijziging **serviceconfiguratie** te**Cloud**.
10. Selecteer Hallo **waarde** veld voor Hallo `ContosoAdsDbConnectionString` instelling en plak Hallo verbindingsreeks die u hebt gekopieerd uit de vorige sectie Hallo Hallo zelfstudie.

     ![Databaseverbindingsreeks voor werkrol](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. Sla uw wijzigingen op.  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a>Hallo oplossing toouse configureren uw Azure-opslagaccount als deze wordt uitgevoerd in Azure
Azure storage-account-verbindingsreeksen voor zowel het webrolproject Hallo als Hallo werkrolproject worden opgeslagen in de omgevingsinstellingen in het cloudserviceproject Hallo. Er is een afzonderlijke reeks instellingen toobe gebruikt bij het Hallo-toepassing lokaal wordt uitgevoerd en wanneer deze wordt uitgevoerd in de cloud Hallo voor elk project. U zult Hallo cloudomgevingsinstellingen voor zowel web als het werkrolproject bijwerken.

1. In **Solution Explorer**, met de rechtermuisknop op **ContosoAdsWeb** onder **rollen** in Hallo **ContosoAdsCloudService** project en klik vervolgens op **Eigenschappen**.

    ![Roleigenschappen](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. Klik op Hallo **instellingen** tabblad. In Hallo **serviceconfiguratie** vervolgkeuzelijst Kies **Cloud**.

    ![Cloudconfiguratie](./media/cloud-services-dotnet-get-started/sccloud.png)
3. Selecteer Hallo **StorageConnectionString** invoer en u ziet een weglatingsteken (**...** ) knop Hallo rechts Hallo-regel op. Klik op Hallo weglatingsteken knop tooopen hello **Create Storage Account Connection String** in het dialoogvenster.

    ![Het dialoogvenster Create Storage Connection String](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. In Hallo **Create Storage Connection String** in het dialoogvenster, klikt u op **uw abonnement**, kies Hallo storage-account dat u eerder hebt gemaakt en klik vervolgens op **OK**. Als u nog niet bent aangemeld, wordt u gevraagd om uw referenties voor uw Azure-account op te geven.

    ![Verbindingsreeks voor opslag maken](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. Sla uw wijzigingen op.
6. Volg Hallo dezelfde procedure die u voor Hallo gebruikt `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` verbindingsreeks.

    Deze verbindingsreeks wordt gebruikt voor logboekregistratie.
7. Volg Hallo dezelfde procedure die u voor Hallo gebruikt **ContosoAdsWeb** rol tooset beide verbindingsreeksen voor Hallo **ContosoAdsWorker** rol. Vergeet niet tooset **serviceconfiguratie** te**Cloud**.

Hallo rolomgevingsinstellingen dat u hebt geconfigureerd met behulp van Visual Studio-gebruikersinterface Hallo worden opgeslagen in de volgende bestanden in de project ContosoAdsCloudService Hallo Hallo:

* *ServiceDefinition.csdef* -namen Hallo definieert.
* *ServiceConfiguration.Cloud.cscfg* -levert waarden voor wanneer Hallo-app wordt uitgevoerd in de cloud Hallo.
* *ServiceConfiguration.Local.cscfg* -levert waarden voor wanneer Hallo app lokaal wordt uitgevoerd.

Hallo ServiceDefinition.csdef omvat bijvoorbeeld Hallo definities te volgen:

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

En Hallo *ServiceConfiguration.Cloud.cscfg* bestand bevat Hallo-waarden die u hebt ingevoerd voor deze instellingen in Visual Studio.

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

Hallo `<Instances>` instelling bepaalt u het aantal virtuele machines die door Azure wordt uitgevoerd Hallo worker-rol op Hallo. Hallo [Vervolgstappen](#next-steps) sectie bevat koppelingen toomore informatie over het uitbreiden van een cloudservice

### <a name="deploy-hello-project-tooazure"></a>Hallo project tooAzure implementeren
1. In **Solution Explorer**, klik met de rechtermuisknop Hallo **ContosoAdsCloudService** cloudproject en selecteer vervolgens **publiceren**.

   ![Het menu Publish](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. In Hallo **aanmelden** stap Hallo **Publish Azure Application** wizard, klikt u op **volgende**.

    ![Aanmeldingsstap](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. In Hallo **instellingen** stap van de wizard hello, klikt u op **volgende**.

    ![De stap Settings](./media/cloud-services-dotnet-get-started/pubsettings.png)

    Standaard-instellingen in Hallo Hallo **Geavanceerd** tabblad zijn afdoende voor deze zelfstudie. Zie voor meer informatie over geavanceerde tabblad Hallo [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).
4. In Hallo **samenvatting** stap, klikt u op **publiceren**.

    ![De stap Summary](./media/cloud-services-dotnet-get-started/pubsummary.png)

   Hallo **Azure Activity Log** venster wordt geopend in Visual Studio.
5. Klik op Hallo pijl naar rechts pictogram tooexpand Hallo details van de implementatie.

    Hallo-implementatie kan too5 minuten of meer toocomplete duren.

    ![Het venster Azure Activity Log](./media/cloud-services-dotnet-get-started/waal.png)
6. Als de implementatiestatus Hallo voltooid is, klikt u op Hallo **Web-app-URL** toostart Hallo-toepassing.
7. U kunt nu Hallo app testen door maken, weergeven en bewerken van advertenties, net als bij u Hallo toepassing lokaal uitgevoerd.

> [!NOTE]
> Wanneer u bent klaar met testen, verwijderen of stoppen Hallo-cloudservice. Zelfs als u geen Hallo cloudservice gebruikt, lopen de kosten omdat bronnen voor virtuele machines worden gereserveerd. Als u de cloudservice actief laat, kan bovendien iedereen die uw URL vindt, advertenties maken en weergeven. In Hallo [Azure-portal](https://portal.azure.com), gaat u toohello **overzicht** tabblad voor de cloudservice en klik vervolgens op Hallo **verwijderen** knop bovenaan Hallo Hallo pagina. Als u alleen wilt tootemporarily voorkomen dat anderen toegang hebben tot Hallo-site, klikt u op **stoppen** in plaats daarvan. In dat geval blijven de kosten tooaccrue. Wanneer u ze niet meer nodig hebt, kunt u een vergelijkbare procedure toodelete Hallo account voor SQL database- en opslaggroepen volgen.
>
>

## <a name="create-hello-application-from-scratch"></a>Hallo toepassing vanaf het begin maken
Als u nog niet hebt gedownload [toepassing hello voltooid](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), doet u dat nu. U kopieert de bestanden uit project Hallo gedownload naar het nieuwe project Hallo.

Hallo Contoso Ads-toepassing maken omvat Hallo stappen te volgen:

* Met Visual Studio een cloudserviceoplossing maken.
* NuGet-pakketten bijwerken en toevoegen.
* Projectverwijzingen instellen.
* Verbindingsreeksen configureren.
* Codebestanden toevoegen.

Nadat het Hallo-oplossing is gemaakt, bekijkt u Hallo-code die uniek toocloud serviceprojecten en Azure blobs en wachtrijen.

### <a name="create-a-cloud-service-visual-studio-solution"></a>Met Visual Studio een cloudserviceoplossing maken
1. Kies in Visual Studio **nieuw Project** van Hallo **bestand** menu.
2. In het linkerdeelvenster van Hallo Hallo **nieuw Project** dialoogvenster Vouw **Visual C#** en kies **Cloud** sjablonen, en kies vervolgens Hallo **Azure Cloud Service** sjabloon.
3. Naam Hallo-project en de oplossing ContosoAdsCloudService en klik vervolgens op **OK**.

    ![Nieuw project](./media/cloud-services-dotnet-get-started/newproject.png)
4. In Hallo **New Azure Cloud Service** dialoogvenster Voeg een Webrol en een werkrol toe. Hallo-Webrol ContosoAdsWeb een naam en de naam Hallo werkrol ContosoAdsWorker. (Hallo potloodpictogram in Hallo rechterdeelvenster toochange Hallo standaardnamen van Hallo-functies gebruiken.)

    ![Nieuw cloudserviceproject](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. Wanneer er Hallo **nieuw ASP.NET-Project** in het dialoogvenster voor de Webrol hello, kies Hallo MVC-sjabloon en klik vervolgens op **verificatie wijzigen**.

    ![Verificatie wijzigen](./media/cloud-services-dotnet-get-started/chgauth.png)
6. In Hallo **verificatie wijzigen** dialoogvenster Kies **geen verificatie**, en klik vervolgens op **OK**.

    ![Geen verificatie](./media/cloud-services-dotnet-get-started/noauth.png)
7. In Hallo **nieuw ASP.NET-Project** dialoogvenster, klikt u op **OK**.
8. In **Solution Explorer**, met de rechtermuisknop op het Hallo-oplossing (niet een van de Hallo projecten) en kies **Add - New Project**.
9. In Hallo **Add New Project** dialoogvenster Kies **Windows** onder **Visual C#** in linkerdeelvenster hello, en klik vervolgens op Hallo **Class Library** de sjabloon.  
10. Naam Hallo project *ContosoAdsCommon*, en klik vervolgens op **OK**.

    U moet tooreference Hallo Entity Framework context en Hallo-gegevensmodel van web- en werkrollen rol projecten. Als alternatief kan u Hallo EF-gerelateerde klassen definiëren in het webrolproject hello en van Hallo werkrolproject naar verwijzen. Maar in de alternatieve methode hello, uw werkrolproject een assembly-verwijzingen tooweb die niet meer nodig hebt.

### <a name="update-and-add-nuget-packages"></a>NuGet-pakketten bijwerken en toevoegen
1. Open Hallo **NuGet-pakketten beheren** in het dialoogvenster voor het Hallo-oplossing.
2. Selecteer bovenaan Hallo Hallo-venster, **Updates**.
3. Zoek naar Hallo *WindowsAzure.Storage* van het pakket en als het in de lijst hello, selecteert u deze en selecteer Hallo web- en werkrollen projecten tooupdate in en klik vervolgens op **Update**.

    Hallo opslagclientbibliotheek wordt vaker bijgewerkt dan Visual Studio-projectsjablonen, zodat u vaak die Hallo-versie in een nieuw gemaakt project moet toobe bijgewerkt zult.
4. Selecteer bovenaan Hallo Hallo-venster, **Bladeren**.
5. Hallo zoeken *EntityFramework* NuGet-pakket en installeer het in alle drie de projecten.
6. Hallo zoeken *Microsoft.WindowsAzure.ConfigurationManager* NuGet-pakket en installeer het in het werkrolproject Hallo.

### <a name="set-project-references"></a>Projectverwijzingen instellen
1. In Hallo ingesteld project ContosoAdsWeb een verwijzing toohello ContosoAdsCommon project. Met de rechtermuisknop op Hallo ContosoAdsWeb-project en klik vervolgens op **verwijzingen** - **Add References**. In Hallo **Reference Manager** dialoogvenster, **Solution – Projects** selecteren in het linkerdeelvenster Hallo **ContosoAdsCommon**, en klik vervolgens op **OK**.
2. In Hallo ingesteld project ContosoAdsWorker een verwijzing toohello Contosoadscommon project.

    ContosoAdsCommon bevat Hallo Entity Framework data model en in het contextmenu klasse, die wordt gebruikt door beide Hallo front-end en back-end.
3. Stel in Hallo project ContosoAdsWorker een verwijzing te`System.Drawing`.

    Deze assembly wordt gebruikt door Hallo back-end tooconvert installatiekopieën toothumbnails.

### <a name="configure-connection-strings"></a>Verbindingsreeksen configureren
In deze sectie configureert u Azure Storage- en SQL-verbindingsreeksen om lokaal te testen. Hallo implementatie-instructies eerder in Hallo zelfstudie wordt uitgelegd hoe tooset Hallo verbinding tekenreeksen voor wanneer hello app wordt uitgevoerd in de cloud Hallo.

1. In Hallo ContosoAdsWeb-project, open Hallo toepassing Web.config-bestand en insert Hallo volgende `connectionStrings` element na Hallo `configSections` element.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Als u Visual Studio 2015 of hoger gebruikt, vervangt u 'v11.0' door 'MSSQLLocalDB'.
2. Sla uw wijzigingen op.
3. Hallo ContosoAdsCloudService-project met de rechtermuisknop op ContosoAdsWeb onder **rollen**, en klik vervolgens op **eigenschappen**.

    ![Roleigenschappen](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. In Hallo **ContosAdsWeb [rol]** eigenschappenvenster, klikt u op Hallo **instellingen** tabblad en klik vervolgens op **instelling toevoegen**.

    Laat **serviceconfiguratie** instellen te**alle configuraties**.
5. Voeg een instelling toe met de naam *StorageConnectionString*. Stel **Type** te*ConnectionString*, en stel **waarde** te*UseDevelopmentStorage = true*.

    ![Nieuwe verbindingsreeks](./media/cloud-services-dotnet-get-started/scall.png)
6. Sla uw wijzigingen op.
7. Volg Hallo dezelfde procedure tooadd een verbindingsreeks voor opslag in de eigenschappen van Hallo ContosoAdsWorker-rol.
8. Nog steeds in Hallo **ContosoAdsWorker [rol]** eigenschappenvenster van een andere verbindingsreeks toevoegen:

   * Name: ContosoAdsDbConnectionString
   * Type: String
   * Waarde: Plakken Hallo dezelfde verbindingsreeks die u voor het webrolproject Hallo gebruikt. (Hallo volgende voorbeeld is voor Visual Studio 2013. Vergeet niet toochange Hallo gegevensbron als u dit voorbeeld kopieert en u Visual Studio 2015 of hoger.)

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>Codebestanden toevoegen
In deze sectie kopieert u codebestanden vanuit Hallo gedownloade oplossing naar de nieuwe oplossing Hallo. Hallo volgende secties wordt weergeven en belangrijke onderdelen van deze code wordt uitgelegd.

tooadd bestanden tooa project of een map, klik met de rechtermuisknop Hallo project of map en klikt u op **toevoegen** - **bestaand Item**. Selecteer Hallo bestanden die u wilt en klik vervolgens op **toevoegen**. Als u wordt gevraagd of u wilt dat de bestaande bestanden tooreplace, klikt u op **Ja**.

1. Verwijder in project ContosoAdsCommon Hallo Hallo *Class1.cs* bestand en voeg in de plaats Hallo *Ad.cs* en *ContosoAdscontext.cs* bestanden van Hallo project gedownload.
2. In het project ContosoAdsWeb Hallo toevoegen Hallo volgende bestanden uit Hallo gedownload project.

   * *Global.asax.cs*.  
   * In Hallo *Views\Shared* map:  *\_Layout.cshtml*.
   * In Hallo *Views\Home* map: *Index.cshtml*.
   * In Hallo *domeincontrollers* map: *AdController.cs*.
   * In Hallo *Views\Ad* map (Maak eerst Hallo map): vijf *.cshtml* bestanden.
3. Voeg in het project ContosoAdsWorker hello *WorkerRole.cs* Hallo project gedownload.

U kunt nu toepassing bouwen en uitvoeren Hallo volgens de instructies eerder in de zelfstudie Hallo en Hallo app gebruikt lokale database- en opslagemulatorresources.

Hallo volgende secties wordt uitgelegd Hallo code gerelateerde tooworking met hello Azure-omgeving, blobs en wachtrijen. Deze zelfstudie wordt niet uitgelegd hoe toocreate MVC-controllers en weergaven met behulp van steigers, hoe toowrite code voor Entity Framework die werkt met SQL Server-databases of Hallo basisbeginselen van asynchrone programmering in ASP.NET 4.5. Zie voor informatie over deze onderwerpen Hallo resources te volgen:

* [Aan de slag met MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Aan de slag met EF 6 en MVC 5](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [Inleiding tooasynchronous programmering in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
bestand van Hallo Ad.cs definieert een enum voor advertentiecategorieën en een POCO-entiteitsklasse voor advertentie-informatie.

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Hallo klasse contosoadscontext geeft aan dat Hallo Ad-klasse wordt gebruikt in een DbSet-verzameling Entity Framework wordt opgeslagen in een SQL-database.

```csharp
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
```

Hallo-klasse heeft twee constructors. Hallo eerst hiervan wordt gebruikt door het webproject Hallo en geeft Hallo-naam van een verbindingsreeks die is opgeslagen in Hallo Web.config-bestand. Hallo tweede constructor kunt u toopass in Hallo werkelijke verbindingsreeks die wordt gebruikt door Hallo werkrolproject, omdat het geen een Web.config-bestand. U eerder hebt gezien waar deze verbindingsreeks is opgeslagen en ziet u hoe Hallo-code Hallo verbindingsreeks ophaalt bij het instantiëren van Hallo DbContext-klasse.

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Code die wordt aangeroepen vanuit Hallo `Application_Start` methode maakt u een *installatiekopieën* blob-container en een *installatiekopieën* als ze nog niet bestaan in de wachtrij. Dit zorgt ervoor dat wanneer u begint met behulp van een nieuw opslagaccount, of met behulp van de opslagemulator Hallo op een nieuwe computer, Hallo vereiste blobcontainer en wachtrij wordt automatisch gemaakt.

code haalt toegang toohello storage-account met behulp van de opslagverbindingsreeks uit Hallo HALLO hallo *.cscfg* bestand.

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

Vervolgens haalt de code een verwijzing toohello *installatiekopieën* blob-container, Hallo container maakt als deze niet al bestaat en stelt deze voor de nieuwe container Hallo toegangsrechten. Standaard staan nieuwe containers alleen clients met storage-account referenties tooaccess blobs. Hallo-website moet blobs toobe openbare Hallo zodat deze afbeeldingen met URL's die punt toohello afbeeldingsblobs wijzen kan weergeven.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

Vergelijkbare code wordt een verwijzing toohello *installatiekopieën* wachtrij en een nieuwe wachtrij gemaakt. In dit geval is er geen machtigingswijziging nodig.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - \_Layout.cshtml
Hallo *_Layout.cshtml* bestand Hallo app-naam stelt in Hallo koptekst en voettekst en maakt een menu-item 'Ads'.

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Hallo *Views\Home\Index.cshtml* bestand geeft categoriekoppelingen weer op Hallo-startpagina. Hallo-koppelingen geven de integerwaarde Hallo Hallo `Category` enum in een pagina querystring variabele toohello Ads Index.

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
In Hallo *AdController.cs* bestand, Hallo constructor aanroepen Hallo `InitializeStorage` methode toocreate Azure Storage-clientbibliotheek objecten die een API leveren voor het werken met blobs en wachtrijen.

Vervolgens Hallo code een verwijzing toohello wordt *installatiekopieën* blobcontainer, zoals u eerder in gezien *Global.asax.cs*. Tijdens het uitvoeren hiervan wordt standaard [beleid voor opnieuw proberen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) ingesteld dat geschikt is voor een web-app. Hallo standaard exponentieel uitstel-beleid voor opnieuw proberen kan vastlopen Hallo web-app langer dan een minuut herhaalde pogingen voor een tijdelijke fout. beleid voor opnieuw proberen Hallo hier opgegeven wacht drie seconden na elke poging up toothree pogingen.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

Vergelijkbare code wordt een verwijzing toohello *installatiekopieën* wachtrij.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

De meeste Hallo controllercode is Typerend voor het werken met een Entity Framework-gegevensmodel met behulp van een DbContext-klasse. Een uitzondering is Hallo HttpPost `Create` methode, waarmee een bestand wordt geüpload en opgeslagen in blob-opslag. Hallo modelbinder levert een [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello methode-object.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

Hallo gebruiker geselecteerd een bestand tooupload, Hallo code Hallo-bestand wordt geüpload, opgeslagen in een blob als Hallo Ad-databaserecord bijgewerkt met een URL die toohello blob verwijst.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

Hallo-code die uploaden Hallo heeft Hallo `UploadAndSaveBlobAsync` methode. Deze maakt een GUID-naam voor Hallo blob, uploads en slaat Hallo-bestand en retourneert een verwijzing toohello opgeslagen blob.

```csharp
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
```

Na het Hallo HttpPost `Create` methode een blob uploadt en updates Hallo database, het maken van een wachtrij bericht tooinform dat back-end-proces dat een afbeelding gereed voor conversie tooa miniatuur is.

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

code voor Hallo HttpPost Hallo `Edit` methode is vergelijkbaar met dit verschil dat als Hallo gebruiker een nieuw afbeeldingsbestand selecteert alle blobs die al bestaan moeten worden verwijderd.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

Hallo volgende voorbeeld ziet u Hallo-code die verwijderen van blobs wanneer u een advertentie verwijdert.

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml en Details.cshtml
Hallo *Index.cshtml* bestand bevat miniaturen Hello andere ad-gegevens.

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

Hallo *Details.cshtml* bestand Hallo-afbeelding wordt weergegeven.

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml en Edit.cshtml
Hallo *Create.cshtml* en *Edit.cshtml* bestanden formulier dat Hiermee controller tooget Hallo Hallo codering opgeven `HttpPostedFileBase` object.

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

Een `<input>` element vertelt Hallo browser tooprovide een dialoogvenster voor bestandsselectie.

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker - WorkerRole.cs - OnStart-methode
Hello Azure worker-rol omgeving roept Hallo `OnStart` methode in Hallo `WorkerRole` klasse wanneer Hallo werkrol begint en Hallo roept `Run` methode wanneer hello `OnStart` methode is voltooid.

Hallo `OnStart` methode haalt de databaseverbindingsreeks Hallo uit Hallo *.cscfg* bestands- en geeft deze door toohello Entity Framework DbContext-klasse. Hallo SQLClient-provider wordt standaard gebruikt, zodat het Hallo-provider heeft geen toobe opgegeven.

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

Hierna is Hallo-methode een verwijzing toohello storage-account opgehaald en Hallo blobcontainer en wachtrij wordt gemaakt als deze nog niet bestaan. Hallo code hiervoor is vergelijkbaar toowhat u al hebt gezien in de Webrol Hallo `Application_Start` methode.

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker - WorkerRole.cs - Run-methode
Hallo `Run` methode wordt aangeroepen wanneer hello `OnStart` methode een initialisatiewerk. Hallo-methode voert een oneindige lus die controleert op nieuwe Wachtrijberichten en verwerkt deze wanneer ze binnenkomen.

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

Na elke herhaling van de lus hello, als er geen wachtrijbericht is gevonden, Hallo inactieve modus ingeschakeld gedurende een seconde. Dit voorkomt dat Hallo werkrol buitensporig CPU tijd en opslag transactiekosten aangaan. Hallo Microsoft Customer Advisory Team kent het verhaal van een ontwikkelaar die tooinclude dit vergeten tooproduction geïmplementeerd en op vakantie ging. Wanneer hij zich ook, duurder zijn toezicht dan Hallo vakantie.

Soms veroorzaakt Hallo inhoud van een wachtrijbericht een fout bij de verwerking. Dit wordt genoemd, een *verontreinigd bericht*, en als u alleen een fout opgetreden in het logboek geregistreerd en Hallo lus opnieuw opgestart, kan dit leiden tot eindeloze probeert tooprocess bericht.  Daarom Hallo catch-blok een if bevat instructie waarmee wordt gecontroleerd toosee hoe vaak Hallo app heeft geprobeerd tooprocess Hallo huidige bericht, en als het al meer dan 5 maal, het Hallo-bericht is verwijderd uit Hallo wachtrij.

`ProcessQueueMessage` wordt aangeroepen wanneer er een wachtrijbericht is gevonden.

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

Deze code leest Hallo database tooget Hallo afbeeldings-URL, converteert de miniatuur tooa Hallo Hallo miniatuur opgeslagen in een blob, werkt Hallo-database met Hallo miniaturen blob-URL en Hallo-bericht van wachtrij worden verwijderd.

> [!NOTE]
> Hallo-code in Hallo `ConvertImageToThumbnailJPG` methode gebruik van klassen in Hallo System.Drawing-naamruimte voor de eenvoud. Hallo-klassen in deze naamruimte zijn echter bedoeld voor gebruik met Windows Forms. Ze worden niet ondersteund voor gebruik in een Windows- of ASP.NET-service. Zie [Afbeeldingen dynamisch genereren](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) en [Alles over het wijzigen van het formaat van afbeeldingen](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) voor meer informatie over opties voor de verwerking van afbeeldingen.
>
>

## <a name="troubleshooting"></a>Problemen oplossen
Als er iets niet werkt terwijl u Hallo-instructies in deze zelfstudie, Hier volgen een aantal veelvoorkomende fouten en hoe tooresolve ze.

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
Hallo `RoleEnvironment` object wordt verstrekt door Azure wanneer u een toepassing in Azure uitvoert of bij het uitvoeren van een lokaal via hello Azure-rekenemulator.  Als u deze fout krijgt wanneer u lokaal uitvoert, zorg ervoor dat u Hallo ContosoAdsCloudService-project als opstartproject Hallo hebt ingesteld. Hiermee stelt u Hallo project toorun met hello Azure-rekenemulator.

Hallo-bewerkingen Hallo toepassing gebruikt hello Azure RoleEnvironment voor tooget Hallo waarden van verbindingsreeksen die zijn opgeslagen in Hallo is *.cscfg* bestanden, zodat een andere oorzaak van deze uitzondering een ontbrekende verbindingsreeks is. Zorg ervoor dat u Hallo StorageConnectionString instelling voor zowel Cloud- en lokale configuraties in Hallo ContosoAdsWeb-project gemaakt en dat u beide verbindingsreeksen voor beide configuraties hebt gemaakt in de project ContosoAdsWorker Hallo. Als u een **Alles zoeken** zoeken voor StorageConnectionString in de hele oplossing hello, ziet u het 9 maal in 6 bestanden.

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>Kan de tooport xxx niet overschrijven. Nieuwe poort onder minimaal toegestane waarde 8080 voor http-protocol
Wijzig Hallo poortnummer dat wordt gebruikt door het webproject Hallo. Met de rechtermuisknop op Hallo ContosoAdsWeb-project en klik vervolgens op **eigenschappen**. Klik op Hallo **Web** tabblad en wijzig vervolgens de Hallo poortnummer in Hallo **Project Url** instelling.

Zie voor een alternatieve Hallo probleem kan mogelijk worden opgelost, Hallo volgende sectie.

### <a name="other-errors-when-running-locally"></a>Andere fouten bij lokale uitvoering
Cloudserviceprojecten gebruik door nieuwe cloud standaard hello Azure compute-emulator snelle toosimulate hello Azure-omgeving. Dit is een lichtgewicht versie van de volledige rekenemulator hello en onder bepaalde omstandigheden Hallo volledige emulator werkt wanneer Hallo express-versie niet.  

toochange Hallo project toouse Hallo volledige emulator, met de rechtermuisknop op Hallo ContosoAdsCloudService-project en klik op **eigenschappen**. In Hallo **eigenschappen** venster klikt u op Hallo **Web** tabblad en klik vervolgens op Hallo **Use Full Emulator** keuzerondje.

In de volgorde toorun Hallo toepassing met de volledige emulator hello hebt u tooopen Visual Studio met administratorbevoegdheden.

## <a name="next-steps"></a>Volgende stappen
Hallo Contoso Ads-toepassing is opzettelijk is eenvoudig gehouden voor een zelfstudie aan de slag. Bijvoorbeeld, implementeert niet [afhankelijkheidsinjectie](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) of Hallo [opslagplaatsen en werkeenheden](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), dat niet het geval [gebruik van een interface voor logboekregistratie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), nietwordtgebruikt[ EF Code First-migraties](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage gegevensmodel wijzigingen of [EF-Verbindingstolerantie](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage tijdelijke netwerkfouten, enzovoort.

Hier volgen enkele cloud service-voorbeeldtoepassingen waarin meer echte code te bevorderen, van cloudservicetoepassingen toomore complexe vermeld:

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31). Qua concept tooContoso advertenties maar implementeert meer functies en meer echte code te bevorderen.
* [Azure Cloud Service-toepassing met meerdere lagen die opslagtabellen, wachtrijen en blobs bevat](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36). Introduceert Azure Storage-tabellen, evenals blobs en wachtrijen. Op basis van een oudere versie van hello Azure SDK voor .NET, is enkele wijzigingen toowork met de huidige versie Hallo vereist.
* [Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Een uitgebreid voorbeeld met van een breed scala aan aanbevolen procedures, opgezet door Hallo Microsoft Patterns and Practice-groep.

Raadpleeg voor algemene informatie over het ontwikkelen voor Hallo cloud [gebouw echte Cloud-Apps met Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).

Aanbevolen procedures en patronen voor een video-inleiding tooAzure opslag, Zie [Microsoft Azure Storage-wat is er nieuw, aanbevolen procedures en patronen](http://channel9.msdn.com/Events/Build/2014/3-628).

Zie voor meer informatie Hallo resources te volgen:

* [Deel 1 Azure Cloud Services: Inleiding](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [Hoe toomanage Cloud-Services](cloud-services-how-to-manage.md)
* [Azure Storage](/documentation/services/storage/)
* [Hoe toochoose een cloud-serviceprovider](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
