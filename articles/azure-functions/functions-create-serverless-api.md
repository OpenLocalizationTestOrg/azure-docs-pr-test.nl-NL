---
title: aaaCreate een zonder Server API met behulp van Azure Functions | Microsoft Docs
description: Hoe toocreate een zonder Server API met behulp van Azure Functions
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="5e1ae-103">Een zonder Server API met behulp van Azure Functions maken</span><span class="sxs-lookup"><span data-stu-id="5e1ae-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="5e1ae-104">In deze zelfstudie leert u hoe Azure-functies kunt u toobuild uiterst schaalbare API's.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="5e1ae-105">Azure Functions wordt geleverd met een verzameling van ingebouwde HTTP-triggers en bindingen zodat het eenvoudig tooauthor een eindpunt in verschillende talen, waaronder Node.JS, C# en meer.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="5e1ae-106">In deze zelfstudie gaat u een HTTP-trigger toohandle specifieke acties in uw ontwerp API aanpassen.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="5e1ae-107">U wordt ook voorbereiden voor uw API groeiende door integratie met Azure Functions-proxy's en het instellen van mock-API's.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="5e1ae-108">Dit alles wordt gerealiseerd boven op Hallo functies zonder server compute omgeving, dus u hebt geen tooworry over het schalen van resources: u kunt alleen zich richten op uw API-logica.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e1ae-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5e1ae-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="5e1ae-110">Hallo resulterende functie wordt gebruikt voor Hallo rest van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="5e1ae-111">Meld u aan tooAzure</span><span class="sxs-lookup"><span data-stu-id="5e1ae-111">Sign in tooAzure</span></span>

<span data-ttu-id="5e1ae-112">Open hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-112">Open hello Azure portal.</span></span> <span data-ttu-id="5e1ae-113">toodo dit te melden[https://portal.azure.com](https://portal.azure.com) met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="5e1ae-114">Aanpassen van uw HTTP-functie</span><span class="sxs-lookup"><span data-stu-id="5e1ae-114">Customize your HTTP function</span></span>

