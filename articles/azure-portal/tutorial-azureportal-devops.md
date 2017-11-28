---
title: 'Zelfstudie: DevOps Hello Azure Portal | Microsoft Docs'
description: Meer informatie over verschillende DevOps-werkstromen in Azure Portal Hallo Hallo.
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a><span data-ttu-id="0cc98-103">Zelfstudie: DevOps Hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0cc98-103">Tutorial: DevOps with hello Azure Portal</span></span>
<span data-ttu-id="0cc98-104">Hello Azure-platform is vol. van flexibele DevOps-werkstromen</span><span class="sxs-lookup"><span data-stu-id="0cc98-104">hello Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="0cc98-105">In deze zelfstudie leert u hoe tooleverage Hallo mogelijkheden van Azure Portal-toodevelop hello, testen, implementeren, oplossen, bewaken en beheren van actieve toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-105">In this tutorial, you learn how tooleverage hello capabilities of hello Azure Portal toodevelop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="0cc98-106">Deze zelfstudie richt zich op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="0cc98-106">This tutorial focuses on hello following:</span></span>

1. <span data-ttu-id="0cc98-107">Een webtoepassing maken en continue implementatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="0cc98-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="0cc98-108">Een app ontwikkelen en testen</span><span class="sxs-lookup"><span data-stu-id="0cc98-108">Develop and test an app</span></span>
3. <span data-ttu-id="0cc98-109">Een app bewaken en problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="0cc98-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="0cc98-110">Algemene taken voor toepassingsbeheer</span><span class="sxs-lookup"><span data-stu-id="0cc98-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="0cc98-111">Een webtoepassing maken en continue implementatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="0cc98-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="0cc98-112">Maken van een Web-app met [Azure App Service](https://azure.microsoft.com/services/app-service/), gebruikt u in de rest van deze handleiding Hallo.</span><span class="sxs-lookup"><span data-stu-id="0cc98-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in hello rest of this tutorial.</span></span> <span data-ttu-id="0cc98-113">In eerste instantie schakelt u continue implementatie in vanuit de opslagplaats van de broncode naar de actieve Azure-omgeving.</span><span class="sxs-lookup"><span data-stu-id="0cc98-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="0cc98-114">Meld u aan bij hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0cc98-114">Sign into hello Azure Portal</span></span>
2. <span data-ttu-id="0cc98-115">Kies **App Services** &gt; **pictogram toevoegen** en voer een naam, kiest u uw abonnement en een nieuwe resource groep tooserve als Hallo-container voor Hallo service maken.</span><span class="sxs-lookup"><span data-stu-id="0cc98-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group tooserve as hello container for hello service.</span></span>
   
   <span data-ttu-id="0cc98-116">Resourcegroepen kunnen u toomanage verschillende aspecten van Hallo oplossing zoals facturering, implementaties en bewaakt alle als één groep via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cc98-116">Resource groups allow you toomanage various aspects of hello solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="0cc98-118">Na enkele ogenblikken is de app-service gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0cc98-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="0cc98-119">Haal een paar minuten tooexplore Hallo verschillende opties voor Hallo-service in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="0cc98-119">Take a few minutes tooexplore hello various menu options for hello service in hello portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="0cc98-121">Klik op Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="0cc98-121">Click hello URL.</span></span> <span data-ttu-id="0cc98-122">U ziet Hallo verschillende beschikbare opties voor hulpprogramma's en -opslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-122">Notice hello variety of available choices for tools and repositories.</span></span> <span data-ttu-id="0cc98-123">U kunt ook Hallo talen en frameworks van uw keuze waaronder .NET, Java en Ruby gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0cc98-123">You can also use hello languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="0cc98-125">Hello Azure-portal maakt continue implementatie een eenvoudig proces waarbij slechts een paar eenvoudige stappen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-125">hello Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="0cc98-126">Kies in hello Azure-portal, instellingen van Hallo pictogram voor Hallo app service die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0cc98-126">In hello Azure portal, choose settings from hello icon for hello app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="0cc98-128">Schuif blade die wordt geopend op de juiste Hallo Hallo toohello sectie publiceren.</span><span class="sxs-lookup"><span data-stu-id="0cc98-128">From hello blade that opens on hello right, scroll toohello publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="0cc98-130">Configureer vervolgens een aantal instellingen tooenable continue implementatie voor Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="0cc98-130">Next, configure some settings tooenable continuous deployment for hello app.</span></span> <span data-ttu-id="0cc98-131">Klik op Implementatiebron en vervolgens op Bron kiezen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="0cc98-132">U ziet Hallo verschillende opties die u voor de opslagplaats bronnen hebt.</span><span class="sxs-lookup"><span data-stu-id="0cc98-132">Notice hello variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="0cc98-134">Kies voor dit voorbeeld GitHub.</span><span class="sxs-lookup"><span data-stu-id="0cc98-134">For this example choose GitHub.</span></span> <span data-ttu-id="0cc98-135">(Optioneel) Kies Hallo opslagplaats van uw keuze en Hallo autorisatiereferenties instellen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-135">Optionally choose hello repository of your choice and setup hello authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="0cc98-137">Na autorisatie tooyour opslagplaats, klikt u vervolgens kunt u een project en de gewenste toodeploy vertakking.</span><span class="sxs-lookup"><span data-stu-id="0cc98-137">After authorization tooyour repository, you can then choose a project and branch you wish toodeploy.</span></span> <span data-ttu-id="0cc98-138">Hieronder ziet u een aantal fictieve voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="0cc98-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="0cc98-140">Klik op OK nadat u het project en de vertakking hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="0cc98-141">U moet eerst toosee meldingen van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="0cc98-141">You should start toosee notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="0cc98-143">Navigeer terug tooGitHub toosee hello webhook toointegrate Hallo bron besturingselement opslagplaats is gemaakt met Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc98-143">Navigate back tooGitHub toosee hello webhook that was created toointegrate hello source control repo with Azure.</span></span> <span data-ttu-id="0cc98-144">Hello Azure Portal kunt integratie met GitHub met slechts een paar eenvoudige stappen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-144">hello Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="0cc98-146">doorlopende implementatie toodemonstrate, u de opslagplaats van bepaalde inhoud toohello snel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-146">toodemonstrate continuous deployment, you quickly add some content toohello repository.</span></span> <span data-ttu-id="0cc98-147">Voor een eenvoudig voorbeeld voegt u een voorbeeld tekst bestand tooa GitHub-repo.</span><span class="sxs-lookup"><span data-stu-id="0cc98-147">For a simple example, add a sample text file tooa GitHub repo.</span></span> <span data-ttu-id="0cc98-148">U bent gratis toouse .NET, Ruby, Python of een ander type toepassing met App Service.</span><span class="sxs-lookup"><span data-stu-id="0cc98-148">You are free toouse .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="0cc98-149">Gratis tooadd een tekstbestand van mening bent dat ASP.NET MVC, Java of Ruby toepassing toohello opslagplaats van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="0cc98-149">Feel free tooadd a text file, ASP.NET MVC, Java, or Ruby application toohello repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="0cc98-151">Na het doorvoeren van wijzigingen tooyour opslagplaats, ziet u een nieuwe implementatie in de portal meldingengebied Hallo initiëren.</span><span class="sxs-lookup"><span data-stu-id="0cc98-151">After committing changes tooyour repository, you see a new deployment initiate in hello portal notifications area.</span></span> <span data-ttu-id="0cc98-152">Klik op synchroniseren als u snel geen wijzigingen ziet na het vastleggen van de opslagplaats tooyour.</span><span class="sxs-lookup"><span data-stu-id="0cc98-152">Click Sync if you do not quickly see changes after committing tooyour repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="0cc98-154">Als u probeert en laden van pagina Hallo voor Hallo app service, wordt u op dit moment een fout 403.</span><span class="sxs-lookup"><span data-stu-id="0cc98-154">At this point, if you try and load hello page for hello app service, you may receive a 403 error.</span></span> <span data-ttu-id="0cc98-155">In dit voorbeeld is het omdat er geen typische standaard documentinstellingen voor Hallo pagina zoals een bestand zoals index.htm of default.html.</span><span class="sxs-lookup"><span data-stu-id="0cc98-155">In this example, it is because there is no typical default document setup for hello page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="0cc98-156">U kunt snel lost dit probleem Hello tooling in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="0cc98-156">You can quickly remedy this with hello tooling in hello Azure Portal.</span></span>  <span data-ttu-id="0cc98-157">Kies in hello Azure Portal instellingen &gt; toepassingsinstellingen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-157">In hello Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="0cc98-159">Er wordt nu een blade met toepassingsinstellingen geopend.</span><span class="sxs-lookup"><span data-stu-id="0cc98-159">A blade opens for application settings.</span></span> <span data-ttu-id="0cc98-160">Hallo-naam van Hallo pagina 'SamplePage.html' en klik op opslaan.</span><span class="sxs-lookup"><span data-stu-id="0cc98-160">Enter hello name of hello page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="0cc98-161">Duren voordat u een paar minuten tooexplore Hallo andere instellingen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-161">Take a few minutes tooexplore hello other settings.</span></span>
    
    ![image14][image14]
