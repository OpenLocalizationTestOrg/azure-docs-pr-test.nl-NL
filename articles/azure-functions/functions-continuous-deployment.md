---
title: Continue implementatie voor Azure Functions | Microsoft Docs
description: Doorlopende implementatie faciliteiten van Azure App Service gebruiken voor het publiceren van uw Azure-functies.
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
ms.openlocfilehash: 3756f1a039730bfd99b0375ce9bfeaf27178f2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="b5545-103">Doorlopende implementatie voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b5545-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="b5545-104">Azure Functions kunt eenvoudig uw functie-app met continue integratie van App Service implementeren.</span><span class="sxs-lookup"><span data-stu-id="b5545-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="b5545-105">Functions integreert met BitBucket, Dropbox, GitHub en Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="b5545-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="b5545-106">Hierdoor wordt een werkstroom waar functiecode updates uitgevoerd met behulp van een van deze implementatie van de trigger geïntegreerde services naar Azure.</span><span class="sxs-lookup"><span data-stu-id="b5545-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="b5545-107">Als u niet bekend met Azure Functions bent, beginnen met een [overzicht van Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5545-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="b5545-108">Continue implementatie is een goede optie voor projecten waar meerdere en regelmatige bijdragen worden geïntegreerd.</span><span class="sxs-lookup"><span data-stu-id="b5545-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="b5545-109">U kunt ook broncodebeheer op uw code functies onderhouden.</span><span class="sxs-lookup"><span data-stu-id="b5545-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="b5545-110">De volgende bronnen voor de implementatie worden momenteel ondersteund:</span><span class="sxs-lookup"><span data-stu-id="b5545-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="b5545-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="b5545-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="b5545-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="b5545-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="b5545-113">Externe opslagplaats (Git of volgt)</span><span class="sxs-lookup"><span data-stu-id="b5545-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="b5545-114">Lokale GIT-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="b5545-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="b5545-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="b5545-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="b5545-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="b5545-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="b5545-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="b5545-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="b5545-118">Implementaties worden geconfigureerd op basis van de app per functie.</span><span class="sxs-lookup"><span data-stu-id="b5545-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="b5545-119">Nadat de doorlopende implementatie is ingeschakeld, toegang tot de functiecode in de portal is ingesteld op *alleen-lezen*.</span><span class="sxs-lookup"><span data-stu-id="b5545-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="b5545-120">Vereisten voor de doorlopende implementatie</span><span class="sxs-lookup"><span data-stu-id="b5545-120">Continuous deployment requirements</span></span>

