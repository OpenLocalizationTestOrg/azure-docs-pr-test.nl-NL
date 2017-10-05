---
title: Configureren van Azure functie App-instellingen | Microsoft Docs
description: Informatie over het configureren van Azure functie app-instellingen.
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 3b23011f66592151d517d61bf806da8743f38e03
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-manage-a-function-app-in-the-azure-portal"></a><span data-ttu-id="53b1e-103">Het beheren van een functie-app in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="53b1e-103">How to manage a function app in the Azure portal</span></span> 

<span data-ttu-id="53b1e-104">In de Azure Functions biedt een functie-app de uitvoeringscontext voor uw afzonderlijke functies.</span><span class="sxs-lookup"><span data-stu-id="53b1e-104">In Azure Functions, a function app provides the execution context for your individual functions.</span></span> <span data-ttu-id="53b1e-105">De functie app-gedrag van toepassing op alle functies die worden gehost door een bepaalde functie-app.</span><span class="sxs-lookup"><span data-stu-id="53b1e-105">Function app behaviors apply to all functions hosted by a given function app.</span></span> <span data-ttu-id="53b1e-106">In dit onderwerp wordt beschreven hoe configureren en beheren van uw apps functie in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="53b1e-106">This topic describes how to configure and manage your function apps in the Azure portal.</span></span>