<span data-ttu-id="5e1ae-115">Uw HTTP-geactiveerde-functie is standaard geconfigureerd tooaccept alle HTTP-methode.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="5e1ae-116">Er is ook een standaard-URL van Hallo formulier `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="5e1ae-117">Als u de Quick Start hello, vervolgens gevolgd `<funcname>` waarschijnlijk ziet er ongeveer zo 'HttpTriggerJS1'.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="5e1ae-118">In deze sectie, wijzigt u Hallo functie toorespond alleen tooGET aanvragen op basis van `/api/hello` in plaats daarvan te routeren.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="5e1ae-119">Navigeer tooyour-functie in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="5e1ae-120">Selecteer **integreren** in Hallo linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-120">Select **Integrate** in hello left navigation.</span></span>

![Aanpassen van een HTTP-functie](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="5e1ae-122">De HTTP-trigger-instellingen zoals opgegeven in de tabel hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="5e1ae-123">Veld</span><span class="sxs-lookup"><span data-stu-id="5e1ae-123">Field</span></span> | <span data-ttu-id="5e1ae-124">Voorbeeldwaarde</span><span class="sxs-lookup"><span data-stu-id="5e1ae-124">Sample value</span></span> | <span data-ttu-id="5e1ae-125">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5e1ae-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="5e1ae-126">Toegestane HTTP-methoden</span><span class="sxs-lookup"><span data-stu-id="5e1ae-126">Allowed HTTP methods</span></span> | <span data-ttu-id="5e1ae-127">Geselecteerde methoden</span><span class="sxs-lookup"><span data-stu-id="5e1ae-127">Selected methods</span></span> | <span data-ttu-id="5e1ae-128">Bepaalt welke HTTP-methoden mogelijk gebruikte tooinvoke deze functie</span><span class="sxs-lookup"><span data-stu-id="5e1ae-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="5e1ae-129">Geselecteerde HTTP-methoden</span><span class="sxs-lookup"><span data-stu-id="5e1ae-129">Selected HTTP methods</span></span> | <span data-ttu-id="5e1ae-130">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="5e1ae-130">GET</span></span> | <span data-ttu-id="5e1ae-131">Kan deze functie hebt gebruikt tooinvoke alleen geselecteerde HTTP-methoden toobe</span><span class="sxs-lookup"><span data-stu-id="5e1ae-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="5e1ae-132">Routesjabloon</span><span class="sxs-lookup"><span data-stu-id="5e1ae-132">Route template</span></span> | <span data-ttu-id="5e1ae-133">uit</span><span class="sxs-lookup"><span data-stu-id="5e1ae-133">/hello</span></span> | <span data-ttu-id="5e1ae-134">Hiermee wordt bepaald welke route gebruikte tooinvoke deze functie</span><span class="sxs-lookup"><span data-stu-id="5e1ae-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="5e1ae-135">U hebt geen Hallo opgenomen opmerking `/api` baseren pad-voorvoegsel op in de Routesjabloon hello, als dit wordt verwerkt door een algemene instelling.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="5e1ae-136">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-136">Click **Save**.</span></span>

<span data-ttu-id="5e1ae-137">U kunt meer informatie over het aanpassen van HTTP-functies in [bindingen van Azure Functions HTTP- en webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="5e1ae-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="5e1ae-138">Uw API testen</span><span class="sxs-lookup"><span data-stu-id="5e1ae-138">Test your API</span></span>

<span data-ttu-id="5e1ae-139">Vervolgens testen uw toosee functie werken met de nieuwe API-gebied Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="5e1ae-140">Navigeer terug toohello ontwikkeling pagina door te klikken op Hallo van de functienaam in de linkernavigatiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="5e1ae-141">Klik op **ophalen van de functie URL** en kopieer Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="5e1ae-142">U ziet dat deze gebruikmaakt van Hallo `/api/hello` nu routeren.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="5e1ae-143">Kopieer Hallo-URL in een nieuw browsertabblad of uw voorkeur REST-client.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="5e1ae-144">Browsers wordt GET standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="5e1ae-145">Hallo-functie uitvoeren en controleren of deze werkt.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="5e1ae-146">U moet mogelijk tooprovide Hallo 'name' parameter als een query-tekenreeks toosatisfy Hallo Quick Start-code.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="5e1ae-147">U kunt ook proberen het Hallo-eindpunt met een andere HTTP-methode tooconfirm Hallo-functie is niet uitgevoerd wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="5e1ae-148">Hiervoor moet u een REST-client, zoals cURL, Postman of Fiddler toouse.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="5e1ae-149">Overzicht van proxy 's</span><span class="sxs-lookup"><span data-stu-id="5e1ae-149">Proxies overview</span></span>

<span data-ttu-id="5e1ae-150">In de volgende sectie hello, wordt u uw API via een proxy surface.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="5e1ae-151">Azure Functions-proxy's is een preview-functie waarmee u tooforward aanvragen tooother resources.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="5e1ae-152">U net zoals een HTTP-eindpunt definiëren met HTTP-trigger, maar in plaats van het schrijven van code tooexecute wanneer dat eindpunt wordt aangeroepen, bieden u een externe URL tooa-implementatie.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="5e1ae-153">Hiermee kunt u meerdere API gegevensbronnen in een enkel API-gebied gemakkelijk voor clients tooconsume toocompose.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="5e1ae-154">Dit is vooral handig als u uw API als microservices toobuild wenst.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="5e1ae-155">Een proxy kan verwijzen tooany HTTP-resource, zoals:</span><span class="sxs-lookup"><span data-stu-id="5e1ae-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="5e1ae-156">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5e1ae-156">Azure Functions</span></span> 
- <span data-ttu-id="5e1ae-157">API-apps in [-Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="5e1ae-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="5e1ae-158">Docker-containers in [op Linux-App Service](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="5e1ae-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="5e1ae-159">Andere gehoste API</span><span class="sxs-lookup"><span data-stu-id="5e1ae-159">Any other hosted API</span></span>

<span data-ttu-id="5e1ae-160">toolearn meer informatie over proxy's, Zie [werken met Azure Functions-proxy's (preview)].</span><span class="sxs-lookup"><span data-stu-id="5e1ae-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="5e1ae-161">Uw eerste proxy maken</span><span class="sxs-lookup"><span data-stu-id="5e1ae-161">Create your first proxy</span></span>

<span data-ttu-id="5e1ae-162">In deze sectie maakt u een nieuwe proxy die fungeert als een frontend tooyour algemene API.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="5e1ae-163">Hallo frontend-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="5e1ae-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="5e1ae-164">Herhaal de stappen van de Hallo te[maken van een functie-app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate een nieuwe functie-app in die u de proxy maakt.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="5e1ae-165">Deze nieuwe app fungeert als Hallo frontend voor onze API en Hallo functie-app die u eerder hebt bewerkt fungeert als een back-end.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="5e1ae-166">Navigeer tooyour nieuwe frontend functie-app in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="5e1ae-167">Selecteer **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-167">Select **Settings**.</span></span> <span data-ttu-id="5e1ae-168">Klik in-of uitschakelen **inschakelen Azure Functions-proxy's (preview)** te 'op'.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="5e1ae-169">Selecteer **Platform instellingen** en kies **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="5e1ae-170">Schuif naar beneden te**appinstellingen** en maak een nieuwe instelling met sleutel 'HELLO_HOST'.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="5e1ae-171">De waarde toohello host van uw back-end-functie-app, zoals ingesteld `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="5e1ae-172">Dit is onderdeel van het Hallo-URL die u eerder hebt gekopieerd bij het testen van uw HTTP-functie.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="5e1ae-173">U moet deze instelling in configuratie hello later naar verwijzen.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="5e1ae-174">App-instellingen worden aanbevolen voor Hallo host configuratie tooprevent een afhankelijkheid vastgelegde omgeving voor Hallo proxy.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="5e1ae-175">Met behulp van appinstellingen betekent dat u de proxyconfiguratie Hallo tussen omgevingen verplaatsen kunt en Hallo omgeving-specifieke app-instellingen worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="5e1ae-176">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="5e1ae-177">Maken van een proxy op Hallo frontend</span><span class="sxs-lookup"><span data-stu-id="5e1ae-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="5e1ae-178">Navigeer terug tooyour frontend functie-app in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="5e1ae-179">Klik in de linkernavigatiebalk hello, op Hallo plusteken '+' volgende te 'Proxy's (preview)'.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![Maken van een proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="5e1ae-181">Proxy-instellingen zoals opgegeven in de tabel hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="5e1ae-182">Veld</span><span class="sxs-lookup"><span data-stu-id="5e1ae-182">Field</span></span> | <span data-ttu-id="5e1ae-183">Voorbeeldwaarde</span><span class="sxs-lookup"><span data-stu-id="5e1ae-183">Sample value</span></span> | <span data-ttu-id="5e1ae-184">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5e1ae-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="5e1ae-185">Naam</span><span class="sxs-lookup"><span data-stu-id="5e1ae-185">Name</span></span> | <span data-ttu-id="5e1ae-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="5e1ae-186">HelloProxy</span></span> | <span data-ttu-id="5e1ae-187">Een beschrijvende naam wordt alleen gebruikt voor beheer</span><span class="sxs-lookup"><span data-stu-id="5e1ae-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="5e1ae-188">Routesjabloon</span><span class="sxs-lookup"><span data-stu-id="5e1ae-188">Route template</span></span> | <span data-ttu-id="5e1ae-189">/ api/Hallo</span><span class="sxs-lookup"><span data-stu-id="5e1ae-189">/api/hello</span></span> | <span data-ttu-id="5e1ae-190">Hiermee wordt bepaald welke route gebruikte tooinvoke deze proxy</span><span class="sxs-lookup"><span data-stu-id="5e1ae-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="5e1ae-191">Back-end-URL</span><span class="sxs-lookup"><span data-stu-id="5e1ae-191">Backend URL</span></span> | <span data-ttu-id="5e1ae-192">https://%HELLO_HOST%/API/Hello</span><span class="sxs-lookup"><span data-stu-id="5e1ae-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="5e1ae-193">Hiermee wordt aangegeven Hallo eindpunt toowhich Hallo aanvraag moeten via proxy</span><span class="sxs-lookup"><span data-stu-id="5e1ae-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="5e1ae-194">Houd er rekening mee dat proxy's geen Hallo biedt `/api` basispad voorvoegsel en deze moet worden opgenomen in de Routesjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="5e1ae-195">Hallo `%HELLO_HOST%` syntaxis wordt verwezen naar Hallo app-instelling die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="5e1ae-196">Hallo opgelost dat URL wordt de oorspronkelijke functie tooyour verwijzen.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="5e1ae-197">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-197">Click **Create**.</span></span>

