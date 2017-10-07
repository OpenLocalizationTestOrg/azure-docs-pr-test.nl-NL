---
title: aaaHow tooMigrate en publiceren van een webtoepassing tooan Azure Cloud Service vanuit Visual Studio | Microsoft Docs
description: Meer informatie over hoe toomigrate en publiceren van uw web application tooan Azure-cloudservice met behulp van Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>Procedure: migreren en publiceren van een webtoepassing tooan Azure Cloud Service vanuit Visual Studio
tootake profiteren van Hallo hosting-services en schaalbaarheid van Azure, u mogelijk wilt toomigrate en publiceren van uw toepassing tooan Azure-cloud-webservice. U kunt een webtoepassing in Azure uitvoeren met minimale wijzigingen tooyour bestaande toepassing.

> [!NOTE]
> Dit onderwerp gaat over het implementeren van services toocloud, niet tooweb sites. Zie voor meer informatie over het implementeren van tooweb sites [een web-app in Azure App Service implementeren](app-service-web/web-sites-deploy.md).
>
>

Zie voor een lijst van specifieke sjablonen die worden ondersteund voor zowel Visual C# en Visual Basic, Hallo sectie **projectsjablonen ondersteund** verderop in dit onderwerp.

U moet eerst uw webtoepassing voor Azure vanuit Visual Studio inschakelen. Hallo volgende afbeelding toont Hallo hoofdstappen toopublish uw webtoepassing door een Azure-project toouse voor implementatie toe te voegen. Dit proces wordt een Azure-project met Hallo vereist web rol tooyour oplossing toegevoegd. Op basis van Hallo type webproject die u hebt, Hallo Projecteigenschappen voor assembly's zijn ook bijgewerkt als het servicepakket Hallo extra assembly's voor implementatie vereist.

