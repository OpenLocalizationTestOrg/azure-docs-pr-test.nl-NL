---
title: "Zeker implementatie (bètaversie testen) in Azure App Service"
description: "Informatie over het flight nieuwe functies in uw app of de updates in deze zelfstudie end-to-end bètaversie te testen. Deze samenbrengt App Service-functies, zoals continue publiceren, sleuven voor verkeersroutering en Application Insights-integratie."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: 83e3247310461ac148fff3c4ade3aa7216478537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a><span data-ttu-id="e32f8-104">Zeker implementatie (bètaversie testen) in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e32f8-104">Flighting deployment (beta testing) in Azure App Service</span></span>
<span data-ttu-id="e32f8-105">Deze zelfstudie wordt beschreven hoe u *zeker implementaties* door de integratie van de verschillende mogelijkheden van [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en [Azure Application Insights](/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="e32f8-105">This tutorial shows you how to do *flighting deployments* by integrating the various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span></span>

<span data-ttu-id="e32f8-106">*Zeker* is een implementatieproces te valideren en een nieuwe functie of wijzigen met een beperkt aantal echte klanten en is een belangrijke test in productiescenario's.</span><span class="sxs-lookup"><span data-stu-id="e32f8-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span></span> <span data-ttu-id="e32f8-107">Het is cloudbeheer beta testen en wordt ook wel aangeduid als 'beheerde test vlucht'.</span><span class="sxs-lookup"><span data-stu-id="e32f8-107">It is akin to beta testing and is sometimes known as "controlled test flight".</span></span> <span data-ttu-id="e32f8-108">Veel grote ondernemingen met een aanwezigheid op het web gebruik deze benadering voor vroege validatie op hun app-updates in de praktijk van [flexibele ontwikkeling](https://en.wikipedia.org/wiki/Agile_software_development).</span><span class="sxs-lookup"><span data-stu-id="e32f8-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="e32f8-109">Azure App Service kunt u testen in de productieomgeving integreren met continue publicatie en Application Insights dezelfde DevOps-scenario implementeren.</span><span class="sxs-lookup"><span data-stu-id="e32f8-109">Azure App Service enables you to integrate test in production with continous publishing and Application Insights to implement the same DevOps scenario.</span></span> <span data-ttu-id="e32f8-110">Voordelen van deze benadering zijn:</span><span class="sxs-lookup"><span data-stu-id="e32f8-110">Benefits of this approach include:</span></span>

* <span data-ttu-id="e32f8-111">**Echte feedback krijgen *voordat* updates gepubliceerd naar productie** -het enige dat beter dan feedback krijgt als u de release is feedback krijgen voordat u loslaat.</span><span class="sxs-lookup"><span data-stu-id="e32f8-111">**Gain real feedback *before* updates are released to production** - The only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span></span> <span data-ttu-id="e32f8-112">U kunt updates met echte gebruikersverkeer en gedragingen vroeg u wenst in de levenscyclus testen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-112">You can test updates with real user traffic and behaviors as early as you desire in the product life cycle.</span></span>
* <span data-ttu-id="e32f8-113">**Verbeter [doorlopende test gebaseerde ontwikkeling (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  - door te testen in de productieomgeving integreren met continue integratie en instrumentation met Application Insights valideren van de gebruiker gebeurt vroeg en automatisch in de levenscyclus van het product.</span><span class="sxs-lookup"><span data-stu-id="e32f8-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span></span> <span data-ttu-id="e32f8-114">Dit reduceert de hoeveelheid tijd investeringen in handmatige testuitvoering.</span><span class="sxs-lookup"><span data-stu-id="e32f8-114">This helps reduce time investments in manual test execution.</span></span>
* <span data-ttu-id="e32f8-115">**Optimaliseert de werkstroom test** -door te testen in de productieomgeving met continue bewaking instrumentation automatiseren, kunt u mogelijk uitvoeren de doelstellingen van verschillende soorten tests in een enkel proces, zoals [integratie](https://en.wikipedia.org/wiki/Integration_testing), [regressie](https://en.wikipedia.org/wiki/Regression_testing), [bruikbaarheid](https://en.wikipedia.org/wiki/Usability_testing), toegankelijkheid, lokalisatie, [prestaties](https://en.wikipedia.org/wiki/Software_performance_testing), [beveiliging](https://en.wikipedia.org/wiki/Security_testing), en [ acceptatie](https://en.wikipedia.org/wiki/Acceptance_testing).</span><span class="sxs-lookup"><span data-stu-id="e32f8-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish the goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span></span>

<span data-ttu-id="e32f8-116">Een flighting implementatie is niet alleen om routering voor live verkeer.</span><span class="sxs-lookup"><span data-stu-id="e32f8-116">A flighting deployment is not just about routing live traffic.</span></span> <span data-ttu-id="e32f8-117">In een dergelijke implementatie die u meer inzicht krijgen zo snel mogelijk wilt maken, of het zijn een onverwachte fout, verminderde prestaties, gebruikerservaring problemen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-117">In such a deployment you want to gain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span></span> <span data-ttu-id="e32f8-118">Denk eraan dat u werkt met real-klanten.</span><span class="sxs-lookup"><span data-stu-id="e32f8-118">Remember, you are dealing with real customers.</span></span> <span data-ttu-id="e32f8-119">Dus om dat te doen rechts en u moet ervoor zorgen dat u hebt uw flighting implementatie ingesteld voor het verzamelen van alle gegevens die u nodig hebt om te beslissen voor de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="e32f8-119">So to do it right, you must make sure that you have set up your flighting deployment to gather all the data you need in order to make an informed decision for your next step.</span></span> <span data-ttu-id="e32f8-120">Deze zelfstudie ziet u het verzamelen van gegevens met Application Insights, maar u kunt New Relic of andere technologieën die past bij uw scenario.</span><span class="sxs-lookup"><span data-stu-id="e32f8-120">This tutorial shows you how to collect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e32f8-121">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="e32f8-121">What you will do</span></span>
<span data-ttu-id="e32f8-122">In deze zelfstudie leert u hoe u de volgende scenario's om uw App Service-app in productie testen samen te brengen:</span><span class="sxs-lookup"><span data-stu-id="e32f8-122">In this tutorial, you will learn how to bring the following scenarios together to test your App Service app in production:</span></span>

* <span data-ttu-id="e32f8-123">[Productie-verkeer routeren](app-service-web-test-in-production-get-start.md) aan uw app beta</span><span class="sxs-lookup"><span data-stu-id="e32f8-123">[Route production traffic](app-service-web-test-in-production-get-start.md) to your beta app</span></span>
* <span data-ttu-id="e32f8-124">[Uw app instrumenteren](../application-insights/app-insights-web-track-usage.md) nuttig metrische gegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="e32f8-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) to obtain useful metrics</span></span>
* <span data-ttu-id="e32f8-125">Continu implementeren van uw bèta-app en live app metrische gegevens bijhouden</span><span class="sxs-lookup"><span data-stu-id="e32f8-125">Continuously deploy your beta app and track live app metrics</span></span>
* <span data-ttu-id="e32f8-126">Metrische gegevens tussen de productie-app en de bèta-app om te zien hoe codewijzigingen vertalen naar resultaten vergelijken</span><span class="sxs-lookup"><span data-stu-id="e32f8-126">Compare metrics between the production app and the beta app to see how code changes translate to results</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="e32f8-127">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="e32f8-127">What you will need</span></span>
* <span data-ttu-id="e32f8-128">Een Azure-account</span><span class="sxs-lookup"><span data-stu-id="e32f8-128">An Azure account</span></span>
* <span data-ttu-id="e32f8-129">Een [GitHub](https://github.com/) account</span><span class="sxs-lookup"><span data-stu-id="e32f8-129">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="e32f8-130">Visual Studio 2015 - u kunt downloaden via de [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="e32f8-130">Visual Studio 2015 - you can download the [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span></span>
* <span data-ttu-id="e32f8-131">GIT-Shell (geïnstalleerd met [GitHub voor Windows](https://windows.github.com/))-Hiermee kunt u de Git- en PowerShell-opdrachten kunt uitvoeren in dezelfde sessie</span><span class="sxs-lookup"><span data-stu-id="e32f8-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you to run both the Git and PowerShell commands in the same session</span></span>
* <span data-ttu-id="e32f8-132">Meest recente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span><span class="sxs-lookup"><span data-stu-id="e32f8-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span></span>
* <span data-ttu-id="e32f8-133">Basiskennis van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="e32f8-133">Basic understanding of the following:</span></span>
  * <span data-ttu-id="e32f8-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) sjabloonimplementatie (Zie [een complexe toepassing zoals verwacht in Azure implementeert](app-service-deploy-complex-application-predictably.md))</span><span class="sxs-lookup"><span data-stu-id="e32f8-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="e32f8-135">Git</span><span class="sxs-lookup"><span data-stu-id="e32f8-135">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="e32f8-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e32f8-136">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="e32f8-137">U hebt een Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="e32f8-137">You need an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="e32f8-138">U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/) -u ontvangt tegoed kunt u uitproberen betaalde Azure-services en zelfs nadat ze zijn gebruikt kunt u het account houden en gebruik gratis Azure-services, zoals Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="e32f8-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="e32f8-139">U kunt [voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -uw Visual Studio-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e32f8-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="e32f8-140">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="e32f8-140">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e32f8-141">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-141">No credit cards required; no commitments.</span></span>
>
>

## <a name="set-up-your-production-web-app"></a><span data-ttu-id="e32f8-142">Instellen van uw web-app voor productie</span><span class="sxs-lookup"><span data-stu-id="e32f8-142">Set up your production web app</span></span>
> [!NOTE]
> <span data-ttu-id="e32f8-143">Het script in deze zelfstudie gebruikt configureert automatisch continue publiceren vanaf uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e32f8-143">The script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="e32f8-144">Dit is vereist dat uw GitHub-referenties worden al opgeslagen in Azure, anders mislukt de implementatie met de scripts bij een poging tot het configureren van instellingen voor bronbeheer voor de web-apps.</span><span class="sxs-lookup"><span data-stu-id="e32f8-144">This requires that your GitHub credentials are already stored in Azure, otherwise the scripted deployment will fail when attempting to configure source control settings for the web apps.</span></span>
>
> <span data-ttu-id="e32f8-145">Als u wilt uw GitHub-referenties in Azure opslaat, maakt u een web-app in de [Azure Portal](https://portal.azure.com/) en [GitHub implementatie configureren](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e32f8-145">To store your GitHub credentials in Azure, create a web app in the [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="e32f8-146">U hoeft hiervoor eenmaal.</span><span class="sxs-lookup"><span data-stu-id="e32f8-146">You only need to do this once.</span></span>
>
>

<span data-ttu-id="e32f8-147">In een typische DevOps-scenario hebt u een toepassing die live in Azure wordt uitgevoerd en u wilt wijzigen via continue publiceren.</span><span class="sxs-lookup"><span data-stu-id="e32f8-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want to make changes to it through continuous publishing.</span></span> <span data-ttu-id="e32f8-148">In dit scenario implementeert u naar productie een sjabloon die u hebt ontwikkeld en getest.</span><span class="sxs-lookup"><span data-stu-id="e32f8-148">In this scenario, you will deploy to production a template that you have developed and tested.</span></span>

1. <span data-ttu-id="e32f8-149">Maak uw eigen fork van de [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e32f8-149">Create your own fork of the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="e32f8-150">Zie voor meer informatie over het maken van uw fork [een opslagplaats vertakken](https://help.github.com/articles/fork-a-repo/).</span><span class="sxs-lookup"><span data-stu-id="e32f8-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="e32f8-151">Zodra uw fork is gemaakt, kunt u deze bekijken in uw browser.</span><span class="sxs-lookup"><span data-stu-id="e32f8-151">Once your fork is created, you can see it in your browser.</span></span>

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="e32f8-152">Open een Git-Shell-sessie.</span><span class="sxs-lookup"><span data-stu-id="e32f8-152">Open a Git Shell session.</span></span> <span data-ttu-id="e32f8-153">Als u nog Git-Shell hebt, installeert u [GitHub voor Windows](https://windows.github.com/) nu.</span><span class="sxs-lookup"><span data-stu-id="e32f8-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="e32f8-154">Maak een lokale kloon van uw fork door het uitvoeren van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e32f8-154">Create a local clone of your fork by executing the following command:</span></span>

     <span data-ttu-id="e32f8-155">GIT kloon https://github.com/<your_fork>/ToDoApp.git</span><span class="sxs-lookup"><span data-stu-id="e32f8-155">git clone https://github.com/<your_fork>/ToDoApp.git</span></span>
4. <span data-ttu-id="e32f8-156">Wanneer u uw lokale kloon hebt, gaat u naar  *&lt;repository_root >*\ARMTemplates, en voer de deploy.ps1 script met een uniek achtervoegsel, zoals hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e32f8-156">Once you have your local clone, navigate to *&lt;repository_root>*\ARMTemplates, and run the deploy.ps1 script with a unique suffix, as shown below:</span></span>

     <span data-ttu-id="e32f8-157">.\deploy.ps1 – RepoUrl https://github.com/<your_fork>/todoapp.git - ResourceGroupSuffix < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="e32f8-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span></span>
5. <span data-ttu-id="e32f8-158">Wanneer u wordt gevraagd, typt u in de gewenste gebruikersnaam en het wachtwoord voor toegang tot de database.</span><span class="sxs-lookup"><span data-stu-id="e32f8-158">When prompted, type in the desired username and password for database access.</span></span> <span data-ttu-id="e32f8-159">Vergeet niet de databasereferenties van uw omdat u ze opnieuw opgeven moet bij het bijwerken van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e32f8-159">Remember your database credentials because you will need to specify them again when updating the resource group.</span></span>

   <span data-ttu-id="e32f8-160">U ziet de voortgang van de inrichting van verschillende Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="e32f8-160">You should see the provisioning progress of various Azure resources.</span></span> <span data-ttu-id="e32f8-161">Wanneer implementatie is voltooid, wordt het script start de toepassing in de browser en bieden u een beschrijvende geluid.</span><span class="sxs-lookup"><span data-stu-id="e32f8-161">When deployment completes, the script will launch the application in the browser and give you a friendly beep.</span></span>
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. <span data-ttu-id="e32f8-162">Terug in uw sessie Git Shell uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e32f8-162">Back in your Git Shell session, run:</span></span>

     <span data-ttu-id="e32f8-163">. \swap – naam ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="e32f8-163">.\swap –Name ToDoApp<your_suffix></span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. <span data-ttu-id="e32f8-164">Wanneer het script is voltooid, gaat u terug om te bladeren naar de frontend-adres (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) om te zien van de toepassing die wordt uitgevoerd in de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e32f8-164">When the script finishes, go back to browse to the frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) to see the application running in production.</span></span>
8. <span data-ttu-id="e32f8-165">Meld u aan bij de [Azure Portal](https://portal.azure.com/) en eens kijken wat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e32f8-165">Log into the [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span></span>

   <span data-ttu-id="e32f8-166">U moet kunnen zien van twee web-apps in dezelfde resourcegroep bevinden, één met de `Api` achtervoegsel in de naam.</span><span class="sxs-lookup"><span data-stu-id="e32f8-166">You should be able to see two web apps in the same resource group, one with the `Api` suffix in the name.</span></span> <span data-ttu-id="e32f8-167">Als u de resourcegroepweergave bekijkt, ook ziet u de SQL-Database en -server, de App Service-abonnement en de staging-sleuven voor de web-apps.</span><span class="sxs-lookup"><span data-stu-id="e32f8-167">If you look at the resource group view, you will also see the SQL Database and server, the App Service plan, and the staging slots for the web apps.</span></span> <span data-ttu-id="e32f8-168">Blader door de verschillende bronnen en vergelijkt ze met  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json om te zien hoe deze zijn geconfigureerd in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e32f8-168">Browse through the different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json to see how they are configured in the template.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

<span data-ttu-id="e32f8-169">U hebt de productie-app ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e32f8-169">You have set up the production app.</span></span>  <span data-ttu-id="e32f8-170">Nu gaan we Stel dat u feedback of bruikbaarheid slechte voor de app is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-170">Now, let's imagine that you receive feedback that usability is poor for the app.</span></span> <span data-ttu-id="e32f8-171">Zodat u besluit om te onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="e32f8-171">So you decide to investigate.</span></span> <span data-ttu-id="e32f8-172">U gaat softwareontwikkelaars van uw app om u feedback geven.</span><span class="sxs-lookup"><span data-stu-id="e32f8-172">You're going to instrument your app to give you feedback.</span></span>

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a><span data-ttu-id="e32f8-173">Onderzoeken: Uw client-app voor bewaking/metrieken softwareontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="e32f8-173">Investigate: Instrument your client app for monitoring/metrics</span></span>
1. <span data-ttu-id="e32f8-174">Open  *&lt;repository_root >*\src\MultiChannelToDo.sln in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e32f8-174">Open *&lt;repository_root>*\src\MultiChannelToDo.sln in Visual Studio.</span></span>
2. <span data-ttu-id="e32f8-175">Herstellen van alle Nuget-pakketten met de rechtermuisknop op de oplossing > **NuGet-pakketten beheren voor oplossing** > **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="e32f8-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span></span>
3. <span data-ttu-id="e32f8-176">Met de rechtermuisknop op **MultiChannelToDo.Web** > **Application Insights Telemetry toevoegen** > **-instellingen configureren** > resourcegroep wijzigen ToDoApp*&lt;your_suffix >* > **Application Insights toevoegen aan Project**.</span><span class="sxs-lookup"><span data-stu-id="e32f8-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
4. <span data-ttu-id="e32f8-177">Open de blade voor in de Azure-Portal, de **MultiChannelToDo.Web** toepassing inzicht resource.</span><span class="sxs-lookup"><span data-stu-id="e32f8-177">In the Azure Portal, open the blade for the **MultiChannelToDo.Web** Application Insight resource.</span></span> <span data-ttu-id="e32f8-178">Klik in de **toepassingsstatus** deel, klikt u op **informatie over het verzamelen van gegevens van browser pagina laden** > code kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e32f8-178">Then in the **Application health** part, click **Learn how to collect browser page load data** > copy code.</span></span>
5. <span data-ttu-id="e32f8-179">De gekopieerde JS instrumentation Voeg code toe aan  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml vlak voordat de afsluiting `<heading>` label.</span><span class="sxs-lookup"><span data-stu-id="e32f8-179">Add the copied JS instrumentation code to *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, just before the closing `<heading>` tag.</span></span> <span data-ttu-id="e32f8-180">De unieke instrumentatiesleutel van uw toepassing inzicht resource moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="e32f8-180">It should contain the unique instrumentation key of your Application Insight resource.</span></span>

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. <span data-ttu-id="e32f8-181">Aangepaste gebeurtenissen verzenden naar Application Insights voor muis klikken door de volgende code toe te voegen aan de onderkant van de hoofdtekst:</span><span class="sxs-lookup"><span data-stu-id="e32f8-181">Send custom events to Application Insights for mouse clicks by adding the following code to the bottom of body:</span></span>

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   <span data-ttu-id="e32f8-182">In dit fragment JavaScript wordt een aangepaste gebeurtenis verzonden naar Application Insights telkens wanneer een gebruiker klikt op een willekeurige plaats in de web-app.</span><span class="sxs-lookup"><span data-stu-id="e32f8-182">This JavaScript snippet sends a custom event to Application Insights every time a user clicks anywhere in the web app.</span></span>
7. <span data-ttu-id="e32f8-183">In de Git-Shell doorvoeren en push de wijzigingen naar uw fork in GitHub.</span><span class="sxs-lookup"><span data-stu-id="e32f8-183">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="e32f8-184">Wacht tot clients browser te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-184">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. <span data-ttu-id="e32f8-185">De geïmplementeerde app-wijzigingen in productie wisselen:</span><span class="sxs-lookup"><span data-stu-id="e32f8-185">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="e32f8-186">. \swap – naam ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="e32f8-186">.\swap –Name ToDoApp<your_suffix></span></span>
9. <span data-ttu-id="e32f8-187">Blader naar de Application Insights-resource die u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e32f8-187">Browse to the Application Insights resource that you configured.</span></span> <span data-ttu-id="e32f8-188">Klik op aangepaste gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-188">Click Custom events.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   <span data-ttu-id="e32f8-189">Als er geen metrische gegevens voor aangepaste gebeurtenissen, wacht een paar minuten en klik op **vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="e32f8-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span></span>

<span data-ttu-id="e32f8-190">Stel dat u zien als een diagram hieronder:</span><span class="sxs-lookup"><span data-stu-id="e32f8-190">Suppose you see a chart like below:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

<span data-ttu-id="e32f8-191">En het raster gebeurtenis hieronder:</span><span class="sxs-lookup"><span data-stu-id="e32f8-191">And the event grid below it:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

<span data-ttu-id="e32f8-192">Volgens uw toepassingscode ToDoApp de **knop** gebeurtenis komt overeen met de verzendknop en de **invoer** gebeurtenis komt overeen met het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="e32f8-192">According to your ToDoApp application code, the **BUTTON** event corresponds to the submit button, and the **INPUT** event corresponds to the textbox.</span></span> <span data-ttu-id="e32f8-193">Tot nu toe, zinvol wat zijn.</span><span class="sxs-lookup"><span data-stu-id="e32f8-193">So far, things make sense.</span></span> <span data-ttu-id="e32f8-194">Echter, het lijkt erop dat er een goede bedrag van muisklikken en zeer weinig klikken op de taakitems is (de **LI** gebeurtenissen).</span><span class="sxs-lookup"><span data-stu-id="e32f8-194">However, it looks like there's a good amount of clicks and very few clicks on the to-do items (the **LI** events).</span></span>

<span data-ttu-id="e32f8-195">Op basis van dit formulier u uw hypothese dat sommige gebruikers hebben verward welk gedeelte van de gebruikersinterface wordt geklikt en is omdat de cursor voor de geselecteerde tekst is opgemaakt als u dit op items in de lijst en hun pictogrammen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-195">Based on this, you form your hypothesis that some users are confused which part of the UI is clickable and it is because the cursor is styled for text selection when it hovers on the list items and their icons.</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

<span data-ttu-id="e32f8-196">Dit wordt mogelijk een voorbeeld van een gekunstelde.</span><span class="sxs-lookup"><span data-stu-id="e32f8-196">This might be a contrived example.</span></span> <span data-ttu-id="e32f8-197">U gaat echter een verbetering van uw app maken en voert u een flighting implementatie voor de bruikbaarheid feedback van klanten live ophalen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-197">Nevertheless, you're going to make an improvement to your app, and then perform a flighting deployment to get usability feedback from live customers.</span></span>

### <a name="instrument-your-server-app-for-monitoringmetrics"></a><span data-ttu-id="e32f8-198">Softwareontwikkelaars van uw server-app voor bewaking/metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="e32f8-198">Instrument your server app for monitoring/metrics</span></span>
<span data-ttu-id="e32f8-199">Dit is een tangens omdat het scenario dat in deze zelfstudie uitgelegd alleen met de client-app omgaat.</span><span class="sxs-lookup"><span data-stu-id="e32f8-199">This is a tangent since the scenario demonstrated in this tutorial only deals with the client app.</span></span> <span data-ttu-id="e32f8-200">Echter, voor de volledigheid stelt u de app-serverzijde.</span><span class="sxs-lookup"><span data-stu-id="e32f8-200">However, for completeness you will set up the server-side app.</span></span>

1. <span data-ttu-id="e32f8-201">Met de rechtermuisknop op **MultiChannelToDo** > **Application Insights Telemetry toevoegen** > **-instellingen configureren** > resourcegroep wijzigen ToDoApp*&lt;your_suffix >* > **Application Insights toevoegen aan Project**.</span><span class="sxs-lookup"><span data-stu-id="e32f8-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
2. <span data-ttu-id="e32f8-202">In de Git-Shell doorvoeren en push de wijzigingen naar uw fork in GitHub.</span><span class="sxs-lookup"><span data-stu-id="e32f8-202">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="e32f8-203">Wacht tot clients browser te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-203">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. <span data-ttu-id="e32f8-204">De geïmplementeerde app-wijzigingen in productie wisselen:</span><span class="sxs-lookup"><span data-stu-id="e32f8-204">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="e32f8-205">. \swap – naam ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="e32f8-205">.\swap –Name ToDoApp<your_suffix></span></span>

<span data-ttu-id="e32f8-206">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="e32f8-206">That's it!</span></span>

## <a name="investigate-add-slot-specific-tags-to-your-client-app-metrics"></a><span data-ttu-id="e32f8-207">Onderzoeken: Sleuf-specifieke labels toevoegen aan de app metrische gegevens van uw client</span><span class="sxs-lookup"><span data-stu-id="e32f8-207">Investigate: Add slot-specific tags to your client app metrics</span></span>
<span data-ttu-id="e32f8-208">In deze sectie configureert u de verschillende implementatiesites voor het verzenden van site-specifieke telemetrie naar dezelfde Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="e32f8-208">In this section, you will configure the different deployment slots to send slot-specific telemetry to the same Application Insights resource.</span></span> <span data-ttu-id="e32f8-209">Op deze manier kunt u telemetriegegevens tussen verkeer van andere sleuven (implementatieomgevingen) vergelijken eenvoudig overzicht van het effect van uw appwijzigingen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) to easily see the effect of your app changes.</span></span> <span data-ttu-id="e32f8-210">Op hetzelfde moment kunt u het verkeer van de productie van de rest scheiden, zodat u kunt doorgaan met het bewaken van uw productie-app naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="e32f8-210">At the same time, you can separate the production traffic from the rest so you can continue to monitor your production app as needed.</span></span>

<span data-ttu-id="e32f8-211">Nadat u van gegevens op clientgedrag verzamelen bent, wordt u [een initialisatiefunctie telemetrie toevoegen aan uw JavaScript-code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span><span class="sxs-lookup"><span data-stu-id="e32f8-211">Since you're gathering data on client behavior, you will [add a telemetry initializer to your JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span></span> <span data-ttu-id="e32f8-212">Als u testen serverzijde prestaties wilt, bijvoorbeeld: u kunt ook doen op dezelfde manier in uw servercode (Zie [Application Insights-API voor aangepaste gebeurtenissen en metrische gegevens](../application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e32f8-212">If you want to test server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span></span>

1. <span data-ttu-id="e32f8-213">Voeg eerst de code bewteen de twee `//` opmerkingen hieronder in JavaScript blokkeren die u hebt toegevoegd aan de `<heading>` eerder labelen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-213">First, add the code bewteen the two `//` comments below in the JavaScript block that you added to the `<heading>` tag earlier.</span></span>

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    <span data-ttu-id="e32f8-214">Deze code initialisatiefunctie zorgt ervoor dat de `appInsights` object toevoegen de naam van een aangepaste eigenschap `Environment` voor elk onderdeel van telemetrie verzendt.</span><span class="sxs-lookup"><span data-stu-id="e32f8-214">This initializer code causes the `appInsights` object to add the a custom property called `Environment` to every piece of telemetry it sends.</span></span>
2. <span data-ttu-id="e32f8-215">Vervolgens voegt u deze aangepaste eigenschap als een [instelling sleuf](web-sites-staged-publishing.md#AboutConfiguration) voor uw web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="e32f8-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span></span> <span data-ttu-id="e32f8-216">Voer hiervoor de volgende opdrachten in uw sessie Git-Shell.</span><span class="sxs-lookup"><span data-stu-id="e32f8-216">To do this, run the following commands in your Git Shell session.</span></span>

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    <span data-ttu-id="e32f8-217">Het bestand Web.config in uw project al definieert de `environment` app-instelling.</span><span class="sxs-lookup"><span data-stu-id="e32f8-217">The Web.config in your project already defines the `environment` app setting.</span></span> <span data-ttu-id="e32f8-218">Met deze instelling wanneer u de app lokaal testen metrische gegevens over uw worden gemarkeerd met `VS Debugger`.</span><span class="sxs-lookup"><span data-stu-id="e32f8-218">With this setting, when you test the app locally, your metrics will be tagged with `VS Debugger`.</span></span> <span data-ttu-id="e32f8-219">Echter, wanneer u uw wijzigingen naar Azure pushen, Azure wordt zoeken en de `environment` app in plaats daarvan instelling in de web-app-configuratie en metrische gegevens over uw worden gemarkeerd met `Production`.</span><span class="sxs-lookup"><span data-stu-id="e32f8-219">However, when you push your changes to Azure, Azure will find and use the `environment` app setting in the web app's configuration instead, and your metrics will be tagged with `Production`.</span></span>
3. <span data-ttu-id="e32f8-220">Doorvoeren en de codewijzigingen push naar uw fork op GitHub en wacht voor uw gebruikers de nieuwe app (u moet de browser te vernieuwen) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e32f8-220">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="e32f8-221">Het duurt ongeveer 15 minuten voor de nieuwe eigenschap worden weergegeven in uw Application Insights `MultiChannelToDo.Web` resource.</span><span class="sxs-lookup"><span data-stu-id="e32f8-221">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo.Web` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for client app"
        git push origin master
4. <span data-ttu-id="e32f8-222">Nu gaat u naar de **aangepaste gebeurtenissen** blade opnieuw en filtert u de metrische gegevens op `Environment=Production`.</span><span class="sxs-lookup"><span data-stu-id="e32f8-222">Now, go to the **Custom events** blade again and filter the metrics on `Environment=Production`.</span></span> <span data-ttu-id="e32f8-223">Nu moet u alle nieuwe aangepaste gebeurtenissen in de productiesite zien met dit filter.</span><span class="sxs-lookup"><span data-stu-id="e32f8-223">You should now be able to see all the new custom events in the production slot with this filter.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. <span data-ttu-id="e32f8-224">Klik op de **Favorieten** om op te slaan van de huidige Metrics Explorer-instellingen naar ongeveer **aangepaste gebeurtenissen: productie**.</span><span class="sxs-lookup"><span data-stu-id="e32f8-224">Click the **Favorites** button to save the current Metrics Explorer settings to something like **Custom events: Production**.</span></span> <span data-ttu-id="e32f8-225">U kunt eenvoudig schakelen tussen deze weergaven en een implementatiesleuf later.</span><span class="sxs-lookup"><span data-stu-id="e32f8-225">You can easily switch between this view and a deployment slot view later.</span></span>

   > [!TIP]
   > <span data-ttu-id="e32f8-226">Voor nog krachtiger analytics, kunt u overwegen [integreren van uw Application Insights-resource met Power BI](../application-insights/app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="e32f8-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span></span>
   >
   >

### <a name="add-slot-specific-tags-to-your-server-app-metrics"></a><span data-ttu-id="e32f8-227">Site-specifieke labels toevoegen aan uw app metrische servergegevens</span><span class="sxs-lookup"><span data-stu-id="e32f8-227">Add slot-specific tags to your server app metrics</span></span>
<span data-ttu-id="e32f8-228">Opnieuw voor de volledigheid stelt u de app-serverzijde.</span><span class="sxs-lookup"><span data-stu-id="e32f8-228">Again, for completeness you will set up the server-side app.</span></span> <span data-ttu-id="e32f8-229">In tegenstelling tot de clientapp die in JavaScript is geïnstrumenteerd, sleuf-specifieke labels voor de server-app is geïnstrumenteerd met .NET-code.</span><span class="sxs-lookup"><span data-stu-id="e32f8-229">Unlike the client app which is instrumented in JavaScript, slot-specific tags for the server app is instrumented with .NET code.</span></span>

1. <span data-ttu-id="e32f8-230">Open  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="e32f8-230">Open *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs.</span></span> <span data-ttu-id="e32f8-231">Voeg het codeblok hieronder, net voordat de afsluiting accolade naamruimte.</span><span class="sxs-lookup"><span data-stu-id="e32f8-231">Add the code block below, just before the closing namespace curly brace.</span></span>

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. <span data-ttu-id="e32f8-232">De naam resolutie fouten corrigeren door toe te voegen de `using` instructies onder aan het begin van het bestand:</span><span class="sxs-lookup"><span data-stu-id="e32f8-232">Correct the name resolution errors by adding the `using` statements below to the beginning of the file:</span></span>

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. <span data-ttu-id="e32f8-233">De volgende code toevoegen aan het begin van de `Application_Start()` methode:</span><span class="sxs-lookup"><span data-stu-id="e32f8-233">Add the code below to the beginning of the `Application_Start()` method:</span></span>

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. <span data-ttu-id="e32f8-234">Doorvoeren en de codewijzigingen push naar uw fork op GitHub en wacht voor uw gebruikers de nieuwe app (u moet de browser te vernieuwen) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e32f8-234">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="e32f8-235">Het duurt ongeveer 15 minuten voor de nieuwe eigenschap worden weergegeven in uw Application Insights `MultiChannelToDo` resource.</span><span class="sxs-lookup"><span data-stu-id="e32f8-235">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a><span data-ttu-id="e32f8-236">Update: Stel uw vertakking beta</span><span class="sxs-lookup"><span data-stu-id="e32f8-236">Update: Set up your beta branch</span></span>
1. <span data-ttu-id="e32f8-237">Open  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json en zoek de `appsettings` resources (zoeken naar `"name": "appsettings"`).</span><span class="sxs-lookup"><span data-stu-id="e32f8-237">Open *&lt;repository_root>*\ARMTemplates\ProdAndStagetest.json and find the `appsettings` resources (search for `"name": "appsettings"`).</span></span> <span data-ttu-id="e32f8-238">Er zijn 4 daarvan, één voor elke site.</span><span class="sxs-lookup"><span data-stu-id="e32f8-238">There are 4 of them, one for each slot.</span></span>
2. <span data-ttu-id="e32f8-239">Voor elk `appsettings` resource, Voeg een `"environment": "[parameters('slotName')]"` app-instelling met het einde van de `properties` matrix.</span><span class="sxs-lookup"><span data-stu-id="e32f8-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting to the end of the `properties` array.</span></span> <span data-ttu-id="e32f8-240">Vergeet niet om te beëindigen van de vorige regel met een komma.</span><span class="sxs-lookup"><span data-stu-id="e32f8-240">Don't forget to end the previous line with a comma.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    <span data-ttu-id="e32f8-241">U hebt zojuist toegevoegd de `environment` app-instelling op de sleuven in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e32f8-241">You have just added the `environment` app setting to all the slots in the template.</span></span>
3. <span data-ttu-id="e32f8-242">Zoek in hetzelfde bestand de `slotconfignames` resources (zoeken naar `"name": "slotconfignames"`).</span><span class="sxs-lookup"><span data-stu-id="e32f8-242">In the same file, find the `slotconfignames` resources (search for `"name": "slotconfignames"`).</span></span> <span data-ttu-id="e32f8-243">Er zijn 2 één voor elke app.</span><span class="sxs-lookup"><span data-stu-id="e32f8-243">There are 2 of them, one for each app.</span></span>
4. <span data-ttu-id="e32f8-244">Voor elk `slotconfignames` resource toevoegen `"environment"` aan het einde van de `appSettingNames` matrix.</span><span class="sxs-lookup"><span data-stu-id="e32f8-244">For each `slotconfignames` resource, add `"environment"` to the end of the `appSettingNames` array.</span></span> <span data-ttu-id="e32f8-245">Vergeet niet om te beëindigen van de vorige regel met een komma.</span><span class="sxs-lookup"><span data-stu-id="e32f8-245">Don't forget to end the previous line with a comma.</span></span>

    <span data-ttu-id="e32f8-246">U zojuist hebt gemaakt de `environment` app stick instellen voor de respectieve implementatiesleuf voor beide apps.</span><span class="sxs-lookup"><span data-stu-id="e32f8-246">You have just made the `environment` app setting stick to its respective deployment slot for both apps.</span></span>  
5. <span data-ttu-id="e32f8-247">Voer de volgende opdrachten met het achtervoegsel met dezelfde resource groep die u eerder hebt gebruikt in uw sessie Git-Shell.</span><span class="sxs-lookup"><span data-stu-id="e32f8-247">In your Git Shell session, run the following commands with the same resource group suffix that you used before.</span></span>

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. <span data-ttu-id="e32f8-248">Wanneer u wordt gevraagd, geeft u de dezelfde SQL-databasereferenties als voordat.</span><span class="sxs-lookup"><span data-stu-id="e32f8-248">When prompted, specify the same SQL database credentials as before.</span></span> <span data-ttu-id="e32f8-249">Wanneer u wordt gevraagd om bij te werken van de resourcegroep, typ `Y`, klikt u vervolgens `ENTER`.</span><span class="sxs-lookup"><span data-stu-id="e32f8-249">Then, when asked to update the resource group, type `Y`, then `ENTER`.</span></span>

    <span data-ttu-id="e32f8-250">Nadat het script is voltooid, worden alle resources in de oorspronkelijke resourcegroep bewaard, maar een nieuwe sleuf met de naam "bètaversie" wordt gemaakt in deze met dezelfde configuratie als de sleuf van 'Fasering' dat is gemaakt in het begin.</span><span class="sxs-lookup"><span data-stu-id="e32f8-250">Once the script finishes, all your resources in the original resource group are retained, but a new slot named "beta" is created in it with the same configuration as the "Staging" slot that was created in the beginning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e32f8-251">Deze methode voor het maken van verschillende omgevingen verschilt van de methode in [flexibele software ontwikkelen met Azure App Service](app-service-agile-software-development.md).</span><span class="sxs-lookup"><span data-stu-id="e32f8-251">This method of creating different deployment environments is different from the method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span></span> <span data-ttu-id="e32f8-252">Hier, maakt u implementatieomgevingen met implementatiesites, waar als er u implementatieomgevingen met resourcegroepen maken.</span><span class="sxs-lookup"><span data-stu-id="e32f8-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span></span> <span data-ttu-id="e32f8-253">Implementatieomgevingen beheren met resourcegroepen kunt u de productieomgeving off-limits houden voor ontwikkelaars, maar het is niet eenvoudig om testen in productie, waarmee u eenvoudig met sleuven doen kunt.</span><span class="sxs-lookup"><span data-stu-id="e32f8-253">Managing deployment environments with resource groups enables you to keep the production environment off-limits to developers, but it's not easy to do testing in production, which you can do easily with slots.</span></span>
   >
   >

<span data-ttu-id="e32f8-254">Als u wenst, kunt u ook een alfa-app maken door te voeren</span><span class="sxs-lookup"><span data-stu-id="e32f8-254">If you wish, you can also create an alpha app by running</span></span>

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

<span data-ttu-id="e32f8-255">Voor deze zelfstudie, wordt u alleen blijven gebruiken uw bèta-app.</span><span class="sxs-lookup"><span data-stu-id="e32f8-255">For this tutorial, you will just keep using your beta app.</span></span>

## <a name="update-push-your-updates-to-the-beta-app"></a><span data-ttu-id="e32f8-256">Update: Implementeer uw updates naar de bètaversie-app</span><span class="sxs-lookup"><span data-stu-id="e32f8-256">Update: Push your updates to the beta app</span></span>
<span data-ttu-id="e32f8-257">Terug naar uw app, die u wilt verbeteren.</span><span class="sxs-lookup"><span data-stu-id="e32f8-257">Back to your app that you want to improve.</span></span>

1. <span data-ttu-id="e32f8-258">Zorg ervoor dat u kunt nu uw vertakking beta</span><span class="sxs-lookup"><span data-stu-id="e32f8-258">Make sure you're now in your beta branch</span></span>

        git checkout beta
2. <span data-ttu-id="e32f8-259">In  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, vinden de `<li>` labelen en voeg de `style="cursor:pointer"` kenmerk toe, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e32f8-259">In *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, find the `<li>` tag and add the `style="cursor:pointer"` attribute, as shown below.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. <span data-ttu-id="e32f8-260">doorvoeren en push naar Azure.</span><span class="sxs-lookup"><span data-stu-id="e32f8-260">commit and push to Azure.</span></span>
4. <span data-ttu-id="e32f8-261">Controleer of dat de wijziging nu in de sleuf beta weergegeven wordt door te navigeren naar http://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/.</span><span class="sxs-lookup"><span data-stu-id="e32f8-261">Verify that the change is now reflected in the beta slot by navigating to http://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span></span> <span data-ttu-id="e32f8-262">Als u de wijziging nog niet ziet, vernieuw uw browser om de nieuwe javascript-code.</span><span class="sxs-lookup"><span data-stu-id="e32f8-262">If you don't see the change yet, refresh your browser to get the new javascript code.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

<span data-ttu-id="e32f8-263">Nu dat u uw wijziging in de sleuf beta wordt uitgevoerd hebt, bent u klaar om een flighting te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e32f8-263">Now that you have your change running in the beta slot, you are ready to perform a flighting deployment.</span></span>

## <a name="validate-route-traffic-to-the-beta-app"></a><span data-ttu-id="e32f8-264">Valideren: Routeverkeer naar de bètaversie-app</span><span class="sxs-lookup"><span data-stu-id="e32f8-264">Validate: Route traffic to the beta app</span></span>
<span data-ttu-id="e32f8-265">In deze sectie wordt u verkeer doorstuurt naar de bètaversie-app.</span><span class="sxs-lookup"><span data-stu-id="e32f8-265">In this section, you will route traffic to the beta app.</span></span> <span data-ttu-id="e32f8-266">Ter verduidelijking van demonstratie gaat u een groot deel van het gebruikersverkeer te routeren.</span><span class="sxs-lookup"><span data-stu-id="e32f8-266">For sake of clarity of demonstration, you're going to route a significant portion of the user traffic to it.</span></span> <span data-ttu-id="e32f8-267">In werkelijkheid is afhankelijk de hoeveelheid verkeer die u wilt routeren van uw specifieke situatie.</span><span class="sxs-lookup"><span data-stu-id="e32f8-267">In reality, the amount of traffic you want to route will depend on your specific situation.</span></span> <span data-ttu-id="e32f8-268">Bijvoorbeeld, als uw site op de schaal van microsoft.com is, mogelijk moet u minder dan één procent van uw totale verkeer om te kunnen krijgen tot nuttige gegevens.</span><span class="sxs-lookup"><span data-stu-id="e32f8-268">For example, if your site is at the scale of microsoft.com, then you may need less than one percent of your total traffic in order to gain useful data.</span></span>

1. <span data-ttu-id="e32f8-269">Voer de volgende opdrachten aan de helft van de productie-verkeer wordt doorgestuurd naar de bèta-sleuf in de Git-Shell-sessie:</span><span class="sxs-lookup"><span data-stu-id="e32f8-269">In your Git Shell session, run the following commands to route half of the production traffic to the beta slot:</span></span>

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   <span data-ttu-id="e32f8-270">De `ReroutePercentage=50` -eigenschap geeft op dat 50% van de productie-verkeer wordt doorgestuurd naar de bètaversie-app-URL (opgegeven door de `ActionHostName` eigenschap).</span><span class="sxs-lookup"><span data-stu-id="e32f8-270">The `ReroutePercentage=50` property specifies that 50% of the production traffic will be routed to the beta app's URL (specified by the `ActionHostName` property).</span></span>
2. <span data-ttu-id="e32f8-271">Nu gaat u naar http://ToDoApp*&lt;your_suffix >*. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="e32f8-271">Now navigate to http://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span></span> <span data-ttu-id="e32f8-272">nu wordt 50% van het verkeer omgeleid naar de bètaversie sleuf.</span><span class="sxs-lookup"><span data-stu-id="e32f8-272">50% of the traffic should now be redirected to the beta slot.</span></span>
3. <span data-ttu-id="e32f8-273">Filter in uw Application Insights-resource, de metrische gegevens door omgeving = "bètaversie".</span><span class="sxs-lookup"><span data-stu-id="e32f8-273">In your Application Insights resource, filter the metrics by environment="beta".</span></span>

   > [!NOTE]
   > <span data-ttu-id="e32f8-274">Als u deze gefilterde weergave als een andere favoriet opslaan, kunt u eenvoudig de weergaven metrische explorer tussen productie en beta weergaven spiegelen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-274">If you save this filtered view as another favorite, then you can easily flip the metric explorer views between production and beta views.</span></span>
   >
   >

<span data-ttu-id="e32f8-275">Stel in Application Insights ziet u iets soortgelijks als in het volgende:</span><span class="sxs-lookup"><span data-stu-id="e32f8-275">Suppose in Application Insights you see something similar to the following:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

<span data-ttu-id="e32f8-276">Niet alleen wordt dit weergegeven dat er zijn veel meer klikken op de `<li>` tags, maar wel een piek muisklikken op `<li>` labels.</span><span class="sxs-lookup"><span data-stu-id="e32f8-276">Not only is this showing that there are many more clicks on the `<li>` tags, but there seems to be a surge of clicks on `<li>` tags.</span></span> <span data-ttu-id="e32f8-277">U kunt beëindigt dat mensen hebben gedetecteerd met de nieuwe `<li>` -tags zijn klikbaar en alle taken eerder voltooid in de app nu wordt gewist.</span><span class="sxs-lookup"><span data-stu-id="e32f8-277">You can then conclude that people have discovered the new `<li>` tags are clickable and are now clearing all their previously-completed tasks in the app.</span></span>

<span data-ttu-id="e32f8-278">Op basis van de gegevens van uw flighting implementatie kunt bepalen u dat de nieuwe gebruikersinterface gereed voor productie is.</span><span class="sxs-lookup"><span data-stu-id="e32f8-278">Based on the data of your flighting deployment, you decide that your new UI is ready for production.</span></span>

## <a name="go-live-move-your-new-code-into-production"></a><span data-ttu-id="e32f8-279">Ga live: je nieuwe code naar de productie verplaatsen</span><span class="sxs-lookup"><span data-stu-id="e32f8-279">Go live: Move your new code into production</span></span>
<span data-ttu-id="e32f8-280">U bent nu klaar voor het verplaatsen van de update naar productie.</span><span class="sxs-lookup"><span data-stu-id="e32f8-280">You're now ready to move your update to production.</span></span> <span data-ttu-id="e32f8-281">Is die wat is een goede nu u weet dat de update is al gevalideerd *voordat* wordt deze doorgegeven naar productie.</span><span class="sxs-lookup"><span data-stu-id="e32f8-281">What's great is that now you know that your update has already been validated *before* it is pushed to production.</span></span> <span data-ttu-id="e32f8-282">Nu kunt u probleemloos deze implementeren.</span><span class="sxs-lookup"><span data-stu-id="e32f8-282">So now you can confidently deploy it.</span></span> <span data-ttu-id="e32f8-283">Omdat u een update naar de AngularJS-client-app hebt aangebracht, worden alleen de client-side '-code gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="e32f8-283">Since you made an update to the AngularJS client app, you only validated the client-side code.</span></span> <span data-ttu-id="e32f8-284">Als u wijzigingen aanbrengen in de back-end Web API-app, kunt u uw wijzigingen kan valideren op dezelfde manier en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="e32f8-284">If you were to make changes to the back-end Web API app, you could validate your changes similarly and easily.</span></span>

1. <span data-ttu-id="e32f8-285">Git-shell, de regel voor het doorsturen van verkeer te verwijderen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e32f8-285">In Git Shell, remove the traffic routing rule by running the following command:</span></span>

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. <span data-ttu-id="e32f8-286">Voer de Git-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="e32f8-286">Run the Git commands:</span></span>

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. <span data-ttu-id="e32f8-287">Wacht enkele minuten duren voordat de nieuwe code worden geïmplementeerd voor de faseringsite en vervolgens starten http://ToDoApp*&lt;your_suffix >*-staging.azurewebsites.net om te controleren of de nieuwe update in de faseringssleuf is opgewarmd.</span><span class="sxs-lookup"><span data-stu-id="e32f8-287">Wait for a few minutes for the new code to be deployed to the staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net to verify that the new update is warmed up in the staging slot.</span></span> <span data-ttu-id="e32f8-288">Houd er rekening mee dat de hoofdvertakking van uw fork is gekoppeld aan de faseringssleuf van uw app.</span><span class="sxs-lookup"><span data-stu-id="e32f8-288">Remember that the your fork's master branch is linked to the staging slot of your app.</span></span>
4. <span data-ttu-id="e32f8-289">Nu de faseringssleuf wisselen naar de productie</span><span class="sxs-lookup"><span data-stu-id="e32f8-289">Now, swap the staging slot into production</span></span>

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a><span data-ttu-id="e32f8-290">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="e32f8-290">Summary</span></span>
<span data-ttu-id="e32f8-291">Azure App Service gemakkelijk voor kleine-middelgrote bedrijven hun apps klantgerichte iets testen in productie, die normaal is uitgevoerd in grote ondernemingen.</span><span class="sxs-lookup"><span data-stu-id="e32f8-291">Azure App Service makes it easy for small- to medium-sized businesses to test their customer-facing apps in production, something that has been traditionally done in big enterprises.</span></span> <span data-ttu-id="e32f8-292">In het ideale geval, deze zelfstudie hebt gekregen de kennis die u nodig hebt bij elkaar brengt App Service en de Application Insights om mogelijke zeker implementatie en zelfs andere testen in productie-scenario's in uw DevOps-wereld.</span><span class="sxs-lookup"><span data-stu-id="e32f8-292">Hopefully, this tutorial has given you the knowledge you need to bring together App Service and Application Insights to make possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span></span>

## <a name="more-resources"></a><span data-ttu-id="e32f8-293">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="e32f8-293">More resources</span></span>
* [<span data-ttu-id="e32f8-294">Flexibele software ontwikkelen met Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e32f8-294">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="e32f8-295">Faseringsomgevingen voor web-apps in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="e32f8-295">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="e32f8-296">Een complexe toepassing zoals verwacht in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="e32f8-296">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="e32f8-297">Azure Resource Manager-sjablonen ontwerpen</span><span class="sxs-lookup"><span data-stu-id="e32f8-297">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="e32f8-298">JSONLint - de validatiefunctie JSON</span><span class="sxs-lookup"><span data-stu-id="e32f8-298">JSONLint - The JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="e32f8-299">GIT vertakking – basis vertakking en samenvoegen</span><span class="sxs-lookup"><span data-stu-id="e32f8-299">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="e32f8-300">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e32f8-300">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="e32f8-301">Project Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="e32f8-301">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)