15. <span data-ttu-id="0cc98-163">Eventueel Vernieuw uw browser-URL tooensure ziet u de wijzigingen Hallo verwacht.</span><span class="sxs-lookup"><span data-stu-id="0cc98-163">Optionally refresh your browser URL tooensure you see hello expected changes.</span></span> <span data-ttu-id="0cc98-164">Er is in dit geval een aantal eenvoudige tekst hello pagina nu in te vullen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-164">In this case, there is some simple text now populating hello page.</span></span> <span data-ttu-id="0cc98-165">Elke aanvullende wijzigen toohello opslagplaats zou leiden tot een nieuwe automatische implementatie.</span><span class="sxs-lookup"><span data-stu-id="0cc98-165">Each additional change toohello repository would result in a new automatic deployment.</span></span>
    
    ![image15][image15]
    
    <span data-ttu-id="0cc98-167">Inschakelen van continue implementatie met hello Azure Portal is een eenvoudige ervaring.</span><span class="sxs-lookup"><span data-stu-id="0cc98-167">Enabling continuous deployment with hello Azure Portal is an easy experience.</span></span> <span data-ttu-id="0cc98-168">U kunt ook complexere release pijplijnen bouwen en veel andere technieken gebruiken met bestaande broncodebeheer en continue integratie systemen toodeploy tooAzure, zoals het gebruik van geautomatiseerde build en release beheersystemen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems toodeploy tooAzure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="0cc98-169">Een app ontwikkelen en testen</span><span class="sxs-lookup"><span data-stu-id="0cc98-169">Develop and test an app</span></span>
