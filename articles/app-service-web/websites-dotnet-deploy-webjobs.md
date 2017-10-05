---
title: WebJobs implementeren met Visual Studio
description: Informatie over het implementeren van Azure WebJobs voor Azure App Service Web Apps met Visual Studio.
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5b0808afdadcf4d86a9a2d07ee6fc63b80b22993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="29a90-103">WebJobs implementeren met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29a90-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="29a90-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="29a90-104">Overview</span></span>
<span data-ttu-id="29a90-105">Dit onderwerp wordt uitgelegd hoe u met Visual Studio een consoletoepassing-project implementeert in een WebApp in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) als een [Azure webtaak](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="29a90-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="29a90-106">Voor informatie over het implementeren van WebJobs met behulp van de [Azure Portal](https://portal.azure.com), Zie [achtergrondtaken uitvoeren met de WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="29a90-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="29a90-107">Visual Studio een consoletoepassing webtaken ingeschakeld-project implementeert, worden twee taken uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="29a90-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="29a90-108">Runtime-bestanden worden gekopieerd naar de juiste map in de web-app (*App_Data/taken/continue* voor doorlopende webtaken *App_Data/taken/geactiveerd* voor geplande en on-demand WebJobs).</span><span class="sxs-lookup"><span data-stu-id="29a90-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="29a90-109">Stelt [Azure Scheduler-taken](#scheduler) voor WebJobs die zijn gepland op bepaalde tijden.</span><span class="sxs-lookup"><span data-stu-id="29a90-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="29a90-110">(Dit is niet nodig voor doorlopende webtaken.)</span><span class="sxs-lookup"><span data-stu-id="29a90-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="29a90-111">Een project WebJobs ingeschakeld heeft de volgende items toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="29a90-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="29a90-112">De [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="29a90-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="29a90-113">Een [webtaak-publiceren settings.json](#publishsettings) -bestand met de implementatie en de scheduler-instellingen.</span><span class="sxs-lookup"><span data-stu-id="29a90-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagram van wat wordt toegevoegd aan een Console-App implementatie als een webtaak moet worden ingeschakeld](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="29a90-115">U kunt deze items toevoegen aan een bestaande Console-toepassing-project of gebruik een sjabloon te maken van een nieuw project voor de consoletoepassing WebJobs ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="29a90-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="29a90-116">U kunt een project implementeert als een webtaak zelfstandig of koppelen aan een webproject dat automatisch wordt geïmplementeerd wanneer u het webproject implementeren.</span><span class="sxs-lookup"><span data-stu-id="29a90-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="29a90-117">Als u wilt koppelen projecten, Visual Studio bevat de naam van het project WebJobs ingeschakeld in een [webjobs list.json](#webjobslist) bestand in het webproject.</span><span class="sxs-lookup"><span data-stu-id="29a90-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Diagram van webtaak project koppelen aan webproject](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="29a90-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="29a90-119">Prerequisites</span></span>
<span data-ttu-id="29a90-120">API-functies voor implementatie zijn beschikbaar in Visual Studio wanneer u de Azure SDK voor .NET installeert:</span><span class="sxs-lookup"><span data-stu-id="29a90-120">WebJobs deployment features are available in Visual Studio when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="29a90-121">[Azure SDK voor .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="29a90-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="29a90-122"><a id="convert"></a>WebJobs-implementatie voor een bestaande consoletoepassingsproject inschakelen</span><span class="sxs-lookup"><span data-stu-id="29a90-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="29a90-123">U hebt hiervoor twee opties:</span><span class="sxs-lookup"><span data-stu-id="29a90-123">You have two options:</span></span>

* <span data-ttu-id="29a90-124">[Schakel automatische implementatie met een webproject](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="29a90-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="29a90-125">Een bestaand project in de Console-toepassing zodanig configureren dat deze automatisch wordt geïmplementeerd als een webtaak wanneer u een webproject implementeert.</span><span class="sxs-lookup"><span data-stu-id="29a90-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="29a90-126">Gebruik deze optie als u wilt uw webtaak uitvoeren in dezelfde web-app waarin u de gerelateerde webtoepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="29a90-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="29a90-127">[Implementatie zonder een webproject inschakelen](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="29a90-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="29a90-128">Een bestaand project-consoletoepassing te implementeren als een webtaak zelfstandig gebruikt, met geen koppeling naar een webproject configureren.</span><span class="sxs-lookup"><span data-stu-id="29a90-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="29a90-129">Gebruik deze optie als u wilt uitvoeren in een web-app een webtaak zelfstandig gebruikt, met geen webtoepassing die wordt uitgevoerd in de web-app.</span><span class="sxs-lookup"><span data-stu-id="29a90-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="29a90-130">Het is raadzaam om dit te doen om te kunnen schalen van uw resources webtaak onafhankelijk van uw webtoepassingsbronnen.</span><span class="sxs-lookup"><span data-stu-id="29a90-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="29a90-131"><a id="convertlink"></a>Automatische WebJobs-implementatie met een webproject inschakelen</span><span class="sxs-lookup"><span data-stu-id="29a90-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="29a90-132">Met de rechtermuisknop op het webproject in **Solution Explorer**, en klik vervolgens op **toevoegen** > **bestaand Project als Azure webtaak**.</span><span class="sxs-lookup"><span data-stu-id="29a90-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Bestaand Project als Azure webtaak](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="29a90-134">De [toevoegen Azure webtaak](#configure) dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="29a90-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="29a90-135">In de **projectnaam** vervolgkeuzelijst, selecteer de consoletoepassing project wilt toevoegen als een webtaak.</span><span class="sxs-lookup"><span data-stu-id="29a90-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Project selecteren in het dialoogvenster Azure webtaak toevoegen](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="29a90-137">Voltooi de [toevoegen Azure webtaak](#configure) dialoogvenster en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="29a90-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="29a90-138"><a id="convertnolink"></a>WebJobs-implementatie zonder een webproject inschakelen</span><span class="sxs-lookup"><span data-stu-id="29a90-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="29a90-139">Met de rechtermuisknop op het project-consoletoepassing in **Solution Explorer**, en klik vervolgens op **publiceren als Azure webtaak...** .</span><span class="sxs-lookup"><span data-stu-id="29a90-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Als Azure webtaak publiceren](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="29a90-141">De [toevoegen Azure webtaak](#configure) dialoogvenster wordt weergegeven, met het project is geselecteerd de **projectnaam** vak.</span><span class="sxs-lookup"><span data-stu-id="29a90-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="29a90-142">Voltooi de [toevoegen Azure webtaak](#configure) in het dialoogvenster en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="29a90-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="29a90-143">De **webpublicatie** wizard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="29a90-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="29a90-144">Als u niet onmiddellijk publiceren wilt, moet u de wizard sluiten.</span><span class="sxs-lookup"><span data-stu-id="29a90-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="29a90-145">De instellingen die u hebt ingevoerd voor worden opgeslagen wanneer u wilt [het project implementeren](#deploy).</span><span class="sxs-lookup"><span data-stu-id="29a90-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <span data-ttu-id="29a90-146"><a id="create"></a>Maak een nieuw project voor WebJobs ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="29a90-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="29a90-147">Voor het maken van een nieuw project voor webtaken is ingeschakeld, kunt u de projectsjabloon consoletoepassing gebruiken en WebJobs implementatie inschakelen zoals toegelicht in [de vorige sectie](#convert).</span><span class="sxs-lookup"><span data-stu-id="29a90-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="29a90-148">Als alternatief kunt kunt u het WebJobs-nieuw project-sjabloon gebruiken:</span><span class="sxs-lookup"><span data-stu-id="29a90-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="29a90-149">Gebruik de sjabloon WebJobs-nieuw project voor een onafhankelijke webtaak</span><span class="sxs-lookup"><span data-stu-id="29a90-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="29a90-150">Een project maken en deze te implementeren door zichzelf als een webtaak, met geen koppeling naar een webproject configureren.</span><span class="sxs-lookup"><span data-stu-id="29a90-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="29a90-151">Gebruik deze optie als u wilt uitvoeren in een web-app een webtaak zelfstandig gebruikt, met geen webtoepassing die wordt uitgevoerd in de web-app.</span><span class="sxs-lookup"><span data-stu-id="29a90-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="29a90-152">Het is raadzaam om dit te doen om te kunnen schalen van uw resources webtaak onafhankelijk van uw webtoepassingsbronnen.</span><span class="sxs-lookup"><span data-stu-id="29a90-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="29a90-153">Gebruik de sjabloon WebJobs-nieuw project voor een webtaak wordt gekoppeld aan een webproject</span><span class="sxs-lookup"><span data-stu-id="29a90-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="29a90-154">Maak een project die is geconfigureerd voor automatisch als een webtaak implementeren wanneer een webproject in de oplossing is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="29a90-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="29a90-155">Gebruik deze optie als u wilt uw webtaak uitvoeren in dezelfde web-app waarin u de gerelateerde webtoepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="29a90-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="29a90-156">De sjabloon voor de API-nieuw project automatisch NuGet-pakketten worden geïnstalleerd en bevat een code in *Program.cs* voor de [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="29a90-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="29a90-157">Als u niet wilt dat de WebJobs SDK wilt gebruiken, verwijder of wijzig de `host.RunAndBlock` -instructie in *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="29a90-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="29a90-158"><a id="createnolink"></a>Gebruik de sjabloon WebJobs-nieuw project voor een onafhankelijke webtaak</span><span class="sxs-lookup"><span data-stu-id="29a90-158"><a id="createnolink"></a> Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="29a90-159">Klik op **bestand** > **nieuw Project**, en klik vervolgens in de **nieuw Project** dialoogvenster vak Klik **Cloud**  >   **Azure webtaak (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="29a90-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Het dialoogvenster New Project webtaak sjabloon weergeven](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="29a90-161">Volg de instructies die eerder naar weergegeven [de consoletoepassing project een onafhankelijk WebJobs-project maken](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="29a90-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="29a90-162"><a id="createlink"></a>Gebruik de sjabloon WebJobs-nieuw project voor een webtaak wordt gekoppeld aan een webproject</span><span class="sxs-lookup"><span data-stu-id="29a90-162"><a id="createlink"></a> Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="29a90-163">Met de rechtermuisknop op het webproject in **Solution Explorer**, en klik vervolgens op **toevoegen** > **nieuwe Azure webtaak Project**.</span><span class="sxs-lookup"><span data-stu-id="29a90-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Nieuwe Azure webtaak Project menu-item](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="29a90-165">De [toevoegen Azure webtaak](#configure) dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="29a90-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="29a90-166">Voltooi de [toevoegen Azure webtaak](#configure) in het dialoogvenster en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="29a90-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="29a90-167"><a id="configure"></a>Het dialoogvenster Azure webtaak toevoegen</span><span class="sxs-lookup"><span data-stu-id="29a90-167"><a id="configure"></a>The Add Azure WebJob dialog</span></span>
<span data-ttu-id="29a90-168">De **toevoegen Azure webtaak** dialoogvenster kunt u de naam van een webtaak en voert u de instelling voor uw webtaak uit.</span><span class="sxs-lookup"><span data-stu-id="29a90-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![Dialoogvenster Azure webtaak toevoegen](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="29a90-170">De velden in dit dialoogvenster overeenkomen met de velden op de **nieuwe taak** dialoogvenster van de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="29a90-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="29a90-171">Zie voor meer informatie [achtergrondtaken uitvoeren met de WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="29a90-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="29a90-172">Zie voor meer informatie over de implementatie van het opdrachtregelprogramma [inschakelen vanaf de opdrachtregel of continue levering van Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="29a90-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="29a90-173">Als u een webtaak implementeert en vervolgens besluit dat u wilt wijzigen van het type webtaak en opnieuw distribueren, moet u het webjobs-publiceren settings.json-bestand te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="29a90-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="29a90-174">Dit maakt Visual Studio weergeven de publicatieopties, zodat u het type webtaak kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="29a90-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="29a90-175">Als u een webtaak implementeert en de uitvoeringsmodus later van continue naar niet-doorlopende of omgekeerd wijzigen, maakt Visual Studio een nieuw webtaak in Azure, wanneer u opnieuw implementeert.</span><span class="sxs-lookup"><span data-stu-id="29a90-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="29a90-176">Als u andere schema-instellingen wijzigen, maar laat uitvoermodus dezelfde of schakelen tussen geplande en op verzoek, Visual Studio updates van de bestaande taak plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="29a90-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="29a90-177"><a id="publishsettings"></a>webtaak-publiceren settings.json</span><span class="sxs-lookup"><span data-stu-id="29a90-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="29a90-178">Wanneer u een consoletoepassing voor WebJobs-implementatie configureert, Visual Studio installeert de [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet-pakket en winkels planningsgegevens in een *webtaak-publiceren settings.json*  bestand in het project *eigenschappen* map van de API-project.</span><span class="sxs-lookup"><span data-stu-id="29a90-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="29a90-179">Hier volgt een voorbeeld van het bestand:</span><span class="sxs-lookup"><span data-stu-id="29a90-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="29a90-180">U kunt dit bestand rechtstreeks bewerken en Visual Studio biedt IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="29a90-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="29a90-181">Het schema van het bestand wordt opgeslagen op [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) en er kan worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="29a90-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="29a90-182"><a id="webjobslist"></a>webjobs list.json</span><span class="sxs-lookup"><span data-stu-id="29a90-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="29a90-183">Wanneer u een project WebJobs ingeschakeld aan een webproject koppelen, Visual Studio slaat de naam van de API-project in een *webjobs list.json* bestand in het webproject *eigenschappen* map.</span><span class="sxs-lookup"><span data-stu-id="29a90-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="29a90-184">De lijst kan meerdere WebJobs projecten bevatten, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="29a90-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

<span data-ttu-id="29a90-185">U kunt dit bestand rechtstreeks bewerken en Visual Studio biedt IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="29a90-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="29a90-186">Het schema van het bestand wordt opgeslagen op [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) en er kan worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="29a90-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="29a90-187"><a id="deploy"></a>Een API-project implementeert</span><span class="sxs-lookup"><span data-stu-id="29a90-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="29a90-188">Een API-project dat u hebt gekoppeld aan een webproject implementeert automatisch met het webproject.</span><span class="sxs-lookup"><span data-stu-id="29a90-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="29a90-189">Zie voor meer informatie over de implementatie van web project [implementeren op Web-Apps](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="29a90-189">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="29a90-190">Als u wilt een API-project implementeert zelfstandig, met de rechtermuisknop op het project in **Solution Explorer** en klik op **publiceren als Azure webtaak...** .</span><span class="sxs-lookup"><span data-stu-id="29a90-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Als Azure webtaak publiceren](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="29a90-192">Voor een onafhankelijke webtaak dezelfde **webpublicatie** wizard die wordt gebruikt voor webprojecten wordt weergegeven, maar met minder instellingen beschikbaar om te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="29a90-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <span data-ttu-id="29a90-193"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="29a90-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="29a90-194">In dit artikel is beschreven WebJobs implementeren met behulp van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29a90-194">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="29a90-195">Zie voor meer informatie over het implementeren van Azure WebJobs [Azure WebJobs - aanbevolen Resources - implementatie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="29a90-195">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

