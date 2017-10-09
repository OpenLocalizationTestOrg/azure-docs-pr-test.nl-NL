---
title: aaaContinuous-implementatie voor Azure Functions | Microsoft Docs
description: Doorlopende implementatie faciliteiten van Azure App Service-toopublish uw Azure-functies gebruiken.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="571e3-103">Doorlopende implementatie voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="571e3-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="571e3-104">Azure Functions maakt het eenvoudig toodeploy uw functie-app met App Service continue integratie.</span><span class="sxs-lookup"><span data-stu-id="571e3-104">Azure Functions makes it easy toodeploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="571e3-105">Functions integreert met BitBucket, Dropbox, GitHub en Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="571e3-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="571e3-106">Hierdoor wordt een werkstroom waar functiecode updates uitgevoerd met behulp van een van deze geïntegreerde services trigger implementatie tooAzure.</span><span class="sxs-lookup"><span data-stu-id="571e3-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment tooAzure.</span></span> <span data-ttu-id="571e3-107">Als u nieuwe functies voor tooAzure, beginnen met [overzicht van Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="571e3-107">If you are new tooAzure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="571e3-108">Continue implementatie is een goede optie voor projecten waar meerdere en regelmatige bijdragen worden geïntegreerd.</span><span class="sxs-lookup"><span data-stu-id="571e3-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="571e3-109">U kunt ook broncodebeheer op uw code functies onderhouden.</span><span class="sxs-lookup"><span data-stu-id="571e3-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="571e3-110">de volgende bronnen voor implementatie Hallo worden momenteel ondersteund:</span><span class="sxs-lookup"><span data-stu-id="571e3-110">hello following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="571e3-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="571e3-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="571e3-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="571e3-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="571e3-113">Externe opslagplaats (Git of volgt)</span><span class="sxs-lookup"><span data-stu-id="571e3-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="571e3-114">Lokale GIT-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="571e3-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="571e3-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="571e3-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="571e3-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="571e3-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="571e3-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="571e3-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="571e3-118">Implementaties worden geconfigureerd op basis van de app per functie.</span><span class="sxs-lookup"><span data-stu-id="571e3-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="571e3-119">Nadat de doorlopende implementatie is ingeschakeld, toofunction toegangscode in Hallo-portal te ingesteld*alleen-lezen*.</span><span class="sxs-lookup"><span data-stu-id="571e3-119">After continuous deployment is enabled, access toofunction code in hello portal is set too*read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="571e3-120">Vereisten voor de doorlopende implementatie</span><span class="sxs-lookup"><span data-stu-id="571e3-120">Continuous deployment requirements</span></span>

