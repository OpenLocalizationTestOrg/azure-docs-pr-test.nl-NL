---
title: aaaDiagnose fouten en uitzonderingen in web-apps met Azure Application Insights | Microsoft Docs
description: Uitzonderingen op de ASP.NET-apps samen met aanvraagtelemetrie vastleggen.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>Diagnose van uitzonderingen in uw web-apps met Application Insights
Uitzonderingen in uw live web-app worden gerapporteerd door [Application Insights](app-insights-overview.md). U kunt mislukte aanvragen correleren met uitzonderingen en andere gebeurtenissen bij zowel Hallo-client en server, zodat u snel kunt u onderzoeken Hallo oorzaken.

## <a name="set-up-exception-reporting"></a>Uitzondering reporting instellen
* toohave-uitzonderingen die zijn gerapporteerd door uw app server:
  * Installeer [Application Insights-SDK](app-insights-asp-net.md) in uw app-code of
  * IIS-webservers: Voer [Application Insights-Agent](app-insights-monitor-performance-live-website-now.md); of
  * Azure-web-apps: Hallo toevoegen [Application Insights-extensie](app-insights-azure-web-apps.md)
  * Java-web-apps: installatie Hallo [Java-agent](app-insights-java-agent.md)
* Hallo installeren [JavaScript-fragment](app-insights-javascript.md) in uw webpagina's toocatch browseruitzonderingen.
* In sommige App-frameworks of met een aantal instellingen, moet u tootake een aantal extra stappen toocatch meer uitzonderingen:
  * [Webformulieren](#web-forms)
  * [MVC](#mvc)
  * [Web-API-1.*](#web-api-1)
  * [Web-API 2.*](#web-api-2)
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>Diagnose van uitzonderingen met Visual Studio
Open Hallo app oplossing in Visual Studio toohelp met foutopsporing.

Hallo-app, uitvoeren op de server of op uw ontwikkelcomputer met behulp van F5.

Venster van de Application Insights zoeken Hallo openen in Visual Studio en stel deze toodisplay gebeurtenissen van uw app. Terwijl u fouten opspoort, kunt u dit doen door te klikken op de knop Application Insights Hallo.

![Met de rechtermuisknop op het Hallo-project en kies Application Insights openen.](./media/app-insights-asp-net-exceptions/34.png)

U ziet dat u alleen uitzonderingen voor Hallo rapport tooshow kunt filteren.

*Er zijn geen uitzonderingen weergegeven? Zie [vastleggen uitzonderingen](#exceptions).*

Klik op een rapport uitzondering tooshow de stacktracering.
Klik op de verwijzing naar een regel in de stacktracering hello, tooopen Hallo relevante codebestand.  

U ziet dat CodeLens gegevens over Hallo uitzonderingen bevat in Hallo-code:

![CodeLens melding van uitzonderingen.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a>Hello Azure-portal met fouten opsporen
Hallo Application Insights-overzicht van uw app, Hallo fouten tegel ziet u diagrammen van uitzonderingen en mislukte HTTP-aanvragen, samen met een lijst met Hallo aanvragen URL's die ertoe leiden de meest voorkomende fouten Hallo dat.

![Instellingen, fouten selecteren](./media/app-insights-asp-net-exceptions/012-start.png)

Klik door een van de Hallo is mislukt, uitzondering typen in Hallo lijst tooget tooindividual voorvallen Hallo uitzondering, kunt u Hallo details bekijken en stacktracering:

![Selecteer een exemplaar van een mislukte aanvraag en onder uitzonderingsdetails, kunt u tooinstances van Hallo-uitzondering.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

**U kunt ook** u kunt starten vanuit Hallo lijst met aanvragen en uitzonderingen gerelateerde tooit.

*Er zijn geen uitzonderingen weergegeven? Zie [vastleggen uitzonderingen](#exceptions).*


## <a name="custom-tracing-and-log-data"></a>Aangepaste tracering en logboekgegevens
tooget diagnostische gegevens specifieke tooyour app, kunt u code toosend uw eigen telemetriegegevens. Dit weergegeven in de diagnostische gegevens doorzoeken naast Hallo aanvraag, paginaweergave en andere gegevens automatisch verzameld.

U hebt verschillende mogelijkheden:

* [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) wordt doorgaans gebruikt voor het bewaken van gebruikspatronen maar Hallo gegevens ook worden verzonden, wordt weergegeven onder aangepaste gebeurtenissen in diagnostische gegevens doorzoeken. Gebeurtenissen zijn benoemde beheerverkeersstromen kan uitvoeren en eigenschappen van een verbindingsreeks en numerieke metrische gegevens waarop u kunt [uw diagnostische zoekopdrachten filteren](app-insights-diagnostic-search.md).
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) kunt u meer gegevens zoals POST informatie verzenden.
* [TrackException()](#exceptions) verzendt stack-traces. [Meer informatie over uitzonderingen](#exceptions).
* Als u al een framework voor logboekregistratie zoals Log4Net of NLog gebruikt, kunt u [deze logboeken vastleggen](app-insights-asp-net-trace-logs.md) en ze ziet in diagnostische gegevens doorzoeken samen met de aanvraag en uitzonderingsgegevens.

Deze gebeurtenissen, opent u toosee [Search](app-insights-diagnostic-search.md)Filter openen en kies vervolgens Custom Event, Trace of uitzondering.

![In detail analyseren](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> Als uw app veel telemetrie genereert, beperkt Hallo adaptieve steekproeven module automatisch Hallo volume dat toohello portal wordt verzonden door alleen een representatieve fractie van gebeurtenissen verzenden. Gebeurtenissen die deel van Hallo dezelfde bewerking worden geselecteerd of gedeselecteerd als groep, uitmaken zodat u tussen gerelateerde gebeurtenissen kunt navigeren. [Meer informatie over steekproeven.](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a>Hoe toosee postgegevens aanvragen
Aanvraaggegevens bevatten geen Hallo gegevens tooyour app verzonden in een POST-aanroep. toohave deze gegevens vermeld:

* [Hallo SDK installeren](app-insights-asp-net.md) in uw toepassingsproject.
* Voeg de code in uw toepassing toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace). Hallo postgegevens in parameter voor Hallo-bericht verzenden. Er is een grootte van de toohello toegestaan beperken zodat u toosend alleen Hallo essentiële gegevens moet proberen.
* Wanneer u bij het onderzoeken van een mislukte aanvraag vinden traceringen Hallo die zijn gekoppeld.  

![In detail analyseren](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a>Vastleggen van uitzonderingen en verwante diagnostische gegevens
Aanvankelijk ziet u niet in de portal Hallo alle Hallo uitzonderingen die ontstaan in uw app problemen. Ziet u alle browseruitzonderingen (als u Hallo [JavaScript SDK](app-insights-javascript.md) in uw webpagina's). Maar de meeste serveruitzonderingen zijn opgepikt door IIS en u een stukje code toosee toowrite hebt ze.

U kunt:

* **Meld u uitzonderingen expliciet** door code te plaatsen in uitzondering handlers tooreport Hallo uitzonderingen.
* **Uitzonderingen automatisch vastleggen** door het configureren van uw ASP.NET-framework. Hallo nodig toevoegingen zijn verschillend voor verschillende soorten framework.

## <a name="reporting-exceptions-explicitly"></a>Uitzonderingen expliciet rapportage
Hallo is eenvoudigste manier een aanroep van tooTrackException() in een uitzonderings-handler tooinsert.

Javascript

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

C#

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

VB

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

Hallo-eigenschappen en metingen parameters zijn optioneel, maar zijn handig voor [filtering en toe te voegen](app-insights-diagnostic-search.md) extra informatie. Als u een app hebt die verschillende games kunt uitvoeren, kan u bijvoorbeeld alle Hallo uitzondering rapporten verwante tooa bepaald spel vinden. U kunt zoveel objecten toevoegen als u zoals tooeach woordenlijst.

## <a name="browser-exceptions"></a>Browseruitzonderingen
De meeste browseruitzonderingen worden gerapporteerd.

Als de webpagina scriptbestanden van netwerken die inhoud leveren of andere domeinen bevat, zorg ervoor dat uw scriptcode Hallo-kenmerk heeft ```crossorigin="anonymous"```, en verzendt deze server Hallo [CORS headers](http://enable-cors.org/). Hierdoor kunt u een stack-trace tooget en details voor niet-verwerkte JavaScript-uitzonderingen van deze resources.

## <a name="web-forms"></a>Webformulieren
Hallo HTTP-Module zijn voor webformulieren kunnen toocollect Hallo uitzonderingen toe wanneer er geen omleidingen geconfigureerd met CustomErrors.

Maar als er actieve omleidingen, Hallo volgen regels toohello Application_Error functie in Global.asax.cs toevoegen. (Het bestand Global.asax toevoegen als u er nog geen hebt).

*C#*

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a>MVC
Als hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuratie is `Off`, en vervolgens uitzonderingen beschikbaar voor Hallo zijn [HTTP-Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect. Echter, als het `RemoteOnly` (standaard), of `On`, Hallo uitzondering worden gewist en niet beschikbaar voor Application Insights tooautomatically verzamelen. U kunt dit oplossen door het overschrijven van Hallo [System.Web.Mvc.HandleErrorAttribute klasse](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), en het toepassen van hallo overschreven klasse zoals weergegeven voor Hallo verschillende MVC versies onderstaande ([github-bron](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a>MVC 2
Hallo HandleError kenmerk vervangen door uw nieuw kenmerk in uw domeincontrollers.

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[Voorbeeld](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a>MVC 3
Registreren `AiHandleErrorAttribute` als globaal filter in Global.asax.cs:

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[Voorbeeld](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a>MVC 4, MVC5
Registreer AiHandleErrorAttribute als globaal filter in FilterConfig.cs:

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[Voorbeeld](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a>Web-API 1.x
System.Web.Http.Filters.ExceptionFilterAttribute overschrijven:

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

U kunt deze overschreven kenmerk toospecific domeincontrollers toevoegt of toohello globaal filterconfiguratie in Hallo WebApiConfig klasse toevoegen:

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[Voorbeeld](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

Er zijn een aantal cases dat Hallo uitzondering filters kunnen niet worden verwerkt. Bijvoorbeeld:

* Uitzonderingen uit controller constructors.
* Uitzonderingen uit bericht handlers.
* Uitzonderingen bij routering.
* Uitzonderingen tijdens de serialisatie van reacties inhoud.

## <a name="web-api-2x"></a>Web-API 2.x
Voeg een implementatie van IExceptionLogger toe:

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

Deze services toohello op WebApiConfig toevoegen:

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  }

[Voorbeeld](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

Als alternatief, kunt u het volgende doen:

1. Vervang Hallo alleen ExceptionHandler met een aangepaste implementatie van IExceptionHandler. Dit wordt alleen genoemd wanneer Hallo-framework is nog steeds kunnen toochoose welke antwoord bericht toosend (niet op Hallo verbinding voor exemplaar is afgebroken)
2. Uitzondering Filters (zoals beschreven in de sectie Hallo op Web-API 1.x domeincontrollers hierboven) - is niet in alle gevallen wordt aangeroepen.

## <a name="wcf"></a>WCF
Toevoegen van een klasse met kenmerk uitbreidt en IErrorHandler en IServiceBehavior implementeert.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

Hallo kenmerk toohello-serverimplementaties toevoegen:

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[Voorbeeld](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>Uitzondering-prestatiemeteritems
Als u hebt [Hallo Application Insights-Agent geïnstalleerd](app-insights-monitor-performance-live-website-now.md) op uw server, kunt u een grafiek van Hallo uitzonderingen snelheid, gemeten door .NET krijgen. Dit omvat verwerkte en onverwerkte uitzonderingen voor .NET.

Een metriek Explorer-blade geopend, Voeg een nieuwe grafiek toe en selecteer **uitzondering snelheid**, vermeld onder prestatiemeteritems.

Hallo .NET framework berekent Hallo snelheid Hallo aantal uitzonderingen in een interval tellen en te delen door Hallo lengte van hello-interval.

Houd er rekening mee dat deze wordt afwijken van Hallo 'uitzonderingen' aantal berekend door Hallo Application Insights-portal te tellen TrackException rapporten. Hallo steekproefintervals zijn verschillend en Hallo SDK niet TrackException rapporten voor alle verwerkte en onverwerkte uitzonderingen verzenden.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>Volgende stappen
* [REST, SQL en andere toodependencies aanroepen bewaken](app-insights-asp-net-dependencies.md)
* [Laadtijden voor pagina's, browseruitzonderingen en AJAX-aanroepen bewaken](app-insights-javascript.md)
* [Prestatiemeteritems van monitor](app-insights-performance-counters.md)