<span data-ttu-id="0cc98-170">Vervolgens brengt u enkele wijzigingen toohello code base en snel implementeren die wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-170">Next, make some changes toohello code base and rapidly deploy those changes.</span></span> <span data-ttu-id="0cc98-171">U wordt ook instellen om sommige prestatietests voor Hallo Web-app.</span><span class="sxs-lookup"><span data-stu-id="0cc98-171">You will also setup up some performance testing for hello Web app.</span></span>

1. <span data-ttu-id="0cc98-172">Kies App Services in het navigatiedeelvenster Hallo in hello Azure-Portal en zoek uw App Service.</span><span class="sxs-lookup"><span data-stu-id="0cc98-172">In hello Azure Portal choose App Services from hello navigation pane, and locate your App Service.</span></span>
   
   ![image16][image16]
2. <span data-ttu-id="0cc98-174">Klik op Hulpprogramma’s</span><span class="sxs-lookup"><span data-stu-id="0cc98-174">Click Tools</span></span>
   
   ![image17][image17]
3. <span data-ttu-id="0cc98-176">U ziet Hallo categorie onder Tools ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-176">Notice hello develop category under Tools.</span></span> <span data-ttu-id="0cc98-177">Er zijn enkele nuttige hulpmiddelen hier dat wij toowork met apps zonder hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="0cc98-177">There are several useful tools here that allow us toowork with apps without leaving hello Azure Portal.</span></span> <span data-ttu-id="0cc98-178">Klik op Console.</span><span class="sxs-lookup"><span data-stu-id="0cc98-178">Click on Console.</span></span>
   
   ![image18][image18]
