---
title: uw eerste functie in Azure met behulp van Visual Studio aaaCreate | Microsoft Docs
description: Maken en publiceren van een eenvoudige HTTP geactiveerd functie tooAzure met behulp van Azure Functions-hulpprogramma's voor Visual Studio.
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
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="52137-104">Uw eerste functie maken met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52137-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="52137-105">Azure Functions, kunt u uw code in een omgeving zonder server uitvoeren zonder toofirst een virtuele machine maken of een webtoepassing publiceert.</span><span class="sxs-lookup"><span data-stu-id="52137-105">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span>

<span data-ttu-id="52137-106">In dit onderwerp leert u hoe toouse 2017 voor Visual Studio-hulpprogramma's voor Azure Functions toocreate Hallo en de functie van een 'Hallo wereld' lokaal testen.</span><span class="sxs-lookup"><span data-stu-id="52137-106">In this topic, you learn how toouse hello Visual Studio 2017 tools for Azure Functions toocreate and test a "hello world" function locally.</span></span> <span data-ttu-id="52137-107">Vervolgens wordt u Hallo functie code tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="52137-107">You will then publish hello function code tooAzure.</span></span> <span data-ttu-id="52137-108">Deze hulpprogramma's zijn beschikbaar als onderdeel van hello Azure ontwikkeling werkbelasting in Visual Studio 2017 versie 15,3 of een latere versie.</span><span class="sxs-lookup"><span data-stu-id="52137-108">These tools are available as part of hello Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Azure-functiecode in een Visual Studio-project](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="52137-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="52137-110">Prerequisites</span></span>

<span data-ttu-id="52137-111">toocomplete deze zelfstudie, installatie:</span><span class="sxs-lookup"><span data-stu-id="52137-111">toocomplete this tutorial, install:</span></span>

* <span data-ttu-id="52137-112">[Visual Studio 2017 versie 15,3](https://www.visualstudio.com/vs/preview/), met inbegrip van Hallo **ontwikkelen van Azure** werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="52137-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including hello **Azure development** workload.</span></span>

    ![Installeer Visual Studio 2017 met hello Azure ontwikkeling werkbelasting](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="52137-114">Nadat u installeren of upgraden van tooVisual Studio 2017 versie 15,3, moet u mogelijk ook toomanually update Hallo 2017 van Visual Studio-hulpprogramma's voor Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="52137-114">After you install or upgrade tooVisual Studio 2017 version 15.3, you might also need toomanually update hello Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="52137-115">U kunt bijwerken Hallo-hulpprogramma's van Hallo **extra** menu onder **uitbreidingen en Updates...**   >  **Updates** > **Visual Studio Marketplace** > **Azure Functions en Web extra taken**  >  **Update**.</span><span class="sxs-lookup"><span data-stu-id="52137-115">You can update hello tools from hello **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="52137-116">Een Azure Functions-project in Visual Studio maken</span><span class="sxs-lookup"><span data-stu-id="52137-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="52137-117">Nu u Hallo-project hebt gemaakt, kunt u uw eerste functie maken.</span><span class="sxs-lookup"><span data-stu-id="52137-117">Now that you have created hello project, you can create your first function.</span></span>

## <a name="create-hello-function"></a><span data-ttu-id="52137-118">Hallo-functie maken</span><span class="sxs-lookup"><span data-stu-id="52137-118">Create hello function</span></span>

1. <span data-ttu-id="52137-119">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer  > **Nieuw item****Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="52137-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="52137-120">Selecteer **Azure-functie** en klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="52137-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="52137-121">Selecteer **HttpTrigger**, typ een **Functienaam**, selecteer **Anoniem** bij **Toegangsrechten** en klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="52137-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="52137-122">Hallo-functie gemaakt, wordt geopend door een HTTP-aanvraag vanaf elke client.</span><span class="sxs-lookup"><span data-stu-id="52137-122">hello function created is accessed by an HTTP request from any client.</span></span> 

    ![Een nieuwe Azure-functie maken](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="52137-124">Een bestand met code toegevoegd tooyour project met een klasse die de functiecode implementeert.</span><span class="sxs-lookup"><span data-stu-id="52137-124">A code file is added tooyour project that contains a class that implements your function code.</span></span> <span data-ttu-id="52137-125">Deze code is gebaseerd op een sjabloon waarmee u een naamwaarde en het gebruik weer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="52137-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="52137-126">Hallo **functienaam** kenmerk Hallo-naam van de functie wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="52137-126">hello **FunctionName** attribute sets hello name of your function.</span></span> <span data-ttu-id="52137-127">Hallo **HttpTrigger** kenmerk geeft aan dat het Hallo-bericht waarmee Hallo-functie wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="52137-127">hello **HttpTrigger** attribute indicates hello message that triggers hello function.</span></span> 

    ![Functie codebestand](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="52137-129">Nu u een HTTP-geactiveerde-functie hebt gemaakt, kunt u deze testen op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="52137-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-hello-function-locally"></a><span data-ttu-id="52137-130">Hallo functie lokaal testen</span><span class="sxs-lookup"><span data-stu-id="52137-130">Test hello function locally</span></span>

<span data-ttu-id="52137-131">Met Azure Functions Core-hulpprogramma's kunt u Azure Functions-projecten uitvoeren op uw lokale ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="52137-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="52137-132">U bent na vragen aan gebruiker tooinstall deze hulpprogramma's Hallo eerste keer dat u een functie vanuit Visual Studio start.</span><span class="sxs-lookup"><span data-stu-id="52137-132">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="52137-133">tootest uw functie druk op F5.</span><span class="sxs-lookup"><span data-stu-id="52137-133">tootest your function, press F5.</span></span> <span data-ttu-id="52137-134">Als u wordt gevraagd, Hallo verzoek van Visual Studio toodownload accepteert en hulpprogramma's voor Azure Functions Core (CLI) installeren.</span><span class="sxs-lookup"><span data-stu-id="52137-134">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="52137-135">U moet mogelijk ook een firewall-uitzondering tooenable zodat Hallo hulpprogramma's voor HTTP-aanvragen kunnen verwerken.</span><span class="sxs-lookup"><span data-stu-id="52137-135">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="52137-136">Hallo-URL kopiëren van de functie van Azure Functions-runtime Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="52137-136">Copy hello URL of your function from hello Azure Functions runtime output.</span></span>  

    ![Lokale Azure-runtime](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="52137-138">Hallo-URL voor Hallo HTTP-aanvraag in de adresbalk van uw browser plakken.</span><span class="sxs-lookup"><span data-stu-id="52137-138">Paste hello URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="52137-139">Hallo-queryreeks toevoegen `&name=<yourname>` toothis URL en Hallo aanvraag uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="52137-139">Append hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span> <span data-ttu-id="52137-140">Hallo hieronder vindt u antwoord Hallo in Hallo browser toohello lokale GET-aanvraag geretourneerd door de functie Hallo:</span><span class="sxs-lookup"><span data-stu-id="52137-140">hello following shows hello response in hello browser toohello local GET request returned by hello function:</span></span> 

    ![Functie localhost-respons in Hallo-browser](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="52137-142">toostop foutopsporing, klikt u op Hallo **stoppen** op de werkbalk van Hallo Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52137-142">toostop debugging, click hello **Stop** button on hello Visual Studio toolbar.</span></span>

<span data-ttu-id="52137-143">Nadat u hebt gecontroleerd of de functie Hallo correct wordt uitgevoerd op de lokale computer, is het tijd toopublish Hallo project tooAzure.</span><span class="sxs-lookup"><span data-stu-id="52137-143">After you have verified that hello function runs correctly on your local computer, it's time toopublish hello project tooAzure.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="52137-144">Hallo project tooAzure publiceren</span><span class="sxs-lookup"><span data-stu-id="52137-144">Publish hello project tooAzure</span></span>

<span data-ttu-id="52137-145">Voordat u uw project kunt publiceren, moet u een functie-app in uw Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="52137-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="52137-146">U kunt rechtstreeks vanuit Visual Studio een functie-app maken.</span><span class="sxs-lookup"><span data-stu-id="52137-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="52137-147">Uw functie testen in Azure</span><span class="sxs-lookup"><span data-stu-id="52137-147">Test your function in Azure</span></span>

1. <span data-ttu-id="52137-148">Hallo basis-URL van de functie-app Hallo van Hallo publiceren profielpagina kopiëren.</span><span class="sxs-lookup"><span data-stu-id="52137-148">Copy hello base URL of hello function app from hello Publish profile page.</span></span> <span data-ttu-id="52137-149">Vervang Hallo `localhost:port` gedeelte van het Hallo-URL die u hebt gebruikt bij het testen van de functie Hallo lokaal met Hallo nieuwe basis-URL.</span><span class="sxs-lookup"><span data-stu-id="52137-149">Replace hello `localhost:port` portion of hello URL you used when testing hello function locally with hello new base URL.</span></span> <span data-ttu-id="52137-150">Als voorheen Zorg ervoor dat tooappend Hallo-queryreeks `&name=<yourname>` toothis URL en Hallo aanvraag uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="52137-150">As before, make sure tooappend hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span>

    <span data-ttu-id="52137-151">Hallo-URL die uw HTTP-aanroepen geactiveerd functie ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="52137-151">hello URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="52137-152">Deze nieuwe URL voor Hallo HTTP-aanvraag in de adresbalk van uw browser plakken.</span><span class="sxs-lookup"><span data-stu-id="52137-152">Paste this new URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="52137-153">Hallo hieronder vindt u antwoord Hallo in Hallo browser toohello externe GET-aanvraag geretourneerd door de functie Hallo:</span><span class="sxs-lookup"><span data-stu-id="52137-153">hello following shows hello response in hello browser toohello remote GET request returned by hello function:</span></span> 

    ![Functie-respons in Hallo-browser](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="52137-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="52137-155">Next steps</span></span>

<span data-ttu-id="52137-156">Met de functie van een eenvoudige HTTP is geactiveerd, hebt u Visual Studio toocreate een C#-functie-app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="52137-156">You have used Visual Studio toocreate a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="52137-157">toolearn hoe tooconfigure uw project toosupport andere soorten triggers en bindingen, Zie Hallo [Hallo-project configureren voor lokale ontwikkeling](functions-develop-vs.md#configure-the-project-for-local-development) in sectie [Azure Functions-Tools voor Visual Studio](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="52137-157">toolearn how tooconfigure your project toosupport other types of triggers and bindings, see hello [Configure hello project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="52137-158">toolearn meer informatie over lokale testen en foutopsporing met hello Azure Functions Core's, Zie [Code en test Azure Functions lokaal](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="52137-158">toolearn more about local testing and debugging using hello Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="52137-159">toolearn meer informatie over het ontwikkelen van functies als .NET-klassebibliotheken, Zie [met behulp van .NET-klassebibliotheken met Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="52137-159">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

