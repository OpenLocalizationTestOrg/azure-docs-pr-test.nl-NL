---
title: "aaaFlighting-implementatie (bètaversie testen) in Azure App Service"
description: Meer informatie over hoe uw updates in deze zelfstudie end-to-end tooflight nieuwe functies in uw app of beta testen. Deze samenbrengt App Service-functies, zoals continue publiceren, sleuven voor verkeersroutering en Application Insights-integratie.
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
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a><span data-ttu-id="c3e80-104">Zeker implementatie (bètaversie testen) in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c3e80-104">Flighting deployment (beta testing) in Azure App Service</span></span>
<span data-ttu-id="c3e80-105">Deze zelfstudie leert u hoe toodo *zeker implementaties* Hallo door integratie van verschillende mogelijkheden van [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en [Azure Application Insights](/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="c3e80-105">This tutorial shows you how toodo *flighting deployments* by integrating hello various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span></span>

<span data-ttu-id="c3e80-106">*Zeker* is een implementatieproces te valideren en een nieuwe functie of wijzigen met een beperkt aantal echte klanten en is een belangrijke test in productiescenario's.</span><span class="sxs-lookup"><span data-stu-id="c3e80-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span></span> <span data-ttu-id="c3e80-107">Deze overeenkomst vertonen toobeta is getest en wordt ook wel aangeduid als 'beheerde test vlucht'.</span><span class="sxs-lookup"><span data-stu-id="c3e80-107">It is akin toobeta testing and is sometimes known as "controlled test flight".</span></span> <span data-ttu-id="c3e80-108">Veel grote ondernemingen met een aanwezigheid op het web gebruik deze benadering voor vroege validatie op hun app-updates in de praktijk van [flexibele ontwikkeling](https://en.wikipedia.org/wiki/Agile_software_development).</span><span class="sxs-lookup"><span data-stu-id="c3e80-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="c3e80-109">Azure App Service kunt u toointegrate testen in de productieomgeving met continue publicatie en Application Insights tooimplement Hallo hetzelfde DevOps-scenario.</span><span class="sxs-lookup"><span data-stu-id="c3e80-109">Azure App Service enables you toointegrate test in production with continous publishing and Application Insights tooimplement hello same DevOps scenario.</span></span> <span data-ttu-id="c3e80-110">Voordelen van deze benadering zijn:</span><span class="sxs-lookup"><span data-stu-id="c3e80-110">Benefits of this approach include:</span></span>

* <span data-ttu-id="c3e80-111">**Echte feedback krijgen *voordat* updates zijn vrijgegeven tooproduction** -Hallo alleen wat is beter dan feedback krijgt als u de release feedback krijgen is voordat u loslaat.</span><span class="sxs-lookup"><span data-stu-id="c3e80-111">**Gain real feedback *before* updates are released tooproduction** - hello only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span></span> <span data-ttu-id="c3e80-112">U kunt updates met de werkelijke gebruikersverkeer en het gedrag vroeg u wenst in de levenscyclus Hallo testen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-112">You can test updates with real user traffic and behaviors as early as you desire in hello product life cycle.</span></span>
* <span data-ttu-id="c3e80-113">**Verbeter [doorlopende test gebaseerde ontwikkeling (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  - door te testen in de productieomgeving integreren met continue integratie en instrumentation met Application Insights valideren van de gebruiker gebeurt vroeg en automatisch in de levenscyclus van het product.</span><span class="sxs-lookup"><span data-stu-id="c3e80-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span></span> <span data-ttu-id="c3e80-114">Dit reduceert de hoeveelheid tijd investeringen in handmatige testuitvoering.</span><span class="sxs-lookup"><span data-stu-id="c3e80-114">This helps reduce time investments in manual test execution.</span></span>
* <span data-ttu-id="c3e80-115">**Optimaliseert de werkstroom test** -door te testen in de productieomgeving met continue bewaking instrumentation automatiseren, kunt u mogelijk uitvoeren Hallo doelstellingen van verschillende soorten tests in een enkel proces, zoals [integratie](https://en.wikipedia.org/wiki/Integration_testing), [regressie](https://en.wikipedia.org/wiki/Regression_testing), [bruikbaarheid](https://en.wikipedia.org/wiki/Usability_testing), toegankelijkheid, lokalisatie, [prestaties](https://en.wikipedia.org/wiki/Software_performance_testing), [beveiliging](https://en.wikipedia.org/wiki/Security_testing), en [ acceptatie](https://en.wikipedia.org/wiki/Acceptance_testing).</span><span class="sxs-lookup"><span data-stu-id="c3e80-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish hello goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span></span>

<span data-ttu-id="c3e80-116">Een flighting implementatie is niet alleen om routering voor live verkeer.</span><span class="sxs-lookup"><span data-stu-id="c3e80-116">A flighting deployment is not just about routing live traffic.</span></span> <span data-ttu-id="c3e80-117">In een dergelijke implementatie u toogain inzicht zo snel mogelijk, ongeacht of deze een onverwachte fout, verminderde prestaties, gebruikerservaring problemen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-117">In such a deployment you want toogain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span></span> <span data-ttu-id="c3e80-118">Denk eraan dat u werkt met real-klanten.</span><span class="sxs-lookup"><span data-stu-id="c3e80-118">Remember, you are dealing with real customers.</span></span> <span data-ttu-id="c3e80-119">In dat geval toodo deze rechts, moet u ervoor zorgen dat u hebt ingesteld uw flighting implementatie toogather alle Hallo-gegevens die u nodig hebt in volgorde toomake een gefundeerde beslissing nemen voor de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="c3e80-119">So toodo it right, you must make sure that you have set up your flighting deployment toogather all hello data you need in order toomake an informed decision for your next step.</span></span> <span data-ttu-id="c3e80-120">Deze zelfstudie leert u hoe toocollect gegevens met Application Insights, maar u kunt New Relic of andere technologieën die past bij uw scenario.</span><span class="sxs-lookup"><span data-stu-id="c3e80-120">This tutorial shows you how toocollect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c3e80-121">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="c3e80-121">What you will do</span></span>
<span data-ttu-id="c3e80-122">In deze zelfstudie leert u hoe toobring Hallo volgende scenario's samen tootest uw App Service-app in productie:</span><span class="sxs-lookup"><span data-stu-id="c3e80-122">In this tutorial, you will learn how toobring hello following scenarios together tootest your App Service app in production:</span></span>

* <span data-ttu-id="c3e80-123">[Productie-verkeer routeren](app-service-web-test-in-production-get-start.md) tooyour beta-app</span><span class="sxs-lookup"><span data-stu-id="c3e80-123">[Route production traffic](app-service-web-test-in-production-get-start.md) tooyour beta app</span></span>
* <span data-ttu-id="c3e80-124">[Uw app instrumenteren](../application-insights/app-insights-web-track-usage.md) tooobtain nuttig metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="c3e80-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) tooobtain useful metrics</span></span>
* <span data-ttu-id="c3e80-125">Continu implementeren van uw bèta-app en live app metrische gegevens bijhouden</span><span class="sxs-lookup"><span data-stu-id="c3e80-125">Continuously deploy your beta app and track live app metrics</span></span>
* <span data-ttu-id="c3e80-126">Metrische gegevens vergelijken tussen Hallo productie-app en Hallo beta app toosee hoe code verandert vertalen tooresults</span><span class="sxs-lookup"><span data-stu-id="c3e80-126">Compare metrics between hello production app and hello beta app toosee how code changes translate tooresults</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="c3e80-127">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="c3e80-127">What you will need</span></span>
* <span data-ttu-id="c3e80-128">Een Azure-account</span><span class="sxs-lookup"><span data-stu-id="c3e80-128">An Azure account</span></span>
* <span data-ttu-id="c3e80-129">Een [GitHub](https://github.com/) account</span><span class="sxs-lookup"><span data-stu-id="c3e80-129">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="c3e80-130">Visual Studio 2015 - kunt u downloaden Hallo [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3e80-130">Visual Studio 2015 - you can download hello [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span></span>
* <span data-ttu-id="c3e80-131">GIT-Shell (geïnstalleerd met [GitHub voor Windows](https://windows.github.com/))-Hierdoor kunt u toorun beide Hallo Git en PowerShell-opdrachten in Hallo dezelfde sessie</span><span class="sxs-lookup"><span data-stu-id="c3e80-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you toorun both hello Git and PowerShell commands in hello same session</span></span>
* <span data-ttu-id="c3e80-132">Meest recente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span><span class="sxs-lookup"><span data-stu-id="c3e80-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span></span>
* <span data-ttu-id="c3e80-133">Basiskennis van Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="c3e80-133">Basic understanding of hello following:</span></span>
  * <span data-ttu-id="c3e80-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) sjabloonimplementatie (Zie [een complexe toepassing zoals verwacht in Azure implementeert](app-service-deploy-complex-application-predictably.md))</span><span class="sxs-lookup"><span data-stu-id="c3e80-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="c3e80-135">Git</span><span class="sxs-lookup"><span data-stu-id="c3e80-135">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="c3e80-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3e80-136">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="c3e80-137">U moet een Azure-account toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="c3e80-137">You need an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="c3e80-138">U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/) -u ontvangt tegoed kunt u tootry uit betaalde Azure-services en zelfs nadat ze zijn gebruikt u Hallo rekening kunt houden en gebruik gratis Azure-services, zoals Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="c3e80-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="c3e80-139">U kunt [voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -uw Visual Studio-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c3e80-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="c3e80-140">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="c3e80-140">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c3e80-141">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-141">No credit cards required; no commitments.</span></span>
>
>

## <a name="set-up-your-production-web-app"></a><span data-ttu-id="c3e80-142">Instellen van uw web-app voor productie</span><span class="sxs-lookup"><span data-stu-id="c3e80-142">Set up your production web app</span></span>
> [!NOTE]
> <span data-ttu-id="c3e80-143">Hallo-script in deze zelfstudie gebruikt configureert automatisch continue publiceren vanaf uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="c3e80-143">hello script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="c3e80-144">Dit is vereist dat uw GitHub-referenties worden al opgeslagen in Azure, anders mislukt de implementatie van Hallo in een script vastgelegd tijdens een poging de instellingen voor bronbeheer tooconfigure voor Hallo web-apps.</span><span class="sxs-lookup"><span data-stu-id="c3e80-144">This requires that your GitHub credentials are already stored in Azure, otherwise hello scripted deployment will fail when attempting tooconfigure source control settings for hello web apps.</span></span>
>
> <span data-ttu-id="c3e80-145">toostore uw GitHub-referenties in Azure, een web-app maken in Hallo [Azure Portal](https://portal.azure.com/) en [GitHub implementatie configureren](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c3e80-145">toostore your GitHub credentials in Azure, create a web app in hello [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="c3e80-146">U hoeft alleen toodo dit één keer.</span><span class="sxs-lookup"><span data-stu-id="c3e80-146">You only need toodo this once.</span></span>
>
>

<span data-ttu-id="c3e80-147">In een typisch scenario voor DevOps, hebt u een toepassing die wordt uitgevoerd in Azure in en gewenste toomake wijzigingen tooit via continue publiceren.</span><span class="sxs-lookup"><span data-stu-id="c3e80-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want toomake changes tooit through continuous publishing.</span></span> <span data-ttu-id="c3e80-148">In dit scenario implementeert u tooproduction een sjabloon die u hebt ontwikkeld en getest.</span><span class="sxs-lookup"><span data-stu-id="c3e80-148">In this scenario, you will deploy tooproduction a template that you have developed and tested.</span></span>

1. <span data-ttu-id="c3e80-149">Maak uw eigen fork Hallo [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="c3e80-149">Create your own fork of hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="c3e80-150">Zie voor meer informatie over het maken van uw fork [een opslagplaats vertakken](https://help.github.com/articles/fork-a-repo/).</span><span class="sxs-lookup"><span data-stu-id="c3e80-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="c3e80-151">Zodra uw fork is gemaakt, kunt u deze bekijken in uw browser.</span><span class="sxs-lookup"><span data-stu-id="c3e80-151">Once your fork is created, you can see it in your browser.</span></span>

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="c3e80-152">Open een Git-Shell-sessie.</span><span class="sxs-lookup"><span data-stu-id="c3e80-152">Open a Git Shell session.</span></span> <span data-ttu-id="c3e80-153">Als u nog Git-Shell hebt, installeert u [GitHub voor Windows](https://windows.github.com/) nu.</span><span class="sxs-lookup"><span data-stu-id="c3e80-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="c3e80-154">Maak een lokale kloon van uw fork door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="c3e80-154">Create a local clone of your fork by executing hello following command:</span></span>

     <span data-ttu-id="c3e80-155">GIT kloon https://github.com/<your_fork>/ToDoApp.git</span><span class="sxs-lookup"><span data-stu-id="c3e80-155">git clone https://github.com/<your_fork>/ToDoApp.git</span></span>
4. <span data-ttu-id="c3e80-156">Zodra u uw lokale kloon hebt, te navigeren*&lt;repository_root >*\ARMTemplates, en Voer Hallo deploy.ps1 script met een uniek achtervoegsel, zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="c3e80-156">Once you have your local clone, navigate too*&lt;repository_root>*\ARMTemplates, and run hello deploy.ps1 script with a unique suffix, as shown below:</span></span>

     <span data-ttu-id="c3e80-157">.\deploy.ps1 – RepoUrl https://github.com/<your_fork>/todoapp.git - ResourceGroupSuffix < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="c3e80-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span></span>
5. <span data-ttu-id="c3e80-158">Wanneer u wordt gevraagd, typt u in Hallo gewenst gebruikersnaam en wachtwoord voor toegang tot de database.</span><span class="sxs-lookup"><span data-stu-id="c3e80-158">When prompted, type in hello desired username and password for database access.</span></span> <span data-ttu-id="c3e80-159">Uw database referenties omdat u toospecify moet onthouden ze opnieuw wanneer bijwerken Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c3e80-159">Remember your database credentials because you will need toospecify them again when updating hello resource group.</span></span>

   <span data-ttu-id="c3e80-160">U ziet de voortgang van de verschillende Azure-resources inrichten Hallo.</span><span class="sxs-lookup"><span data-stu-id="c3e80-160">You should see hello provisioning progress of various Azure resources.</span></span> <span data-ttu-id="c3e80-161">Wanneer implementatie is voltooid, wordt de Hallo script toepassing hello in Hallo browser starten en de bieden u een beschrijvende geluid.</span><span class="sxs-lookup"><span data-stu-id="c3e80-161">When deployment completes, hello script will launch hello application in hello browser and give you a friendly beep.</span></span>
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. <span data-ttu-id="c3e80-162">Terug in uw sessie Git Shell uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c3e80-162">Back in your Git Shell session, run:</span></span>

     <span data-ttu-id="c3e80-163">. \swap – naam ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="c3e80-163">.\swap –Name ToDoApp<your_suffix></span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. <span data-ttu-id="c3e80-164">Wanneer Hallo-script is voltooid, gaat u terug toobrowse toohello frontend-adres (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee Hallo toepassing die wordt uitgevoerd in de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c3e80-164">When hello script finishes, go back toobrowse toohello frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) toosee hello application running in production.</span></span>
8. <span data-ttu-id="c3e80-165">Meld u aan bij Hallo [Azure Portal](https://portal.azure.com/) en eens kijken wat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c3e80-165">Log into hello [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span></span>

   <span data-ttu-id="c3e80-166">U moet de web-apps kunnen toosee twee in Hallo dezelfde resourcegroep bevinden, één met de Hallo `Api` achtervoegsel in Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="c3e80-166">You should be able toosee two web apps in hello same resource group, one with hello `Api` suffix in hello name.</span></span> <span data-ttu-id="c3e80-167">Als u bekijkt hello resourcegroepweergave in, ook ziet u Hallo SQL-Database en -server, Hallo App Service-abonnement en fasering sleuven Hallo voor Hallo web-apps.</span><span class="sxs-lookup"><span data-stu-id="c3e80-167">If you look at hello resource group view, you will also see hello SQL Database and server, hello App Service plan, and hello staging slots for hello web apps.</span></span> <span data-ttu-id="c3e80-168">Blader door de verschillende bronnen Hallo en vergelijkt ze met  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hoe deze zijn geconfigureerd in Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c3e80-168">Browse through hello different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json toosee how they are configured in hello template.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

<span data-ttu-id="c3e80-169">U hebt Hallo productie-app ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c3e80-169">You have set up hello production app.</span></span>  <span data-ttu-id="c3e80-170">Nu gaan we Stel dat u feedback of bruikbaarheid slechte voor Hallo-app is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-170">Now, let's imagine that you receive feedback that usability is poor for hello app.</span></span> <span data-ttu-id="c3e80-171">U bepaalt dus tooinvestigate.</span><span class="sxs-lookup"><span data-stu-id="c3e80-171">So you decide tooinvestigate.</span></span> <span data-ttu-id="c3e80-172">U gaat tooinstrument uw app toogive u feedback.</span><span class="sxs-lookup"><span data-stu-id="c3e80-172">You're going tooinstrument your app toogive you feedback.</span></span>

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a><span data-ttu-id="c3e80-173">Onderzoeken: Uw client-app voor bewaking/metrieken softwareontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="c3e80-173">Investigate: Instrument your client app for monitoring/metrics</span></span>
1. <span data-ttu-id="c3e80-174">Open  *&lt;repository_root >*\src\MultiChannelToDo.sln in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3e80-174">Open *&lt;repository_root>*\src\MultiChannelToDo.sln in Visual Studio.</span></span>
2. <span data-ttu-id="c3e80-175">Herstellen van alle Nuget-pakketten met de rechtermuisknop op de oplossing > **NuGet-pakketten beheren voor oplossing** > **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="c3e80-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span></span>
3. <span data-ttu-id="c3e80-176">Met de rechtermuisknop op **MultiChannelToDo.Web** > **Application Insights Telemetry toevoegen** > **-instellingen configureren** > resourcegroep wijzigen tooToDoApp*&lt;your_suffix >* > **Application Insights toevoegen tooProject**.</span><span class="sxs-lookup"><span data-stu-id="c3e80-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group tooToDoApp*&lt;your_suffix>* > **Add Application Insights tooProject**.</span></span>
4. <span data-ttu-id="c3e80-177">Open in hello Azure Portal, Hallo blade voor Hallo **MultiChannelToDo.Web** toepassing inzicht resource.</span><span class="sxs-lookup"><span data-stu-id="c3e80-177">In hello Azure Portal, open hello blade for hello **MultiChannelToDo.Web** Application Insight resource.</span></span> <span data-ttu-id="c3e80-178">Klik dan in Hallo **toepassingsstatus** deel, klikt u op **meer informatie over hoe de gegevens voor het laden van browserpagina toocollect** > code kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c3e80-178">Then in hello **Application health** part, click **Learn how toocollect browser page load data** > copy code.</span></span>
5. <span data-ttu-id="c3e80-179">Voeg Hallo gekopieerd JS instrumentation code te*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml net vóór Hallo sluiten `<heading>` label.</span><span class="sxs-lookup"><span data-stu-id="c3e80-179">Add hello copied JS instrumentation code too*&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, just before hello closing `<heading>` tag.</span></span> <span data-ttu-id="c3e80-180">Hallo unieke instrumentatiesleutel van uw toepassing inzicht resource moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="c3e80-180">It should contain hello unique instrumentation key of your Application Insight resource.</span></span>

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. <span data-ttu-id="c3e80-181">Aangepaste gebeurtenissen tooApplication Insights voor klikken met de muis door toe te voegen Hallo na code toohello onder aan de hoofdtekst verzenden:</span><span class="sxs-lookup"><span data-stu-id="c3e80-181">Send custom events tooApplication Insights for mouse clicks by adding hello following code toohello bottom of body:</span></span>

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   <span data-ttu-id="c3e80-182">Deze JavaScript-fragment verzendt een aangepaste gebeurtenis tooApplication Insights telkens wanneer een gebruiker klikt op een willekeurige plaats in Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="c3e80-182">This JavaScript snippet sends a custom event tooApplication Insights every time a user clicks anywhere in hello web app.</span></span>
7. <span data-ttu-id="c3e80-183">In de Git-Shell doorvoeren en uw wijzigingen tooyour fork push in GitHub.</span><span class="sxs-lookup"><span data-stu-id="c3e80-183">In Git Shell, commit and push your changes tooyour fork in GitHub.</span></span> <span data-ttu-id="c3e80-184">Wacht tot clients toorefresh browser.</span><span class="sxs-lookup"><span data-stu-id="c3e80-184">Then, wait for clients toorefresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. <span data-ttu-id="c3e80-185">Wisseling Hallo app wijzigingen tooproduction geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="c3e80-185">Swap hello deployed app changes tooproduction:</span></span>

     <span data-ttu-id="c3e80-186">. \swap – naam ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="c3e80-186">.\swap –Name ToDoApp<your_suffix></span></span>
9. <span data-ttu-id="c3e80-187">Blader toohello Application Insights-resource die u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c3e80-187">Browse toohello Application Insights resource that you configured.</span></span> <span data-ttu-id="c3e80-188">Klik op aangepaste gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-188">Click Custom events.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   <span data-ttu-id="c3e80-189">Als er geen metrische gegevens voor aangepaste gebeurtenissen, wacht een paar minuten en klik op **vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="c3e80-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span></span>

<span data-ttu-id="c3e80-190">Stel dat u zien als een diagram hieronder:</span><span class="sxs-lookup"><span data-stu-id="c3e80-190">Suppose you see a chart like below:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

<span data-ttu-id="c3e80-191">En Hallo gebeurtenis raster hieronder:</span><span class="sxs-lookup"><span data-stu-id="c3e80-191">And hello event grid below it:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

<span data-ttu-id="c3e80-192">Volgens tooyour ToDoApp toepassingscode, Hallo **knop** gebeurtenis komt overeen met de knop verzenden toohello en Hallo **invoer** gebeurtenis komt overeen met toohello textbox.</span><span class="sxs-lookup"><span data-stu-id="c3e80-192">According tooyour ToDoApp application code, hello **BUTTON** event corresponds toohello submit button, and hello **INPUT** event corresponds toohello textbox.</span></span> <span data-ttu-id="c3e80-193">Tot nu toe, zinvol wat zijn.</span><span class="sxs-lookup"><span data-stu-id="c3e80-193">So far, things make sense.</span></span> <span data-ttu-id="c3e80-194">Echter, het lijkt erop dat er een goede bedrag van muisklikken en zeer weinig klikken op Hallo taakitems is (Hallo **LI** gebeurtenissen).</span><span class="sxs-lookup"><span data-stu-id="c3e80-194">However, it looks like there's a good amount of clicks and very few clicks on hello to-do items (hello **LI** events).</span></span>

<span data-ttu-id="c3e80-195">Op basis van dit formulier u uw hypothese dat sommige gebruikers hebben verward welk gedeelte van Hallo UI klikbaar en is dit omdat Hallo cursor voor de geselecteerde tekst is opgemaakt als u dit op Hallo lijstitems en hun pictogrammen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-195">Based on this, you form your hypothesis that some users are confused which part of hello UI is clickable and it is because hello cursor is styled for text selection when it hovers on hello list items and their icons.</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

<span data-ttu-id="c3e80-196">Dit wordt mogelijk een voorbeeld van een gekunstelde.</span><span class="sxs-lookup"><span data-stu-id="c3e80-196">This might be a contrived example.</span></span> <span data-ttu-id="c3e80-197">Niettemin u bent momenteel toomake een verbetering tooyour app en voer flighting implementatie tooget bruikbaarheid feedback van live-klanten.</span><span class="sxs-lookup"><span data-stu-id="c3e80-197">Nevertheless, you're going toomake an improvement tooyour app, and then perform a flighting deployment tooget usability feedback from live customers.</span></span>

### <a name="instrument-your-server-app-for-monitoringmetrics"></a><span data-ttu-id="c3e80-198">Softwareontwikkelaars van uw server-app voor bewaking/metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="c3e80-198">Instrument your server app for monitoring/metrics</span></span>
<span data-ttu-id="c3e80-199">Dit is een tangens omdat Hallo-scenario in deze zelfstudie uitgelegd alleen met de Hallo client-app omgaat.</span><span class="sxs-lookup"><span data-stu-id="c3e80-199">This is a tangent since hello scenario demonstrated in this tutorial only deals with hello client app.</span></span> <span data-ttu-id="c3e80-200">Echter, voor de volledigheid stelt u Hallo serverzijde app.</span><span class="sxs-lookup"><span data-stu-id="c3e80-200">However, for completeness you will set up hello server-side app.</span></span>

1. <span data-ttu-id="c3e80-201">Met de rechtermuisknop op **MultiChannelToDo** > **Application Insights Telemetry toevoegen** > **-instellingen configureren** > resourcegroep wijzigen tooToDoApp*&lt;your_suffix >* > **Application Insights toevoegen tooProject**.</span><span class="sxs-lookup"><span data-stu-id="c3e80-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group tooToDoApp*&lt;your_suffix>* > **Add Application Insights tooProject**.</span></span>
2. <span data-ttu-id="c3e80-202">In de Git-Shell doorvoeren en uw wijzigingen tooyour fork push in GitHub.</span><span class="sxs-lookup"><span data-stu-id="c3e80-202">In Git Shell, commit and push your changes tooyour fork in GitHub.</span></span> <span data-ttu-id="c3e80-203">Wacht tot clients toorefresh browser.</span><span class="sxs-lookup"><span data-stu-id="c3e80-203">Then, wait for clients toorefresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. <span data-ttu-id="c3e80-204">Wisseling Hallo app wijzigingen tooproduction geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="c3e80-204">Swap hello deployed app changes tooproduction:</span></span>

     <span data-ttu-id="c3e80-205">. \swap – naam ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="c3e80-205">.\swap –Name ToDoApp<your_suffix></span></span>

<span data-ttu-id="c3e80-206">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="c3e80-206">That's it!</span></span>

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a><span data-ttu-id="c3e80-207">Onderzoeken: Metrische gegevens voor site-specifieke labels tooyour client app toevoegen</span><span class="sxs-lookup"><span data-stu-id="c3e80-207">Investigate: Add slot-specific tags tooyour client app metrics</span></span>
<span data-ttu-id="c3e80-208">In deze sectie configureert u Hallo verschillende implementatie sleuven toosend sleuf-specifieke telemetrie toohello dezelfde Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="c3e80-208">In this section, you will configure hello different deployment slots toosend slot-specific telemetry toohello same Application Insights resource.</span></span> <span data-ttu-id="c3e80-209">Op deze manier kunt u telemetrie vergelijken gegevens tussen verkeer van andere sleuven (implementatieomgevingen) tooeasily Hallo effect van uw appwijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="c3e80-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) tooeasily see hello effect of your app changes.</span></span> <span data-ttu-id="c3e80-210">AT Hallo dezelfde tijd, kunt u Hallo productie verkeer van Hallo rest scheiden zodat u kunt doorgaan toomonitor uw productie-app naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="c3e80-210">At hello same time, you can separate hello production traffic from hello rest so you can continue toomonitor your production app as needed.</span></span>

<span data-ttu-id="c3e80-211">Nadat u van gegevens op clientgedrag verzamelen bent, wordt u [toevoegen van een telemetrie initialisatiefunctie tooyour JavaScript-code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span><span class="sxs-lookup"><span data-stu-id="c3e80-211">Since you're gathering data on client behavior, you will [add a telemetry initializer tooyour JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span></span> <span data-ttu-id="c3e80-212">Als u tootest serverzijde prestaties wilt, bijvoorbeeld: u kunt ook doen op dezelfde manier in uw servercode (Zie [Application Insights-API voor aangepaste gebeurtenissen en metrische gegevens](../application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c3e80-212">If you want tootest server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span></span>

1. <span data-ttu-id="c3e80-213">Voeg eerst Hallo code bewteen Hallo twee `//` opmerkingen hieronder in Hallo JavaScript-blok dat u toohello toegevoegd `<heading>` eerder labelen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-213">First, add hello code bewteen hello two `//` comments below in hello JavaScript block that you added toohello `<heading>` tag earlier.</span></span>

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

    <span data-ttu-id="c3e80-214">Deze code initialisatiefunctie zorgt ervoor dat Hallo `appInsights` object tooadd Hallo een aangepaste eigenschap met de naam `Environment` tooevery stukje telemetrie verzendt.</span><span class="sxs-lookup"><span data-stu-id="c3e80-214">This initializer code causes hello `appInsights` object tooadd hello a custom property called `Environment` tooevery piece of telemetry it sends.</span></span>
2. <span data-ttu-id="c3e80-215">Vervolgens voegt u deze aangepaste eigenschap als een [instelling sleuf](web-sites-staged-publishing.md#AboutConfiguration) voor uw web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e80-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span></span> <span data-ttu-id="c3e80-216">toodo deze, Voer Hallo opdrachten te volgen in uw sessie Git-Shell.</span><span class="sxs-lookup"><span data-stu-id="c3e80-216">toodo this, run hello following commands in your Git Shell session.</span></span>

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    <span data-ttu-id="c3e80-217">Hallo Web.config in uw project al definieert Hallo `environment` app-instelling.</span><span class="sxs-lookup"><span data-stu-id="c3e80-217">hello Web.config in your project already defines hello `environment` app setting.</span></span> <span data-ttu-id="c3e80-218">Met deze instelling wanneer u een lokaal, Hallo-app test metrische gegevens over uw worden gemarkeerd met `VS Debugger`.</span><span class="sxs-lookup"><span data-stu-id="c3e80-218">With this setting, when you test hello app locally, your metrics will be tagged with `VS Debugger`.</span></span> <span data-ttu-id="c3e80-219">Echter, wanneer u uw wijzigingen tooAzure pushen, Azure wordt zoeken en Hallo `environment` app-instelling in configuratie van de Hallo van web-app in plaats daarvan en metrische gegevens over uw worden gemarkeerd met `Production`.</span><span class="sxs-lookup"><span data-stu-id="c3e80-219">However, when you push your changes tooAzure, Azure will find and use hello `environment` app setting in hello web app's configuration instead, and your metrics will be tagged with `Production`.</span></span>
3. <span data-ttu-id="c3e80-220">Doorvoeren en uw code wijzigingen tooyour fork push op GitHub en wacht voor uw gebruikers toouse Hallo nieuwe app (nodig toorefresh Hallo-browser).</span><span class="sxs-lookup"><span data-stu-id="c3e80-220">Commit and push your code changes tooyour fork on GitHub, and then wait for your users toouse hello new app (need toorefresh hello browser).</span></span> <span data-ttu-id="c3e80-221">Het duurt ongeveer 15 minuten voor de nieuwe eigenschap tooshow Hallo omhoog in uw Application Insights `MultiChannelToDo.Web` resource.</span><span class="sxs-lookup"><span data-stu-id="c3e80-221">It takes about 15 minutes for hello new property tooshow up in your Application Insights `MultiChannelToDo.Web` resource.</span></span>

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. <span data-ttu-id="c3e80-222">Nu gaat u toohello **aangepaste gebeurtenissen** blade opnieuw en filter Hallo metrische gegevens op `Environment=Production`.</span><span class="sxs-lookup"><span data-stu-id="c3e80-222">Now, go toohello **Custom events** blade again and filter hello metrics on `Environment=Production`.</span></span> <span data-ttu-id="c3e80-223">Nu moet u kunnen toosee alle Hallo nieuwe aangepaste gebeurtenissen in productie Hallo sleuf met dit filter.</span><span class="sxs-lookup"><span data-stu-id="c3e80-223">You should now be able toosee all hello new custom events in hello production slot with this filter.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. <span data-ttu-id="c3e80-224">Klik op Hallo **Favorieten** knop toosave Hallo huidige Metrics Explorer-instellingen toosomething zoals **aangepaste gebeurtenissen: productie**.</span><span class="sxs-lookup"><span data-stu-id="c3e80-224">Click hello **Favorites** button toosave hello current Metrics Explorer settings toosomething like **Custom events: Production**.</span></span> <span data-ttu-id="c3e80-225">U kunt eenvoudig schakelen tussen deze weergaven en een implementatiesleuf later.</span><span class="sxs-lookup"><span data-stu-id="c3e80-225">You can easily switch between this view and a deployment slot view later.</span></span>

   > [!TIP]
   > <span data-ttu-id="c3e80-226">Voor nog krachtiger analytics, kunt u overwegen [integreren van uw Application Insights-resource met Power BI](../application-insights/app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="c3e80-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span></span>
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a><span data-ttu-id="c3e80-227">Site-specifieke labels tooyour serverstatistieken app toevoegen</span><span class="sxs-lookup"><span data-stu-id="c3e80-227">Add slot-specific tags tooyour server app metrics</span></span>
<span data-ttu-id="c3e80-228">Opnieuw voor de volledigheid stelt u Hallo serverzijde app.</span><span class="sxs-lookup"><span data-stu-id="c3e80-228">Again, for completeness you will set up hello server-side app.</span></span> <span data-ttu-id="c3e80-229">In tegenstelling tot Hallo client-app die in JavaScript is geïnstrumenteerd, sleuf-specifieke labels voor Hallo server app is geïnstrumenteerd met .NET-code.</span><span class="sxs-lookup"><span data-stu-id="c3e80-229">Unlike hello client app which is instrumented in JavaScript, slot-specific tags for hello server app is instrumented with .NET code.</span></span>

1. <span data-ttu-id="c3e80-230">Open  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="c3e80-230">Open *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs.</span></span> <span data-ttu-id="c3e80-231">Hallo codeblok hieronder, net vóór Hallo naamruimte accolade sluiten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-231">Add hello code block below, just before hello closing namespace curly brace.</span></span>

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
2. <span data-ttu-id="c3e80-232">Hallo name resolution fouten corrigeren door toe te voegen Hallo `using` instructies hieronder toohello begin van Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="c3e80-232">Correct hello name resolution errors by adding hello `using` statements below toohello beginning of hello file:</span></span>

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. <span data-ttu-id="c3e80-233">Voeg code hieronder toohello begin Hallo Hallo `Application_Start()` methode:</span><span class="sxs-lookup"><span data-stu-id="c3e80-233">Add hello code below toohello beginning of hello `Application_Start()` method:</span></span>

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. <span data-ttu-id="c3e80-234">Doorvoeren en uw code wijzigingen tooyour fork push op GitHub en wacht voor uw gebruikers toouse Hallo nieuwe app (nodig toorefresh Hallo-browser).</span><span class="sxs-lookup"><span data-stu-id="c3e80-234">Commit and push your code changes tooyour fork on GitHub, and then wait for your users toouse hello new app (need toorefresh hello browser).</span></span> <span data-ttu-id="c3e80-235">Het duurt ongeveer 15 minuten voor de nieuwe eigenschap tooshow Hallo omhoog in uw Application Insights `MultiChannelToDo` resource.</span><span class="sxs-lookup"><span data-stu-id="c3e80-235">It takes about 15 minutes for hello new property tooshow up in your Application Insights `MultiChannelToDo` resource.</span></span>

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a><span data-ttu-id="c3e80-236">Update: Stel uw vertakking beta</span><span class="sxs-lookup"><span data-stu-id="c3e80-236">Update: Set up your beta branch</span></span>
1. <span data-ttu-id="c3e80-237">Open  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json en zoeken naar Hallo `appsettings` resources (zoeken naar `"name": "appsettings"`).</span><span class="sxs-lookup"><span data-stu-id="c3e80-237">Open *&lt;repository_root>*\ARMTemplates\ProdAndStagetest.json and find hello `appsettings` resources (search for `"name": "appsettings"`).</span></span> <span data-ttu-id="c3e80-238">Er zijn 4 daarvan, één voor elke site.</span><span class="sxs-lookup"><span data-stu-id="c3e80-238">There are 4 of them, one for each slot.</span></span>
2. <span data-ttu-id="c3e80-239">Voor elk `appsettings` resource, Voeg een `"environment": "[parameters('slotName')]"` end van app-instelling toohello Hallo `properties` matrix.</span><span class="sxs-lookup"><span data-stu-id="c3e80-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting toohello end of hello `properties` array.</span></span> <span data-ttu-id="c3e80-240">Vergeet niet tooend Hallo vorige regel met een komma.</span><span class="sxs-lookup"><span data-stu-id="c3e80-240">Don't forget tooend hello previous line with a comma.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    <span data-ttu-id="c3e80-241">U hebt zojuist toegevoegd Hallo `environment` app tooall Hallo sleuven instellen in Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c3e80-241">You have just added hello `environment` app setting tooall hello slots in hello template.</span></span>
3. <span data-ttu-id="c3e80-242">In hetzelfde bestand Hallo, Hallo zoeken `slotconfignames` resources (zoeken naar `"name": "slotconfignames"`).</span><span class="sxs-lookup"><span data-stu-id="c3e80-242">In hello same file, find hello `slotconfignames` resources (search for `"name": "slotconfignames"`).</span></span> <span data-ttu-id="c3e80-243">Er zijn 2 één voor elke app.</span><span class="sxs-lookup"><span data-stu-id="c3e80-243">There are 2 of them, one for each app.</span></span>
4. <span data-ttu-id="c3e80-244">Voor elk `slotconfignames` resource toevoegen `"environment"` toohello einde van Hallo `appSettingNames` matrix.</span><span class="sxs-lookup"><span data-stu-id="c3e80-244">For each `slotconfignames` resource, add `"environment"` toohello end of hello `appSettingNames` array.</span></span> <span data-ttu-id="c3e80-245">Vergeet niet tooend Hallo vorige regel met een komma.</span><span class="sxs-lookup"><span data-stu-id="c3e80-245">Don't forget tooend hello previous line with a comma.</span></span>

    <span data-ttu-id="c3e80-246">U hebt zojuist hebt gemaakt Hallo `environment` app instelling stick tooits respectieve implementatiesleuf voor beide apps.</span><span class="sxs-lookup"><span data-stu-id="c3e80-246">You have just made hello `environment` app setting stick tooits respective deployment slot for both apps.</span></span>  
5. <span data-ttu-id="c3e80-247">In de Git-Shell-sessie uitvoeren Hallo deze opdrachten Hello dezelfde resource groep achtervoegsel dat u eerder hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c3e80-247">In your Git Shell session, run hello following commands with hello same resource group suffix that you used before.</span></span>

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. <span data-ttu-id="c3e80-248">Wanneer u wordt gevraagd, geeft u Hallo dezelfde referenties voor SQL-database als voorheen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-248">When prompted, specify hello same SQL database credentials as before.</span></span> <span data-ttu-id="c3e80-249">Wanneer gevraagd vervolgens tooupdate Hallo-resourcegroep, type `Y`, klikt u vervolgens `ENTER`.</span><span class="sxs-lookup"><span data-stu-id="c3e80-249">Then, when asked tooupdate hello resource group, type `Y`, then `ENTER`.</span></span>

    <span data-ttu-id="c3e80-250">Zodra het Hallo-script is voltooid, alle resources in de oorspronkelijke resourcegroep Hallo worden bewaard, maar een nieuwe site met de naam "bètaversie" wordt gemaakt in het met Hallo dezelfde configuratie als Hallo "Fasering" sleuf dat is gemaakt in Hallo begin.</span><span class="sxs-lookup"><span data-stu-id="c3e80-250">Once hello script finishes, all your resources in hello original resource group are retained, but a new slot named "beta" is created in it with hello same configuration as hello "Staging" slot that was created in hello beginning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c3e80-251">Deze methode voor het maken van verschillende omgevingen verschilt van het Hallo-methode in [flexibele software ontwikkelen met Azure App Service](app-service-agile-software-development.md).</span><span class="sxs-lookup"><span data-stu-id="c3e80-251">This method of creating different deployment environments is different from hello method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span></span> <span data-ttu-id="c3e80-252">Hier, maakt u implementatieomgevingen met implementatiesites, waar als er u implementatieomgevingen met resourcegroepen maken.</span><span class="sxs-lookup"><span data-stu-id="c3e80-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span></span> <span data-ttu-id="c3e80-253">Implementatieomgevingen beheren met resourcegroepen kunt u tookeep Hallo productie-omgeving off-limits toodevelopers, maar het is niet eenvoudig toodo testen in productie, waarmee u eenvoudig met sleuven doen kunt.</span><span class="sxs-lookup"><span data-stu-id="c3e80-253">Managing deployment environments with resource groups enables you tookeep hello production environment off-limits toodevelopers, but it's not easy toodo testing in production, which you can do easily with slots.</span></span>
   >
   >

<span data-ttu-id="c3e80-254">Als u wenst, kunt u ook een alfa-app maken door te voeren</span><span class="sxs-lookup"><span data-stu-id="c3e80-254">If you wish, you can also create an alpha app by running</span></span>

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

<span data-ttu-id="c3e80-255">Voor deze zelfstudie, wordt u alleen blijven gebruiken uw bèta-app.</span><span class="sxs-lookup"><span data-stu-id="c3e80-255">For this tutorial, you will just keep using your beta app.</span></span>

## <a name="update-push-your-updates-toohello-beta-app"></a><span data-ttu-id="c3e80-256">Update: Push uw updates toohello beta-app</span><span class="sxs-lookup"><span data-stu-id="c3e80-256">Update: Push your updates toohello beta app</span></span>
<span data-ttu-id="c3e80-257">Back-tooyour-app die u tooimprove wilt maken.</span><span class="sxs-lookup"><span data-stu-id="c3e80-257">Back tooyour app that you want tooimprove.</span></span>

1. <span data-ttu-id="c3e80-258">Zorg ervoor dat u kunt nu uw vertakking beta</span><span class="sxs-lookup"><span data-stu-id="c3e80-258">Make sure you're now in your beta branch</span></span>

        git checkout beta
2. <span data-ttu-id="c3e80-259">In  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, zoeken Hallo `<li>` labelen en voeg Hallo `style="cursor:pointer"` kenmerk toe, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c3e80-259">In *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, find hello `<li>` tag and add hello `style="cursor:pointer"` attribute, as shown below.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. <span data-ttu-id="c3e80-260">doorvoeren en tooAzure push.</span><span class="sxs-lookup"><span data-stu-id="c3e80-260">commit and push tooAzure.</span></span>
4. <span data-ttu-id="c3e80-261">Controleer of deze Hallo wijziging nu gereflecteerd in Hallo beta sleuf door te navigeren toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/.</span><span class="sxs-lookup"><span data-stu-id="c3e80-261">Verify that hello change is now reflected in hello beta slot by navigating toohttp://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span></span> <span data-ttu-id="c3e80-262">Als er geen Hallo wijzigen nog Vernieuw uw browser tooget Hallo nieuwe javascript-code.</span><span class="sxs-lookup"><span data-stu-id="c3e80-262">If you don't see hello change yet, refresh your browser tooget hello new javascript code.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

<span data-ttu-id="c3e80-263">Nu dat u uw wijziging in Hallo beta sleuf wordt uitgevoerd hebt, bent u klaar tooperform een flighting implementatie.</span><span class="sxs-lookup"><span data-stu-id="c3e80-263">Now that you have your change running in hello beta slot, you are ready tooperform a flighting deployment.</span></span>

## <a name="validate-route-traffic-toohello-beta-app"></a><span data-ttu-id="c3e80-264">Valideren: Route verkeer toohello beta-app</span><span class="sxs-lookup"><span data-stu-id="c3e80-264">Validate: Route traffic toohello beta app</span></span>
<span data-ttu-id="c3e80-265">In deze sectie wordt u verkeer toohello beta app versturen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-265">In this section, you will route traffic toohello beta app.</span></span> <span data-ttu-id="c3e80-266">Ter verduidelijking van demonstratie gaat u een groot deel van Hallo gebruiker verkeer tooit tooroute.</span><span class="sxs-lookup"><span data-stu-id="c3e80-266">For sake of clarity of demonstration, you're going tooroute a significant portion of hello user traffic tooit.</span></span> <span data-ttu-id="c3e80-267">Hallo hoeveelheid verkeer die u wilt dat tooroute hangen af van uw specifieke situatie in werkelijkheid is.</span><span class="sxs-lookup"><span data-stu-id="c3e80-267">In reality, hello amount of traffic you want tooroute will depend on your specific situation.</span></span> <span data-ttu-id="c3e80-268">Bijvoorbeeld, als uw site op Hallo van schaal van microsoft.com, mogelijk moet u minder dan één procent van uw totale verkeer in volgorde toogain nuttige gegevens.</span><span class="sxs-lookup"><span data-stu-id="c3e80-268">For example, if your site is at hello scale of microsoft.com, then you may need less than one percent of your total traffic in order toogain useful data.</span></span>

1. <span data-ttu-id="c3e80-269">In uw sessie Git Shell uitvoeren Hallo opdrachten tooroute na de helft van Hallo verkeer toohello beta productiesite:</span><span class="sxs-lookup"><span data-stu-id="c3e80-269">In your Git Shell session, run hello following commands tooroute half of hello production traffic toohello beta slot:</span></span>

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   <span data-ttu-id="c3e80-270">Hallo `ReroutePercentage=50` -eigenschap geeft op dat de 50% van Hallo productie verkeer gerouteerd toohello beta app-URL worden (opgegeven door Hallo `ActionHostName` eigenschap).</span><span class="sxs-lookup"><span data-stu-id="c3e80-270">hello `ReroutePercentage=50` property specifies that 50% of hello production traffic will be routed toohello beta app's URL (specified by hello `ActionHostName` property).</span></span>
2. <span data-ttu-id="c3e80-271">Navigeer nu toohttp://ToDoApp*&lt;your_suffix >*. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="c3e80-271">Now navigate toohttp://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span></span> <span data-ttu-id="c3e80-272">50% van het Hallo-verkeer worden omgeleid toohello beta sleuf nu.</span><span class="sxs-lookup"><span data-stu-id="c3e80-272">50% of hello traffic should now be redirected toohello beta slot.</span></span>
3. <span data-ttu-id="c3e80-273">Filter in uw Application Insights-resource Hallo metrische gegevens door omgeving = "bètaversie".</span><span class="sxs-lookup"><span data-stu-id="c3e80-273">In your Application Insights resource, filter hello metrics by environment="beta".</span></span>

   > [!NOTE]
   > <span data-ttu-id="c3e80-274">Als u deze gefilterde weergave als een andere favoriet opslaan, kunt u eenvoudig hello metrische explorer weergaven tussen productie en beta weergaven spiegelen.</span><span class="sxs-lookup"><span data-stu-id="c3e80-274">If you save this filtered view as another favorite, then you can easily flip hello metric explorer views between production and beta views.</span></span>
   >
   >

<span data-ttu-id="c3e80-275">Stel in Application Insights ziet er iets dergelijks toohello:</span><span class="sxs-lookup"><span data-stu-id="c3e80-275">Suppose in Application Insights you see something similar toohello following:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

<span data-ttu-id="c3e80-276">Niet alleen wordt dit weergegeven dat er veel meer klikt op Hallo zijn `<li>` tags, maar er lijkt een piek muisklikken toobe op `<li>` labels.</span><span class="sxs-lookup"><span data-stu-id="c3e80-276">Not only is this showing that there are many more clicks on hello `<li>` tags, but there seems toobe a surge of clicks on `<li>` tags.</span></span> <span data-ttu-id="c3e80-277">U kunt beëindigt mensen gedetecteerd zijn nieuwe Hallo `<li>` tags zijn klikbaar en alle taken eerder voltooid in Hallo-app wordt nu worden gewist.</span><span class="sxs-lookup"><span data-stu-id="c3e80-277">You can then conclude that people have discovered hello new `<li>` tags are clickable and are now clearing all their previously-completed tasks in hello app.</span></span>

<span data-ttu-id="c3e80-278">Op basis van gegevens van uw implementatie flighting Hallo kunt bepalen u dat de nieuwe gebruikersinterface gereed voor productie is.</span><span class="sxs-lookup"><span data-stu-id="c3e80-278">Based on hello data of your flighting deployment, you decide that your new UI is ready for production.</span></span>

## <a name="go-live-move-your-new-code-into-production"></a><span data-ttu-id="c3e80-279">Ga live: je nieuwe code naar de productie verplaatsen</span><span class="sxs-lookup"><span data-stu-id="c3e80-279">Go live: Move your new code into production</span></span>
<span data-ttu-id="c3e80-280">U bent nu klaar toomove uw tooproduction update.</span><span class="sxs-lookup"><span data-stu-id="c3e80-280">You're now ready toomove your update tooproduction.</span></span> <span data-ttu-id="c3e80-281">Is die wat is een goede nu u weet dat de update is al gevalideerd *voordat* tooproduction wordt deze doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="c3e80-281">What's great is that now you know that your update has already been validated *before* it is pushed tooproduction.</span></span> <span data-ttu-id="c3e80-282">Nu kunt u probleemloos deze implementeren.</span><span class="sxs-lookup"><span data-stu-id="c3e80-282">So now you can confidently deploy it.</span></span> <span data-ttu-id="c3e80-283">Nadat u een update toohello AngularJS-client-app hebt gemaakt, worden alleen Hallo clientcode gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="c3e80-283">Since you made an update toohello AngularJS client app, you only validated hello client-side code.</span></span> <span data-ttu-id="c3e80-284">Als u toomake wijzigingen toohello back-end Web API-app, kunt u uw wijzigingen kan valideren op dezelfde manier en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="c3e80-284">If you were toomake changes toohello back-end Web API app, you could validate your changes similarly and easily.</span></span>

1. <span data-ttu-id="c3e80-285">In de Git-Shell verwijderen routeringsregel Hallo-verkeer door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="c3e80-285">In Git Shell, remove hello traffic routing rule by running hello following command:</span></span>

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. <span data-ttu-id="c3e80-286">Voer Hallo Git-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="c3e80-286">Run hello Git commands:</span></span>

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. <span data-ttu-id="c3e80-287">Wacht een paar minuten voordat Hallo nieuwe toobe geïmplementeerd toohello faseringssleuven code en vervolgens starten http://ToDoApp*&lt;your_suffix >*-staging.azurewebsites.net tooverify die nieuwe update Hallo is opgewarmd in Hallo fasering sleuf.</span><span class="sxs-lookup"><span data-stu-id="c3e80-287">Wait for a few minutes for hello new code toobe deployed toohello staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net tooverify that hello new update is warmed up in hello staging slot.</span></span> <span data-ttu-id="c3e80-288">Houd er rekening mee dat uw fork hoofdvertakking is Hallo gekoppeld toohello fasering sleuf van uw app.</span><span class="sxs-lookup"><span data-stu-id="c3e80-288">Remember that hello your fork's master branch is linked toohello staging slot of your app.</span></span>
4. <span data-ttu-id="c3e80-289">Nu wisselen Hallo faseringssleuven in productie</span><span class="sxs-lookup"><span data-stu-id="c3e80-289">Now, swap hello staging slot into production</span></span>

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a><span data-ttu-id="c3e80-290">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c3e80-290">Summary</span></span>
<span data-ttu-id="c3e80-291">Azure App Service maakt het eenvoudig voor kleine toomedium grote bedrijven tootest hun apps klantgerichte in productie, is er iets die doorgaans in grote ondernemingen is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c3e80-291">Azure App Service makes it easy for small- toomedium-sized businesses tootest their customer-facing apps in production, something that has been traditionally done in big enterprises.</span></span> <span data-ttu-id="c3e80-292">In het ideale geval, deze zelfstudie hebt gekregen kennis moet u toobring samen App Service en de Application Insights toomake mogelijke zeker implementatie en zelfs andere testen in productie-scenario's in uw DevOps-wereld Hallo.</span><span class="sxs-lookup"><span data-stu-id="c3e80-292">Hopefully, this tutorial has given you hello knowledge you need toobring together App Service and Application Insights toomake possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span></span>

## <a name="more-resources"></a><span data-ttu-id="c3e80-293">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="c3e80-293">More resources</span></span>
* [<span data-ttu-id="c3e80-294">Flexibele software ontwikkelen met Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c3e80-294">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="c3e80-295">Faseringsomgevingen voor web-apps in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="c3e80-295">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="c3e80-296">Een complexe toepassing zoals verwacht in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="c3e80-296">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="c3e80-297">Azure Resource Manager-sjablonen ontwerpen</span><span class="sxs-lookup"><span data-stu-id="c3e80-297">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="c3e80-298">JSONLint - Hallo JSON Validator</span><span class="sxs-lookup"><span data-stu-id="c3e80-298">JSONLint - hello JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="c3e80-299">GIT vertakking – basis vertakking en samenvoegen</span><span class="sxs-lookup"><span data-stu-id="c3e80-299">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="c3e80-300">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3e80-300">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="c3e80-301">Project Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="c3e80-301">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)
