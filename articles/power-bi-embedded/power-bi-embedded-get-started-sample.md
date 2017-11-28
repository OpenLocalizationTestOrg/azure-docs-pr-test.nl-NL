---
title: aaaGet gestart met een steekproef
description: Power BI Embedded, gebruikt u SDK tooadd interactieve Power BI-in uw business intelligence-toepassing rapporten
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="ea520-103">Aan de slag met Power BI Embedded voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ea520-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="ea520-104">Met **Microsoft Power BI Embedded**, kunt u Power BI-rapporten integreren in uw web- of mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ea520-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="ea520-105">In dit artikel maakt u kennis toohello **Power BI Embedded** gestart get-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ea520-105">In this article, we'll introduce you toohello **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="ea520-106">Voordat we verdergaan, moet u waarschijnlijk toosave Hallo resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="ea520-106">Before we go any further, you'll probably want toosave hello following resources.</span></span> <span data-ttu-id="ea520-107">Ze helpen u bij het Power BI-rapporten te integreren in Hallo voorbeeld-app en uw eigen apps.</span><span class="sxs-lookup"><span data-stu-id="ea520-107">They'll help you when integrating Power BI reports into hello sample app and your own apps too.</span></span>

* [<span data-ttu-id="ea520-108">Voorbeeld werkruimte web-app</span><span class="sxs-lookup"><span data-stu-id="ea520-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="ea520-109">Power BI Embedded API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="ea520-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="ea520-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (beschikbaar via NuGet)</span><span class="sxs-lookup"><span data-stu-id="ea520-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="ea520-111">JavaScript-rapport insluiten voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ea520-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="ea520-112">Voordat u configureren kunt en Voer Hallo Power BI Embedded ophalen voorbeeld gestart, moet u toocreate ten minste één **Werkruimteverzameling** in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ea520-112">Before you can configure and run hello Power BI Embedded get started sample, you need toocreate at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="ea520-113">toolearn hoe toocreate een **Werkruimteverzameling** in hello Azure-Portal bekijken [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ea520-113">toolearn how toocreate a **Workspace Collection** in hello Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-hello-sample-app"></a><span data-ttu-id="ea520-114">Hallo voorbeeld-app configureren</span><span class="sxs-lookup"><span data-stu-id="ea520-114">Configure hello sample app</span></span>

<span data-ttu-id="ea520-115">Laten we helpt u stapsgewijs door het instellen van uw Visual Studio development environment tooaccess Hallo onderdelen benodigde toorun Hallo voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="ea520-115">Let's walk through setting up your Visual Studio development environment tooaccess hello  components needed toorun hello sample app.</span></span>

1. <span data-ttu-id="ea520-116">Downloaden en uitpakken Hallo [Power BI Embedded - integreren van een rapport in een web-app](http://go.microsoft.com/fwlink/?LinkId=761493) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="ea520-116">Download and unzip hello [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="ea520-117">Open **PowerBI embedded.sln** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea520-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="ea520-118">Mogelijk moet u tooexecute hello **-updatepakket** opdracht in Hallo NuGET Package Manager Console in volgorde tooupdate Hallo pakketten gebruikt voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="ea520-118">You may need tooexecute hello **Update-Package** command in hello NuGET Package Manager Console in order tooupdate hello packages used in this solution.</span></span>
3. <span data-ttu-id="ea520-119">Hallo-oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="ea520-119">Build hello solution.</span></span>
4. <span data-ttu-id="ea520-120">Voer Hallo **ProvisionSample** console-app.</span><span class="sxs-lookup"><span data-stu-id="ea520-120">Run hello **ProvisionSample** console app.</span></span> <span data-ttu-id="ea520-121">In Hallo voorbeeld console-app inrichten van een werkruimte en een PBIX-bestand importeren.</span><span class="sxs-lookup"><span data-stu-id="ea520-121">In hello sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="ea520-122">tooprovision een nieuwe **werkruimte**, Selecteer optie 1, **verzameling management**, en selecteer vervolgens de optie 6, **inrichten van een nieuwe werkruimte**</span><span class="sxs-lookup"><span data-stu-id="ea520-122">tooprovision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="ea520-123">tooimport een nieuwe **rapport**, Selecteer optie 2, **rapporteren management**, en selecteer vervolgens de optie 3, **importeren PBIX Desktop-bestand in een werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="ea520-123">tooimport a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="ea520-124">Voer uw **Werkruimteverzameling** naam, en **toegangssleutel**.</span><span class="sxs-lookup"><span data-stu-id="ea520-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="ea520-125">U krijgt deze in Hallo **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="ea520-125">You can get these in hello **Azure Portal**.</span></span> <span data-ttu-id="ea520-126">meer informatie over hoe toolearn tooget uw **toegangssleutel**, Zie [toegangstoetsen voor weergave Power BI API](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in aan de slag met Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="ea520-126">toolearn more about how tooget your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="ea520-127">Kopieer en sla Hallo nieuw gemaakte **werkruimte-ID** toouse verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ea520-127">Copy and save hello newly created **Workspace ID** toouse later in this article.</span></span> <span data-ttu-id="ea520-128">Na het Hallo **werkruimte-ID** is gemaakt, kunt u deze vinden Hallo **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="ea520-128">After hello **Workspace ID** is created, you can find it hello **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="ea520-129">tooimport een PBIX-bestand naar uw **werkruimte**, Selecteer optie **6. Bureaublad PBIX-bestand importeren in een bestaande werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="ea520-129">tooimport a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="ea520-130">Als u een PBIX-bestand bij de hand hebt, kunt u downloaden Hallo [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="ea520-130">If you don't have a PBIX file handy, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="ea520-131">Als u wordt gevraagd, voert u een beschrijvende naam voor uw **gegevensset**.</span><span class="sxs-lookup"><span data-stu-id="ea520-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="ea520-132">U ziet een antwoord zoals:</span><span class="sxs-lookup"><span data-stu-id="ea520-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="ea520-133">Als uw PBIX-bestand de directe query-verbindingen bevat, voert u de optie 7 tooupdate Hallo-verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="ea520-133">If your PBIX file contains any direct query connections, run option 7 tooupdate hello connection strings.</span></span>

<span data-ttu-id="ea520-134">Op dit moment hebt u een Power BI PBIX-rapport geïmporteerd in uw **werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="ea520-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="ea520-135">Nu gaan we kijken hoe toorun hello **Power BI Embedded** ophalen gestart voorbeeld web-app.</span><span class="sxs-lookup"><span data-stu-id="ea520-135">Now, let's look at how toorun hello **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-hello-sample-web-app"></a><span data-ttu-id="ea520-136">Hallo voorbeeld-web-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ea520-136">Run hello sample web app</span></span>
<span data-ttu-id="ea520-137">Hallo web app voorbeeld is een voorbeeldtoepassing die renders rapporten die worden geïmporteerd in uw **werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="ea520-137">hello web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="ea520-138">Hier ziet u hoe tooconfigure Hallo voorbeeld van web-app.</span><span class="sxs-lookup"><span data-stu-id="ea520-138">Here's how tooconfigure hello web app sample.</span></span>

1. <span data-ttu-id="ea520-139">In Hallo **Power BI embedded** Visual Studio-oplossing, rechts, klikt u op Hallo **EmbedSample** webtoepassing en kies **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="ea520-139">In hello **PowerBI-embedded** Visual Studio solution, right click hello **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="ea520-140">In **web.config**, in Hallo **EmbedSample** webtoepassing, Hallo bewerken **appSettings**: **AccessKey**,  **WorkspaceCollection** naam, en **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="ea520-140">In **web.config**, in hello **EmbedSample** web application, edit hello **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="ea520-141">Voer Hallo **EmbedSample** webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="ea520-141">Run hello **EmbedSample** web application.</span></span>

<span data-ttu-id="ea520-142">Zodra u Hallo uitvoert **EmbedSample** webtoepassing, Hallo linkernavigatievenster moet bevatten een **rapporten** menu.</span><span class="sxs-lookup"><span data-stu-id="ea520-142">Once you run hello **EmbedSample** web application, hello left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="ea520-143">tooview hello rapport die u hebt geïmporteerd, vouw **rapporten**, en klikt u op een rapport.</span><span class="sxs-lookup"><span data-stu-id="ea520-143">tooview hello report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="ea520-144">Als u Hallo geïmporteerd [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), Hallo voorbeeld-web-app eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="ea520-144">If you imported hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="ea520-145">Nadat u een rapport op, Hallo **EmbedSample** webtoepassing ziet er ongeveer dit:</span><span class="sxs-lookup"><span data-stu-id="ea520-145">After you click a report, hello **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a><span data-ttu-id="ea520-146">Hallo voorbeeldcode verkennen</span><span class="sxs-lookup"><span data-stu-id="ea520-146">Explore hello sample code</span></span>

<span data-ttu-id="ea520-147">Hallo **Microsoft Power BI Embedded** voorbeeld is een voorbeeld-web-app die laat u hoe zien toointegrate **Power BI** rapporten in uw app.</span><span class="sxs-lookup"><span data-stu-id="ea520-147">hello **Microsoft Power BI Embedded** sample is an example web app that shows you how toointegrate **Power BI** reports into your app.</span></span> <span data-ttu-id="ea520-148">Dit maakt gebruik van een Model-View-Controller (MVC) ontwerpen patroon toodemonstrate aanbevolen procedures.</span><span class="sxs-lookup"><span data-stu-id="ea520-148">It uses a Model-View-Controller (MVC) design pattern toodemonstrate best practices.</span></span> <span data-ttu-id="ea520-149">In deze sectie worden de onderdelen van Hallo voorbeeldcode die u binnen Hallo verkennen kunt **Power BI embedded** web-app-oplossing.</span><span class="sxs-lookup"><span data-stu-id="ea520-149">This section highlights parts of hello sample code that you can explore within hello **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="ea520-150">Hallo Model-View-Controller (MVC) patroon scheidt Hallo modellering van Hallo domein, Hallo presentatie en Hallo acties op basis van gebruikersinvoer in drie afzonderlijke klassen: Model, weergeven en beheren.</span><span class="sxs-lookup"><span data-stu-id="ea520-150">hello Model-View-Controller (MVC) pattern separates hello modeling of hello domain, hello presentation, and hello actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="ea520-151">toolearn meer informatie over MVC, Zie [meer informatie over ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="ea520-151">toolearn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="ea520-152">Hallo **Microsoft Power BI Embedded** voorbeeldcode als volgt worden gescheiden.</span><span class="sxs-lookup"><span data-stu-id="ea520-152">hello **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="ea520-153">Elke sectie bevat Hallo-bestandsnaam in Hallo Power BI-embedded.sln oplossing, zodat u eenvoudig hello code in de steekproef Hallo vinden kunt.</span><span class="sxs-lookup"><span data-stu-id="ea520-153">Each section includes hello file name in hello PowerBI-embedded.sln solution so that you can easily find hello code in hello sample.</span></span>

> [!NOTE]
> <span data-ttu-id="ea520-154">Deze sectie wordt een samenvatting van Hallo voorbeeldcode die laat zien hoe Hallo code is geschreven.</span><span class="sxs-lookup"><span data-stu-id="ea520-154">This section is a summary of hello sample code that shows how hello code was written.</span></span> <span data-ttu-id="ea520-155">tooview hello voltooid steekproef, laad Hallo Power BI-embedded.sln oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea520-155">tooview hello complete sample, please load hello PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="ea520-156">Model</span><span class="sxs-lookup"><span data-stu-id="ea520-156">Model</span></span>

<span data-ttu-id="ea520-157">Hallo voorbeeld heeft een **ReportsViewModel** en **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="ea520-157">hello sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="ea520-158">**ReportsViewModel.cs**: Hiermee geeft u Power BI-rapporten.</span><span class="sxs-lookup"><span data-stu-id="ea520-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="ea520-159">**ReportViewModel.cs**: Hiermee geeft u een Power BI-rapport.</span><span class="sxs-lookup"><span data-stu-id="ea520-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="ea520-160">Verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="ea520-160">Connection string</span></span>

<span data-ttu-id="ea520-161">Hallo-verbindingsreeks moet Hallo na indeling zijn:</span><span class="sxs-lookup"><span data-stu-id="ea520-161">hello connection string must be in hello following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="ea520-162">Met behulp van algemene kenmerken voor server en de database mislukt.</span><span class="sxs-lookup"><span data-stu-id="ea520-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="ea520-163">Bijvoorbeeld: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="ea520-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="ea520-164">Weergave</span><span class="sxs-lookup"><span data-stu-id="ea520-164">View</span></span>

<span data-ttu-id="ea520-165">Hallo **weergave** beheert Hallo-weergave van Power BI **rapporten** en een Power BI **rapport**.</span><span class="sxs-lookup"><span data-stu-id="ea520-165">hello **View** manages hello display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="ea520-166">**Reports.cshtml**: doorlopen **Model.Reports** toocreate een **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="ea520-166">**Reports.cshtml**: Iterate over **Model.Reports** toocreate an **ActionLink**.</span></span> <span data-ttu-id="ea520-167">Hallo **ActionLink** is samengesteld als volgt:</span><span class="sxs-lookup"><span data-stu-id="ea520-167">hello **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="ea520-168">Onderdeel</span><span class="sxs-lookup"><span data-stu-id="ea520-168">Part</span></span> | <span data-ttu-id="ea520-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ea520-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea520-170">Titel</span><span class="sxs-lookup"><span data-stu-id="ea520-170">Title</span></span> |<span data-ttu-id="ea520-171">Naam van Hallo rapport.</span><span class="sxs-lookup"><span data-stu-id="ea520-171">Name of hello Report.</span></span> |
| <span data-ttu-id="ea520-172">Queryreeks</span><span class="sxs-lookup"><span data-stu-id="ea520-172">QueryString</span></span> |<span data-ttu-id="ea520-173">Een koppeling toohello rapport-ID.</span><span class="sxs-lookup"><span data-stu-id="ea520-173">A link toohello Report ID.</span></span> |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

<span data-ttu-id="ea520-174">Report.cshtml: Stel Hallo **Model.AccessToken**, en Hallo Lambda-expressie voor **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="ea520-174">Report.cshtml: Set hello **Model.AccessToken**, and hello Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="ea520-175">Domeincontroller</span><span class="sxs-lookup"><span data-stu-id="ea520-175">Controller</span></span>

<span data-ttu-id="ea520-176">**DashboardController.cs**: maakt een PowerBIClient geven een **app-token**.</span><span class="sxs-lookup"><span data-stu-id="ea520-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="ea520-177">Een JSON Web Token (JWT) is gegenereerd op basis van Hallo **handtekeningsleutel** tooget hello **referenties**.</span><span class="sxs-lookup"><span data-stu-id="ea520-177">A JSON Web Token (JWT) is generated from hello **Signing Key** tooget hello **Credentials**.</span></span> <span data-ttu-id="ea520-178">Hallo **referenties** gebruikte toocreate zijn een exemplaar van **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="ea520-178">hello **Credentials** are used toocreate an instance of **PowerBIClient**.</span></span> <span data-ttu-id="ea520-179">Zodra u een exemplaar van hebt **PowerBIClient**, kunt u GetReports() en GetReportsAsync() aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ea520-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="ea520-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="ea520-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="ea520-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="ea520-181">ActionResult Reports()</span></span>

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


<span data-ttu-id="ea520-182">Taak<ActionResult> rapport (reportId tekenreeks)</span><span class="sxs-lookup"><span data-stu-id="ea520-182">Task<ActionResult> Report(string reportId)</span></span>

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="ea520-183">Een rapport integreren in uw app</span><span class="sxs-lookup"><span data-stu-id="ea520-183">Integrate a report into your app</span></span>

<span data-ttu-id="ea520-184">Zodra u hebt een **rapport**, u een **IFrame** tooembed Hallo Power BI **rapport**.</span><span class="sxs-lookup"><span data-stu-id="ea520-184">Once you have a **Report**, you use an **IFrame** tooembed hello Power BI **Report**.</span></span> <span data-ttu-id="ea520-185">Hier volgt een codefragment van powerbi.js in Hallo **Microsoft Power BI Embedded** voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ea520-185">Here is a code snippet from  powerbi.js in hello **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="ea520-186">Filterrapporten die zijn ingesloten in uw toepassing</span><span class="sxs-lookup"><span data-stu-id="ea520-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="ea520-187">U kunt een ingesloten rapport filteren met behulp van een URL-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="ea520-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="ea520-188">toodo dit u toevoegen een **$filter** Querytekenreeksparameter met een **eq** operator tooyour iFrame src-url met Hallo filter dat is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ea520-188">toodo this, you add a **$filter** query string parameter with an **eq** operator tooyour iFrame src url with hello filter specified.</span></span> <span data-ttu-id="ea520-189">Hier volgt querysyntaxis Hallo-filter:</span><span class="sxs-lookup"><span data-stu-id="ea520-189">Here is hello filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="ea520-190">{tableName/fieldName} mag geen spaties of speciale tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="ea520-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="ea520-191">Hallo {fieldValue} accepteert één categorische waarde.</span><span class="sxs-lookup"><span data-stu-id="ea520-191">hello {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="ea520-192">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ea520-192">See also</span></span>

[<span data-ttu-id="ea520-193">Algemene scenario's voor Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="ea520-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="ea520-194">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="ea520-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="ea520-195">Een rapport insluiten</span><span class="sxs-lookup"><span data-stu-id="ea520-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="ea520-196">Een nieuw rapport maken op basis van een gegevensset</span><span class="sxs-lookup"><span data-stu-id="ea520-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="ea520-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="ea520-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="ea520-198">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="ea520-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="ea520-199">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="ea520-199">More questions?</span></span> [<span data-ttu-id="ea520-200">Probeer Hallo Power BI-Community</span><span class="sxs-lookup"><span data-stu-id="ea520-200">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