4. <span data-ttu-id="0cc98-180">In het consolevenster hello, kunt u live opdrachten uitgeven voor uw app.</span><span class="sxs-lookup"><span data-stu-id="0cc98-180">In hello console window, you can issue live commands for your app.</span></span> <span data-ttu-id="0cc98-181">Typ Hallo dir opdracht en drukt op enter.</span><span class="sxs-lookup"><span data-stu-id="0cc98-181">Type hello dir command and hit enter.</span></span> <span data-ttu-id="0cc98-182">Opdrachten waarvoor verhoogde bevoegdheden zijn vereist, werken echter niet.</span><span class="sxs-lookup"><span data-stu-id="0cc98-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![image19][image19]
5. <span data-ttu-id="0cc98-184">Toohello ontwikkelen categorie terug en kies Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="0cc98-184">Move back toohello Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="0cc98-185">Opmerking: Visual Studio Online heet nu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="0cc98-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![image20][image20]
6. <span data-ttu-id="0cc98-187">In-of uitschakelen op Hallo in de browser bewerken ervaring voor uw App.</span><span class="sxs-lookup"><span data-stu-id="0cc98-187">Toggle on hello in-browser editing experience for your App.</span></span>
   
   ![image21][image21]
7. <span data-ttu-id="0cc98-189">Er wordt een webservice-extensie voor uw app geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0cc98-189">A web extension installs for your app.</span></span> <span data-ttu-id="0cc98-190">Snel en eenvoudig toevoegen extensies tooapps functionaliteit in Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc98-190">Extensions quickly and easily add functionality tooapps in Azure.</span></span> <span data-ttu-id="0cc98-191">U ziet enkele Hallo andere Uitbreidingstypen beschikbaar is in onderstaande schermafbeelding voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="0cc98-191">Notice some of hello other extension types available in hello screenshot below.</span></span>
   
   ![image22][image22]
8. <span data-ttu-id="0cc98-193">Zodra Hallo Visual Studio Online-extensie is geïnstalleerd, klikt u op Start.</span><span class="sxs-lookup"><span data-stu-id="0cc98-193">Once hello Visual Studio Online extension installs, click Go.</span></span>
   
   ![image23][image23]
9. <span data-ttu-id="0cc98-195">Een browser wordt geopend waarin u zien hoe een ontwikkeling IDE rechtstreeks in de browser Hallo tabblad.</span><span class="sxs-lookup"><span data-stu-id="0cc98-195">A browser tab opens where you see a development IDE directly in hello browser.</span></span> <span data-ttu-id="0cc98-196">Kennisgeving Hallo ervaring onderstaande wordt Chrome.</span><span class="sxs-lookup"><span data-stu-id="0cc98-196">Notice hello experience below is in Chrome.</span></span>
   
   ![image24][image24]
10. <span data-ttu-id="0cc98-198">U kunt uitvoeren van verschillende activiteiten zoals bewerken bestanden, bestanden en mappen toevoegen en downloaden inhoud vanaf Hallo live site.</span><span class="sxs-lookup"><span data-stu-id="0cc98-198">You can perform several activities such as edit files, add files and folders, and download content from hello live site.</span></span> <span data-ttu-id="0cc98-199">Een snelle bewerken toohello SamplePage.html-bestand maken.</span><span class="sxs-lookup"><span data-stu-id="0cc98-199">Make a quick edit toohello SamplePage.html file.</span></span>
    
    ![image25][image25]
11. <span data-ttu-id="0cc98-201">Hallo wijzigingen worden automatisch opgeslagen in een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="0cc98-201">In a few moments, hello changes are automatically saved.</span></span> <span data-ttu-id="0cc98-202">Als u back-toohello pagina navigeert, kunt u Hallo wijzigingen kan zien.</span><span class="sxs-lookup"><span data-stu-id="0cc98-202">If you navigate back toohello page, you can see hello changes.</span></span> <span data-ttu-id="0cc98-203">Let op: dit soort live bewerkingen is doorgaans niet geschikt voor productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="0cc98-204">Hallo-hulpprogramma's zijn echter maken het heel eenvoudig toomake snelle wijzigingen voor dev en testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0cc98-204">However, hello tools make it very easy toomake quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="0cc98-207">Toohello extra blade teruggaan en onder Hallo ontwikkelen categorie, klik op prestatietest.</span><span class="sxs-lookup"><span data-stu-id="0cc98-207">Move back toohello tools blade and under hello Develop category, click on Performance Test.</span></span>
    
    ![image28][image28]
