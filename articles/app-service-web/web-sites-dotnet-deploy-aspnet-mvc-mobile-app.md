---
title: een ASP.NET MVC 5 aaaDeploy mobiele web-app in Azure App Service
description: Een zelfstudie waarmee u leert u hoe een web-app tooAzure App Service met behulp van mobiele toodeploy functies in ASP.NET MVC 5-webtoepassing.
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a>Een ASP.NET MVC 5 mobiele web-app in Azure App Service implementeren
Deze zelfstudie leert u basisprincipes van hoe een ASP.NET MVC 5 toobuild web-app die mobiele apparaten geschikte Hallo en tooAzure App Service implementeren. Voor deze zelfstudie, moet u [Visual Studio Express 2013 for Web] [ Visual Studio Express 2013] of Hallo professional edition van Visual Studio als u die hebt. U kunt [Visual Studio 2015] maar Hallo schermopnamen afwijken en moet u Hallo ASP.NET 4.x-sjablonen.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a>Wat u moet bouwen
Voor deze zelfstudie, voegt u functies voor mobiele toohello eenvoudige conferentie aanbieding toepassing die opgegeven in Hallo [starter project][StarterProject]. Hallo volgende schermafbeelding ziet u Hallo ASP.NET-sessies in de toepassing hello voltooid, zoals te zien is in de browser-emulator Hallo in Internet Explorer 11 F12-hulpprogramma's voor ontwikkelaars.

![][FixedSessionsByTag]

Kunt u Internet Explorer 11 F12 Hallo-hulpprogramma's voor ontwikkelaars en Hallo [Fiddler hulpprogramma] [ Fiddler] toohelp opsporen in uw toepassing. 

## <a name="skills-youll-learn"></a>U leert vaardigheden
Dit is wat u leert:

* Hoe toouse Visual Studio 2013 toopublish uw webtoepassing rechtstreeks tooa web-app in Azure App Service.
* Hoe sjablonen Hallo ASP.NET MVC 5 Hallo CSS Bootstrap framework gebruiken voor het verbeteren van de weergave op mobiele apparaten
* Hoe toocreate mobiele-specifieke tootarget specifieke mobiele browsers, zoals Hallo iPhone- en Android-weergaven
* Hoe toocreate responsief weergaven (weergaven die toodifferent browsers op apparaten reageren)

## <a name="set-up-hello-development-environment"></a>Hallo-ontwikkelomgeving instellen
Uw ontwikkelomgeving instellen door het installeren van hello Azure SDK voor .NET 2.5.1 of hoger. 

1. tooinstall hello Azure SDK voor .NET, klik op onderstaande koppeling voor Hallo. Als u geen Visual Studio 2013 nog is geïnstalleerd, wordt deze door een koppeling Hallo geïnstalleerd. Deze zelfstudie vereist de Visual Studio 2013. [Azure SDK voor Visual Studio 2013][AzureSDKVs2013]
2. Op het Web Platform Installer venster Hallo **installeren** te gaan met Hallo-installatie.

U moet ook een browser mobiele emulator. Geen van de volgende Hallo werkt:

