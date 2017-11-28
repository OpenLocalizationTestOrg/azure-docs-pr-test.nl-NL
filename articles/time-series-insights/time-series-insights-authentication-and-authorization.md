---
title: Verificatie en autorisatie voor een aangepaste toepassing die de Azure Time Series Insights-API aanroept configureren | Microsoft Docs
description: Deze zelfstudie wordt uitgelegd hoe u verificatie en autorisatie voor een aangepaste toepassing die de Azure Time Series Insights-API aanroept configureren
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
ms.openlocfilehash: 4dd4865dc556e09a31d2cb7a32768aeb19ba9900
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="09199-103">Verificatie en autorisatie voor Azure Time Series Insights-API</span><span class="sxs-lookup"><span data-stu-id="09199-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="09199-104">Dit artikel wordt uitgelegd hoe u configureert een aangepaste toepassing die de Azure Time Series Insights-API aanroept.</span><span class="sxs-lookup"><span data-stu-id="09199-104">This article explains how to configure a custom application that calls the Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="09199-105">Service-principal</span><span class="sxs-lookup"><span data-stu-id="09199-105">Service principal</span></span>

<span data-ttu-id="09199-106">Deze sectie wordt uitgelegd hoe een toepassing voor toegang tot de inzicht API van tijd reeks namens de toepassing wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="09199-106">This section explains how to configure an application to access the Time Series Insights API on behalf of the application.</span></span> <span data-ttu-id="09199-107">De toepassing kan vervolgens een query over gegevens of referentiegegevens publiceren in de omgeving Time Series Insights met referenties van de toepassing en niet de referenties van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="09199-107">The application can then query data or publish reference data in the Time Series Insights environment with application credentials and not the user credentials.</span></span>

