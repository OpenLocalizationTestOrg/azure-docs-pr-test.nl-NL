---
title: aaaDeploy WebJobs met Visual Studio
description: Meer informatie over hoe toodeploy Azure WebJobs tooAzure App Service Web Apps met Visual Studio.
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a>WebJobs implementeren met Visual Studio
## <a name="overview"></a>Overzicht
Dit onderwerp wordt uitgelegd hoe toouse Visual Studio toodeploy een consoletoepassing tooa web-app in project [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) als een [Azure webtaak](http://go.microsoft.com/fwlink/?LinkId=390226). Voor informatie over hoe toodeploy WebJobs met behulp van Hallo [Azure Portal](https://portal.azure.com), Zie [achtergrondtaken uitvoeren met de WebJobs](web-sites-create-web-jobs.md).

Visual Studio een consoletoepassing webtaken ingeschakeld-project implementeert, worden twee taken uitgevoerd:

* Kopieën runtime toohello geschikte map in Hallo web-app-bestanden (*App_Data/taken/continue* voor doorlopende webtaken *App_Data/taken/geactiveerd* voor geplande en on-demand WebJobs).
* Stelt [Azure Scheduler-taken](#scheduler) voor WebJobs die geplande toorun op bepaalde tijden zijn. (Dit is niet nodig voor doorlopende webtaken.)

Een project WebJobs ingeschakeld heeft Hallo items toegevoegde tooit te volgen:

* Hallo [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet-pakket.
* Een [webtaak-publiceren settings.json](#publishsettings) -bestand met de implementatie en de scheduler-instellingen. 

![Diagram van wat tooa consoletoepassing tooenable implementatie als een webtaak is toegevoegd](./media/websites-dotnet-deploy-webjobs/convert.png)

U kunt deze items tooan bestaande consoletoepassingsproject toevoegen of gebruik een sjabloon toocreate een nieuw project voor de consoletoepassing WebJobs ingeschakeld. 

U kunt een project implementeert als een webtaak zelfstandig of een koppeling tooa webproject zodat deze automatisch wordt geïmplementeerd wanneer u Hallo-webproject implementeert. toolink projecten, Visual Studio bevat Hallo-naam van Hallo webtaken ingeschakeld project in een [webjobs list.json](#webjobslist) bestand in het Hallo-webproject.

![Diagram van webtaak project tooweb project koppelen](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>Vereisten
API-functies voor implementatie zijn beschikbaar in Visual Studio wanneer u hello Azure SDK voor .NET installeert:

* [Azure SDK voor .NET (Visual Studio)](https://azure.microsoft.com/downloads/).

## <a id="convert"></a>WebJobs-implementatie voor een bestaande consoletoepassingsproject inschakelen
U hebt hiervoor twee opties:

* [Schakel automatische implementatie met een webproject](#convertlink).
  
    Een bestaand project in de Console-toepassing zodanig configureren dat deze automatisch wordt geïmplementeerd als een webtaak wanneer u een webproject implementeert. Gebruik deze optie als u wilt dat toorun uw webtaak in Hallo dezelfde web-app waarin u Hallo uitvoeren gerelateerde webtoepassing.
* [Implementatie zonder een webproject inschakelen](#convertnolink).
  
    Configureer een bestaande Console Application project toodeploy als een webtaak zelfstandig gebruikt, met geen koppeling tooa webproject. Gebruik deze optie als u toorun een webtaak in een web-app wilt zelfstandig gebruikt, met geen webtoepassing in Hallo web-app wordt uitgevoerd. U kunt toodo dit in volgorde toobe kunnen tooscale uw resources webtaak onafhankelijk van uw webtoepassingsbronnen.

### <a id="convertlink"></a>Automatische WebJobs-implementatie met een webproject inschakelen
1. Klik met de rechtermuisknop Hallo-webproject in **Solution Explorer**, en klik vervolgens op **toevoegen** > **bestaand Project als Azure webtaak**.
   
    ![Bestaand Project als Azure webtaak](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    Hallo [toevoegen Azure webtaak](#configure) dialoogvenster wordt weergegeven.
2. In Hallo **projectnaam** vervolgkeuzelijst, selecteer Hallo consoletoepassing project tooadd als een webtaak.
   
    ![Project selecteren in het dialoogvenster Azure webtaak toevoegen](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. Volledige Hallo [toevoegen Azure webtaak](#configure) dialoogvenster en klik vervolgens op **OK**. 

### <a id="convertnolink"></a>WebJobs-implementatie zonder een webproject inschakelen
1. Klik met de rechtermuisknop Hallo consoletoepassingsproject in **Solution Explorer**, en klik vervolgens op **publiceren als Azure webtaak...** . 
   
    ![Als Azure webtaak publiceren](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    Hallo [toevoegen Azure webtaak](#configure) dialoogvenster wordt weergegeven, met Hallo project is geselecteerd in Hallo **projectnaam** vak.
2. Volledige Hallo [toevoegen Azure webtaak](#configure) in het dialoogvenster en klik vervolgens op **OK**.
   
   Hallo **webpublicatie** wizard wordt weergegeven.  Als u toopublish niet onmiddellijk wilt, kunt u Hallo wizard sluiten. Hallo-instellingen die u hebt ingevoerd voor worden opgeslagen wanneer u dat te wilt[Hallo-project implementeert](#deploy).

## <a id="create"></a>Maak een nieuw project voor WebJobs ingeschakeld
toocreate een nieuw project voor webtaken is ingeschakeld, kunt u Hallo Console project sjabloon en schakel webtaken toepassingsimplementatie zoals toegelicht in [Hallo van de vorige sectie](#convert). Als alternatief kunt u Hallo webtaken nieuw project sjabloon:

* [Hallo webtaken nieuw project-sjabloon gebruiken voor een onafhankelijke webtaak](#createnolink)
  
    Een project maken en configureren toodeploy zelfstandig als een webtaak, met geen koppeling tooa webproject. Gebruik deze optie als u toorun een webtaak in een web-app wilt zelfstandig gebruikt, met geen webtoepassing in Hallo web-app wordt uitgevoerd. U kunt toodo dit in volgorde toobe kunnen tooscale uw resources webtaak onafhankelijk van uw webtoepassingsbronnen.
* [Hallo webtaken nieuw project-sjabloon gebruiken voor een webtaak gekoppelde tooa-webproject](#createlink)
  
    Een project maken dat geconfigureerde toodeploy automatisch als een webtaak wanneer een webproject in Hallo dezelfde oplossing is geïmplementeerd. Gebruik deze optie als u wilt dat toorun uw webtaak in Hallo dezelfde web-app waarin u Hallo uitvoeren gerelateerde webtoepassing.

> [!NOTE]
> Hallo webtaken nieuw project sjabloon automatisch NuGet-pakketten worden geïnstalleerd en bevat een code in *Program.cs* voor Hallo [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs). Als u niet toouse hello WebJobs SDK wilt, verwijderen of wijzigen van Hallo `host.RunAndBlock` -instructie in *Program.cs*.
> 
> 

### <a id="createnolink"></a>Hallo webtaken nieuw project-sjabloon gebruiken voor een onafhankelijke webtaak
1. Klik op **bestand** > **nieuw Project**, en klik vervolgens in Hallo **nieuw Project** dialoogvenster vak Klik **Cloud**  >   **Azure webtaak (.NET Framework)**.
   
    ![Het dialoogvenster New Project webtaak sjabloon weergeven](./media/websites-dotnet-deploy-webjobs/np.png)
2. Volg Hallo-instructies hierboven te[Hallo consoletoepassingsproject een onafhankelijk WebJobs-project maken](#convertnolink).

### <a id="createlink"></a>Hallo webtaken nieuw project-sjabloon gebruiken voor een webtaak gekoppelde tooa-webproject
1. Klik met de rechtermuisknop Hallo-webproject in **Solution Explorer**, en klik vervolgens op **toevoegen** > **nieuwe Azure webtaak Project**.
   
    ![Nieuwe Azure webtaak Project menu-item](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    Hallo [toevoegen Azure webtaak](#configure) dialoogvenster wordt weergegeven.
2. Volledige Hallo [toevoegen Azure webtaak](#configure) in het dialoogvenster en klik vervolgens op **OK**.

## <a id="configure"></a>dialoogvenster voor Hello Azure webtaak toevoegen
Hallo **toevoegen Azure webtaak** dialoogvenster kunt u de naam van een webtaak Hallo en voert u de instelling voor uw webtaak uit. 

![Dialoogvenster Azure webtaak toevoegen](./media/websites-dotnet-deploy-webjobs/aaw2.png)

Hallo-velden in dit dialoogvenster komen overeen toofields op Hallo **nieuwe taak** dialoogvenster Hallo Azure-Portal. Zie voor meer informatie [achtergrondtaken uitvoeren met de WebJobs](web-sites-create-web-jobs.md).

> [!NOTE]
> * Zie voor meer informatie over de implementatie van het opdrachtregelprogramma [inschakelen vanaf de opdrachtregel of continue levering van Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).
> * Als u een webtaak implementeert en vervolgens besluit gewenste toochange Hallo type webtaak en opnieuw distribueren, moet u toodelete hello webjobs-publiceren settings.json bestand. Hiermee maakt u Visual Studio weergeven Hallo publicatieopties opnieuw, zodat u Hallo type webtaak kunt wijzigen.
> * Als u een webtaak implementeert en later wijzigen Hallo uitvoeringsmodus van continue toonon continue of omgekeerd, Visual Studio maakt een nieuwe webtaak in Azure wanneer u opnieuw implementeert. Als u andere schema-instellingen wijzigen, maar laat uitvoeren modus Hallo dezelfde of schakelen tussen geplande en op verzoek, Visual Studio-updates Hallo bestaande taak plaats van een nieuwe maken.
> 
> 

## <a id="publishsettings"></a>webtaak-publiceren settings.json
Wanneer u een consoletoepassing voor WebJobs-implementatie configureert, Visual Studio Hallo installeert [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet-pakket en winkels planningsgegevens in een *webtaak-publiceren settings.json*  bestand in Hallo project *eigenschappen* map van Hallo WebJobs project. Hier volgt een voorbeeld van het bestand:

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

U kunt dit bestand rechtstreeks bewerken en Visual Studio biedt IntelliSense. Hallo bestand schema wordt opgeslagen op [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) en er kan worden weergegeven.  

## <a id="webjobslist"></a>webjobs list.json
Als u een project WebJobs ingeschakeld tooa-webproject koppelt, Visual Studio slaat Hallo-naam van Hallo WebJobs-project in een *webjobs list.json* bestand in het Hallo-webproject *eigenschappen* map. Hallo lijst kan meerdere WebJobs projecten bevatten, zoals wordt weergegeven in het volgende voorbeeld Hallo:

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

U kunt dit bestand rechtstreeks bewerken en Visual Studio biedt IntelliSense. Hallo bestand schema wordt opgeslagen op [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) en er kan worden weergegeven.

## <a id="deploy"></a>Een API-project implementeert
Een API-project dat u hebt gekoppeld aan tooa-webproject implementeert automatisch met het Hallo-webproject. Zie voor meer informatie over de implementatie van web project [hoe toodeploy tooWeb Apps](web-sites-deploy.md).

toodeploy een API-project zelfstandig gebruikt, met de rechtermuisknop op Hallo-project in **Solution Explorer** en klik op **publiceren als Azure webtaak...** . 

![Als Azure webtaak publiceren](./media/websites-dotnet-deploy-webjobs/paw.png)

Voor een onafhankelijke webtaak Hallo dezelfde **webpublicatie** wizard die wordt gebruikt voor webprojecten wordt weergegeven, maar met minder instellingen beschikbaar toochange.

## <a id="nextsteps"></a>Volgende stappen
In dit artikel is beschreven hoe toodeploy WebJobs met behulp van Visual Studio. Voor meer informatie over hoe toodeploy Azure WebJobs zien [Azure WebJobs - aanbevolen Resources - implementatie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).