![Een Web application tooMicrosoft Azure publiceren](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> Hallo **converteren**, **tooAzure Cloudserviceproject converteren** opdracht wordt alleen weergegeven voor Hallo-webproject in uw oplossing. Hallo-opdracht is bijvoorbeeld niet beschikbaar is voor een Silverlight-project in uw oplossing.
> Wanneer u een servicepakket maakt of uw toepassing tooAzure publiceert, optreden waarschuwingen of fouten. Deze waarschuwingen en fouten kunt u bij het oplossen van problemen voordat u tooAzure implementeert. Bijvoorbeeld, verschijnt er een waarschuwing over een ontbrekende assembly. Voor meer informatie over hoe tootreat eventuele waarschuwingen als fouten zien [configureren van een Azure-Cloudserviceproject met Visual Studio](vs-azure-tools-configuring-an-azure-project.md). Als u uw toepassing bouwen, deze lokaal met behulp van de rekenemulator Hallo uitvoeren of tooAzure publiceren, ziet u mogelijk Hallo volgende fout in Hallo **foutenlijst** venster: **Hallo opgegeven pad, bestandsnaam, of beide zijn te lang** . Deze fout treedt op omdat Hallo van hello Azure-project volledig gekwalificeerde naam te lang is. Hallo-lengte van de projectnaam hello, inclusief het volledige pad hello, mag niet meer dan 146 tekens. Dit is bijvoorbeeld Hallo volledige projectnaam inclusief bestandspad voor een Azure-project dat wordt gemaakt voor een Silverlight-toepassing: `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`. Mogelijk hebt u toomove uw oplossing tooa andere map met een korter pad tooreduce Hallo lengte van Hallo volledig gekwalificeerde naam.
>
>

toomigrate en publiceren van een web application tooAzure vanuit Visual Studio, als volgt te werk.

## <a name="enable-a-web-application-for-deployment-tooazure"></a>Een webtoepassing voor implementatie tooAzure inschakelen
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>een webtoepassing voor implementatie tooAzure tooenable
1. tooenable uw webtoepassing voor implementatie tooAzure, open Hallo snelmenu voor een web-project in uw oplossing en kies Azure implementatieproject toevoegen.

    Hallo volgende acties uitgevoerd:

   * Een Azure-project aangeroepen `<name of hello web project>.Azure` toohello oplossing voor uw toepassing wordt toegevoegd.
   * Een Webrol voor Hallo-webproject toegevoegd toothis Azure-project.
   * Hallo **lokale kopie** eigenschap tootrue is ingesteld voor assembly's die vereist voor de MVC-2, 3 MVC, MVC 4 en Silverlight Business-toepassingen zijn. Hiermee voegt u deze assembly's toohello servicepakket dat wordt gebruikt voor implementatie.

   > [!IMPORTANT]
   > Als u andere assembly's of bestanden die vereist voor deze webtoepassing zijn hebt, moet u de eigenschappen voor deze bestanden Hallo handmatig instellen. Voor informatie over hoe tooset deze eigenschappen, Zie sectie Hallo **bestanden opnemen in Hallo servicepakket** verderop in dit artikel.
   >
   > [!NOTE]
   > Als een Webrol voor een specifieke webproject al in een Azure-project in Hallo oplossing bestaat **converteren**, **tooAzure Cloudserviceproject converteren** wordt niet weergegeven in het snelmenu Hallo voor dit webproject .
   >
   >

   Als u meerdere webprojecten in uw webtoepassing hebt en u voor elk webproject toocreate webrollen wilt instellen, moet u Hallo stappen uitvoeren in deze procedure voor elke webproject. Hiermee maakt u afzonderlijke Azure projecten voor elke Webrol. Elke webproject kan afzonderlijk worden gepubliceerd. U kunt ook handmatig een andere rol tooan bestaande Azure webproject in uw webtoepassing toevoegen. toodo dit, open Hallo snelmenu voor Hallo **rollen** map in uw Azure-project, kies **toevoegen**, klikt u vervolgens **Webrolproject in oplossing**, Hallo project tooadd als een web te kiezen rol, en kies vervolgens Hallo **OK** knop.

## <a name="use-an-azure-sql-database-for-your-application"></a>Een Azure SQL-Database voor uw toepassing gebruiken
Als u een verbindingsreeks voor uw webtoepassing die gebruikmaakt van een SQL Server-database die on-premises Hallo hebt, moet u deze verbinding tekenreeks toouse een exemplaar van SQL-Database die Azure als host fungeert in plaats daarvan.

> [!IMPORTANT]
> Uw abonnement moet inschakelen toouse SQL-Database. Als u uw abonnement toegang Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), kunt u bepalen welke services voorziet in uw abonnement. Hallo volgende instructies gelden toohello uitgebracht [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885). Als u van Hallo gebruikmaakt [Azure-portal](http://portal.microsoft.com), de volgende procedure toohello overslaan.
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse een exemplaar van SQL-Database in uw Webrol voor de verbindingsreeks
1. een exemplaar van SQL-Database in Hallo toocreate [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), Hallo stappen in het volgende artikel Hallo: [maken van een SQL-databaseserver](http://go.microsoft.com/fwlink/?LinkId=225109).

   > [!NOTE]
   > Bij het instellen van Hallo firewallregels voor uw exemplaar van SQL-Database, moet u Hallo **andere tooaccess Azure-services op deze server toestaan** selectievakje.
   >
   >
2. toocreate een instantie van SQL-Database toouse voor de verbindingsreeks Hallo stappen in de volgende sectie in het volgende artikel Hallo Hallo: [maken van een SQL-Database](http://go.microsoft.com/fwlink/?LinkId=225110).
3. toocopy hello ADO.NET connection string toouse voor de verbindingsreeks uitvoeren Hallo stappen te volgen in Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).  

   1. Kies Hallo **Database** knop en open vervolgens Hallo knooppunt voor het Hallo-abonnement dat u toocreate uw exemplaar van SQL-Database gebruikt.
   2. toodisplay hello beschikbare exemplaren van SQL-Database, kiest u Hallo **SQL-Databases** knooppunt.
   3. toodisplay hello eigenschappen voor Hallo-database, kies Hallo-database. Hallo **eigenschappen** weergegeven.

      > [!NOTE]
      > Als hello **eigenschappen** weergave niet wordt weergegeven, moet u mogelijk het met behulp van de scheidingsmarkering Hallo tooopen.
      >
      >
   4. Hallo verbindingsreeksen toodisplay kiezen Hallo weglatingsteken (...) knop volgende tooView.

      Hallo **verbindingsreeksen** dialoogvenster wordt weergegeven.
   5. toocopy hello ADO.NET-verbindingsreeks, selecteert u de tekst hello en kies Hallo Ctrl + C sleutels.
   6. tooclose hello dialoogvenster Kies Hallo **sluiten** knop.
4. tooreplace hello verbinding een tekenreeks Hallo web.config-bestand toouse dit exemplaar van SQL-Database, Hallo web.config-bestand te openen, markeer Hallo bestaande verbinding tekenreeks vermelding en kies vervolgens Hallo Ctrl + V sleutels. Hallo ADO.NET-verbindingsreeks voor Hallo exemplaar van SQL-Database vervangt de bestaande verbindingsreeks Hallo.
5. U moet ook Hallo parameter toevoegen `MultipleActiveResultSets=True` toohello-verbindingsreeks. Hallo-verbindingsreeks moet Hallo volgende indeling hebben:

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. (Optioneel) Een alternatieve methode toochanging Hallo-verbindingsreeks is rechtstreeks in het web.config-bestand Hallo tooadd een sectie in één Hallo web.config-transformatie-bestanden, afhankelijk van Hallo buildconfiguratie dat u toocreate het servicepakket. Hallo Web.Debug.Config bestand of Hallo Web.Release.Config bestand openen. Hallo volgende sectie in dit bestand toevoegen:

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. Hallo-bestand dat u gewijzigd opslaan en opnieuw publiceren van uw toepassing.

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>een exemplaar van SQL Database met behulp van toouse Hallo klassieke Azure-portal
1. In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), kies Hallo SQL-Databases knooppunt.

   * Als het Hallo-exemplaar van SQL-Database die u wilt dat toouse wordt weergegeven, kiest u tooopen deze.
   * Als u geen instanties dat nog niet hebt gemaakt, kies de juiste koppeling Hallo en maak vervolgens een exemplaar.
2. Nadat u openen of maken van een database-exemplaar, kiest u Hallo **verbindingsreeksen** koppeling.
3. Hallo onderaan pagina Hallo in Hallo koppeling tooconfigure firewall-instellingen, kies en accepteer de standaardwaarden Hallo of Hallo-waarden die u moet configureren.
4. Hallo ADO.NET-verbindingsreeks kopiëren, plak deze in het web.config-bestand via Hallo oude verbindingsreeks voor Hallo lokale-database en worden ervoor tooadd `MultipleActiveResultSets=True`.

## <a name="publish-a-web-application-tooazure"></a>Een webtoepassing tooAzure publiceren
### <a name="toopublish-a-web-application-tooazure"></a>een Web application tooAzure toopublish
1. tootest Hallo-toepassing in lokale ontwikkelingsomgeving Hallo hello Azure-rekenemulator met open Hallo snelmenu voor hello Azure-project voor de Webrol Hallo en kies **instellen als opstartproject**. Kies vervolgens **Debug**, **foutopsporing starten** (toetsenbord: **F5**).

    Hallo **Start hello Azure-omgeving voor foutopsporing** in het dialoogvenster wordt geopend en het Hallo-toepassing wordt gestart in de browser Hallo. Voor specifieke informatie over hoe toostart elk type van de webtoepassing in Hallo rekenemulator, Zie de tabel Hallo in deze sectie.
2. tooset Hallo-services voor uw toepassing toopublish tooAzure installeren, moet u een Microsoft-account en een Azure-abonnement hebben. Gebruik Hallo stappen voor het volgende onderwerp tooset van uw services Hallo: [toopublish voorbereiden of implementeren van een Azure-toepassing vanuit Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
3. toopublish hello web application tooAzure Hallo snelmenu voor Hallo webproject openen en kies **tooAzure publiceren**.

    Hallo **Publish Azure Application** dialoogvenster wordt geopend en Visual Studio begint met het Hallo-implementatieproces. Zie voor meer informatie over hoe toopublish toepassing hello Hallo sectie **publiceren van een Azure-toepassing vanuit Visual Studio** in [publiceren van een Cloudservice met behulp van hulpprogramma's van Azure Hallo](vs-azure-tools-publishing-a-cloud-service.md).

   > [!NOTE]
   > U kunt ook Hallo-toepassing hello Azure-project publiceren. toodo, open Hallo snelmenu voor hello Azure-project en kies **publiceren**.
   >
   >
4. voortgang van de toosee Hallo van Hallo-implementatie, kunt u bekijken Hallo **Azure Activity Log** venster. Dit logboek wordt automatisch weergegeven wanneer het Hallo-implementatieproces begint. U kunt uitbreiden Hallo regelitem in Hallo activiteitenlogboek tooshow gedetailleerde informatie, zoals wordt weergegeven in de volgende illustratie Hallo:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. (Optioneel) toocancel Hallo implementatieproces open Hallo snelmenu voor het regelitem Hallo in Hallo activiteitenlogboek en kies **annuleren en verwijder**. Dit Hallo implementatieproces stopt en verwijdert deze Hallo implementatieomgeving van Azure.

   > [!NOTE]
   > tooremove deze implementatieomgeving nadat deze is geïmplementeerd, moet u Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).
   >
   >
6. (Optioneel) Nadat uw rolinstanties hebt gestart, Visual Studio Hallo implementatieomgeving automatisch weergegeven in Hallo **Azure Compute** knooppunt in **Cloud Explorer** of **Server Explorer**. U kunt hier Hallo status van de afzonderlijke rolinstanties Hallo bekijken.

    Hallo volgende afbeelding ziet u de rolinstanties Hallo in **Server Explorer** als ze nog steeds in Hallo status Bezig met initialiseren:

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. tooaccess uw toepassing na de implementatie kiezen Hallo pijl volgende tooyour implementatie wanneer de status van **voltooid** wordt weergegeven in Hallo **Azure Activity log**. Hiermee geeft Hallo-URL voor uw webtoepassing in Azure. Zie de volgende tabel voor informatie over hoe toostart een specifieke type van de webtoepassing van Azure Hallo Hallo.

    Hallo volgende tabel geeft een lijst van Hallo meer informatie over hoe toostart specifieke webtoepassingen van Azure of toorun of fouten opsporen in een webtoepassing lokaal via hello Azure Compute-Emulator:

   | Webtoepassingstype | Hallo uitvoeren/Debug lokaal via Compute-Emulator | in Azure wordt uitgevoerd |
   | --- | --- | --- |
   | ASP.NET-webtoepassing |Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |Kies Hallo URL hyperlink weergegeven in Hallo **implementatie** tabblad voor Hallo **Azure Activity log** tooload Hallo-startpagina in Hallo browser. |
   | ASP.NET MVC 2-webtoepassing |Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |Kies Hallo URL hyperlink weergegeven in Hallo **implementatie** tabblad voor Hallo **Azure Activity log** tooload Hallo-startpagina in Hallo browser. |
   | ASP.NET MVC 3-webtoepassing |Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |Kies Hallo URL hyperlink weergegeven in Hallo **implementatie** tabblad voor Hallo **Azure Activity log** tooload Hallo-startpagina in Hallo browser. |
   | ASP.NET MVC 4-webtoepassing |Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |Kies Hallo URL hyperlink weergegeven in Hallo **implementatie** tabblad voor Hallo **Azure Activity log** tooload Hallo-startpagina in Hallo browser. |
   | Lege ASP.NET-webtoepassing |U moet een ASPX-pagina in uw toepassing die u voor uw webproject als startpagina Hallo instellen toevoegen. Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |Als u een standaard .aspx-pagina in uw toepassing hebt, kies Hallo URL hyperlink weergegeven in Hallo **implementatie** tabblad voor Hallo **Azure Activity log** en deze pagina wordt geladen in de browser Hallo. Als u een andere ASPX-pagina hebt, moet u toonavigate toothis specifieke pagina met de Hallo indeling voor de url te volgen:`<url for deployment>/<name of page>.aspx` |
   | Silverlight-toepassing |Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |Toonavigate toohello bepaalde pagina moet u voor uw toepassing met behulp van Hallo indeling voor de url van de volgende:`<url for deployment>/<name of page>.aspx` |
   | Silverlight-Business-toepassing |Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |Toonavigate toohello bepaalde pagina moet u voor uw toepassing met behulp van Hallo indeling voor de url van de volgende:`<url for deployment>/<name of page>.aspx` |
   | Silverlight-toepassing voor navigatie |Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |Toonavigate toohello bepaalde pagina moet u voor uw toepassing met behulp van Hallo indeling voor de url van de volgende:`<url for deployment>/<name of page>.aspx` |
   | WCF-Service-toepassing |Hallo .svc-bestand moet u instellen als Hallo startpagina voor uw project WCF-Service. Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |Toonavigate toohello svc-bestand moet u voor uw toepassing met behulp van Hallo indeling voor de url van de volgende:`<url for deployment>/<name of service file>.svc` |
   | WCF-werkstroom-servicetoepassing |Hallo .svc-bestand moet u instellen als Hallo startpagina voor uw project WCF-Service. Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |Toonavigate toohello svc-bestand moet u voor uw toepassing met behulp van Hallo indeling voor de url van de volgende:`<url for deployment>/<name of service file>.svc` |
   | ASP.NET dynamische entiteiten |Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |U moet de verbindingsreeks Hallo bijwerken (Zie volgende sectie). Toonavigate toohello bepaalde pagina moet u ook voor uw toepassing met behulp van Hallo indeling voor de url van de volgende:`<url for deployment>/<name of page>.aspx` |
   | ASP.NET dynamische gegevens Linq tooSQL |Kies op de menubalk Hallo **Debug**, **foutopsporing starten** (toetsenbord: Kies Hallo **F5** sleutel.). |U moet Hallo stappen in deze procedure: een Azure SQL-database gebruiken voor uw toepassing (Zie eerdere sectie in dit onderwerp). Toonavigate toohello bepaalde pagina moet u ook voor uw toepassing met behulp van Hallo indeling voor de url van de volgende:`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>Bijwerken van een verbindingsreeks voor ASP.NET dynamische entiteiten
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>tooUpdate een verbindingsreeks voor ASP.NET dynamische entiteiten
1. een Azure SQL-database die kan worden gebruikt voor een webtoepassing ASP.NET dynamische entiteiten toocreate Hallo stappen in Hallo procedure **een Azure SQL-database gebruiken voor uw toepassing** eerder in dit onderwerp.
2. Hallo-tabellen en velden die u nodig hebt voor deze database uit Hallo toevoegen [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).
3. Hallo-verbindingsreeks voor dit type toepassing heeft de volgende indeling in het web.config-bestand Hallo Hallo:  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    Update Hallo *connectionString* waarde met de Hallo ADO.NET-verbindingsreeks voor uw Azure SQL database als volgt:

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. toosave hello web.config-bestand met de Hallo-wijzigingen die u hebt aangebracht toohello verbindingsreeks, op de menubalk Hallo kiezen **bestand**, **opslaan web.config**.

## <a name="supported-project-templates"></a>Ondersteunde projectsjablonen
een web application tooAzure toopublish, Hallo toepassing moet gebruiken een van de projectsjablonen Hallo voor C# of Visual Basic die wordt weergegeven in onderstaande tabel voor Hallo.

| Groep Project-sjabloon | Project-sjabloon |
| --- | --- |
| Web |ASP.NET-webtoepassing |
| Web |ASP.NET MVC 2-webtoepassing |
| Web |ASP.NET MVC 3-webtoepassing |
| Web |MVC4 voor ASP.NET-webtoepassing |
| Web |Lege ASP.NET-webtoepassing |
| Web |Lege ASP.NET MVC 2-webtoepassing |
| Web |De webtoepassing van ASP.NET dynamische gegevensentiteiten |
| Web |ASP.NET dynamische gegevens Linq tooSQL webtoepassing |
| Silverlight |Silverlight-toepassing |
| Silverlight |Silverlight-Business-toepassing |
| Silverlight |Silverlight-toepassing voor navigatie |
| WCF |WCF-Service-toepassing |
| WCF |WCF-werkstroom-servicetoepassing |
| Werkstroom |WCF-werkstroom-servicetoepassing |

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over publiceren [tooPublish voorbereiden of implementeren van een Azure-toepassing vanuit Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md). Lees ook [instelling Up met de naam verificatiereferenties](vs-azure-tools-setting-up-named-authentication-credentials.md).
