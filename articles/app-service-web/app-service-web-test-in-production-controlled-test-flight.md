---
title: "Zeker implementatie (bètaversie testen) in Azure App Service"
description: "Informatie over het flight nieuwe functies in uw app of de updates in deze zelfstudie end-to-end bètaversie te testen. Deze samenbrengt App Service-functies, zoals continue publiceren, sleuven voor verkeersroutering en Application Insights-integratie."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: 83e3247310461ac148fff3c4ade3aa7216478537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Zeker implementatie (bètaversie testen) in Azure App Service
Deze zelfstudie wordt beschreven hoe u *zeker implementaties* door de integratie van de verschillende mogelijkheden van [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en [Azure Application Insights](/services/application-insights/).

*Zeker* is een implementatieproces te valideren en een nieuwe functie of wijzigen met een beperkt aantal echte klanten en is een belangrijke test in productiescenario's. Het is cloudbeheer beta testen en wordt ook wel aangeduid als 'beheerde test vlucht'. Veel grote ondernemingen met een aanwezigheid op het web gebruik deze benadering voor vroege validatie op hun app-updates in de praktijk van [flexibele ontwikkeling](https://en.wikipedia.org/wiki/Agile_software_development). Azure App Service kunt u testen in de productieomgeving integreren met continue publicatie en Application Insights dezelfde DevOps-scenario implementeren. Voordelen van deze benadering zijn:

* **Echte feedback krijgen *voordat* updates gepubliceerd naar productie** -het enige dat beter dan feedback krijgt als u de release is feedback krijgen voordat u loslaat. U kunt updates met echte gebruikersverkeer en gedragingen vroeg u wenst in de levenscyclus testen.
* **Verbeter [doorlopende test gebaseerde ontwikkeling (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  - door te testen in de productieomgeving integreren met continue integratie en instrumentation met Application Insights valideren van de gebruiker gebeurt vroeg en automatisch in de levenscyclus van het product. Dit reduceert de hoeveelheid tijd investeringen in handmatige testuitvoering.
* **Optimaliseert de werkstroom test** -door te testen in de productieomgeving met continue bewaking instrumentation automatiseren, kunt u mogelijk uitvoeren de doelstellingen van verschillende soorten tests in een enkel proces, zoals [integratie](https://en.wikipedia.org/wiki/Integration_testing), [regressie](https://en.wikipedia.org/wiki/Regression_testing), [bruikbaarheid](https://en.wikipedia.org/wiki/Usability_testing), toegankelijkheid, lokalisatie, [prestaties](https://en.wikipedia.org/wiki/Software_performance_testing), [beveiliging](https://en.wikipedia.org/wiki/Security_testing), en [ acceptatie](https://en.wikipedia.org/wiki/Acceptance_testing).

Een flighting implementatie is niet alleen om routering voor live verkeer. In een dergelijke implementatie die u meer inzicht krijgen zo snel mogelijk wilt maken, of het zijn een onverwachte fout, verminderde prestaties, gebruikerservaring problemen. Denk eraan dat u werkt met real-klanten. Dus om dat te doen rechts en u moet ervoor zorgen dat u hebt uw flighting implementatie ingesteld voor het verzamelen van alle gegevens die u nodig hebt om te beslissen voor de volgende stap. Deze zelfstudie ziet u het verzamelen van gegevens met Application Insights, maar u kunt New Relic of andere technologieën die past bij uw scenario.

## <a name="what-you-will-do"></a>Wat u doet
In deze zelfstudie leert u hoe u de volgende scenario's om uw App Service-app in productie testen samen te brengen:

* [Productie-verkeer routeren](app-service-web-test-in-production-get-start.md) aan uw app beta
* [Uw app instrumenteren](../application-insights/app-insights-web-track-usage.md) nuttig metrische gegevens ophalen
* Continu implementeren van uw bèta-app en live app metrische gegevens bijhouden
* Metrische gegevens tussen de productie-app en de bèta-app om te zien hoe codewijzigingen vertalen naar resultaten vergelijken

## <a name="what-you-will-need"></a>Wat u nodig hebt
* Een Azure-account
* Een [GitHub](https://github.com/) account
* Visual Studio 2015 - u kunt downloaden via de [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* GIT-Shell (geïnstalleerd met [GitHub voor Windows](https://windows.github.com/))-Hiermee kunt u de Git- en PowerShell-opdrachten kunt uitvoeren in dezelfde sessie
* Meest recente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits
* Basiskennis van de volgende opties:
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) sjabloonimplementatie (Zie [een complexe toepassing zoals verwacht in Azure implementeert](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> U hebt een Azure-account nodig om deze zelfstudie te voltooien.
>
> * U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/) -u ontvangt tegoed kunt u uitproberen betaalde Azure-services en zelfs nadat ze zijn gebruikt kunt u het account houden en gebruik gratis Azure-services, zoals Web-Apps.
> * U kunt [voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -uw Visual Studio-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.
>
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
>
>

## <a name="set-up-your-production-web-app"></a>Instellen van uw web-app voor productie
> [!NOTE]
> Het script in deze zelfstudie gebruikt configureert automatisch continue publiceren vanaf uw GitHub-opslagplaats. Dit is vereist dat uw GitHub-referenties worden al opgeslagen in Azure, anders mislukt de implementatie met de scripts bij een poging tot het configureren van instellingen voor bronbeheer voor de web-apps.
>
> Als u wilt uw GitHub-referenties in Azure opslaat, maakt u een web-app in de [Azure Portal](https://portal.azure.com/) en [GitHub implementatie configureren](app-service-continuous-deployment.md). U hoeft hiervoor eenmaal.
>
>

In een typische DevOps-scenario hebt u een toepassing die live in Azure wordt uitgevoerd en u wilt wijzigen via continue publiceren. In dit scenario implementeert u naar productie een sjabloon die u hebt ontwikkeld en getest.

1. Maak uw eigen fork van de [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) opslagplaats. Zie voor meer informatie over het maken van uw fork [een opslagplaats vertakken](https://help.github.com/articles/fork-a-repo/). Zodra uw fork is gemaakt, kunt u deze bekijken in uw browser.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Open een Git-Shell-sessie. Als u nog Git-Shell hebt, installeert u [GitHub voor Windows](https://windows.github.com/) nu.
3. Maak een lokale kloon van uw fork door het uitvoeren van de volgende opdracht:

     GIT kloon https://github.com/<your_fork>/ToDoApp.git
4. Wanneer u uw lokale kloon hebt, gaat u naar  *&lt;repository_root >*\ARMTemplates, en voer de deploy.ps1 script met een uniek achtervoegsel, zoals hieronder weergegeven:

     .\deploy.ps1 – RepoUrl https://github.com/<your_fork>/todoapp.git - ResourceGroupSuffix < your_suffix >
5. Wanneer u wordt gevraagd, typt u in de gewenste gebruikersnaam en het wachtwoord voor toegang tot de database. Vergeet niet de databasereferenties van uw omdat u ze opnieuw opgeven moet bij het bijwerken van de resourcegroep.

   U ziet de voortgang van de inrichting van verschillende Azure-resources. Wanneer implementatie is voltooid, wordt het script start de toepassing in de browser en bieden u een beschrijvende geluid.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. Terug in uw sessie Git Shell uitvoeren:

     . \swap – naam ToDoApp < your_suffix >

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Wanneer het script is voltooid, gaat u terug om te bladeren naar de frontend-adres (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) om te zien van de toepassing die wordt uitgevoerd in de productieomgeving.
8. Meld u aan bij de [Azure Portal](https://portal.azure.com/) en eens kijken wat wordt gemaakt.

   U moet kunnen zien van twee web-apps in dezelfde resourcegroep bevinden, één met de `Api` achtervoegsel in de naam. Als u de resourcegroepweergave bekijkt, ook ziet u de SQL-Database en -server, de App Service-abonnement en de staging-sleuven voor de web-apps. Blader door de verschillende bronnen en vergelijkt ze met  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json om te zien hoe deze zijn geconfigureerd in de sjabloon.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

U hebt de productie-app ingesteld.  Nu gaan we Stel dat u feedback of bruikbaarheid slechte voor de app is ontvangen. Zodat u besluit om te onderzoeken. U gaat softwareontwikkelaars van uw app om u feedback geven.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Onderzoeken: Uw client-app voor bewaking/metrieken softwareontwikkelaars
1. Open  *&lt;repository_root >*\src\MultiChannelToDo.sln in Visual Studio.
2. Herstellen van alle Nuget-pakketten met de rechtermuisknop op de oplossing > **NuGet-pakketten beheren voor oplossing** > **herstellen**.
3. Met de rechtermuisknop op **MultiChannelToDo.Web** > **Application Insights Telemetry toevoegen** > **-instellingen configureren** > resourcegroep wijzigen ToDoApp*&lt;your_suffix >* > **Application Insights toevoegen aan Project**.
4. Open de blade voor in de Azure-Portal, de **MultiChannelToDo.Web** toepassing inzicht resource. Klik in de **toepassingsstatus** deel, klikt u op **informatie over het verzamelen van gegevens van browser pagina laden** > code kopiëren.
5. De gekopieerde JS instrumentation Voeg code toe aan  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml vlak voordat de afsluiting `<heading>` label. De unieke instrumentatiesleutel van uw toepassing inzicht resource moet bevatten.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Aangepaste gebeurtenissen verzenden naar Application Insights voor muis klikken door de volgende code toe te voegen aan de onderkant van de hoofdtekst:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   In dit fragment JavaScript wordt een aangepaste gebeurtenis verzonden naar Application Insights telkens wanneer een gebruiker klikt op een willekeurige plaats in de web-app.
7. In de Git-Shell doorvoeren en push de wijzigingen naar uw fork in GitHub. Wacht tot clients browser te vernieuwen.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. De geïmplementeerde app-wijzigingen in productie wisselen:

     . \swap – naam ToDoApp < your_suffix >
9. Blader naar de Application Insights-resource die u hebt geconfigureerd. Klik op aangepaste gebeurtenissen.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Als er geen metrische gegevens voor aangepaste gebeurtenissen, wacht een paar minuten en klik op **vernieuwen**.

Stel dat u zien als een diagram hieronder:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

En het raster gebeurtenis hieronder:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

Volgens uw toepassingscode ToDoApp de **knop** gebeurtenis komt overeen met de verzendknop en de **invoer** gebeurtenis komt overeen met het tekstvak. Tot nu toe, zinvol wat zijn. Echter, het lijkt erop dat er een goede bedrag van muisklikken en zeer weinig klikken op de taakitems is (de **LI** gebeurtenissen).

Op basis van dit formulier u uw hypothese dat sommige gebruikers hebben verward welk gedeelte van de gebruikersinterface wordt geklikt en is omdat de cursor voor de geselecteerde tekst is opgemaakt als u dit op items in de lijst en hun pictogrammen.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Dit wordt mogelijk een voorbeeld van een gekunstelde. U gaat echter een verbetering van uw app maken en voert u een flighting implementatie voor de bruikbaarheid feedback van klanten live ophalen.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Softwareontwikkelaars van uw server-app voor bewaking/metrische gegevens
Dit is een tangens omdat het scenario dat in deze zelfstudie uitgelegd alleen met de client-app omgaat. Echter, voor de volledigheid stelt u de app-serverzijde.

1. Met de rechtermuisknop op **MultiChannelToDo** > **Application Insights Telemetry toevoegen** > **-instellingen configureren** > resourcegroep wijzigen ToDoApp*&lt;your_suffix >* > **Application Insights toevoegen aan Project**.
2. In de Git-Shell doorvoeren en push de wijzigingen naar uw fork in GitHub. Wacht tot clients browser te vernieuwen.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. De geïmplementeerde app-wijzigingen in productie wisselen:

     . \swap – naam ToDoApp < your_suffix >

Dat is alles.

## <a name="investigate-add-slot-specific-tags-to-your-client-app-metrics"></a>Onderzoeken: Sleuf-specifieke labels toevoegen aan de app metrische gegevens van uw client
In deze sectie configureert u de verschillende implementatiesites voor het verzenden van site-specifieke telemetrie naar dezelfde Application Insights-resource. Op deze manier kunt u telemetriegegevens tussen verkeer van andere sleuven (implementatieomgevingen) vergelijken eenvoudig overzicht van het effect van uw appwijzigingen. Op hetzelfde moment kunt u het verkeer van de productie van de rest scheiden, zodat u kunt doorgaan met het bewaken van uw productie-app naar behoefte.

Nadat u van gegevens op clientgedrag verzamelen bent, wordt u [een initialisatiefunctie telemetrie toevoegen aan uw JavaScript-code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml. Als u testen serverzijde prestaties wilt, bijvoorbeeld: u kunt ook doen op dezelfde manier in uw servercode (Zie [Application Insights-API voor aangepaste gebeurtenissen en metrische gegevens](../application-insights/app-insights-api-custom-events-metrics.md).

1. Voeg eerst de code bewteen de twee `//` opmerkingen hieronder in JavaScript blokkeren die u hebt toegevoegd aan de `<heading>` eerder labelen.

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    Deze code initialisatiefunctie zorgt ervoor dat de `appInsights` object toevoegen de naam van een aangepaste eigenschap `Environment` voor elk onderdeel van telemetrie verzendt.
2. Vervolgens voegt u deze aangepaste eigenschap als een [instelling sleuf](web-sites-staged-publishing.md#AboutConfiguration) voor uw web-app in Azure. Voer hiervoor de volgende opdrachten in uw sessie Git-Shell.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Het bestand Web.config in uw project al definieert de `environment` app-instelling. Met deze instelling wanneer u de app lokaal testen metrische gegevens over uw worden gemarkeerd met `VS Debugger`. Echter, wanneer u uw wijzigingen naar Azure pushen, Azure wordt zoeken en de `environment` app in plaats daarvan instelling in de web-app-configuratie en metrische gegevens over uw worden gemarkeerd met `Production`.
3. Doorvoeren en de codewijzigingen push naar uw fork op GitHub en wacht voor uw gebruikers de nieuwe app (u moet de browser te vernieuwen) gebruiken. Het duurt ongeveer 15 minuten voor de nieuwe eigenschap worden weergegeven in uw Application Insights `MultiChannelToDo.Web` resource.

        git add -A :/
        git commit -m "add environment property to AI events for client app"
        git push origin master
4. Nu gaat u naar de **aangepaste gebeurtenissen** blade opnieuw en filtert u de metrische gegevens op `Environment=Production`. Nu moet u alle nieuwe aangepaste gebeurtenissen in de productiesite zien met dit filter.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Klik op de **Favorieten** om op te slaan van de huidige Metrics Explorer-instellingen naar ongeveer **aangepaste gebeurtenissen: productie**. U kunt eenvoudig schakelen tussen deze weergaven en een implementatiesleuf later.

   > [!TIP]
   > Voor nog krachtiger analytics, kunt u overwegen [integreren van uw Application Insights-resource met Power BI](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-to-your-server-app-metrics"></a>Site-specifieke labels toevoegen aan uw app metrische servergegevens
Opnieuw voor de volledigheid stelt u de app-serverzijde. In tegenstelling tot de clientapp die in JavaScript is geïnstrumenteerd, sleuf-specifieke labels voor de server-app is geïnstrumenteerd met .NET-code.

1. Open  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs. Voeg het codeblok hieronder, net voordat de afsluiting accolade naamruimte.

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. De naam resolutie fouten corrigeren door toe te voegen de `using` instructies onder aan het begin van het bestand:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. De volgende code toevoegen aan het begin van de `Application_Start()` methode:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Doorvoeren en de codewijzigingen push naar uw fork op GitHub en wacht voor uw gebruikers de nieuwe app (u moet de browser te vernieuwen) gebruiken. Het duurt ongeveer 15 minuten voor de nieuwe eigenschap worden weergegeven in uw Application Insights `MultiChannelToDo` resource.

        git add -A :/
        git commit -m "add environment property to AI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Update: Stel uw vertakking beta
1. Open  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json en zoek de `appsettings` resources (zoeken naar `"name": "appsettings"`). Er zijn 4 daarvan, één voor elke site.
2. Voor elk `appsettings` resource, Voeg een `"environment": "[parameters('slotName')]"` app-instelling met het einde van de `properties` matrix. Vergeet niet om te beëindigen van de vorige regel met een komma.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    U hebt zojuist toegevoegd de `environment` app-instelling op de sleuven in de sjabloon.
3. Zoek in hetzelfde bestand de `slotconfignames` resources (zoeken naar `"name": "slotconfignames"`). Er zijn 2 één voor elke app.
4. Voor elk `slotconfignames` resource toevoegen `"environment"` aan het einde van de `appSettingNames` matrix. Vergeet niet om te beëindigen van de vorige regel met een komma.

    U zojuist hebt gemaakt de `environment` app stick instellen voor de respectieve implementatiesleuf voor beide apps.  
5. Voer de volgende opdrachten met het achtervoegsel met dezelfde resource groep die u eerder hebt gebruikt in uw sessie Git-Shell.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. Wanneer u wordt gevraagd, geeft u de dezelfde SQL-databasereferenties als voordat. Wanneer u wordt gevraagd om bij te werken van de resourcegroep, typ `Y`, klikt u vervolgens `ENTER`.

    Nadat het script is voltooid, worden alle resources in de oorspronkelijke resourcegroep bewaard, maar een nieuwe sleuf met de naam "bètaversie" wordt gemaakt in deze met dezelfde configuratie als de sleuf van 'Fasering' dat is gemaakt in het begin.

   > [!NOTE]
   > Deze methode voor het maken van verschillende omgevingen verschilt van de methode in [flexibele software ontwikkelen met Azure App Service](app-service-agile-software-development.md). Hier, maakt u implementatieomgevingen met implementatiesites, waar als er u implementatieomgevingen met resourcegroepen maken. Implementatieomgevingen beheren met resourcegroepen kunt u de productieomgeving off-limits houden voor ontwikkelaars, maar het is niet eenvoudig om testen in productie, waarmee u eenvoudig met sleuven doen kunt.
   >
   >

Als u wenst, kunt u ook een alfa-app maken door te voeren

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

Voor deze zelfstudie, wordt u alleen blijven gebruiken uw bèta-app.

## <a name="update-push-your-updates-to-the-beta-app"></a>Update: Implementeer uw updates naar de bètaversie-app
Terug naar uw app, die u wilt verbeteren.

1. Zorg ervoor dat u kunt nu uw vertakking beta

        git checkout beta
2. In  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, vinden de `<li>` labelen en voeg de `style="cursor:pointer"` kenmerk toe, zoals hieronder wordt weergegeven.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. doorvoeren en push naar Azure.
4. Controleer of dat de wijziging nu in de sleuf beta weergegeven wordt door te navigeren naar http://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/. Als u de wijziging nog niet ziet, vernieuw uw browser om de nieuwe javascript-code.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Nu dat u uw wijziging in de sleuf beta wordt uitgevoerd hebt, bent u klaar om een flighting te implementeren.

## <a name="validate-route-traffic-to-the-beta-app"></a>Valideren: Routeverkeer naar de bètaversie-app
In deze sectie wordt u verkeer doorstuurt naar de bètaversie-app. Ter verduidelijking van demonstratie gaat u een groot deel van het gebruikersverkeer te routeren. In werkelijkheid is afhankelijk de hoeveelheid verkeer die u wilt routeren van uw specifieke situatie. Bijvoorbeeld, als uw site op de schaal van microsoft.com is, mogelijk moet u minder dan één procent van uw totale verkeer om te kunnen krijgen tot nuttige gegevens.

1. Voer de volgende opdrachten aan de helft van de productie-verkeer wordt doorgestuurd naar de bèta-sleuf in de Git-Shell-sessie:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   De `ReroutePercentage=50` -eigenschap geeft op dat 50% van de productie-verkeer wordt doorgestuurd naar de bètaversie-app-URL (opgegeven door de `ActionHostName` eigenschap).
2. Nu gaat u naar http://ToDoApp*&lt;your_suffix >*. azurewebsites.net. nu wordt 50% van het verkeer omgeleid naar de bètaversie sleuf.
3. Filter in uw Application Insights-resource, de metrische gegevens door omgeving = "bètaversie".

   > [!NOTE]
   > Als u deze gefilterde weergave als een andere favoriet opslaan, kunt u eenvoudig de weergaven metrische explorer tussen productie en beta weergaven spiegelen.
   >
   >

Stel in Application Insights ziet u iets soortgelijks als in het volgende:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Niet alleen wordt dit weergegeven dat er zijn veel meer klikken op de `<li>` tags, maar wel een piek muisklikken op `<li>` labels. U kunt beëindigt dat mensen hebben gedetecteerd met de nieuwe `<li>` -tags zijn klikbaar en alle taken eerder voltooid in de app nu wordt gewist.

Op basis van de gegevens van uw flighting implementatie kunt bepalen u dat de nieuwe gebruikersinterface gereed voor productie is.

## <a name="go-live-move-your-new-code-into-production"></a>Ga live: je nieuwe code naar de productie verplaatsen
U bent nu klaar voor het verplaatsen van de update naar productie. Is die wat is een goede nu u weet dat de update is al gevalideerd *voordat* wordt deze doorgegeven naar productie. Nu kunt u probleemloos deze implementeren. Omdat u een update naar de AngularJS-client-app hebt aangebracht, worden alleen de client-side '-code gevalideerd. Als u wijzigingen aanbrengen in de back-end Web API-app, kunt u uw wijzigingen kan valideren op dezelfde manier en eenvoudig.

1. Git-shell, de regel voor het doorsturen van verkeer te verwijderen met de volgende opdracht:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Voer de Git-opdrachten:

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Wacht enkele minuten duren voordat de nieuwe code worden geïmplementeerd voor de faseringsite en vervolgens starten http://ToDoApp*&lt;your_suffix >*-staging.azurewebsites.net om te controleren of de nieuwe update in de faseringssleuf is opgewarmd. Houd er rekening mee dat de hoofdvertakking van uw fork is gekoppeld aan de faseringssleuf van uw app.
4. Nu de faseringssleuf wisselen naar de productie

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Samenvatting
Azure App Service gemakkelijk voor kleine-middelgrote bedrijven hun apps klantgerichte iets testen in productie, die normaal is uitgevoerd in grote ondernemingen. In het ideale geval, deze zelfstudie hebt gekregen de kennis die u nodig hebt bij elkaar brengt App Service en de Application Insights om mogelijke zeker implementatie en zelfs andere testen in productie-scenario's in uw DevOps-wereld.

## <a name="more-resources"></a>Meer bronnen
* [Flexibele software ontwikkelen met Azure App Service](app-service-agile-software-development.md)
* [Faseringsomgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md)
* [Een complexe toepassing zoals verwacht in Azure implementeren](app-service-deploy-complex-application-predictably.md)
* [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - de validatiefunctie JSON](http://jsonlint.com/)
* [GIT vertakking – basis vertakking en samenvoegen](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Project Kudu Wiki](https://github.com/projectkudu/kudu/wiki)
