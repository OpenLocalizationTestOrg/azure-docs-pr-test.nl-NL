---
title: aaaTroubleshoot een web-app in Azure App Service met behulp van Visual Studio
description: Meer informatie over hoe een Azure-web-app met behulp van foutopsporing op afstand tootroubleshoot, tracering en logboekregistratie hulpprogramma's die zijn ingebouwd in tooVisual Studio 2013.
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: 
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: 8e3a8a58293f2ebcdc131fbf2534f8ff99b26730
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a>Een web-app in Azure App Service met behulp van Visual Studio oplossen
## <a name="overview"></a>Overzicht
Deze zelfstudie laat zien hoe toouse Visual Studio-hulpprogramma's waarmee fouten opsporen in een web-app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), door te voeren in [foutopsporingsmodus](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) op afstand of door toepassingslogboeken en webserverlogboeken te bekijken.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

U leert het volgende:

* Welke Azure-web-app-beheerfuncties zijn beschikbaar in Visual Studio.
* Hoe toouse Visual Studio afstand toomake snelle wijzigingen in een externe web-app weergeven.
* Hoe worden de foutopsporingsmodus toorun op afstand tijdens een project wordt uitgevoerd in Azure, voor een web-app en een webtaak.
* Hoe toocreate toepassing traceerlogboeken en ze weergeven tijdens het Hallo-toepassing is ze worden gemaakt.
* Hoe tooview webserverlogboeken, met inbegrip van gedetailleerde foutberichten en tracering van mislukte aanvragen.
* Hoe toosend diagnostische logboeken tooan Azure Storage-account en ze er weergeven.

Als u Visual Studio Ultimate hebt, kunt u ook gebruiken [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) voor foutopsporing. IntelliTrace wordt niet behandeld in deze zelfstudie.

## <a name="prerequisites"></a>Vereisten
Deze zelfstudie werkt met Hallo ontwikkelomgeving webproject en Azure-web-app die u hebt ingesteld in [aan de slag met Azure en ASP.NET][GetStarted]. Voor Hallo webtaken secties, moet u Hallo-toepassing die u maakt in [aan de slag met Azure WebJobs SDK Hallo][GetStartedWJ].

Hallo code voorbeelden in deze zelfstudie wordt weergegeven voor een C# MVC-webtoepassing, maar de procedures voor probleemoplossing Hallo zijn Hallo dezelfde voor Visual Basic en Web Forms-toepassingen.

Hallo-zelfstudie wordt ervan uitgegaan dat u Visual Studio 2015 of 2013. Als u Visual Studio 2013, Hallo WebJobs functies vereisen [Update 4](http://go.microsoft.com/fwlink/?LinkID=510314) of hoger.

streaminglogboeken Hello functie werkt alleen voor toepassingen die zijn gericht op .NET Framework 4 of hoger.

## <a name="sitemanagement"></a>Web-app-configuratie en beheer
Visual Studio biedt toegang tot tooa subset van Hallo web-app-beheerfuncties en configuratie-instellingen die beschikbaar zijn in Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). In deze sectie ziet u wat er beschikbaar is via **Server Explorer**. toosee hello nieuwste integratie van Azure functies uitproberen **Cloud Explorer** ook. U kunt zowel windows openen vanuit Hallo **weergave** menu.

1. Als u nog niet hebt aangemeld in tooAzure in Visual Studio, klikt u op Hallo **verbinding tooAzure** knop in **Server Explorer**.

    Een alternatief is tooinstall een beheercertificaat dat hiermee toegang tooyour-account tot. U kunt eventueel tooinstall een certificaat met de rechtermuisknop op Hallo **Azure** knooppunt in **Server Explorer**, en klik vervolgens op **beheren en Filter abonnementen** in het contextmenu Hallo. In Hallo **Azure-abonnementen beheren** dialoogvenster vak, klikt u op Hallo **certificaten** tabblad en klik vervolgens op **importeren**. Hallo richtingen toodownload volgen en een abonnementsbestand vervolgens importeren (ook wel een *.publishsettings* bestand) voor uw Azure-account.

   > [!NOTE]
   > Als u een abonnementsbestand hebt gedownload, tooa map buiten uw adreslijsten source code (bijvoorbeeld in de map Downloads Hallo) opslaan en verwijderen wanneer Hallo importeren is voltooid. Een kwaadwillende gebruiker die toegang tot toohello abonnementsbestand krijgt kunt bewerken, maken en verwijderen van uw Azure-services.
   >
   >

    Zie voor meer informatie over het verbinden van resources tooAzure vanuit Visual Studio [Accounts beheren, abonnementen en beheerdersrollen](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).
