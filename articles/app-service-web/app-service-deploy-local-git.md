---
title: Lokale Git-implementatie op de Azure App Service
description: Informatie over het inschakelen van lokale Git-implementatie in Azure App Service.
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
ms.openlocfilehash: f1c4911670d3aa32e74b3dfebd83cf3dc3830805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="local-git-deployment-to-azure-app-service"></a><span data-ttu-id="9391c-103">Lokale Git-implementatie op de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9391c-103">Local Git Deployment to Azure App Service</span></span>
<span data-ttu-id="9391c-104">Deze zelfstudie leert u hoe u uw app implementeert [Azure App Service] van een Git-opslagplaats op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="9391c-104">This tutorial shows you how to deploy your app to [Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="9391c-105">App Service ondersteunt deze methode met de **lokale Git** Implementatieoptie wordt gebruikt in de [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="9391c-105">App Service supports this approach with the **Local Git** deployment option in the [Azure Portal].</span></span>  
<span data-ttu-id="9391c-106">Veel van de Git-opdrachten die worden beschreven in dit artikel worden automatisch uitgevoerd tijdens het maken van een App Service-app met de [Azure-opdrachtregelinterface] zoals beschreven [hier](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9391c-106">Many of the Git commands described in this article are performed automatically when creating an App Service app using the [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9391c-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9391c-107">Prerequisites</span></span>
<span data-ttu-id="9391c-108">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="9391c-108">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="9391c-109">GIT.</span><span class="sxs-lookup"><span data-stu-id="9391c-109">Git.</span></span> <span data-ttu-id="9391c-110">U kunt de installatie van de binaire downloaden [hier](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="9391c-110">You can download the installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="9391c-111">Basiskennis van Git.</span><span class="sxs-lookup"><span data-stu-id="9391c-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="9391c-112">Een Microsoft Azure-account.</span><span class="sxs-lookup"><span data-stu-id="9391c-112">A Microsoft Azure account.</span></span> <span data-ttu-id="9391c-113">Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="9391c-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="9391c-114">Als u wilt dat aan de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="9391c-114">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="9391c-115">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="9391c-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="9391c-116"><a name="Step1"></a>Stap 1: Maak een lokale opslagplaats</span><span class="sxs-lookup"><span data-stu-id="9391c-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="9391c-117">De volgende taken uitvoeren om een nieuwe Git-opslagplaats maken.</span><span class="sxs-lookup"><span data-stu-id="9391c-117">Perform the following tasks to create a new Git repository.</span></span>

1. <span data-ttu-id="9391c-118">Start een opdrachtregelprogramma, zoals **GitBash** (Windows) of **Bash** (Unix-Shell).</span><span class="sxs-lookup"><span data-stu-id="9391c-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="9391c-119">Op OS X-systemen is toegankelijk via de opdrachtregel de **Terminal** toepassing.</span><span class="sxs-lookup"><span data-stu-id="9391c-119">On OS X systems you can access the command-line through the **Terminal** application.</span></span>
2. <span data-ttu-id="9391c-120">Ga naar de map waar de inhoud voor het implementeren van geplaatst worden.</span><span class="sxs-lookup"><span data-stu-id="9391c-120">Navigate to the directory where the content to deploy would be located.</span></span>
3. <span data-ttu-id="9391c-121">Gebruik de volgende opdracht in een nieuwe Git-opslagplaats te initialiseren:</span><span class="sxs-lookup"><span data-stu-id="9391c-121">Use the following command to initialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="9391c-122"><a name="Step2"></a>Stap 2: Uw inhoud doorvoeren</span><span class="sxs-lookup"><span data-stu-id="9391c-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="9391c-123">App Service biedt ondersteuning voor toepassingen die zijn gemaakt in diverse programmeertalen.</span><span class="sxs-lookup"><span data-stu-id="9391c-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="9391c-124">Als uw opslagplaats bevat inhoud overslaan dit punt en verplaatsen naar het punt 2 hieronder.</span><span class="sxs-lookup"><span data-stu-id="9391c-124">If your repository already includes content skip this point and move to point 2 below.</span></span> <span data-ttu-id="9391c-125">Als uw opslagplaats geen inhoud gewoon bevat nog te vullen met een statische HTML-bestand als volgt:</span><span class="sxs-lookup"><span data-stu-id="9391c-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="9391c-126">Start een teksteditor en maak een nieuw bestand met de naam **index.html** in de hoofdmap van de Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="9391c-126">Using a text editor, create a new file named **index.html** at the root of the Git repository</span></span>
   * <span data-ttu-id="9391c-127">De volgende tekst toevoegen als de inhoud voor de index.html bestand en sla het: *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="9391c-127">Add the following text as the contents for the index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="9391c-128">Vanaf de opdrachtregel, controleert u of u onder de hoofdmap van de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="9391c-128">From the command-line, verify that you are under the root of your Git repository.</span></span> <span data-ttu-id="9391c-129">Gebruik vervolgens de volgende opdracht om bestanden naar uw opslagplaats toevoegen:</span><span class="sxs-lookup"><span data-stu-id="9391c-129">Then use the following command to add files to your repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="9391c-130">Voer vervolgens de wijzigingen aan de opslagplaats met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9391c-130">Next, commit the changes to the repository by using the following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="9391c-131"><a name="Step3"></a>Stap 3: De App Service-app-opslagplaats inschakelen</span><span class="sxs-lookup"><span data-stu-id="9391c-131"><a name="Step3"></a>Step 3: Enable the App Service app repository</span></span>
<span data-ttu-id="9391c-132">De volgende stappen om in te schakelen van een Git-opslagplaats voor uw App Service-app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9391c-132">Perform the following steps to enable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="9391c-133">Meld u aan bij de [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="9391c-133">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="9391c-134">Klik op de blade van uw App Service-app **instellingen > implementatiebron**.</span><span class="sxs-lookup"><span data-stu-id="9391c-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="9391c-135">Klik op **bron kiezen**, klikt u vervolgens op **lokale Git-opslagplaats**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9391c-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Lokale Git-opslagplaats](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="9391c-137">Als dit de eerste keer instellen van een opslagplaats in Azure, moet u aanmeldingsreferenties voor het maken.</span><span class="sxs-lookup"><span data-stu-id="9391c-137">If this is your first time setting up a repository in Azure, you need to create login credentials for it.</span></span> <span data-ttu-id="9391c-138">U gebruikt deze aan te melden bij de Azure-opslagplaats en push wijzigingen vanaf uw lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="9391c-138">You will use them to log into the Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="9391c-139">Op de blade van uw app, klikt u op **instellingen > implementatiereferenties**, configureert u uw implementatie gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="9391c-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="9391c-140">Wanneer u bent klaar, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9391c-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="9391c-141"><a name="Step4"></a>Stap 4: Implementeer uw project</span><span class="sxs-lookup"><span data-stu-id="9391c-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="9391c-142">Gebruik de volgende stappen voor het publiceren van uw app in App Service met lokale Git.</span><span class="sxs-lookup"><span data-stu-id="9391c-142">Use the following steps to publish your app to App Service using Local Git.</span></span>

1. <span data-ttu-id="9391c-143">Klik in de blade van uw app in de Azure Portal op **instellingen > eigenschappen** voor de **Git-URL**.</span><span class="sxs-lookup"><span data-stu-id="9391c-143">In your app's blade in the Azure Portal, click **Settings > Properties** for the **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="9391c-144">**GIT-URL** is de externe verwijzing om te implementeren op van uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="9391c-144">**Git URL** is the remote reference to deploy to from your local repository.</span></span> <span data-ttu-id="9391c-145">U gebruikt deze URL in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="9391c-145">You'll use this URL in the following steps.</span></span>
2. <span data-ttu-id="9391c-146">Met behulp van de opdrachtregel, controleert u of u in de hoofdmap van uw lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="9391c-146">Using the command-line, verify that you are in the root of your local Git repository.</span></span>
3. <span data-ttu-id="9391c-147">Gebruik `git remote` om toe te voegen van de externe verwijzing die worden vermeld in **Git-URL** uit stap 1.</span><span class="sxs-lookup"><span data-stu-id="9391c-147">Use `git remote` to add the remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="9391c-148">De opdracht ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="9391c-148">Your command will look similar to the following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="9391c-149">De **externe** opdracht voegt een benoemde verwijzing naar een externe opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="9391c-149">The **remote** command adds a named reference to a remote repository.</span></span> <span data-ttu-id="9391c-150">In dit voorbeeld wordt een verwijzing met de naam 'azure' voor uw web-app-opslagplaats gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9391c-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="9391c-151">De inhoud van uw App service met behulp van de nieuwe push **azure** externe u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9391c-151">Push your content to App Service using the new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for the password you created earlier when you reset your deployment credentials in the Azure Portal. Enter the password (note that Gitbash does not echo asterisks to the console as you type your password). 
5. <span data-ttu-id="9391c-152">Ga terug naar uw app in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9391c-152">Go back to your app in the Azure Portal.</span></span> <span data-ttu-id="9391c-153">Een logboekvermelding van de meest recente push moet worden weergegeven in de **implementaties** blade.</span><span class="sxs-lookup"><span data-stu-id="9391c-153">A log entry of your most recent push should be displayed in the **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="9391c-154">Klik op de **Bladeren** knop aan de bovenkant van de app-blade om te controleren of de inhoud is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="9391c-154">Click the **Browse** button at the top of the app's blade to verify the content has been deployed.</span></span> 

## <span data-ttu-id="9391c-155"><a name="Step5"></a>Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="9391c-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="9391c-156">Hier volgen enkele fouten of problemen meestal opgetreden bij het gebruik van Git publiceren naar een App Service-app in Azure:</span><span class="sxs-lookup"><span data-stu-id="9391c-156">The following are errors or problems commonly encountered when using Git to publish to an App Service app in Azure:</span></span>

- - -
<span data-ttu-id="9391c-157">**Symptoom**: geen toegang mogelijk tot [siteURL]: kan geen verbinding met [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="9391c-157">**Symptom**: Unable to access '[siteURL]': Failed to connect to [scmAddress]</span></span>

<span data-ttu-id="9391c-158">**Oorzaak**: deze fout kan optreden als de app niet actief is.</span><span class="sxs-lookup"><span data-stu-id="9391c-158">**Cause**: This error can occur if the app is not up and running.</span></span>

<span data-ttu-id="9391c-159">**Resolutie**: de app te starten in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9391c-159">**Resolution**: Start the app in the Azure Portal.</span></span> <span data-ttu-id="9391c-160">GIT-implementatie werkt niet, tenzij de app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9391c-160">Git deployment will not work unless the app is running.</span></span> 

- - -
<span data-ttu-id="9391c-161">**Symptoom**: host 'naam' niet oplossen</span><span class="sxs-lookup"><span data-stu-id="9391c-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="9391c-162">**Oorzaak**: deze fout kan optreden als de gegevens hebt ingevoerd bij het maken van de 'azure' externe onjuist is.</span><span class="sxs-lookup"><span data-stu-id="9391c-162">**Cause**: This error can occur if the address information entered when creating the 'azure' remote was incorrect.</span></span>

<span data-ttu-id="9391c-163">**Resolutie**: Gebruik de `git remote -v` opdracht om een lijst van alle afstandsbedieningen, samen met de bijbehorende URL.</span><span class="sxs-lookup"><span data-stu-id="9391c-163">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span></span> <span data-ttu-id="9391c-164">Controleer of de URL voor de externe 'azure' klopt.</span><span class="sxs-lookup"><span data-stu-id="9391c-164">Verify that the URL for the 'azure' remote is correct.</span></span> <span data-ttu-id="9391c-165">Indien nodig, verwijderen en opnieuw maken van deze extern met behulp van de juiste URL.</span><span class="sxs-lookup"><span data-stu-id="9391c-165">If needed, remove and recreate this remote using the correct URL.</span></span>

- - -
<span data-ttu-id="9391c-166">**Symptoom**: Er is geen refs in algemene en er is geen opgegeven; niets te doen.</span><span class="sxs-lookup"><span data-stu-id="9391c-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="9391c-167">Mogelijk moet u een vertakking zoals 'master' opgeven.</span><span class="sxs-lookup"><span data-stu-id="9391c-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="9391c-168">**Oorzaak**: deze fout kan optreden als u niet een vertakking opgeven bij het uitvoeren van een git push-bewerking en de push.default-waarde die wordt gebruikt door Git niet is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9391c-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set the push.default value used by Git.</span></span>

<span data-ttu-id="9391c-169">**Resolutie**: uitvoeren van de push-bewerking opnieuw, geven de hoofdvertakking.</span><span class="sxs-lookup"><span data-stu-id="9391c-169">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="9391c-170">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9391c-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="9391c-171">**Symptoom**: src refspec [branchname] komt niet overeen.</span><span class="sxs-lookup"><span data-stu-id="9391c-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="9391c-172">**Oorzaak**: deze fout kan optreden als u probeert te pushen naar een vertakking dan master in de 'azure' externe.</span><span class="sxs-lookup"><span data-stu-id="9391c-172">**Cause**: This error can occur if you attempt to push to a branch other than master on the 'azure' remote.</span></span>

<span data-ttu-id="9391c-173">**Resolutie**: uitvoeren van de push-bewerking opnieuw, geven de hoofdvertakking.</span><span class="sxs-lookup"><span data-stu-id="9391c-173">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="9391c-174">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9391c-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="9391c-175">**Symptoom**: RPC is mislukt; resulteren = 22, HTTP-code = 502.</span><span class="sxs-lookup"><span data-stu-id="9391c-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="9391c-176">**Oorzaak**: deze fout kan optreden als u probeert om een grote git-opslagplaats via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9391c-176">**Cause**: This error can occur if you attempt to push a large git repository over HTTPS.</span></span>

<span data-ttu-id="9391c-177">**Resolutie**: Wijzig de git-configuratie op de lokale computer naar de postBuffer groter maken</span><span class="sxs-lookup"><span data-stu-id="9391c-177">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="9391c-178">**Symptoom**: fout - de wijzigingen die zijn toegewezen aan externe opslagplaats, maar uw web-app niet bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="9391c-178">**Symptom**: Error - Changes committed to remote repository but your web app not updated.</span></span>

<span data-ttu-id="9391c-179">**Oorzaak**: deze fout kan optreden als u een Node.js-app met een package.json-bestand waarin aanvullende vereiste modules implementeert.</span><span class="sxs-lookup"><span data-stu-id="9391c-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="9391c-180">**Resolutie**: aanvullende berichten met 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="9391c-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="9391c-181">moet de aangemelde voorafgaand aan deze fout en aanvullende context kan bieden over de fout.</span><span class="sxs-lookup"><span data-stu-id="9391c-181">should be logged prior to this error, and can provide additional context on the failure.</span></span> <span data-ttu-id="9391c-182">Hier volgen enkele bekende oorzaken van deze fout en de bijbehorende 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="9391c-182">The following are known causes of this error and the corresponding 'npm ERR!'</span></span> <span data-ttu-id="9391c-183">Bericht:</span><span class="sxs-lookup"><span data-stu-id="9391c-183">message:</span></span>

* <span data-ttu-id="9391c-184">**Ongeldige package.json-bestand**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="9391c-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="9391c-185">Afhankelijkheden kan niet worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="9391c-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="9391c-186">**Systeemeigen module die geen heeft een binaire distributiepunt voor Windows**:</span><span class="sxs-lookup"><span data-stu-id="9391c-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="9391c-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="9391c-187">npm ERR!</span></span> <span data-ttu-id="9391c-188">\`cmd '/ c"'knooppunt gyp rebuild'\` is mislukt: 1</span><span class="sxs-lookup"><span data-stu-id="9391c-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="9391c-189">OF</span><span class="sxs-lookup"><span data-stu-id="9391c-189">OR</span></span>
  * <span data-ttu-id="9391c-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="9391c-190">npm ERR!</span></span> <span data-ttu-id="9391c-191">[modulename@version] vooraf: \`zorg || gmake\`</span><span class="sxs-lookup"><span data-stu-id="9391c-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9391c-192">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="9391c-192">Additional Resources</span></span>
* [<span data-ttu-id="9391c-193">Git-documentatie</span><span class="sxs-lookup"><span data-stu-id="9391c-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="9391c-194">Project Kudu documentatie</span><span class="sxs-lookup"><span data-stu-id="9391c-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="9391c-195">Continue implementatie in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9391c-195">Continous Deployment to Azure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="9391c-196">PowerShell voor Azure gebruiken</span><span class="sxs-lookup"><span data-stu-id="9391c-196">How to use PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="9391c-197">Het gebruik van de Azure-opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="9391c-197">How to use the Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="9391c-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="9391c-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span></span>
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
<span data-ttu-id="9391c-199">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="9391c-199">[Azure Portal]: https://portal.azure.com</span></span>
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="9391c-200">[Azure-opdrachtregelinterface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span><span class="sxs-lookup"><span data-stu-id="9391c-200">[Azure Command-Line Interface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span></span>

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