<span data-ttu-id="b5545-121">In de implementatiebron voordat u continue implementatie instelt, moet u uw implementatiebron geconfigureerd en uw code functies hebben.</span><span class="sxs-lookup"><span data-stu-id="b5545-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="b5545-122">Elke functie woont in een bepaalde functie app-implementatie in een benoemde submap, waarbij de mapnaam de naam van de functie is.</span><span class="sxs-lookup"><span data-stu-id="b5545-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="b5545-123">Doorlopende implementatie instellen</span><span class="sxs-lookup"><span data-stu-id="b5545-123">Set up continuous deployment</span></span>
<span data-ttu-id="b5545-124">Gebruik deze procedure voor het configureren van continue implementatie voor een bestaande functie-app.</span><span class="sxs-lookup"><span data-stu-id="b5545-124">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="b5545-125">Deze stappen laten zien integratie met een GitHub-opslagplaats, maar gelijksoortige stappen gelden voor Visual Studio Team Services of andere implementatieservices.</span><span class="sxs-lookup"><span data-stu-id="b5545-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="b5545-126">In de functie-app in de [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **implementatieopties**.</span><span class="sxs-lookup"><span data-stu-id="b5545-126">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="b5545-128">Klik in de **implementaties** Klik op de blade **Setup**.</span><span class="sxs-lookup"><span data-stu-id="b5545-128">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="b5545-130">In de **implementatiebron** blade, klikt u op **bron kiezen**, vul vervolgens de gegevens voor uw gekozen implementatiebron en klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5545-130">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![Implementatiebron kiezen](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="b5545-132">Nadat doorlopende implementatie is geconfigureerd, alle bestandswijzigingen in de implementatiebron-worden gekopieerd naar de functie-app en een volledige site-implementatie wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b5545-132">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="b5545-133">De site is opnieuw geïmplementeerd wanneer bestanden in de bron worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b5545-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="b5545-134">Implementatieopties</span><span class="sxs-lookup"><span data-stu-id="b5545-134">Deployment options</span></span>

<span data-ttu-id="b5545-135">Hier volgen enkele typische implementatiescenario's:</span><span class="sxs-lookup"><span data-stu-id="b5545-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="b5545-136">Een gefaseerde installatie implementatie maken</span><span class="sxs-lookup"><span data-stu-id="b5545-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="b5545-137">Verplaatsen van bestaande functies voor continue implementatie</span><span class="sxs-lookup"><span data-stu-id="b5545-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="b5545-138">Een gefaseerde installatie implementatie maken</span><span class="sxs-lookup"><span data-stu-id="b5545-138">Create a staging deployment</span></span>

<span data-ttu-id="b5545-139">Functie Apps ondersteunt nog geen implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="b5545-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="b5545-140">U kunt echter nog steeds afzonderlijke fasering en productie-implementaties beheren met behulp van continue integratie.</span><span class="sxs-lookup"><span data-stu-id="b5545-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="b5545-141">Het proces voor het configureren en werken met een gefaseerde installatie implementatie ziet er meestal als volgt:</span><span class="sxs-lookup"><span data-stu-id="b5545-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="b5545-142">Maak twee functie apps in uw abonnement, één voor de productiecode en één voor fasering.</span><span class="sxs-lookup"><span data-stu-id="b5545-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="b5545-143">Maak een implementatiebron als u er nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="b5545-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="b5545-144">In dit voorbeeld wordt [GitHub].</span><span class="sxs-lookup"><span data-stu-id="b5545-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="b5545-145">Voor uw app van de functie productie voltooid de stappen **continue implementatie instellen** en stel de vertakking implementatie naar de hoofdvertakking van de GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="b5545-145">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![Vertakking implementatie kiezen](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="b5545-147">Herhaal deze stap voor fasering functie-app, maar de fasering vertakking in plaats daarvan kiezen in uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="b5545-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="b5545-148">Als de implementatiebron-biedt geen ondersteuning voor vertakking, gebruikt u een andere map.</span><span class="sxs-lookup"><span data-stu-id="b5545-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="b5545-149">Updates aanbrengen in uw code in de tijdelijke map of vertakking, controleer dan vervolgens dat deze wijzigingen zijn doorgevoerd in de staging-implementatie.</span><span class="sxs-lookup"><span data-stu-id="b5545-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="b5545-150">Na het testen verandert het samenvoegen van de staging vertakking naar de hoofdvertakking.</span><span class="sxs-lookup"><span data-stu-id="b5545-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="b5545-151">Deze samenvoegen activeert implementatie naar de productie-app voor de functie.</span><span class="sxs-lookup"><span data-stu-id="b5545-151">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="b5545-152">Als de implementatiebron-biedt geen ondersteuning voor filialen, overschrijven de bestanden in de productie-map met de bestanden van de map.</span><span class="sxs-lookup"><span data-stu-id="b5545-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="b5545-153">Verplaatsen van bestaande functies voor continue implementatie</span><span class="sxs-lookup"><span data-stu-id="b5545-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="b5545-154">Wanneer u hebt bestaande functies die u hebt gemaakt en onderhouden in de portal, moet u uw bestaande functie codebestanden met FTP downloaden of het lokale Git-opslagplaats voordat u continue implementatie instellen kunt zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="b5545-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="b5545-155">U kunt dit doen in de App Service-instellingen voor de functie-app.</span><span class="sxs-lookup"><span data-stu-id="b5545-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="b5545-156">Nadat de bestanden zijn gedownload, kunt u ze kunt uploaden naar uw bron gekozen continue implementatie.</span><span class="sxs-lookup"><span data-stu-id="b5545-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="b5545-157">Nadat u continue integratie hebt geconfigureerd, kunt u zich niet langer bewerken van de bronbestanden in de portal functies.</span><span class="sxs-lookup"><span data-stu-id="b5545-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="b5545-158">Hoe: Configureer de referenties voor implementatie</span><span class="sxs-lookup"><span data-stu-id="b5545-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="b5545-159">Hoe: downloaden van bestanden met FTP</span><span class="sxs-lookup"><span data-stu-id="b5545-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="b5545-160">Hoe: downloaden van bestanden met behulp van de lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="b5545-160">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="b5545-161">Hoe: Configureer de referenties voor implementatie</span><span class="sxs-lookup"><span data-stu-id="b5545-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="b5545-162">Voordat u bestanden van de functie-app met FTP- of lokale Git-opslagplaats downloaden kunt, moet u uw referenties voor toegang tot de site configureren.</span><span class="sxs-lookup"><span data-stu-id="b5545-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="b5545-163">Referenties worden ingesteld op het niveau van de functie-app.</span><span class="sxs-lookup"><span data-stu-id="b5545-163">Credentials are set at the Function app level.</span></span> <span data-ttu-id="b5545-164">Gebruik de volgende stappen uit als implementatiereferenties wilt instellen in de Azure portal:</span><span class="sxs-lookup"><span data-stu-id="b5545-164">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="b5545-165">In de functie-app in de [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="b5545-165">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Lokale implementatiereferenties instellen](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="b5545-167">Typ een gebruikersnaam en wachtwoord en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b5545-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="b5545-168">U kunt deze referenties nu gebruiken voor toegang tot uw app in de functie van FTP of de ingebouwde Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="b5545-168">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="b5545-169">Hoe: downloaden van bestanden met FTP</span><span class="sxs-lookup"><span data-stu-id="b5545-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="b5545-170">In de functie-app in de [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **eigenschappen**, kopieert u de waarden voor **FTP-/ Implementatiegebruiker gebruiker**, **FTP-hostnaam**, en **FTPS hostnaam**.</span><span class="sxs-lookup"><span data-stu-id="b5545-170">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="b5545-171">**FTP-/ Implementatiegebruiker gebruiker** moet worden ingevoerd zoals weergegeven in de portal, met inbegrip van de naam van de app, zodat de juiste context voor de FTP-server.</span><span class="sxs-lookup"><span data-stu-id="b5545-171">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![Uw implementatie-informatie ophalen](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="b5545-173">Gebruik de gegevens van uw FTP-client. u hebt verzameld voor het verbinding maken met uw app en download de bronbestanden voor uw functies.</span><span class="sxs-lookup"><span data-stu-id="b5545-173">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="b5545-174">Hoe: downloaden van bestanden met behulp van een lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="b5545-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="b5545-175">In de functie-app in de [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **implementatieopties**.</span><span class="sxs-lookup"><span data-stu-id="b5545-175">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="b5545-177">Klik in de **implementaties** Klik op de blade **Setup**.</span><span class="sxs-lookup"><span data-stu-id="b5545-177">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="b5545-179">In de **implementatiebron** blade, klikt u op **lokale Git-opslagplaats** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5545-179">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="b5545-180">In **platformfuncties**, klikt u op **eigenschappen** en noteer de waarde van de Git-URL.</span><span class="sxs-lookup"><span data-stu-id="b5545-180">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="b5545-182">Kloon de opslagplaats op uw lokale computer met een Git-bewuste opdrachtprompt of uw favoriete Git-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="b5545-182">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="b5545-183">De Git-kloon-opdracht ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="b5545-183">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="b5545-184">Bestanden ophalen van de functie-app op de kloon op uw lokale computer, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b5545-184">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="b5545-185">Als u hebt aangevraagd, geeft u uw [implementatiereferenties geconfigureerd](#credentials).</span><span class="sxs-lookup"><span data-stu-id="b5545-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

<span data-ttu-id="b5545-186">[GitHub]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="b5545-186">[GitHub]: https://github.com/</span></span>