<span data-ttu-id="09199-108">Wanneer u een toepassing die moet op tijd toegang reeks Insights hebt, moet u een Azure Active Directory-toepassing instellen en toewijzen van het toegangsbeleid van de gegevens in de Time Series Insights-omgeving.</span><span class="sxs-lookup"><span data-stu-id="09199-108">When you have an application that needs to access Time Series Insights, you must set up an Azure Active Directory application and assign the data access policies in the Time Series Insights environment.</span></span> <span data-ttu-id="09199-109">Deze aanpak is voorkeur boven het uitvoeren van de app met uw eigen referenties, omdat:</span><span class="sxs-lookup"><span data-stu-id="09199-109">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="09199-110">U kunt machtigingen toewijzen aan de identiteit van de app die afwijken van uw eigen machtigingen.</span><span class="sxs-lookup"><span data-stu-id="09199-110">You can assign permissions to the app identity that are different from your own permissions.</span></span> <span data-ttu-id="09199-111">Deze machtigingen zijn meestal beperkt tot precies wat de app moet doen.</span><span class="sxs-lookup"><span data-stu-id="09199-111">Typically, these permissions are restricted to exactly what the app needs to do.</span></span> <span data-ttu-id="09199-112">U kunt bijvoorbeeld toestaan dat de app alleen lezen van gegevens in een bepaalde tijd reeks Insights-omgeving.</span><span class="sxs-lookup"><span data-stu-id="09199-112">For example, you can allow the app to only read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="09199-113">U hoeft niet te wijzigen van de referenties van de app als uw verantwoordelijkheden wijzigt.</span><span class="sxs-lookup"><span data-stu-id="09199-113">You don't have to change the app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="09199-114">U kunt een certificaat of een Toepassingssleutel automatiseren verificatie wanneer u een script zonder toezicht uitvoert.</span><span class="sxs-lookup"><span data-stu-id="09199-114">You can use a certificate or an application key to automate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="09199-115">Dit artikel laat zien hoe u deze stappen uitvoert via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="09199-115">This article shows you how to perform those steps through the Azure portal.</span></span> <span data-ttu-id="09199-116">Het is gericht op een één-tenant-toepassing waarin de toepassing is bedoeld om uit te voeren in slechts één organisatie.</span><span class="sxs-lookup"><span data-stu-id="09199-116">It focuses on a single-tenant application where the application is intended to run in only one organization.</span></span> <span data-ttu-id="09199-117">Doorgaans gebruikt u toepassingen voor één tenant voor line-of-business-toepassingen die worden uitgevoerd in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="09199-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="09199-118">De setup-stroom bestaat uit drie hoofdstappen:</span><span class="sxs-lookup"><span data-stu-id="09199-118">The setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="09199-119">Een toepassing maakt in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="09199-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="09199-120">De autorisatie voor deze toepassing te krijgen tot de Time Series Insights-omgeving.</span><span class="sxs-lookup"><span data-stu-id="09199-120">Authorize this application to access the Time Series Insights environment.</span></span>
3. <span data-ttu-id="09199-121">Gebruik de toepassings-ID en de sleutel te verkrijgen van een token dat de `"https://api.timeseries.azure.com/"` doelgroep of resource.</span><span class="sxs-lookup"><span data-stu-id="09199-121">Use the application ID and key to acquire a token to the `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="09199-122">Het token kan vervolgens worden gebruikt de Time Series Insights-API aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="09199-122">The token can then be used to call the Time Series Insights API.</span></span>

<span data-ttu-id="09199-123">Hier volgen gedetailleerde stappen:</span><span class="sxs-lookup"><span data-stu-id="09199-123">Here are the detailed steps:</span></span>

1. <span data-ttu-id="09199-124">Selecteer in de Azure-portal **Azure Active Directory** > **App registraties** > **registratie van de nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="09199-124">In the Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Registratie van de nieuwe toepassing in Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="09199-126">Geef een naam op voor de toepassing, selecteer het type moet **Web-app / API**, selecteer een geldige URI voor **aanmeldings-URL**, en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="09199-126">Give the application a name, select the type to be **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![De toepassing in Azure Active Directory maken](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="09199-128">Selecteer de zojuist gemaakte toepassing en kopieer de toepassings-ID naar uw favoriete teksteditor.</span><span class="sxs-lookup"><span data-stu-id="09199-128">Select your newly created application and copy its application ID to your favorite text editor.</span></span>

   ![Kopieer de toepassings-ID](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="09199-130">Selecteer **sleutels**, voer de naam van de sleutel, selecteert u de vervaldatum en klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="09199-130">Select **Keys**, enter the key name, select the expiration, and click **Save**.</span></span>

   ![Sleutels van de toepassing selecteren](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Voer de sleutelnaam en de vervaldatum en klik op Opslaan](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="09199-133">Kopieer de sleutel naar uw favoriete teksteditor.</span><span class="sxs-lookup"><span data-stu-id="09199-133">Copy the key to your favorite text editor.</span></span>

   ![Kopieer de Toepassingssleutel](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="09199-135">Selecteer voor de omgeving Time Series Insights **Gegevenstoegangsbeleid** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="09199-135">For the Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Nieuwe gegevens toegangsbeleid toevoegen aan de Time Series Insights-omgeving](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="09199-137">In de **gebruiker selecteren** in het dialoogvenster, plak de naam van de toepassing (uit stap 2) of toepassings-ID (uit stap 3).</span><span class="sxs-lookup"><span data-stu-id="09199-137">In the **Select User** dialog box, paste the application name (from step 2) or application ID (from step 3).</span></span>

   ![Een toepassing niet vinden in het dialoogvenster gebruiker selecteren](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="09199-139">Selecteer de rol (**lezer** voor het opvragen van gegevens, **Inzender** voor het opvragen van gegevens en het wijzigen van referentiegegevens) en klik op **Ok**.</span><span class="sxs-lookup"><span data-stu-id="09199-139">Select the role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Lezer of bijdrager kiezen in het dialoogvenster rol selecteren](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="09199-141">Het beleid opslaan door te klikken op **Ok**.</span><span class="sxs-lookup"><span data-stu-id="09199-141">Save the policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="09199-142">Gebruik de toepassings-ID (uit stap 3) en de sleutel van de toepassing (uit stap 5) te verkrijgen van het token voor de toepassing is.</span><span class="sxs-lookup"><span data-stu-id="09199-142">Use the application ID (from step 3) and application key (from step 5) to acquire the token on behalf of the application.</span></span> <span data-ttu-id="09199-143">Het token kan vervolgens worden doorgegeven de `Authorization` header wanneer de toepassing de Time Series Insights-API aanroept.</span><span class="sxs-lookup"><span data-stu-id="09199-143">The token can then be passed in the `Authorization` header when the application calls the Time Series Insights API.</span></span>

    <span data-ttu-id="09199-144">Als u van C# gebruikmaakt, kunt u de volgende code te verkrijgen van het token voor de toepassing is.</span><span class="sxs-lookup"><span data-stu-id="09199-144">If you're using C#, you can use the following code to acquire the token on behalf of the application.</span></span> <span data-ttu-id="09199-145">Zie voor een compleet codevoorbeeld [opvragen van gegevens met C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="09199-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set the resource URI to the Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of the application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="09199-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="09199-146">Next steps</span></span>

<span data-ttu-id="09199-147">Gebruik de toepassings-ID en sleutel in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="09199-147">Use the application ID and key in your application.</span></span> <span data-ttu-id="09199-148">Zie voor een voorbeeld van code die de Time Series Insights-API aanroept, [opvragen van gegevens met C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="09199-148">For sample code that calls the Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="09199-149">Zie ook</span><span class="sxs-lookup"><span data-stu-id="09199-149">See also</span></span>

* <span data-ttu-id="09199-150">[Query uitvoeren op API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) voor de volledige Query API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="09199-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for the full Query API reference</span></span>
* [<span data-ttu-id="09199-151">Een service-principal maken in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="09199-151">Create a service principal in the Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
