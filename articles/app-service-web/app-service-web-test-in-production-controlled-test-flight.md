---
title: "aaaFlighting-implementatie (bètaversie testen) in Azure App Service"
description: Meer informatie over hoe uw updates in deze zelfstudie end-to-end tooflight nieuwe functies in uw app of beta testen. Deze samenbrengt App Service-functies, zoals continue publiceren, sleuven voor verkeersroutering en Application Insights-integratie.
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
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Zeker implementatie (bètaversie testen) in Azure App Service
Deze zelfstudie leert u hoe toodo *zeker implementaties* Hallo door integratie van verschillende mogelijkheden van [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en [Azure Application Insights](/services/application-insights/).

*Zeker* is een implementatieproces te valideren en een nieuwe functie of wijzigen met een beperkt aantal echte klanten en is een belangrijke test in productiescenario's. Deze overeenkomst vertonen toobeta is getest en wordt ook wel aangeduid als 'beheerde test vlucht'. Veel grote ondernemingen met een aanwezigheid op het web gebruik deze benadering voor vroege validatie op hun app-updates in de praktijk van [flexibele ontwikkeling](https://en.wikipedia.org/wiki/Agile_software_development). Azure App Service kunt u toointegrate testen in de productieomgeving met continue publicatie en Application Insights tooimplement Hallo hetzelfde DevOps-scenario. Voordelen van deze benadering zijn:

* **Echte feedback krijgen *voordat* updates zijn vrijgegeven tooproduction** -Hallo alleen wat is beter dan feedback krijgt als u de release feedback krijgen is voordat u loslaat. U kunt updates met de werkelijke gebruikersverkeer en het gedrag vroeg u wenst in de levenscyclus Hallo testen.
* **Verbeter [doorlopende test gebaseerde ontwikkeling (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  - door te testen in de productieomgeving integreren met continue integratie en instrumentation met Application Insights valideren van de gebruiker gebeurt vroeg en automatisch in de levenscyclus van het product. Dit reduceert de hoeveelheid tijd investeringen in handmatige testuitvoering.
* **Optimaliseert de werkstroom test** -door te testen in de productieomgeving met continue bewaking instrumentation automatiseren, kunt u mogelijk uitvoeren Hallo doelstellingen van verschillende soorten tests in een enkel proces, zoals [integratie](https://en.wikipedia.org/wiki/Integration_testing), [regressie](https://en.wikipedia.org/wiki/Regression_testing), [bruikbaarheid](https://en.wikipedia.org/wiki/Usability_testing), toegankelijkheid, lokalisatie, [prestaties](https://en.wikipedia.org/wiki/Software_performance_testing), [beveiliging](https://en.wikipedia.org/wiki/Security_testing), en [ acceptatie](https://en.wikipedia.org/wiki/Acceptance_testing).

Een flighting implementatie is niet alleen om routering voor live verkeer. In een dergelijke implementatie u toogain inzicht zo snel mogelijk, ongeacht of deze een onverwachte fout, verminderde prestaties, gebruikerservaring problemen. Denk eraan dat u werkt met real-klanten. In dat geval toodo deze rechts, moet u ervoor zorgen dat u hebt ingesteld uw flighting implementatie toogather alle Hallo-gegevens die u nodig hebt in volgorde toomake een gefundeerde beslissing nemen voor de volgende stap. Deze zelfstudie leert u hoe toocollect gegevens met Application Insights, maar u kunt New Relic of andere technologieën die past bij uw scenario.

## <a name="what-you-will-do"></a>Wat u doet
In deze zelfstudie leert u hoe toobring Hallo volgende scenario's samen tootest uw App Service-app in productie:

* [Productie-verkeer routeren](app-service-web-test-in-production-get-start.md) tooyour beta-app
* [Uw app instrumenteren](../application-insights/app-insights-web-track-usage.md) tooobtain nuttig metrische gegevens
* Continu implementeren van uw bèta-app en live app metrische gegevens bijhouden
* Metrische gegevens vergelijken tussen Hallo productie-app en Hallo beta app toosee hoe code verandert vertalen tooresults

## <a name="what-you-will-need"></a>Wat u nodig hebt
* Een Azure-account
* Een [GitHub](https://github.com/) account
* Visual Studio 2015 - kunt u downloaden Hallo [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* GIT-Shell (geïnstalleerd met [GitHub voor Windows](https://windows.github.com/))-Hierdoor kunt u toorun beide Hallo Git en PowerShell-opdrachten in Hallo dezelfde sessie
* Meest recente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits
* Basiskennis van Hallo volgende:
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) sjabloonimplementatie (Zie [een complexe toepassing zoals verwacht in Azure implementeert](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> U moet een Azure-account toocomplete in deze zelfstudie:
>
> * U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/) -u ontvangt tegoed kunt u tootry uit betaalde Azure-services en zelfs nadat ze zijn gebruikt u Hallo rekening kunt houden en gebruik gratis Azure-services, zoals Web-Apps.
> * U kunt [voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -uw Visual Studio-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.
>
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
>
>

## <a name="set-up-your-production-web-app"></a>Instellen van uw web-app voor productie
> [!NOTE]
> Hallo-script in deze zelfstudie gebruikt configureert automatisch continue publiceren vanaf uw GitHub-opslagplaats. Dit is vereist dat uw GitHub-referenties worden al opgeslagen in Azure, anders mislukt de implementatie van Hallo in een script vastgelegd tijdens een poging de instellingen voor bronbeheer tooconfigure voor Hallo web-apps.
>
> toostore uw GitHub-referenties in Azure, een web-app maken in Hallo [Azure Portal](https://portal.azure.com/) en [GitHub implementatie configureren](app-service-continuous-deployment.md). U hoeft alleen toodo dit één keer.
>
>

In een typisch scenario voor DevOps, hebt u een toepassing die wordt uitgevoerd in Azure in en gewenste toomake wijzigingen tooit via continue publiceren. In dit scenario implementeert u tooproduction een sjabloon die u hebt ontwikkeld en getest.

1. Maak uw eigen fork Hallo [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) opslagplaats. Zie voor meer informatie over het maken van uw fork [een opslagplaats vertakken](https://help.github.com/articles/fork-a-repo/). Zodra uw fork is gemaakt, kunt u deze bekijken in uw browser.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Open een Git-Shell-sessie. Als u nog Git-Shell hebt, installeert u [GitHub voor Windows](https://windows.github.com/) nu.
3. Maak een lokale kloon van uw fork door het uitvoeren van de volgende opdracht Hallo:

     GIT kloon https://github.com/<your_fork>/ToDoApp.git
4. Zodra u uw lokale kloon hebt, te navigeren*&lt;repository_root >*\ARMTemplates, en Voer Hallo deploy.ps1 script met een uniek achtervoegsel, zoals hieronder:

     .\deploy.ps1 – RepoUrl https://github.com/<your_fork>/todoapp.git - ResourceGroupSuffix < your_suffix >
5. Wanneer u wordt gevraagd, typt u in Hallo gewenst gebruikersnaam en wachtwoord voor toegang tot de database. Uw database referenties omdat u toospecify moet onthouden ze opnieuw wanneer bijwerken Hallo resourcegroep.

   U ziet de voortgang van de verschillende Azure-resources inrichten Hallo. Wanneer implementatie is voltooid, wordt de Hallo script toepassing hello in Hallo browser starten en de bieden u een beschrijvende geluid.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. Terug in uw sessie Git Shell uitvoeren:

     . \swap – naam ToDoApp < your_suffix >

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Wanneer Hallo-script is voltooid, gaat u terug toobrowse toohello frontend-adres (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee Hallo toepassing die wordt uitgevoerd in de productieomgeving.
8. Meld u aan bij Hallo [Azure Portal](https://portal.azure.com/) en eens kijken wat wordt gemaakt.

   U moet de web-apps kunnen toosee twee in Hallo dezelfde resourcegroep bevinden, één met de Hallo `Api` achtervoegsel in Hallo naam. Als u bekijkt hello resourcegroepweergave in, ook ziet u Hallo SQL-Database en -server, Hallo App Service-abonnement en fasering sleuven Hallo voor Hallo web-apps. Blader door de verschillende bronnen Hallo en vergelijkt ze met  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hoe deze zijn geconfigureerd in Hallo-sjabloon.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

U hebt Hallo productie-app ingesteld.  Nu gaan we Stel dat u feedback of bruikbaarheid slechte voor Hallo-app is ontvangen. U bepaalt dus tooinvestigate. U gaat tooinstrument uw app toogive u feedback.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Onderzoeken: Uw client-app voor bewaking/metrieken softwareontwikkelaars
1. Open  *&lt;repository_root >*\src\MultiChannelToDo.sln in Visual Studio.
2. Herstellen van alle Nuget-pakketten met de rechtermuisknop op de oplossing > **NuGet-pakketten beheren voor oplossing** > **herstellen**.
3. Met de rechtermuisknop op **MultiChannelToDo.Web** > **Application Insights Telemetry toevoegen** > **-instellingen configureren** > resourcegroep wijzigen tooToDoApp*&lt;your_suffix >* > **Application Insights toevoegen tooProject**.
4. Open in hello Azure Portal, Hallo blade voor Hallo **MultiChannelToDo.Web** toepassing inzicht resource. Klik dan in Hallo **toepassingsstatus** deel, klikt u op **meer informatie over hoe de gegevens voor het laden van browserpagina toocollect** > code kopiëren.
5. Voeg Hallo gekopieerd JS instrumentation code te*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml net vóór Hallo sluiten `<heading>` label. Hallo unieke instrumentatiesleutel van uw toepassing inzicht resource moet bevatten.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Aangepaste gebeurtenissen tooApplication Insights voor klikken met de muis door toe te voegen Hallo na code toohello onder aan de hoofdtekst verzenden:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Deze JavaScript-fragment verzendt een aangepaste gebeurtenis tooApplication Insights telkens wanneer een gebruiker klikt op een willekeurige plaats in Hallo web-app.
7. In de Git-Shell doorvoeren en uw wijzigingen tooyour fork push in GitHub. Wacht tot clients toorefresh browser.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Wisseling Hallo app wijzigingen tooproduction geïmplementeerd:

     . \swap – naam ToDoApp < your_suffix >
9. Blader toohello Application Insights-resource die u hebt geconfigureerd. Klik op aangepaste gebeurtenissen.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Als er geen metrische gegevens voor aangepaste gebeurtenissen, wacht een paar minuten en klik op **vernieuwen**.

Stel dat u zien als een diagram hieronder:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

En Hallo gebeurtenis raster hieronder:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

Volgens tooyour ToDoApp toepassingscode, Hallo **knop** gebeurtenis komt overeen met de knop verzenden toohello en Hallo **invoer** gebeurtenis komt overeen met toohello textbox. Tot nu toe, zinvol wat zijn. Echter, het lijkt erop dat er een goede bedrag van muisklikken en zeer weinig klikken op Hallo taakitems is (Hallo **LI** gebeurtenissen).

Op basis van dit formulier u uw hypothese dat sommige gebruikers hebben verward welk gedeelte van Hallo UI klikbaar en is dit omdat Hallo cursor voor de geselecteerde tekst is opgemaakt als u dit op Hallo lijstitems en hun pictogrammen.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Dit wordt mogelijk een voorbeeld van een gekunstelde. Niettemin u bent momenteel toomake een verbetering tooyour app en voer flighting implementatie tooget bruikbaarheid feedback van live-klanten.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Softwareontwikkelaars van uw server-app voor bewaking/metrische gegevens
Dit is een tangens omdat Hallo-scenario in deze zelfstudie uitgelegd alleen met de Hallo client-app omgaat. Echter, voor de volledigheid stelt u Hallo serverzijde app.

1. Met de rechtermuisknop op **MultiChannelToDo** > **Application Insights Telemetry toevoegen** > **-instellingen configureren** > resourcegroep wijzigen tooToDoApp*&lt;your_suffix >* > **Application Insights toevoegen tooProject**.
2. In de Git-Shell doorvoeren en uw wijzigingen tooyour fork push in GitHub. Wacht tot clients toorefresh browser.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Wisseling Hallo app wijzigingen tooproduction geïmplementeerd:

     . \swap – naam ToDoApp < your_suffix >

Dat is alles.

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>Onderzoeken: Metrische gegevens voor site-specifieke labels tooyour client app toevoegen
In deze sectie configureert u Hallo verschillende implementatie sleuven toosend sleuf-specifieke telemetrie toohello dezelfde Application Insights-resource. Op deze manier kunt u telemetrie vergelijken gegevens tussen verkeer van andere sleuven (implementatieomgevingen) tooeasily Hallo effect van uw appwijzigingen te bekijken. AT Hallo dezelfde tijd, kunt u Hallo productie verkeer van Hallo rest scheiden zodat u kunt doorgaan toomonitor uw productie-app naar behoefte.

Nadat u van gegevens op clientgedrag verzamelen bent, wordt u [toevoegen van een telemetrie initialisatiefunctie tooyour JavaScript-code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml. Als u tootest serverzijde prestaties wilt, bijvoorbeeld: u kunt ook doen op dezelfde manier in uw servercode (Zie [Application Insights-API voor aangepaste gebeurtenissen en metrische gegevens](../application-insights/app-insights-api-custom-events-metrics.md).

1. Voeg eerst Hallo code bewteen Hallo twee `//` opmerkingen hieronder in Hallo JavaScript-blok dat u toohello toegevoegd `<heading>` eerder labelen.

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

    Deze code initialisatiefunctie zorgt ervoor dat Hallo `appInsights` object tooadd Hallo een aangepaste eigenschap met de naam `Environment` tooevery stukje telemetrie verzendt.
2. Vervolgens voegt u deze aangepaste eigenschap als een [instelling sleuf](web-sites-staged-publishing.md#AboutConfiguration) voor uw web-app in Azure. toodo deze, Voer Hallo opdrachten te volgen in uw sessie Git-Shell.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Hallo Web.config in uw project al definieert Hallo `environment` app-instelling. Met deze instelling wanneer u een lokaal, Hallo-app test metrische gegevens over uw worden gemarkeerd met `VS Debugger`. Echter, wanneer u uw wijzigingen tooAzure pushen, Azure wordt zoeken en Hallo `environment` app-instelling in configuratie van de Hallo van web-app in plaats daarvan en metrische gegevens over uw worden gemarkeerd met `Production`.
3. Doorvoeren en uw code wijzigingen tooyour fork push op GitHub en wacht voor uw gebruikers toouse Hallo nieuwe app (nodig toorefresh Hallo-browser). Het duurt ongeveer 15 minuten voor de nieuwe eigenschap tooshow Hallo omhoog in uw Application Insights `MultiChannelToDo.Web` resource.

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. Nu gaat u toohello **aangepaste gebeurtenissen** blade opnieuw en filter Hallo metrische gegevens op `Environment=Production`. Nu moet u kunnen toosee alle Hallo nieuwe aangepaste gebeurtenissen in productie Hallo sleuf met dit filter.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Klik op Hallo **Favorieten** knop toosave Hallo huidige Metrics Explorer-instellingen toosomething zoals **aangepaste gebeurtenissen: productie**. U kunt eenvoudig schakelen tussen deze weergaven en een implementatiesleuf later.

   > [!TIP]
   > Voor nog krachtiger analytics, kunt u overwegen [integreren van uw Application Insights-resource met Power BI](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>Site-specifieke labels tooyour serverstatistieken app toevoegen
Opnieuw voor de volledigheid stelt u Hallo serverzijde app. In tegenstelling tot Hallo client-app die in JavaScript is geïnstrumenteerd, sleuf-specifieke labels voor Hallo server app is geïnstrumenteerd met .NET-code.

1. Open  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs. Hallo codeblok hieronder, net vóór Hallo naamruimte accolade sluiten toevoegen.

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
2. Hallo name resolution fouten corrigeren door toe te voegen Hallo `using` instructies hieronder toohello begin van Hallo-bestand:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Voeg code hieronder toohello begin Hallo Hallo `Application_Start()` methode:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Doorvoeren en uw code wijzigingen tooyour fork push op GitHub en wacht voor uw gebruikers toouse Hallo nieuwe app (nodig toorefresh Hallo-browser). Het duurt ongeveer 15 minuten voor de nieuwe eigenschap tooshow Hallo omhoog in uw Application Insights `MultiChannelToDo` resource.

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Update: Stel uw vertakking beta
1. Open  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json en zoeken naar Hallo `appsettings` resources (zoeken naar `"name": "appsettings"`). Er zijn 4 daarvan, één voor elke site.
2. Voor elk `appsettings` resource, Voeg een `"environment": "[parameters('slotName')]"` end van app-instelling toohello Hallo `properties` matrix. Vergeet niet tooend Hallo vorige regel met een komma.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    U hebt zojuist toegevoegd Hallo `environment` app tooall Hallo sleuven instellen in Hallo-sjabloon.
3. In hetzelfde bestand Hallo, Hallo zoeken `slotconfignames` resources (zoeken naar `"name": "slotconfignames"`). Er zijn 2 één voor elke app.
4. Voor elk `slotconfignames` resource toevoegen `"environment"` toohello einde van Hallo `appSettingNames` matrix. Vergeet niet tooend Hallo vorige regel met een komma.

    U hebt zojuist hebt gemaakt Hallo `environment` app instelling stick tooits respectieve implementatiesleuf voor beide apps.  
5. In de Git-Shell-sessie uitvoeren Hallo deze opdrachten Hello dezelfde resource groep achtervoegsel dat u eerder hebt gebruikt.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. Wanneer u wordt gevraagd, geeft u Hallo dezelfde referenties voor SQL-database als voorheen. Wanneer gevraagd vervolgens tooupdate Hallo-resourcegroep, type `Y`, klikt u vervolgens `ENTER`.

    Zodra het Hallo-script is voltooid, alle resources in de oorspronkelijke resourcegroep Hallo worden bewaard, maar een nieuwe site met de naam "bètaversie" wordt gemaakt in het met Hallo dezelfde configuratie als Hallo "Fasering" sleuf dat is gemaakt in Hallo begin.

   > [!NOTE]
   > Deze methode voor het maken van verschillende omgevingen verschilt van het Hallo-methode in [flexibele software ontwikkelen met Azure App Service](app-service-agile-software-development.md). Hier, maakt u implementatieomgevingen met implementatiesites, waar als er u implementatieomgevingen met resourcegroepen maken. Implementatieomgevingen beheren met resourcegroepen kunt u tookeep Hallo productie-omgeving off-limits toodevelopers, maar het is niet eenvoudig toodo testen in productie, waarmee u eenvoudig met sleuven doen kunt.
   >
   >

Als u wenst, kunt u ook een alfa-app maken door te voeren

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

Voor deze zelfstudie, wordt u alleen blijven gebruiken uw bèta-app.

## <a name="update-push-your-updates-toohello-beta-app"></a>Update: Push uw updates toohello beta-app
Back-tooyour-app die u tooimprove wilt maken.

1. Zorg ervoor dat u kunt nu uw vertakking beta

        git checkout beta
2. In  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, zoeken Hallo `<li>` labelen en voeg Hallo `style="cursor:pointer"` kenmerk toe, zoals hieronder wordt weergegeven.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. doorvoeren en tooAzure push.
4. Controleer of deze Hallo wijziging nu gereflecteerd in Hallo beta sleuf door te navigeren toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/. Als er geen Hallo wijzigen nog Vernieuw uw browser tooget Hallo nieuwe javascript-code.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Nu dat u uw wijziging in Hallo beta sleuf wordt uitgevoerd hebt, bent u klaar tooperform een flighting implementatie.

## <a name="validate-route-traffic-toohello-beta-app"></a>Valideren: Route verkeer toohello beta-app
In deze sectie wordt u verkeer toohello beta app versturen. Ter verduidelijking van demonstratie gaat u een groot deel van Hallo gebruiker verkeer tooit tooroute. Hallo hoeveelheid verkeer die u wilt dat tooroute hangen af van uw specifieke situatie in werkelijkheid is. Bijvoorbeeld, als uw site op Hallo van schaal van microsoft.com, mogelijk moet u minder dan één procent van uw totale verkeer in volgorde toogain nuttige gegevens.

1. In uw sessie Git Shell uitvoeren Hallo opdrachten tooroute na de helft van Hallo verkeer toohello beta productiesite:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   Hallo `ReroutePercentage=50` -eigenschap geeft op dat de 50% van Hallo productie verkeer gerouteerd toohello beta app-URL worden (opgegeven door Hallo `ActionHostName` eigenschap).
2. Navigeer nu toohttp://ToDoApp*&lt;your_suffix >*. azurewebsites.net. 50% van het Hallo-verkeer worden omgeleid toohello beta sleuf nu.
3. Filter in uw Application Insights-resource Hallo metrische gegevens door omgeving = "bètaversie".

   > [!NOTE]
   > Als u deze gefilterde weergave als een andere favoriet opslaan, kunt u eenvoudig hello metrische explorer weergaven tussen productie en beta weergaven spiegelen.
   >
   >

Stel in Application Insights ziet er iets dergelijks toohello:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Niet alleen wordt dit weergegeven dat er veel meer klikt op Hallo zijn `<li>` tags, maar er lijkt een piek muisklikken toobe op `<li>` labels. U kunt beëindigt mensen gedetecteerd zijn nieuwe Hallo `<li>` tags zijn klikbaar en alle taken eerder voltooid in Hallo-app wordt nu worden gewist.

Op basis van gegevens van uw implementatie flighting Hallo kunt bepalen u dat de nieuwe gebruikersinterface gereed voor productie is.

## <a name="go-live-move-your-new-code-into-production"></a>Ga live: je nieuwe code naar de productie verplaatsen
U bent nu klaar toomove uw tooproduction update. Is die wat is een goede nu u weet dat de update is al gevalideerd *voordat* tooproduction wordt deze doorgegeven. Nu kunt u probleemloos deze implementeren. Nadat u een update toohello AngularJS-client-app hebt gemaakt, worden alleen Hallo clientcode gevalideerd. Als u toomake wijzigingen toohello back-end Web API-app, kunt u uw wijzigingen kan valideren op dezelfde manier en eenvoudig.

1. In de Git-Shell verwijderen routeringsregel Hallo-verkeer door het uitvoeren van de volgende opdracht Hallo:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Voer Hallo Git-opdrachten:

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Wacht een paar minuten voordat Hallo nieuwe toobe geïmplementeerd toohello faseringssleuven code en vervolgens starten http://ToDoApp*&lt;your_suffix >*-staging.azurewebsites.net tooverify die nieuwe update Hallo is opgewarmd in Hallo fasering sleuf. Houd er rekening mee dat uw fork hoofdvertakking is Hallo gekoppeld toohello fasering sleuf van uw app.
4. Nu wisselen Hallo faseringssleuven in productie

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Samenvatting
Azure App Service maakt het eenvoudig voor kleine toomedium grote bedrijven tootest hun apps klantgerichte in productie, is er iets die doorgaans in grote ondernemingen is uitgevoerd. In het ideale geval, deze zelfstudie hebt gekregen kennis moet u toobring samen App Service en de Application Insights toomake mogelijke zeker implementatie en zelfs andere testen in productie-scenario's in uw DevOps-wereld Hallo.

## <a name="more-resources"></a>Meer bronnen
* [Flexibele software ontwikkelen met Azure App Service](app-service-agile-software-development.md)
* [Faseringsomgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md)
* [Een complexe toepassing zoals verwacht in Azure implementeren](app-service-deploy-complex-application-predictably.md)
* [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - Hallo JSON Validator](http://jsonlint.com/)
* [GIT vertakking – basis vertakking en samenvoegen](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Project Kudu Wiki](https://github.com/projectkudu/kudu/wiki)
