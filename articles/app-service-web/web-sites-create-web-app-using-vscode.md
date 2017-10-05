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
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="7b258-103">Een ASP.NET Core web-app maken in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7b258-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="7b258-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7b258-104">Overview</span></span>
<span data-ttu-id="7b258-105">Deze zelfstudie ziet u het maken van een ASP.NET Core web app met behulp van [Visual Studio Code (VS-Code)](http://code.visualstudio.com//Docs/whyvscode) en implementeert [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="7b258-105">This tutorial shows you how to create an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="7b258-106">Hoewel dit artikel naar web-apps verwijst, is het ook van toepassing op API Apps en mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="7b258-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="7b258-107">ASP.NET Core is een belangrijke nieuwe opzet van ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7b258-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="7b258-108">ASP.NET Core is een nieuw open source en platformoverschrijdende framework voor het bouwen van moderne cloud-gebaseerde WebApps met behulp van .NET.</span><span class="sxs-lookup"><span data-stu-id="7b258-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="7b258-109">Zie voor meer informatie [Inleiding tot ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="7b258-109">For more information, see [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="7b258-110">Zie voor meer informatie over Azure App Service WebApps [overzicht van Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b258-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="7b258-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b258-111">Prerequisites</span></span>
* <span data-ttu-id="7b258-112">Installeer [tegenover Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="7b258-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="7b258-113">Installeer Git - u kunt deze installeren via een van deze locaties: [Chocolatey](https://chocolatey.org/packages/git) of [git scm.com](http://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="7b258-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span></span> <span data-ttu-id="7b258-114">Als u niet bekend met Git bent, kiest u [git scm.com](http://git-scm.com/downloads) en selecteer de optie voor **gebruik Git vanaf de opdrachtprompt van Windows**.</span><span class="sxs-lookup"><span data-stu-id="7b258-114">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span></span> <span data-ttu-id="7b258-115">Zodra u Git installeert, moet u ook de Git-gebruikersnaam en e-dit verderop in de zelfstudie vereist (bij het uitvoeren van een doorvoer van VS-Code).</span><span class="sxs-lookup"><span data-stu-id="7b258-115">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="7b258-116">Installeren van ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7b258-116">Install ASP.NET Core</span></span>
<span data-ttu-id="7b258-117">ASP.NET Core is een lean .NET-stack voor het bouwen van moderne cloud- en web-apps die worden uitgevoerd op OS X, Linux en Windows.</span><span class="sxs-lookup"><span data-stu-id="7b258-117">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="7b258-118">Deze is opgebouwd compleet voor een geoptimaliseerde ontwikkelframework voor apps die worden geïmplementeerd naar de cloud of on-premises uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b258-118">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span></span> <span data-ttu-id="7b258-119">Deze bestaat uit modulaire onderdelen met een minimale overhead, zodat u de flexibiliteit behouden tijdens het bouwen van uw oplossingen.</span><span class="sxs-lookup"><span data-stu-id="7b258-119">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="7b258-120">Deze zelfstudie is ontworpen om u op weg toepassingen maken met de nieuwste versies van de ontwikkeling van ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7b258-120">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="7b258-121">De volgende instructies zijn specifiek voor Windows.</span><span class="sxs-lookup"><span data-stu-id="7b258-121">The following instructions are specific to Windows.</span></span> <span data-ttu-id="7b258-122">Zie voor installatie-instructies voor OS X, Linux en Windows [aan de slag met ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="7b258-122">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="7b258-123">Zie voor meer installatie-instructies voor OS X, Linux en Windows, [installeren van ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="7b258-123">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-the-web-app"></a><span data-ttu-id="7b258-124">De web-app maken</span><span class="sxs-lookup"><span data-stu-id="7b258-124">Create the web app</span></span>
<span data-ttu-id="7b258-125">Deze sectie wordt beschreven hoe u ondersteuning van een nieuwe app ASP.NET web-app met behulp van de .NET-CLI-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="7b258-125">This section shows you how to scaffold a new app ASP.NET web app using the .NET CLI tool.</span></span> 

1. <span data-ttu-id="7b258-126">Typ het volgende achter de opdrachtprompt voor het maken van de projectmap en ondersteuning van de app.</span><span class="sxs-lookup"><span data-stu-id="7b258-126">Enter the following at the command prompt to create the project folder and scaffold the app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![CLI - generator van ASP.NET Core DotNet](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="7b258-128">Voer de volgende opdracht voor het herstellen van de benodigde NuGet-pakketten:</span><span class="sxs-lookup"><span data-stu-id="7b258-128">To restore the necessary NuGet packages, run the following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a><span data-ttu-id="7b258-129">De web-app lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7b258-129">Run the web app locally</span></span>
<span data-ttu-id="7b258-130">Nu dat u hebt gemaakt van de web-app en de NuGet-pakketten voor de app opgehaald, kunt u de web-app lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7b258-130">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span></span>

1. <span data-ttu-id="7b258-131">Voer de app (de `dotnet run` opdracht wordt de app bouwen wanneer deze verouderd is):</span><span class="sxs-lookup"><span data-stu-id="7b258-131">Run the app  (the `dotnet run` command will build the app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="7b258-132">Open een browser en Ga naar de volgende URL.</span><span class="sxs-lookup"><span data-stu-id="7b258-132">Open a browser and navigate to the following URL.</span></span>
   
    <span data-ttu-id="7b258-133">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="7b258-133">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="7b258-134">De standaardpagina van de web-app wordt als volgt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7b258-134">The default page of the web app will appear as follows.</span></span>
   
    ![Lokale web-app in een browser](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="7b258-136">Sluit uw browser.</span><span class="sxs-lookup"><span data-stu-id="7b258-136">Close your browser.</span></span> <span data-ttu-id="7b258-137">In de **opdrachtvenster**, drukt u op **Ctrl + C** afsluiten van de toepassing en sluit de **opdrachtvenster**.</span><span class="sxs-lookup"><span data-stu-id="7b258-137">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span></span> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="7b258-138">Een web-app maken in de Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="7b258-138">Create a web app in the Azure Portal</span></span>
<span data-ttu-id="7b258-139">De volgende stappen begeleidt u bij het maken van een web-app in de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="7b258-139">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="7b258-140">Meld u aan bij de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b258-140">Log in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7b258-141">Klik op **nieuw** links aan de bovenkant van de Portal.</span><span class="sxs-lookup"><span data-stu-id="7b258-141">Click **NEW** at the top left of the Portal.</span></span>
3. <span data-ttu-id="7b258-142">Klik op **Web-Apps > Web-App**.</span><span class="sxs-lookup"><span data-stu-id="7b258-142">Click **Web Apps > Web App**.</span></span>
   
    ![Azure nieuwe web-app](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="7b258-144">Voer een waarde voor **naam**, zoals **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="7b258-144">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="7b258-145">Merk op dat deze naam moet uniek en de portal wordt afdwingen dat wanneer u probeert de naam te geven.</span><span class="sxs-lookup"><span data-stu-id="7b258-145">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span></span> <span data-ttu-id="7b258-146">Dus als u een Voer een andere waarde selecteert, moet u die waarde voor elk exemplaar van vervangende **SampleWebAppDemo** die u ziet in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7b258-146">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="7b258-147">Selecteer een bestaande **App Service-Plan** of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="7b258-147">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="7b258-148">Als u een nieuw plan maakt, selecteert u de prijscategorie, locatie en andere opties.</span><span class="sxs-lookup"><span data-stu-id="7b258-148">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="7b258-149">Zie het artikel voor meer informatie over App Service-abonnementen [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b258-149">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Azure blade voor nieuwe web-app](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="7b258-151">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b258-151">Click **Create**.</span></span>
   
    ![blade web-app](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="7b258-153">Git-publicatie voor de nieuwe web-app inschakelen</span><span class="sxs-lookup"><span data-stu-id="7b258-153">Enable Git publishing for the new web app</span></span>
<span data-ttu-id="7b258-154">GIT is een gedistribueerd versiebeheersysteem waarmee u kunt uw Azure App Service-web-app implementeren.</span><span class="sxs-lookup"><span data-stu-id="7b258-154">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="7b258-155">U slaat de code die u voor uw web-app schrijft, op in een lokale Git-opslagplaats en u implementeert uw code in Azure door deze naar een externe opslagplaats te pushen.</span><span class="sxs-lookup"><span data-stu-id="7b258-155">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>   

1. <span data-ttu-id="7b258-156">Meld u aan bij de [Azure-Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b258-156">Log into the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7b258-157">Klik op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="7b258-157">Click **Browse**.</span></span>
3. <span data-ttu-id="7b258-158">Klik op **Web-Apps** om een lijst met de web-apps die zijn gekoppeld aan uw Azure-abonnement weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7b258-158">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="7b258-159">Selecteer de web-app die u in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b258-159">Select the web app you created in this tutorial.</span></span>
5. <span data-ttu-id="7b258-160">Klik in de blade web-app op **instellingen** > **continue implementatie**.</span><span class="sxs-lookup"><span data-stu-id="7b258-160">In the web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Azure-web-app host](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="7b258-162">Klik op **bron kiezen > lokale Git-opslagplaats**.</span><span class="sxs-lookup"><span data-stu-id="7b258-162">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="7b258-163">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b258-163">Click **OK**.</span></span>
   
    ![Azure lokale Git-opslagplaats](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="7b258-165">Als u hebt geen eerder implementatiereferenties voor het publiceren van een web-app of een andere App Service-app hebt ingesteld, ze nu instellen:</span><span class="sxs-lookup"><span data-stu-id="7b258-165">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="7b258-166">Klik op **instellingen** > **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="7b258-166">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="7b258-167">De **implementatiereferenties instellen** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7b258-167">The **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="7b258-168">Maak een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="7b258-168">Create a user name and password.</span></span>  <span data-ttu-id="7b258-169">U hebt dit wachtwoord later nodig bij het instellen van Git.</span><span class="sxs-lookup"><span data-stu-id="7b258-169">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="7b258-170">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7b258-170">Click **Save**.</span></span>
9. <span data-ttu-id="7b258-171">Klik op de blade van uw web-app **instellingen > eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b258-171">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="7b258-172">De URL van de externe Git-opslagplaats die u implementeert op die wordt weergegeven onder **GIT-URL**.</span><span class="sxs-lookup"><span data-stu-id="7b258-172">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>
10. <span data-ttu-id="7b258-173">Kopieer de **GIT-URL** voor later gebruik in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7b258-173">Copy the **GIT URL** value for later use in the tutorial.</span></span>
    
    ![Azure Git-URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="7b258-175">Publiceren van uw web-app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7b258-175">Publish your web app to Azure App Service</span></span>
<span data-ttu-id="7b258-176">In deze sectie maakt u een lokale Git-opslagplaats en push vanuit die opslagplaats naar Azure voor het implementeren van uw web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b258-176">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span></span>

1. <span data-ttu-id="7b258-177">Selecteer in VS-Code, de **Git** optie in de linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="7b258-177">In VS Code, select the **Git** option in the left navigation bar.</span></span>
   
    ![GIT-pictogram in VS-Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="7b258-179">Selecteer **initialiseren git-opslagplaats** om ervoor te zorgen dat uw werkruimte is onder git-bronbeheer.</span><span class="sxs-lookup"><span data-stu-id="7b258-179">Select **Initialize git repository** to make sure your workspace is under git source control.</span></span> 
   
    ![Git geïnitialiseerd](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="7b258-181">Open het opdrachtvenster en wijzig de mappen in de map van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7b258-181">Open the Command Window and change directories to the directory of your web app.</span></span> <span data-ttu-id="7b258-182">Voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7b258-182">Then, enter the following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="7b258-183">Met deze opdracht voorkomt u dat een probleem over tekst waar CRLF uitgangen en LF uitgangen zijn betrokken.</span><span class="sxs-lookup"><span data-stu-id="7b258-183">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="7b258-184">In de Code van de VS, een commit-bericht toevoegen en klik op de **doorvoeren alle** vinkje.</span><span class="sxs-lookup"><span data-stu-id="7b258-184">In VS Code, add a commit message and click the **Commit All** check icon.</span></span>
   
    ![GIT alle doorvoeren](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="7b258-186">Nadat de Git is verwerkt, ziet u dat er zijn geen bestanden die worden weergegeven in het venster Git onder **wijzigingen**.</span><span class="sxs-lookup"><span data-stu-id="7b258-186">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span></span> 
   
    ![GIT geen wijzigingen](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="7b258-188">Wijzig weer in het opdrachtvenster waar de opdrachtprompt naar de map verwijst waarin uw web-app zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="7b258-188">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span></span>
7. <span data-ttu-id="7b258-189">Maak een externe verwijzing voor om updates te pushen naar uw web-app met behulp van de Git-URL (eindigend op '.git') die u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="7b258-189">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="7b258-190">Configureer Git om uw referenties lokaal opslaan zodat ze automatisch worden toegevoegd aan uw opdrachten push is gegenereerd op basis van de VS-Code.</span><span class="sxs-lookup"><span data-stu-id="7b258-190">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="7b258-191">Pusht u uw wijzigingen naar Azure met de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="7b258-191">Push your changes to Azure by entering the following command.</span></span> <span data-ttu-id="7b258-192">Na deze eerste push naar Azure, kunt u zich kunt alle push-opdrachten uitvoeren vanuit VS-Code.</span><span class="sxs-lookup"><span data-stu-id="7b258-192">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="7b258-193">U wordt gevraagd om het wachtwoord dat u eerder in Azure gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b258-193">You are prompted for the password you created earlier in Azure.</span></span> <span data-ttu-id="7b258-194">**Opmerking: Uw wachtwoord wordt niet meer zichtbaar.**</span><span class="sxs-lookup"><span data-stu-id="7b258-194">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="7b258-195">De uitvoer van de bovenstaande opdracht eindigt met een bericht dat de implementatie geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="7b258-195">The output from the above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="7b258-196">Als u wijzigingen aan uw app aanbrengt, kunt u opnieuw publiceren rechtstreeks in VS-Code door te selecteren met behulp van de ingebouwde functionaliteit voor Git de **alle doorvoeren** optie gevolgd door de **Push** optie.</span><span class="sxs-lookup"><span data-stu-id="7b258-196">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span></span> <span data-ttu-id="7b258-197">U vindt de **Push** optie beschikbaar in de vervolgkeuzelijst naast de **alle doorvoeren** en **vernieuwen** knoppen.</span><span class="sxs-lookup"><span data-stu-id="7b258-197">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="7b258-198">Als u samenwerken aan een project wilt, moet u rekening houden met GitHub worden gepusht Between pushen naar Azure.</span><span class="sxs-lookup"><span data-stu-id="7b258-198">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span></span>

## <a name="run-the-app-in-azure"></a><span data-ttu-id="7b258-199">De app in Azure uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7b258-199">Run the app in Azure</span></span>
<span data-ttu-id="7b258-200">Nu dat u uw web-app hebt geïmplementeerd, gaan we de app terwijl gehost in Azure worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b258-200">Now that you have deployed your web app, let's run the app while hosted in Azure.</span></span> 

<span data-ttu-id="7b258-201">Dit kan op twee manieren doen:</span><span class="sxs-lookup"><span data-stu-id="7b258-201">This can be done in two ways:</span></span>

* <span data-ttu-id="7b258-202">Open een browser en voer de naam van uw web-app als volgt.</span><span class="sxs-lookup"><span data-stu-id="7b258-202">Open a browser and enter the name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="7b258-203">Ga naar de blade web-app voor uw web-app in de Azure-Portal en klikt u op **Bladeren** om weer te geven van uw app</span><span class="sxs-lookup"><span data-stu-id="7b258-203">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span></span> 
* <span data-ttu-id="7b258-204">in de browser.</span><span class="sxs-lookup"><span data-stu-id="7b258-204">in your default browser.</span></span>

![Azure-web-app](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="7b258-206">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="7b258-206">Summary</span></span>
<span data-ttu-id="7b258-207">In deze zelfstudie hebt u geleerd hoe u een web-app in VS-Code maken en deze implementeren in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b258-207">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span></span> <span data-ttu-id="7b258-208">Raadpleeg het artikel voor meer informatie over de Code van de VS, [waarom Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="7b258-208">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="7b258-209">Zie voor meer informatie over App Service WebApps [overzicht van Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b258-209">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

