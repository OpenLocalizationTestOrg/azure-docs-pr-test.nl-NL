---
title: Maken van een zonder Server API met behulp van Azure Functions | Microsoft Docs
description: Het maken van een zonder Server API met behulp van Azure Functions
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
ms.openlocfilehash: 28056a385b058f7daeca2253ccb304116b49eba0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="a3270-103">Een zonder Server API met behulp van Azure Functions maken</span><span class="sxs-lookup"><span data-stu-id="a3270-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="a3270-104">In deze zelfstudie leert u hoe Azure-functies kunt u zeer schaalbare API's maken.</span><span class="sxs-lookup"><span data-stu-id="a3270-104">In this tutorial you will learn how Azure Functions allows you to build highly-scalable APIs.</span></span> <span data-ttu-id="a3270-105">Azure Functions wordt geleverd met een verzameling van ingebouwde HTTP-triggers en bindingen die gemakkelijk te maken van een eindpunt in verschillende talen, waaronder Node.JS, C# en meer.</span><span class="sxs-lookup"><span data-stu-id="a3270-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy to author an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="a3270-106">In deze zelfstudie maakt gaat u een HTTP-trigger voor het afhandelen van bepaalde acties in uw API-ontwerp aanpassen.</span><span class="sxs-lookup"><span data-stu-id="a3270-106">In this tutorial, you will customize an HTTP trigger to handle specific actions in your API design.</span></span> <span data-ttu-id="a3270-107">U wordt ook voorbereiden voor uw API groeiende door integratie met Azure Functions-proxy's en het instellen van mock-API's.</span><span class="sxs-lookup"><span data-stu-id="a3270-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="a3270-108">Dit alles wordt gerealiseerd boven op de compute-functies zonder server omgeving, zodat u geen zorgen te hoeven maken over het schalen van resources - u kunt alleen zich richten op uw API-logica.</span><span class="sxs-lookup"><span data-stu-id="a3270-108">All of this is accomplished on top of the Functions serverless compute environment, so you don't have to worry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3270-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a3270-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="a3270-110">De resulterende functie wordt gebruikt voor de rest van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a3270-110">The resulting function will be used for the rest of this tutorial.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="a3270-111">Aanmelden bij Azure</span><span class="sxs-lookup"><span data-stu-id="a3270-111">Sign in to Azure</span></span>

<span data-ttu-id="a3270-112">Open de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a3270-112">Open the Azure portal.</span></span> <span data-ttu-id="a3270-113">Om dit te doen, moet u zich aanmelden bij [https://portal.azure.com](https://portal.azure.com) met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a3270-113">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="a3270-114">Aanpassen van uw HTTP-functie</span><span class="sxs-lookup"><span data-stu-id="a3270-114">Customize your HTTP function</span></span>

