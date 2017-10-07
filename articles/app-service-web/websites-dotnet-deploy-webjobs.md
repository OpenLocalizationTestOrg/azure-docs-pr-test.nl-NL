---
title: aaaDeploy WebJobs met Visual Studio
description: Meer informatie over hoe toodeploy Azure WebJobs tooAzure App Service Web Apps met Visual Studio.
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
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="6964d-103">WebJobs implementeren met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6964d-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="6964d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6964d-104">Overview</span></span>
<span data-ttu-id="6964d-105">Dit onderwerp wordt uitgelegd hoe toouse Visual Studio toodeploy een consoletoepassing tooa web-app in project [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) als een [Azure webtaak](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="6964d-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="6964d-106">Voor informatie over hoe toodeploy WebJobs met behulp van Hallo [Azure Portal](https://portal.azure.com), Zie [achtergrondtaken uitvoeren met de WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="6964d-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="6964d-107">Visual Studio een consoletoepassing webtaken ingeschakeld-project implementeert, worden twee taken uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="6964d-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="6964d-108">Kopieën runtime toohello geschikte map in Hallo web-app-bestanden (*App_Data/taken/continue* voor doorlopende webtaken *App_Data/taken/geactiveerd* voor geplande en on-demand WebJobs).</span><span class="sxs-lookup"><span data-stu-id="6964d-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="6964d-109">Stelt [Azure Scheduler-taken](#scheduler) voor WebJobs die geplande toorun op bepaalde tijden zijn.</span><span class="sxs-lookup"><span data-stu-id="6964d-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="6964d-110">(Dit is niet nodig voor doorlopende webtaken.)</span><span class="sxs-lookup"><span data-stu-id="6964d-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="6964d-111">Een project WebJobs ingeschakeld heeft Hallo items toegevoegde tooit te volgen:</span><span class="sxs-lookup"><span data-stu-id="6964d-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="6964d-112">Hallo [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="6964d-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="6964d-113">Een [webtaak-publiceren settings.json](#publishsettings) -bestand met de implementatie en de scheduler-instellingen.</span><span class="sxs-lookup"><span data-stu-id="6964d-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagram van wat tooa consoletoepassing tooenable implementatie als een webtaak is toegevoegd](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="6964d-115">U kunt deze items tooan bestaande consoletoepassingsproject toevoegen of gebruik een sjabloon toocreate een nieuw project voor de consoletoepassing WebJobs ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6964d-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="6964d-116">U kunt een project implementeert als een webtaak zelfstandig of een koppeling tooa webproject zodat deze automatisch wordt geïmplementeerd wanneer u Hallo-webproject implementeert.</span><span class="sxs-lookup"><span data-stu-id="6964d-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="6964d-117">toolink projecten, Visual Studio bevat Hallo-naam van Hallo webtaken ingeschakeld project in een [webjobs list.json](#webjobslist) bestand in het Hallo-webproject.</span><span class="sxs-lookup"><span data-stu-id="6964d-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![Diagram van webtaak project tooweb project koppelen](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="6964d-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6964d-119">Prerequisites</span></span>
<span data-ttu-id="6964d-120">API-functies voor implementatie zijn beschikbaar in Visual Studio wanneer u hello Azure SDK voor .NET installeert:</span><span class="sxs-lookup"><span data-stu-id="6964d-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="6964d-121">[Azure SDK voor .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6964d-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="6964d-122"><a id="convert"></a>WebJobs-implementatie voor een bestaande consoletoepassingsproject inschakelen</span><span class="sxs-lookup"><span data-stu-id="6964d-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="6964d-123">U hebt hiervoor twee opties:</span><span class="sxs-lookup"><span data-stu-id="6964d-123">You have two options:</span></span>

* <span data-ttu-id="6964d-124">[Schakel automatische implementatie met een webproject](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="6964d-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="6964d-125">Een bestaand project in de Console-toepassing zodanig configureren dat deze automatisch wordt geïmplementeerd als een webtaak wanneer u een webproject implementeert.</span><span class="sxs-lookup"><span data-stu-id="6964d-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="6964d-126">Gebruik deze optie als u wilt dat toorun uw webtaak in Hallo dezelfde web-app waarin u Hallo uitvoeren gerelateerde webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="6964d-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="6964d-127">[Implementatie zonder een webproject inschakelen](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="6964d-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="6964d-128">Configureer een bestaande Console Application project toodeploy als een webtaak zelfstandig gebruikt, met geen koppeling tooa webproject.</span><span class="sxs-lookup"><span data-stu-id="6964d-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="6964d-129">Gebruik deze optie als u toorun een webtaak in een web-app wilt zelfstandig gebruikt, met geen webtoepassing in Hallo web-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6964d-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="6964d-130">U kunt toodo dit in volgorde toobe kunnen tooscale uw resources webtaak onafhankelijk van uw webtoepassingsbronnen.</span><span class="sxs-lookup"><span data-stu-id="6964d-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="6964d-131"><a id="convertlink"></a>Automatische WebJobs-implementatie met een webproject inschakelen</span><span class="sxs-lookup"><span data-stu-id="6964d-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="6964d-132">Klik met de rechtermuisknop Hallo-webproject in **Solution Explorer**, en klik vervolgens op **toevoegen** > **bestaand Project als Azure webtaak**.</span><span class="sxs-lookup"><span data-stu-id="6964d-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Bestaand Project als Azure webtaak](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="6964d-134">Hallo [toevoegen Azure webtaak](#configure) dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6964d-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="6964d-135">In Hallo **projectnaam** vervolgkeuzelijst, selecteer Hallo consoletoepassing project tooadd als een webtaak.</span><span class="sxs-lookup"><span data-stu-id="6964d-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Project selecteren in het dialoogvenster Azure webtaak toevoegen](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="6964d-137">Volledige Hallo [toevoegen Azure webtaak](#configure) dialoogvenster en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6964d-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="6964d-138"><a id="convertnolink"></a>WebJobs-implementatie zonder een webproject inschakelen</span><span class="sxs-lookup"><span data-stu-id="6964d-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="6964d-139">Klik met de rechtermuisknop Hallo consoletoepassingsproject in **Solution Explorer**, en klik vervolgens op **publiceren als Azure webtaak...** .</span><span class="sxs-lookup"><span data-stu-id="6964d-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Als Azure webtaak publiceren](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="6964d-141">Hallo [toevoegen Azure webtaak](#configure) dialoogvenster wordt weergegeven, met Hallo project is geselecteerd in Hallo **projectnaam** vak.</span><span class="sxs-lookup"><span data-stu-id="6964d-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="6964d-142">Volledige Hallo [toevoegen Azure webtaak](#configure) in het dialoogvenster en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6964d-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="6964d-143">Hallo **webpublicatie** wizard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6964d-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="6964d-144">Als u toopublish niet onmiddellijk wilt, kunt u Hallo wizard sluiten.</span><span class="sxs-lookup"><span data-stu-id="6964d-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="6964d-145">Hallo-instellingen die u hebt ingevoerd voor worden opgeslagen wanneer u dat te wilt[Hallo-project implementeert](#deploy).</span><span class="sxs-lookup"><span data-stu-id="6964d-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="6964d-146"><a id="create"></a>Maak een nieuw project voor WebJobs ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="6964d-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="6964d-147">toocreate een nieuw project voor webtaken is ingeschakeld, kunt u Hallo Console project sjabloon en schakel webtaken toepassingsimplementatie zoals toegelicht in [Hallo van de vorige sectie](#convert).</span><span class="sxs-lookup"><span data-stu-id="6964d-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="6964d-148">Als alternatief kunt u Hallo webtaken nieuw project sjabloon:</span><span class="sxs-lookup"><span data-stu-id="6964d-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="6964d-149">Hallo webtaken nieuw project-sjabloon gebruiken voor een onafhankelijke webtaak</span><span class="sxs-lookup"><span data-stu-id="6964d-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="6964d-150">Een project maken en configureren toodeploy zelfstandig als een webtaak, met geen koppeling tooa webproject.</span><span class="sxs-lookup"><span data-stu-id="6964d-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="6964d-151">Gebruik deze optie als u toorun een webtaak in een web-app wilt zelfstandig gebruikt, met geen webtoepassing in Hallo web-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6964d-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="6964d-152">U kunt toodo dit in volgorde toobe kunnen tooscale uw resources webtaak onafhankelijk van uw webtoepassingsbronnen.</span><span class="sxs-lookup"><span data-stu-id="6964d-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="6964d-153">Hallo webtaken nieuw project-sjabloon gebruiken voor een webtaak gekoppelde tooa-webproject</span><span class="sxs-lookup"><span data-stu-id="6964d-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="6964d-154">Een project maken dat geconfigureerde toodeploy automatisch als een webtaak wanneer een webproject in Hallo dezelfde oplossing is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="6964d-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="6964d-155">Gebruik deze optie als u wilt dat toorun uw webtaak in Hallo dezelfde web-app waarin u Hallo uitvoeren gerelateerde webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="6964d-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="6964d-156">Hallo webtaken nieuw project sjabloon automatisch NuGet-pakketten worden geïnstalleerd en bevat een code in *Program.cs* voor Hallo [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="6964d-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="6964d-157">Als u niet toouse hello WebJobs SDK wilt, verwijderen of wijzigen van Hallo `host.RunAndBlock` -instructie in *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="6964d-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="6964d-158"><a id="createnolink"></a>Hallo webtaken nieuw project-sjabloon gebruiken voor een onafhankelijke webtaak</span><span class="sxs-lookup"><span data-stu-id="6964d-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="6964d-159">Klik op **bestand** > **nieuw Project**, en klik vervolgens in Hallo **nieuw Project** dialoogvenster vak Klik **Cloud**  >   **Azure webtaak (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="6964d-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Het dialoogvenster New Project webtaak sjabloon weergeven](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="6964d-161">Volg Hallo-instructies hierboven te[Hallo consoletoepassingsproject een onafhankelijk WebJobs-project maken](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="6964d-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="6964d-162"><a id="createlink"></a>Hallo webtaken nieuw project-sjabloon gebruiken voor een webtaak gekoppelde tooa-webproject</span><span class="sxs-lookup"><span data-stu-id="6964d-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="6964d-163">Klik met de rechtermuisknop Hallo-webproject in **Solution Explorer**, en klik vervolgens op **toevoegen** > **nieuwe Azure webtaak Project**.</span><span class="sxs-lookup"><span data-stu-id="6964d-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Nieuwe Azure webtaak Project menu-item](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="6964d-165">Hallo [toevoegen Azure webtaak](#configure) dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6964d-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="6964d-166">Volledige Hallo [toevoegen Azure webtaak](#configure) in het dialoogvenster en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6964d-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="6964d-167"><a id="configure"></a>dialoogvenster voor Hello Azure webtaak toevoegen</span><span class="sxs-lookup"><span data-stu-id="6964d-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="6964d-168">Hallo **toevoegen Azure webtaak** dialoogvenster kunt u de naam van een webtaak Hallo en voert u de instelling voor uw webtaak uit.</span><span class="sxs-lookup"><span data-stu-id="6964d-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![Dialoogvenster Azure webtaak toevoegen](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="6964d-170">Hallo-velden in dit dialoogvenster komen overeen toofields op Hallo **nieuwe taak** dialoogvenster Hallo Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="6964d-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="6964d-171">Zie voor meer informatie [achtergrondtaken uitvoeren met de WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="6964d-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="6964d-172">Zie voor meer informatie over de implementatie van het opdrachtregelprogramma [inschakelen vanaf de opdrachtregel of continue levering van Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="6964d-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="6964d-173">Als u een webtaak implementeert en vervolgens besluit gewenste toochange Hallo type webtaak en opnieuw distribueren, moet u toodelete hello webjobs-publiceren settings.json bestand.</span><span class="sxs-lookup"><span data-stu-id="6964d-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="6964d-174">Hiermee maakt u Visual Studio weergeven Hallo publicatieopties opnieuw, zodat u Hallo type webtaak kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6964d-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="6964d-175">Als u een webtaak implementeert en later wijzigen Hallo uitvoeringsmodus van continue toonon continue of omgekeerd, Visual Studio maakt een nieuwe webtaak in Azure wanneer u opnieuw implementeert.</span><span class="sxs-lookup"><span data-stu-id="6964d-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="6964d-176">Als u andere schema-instellingen wijzigen, maar laat uitvoeren modus Hallo dezelfde of schakelen tussen geplande en op verzoek, Visual Studio-updates Hallo bestaande taak plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="6964d-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="6964d-177"><a id="publishsettings"></a>webtaak-publiceren settings.json</span><span class="sxs-lookup"><span data-stu-id="6964d-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="6964d-178">Wanneer u een consoletoepassing voor WebJobs-implementatie configureert, Visual Studio Hallo installeert [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet-pakket en winkels planningsgegevens in een *webtaak-publiceren settings.json*  bestand in Hallo project *eigenschappen* map van Hallo WebJobs project.</span><span class="sxs-lookup"><span data-stu-id="6964d-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="6964d-179">Hier volgt een voorbeeld van het bestand:</span><span class="sxs-lookup"><span data-stu-id="6964d-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="6964d-180">U kunt dit bestand rechtstreeks bewerken en Visual Studio biedt IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="6964d-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="6964d-181">Hallo bestand schema wordt opgeslagen op [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) en er kan worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6964d-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="6964d-182"><a id="webjobslist"></a>webjobs list.json</span><span class="sxs-lookup"><span data-stu-id="6964d-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="6964d-183">Als u een project WebJobs ingeschakeld tooa-webproject koppelt, Visual Studio slaat Hallo-naam van Hallo WebJobs-project in een *webjobs list.json* bestand in het Hallo-webproject *eigenschappen* map.</span><span class="sxs-lookup"><span data-stu-id="6964d-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="6964d-184">Hallo lijst kan meerdere WebJobs projecten bevatten, zoals wordt weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="6964d-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

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

<span data-ttu-id="6964d-185">U kunt dit bestand rechtstreeks bewerken en Visual Studio biedt IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="6964d-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="6964d-186">Hallo bestand schema wordt opgeslagen op [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) en er kan worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6964d-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="6964d-187"><a id="deploy"></a>Een API-project implementeert</span><span class="sxs-lookup"><span data-stu-id="6964d-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="6964d-188">Een API-project dat u hebt gekoppeld aan tooa-webproject implementeert automatisch met het Hallo-webproject.</span><span class="sxs-lookup"><span data-stu-id="6964d-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="6964d-189">Zie voor meer informatie over de implementatie van web project [hoe toodeploy tooWeb Apps](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6964d-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="6964d-190">toodeploy een API-project zelfstandig gebruikt, met de rechtermuisknop op Hallo-project in **Solution Explorer** en klik op **publiceren als Azure webtaak...** .</span><span class="sxs-lookup"><span data-stu-id="6964d-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Als Azure webtaak publiceren](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="6964d-192">Voor een onafhankelijke webtaak Hallo dezelfde **webpublicatie** wizard die wordt gebruikt voor webprojecten wordt weergegeven, maar met minder instellingen beschikbaar toochange.</span><span class="sxs-lookup"><span data-stu-id="6964d-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="6964d-193"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6964d-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="6964d-194">In dit artikel is beschreven hoe toodeploy WebJobs met behulp van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6964d-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="6964d-195">Voor meer informatie over hoe toodeploy Azure WebJobs zien [Azure WebJobs - aanbevolen Resources - implementatie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="6964d-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

