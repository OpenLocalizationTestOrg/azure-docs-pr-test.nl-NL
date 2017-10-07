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
# <a name="get-started-with-power-bi-embedded-sample"></a>Aan de slag met Power BI Embedded voorbeeld

Met **Microsoft Power BI Embedded**, kunt u Power BI-rapporten integreren in uw web- of mobiele toepassingen. In dit artikel maakt u kennis toohello **Power BI Embedded** gestart get-voorbeeld.

Voordat we verdergaan, moet u waarschijnlijk toosave Hallo resources te volgen. Ze helpen u bij het Power BI-rapporten te integreren in Hallo voorbeeld-app en uw eigen apps.

* [Voorbeeld werkruimte web-app](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Power BI Embedded API-referentiemateriaal](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (beschikbaar via NuGet)
* [JavaScript-rapport insluiten voorbeeld](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> Voordat u configureren kunt en Voer Hallo Power BI Embedded ophalen voorbeeld gestart, moet u toocreate ten minste één **Werkruimteverzameling** in uw Azure-abonnement. toolearn hoe toocreate een **Werkruimteverzameling** in hello Azure-Portal bekijken [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="configure-hello-sample-app"></a>Hallo voorbeeld-app configureren

Laten we helpt u stapsgewijs door het instellen van uw Visual Studio development environment tooaccess Hallo onderdelen benodigde toorun Hallo voorbeeld-app.

1. Downloaden en uitpakken Hallo [Power BI Embedded - integreren van een rapport in een web-app](http://go.microsoft.com/fwlink/?LinkId=761493) op GitHub.
2. Open **PowerBI embedded.sln** in Visual Studio. Mogelijk moet u tooexecute hello **-updatepakket** opdracht in Hallo NuGET Package Manager Console in volgorde tooupdate Hallo pakketten gebruikt voor deze oplossing.
3. Hallo-oplossing bouwen.
4. Voer Hallo **ProvisionSample** console-app. In Hallo voorbeeld console-app inrichten van een werkruimte en een PBIX-bestand importeren.
5. tooprovision een nieuwe **werkruimte**, Selecteer optie 1, **verzameling management**, en selecteer vervolgens de optie 6, **inrichten van een nieuwe werkruimte**
6. tooimport een nieuwe **rapport**, Selecteer optie 2, **rapporteren management**, en selecteer vervolgens de optie 3, **importeren PBIX Desktop-bestand in een werkruimte**.

7. Voer uw **Werkruimteverzameling** naam, en **toegangssleutel**. U krijgt deze in Hallo **Azure Portal**. meer informatie over hoe toolearn tooget uw **toegangssleutel**, Zie [toegangstoetsen voor weergave Power BI API](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in aan de slag met Microsoft Power BI Embedded.

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. Kopieer en sla Hallo nieuw gemaakte **werkruimte-ID** toouse verderop in dit artikel. Na het Hallo **werkruimte-ID** is gemaakt, kunt u deze vinden Hallo **Azure Portal**.

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. tooimport een PBIX-bestand naar uw **werkruimte**, Selecteer optie **6. Bureaublad PBIX-bestand importeren in een bestaande werkruimte**. Als u een PBIX-bestand bij de hand hebt, kunt u downloaden Hallo [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).
10. Als u wordt gevraagd, voert u een beschrijvende naam voor uw **gegevensset**.

U ziet een antwoord zoals:

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> Als uw PBIX-bestand de directe query-verbindingen bevat, voert u de optie 7 tooupdate Hallo-verbindingsreeksen.

Op dit moment hebt u een Power BI PBIX-rapport geïmporteerd in uw **werkruimte**. Nu gaan we kijken hoe toorun hello **Power BI Embedded** ophalen gestart voorbeeld web-app.

## <a name="run-hello-sample-web-app"></a>Hallo voorbeeld-web-app uitvoeren
Hallo web app voorbeeld is een voorbeeldtoepassing die renders rapporten die worden geïmporteerd in uw **werkruimte**. Hier ziet u hoe tooconfigure Hallo voorbeeld van web-app.

1. In Hallo **Power BI embedded** Visual Studio-oplossing, rechts, klikt u op Hallo **EmbedSample** webtoepassing en kies **instellen als opstartproject**.
2. In **web.config**, in Hallo **EmbedSample** webtoepassing, Hallo bewerken **appSettings**: **AccessKey**,  **WorkspaceCollection** naam, en **WorkspaceId**.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Voer Hallo **EmbedSample** webtoepassing.

Zodra u Hallo uitvoert **EmbedSample** webtoepassing, Hallo linkernavigatievenster moet bevatten een **rapporten** menu. tooview hello rapport die u hebt geïmporteerd, vouw **rapporten**, en klikt u op een rapport. Als u Hallo geïmporteerd [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), Hallo voorbeeld-web-app eruit als volgt:

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

Nadat u een rapport op, Hallo **EmbedSample** webtoepassing ziet er ongeveer dit:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a>Hallo voorbeeldcode verkennen

Hallo **Microsoft Power BI Embedded** voorbeeld is een voorbeeld-web-app die laat u hoe zien toointegrate **Power BI** rapporten in uw app. Dit maakt gebruik van een Model-View-Controller (MVC) ontwerpen patroon toodemonstrate aanbevolen procedures. In deze sectie worden de onderdelen van Hallo voorbeeldcode die u binnen Hallo verkennen kunt **Power BI embedded** web-app-oplossing. Hallo Model-View-Controller (MVC) patroon scheidt Hallo modellering van Hallo domein, Hallo presentatie en Hallo acties op basis van gebruikersinvoer in drie afzonderlijke klassen: Model, weergeven en beheren. toolearn meer informatie over MVC, Zie [meer informatie over ASP.NET](http://www.asp.net/mvc).

Hallo **Microsoft Power BI Embedded** voorbeeldcode als volgt worden gescheiden. Elke sectie bevat Hallo-bestandsnaam in Hallo Power BI-embedded.sln oplossing, zodat u eenvoudig hello code in de steekproef Hallo vinden kunt.

> [!NOTE]
> Deze sectie wordt een samenvatting van Hallo voorbeeldcode die laat zien hoe Hallo code is geschreven. tooview hello voltooid steekproef, laad Hallo Power BI-embedded.sln oplossing in Visual Studio.

### <a name="model"></a>Model

Hallo voorbeeld heeft een **ReportsViewModel** en **ReportViewModel**.

**ReportsViewModel.cs**: Hiermee geeft u Power BI-rapporten.

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

**ReportViewModel.cs**: Hiermee geeft u een Power BI-rapport.

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a>Verbindingsreeks

Hallo-verbindingsreeks moet Hallo na indeling zijn:

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

Met behulp van algemene kenmerken voor server en de database mislukt. Bijvoorbeeld: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>Weergave

Hallo **weergave** beheert Hallo-weergave van Power BI **rapporten** en een Power BI **rapport**.

**Reports.cshtml**: doorlopen **Model.Reports** toocreate een **ActionLink**. Hallo **ActionLink** is samengesteld als volgt:

| Onderdeel | Beschrijving |
| --- | --- |
| Titel |Naam van Hallo rapport. |
| Queryreeks |Een koppeling toohello rapport-ID. |

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

Report.cshtml: Stel Hallo **Model.AccessToken**, en Hallo Lambda-expressie voor **PowerBIReportFor**.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Domeincontroller

**DashboardController.cs**: maakt een PowerBIClient geven een **app-token**. Een JSON Web Token (JWT) is gegenereerd op basis van Hallo **handtekeningsleutel** tooget hello **referenties**. Hallo **referenties** gebruikte toocreate zijn een exemplaar van **PowerBIClient**. Zodra u een exemplaar van hebt **PowerBIClient**, kunt u GetReports() en GetReportsAsync() aanroepen.

CreatePowerBIClient()

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

ActionResult Reports()

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


Taak<ActionResult> rapport (reportId tekenreeks)

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

### <a name="integrate-a-report-into-your-app"></a>Een rapport integreren in uw app

Zodra u hebt een **rapport**, u een **IFrame** tooembed Hallo Power BI **rapport**. Hier volgt een codefragment van powerbi.js in Hallo **Microsoft Power BI Embedded** voorbeeld.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>Filterrapporten die zijn ingesloten in uw toepassing

U kunt een ingesloten rapport filteren met behulp van een URL-syntaxis. toodo dit u toevoegen een **$filter** Querytekenreeksparameter met een **eq** operator tooyour iFrame src-url met Hallo filter dat is opgegeven. Hier volgt querysyntaxis Hallo-filter:

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName} mag geen spaties of speciale tekens bevatten. Hallo {fieldValue} accepteert één categorische waarde.  

## <a name="see-also"></a>Zie ook

[Algemene scenario's voor Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Een rapport insluiten](power-bi-embedded-embed-report.md)  
[Een nieuw rapport maken op basis van een gegevensset](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Voorbeeld van ingesloten JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Nog vragen? [Probeer Hallo Power BI-Community](http://community.powerbi.com/)
