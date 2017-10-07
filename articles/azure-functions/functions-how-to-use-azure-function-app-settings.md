---
title: aaaConfigure Azure functie App-instellingen | Microsoft Docs
description: Meer informatie over hoe de app-instellingen voor het functioneren van tooconfigure Azure.
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
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a><span data-ttu-id="7cf67-103">Hoe toomanage een functie-app in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="7cf67-103">How toomanage a function app in hello Azure portal</span></span> 

<span data-ttu-id="7cf67-104">In de Azure Functions biedt een functie-app Hallo uitvoeringscontext voor uw afzonderlijke functies.</span><span class="sxs-lookup"><span data-stu-id="7cf67-104">In Azure Functions, a function app provides hello execution context for your individual functions.</span></span> <span data-ttu-id="7cf67-105">De functie app-gedrag van toepassing tooall functies gehost door een bepaalde functie-app.</span><span class="sxs-lookup"><span data-stu-id="7cf67-105">Function app behaviors apply tooall functions hosted by a given function app.</span></span> <span data-ttu-id="7cf67-106">Dit onderwerp wordt beschreven hoe tooconfigure en beheren van uw apps functie in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7cf67-106">This topic describes how tooconfigure and manage your function apps in hello Azure portal.</span></span>

<span data-ttu-id="7cf67-107">toobegin, Ga toohello [Azure-portal](http://portal.azure.com) en meld u aan tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7cf67-107">toobegin, go toohello [Azure portal](http://portal.azure.com) and sign in tooyour Azure account.</span></span> <span data-ttu-id="7cf67-108">In de zoekbalk Hallo Hallo boven aan het Hallo-portal, typ Hallo-naam van de functie-app en selecteren in lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="7cf67-108">In hello search bar at hello top of hello portal, type hello name of your function app and select it from hello list.</span></span> <span data-ttu-id="7cf67-109">Na het selecteren van de functie-app, ziet u Hallo na pagina:</span><span class="sxs-lookup"><span data-stu-id="7cf67-109">After selecting your function app, you see hello following page:</span></span>

![Overzicht van de functie-app in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="7cf67-111"><a name="manage-app-service-settings"></a>Tabblad voor de functie app-instellingen</span><span class="sxs-lookup"><span data-stu-id="7cf67-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Overzicht van de functie app in hello Azure-portal.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="7cf67-113">Hallo **instellingen** tabblad is waarin u Hallo functies runtime-versie die wordt gebruikt door de functie-app kunt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7cf67-113">hello **Settings** tab is where you can update hello Functions runtime version used by your function app.</span></span> <span data-ttu-id="7cf67-114">Het is ook waar u Hallo host sleutels die worden gebruikt toorestrict HTTP tooall toegangsfuncties gehost door Hallo functie-app beheren.</span><span class="sxs-lookup"><span data-stu-id="7cf67-114">It is also where you manage hello host keys used toorestrict HTTP access tooall functions hosted by hello function app.</span></span>

<span data-ttu-id="7cf67-115">Functies ondersteunt zowel verbruik die als host fungeert als App Service-hostingplannen.</span><span class="sxs-lookup"><span data-stu-id="7cf67-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="7cf67-116">Zie voor meer informatie [Kies Hallo juiste service-plan voor Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="7cf67-116">For more information, see [Choose hello correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="7cf67-117">Voor betere voorspelbaarheid van Hallo verbruik plan functies kunt u platform-gebruik beperken door een dagelijkse gebruiksquotum instellen in gigabytes seconden.</span><span class="sxs-lookup"><span data-stu-id="7cf67-117">For better predictability in hello Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="7cf67-118">Zodra de dagelijkse gebruiksquotum Hallo is bereikt, is Hallo functie-app gestopt.</span><span class="sxs-lookup"><span data-stu-id="7cf67-118">Once hello daily usage quota is reached, hello function app is stopped.</span></span> <span data-ttu-id="7cf67-119">Een functie-app gestopt als gevolg van Hallo uitgaven quotum bereikt kan opnieuw worden ingeschakeld vanuit Hallo worden dezelfde context als dagelijks uitgaven quotum Hallo tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="7cf67-119">A function app stopped as a result of reaching hello spending quota can be re-enabled from hello same context as establishing hello daily spending quota.</span></span> <span data-ttu-id="7cf67-120">Zie Hallo [Azure Functions pagina met prijzen](http://azure.microsoft.com/pricing/details/functions/) voor meer informatie over de facturering.</span><span class="sxs-lookup"><span data-stu-id="7cf67-120">See hello [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="7cf67-121">Tabblad voor platform-onderdelen</span><span class="sxs-lookup"><span data-stu-id="7cf67-121">Platform features tab</span></span>

![De functie app platform functies tabblad.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="7cf67-123">Functie apps in uitgevoerd en worden beheerd, door hello Azure App Service-platform.</span><span class="sxs-lookup"><span data-stu-id="7cf67-123">Function apps run in, and are maintained, by hello Azure App Service platform.</span></span> <span data-ttu-id="7cf67-124">Als zodanig hebben uw apps functie toegang toomost van Hallo functies van Azure core webhosting-platform.</span><span class="sxs-lookup"><span data-stu-id="7cf67-124">As such, your function apps have access toomost of hello features of Azure's core web hosting platform.</span></span> <span data-ttu-id="7cf67-125">Hallo **platformfuncties** tabblad is waar u de toegang tot veel functies van App Service-platform die u in uw apps functie gebruiken kunt Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7cf67-125">hello **Platform features** tab is where you access hello many features of hello App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="7cf67-126">Niet alle App Service-functies zijn beschikbaar wanneer een functie-app wordt uitgevoerd op Hallo verbruik hosting plan.</span><span class="sxs-lookup"><span data-stu-id="7cf67-126">Not all App Service features are available when a function app runs on hello Consumption hosting plan.</span></span>

<span data-ttu-id="7cf67-127">Hallo rest van dit onderwerp richt zich op Hallo na App Service-functies in hello Azure-portal die handig zijn voor functies:</span><span class="sxs-lookup"><span data-stu-id="7cf67-127">hello rest of this topic focuses on hello following App Service features in hello Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="7cf67-128">App Service-editor</span><span class="sxs-lookup"><span data-stu-id="7cf67-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="7cf67-129">Toepassingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="7cf67-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="7cf67-130">Console</span><span class="sxs-lookup"><span data-stu-id="7cf67-130">Console</span></span>](#console)
+ [<span data-ttu-id="7cf67-131">Geavanceerde tools (Kudu)</span><span class="sxs-lookup"><span data-stu-id="7cf67-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="7cf67-132">Implementatie-opties</span><span class="sxs-lookup"><span data-stu-id="7cf67-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="7cf67-133">CORS</span><span class="sxs-lookup"><span data-stu-id="7cf67-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="7cf67-134">Verificatie</span><span class="sxs-lookup"><span data-stu-id="7cf67-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="7cf67-135">API-definitie</span><span class="sxs-lookup"><span data-stu-id="7cf67-135">API definition</span></span>](#swagger)

<span data-ttu-id="7cf67-136">Voor meer informatie over het toowork met App Service-instellingen, Zie [Azure App Service-instellingen configureren](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7cf67-136">For more information about how toowork with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="7cf67-137"><a name="editor"></a>App Service-Editor</span><span class="sxs-lookup"><span data-stu-id="7cf67-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![De functie app-App Service-editor.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="7cf67-139">Hallo-App Service-editor is een geavanceerde in de portal-editor die u toomodify JSON-configuratiebestanden en codebestanden hetzelfde gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="7cf67-139">hello App Service editor is an advanced in-portal editor that you can use toomodify JSON configuration files and code files alike.</span></span> <span data-ttu-id="7cf67-140">Als u deze optie kiest, wordt een afzonderlijke browsertabblad met een basic-editor gestart.</span><span class="sxs-lookup"><span data-stu-id="7cf67-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="7cf67-141">Dit kunt u toointegrate met Hallo Git-opslagplaats, uitvoeren en foutopsporing code en de functie app-instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7cf67-141">This enables you toointegrate with hello Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="7cf67-142">Deze editor biedt een verbeterde development environment voor uw functies vergeleken met de blade Hallo standaard functie-app.</span><span class="sxs-lookup"><span data-stu-id="7cf67-142">This editor provides an enhanced development environment for your functions compared with hello default function app blade.</span></span>    |

![Hallo-App Service-editor](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="7cf67-144"><a name="settings"></a>Toepassingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="7cf67-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Toepassingsinstellingen voor functie-app.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="7cf67-146">Hallo-App Service **toepassingsinstellingen** blade is waar u configureren en beheren van de framework-versies, foutopsporing op afstand, app-instellingen en verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="7cf67-146">hello App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="7cf67-147">Wanneer u de functie-app met andere Azure en services van derden integreren, kunt u deze instellingen hier wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7cf67-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Configureer toepassingsinstellingen](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="7cf67-149"><a name="console"></a>Console</span><span class="sxs-lookup"><span data-stu-id="7cf67-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![De functie app-console in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="7cf67-151">Hallo-portal-console is een hulpprogramma ideaal ontwikkelaar wanneer u toointeract met uw app functie vanaf de opdrachtregel Hallo liever.</span><span class="sxs-lookup"><span data-stu-id="7cf67-151">hello in-portal console is an ideal developer tool when you prefer toointeract with your function app from hello command line.</span></span> <span data-ttu-id="7cf67-152">Veelgebruikte opdrachten zijn directory en maken van het bestand en navigatie, evenals batch-bestanden en scripts uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7cf67-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![De functie app-console](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="7cf67-154"><a name="kudu"></a>Geavanceerde tools (Kudu)</span><span class="sxs-lookup"><span data-stu-id="7cf67-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Functie-app Kudu in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="7cf67-156">Hallo bieden geavanceerde hulpprogramma's voor App Service (ook wel bekend als Kudu) toegang tooadvanced beheerfuncties van uw app functie.</span><span class="sxs-lookup"><span data-stu-id="7cf67-156">hello advanced tools for App Service (also known as Kudu) provide access tooadvanced administrative features of your function app.</span></span> <span data-ttu-id="7cf67-157">U beheert van kudu bovendien, systeemgegevens, app-instellingen, omgevingsvariabelen, site-uitbreidingen, HTTP-headers en servervariabelen.</span><span class="sxs-lookup"><span data-stu-id="7cf67-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="7cf67-158">U kunt ook starten **Kudu** door te bladeren toohello SCM-eindpunt voor de functie-app, zoals`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="7cf67-158">You can also launch **Kudu** by browsing toohello SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Kudu configureren](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="7cf67-160"><a name="deployment">Implementatie-opties</span><span class="sxs-lookup"><span data-stu-id="7cf67-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Opties voor de functie app-implementatie in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="7cf67-162">Functies kunt u uw functiecode op uw lokale machine ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="7cf67-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="7cf67-163">Vervolgens kunt u uw lokale functie app-project tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="7cf67-163">You can then upload your local function app project tooAzure.</span></span> <span data-ttu-id="7cf67-164">Bovendien tootraditional FTP uploaden, functies kunt u de functie-app met behulp van populaire continue integratie-oplossingen, zoals GitHub, VSTS Dropbox, Bitbucket en anderen implementeren.</span><span class="sxs-lookup"><span data-stu-id="7cf67-164">In addition tootraditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="7cf67-165">Zie voor meer informatie [continue implementatie voor Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7cf67-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="7cf67-166">tooupload handmatig met behulp van FTP- of lokale Git, moet u [configureren van de referenties voor uw implementatie](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="7cf67-166">tooupload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="7cf67-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="7cf67-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Functie-app CORS in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="7cf67-169">tooprevent schadelijke code wordt uitgevoerd in uw services, App-Service blokkeert roept tooyour functie apps uit externe bronnen.</span><span class="sxs-lookup"><span data-stu-id="7cf67-169">tooprevent malicious code execution in your services, App Service blocks calls tooyour function apps from external sources.</span></span> <span data-ttu-id="7cf67-170">Functies biedt ondersteuning voor cross-origin-resource delen (CORS) toolet u een 'whitelist definieert' toegestane oorsprongen waarvan van uw functies kunnen externe aanvragen accepteert.</span><span class="sxs-lookup"><span data-stu-id="7cf67-170">Functions supports cross-origin resource sharing (CORS) toolet you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Functie-App configureren CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="7cf67-172"><a name="auth"></a>Verificatie</span><span class="sxs-lookup"><span data-stu-id="7cf67-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Verificatie van de functie-app in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="7cf67-174">Wanneer functies een HTTP-trigger te gebruiken, kunt u ook vragen oproepen toofirst worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="7cf67-174">When functions use an HTTP trigger, you can require calls toofirst be authenticated.</span></span> <span data-ttu-id="7cf67-175">App Service biedt ondersteuning voor Azure Active Directory-verificatie en meld u aan met sociale providers, zoals Microsoft, Facebook en Twitter.</span><span class="sxs-lookup"><span data-stu-id="7cf67-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="7cf67-176">Zie voor meer informatie over het configureren van specifieke verificatieproviders [overzicht van Azure App Service-authenticatie](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7cf67-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Verificatie voor een functie-app configureren](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="7cf67-178"><a name="swagger"></a>API-definitie</span><span class="sxs-lookup"><span data-stu-id="7cf67-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![De functie app API swagger-definitie in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="7cf67-180">Functions ondersteunt Swagger tooallow clients toomore eenvoudig uw HTTP-geactiveerde functies gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7cf67-180">Functions supports Swagger tooallow clients toomore easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="7cf67-181">Bezoek voor meer informatie over het maken van API-definities met Swagger [aan de slag met API-Apps, ASP.NET en Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7cf67-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="7cf67-182">U kunt ook functies proxy's toodefine één API-gebied voor meerdere functies.</span><span class="sxs-lookup"><span data-stu-id="7cf67-182">You can also use Functions Proxies toodefine a single API surface for multiple functions.</span></span> <span data-ttu-id="7cf67-183">Zie voor meer informatie [werken met Azure Functions-proxy's](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="7cf67-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![API voor functie-App configureren](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="7cf67-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7cf67-185">Next steps</span></span>

+ [<span data-ttu-id="7cf67-186">Azure App Service-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="7cf67-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="7cf67-187">Doorlopende implementatie voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7cf67-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



