---
title: aaaConfigure verificatie en autorisatie voor een aangepaste toepassing die aanroept hello Azure Time Series Insights-API | Microsoft Docs
description: Deze zelfstudie wordt uitgelegd hoe tooconfigure verificatie en autorisatie voor een aangepaste toepassing die aanroept hello Azure Time Series Insights-API
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="9f89a-103">Verificatie en autorisatie voor Azure Time Series Insights-API</span><span class="sxs-lookup"><span data-stu-id="9f89a-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="9f89a-104">Dit artikel wordt uitgelegd hoe een aangepaste toepassing die aanroept tooconfigure inzicht API van Azure Time Series Hallo.</span><span class="sxs-lookup"><span data-stu-id="9f89a-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="9f89a-105">Service-principal</span><span class="sxs-lookup"><span data-stu-id="9f89a-105">Service principal</span></span>

<span data-ttu-id="9f89a-106">Deze sectie wordt uitgelegd hoe een toepassing tooaccess tooconfigure Time Series inzicht API Hallo namens de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="9f89a-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="9f89a-107">Hallo-toepassing kunt vervolgens gegevens opvragen of referentiegegevens publiceren in Hallo Time Series Insights omgeving met referenties van de toepassing en geen Hallo gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="9f89a-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="9f89a-108">Wanneer u een toepassing die tooaccess Time Series inzichten nodig hebt, moet u een Azure Active Directory-toepassing instellen en toewijzen van Hallo gegevenstoegangsbeleid in Hallo Time Series Insights omgeving.</span><span class="sxs-lookup"><span data-stu-id="9f89a-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="9f89a-109">Deze aanpak is beter toorunning Hallo app met uw eigen referenties, omdat:</span><span class="sxs-lookup"><span data-stu-id="9f89a-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="9f89a-110">U kunt machtigingen toohello app identiteit die afwijken van uw eigen machtigingen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="9f89a-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="9f89a-111">Deze machtigingen zijn normaal gesproken beperkt tooexactly welke app Hallo moet toodo.</span><span class="sxs-lookup"><span data-stu-id="9f89a-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="9f89a-112">U kunt bijvoorbeeld toestaan Hallo app tooonly lezen van gegevens in een bepaalde tijd reeks Insights-omgeving.</span><span class="sxs-lookup"><span data-stu-id="9f89a-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="9f89a-113">U hebt geen toochange Hallo app referenties als uw verantwoordelijkheden wijzigt.</span><span class="sxs-lookup"><span data-stu-id="9f89a-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="9f89a-114">U kunt een certificaat of een toepassing sleutel tooautomate authenticatie gebruiken wanneer u een script zonder toezicht uitvoert.</span><span class="sxs-lookup"><span data-stu-id="9f89a-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="9f89a-115">Dit artikel laat zien hoe deze stappen via tooperform hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9f89a-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="9f89a-116">Het is gericht op een één-tenant-toepassing waarbij de toepassing hello beoogde toorun in slechts één organisatie is.</span><span class="sxs-lookup"><span data-stu-id="9f89a-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="9f89a-117">Doorgaans gebruikt u toepassingen voor één tenant voor line-of-business-toepassingen die worden uitgevoerd in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="9f89a-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="9f89a-118">Hallo setup stroom bestaat uit drie hoofdstappen:</span><span class="sxs-lookup"><span data-stu-id="9f89a-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="9f89a-119">Een toepassing maakt in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9f89a-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="9f89a-120">Toestaan dat deze toepassing tooaccess Hallo Time Series Insights-omgeving.</span><span class="sxs-lookup"><span data-stu-id="9f89a-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="9f89a-121">Gebruik Hallo toepassings-ID en sleutel tooacquire een token toohello `"https://api.timeseries.azure.com/"` doelgroep of resource.</span><span class="sxs-lookup"><span data-stu-id="9f89a-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="9f89a-122">Hallo-token kan vervolgens worden gebruikte toocall Hallo Time Series Insights-API.</span><span class="sxs-lookup"><span data-stu-id="9f89a-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="9f89a-123">Hier volgen gedetailleerde stappen Hallo:</span><span class="sxs-lookup"><span data-stu-id="9f89a-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="9f89a-124">Selecteer in de Azure-portal Hallo, **Azure Active Directory** > **App registraties** > **registratie van de nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="9f89a-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Registratie van de nieuwe toepassing in Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="9f89a-126">Hallo-toepassing een naam, selecteer Hallo type toobe geven **Web-app / API**, selecteer een geldige URI voor **aanmeldings-URL**, en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="9f89a-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Hallo-toepassing maken in Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="9f89a-128">Uw nieuwe toepassing selecteren en kopiëren van de toepassing-ID tooyour favoriete teksteditor.</span><span class="sxs-lookup"><span data-stu-id="9f89a-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![Kopieer Hallo toepassings-ID](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="9f89a-130">Selecteer **sleutels**, Voer Hallo sleutelnaam, selecteer Hallo verlopen, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9f89a-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![Sleutels van de toepassing selecteren](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Hallo-sleutelnaam en verlopen en klik op Opslaan](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="9f89a-133">Kopieer Hallo sleutel tooyour favoriete teksteditor.</span><span class="sxs-lookup"><span data-stu-id="9f89a-133">Copy hello key tooyour favorite text editor.</span></span>

   ![Kopieer de sleutel van de toepassing hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="9f89a-135">Selecteer Hallo Time Series Insights omgeving **Gegevenstoegangsbeleid** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9f89a-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Toevoegen van nieuwe data access-beleid toohello Time Series Insights-omgeving](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="9f89a-137">In Hallo **gebruiker selecteren** in het dialoogvenster, plakken Hallo toepassingsnaam (uit stap 2) of toepassings-ID (uit stap 3).</span><span class="sxs-lookup"><span data-stu-id="9f89a-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![Een toepassing niet vinden in het dialoogvenster voor Hallo gebruiker selecteren](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="9f89a-139">Selecteer Hallo-rol (**lezer** voor het opvragen van gegevens, **Inzender** voor het opvragen van gegevens en het wijzigen van referentiegegevens) en klik op **Ok**.</span><span class="sxs-lookup"><span data-stu-id="9f89a-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Lezer of bijdrager kiezen in het dialoogvenster van Hallo rol selecteren](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="9f89a-141">Hallo beleid opslaan door te klikken op **Ok**.</span><span class="sxs-lookup"><span data-stu-id="9f89a-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="9f89a-142">Hallo toepassings-ID (uit stap 3) en de toepassing (uit stap 5) sleutel tooacquire Hallo token namens de toepassing hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9f89a-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="9f89a-143">Hallo token kan vervolgens worden doorgegeven in Hallo `Authorization` header bij het aanroepen van de toepassing hello Hallo Time Series Insights-API.</span><span class="sxs-lookup"><span data-stu-id="9f89a-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="9f89a-144">Als u van C# gebruikmaakt, kunt u de volgende code tooacquire Hallo token namens Hallo toepassing hello kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9f89a-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="9f89a-145">Zie voor een compleet codevoorbeeld [opvragen van gegevens met C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="9f89a-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="9f89a-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9f89a-146">Next steps</span></span>

<span data-ttu-id="9f89a-147">Hallo toepassings-ID en sleutel gebruiken in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9f89a-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="9f89a-148">Zie voor een voorbeeld van code die Hallo Time Series Insights-API aanroept, [opvragen van gegevens met C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="9f89a-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="9f89a-149">Zie ook</span><span class="sxs-lookup"><span data-stu-id="9f89a-149">See also</span></span>

* <span data-ttu-id="9f89a-150">[Query uitvoeren op API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) voor Hallo volledige Query API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="9f89a-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="9f89a-151">Maken van een service principal in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9f89a-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
