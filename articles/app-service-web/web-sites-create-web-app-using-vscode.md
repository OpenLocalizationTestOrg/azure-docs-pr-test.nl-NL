---
title: Een ASP.NET Core web-app maken in Visual Studio Code
description: Deze zelfstudie ziet u hoe u een ASP.NET Core web-app met behulp van Visual Studio Code maakt.
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
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Een ASP.NET Core web-app maken in Visual Studio Code
## <a name="overview"></a>Overzicht
Deze zelfstudie ziet u het maken van een ASP.NET Core web app met behulp van [Visual Studio Code (VS-Code)](http://code.visualstudio.com//Docs/whyvscode) en implementeert [Azure App Service](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Hoewel dit artikel naar web-apps verwijst, is het ook van toepassing op API Apps en mobiele apps. 
> 
> 

ASP.NET Core is een belangrijke nieuwe opzet van ASP.NET. ASP.NET Core is een nieuw open source en platformoverschrijdende framework voor het bouwen van moderne cloud-gebaseerde WebApps met behulp van .NET. Zie voor meer informatie [Inleiding tot ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Zie voor meer informatie over Azure App Service WebApps [overzicht van Web Apps](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Vereisten
* Installeer [tegenover Code](http://code.visualstudio.com/Docs/setup).
* Installeer Git - u kunt deze installeren via een van deze locaties: [Chocolatey](https://chocolatey.org/packages/git) of [git scm.com](http://git-scm.com/downloads). Als u niet bekend met Git bent, kiest u [git scm.com](http://git-scm.com/downloads) en selecteer de optie voor **gebruik Git vanaf de opdrachtprompt van Windows**. Zodra u Git installeert, moet u ook de Git-gebruikersnaam en e-dit verderop in de zelfstudie vereist (bij het uitvoeren van een doorvoer van VS-Code).  

## <a name="install-aspnet-core"></a>Installeren van ASP.NET Core
ASP.NET Core is een lean .NET-stack voor het bouwen van moderne cloud- en web-apps die worden uitgevoerd op OS X, Linux en Windows. Deze is opgebouwd compleet voor een geoptimaliseerde ontwikkelframework voor apps die worden geïmplementeerd naar de cloud of on-premises uitgevoerd. Deze bestaat uit modulaire onderdelen met een minimale overhead, zodat u de flexibiliteit behouden tijdens het bouwen van uw oplossingen.

Deze zelfstudie is ontworpen om u op weg toepassingen maken met de nieuwste versies van de ontwikkeling van ASP.NET Core. De volgende instructies zijn specifiek voor Windows. Zie voor installatie-instructies voor OS X, Linux en Windows [aan de slag met ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started). 


> [!NOTE]
> Zie voor meer installatie-instructies voor OS X, Linux en Windows, [installeren van ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx). 
> 
> 

## <a name="create-the-web-app"></a>De web-app maken
Deze sectie wordt beschreven hoe u ondersteuning van een nieuwe app ASP.NET web-app met behulp van de .NET-CLI-hulpprogramma. 

1. Typ het volgende achter de opdrachtprompt voor het maken van de projectmap en ondersteuning van de app.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![CLI - generator van ASP.NET Core DotNet](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. Voer de volgende opdracht voor het herstellen van de benodigde NuGet-pakketten:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a>De web-app lokaal uitvoeren
Nu dat u hebt gemaakt van de web-app en de NuGet-pakketten voor de app opgehaald, kunt u de web-app lokaal uitvoeren.

1. Voer de app (de `dotnet run` opdracht wordt de app bouwen wanneer deze verouderd is):
    ```terminal
    dotnet run
    ```
2. Open een browser en Ga naar de volgende URL.
   
    **http://localhost:5000**
   
    De standaardpagina van de web-app wordt als volgt weergegeven.
   
    ![Lokale web-app in een browser](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Sluit uw browser. In de **opdrachtvenster**, drukt u op **Ctrl + C** afsluiten van de toepassing en sluit de **opdrachtvenster**. 

## <a name="create-a-web-app-in-the-azure-portal"></a>Een web-app maken in de Azure-Portal
De volgende stappen begeleidt u bij het maken van een web-app in de Azure-Portal.

1. Meld u aan bij de [Azure Portal](https://portal.azure.com).
2. Klik op **nieuw** links aan de bovenkant van de Portal.
3. Klik op **Web-Apps > Web-App**.
   
    ![Azure nieuwe web-app](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. Voer een waarde voor **naam**, zoals **SampleWebAppDemo**. Merk op dat deze naam moet uniek en de portal wordt afdwingen dat wanneer u probeert de naam te geven. Dus als u een Voer een andere waarde selecteert, moet u die waarde voor elk exemplaar van vervangende **SampleWebAppDemo** die u ziet in deze zelfstudie. 
5. Selecteer een bestaande **App Service-Plan** of maak een nieuwe. Als u een nieuw plan maakt, selecteert u de prijscategorie, locatie en andere opties. Zie het artikel voor meer informatie over App Service-abonnementen [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Azure blade voor nieuwe web-app](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. Klik op **Create**.
   
    ![blade web-app](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a>Git-publicatie voor de nieuwe web-app inschakelen
GIT is een gedistribueerd versiebeheersysteem waarmee u kunt uw Azure App Service-web-app implementeren. U slaat de code die u voor uw web-app schrijft, op in een lokale Git-opslagplaats en u implementeert uw code in Azure door deze naar een externe opslagplaats te pushen.   

1. Meld u aan bij de [Azure-Portal](https://portal.azure.com).
2. Klik op **Bladeren**.
3. Klik op **Web-Apps** om een lijst met de web-apps die zijn gekoppeld aan uw Azure-abonnement weer te geven.
4. Selecteer de web-app die u in deze zelfstudie hebt gemaakt.
5. Klik in de blade web-app op **instellingen** > **continue implementatie**. 
   
    ![Azure-web-app host](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Klik op **bron kiezen > lokale Git-opslagplaats**.
7. Klik op **OK**.
   
    ![Azure lokale Git-opslagplaats](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Als u hebt geen eerder implementatiereferenties voor het publiceren van een web-app of een andere App Service-app hebt ingesteld, ze nu instellen:
   
   * Klik op **instellingen** > **implementatiereferenties**. De **implementatiereferenties instellen** blade wordt weergegeven.
   * Maak een gebruikersnaam en wachtwoord.  U hebt dit wachtwoord later nodig bij het instellen van Git.
   * Klik op **Opslaan**.
9. Klik op de blade van uw web-app **instellingen > eigenschappen**. De URL van de externe Git-opslagplaats die u implementeert op die wordt weergegeven onder **GIT-URL**.
10. Kopieer de **GIT-URL** voor later gebruik in de zelfstudie.
    
    ![Azure Git-URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a>Publiceren van uw web-app in Azure App Service
In deze sectie maakt u een lokale Git-opslagplaats en push vanuit die opslagplaats naar Azure voor het implementeren van uw web-app in Azure.

1. Selecteer in VS-Code, de **Git** optie in de linkernavigatiebalk.
   
    ![GIT-pictogram in VS-Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Selecteer **initialiseren git-opslagplaats** om ervoor te zorgen dat uw werkruimte is onder git-bronbeheer. 
   
    ![Git geïnitialiseerd](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Open het opdrachtvenster en wijzig de mappen in de map van uw web-app. Voer de volgende opdracht:
   
        git config core.autocrlf false
   
    Met deze opdracht voorkomt u dat een probleem over tekst waar CRLF uitgangen en LF uitgangen zijn betrokken.
4. In de Code van de VS, een commit-bericht toevoegen en klik op de **doorvoeren alle** vinkje.
   
    ![GIT alle doorvoeren](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Nadat de Git is verwerkt, ziet u dat er zijn geen bestanden die worden weergegeven in het venster Git onder **wijzigingen**. 
   
    ![GIT geen wijzigingen](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Wijzig weer in het opdrachtvenster waar de opdrachtprompt naar de map verwijst waarin uw web-app zich bevindt.
7. Maak een externe verwijzing voor om updates te pushen naar uw web-app met behulp van de Git-URL (eindigend op '.git') die u eerder hebt gekopieerd.
   
        git remote add azure [URL for remote repository]
8. Configureer Git om uw referenties lokaal opslaan zodat ze automatisch worden toegevoegd aan uw opdrachten push is gegenereerd op basis van de VS-Code.
   
        git config credential.helper store
9. Pusht u uw wijzigingen naar Azure met de volgende opdracht. Na deze eerste push naar Azure, kunt u zich kunt alle push-opdrachten uitvoeren vanuit VS-Code. 
   
        git push -u azure master
   
    U wordt gevraagd om het wachtwoord dat u eerder in Azure gemaakt. **Opmerking: Uw wachtwoord wordt niet meer zichtbaar.**
   
    De uitvoer van de bovenstaande opdracht eindigt met een bericht dat de implementatie geslaagd is.
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Als u wijzigingen aan uw app aanbrengt, kunt u opnieuw publiceren rechtstreeks in VS-Code door te selecteren met behulp van de ingebouwde functionaliteit voor Git de **alle doorvoeren** optie gevolgd door de **Push** optie. U vindt de **Push** optie beschikbaar in de vervolgkeuzelijst naast de **alle doorvoeren** en **vernieuwen** knoppen.
> 
> 

Als u samenwerken aan een project wilt, moet u rekening houden met GitHub worden gepusht Between pushen naar Azure.

## <a name="run-the-app-in-azure"></a>De app in Azure uitvoeren
Nu dat u uw web-app hebt geïmplementeerd, gaan we de app terwijl gehost in Azure worden uitgevoerd. 

Dit kan op twee manieren doen:

* Open een browser en voer de naam van uw web-app als volgt.   
  
        http://SampleWebAppDemo.azurewebsites.net
* Ga naar de blade web-app voor uw web-app in de Azure-Portal en klikt u op **Bladeren** om weer te geven van uw app 
* in de browser.

![Azure-web-app](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Samenvatting
In deze zelfstudie hebt u geleerd hoe u een web-app in VS-Code maken en deze implementeren in Azure. Raadpleeg het artikel voor meer informatie over de Code van de VS, [waarom Visual Studio Code?](https://code.visualstudio.com/Docs/) Zie voor meer informatie over App Service WebApps [overzicht van Web Apps](app-service-web-overview.md). 

