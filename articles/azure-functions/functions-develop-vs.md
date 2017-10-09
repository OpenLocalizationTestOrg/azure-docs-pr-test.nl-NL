---
title: aaaDevelop Azure Functions met Visual Studio | Microsoft Docs
description: Meer informatie over hoe Azure-functies voor toodevelop en testen met behulp van Azure Functions-hulpprogramma's voor Visual Studio 2017.
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="fcc9a-103">Azure Functions-Tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fcc9a-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="fcc9a-104">Azure Functions-hulpprogramma's voor Visual Studio 2017 is een uitbreiding voor Visual Studio waarmee u ontwikkelen, testen en implementeren van tooAzure van C#-functies.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions tooAzure.</span></span> <span data-ttu-id="fcc9a-105">Als dit de eerste ervaring met Azure Functions, kunt u meer informatie op [fungeert voor een inleiding tooAzure](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-105">If this is your first experience with Azure Functions, you can learn more at [An introduction tooAzure Functions](functions-overview.md).</span></span>

<span data-ttu-id="fcc9a-106">Hallo hulpprogramma's van Azure Functions biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fcc9a-106">hello Azure Functions Tools provides hello following benefits:</span></span> 

* <span data-ttu-id="fcc9a-107">Bewerken, bouwen en uitvoeren van functies op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="fcc9a-108">Publiceren van uw Azure Functions project rechtstreeks tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-108">Publish your Azure Functions project directly tooAzure.</span></span> 
* <span data-ttu-id="fcc9a-109">Gebruik WebJobs kenmerken toodeclare functiebindingen rechtstreeks in Hallo C#-code in plaats van het onderhouden van een afzonderlijke function.json voor het binden van definities.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-109">Use WebJobs attributes toodeclare function bindings directly in hello C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="fcc9a-110">Ontwikkelen en implementeren van vooraf gecompileerde C#-functies.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="fcc9a-111">Vooraf gecompileerde functies bieden een betere koude start prestaties dan C# script gebaseerde functies.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="fcc9a-112">Terwijl alle Hallo voordelen van Visual Studio-ontwikkeling van uw functies in C#-code.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-112">Code your functions in C# while having all of hello benefits of Visual Studio development.</span></span> 

<span data-ttu-id="fcc9a-113">Dit onderwerp leest u hoe toouse hello Azure Functions-Tools voor Visual Studio 2017 toodevelop uw functies in C#.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-113">This topic shows you how toouse hello Azure Functions Tools for Visual Studio 2017 toodevelop your functions in C#.</span></span> <span data-ttu-id="fcc9a-114">U leert ook hoe toopublish uw project tooAzure als een .NET-assembly.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-114">You also learn how toopublish your project tooAzure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcc9a-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fcc9a-115">Prerequisites</span></span>

<span data-ttu-id="fcc9a-116">Azure Functions-hulpprogramma's is opgenomen in hello Azure ontwikkeling werkbelasting van [Visual Studio 2017 versie 15,3](https://www.visualstudio.com/vs/), of een latere versie.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-116">Azure Functions Tools is included in hello Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="fcc9a-117">Zorg ervoor dat u Hallo **ontwikkelen van Azure** werkbelasting in uw Visual Studio 2017 versie 15,3 installatie:</span><span class="sxs-lookup"><span data-stu-id="fcc9a-117">Make sure you include hello **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Installeer Visual Studio 2017 met hello Azure ontwikkeling werkbelasting](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="fcc9a-119">toocreate en implementeren van functies, moet u ook:</span><span class="sxs-lookup"><span data-stu-id="fcc9a-119">toocreate and deploy functions, you also need:</span></span>