<span data-ttu-id="571e3-121">In de implementatiebron Hallo voordat u continue implementatie instellen, moet u uw implementatiebron geconfigureerd en uw code functies hebben.</span><span class="sxs-lookup"><span data-stu-id="571e3-121">You must have your deployment source configured and your functions code in hello deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="571e3-122">Elke functie woont in een bepaalde functie app-implementatie in een benoemde submap, waarbij de mapnaam Hallo Hallo naam van Hallo-functie is.</span><span class="sxs-lookup"><span data-stu-id="571e3-122">In a given function app deployment, each function lives in a named subdirectory, where hello directory name is hello name of hello function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="571e3-123">Doorlopende implementatie instellen</span><span class="sxs-lookup"><span data-stu-id="571e3-123">Set up continuous deployment</span></span>
<span data-ttu-id="571e3-124">Gebruik deze procedure tooconfigure continue implementatie voor een bestaande functie-app.</span><span class="sxs-lookup"><span data-stu-id="571e3-124">Use this procedure tooconfigure continuous deployment for an existing function app.</span></span> <span data-ttu-id="571e3-125">Deze stappen laten zien integratie met een GitHub-opslagplaats, maar gelijksoortige stappen gelden voor Visual Studio Team Services of andere implementatieservices.</span><span class="sxs-lookup"><span data-stu-id="571e3-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="571e3-126">In de functie-app in Hallo [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **implementatieopties**.</span><span class="sxs-lookup"><span data-stu-id="571e3-126">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="571e3-128">Klik dan in Hallo **implementaties** Klik op de blade **Setup**.</span><span class="sxs-lookup"><span data-stu-id="571e3-128">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="571e3-130">In Hallo **implementatiebron** blade, klikt u op **bron kiezen**, vul vervolgens Hallo-informatie voor uw gekozen implementatiebron en klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="571e3-130">In hello **Deployment source** blade, click **Choose source**, then fill in hello information for your chosen deployment source and click **OK**.</span></span>
   
    ![Implementatiebron kiezen](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="571e3-132">Nadat de doorlopende implementatie is geconfigureerd, alle bestandswijzigingen in de implementatiebron-zijn gekopieerde toohello functie-app en een volledige site-implementatie wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="571e3-132">After continuous deployment is configured, all file changes in your deployment source are copied toohello function app and a full site deployment is triggered.</span></span> <span data-ttu-id="571e3-133">Hallo-site is opnieuw geïmplementeerd wanneer bestanden in de broninhoud Hallo zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="571e3-133">hello site is redeployed when files in hello source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="571e3-134">Implementatieopties</span><span class="sxs-lookup"><span data-stu-id="571e3-134">Deployment options</span></span>

<span data-ttu-id="571e3-135">Hallo Hieronder volgen enkele typische implementatiescenario's:</span><span class="sxs-lookup"><span data-stu-id="571e3-135">hello following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="571e3-136">Een gefaseerde installatie implementatie maken</span><span class="sxs-lookup"><span data-stu-id="571e3-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="571e3-137">Verplaatsen van bestaande functies toocontinuous implementatie</span><span class="sxs-lookup"><span data-stu-id="571e3-137">Move existing functions toocontinuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="571e3-138">Een gefaseerde installatie implementatie maken</span><span class="sxs-lookup"><span data-stu-id="571e3-138">Create a staging deployment</span></span>

<span data-ttu-id="571e3-139">Functie Apps ondersteunt nog geen implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="571e3-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="571e3-140">U kunt echter nog steeds afzonderlijke fasering en productie-implementaties beheren met behulp van continue integratie.</span><span class="sxs-lookup"><span data-stu-id="571e3-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="571e3-141">Hallo proces tooconfigure en werken met een gefaseerde installatie-implementatie in het algemeen zien er zo uit:</span><span class="sxs-lookup"><span data-stu-id="571e3-141">hello process tooconfigure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="571e3-142">Maak twee functie apps in uw abonnement, één voor de productiecode Hallo en één voor fasering.</span><span class="sxs-lookup"><span data-stu-id="571e3-142">Create two function apps in your subscription, one for hello production code and one for staging.</span></span> 

2. <span data-ttu-id="571e3-143">Maak een implementatiebron als u er nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="571e3-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="571e3-144">In dit voorbeeld wordt [GitHub].</span><span class="sxs-lookup"><span data-stu-id="571e3-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="571e3-145">Voor uw app van de functie productie voltooid Hallo voorgaande stappen in **continue implementatie instellen** en set Hallo implementatie vertakking toohello hoofdvertakking van uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="571e3-145">For your production function app, complete hello preceding steps in **Set up continuous deployment** and set hello deployment branch toohello master branch of your GitHub repository.</span></span>
   
    ![Vertakking implementatie kiezen](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="571e3-147">Herhaal deze stap voor Hallo staging-functie-app, maar Hallo vertakking in plaats daarvan fasering in uw GitHub-repo kiezen.</span><span class="sxs-lookup"><span data-stu-id="571e3-147">Repeat this step for hello staging function app, but choose hello staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="571e3-148">Als de implementatiebron-biedt geen ondersteuning voor vertakking, gebruikt u een andere map.</span><span class="sxs-lookup"><span data-stu-id="571e3-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="571e3-149">Controleer updates tooyour code in Hallo vertakking of de map voor gefaseerde installatie en controleer of dat deze wijzigingen zijn doorgevoerd in Hallo staging-implementatie.</span><span class="sxs-lookup"><span data-stu-id="571e3-149">Make updates tooyour code in hello staging branch or folder, then verify that those changes are reflected in hello staging deployment.</span></span>

6. <span data-ttu-id="571e3-150">Nadat u hebt getest, wijzigingen van de staging-vertakking naar de hoofdvertakking Hallo Hallo samen te voegen.</span><span class="sxs-lookup"><span data-stu-id="571e3-150">After testing, merge changes from hello staging branch into hello master branch.</span></span> <span data-ttu-id="571e3-151">Deze samenvoegen triggers implementatie toohello productie functie-app.</span><span class="sxs-lookup"><span data-stu-id="571e3-151">This merge triggers deployment toohello production function app.</span></span> <span data-ttu-id="571e3-152">Als de implementatiebron-biedt geen ondersteuning voor filialen, met Hallo-bestanden van de map voor gefaseerde installatie Hallo worden Hallo-bestanden in Hallo productie map overschreven.</span><span class="sxs-lookup"><span data-stu-id="571e3-152">If your deployment source doesn't support branches, overwrite hello files in hello production folder with hello files from hello staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a><span data-ttu-id="571e3-153">Verplaatsen van bestaande functies toocontinuous implementatie</span><span class="sxs-lookup"><span data-stu-id="571e3-153">Move existing functions toocontinuous deployment</span></span>
<span data-ttu-id="571e3-154">Wanneer u bestaande functies die u hebt gemaakt en onderhouden in Hallo-portal, moet u toodownload uw bestaande functioneren codebestanden FTP of Hallo lokale Git-opslagplaats met voordat u continue implementatie instellen kunt zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="571e3-154">When you have existing functions that you have created and maintained in hello portal, you need toodownload your existing function code files using FTP or hello local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="571e3-155">U kunt dit doen in Hallo App Service-instellingen voor de functie-app.</span><span class="sxs-lookup"><span data-stu-id="571e3-155">You can do this in hello App Service settings for your function app.</span></span> <span data-ttu-id="571e3-156">Nadat de bestanden zijn gedownload, kunt u ze tooyour gekozen continue implementatiebron uploaden.</span><span class="sxs-lookup"><span data-stu-id="571e3-156">After your files are downloaded, you can upload them tooyour chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="571e3-157">Nadat u continue integratie configureert, langer u niet kunnen tooedit uw in Hallo Functions-portal bronbestanden.</span><span class="sxs-lookup"><span data-stu-id="571e3-157">After you configure continuous integration, you will no longer be able tooedit your source files in hello Functions portal.</span></span>

- [<span data-ttu-id="571e3-158">Hoe: Configureer de referenties voor implementatie</span><span class="sxs-lookup"><span data-stu-id="571e3-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="571e3-159">Hoe: downloaden van bestanden met FTP</span><span class="sxs-lookup"><span data-stu-id="571e3-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="571e3-160">Hoe: downloaden van bestanden met Hallo lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="571e3-160">How to: Download files using hello local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="571e3-161">Hoe: Configureer de referenties voor implementatie</span><span class="sxs-lookup"><span data-stu-id="571e3-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="571e3-162">Voordat u bestanden van de functie-app met FTP- of lokale Git-opslagplaats downloaden kunt, moet u uw referenties tooaccess Hallo site configureren.</span><span class="sxs-lookup"><span data-stu-id="571e3-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials tooaccess hello site.</span></span> <span data-ttu-id="571e3-163">Referenties worden ingesteld op Hallo functie app-niveau.</span><span class="sxs-lookup"><span data-stu-id="571e3-163">Credentials are set at hello Function app level.</span></span> <span data-ttu-id="571e3-164">Gebruik Hallo stappen tooset implementatiereferenties in hello Azure-portal te volgen:</span><span class="sxs-lookup"><span data-stu-id="571e3-164">Use hello following steps tooset deployment credentials in hello Azure portal:</span></span>

1. <span data-ttu-id="571e3-165">In de functie-app in Hallo [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="571e3-165">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Lokale implementatiereferenties instellen](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="571e3-167">Typ een gebruikersnaam en wachtwoord en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="571e3-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="571e3-168">U kunt deze referenties tooaccess nu uw app in de functie van de FTP- of Hallo ingebouwde Git-opslagplaats gebruiken.</span><span class="sxs-lookup"><span data-stu-id="571e3-168">You can now use these credentials tooaccess your function app from FTP or hello built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="571e3-169">Hoe: downloaden van bestanden met FTP</span><span class="sxs-lookup"><span data-stu-id="571e3-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="571e3-170">In de functie-app in Hallo [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **eigenschappen**, kopieert u Hallo waarden voor **FTP-/ Implementatiegebruiker gebruiker**, **FTP-hostnaam**, en **FTPS hostnaam**.</span><span class="sxs-lookup"><span data-stu-id="571e3-170">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="571e3-171">**FTP-/ Implementatiegebruiker gebruiker** moet worden ingevoerd zoals weergegeven in de Hallo-portal, met inbegrip van Hallo app-naam, de juiste context tooprovide voor Hallo FTP-server.</span><span class="sxs-lookup"><span data-stu-id="571e3-171">**FTP/Deployment User** must be entered as displayed in hello portal, including hello app name, tooprovide proper context for hello FTP server.</span></span>
   
    ![Uw implementatie-informatie ophalen](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="571e3-173">Van uw FTP-client gebruikt Hallo verbindingsinformatie verzameld van tooconnect tooyour app en download de bronbestanden Hallo voor uw functies.</span><span class="sxs-lookup"><span data-stu-id="571e3-173">From your FTP client, use hello connection information you gathered tooconnect tooyour app and download hello source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="571e3-174">Hoe: downloaden van bestanden met behulp van een lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="571e3-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="571e3-175">In de functie-app in Hallo [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **implementatieopties**.</span><span class="sxs-lookup"><span data-stu-id="571e3-175">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="571e3-177">Klik dan in Hallo **implementaties** Klik op de blade **Setup**.</span><span class="sxs-lookup"><span data-stu-id="571e3-177">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="571e3-179">In Hallo **implementatiebron** blade, klikt u op **lokale Git-opslagplaats** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="571e3-179">In hello **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="571e3-180">In **platformfuncties**, klikt u op **eigenschappen** en bekijkt hello waarde Git-URL.</span><span class="sxs-lookup"><span data-stu-id="571e3-180">In **Platform features**, click **Properties** and note hello value of Git URL.</span></span> 
   
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="571e3-182">Kloon de opslagplaats Hallo op uw lokale computer met een Git-bewuste opdrachtprompt of uw favoriete Git-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="571e3-182">Clone hello repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="571e3-183">Hallo Git kloonopdracht ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="571e3-183">hello Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="571e3-184">Bestanden ophalen van de kloon van de functie app-toohello op uw lokale computer, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="571e3-184">Fetch files from your function app toohello clone on your local computer, as in hello following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="571e3-185">Als u hebt aangevraagd, geeft u uw [implementatiereferenties geconfigureerd](#credentials).</span><span class="sxs-lookup"><span data-stu-id="571e3-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/
