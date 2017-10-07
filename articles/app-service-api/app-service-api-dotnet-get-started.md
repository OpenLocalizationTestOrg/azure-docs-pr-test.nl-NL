---
title: aaaGet slag met API-Apps en ASP.NET in App Service | Microsoft Docs
description: Ontdek hoe toocreate, implementeren en gebruiken van een ASP.NET API-app in Azure App Service met behulp van Visual Studio 2015.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a>Aan de slag met API-apps, ASP.NET en Swagger in Azure App Service
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

Dit is Hallo eerst in een reeks zelfstudies die laten zien hoe toouse functies van Azure App Service die zijn handig voor het ontwikkelen en hosten van RESTful-API's.  In deze zelfstudie wordt ondersteuning voor API-metagegevens in Swagger-indeling besproken.

U leert het volgende:

* Hoe toocreate en implementeren van [API-apps](app-service-api-apps-why-best-platform.md) in Azure App Service met behulp van hulpprogramma's die zijn ingebouwd in Visual Studio 2015.
* Hoe tooautomate API-detectie met behulp van Hallo Swashbuckle NuGet-pakket genereren toodynamically Swagger API-metagegevens.
* Hoe toouse Swagger API-metagegevens tooautomatically clientcode genereren voor een API-app.

## <a name="sample-application-overview"></a>Overzicht van voorbeeldtoepassing
In deze zelfstudie werkt u met een voorbeeld van een eenvoudige takenlijsttoepassing. Hallo-toepassing heeft een front-end van één pagina (SPA application '), een ASP.NET Web API als middelste laag en een ASP.NET Web API als gegevenslaag.

![Diagram van API-apps-voorbeeldtoepassing](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

Hier volgt een schermopname van het Hallo [AngularJS](https://angularjs.org/) front-end.

![Lijst met toepassingen toodo en API Apps-voorbeeld](./media/app-service-api-dotnet-get-started/todospa.png)

Hallo Visual Studio-oplossing omvat drie projecten:

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* **ToDoListAngular** -Hallo-front-end: een AngularJS SPA die Hallo middelste laag aanroept.
* **ToDoListAPI** -Hallo middelste laag: een ASP.NET Web API-project die Hallo gegevenslaag tooperform CRUD-bewerkingen op taken aanroept.
* **ToDoListDataAPI** -Hallo gegevenslaag: een ASP.NET Web API-project dat CRUD-bewerkingen op taken uitvoert.

Hallo architectuur met drie lagen is een van de vele architecturen die u kunt implementeren met behulp van API Apps en wordt hier alleen voor demonstratiedoeleinden gebruikt. Hallo-code in elke laag is net zo eenvoudig als mogelijke toodemonstrate API Apps-functies. Hallo gegevenslaag gebruikt bijvoorbeeld geheugen van de server in plaats van een database als het mechanisme voor persistentie.

Op het voltooien van deze zelfstudie hebt u Hallo twee Web API-projecten en uitgevoerd in de cloud Hallo in App Service API-apps.

Hallo volgende zelfstudie in de reeks Hallo implementeert Hallo SPA-front-end toohello cloud.

## <a name="prerequisites"></a>Vereisten
* ASP.NET Web API - instructies Hallo-zelfstudie wordt ervan uitgegaan dat u een elementaire kennis hebben van hoe toowork met ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.
* Azure-account: u kunt [een gratis Azure-account openen](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
  
    Als u wilt dat tooget gestart met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/). Daar kunt u direct een eenvoudige, tijdelijke app maken in App Service. U hebt hiervoor **geen creditcard nodig** en bent nergens toe verplicht.
* Visual Studio 2015 met de Hallo [Azure SDK voor .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -Hallo SDK installeert Visual Studio 2015 automatisch als u nog geen hebt.
  
  * Klik in Visual Studio op Help -> Over Microsoft Visual Studio en zorg ervoor dat 'Azure App Service Tools v2.9.1' of hoger is geïnstalleerd.
    
    ![Versie van Azure App Tools](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > Afhankelijk van hoeveel van Hallo SDK-afhankelijkheden u al op uw computer hebt, kan installeren Hallo SDK lang duren, van enkele minuten tooa halfuur of meer.
    > 
    > 

## <a name="download-hello-sample-application"></a>Hallo-voorbeeldtoepassing downloaden
1. Hallo downloaden [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) opslagplaats.
   
    U kunt klikken op Hallo **ZIP downloaden** knop of kloon Hallo-opslagplaats op uw lokale machine.
2. Open de ToDoList-oplossing Hallo in Visual Studio 2015 of 2013.
   
   1. U moet tootrust elke oplossing.
         ![Beveiligingswaarschuwing](./media/app-service-api-dotnet-get-started/securitywarning.png)
3. Hallo-oplossing (CTRL + SHIFT + B) toorestore hello NuGet-pakketten maken.
   
    Als u toosee Hallo toepassing in bewerking wilt voordat u deze implementeert, kunt u deze lokaal uitvoeren. Zorg ervoor dat de ToDoListDataAPI uw opstartproject en Voer Hallo-oplossing is. Verwachte toosee 403 HTTP-fout in uw browser.

## <a name="use-swagger-api-metadata-and-ui"></a>Swagger API-metagegevens en -gebruikersinterface gebruiken
Ondersteuning voor [Swagger](http://swagger.io/) 2.0 API-metagegevens is ingebouwd in Azure App Service. Elke API-app kunt een URL-eindpunt dat metagegevens voor Hallo API in Swagger JSON-indeling retourneert opgeven. Hallo metagegevens geretourneerd vanuit dat eindpunt mag toogenerate clientcode gebruikt.

Een ASP.NET Web API-project kan Swagger-metagegevens dynamisch genereren met behulp van Hallo [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet-pakket. Hallo Swashbuckle NuGet-pakket is al geïnstalleerd in Hallo ToDoListDataAPI- en ToDoListAPI-projecten die u hebt gedownload.

In deze sectie van de zelfstudie Hallo u bekijkt hello gegenereerde Swagger 2.0-metagegevens en probeert u een testgebruikersinterface die is gebaseerd op Hallo Swagger-metagegevens.

1. Hallo ToDoListDataAPI project instellen (**niet** hello ToDoListAPI-project) als opstartproject Hallo.
   
    ![ToDoDataAPI instellen als opstartproject](./media/app-service-api-dotnet-get-started/startupproject.png)
2. Druk op F5 of klik op **fouten opsporen > Foutopsporing starten** toorun Hallo-project in de foutopsporingsmodus.
   
    Hallo-browser wordt geopend en ziet u Hallo HTTP 403-foutpagina.
3. Voeg in de adresbalk van uw browser `swagger/docs/v1` toohello einde van het Hallo-regel en druk vervolgens op ENTER. (Hallo-URL is `http://localhost:45914/swagger/docs/v1`.)
   
    Dit is standaard-URL Hallo door Swashbuckle tooreturn Swagger 2.0 JSON-metagegevens gebruikt voor Hallo API.
   
    Als u van Internet Explorer gebruikmaakt, Hallo browser wordt u gevraagd toodownload een *v1.json* bestand.
   
    ![JSON-metagegevens downloaden in Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    Als u Chrome, Firefox of Edge gebruikt, wordt in Hallo browser Hallo JSON in Hallo browservenster weergegeven. Verschillende browsers verwerken JSON anders en uw browservenster mag niet precies hetzelfde uitzien als Hallo-voorbeeld.
   
    ![JSON-metagegevens in Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    Hallo volgende voorbeeld toont de eerste sectie Hallo van Hallo Swagger-metagegevens voor Hallo-API met Hallo definitie voor Hallo methode Get. Deze metagegevens is welke stations Hallo Swagger-gebruikersinterface die u in de volgende stappen uit Hallo gebruikt, en u deze in een volgende sectie van de zelfstudie tooautomatically Hallo gebruiken genereren van clientcode.
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. Sluit Hallo browser en stop de foutopsporing van Visual Studio.
5. Project in Hallo ToDoListDataAPI in **Solution Explorer**Open Hallo *App_Start\SwaggerConfig.cs* file en schuif omlaag tooline 174 en het commentaar verwijderen Hallo code te volgen.
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    Hallo *SwaggerConfig.cs* bestand wordt gemaakt wanneer u Hallo Swashbuckle-pakket in een project installeert. Hallo-bestand bevat een aantal manieren tooconfigure Swashbuckle.
   
    Hallo-code u hebt zonder opmerkingen schakelt Hallo Swagger-gebruikersinterface die u gebruikt in hello te volgen stappen. Wanneer u een Web API-project maakt met behulp van Hallo API-app-projectsjabloon, wordt deze code standaard uitgecommentarieerd als veiligheidsmaatregel.
6. Hallo-project opnieuw uitgevoerd.
7. Voeg in de adresbalk van uw browser `swagger` toohello einde van het Hallo-regel en druk vervolgens op ENTER. (Hallo-URL is `http://localhost:45914/swagger`.)
8. Wanneer Hallo Swagger-gebruikersinterface pagina wordt weergegeven, klikt u op **ToDoList** toosee Hallo methoden beschikbaar.
   
    ![Beschikbare methoden in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/methods.png)
9. Klik eerst op Hallo **ophalen** knop in Hallo-lijst.
10. In Hallo **Parameters** sectie, geeft u een sterretje als waarde Hallo Hallo `owner` parameter en klik vervolgens op **Try it out in**.
    
    Wanneer u verificatie in latere zelfstudies toevoegt, geven de middelste laag Hallo toohello gegevenslaag voor Hallo werkelijke gebruikers-ID. Nu alle taken een sterretje als eigenaar-ID tijdens het Hallo-toepassing wordt uitgevoerd zonder verificatie is ingeschakeld.
    
    ![Try it out in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    Hallo Swagger-gebruikersinterface roept Hallo ToDoList Get-methode en Hallo responscode en JSON-resultaten weergegeven.
    
    ![Resultaten van Try it out in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. Klik op **Post**, en klik vervolgens op Hallo vak onder **modelschema**.
    
    Als u op Hallo model schema prefills Hallo invoervak waarin u de parameterwaarde Hallo voor Hallo Post-methode kunt opgeven. (Als dit niet in Internet Explorer werkt, een andere browser gebruikt of Hallo parameterwaarde handmatig invoeren in de volgende stap Hallo.)  
    
    ![Post voor Try it out in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/post.png)
12. Wijziging Hallo JSON in Hallo `todo` parameter invoer vak zodat het lijkt erop dat Hallo volgende voorbeeld of vervang deze door uw eigen beschrijvende tekst:
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. Klik op **Try it out**.
    
    Hallo ToDoList-API retourneert een 204 HTTP-antwoordcode die slagen aangeeft.
14. Klik eerst op Hallo **ophalen** knop en klik vervolgens in die sectie van de pagina Hallo op Hallo **Try it out in** knop.
    
    Hallo antwoord van Get-methode bevat nu Hallo nieuw toodo item.
15. Optioneel: Probeer ook Hallo Put, Delete, en Get by ID methoden.
16. Sluit Hallo browser en stop de foutopsporing van Visual Studio.

Swashbuckle werkt met elk ASP.NET Web API-project. Als u tooadd Swagger-metagegevens generatie tooan bestaand project wilt, gewoon Hallo Swashbuckle-pakket te installeren.

> [!NOTE]
> De Swagger-metagegevens bevatten voor elke API-bewerking een unieke id. Standaard kan Swashbuckle dubbele Swagger-bewerkings-id's genereren voor uw Web API-controllermethoden. Dit gebeurt als uw domeincontroller overbelaste HTTP-methoden bevat, zoals `Get()` en `Get(id)`. Zie voor meer informatie over hoe toohandle overloads [aanpassen door Swashbuckle gegenereerde API-definities](app-service-api-dotnet-swashbuckle-customize.md). Als u een Web API-project in Visual Studio met hello Azure API-App-sjabloon maakt, code die unieke bewerkings-id gegenereerd toohello wordt automatisch toegevoegd *SwaggerConfig.cs* bestand.  
> 
> 

## <a id="createapiapp"></a>Een API-app in Azure maken en implementeren van code tooit
In deze sectie gebruikt u Azure-hulpprogramma's die zijn geïntegreerd met Visual Studio Hallo **webpublicatie** wizard toocreate een nieuwe API-app in Azure. Vervolgens Hallo ToDoListDataAPI project toohello nieuwe API-app implementeren en Hallo API aanroepen door het uitvoeren van Hallo Swagger-gebruikersinterface.

1. In **Solution Explorer**, met de rechtermuisknop op Hallo ToDoListDataAPI project en klik vervolgens op **publiceren**.
   
    ![Klikken op Publish in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. In Hallo **profiel** stap Hallo **webpublicatie** wizard, klikt u op **Microsoft Azure App Service**.
   
   ![Klikken op Azure App Service in de wizard Publish Web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. Meld u aan tooyour Azure-account als u dit nog niet hebt gedaan of vernieuw uw referenties als deze zijn verlopen.
4. In het dialoogvenster App Service Hallo, kiest u hello Azure **abonnement** u toouse wilt en klik vervolgens op **nieuw**.
   
    ![Klikken op New in het dialoogvenster App Service](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    Hallo **Hosting** tabblad Hallo **Create App Service** dialoogvenster wordt weergegeven.
   
    Omdat u een Web-API-project dat swashbuckle is geïnstalleerd implementeert, Visual Studio wordt ervan uitgegaan dat u wilt dat toocreate een API-App. Dit wordt aangegeven door Hallo **API App Name** title en door Hallo feit die Hallo **wijzigingstype** vervolgkeuzelijst is ingesteld, te**API-App**.
   
    ![App-type in het dialoogvenster App Service](./media/app-service-api-dotnet-get-started/apptype.png)
5. Voer een **API App Name** die uniek is in Hallo *azurewebsites.net* domein. U kunt de standaardnaam Hallo die Visual Studio wordt voorgesteld accepteren.
   
    Als u een naam die iemand anders al gebruikt opgeeft, ziet u een rood uitroepteken toohello rechts.
   
    Hallo URL van Hallo API-app worden `{API app name}.azurewebsites.net`.
6. In Hallo **resourcegroep** omlaag, klikt u op **nieuw**, en voer vervolgens 'ToDoListGroup' of een andere naam desgewenst.
   
    Een resourcegroep is een verzameling Azure-resources, zoals web-apps, databases, virtuele machines, enzovoort.    Voor deze zelfstudie is het beste toocreate een nieuwe resourcegroep kunt dan eenvoudig toodelete in één stap die alle Azure-resources die u voor de zelfstudie Hallo maakt Hallo.
   
    In dit vak kunt u een bestaande [resourcegroep](../azure-resource-manager/resource-group-overview.md) selecteren of een nieuwe maken door een naam te typen die anders is dan alle bestaande resourcegroepen in uw abonnement.
7. Klik op Hallo **nieuw** knop volgende toohello **App Service-Plan** vervolgkeuzelijst.
   
    Hallo Schermafbeelding toont voorbeeldwaarden voor **API App Name**, **abonnement**, en **resourcegroep** --de waarden zijn anders.
   
    ![Het dialoogvenster App Service maken](./media/app-service-api-dotnet-get-started/createas.png)
   
    In Hallo stappen maakt u een App Service-plan voor de nieuwe resourcegroep Hallo. Een App Service-plan bevat Hallo rekenresources die door uw API-app wordt uitgevoerd op. Bijvoorbeeld, als u de gratis laag hello, uw API-app wordt uitgevoerd op gedeelde virtuele machines, terwijl voor sommige betaald lagen deze wordt uitgevoerd via exclusieve virtuele machines. Zie [Overzicht van App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) voor informatie over App Service-plannen
8. In Hallo **Configure App Service Plan** dialoogvenster 'ToDoListPlan' of een andere naam invoeren als u liever.
9. In Hallo **locatie** vervolgkeuzelijst Kies Hallo locatie die het dichtst tooyou.
   
    Met deze instelling bepaalt u in welk Azure-datacentrum uw app wordt uitgevoerd. Kies een locatie sluiten tooyou toominimize [latentie](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).
10. In Hallo **grootte** omlaag, klikt u op **vrije**.
    
    Voor deze zelfstudie bieden Hallo gratis prijscategorie voldoende prestaties.
11. In Hallo **Configure App Service Plan** dialoogvenster, klikt u op **OK**.
    
    ![Klikken op OK in het dialoogvenster Configure App Service Plan](./media/app-service-api-dotnet-get-started/configasp.png)
12. In Hallo **Create App Service** in het dialoogvenster, klikt u op **maken**.
    
    ![Klikken op Create in het dialoogvenster Create App Service](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    Visual Studio maakt Hallo API-app en een publicatieprofiel met alle vereiste Hallo-instellingen voor Hallo API-app. En vervolgens het openen van Hallo **webpublicatie** wizard, waar u toodeploy Hallo project.
    
    Hallo **webpublicatie** wizard wordt geopend op Hallo **verbinding** tabblad (Zie hieronder).
    
    Op Hallo **verbinding** tabblad hello **Server** en **sitenaam** instellingen punt tooyour API-app. Hallo **gebruikersnaam** en **wachtwoord** zijn implementatiereferenties die Azure voor u maakt. Na de implementatie opent Visual Studio een browser toohello **doel-URL** (oftewel Hallo enige doel van het **doel-URL**).  
13. Klik op **Volgende**.
    
    ![Klikken op Next op het tabblad Connection van de wizard Publish Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    Hallo volgende tabblad is Hallo **instellingen** tabblad (Zie hieronder). Hier kunt u wijzigen Hallo build configuration tabblad toodeploy een foutopsporingsversie voor [foutopsporing op afstand](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug). Hallo tabblad biedt ook diverse **opties voor het publiceren van bestand**:
    
    * Aanvullende bestanden op de bestemming verwijderen
    * Voorcompileren tijdens het publiceren
    * Bestanden uitsluiten van de map App_Data Hallo
    
    Voor deze zelfstudie hebt u geen van deze opties nodig. Zie [Procedure: een webproject implementeren met behulp van publicatie met één klik in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) voor gedetailleerde uitleg over deze opties.
14. Klik op **Volgende**.
    
    ![Klikken op Next op het tabblad Settings van de wizard Publish Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    Hierna volgt Hallo **Preview** tabblad (Zie hieronder), waarmee u een kans toosee welke bestanden toobe gekopieerd van uw project toohello API-app gaat. Wanneer u een project tooan API-app die u hebt al geïmplementeerd tooearlier implementeert, worden alleen de gewijzigde bestanden gekopieerd. Als u een lijst met wat er wordt gekopieerd toosee wilt, kunt u Hallo **Start Preview** knop.
15. Klik op **Publish**.
    
    ![Klikken op Publish op het tabblad Preview van de wizard Publish Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    Visual Studio implementeert Hallo ToDoListDataAPI project toohello nieuwe API-app. Hallo **uitvoer** venster Logboeken geslaagde implementatie en een 'is gemaakt' pagina wordt weergegeven in een browser geopend venster toohello URL van Hallo API-app.
    
    ![Bevestiging van geslaagde implementatie in het venster Output](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Pagina met melding dat de nieuwe API-app is gemaakt](./media/app-service-api-dotnet-get-started/appcreated.png)
16. 'Swagger' toohello URL toevoegen in de adresbalk van Hallo browser en druk op Enter. (Hallo-URL is `http://{apiappname}.azurewebsites.net/swagger`.)
    
    Hallo browser geeft dezelfde Swagger-gebruikersinterface die u eerder hebt gezien, maar nu wordt uitgevoerd in de cloud Hallo Hallo weer. Probeer Hallo Get-methode en u ziet dat je back toohello standaard 2 taakitems. Hallo-wijzigingen die u eerder hebt gemaakt zijn opgeslagen in het geheugen van de lokale computer Hallo.
17. Open Hallo [Azure-portal](https://portal.azure.com/).
    
    Hello Azure-portal is een webinterface voor het beheer van Azure-bronnen zoals API-apps.
18. Klik op **Meer Services > App Services**.
    
    ![Bladeren door App Services](./media/app-service-api-dotnet-get-started/browseas.png)
19. In Hallo **App Services** blade zoeken en klikt u op uw nieuwe API-app. (In hello Azure-portal, windows dat toohello rechts openen genoemd *blades*.)
    
    ![De blade App Services](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    Er worden twee blades geopend. Een blade bevat een overzicht van Hallo API-app en een heeft een lange lijst met instellingen die u kunt weergeven en wijzigen.
20. In Hallo **instellingen** blade, zoeken Hallo **API** sectie en klik op **API-definitie**.
    
    ![API-definitie op de blade Instellingen](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    Hallo **API-definitie** blade kunt u opgeven Hallo-URL die de metagegevens van Swagger 2.0 JSON-indeling retourneert. Als u Visual Studio Hallo API-app maakt, wordt Hallo API-definitie URL toohello-standaardwaarde voor door Swashbuckle gegenereerde metagegevens die u eerder hebt gezien dat Hallo API-app van de basis URL plus `/swagger/docs/v1`.
    
    ![URL van de API-definitie](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    Wanneer u een API-app toogenerate client-code voor deze selecteert, haalt Visual Studio Hallo metagegevens van deze URL.

## <a id="codegen"></a>Genereren van clientcode voor Hallo gegevenslaag
Een van de voordelen van de integratie van Swagger in Azure API-apps Hallo is automatisch genereren van code. Gegenereerde clientklassen maken het gemakkelijker toowrite-code die een API-app aanroept.

Hallo ToDoListAPI-project bevat al de clientcode Hallo gegenereerd, maar in de volgende stappen uit Hallo past u deze verwijderen en opnieuw genereren toosee hoe toodo Hallo genereren van code.

1. In Visual Studio **Solution Explorer**in Hallo ToDoListAPI-project, Hallo verwijderen, *ToDoListDataAPI* map. **Waarschuwing: Alleen Hallo map, niet Hallo-project ToDoListDataAPI verwijderen.**
   
    ![Gegenereerde clientcode verwijderen](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    Deze map is gemaakt met behulp van Hallo codeproces voor het genereren waarmee u over toogo via bent.
2. Met de rechtermuisknop op Hallo ToDoListAPI-project en klik vervolgens op **Add > REST API Client**.
   
    ![REST-API-client toevoegen in Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. In Hallo **Add REST API Client** in het dialoogvenster, klikt u op **Swagger URL**, en klik vervolgens op **Select Azure Asset**.
   
    ![Azure-asset selecteren](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. In Hallo **App Service** in het dialoogvenster vouwt u Hallo-resourcegroep die u voor deze zelfstudie en selecteer uw API-app en klik vervolgens op **OK**.
   
    ![API-app selecteren voor het genereren van code](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    Merk op dat wanneer u toohello terugkeert **Add REST API Client** dialoogvenster Hallo tekstvak is ingevuld Hallo API-definitie URL-waarde die u eerder in de portal Hallo hebt gezien.
   
    ![URL van de API-definitie](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > Een andere manier tooget-metagegevens voor het genereren van code is tooenter Hallo URL rechtstreeks in plaats van het Hallo-bladervenster doorlopen. Of als u clientcode toogenerate wilt voordat u tooAzure implementeert, kan Hallo Web API-project lokaal uitvoeren, Ga toohello URL waarmee Hallo Swagger JSON-bestand, Hallo-bestand opslaan en hello gebruiken **Selecteer een bestaand bestand Swagger-metagegevens**optie.
   > 
   > 
5. In Hallo **Add REST API Client** in het dialoogvenster, klikt u op **OK**.
   
    Visual Studio maakt een map met de naam van Hallo API-app en genereert clientklassen.
   
    ![Codebestanden voor gegenereerde client](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. Open in het project ToDoListAPI hello *Controllers\ToDoListController.cs* toosee Hallo code op de regel 40 die Hallo-API aanroept met behulp van de client Hallo gegenereerd.
   
    Hallo volgende fragment toont hoe Hallo code Hallo clientobject instantieert en aanroepen Hallo Get-methode.
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    Hallo-constructorparameter haalt Hallo eindpunt-URL van Hallo `toDoListDataAPIURL` app-instelling. In Hallo Web.config-bestand wordt die waarde set toohello lokale IIS Express URL Hallo API project, zodat u de toepassing hello lokaal kunt uitvoeren. Als u Hallo constructorparameter weglaat, is het standaardeindpunt Hallo Hallo-URL die u hebt gegenereerd Hallo code uit.
7. De clientklasse wordt gegenereerd met een andere naam op basis van de naam van uw API-app; Hallo-code in wijzigen *Controllers\ToDoListController.cs* zodat hello typenaam overeenkomt met wat in uw project is gegenereerd. Als de naam van uw API-app bijvoorbeeld ToDoListDataAPI071316 is, zou u deze code wijzigen:
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

toothis:

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a>Een API-app toohost Hallo middelste laag maken
Eerder u [Hallo gegevens laag API-app gemaakt en geïmplementeerd code tooit](#createapiapp).  Nu u Hallo Volg dezelfde procedure voor de middelste laag API-app Hallo.

1. In **Solution Explorer**, klik met de rechtermuisknop Hallo middelste laag ToDoListAPI-project (geen Hallo gegevenslaag ToDoListDataAPI) en klik vervolgens op **publiceren**.
   
    ![Klikken op Publish in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. In Hallo **profiel** tabblad Hallo **webpublicatie** wizard, klikt u op **Microsoft Azure App Service**.
3. In Hallo **App Service** in het dialoogvenster, klikt u op **nieuw**.
4. In Hallo **Hosting** tabblad Hallo **Create App Service** dialoogvenster vak, accepteer de standaardinstelling Hallo **API App Name** of geef een naam die uniek is in Hallo  *azurewebsites.NET* domein.
5. Kies hello Azure **abonnement** u hebt gebruikt.
6. In Hallo **resourcegroep** vervolgkeuzelijst, kiest u Hallo dezelfde resourcegroep die u eerder hebt gemaakt.
7. In Hallo **App Service-abonnement** vervolgkeuzelijst, kiest u Hallo hetzelfde abonnement dat u eerder hebt gemaakt. Wordt standaard toothat waarde.
8. Klik op **Create**.
   
    Visual Studio maakt Hallo API-app, maakt er een publicatieprofiel voor en geeft weer Hallo **verbinding** stap Hallo **webpublicatie** wizard.
9. In Hallo **verbinding** stap Hallo **webpublicatie** wizard, klikt u op **publiceren**.
   
   Visual Studio Hallo ToDoListAPI-project toohello nieuwe API-app implementeert en een URL van de browser toohello van Hallo API-app wordt geopend. Hallo 'is gemaakt' pagina wordt weergegeven.

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a>Hallo middelste laag toocall Hallo-gegevenslaag configureren
Als u de API-app voor Hallo middelste laag nu aangeroepen, probeert deze toocall Hallo-gegevenslaag met Hallo localhost-URL die wordt nog steeds Hallo Web.config-bestand. In deze sectie voert u Hallo gegevens laag API-app-URL in een omgevingsinstelling in Hallo middelste laag API-app. Wanneer hello code in de middelste laag API-app Hallo Hallo gegevens laag URL-instelling ophaalt, overschrijft Hallo omgevingsinstelling wat is er in Hallo Web.config-bestand.

1. Ga toohello [Azure-portal](https://portal.azure.com/), en navigeert u vervolgens toohello **API-App** blade voor Hallo API-app die u hebt gemaakt project toohost Hallo-TodoListAPI (middelste laag).
2. Hallo in API-App **instellingen** blade, klikt u op **toepassingsinstellingen**.
3. Hallo in API-App **toepassingsinstellingen** blade, schuif omlaag toohello **appinstellingen** sectie en voeg de volgende Hallo sleutel en waarde. Hallo-waarde is Hallo-URL van Hallo eerste API-App die u in deze zelfstudie hebt gepubliceerd.
   
   | **Sleutel** | toDoListDataAPIURL |
   | --- | --- |
   | **Waarde** |https://{de naam van uw API-app voor de gegevenslaag}.azurewebsites.net |
   | **Voorbeeld** |https://todolistdataapi.azurewebsites.net |
4. Klik op **Opslaan**.
   
    ![Klikken op Opslaan in het gedeelte App-instellingen](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    Wanneer het Hallo-code wordt uitgevoerd in Azure, overschrijft deze waarde Hallo localhost-URL die zich in Hallo Web.config-bestand.

## <a name="test"></a>Test
1. Blader in een browservenster toohello-URL van Hallo nieuwe middelste laag API-app die u zojuist hebt gemaakt voor ToDoListAPI. U kunt er ophalen door te klikken op Hallo-URL in de hoofdblade Hallo API-app in Hallo-portal.
2. 'Swagger' toohello URL toevoegen in de adresbalk van Hallo browser en druk op Enter. (Hallo-URL is `http://{apiappname}.azurewebsites.net/swagger`.)
   
    Hallo browser geeft Hallo dezelfde Swagger-gebruikersinterface die u eerder hebt gezien voor ToDoListDataAPI, maar nu `owner` is niet een verplicht veld voor Hallo Get-bewerking, omdat Hallo middelste laag API-app voor u die waarde toohello API app voor de gegevenslaag verzendt. (Als u zelfstudies over verificatie volgt hello, stuurt Hallo middelste laag werkelijke gebruikers-id's voor Hallo `owner` parameter; voor nu er wordt hard-coding van een sterretje.)
3. Probeer Hallo Get-methode en hello andere methoden toovalidate die Hallo middelste laag API-app op correcte wijze aanroept Hallo gegevenslaag API-app.
   
    ![Get-methode van de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a>Problemen oplossen
Als u tijdens het doorlopen van deze zelfstudie tegen problemen aanloopt, vindt u hier enkele ideeën voor probleemoplossing.

* Zorg ervoor dat u de meest recente versie Hallo Hallo [Azure SDK voor .NET](http://go.microsoft.com/fwlink/?linkid=518003).
* Twee van de projectnamen Hallo zijn elkaar (ToDoListAPI, ToDoListDataAPI). Als dingen niet zo uitzien zoals beschreven in Hallo instructies wanneer u met een project werkt, zorg er dan voor dat u de juiste Hallo-project hebt geopend.
* Als u een bedrijfsnetwerk en toodeploy tooAzure App Service via een firewall probeert, zorg ervoor dat de poorten 443 en 8172 geopend voor Web Deploy zijn. Als u deze poorten niet kunt openen, gebruik dan een andere implementatiemethode.  Zie [implementeren van uw app tooAzure App Service](../app-service-web/web-sites-deploy.md).
* Fouten 'routenamen moeten uniek zijn'--mogelijk doen deze als u per ongeluk Hallo verkeerde project tooan API-app implementeren en vervolgens de juiste één tooit Hallo later implementeren. toocorrect deze, de implementatie opnieuw Hallo juiste project toohello API-app en op Hallo **instellingen** tabblad Hallo **webpublicatie** wizard selecteert **verwijderen van aanvullende bestanden op de bestemming**.

Nadat u uw ASP.NET-API-app uitgevoerd in Azure App Service hebt, kunt u toolearn meer over de functies van Visual Studio die probleemoplossing vereenvoudigen. Voor meer informatie over logboekregistratie, foutopsporing op afstand en meer raadpleegt u [Problemen met Azure App Service-apps in Visual Studio oplossen](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Volgende stappen
U hebt gezien hoe toodeploy bestaande Web-API-projecten tooAPI apps genereren van clientcode voor API-apps en API-apps vanuit .NET-clients gebruiken. Hallo volgende zelfstudie in deze reeks ziet u hoe te[CORS tooconsume API apps vanuit JavaScript-clients gebruiken](app-service-api-cors-consume-javascript.md).

Zie voor meer informatie over client-codegeneratie Hallo [Azure/AutoRest](https://github.com/azure/autorest) opslagplaats op GitHub.com. Voor hulp bij problemen met behulp van de client gegenereerd hello, opent u een [probleem in de AutoRest-opslagplaats Hallo](https://github.com/azure/autorest/issues).

Als u toocreate nieuwe API-app-projecten maken wilt, gebruikt u Hallo **Azure API-App** sjabloon.

![API-app-sjabloon in Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

Hallo **Azure API-App** projectsjabloon is gelijkwaardig toochoosing hello **leeg** ASP.NET 4.5.2-sjabloon sjabloon, te klikken op Hallo selectievakje tooadd Web API-ondersteuning en Hallo Swashbuckle NuGet-pakket installeert. Hallo-sjabloon wordt bovendien sommige Swashbuckle configuratie code ontworpen tooprevent Hallo maken van dubbele Swagger-bewerkings-id's toegevoegd. Als u een API-App-project hebt gemaakt, kunt u dit implementeren tooan API app Hallo dezelfde manier als u in deze zelfstudie hebt gezien.

