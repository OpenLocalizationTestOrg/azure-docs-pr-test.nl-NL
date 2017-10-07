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
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="64a8a-103">Een ASP.NET Core web-app maken in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="64a8a-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="64a8a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="64a8a-104">Overview</span></span>
<span data-ttu-id="64a8a-105">Deze zelfstudie laat zien hoe een ASP.NET Core toocreate web-app met behulp [Visual Studio Code (VS-Code)](http://code.visualstudio.com//Docs/whyvscode) en te implementeren[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="64a8a-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="64a8a-106">Hoewel dit artikel tooweb apps verwijst, geldt dit ook tooAPI apps en mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="64a8a-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="64a8a-107">ASP.NET Core is een belangrijke nieuwe opzet van ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="64a8a-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="64a8a-108">ASP.NET Core is een nieuw open source en platformoverschrijdende framework voor het bouwen van moderne cloud-gebaseerde WebApps met behulp van .NET.</span><span class="sxs-lookup"><span data-stu-id="64a8a-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="64a8a-109">Zie voor meer informatie [inleiding tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="64a8a-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="64a8a-110">Zie voor meer informatie over Azure App Service WebApps [overzicht van Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64a8a-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="64a8a-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="64a8a-111">Prerequisites</span></span>
* <span data-ttu-id="64a8a-112">Installeer [tegenover Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="64a8a-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="64a8a-113">Installeer Git - u kunt deze installeren via een van deze locaties: [Chocolatey](https://chocolatey.org/packages/git) of [git scm.com](http://git-scm.com/downloads). Als u nieuwe tooGit bent, kiest u [git scm.com](http://git-scm.com/downloads) en optie hello te**gebruik Git vanaf de opdrachtprompt van Windows hello**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="64a8a-114">Als u Git installeren, moet u ook tooset Hallo Git-gebruikersnaam en het e-mailadres als je later in de zelfstudie hello (bij het uitvoeren van een doorvoer van VS-Code).</span><span class="sxs-lookup"><span data-stu-id="64a8a-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="64a8a-115">Installeren van ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="64a8a-115">Install ASP.NET Core</span></span>
<span data-ttu-id="64a8a-116">ASP.NET Core is een lean .NET-stack voor het bouwen van moderne cloud- en web-apps die worden uitgevoerd op OS X, Linux en Windows.</span><span class="sxs-lookup"><span data-stu-id="64a8a-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="64a8a-117">Het is gemaakt van Hallo gemalen up tooprovide een geoptimaliseerde ontwikkelframework voor apps die zijn beide geïmplementeerde toohello cloud of on-premises uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="64a8a-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="64a8a-118">Deze bestaat uit modulaire onderdelen met een minimale overhead, zodat u de flexibiliteit behouden tijdens het bouwen van uw oplossingen.</span><span class="sxs-lookup"><span data-stu-id="64a8a-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="64a8a-119">Deze zelfstudie is ontworpen tooget toepassingen maken met de meest recente ontwikkeling versies van ASP.NET Core Hallo is gestart.</span><span class="sxs-lookup"><span data-stu-id="64a8a-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="64a8a-120">Hallo-instructies zijn specifiek tooWindows.</span><span class="sxs-lookup"><span data-stu-id="64a8a-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="64a8a-121">Zie voor installatie-instructies voor OS X, Linux en Windows [aan de slag met ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="64a8a-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="64a8a-122">Zie voor meer installatie-instructies voor OS X, Linux en Windows, [installeren van ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="64a8a-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="64a8a-123">Hallo-web-app maken</span><span class="sxs-lookup"><span data-stu-id="64a8a-123">Create hello web app</span></span>
<span data-ttu-id="64a8a-124">Deze sectie wordt beschreven hoe een nieuwe ASP.NET-app tooscaffold web-app met Hallo .NET CLI-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="64a8a-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="64a8a-125">Hiermee voert u de volgende Hallo op Hallo opdrachtprompt toocreate Hallo project map en scaffold Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="64a8a-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![CLI - generator van ASP.NET Core DotNet](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="64a8a-127">toorestore hello nodig NuGet-pakketten Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="64a8a-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="64a8a-128">Hallo-web-app lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="64a8a-128">Run hello web app locally</span></span>
<span data-ttu-id="64a8a-129">Nu dat u hebt gemaakt Hallo web-app en alle Hallo NuGet-pakketten voor Hallo app opgehaald, kunt u Hallo web-app lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="64a8a-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="64a8a-130">Hallo-app uitvoeren (Hallo `dotnet run` opdracht bouwt Hallo app wanneer deze verouderd is):</span><span class="sxs-lookup"><span data-stu-id="64a8a-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="64a8a-131">Open een browser en ga toohello URL te volgen.</span><span class="sxs-lookup"><span data-stu-id="64a8a-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="64a8a-132">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="64a8a-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="64a8a-133">Hallo standaardpagina van web-app Hallo verschijnt.</span><span class="sxs-lookup"><span data-stu-id="64a8a-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![Lokale web-app in een browser](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="64a8a-135">Sluit uw browser.</span><span class="sxs-lookup"><span data-stu-id="64a8a-135">Close your browser.</span></span> <span data-ttu-id="64a8a-136">In Hallo **opdrachtvenster**, drukt u op **Ctrl + C** tooshut toepassing hello en sluiten Hallo **opdrachtvenster**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="64a8a-137">Een web-app maken in hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="64a8a-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="64a8a-138">Hallo leidt volgt u door een web-app maken in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="64a8a-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="64a8a-139">Meld u bij toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64a8a-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="64a8a-140">Klik op **nieuw** op Hallo linksboven Hallo Portal.</span><span class="sxs-lookup"><span data-stu-id="64a8a-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="64a8a-141">Klik op **Web-Apps > Web-App**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-141">Click **Web Apps > Web App**.</span></span>
   
    ![Azure nieuwe web-app](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="64a8a-143">Voer een waarde voor **naam**, zoals **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="64a8a-144">Houd er rekening mee dat deze naam toobe uniek moet en Hallo portal dat afdwingen wanneer u tooenter Hallo naam probeert.</span><span class="sxs-lookup"><span data-stu-id="64a8a-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="64a8a-145">Dus als u een Voer een andere waarde selecteert, moet u toosubstitute die waarde voor elk exemplaar van **SampleWebAppDemo** die u ziet in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="64a8a-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="64a8a-146">Selecteer een bestaande **App Service-Plan** of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="64a8a-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="64a8a-147">Als u een nieuw plan maakt, selecteert u Hallo prijscategorie, locatie, en andere opties.</span><span class="sxs-lookup"><span data-stu-id="64a8a-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="64a8a-148">Zie voor meer informatie over App Service-abonnementen Hallo artikel [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64a8a-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Azure blade voor nieuwe web-app](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="64a8a-150">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-150">Click **Create**.</span></span>
   
    ![blade web-app](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="64a8a-152">Git-publicatie voor de nieuwe web-app Hallo inschakelen</span><span class="sxs-lookup"><span data-stu-id="64a8a-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="64a8a-153">GIT is een gedistribueerd versiebeheersysteem waarmee u toodeploy uw Azure App Service-web-app kunt.</span><span class="sxs-lookup"><span data-stu-id="64a8a-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="64a8a-154">U Hallo code voor uw web-app in een lokale Git-opslagplaats schrijven wilt opslaan en implementeert u uw code tooAzure door tooa externe opslagplaats pushen.</span><span class="sxs-lookup"><span data-stu-id="64a8a-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="64a8a-155">Meld u aan bij Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64a8a-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="64a8a-156">Klik op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-156">Click **Browse**.</span></span>
3. <span data-ttu-id="64a8a-157">Klik op **Web-Apps** tooview een lijst met Hallo web-apps die zijn gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="64a8a-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="64a8a-158">Selecteer Hallo WebApp die u in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64a8a-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="64a8a-159">Hallo blade web-app klikt u op **instellingen** > **continue implementatie**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Azure-web-app host](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="64a8a-161">Klik op **bron kiezen > lokale Git-opslagplaats**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="64a8a-162">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-162">Click **OK**.</span></span>
   
    ![Azure lokale Git-opslagplaats](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="64a8a-164">Als u hebt geen eerder implementatiereferenties voor het publiceren van een web-app of een andere App Service-app hebt ingesteld, ze nu instellen:</span><span class="sxs-lookup"><span data-stu-id="64a8a-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="64a8a-165">Klik op **instellingen** > **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="64a8a-166">Hallo **implementatiereferenties instellen** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="64a8a-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="64a8a-167">Maak een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="64a8a-167">Create a user name and password.</span></span>  <span data-ttu-id="64a8a-168">U hebt dit wachtwoord later nodig bij het instellen van Git.</span><span class="sxs-lookup"><span data-stu-id="64a8a-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="64a8a-169">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-169">Click **Save**.</span></span>
9. <span data-ttu-id="64a8a-170">Klik op de blade van uw web-app **instellingen > eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="64a8a-171">Hallo-URL van Hallo externe Git-opslagplaats die u die wordt weergegeven implementeert onder toois **GIT-URL**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="64a8a-172">Kopiëren Hallo **GIT-URL** voor later gebruik in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="64a8a-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![Azure Git-URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="64a8a-174">Publiceren van uw web-app tooAzure App Service</span><span class="sxs-lookup"><span data-stu-id="64a8a-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="64a8a-175">In deze sectie maakt een lokale Git-opslagplaats en push vanuit die opslagplaats tooAzure toodeploy uw web-app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="64a8a-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="64a8a-176">Selecteer in de Code van de VS, Hallo **Git** optie in de linkernavigatiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="64a8a-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![GIT-pictogram in VS-Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="64a8a-178">Selecteer **initialiseren git-opslagplaats** toomake ervoor dat uw werkruimte is onder git-bronbeheer.</span><span class="sxs-lookup"><span data-stu-id="64a8a-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![Git geïnitialiseerd](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="64a8a-180">Hallo-opdrachtvenster openen en wijzig de mappen toohello map van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="64a8a-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="64a8a-181">Voer de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="64a8a-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="64a8a-182">Met deze opdracht voorkomt u dat een probleem over tekst waar CRLF uitgangen en LF uitgangen zijn betrokken.</span><span class="sxs-lookup"><span data-stu-id="64a8a-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="64a8a-183">In de Code van de VS, een commit-bericht toevoegen en klik op Hallo **doorvoeren alle** vinkje.</span><span class="sxs-lookup"><span data-stu-id="64a8a-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![GIT alle doorvoeren](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="64a8a-185">Nadat de Git is verwerkt, ziet u dat er zijn geen bestanden die worden vermeld in Hallo Git venster onder **wijzigingen**.</span><span class="sxs-lookup"><span data-stu-id="64a8a-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![GIT geen wijzigingen](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="64a8a-187">Wijzig back toohello opdrachtvenster waar Hallo opdrachtprompt toohello map verwijst waarin uw web-app zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="64a8a-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="64a8a-188">Maak een externe verwijzing voor het pushen van updates tooyour web-app met behulp van Hallo Git-URL (eindigend op '.git') die u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="64a8a-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="64a8a-189">Git toosave uw referenties lokaal zodanig configureren dat ze automatisch toegevoegd tooyour push opdrachten gegenereerd op basis van de VS-Code worden.</span><span class="sxs-lookup"><span data-stu-id="64a8a-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="64a8a-190">Uw tooAzure wijzigingen door te voeren opdracht volgende Hallo push.</span><span class="sxs-lookup"><span data-stu-id="64a8a-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="64a8a-191">Na deze eerste push tooAzure, kunt u zich kunt toodo alle Hallo push in VS-Code opdrachten.</span><span class="sxs-lookup"><span data-stu-id="64a8a-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="64a8a-192">U wordt gevraagd om Hallo wachtwoord die u eerder in Azure gemaakt.</span><span class="sxs-lookup"><span data-stu-id="64a8a-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="64a8a-193">**Opmerking: Uw wachtwoord wordt niet meer zichtbaar.**</span><span class="sxs-lookup"><span data-stu-id="64a8a-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="64a8a-194">Hallo-uitvoer van Hallo hierboven opdracht eindigt met een bericht dat de implementatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="64a8a-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="64a8a-195">Als u wijzigingen tooyour app maakt, kunt u opnieuw publiceren rechtstreeks in VS-Code Hallo ingebouwde Git-functionaliteit met door het selecteren van Hallo **alle doorvoeren** optie gevolgd door Hallo **Push** optie.</span><span class="sxs-lookup"><span data-stu-id="64a8a-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="64a8a-196">Vindt u Hallo **Push** optie beschikbaar in Hallo vervolgkeuzelijst volgende toohello **alle doorvoeren** en **vernieuwen** knoppen.</span><span class="sxs-lookup"><span data-stu-id="64a8a-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="64a8a-197">Als u toocollaborate aan een project nodig hebt, kunt u overwegen tooGitHub Between pushen tooAzure worden gepusht.</span><span class="sxs-lookup"><span data-stu-id="64a8a-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="64a8a-198">Hallo-app in Azure uitvoeren</span><span class="sxs-lookup"><span data-stu-id="64a8a-198">Run hello app in Azure</span></span>
<span data-ttu-id="64a8a-199">Nu dat u uw web-app hebt geïmplementeerd, gaan we Hallo app terwijl gehost in Azure worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="64a8a-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="64a8a-200">Dit kan op twee manieren doen:</span><span class="sxs-lookup"><span data-stu-id="64a8a-200">This can be done in two ways:</span></span>

* <span data-ttu-id="64a8a-201">Open een browser en Voer Hallo-naam van uw web-app als volgt.</span><span class="sxs-lookup"><span data-stu-id="64a8a-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="64a8a-202">In Azure Portal hello, zoekt Hallo-blade web-app voor uw web-app en klikt u op **Bladeren** tooview uw app</span><span class="sxs-lookup"><span data-stu-id="64a8a-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="64a8a-203">in de browser.</span><span class="sxs-lookup"><span data-stu-id="64a8a-203">in your default browser.</span></span>

![Azure-web-app](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="64a8a-205">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="64a8a-205">Summary</span></span>
<span data-ttu-id="64a8a-206">In deze zelfstudie hebt u geleerd hoe toocreate een web-app in VS-Code en deze tooAzure implementeren.</span><span class="sxs-lookup"><span data-stu-id="64a8a-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="64a8a-207">Zie voor meer informatie over tegenover Code Hallo artikel [waarom Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="64a8a-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="64a8a-208">Zie voor meer informatie over App Service WebApps [overzicht van Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64a8a-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