2. In **Server Explorer**, vouw **Azure** en vouw **App Service**.
3. Vouw Hallo bronnengroep met Hallo web-app die u hebt gemaakt in [aan de slag met Azure en ASP.NET][GetStarted], en vervolgens met de rechtermuisknop op Hallo web-app-knooppunt en klik op **weergave-instellingen**.

    ![Instellingen weergeven in Server Explorer](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    Hallo **Azure-Web-App** tabblad wordt weergegeven en kunt u zien er Hallo web app management- en configuratietaken die beschikbaar in Visual Studio zijn.

    ![Azure-Web-App-venster](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    In deze zelfstudie hebt u Hallo logboekregistratie en tracering vervolgkeuzelijsten gebruiken. U zult ook gebruiken voor foutopsporing op afstand, maar gebruikt u een andere methode tooenable deze.

    Zie voor meer informatie over de App-instellingen en verbindingsreeksen vakken Hallo in dit venster [Azure Web Apps: tekenreeksen van toepassingen en verbindingsreeksen](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

    Als u wilt dat tooperform een beheertaak voor web-app die in dit venster kan niet worden uitgevoerd, klikt u op **openen in de beheerportal** tooopen een browser venster toohello Azure-portal.

## <a name="remoteview"></a>Toegang tot web-app-bestanden in Server Explorer
U doorgaans een webproject Hello implementeert `customErrors` te markeren in Web.config-bestandsset Hallo`On` of `RemoteOnly`, wat betekent dat er geen een handig foutbericht als er iets mis gaat. Voor veel fouten is alle dat u een pagina zoals Hallo toepassingsgroepen te volgen.

**Serverfout in '/' toepassing:**

![Onnuttige foutpagina](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

**Er is een fout opgetreden:**

![Onnuttige foutpagina](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

**Hallo website Hallo pagina kan niet worden weergegeven**

![Onnuttige foutpagina](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

Vaak Hallo gemakkelijkste manier toofind Hallo Hallo-fout is te wijten aan tooenable gedetailleerde foutberichten die eerste van de voorgaande schermafbeeldingen Hallo Hallo wordt uitgelegd hoe toodo. Die vereist dat een wijziging in Hallo geïmplementeerd Web.config-bestand. Kan u Hallo bewerken *Web.config* bestand in het Hallo-project en de implementatie opnieuw Hallo project of maak een [Web.config-transformatie](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) en implementeren van een foutopsporingsversie, maar er is een snellere manier: in **oplossing Explorer** u rechtstreeks kunt bekijken en bewerken van bestanden in Hallo remote web-app met behulp van Hallo *externe weergave* functie.

1. In **Server Explorer**, vouw **Azure**, vouw **App Service**, vouwt u de resourcegroep Hallo die zich in uw web-app uit en vouw vervolgens Hallo knooppunt voor uw web-app.

    Ziet u knooppunten waarmee u de inhoudsbestanden en logboekbestanden toegang toohello van web-app.
2. Vouw Hallo **bestanden** knooppunt en dubbelklikt u op Hallo *Web.config* bestand.

    ![Open Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    Visual Studio Hallo Web.config-bestand wordt geopend vanuit Hallo remote web-app en toont [afstand] volgende toohello-bestandsnaam in de titelbalk Hallo.
3. Hallo volgende regel toohello toevoegen `system.web` element:

    `<customErrors mode="Off"></customErrors>`

    ![Web.config bewerken](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. Vernieuw Hallo browser dat Hallo onnuttige foutbericht wordt weergegeven en nu het ophalen van een gedetailleerd foutbericht, zoals Hallo voorbeeld te volgen:

    ![Gedetailleerd foutbericht](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    (Hallo fout weergegeven is gemaakt door het Hallo-regel te in rood weergegeven toe te voegen*Views\Home\Index.cshtml*.)

Bewerking Hallo Web.config-bestand is slechts één voorbeeld van scenario's tooread en bewerk bestanden op uw Azure-web-app maken in welke mogelijkheid Hallo probleemoplossing eenvoudiger.

## <a name="remotedebug"></a>Externe foutopsporing web-apps
Als gedetailleerde fout het Hallo-bericht niet voldoende informatie geven, en u kunt geen lokaal Hallo fout opnieuw maken, is een andere manier tootroubleshoot toorun in de foutopsporingsmodus op afstand. U kunt onderbrekingspunten instellen, geheugen rechtstreeks te manipuleren, analyseer code en zelfs Hallo codepad wijzigen.

Foutopsporing op afstand werkt niet in de Express-edities van Visual Studio.

Deze sectie wordt beschreven hoe extern met Hallo toodebug project maken in [aan de slag met Azure en ASP.NET][GetStarted].

1. Open Hallo-webproject dat u hebt gemaakt in [aan de slag met Azure en ASP.NET][GetStarted].
2. Open *Controllers\HomeController.cs*.
3. Hallo verwijderen `About()` methode en insert Hallo volgende code in plaats daarvan.

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "hello current time is " + currentTime;
            return View();
        }
4. [Stel een onderbrekingspunt in](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) op Hallo `ViewBag.Message` regel.
5. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en klik op **publiceren**.
6. In Hallo **profiel** vervolgkeuzelijst, selecteer Hallo dezelfde profiel dat u gebruikt in [aan de slag met Azure en ASP.NET][GetStarted].
7. Klik op Hallo **instellingen** tabblad en wijzig **configuratie** te**Debug**, en klik vervolgens op **publiceren**.

    ![In de foutopsporingsmodus publiceren](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. Na de implementatie openen is voltooid en de browser toohello Azure-URL van uw web-app sluiten Hallo-browser
9. In **Server Explorer**, met de rechtermuisknop op uw web-app en klik vervolgens op **foutopsporingsprogramma koppelen**.

    ![Foutopsporingsprogramma koppelen](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    Hallo browser geopend automatisch tooyour startpagina in Azure wordt uitgevoerd. U mogelijk toowait 20 seconden of dus terwijl Azure Hallo-server voor het opsporen van ingesteld. Deze vertraging gebeurt Hallo alleen eerste keer dat u in de foutopsporingsmodus op een web-app uitvoert. Daaropvolgende tijden binnen Hallo komende 48 uur wanneer u foutopsporing er opnieuw start niet een vertraging optreden.

    **Opmerking:** als er problemen Hallo foutopsporingsprogramma wordt gestart, probeert u het toodo deze met behulp van **Cloud Explorer** in plaats van **Server Explorer**.
10. Klik op **over** in Hallo-menu.

     Visual Studio op Hallo onderbrekingspunt gestopt en Hallo code wordt uitgevoerd in Azure, niet op uw lokale computer.
11. Beweeg de muisaanwijzer over Hallo `currentTime` variabele toosee Hallo tijd-waarde.

     ![De variabele in de foutopsporingsmodus in Azure wordt uitgevoerd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     Hallo-tijd u ziet is tijd hello Azure-server die mogelijk in een andere tijdzone dan uw lokale computer.
12. Voer een nieuwe waarde voor Hallo `currentTime` variabele, zoals 'Wordt nu uitgevoerd in Azure'.
13. Druk op F5 toocontinue uitgevoerd.

     Hallo over pagina uitgevoerd in Azure Hallo nieuwe waarde weergegeven die u hebt ingevoerd in Hallo currentTime variabele.

     ![Over de pagina met de nieuwe waarde](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <a name="remotedebugwj"></a>Externe foutopsporing WebJobs
Deze sectie ziet u hoe toodebug extern met Hallo-project en de web-app maken [aan de slag met Azure WebJobs SDK Hallo](websites-dotnet-webjobs-sdk.md).

Hallo-functies weergegeven in deze sectie zijn alleen beschikbaar in Visual Studio 2013 met Update 4 of hoger.

Foutopsporing op afstand werkt alleen met doorlopende webtaken. Geplande en on-demand WebJobs foutopsporing worden niet ondersteund.

1. Open Hallo-webproject dat u hebt gemaakt in [aan de slag met Azure WebJobs SDK Hallo][GetStartedWJ].
2. Open in Hallo ContosoAdsWebJob project *Functions.cs*.
3. [Stel een onderbrekingspunt in](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) op de eerste instructie in Hallo Hallo `GnerateThumbnail` methode.

    ![Onderbrekingspunt instellen](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. In **Solution Explorer**, met de rechtermuisknop op het Hallo-webproject (geen Hallo webtaak project) en klik op **publiceren**.
5. In Hallo **profiel** vervolgkeuzelijst, selecteer Hallo dezelfde profiel dat u gebruikt in [aan de slag met Azure WebJobs SDK Hallo](websites-dotnet-webjobs-sdk.md).
6. Klik op Hallo **instellingen** tabblad en wijzig **configuratie** te**Debug**, en klik vervolgens op **publiceren**.

    Uw browser worden geopend toohello Azure-URL van uw web-app en Visual Studio implementeert Hallo web- en webtaak projecten.
7. In **Server Explorer** Vouw **Azure > App Service > uw resourcegroep > uw web-app > WebJobs > doorlopend**, en klik vervolgens met de rechtermuisknop op **ContosoAdsWebJob**.
8. Klik op **foutopsporingsprogramma koppelen**.

    ![Foutopsporingsprogramma koppelen](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    Hallo browser geopend automatisch tooyour startpagina in Azure wordt uitgevoerd. U mogelijk toowait 20 seconden of dus terwijl Azure Hallo-server voor het opsporen van ingesteld. Deze vertraging gebeurt Hallo alleen eerste keer dat u in de foutopsporingsmodus op een web-app uitvoert. Hallo volgende keer dat u er Hallo foutopsporingsprogramma koppelen niet een vertraging als u dit binnen 48 uur doet.
9. In de webbrowser die is geopend toohello Contoso Ads-startpagina Hallo, maak een nieuw ad.

    Maken van een ad zorgt ervoor dat een wachtrij bericht toobe gemaakt, die worden opgehaald door Hallo webtaak en verwerkt. Hallo-code wordt de uw onderbrekingspunt uitvoeren wanneer Hallo WebJobs SDK Hallo functie tooprocess Hallo-bericht van wachtrij aanroept.
10. Wanneer het Hallo-foutopsporingsprogramma onderbreekt op uw onderbrekingspunt, kunt u onderzoeken en variabelewaarden wijzigen terwijl Hallo programma Hallo cloud wordt uitgevoerd. Volgende illustratie Hallo debugger wordt in Hallo Hallo inhoud van Hallo blobInfo-object dat is doorgegeven toohello GenerateThumbnail methode weergegeven.

     ![blobInfo-object in het foutopsporingsprogramma](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. Druk op F5 toocontinue uitgevoerd.

     Hallo GenerateThumbnail methode is voltooid Hallo miniatuur maken.
12. In de browser Hallo ziet vernieuwen Hallo indexpagina en u Hallo miniatuur.
13. In Visual Studio, drukt u op SHIFT + F5 toostop foutopsporing.
14. In **Server Explorer**, met de rechtermuisknop op Hallo ContosoAdsWebJob knooppunt en klik op **weergave Dashboard**.
15. Meld u aan met uw Azure-referenties en klik vervolgens op Hallo webtaak naam toogo toohello pagina voor uw webtaak.

     ![Klik op ContosoAdsWebJob](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     Hallo Dashboard ziet u dat Hallo GenerateThumbnail functie onlangs is uitgevoerd.

     (wanneer u op Hallo **weergave Dashboard**, u hebt geen toosign in en Hallo browser gaat rechtstreeks toohello pagina voor uw webtaak.)
16. Klik op Hallo functie naam toosee details over Hallo functie wordt uitgevoerd.

     ![Details van functie](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

Als de functie [Logboeken geschreven](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), kunt u op **ToggleOutput** toosee ze.

## <a name="notes-about-remote-debugging"></a>Opmerkingen over foutopsporing op afstand
* Uitgevoerd in de foutopsporingsmodus in productie wordt niet aanbevolen. Als uw web-app voor productie is toomultiple server-exemplaren niet worden uitgebreid, foutopsporing wordt voorkomen dat Hallo-webserver niet reageert tooother aanvragen. Als u dit doet meerdere web server-exemplaren, wanneer u koppelt toohello foutopsporingsprogramma krijgt u een willekeurig exemplaar, en u hebt geen tooensure manier verdere browser aanvragen gaat toothat exemplaar. Bovendien kunnen doorgaans een foutopsporing build tooproduction niet implementeren, en optimalisatie van de compiler voor release builds het onmogelijk tooshow wat er gebeurt per regel in de broncode. Voor het oplossen van problemen, is de beste bron toepassing tracering en web server-Logboeken.
* Lange wordt gestopt bij onderbrekingspunten wanneer externe voorkomen foutopsporing. Azure beschouwt een proces dat is langer dan een paar minuten als een niet-reagerende proces gestopt en wordt afgesloten.
* Terwijl u fouten opspoort, verzendt Hallo server gegevens tooVisual Studio bandbreedte kosten kan beïnvloeden. Zie voor meer informatie over bandbreedte tarieven [prijzen van Azure](https://azure.microsoft.com/pricing/calculator/).
* Zorg ervoor dat Hallo `debug` kenmerk Hallo `compilation` -element in Hallo *Web.config* bestand tootrue is ingesteld. Wanneer u een configuratie van de build foutopsporing publiceert, is dit tootrue standaard ingesteld.

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* Als u dat foutopsporingsprogramma Hallo won't stap in de code vindt die u toodebug wilt, hebt u mogelijk toochange Hallo alleen mijn Code instelling.  Zie voor meer informatie [beperken stap voor stap tooJust mijn Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).
* Wanneer u externe foutopsporingsfunctie Hallo inschakelen en na 48 uur Hallo functie automatisch wordt uitgeschakeld, wordt een timer op Hallo server starten. Deze limiet 48 uur wordt gedaan voor beveiliging en prestaties. U kunt eenvoudig hello functie weer inschakelen als vaak is als u wilt. U wordt aangeraden deze uitgeschakeld wanneer u niet actief foutopsporing.
* Hallo foutopsporingsprogramma tooany proces, niet alleen Hallo web app proces (w3wp.exe) kunt u handmatig koppelen. Zie voor meer informatie over hoe toouse foutopsporingsmodus in Visual Studio, [foutopsporing in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).

## <a name="logsoverview"></a>Overzicht van diagnostische logboeken
Een ASP.NET-toepassing die wordt uitgevoerd in een Azure-web-app kunt maken Hallo soorten logboeken te volgen:

* **Logboeken voor tracering van toepassing**<br/>
  Hallo toepassing maakt deze logboeken door het aanroepen van methoden van Hallo [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) klasse.
* **Web server-Logboeken**<br/>
  Hallo-webserver maakt een logboekvermelding voor elke HTTP-aanvraag toohello web-app.
* **Gedetailleerde foutenlogboeken voor bericht**<br/>
  Hallo-webserver maakt een HTML-pagina met aanvullende informatie voor mislukte HTTP-aanvragen (die in statuscode 400 of hoger resulteren).
* **Logboeken voor tracering van aanvraag is mislukt**<br/>
  Hallo-webserver maakt een XML-bestand met gedetailleerde traceringsgegevens voor mislukte HTTP-aanvragen. Hallo-webserver biedt ook een XSL-bestand tooformat Hallo XML in een browser.

Logboekregistratie is van invloed op web-app-prestaties zodat Azure u biedt de mogelijkheid tooenable Hallo- of uitschakelen van elk type logboek indien nodig. Toepassingslogboeken, kunt u opgeven dat alleen de logboeken boven een bepaalde mate van ernst worden geschreven. Wanneer u maakt een nieuwe web-app standaard alle logboekregistratie is uitgeschakeld.

Logboeken toofiles zijn geschreven in een *logboekbestanden* map in het bestandssysteem Hallo van uw web-app en zijn toegankelijk via FTP. Webserverlogboeken en toepassingslogboeken kunnen ook worden geschreven tooan Azure Storage-account. U kunt een groter volume aan logboeken in een opslagaccount dan mogelijk in het bestandssysteem Hallo behouden. Wanneer u het bestandssysteem Hallo bent u beperkt tooa maximaal 100 MB van Logboeken. (Alleen voor het bewaren van de korte termijn zijn bestand het systeemlogboek in Logboeken. Azure verwijdert oude logboek bestanden toomake ruimte voor nieuwe nadat Hallo limiet is bereikt.)  

## <a name="apptracelogs"></a>Maken en toepassing traceringslogboeken weergeven
In deze sectie, doet u Hallo volgende taken:

* Voeg tracering instructies toohello webproject dat u hebt gemaakt in [aan de slag met Azure en ASP.NET][GetStarted].
* Hallo logboeken bekijken wanneer u Hallo-project lokaal uitvoeren.
* Hallo logboeken bekijken nadat ze zijn gegenereerd door Hallo-toepassing in Azure wordt uitgevoerd.

Zie voor meer informatie over hoe toocreate in WebJobs toepassingslogboeken [hoe toowork met het gebruik van Azure queue storage Hallo WebJobs SDK - hoe toowrite registreert](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs). Hallo volgende instructies voor het weergeven van Logboeken en hoe ze zijn opgeslagen in Azure beheren ook van toepassing tooapplication logboeken die zijn gemaakt door WebJobs.

### <a name="add-tracing-statements-toohello-application"></a>Tracering instructies toohello toepassing toevoegen
1. Open *Controllers\HomeController.cs*, en vervang Hallo `Index`, `About`, en `Contact` methoden met Hallo volgende code in volgorde tooadd `Trace` instructies en een `using` instructie voor `System.Diagnostics`:

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template toojump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying hello Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on hello About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on hello Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. Voeg een `using System.Diagnostics;` instructie toohello boven in Hallo-bestand.

### <a name="view-hello-tracing-output-locally"></a>Weergave Hallo tracering lokaal uitvoeren
1. Druk op F5 toorun Hallo toepassing in de foutopsporingsmodus.

    Hallo standaard traceringslistener schrijft alle trace-uitvoer toohello **uitvoer** venster, samen met andere foutopsporingsuitvoer. Hallo volgende afbeelding ziet u uitvoer van Hallo Hallo trace-instructies die u toohello toegevoegd `Index` methode.

    ![Tracering in het venster Foutopsporing](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    Hallo stappen laten zien hoe tooview trace uitvoer in een webpagina zonder compileren in de foutopsporingsmodus.
2. Open Hallo toepassing Web.config-bestand (hello een zich in de projectmap Hallo) en voeg toe een `<system.diagnostics>` element bij de Hallo bestandseindemarkering Hallo vlak voordat de afsluiting Hallo `</configuration>` element:

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    Hallo `WebPageTraceListener` Hiermee kunt u weergeven door te bladeren uitvoer van traceringen`/trace.axd`.
3. Voeg een <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace-element</a> onder `<system.web>` in Hallo Web.config-bestand, zoals Hallo voorbeeld te volgen:

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. Druk op CTRL + F5 toorun Hallo toepassing.
5. In de adresbalk Hallo van Hallo browservenster toevoegen *trace.axd* toohello-URL, en druk op Enter (Hallo URL zijn vergelijkbaar toohttp://localhost:53370/trace.axd).
6. Op Hallo **toepassing Trace** pagina, klikt u op **Details weergeven** op Hallo eerste regel (geen hello BrowserLink regel).

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    Hallo **aanvraaggegevens** pagina wordt weergegeven, en in Hallo **traceringsinformatie** sectie ziet u uitvoer Hallo van Hallo trace-instructies die u toohello toegevoegd `Index` methode.

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    Standaard `trace.axd` alleen lokaal beschikbaar is. Indien u wenste de toomake deze beschikbaar is via een externe web-app, zou u `localOnly="false"` toohello `trace` -element in Hallo *Web.config* bestand, zoals weergegeven in het volgende voorbeeld Hallo:

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    Inschakelen van echter `trace.axd` in een productie-web-app is over het algemeen niet aanbevolen vanwege veiligheidsredenen en in de volgende secties Hallo ziet u een eenvoudiger manier tooread traceringslogboek in een Azure-web-app.

### <a name="view-hello-tracing-output-in-azure"></a>Hallo traceringsuitvoer weergeven in Azure
1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-webproject en klik op **publiceren**.
2. In Hallo **webpublicatie** in het dialoogvenster, klikt u op **publiceren**.

    Nadat Visual Studio publiceert de update, deze wordt geopend de startpagina van een browser venster tooyour (ervan uitgaande dat u hebt niet wissen **doel-URL** op Hallo **verbinding** tabblad).
3. In **Server Explorer**, met de rechtermuisknop op uw web-app en selecteer **Streaming logboeken bekijken**.

    ![Streaming-logboeken bekijken in het snelmenu](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    Hallo **uitvoer** zien dat u verbonden toohello logboek streaming service en wordt een lijn melding elke minuut dat door zonder een toodisplay logboek gaat wordt toegevoegd.

    ![Streaming-logboeken bekijken in het snelmenu](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. Klik in het Hallo-browservenster waarin de startpagina van uw toepassing, op **Contact**.

    Binnen een paar seconden Hallo de uitvoer van Hallo foutniveau trace die u hebt toegevoegd toohello `Contact` wordt weergegeven in Hallo **uitvoer** venster.

    ![Fouttracering in uitvoervenster](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    Visual Studio wordt alleen weergegeven voor foutniveau traceringen omdat die Hallo standaardinstelling bij het inschakelen van Hallo log-service controleren. Wanneer u een nieuwe Azure-web-app maakt, is alle logboekregistratie standaard uitgeschakeld, zoals u hebt gezien wanneer u de instellingenpagina Hallo eerder geopend:

    ![Toepassing afmelden](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    Echter, wanneer u hebt geselecteerd **Streaming logboeken bekijken**, Visual Studio automatisch gewijzigd **toepassing Logging(File System)** te**fout**, wat betekent dat foutniveau Logboeken ophalen van gerapporteerd. In alle van de logboeken voor tracering van toosee sorteren, kunt u deze instelling te wijzigen**uitgebreid**. Wanneer u een urgentieniveau lager is dan fout selecteert, worden ook alle logboeken voor hogere niveaus gemeld. Dus als u uitgebreide selecteert, ziet ook u informatie, waarschuwing en foutenlogboeken.  

1. In **Server Explorer**, met de rechtermuisknop op het Hallo-web-app en klik vervolgens op **weergave-instellingen** zoals u eerder hebt gedaan.
2. Wijziging **toepassingslogboeken (bestandssysteem)** te**uitgebreid**, en klik vervolgens op **opslaan**.

    ![Tracering niveau tooVerbose instellen](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. In Hallo-browservenster dat wordt nu weergegeven uw **Contact** pagina, klikt u op **Start**, klikt u vervolgens op **over**, en klik vervolgens op **Contact**.

    Binnen een paar seconden Hallo **uitvoer** venster bevat alle van de traceringsuitvoer.

    ![Uitgebreide trace-uitvoer](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    In deze sectie ingeschakeld en logboekregistratie met behulp van Azure-web-app-instellingen uitgeschakeld. U kunt ook inschakelen en uitschakelen van traceer-listeners door Hallo Web.config-bestand te wijzigen. Hallo Web.config-bestand wijzigt veroorzaakt echter Hallo app domain toorecycle tijdens het inschakelen van logboekregistratie via Hallo web-app-configuratie niet doen. Hallo probleem een tooreproduce lang duurt, of wordt onderbroken, recycling Hallo toepassingsdomein mogelijk 'op te lossen' deze als u toowait verplichten totdat deze zich weer voordoet. Inschakelen van diagnostische gegevens in Azure doen niet dit, zodat u kunt informatie over de fout onmiddellijk vastleggen.

### <a name="output-window-features"></a>Functies van het venster Output
Hallo **Azure logboeken** tabblad Hallo **uitvoer** venster bevat verschillende knoppen en een tekstvak:

![Logboeken tabblad knoppen](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

Deze uitvoeren Hallo na functies:

* Schakel Hallo **uitvoer** venster.
* In- of uitschakelen van automatische terugloop.
* Starten of stoppen van de bewaking van Logboeken.
* Geef op welke toomonitor registreert.
* Logboeken downloaden.
* Filteren op basis van een zoekopdracht of een reguliere expressie Logboeken.
* Sluit Hallo **uitvoer** venster.

Als u een zoekreeks of standaardexpressie invoert, wordt in Visual Studio logboekinformatie op Hallo client filtert. Dit betekent dat kunt u criteria Hallo nadat Hallo logboeken worden weergegeven in Hallo **uitvoer** venster en u kunt filtercriteria wijzigen zonder tooregenerate Hallo Logboeken.

## <a name="webserverlogs"></a>Web server-logboeken bekijken
Webserverlogboeken Leg alle HTTP-activiteit voor Hallo web-app. In de volgorde toosee ze in Hallo **uitvoer** venster er tooenable voor Hallo web-app en meld Visual Studio die u wilt dat toomonitor ze.

1. In Hallo **Azure Web App-configuratie** tabblad dat u hebt geopend vanuit **Server Explorer**, ook Web Server-logboekregistratie wijzigen**op**, en klik vervolgens op **Opslaan**.

    ![Web server-logboekregistratie inschakelen](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. In Hallo **uitvoer** venster, klikt u op Hallo **opgeven welke Azure logboeken toomonitor** knop.

    ![Opgeven welke toomonitor Azure Logboeken](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. In Hallo **opties voor logboekregistratie van Azure** dialoogvenster, **Web server-logboeken**, en klik vervolgens op **OK**.

    ![Web server-logboeken bewaken](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. In Hallo-browservenster waarin Hallo web-app wordt weergegeven, klikt u op **Start**, klikt u vervolgens op **over**, en klik vervolgens op **Contact**.

    Hallo-toepassingslogboeken doorgaans weergegeven eerst, gevolgd door Hallo web server-Logboeken. U moet wellicht toowait even Hallo tooappear registreert.

    ![Logboekbestanden van de webserver in het venster Output](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

Wanneer u eerst webserverlogboeken inschakelen met behulp van Visual Studio schrijft Azure standaard Hallo logboeken toohello-bestandssysteem. Als alternatief kunt u hello Azure portal toospecify die web server-logboeken worden geschreven tooa blob-container in een opslagaccount.

Als u Hallo tooenable portal-webserver logboekregistratie tooan Azure storage-account gebruiken en Schakel logboekregistratie in Visual Studio wanneer u opnieuw inschakelen van logboekregistratie in Visual Studio uit zijn de instellingen van uw storage-account hersteld.

## <a name="detailederrorlogs"></a>Gedetailleerde bericht foutenlogboeken weergeven
Gedetailleerde foutenlogboeken aanvullende informatie geven over HTTP-aanvragen die in fout reactiecodes (400 of hoger resulteren). In de volgorde toosee ze in Hallo **uitvoer** venster, hebt u tooenable voor Hallo web-app en meld Visual Studio die u wilt dat toomonitor ze.

1. In Hallo **Azure Web App-configuratie** tabblad dat u hebt geopend vanuit **Server Explorer**, wijzigen **gedetailleerde foutberichten** te**op**, en Klik vervolgens op **opslaan**.

    ![Gedetailleerde foutberichten inschakelen](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. In Hallo **uitvoer** venster, klikt u op Hallo **opgeven welke Azure logboeken toomonitor** knop.
3. In Hallo **opties voor logboekregistratie van Azure** in het dialoogvenster, klikt u op **alle logboeken**, en klik vervolgens op **OK**.

    ![Alle logboeken bewaken](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. In de adresbalk van Hallo browservenster hello, Voeg een extra teken toohello URL toocause een 404-fout (bijvoorbeeld `http://localhost:53370/Home/Contactx`), en druk op Enter.

    Na enkele seconden Hallo gedetailleerd foutenlogboek wordt weergegeven in Visual Studio Hallo **uitvoer** venster.

    ![Gedetailleerd foutenlogboek in uitvoervenster](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    Control + klik op Hallo koppeling toosee Hallo logboekuitvoer opgemaakt in een browser:

    ![Gedetailleerd foutenlogboek in browservenster](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <a name="downloadlogs"></a>Systeemlogboeken bestand downloaden
Alle logboeken die u in Hallo bewaken kunt **uitvoer** venster kan ook worden gedownload als een *.zip* bestand.

1. In Hallo **uitvoer** venster, klikt u op **Streaming logboeken downloaden**.

    ![Logboeken tabblad knoppen](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    Windows Verkenner wordt geopend tooyour *downloadt* map Hello gedownload bestand geselecteerd.

    ![Gedownloade bestand](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. Hallo extraheren *.zip* bestand en u ziet u Hallo volgende mapstructuur:

    ![Gedownloade bestand](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * Logboeken voor tracering van toepassing zijn in *.txt* bestanden in Hallo *LogFiles\Application* map.
   * Webserverlogboeken zijn *.log* bestanden in Hallo *LogFiles\http\RawLogs* map. U kunt een hulpprogramma zoals [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) tooview en het bewerken van deze bestanden.
   * Bericht van gedetailleerde foutenlogboeken zijn in *.html* bestanden in Hallo *LogFiles\DetailedErrors* map.

     (Hallo *implementaties* map is voor bestanden die zijn gemaakt door het besturingselement voor publiceren; er geen alles gerelateerde tooVisual Studio publiceren. Hallo *Git* map voor traceringen gerelateerde toosource besturingselement publiceren en Hallo logboekbestand streaming-service is.)  

## <a name="storagelogs"></a>Opslag-logboeken bekijken
Logboeken voor tracering van toepassing kunnen ook worden verzonden tooan Azure storage-account en kunt u deze bekijken in Visual Studio. toodo dat u hebt een opslagaccount maken, opslag Logboeken in de klassieke portal hello, en ze in Hallo weergeven **logboeken** tabblad Hallo **Azure-Web-App** venster.

U kunt Logboeken tooany of alle drie bestemmingen verzenden:

* Hallo-bestandssysteem.
* Storage-account-tabellen.
* Storage-account blobs.

U kunt een andere ernstniveau voor elk doel opgeven.

Tabellen maken het gemakkelijk tooview details van Logboeken online, en ze ondersteunen streaming; u kunt Logboeken in tabellen opvragen en nieuwe logboeken zien zoals ze worden gemaakt. BLOBs maken het gemakkelijk toodownload Logboeken in bestanden en tooanalyze ze met HDInsight, aangezien HDInsight weet hoe toowork met blob storage. Zie voor meer informatie **Hadoop en MapReduce** in [opties voor opslag van gegevens (gebouw echte Cloud-Apps met Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).

U hebt momenteel logboeken set tooverbose bestandssysteemniveau; Hallo doorlopen volgende stappen niveau logboeken toogo toostorage account uit de tabellen in te stellen. Informatie niveau betekent dat alle logboeken die zijn gemaakt door het aanroepen van `Trace.TraceInformation`, `Trace.TraceWarning`, en `Trace.TraceError` wordt weergegeven, maar niet de logboeken die zijn gemaakt door het aanroepen van `Trace.WriteLine`.

Storage-accounts bieden dat meer opslagruimte en het langer blijvende bewaren voor logboeken vergeleken toohello-bestandssysteem. Een ander voordeel van de betreffende toepassing Logboeken toostorage tracering is dat u aanvullende informatie met elk logboek die u via het systeemlogboek in Logboeken bestand niet ophalen.

1. Met de rechtermuisknop op **opslag** onder hello Azure knooppunt en klik vervolgens op **Storage-Account maken**.

![Storage-Account maken](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. In Hallo **Storage-Account maken** dialoogvenster, voer een naam voor het Hallo-opslagaccount.

    Hallo-naam moet uniek zijn (geen Azure storage-account kan Hallo hebben dezelfde naam). Als het Hallo-naam die u invoert, wordt al gebruikt krijgt u een kans toochange deze.

    Hallo URL tooaccess uw storage-account worden *{name}*. core.windows.net.
2. Set Hallo **regio of Affiniteitsgroep** vervolgkeuzelijst toohello regio dichtstbijzijnde tooyou.

    Deze instelling bepaalt u welke Azure-datacenter fungeert als host voor uw opslagaccount. Voor deze zelfstudie won't uw keuze maakt geen merkbaar verschil, maar voor een productie-web-app die u wilt uw webserver en uw storage-account toobe in Hallo dezelfde regio toominimize latentie en gegevens uitgaande kosten. Hallo-web-app (die u later maken) moet worden uitgevoerd in een regio zo dicht mogelijk toohello browsers toegang tot uw web-app in volgorde toominimize latentie.
3. Set Hallo **replicatie** vervolgkeuzelijst te**lokaal redundante**.
   
    Wanneer geo-replicatie is ingeschakeld voor een opslagaccount, is Hallo opgeslagen inhoud gerepliceerde tooa secundair datacenter tooenable failover toothat locatie in het geval van een noodgeval op Hallo primaire locatie. Geo-replicatie kan extra kosten met zich meebrengen. Voor test- en -accounts in het algemeen niet de bedoeling toopay voor geo-replicatie. Zie [Een opslagaccount maken, beheren of verwijderen](../storage/common/storage-create-storage-account.md) voor meer informatie.
4. Klik op **Create**.

    ![Nieuw opslagaccount](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. In Visual Studio Hallo **Azure-Web-App** venster, klikt u op Hallo **logboeken** tabblad en klik vervolgens op **logboekregistratie configureren in de beheerportal**.

    <!-- todo:screenshot of new portal if hello VS page link goes toonew portal -->
    ![Logboekregistratie configureren](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    Hiermee opent u Hallo **configureren** tabblad in de klassieke portal Hallo voor uw web-app.
6. In Hallo klassieke portal **configureren** tabblad, schuif naar beneden toohello application diagnostics sectie en wijzig vervolgens **toepassingslogboeken (Table Storage)** te**op**.
7. Wijziging **niveau van logboekregistratie** te**informatie**.
8. Klik op **Table Storage beheren**.

    ![Klik op beheren TableStorage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    In Hallo **beheren voor application diagnostics-tabelopslag** vak kunt u uw storage-account als u meer dan één hebt. U kunt een nieuwe tabel maken of een bestaande gebruiken.

    ![Table storage beheren](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. In Hallo **beheren voor application diagnostics-tabelopslag** vak klikt u op Hallo vinkje tooclose Hallo vak.
10. In Hallo klassieke portal **configureren** tabblad **opslaan**.
11. In het browservenster Hallo die Hallo toepassing web-app wordt weergegeven, klikt u op **Start**, klikt u vervolgens op **over**, en klik vervolgens op **Contact**.

     Hallo logboekregistratie informatie die wordt geproduceerd door deze webpagina's bladeren wordt toohello storage-account geschreven.
12. In Hallo **logboeken** tabblad Hallo **Azure-Web-App** venster in Visual Studio, klikt u op **vernieuwen** onder **diagnostische samenvatting**.

     ![Klik op vernieuwen](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     Hallo **diagnostische samenvatting** sectie toont logboeken voor Hallo afgelopen 15 minuten standaard. U kunt Hallo periode toosee meer logboeken te wijzigen.

     (Als u een 'tabel is niet gevonden'-fout krijgt, controleert u of dat u toohello-pagina's die Hallo bekeken nadat u hebt ingeschakeld voor het traceren **toepassingslogboeken (opslag)** en nadat u hebt geklikt **opslaan**.)

     ![Opslag Logboeken](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     U ziet dat in deze weergave die u Zie **proces-ID** en **Thread-ID** voor elk logboek die u in de systeemlogboeken Hallo-bestand niet ophalen. U kunt aanvullende velden zien door rechtstreeks hello Azure storage tabel weer te geven.
13. Klik op **weergeven van alle toepassingslogboeken**.

     Hallo trace logboektabel wordt weergegeven in hello Azure storage tabel viewer.

     (Als u krijgt een fout 'reeks bevat geen elementen', opent u **Server Explorer**, vouwt u Hallo knooppunt voor uw opslagaccount onder Hallo **Azure** -knooppunt en klik met de rechtermuisknop **tabellen**en klik op **vernieuwen**.)

     ![Opslag wordt geregistreerd in tabelweergave](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     Deze weergave toont aanvullende velden dat niet wordt weergegeven in andere weergaven. Deze weergave kunt u ook toofilter logboeken met behulp van de gebruikersinterface van de opbouwfunctie voor speciale Query voor het samenstellen van een query. Zie voor meer informatie, werken met Resources van de tabel - entiteiten in filteren [opslagbronnen bladeren met Server Explorer](http://msdn.microsoft.com/library/ff683677.aspx).
14. toolook Hallo-informatie voor een enkele rij, dubbelklik op een van de rijen Hallo.

     ![Trace-tabel in Server Explorer](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <a name="failedrequestlogs"></a>Logboeken voor tracering van mislukte aanvragen weergeven
Logboeken voor tracering van mislukte aanvragen zijn nuttig wanneer u toounderstand Hallo details van hoe IIS een HTTP-aanvraag in scenario's zoals URL herschrijven of verificatie problemen verwerkt.

Azure-web-apps gebruik Hallo dezelfde kan aanvragen tracering-functionaliteit is beschikbaar in IIS 7.0 en hoger. U hebt geen toegang tot toohello IIS-instellingen die welke fouten configureren worden geregistreerd, maar. Wanneer u tracering van mislukte aanvragen inschakelt, worden alle fouten worden vastgelegd.

U kunt tracering van mislukte aanvragen inschakelen met behulp van Visual Studio, maar u kunt ze niet weergeven in Visual Studio. Deze logboeken vormen een XML-bestanden. Hallo streaming log-service controleert de bestanden die worden geacht leesbaar in tekstmodus zonder opmaak: *.txt*, *.html*, en *.log* bestanden.

U kunt de logboeken voor tracering van mislukte aanvragen weergeven in een browser rechtstreeks via de FTP- of lokaal na gebruik van een FTP-hulpprogramma toodownload ze tooyour lokale computer. In deze sectie bekijkt u ze in een browser rechtstreeks.

1. In Hallo **configuratie** tabblad Hallo **Azure-Web-App** venster dat u hebt geopend vanuit **Server Explorer**, wijzigen **tracering van mislukte aanvragen**te**op**, en klik vervolgens op **opslaan**.

    ![Tracering van mislukte aanvragen inschakelen](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. Een extra teken toohello-URL toevoegen in de adresbalk Hallo van Hallo-browservenster waarin Hallo web-app en klikt u op Enter toocause een 404-fout.

    Dit zorgt ervoor dat toobe logboek met de tracering van mislukte aanvragen gemaakt en hello volgende stappen laten zien hoe Hallo logboek tooview of downloaden.
3. In Visual Studio in Hallo **configuratie** tabblad Hallo **Azure-Web-App** venster, klikt u op **openen in de beheerportal**.
4. In Hallo [Azure Portal](https://portal.azure.com) **instellingen** blade voor uw web-app klikt u op **implementatiereferenties**, en voer vervolgens een nieuwe gebruikersnaam en wachtwoord.

    ![Nieuwe FTP-gebruikersnaam en wachtwoord](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    ** Wanneer u zich aanmeldt, hebt u toouse Hallo volledige gebruikersnaam met de Hallo web app name voorafgegaan tooit. Bijvoorbeeld, als u "myid" als een gebruikersnaam invoeren en Hallo site 'myexample' is, aanmelden u als 'myexample\myid'.
5. Ga in een nieuw browservenster toohello-URL die wordt weergegeven onder **FTP-hostnaam** of **FTPS hostnaam** in Hallo **Web-App** blade voor uw web-app.
6. Meld u aan met Hallo FTP-referenties die u eerder (inclusief Hallo web app voorvoegsel voor de gebruikersnaam Hallo) gemaakt.

    Hallo browser toont Hallo-hoofdmap van het Hallo-web-app.
7. Open Hallo *logboekbestanden* map.

    ![Logboekbestanden openen](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. Open Hallo-map met de naam W3SVC plus een numerieke waarde.

    ![Open de map W3SVC](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    Hallo-map bevat de XML-bestanden op fouten die zijn geregistreerd nadat u de tracering van mislukte aanvragen ingeschakeld en een XSL-bestand dat een browser tooformat Hallo XML kunt gebruiken.

    ![W3SVC-map](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. Klik op Hallo XML-bestand voor Hallo van mislukte aanvragen die u wilt dat de traceringsinformatie toosee voor.

    Hallo volgende afbeelding ziet u deel uit van de traceringsinformatie Hallo voor een voorbeeld-fout.

    ![Tracering van mislukte aanvragen in de browser](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <a name="nextsteps"></a>Volgende stappen
U hebt gezien hoe Visual Studio maakt het eenvoudig tooview logboeken die zijn gemaakt door een Azure-web-app. Hallo volgende secties vindt u koppelingen toomore resources op Verwante onderwerpen:

* Azure-web-app oplossen
* Foutopsporing in Visual Studio
* Externe foutopsporing in Azure
* Traceren in ASP.NET-toepassingen
* Analyseren van weblogboeken van server
* Analyseren van Logboeken voor tracering van mislukte aanvragen
* Foutopsporing van Cloud-Services

### <a name="azure-web-app-troubleshooting"></a>Azure-web-app oplossen
Zie voor meer informatie over het oplossen van web-apps in Azure App Service Hallo resources te volgen:

* [Hoe toomonitor web-apps](/manage/services/web-sites/how-to-monitor-websites/)
* [Onderzoeken geheugenlekken in Azure-Web-Apps met Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx). Microsoft ALM blogbericht over de functies van Visual Studio voor het analyseren van problemen met het systeemgeheugen beheerd.
* [Azure-web-apps online hulpprogramma's u moet weten over](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/). Blogbericht Amit Apple.

Voor meer informatie over een specifieke vraag voor het oplossen van problemen, een thread in een van volgende forums hello te starten:

* [Azure-forum op Hallo ASP.NET-website Hallo](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).
* [Azure-forum op MSDN Hallo](http://social.msdn.microsoft.com/Forums/windowsazure/).
* [StackOverflow.com](http://www.stackoverflow.com).

### <a name="debugging-in-visual-studio"></a>Foutopsporing in Visual Studio
Zie voor meer informatie over hoe toouse foutopsporingsmodus in Visual Studio, Hallo [foutopsporing in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) MSDN-onderwerp en [Tips foutopsporing met Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).

### <a name="remote-debugging-in-azure"></a>Externe foutopsporing in Azure
Zie voor meer informatie over foutopsporing op afstand voor Azure-web-apps en WebJobs Hallo resources te volgen:

* [Inleiding tooRemote foutopsporing in Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).
* [Inleiding tooRemote foutopsporing in Azure App Service Web Apps deel 2 - binnen foutopsporing op afstand](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [Inleiding tooRemote foutopsporing op Azure App Service Web Apps deel 3 - omgeving met meerdere exemplaren en GIT](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [WebJobs foutopsporing (video)](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

Als uw web-app gebruikmaakt van een Azure-Web-API of Mobile Services back-end en moet u toodebug die zien [.NET Backend foutopsporing in Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).

### <a name="tracing-in-aspnet-applications"></a>Traceren in ASP.NET-toepassingen
Er zijn geen grondige en up-to-date inleidingen tooASP.NET tracering beschikbaar op Hallo Internet. Hallo best kunt u doen is aan de slag met oude inleidende materialen die zijn geschreven voor webformulieren omdat MVC niet nog bestaat en dat met nieuwere blog vullen die gericht zijn op specifieke problemen boekt. Sommige toostart geschikte locaties zijn Hallo resources te volgen:

* [Bewaking en telemetrie (gebouw echte Cloud-Apps met Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).<br>
  E-book hoofdstuk met aanbevelingen voor tracering in Azure-cloud-toepassingen.
* [ASP.NET-tracering](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  Oude maar nog steeds een goede bron voor een algemene inleiding tot toohello onderwerp.
* [Traceer-Listeners](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  Informatie over traceer-listeners, maar wordt niet vermeld Hallo [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).
* [Overzicht: ASP.NET-tracering integreren met System.Diagnostics tracering](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  Dit dat te oud is, maar bevat aanvullende informatie die Hallo inleidende artikel wordt niet beschreven.
* [Traceren in ASP.NET MVC Razor weergaven](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  Naast de tracering in Razor weergaven Hallo post ook wordt uitgelegd hoe een fout toocreate filter in volgorde toolog alle niet-verwerkte uitzonderingen in een MVC-toepassing. Voor informatie over hoe toolog alle niet-verwerkte uitzonderingen in een toepassing webformulieren Zie Hallo Global.asax voorbeeld in [compleet voorbeeld voor fout-Handlers](http://msdn.microsoft.com/library/bb397417.aspx) op MSDN. In MVC of webformulieren, als u toolog bepaalde uitzonderingen wilt maar Hallo standaard framework afhandeling van kracht, zodat kunt u catch en rethrow zoals in het volgende voorbeeld Hallo:

        try
        {
           // Your code that might cause an exception toobe thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [Streaming Diagnostics Trace Logging van hello Azure-opdrachtregelinterface (plus blik!)](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  Hoe toouse Hallo opdrachtregel toodo welke van deze zelfstudie ziet hoe toodo in Visual Studio. [Blik](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) is een hulpprogramma voor het opsporen van ASP.NET-toepassingen.
* [Met behulp van WebApps-logboekregistratie en diagnose - met David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) en [Streaminglogboeken van Web-Apps - met David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)<br>
  Video van Scott Hanselman en David Ebbo.

Voor logboekregistratie, fout, een alternatieve toowriting uw eigen code tracering is toouse een open-source framework voor logboekregistratie zoals [ELMAH](http://nuget.org/packages/elmah/). Zie voor meer informatie [van Scott Hanselman blogberichten over ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).

Merk ook op dat u geen toouse ASP.NET hebt of System.Diagnostics tracering als u wilt dat tooget streaming van Azure registreert. Hello Azure-web-app streaming log-service wordt stream een *.txt*, *.html*, of *.log* bestand dat wordt aangetroffen in Hallo *logboekbestanden* map. Daarom kunt u uw eigen systeem logboekregistratie die toohello bestandssysteem van Hallo web-app schrijft maken en het bestand wordt automatisch worden gestreamd en gedownload. U toodo alleen schrijven toepassingscode die bestanden maakt in Hallo *d:\home\logfiles* map.

### <a name="analyzing-web-server-logs"></a>Analyseren van weblogboeken van server
Zie voor meer informatie over het analyseren van webserverlogboeken Hallo resources te volgen:

* [LogParser](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  Een hulpprogramma voor het weergeven van gegevens in de web server-Logboeken (*.log* bestanden).
* [Het oplossen van problemen met prestaties van IIS of toepassingsfouten LogParser met](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  Een inleiding toohello Log Parser hulpprogramma waarmee u de webserver tooanalyze kunt registreert.
* [Blogberichten door Robert McMurray over het gebruik van LogParser](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [Hallo HTTP-statuscode in IIS 7.0, IIS 7.5 en IIS 8.0](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a>Analyseren van Logboeken voor tracering van mislukte aanvragen
Hallo Microsoft TechNet-website bevat een [met behulp van tracering van mislukte aanvragen](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) sectie die mogelijk handig om te begrijpen hoe toouse deze logboeken. Echter, deze documentatie richt zich voornamelijk op de tracering van mislukte aanvragen configureren in IIS, dat niet mogelijk in Azure Web Apps.

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