<span data-ttu-id="a3270-115">Uw HTTP-geactiveerde-functie is standaard geconfigureerd voor het accepteren van een HTTP-methode.</span><span class="sxs-lookup"><span data-stu-id="a3270-115">By default, your HTTP-triggered function is configured to accept any HTTP method.</span></span> <span data-ttu-id="a3270-116">Er is ook een standaard-URL van het formulier `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="a3270-116">There is also a default URL of the form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="a3270-117">Als u de Quick Start, vervolgens gevolgd `<funcname>` waarschijnlijk ziet er ongeveer zo 'HttpTriggerJS1'.</span><span class="sxs-lookup"><span data-stu-id="a3270-117">If you followed the quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="a3270-118">In deze sectie, wijzigt u de functie zodat deze alleen reageert op GET-aanvragen op basis van `/api/hello` in plaats daarvan te routeren.</span><span class="sxs-lookup"><span data-stu-id="a3270-118">In this section, you will modify the function to respond only to GET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="a3270-119">Navigeer naar de functie in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a3270-119">Navigate to your function in the Azure portal.</span></span> <span data-ttu-id="a3270-120">Selecteer **integreren** in de linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="a3270-120">Select **Integrate** in the left navigation.</span></span>

![Aanpassen van een HTTP-functie](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="a3270-122">Gebruik de instellingen van de HTTP-trigger zoals opgegeven in de tabel.</span><span class="sxs-lookup"><span data-stu-id="a3270-122">Use the HTTP trigger settings as specified in the table.</span></span>

| <span data-ttu-id="a3270-123">Veld</span><span class="sxs-lookup"><span data-stu-id="a3270-123">Field</span></span> | <span data-ttu-id="a3270-124">Voorbeeldwaarde</span><span class="sxs-lookup"><span data-stu-id="a3270-124">Sample value</span></span> | <span data-ttu-id="a3270-125">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a3270-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="a3270-126">Toegestane HTTP-methoden</span><span class="sxs-lookup"><span data-stu-id="a3270-126">Allowed HTTP methods</span></span> | <span data-ttu-id="a3270-127">Geselecteerde methoden</span><span class="sxs-lookup"><span data-stu-id="a3270-127">Selected methods</span></span> | <span data-ttu-id="a3270-128">Hiermee wordt bepaald welke HTTP-methoden kunnen worden gebruikt voor deze functie aanroepen</span><span class="sxs-lookup"><span data-stu-id="a3270-128">Determines what HTTP methods may be used to invoke this function</span></span> |
| <span data-ttu-id="a3270-129">Geselecteerde HTTP-methoden</span><span class="sxs-lookup"><span data-stu-id="a3270-129">Selected HTTP methods</span></span> | <span data-ttu-id="a3270-130">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="a3270-130">GET</span></span> | <span data-ttu-id="a3270-131">Hiermee kunt u alleen geselecteerde HTTP-methoden moeten worden gebruikt voor deze functie aanroepen</span><span class="sxs-lookup"><span data-stu-id="a3270-131">Allows only selected HTTP methods to be used to invoke this function</span></span> |
| <span data-ttu-id="a3270-132">Routesjabloon</span><span class="sxs-lookup"><span data-stu-id="a3270-132">Route template</span></span> | <span data-ttu-id="a3270-133">uit</span><span class="sxs-lookup"><span data-stu-id="a3270-133">/hello</span></span> | <span data-ttu-id="a3270-134">Bepaalt welke route wordt gebruikt voor deze functie aanroepen</span><span class="sxs-lookup"><span data-stu-id="a3270-134">Determines what route is used to invoke this function</span></span> |

<span data-ttu-id="a3270-135">Opmerking die u niet de `/api` pad-voorvoegsel op in de Routesjabloon baseren als dit wordt verwerkt door een algemene instelling.</span><span class="sxs-lookup"><span data-stu-id="a3270-135">Note that you did not include the `/api` base path prefix in the route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="a3270-136">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a3270-136">Click **Save**.</span></span>

<span data-ttu-id="a3270-137">U kunt meer informatie over het aanpassen van HTTP-functies in [bindingen van Azure Functions HTTP- en webhook](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="a3270-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="a3270-138">Uw API testen</span><span class="sxs-lookup"><span data-stu-id="a3270-138">Test your API</span></span>

<span data-ttu-id="a3270-139">De functie voor het werken met de nieuwe API-gebied vervolgens testen.</span><span class="sxs-lookup"><span data-stu-id="a3270-139">Next, test your function to see it working with the new API surface.</span></span>

<span data-ttu-id="a3270-140">Ga terug naar de pagina ontwikkeling door te klikken op de functienaam in de linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="a3270-140">Navigate back to the development page by clicking on the function's name in the left navigation.</span></span>

<span data-ttu-id="a3270-141">Klik op **ophalen van de functie URL** en kopieer de URL.</span><span class="sxs-lookup"><span data-stu-id="a3270-141">Click **Get function URL** and copy the URL.</span></span> <span data-ttu-id="a3270-142">U ziet dat deze gebruikmaakt van de `/api/hello` nu routeren.</span><span class="sxs-lookup"><span data-stu-id="a3270-142">You should see that it uses the `/api/hello` route now.</span></span>

<span data-ttu-id="a3270-143">Kopieer de URL naar een nieuw browsertabblad of uw voorkeur REST-client.</span><span class="sxs-lookup"><span data-stu-id="a3270-143">Copy the URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="a3270-144">Browsers wordt GET standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a3270-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="a3270-145">De functie uitvoeren en controleren of deze werkt.</span><span class="sxs-lookup"><span data-stu-id="a3270-145">Run the function and confirm that it is working.</span></span> <span data-ttu-id="a3270-146">Mogelijk moet u de parameter 'name' opgeven als een queryreeks om te voldoen aan de Quick Start-code.</span><span class="sxs-lookup"><span data-stu-id="a3270-146">You may need to provide the "name" parameter as a query string to satisfy the quickstart code.</span></span>

<span data-ttu-id="a3270-147">U kunt ook proberen het aanroepen van het eindpunt met een andere HTTP-methode om te bevestigen dat de functie niet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a3270-147">You can also try calling the endpoint with another HTTP method to confirm that the function is not executed.</span></span> <span data-ttu-id="a3270-148">Hiervoor moet u een REST-client, zoals cURL, Postman of Fiddler gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a3270-148">For this, you will need to use a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="a3270-149">Overzicht van proxy 's</span><span class="sxs-lookup"><span data-stu-id="a3270-149">Proxies overview</span></span>

<span data-ttu-id="a3270-150">U kunt uw API via een proxy wordt surface in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="a3270-150">In the next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="a3270-151">Azure Functions-proxy's is een preview-functie waarmee u aanvragen doorsturen naar andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="a3270-151">Azure Functions Proxies is a preview feature that allows you to forward requests to other resources.</span></span> <span data-ttu-id="a3270-152">U definieert een HTTP-eindpunt net zoals met HTTP-trigger, maar in plaats van het schrijven van code voor het uitvoeren als dat eindpunt wordt aangeroepen, u een URL naar een externe implementatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="a3270-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code to execute when that endpoint is called, you provide a URL to a remote implementation.</span></span> <span data-ttu-id="a3270-153">Hiermee kunt u meerdere API bronnen in één API-gebied op die clients gebruiken voor eenvoudige opstellen.</span><span class="sxs-lookup"><span data-stu-id="a3270-153">This allows you to compose multiple API sources into a single API surface which is easy for clients to consume.</span></span> <span data-ttu-id="a3270-154">Dit is vooral handig als u wilt maken van uw API als microservices.</span><span class="sxs-lookup"><span data-stu-id="a3270-154">This is particularly useful if you wish to build your API as microservices.</span></span>

<span data-ttu-id="a3270-155">Een proxy kan verwijzen naar een HTTP-resource, zoals:</span><span class="sxs-lookup"><span data-stu-id="a3270-155">A proxy can point to any HTTP resource, such as:</span></span>
- <span data-ttu-id="a3270-156">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a3270-156">Azure Functions</span></span> 
- <span data-ttu-id="a3270-157">API-apps in [-Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="a3270-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="a3270-158">Docker-containers in [op Linux-App Service](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="a3270-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="a3270-159">Andere gehoste API</span><span class="sxs-lookup"><span data-stu-id="a3270-159">Any other hosted API</span></span>

<span data-ttu-id="a3270-160">Zie voor meer informatie over proxy's, [werken met Azure Functions-proxy's (preview)].</span><span class="sxs-lookup"><span data-stu-id="a3270-160">To learn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="a3270-161">Uw eerste proxy maken</span><span class="sxs-lookup"><span data-stu-id="a3270-161">Create your first proxy</span></span>

<span data-ttu-id="a3270-162">In deze sectie maakt u een nieuwe proxy die als een frontend naar uw algehele API fungeert.</span><span class="sxs-lookup"><span data-stu-id="a3270-162">In this section, you will create a new proxy which serves as a frontend to your overall API.</span></span> 

### <a name="setting-up-the-frontend-environment"></a><span data-ttu-id="a3270-163">De frontend-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="a3270-163">Setting up the frontend environment</span></span>

<span data-ttu-id="a3270-164">Herhaal de stappen voor het [maken van een functie-app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) voor het maken van een nieuwe functie-app waarin u uw proxy maakt.</span><span class="sxs-lookup"><span data-stu-id="a3270-164">Repeat the steps to [Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) to create a new function app in which you will create your proxy.</span></span> <span data-ttu-id="a3270-165">Deze nieuwe app fungeert als de frontend voor onze API en de functie-app die u eerder hebt bewerkt fungeert als een back-end.</span><span class="sxs-lookup"><span data-stu-id="a3270-165">This new app will serve as the frontend for our API, and the function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="a3270-166">Navigeer naar uw nieuwe frontend functie-app in de portal.</span><span class="sxs-lookup"><span data-stu-id="a3270-166">Navigate to your new frontend function app in the portal.</span></span>

<span data-ttu-id="a3270-167">Selecteer **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="a3270-167">Select **Settings**.</span></span> <span data-ttu-id="a3270-168">Klik in-of uitschakelen **inschakelen Azure Functions-proxy's (preview)** naar 'Op'.</span><span class="sxs-lookup"><span data-stu-id="a3270-168">Then toggle **Enable Azure Functions Proxies (preview)** to "On".</span></span>

<span data-ttu-id="a3270-169">Selecteer **Platform instellingen** en kies **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="a3270-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="a3270-170">Schuif omlaag naar **appinstellingen** en maak een nieuwe instelling met sleutel 'HELLO_HOST'.</span><span class="sxs-lookup"><span data-stu-id="a3270-170">Scroll down to **App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="a3270-171">Stel de waarde voor de host van uw back-end-functie-app, zoals `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="a3270-171">Set its value to the host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="a3270-172">Dit is onderdeel van de URL die u eerder hebt gekopieerd bij het testen van uw HTTP-functie.</span><span class="sxs-lookup"><span data-stu-id="a3270-172">This is part of the URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="a3270-173">U moet deze instelling in de configuratie later naar verwijzen.</span><span class="sxs-lookup"><span data-stu-id="a3270-173">You'll reference this setting in the configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="a3270-174">App-instellingen worden aanbevolen voor de configuratie van de host om te voorkomen dat een afhankelijkheid vastgelegde omgeving voor de proxy.</span><span class="sxs-lookup"><span data-stu-id="a3270-174">App settings are recommended for the host configuration to prevent a hard-coded environment dependency for the proxy.</span></span> <span data-ttu-id="a3270-175">Met behulp van appinstellingen, betekent dat u de proxyconfiguratie tussen omgevingen verplaatsen kunt en de omgeving-specifieke app-instellingen worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="a3270-175">Using app settings means that you can move the proxy configuration between environments, and the environment-specific app settings will be applied.</span></span>

