---
title: een ASP.NET-app in Azure met SQL-Database aaaBuild | Microsoft Docs
description: Meer informatie over hoe een ASP.NET-tooget app in Azure, werken met verbinding tooa SQL-Database.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>Een ASP.NET-app in Azure met SQL-Database maken

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie. Deze zelfstudie leert u hoe toodeploy een gegevensgestuurde ASP.NET web-app in Azure en te verbinden[Azure SQL Database](../sql-database/sql-database-technical-overview.md). Wanneer u klaar bent, hebt u een ASP.NET-app uitgevoerd in de [Azure App Service](../app-service/app-service-value-prop-what-is.md) en tooSQL Database verbonden.

![Gepubliceerde ASP.NET-toepassing in Azure-web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maken van een SQL-Database in Azure
> * Verbinding maken met een ASP.NET-app tooSQL Database
> * Hallo app tooAzure implementeren
> * Hallo-gegevensmodel bijwerken en Hallo app implementeren
> * Logboeken van de stroom van Azure tooyour terminal
> * Hallo-app in hello Azure-portal beheren

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

* Installeer [Visual Studio 2017](https://www.visualstudio.com/downloads/) Hello werkbelastingen te volgen:
  - **ASP.NET- en web-ontwikkeling**
  - **Azure-ontwikkeling**

  ![ASP.NET- en web-ontwikkeling en Azure-ontwikkeling (onder Web en cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Hallo voorbeeld downloaden

[Hallo-voorbeeldproject downloaden](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).

Pak (uitpakken) Hallo *dotnet-sqldb-zelfstudie-master.zip* bestand.

Hallo-voorbeeldproject bevat een eenvoudige [ASP.NET MVC](https://www.asp.net/mvc) CRUD (maken-lezen-update-verwijderen) met behulp van app [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="run-hello-app"></a>Hallo-app uitvoeren

Open Hallo *dotnet-sqldb-zelfstudie-master/DotNetAppSqlDb.sln* bestand in Visual Studio. 

Type `Ctrl+F5` toorun Hallo app zonder foutopsporing. Hallo-app wordt weergegeven in de browser. Selecteer Hallo **nieuw** koppelen en maken van een paar *taak* items. 

![Het dialoogvenster Nieuw ASP.NET-project](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

Test Hallo **bewerken**, **Details**, en **verwijderen** koppelingen.

Hallo app gebruikmaakt van een database context tooconnect met Hallo-database. In dit voorbeeld wordt de databasecontext Hallo maakt gebruik van een verbindingsreeks met de naam `MyDbConnection`. Hallo-verbindingsreeks is ingesteld in Hallo *Web.config* bestands- en waarnaar wordt verwezen in Hallo *Models/MyDatabaseContext.cs* bestand. naam van verbindingsreeks Hello wordt later in Hallo zelfstudie tooconnect hello Azure-web-app tooan Azure SQL Database gebruikt. 

## <a name="publish-tooazure-with-sql-database"></a>TooAzure met SQL Database publiceren

In Hallo **Solution Explorer**, met de rechtermuisknop op uw **DotNetAppSqlDb** project en selecteer **publiceren**.

![Publiceren vanuit Solution Explorer](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

Zorg ervoor dat **Microsoft Azure App Service** is geselecteerd en klik op **Publiceren**.

![Publiceren vanaf de projectoverzichtspagina](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

Publicatie wordt geopend Hallo **Create App Service** dialoogvenster waarmee u alle hello Azure-resources u toorun moet uw ASP.NET-web-app in Azure.

### <a name="sign-in-tooazure"></a>Meld u aan tooAzure

In Hallo **Create App Service** dialoogvenster, klikt u op **account toevoegen**, en vervolgens weer aanmelden tooyour Azure-abonnement. Als u al bent aangemeld bij een Microsoft-account, moet u ervoor zorgen dat dit account uw Azure-abonnement bevat. Als Hallo ondertekend in Microsoft-account niet uw Azure-abonnement hebt, klikt u erop tooadd Hallo juiste account.
   
![Meld u aan tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

Nadat u bent aangemeld, bent u klaar toocreate die alle bronnen die u nodig hebt voor uw Azure-web-app in dit dialoogvenster Hallo.

### <a name="configure-hello-web-app-name"></a>Hallo web-appnaam configureren

Hallo gegenereerd web-appnaam behouden of deze tooanother unieke naam wijzigen (geldige tekens zijn `a-z`, `0-9`, en `-`). Hallo web-appnaam wordt gebruikt als onderdeel van Hallo standaard-URL voor uw app (`<app_name>.azurewebsites.net`, waarbij `<app_name>` is de naam van uw web-app). Hallo web-appnaam moet toobe uniek zijn in alle apps in Azure. 

![Het dialoogvenster app service maken](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>Een resourcegroep maken

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Volgende te**resourcegroep**, klikt u op **nieuw**.

![Volgende tooResource groep, klikt u op Nieuw.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

Naam Hallo resourcegroep **myResourceGroup**.

> [!NOTE]
> Klik niet op **maken**. U moet eerst tooset van een SQL-Database in een later stadium.

### <a name="create-an-app-service-plan"></a>Een App Service-plan maken

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Volgende te**App Service-Plan**, klikt u op **nieuw**. 

In Hallo **App Service-Plan configureren** dialoogvenster Hallo nieuwe App Service-abonnement met Hallo volgende instellingen configureren:

![Een App Service-plan maken](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| Instelling  | Voorgestelde waarde | Voor meer informatie |
| ----------------- | ------------ | ----|
|**App Service-abonnement**| myAppServicePlan | [App Service-abonnementen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**Locatie**| West-Europa | [Azure-regio's](https://azure.microsoft.com/regions/) |
|**Grootte**| Gratis | [Prijscategorieën](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>Maak een SQL Server-exemplaar

Voordat u een database maakt, moet u een [logische Azure SQL Database-server](../sql-database/sql-database-features.md). Een logische server bevat een groep met databases die worden beheerd als groep.

Selecteer **verkennen extra Azure-services**.

![Naam van web-app configureren](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

In Hallo **Services** en klik op Hallo  **+**  pictogram volgende te**SQL-Database**. 

![Hallo-Services op het tabblad pictogram + Hallo volgende tooSQL Database.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

In Hallo **SQL-Database configureren** dialoogvenster, klikt u op **nieuw** volgende te**SQL Server**. 

Er wordt een unieke naam gegenereerd. Deze naam wordt gebruikt als onderdeel van Hallo standaard-URL voor de logische server `<server_name>.database.windows.net`. Het moet uniek zijn in alle exemplaren van logische server in Azure. U kunt Hallo servernaam wijzigen, maar voor deze zelfstudie Hallo gegenereerde waarde behouden.

Toevoegen van een gebruikersnaam voor de beheerder en het wachtwoord en selecteer vervolgens **OK**. Zie voor de vereisten voor wachtwoordcomplexiteit, [wachtwoordbeleid](/sql/relational-databases/security/password-policy).

Deze gebruikersnaam en wachtwoord onthouden. U moet ze toomanage Hallo logische server later-instantie.

![SQL Server-exemplaar maken](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>Een SQL-database maken

In Hallo **SQL-Database configureren** dialoogvenster: 

* Hallo standaard gegenereerde houden **databasenaam**.
* In **Verbindingsreeksnaam**, type *MyDbConnection*. Deze naam moet overeenkomen met de verbindingsreeks Hallo waarnaar wordt verwezen in *Models/MyDatabaseContext.cs*.
* Selecteer **OK**.

![SQL-Database configureren](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

Hallo **Create App Service** dialoogvenster Hallo resources weergegeven die u hebt gemaakt. Klik op **Create**. 

![Hallo-resources die u hebt gemaakt](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

Zodra het Hallo-wizard is voltooid hello Azure-resources maken, wordt uw ASP.NET-app tooAzure gepubliceerd. De standaardbrowser wordt gestart met Hallo URL toohello geïmplementeerd app. 

Enkele taakitems toevoegen.

![Gepubliceerde ASP.NET-toepassing in Azure-web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Gefeliciteerd. Uw ASP.NET-toepassing voor gegevensgestuurde wordt live in Azure App Service uitgevoerd.

## <a name="access-hello-sql-database-locally"></a>Toegang tot lokaal Hallo SQL-Database

Visual Studio kunt u bekijken en beheren van uw nieuwe SQL-Database eenvoudig in Hallo **SQL Server Object Explorer**.

### <a name="create-a-database-connection"></a>Een databaseverbinding maken

Van Hallo **weergave** selecteert u **SQL Server Object Explorer**.

Hallo boven aan het **SQL Server Object Explorer**, klikt u op Hallo **SQL-Server toevoegen** knop.

### <a name="configure-hello-database-connection"></a>Hallo-databaseverbinding configureren

In Hallo **Connect** dialoogvenster Vouw Hallo **Azure** knooppunt. Uw SQL-Database-exemplaren in Azure worden hier weergegeven.

Selecteer Hallo `DotNetAppSqlDb` SQL-Database. Hallo-verbinding die u eerder hebt gemaakt, wordt automatisch gevuld Hallo onderaan.

Typ Hallo database administrator-wachtwoord die u eerder hebt gemaakt en klik op **Connect**.

![Databaseverbinding vanuit Visual Studio configureren](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>Clientverbinding van uw computer toestaan

Hallo **maken van een nieuwe firewallregel** dialoogvenster wordt geopend. Uw exemplaar van SQL-Database kunt standaard alleen verbindingen van Azure-services, zoals uw Azure-web-app. tooconnect tooyour database, maakt u een firewallregel in Hallo SQL Database-exemplaar. Hallo firewallregel kunt Hallo openbaar IP-adres van uw lokale computer.

dialoogvenster Hallo is al ingevuld met het openbare IP-adres van uw computer.

Zorg ervoor dat **mijn client-IP toevoegen** is geselecteerd en klik op **OK**. 

![Firewall voor SQL Database-instantie instellen](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

Zodra de Visual Studio is voltooid Hallo firewall-instellingen voor uw exemplaar van SQL-Database maken, de verbinding wordt weergegeven in **SQL Server Object Explorer**.

Hier kunt u uitvoeren Hallo meest voorkomende databasebewerkingen, zoals het uitvoeren van query's maken, weergaven en opgeslagen procedures en meer. 

Met de rechtermuisknop op Hallo `Todoes` tabel en selecteer **weergavegegevens**. 

![Objecten van de SQL-Database verkennen](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>App kunt bijwerken met Code First-migraties

U kunt Hallo vertrouwde hulpprogramma's in Visual Studio tooupdate uw database en web-app in Azure gebruiken. In deze stap maakt u gebruik Code First-migraties in Entity Framework toomake een wijziging tooyour-databaseschema en tooAzure publiceren.

Zie voor meer informatie over het gebruik van Entity Framework Code First-migraties [aan de slag met Entity Framework 6 Code First met MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="update-your-data-model"></a>Uw gegevensmodel bijwerken

Open _Models\Todo.cs_ in Hallo code-editor. Hallo eigenschap toohello na toevoegen `ToDo` klasse:

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Code First-migraties lokaal uitvoeren

Voer enkele opdrachten toomake updates tooyour lokale database. 

Van Hallo **extra** menu, klikt u op **NuGet Package Manager** > **Package Manager Console**.

Schakel in het venster Package Manager Console Hallo, Code First-migraties:

```PowerShell
Enable-Migrations
```

Toevoegen van een migratie:

```PowerShell
Add-Migration AddProperty
```

Hallo lokale database bijwerken:

```PowerShell
Update-Database
```

Type `Ctrl+F5` toorun Hallo app. Test Hallo details, bewerken en maken van koppelingen.

Als de toepassing hello wordt geladen zonder fouten, is de Code First-migraties van voltooid zijn. Uw pagina nog steeds uitstraling kunt u echter Hallo op dezelfde omdat uw toepassingslogica wordt deze nieuwe eigenschap niet nog gebruikt. 

### <a name="use-hello-new-property"></a>De nieuwe eigenschap hello te gebruiken

Enkele wijzigingen aanbrengen in uw code toouse hello `Done` eigenschap. Voor het gemak in deze zelfstudie gaat u alleen toochange hello `Index` en `Create` toosee Hallo eigenschap weergaven in te grijpen.

Open _Controllers\TodosController.cs_.

Hallo zoeken `Create()` methode en voeg `Done` toohello lijst met eigenschappen in Hallo `Bind` kenmerk. Wanneer u bent klaar, uw `Create()` methodehandtekening ziet eruit als Hallo code te volgen:

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

Open _Views\Todos\Create.cshtml_.

In Hallo Razor code, ziet u een `<div class="form-group">` element die gebruikmaakt van `model.Description`, en vervolgens een andere `<div class="form-group">` element die gebruikmaakt van `model.CreatedDate`. Direct na deze twee elementen toevoegen `<div class="form-group">` element die gebruikmaakt van `model.Done`:

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

Open _Views\Todos\Index.cshtml_.

Zoeken naar Hallo leeg `<th></th>` element. Net boven dit element toevoegen Hallo Razor code te volgen:

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Hallo zoeken `<td>` element met Hallo `Html.ActionLink()` Help-methoden. Net boven dit element toevoegen Hallo Razor code te volgen:

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

Dit is alles wat u toosee Hallo wijzigingen in Hallo moet `Index` en `Create` weergaven. 

Type `Ctrl+F5` toorun Hallo app.

U kunt nu een taakitem toegevoegd en controleer of **gedaan**. Vervolgens moet het weergegeven in uw startpagina als een item voltooid. Houd er rekening mee dat Hallo `Edit` weergave niet Hallo `Done` veld, omdat u niet Hallo wijzigen `Edit` weergeven.

### <a name="enable-code-first-migrations-in-azure"></a>Code First-migraties in Azure inschakelen

Nu dat uw code wijzigen werkt, met inbegrip van de database wilt migreren, kunt u deze tooyour Azure-web-app publiceren en uw SQL-Database te werken met Code First-migraties.

Net zoals, met de rechtermuisknop op uw project en selecteer **publiceren**.

Klik op **instellingen** tooopen Hallo wizard publiceren.

![Open publicatie-instellingen](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

Klik in de wizard Hallo op **volgende**.

Zorg ervoor dat deze Hallo-verbindingsreeks voor de SQL-Database wordt ingevuld **MyDatabaseContext (MyDbConnection)**. Mogelijk moet u tooselect hello **myToDoAppDb** database uit de vervolgkeuzelijst Hallo. 

Selecteer **uitvoeren Code First-migraties (wordt uitgevoerd op de start van toepassing)**, klikt u vervolgens op **opslaan**.

![Code First-migraties inschakelen in Azure-web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>Uw wijzigingen publiceren

Nu dat u Code First-migraties in uw Azure-web-app hebt ingeschakeld, moet u uw codewijzigingen publiceren.

In Hallo pagina publiceren, klikt u op **publiceren**.

Selecteer en probeer het opnieuw toe te voegen taakitems **gedaan**, en ze moeten worden weergegeven in uw startpagina als een item voltooid.

![Azure-web-app na de eerste Code-migratie](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

Uw bestaande taakitems nog steeds worden weergegeven. Wanneer u uw ASP.NET-toepassing opnieuw publiceren, is er geen bestaande gegevens in de SQL-Database verloren. Bovendien Code First-migraties Hallo gegevensschema alleen verandert en uw bestaande gegevens intact blijft.


## <a name="stream-application-logs"></a>Toepassingslogboeken Stream

U kunt tracering berichten rechtstreeks vanuit uw Azure-web-app tooVisual Studio streamen.

Open _Controllers\TodosController.cs_.

Elke actie begint met een `Trace.WriteLine()` methode. Deze code wordt toegevoegd tooshow u hoe tooadd trace berichten tooyour Azure-web-app.

### <a name="open-server-explorer"></a>Open Server Explorer

Van Hallo **weergave** selecteert u **Server Explorer**. U kunt logboekregistratie configureren voor uw Azure-web-app in **Server Explorer**. 

### <a name="enable-log-streaming"></a>Streaming-logboek inschakelen

In **Server Explorer**, vouw **Azure** > **App Service**.

Vouw Hallo **myResourceGroup** resourcegroep, u hebt gemaakt tijdens het maken van hello Azure-web-app.

Met de rechtermuisknop op uw Azure-web-app en selecteer **Streaming logboeken bekijken**.

![Streaming-logboek inschakelen](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

Hallo logboeken worden nu gestreamd naar Hallo **uitvoer** venster. 

![In het uitvoervenster streaming logboek](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

Echter, u niet ziet van Hallo traceringsberichten nog. Dat omdat wanneer u eerst selecteert **Streaming logboeken bekijken**, uw Azure-web-app stelt het traceringsniveau hello te`Error`, die alleen legt foutgebeurtenissen vast in (Hello `Trace.TraceError()` methode).

### <a name="change-trace-levels"></a>De traceringsniveaus wijzigen

toochange hello trace niveaus toooutput andere traceringsberichten, gaat u terug te**Server Explorer**.

Opnieuw met de rechtermuisknop op uw Azure-web-app en selecteer **instellingen**.

In Hallo **toepassingslogboeken (bestandssysteem)** vervolgkeuzelijst **uitgebreid**. Klik op **Opslaan**.

![Niveau tooVerbose tracering wijzigen](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> U kunt experimenteren met verschillende trace niveaus toosee welke soorten berichten worden weergegeven voor elk bedreigingsniveau. Bijvoorbeeld, Hallo **informatie** niveau omvat alle logboeken die zijn gemaakt door `Trace.TraceInformation()`, `Trace.TraceWarning()`, en `Trace.TraceError()`, maar niet de logboeken die zijn gemaakt door `Trace.WriteLine()`.
>
>

In de browser probeert te klikken op rond Hallo taak lijst toepassing in Azure. Hallo traceringsberichten worden nu gestreamd toohello **uitvoer** venster in Visual Studio.

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>Logboek streaming stoppen

toostop Hallo logboek streaming-service, klikt u op Hallo **bewaking stopt** knop in Hallo **uitvoer** venster.

![Logboek streaming stoppen](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>Uw Azure-web-app beheren

Ga toohello [Azure-portal](https://portal.azure.com) toosee Hallo web-app die u hebt gemaakt. 



In het linkermenu hello, klikt u op **App Service**, klikt u op Hallo-naam van uw Azure-web-app.

![Navigatie in de portal tooAzure web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

U bevindt zich in uw web-app-pagina. 

Standaard Hallo portal weergegeven Hallo **overzicht** pagina. Deze pagina geeft u een overzicht van hoe uw app presteert. Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen. Hallo tabbladen aan de linkerkant Hallo van Hallo pagina bevatten Hallo verschillende configuratiepagina's die u kunt openen. 

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Maken van een SQL-Database in Azure
> * Verbinding maken met een ASP.NET-app tooSQL Database
> * Hallo app tooAzure implementeren
> * Hallo-gegevensmodel bijwerken en Hallo app implementeren
> * Logboeken van de stroom van Azure tooyour terminal
> * Hallo-app in hello Azure-portal beheren

De volgende zelfstudie toolearn toohello gaan hoe toomap een aangepaste DNS-Server name toohello web-app.

> [!div class="nextstepaction"]
> [Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps](app-service-web-tutorial-custom-domain.md)