<span data-ttu-id="53b1e-107">Om te beginnen, gaat u naar de [Azure-portal](http://portal.azure.com) en meld u aan bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="53b1e-107">To begin, go to the [Azure portal](http://portal.azure.com) and sign in to your Azure account.</span></span> <span data-ttu-id="53b1e-108">Typ de naam van uw functie-app in de zoekbalk boven in de portal en selecteer deze in de lijst.</span><span class="sxs-lookup"><span data-stu-id="53b1e-108">In the search bar at the top of the portal, type the name of your function app and select it from the list.</span></span> <span data-ttu-id="53b1e-109">Na het selecteren van de functie-app, ziet u de volgende pagina:</span><span class="sxs-lookup"><span data-stu-id="53b1e-109">After selecting your function app, you see the following page:</span></span>

![Overzicht van de functie-app in de Azure portal](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="53b1e-111"><a name="manage-app-service-settings"></a>Tabblad voor de functie app-instellingen</span><span class="sxs-lookup"><span data-stu-id="53b1e-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Overzicht van de functie app in de Azure portal.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="53b1e-113">De **instellingen** tabblad is waarin u de functies runtime-versie die wordt gebruikt door de functie-app kunt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="53b1e-113">The **Settings** tab is where you can update the Functions runtime version used by your function app.</span></span> <span data-ttu-id="53b1e-114">Het is ook waar u de sleutels van de host gebruikt voor het beperken van HTTP-toegang tot alle functies die worden gehost door de functie-app beheren.</span><span class="sxs-lookup"><span data-stu-id="53b1e-114">It is also where you manage the host keys used to restrict HTTP access to all functions hosted by the function app.</span></span>

<span data-ttu-id="53b1e-115">Functies ondersteunt zowel verbruik die als host fungeert als App Service-hostingplannen.</span><span class="sxs-lookup"><span data-stu-id="53b1e-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="53b1e-116">Zie voor meer informatie [Kies de juiste service-abonnement voor Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="53b1e-116">For more information, see [Choose the correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="53b1e-117">Voor betere voorspelbaarheid in het plan verbruik functies kunt u platform-gebruik beperken door een dagelijkse gebruiksquotum instellen in gigabytes seconden.</span><span class="sxs-lookup"><span data-stu-id="53b1e-117">For better predictability in the Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="53b1e-118">Zodra de dagelijkse gebruiksquotum is bereikt, wordt de functie-app is gestopt.</span><span class="sxs-lookup"><span data-stu-id="53b1e-118">Once the daily usage quota is reached, the function app is stopped.</span></span> <span data-ttu-id="53b1e-119">Een functie-app gestopt als gevolg van de quota voor bestedingslimiet bereikt kan opnieuw worden ingeschakeld vanuit de context hetzelfde als het tot stand brengen van de dagelijkse quotum uitgaven zijn.</span><span class="sxs-lookup"><span data-stu-id="53b1e-119">A function app stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span></span> <span data-ttu-id="53b1e-120">Zie de [Azure Functions pagina met prijzen](http://azure.microsoft.com/pricing/details/functions/) voor meer informatie over de facturering.</span><span class="sxs-lookup"><span data-stu-id="53b1e-120">See the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="53b1e-121">Tabblad voor platform-onderdelen</span><span class="sxs-lookup"><span data-stu-id="53b1e-121">Platform features tab</span></span>

![De functie app platform functies tabblad.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="53b1e-123">Functie apps in uitgevoerd en worden beheerd, door de Azure App Service-platform.</span><span class="sxs-lookup"><span data-stu-id="53b1e-123">Function apps run in, and are maintained, by the Azure App Service platform.</span></span> <span data-ttu-id="53b1e-124">Als zodanig hebben uw functie apps toegang tot de meeste van de functies van Azure core webhosting-platform.</span><span class="sxs-lookup"><span data-stu-id="53b1e-124">As such, your function apps have access to most of the features of Azure's core web hosting platform.</span></span> <span data-ttu-id="53b1e-125">De **platformfuncties** tabblad is waar u de vele nieuwe functies van de App Service-platform die u in uw apps functie gebruiken kunt toegang.</span><span class="sxs-lookup"><span data-stu-id="53b1e-125">The **Platform features** tab is where you access the many features of the App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="53b1e-126">Niet alle App Service-functies zijn beschikbaar wanneer een functie-app wordt uitgevoerd op het verbruik hosting-plan.</span><span class="sxs-lookup"><span data-stu-id="53b1e-126">Not all App Service features are available when a function app runs on the Consumption hosting plan.</span></span>

<span data-ttu-id="53b1e-127">De rest van dit onderwerp richt zich op de volgende App Service-functies in de Azure-portal die handig voor functies zijn:</span><span class="sxs-lookup"><span data-stu-id="53b1e-127">The rest of this topic focuses on the following App Service features in the Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="53b1e-128">App Service-editor</span><span class="sxs-lookup"><span data-stu-id="53b1e-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="53b1e-129">Toepassingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="53b1e-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="53b1e-130">Console</span><span class="sxs-lookup"><span data-stu-id="53b1e-130">Console</span></span>](#console)
+ [<span data-ttu-id="53b1e-131">Geavanceerde tools (Kudu)</span><span class="sxs-lookup"><span data-stu-id="53b1e-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="53b1e-132">Implementatie-opties</span><span class="sxs-lookup"><span data-stu-id="53b1e-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="53b1e-133">CORS</span><span class="sxs-lookup"><span data-stu-id="53b1e-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="53b1e-134">Verificatie</span><span class="sxs-lookup"><span data-stu-id="53b1e-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="53b1e-135">API-definitie</span><span class="sxs-lookup"><span data-stu-id="53b1e-135">API definition</span></span>](#swagger)

<span data-ttu-id="53b1e-136">Zie voor meer informatie over het werken met App Service-instellingen, [Azure App Service-instellingen configureren](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="53b1e-136">For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="53b1e-137"><a name="editor"></a>App Service-Editor</span><span class="sxs-lookup"><span data-stu-id="53b1e-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![De functie app-App Service-editor.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="53b1e-139">De App Service-editor is een geavanceerde in de portal-editor die u gebruiken kunt om JSON-configuratiebestanden en codebestanden die met te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="53b1e-139">The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike.</span></span> <span data-ttu-id="53b1e-140">Als u deze optie kiest, wordt een afzonderlijke browsertabblad met een basic-editor gestart.</span><span class="sxs-lookup"><span data-stu-id="53b1e-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="53b1e-141">Hiermee kunt u integreren met de Git-opslagplaats, uitvoeren en foutopsporing van code en de functie app-instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="53b1e-141">This enables you to integrate with the Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="53b1e-142">Deze editor biedt een verbeterde development environment voor uw functies vergeleken met de standaardblade voor de functie-app.</span><span class="sxs-lookup"><span data-stu-id="53b1e-142">This editor provides an enhanced development environment for your functions compared with the default function app blade.</span></span>    |

![De App Service-editor](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="53b1e-144"><a name="settings"></a>Toepassingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="53b1e-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Toepassingsinstellingen voor functie-app.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="53b1e-146">De App Service **toepassingsinstellingen** blade is waar u configureren en beheren van de framework-versies, foutopsporing op afstand, app-instellingen en verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="53b1e-146">The App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="53b1e-147">Wanneer u de functie-app met andere Azure en services van derden integreren, kunt u deze instellingen hier wijzigen.</span><span class="sxs-lookup"><span data-stu-id="53b1e-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Configureer toepassingsinstellingen](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="53b1e-149"><a name="console"></a>Console</span><span class="sxs-lookup"><span data-stu-id="53b1e-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![De functie app-console in de Azure portal](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="53b1e-151">De console in de portal is een hulpprogramma developer ideaal als u liever om te communiceren met de functie-app vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="53b1e-151">The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line.</span></span> <span data-ttu-id="53b1e-152">Veelgebruikte opdrachten zijn directory en maken van het bestand en navigatie, evenals batch-bestanden en scripts uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="53b1e-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![De functie app-console](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="53b1e-154"><a name="kudu"></a>Geavanceerde tools (Kudu)</span><span class="sxs-lookup"><span data-stu-id="53b1e-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Functie-app Kudu in de Azure portal](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="53b1e-156">De geavanceerde hulpprogramma's voor App Service (ook wel bekend als Kudu) bieden toegang tot geavanceerde beheerfuncties van uw app in de functie.</span><span class="sxs-lookup"><span data-stu-id="53b1e-156">The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app.</span></span> <span data-ttu-id="53b1e-157">U beheert van kudu bovendien, systeemgegevens, app-instellingen, omgevingsvariabelen, site-uitbreidingen, HTTP-headers en servervariabelen.</span><span class="sxs-lookup"><span data-stu-id="53b1e-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="53b1e-158">U kunt ook starten **Kudu** door te bladeren naar het eindpunt SCM voor uw app in de functie, zoals`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="53b1e-158">You can also launch **Kudu** by browsing to the SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Kudu configureren](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="53b1e-160"><a name="deployment">Implementatie-opties</span><span class="sxs-lookup"><span data-stu-id="53b1e-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Opties voor de functie app-implementatie in de Azure portal](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="53b1e-162">Functies kunt u uw functiecode op uw lokale machine ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="53b1e-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="53b1e-163">Vervolgens kunt u uw lokale functie app-project uploaden naar Azure.</span><span class="sxs-lookup"><span data-stu-id="53b1e-163">You can then upload your local function app project to Azure.</span></span> <span data-ttu-id="53b1e-164">Naast het uploaden van de traditionele FTP-functies kunt u een functie-app met populaire continue integratie-oplossingen zoals GitHub, VSTS Dropbox, Bitbucket en anderen implementeren.</span><span class="sxs-lookup"><span data-stu-id="53b1e-164">In addition to traditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="53b1e-165">Zie voor meer informatie [continue implementatie voor Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="53b1e-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="53b1e-166">Als u wilt uploaden handmatig met behulp van FTP- of lokale Git, moet u ook [configureren van de referenties voor uw implementatie](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="53b1e-166">To upload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="53b1e-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="53b1e-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Functie-app CORS in de Azure portal](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="53b1e-169">Om te voorkomen dat schadelijke code wordt uitgevoerd in uw services, blokkeert App Service aanroepen naar uw apps functie van externe bronnen.</span><span class="sxs-lookup"><span data-stu-id="53b1e-169">To prevent malicious code execution in your services, App Service blocks calls to your function apps from external sources.</span></span> <span data-ttu-id="53b1e-170">Functies biedt ondersteuning voor cross-origin-resource delen (CORS) zodat u het definiëren van een 'whitelist' toegestane oorsprongen waarvan van uw functies kunnen externe aanvragen accepteert.</span><span class="sxs-lookup"><span data-stu-id="53b1e-170">Functions supports cross-origin resource sharing (CORS) to let you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Functie-App configureren CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="53b1e-172"><a name="auth"></a>Verificatie</span><span class="sxs-lookup"><span data-stu-id="53b1e-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Verificatie van de functie app in de Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="53b1e-174">Wanneer functies een HTTP-trigger gebruikt, kunt u vereisen aanroepen voor het eerst worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="53b1e-174">When functions use an HTTP trigger, you can require calls to first be authenticated.</span></span> <span data-ttu-id="53b1e-175">App Service biedt ondersteuning voor Azure Active Directory-verificatie en meld u aan met sociale providers, zoals Microsoft, Facebook en Twitter.</span><span class="sxs-lookup"><span data-stu-id="53b1e-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="53b1e-176">Zie voor meer informatie over het configureren van specifieke verificatieproviders [overzicht van Azure App Service-authenticatie](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="53b1e-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Verificatie voor een functie-app configureren](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="53b1e-178"><a name="swagger"></a>API-definitie</span><span class="sxs-lookup"><span data-stu-id="53b1e-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![De functie app API swagger-definitie in de Azure portal](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="53b1e-180">Functies biedt ondersteuning voor Swagger wilt toestaan dat clients eenvoudiger uw HTTP-geactiveerde functies gebruiken.</span><span class="sxs-lookup"><span data-stu-id="53b1e-180">Functions supports Swagger to allow clients to more easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="53b1e-181">Bezoek voor meer informatie over het maken van API-definities met Swagger [aan de slag met API-Apps, ASP.NET en Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="53b1e-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="53b1e-182">U kunt ook functies proxy's gebruiken voor het definiëren van een één API-gebied voor meerdere functies.</span><span class="sxs-lookup"><span data-stu-id="53b1e-182">You can also use Functions Proxies to define a single API surface for multiple functions.</span></span> <span data-ttu-id="53b1e-183">Zie voor meer informatie [werken met Azure Functions-proxy's](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="53b1e-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![API voor functie-App configureren](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="53b1e-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="53b1e-185">Next steps</span></span>

+ [<span data-ttu-id="53b1e-186">Azure App Service-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="53b1e-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="53b1e-187">Doorlopende implementatie voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="53b1e-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