<span data-ttu-id="5e1ae-198">U kunt uw nieuwe proxy uitproberen door Hallo Proxy URL kopiëren en testen van het in de browser Hallo of met uw favoriete HTTP-client.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="5e1ae-199">Een mock-API maken</span><span class="sxs-lookup"><span data-stu-id="5e1ae-199">Create a mock API</span></span>

<span data-ttu-id="5e1ae-200">Vervolgens gebruikt u een proxy toocreate een mock-API voor uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="5e1ae-201">Hierdoor kunnen client-ontwikkeling tooprogress zonder Hallo backend volledig geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="5e1ae-202">Verderop in ontwikkeling, kan u een nieuwe functie-app die ondersteuning biedt voor deze logica maken en uw proxy-tooit omleiden.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="5e1ae-203">toocreate dit model API, maken we een nieuwe proxy met behulp van Hallo [App Service-Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="5e1ae-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="5e1ae-204">tooget gestart, gaat u tooyour functie-app in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="5e1ae-205">Selecteer **platformfuncties** en zoek **App Service-Editor**.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="5e1ae-206">Als u dit opent u Hallo App Service-Editor in een nieuw tabblad.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="5e1ae-207">Selecteer `proxies.json` in Hallo linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="5e1ae-208">Dit is Hallo-bestand waarin Hallo-configuratie voor al uw proxy's worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="5e1ae-209">Als u een Hallo [fungeert implementatiemethoden](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), dit is een Hallo u in broncodebeheer bewaart.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="5e1ae-210">Zie toolearn meer informatie over dit bestand [proxy's geavanceerde configuratie](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="5e1ae-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="5e1ae-211">Als u tot nu toe hebt opgevolgd langs, worden uw proxies.json moet eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5e1ae-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="5e1ae-212">Vervolgens voegt u uw mock-API.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-212">Next you'll add your mock API.</span></span> <span data-ttu-id="5e1ae-213">Uw bestand proxies.json vervangen door de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="5e1ae-213">Replace your proxies.json file with hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="5e1ae-214">Hiermee wordt een nieuwe proxy 'GetUserByName' zonder Hallo backendUri eigenschap toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="5e1ae-215">In plaats van een andere resource aanroept, wijzigt het Hallo standaardreactie van proxy's met een onderdrukking antwoord.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="5e1ae-216">Aanvraag en -antwoord onderdrukkingen kunnen ook worden gebruikt in combinatie met een back-end-URL.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="5e1ae-217">Dit is vooral handig bij het gebruik van proxy tooa oude systeem, zult u toomodify headers, queryparameters, enz. toolearn meer informatie over aanvraag- en onderdrukkingen, Zie [wijzigen aanvragen en antwoorden in de proxy's](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="5e1ae-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="5e1ae-218">Uw mock API testen door aanroepen Hallo `/api/users/{username}` -eindpunt met een browser of uw favoriete REST-client.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="5e1ae-219">Ervoor tooreplace worden _{username}_ met de waarde van een tekenreeks die een gebruikersnaam vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e1ae-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e1ae-220">Next steps</span></span>

<span data-ttu-id="5e1ae-221">In deze zelfstudie hebt u geleerd hoe toobuild en aanpassen van een API van Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="5e1ae-222">U hebt ook geleerd hoe toobring meerdere API's, waaronder mocks, samen als een geïntegreerde API-gebied.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="5e1ae-223">U kunt deze toobuild technieken uit API's van elk complexiteit, alle bij het uitvoeren op Hallo zonder server model verstrekt door Azure Functions compute.</span><span class="sxs-lookup"><span data-stu-id="5e1ae-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="5e1ae-224">Hallo te volgende verwijzingen helpen bij het ontwikkelen van uw API verder:</span><span class="sxs-lookup"><span data-stu-id="5e1ae-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="5e1ae-225">Azure Functions HTTP- en webhook bindingen</span><span class="sxs-lookup"><span data-stu-id="5e1ae-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="5e1ae-226">[werken met Azure Functions-proxy's (preview)]</span><span class="sxs-lookup"><span data-stu-id="5e1ae-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="5e1ae-227">Een Azure-functies-API (preview) documenteren</span><span class="sxs-lookup"><span data-stu-id="5e1ae-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[werken met Azure Functions-proxy's (preview)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
