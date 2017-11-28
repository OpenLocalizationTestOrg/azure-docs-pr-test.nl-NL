---
title: "aaaDeploy, aanroepen en verifiëren van web-API's & REST-API's voor Azure Logic Apps | Microsoft Docs"
description: "Implementeren, te verifiëren en web-API's & REST-API's aanroepen in werkstromen voor systeemintegraties met Azure Logic Apps"
keywords: "Web-API's, REST-API's, connectors, werkstromen, systeemintegraties, verifiëren"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="a108d-104">Implementeren en verifiëren van aangepaste API's als connectors voor logic apps aanroepen</span><span class="sxs-lookup"><span data-stu-id="a108d-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="a108d-105">Nadat u [maken van aangepaste API's](./logic-apps-create-api-app.md) die acties of triggers toouse in logic apps werkstromen bieden, moet u uw API's implementeren voordat u ze kunt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="a108d-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="a108d-106">En hoewel voor de beste ervaring hello, u API vanuit een logische app aanroepen kunt, toe te voegen [Swagger-metagegevens](http://swagger.io/specification/) die uw API bewerkingen en parameters beschrijft.</span><span class="sxs-lookup"><span data-stu-id="a108d-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="a108d-107">Dit bestand Swagger helpt uw API werken beter en eenvoudiger te integreren met logische apps.</span><span class="sxs-lookup"><span data-stu-id="a108d-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="a108d-108">U kunt uw API's als implementeren [web-apps](../app-service-web/app-service-web-overview.md), maar overweeg het implementeren van uw API's als [API-apps](../app-service-api/app-service-api-apps-why-best-platform.md), zodat u uw taak gemakkelijker wanneer ontwikkelen, hosten en API's in Hallo cloud en on-premises gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a108d-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="a108d-109">Er geen toochange code in de API's, u hoeft de code tooan API-app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="a108d-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="a108d-110">U kunt uw API's hosten op [Azure App Service](../app-service/app-service-value-prop-what-is.md), een platform-as-a-service (PaaS) die het beste eenvoudigste en meest schaalbare manieren Hallo biedt voor het hosten van de API.</span><span class="sxs-lookup"><span data-stu-id="a108d-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="a108d-111">tooauthenticate aanroepen vanuit logic apps tooyour API's, u kunt instellen Azure Active Directory in hello Azure-portal dus u geen tooupdate uw code hebt.</span><span class="sxs-lookup"><span data-stu-id="a108d-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="a108d-112">Of u kunt vereisen en afdwingen van verificatie via de API-code.</span><span class="sxs-lookup"><span data-stu-id="a108d-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="a108d-113">Uw API als een web-app of API-app implementeren</span><span class="sxs-lookup"><span data-stu-id="a108d-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="a108d-114">Voordat u uw aangepaste API vanuit een logische app aanroepen kunt, implementeert u uw API als een web-app of API-app tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="a108d-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="a108d-115">Ook toomake uw Swagger document gelezen door Hallo Logic App-ontwerper, Hallo API-definitie-eigenschappen instellen en inschakelen [cross-origin-resource delen (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) voor uw web-app of API-app.</span><span class="sxs-lookup"><span data-stu-id="a108d-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="a108d-116">In hello Azure-portal, selecteer uw web-app of API-app.</span><span class="sxs-lookup"><span data-stu-id="a108d-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="a108d-117">Hallo-blade die wordt geopend, klikt u onder **API**, kies **API-definitie**.</span><span class="sxs-lookup"><span data-stu-id="a108d-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="a108d-118">Set Hallo **locatie voor API-definitie** toohello-URL voor uw swagger.json-bestand.</span><span class="sxs-lookup"><span data-stu-id="a108d-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="a108d-119">Normaal gesproken Hallo-URL wordt weergegeven in deze indeling:`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="a108d-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Koppeling tooSwagger-bestand voor uw aangepaste API gebruiken](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="a108d-121">Onder **API**, kies **CORS**.</span><span class="sxs-lookup"><span data-stu-id="a108d-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="a108d-122">Hallo CORS beleid instellen voor **toegestane oorsprongen** te**'*'** (alle toestaan).</span><span class="sxs-lookup"><span data-stu-id="a108d-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="a108d-123">Deze instelling kan aanvragen van Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="a108d-123">This setting permits requests from Logic App Designer.</span></span>

   ![Toestaan van aanvragen van Logic App-ontwerper tooyour aangepaste API](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="a108d-125">Zie voor meer informatie in deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="a108d-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="a108d-126">Swagger-metagegevens voor ASP.NET web-API's toevoegen</span><span class="sxs-lookup"><span data-stu-id="a108d-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="a108d-127">ASP.NET web API's tooAzure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="a108d-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="a108d-128">Uw aangepaste API aanroepen vanuit logic app-werkstromen</span><span class="sxs-lookup"><span data-stu-id="a108d-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="a108d-129">Na het instellen van eigenschappen van Hallo API-definitie en CORS, moeten triggers en acties van uw aangepaste API beschikbaar worden voor tooinclude in uw logische app-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="a108d-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="a108d-130">tooview hello websites die Swagger URL's hebben, kunt u uw abonnement websites in Hallo Logic Apps Designer bladeren.</span><span class="sxs-lookup"><span data-stu-id="a108d-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="a108d-131">de beschikbare acties tooview en invoer door aan te wijzen op een Swagger-document gebruiken Hallo [HTTP + Swagger actie](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="a108d-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="a108d-132">toocall API, met inbegrip van API's die niet hebt of blootstellen van een Swagger-document, kunt u altijd een aanvraag maken met de Hallo [HTTP-actie](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="a108d-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="a108d-133">Aangepaste tooyour-API aanroepen verifiëren</span><span class="sxs-lookup"><span data-stu-id="a108d-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="a108d-134">U kunt beveiligen aanroepen tooyour aangepaste API op de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="a108d-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="a108d-135">[Er is geen codewijzigingen](#no-code): uw API beveiligen met [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) via hello Azure-portal, zodat u niet hebt tooupdate uw code of implementeren van uw API.</span><span class="sxs-lookup"><span data-stu-id="a108d-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a108d-136">Standaard bieden niet hello Azure AD authentication die u in Azure-portal Hallo inschakelen fijnmazig autorisatie.</span><span class="sxs-lookup"><span data-stu-id="a108d-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="a108d-137">Deze verificatie wordt bijvoorbeeld uw API-toojust vergrendeld een specifieke tenant, niet tooa specifieke gebruiker of app.</span><span class="sxs-lookup"><span data-stu-id="a108d-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="a108d-138">[Werk uw API-code](#update-code): uw API beveiligen door af te dwingen [certificaatverificatie](#certificate), [basisverificatie](#basic), of [Azure AD authentication](#azure-ad-code) via code.</span><span class="sxs-lookup"><span data-stu-id="a108d-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="a108d-139">Aanroepen tooyour API verifiëren zonder code te wijzigen</span><span class="sxs-lookup"><span data-stu-id="a108d-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="a108d-140">Hier volgt de algemene stappen Hallo voor deze methode:</span><span class="sxs-lookup"><span data-stu-id="a108d-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="a108d-141">Maak twee [Azure Active Directory (Azure AD) toepassing identiteiten](../app-service-api/app-service-api-dotnet-service-principal-auth.md): één voor uw logische app en één voor uw web-app (of API-app).</span><span class="sxs-lookup"><span data-stu-id="a108d-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="a108d-142">tooauthenticate aanroepen tooyour API, Hallo referenties (client-ID en geheim) gebruikt voor Hallo [service-principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) die gekoppeld is aan hello Azure AD-toepassingsidentiteit voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="a108d-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="a108d-143">Hallo toepassing id's in de definitie van de logische app opnemen.</span><span class="sxs-lookup"><span data-stu-id="a108d-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="a108d-144">Deel 1: Een Azure AD-toepassings-id voor uw logische app maken</span><span class="sxs-lookup"><span data-stu-id="a108d-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="a108d-145">Uw logische app maakt gebruik van deze Azure AD-toepassing identiteit tooauthenticate met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a108d-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="a108d-146">U hoeft alleen tooset van deze identiteit voor uw directory.</span><span class="sxs-lookup"><span data-stu-id="a108d-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="a108d-147">U kunt bijvoorbeeld toouse Hallo dezelfde identiteit voor alle logic apps, zelfs als u de unieke id's voor elke logische app kunt maken.</span><span class="sxs-lookup"><span data-stu-id="a108d-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="a108d-148">U kunt deze identiteiten in hello Azure-portal instellen [klassieke Azure-portal](#app-identity-logic-classic), of gebruik [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="a108d-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="a108d-149">**Hallo toepassings-id voor uw logische app maken in hello Azure-portal**</span><span class="sxs-lookup"><span data-stu-id="a108d-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="a108d-150">In Hallo [Azure-portal](https://portal.azure.com "https://portal.azure.com"), kies **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a108d-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="a108d-151">Bevestig dat u bent klaar Hallo dezelfde directory als uw web-app of API-app.</span><span class="sxs-lookup"><span data-stu-id="a108d-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="a108d-152">tooswitch mappen, klikt u op uw profiel en selecteer een andere map.</span><span class="sxs-lookup"><span data-stu-id="a108d-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="a108d-153">Of kies **overzicht** > **Switch directory**.</span><span class="sxs-lookup"><span data-stu-id="a108d-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="a108d-154">Hallo directory menu onder **beheren**, kies **App registraties** > **registratie van de nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="a108d-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="a108d-155">Standaard worden alle app-registraties Hallo app registraties lijst weergegeven in uw directory.</span><span class="sxs-lookup"><span data-stu-id="a108d-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="a108d-156">selecteert u alleen uw app registraties, volgende toohello zoekvak tooview **mijn apps**.</span><span class="sxs-lookup"><span data-stu-id="a108d-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![Maken van nieuwe app-registratie](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="a108d-158">Geef een naam op voor de toepassingsidentiteit van uw, laat u **toepassingstype** instellen te**Web-app / API**, bieden een unieke tekenreeks die is opgemaakt als een domein voor **aanmeldings-URL**, en kies  **Maak**.</span><span class="sxs-lookup"><span data-stu-id="a108d-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Geef de naam van en aanmelding URL voor toepassings-id](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="a108d-160">Hallo toepassings-id die u hebt gemaakt voor uw logische app wordt nu weergegeven in Hallo app registraties lijst.</span><span class="sxs-lookup"><span data-stu-id="a108d-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![Toepassings-id voor uw logische app](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="a108d-162">Selecteer de nieuwe toepassingsidentiteit in Hallo app registraties lijst.</span><span class="sxs-lookup"><span data-stu-id="a108d-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="a108d-163">Kopiëren en opslaan van Hallo **toepassings-ID** toouse zoals Hallo 'client-ID' voor uw logische app in deel 3.</span><span class="sxs-lookup"><span data-stu-id="a108d-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![Kopiëren en opslaan van toepassings-ID voor de logische app](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="a108d-165">Als de identity-instellingen van de toepassing niet weergegeven worden, kiest u **instellingen** of **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="a108d-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="a108d-166">Onder **API-toegang**, kies **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="a108d-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="a108d-167">Onder **beschrijving**, Geef een naam voor uw sleutel.</span><span class="sxs-lookup"><span data-stu-id="a108d-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="a108d-168">Onder **verloopt**, selecteert u een duur voor uw sleutel.</span><span class="sxs-lookup"><span data-stu-id="a108d-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="a108d-169">Hallo-sleutel die u maakt, fungeert als Hallo toepassings-id van 'geheime' of het wachtwoord voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="a108d-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![Sleutel voor de id van logische app maken](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="a108d-171">Kies op de werkbalk Hallo **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a108d-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="a108d-172">Onder **waarde**, uw sleutel wordt nu weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a108d-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="a108d-173">**Zorg ervoor dat toocopy en opslaan van uw sleutel** voor later gebruik omdat Hallo-sleutel wordt verborgen wanneer u laat Hallo sleutel blade.</span><span class="sxs-lookup"><span data-stu-id="a108d-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="a108d-174">Wanneer u uw logische app in deel 3 configureert, geeft u deze sleutel als Hallo 'geheime' of het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a108d-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![Kopieer en sleutel opslaan voor later](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="a108d-176">**Hallo toepassings-id voor uw logische app maken in Hallo klassieke Azure-portal**</span><span class="sxs-lookup"><span data-stu-id="a108d-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="a108d-177">In de klassieke Azure-portal Hallo, kiest u [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="a108d-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="a108d-178">Selecteer Hallo dezelfde map die u voor uw web-app of API-app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a108d-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="a108d-179">Op Hallo **toepassingen** Kies **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="a108d-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="a108d-180">Geef een naam op voor de toepassingsidentiteit van uw en kies **volgende** (pijl naar rechts).</span><span class="sxs-lookup"><span data-stu-id="a108d-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="a108d-181">Onder **App-eigenschappen**, Geef een unieke tekenreeks die is opgemaakt als een domein voor **aanmeldings-URL** en **App ID URI**, en kies **Complete** (vinkje).</span><span class="sxs-lookup"><span data-stu-id="a108d-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="a108d-182">Op Hallo **configureren** tabblad, kopiëren en opslaan van Hallo **Client-ID** voor uw logische app toouse in deel 3.</span><span class="sxs-lookup"><span data-stu-id="a108d-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="a108d-183">Onder **sleutels**Open Hallo **Selecteer duur** lijst.</span><span class="sxs-lookup"><span data-stu-id="a108d-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="a108d-184">Selecteer een duur voor de sleutel.</span><span class="sxs-lookup"><span data-stu-id="a108d-184">Select a duration for your key.</span></span>

   <span data-ttu-id="a108d-185">Hallo-sleutel die u maakt, fungeert als Hallo toepassings-id van 'geheime' of het wachtwoord voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="a108d-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="a108d-186">Aan de onderkant van de Hallo van Hallo pagina, kies **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a108d-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="a108d-187">Mogelijk hebt u toowait een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="a108d-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="a108d-188">Onder **sleutels**, zorg ervoor dat toocopy en slaat u Hallo-sleutel die wordt nu weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a108d-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="a108d-189">Wanneer u uw logische app in deel 3 configureert, geeft u deze sleutel als Hallo 'geheime' of het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a108d-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="a108d-190">Voor meer informatie meer informatie over hoe te [configureren van uw App Service-toepassing toouse Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a108d-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="a108d-191">**Hallo toepassings-id voor uw logische app maken in PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a108d-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="a108d-192">U kunt deze taak via Azure Resource Manager met PowerShell uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a108d-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="a108d-193">Voer deze opdrachten uit in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a108d-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="a108d-194">Zorg ervoor dat toocopy hello **Tenant-ID** (GUID voor uw Azure AD-tenant), Hallo **toepassings-ID**, en het Hallo-wachtwoord die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a108d-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="a108d-195">Voor meer informatie meer informatie over hoe te [een service-principal maken met PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="a108d-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="a108d-196">Deel 2: Een Azure AD-toepassings-id voor uw web-app of API-app maken</span><span class="sxs-lookup"><span data-stu-id="a108d-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="a108d-197">Als uw web-app of API-app al is geïmplementeerd, kunt u verificatie inschakelen en Hallo toepassings-id maken in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a108d-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="a108d-198">Anders kunt u [authentication inschakelen wanneer u met een Azure Resource Manager-sjabloon implementeert](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="a108d-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="a108d-199">**Hallo toepassings-id maken en verificatie in hello Azure-portal voor geïmplementeerde apps inschakelen**</span><span class="sxs-lookup"><span data-stu-id="a108d-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="a108d-200">In Hallo [Azure-portal](https://portal.azure.com "https://portal.azure.com"), zoeken en selecteert u uw web-app of API-app.</span><span class="sxs-lookup"><span data-stu-id="a108d-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="a108d-201">Onder **instellingen**, kies **verificatie/autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="a108d-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="a108d-202">Onder **verificatie van App Service**, schakelt u verificatie **op**.</span><span class="sxs-lookup"><span data-stu-id="a108d-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="a108d-203">Onder **verificatieproviders**, kies **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a108d-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Authentication inschakelen](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="a108d-205">Maak nu een toepassings-id voor uw web-app of API-app zoals hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a108d-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="a108d-206">Op Hallo **Azure Active Directory-instellingen** blade ingesteld **beheermodus** te**Express**.</span><span class="sxs-lookup"><span data-stu-id="a108d-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="a108d-207">Kies **nieuwe AD-App maken**.</span><span class="sxs-lookup"><span data-stu-id="a108d-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="a108d-208">Geef een naam op voor de toepassingsidentiteit van uw en kies **OK**.</span><span class="sxs-lookup"><span data-stu-id="a108d-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Toepassings-id voor uw web-app of API-app maken](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="a108d-210">Op Hallo **verificatie / autorisatie-blade**, kies **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a108d-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="a108d-211">U moet nu Hallo client-ID vinden en tenant-ID voor Hallo toepassings-id die is gekoppeld aan uw web-app of API-app.</span><span class="sxs-lookup"><span data-stu-id="a108d-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="a108d-212">U gebruikt deze id in deel 3.</span><span class="sxs-lookup"><span data-stu-id="a108d-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="a108d-213">Dus doorgaan met deze stappen voor hello Azure-portal of [klassieke Azure-portal](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="a108d-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="a108d-214">**Toepassings-id client-ID vinden en tenant-ID voor uw web-app of API-app in hello Azure-portal**</span><span class="sxs-lookup"><span data-stu-id="a108d-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="a108d-215">Onder **verificatieproviders**, kies **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a108d-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   !['Azure Active Directory' kiezen](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="a108d-217">Op Hallo **Azure Active Directory-instellingen** blade ingesteld **beheermodus** te**Geavanceerd**.</span><span class="sxs-lookup"><span data-stu-id="a108d-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="a108d-218">Kopiëren Hallo **Client-ID**, en sla deze GUID voor gebruik in deel 3.</span><span class="sxs-lookup"><span data-stu-id="a108d-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="a108d-219">Als **Client-ID** en **Url-verlener** niet worden weergegeven, vernieuw hello Azure-portal en Herhaal stap 1.</span><span class="sxs-lookup"><span data-stu-id="a108d-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="a108d-220">Onder **Url-verlener**, kopiëren en opslaan net hello GUID voor deel 3.</span><span class="sxs-lookup"><span data-stu-id="a108d-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="a108d-221">U kunt ook deze GUID gebruiken in uw web-app of sjabloon API-app-implementatie, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="a108d-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="a108d-222">Deze GUID is van de tenant van uw specifieke GUID ('tenant-ID') en moet worden weergegeven in deze URL:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="a108d-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="a108d-223">Sluit zonder de wijzigingen worden opgeslagen, Hallo **Azure Active Directory-instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="a108d-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="a108d-224">**Toepassings-id client-ID vinden en tenant-ID voor uw web-app of API-app in de klassieke Azure-portal Hallo**</span><span class="sxs-lookup"><span data-stu-id="a108d-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="a108d-225">In de klassieke Azure-portal Hallo, kiest u [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="a108d-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="a108d-226">Hallo directory selecteren die u voor uw web-app of API-app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a108d-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="a108d-227">In Hallo **Search** , zoeken en kiest u Hallo toepassings-id voor uw web-app of API-app.</span><span class="sxs-lookup"><span data-stu-id="a108d-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="a108d-228">Op Hallo **configureren** tabblad, kopie Hallo **Client-ID**, en sla deze GUID voor gebruik in deel 3.</span><span class="sxs-lookup"><span data-stu-id="a108d-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="a108d-229">Nadat u Hallo client-ID aan de onderkant Hallo Hallo **configureren** Kies **eindpunten weergeven**.</span><span class="sxs-lookup"><span data-stu-id="a108d-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="a108d-230">Kopieer de URL Hallo voor **Document met federatieve metagegevens**, en blader toothat URL.</span><span class="sxs-lookup"><span data-stu-id="a108d-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="a108d-231">Zoeken in het document metagegevens Hallo dat wordt geopend, Hallo hoofdmap **EntityDescriptor ID** -element, wat is een **id van de entiteit** kenmerk in dit formulier:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="a108d-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="a108d-232">Hallo GUID in dit kenmerk is van de tenant van uw specifieke GUID (tenant-ID).</span><span class="sxs-lookup"><span data-stu-id="a108d-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="a108d-233">Hallo tenant-ID kopiëren en opslaan van die ID voor gebruik in deel 3 en toouse in uw web-app of sjabloon API-app-implementatie, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="a108d-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="a108d-234">Zie de volgende onderwerpen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="a108d-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="a108d-235">Gebruikersverificatie voor API-apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a108d-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="a108d-236">Verificatie en autorisatie in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a108d-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="a108d-237">**Verificatie inschakelen wanneer u met een Azure Resource Manager-sjabloon implementeren**</span><span class="sxs-lookup"><span data-stu-id="a108d-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="a108d-238">U moet nog steeds een Azure AD-toepassings-id voor uw web-app of API-app die verschilt Hallo app identiteit maken voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="a108d-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="a108d-239">Deel 2 stappen toocreate Hallo toepassingsidentiteit, volg Hallo vorige voor hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a108d-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="a108d-240">U kunt ook Hallo stappen in deel 1 maar zorg ervoor dat toouse uw web-app of API-app werkelijke `https://{URL}` voor **aanmeldings-URL** en **App ID URI**.</span><span class="sxs-lookup"><span data-stu-id="a108d-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="a108d-241">Van deze stappen hebt u toosave zowel Hallo-client-ID en tenant-ID voor gebruik in uw app implementatiesjabloon en ook voor deel 3.</span><span class="sxs-lookup"><span data-stu-id="a108d-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="a108d-242">Wanneer u hello Azure AD-toepassings-id voor uw web-app of API-app maakt, moet u hello Azure-portal of klassieke Azure-portal, in plaats van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a108d-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="a108d-243">Hallo PowerShell-cmdlet niet Hallo vereist machtigingen instellen toosign gebruikers in een website.</span><span class="sxs-lookup"><span data-stu-id="a108d-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="a108d-244">Nadat u Hallo client-ID en tenant-ID hebt ontvangen, moet u deze id opnemen als een subresource van uw web-app of API-app in de implementatiesjabloon voor:</span><span class="sxs-lookup"><span data-stu-id="a108d-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="a108d-245">tooautomatically een leeg web-app en een logische app samen met Azure Active Directory-verificatie implementeren [Hallo volledige sjabloon weergeven hier](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), of klik op **tooAzure implementeren** hier:</span><span class="sxs-lookup"><span data-stu-id="a108d-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="a108d-246">[![TooAzure implementeren](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a108d-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="a108d-247">Deel 3: Hallo autorisatie-sectie in uw logische app vullen</span><span class="sxs-lookup"><span data-stu-id="a108d-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="a108d-248">Hallo vorige sjabloon is al in deze sectie autorisatie is ingesteld, maar als u rechtstreeks Hallo logische app maakt, moet u Hallo volledige autorisatie sectie opnemen.</span><span class="sxs-lookup"><span data-stu-id="a108d-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="a108d-249">Open de definitie van de logische app in de codeweergave Ga toohello **HTTP** sectie actie, zoeken Hallo **autorisatie** sectie en deze regel:</span><span class="sxs-lookup"><span data-stu-id="a108d-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="a108d-250">Element</span><span class="sxs-lookup"><span data-stu-id="a108d-250">Element</span></span> | <span data-ttu-id="a108d-251">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a108d-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="a108d-252">Tenant</span><span class="sxs-lookup"><span data-stu-id="a108d-252">tenant</span></span> |<span data-ttu-id="a108d-253">Hallo GUID voor hello Azure AD-tenant</span><span class="sxs-lookup"><span data-stu-id="a108d-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="a108d-254">doelgroep</span><span class="sxs-lookup"><span data-stu-id="a108d-254">audience</span></span> |<span data-ttu-id="a108d-255">Vereist.</span><span class="sxs-lookup"><span data-stu-id="a108d-255">Required.</span></span> <span data-ttu-id="a108d-256">Hallo GUID voor Hallo doelresource dat u wilt dat tooaccess - Hallo client-ID van Hallo toepassings-id voor uw web-app of API-app</span><span class="sxs-lookup"><span data-stu-id="a108d-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="a108d-257">clientId</span><span class="sxs-lookup"><span data-stu-id="a108d-257">clientId</span></span> |<span data-ttu-id="a108d-258">Hallo GUID voor Hallo client access - client-ID Hallo van Hallo toepassings-id voor uw logische app aanvragen</span><span class="sxs-lookup"><span data-stu-id="a108d-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="a108d-259">Geheim</span><span class="sxs-lookup"><span data-stu-id="a108d-259">secret</span></span> |<span data-ttu-id="a108d-260">Vereist.</span><span class="sxs-lookup"><span data-stu-id="a108d-260">Required.</span></span> <span data-ttu-id="a108d-261">Hallo sleutel of het wachtwoord van Hallo toepassings-id voor Hallo-client die Hallo toegangstoken aanvraagt</span><span class="sxs-lookup"><span data-stu-id="a108d-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="a108d-262">type</span><span class="sxs-lookup"><span data-stu-id="a108d-262">type</span></span> |<span data-ttu-id="a108d-263">Hallo verificatietype.</span><span class="sxs-lookup"><span data-stu-id="a108d-263">hello authentication type.</span></span> <span data-ttu-id="a108d-264">Hallo-waarde voor ActiveDirectoryOAuth verificatie, heeft `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="a108d-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="a108d-265">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a108d-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="a108d-266">Beveiligde API-aanroepen via code</span><span class="sxs-lookup"><span data-stu-id="a108d-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="a108d-267">Verificatie via certificaat</span><span class="sxs-lookup"><span data-stu-id="a108d-267">Certificate authentication</span></span>

<span data-ttu-id="a108d-268">toovalidate hello binnenkomende aanvragen van uw logische app tooyour WebApp of API-app, kunt u clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="a108d-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="a108d-269">tooset om uw code meer [hoe tooconfigure TLS wederzijdse verificatie](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="a108d-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="a108d-270">In Hallo **autorisatie** sectie, voeg deze regel:</span><span class="sxs-lookup"><span data-stu-id="a108d-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="a108d-271">Element</span><span class="sxs-lookup"><span data-stu-id="a108d-271">Element</span></span> | <span data-ttu-id="a108d-272">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a108d-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="a108d-273">type</span><span class="sxs-lookup"><span data-stu-id="a108d-273">type</span></span> |<span data-ttu-id="a108d-274">Vereist.</span><span class="sxs-lookup"><span data-stu-id="a108d-274">Required.</span></span> <span data-ttu-id="a108d-275">Hallo verificatietype.</span><span class="sxs-lookup"><span data-stu-id="a108d-275">hello authentication type.</span></span> <span data-ttu-id="a108d-276">Voor SSL-clientcertificaten moet Hallo waarde `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="a108d-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="a108d-277">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a108d-277">password</span></span> |<span data-ttu-id="a108d-278">Vereist.</span><span class="sxs-lookup"><span data-stu-id="a108d-278">Required.</span></span> <span data-ttu-id="a108d-279">Hallo-wachtwoord voor toegang tot het clientcertificaat hello (PFX-bestand)</span><span class="sxs-lookup"><span data-stu-id="a108d-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="a108d-280">PFX</span><span class="sxs-lookup"><span data-stu-id="a108d-280">pfx</span></span> |<span data-ttu-id="a108d-281">Vereist.</span><span class="sxs-lookup"><span data-stu-id="a108d-281">Required.</span></span> <span data-ttu-id="a108d-282">Base64-gecodeerde inhoud van het clientcertificaat hello (PFX-bestand)</span><span class="sxs-lookup"><span data-stu-id="a108d-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="a108d-283">Basisverificatie</span><span class="sxs-lookup"><span data-stu-id="a108d-283">Basic authentication</span></span>

<span data-ttu-id="a108d-284">inkomende aanvragen toovalidate van uw logische app tooyour WebApp of API-app, kunt u basisverificatie, zoals een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a108d-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="a108d-285">Basisverificatie is een algemene patroon en kunt u deze verificatie in een toobuild taal wordt gebruikt voor uw web-app of API-app.</span><span class="sxs-lookup"><span data-stu-id="a108d-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="a108d-286">In Hallo **autorisatie** sectie, voeg deze regel:</span><span class="sxs-lookup"><span data-stu-id="a108d-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="a108d-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="a108d-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="a108d-288">Element</span><span class="sxs-lookup"><span data-stu-id="a108d-288">Element</span></span> | <span data-ttu-id="a108d-289">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a108d-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a108d-290">type</span><span class="sxs-lookup"><span data-stu-id="a108d-290">type</span></span> |<span data-ttu-id="a108d-291">Vereist.</span><span class="sxs-lookup"><span data-stu-id="a108d-291">Required.</span></span> <span data-ttu-id="a108d-292">Hallo verificatietype.</span><span class="sxs-lookup"><span data-stu-id="a108d-292">hello authentication type.</span></span> <span data-ttu-id="a108d-293">Voor basisverificatie, moet Hallo waarde `Basic`.</span><span class="sxs-lookup"><span data-stu-id="a108d-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="a108d-294">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="a108d-294">username</span></span> |<span data-ttu-id="a108d-295">Vereist.</span><span class="sxs-lookup"><span data-stu-id="a108d-295">Required.</span></span> <span data-ttu-id="a108d-296">Hallo-gebruikersnaam voor verificatie</span><span class="sxs-lookup"><span data-stu-id="a108d-296">hello username for authentication</span></span> |
| <span data-ttu-id="a108d-297">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a108d-297">password</span></span> |<span data-ttu-id="a108d-298">Vereist.</span><span class="sxs-lookup"><span data-stu-id="a108d-298">Required.</span></span> <span data-ttu-id="a108d-299">Hallo-wachtwoord voor verificatie</span><span class="sxs-lookup"><span data-stu-id="a108d-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="a108d-300">Azure Active Directory-verificatie via code</span><span class="sxs-lookup"><span data-stu-id="a108d-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="a108d-301">Standaard bieden niet hello Azure AD authentication die u in Azure-portal Hallo inschakelen fijnmazig autorisatie.</span><span class="sxs-lookup"><span data-stu-id="a108d-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="a108d-302">Deze verificatie wordt bijvoorbeeld uw API-toojust vergrendeld een specifieke tenant, niet tooa specifieke gebruiker of app.</span><span class="sxs-lookup"><span data-stu-id="a108d-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="a108d-303">toorestrict API toegang tooyour logische app via programmacode, pak Hallo-header die heeft Hallo JSON web token (JWT).</span><span class="sxs-lookup"><span data-stu-id="a108d-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="a108d-304">Controleer Hallo aanroeper ID en aanvragen die niet overeenkomen met weigeren.</span><span class="sxs-lookup"><span data-stu-id="a108d-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="a108d-305">Doorgaat, tooimplement deze verificatie volledig in uw eigen code en geen gebruik hello Azure-portal, informatie over hoe te [verificatie met de lokale Active Directory in uw app in Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="a108d-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="a108d-306">een toepassings-id voor uw logische app toocreate en die identiteit toocall uw API gebruiken, moet u de vorige stappen Hallo volgen.</span><span class="sxs-lookup"><span data-stu-id="a108d-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a108d-307">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a108d-307">Next steps</span></span>

* [<span data-ttu-id="a108d-308">Logica van app-prestaties met diagnostische logboeken en waarschuwingen controleren</span><span class="sxs-lookup"><span data-stu-id="a108d-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)