---
title: een ASP.NET Core web-app in Visual Studio Code aaaCreate
description: Deze zelfstudie ziet u hoe een ASP.NET Core toocreate web-app met behulp van Visual Studio Code.
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Een ASP.NET Core web-app maken in Visual Studio Code
## <a name="overview"></a>Overzicht
Deze zelfstudie laat zien hoe een ASP.NET Core toocreate web-app met behulp [Visual Studio Code (VS-Code)](http://code.visualstudio.com//Docs/whyvscode) en te implementeren[Azure App Service](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Hoewel dit artikel tooweb apps verwijst, geldt dit ook tooAPI apps en mobiele apps. 
> 
> 

ASP.NET Core is een belangrijke nieuwe opzet van ASP.NET. ASP.NET Core is een nieuw open source en platformoverschrijdende framework voor het bouwen van moderne cloud-gebaseerde WebApps met behulp van .NET. Zie voor meer informatie [inleiding tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Zie voor meer informatie over Azure App Service WebApps [overzicht van Web Apps](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Vereisten
* Installeer [tegenover Code](http://code.visualstudio.com/Docs/setup).
* Installeer Git - u kunt deze installeren via een van deze locaties: [Chocolatey](https://chocolatey.org/packages/git) of [git scm.com](http://git-scm.com/downloads). Als u nieuwe tooGit bent, kiest u [git scm.com](http://git-scm.com/downloads) en optie hello te**gebruik Git vanaf de opdrachtprompt van Windows hello**. Als u Git installeren, moet u ook tooset Hallo Git-gebruikersnaam en het e-mailadres als je later in de zelfstudie hello (bij het uitvoeren van een doorvoer van VS-Code).  

## <a name="install-aspnet-core"></a>Installeren van ASP.NET Core
ASP.NET Core is een lean .NET-stack voor het bouwen van moderne cloud- en web-apps die worden uitgevoerd op OS X, Linux en Windows. Het is gemaakt van Hallo gemalen up tooprovide een geoptimaliseerde ontwikkelframework voor apps die zijn beide geïmplementeerde toohello cloud of on-premises uitgevoerd. Deze bestaat uit modulaire onderdelen met een minimale overhead, zodat u de flexibiliteit behouden tijdens het bouwen van uw oplossingen.

Deze zelfstudie is ontworpen tooget toepassingen maken met de meest recente ontwikkeling versies van ASP.NET Core Hallo is gestart. Hallo-instructies zijn specifiek tooWindows. Zie voor installatie-instructies voor OS X, Linux en Windows [aan de slag met ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started). 


> [!NOTE]
> Zie voor meer installatie-instructies voor OS X, Linux en Windows, [installeren van ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx). 
> 
> 

## <a name="create-hello-web-app"></a>Hallo-web-app maken
Deze sectie wordt beschreven hoe een nieuwe ASP.NET-app tooscaffold web-app met Hallo .NET CLI-hulpprogramma. 

1. Hiermee voert u de volgende Hallo op Hallo opdrachtprompt toocreate Hallo project map en scaffold Hallo-app.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![CLI - generator van ASP.NET Core DotNet](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore hello nodig NuGet-pakketten Hallo volgende opdracht uitvoeren:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>Hallo-web-app lokaal uitvoeren
Nu dat u hebt gemaakt Hallo web-app en alle Hallo NuGet-pakketten voor Hallo app opgehaald, kunt u Hallo web-app lokaal uitvoeren.

1. Hallo-app uitvoeren (Hallo `dotnet run` opdracht bouwt Hallo app wanneer deze verouderd is):
    ```terminal
    dotnet run
    ```
2. Open een browser en ga toohello URL te volgen.
   
    **http://localhost:5000**
   
    Hallo standaardpagina van web-app Hallo verschijnt.
   
    ![Lokale web-app in een browser](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Sluit uw browser. In Hallo **opdrachtvenster**, drukt u op **Ctrl + C** tooshut toepassing hello en sluiten Hallo **opdrachtvenster**. 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Een web-app maken in hello Azure Portal
Hallo leidt volgt u door een web-app maken in hello Azure-Portal.

1. Meld u bij toohello [Azure Portal](https://portal.azure.com).
2. Klik op **nieuw** op Hallo linksboven Hallo Portal.
3. Klik op **Web-Apps > Web-App**.
   
    ![Azure nieuwe web-app](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. Voer een waarde voor **naam**, zoals **SampleWebAppDemo**. Houd er rekening mee dat deze naam toobe uniek moet en Hallo portal dat afdwingen wanneer u tooenter Hallo naam probeert. Dus als u een Voer een andere waarde selecteert, moet u toosubstitute die waarde voor elk exemplaar van **SampleWebAppDemo** die u ziet in deze zelfstudie. 
5. Selecteer een bestaande **App Service-Plan** of maak een nieuwe. Als u een nieuw plan maakt, selecteert u Hallo prijscategorie, locatie, en andere opties. Zie voor meer informatie over App Service-abonnementen Hallo artikel [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Azure blade voor nieuwe web-app](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. Klik op **Create**.
   
    ![blade web-app](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>Git-publicatie voor de nieuwe web-app Hallo inschakelen
GIT is een gedistribueerd versiebeheersysteem waarmee u toodeploy uw Azure App Service-web-app kunt. U Hallo code voor uw web-app in een lokale Git-opslagplaats schrijven wilt opslaan en implementeert u uw code tooAzure door tooa externe opslagplaats pushen.   

1. Meld u aan bij Hallo [Azure Portal](https://portal.azure.com).
2. Klik op **Bladeren**.
3. Klik op **Web-Apps** tooview een lijst met Hallo web-apps die zijn gekoppeld aan uw Azure-abonnement.
4. Selecteer Hallo WebApp die u in deze zelfstudie hebt gemaakt.
5. Hallo blade web-app klikt u op **instellingen** > **continue implementatie**. 
   
    ![Azure-web-app host](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Klik op **bron kiezen > lokale Git-opslagplaats**.
7. Klik op **OK**.
   
    ![Azure lokale Git-opslagplaats](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Als u hebt geen eerder implementatiereferenties voor het publiceren van een web-app of een andere App Service-app hebt ingesteld, ze nu instellen:
   
   * Klik op **instellingen** > **implementatiereferenties**. Hallo **implementatiereferenties instellen** blade wordt weergegeven.
   * Maak een gebruikersnaam en wachtwoord.  U hebt dit wachtwoord later nodig bij het instellen van Git.
   * Klik op **Opslaan**.
9. Klik op de blade van uw web-app **instellingen > eigenschappen**. Hallo-URL van Hallo externe Git-opslagplaats die u die wordt weergegeven implementeert onder toois **GIT-URL**.
10. Kopiëren Hallo **GIT-URL** voor later gebruik in de zelfstudie Hallo.
    
    ![Azure Git-URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>Publiceren van uw web-app tooAzure App Service
In deze sectie maakt een lokale Git-opslagplaats en push vanuit die opslagplaats tooAzure toodeploy uw web-app tooAzure.

1. Selecteer in de Code van de VS, Hallo **Git** optie in de linkernavigatiebalk Hallo.
   
    ![GIT-pictogram in VS-Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Selecteer **initialiseren git-opslagplaats** toomake ervoor dat uw werkruimte is onder git-bronbeheer. 
   
    ![Git geïnitialiseerd](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Hallo-opdrachtvenster openen en wijzig de mappen toohello map van uw web-app. Voer de volgende opdracht Hallo:
   
        git config core.autocrlf false
   
    Met deze opdracht voorkomt u dat een probleem over tekst waar CRLF uitgangen en LF uitgangen zijn betrokken.
4. In de Code van de VS, een commit-bericht toevoegen en klik op Hallo **doorvoeren alle** vinkje.
   
    ![GIT alle doorvoeren](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Nadat de Git is verwerkt, ziet u dat er zijn geen bestanden die worden vermeld in Hallo Git venster onder **wijzigingen**. 
   
    ![GIT geen wijzigingen](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Wijzig back toohello opdrachtvenster waar Hallo opdrachtprompt toohello map verwijst waarin uw web-app zich bevindt.
7. Maak een externe verwijzing voor het pushen van updates tooyour web-app met behulp van Hallo Git-URL (eindigend op '.git') die u eerder hebt gekopieerd.
   
        git remote add azure [URL for remote repository]
8. Git toosave uw referenties lokaal zodanig configureren dat ze automatisch toegevoegd tooyour push opdrachten gegenereerd op basis van de VS-Code worden.
   
        git config credential.helper store
9. Uw tooAzure wijzigingen door te voeren opdracht volgende Hallo push. Na deze eerste push tooAzure, kunt u zich kunt toodo alle Hallo push in VS-Code opdrachten. 
   
        git push -u azure master
   
    U wordt gevraagd om Hallo wachtwoord die u eerder in Azure gemaakt. **Opmerking: Uw wachtwoord wordt niet meer zichtbaar.**
   
    Hallo-uitvoer van Hallo hierboven opdracht eindigt met een bericht dat de implementatie geslaagd is.
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Als u wijzigingen tooyour app maakt, kunt u opnieuw publiceren rechtstreeks in VS-Code Hallo ingebouwde Git-functionaliteit met door het selecteren van Hallo **alle doorvoeren** optie gevolgd door Hallo **Push** optie. Vindt u Hallo **Push** optie beschikbaar in Hallo vervolgkeuzelijst volgende toohello **alle doorvoeren** en **vernieuwen** knoppen.
> 
> 

Als u toocollaborate aan een project nodig hebt, kunt u overwegen tooGitHub Between pushen tooAzure worden gepusht.

## <a name="run-hello-app-in-azure"></a>Hallo-app in Azure uitvoeren
Nu dat u uw web-app hebt geïmplementeerd, gaan we Hallo app terwijl gehost in Azure worden uitgevoerd. 

Dit kan op twee manieren doen:

* Open een browser en Voer Hallo-naam van uw web-app als volgt.   
  
        http://SampleWebAppDemo.azurewebsites.net
* In Azure Portal hello, zoekt Hallo-blade web-app voor uw web-app en klikt u op **Bladeren** tooview uw app 
* in de browser.

![Azure-web-app](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Samenvatting
In deze zelfstudie hebt u geleerd hoe toocreate een web-app in VS-Code en deze tooAzure implementeren. Zie voor meer informatie over tegenover Code Hallo artikel [waarom Visual Studio Code?](https://code.visualstudio.com/Docs/) Zie voor meer informatie over App Service WebApps [overzicht van Web Apps](app-service-web-overview.md). 