* Browser-Emulator in [Internet Explorer 11 F12 ontwikkelhulpprogramma's] [ EmulatorIE11] (gebruikt in alle mobiele browser schermafbeeldingen). Deze heeft gebruiker agent tekenreeks standaardinstellingen voor Windows Phone 8, Windows Phone 7 en Apple iPad.
* Browser-Emulator in [Google Chrome DevTools][EmulatorChrome]. Deze bevat standaardinstellingen voor talloze Android-apparaten, evenals Apple iPhone, iPad Apple en Amazon Kindle Fire. Het emuleert touch-gebeurtenissen ook.
* [Opera mobiele Emulator][EmulatorOpera]

Visual Studio-projecten met C\# broncode tooaccompany beschikbaar zijn in dit onderwerp:

* [Download voor Starter-project][StarterProject]
* [Download voor project voltooid][CompletedProject]

## <a name="bkmk_DeployStarterProject"></a>Hallo starter project tooan Azure-web-app implementeren
1. Hallo conferentie aanbieding toepassing downloaden [starter project][StarterProject].
2. Klik in Windows Verkenner met de rechtermuisknop op Hallo gedownloade ZIP-bestand en kies *eigenschappen*.
3. In Hallo **eigenschappen** dialoogvenster Kies Hallo **blokkering** knop. (Deblokkering wordt voorkomen dat een beveiligingswaarschuwing die optreedt wanneer u toouse probeert een *.zip* -bestand dat u hebt gedownload vanuit web Hallo.)
4. Met de rechtermuisknop op Hallo ZIP-bestand en selecteer **Alles uitpakken** Hallo-bestand uitpakken. 
5. Open in Visual Studio Hallo *C#\Mvc5Mobile.sln* bestand.
6. Klik in Solution Explorer met de rechtermuisknop op het Hallo-project en klik op **publiceren**.
   
   ![][DeployClickPublish]
7. Klik in het Web publiceren op **Microsoft Azure App Service**.
   
   ![][DeployClickWebSites]
8. Als u nog niet al aangemeld bij Azure, klikt u op **account toevoegen**.
   
   ![][DeploySignIn]
9. Ga als volgt Hallo prompts toolog in uw Azure-account.
10. Hallo dialoogvenster App Service wordt nu u weergegeven, zoals aangemeld. Klik op **Nieuw**.
    
    ![][DeployNewWebsite]  
11. In Hallo **Web-Appnaam** veld, geeft u een unieke app-voorvoegsel. De naam van uw volledige web-app worden  *&lt;voorvoegsel >*. azurewebsites.net. Ook selecteren of geef een nieuwe Resourcegroepnaam in **resourcegroep**. Klik vervolgens op **nieuw** toocreate een nieuw App Service-plan.
    
    ![][DeploySiteSettings]
12. Hallo nieuwe App Service-abonnement configureren en klik op **OK**. 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. Klik op terug in het dialoogvenster Create App Service Hallo, **maken**.
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. Nadat hello Azure-resources zijn gemaakt, wordt met instellingen voor uw nieuwe app Hallo Hallo webpublicatie dialoogvenster ingevuld. Klik op **Publish**.
    
    ![][DeployPublishSite]
    
    Als Visual Studio is voltooid publishing Hallo starter-project toohello Azure-web-app, open Hallo bureaublad browser toodisplay Hallo live web-app.
15. Start uw browser mobiele emulator, Hallo-URL voor Hallo conferentie toepassing kopiëren (*<prefix>*. azurewebsites.net) in de emulator hello, en klik op de knop rechts bovenaan en selecteer **bladeren door de tag**. Als u van Internet Explorer 11 als standaardbrowser hello gebruikmaakt, hoeft u alleen tootype `F12`, klikt u vervolgens `Ctrl+8`, en wijzig vervolgens de browser-profiel op Hallo te**Windows Phone**. De onderstaande afbeelding ziet u Hallo *AllTags* weergeven in de modus Staand (wordt gekozen door **bladeren door de tag**).
    
    ![][AllTags]

> [!TIP]
> Terwijl u fouten in uw MVC 5-toepassingen vanuit Visual Studio opsporen kunt, kunt u uw web-app tooAzure publiceren opnieuw tooverify Hallo live web-app rechtstreeks vanuit uw mobiele browser of een browser-emulator.
> 
> 

Hallo-weergave is erg leesbaar op een mobiel apparaat. U ziet ook al enkele Hallo visual effecten toegepast door Hallo Bootstrap CSS-framework.
Klik op Hallo **ASP.NET** koppeling.

![][SessionsByTagASP.NET]

Hallo ASP.NET tag weergave is zoomen gemonteerd toohello-scherm Bootstrap automatisch voor u gebeurt. U kunt echter deze weergave toobetter gesorteerde Hallo mobiele browser verbeteren. Bijvoorbeeld, Hallo **datum** kolom moeilijk leesbaar is. Later in de zelfstudie Hallo wijzigt u Hallo *AllTags* toomake weergeven deze mobiele apparaten geschikte.

## <a name="bkmk_bootstrap"></a>Bootstrap CSS-Framework
Sjabloon is nieuw in Hallo MVC 5 ingebouwde Bootstrap ondersteuning. U hebt al gezien hoe deze verschillende weergaven in uw toepassing hello onmiddellijk verbetert. Hallo-navigatiebalk bovenaan Hallo is automatisch samenvouwbare Hallo browser breedte kleiner is. Wijzig het formaat van het browservenster Hallo op Hallo bureaublad browser, en zien hoe de navigatiebalk Hallo verandert het uiterlijk. Dit is Hallo responsief ontwerp die is ingebouwd in de Bootstrap.

toosee hoe Hallo Web-app eruit zonder Bootstrap, open *App\_Start\\BundleConfig.cs* en uitcommentarieer Hallo regels met *bootstrap.js* en *bootstrap.css*. Hallo volgende code toont Hallo laatste twee instructies Hallo `RegisterBundles` methode na Hallo wijziging:

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

Druk op `Ctrl+F5` toorun Hallo-toepassing.

Houd rekening met dat deze Hallo samenvouwbare navigatiebalk is nu alleen een gewone niet-geordende lijst. Klik op **bladeren door de tag** opnieuw in en klik vervolgens op **ASP.NET**.
In de weergave van de mobiele emulator hello ziet u nu dat het is niet meer toohello zoomen gemonteerd scherm en u horizontaal in volgorde toosee Hallo rechterzijde van Hallo tabel schuiven moet.

![][SessionsByTagASP.NETNoBootstrap]

De wijzigingen ongedaan maken en vernieuwen Hallo mobiele browser tooverify Hallo mobiele apparaten geschikte weer is hersteld.

Bootstrap is niet specifiek tooASP.NET MVC 5 en kunt u profiteren van deze functies in een webtoepassing. Maar is nu ingebouwd in de ASP.NET MVC 5-projectsjabloon, zodat uw MVC 5-webtoepassing van de Bootstrap standaard profiteren kan.

Ga voor meer informatie over Bootstrap toothe [Bootstrap] [ BootstrapSite] site.

In de volgende sectie Hallo ziet u hoe tooprovide mobile browser specifieke weergaven.

## <a name="bkmk_overrideviews"></a>Hallo weergaven, indelingen en gedeeltelijke weergaven overschrijven
U kunt elke weergave (inclusief indelingen en gedeeltelijke weergaven) voor mobiele browsers in het algemeen voor een afzonderlijke mobiele browser of voor een bepaalde browser overschrijven. tooprovide een mobiele-specifieke weergeven, kunt u een weergavebestand kopiëren en toevoegen *. Mobiele* toohello bestandsnaam. Bijvoorbeeld een mobiele telefoon toocreate *Index* weergeven, kunt u *weergaven\\Start\\Index.cshtml* naar *weergaven\\Start\\ Index.Mobile.cshtml*.

In deze sectie maakt u een indelingsbestand mobile-specifieke.

toostart, kopie *weergaven\\gedeelde\\\_Layout.cshtml* naar *weergaven\\gedeelde\\\_Layout.Mobile.cshtml* . Open  *\_Layout.Mobile.cshtml* en wijzig Hallo titel van **MVC5 toepassing** te**MVC5 toepassing (mobiel)**.

In elk `Html.ActionLink` -aanroep voor navigatiebalk hello, verwijdert u 'Zoeken op' in elke koppeling *ActionLink*. Hallo volgende code toont Hallo voltooid `<ul class="nav navbar-nav">` tag van Hallo mobiele indelingsbestand.

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

Kopiëren Hallo *weergaven\\Start\\AllTags.cshtml* van het bestand in *weergaven\\Start\\AllTags.Mobile.cshtml*. Open nieuwe Hallo-bestand en wijzig de `<h2>` -element van de 'Labels' te ' labels (M) ':

    <h2>Tags (M)</h2>

Blader toohello labels pagina met een bureaublad browser en browser mobiele emulator. Hallo mobiele browser emulator Hallo bevat twee wijzigingen (titel van Hallo  *\_Layout.Mobile.cshtml* en de titel van Hallo *AllTags.Mobile.cshtml*).

![][AllTagsMobile_LayoutMobile]

Daarentegen Hallo bureaubladweergave niet is gewijzigd (met de titels van  *\_Layout.cshtml* en *AllTags.cshtml*).

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a>Browser-specifieke weergaven maken
Bovendien toomobile-specifieke en bureaublad-specifieke weergaven, kunt u weergaven voor een afzonderlijke browser. U kunt bijvoorbeeld weergaven die specifiek voor Hallo iPhone- of Android-browser Hallo zijn maken. In deze sectie maakt u een indeling voor Hallo iPhone browser en een iPhone-versie van Hallo *AllTags* weergeven.

Open Hallo *Global.asax* bestand en voeg Hallo na code toohello onder aan de `Application_Start` methode.

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

Deze code definieert een nieuwe weergavemodus met de naam 'iPhone' die wordt vergeleken met elke inkomende aanvraag. Als de binnenkomende aanvraag Hallo overeenkomt met de voorwaarde die u gedefinieerd (dat wil zeggen, als de gebruikersagent Hallo bevat Hallo tekenreeks 'iPhone'), zoekt ASP.NET MVC weergaven waarvan de naam het achtervoegsel 'iPhone bevat'.

> [!NOTE]
> Wanneer toe te voegen mobiele browserspecifieke weergavemodus, zoals voor iPhone- en Android, of tooset Hallo eerste argument te worden`0` (insert Hallo boven aan het Hallo-lijst) toomake ervoor die Hallo browserspecifieke modus heeft voorrang op Hallo mobile-sjabloon (*. Mobile.cshtml). Als mobile Hallo-sjabloon in plaats daarvan Hallo boven aan het Hallo-lijst is, wordt het via uw beoogde weergavemodus geselecteerd (eerste overeenkomst wins Hallo en Hallo mobiele sjabloon komt overeen met alle mobiele browsers). 
> 
> 

Hallo-code, met de rechtermuisknop op `DefaultDisplayMode`, kies **los**, en kies vervolgens `using System.Web.WebPages;`. Hiermee voegt u een verwijzing toothe `System.Web.WebPages` naamruimte, is de locatie de `DisplayModeProvider` en `DefaultDisplayMode` typen zijn gedefinieerd.

![][ResolveDefaultDisplayMode]

U kunt ook kunt u alleen handmatig Hallo regel toothe na toevoegen `using` sectie van het Hallo-bestand.

    using System.Web.WebPages;

Hallo wijzigingen opslaan. Kopieer de *weergaven\\gedeelde\\\_Layout.Mobile.cshtml* van het bestand in *weergaven\\gedeelde\\\_Layout.iPhone.cshtml*. Hallo nieuw bestand open en wijzig de titel van Hallo `MVC5 Application (Mobile)` naar `MVC5 Application (iPhone)`.

Kopiëren Hallo *weergaven\\Start\\AllTags.Mobile.cshtml* van het bestand in *weergaven\\Start\\AllTags.iPhone.cshtml*. Wijzig in nieuw bestand Hallo Hallo `<h2>` element van ' labels (M) ' te 'Tags (iPhone)'.

Hallo-toepassing uitvoeren. Voer een emulator mobiele browser, zorg ervoor dat de gebruikersagent te is ingesteld 'iPhone' en blader toohello *AllTags* weergeven. Als u de emulator Hallo in Internet Explorer 11 F12 ontwikkelhulpprogramma's gebruikt, configureert u emulatie toohello volgende:

* Browser-profiel = **Windows Phone**
* Tekenreeks van de gebruikersagent = **aangepast**
* Aangepaste tekenreeks = **Apple-iPhone5C1/1001.525**

Hallo volgende schermafbeelding ziet u Hallo *AllTags* weergave die wordt weergegeven in de emulator in Internet Explorer 11 F12 ontwikkelhulpprogramma's met aangepaste tekenreeks gebruikersagent hello (dit is een tekenreeks van de gebruikersagent iPhone 5 C).

![][AllTagsIPhone_LayoutIPhone]

Selecteer in de mobiele browser Hallo Hallo **luidsprekers** koppeling. Omdat er geen een mobiele weergave (*AllSpeakers.Mobile.cshtml*), Hallo standaard luidsprekers weergeven (*AllSpeakers.cshtml*) is gegenereerd door middel van Hallo mobiele weergave ( *\_ Layout.Mobile.cshtml*). Zoals hieronder aangegeven, Hallo titel **MVC5 toepassing (mobiel)** is gedefinieerd in  *\_Layout.Mobile.cshtml*.

![][AllSpeakers_LayoutMobile]

U kunt een standaard (niet-mobiele) weergave van rendering binnen een mobiele indeling globaal uitschakelen door in te stellen `RequireConsistentDisplayMode` naar `true` in Hallo *weergaven\\\_ViewStart.cshtml* bestand als volgt:

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

Wanneer `RequireConsistentDisplayMode` te is ingesteld,`true`, mobiele Hallo-indeling (*\_Layout.Mobile.cshtml*) wordt alleen gebruikt voor mobiele weergaven (dat wil zeggen wanneer het weergavebestand is van Hallo formulier  ***weergavenaam** . Mobile.cshtml*). U kunt tooset `RequireConsistentDisplayMode` te`true` als uw mobiele lay-out niet goed met niet-mobiele weergaven werkt. Hallo schermafbeelding hieronder toont hoe Hallo *luidsprekers* behalve wanneer `RequireConsistentDisplayMode` te is ingesteld,`true` (zonder Hallo tekenreeks '(mobiel)' in hello navigeerbare balk Hallo boven).

![][AllSpeakers_LayoutMobileOverridden]

U kunt consistent weergavemodus in een bepaalde weergave uitschakelen door in te stellen `RequireConsistentDisplayMode` te`false` in Hallo-bestand voor weergave. De volgende tekst in Hallo *weergaven\\Start\\AllSpeakers.cshtml* bestand sets `RequireConsistentDisplayMode` te`false`:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

In deze sectie we hebt gezien hoe toocreate mobiele indelingen en weergaven en hoe toocreate indelingen en weergaven voor specifieke apparaten, zoals iPhone Hallo.
Hallo belangrijkste voordeel van het Hallo Bootstrap CSS-framework is echter de responsieve indeling, wat betekent dat een enkele opmaakmodel kan worden toegepast op het bureaublad, telefoon en Tablet PC-browsers toocreate een consistent uiterlijk. In de volgende sectie Hallo ziet u hoe tooleverage toocreate mobiele apparaten geschikte Bootstrap weergaven.

## <a name="bkmk_Improvespeakerslist"></a>Hallo luidsprekers lijst verbeteren
Zoals u zojuist hebt gezien, Hallo *luidsprekers* weergave kan worden gelezen, maar Hallo koppelingen zijn klein en moeilijk tootap op een mobiel apparaat. In deze sectie maakt u Hallo *AllSpeakers* weergave mobiele apparaten geschikte, die grote, gemakkelijk Tik koppelingen worden weergegeven en bevat een zoekopdracht vak tooquickly luidsprekers vinden.

Kunt u Hallo Bootstrap [gekoppelde lijstgroep] [ linked list group] stijlen voor het verbeteren van Hallo *luidsprekers* weergeven. In *weergaven\\Start\\AllSpeakers.cshtml*, Hallo inhoud van Hallo Razor bestand vervangen door Hallo-code hieronder.

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

Hallo `class="list-group"` kenmerk in Hallo `<div>` tag geldt de Bootstrap lijst stijlen en Hallo `class="input-group-item"` kenmerk Bootstrap lijst item stijlen tooeach koppeling wordt toegepast.

Hallo mobiele browser vernieuwen. Hallo bijgewerkt weergave ziet er als volgt:

![][AllSpeakersFixed]

Hallo Bootstrap [gekoppelde lijstgroep] [ linked list group] stijlen maakt Hallo hele vak voor elke koppeling geklikt, dit een veel betere gebruikerservaring is. Overschakelen van toothe bureaublad en bekijk Hallo consistente look gebruiken.

![][AllSpeakersFixedDesktop]

Hallo mobiele browserweergave is verbeterd, is het moeilijk om te navigeren Hallo lange lijst met luidsprekers. Bootstrap geen biedt een zoekopdracht filter functionaliteit out-of-the-box, maar u kunt deze toevoegen met een paar regels code. U wordt eerst een zoekopdracht vak toohello weergave toevoegen en vervolgens met JavaScript-code voor filterfunctie Hallo Hallo aansluiten. In *weergaven\\Start\\AllSpeakers.cshtml*, Voeg een \<formulier\> code direct na Hallo \<h2\> labels, zoals hieronder wordt weergegeven:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

U ziet dat Hallo `<form>` en `<input>` labels beide Hallo Bootstrap stijlen toegepast toothem hebben. Hallo `<span>` element voegt een Bootstrap [glyphicon] [ glyphicon] toothe zoekvak.

In Hallo *Scripts* map, Voeg een JavaScript-bestand aangeroepen *filter.js*. Hallo-bestand openen en plak Hallo code in het volgende:

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

U moet ook tooinclude filter.js in uw geregistreerde pakketten. Open *App\_Start\\BundleConfig.cs* en eerste hello-pakketten te wijzigen. Wijzigen van de eerste `bundles.Add` instructie (voor Hallo **jquery** bundel) tooinclude *Scripts\\filter.js*als volgt:

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

Hallo **jquery** bundel wordt al weergegeven Hallo standaard  *\_lay-out* weergeven. Later kunt u gebruikmaken van Hallo dezelfde JavaScript-code tooapply de lijstweergaven filter functionaliteit tooother.

Vernieuw Hallo mobiele browser en ga toohello *AllSpeakers* weergeven. In het zoekvak typt u 'sc'. Hallo luidsprekers lijst moet nu worden gefilterd op basis van de zoekreeks tooyour.

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a>Hallo lijst Tags verbeteren
Zoals Hallo *luidsprekers* weergeven, hello *labels* weergave kan worden gelezen, maar Hallo koppelingen zijn kort en moeilijk tootap op een mobiel apparaat. Kunt u Hallo oplossen *labels* weergave Hallo dezelfde manier oplossen van Hallo *luidsprekers* weergeven, als u codewijzigingen Hallo beschreven eerder, maar met de volgende Hallo `Html.ActionLink` syntaxis van de methode in  *Weergaven\\Start\\AllTags.cshtml*:

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

Hallo vernieuwd bureaublad browser ziet er als volgt:

![][AllTagsFixedDesktop]

En Hallo vernieuwd mobiele browser ziet er als volgt: 

![][AllTagsFixed]

> [!NOTE]
> Als u dat Hallo oorspronkelijke lijstopmaak merkt is er nog steeds mobiele browser Hallo en zich afvragen wat is er gebeurd tooyour nice Bootstrap stijlen, is dit een artefact van uw eerdere actie toocreate mobiele specifieke weergaven. Nu dat u Hallo Bootstrap CSS-framework toocreate een responsief ontwerp gebruikt, gaat u head en verwijderen van deze mobiele-specifieke weergaven en Hallo mobiele-specifieke indeling. Wanneer u dit hebt gedaan, wordt vernieuwd mobiele browser Hallo Hallo Bootstrap stijlen weergegeven.
> 
> 

## <a name="bkmk_improvedates"></a>Hallo lijst datums verbeteren
U kunt de verbeteren Hallo *datums* weergeven zoals verbeterde van Hallo *luidsprekers* en *labels* bekijkt hello codewijzigingen beschreven eerder, maar met de volgende Hallo Alsu`Html.ActionLink` syntaxis van de methode in *weergaven\\Start\\AllDates.cshtml*:

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

U ontvangt een weergave vernieuwd mobiele browser als volgt:

![][AllDatesFixed]

U kunt verder verbeteren Hallo *datums* weergeven door te organiseren Hallo datum / tijd-waarden per datum. Dit kan worden gedaan met Hallo Bootstrap [panelen] [ panels] opmaak. Vervang de inhoud Hallo Hallo *weergaven\\Start\\AllDates.cshtml* bestand met de volgende code:

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

Deze code maakt een afzonderlijke `<div class="panel panel-primary">` label voor elke afzonderlijke datum in de lijst Hallo en maakt gebruik van Hallo [gekoppelde lijstgroep] [ linked list group] voor de respectieve koppelingen als voorheen. Hier ziet u welke Hallo mobiele browser lijkt wanneer deze code wordt uitgevoerd:

![][AllDatesFixed2]

Switch toohello bureaublad browser. Opnieuw, houd er rekening mee Hallo consistent uiterlijk.

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a>Hallo SessionsTable weergave verbeteren
In deze sectie maakt u Hallo *SessionsTable* meer mobiele apparaten geschikte weergeven. Deze wijziging is uitgebreider Hallo eerdere wijzigingen.

Tik op Hallo in Hallo mobiele browser **Tag** knop, voert u `asp` in het zoekvak.

![][AllTagsFixedSearchByASP]

Tik op Hallo **ASP.NET** koppeling.

![][SessionsTableTagASP.NET]

Zoals u ziet, is Hallo weergave opgemaakt als een tabel, momenteel ontworpen toobe in Hallo bureaublad browser weergegeven is. Het is echter iets moeilijk tooread op een mobiele browser. toofix deze, open *weergaven\\Start\\SessionsTable.cshtml* en vervang Hallo inhoud van het bestand met de volgende code Hallo:

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

Hallo code doet 3 dingen:

* maakt gebruik van Hallo Bootstrap [aangepaste gekoppelde lijstgroep] [ custom linked list group] tooformat Hallo sessiegegevens verticaal, zodat deze informatie kan worden gelezen op een mobiele browser (met behulp van klassen, zoals lijst-groep-item-tekst)
* van toepassing hello [raster system] [ grid system] toothe lay-out, dus die sessie Hallo-items stroom horizontaal in Hallo bureaublad browser en verticaal in Hallo mobiele browser (met behulp van Hallo col-md-4-klasse)
* maakt gebruik van Hallo [responsief hulpprogramma's] [ responsive utilities] verbergen Hallo sessie labels ziet er in Hallo mobiele browser (met behulp van Hallo verborgen xs klasse)

U kunt ook een titel koppeling toogo toohello respectieve sessie tikken. Hallo in onderstaande afbeelding weerspiegelt Hallo codewijzigingen.

![][FixedSessionsByTag]

Hallo Bootstrap rastersysteem die u automatisch toegepast rangschikt de sessies verticaal in Hallo mobiele browser. U ziet ook Hallo labels worden niet weergegeven. Switch toohello bureaublad browser.

![][SessionsTableFixedTagASP.NETDesktop]

Let op Hallo labels worden nu weergegeven in Hallo bureaublad browser. Bovendien kunt u zien dat Hallo Bootstrap rastersysteem die u toegepast Hallo-items voor sessie in twee kolommen rangschikt. Als u de browser vergroot, ziet u dat Hallo regeling toothree kolommen is gewijzigd.

## <a name="bkmk_improvesessionbycode"></a>Hallo SessionByCode weergave verbeteren
Ten slotte kunt u straks Hallo *SessionByCode* toomake weergeven deze mobiele apparaten geschikte.

Tik op Hallo in Hallo mobiele browser **Tag** knop, voert u `asp` in het zoekvak.

![][AllTagsFixedSearchByASP]

Tik op Hallo **ASP.NET** koppeling. Hallo ASP.NET tag-sessies worden weergegeven.

![][FixedSessionsByTag]

Kies Hallo **bouwen van één pagina toepassing met ASP.NET en AngularJS** koppeling.

![][SessionByCode3-644]

Hallo standaard bureaubladweergave functioneert, maar u kunt Hallo uiterlijk eenvoudig verbeteren met behulp van een aantal onderdelen Bootstrap GUI.

Open *weergaven\\Start\\SessionByCode.cshtml* en vervang Hallo inhoud door Hallo aantekeningen te volgen:

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

nieuwe markup Hallo Bootstrap panelen opmaak tooimprove Hallo mobiele weergave gebruikt. 

Hallo mobiele browser vernieuwen. Hallo geeft volgende afbeelding Hallo codewijzigingen die u zojuist hebt gemaakt:

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a>Inpakken en controleren
Deze zelfstudie leert u hoe ASP.NET MVC 5 toodevelop mobiele apparaten geschikte toouse webtoepassingen. Deze omvatten:

* Een ASP.NET MVC 5 toepassing tooan App Service-web-app implementeren
* Bootstrap toocreate responsief web-indeling gebruiken in uw toepassing MVC 5
* Lay-out, weergaven en gedeeltelijke weergaven vervangen globaal en voor een afzonderlijke weergave
* Indeling bepalen en gedeeltelijke overschrijven afdwingen met behulp van de `RequireConsistentDisplayMode` eigenschap
* Weergaven die zijn gericht op specifieke browsers, zoals Hallo iPhone browser maken
* Bootstrap stijlen in Razor code toepassen

## <a name="see-also"></a>Zie ook
* [9 basisprincipes van responsief ontwerp](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* [Bootstrap][BootstrapSite]
* [Officiële Blog van het Bootstrap][Official Bootstrap Blog]
* [Twitter Bootstrap zelfstudie uit zelfstudie Republiek][Twitter Bootstrap Tutorial from Tutorial Republic]
* [Hallo Bootstrap Playground][hello Bootstrap Playground]
* [W3C aanbeveling mobiele Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]
* [W3C Candidate aanbeveling voor query's voor media][W3C Candidate Recommendation for media queries]

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