13. <span data-ttu-id="0cc98-209">U moet tooset een team services-account.</span><span class="sxs-lookup"><span data-stu-id="0cc98-209">You need tooset a team services account.</span></span> <span data-ttu-id="0cc98-210">Zie [Een Team Services-account maken](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="0cc98-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="0cc98-211">Klik op nieuwe toocreate een prestatietest.</span><span class="sxs-lookup"><span data-stu-id="0cc98-211">Click on New toocreate a performance test.</span></span>
    
    ![image29][image29]
    
    <span data-ttu-id="0cc98-213">Configureer Hallo verschillende waarden en klik op Test uitvoeren Hallo Hallo dialoog tooinitiate een prestatietest onderaan in.</span><span class="sxs-lookup"><span data-stu-id="0cc98-213">Configure hello various values and click Run Test at hello bottom of hello dialogue tooinitiate a performance test.</span></span>
    
    ![image30][image30]
    
    ![image31][image31]
15. <span data-ttu-id="0cc98-216">Zodra Hallo test uitgevoerd start, kunt u Hallo status controleren.</span><span class="sxs-lookup"><span data-stu-id="0cc98-216">Once hello test starts running, you can monitor hello state.</span></span>
    
    ![image32][image32]
    
    <span data-ttu-id="0cc98-218">Zodra het Hallo-test is voltooid, bevat te klikken op Hallo resultaat meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0cc98-218">Once hello test finishes, clicking on hello result shows more details.</span></span>
    
    ![image33][image33]
16. <span data-ttu-id="0cc98-220">In dit voorbeeld moet u een korte test uitvoeren, zodat er beperkte gegevens tooanalyze, maar u kunt verschillende metrische gegevens te verzamelen, evenals uw test in deze weergave opnieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0cc98-220">In this example, you created a small test run, so there is limited data tooanalyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="0cc98-221">Hello Azure Portal kunt maken, uitvoeren en analyseren van webtests voor prestaties van een eenvoudig proces.</span><span class="sxs-lookup"><span data-stu-id="0cc98-221">hello Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="0cc98-222">Hallo onderstaande schermafbeeldingen Hallo-prestatiegegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0cc98-222">hello screenshots below display hello performance data.</span></span>
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="0cc98-226">Een app bewaken en problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="0cc98-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="0cc98-227">Azure biedt veel opties voor het bewaken van actieve toepassingen en het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="0cc98-228">Kies de hulpprogramma's in hello Azure-Portal voor de Web-app.</span><span class="sxs-lookup"><span data-stu-id="0cc98-228">In hello Azure Portal for our Web app choose Tools.</span></span>
   
   ![image37][image37]
2. <span data-ttu-id="0cc98-230">Let op Hallo van verschillende opties voor het gebruik van hulpprogramma's voor tootroubleshoot potentiële problemen met een actieve app onder Hallo oplossen categorie.</span><span class="sxs-lookup"><span data-stu-id="0cc98-230">Under hello Troubleshoot category, notice hello various choices for using tools tootroubleshoot potential issues with a running app.</span></span> <span data-ttu-id="0cc98-231">U kunt onder andere live HTTP-verkeer bewaken, zelfherstel inschakelen en logboeken weergeven.</span><span class="sxs-lookup"><span data-stu-id="0cc98-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![image38][image38]
3. <span data-ttu-id="0cc98-233">Kies Site metrische gegevens tooquickly get een weergave van bepaalde HTTP-codes.</span><span class="sxs-lookup"><span data-stu-id="0cc98-233">Choose Site Metrics tooquickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="0cc98-235">Kies Diagnostics as a Service.</span><span class="sxs-lookup"><span data-stu-id="0cc98-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="0cc98-236">Kies het toepassingstype en klik op Uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0cc98-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="0cc98-238">De gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="0cc98-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="0cc98-240">U kunt Hallo juiste logboek toodiagnose potentiële problemen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-240">You may choose hello appropriate log toodiagnose potential issues.</span></span> <span data-ttu-id="0cc98-241">U moet tooenable logboekregistratie toosee alle beschikbare gegevens Hallo opties zoals HTTP-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="0cc98-241">You need tooenable logging toosee all of hello available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="0cc98-243">Analyse rapport toohelp vinden door te klikken op Hallo geheugendumpbestand kunt u downloaden en analyseren van een DebugDiag potentiële problemen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-243">By clicking on hello Memory Dump file you can download and analyze a DebugDiag analysis report toohelp find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="0cc98-245">tooview meer gegevens, moet u aanvullende logboekregistratie tooenable.</span><span class="sxs-lookup"><span data-stu-id="0cc98-245">tooview more data, you need tooenable additional logging.</span></span> <span data-ttu-id="0cc98-246">In hello Azure Portal, gaat u toohello Web-app en kies instellingen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-246">In hello Azure Portal, navigate toohello Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="0cc98-248">Schuif naar beneden toohello functies categorie en kies diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="0cc98-248">Scroll down toohello features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="0cc98-250">Let op Hallo van verschillende opties voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="0cc98-250">Notice hello various options for logging.</span></span> <span data-ttu-id="0cc98-251">Schakel Webserverlogboeken in en klik op Opslaan.</span><span class="sxs-lookup"><span data-stu-id="0cc98-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="0cc98-253">Toohello extra gebied voor Hallo app teruggaan en diagnostische gegevens als een service en klik op uitvoeren toorerun Hallo gegevensverzameling.</span><span class="sxs-lookup"><span data-stu-id="0cc98-253">Move back toohello tools area for hello app and choose Diagnostics as a service and click Run toorerun hello data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="0cc98-255">Instelling van Hallo HTTP-logboekregistratie is ingeschakeld, ziet u nu gegevens verzameld voor HTTP-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="0cc98-255">With hello HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="0cc98-257">Door te klikken op Hallo HTML-logbestand, moet u een uitgebreid rapport op basis van een browser voor verder onderzoek produceren.</span><span class="sxs-lookup"><span data-stu-id="0cc98-257">By clicking hello HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="0cc98-259">Toohello extra sectie in hello Azure-Portal voor Hallo app gaan.</span><span class="sxs-lookup"><span data-stu-id="0cc98-259">Move back toohello tools section in hello Azure Portal for hello app.</span></span> <span data-ttu-id="0cc98-260">Schuif toohello extra sectie en kies Procesverkenner.</span><span class="sxs-lookup"><span data-stu-id="0cc98-260">Scroll toohello Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="0cc98-262">Kies Procesverkenner als u gegevens over actieve processen wilt bekijken.</span><span class="sxs-lookup"><span data-stu-id="0cc98-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="0cc98-263">U ziet u kunt inzoomen processen en zelfs kill processen via hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="0cc98-263">Notice below you can drill into processes and even kill processes all from hello Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="0cc98-266">De blade instellingen toohello op Hallo links terugwaartse.</span><span class="sxs-lookup"><span data-stu-id="0cc98-266">Move back toohello Settings blade on hello left.</span></span> <span data-ttu-id="0cc98-267">Klik op Nieuw ondersteuningsverzoek.</span><span class="sxs-lookup"><span data-stu-id="0cc98-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="0cc98-269">Hallo blade op Hallo rechts kunt u meer informatie over problemen Hallo invullen, contactgegevens invoeren en zelfs diagnostische gegevens uploaden.</span><span class="sxs-lookup"><span data-stu-id="0cc98-269">From hello blade on hello right, you can fill out details about hello issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="0cc98-270">Hello Azure Portal kunt werken met Microsoft ondersteuning naadloos.</span><span class="sxs-lookup"><span data-stu-id="0cc98-270">hello Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="0cc98-273">Hello Azure Portal biedt krachtige en bekend tooling ervaringen toohelp bewaken en problemen oplossen onze waarop toepassingen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0cc98-273">hello Azure Portal helps provide powerful and familiar tooling experiences toohelp monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="0cc98-274">Bent u ook kunnen tootake actie snel door taken uitvoeren zoals het recyclen van processen, inschakelen en uitschakelen van verschillende verzamelen van gegevens en zelfs integreren met Microsoft ondersteuning op professional.</span><span class="sxs-lookup"><span data-stu-id="0cc98-274">You are also able tootake action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="0cc98-275">Algemeen toepassingsbeheer</span><span class="sxs-lookup"><span data-stu-id="0cc98-275">General Application Management</span></span>
<span data-ttu-id="0cc98-276">Bij het beheren van toepassingen, moet u vaak tooperform tal van activiteiten, zoals back-strategieën configureren, implementeren en id-providers beheren en configureren van toegangsbeheer op basis van rollen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-276">When managing applications, you often need tooperform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="0cc98-277">Als hello met andere ervaringen DevOps, hello Azure-platform geïntegreerd met deze taken rechtstreeks Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="0cc98-277">As with hello other DevOps experiences, hello Azure platform integrates these tasks directly into hello portal.</span></span>

1. <span data-ttu-id="0cc98-278">tooensure die u bijhoudt Hallo Web-App tegen verlies van gegevens moet u tooconfigure back-ups.</span><span class="sxs-lookup"><span data-stu-id="0cc98-278">tooensure you are keeping hello Web App safe from data loss you need tooconfigure backups.</span></span> <span data-ttu-id="0cc98-279">Navigeer toohello gebied voor instellingen voor uw Web-app.</span><span class="sxs-lookup"><span data-stu-id="0cc98-279">Navigate toohello Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="0cc98-281">Hallo-blade op Hallo rechts, schuif naar beneden toohello functies categorie.</span><span class="sxs-lookup"><span data-stu-id="0cc98-281">In hello blade on hello right, scroll down toohello Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="0cc98-283">Kies de back-ups; Er wordt een blade geopend op de juiste Hallo.</span><span class="sxs-lookup"><span data-stu-id="0cc98-283">Choose Backups; a blade opens on hello right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="0cc98-285">Klik op configureren, kiest u een opslagaccount Hallo-blade op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="0cc98-285">Click Configure, choose a storage account from hello blade on hello right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="0cc98-287">Nu maakt en kies een container opslag toohold uw back-ups.</span><span class="sxs-lookup"><span data-stu-id="0cc98-287">Now create and choose a storage container toohold your backups.</span></span> <span data-ttu-id="0cc98-288">Klik op maken Hallo Hallo blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="0cc98-288">Click create at hello bottom of hello blade.</span></span> <span data-ttu-id="0cc98-289">Selecteer vervolgens Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="0cc98-289">Then select hello container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="0cc98-291">Zodra u Hallo container hebt gekozen, kunt u schema's, evenals de setup-back-ups kunt configureren voor uw databases.</span><span class="sxs-lookup"><span data-stu-id="0cc98-291">Once you have chosen hello container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="0cc98-292">Klik op Hallo opslaan pictogram voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="0cc98-292">For this scenario, click hello save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="0cc98-294">Schuif terug toohello blade aan de linkerkant Hallo voor back-ups nadat ze zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-294">After saving, scroll back toohello blade on hello left for Backups.</span></span> <span data-ttu-id="0cc98-295">Klik op Nu back-up tooback Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="0cc98-295">Click Backup Now tooback hello application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="0cc98-297">Binnen enkele tellen ziet u dat er een back-up wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0cc98-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="0cc98-298">Kennisgeving hello nu terugzetten optie op Hallo schermafbeelding hieronder.</span><span class="sxs-lookup"><span data-stu-id="0cc98-298">Notice hello Restore Now option on hello screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="0cc98-300">Klik op Nu terugzetten en Hallo opties toohello blade op Hallo rechts onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="0cc98-300">Click on Restore Now and examine hello options toohello blade on hello right.</span></span> <span data-ttu-id="0cc98-301">U kunt dat een geschikte back-up en eenvoudig terugzetten tooan eerder status zo nodig.</span><span class="sxs-lookup"><span data-stu-id="0cc98-301">You can choose an appropriate backup and easily restore tooan earlier state as necessary.</span></span> <span data-ttu-id="0cc98-302">Hello Azure-portal heeft geholpen ons gemakkelijk een eenvoudige strategie voor noodherstel van Hallo app inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-302">hello Azure portal has helped us easily enable a simple disaster recovery strategy for hello app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="0cc98-304">Verplaats terug toohello instellingenblade op Hallo links en -functies en -verificatie/autorisatie kiezen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-304">Move back toohello Settings blade on hello left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="0cc98-306">Hallo-blade op Hallo rechts App Service-verificatie te kiezen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-306">In hello blade on hello right choose App Service Authentication.</span></span> <span data-ttu-id="0cc98-307">U ziet Hallo verschillende opties die u met populaire providers configureren kunt.</span><span class="sxs-lookup"><span data-stu-id="0cc98-307">Notice hello variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="0cc98-309">Kies een Hallo-provider van uw keuze en Hallo opties voor Hallo scope zien.</span><span class="sxs-lookup"><span data-stu-id="0cc98-309">Choose hello provider of your choice and notice hello options for hello scope.</span></span> <span data-ttu-id="0cc98-310">U kunt een App-ID en de App geheim opgeeft en snel Facebook-verificatie inschakelen voor Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="0cc98-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for hello app.</span></span> <span data-ttu-id="0cc98-311">Hello Azure Portal kunt verificatie als klare oplossing voor apps.</span><span class="sxs-lookup"><span data-stu-id="0cc98-311">hello Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="0cc98-313">De blade instellingen toohello terug en kies gebruikers onder Hallo bronbeheer categorie.</span><span class="sxs-lookup"><span data-stu-id="0cc98-313">Move back toohello Settings blade and choose Users under hello Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="0cc98-315">Hallo-blade op Hallo rechts onderzoeken Hallo verschillende opties voor het toevoegen van rollen en gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0cc98-315">In hello blade on hello right examine hello various options for adding roles and users.</span></span> <span data-ttu-id="0cc98-316">Hello Azure Portal kunt u gemakkelijk RBAC (op rollen gebaseerde toegangsbeheer) voor de toepassing hello beheren.</span><span class="sxs-lookup"><span data-stu-id="0cc98-316">hello Azure Portal lets you easily control RBAC (Role-based access control) for hello application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="0cc98-318">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="0cc98-318">Summary</span></span>
<span data-ttu-id="0cc98-319">Deze zelfstudie gedemonstreerd aantal Hallo power Hello Azure-platform door snel inschakelen van continue implementatie voor een web-app, uitvoeren van verschillende ontwikkeling en testen van activiteiten, bewaking en het oplossen van een live-app en ten slotte het beheren van de sleutel strategieën zoals herstel na noodgevallen, identiteit en toegangsbeheer op basis van rollen.</span><span class="sxs-lookup"><span data-stu-id="0cc98-319">This tutorial demonstrated some of hello power with hello Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="0cc98-320">Hello Azure-platform kan een geïntegreerde ervaring voor deze DevOps-werkstromen en u kunt efficiënt werken door in de context voor Hallo uit te voeren taak bijwerkt.</span><span class="sxs-lookup"><span data-stu-id="0cc98-320">hello Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for hello task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cc98-321">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0cc98-321">Next steps</span></span>
* <span data-ttu-id="0cc98-322">Azure Resource Manager is het belangrijk is voor het inschakelen van DevOps op Hallo Azure-platform.</span><span class="sxs-lookup"><span data-stu-id="0cc98-322">Azure Resource Manager is important for enabling DevOps on hello Azure platform.</span></span>  <span data-ttu-id="0cc98-323">Ga meer toolearn naar [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cc98-323">toolearn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="0cc98-324">meer informatie over Azure App Service-implementatie gaat u naar toolearn [uw app tooAzure App Service implementeren](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="0cc98-324">toolearn more about Azure App Service deployment visit [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md)</span></span>

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
