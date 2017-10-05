---
title: Azure Functions met Visual Studio ontwikkelen | Microsoft Docs
description: Informatie over het ontwikkelen en testen van Azure Functions met behulp van Azure Functions-hulpprogramma's voor Visual Studio 2017.
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
ms.openlocfilehash: 1e0568bc58e8879cabe409cf8e9b5866f922e7c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="eeb89-103">Azure Functions-Tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eeb89-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="eeb89-104">Azure Functions-hulpprogramma's voor Visual Studio 2017 is een uitbreiding voor Visual Studio waarmee u ontwikkelen, testen en implementeren van C#-functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="eeb89-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions to Azure.</span></span> <span data-ttu-id="eeb89-105">Als dit de eerste ervaring met Azure Functions, kunt u meer informatie op [een inleiding tot Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eeb89-105">If this is your first experience with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview.md).</span></span>

<span data-ttu-id="eeb89-106">De hulpprogramma's van Azure Functions biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="eeb89-106">The Azure Functions Tools provides the following benefits:</span></span> 

* <span data-ttu-id="eeb89-107">Bewerken, bouwen en uitvoeren van functies op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="eeb89-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="eeb89-108">Uw project Azure Functions rechtstreeks publiceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="eeb89-108">Publish your Azure Functions project directly to Azure.</span></span> 
* <span data-ttu-id="eeb89-109">WebJobs kenmerken gebruiken om te declareren functiebindingen rechtstreeks in de C#-code in plaats van het onderhouden van een afzonderlijke function.json voor het binden van definities.</span><span class="sxs-lookup"><span data-stu-id="eeb89-109">Use WebJobs attributes to declare function bindings directly in the C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="eeb89-110">Ontwikkelen en implementeren van vooraf gecompileerde C#-functies.</span><span class="sxs-lookup"><span data-stu-id="eeb89-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="eeb89-111">Vooraf gecompileerde functies bieden een betere koude start prestaties dan C# script gebaseerde functies.</span><span class="sxs-lookup"><span data-stu-id="eeb89-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="eeb89-112">Uw functies in C#-code terwijl alle voordelen van Visual Studio-ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="eeb89-112">Code your functions in C# while having all of the benefits of Visual Studio development.</span></span> 

<span data-ttu-id="eeb89-113">Dit onderwerp leest u hoe de Azure Functions-Tools voor Visual Studio 2017 gebruiken voor het ontwikkelen van uw functies in C#.</span><span class="sxs-lookup"><span data-stu-id="eeb89-113">This topic shows you how to use the Azure Functions Tools for Visual Studio 2017 to develop your functions in C#.</span></span> <span data-ttu-id="eeb89-114">U leert ook hoe uw project publiceren naar Azure als een .NET-assembly.</span><span class="sxs-lookup"><span data-stu-id="eeb89-114">You also learn how to publish your project to Azure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eeb89-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="eeb89-115">Prerequisites</span></span>

<span data-ttu-id="eeb89-116">Azure Functions-hulpprogramma's is opgenomen in de werklast Azure ontwikkeling van [Visual Studio 2017 versie 15,3](https://www.visualstudio.com/vs/), of een latere versie.</span><span class="sxs-lookup"><span data-stu-id="eeb89-116">Azure Functions Tools is included in the Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="eeb89-117">Zorg ervoor dat u de **ontwikkelen van Azure** werkbelasting in uw Visual Studio 2017 versie 15,3 installatie:</span><span class="sxs-lookup"><span data-stu-id="eeb89-117">Make sure you include the **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Visual Studio 2017 installeren met de Azure-ontwikkelworkload](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="eeb89-119">Als u wilt maken en implementeren van functies, moet u ook:</span><span class="sxs-lookup"><span data-stu-id="eeb89-119">To create and deploy functions, you also need:</span></span>

