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
# <a name="get-started-with-power-bi-embedded-sample"></a>Aan de slag met Power BI Embedded voorbeeld

Met **Microsoft Power BI Embedded**, kunt u Power BI-rapporten integreren in uw web- of mobiele toepassingen. In dit artikel maakt u kennis aan de **Power BI Embedded** gestart get-voorbeeld.

Voordat we verdergaan, wilt u waarschijnlijk opslaan van de volgende resources. Ze helpen u bij het Power BI-rapporten te integreren in de voorbeeld-app en uw eigen apps.

* [Voorbeeld werkruimte web-app](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Power BI Embedded API-referentiemateriaal](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (beschikbaar via NuGet)
* [JavaScript-rapport insluiten voorbeeld](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> Voordat u configureren kunt en uitvoeren Power BI Embedded ophalen voorbeeld gestart, moet u ten minste één maken **Werkruimteverzameling** in uw Azure-abonnement. Voor meer informatie over het maken van een **Werkruimteverzameling** in de Azure Portal zien [aan de slag met Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="configure-the-sample-app"></a>De voorbeeld-app configureren

Laten we helpt u stapsgewijs door het instellen van uw ontwikkelomgeving Visual Studio voor toegang tot de onderdelen die nodig zijn voor het uitvoeren van de voorbeeld-app.

1. Downloaden en uitpakken van de [Power BI Embedded - integreren van een rapport in een web-app](http://go.microsoft.com/fwlink/?LinkId=761493) op GitHub.
2. Open **PowerBI embedded.sln** in Visual Studio. Mogelijk moet u uitvoeren de **-updatepakket** opdracht in de NuGET Package Manager-Console om bij te werken van de pakketten die in deze oplossing gebruikt.
3. De oplossing bouwen.
4. Voer de **ProvisionSample** console-app. In de voorbeeld-console-app inrichten van een werkruimte en een PBIX-bestand importeren.
5. Voor het inrichten van een nieuwe **werkruimte**, Selecteer optie 1, **verzameling management**, en selecteer vervolgens de optie 6, **inrichten van een nieuwe werkruimte**
6. Voor het importeren van een nieuwe **rapport**, Selecteer optie 2, **rapporteren management**, en selecteer vervolgens de optie 3, **importeren PBIX Desktop-bestand in een werkruimte**.

7. Voer uw **Werkruimteverzameling** naam, en **toegangssleutel**. U kunt deze krijgen in de **Azure Portal**. Voor meer informatie over het ophalen van uw **toegangssleutel**, Zie [toegangstoetsen voor weergave Power BI API](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in aan de slag met Microsoft Power BI Embedded.

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. Kopieer en sla het zojuist gemaakte **werkruimte-ID** verderop in dit artikel gebruiken. Na de **werkruimte-ID** is gemaakt, kun je de **Azure Portal**.

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. Voor het importeren van een PBIX-bestand in uw **werkruimte**, Selecteer optie **6. Bureaublad PBIX-bestand importeren in een bestaande werkruimte**. Als u een PBIX-bestand bij de hand hebt, kunt u downloaden de [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).
10. Als u wordt gevraagd, voert u een beschrijvende naam voor uw **gegevensset**.

U ziet een antwoord zoals:

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> Als uw PBIX-bestand de directe query-verbindingen bevat, voert u de optie 7 voor het bijwerken van de verbindingsreeksen.

Op dit moment hebt u een Power BI PBIX-rapport geïmporteerd in uw **werkruimte**. Nu we kijken hoe u kunt uitvoeren naar de **Power BI Embedded** ophalen gestart voorbeeld web-app.

## <a name="run-the-sample-web-app"></a>De voorbeeld-web-app uitvoeren
De web-app-voorbeeld is een voorbeeldtoepassing die geïmporteerd worden in rapporten uw **werkruimte**. Hier volgt het configureren van de web-app-voorbeeld.

1. In de **Power BI embedded** Visual Studio-oplossing, klik met rechts op de **EmbedSample** webtoepassing en kies **instellen als opstartproject**.
2. In **web.config**, in de **EmbedSample** webtoepassing maakt, bewerk de **appSettings**: **AccessKey**, **WorkspaceCollection** naam, en **WorkspaceId**.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Voer de **EmbedSample** webtoepassing.

Zodra u uitvoert het **EmbedSample** webtoepassing, het linkernavigatievenster moet bevatten een **rapporten** menu. Als u wilt weergeven in het rapport dat u hebt geïmporteerd, vouw **rapporten**, en klikt u op een rapport. Als u hebt geïmporteerd de [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), de voorbeeld-web-app eruit als volgt:

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

Nadat u een rapport op de **EmbedSample** webtoepassing ziet er ongeveer dit:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a>De voorbeeldcode verkennen

De **Microsoft Power BI Embedded** voorbeeld is een voorbeeld-web-app waarin het integreren van **Power BI** rapporten in uw app. Het ontwerppatroon voor een Model-View-Controller (MVC) wordt gebruikt voor het demonstreren van aanbevolen procedures. In deze sectie worden de onderdelen van de voorbeeldcode die u kunt verkennen binnen de **Power BI embedded** web-app-oplossing. Het patroon Model-View-Controller (MVC) worden gescheiden van de modellering van het domein, de presentatie en de acties op basis van gebruikersinvoer in drie afzonderlijke klassen: Model, weergeven en beheren. Zie voor meer informatie over MVC, [meer informatie over ASP.NET](http://www.asp.net/mvc).

De **Microsoft Power BI Embedded** voorbeeldcode als volgt worden gescheiden. Elke sectie bevat de bestandsnaam in de Power BI-embedded.sln oplossing zodat u de code eenvoudig in de steekproef vinden kunt.

> [!NOTE]
> Deze sectie wordt een samenvatting van de voorbeeldcode die laat zien hoe de code is geschreven. Laad de Power BI-embedded.sln oplossing in Visual Studio om weer te geven het complete voorbeeld.

### <a name="model"></a>Model

Het voorbeeld is een **ReportsViewModel** en **ReportViewModel**.

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

De verbindingsreeks moet in de volgende indeling:

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

Met behulp van algemene kenmerken voor server en de database mislukt. Bijvoorbeeld: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>Weergave

De **weergave** beheert de weergave van Power BI **rapporten** en een Power BI **rapport**.

**Reports.cshtml**: doorlopen **Model.Reports** maken een **ActionLink**. De **ActionLink** is samengesteld als volgt:

| Onderdeel | Beschrijving |
| --- | --- |
| Titel |Naam van het rapport. |
| Queryreeks |Een koppeling naar de rapport-ID. |

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

Report.cshtml: Stel de **Model.AccessToken**, en de Lambda-expressie voor **PowerBIReportFor**.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Domeincontroller

**DashboardController.cs**: maakt een PowerBIClient geven een **app-token**. Een JSON Web Token (JWT) is gegenereerd op basis van de **handtekeningsleutel** ophalen van de **referenties**. De **referenties** gebruikt bij het maken van een exemplaar van **PowerBIClient**. Zodra u een exemplaar van hebt **PowerBIClient**, kunt u GetReports() en GetReportsAsync() aanroepen.

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

Zodra u hebt een **rapport**, u een **IFrame** voor het insluiten van de Power BI **rapport**. Hier volgt een codefragment van powerbi.js in de **Microsoft Power BI Embedded** voorbeeld.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>Filterrapporten die zijn ingesloten in uw toepassing

U kunt een ingesloten rapport filteren met behulp van een URL-syntaxis. U doet dit door u toevoegen een **$filter** Querytekenreeksparameter met een **eq** operator aan uw iFrame src-url met het opgegeven filter. Hier volgt de syntaxis van de filter-query:

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName} mag geen spaties of speciale tekens bevatten. De {fieldValue} accepteert één categorische waarde.  

## <a name="see-also"></a>Zie ook

[Algemene scenario's voor Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Een rapport insluiten](power-bi-embedded-embed-report.md)  
[Een nieuw rapport maken op basis van een gegevensset](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Voorbeeld van ingesloten JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Nog vragen? [Probeer de Power BI-community](http://community.powerbi.com/)