* <span data-ttu-id="fcc9a-120">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-120">An active Azure subscription.</span></span> <span data-ttu-id="fcc9a-121">Als u een Azure-abonnement geen [gratis accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="fcc9a-122">Een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-122">An Azure Storage account.</span></span> <span data-ttu-id="fcc9a-123">een opslagaccount toocreate Zie [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-123">toocreate a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="fcc9a-124">Een Azure Functions-project maken</span><span class="sxs-lookup"><span data-stu-id="fcc9a-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a><span data-ttu-id="fcc9a-125">Hallo-project voor lokale ontwikkeling configureren</span><span class="sxs-lookup"><span data-stu-id="fcc9a-125">Configure hello project for local development</span></span>

<span data-ttu-id="fcc9a-126">Wanneer u een nieuw project met hello Azure Functions-sjabloon maakt, kunt u een leeg C#-project met de volgende bestanden Hallo krijgen:</span><span class="sxs-lookup"><span data-stu-id="fcc9a-126">When you create a new project using hello Azure Functions template, you get an empty C# project that contains hello following files:</span></span>

* <span data-ttu-id="fcc9a-127">**host.JSON**: Hiermee kunt u configureren Hallo functies host.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-127">**host.json**: Lets you configure hello Functions host.</span></span> <span data-ttu-id="fcc9a-128">Deze instellingen gelden beide wanneer lokaal en in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="fcc9a-129">Zie voor meer informatie [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) artikel.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="fcc9a-130">**Local.Settings.JSON**: onderhoudt instellingen bij lokale uitvoering van de functies die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="fcc9a-131">Deze instellingen worden niet gebruikt door Azure, ze worden gebruikt door Hallo [kernonderdelen van Azure Functions](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-131">These settings are not used by Azure, they are used by hello [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="fcc9a-132">Gebruik deze instellingen toospecify, zoals verbinding tekenreeksen tooother Azure services.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-132">Use this file toospecify settings, such as connection strings tooother Azure services.</span></span> <span data-ttu-id="fcc9a-133">Voeg een nieuwe sleutel toohello **waarden** matrix voor elke verbinding vereist voor functies in uw project.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-133">Add a new key toohello **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="fcc9a-134">Zie voor meer informatie [lokale instellingenbestand](functions-run-local.md#local-settings-file) in Hallo kernonderdelen van Azure Functions onderwerp.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in hello Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="fcc9a-135">Hallo functies runtime wordt intern gebruikt een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-135">hello Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="fcc9a-136">Voor alle typen dan HTTP en webhooks activeert, moet u instellen Hallo **Values.AzureWebJobsStorage** sleutel tooa geldige Azure Storage-account-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-136">For all trigger types other than HTTP and webhooks, you must set hello **Values.AzureWebJobsStorage** key tooa valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="fcc9a-137">tooset hello account opslagverbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="fcc9a-137">tooset hello storage account connection string:</span></span>

1. <span data-ttu-id="fcc9a-138">Open in Visual Studio **Cloud Explorer**, vouw **Opslagaccount** > **uw Opslagaccount**, selecteer daarna **eigenschappen**en kopiëren Hallo **primaire verbindingsreeks** waarde.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy hello **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="fcc9a-139">In uw project Hallo local.settings.json projectbestand openen en stel de waarde Hallo Hallo **AzureWebJobsStorage** sleutel toohello-verbindingsreeks die u hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-139">In your project, open hello local.settings.json project file and set hello value of hello **AzureWebJobsStorage** key toohello connection string you copied.</span></span>

3. <span data-ttu-id="fcc9a-140">Herhaal Hallo vorige stap tooadd unieke sleutels toohello **waarden** matrix voor eventuele andere verbindingen die vereist zijn voor uw functies.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-140">Repeat hello previous step tooadd unique keys toohello **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="fcc9a-141">Een functie maken</span><span class="sxs-lookup"><span data-stu-id="fcc9a-141">Create a function</span></span>

<span data-ttu-id="fcc9a-142">Hallo bindingen die wordt gebruikt door de functie Hallo worden in de vooraf gecompileerde functies gedefinieerd door de kenmerken in het Hallo-code toepassen.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-142">In pre-compiled functions, hello bindings used by hello function are defined by applying attributes in hello code.</span></span> <span data-ttu-id="fcc9a-143">Wanneer u uw functies van Hallo opgegeven sjablonen hello Azure Functions Tools toocreate opgeeft, wordt deze kenmerken worden toegepast voor u.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-143">When you use hello Azure Functions Tools toocreate your functions from hello provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="fcc9a-144">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer  > **Nieuw item****Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="fcc9a-145">Selecteer **Azure-functie**, typ een **naam** voor Hallo klasse en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-145">Select **Azure Function**, type a **Name** for hello class, and click **Add**.</span></span>

2. <span data-ttu-id="fcc9a-146">Kies de trigger en klikt u op Hallo bindingeigenschappen instellen **maken**.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-146">Choose your trigger, set hello binding properties, and click **Create**.</span></span> <span data-ttu-id="fcc9a-147">Hallo volgende voorbeeld ziet Hallo instellingen wanneer de functie voor het maken van een Queue storage geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-147">hello following example shows hello settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="fcc9a-148">Een sleutelreeks voor verbinding met de naam **QueueStorage** wordt geleverd, die is gedefinieerd in Hallo local.settings.json bestand.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-148">A connection string key named **QueueStorage** is supplied, which is defined in hello local.settings.json file.</span></span> 
 
3. <span data-ttu-id="fcc9a-149">Bekijk Hallo toegevoegde klasse.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-149">Examine hello newly added class.</span></span> <span data-ttu-id="fcc9a-150">U ziet een statische **uitvoeren** methode, dat is toegewezen met Hallo **functienaam** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-150">You see a static **Run** method, that is attributed with hello **FunctionName** attribute.</span></span> <span data-ttu-id="fcc9a-151">Dit kenmerk geeft aan dat Hallo methode Hallo toegangspunt voor Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-151">This attribute indicates that hello method is hello entry point for hello function.</span></span> 

    <span data-ttu-id="fcc9a-152">Hallo volgende C#-klasse vertegenwoordigt bijvoorbeeld een eenvoudige wachtrij geactiveerd opslagfunctie:</span><span class="sxs-lookup"><span data-stu-id="fcc9a-152">For example, hello following C# class represents a basic Queue storage triggered function:</span></span>

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    <span data-ttu-id="fcc9a-153">Een binding-specifieke kenmerk is toegepaste tooeach binding geleverde parameter toohello entry point-methode.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-153">A binding-specific attribute is applied tooeach binding parameter supplied toohello entry point method.</span></span> <span data-ttu-id="fcc9a-154">Hallo-kenmerk heeft Hallo bindingsgegevens als parameters.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-154">hello attribute takes hello binding information as parameters.</span></span> <span data-ttu-id="fcc9a-155">In het vorige voorbeeld Hallo Hallo eerste parameter heeft een **QueueTrigger** kenmerk dat wordt toegepast, die wachtrij geactiveerd functie aangeeft.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-155">In hello previous example, hello first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="fcc9a-156">Hallo wachtrijnaam en de naam van instelling verbindingsreeks worden als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-156">hello queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="fcc9a-157">Functies testen</span><span class="sxs-lookup"><span data-stu-id="fcc9a-157">Testing functions</span></span>

<span data-ttu-id="fcc9a-158">Met Azure Functions Core-hulpprogramma's kunt u Azure Functions-projecten uitvoeren op uw lokale ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="fcc9a-159">U bent na vragen aan gebruiker tooinstall deze hulpprogramma's Hallo eerste keer dat u een functie vanuit Visual Studio start.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-159">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="fcc9a-160">tootest uw functie druk op F5.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-160">tootest your function, press F5.</span></span> <span data-ttu-id="fcc9a-161">Als u wordt gevraagd, Hallo verzoek van Visual Studio toodownload accepteert en hulpprogramma's voor Azure Functions Core (CLI) installeren.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-161">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="fcc9a-162">U moet mogelijk ook een firewall-uitzondering tooenable zodat Hallo hulpprogramma's voor HTTP-aanvragen kunnen verwerken.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-162">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

<span data-ttu-id="fcc9a-163">Hallo-project is uitgevoerd, kunt u uw code testen zoals u zou geïmplementeerde functie testen.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-163">With hello project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="fcc9a-164">Zie voor meer informatie [strategieën voor het testen van uw code in Azure Functions](functions-test-a-function.md).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="fcc9a-165">Wanneer in de foutopsporingsmodus wordt uitgevoerd, worden de onderbrekingspunten druk in Visual Studio zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="fcc9a-166">Zie voor een voorbeeld van hoe een wachtrij tootest functie geactiveerd, Hallo [wachtrij geactiveerd functie Quick Start-zelfstudie](functions-create-storage-queue-triggered-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-166">For an example of how tootest a queue triggered function, see hello [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="fcc9a-167">toolearn meer over het gebruik van de kernonderdelen van hello Azure Functions, Zie [Code en testen van Azure functions lokaal](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-167">toolearn more about using hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-tooazure"></a><span data-ttu-id="fcc9a-168">TooAzure publiceren</span><span class="sxs-lookup"><span data-stu-id="fcc9a-168">Publish tooAzure</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="fcc9a-169">Alle instellingen die u hebt toegevoegd in Hallo local.settings.json moeten ook toevoegen toohello functie-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-169">Any settings you added in hello local.settings.json must be also added toohello function app in Azure.</span></span> <span data-ttu-id="fcc9a-170">Deze instellingen worden niet automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-170">These settings are not added automatically.</span></span> <span data-ttu-id="fcc9a-171">U kunt de vereiste instellingen tooyour functie-app in een van de volgende manieren toevoegen:</span><span class="sxs-lookup"><span data-stu-id="fcc9a-171">You can add required settings tooyour function app in one of these ways:</span></span>
>
>* <span data-ttu-id="fcc9a-172">[Azure-portal met behulp van Hallo](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-172">[Using hello Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="fcc9a-173">[Met behulp van Hallo `--publish-local-settings` optie publiceren in Hallo kernonderdelen van Azure Functions](functions-run-local.md#publish).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-173">[Using hello `--publish-local-settings` publish option in hello Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="fcc9a-174">[Met behulp van Azure CLI Hallo](/cli/azure/functionapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-174">[Using hello Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fcc9a-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fcc9a-175">Next steps</span></span>

<span data-ttu-id="fcc9a-176">Zie voor meer informatie over hulpprogramma's van Azure-functies, de sectie Algemene vragen Hallo Hallo [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blogbericht.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-176">For more information about Azure Functions Tools, see hello Common Questions section of hello [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="fcc9a-177">toolearn meer informatie over de kernonderdelen van hello Azure Functions, Zie [Code en testen van Azure functions lokaal](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-177">toolearn more about hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="fcc9a-178">toolearn meer informatie over het ontwikkelen van functies als .NET-klassebibliotheken, Zie [met behulp van .NET-klassebibliotheken met Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="fcc9a-178">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="fcc9a-179">Dit onderwerp bevat ook voorbeelden van hoe toouse kenmerken toodeclare Hallo voor verschillende soorten bindingen die worden ondersteund door Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="fcc9a-179">This topic also provides examples of how toouse attributes toodeclare hello various types of bindings supported by Azure Functions.</span></span>    