* <span data-ttu-id="eeb89-120">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="eeb89-120">An active Azure subscription.</span></span> <span data-ttu-id="eeb89-121">Als u een Azure-abonnement geen [gratis accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="eeb89-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="eeb89-122">Een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="eeb89-122">An Azure Storage account.</span></span> <span data-ttu-id="eeb89-123">Zie het maken van een opslagaccount [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="eeb89-123">To create a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="eeb89-124">Een Azure Functions-project maken</span><span class="sxs-lookup"><span data-stu-id="eeb89-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using the Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-the-project-for-local-development"></a><span data-ttu-id="eeb89-125">Het project voor lokale ontwikkeling configureren</span><span class="sxs-lookup"><span data-stu-id="eeb89-125">Configure the project for local development</span></span>

<span data-ttu-id="eeb89-126">Als u een nieuw project met de Azure Functions-sjabloon maakt, krijgt u een leeg C#-project met de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="eeb89-126">When you create a new project using the Azure Functions template, you get an empty C# project that contains the following files:</span></span>

* <span data-ttu-id="eeb89-127">**host.JSON**: Hiermee kunt u de functies host configureren.</span><span class="sxs-lookup"><span data-stu-id="eeb89-127">**host.json**: Lets you configure the Functions host.</span></span> <span data-ttu-id="eeb89-128">Deze instellingen gelden beide wanneer lokaal en in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="eeb89-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="eeb89-129">Zie voor meer informatie [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) artikel.</span><span class="sxs-lookup"><span data-stu-id="eeb89-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="eeb89-130">**Local.Settings.JSON**: onderhoudt instellingen bij lokale uitvoering van de functies die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="eeb89-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="eeb89-131">Deze instellingen worden niet gebruikt door Azure, ze worden gebruikt door de [kernonderdelen van Azure Functions](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="eeb89-131">These settings are not used by Azure, they are used by the [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="eeb89-132">Dit bestand opgeven van instellingen, zoals de verbindingsreeksen om andere Azure-services te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eeb89-132">Use this file to specify settings, such as connection strings to other Azure services.</span></span> <span data-ttu-id="eeb89-133">Een nieuwe sleutel toevoegen aan de **waarden** matrix voor elke verbinding vereist voor functies in uw project.</span><span class="sxs-lookup"><span data-stu-id="eeb89-133">Add a new key to the **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="eeb89-134">Zie voor meer informatie [lokale instellingenbestand](functions-run-local.md#local-settings-file) in het onderwerp kernonderdelen van Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="eeb89-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in the Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="eeb89-135">De runtime van Functions wordt intern gebruikt een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="eeb89-135">The Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="eeb89-136">Voor alle typen dan HTTP en webhooks activeert, moet u instellen de **Values.AzureWebJobsStorage** sleutel op een geldige verbindingsreeks voor Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="eeb89-136">For all trigger types other than HTTP and webhooks, you must set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="eeb89-137">De verbindingsreeks voor opslag account instellen:</span><span class="sxs-lookup"><span data-stu-id="eeb89-137">To set the storage account connection string:</span></span>

1. <span data-ttu-id="eeb89-138">Open in Visual Studio **Cloud Explorer**, vouw **Opslagaccount** > **uw Opslagaccount**, selecteer daarna **eigenschappen**en kopieer de **primaire verbindingsreeks** waarde.</span><span class="sxs-lookup"><span data-stu-id="eeb89-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy the **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="eeb89-139">Open het projectbestand local.settings.json in uw project en stel de waarde van de **AzureWebJobsStorage** sleutel op de verbindingsreeks die u hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="eeb89-139">In your project, open the local.settings.json project file and set the value of the **AzureWebJobsStorage** key to the connection string you copied.</span></span>

3. <span data-ttu-id="eeb89-140">Herhaal de vorige stap om toe te voegen unieke sleutels zijn aan de **waarden** matrix voor eventuele andere verbindingen die vereist zijn voor uw functies.</span><span class="sxs-lookup"><span data-stu-id="eeb89-140">Repeat the previous step to add unique keys to the **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="eeb89-141">Een functie maken</span><span class="sxs-lookup"><span data-stu-id="eeb89-141">Create a function</span></span>

<span data-ttu-id="eeb89-142">In de vooraf gecompileerde functies worden de bindingen die wordt gebruikt door de functie gedefinieerd door het toepassen van kenmerken in de code.</span><span class="sxs-lookup"><span data-stu-id="eeb89-142">In pre-compiled functions, the bindings used by the function are defined by applying attributes in the code.</span></span> <span data-ttu-id="eeb89-143">Wanneer u de hulpprogramma's van Azure Functions voor het maken van uw functies van de opgegeven sjablonen gebruikt, worden deze kenmerken worden toegepast voor u.</span><span class="sxs-lookup"><span data-stu-id="eeb89-143">When you use the Azure Functions Tools to create your functions from the provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="eeb89-144">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer  > **Nieuw item****Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="eeb89-145">Selecteer **Azure-functie**, typ een **naam** voor de klasse en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-145">Select **Azure Function**, type a **Name** for the class, and click **Add**.</span></span>

2. <span data-ttu-id="eeb89-146">Kies de trigger, stelt u de bindingeigenschappen en klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="eeb89-146">Choose your trigger, set the binding properties, and click **Create**.</span></span> <span data-ttu-id="eeb89-147">Het volgende voorbeeld ziet de instellingen wanneer de functie voor het maken van een Queue storage geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="eeb89-147">The following example shows the settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="eeb89-148">Een sleutelreeks voor verbinding met de naam **QueueStorage** wordt geleverd, die is gedefinieerd in het bestand local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="eeb89-148">A connection string key named **QueueStorage** is supplied, which is defined in the local.settings.json file.</span></span> 
 
3. <span data-ttu-id="eeb89-149">Onderzoek de zojuist toegevoegde klasse.</span><span class="sxs-lookup"><span data-stu-id="eeb89-149">Examine the newly added class.</span></span> <span data-ttu-id="eeb89-150">U ziet een statische **uitvoeren** methode, dat is toegewezen met de **functienaam** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="eeb89-150">You see a static **Run** method, that is attributed with the **FunctionName** attribute.</span></span> <span data-ttu-id="eeb89-151">Dit kenmerk geeft aan dat de methode het toegangspunt voor de functie.</span><span class="sxs-lookup"><span data-stu-id="eeb89-151">This attribute indicates that the method is the entry point for the function.</span></span> 

    <span data-ttu-id="eeb89-152">De volgende C#-klasse staat bijvoorbeeld voor een eenvoudige wachtrij geactiveerd opslagfunctie:</span><span class="sxs-lookup"><span data-stu-id="eeb89-152">For example, the following C# class represents a basic Queue storage triggered function:</span></span>

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
 
    <span data-ttu-id="eeb89-153">Een kenmerk binding-specifieke wordt toegepast op elke binding parameter doorgegeven aan de methode post point.</span><span class="sxs-lookup"><span data-stu-id="eeb89-153">A binding-specific attribute is applied to each binding parameter supplied to the entry point method.</span></span> <span data-ttu-id="eeb89-154">Het kenmerk neemt de bindingsgegevens als parameters.</span><span class="sxs-lookup"><span data-stu-id="eeb89-154">The attribute takes the binding information as parameters.</span></span> <span data-ttu-id="eeb89-155">In het vorige voorbeeld wordt de eerste parameter heeft een **QueueTrigger** kenmerk dat wordt toegepast, die wachtrij geactiveerd functie aangeeft.</span><span class="sxs-lookup"><span data-stu-id="eeb89-155">In the previous example, The first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="eeb89-156">De wachtrijnaam en de naam van instelling verbindingsreeks worden als parameters doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="eeb89-156">The queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="eeb89-157">Functies testen</span><span class="sxs-lookup"><span data-stu-id="eeb89-157">Testing functions</span></span>

<span data-ttu-id="eeb89-158">Met Azure Functions Core-hulpprogramma's kunt u Azure Functions-projecten uitvoeren op uw lokale ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="eeb89-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="eeb89-159">De eerste keer dat u een functie vanuit Visual Studio start, wordt u gevraagd deze hulpprogramma's te installeren.</span><span class="sxs-lookup"><span data-stu-id="eeb89-159">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="eeb89-160">Druk op F5 om de functie testen.</span><span class="sxs-lookup"><span data-stu-id="eeb89-160">To test your function, press F5.</span></span> <span data-ttu-id="eeb89-161">Accepteer desgevraagd de aanvraag van Visual Studio om Azure Functions Core (CLI)-hulpprogramma's te downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="eeb89-161">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="eeb89-162">Mogelijk moet u ook een firewall-uitzondering inschakelen, zodat de hulpprogramma's HTTP-aanvragen kunnen afhandelen.</span><span class="sxs-lookup"><span data-stu-id="eeb89-162">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

<span data-ttu-id="eeb89-163">Aan het project dat wordt uitgevoerd, kunt u uw code testen, zoals u zou geïmplementeerde functie testen.</span><span class="sxs-lookup"><span data-stu-id="eeb89-163">With the project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="eeb89-164">Zie voor meer informatie [strategieën voor het testen van uw code in Azure Functions](functions-test-a-function.md).</span><span class="sxs-lookup"><span data-stu-id="eeb89-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="eeb89-165">Wanneer in de foutopsporingsmodus wordt uitgevoerd, worden de onderbrekingspunten druk in Visual Studio zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="eeb89-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="eeb89-166">Zie voor een voorbeeld van het testen van een wachtrij geactiveerd door de functie, de [wachtrij geactiveerd functie Quick Start-zelfstudie](functions-create-storage-queue-triggered-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="eeb89-166">For an example of how to test a queue triggered function, see the [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="eeb89-167">Zie voor meer informatie over het gebruik van de hulpprogramma's van Azure Functions Core, [Code en testen van Azure functions lokaal](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="eeb89-167">To learn more about using the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-to-azure"></a><span data-ttu-id="eeb89-168">Publiceren naar Azure</span><span class="sxs-lookup"><span data-stu-id="eeb89-168">Publish to Azure</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="eeb89-169">Alle instellingen die u hebt toegevoegd in de local.settings.json moeten ook worden toegevoegd aan de functie-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="eeb89-169">Any settings you added in the local.settings.json must be also added to the function app in Azure.</span></span> <span data-ttu-id="eeb89-170">Deze instellingen worden niet automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="eeb89-170">These settings are not added automatically.</span></span> <span data-ttu-id="eeb89-171">U kunt de vereiste instellingen toevoegen aan uw app functie in een van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="eeb89-171">You can add required settings to your function app in one of these ways:</span></span>
>
>* <span data-ttu-id="eeb89-172">[Met de Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="eeb89-172">[Using the Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="eeb89-173">[Met behulp van de `--publish-local-settings` optie publiceren in de hulpprogramma's van Azure Functions Core](functions-run-local.md#publish).</span><span class="sxs-lookup"><span data-stu-id="eeb89-173">[Using the `--publish-local-settings` publish option in the Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="eeb89-174">[De Azure CLI gebruiken](/cli/azure/functionapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="eeb89-174">[Using the Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eeb89-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eeb89-175">Next steps</span></span>

<span data-ttu-id="eeb89-176">Zie voor meer informatie over hulpprogramma's van Azure Functions, de sectie Veelgestelde vragen van de [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blogbericht.</span><span class="sxs-lookup"><span data-stu-id="eeb89-176">For more information about Azure Functions Tools, see the Common Questions section of the [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="eeb89-177">Zie voor meer informatie over de hulpprogramma's van Azure Functions Core, [Code en testen van Azure functions lokaal](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="eeb89-177">To learn more about the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="eeb89-178">Zie [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md) (.NET-klassebibliotheken gebruiken met Azure Functions) voor meer informatie over het ontwikkelen van functies als .NET-klassebibliotheken.</span><span class="sxs-lookup"><span data-stu-id="eeb89-178">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="eeb89-179">Dit onderwerp bevat ook voorbeelden van het gebruik van kenmerken voor de verschillende typen bindingen die worden ondersteund door Azure Functions declareren.</span><span class="sxs-lookup"><span data-stu-id="eeb89-179">This topic also provides examples of how to use attributes to declare the various types of bindings supported by Azure Functions.</span></span>    