<span data-ttu-id="a3270-176">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a3270-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-the-frontend"></a><span data-ttu-id="a3270-177">Maken van een proxy op de frontend</span><span class="sxs-lookup"><span data-stu-id="a3270-177">Creating a proxy on the frontend</span></span>

<span data-ttu-id="a3270-178">Ga terug naar uw frontend-functie-app in de portal.</span><span class="sxs-lookup"><span data-stu-id="a3270-178">Navigate back to your frontend function app in the portal.</span></span>

<span data-ttu-id="a3270-179">Klik op het plusteken in de linkernavigatiebalk '+' naast 'Proxy's (preview)'.</span><span class="sxs-lookup"><span data-stu-id="a3270-179">In the left-hand navigation, click the plus sign '+' next to "Proxies (preview)".</span></span>

![Maken van een proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="a3270-181">Proxy-instellingen gebruiken die zijn opgegeven in de tabel.</span><span class="sxs-lookup"><span data-stu-id="a3270-181">Use proxy settings as specified in the table.</span></span>

| <span data-ttu-id="a3270-182">Veld</span><span class="sxs-lookup"><span data-stu-id="a3270-182">Field</span></span> | <span data-ttu-id="a3270-183">Voorbeeldwaarde</span><span class="sxs-lookup"><span data-stu-id="a3270-183">Sample value</span></span> | <span data-ttu-id="a3270-184">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a3270-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="a3270-185">Naam</span><span class="sxs-lookup"><span data-stu-id="a3270-185">Name</span></span> | <span data-ttu-id="a3270-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="a3270-186">HelloProxy</span></span> | <span data-ttu-id="a3270-187">Een beschrijvende naam wordt alleen gebruikt voor beheer</span><span class="sxs-lookup"><span data-stu-id="a3270-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="a3270-188">Routesjabloon</span><span class="sxs-lookup"><span data-stu-id="a3270-188">Route template</span></span> | <span data-ttu-id="a3270-189">/ api/Hallo</span><span class="sxs-lookup"><span data-stu-id="a3270-189">/api/hello</span></span> | <span data-ttu-id="a3270-190">Bepaalt welke route wordt gebruikt om aan te roepen via deze proxy</span><span class="sxs-lookup"><span data-stu-id="a3270-190">Determines what route is used to invoke this proxy</span></span> |
| <span data-ttu-id="a3270-191">Back-end-URL</span><span class="sxs-lookup"><span data-stu-id="a3270-191">Backend URL</span></span> | <span data-ttu-id="a3270-192">https://%HELLO_HOST%/API/Hello</span><span class="sxs-lookup"><span data-stu-id="a3270-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="a3270-193">Hiermee geeft u het eindpunt waarop de aanvraag via proxy moet</span><span class="sxs-lookup"><span data-stu-id="a3270-193">Specifies the endpoint to which the request should be proxied</span></span> |

<span data-ttu-id="a3270-194">Let op proxy's zorgt niet voor de `/api` basispad voorvoegsel en deze moet worden opgenomen in de Routesjabloon.</span><span class="sxs-lookup"><span data-stu-id="a3270-194">Note that Proxies does not provide the `/api` base path prefix, and this must be included in the route template.</span></span>

<span data-ttu-id="a3270-195">De `%HELLO_HOST%` syntaxis wordt verwezen naar de app-instelling die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a3270-195">The `%HELLO_HOST%` syntax will reference the app setting you created earlier.</span></span> <span data-ttu-id="a3270-196">De opgelost URL verwijst naar de oorspronkelijke functie.</span><span class="sxs-lookup"><span data-stu-id="a3270-196">The resolved URL will point to your original function.</span></span>

<span data-ttu-id="a3270-197">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a3270-197">Click **Create**.</span></span>

<span data-ttu-id="a3270-198">U kunt uw nieuwe proxy uitproberen door te kopiëren van de Proxy-URL en testen van het in de browser of met uw favoriete HTTP-client.</span><span class="sxs-lookup"><span data-stu-id="a3270-198">You can try out your new proxy by copying the Proxy URL and testing it in the browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="a3270-199">Een mock-API maken</span><span class="sxs-lookup"><span data-stu-id="a3270-199">Create a mock API</span></span>

<span data-ttu-id="a3270-200">Vervolgens gebruikt u een proxy voor het maken van een mock-API voor uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="a3270-200">Next, you will use a proxy to create a mock API for your solution.</span></span> <span data-ttu-id="a3270-201">Hierdoor kunnen client-ontwikkeling voor de voortgang, zonder dat de back-end volledig geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a3270-201">This allows client development to progress, without needing the backend fully implemented.</span></span> <span data-ttu-id="a3270-202">Verderop in ontwikkeling, kan u een nieuwe functie-app die ondersteuning biedt voor deze logica maken en uw proxy omleiden naar deze.</span><span class="sxs-lookup"><span data-stu-id="a3270-202">Later in development, you could create a new function app which supports this logic and redirect your proxy to it.</span></span>

<span data-ttu-id="a3270-203">Voor het maken van deze mock-API maken we een nieuwe proxy deze tijd met de [App Service-Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="a3270-203">To create this mock API, we will create a new proxy, this time using the [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="a3270-204">Navigeer naar de functie-app in de portal om te beginnen.</span><span class="sxs-lookup"><span data-stu-id="a3270-204">To get started, navigate to your function app in the portal.</span></span> <span data-ttu-id="a3270-205">Selecteer **platformfuncties** en zoek **App Service-Editor**.</span><span class="sxs-lookup"><span data-stu-id="a3270-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="a3270-206">Als u dit opent u de App Service-Editor in een nieuw tabblad.</span><span class="sxs-lookup"><span data-stu-id="a3270-206">Clicking this will open the App Service Editor in a new tab.</span></span>

<span data-ttu-id="a3270-207">Selecteer `proxies.json` in de linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="a3270-207">Select `proxies.json` in the left navigation.</span></span> <span data-ttu-id="a3270-208">Dit is het bestand waarin de configuratie voor al uw proxy's worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a3270-208">This is the file which stores the configuration for all of your proxies.</span></span> <span data-ttu-id="a3270-209">Als u een van de [fungeert implementatiemethoden](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), dit is het bestand dat u in bronbeheer wordt onderhouden.</span><span class="sxs-lookup"><span data-stu-id="a3270-209">If you use one of the [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is the file you will maintain in source control.</span></span> <span data-ttu-id="a3270-210">Zie voor meer informatie over dit bestand, [proxy's geavanceerde configuratie](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="a3270-210">To learn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="a3270-211">Als u tot nu toe hebt opgevolgd langs, worden uw proxies.json moet eruitzien als in het volgende:</span><span class="sxs-lookup"><span data-stu-id="a3270-211">If you've followed along so far, your proxies.json should look like the following:</span></span>

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

<span data-ttu-id="a3270-212">Vervolgens voegt u uw mock-API.</span><span class="sxs-lookup"><span data-stu-id="a3270-212">Next you'll add your mock API.</span></span> <span data-ttu-id="a3270-213">Vervang uw proxies.json-bestand met de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="a3270-213">Replace your proxies.json file with the following:</span></span>

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

<span data-ttu-id="a3270-214">Hiermee wordt een nieuwe proxy 'GetUserByName', zonder de eigenschap backendUri toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a3270-214">This adds a new proxy, "GetUserByName", without the backendUri property.</span></span> <span data-ttu-id="a3270-215">In plaats van een andere resource aanroept, wordt het standaardantwoord van proxy's met een onderdrukking antwoord gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a3270-215">Instead of calling another resource, it modifies the default response from Proxies using a response override.</span></span> <span data-ttu-id="a3270-216">Aanvraag en -antwoord onderdrukkingen kunnen ook worden gebruikt in combinatie met een back-end-URL.</span><span class="sxs-lookup"><span data-stu-id="a3270-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="a3270-217">Dit is vooral handig als proxy voor een oudere systeem, waarin u mogelijk wilt wijzigen, kopteksten, query's parameters, enzovoort. Zie voor meer informatie over aanvraag- en onderdrukkingen, [wijzigen aanvragen en antwoorden in de proxy's](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="a3270-217">This is particularly useful when proxying to a legacy system, where you might need to modify headers, query parameters, etc. To learn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="a3270-218">Uw mock API testen door het aanroepen van de `/api/users/{username}` -eindpunt met een browser of uw favoriete REST-client.</span><span class="sxs-lookup"><span data-stu-id="a3270-218">Test your mock API by calling the `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="a3270-219">Zorg ervoor dat u _{username}_ met de waarde van een tekenreeks die een gebruikersnaam vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="a3270-219">Be sure to replace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3270-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3270-220">Next steps</span></span>

<span data-ttu-id="a3270-221">In deze zelfstudie hebt u geleerd hoe ontwikkelen en aanpassen van een API van Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a3270-221">In this tutorial, you learned how to build and customize an API on Azure Functions.</span></span> <span data-ttu-id="a3270-222">U hebt ook geleerd hoe om meerdere API's, inclusief mocks, samenwerken als een geïntegreerde API-gebied.</span><span class="sxs-lookup"><span data-stu-id="a3270-222">You also learned how to bring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="a3270-223">U kunt deze technieken gebruiken voor het bouwen van API's van elk complexiteit alle tijdens de uitvoering van het model zonder server compute verstrekt door Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a3270-223">You can use these techniques to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="a3270-224">De volgende verwijzingen te helpen bij het ontwikkelen van uw API verder:</span><span class="sxs-lookup"><span data-stu-id="a3270-224">The following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="a3270-225">Azure Functions HTTP- en webhook bindingen</span><span class="sxs-lookup"><span data-stu-id="a3270-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="a3270-226">[werken met Azure Functions-proxy's (preview)]</span><span class="sxs-lookup"><span data-stu-id="a3270-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="a3270-227">Een Azure-functies-API (preview) documenteren</span><span class="sxs-lookup"><span data-stu-id="a3270-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[werken met Azure Functions-proxy's (preview)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
