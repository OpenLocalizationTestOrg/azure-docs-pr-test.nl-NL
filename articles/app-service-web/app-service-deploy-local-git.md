---
title: aaaLocal Git-implementatie tooAzure App Service
description: Meer informatie over hoe tooenable lokale Git-implementatie tooAzure App Service.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a><span data-ttu-id="82f40-103">Lokale Git-implementatie tooAzure App Service</span><span class="sxs-lookup"><span data-stu-id="82f40-103">Local Git Deployment tooAzure App Service</span></span>
<span data-ttu-id="82f40-104">Deze zelfstudie leert u hoe toodeploy uw app te[Azure App Service] van een Git-opslagplaats op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="82f40-104">This tutorial shows you how toodeploy your app too[Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="82f40-105">App Service biedt ondersteuning voor deze benadering Hello **lokale Git** Implementatieoptie in Hallo [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="82f40-105">App Service supports this approach with hello **Local Git** deployment option in hello [Azure Portal].</span></span>  
<span data-ttu-id="82f40-106">Veel van Hallo Git-opdrachten die worden beschreven in dit artikel worden automatisch uitgevoerd tijdens het maken van een App Service-app met behulp van Hallo [Azure-opdrachtregelinterface] zoals beschreven [hier](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="82f40-106">Many of hello Git commands described in this article are performed automatically when creating an App Service app using hello [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82f40-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="82f40-107">Prerequisites</span></span>
<span data-ttu-id="82f40-108">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="82f40-108">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="82f40-109">GIT.</span><span class="sxs-lookup"><span data-stu-id="82f40-109">Git.</span></span> <span data-ttu-id="82f40-110">U kunt downloaden Hallo installatie binaire [hier](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="82f40-110">You can download hello installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="82f40-111">Basiskennis van Git.</span><span class="sxs-lookup"><span data-stu-id="82f40-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="82f40-112">Een Microsoft Azure-account.</span><span class="sxs-lookup"><span data-stu-id="82f40-112">A Microsoft Azure account.</span></span> <span data-ttu-id="82f40-113">Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="82f40-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="82f40-114">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="82f40-114">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="82f40-115">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="82f40-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="82f40-116"><a name="Step1"></a>Stap 1: Maak een lokale opslagplaats</span><span class="sxs-lookup"><span data-stu-id="82f40-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="82f40-117">Voer Hallo taken toocreate nieuwe Git-opslagplaats te volgen.</span><span class="sxs-lookup"><span data-stu-id="82f40-117">Perform hello following tasks toocreate a new Git repository.</span></span>

1. <span data-ttu-id="82f40-118">Start een opdrachtregelprogramma, zoals **GitBash** (Windows) of **Bash** (Unix-Shell).</span><span class="sxs-lookup"><span data-stu-id="82f40-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="82f40-119">U kunt op OS X-systemen Hallo opdrachtregelprogramma benaderen via Hallo **Terminal** toepassing.</span><span class="sxs-lookup"><span data-stu-id="82f40-119">On OS X systems you can access hello command-line through hello **Terminal** application.</span></span>
2. <span data-ttu-id="82f40-120">Navigeer toohello directory waar de inhoud toodeploy Hallo geplaatst worden.</span><span class="sxs-lookup"><span data-stu-id="82f40-120">Navigate toohello directory where hello content toodeploy would be located.</span></span>
3. <span data-ttu-id="82f40-121">Gebruik Hallo opdracht tooinitialize nieuwe Git-opslagplaats te volgen:</span><span class="sxs-lookup"><span data-stu-id="82f40-121">Use hello following command tooinitialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="82f40-122"><a name="Step2"></a>Stap 2: Uw inhoud doorvoeren</span><span class="sxs-lookup"><span data-stu-id="82f40-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="82f40-123">App Service biedt ondersteuning voor toepassingen die zijn gemaakt in diverse programmeertalen.</span><span class="sxs-lookup"><span data-stu-id="82f40-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="82f40-124">Als uw opslagplaats al inhoud overslaan dit punt bevat en toopoint 2 hieronder verplaatsen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="82f40-124">If your repository already includes content skip this point and move toopoint 2 below.</span></span> <span data-ttu-id="82f40-125">Als uw opslagplaats geen inhoud gewoon bevat nog te vullen met een statische HTML-bestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="82f40-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="82f40-126">Start een teksteditor en maak een nieuw bestand met de naam **index.html** in de hoofdmap Hallo van Hallo Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="82f40-126">Using a text editor, create a new file named **index.html** at hello root of hello Git repository</span></span>
   * <span data-ttu-id="82f40-127">Hallo na tekst hello inhoud voor Hallo index.html bestand en slaat u deze toevoegen: *Hallo Git!*</span><span class="sxs-lookup"><span data-stu-id="82f40-127">Add hello following text as hello contents for hello index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="82f40-128">Vanaf de opdrachtregel hello, controleert u of u onder Hallo hoofdmap van de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="82f40-128">From hello command-line, verify that you are under hello root of your Git repository.</span></span> <span data-ttu-id="82f40-129">Gebruik vervolgens de volgende opdracht tooadd bestanden tooyour opslagplaats Hallo:</span><span class="sxs-lookup"><span data-stu-id="82f40-129">Then use hello following command tooadd files tooyour repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="82f40-130">Vervolgens doorvoeren Hallo wijzigingen toohello opslagplaats met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="82f40-130">Next, commit hello changes toohello repository by using hello following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="82f40-131"><a name="Step3"></a>Stap 3: Schakel Hallo App Service-app-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="82f40-131"><a name="Step3"></a>Step 3: Enable hello App Service app repository</span></span>
<span data-ttu-id="82f40-132">Hallo te volgen stappen tooenable een Git-opslagplaats voor uw App Service-app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="82f40-132">Perform hello following steps tooenable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="82f40-133">Meld u bij toohello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="82f40-133">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="82f40-134">Klik op de blade van uw App Service-app **instellingen > implementatiebron**.</span><span class="sxs-lookup"><span data-stu-id="82f40-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="82f40-135">Klik op **bron kiezen**, klikt u vervolgens op **lokale Git-opslagplaats**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="82f40-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Lokale Git-opslagplaats](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="82f40-137">Als dit de eerste keer instellen van een opslagplaats in Azure, moet u de aanmeldingsreferenties toocreate voor deze.</span><span class="sxs-lookup"><span data-stu-id="82f40-137">If this is your first time setting up a repository in Azure, you need toocreate login credentials for it.</span></span> <span data-ttu-id="82f40-138">U gebruikt deze toolog in hello Azure-opslagplaats en wijzigingen van uw lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="82f40-138">You will use them toolog into hello Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="82f40-139">Op de blade van uw app, klikt u op **instellingen > implementatiereferenties**, configureert u uw implementatie gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="82f40-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="82f40-140">Wanneer u bent klaar, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="82f40-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="82f40-141"><a name="Step4"></a>Stap 4: Implementeer uw project</span><span class="sxs-lookup"><span data-stu-id="82f40-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="82f40-142">Hallo toopublish stappen na de tooApp van uw app Service met lokale Git gebruiken.</span><span class="sxs-lookup"><span data-stu-id="82f40-142">Use hello following steps toopublish your app tooApp Service using Local Git.</span></span>

1. <span data-ttu-id="82f40-143">Klik in de blade van uw app in Azure Portal Hallo op **instellingen > eigenschappen** voor Hallo **Git-URL**.</span><span class="sxs-lookup"><span data-stu-id="82f40-143">In your app's blade in hello Azure Portal, click **Settings > Properties** for hello **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="82f40-144">**GIT-URL** Hallo externe verwijzing toodeploy toofrom is uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="82f40-144">**Git URL** is hello remote reference toodeploy toofrom your local repository.</span></span> <span data-ttu-id="82f40-145">U gebruikt deze URL in Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="82f40-145">You'll use this URL in hello following steps.</span></span>
2. <span data-ttu-id="82f40-146">Hallo opdrachtregelprogramma gebruikt, controleert u of u in de hoofdmap Hallo van uw lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="82f40-146">Using hello command-line, verify that you are in hello root of your local Git repository.</span></span>
3. <span data-ttu-id="82f40-147">Gebruik `git remote` tooadd Hallo externe verwijzing die worden vermeld in **Git-URL** uit stap 1.</span><span class="sxs-lookup"><span data-stu-id="82f40-147">Use `git remote` tooadd hello remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="82f40-148">De opdracht ziet er vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="82f40-148">Your command will look similar toohello following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="82f40-149">Hallo **externe** opdracht voegt een benoemde verwijzing tooa externe opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="82f40-149">hello **remote** command adds a named reference tooa remote repository.</span></span> <span data-ttu-id="82f40-150">In dit voorbeeld wordt een verwijzing met de naam 'azure' voor uw web-app-opslagplaats gemaakt.</span><span class="sxs-lookup"><span data-stu-id="82f40-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="82f40-151">Uw inhoud tooApp Service push met Hallo nieuwe **azure** externe u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="82f40-151">Push your content tooApp Service using hello new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. <span data-ttu-id="82f40-152">Ga terug in Azure Portal Hallo tooyour app.</span><span class="sxs-lookup"><span data-stu-id="82f40-152">Go back tooyour app in hello Azure Portal.</span></span> <span data-ttu-id="82f40-153">Een logboekvermelding van de meest recente push moet worden weergegeven in Hallo **implementaties** blade.</span><span class="sxs-lookup"><span data-stu-id="82f40-153">A log entry of your most recent push should be displayed in hello **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="82f40-154">Klik op Hallo **Bladeren** knop Hallo boven aan het Hallo-app blade tooverify Hallo inhoud is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="82f40-154">Click hello **Browse** button at hello top of hello app's blade tooverify hello content has been deployed.</span></span> 

## <span data-ttu-id="82f40-155"><a name="Step5"></a>Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="82f40-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="82f40-156">Hallo volgen fouten of problemen meestal opgetreden bij het gebruik van Git toopublish tooan App Service-app in Azure:</span><span class="sxs-lookup"><span data-stu-id="82f40-156">hello following are errors or problems commonly encountered when using Git toopublish tooan App Service app in Azure:</span></span>

- - -
<span data-ttu-id="82f40-157">**Symptoom**: kan geen tooaccess [siteURL]: tooconnect te is mislukt [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="82f40-157">**Symptom**: Unable tooaccess '[siteURL]': Failed tooconnect too[scmAddress]</span></span>

<span data-ttu-id="82f40-158">**Oorzaak**: deze fout kan optreden als het Hallo-app niet actief is.</span><span class="sxs-lookup"><span data-stu-id="82f40-158">**Cause**: This error can occur if hello app is not up and running.</span></span>

<span data-ttu-id="82f40-159">**Resolutie**: begin Hallo-app in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="82f40-159">**Resolution**: Start hello app in hello Azure Portal.</span></span> <span data-ttu-id="82f40-160">GIT-implementatie werkt niet, tenzij het Hallo-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="82f40-160">Git deployment will not work unless hello app is running.</span></span> 

- - -
<span data-ttu-id="82f40-161">**Symptoom**: host 'naam' niet oplossen</span><span class="sxs-lookup"><span data-stu-id="82f40-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="82f40-162">**Oorzaak**: deze fout kan optreden als de adresgegevens Hallo ingevoerd bij het maken van Hallo 'azure' externe is onjuist.</span><span class="sxs-lookup"><span data-stu-id="82f40-162">**Cause**: This error can occur if hello address information entered when creating hello 'azure' remote was incorrect.</span></span>

<span data-ttu-id="82f40-163">**Resolutie**: gebruik Hallo `git remote -v` opdracht toolist alle afstandsbedieningen, samen met de URL van de Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="82f40-163">**Resolution**: Use hello `git remote -v` command toolist all remotes, along with hello associated URL.</span></span> <span data-ttu-id="82f40-164">Controleer of Hallo-URL voor Hallo 'azure' externe klopt.</span><span class="sxs-lookup"><span data-stu-id="82f40-164">Verify that hello URL for hello 'azure' remote is correct.</span></span> <span data-ttu-id="82f40-165">Indien nodig, verwijderen en maak dit externe met behulp van de juiste URL Hallo.</span><span class="sxs-lookup"><span data-stu-id="82f40-165">If needed, remove and recreate this remote using hello correct URL.</span></span>

- - -
<span data-ttu-id="82f40-166">**Symptoom**: Er is geen refs in algemene en er is geen opgegeven; niets te doen.</span><span class="sxs-lookup"><span data-stu-id="82f40-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="82f40-167">Mogelijk moet u een vertakking zoals 'master' opgeven.</span><span class="sxs-lookup"><span data-stu-id="82f40-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="82f40-168">**Oorzaak**: deze fout kan optreden als u geen een vertakking opgeven wanneer u een git push-bewerking uitvoert, en er geen set Hallo push.default waarde die wordt gebruikt door Git.</span><span class="sxs-lookup"><span data-stu-id="82f40-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set hello push.default value used by Git.</span></span>

<span data-ttu-id="82f40-169">**Resolutie**: Hallo push-bewerking opnieuw uitvoeren Hallo hoofdvertakking opgeven.</span><span class="sxs-lookup"><span data-stu-id="82f40-169">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="82f40-170">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="82f40-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="82f40-171">**Symptoom**: src refspec [branchname] komt niet overeen.</span><span class="sxs-lookup"><span data-stu-id="82f40-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="82f40-172">**Oorzaak**: deze fout kan optreden als u toopush tooa vertakking dan master op Hallo 'azure' externe probeert.</span><span class="sxs-lookup"><span data-stu-id="82f40-172">**Cause**: This error can occur if you attempt toopush tooa branch other than master on hello 'azure' remote.</span></span>

<span data-ttu-id="82f40-173">**Resolutie**: Hallo push-bewerking opnieuw uitvoeren Hallo hoofdvertakking opgeven.</span><span class="sxs-lookup"><span data-stu-id="82f40-173">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="82f40-174">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="82f40-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="82f40-175">**Symptoom**: RPC is mislukt; resulteren = 22, HTTP-code = 502.</span><span class="sxs-lookup"><span data-stu-id="82f40-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="82f40-176">**Oorzaak**: deze fout kan optreden als u een groot git-opslagplaats toopush via HTTPS probeert.</span><span class="sxs-lookup"><span data-stu-id="82f40-176">**Cause**: This error can occur if you attempt toopush a large git repository over HTTPS.</span></span>

<span data-ttu-id="82f40-177">**Resolutie**: Hallo git-configuratie wijzigen op Hallo lokale machine toomake Hallo postBuffer groter</span><span class="sxs-lookup"><span data-stu-id="82f40-177">**Resolution**: Change hello git configuration on hello local machine toomake hello postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="82f40-178">**Symptoom**: fout - wijzigingen doorgevoerd tooremote opslagplaats maar uw web-app niet bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="82f40-178">**Symptom**: Error - Changes committed tooremote repository but your web app not updated.</span></span>

<span data-ttu-id="82f40-179">**Oorzaak**: deze fout kan optreden als u een Node.js-app met een package.json-bestand waarin aanvullende vereiste modules implementeert.</span><span class="sxs-lookup"><span data-stu-id="82f40-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="82f40-180">**Resolutie**: aanvullende berichten met 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="82f40-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="82f40-181">moet aangemelde voorafgaande toothis fout en aanvullende context kan bieden bij Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="82f40-181">should be logged prior toothis error, and can provide additional context on hello failure.</span></span> <span data-ttu-id="82f40-182">Hallo Hieronder volgen bekende oorzaken van deze fout en bijbehorende 'npm ERR!' Hallo</span><span class="sxs-lookup"><span data-stu-id="82f40-182">hello following are known causes of this error and hello corresponding 'npm ERR!'</span></span> <span data-ttu-id="82f40-183">Bericht:</span><span class="sxs-lookup"><span data-stu-id="82f40-183">message:</span></span>

* <span data-ttu-id="82f40-184">**Ongeldige package.json-bestand**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="82f40-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="82f40-185">Afhankelijkheden kan niet worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="82f40-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="82f40-186">**Systeemeigen module die geen heeft een binaire distributiepunt voor Windows**:</span><span class="sxs-lookup"><span data-stu-id="82f40-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="82f40-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="82f40-187">npm ERR!</span></span> <span data-ttu-id="82f40-188">\`cmd '/ c"'knooppunt gyp rebuild'\` is mislukt: 1</span><span class="sxs-lookup"><span data-stu-id="82f40-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="82f40-189">OF</span><span class="sxs-lookup"><span data-stu-id="82f40-189">OR</span></span>
  * <span data-ttu-id="82f40-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="82f40-190">npm ERR!</span></span> <span data-ttu-id="82f40-191">[modulename@version] vooraf: \`zorg || gmake\`</span><span class="sxs-lookup"><span data-stu-id="82f40-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82f40-192">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="82f40-192">Additional Resources</span></span>
* [<span data-ttu-id="82f40-193">Git-documentatie</span><span class="sxs-lookup"><span data-stu-id="82f40-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="82f40-194">Project Kudu documentatie</span><span class="sxs-lookup"><span data-stu-id="82f40-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="82f40-195">Continue implementatie tooAzure App Service</span><span class="sxs-lookup"><span data-stu-id="82f40-195">Continous Deployment tooAzure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="82f40-196">Hoe toouse PowerShell voor Azure</span><span class="sxs-lookup"><span data-stu-id="82f40-196">How toouse PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="82f40-197">Hoe toouse hello Azure-opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="82f40-197">How toouse hello Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure Portal]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Azure-opdrachtregelinterface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
