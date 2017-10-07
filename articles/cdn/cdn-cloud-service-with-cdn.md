---
title: een cloudservice van Azure met Azure CDN aaaIntegrate | Microsoft Docs
description: "Meer informatie over hoe toodeploy een cloudservice die fungeert inhoud van een geïntegreerde Azure CDN-eindpunt"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="intro"></a>Een cloudservice integreren met Azure CDN
Een cloudservice kan worden geïntegreerd met Azure CDN, voor de inhoud van Hallo cloudservice-locatie. Deze aanpak geeft u Hallo volgende voordelen:

* Eenvoudig implementeren en bijwerken van installatiekopieën, scripts en stylesheets in mappen van uw cloudservice-project
* Hallo NuGet-pakketten in uw cloudservice, zoals jQuery of Bootstrap versies vervolgens gemakkelijk upgraden
* Beheren van uw webtoepassing en uw CDN-aangeboden inhoud vanaf Hallo dezelfde Visual Studio-interface
* Uniforme implementatiewerkstroom voor uw webtoepassing en de inhoud van uw CDN-geleverd
* ASP.NET bundeling en minification integreren met Azure CDN

## <a name="what-you-will-learn"></a>Wat u leert
In deze zelfstudie leert u hoe:

* [Een Azure CDN-eindpunt integreren met de cloudservice en bedienen van statische inhoud in uw webpagina's van Azure CDN](#deploy)
* [Cache-instellingen voor statische inhoud configureren in uw cloudservice](#caching)
* [Inhoud verzorgen vanaf een domeincontroller acties via Azure CDN](#controller)
* [Dienst gebundeld en inhoud via Azure CDN minified behoud Hallo script foutopsporing ervaring in Visual Studio](#bundling)
* [Terugval uw scripts en CSS configureren wanneer uw Azure CDN offline is](#fallback)

## <a name="what-you-will-build"></a>Wat u bouwt
U implementeert een cloud service-Webrol Hallo standaard-ASP.NET MVC-sjabloon gebruikt, voegt u code tooserve inhoud van een geïntegreerde Azure CDN, zoals een installatiekopie van een domeincontroller actie resultaten en Hallo standaard JavaScript en CSS-bestanden, en ook schrijven code tooconfigure Hallo terugval mechanisme voor bundels geleverd in Hallo gebeurtenis die Hallo CDN is offline.

## <a name="what-you-will-need"></a>Wat u nodig hebt
Deze zelfstudie heeft Hallo volgende vereisten:

* Een actieve [Microsoft Azure-account](/account/)
* Visual Studio 2015 met [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> U moet een Azure-account toocomplete in deze zelfstudie:
> 
> * U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/) -u ontvangt tegoed kunt u tootry uit betaalde Azure-services en zelfs nadat ze allemaal hebt gebruikt kunt u maximaal Hallo account houden en gebruik gratis Azure-services, zoals Websites.
> * U kunt [voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -uw MSDN-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>Een cloudservice implementeren
In deze sectie wordt u Hallo standaard ASP.NET MVC-toepassingssjabloon in Visual Studio 2015 tooa cloud service-Webrol implementeren en vervolgens te integreren met een nieuw CDN-eindpunt. Volg onderstaande Hallo instructies:

1. In Visual Studio 2015, moet u een nieuwe Azure-cloud-service in de menubalk Hallo maken te gaan**bestand > Nieuw > Project > Cloud > Azure Cloud Service**. Een naam geven en klik op **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. Selecteer **ASP.NET-Webrol** en klik op Hallo  **>**  knop. Klik op OK.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. Selecteer **MVC** en klik op **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. Publiceer nu deze Web-rol tooan Azure-cloudservice. Hallo-cloudserviceproject met de rechtermuisknop en selecteer **publiceren**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. Als u nog niet aangemeld bij Microsoft Azure, klikt u op Hallo **account toevoegen...**  vervolgkeuzelijst en klik op Hallo **account toevoegen** menu-item.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. In het Hallo-aanmeldingspagina, zich aanmelden met Hallo Microsoft-account die u gebruikt tooactivate uw Azure-account.
7. Nadat u bent aangemeld, klikt u op **volgende**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. Ervan uitgaande dat u een cloud-service of storage-account niet hebt gemaakt, kunt Visual Studio u beide maken. In Hallo **Cloudservice maken en de Account** dialoogvenster, type Hallo gewenste servicenaam en selecteer Hallo gewenste regio. Klik vervolgens op **Maken**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. In Hallo instellingenpagina publiceren, Hallo-configuratie controleren en klikt u op **publiceren**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > Hallo publicatieproces voor cloudservices kan lang duren. Hallo Web Deploy inschakelen voor alle functies optie kan zorgen dat uw cloudservice veel sneller door snelle (maar tijdelijke) updates tooyour webrollen foutopsporing. Zie voor meer informatie over deze optie [publiceren van een Cloudservice met behulp van hulpprogramma's van Azure Hallo](http://msdn.microsoft.com/library/ff683672.aspx).
   > 
   > 
   
    Wanneer Hallo **Microsoft Azure Activity Log** zien is dat publicatiestatus **voltooid**, maakt u een CDN-eindpunt geïntegreerd met deze cloudservice.
   
   > [!WARNING]
   > Als, Hallo geïmplementeerd cloudservice weergegeven na de publicatie, een foutscherm, is het waarschijnlijk omdat het Hallo-cloudservice die u hebt geïmplementeerd een [Gast OS die geen .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).  U kunt dit probleem door omzeilen [.NET 4.5.2 als een taak starten implementeren](../cloud-services/cloud-services-dotnet-install-dotnet.md).
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>Nieuwe CDN-profielen maken
Een CDN-profiel is een verzameling van CDN-eindpunten.  Elk profiel bevat een of meer CDN-eindpunten.  U kunt desgewenst toouse meerdere profielen tooorganize uw CDN-eindpunten door internetdomein, webtoepassing of andere criteria.

> [!TIP]
> Als u al een CDN-profiel wilt u toouse voor deze zelfstudie hebt, gaat u verder te[een nieuw CDN-eindpunt maken](#create-a-new-cdn-endpoint).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Nieuwe CDN-eindpunten maken
**een nieuw CDN-eindpunt voor uw opslagaccount toocreate**

1. In Hallo [Azure Management Portal](https://portal.azure.com), navigeer tooyour CDN-profiel.  U kunt hebt vastgemaakt toohello dashboard in de vorige stap Hallo.  Als u niet, u kunt vinden door te klikken op **Bladeren**, klikt u vervolgens **CDN-profielen**, en te klikken op Hallo profiel u van plan bent tooadd het eindpunt.
   
    blade Hallo CDN-profiel wordt weergegeven.
   
    ![CDN-profiel][cdn-profile-settings]
2. Klik op Hallo **eindpunt toevoegen** knop.
   
    ![De knop Eindpunt toevoegen][cdn-new-endpoint-button]
   
    Hallo **een eindpunt toevoegen** blade wordt weergegeven.
   
    ![De blade Een eindpunt toevoegen][cdn-add-endpoint]
3. Voer een **naam** voor dit CDN-eindpunt.  Deze naam worden uw resources in de cache op Hallo domein gebruikte tooaccess `<EndpointName>.azureedge.net`.
4. In Hallo **oorsprongtype** vervolgkeuzelijst *Cloudservice*.  
5. In Hallo **de hostnaam van oorsprong** vervolgkeuzelijst, selecteer uw cloudservice.
6. Laat de standaardwaarden voor Hallo **oorsprongpad**, **host-header van oorsprong**, en **Protocol/oorsprong poort**.  U moet ten minste één protocol (HTTP of HTTPS) opgeven.
7. Klik op Hallo **toevoegen** knop toocreate Hallo nieuw eindpunt.
8. Zodra het Hallo-eindpunt is gemaakt, wordt deze weergegeven in een lijst met eindpunten voor Hallo-profiel. Hallo lijstweergave kunt u zien Hallo URL toouse tooaccess in de cache opgeslagen inhoud, evenals Hallo brondomein.
   
    ![CDN-eindpunt][cdn-endpoint-success]
   
   > [!NOTE]
   > Hallo-eindpunt onmiddellijk worden niet beschikbaar voor gebruik.  Hallo registratie toopropagate via Hallo CDN netwerk too90 minuten kan duren. Totdat het Hallo-inhoud is beschikbaar via Hallo CDN, kunnen gebruikers die direct toouse Hallo CDN-domeinnaam proberen statuscode 404 ontvangen.
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a>Test Hallo CDN-eindpunt
Wanneer Hallo publicatiestatus is **voltooid**, open een browservenster en navigeer te**http://<cdnName>*.azureedge.net/Content/bootstrap.css**. In mijn setup is deze URL:

    http://camservice.azureedge.net/Content/bootstrap.css

Dat overeenkomt met toohello oorsprong URL bij Hallo CDN-eindpunt te volgen:

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

Wanneer u navigeert te**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, afhankelijk van uw browser, kunt u zich na vragen aan gebruiker toodownload of open Hallo bootstrap.css die afkomstig zijn van uw gepubliceerde Web-app.

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

U hebt ook toegang tot een openbaar toegankelijke URL zijn op  **http://*&lt;serviceName >*.cloudapp.net/** rechtstreeks vanuit uw CDN-eindpunt. Bijvoorbeeld:

* Een bestand .js van Hallo/script-pad
* Alle inhoud bestanden Hallo/Content pad
* Elke domeincontroller/actie
* Als de queryreeks Hallo is ingeschakeld op uw CDN-eindpunt elke URL's met querytekenreeksen

Met Hallo bovenstaande configuratie, kunt u in feite Hallo volledige in de cloud-service hosten  **http://*&lt;cdnName >*.azureedge.net/**. Als ik te navigeren**http://camservice.azureedge.net/ ** verschijnt Hallo actie resultaat van de startpagina/Index.

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

Dit betekent niet, maar het is altijd een goed idee tooserve een volledige in de cloud-service via Azure CDN. 

Een CDN met statische leveringsoptimalisatie niet per se versnellen levering van dynamische elementen die zijn niet bedoeld voor toobe in de cache opgeslagen of heel vaak worden bijgewerkt omdat Hallo CDN moet pull-een nieuwe versie van Hallo asset van de bronserver Hallo heel vaak. Voor dit scenario kunt u inschakelen [dynamische Site-versnelling](cdn-dynamic-site-acceleration.md) optimalisatie (DSA) op uw CDN-eindpunt dat gebruikmaakt van verschillende technieken toospeed up levering van niet-caching geschikte dynamische activa. 

Als u een site met een combinatie van statische en dynamische inhoud hebt, kunt u kiezen tooserve uw statische inhoud uit CDN met een statische optimalisatie type (zoals algemene webtoepassingen levering) en tooserve dynamische inhoud rechtstreeks vanaf de bronserver Hallo of via een CDN het eindpunt met DSA optimalisatie per geval ingeschakeld. einde toothat, u hebt al gezien hoe afzonderlijke inhoud tooaccess bestanden van Hallo CDN-eindpunt. Ik ziet u hoe tooserve een specifieke domeincontroller actie via een specifieke CDN-eindpunt in dienen uit controller acties via Azure CDN-inhoud.

Hallo alternatief is toodetermine die inhoud tooserve van Azure CDN op basis van geval in uw cloudservice. einde toothat, u hebt al gezien hoe afzonderlijke inhoud tooaccess bestanden van Hallo CDN-eindpunt. Leest u hoe tooserve een specifieke domeincontroller actie via Hallo CDN-eindpunt in [inhoud verzorgen vanaf een domeincontroller acties via Azure CDN](#controller).

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>Cacheopties voor statische bestanden in uw cloudservice configureren
U kunt opgeven hoe u statische inhoud toobe in de cache opgeslagen in de CDN-eindpunt hello wilt met Azure CDN-integratie in uw cloudservice. toodo deze, open *Web.config* van uw rol Web project (bijvoorbeeld WebRole1) en voeg een `<staticContent>` element te`<system.webServer>`. Hallo XML onderstaande configureert Hallo cache tooexpire 3 dagen.  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

Als u dit doet, ziet alle statische bestanden in uw cloudservice Hallo dezelfde regel in uw CDN-cache. Voor gedetailleerde controle over de clientcache-instellingen, voegt u een *Web.config* bestand naar een map en uw instellingen toe te voegen. Bijvoorbeeld, Voeg een *Web.config* bestand toohello *\Content* map en vervang Hallo inhoud Hello XML te volgen:

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

Deze instelling zorgt ervoor dat alle statische bestanden van Hallo *\Content* map toobe 15 dagen in de cache opgeslagen.

Voor meer informatie over het tooconfigure hello `<clientCache>` element, Zie [clientcache &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).

In [inhoud verzorgen vanaf een domeincontroller acties via Azure CDN](#controller), ook leest u hoe u de cache-instellingen voor de controller actie resultaten in Hallo CDN cache kunt configureren.

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>Inhoud verzorgen vanaf een domeincontroller acties via Azure CDN
Wanneer u een cloud service-Webrol met Azure CDN integreert, is relatief gemakkelijk tooserve inhoud van de domeincontroller acties via hello Azure CDN. Anders dan voor uw cloud service rechtstreeks via Azure CDN (uitgelegd hierboven) [Maarten Balliauw](https://twitter.com/maartenballiauw) laat u zien hoe toodo deze met een leuk MemeGenerator controller in [korte wachttijden op Hallo web Hello Azure CDN ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN). Ik zal gewoon reproduceer het hier.

Stel dat in uw cloudservice die u wilt toogenerate memes op basis van de installatiekopie van een jonge Chuck Norris (foto's door [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) zoals deze:

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

U hebt een eenvoudige `Index` hello meme actie waarmee klanten Hallo toospecify Hallo items in Hallo-installatiekopie wordt gegenereerd zodra ze boeken toohello actie. Aangezien het Chuck Norris, u mag verwachten deze pagina toobecome sterk populaire globaal. Dit is een goed voorbeeld van voor de semi dynamische inhoud met Azure CDN.

Stappen Hallo hierboven toosetup deze controller actie:

1. In Hallo *\Controllers* map, maak een nieuw .cs bestand aangeroepen *MemeGeneratorController.cs* en vervang Hallo inhoud met Hallo de volgende code. Ervoor tooreplace Hallo gemarkeerd deel worden met de naam van uw CDN.  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. Met de rechtermuisknop in de standaard Hallo `Index()` actie en selecteer **weergave toevoegen**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. Accepteer de onderstaande Hallo-instellingen en klik op **toevoegen**.
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. Open Hallo nieuwe *Views\MemeGenerator\Index.cshtml* en vervang Hallo inhoud door Hallo eenvoudig HTML-code voor het indienen van items hello te volgen:
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. Hallo-cloudservice opnieuw publiceren en te navigeren**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** in uw browser.

Wanneer u Hallo formulierwaarden te verzenden`/MemeGenerator/Index`, Hallo `Index_Post` actiemethode retourneert een koppeling toohello `Show` actiemethode met Hallo respectieve invoer-ID. Wanneer u Hallo koppeling klikt, kunt u Hallo na code bereiken:  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

Als uw lokale foutopsporing is gekoppeld, krijgt u Hallo reguliere foutopsporing ervaring met een lokale omleiding. Als deze wordt uitgevoerd in de cloudservice hello, wordt naar het omleiden:

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

Dit komt overeen met toohello oorsprong URL bij uw CDN-eindpunt te volgen:

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


Vervolgens kunt u Hallo `OutputCacheAttribute` -kenmerk op Hallo `Generate` methode-toospecify hoe Hallo actie resultaat moet worden in de cache, die Azure CDN wordt geacht. Hallo-code hieronder opgeven voor de vervaldatum van een cache van 1 uur (3600 seconden).

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

Evenzo kan u fungeren inhoud van elke domeincontroller actie in uw cloudservice via uw Azure CDN, met Hallo gewenst cache-instelling.

In de volgende sectie hello leest u hoe tooserve Hallo gebundeld en scripts en CSS via Azure CDN minified.

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>ASP.NET bundeling en minification integreren met Azure CDN
Scripts en CSS stylesheets niet vaak worden gewijzigd en voornaamste kandidaten zijn voor hello Azure CDN-cache. Levering Hallo gehele Webrol via uw Azure CDN is de eenvoudigste manier toointegrate Hallo bundeling en minification met Azure CDN. Echter, als u niet toodo dit wilt, leest u hoe toodo het behoud van Hallo gewenst ontwikkelaars ervaring voor ASP.NET bundeling en minification, zoals:

* Goede foutopsporing modus ervaring
* Gestroomlijnde implementatie
* Onmiddellijke updates tooclients voor script/CSS versie-upgrades
* Terugval mechanisme als uw CDN-eindpunt is mislukt
* Codewijzigingen minimaliseren

In Hallo **WebRole1** project dat u hebt gemaakt in [integreren van een Azure CDN-eindpunt met uw Azure-website en bedienen van statische inhoud in uw webpagina's van Azure CDN](#deploy)Open *App_Start\ BundleConfig.cs* en eens kijken Hallo `bundles.Add()` methodeaanroepen.

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

Hallo eerst `bundles.Add()` instructie voegt u een script bundel op de virtuele map Hallo `~/bundles/jquery`. Open vervolgens *Views\Shared\_Layout.cshtml* toosee hoe Hallo-scriptcode bundel wordt weergegeven. U moet kunnen toofind Hallo Razor coderegel te volgen:

    @Scripts.Render("~/bundles/jquery")

Wanneer deze Razor code wordt uitgevoerd in Azure-Webrol hello, krijgt het een `<script>` tag voor Hallo bundel vergelijkbare toohello volgende script:

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

Echter, als deze wordt uitgevoerd in Visual Studio door te typen `F5`, geeft deze afzonderlijk elke scriptbestand in Hallo bundel weer (in Hallo geval bovenstaande slechts één scriptbestand is in de bundel Hallo):

    <script src="/Scripts/jquery-1.10.2.js"></script>

Hiermee kunt u toodebug Hallo JavaScript-code in uw ontwikkelomgeving terwijl gelijktijdige clientverbindingen (bundeling) verminderen en het verbeteren van bestand prestaties (minification) in de productieomgeving downloaden. Het is een uitstekende functie toopreserve met Azure CDN-integratie. Bovendien omdat Hallo gerenderd bundel al een automatisch gegenereerde versietekenreeks bevat, gewenste tooreplicate die functionaliteit Hallo dus wanneer u uw jQuery-versie via NuGet, werken deze kan worden bijgewerkt op Hallo client zodra mogelijk is.

Hallo stappen hieronder toointegration ASP.NET bundeling en minification met uw CDN-eindpunt.

1. Terug in de *App_Start\BundleConfig.cs*, Hallo wijzigen `bundles.Add()` methoden toouse een andere [bundel constructor](http://msdn.microsoft.com/library/jj646464.aspx), die een CDN-adres. toodo deze, Hallo vervangen `RegisterBundles` methodedefinitie Hello code te volgen:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Ervoor tooreplace worden `<yourCDNName>` met Hallo-naam van uw Azure CDN.
   
    In een gewone woorden die u instelt `bundles.UseCdn = true` en een zorgvuldig ontworpen CDN URL tooeach bundel toegevoegd. Bijvoorbeeld, Hallo eerste constructor Hallo code:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    is hetzelfde als Hallo:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    Deze constructor vertelt ASP.NET bundeling en minification toorender afzonderlijke scriptbestanden wanneer foutopsporing lokaal, maar gebruik Hallo opgegeven CDN adres tooaccess Hallo script in kwestie. Let echter op twee belangrijke kenmerken met deze zorgvuldig ontworpen CDN-URL:
   
   * Hallo oorsprong voor dit CDN-URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, die eigenlijk Hallo virtuele map van Hallo script bundel in uw cloudservice is.
   * Aangezien u CDN constructor gebruikt, bevat Hallo CDN scriptcode voor Hallo-bundel niet langer versietekenreeks Hallo automatisch gegenereerd in Hallo URL weergegeven. Elke keer Hallo script bundel wordt gewijzigd tooforce een cache op uw Azure CDN gemist, moet u handmatig een unieke versietekenreeks genereren. AT Hallo dezelfde tijd, deze unieke versietekenreeks constante via Hallo levensduur van Hallo implementatie toomaximize cachetreffers op uw Azure CDN moet blijven nadat Hallo bundel is geïmplementeerd.
   * Hallo queryreeks v = < W.X.Y.Z > worden van *Properties\AssemblyInfo.cs* in uw webproject rol. U kunt een werkstroom voor de implementatie met Hallo assembly-versie wordt verhoogd telkens wanneer u tooAzure publiceren hebben. Of u kunt alleen wijzigen *Properties\AssemblyInfo.cs* in uw project tooautomatically verhoging Hallo versietekenreeks telkens wanneer u bouwt, met behulp van Hallo jokerteken ' *'. Bijvoorbeeld:
     
        [assembly: AssemblyVersion("1.0.0.*")]
     
     Andere strategie-toostreamline genereren van een unieke tekenreeks voor Hallo levensduur van een implementatie wordt hier werken.
2. Opnieuw publiceren Hallo cloud-service en access Hallo startpagina.
3. Weergave hello HTML-code voor het Hallo-pagina. U moet kunnen toosee Hallo CDN URL weergegeven, met een unieke versietekenreeks telkens wanneer u wijzigingen tooyour cloudservice opnieuw publiceren. Bijvoorbeeld:  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. Foutopsporing in Visual Studio Hallo cloudservice in Visual Studio door te typen `F5`.,
5. Weergave hello HTML-code voor het Hallo-pagina. U ziet nog steeds elke scriptbestand afzonderlijk weergegeven zodat u kunt een consistente foutopsporing optreden in Visual Studio hebben.  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a>Terugval mechanisme voor CDN-URL 's
Als uw Azure CDN-eindpunt voor een of andere reden mislukt, wilt u uw webpagina toobe slimme voldoende tooaccess uw webserver oorsprong als terugvaloptie voor het laden van JavaScript of Bootstrap Hallo. Het is ernstig genoeg toolose installatiekopieën op uw website vanwege tooCDN niet beschikbaar zijn, maar veel ernstiger toolose cruciaal pagina functionaliteit van uw scripts en stylesheets.

Hallo [bundel](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) klasse bevat een eigenschap genaamd [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) waarmee u tooconfigure Hallo terugval mechanisme voor CDN-fout. toouse deze eigenschap, Hallo stappen hieronder:

1. Open in uw webrolproject *App_Start\BundleConfig.cs*, waarin u een CDN-URL toegevoegd in elk [bundel constructor](http://msdn.microsoft.com/library/jj646464.aspx), en zorg Hallo volgende gemarkeerd tooadd terugval mechanisme toohello wordt gewijzigd standaard-pakketten:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Wanneer `CdnFallbackExpression` is niet null script is opgenomen in Hallo HTML tootest of Hallo bundel is geladen en als dat niet Hallo bundel rechtstreeks vanuit Hallo oorsprong webserver openen. Deze eigenschap moet toobe set tooa JavaScript-expressie die wordt gecontroleerd of de respectieve CDN bundel Hallo correct wordt geladen. Hallo expressie nodig tootest elke bundel verschilt volgens toohello inhoud. Voor Hallo standaard bundels bovenstaande:
   
   * `window.jquery`is gedefinieerd in jquery-{version} .js
   * `$.validator`is gedefinieerd in jquery.validate.js
   * `window.Modernizr`is gedefinieerd in modernizer-{version} .js
   * `$.fn.modal`is gedefinieerd in bootstrap.js
     
     U mogelijk opgevallen dat ik CdnFallbackExpression niet is ingesteld voor Hallo `~/Cointent/css` bundel. Dit is omdat er momenteel een [fout in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) die injects een `<script>` tag voor terugval CSS in plaats van Hallo verwacht Hallo `<link>` label.
     
     Er is echter een goede [stijl bundel terugval](https://github.com/EmberConsultingGroup/StyleBundleFallback) die worden aangeboden door [Ember advies groep](https://github.com/EmberConsultingGroup).
2. toouse hello oplossing voor CSS en maak een nieuw .cs-bestand in uw webrolproject *App_Start* map met de naam *StyleBundleExtensions.cs*, en vervang de inhoud ervan Hello [code uit GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).
3. In *App_Start\StyleFundleExtensions.cs*, Hallo naamruimte tooyour Webrol van naam (bijvoorbeeld **WebRole1**).
4. Ga terug te`App_Start\BundleConfig.cs` en Hallo laatste wijzigen `bundles.Add` instructie Hello gemarkeerde code te volgen:  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    Deze nieuwe uitbreidingsmethode Hallo gebruikt dezelfde idee tooinject script in Hallo HTML toocheck Hallo DOM voor Hallo een overeenkomende klassenaam, regelnaam en regel waarde die is gedefinieerd in Hallo CSS-bundel en valt back toohello oorsprong webserver als deze uitvalt toofind Hallo overeen.
5. Hallo cloud-service opnieuw en toegang Hallo-startpagina publiceren.
6. Weergave hello HTML-code voor het Hallo-pagina. U moet de geïnjecteerde scripts vergelijkbare toohello volgende vinden:    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    Ingevoegd script voor Hallo CSS-bundel bevat nog steeds onjuiste restant Hallo van Hallo `CdnFallbackExpression` eigenschap in Hallo regel:

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    Maar omdat het eerste deel van de Hallo Hallo || expressie wordt altijd waar retourneren, (op Hallo regel boven die), Hallo document.write() functie wordt nooit uitgevoerd.

## <a name="more-information"></a>Meer informatie
* [Overzicht van hello Azure Content Delivery Network (CDN)](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [Azure CDN gebruiken](cdn-create-new-endpoint.md)
* [ASP.NET bundeling en Minification](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
