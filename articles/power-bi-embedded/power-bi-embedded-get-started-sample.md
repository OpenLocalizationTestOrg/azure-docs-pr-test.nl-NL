---
title: Aan de slag met een voorbeeld
description: Power BI Embedded, SDK gebruiken om toe te voegen interactieve Power BI-rapporten in uw business intelligence-toepassing
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
ms.openlocfilehash: c3cb1763f807220a4a829f410d7eb77974b25776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="c8107-103">Aan de slag met Power BI Embedded voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c8107-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="c8107-104">Met **Microsoft Power BI Embedded**, kunt u Power BI-rapporten integreren in uw web- of mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c8107-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="c8107-105">In dit artikel maakt u kennis aan de **Power BI Embedded** gestart get-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c8107-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="c8107-106">Voordat we verdergaan, wilt u waarschijnlijk opslaan van de volgende resources.</span><span class="sxs-lookup"><span data-stu-id="c8107-106">Before we go any further, you'll probably want to save the following resources.</span></span> <span data-ttu-id="c8107-107">Ze helpen u bij het Power BI-rapporten te integreren in de voorbeeld-app en uw eigen apps.</span><span class="sxs-lookup"><span data-stu-id="c8107-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span></span>

* [<span data-ttu-id="c8107-108">Voorbeeld werkruimte web-app</span><span class="sxs-lookup"><span data-stu-id="c8107-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="c8107-109">Power BI Embedded API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="c8107-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="c8107-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (beschikbaar via NuGet)</span><span class="sxs-lookup"><span data-stu-id="c8107-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="c8107-111">JavaScript-rapport insluiten voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c8107-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="c8107-112">Voordat u configureren kunt en uitvoeren Power BI Embedded ophalen voorbeeld gestart, moet u ten minste één maken **Werkruimteverzameling** in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c8107-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="c8107-113">Voor meer informatie over het maken van een **Werkruimteverzameling** in de Azure Portal zien [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c8107-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-the-sample-app"></a><span data-ttu-id="c8107-114">De voorbeeld-app configureren</span><span class="sxs-lookup"><span data-stu-id="c8107-114">Configure the sample app</span></span>

<span data-ttu-id="c8107-115">Laten we helpt u stapsgewijs door het instellen van uw ontwikkelomgeving Visual Studio voor toegang tot de onderdelen die nodig zijn voor het uitvoeren van de voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="c8107-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span></span>

1. <span data-ttu-id="c8107-116">Downloaden en uitpakken van de [Power BI Embedded - integreren van een rapport in een web-app](http://go.microsoft.com/fwlink/?LinkId=761493) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="c8107-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="c8107-117">Open **PowerBI embedded.sln** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c8107-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="c8107-118">Mogelijk moet u uitvoeren de **-updatepakket** opdracht in de NuGET Package Manager-Console om bij te werken van de pakketten die in deze oplossing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c8107-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span></span>
3. <span data-ttu-id="c8107-119">De oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="c8107-119">Build the solution.</span></span>
4. <span data-ttu-id="c8107-120">Voer de **ProvisionSample** console-app.</span><span class="sxs-lookup"><span data-stu-id="c8107-120">Run the **ProvisionSample** console app.</span></span> <span data-ttu-id="c8107-121">In de voorbeeld-console-app inrichten van een werkruimte en een PBIX-bestand importeren.</span><span class="sxs-lookup"><span data-stu-id="c8107-121">In the sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="c8107-122">Voor het inrichten van een nieuwe **werkruimte**, Selecteer optie 1, **verzameling management**, en selecteer vervolgens de optie 6, **inrichten van een nieuwe werkruimte**</span><span class="sxs-lookup"><span data-stu-id="c8107-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="c8107-123">Voor het importeren van een nieuwe **rapport**, Selecteer optie 2, **rapporteren management**, en selecteer vervolgens de optie 3, **importeren PBIX Desktop-bestand in een werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="c8107-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="c8107-124">Voer uw **Werkruimteverzameling** naam, en **toegangssleutel**.</span><span class="sxs-lookup"><span data-stu-id="c8107-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="c8107-125">U kunt deze krijgen in de **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="c8107-125">You can get these in the **Azure Portal**.</span></span> <span data-ttu-id="c8107-126">Voor meer informatie over het ophalen van uw **toegangssleutel**, Zie [toegangstoetsen voor weergave Power BI API](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in aan de slag met Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="c8107-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="c8107-127">Kopieer en sla het zojuist gemaakte **werkruimte-ID** verderop in dit artikel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c8107-127">Copy and save the newly created **Workspace ID** to use later in this article.</span></span> <span data-ttu-id="c8107-128">Na de **werkruimte-ID** is gemaakt, kun je de **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="c8107-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="c8107-129">Voor het importeren van een PBIX-bestand in uw **werkruimte**, Selecteer optie **6. Bureaublad PBIX-bestand importeren in een bestaande werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="c8107-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="c8107-130">Als u een PBIX-bestand bij de hand hebt, kunt u downloaden de [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="c8107-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="c8107-131">Als u wordt gevraagd, voert u een beschrijvende naam voor uw **gegevensset**.</span><span class="sxs-lookup"><span data-stu-id="c8107-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="c8107-132">U ziet een antwoord zoals:</span><span class="sxs-lookup"><span data-stu-id="c8107-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="c8107-133">Als uw PBIX-bestand de directe query-verbindingen bevat, voert u de optie 7 voor het bijwerken van de verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="c8107-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span></span>

<span data-ttu-id="c8107-134">Op dit moment hebt u een Power BI PBIX-rapport geïmporteerd in uw **werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="c8107-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="c8107-135">Nu we kijken hoe u kunt uitvoeren naar de **Power BI Embedded** ophalen gestart voorbeeld web-app.</span><span class="sxs-lookup"><span data-stu-id="c8107-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-the-sample-web-app"></a><span data-ttu-id="c8107-136">De voorbeeld-web-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c8107-136">Run the sample web app</span></span>
<span data-ttu-id="c8107-137">De web-app-voorbeeld is een voorbeeldtoepassing die geïmporteerd worden in rapporten uw **werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="c8107-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="c8107-138">Hier volgt het configureren van de web-app-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c8107-138">Here's how to configure the web app sample.</span></span>

1. <span data-ttu-id="c8107-139">In de **Power BI embedded** Visual Studio-oplossing, klik met rechts op de **EmbedSample** webtoepassing en kies **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="c8107-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="c8107-140">In **web.config**, in de **EmbedSample** webtoepassing maakt, bewerk de **appSettings**: **AccessKey**, **WorkspaceCollection** naam, en **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="c8107-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="c8107-141">Voer de **EmbedSample** webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="c8107-141">Run the **EmbedSample** web application.</span></span>

<span data-ttu-id="c8107-142">Zodra u uitvoert het **EmbedSample** webtoepassing, het linkernavigatievenster moet bevatten een **rapporten** menu.</span><span class="sxs-lookup"><span data-stu-id="c8107-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="c8107-143">Als u wilt weergeven in het rapport dat u hebt geïmporteerd, vouw **rapporten**, en klikt u op een rapport.</span><span class="sxs-lookup"><span data-stu-id="c8107-143">To view the report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="c8107-144">Als u hebt geïmporteerd de [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), de voorbeeld-web-app eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="c8107-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="c8107-145">Nadat u een rapport op de **EmbedSample** webtoepassing ziet er ongeveer dit:</span><span class="sxs-lookup"><span data-stu-id="c8107-145">After you click a report, the **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a><span data-ttu-id="c8107-146">De voorbeeldcode verkennen</span><span class="sxs-lookup"><span data-stu-id="c8107-146">Explore the sample code</span></span>

<span data-ttu-id="c8107-147">De **Microsoft Power BI Embedded** voorbeeld is een voorbeeld-web-app waarin het integreren van **Power BI** rapporten in uw app.</span><span class="sxs-lookup"><span data-stu-id="c8107-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span></span> <span data-ttu-id="c8107-148">Het ontwerppatroon voor een Model-View-Controller (MVC) wordt gebruikt voor het demonstreren van aanbevolen procedures.</span><span class="sxs-lookup"><span data-stu-id="c8107-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span></span> <span data-ttu-id="c8107-149">In deze sectie worden de onderdelen van de voorbeeldcode die u kunt verkennen binnen de **Power BI embedded** web-app-oplossing.</span><span class="sxs-lookup"><span data-stu-id="c8107-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="c8107-150">Het patroon Model-View-Controller (MVC) worden gescheiden van de modellering van het domein, de presentatie en de acties op basis van gebruikersinvoer in drie afzonderlijke klassen: Model, weergeven en beheren.</span><span class="sxs-lookup"><span data-stu-id="c8107-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="c8107-151">Zie voor meer informatie over MVC, [meer informatie over ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="c8107-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="c8107-152">De **Microsoft Power BI Embedded** voorbeeldcode als volgt worden gescheiden.</span><span class="sxs-lookup"><span data-stu-id="c8107-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="c8107-153">Elke sectie bevat de bestandsnaam in de Power BI-embedded.sln oplossing zodat u de code eenvoudig in de steekproef vinden kunt.</span><span class="sxs-lookup"><span data-stu-id="c8107-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span></span>

> [!NOTE]
> <span data-ttu-id="c8107-154">Deze sectie wordt een samenvatting van de voorbeeldcode die laat zien hoe de code is geschreven.</span><span class="sxs-lookup"><span data-stu-id="c8107-154">This section is a summary of the sample code that shows how the code was written.</span></span> <span data-ttu-id="c8107-155">Laad de Power BI-embedded.sln oplossing in Visual Studio om weer te geven het complete voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c8107-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="c8107-156">Model</span><span class="sxs-lookup"><span data-stu-id="c8107-156">Model</span></span>

<span data-ttu-id="c8107-157">Het voorbeeld is een **ReportsViewModel** en **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="c8107-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="c8107-158">**ReportsViewModel.cs**: Hiermee geeft u Power BI-rapporten.</span><span class="sxs-lookup"><span data-stu-id="c8107-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="c8107-159">**ReportViewModel.cs**: Hiermee geeft u een Power BI-rapport.</span><span class="sxs-lookup"><span data-stu-id="c8107-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="c8107-160">Verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="c8107-160">Connection string</span></span>

<span data-ttu-id="c8107-161">De verbindingsreeks moet in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="c8107-161">The connection string must be in the following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="c8107-162">Met behulp van algemene kenmerken voor server en de database mislukt.</span><span class="sxs-lookup"><span data-stu-id="c8107-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="c8107-163">Bijvoorbeeld: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="c8107-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="c8107-164">Weergave</span><span class="sxs-lookup"><span data-stu-id="c8107-164">View</span></span>

<span data-ttu-id="c8107-165">De **weergave** beheert de weergave van Power BI **rapporten** en een Power BI **rapport**.</span><span class="sxs-lookup"><span data-stu-id="c8107-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="c8107-166">**Reports.cshtml**: doorlopen **Model.Reports** maken een **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="c8107-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span></span> <span data-ttu-id="c8107-167">De **ActionLink** is samengesteld als volgt:</span><span class="sxs-lookup"><span data-stu-id="c8107-167">The **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="c8107-168">Onderdeel</span><span class="sxs-lookup"><span data-stu-id="c8107-168">Part</span></span> | <span data-ttu-id="c8107-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c8107-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8107-170">Titel</span><span class="sxs-lookup"><span data-stu-id="c8107-170">Title</span></span> |<span data-ttu-id="c8107-171">Naam van het rapport.</span><span class="sxs-lookup"><span data-stu-id="c8107-171">Name of the Report.</span></span> |
| <span data-ttu-id="c8107-172">Queryreeks</span><span class="sxs-lookup"><span data-stu-id="c8107-172">QueryString</span></span> |<span data-ttu-id="c8107-173">Een koppeling naar de rapport-ID.</span><span class="sxs-lookup"><span data-stu-id="c8107-173">A link to the Report ID.</span></span> |

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

<span data-ttu-id="c8107-174">Report.cshtml: Stel de **Model.AccessToken**, en de Lambda-expressie voor **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="c8107-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="c8107-175">Domeincontroller</span><span class="sxs-lookup"><span data-stu-id="c8107-175">Controller</span></span>

<span data-ttu-id="c8107-176">**DashboardController.cs**: maakt een PowerBIClient geven een **app-token**.</span><span class="sxs-lookup"><span data-stu-id="c8107-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="c8107-177">Een JSON Web Token (JWT) is gegenereerd op basis van de **handtekeningsleutel** ophalen van de **referenties**.</span><span class="sxs-lookup"><span data-stu-id="c8107-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span></span> <span data-ttu-id="c8107-178">De **referenties** gebruikt bij het maken van een exemplaar van **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="c8107-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span></span> <span data-ttu-id="c8107-179">Zodra u een exemplaar van hebt **PowerBIClient**, kunt u GetReports() en GetReportsAsync() aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c8107-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="c8107-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="c8107-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="c8107-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="c8107-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="c8107-182">Taak<ActionResult> rapport (reportId tekenreeks)</span><span class="sxs-lookup"><span data-stu-id="c8107-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="c8107-183">Een rapport integreren in uw app</span><span class="sxs-lookup"><span data-stu-id="c8107-183">Integrate a report into your app</span></span>

<span data-ttu-id="c8107-184">Zodra u hebt een **rapport**, u een **IFrame** voor het insluiten van de Power BI **rapport**.</span><span class="sxs-lookup"><span data-stu-id="c8107-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span></span> <span data-ttu-id="c8107-185">Hier volgt een codefragment van powerbi.js in de **Microsoft Power BI Embedded** voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c8107-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="c8107-186">Filterrapporten die zijn ingesloten in uw toepassing</span><span class="sxs-lookup"><span data-stu-id="c8107-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="c8107-187">U kunt een ingesloten rapport filteren met behulp van een URL-syntaxis.</span><span class="sxs-lookup"><span data-stu-id="c8107-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="c8107-188">U doet dit door u toevoegen een **$filter** Querytekenreeksparameter met een **eq** operator aan uw iFrame src-url met het opgegeven filter.</span><span class="sxs-lookup"><span data-stu-id="c8107-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span></span> <span data-ttu-id="c8107-189">Hier volgt de syntaxis van de filter-query:</span><span class="sxs-lookup"><span data-stu-id="c8107-189">Here is the filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="c8107-190">{tableName/fieldName} mag geen spaties of speciale tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="c8107-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="c8107-191">De {fieldValue} accepteert één categorische waarde.</span><span class="sxs-lookup"><span data-stu-id="c8107-191">The {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="c8107-192">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c8107-192">See also</span></span>

[<span data-ttu-id="c8107-193">Algemene scenario's voor Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c8107-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="c8107-194">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c8107-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="c8107-195">Een rapport insluiten</span><span class="sxs-lookup"><span data-stu-id="c8107-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="c8107-196">Een nieuw rapport maken op basis van een gegevensset</span><span class="sxs-lookup"><span data-stu-id="c8107-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="c8107-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c8107-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="c8107-198">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="c8107-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="c8107-199">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="c8107-199">More questions?</span></span> [<span data-ttu-id="c8107-200">Probeer de Power BI-community</span><span class="sxs-lookup"><span data-stu-id="c8107-200">Try the Power BI Community</span></span>](http://community.powerbi.com/)
