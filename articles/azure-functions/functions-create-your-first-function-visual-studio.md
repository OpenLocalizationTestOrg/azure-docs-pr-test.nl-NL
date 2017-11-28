---
title: Uw eerste functie maken in Azure met behulp van Visual Studio | Microsoft Docs
description: Maak een eenvoudige HTTP-geactiveerde functie en publiceer deze op Azure met behulp van Azure Functions-hulpprogramma's voor Visual Studio.
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: azure-functies, functies, gebeurtenisverwerking, berekenen, architectuur zonder server
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 04370558725d76ffe83d8aaf5d16c88fd2803ba9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="45923-104">Uw eerste functie maken met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45923-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="45923-105">Met Azure Functions kunt u uw code in een serverloze omgeving uitvoeren zonder dat u eerst een virtuele machine moet maken of een webtoepassing moet publiceren.</span><span class="sxs-lookup"><span data-stu-id="45923-105">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span>

<span data-ttu-id="45923-106">In dit onderwerp leert u hoe u met de Visual Studio 2017 hulpprogramma's voor Azure Functions maken en testen van een functie 'Hallo wereld' lokaal.</span><span class="sxs-lookup"><span data-stu-id="45923-106">In this topic, you learn how to use the Visual Studio 2017 tools for Azure Functions to create and test a "hello world" function locally.</span></span> <span data-ttu-id="45923-107">Vervolgens publiceert u de functiecode op Azure.</span><span class="sxs-lookup"><span data-stu-id="45923-107">You will then publish the function code to Azure.</span></span> <span data-ttu-id="45923-108">Deze hulpprogramma's zijn beschikbaar als onderdeel van de Azure-ontwikkelworkload in Visual Studio 2017 versie 15.3 of een latere versie.</span><span class="sxs-lookup"><span data-stu-id="45923-108">These tools are available as part of the Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Azure-functiecode in een Visual Studio-project](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="45923-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="45923-110">Prerequisites</span></span>

<span data-ttu-id="45923-111">Voor deze zelfstudie installeert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="45923-111">To complete this tutorial, install:</span></span>

* <span data-ttu-id="45923-112">[Visual Studio 2017 versie 15.3](https://www.visualstudio.com/vs/preview/), waaronder de **Azure-ontwikkelworkload**.</span><span class="sxs-lookup"><span data-stu-id="45923-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span></span>

    ![Visual Studio 2017 installeren met de Azure-ontwikkelworkload](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="45923-114">Nadat u installeert of een upgrade naar Visual Studio 2017 versie 15,3 uitvoert, moet u mogelijk ook handmatig bijwerken van de Visual Studio 2017 hulpprogramma's voor Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="45923-114">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="45923-115">U kunt de hulpprogramma's van bijwerken de **extra** menu onder **uitbreidingen en Updates...**   >  **Updates** > **Visual Studio Marketplace** > **Azure Functions en Web extra taken** > **Update**.</span><span class="sxs-lookup"><span data-stu-id="45923-115">You can update the tools from the **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="45923-116">Een Azure Functions-project in Visual Studio maken</span><span class="sxs-lookup"><span data-stu-id="45923-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using the Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="45923-117">Nu u het project hebt gemaakt, kunt u uw eerste functie maken.</span><span class="sxs-lookup"><span data-stu-id="45923-117">Now that you have created the project, you can create your first function.</span></span>

## <a name="create-the-function"></a><span data-ttu-id="45923-118">De functie maken</span><span class="sxs-lookup"><span data-stu-id="45923-118">Create the function</span></span>

1. <span data-ttu-id="45923-119">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer  > **Nieuw item****Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="45923-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="45923-120">Selecteer **Azure-functie** en klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="45923-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="45923-121">Selecteer **HttpTrigger**, typ een **Functienaam**, selecteer **Anoniem** bij **Toegangsrechten** en klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="45923-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="45923-122">De gemaakte functie wordt geopend door een HTTP-aanvraag vanaf een client.</span><span class="sxs-lookup"><span data-stu-id="45923-122">The function created is accessed by an HTTP request from any client.</span></span> 

    ![Een nieuwe Azure-functie maken](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="45923-124">Een bestand met code wordt toegevoegd aan uw project met een klasse die de functiecode implementeert.</span><span class="sxs-lookup"><span data-stu-id="45923-124">A code file is added to your project that contains a class that implements your function code.</span></span> <span data-ttu-id="45923-125">Deze code is gebaseerd op een sjabloon waarmee u een naamwaarde en het gebruik weer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="45923-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="45923-126">De **functienaam** kenmerk stelt de naam van de functie.</span><span class="sxs-lookup"><span data-stu-id="45923-126">The **FunctionName** attribute sets the name of your function.</span></span> <span data-ttu-id="45923-127">De **HttpTrigger** kenmerk geeft aan dat het bericht dat de functie activeert.</span><span class="sxs-lookup"><span data-stu-id="45923-127">The **HttpTrigger** attribute indicates the message that triggers the function.</span></span> 

    ![Functie codebestand](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="45923-129">Nu u een HTTP-geactiveerde-functie hebt gemaakt, kunt u deze testen op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="45923-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-the-function-locally"></a><span data-ttu-id="45923-130">De functie lokaal testen</span><span class="sxs-lookup"><span data-stu-id="45923-130">Test the function locally</span></span>

<span data-ttu-id="45923-131">Met Azure Functions Core-hulpprogramma's kunt u Azure Functions-projecten uitvoeren op uw lokale ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="45923-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="45923-132">De eerste keer dat u een functie vanuit Visual Studio start, wordt u gevraagd deze hulpprogramma's te installeren.</span><span class="sxs-lookup"><span data-stu-id="45923-132">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="45923-133">Druk op F5 om de functie testen.</span><span class="sxs-lookup"><span data-stu-id="45923-133">To test your function, press F5.</span></span> <span data-ttu-id="45923-134">Accepteer desgevraagd de aanvraag van Visual Studio om Azure Functions Core (CLI)-hulpprogramma's te downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="45923-134">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="45923-135">Mogelijk moet u ook een firewall-uitzondering inschakelen, zodat de hulpprogramma's HTTP-aanvragen kunnen afhandelen.</span><span class="sxs-lookup"><span data-stu-id="45923-135">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="45923-136">Kopieer de URL van uw functie vanuit de uitvoer van de Azure Functions-runtime.</span><span class="sxs-lookup"><span data-stu-id="45923-136">Copy the URL of your function from the Azure Functions runtime output.</span></span>  

    ![Lokale Azure-runtime](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="45923-138">Plak de URL van de HTTP-aanvraag in de adresbalk van uw browser.</span><span class="sxs-lookup"><span data-stu-id="45923-138">Paste the URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="45923-139">Voeg de queryreeks `&name=<yourname>` toe aan de URL en voer de aanvraag uit.</span><span class="sxs-lookup"><span data-stu-id="45923-139">Append the query string `&name=<yourname>` to this URL and execute the request.</span></span> <span data-ttu-id="45923-140">Hieronder ziet u de reactie op de lokale GET-aanvraag die door de functie wordt geretourneerd, weergegeven in de browser:</span><span class="sxs-lookup"><span data-stu-id="45923-140">The following shows the response in the browser to the local GET request returned by the function:</span></span> 

    ![De reactie van de lokale host van de functie in de browser](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="45923-142">Als u de foutopsporing wilt stoppen, klikt u op de knop **Stop** op de werkbalk van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45923-142">To stop debugging, click the **Stop** button on the Visual Studio toolbar.</span></span>

<span data-ttu-id="45923-143">Nadat u hebt gecontroleerd of de functie correct wordt uitgevoerd op uw lokale computer, is het tijd om het project te publiceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="45923-143">After you have verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="45923-144">Het project naar Azure publiceren</span><span class="sxs-lookup"><span data-stu-id="45923-144">Publish the project to Azure</span></span>

<span data-ttu-id="45923-145">Voordat u uw project kunt publiceren, moet u een functie-app in uw Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="45923-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="45923-146">U kunt rechtstreeks vanuit Visual Studio een functie-app maken.</span><span class="sxs-lookup"><span data-stu-id="45923-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="45923-147">Uw functie testen in Azure</span><span class="sxs-lookup"><span data-stu-id="45923-147">Test your function in Azure</span></span>

1. <span data-ttu-id="45923-148">Kopieer de basis-URL van de functie-app van de pagina Profiel publiceren.</span><span class="sxs-lookup"><span data-stu-id="45923-148">Copy the base URL of the function app from the Publish profile page.</span></span> <span data-ttu-id="45923-149">Vervang het `localhost:port`-deel van de URL dat u hebt gebruikt bij het lokaal testen van de functie door de nieuwe basis-URL.</span><span class="sxs-lookup"><span data-stu-id="45923-149">Replace the `localhost:port` portion of the URL you used when testing the function locally with the new base URL.</span></span> <span data-ttu-id="45923-150">Zorg ervoor dat u net als eerder de queryreeks `&name=<yourname>` toevoegt aan de URL en de aanvraag uitvoert.</span><span class="sxs-lookup"><span data-stu-id="45923-150">As before, make sure to append the query string `&name=<yourname>` to this URL and execute the request.</span></span>

    <span data-ttu-id="45923-151">De URL die uw HTTP-geactiveerde functie aanroept, ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="45923-151">The URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="45923-152">Plak deze nieuwe URL van de HTTP-aanvraag in de adresbalk van uw browser.</span><span class="sxs-lookup"><span data-stu-id="45923-152">Paste this new URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="45923-153">Hieronder ziet u het antwoord op de externe GET-aanvraag dat door de functie wordt geretourneerd, weergegeven in de browser:</span><span class="sxs-lookup"><span data-stu-id="45923-153">The following shows the response in the browser to the remote GET request returned by the function:</span></span> 

    ![Het antwoord van de functie in de browser](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="45923-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45923-155">Next steps</span></span>

<span data-ttu-id="45923-156">U hebt een C#-functie-app met een eenvoudige HTTP-geactiveerde functie gemaakt in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45923-156">You have used Visual Studio to create a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="45923-157">Zie [Het project configureren voor lokale ontwikkeling](functions-develop-vs.md#configure-the-project-for-local-development) in de sectie [Azure Functions-tools voor Visual Studio](functions-develop-vs.md) voor meer informatie over het configureren van uw project ter ondersteuning van andere soorten triggers en bindingen.</span><span class="sxs-lookup"><span data-stu-id="45923-157">To learn how to configure your project to support other types of triggers and bindings, see the [Configure the project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="45923-158">Zie voor meer informatie over het lokale testen en foutopsporing met behulp van de Azure Functions Core Tools, [Code and test Azure Functions locally](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="45923-158">To learn more about local testing and debugging using the Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="45923-159">Zie [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md) (.NET-klassebibliotheken gebruiken met Azure Functions) voor meer informatie over het ontwikkelen van functies als .NET-klassebibliotheken.</span><span class="sxs-lookup"><span data-stu-id="45923-159">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

