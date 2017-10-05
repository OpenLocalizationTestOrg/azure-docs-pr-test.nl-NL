---
title: Azure Active Directory gebruiken voor verificatie van oplossingen voor het beheer van de Batch | Microsoft Docs
description: "Toepassingen die zijn gebouwd met Azure resourcemanager en de Batch-resourceprovider zich verifiëren met Azure AD."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 26d4adf4f74f9aacc4cf8cf24be293ebdb4d63c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="d290a-103">Verificatie van oplossingen voor het beheer van de Batch met Active Directory</span><span class="sxs-lookup"><span data-stu-id="d290a-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="d290a-104">Toepassingen die de Azure Batch Management-service aanroepen verifiëren met [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d290a-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="d290a-105">Azure AD is Microsoft multitenant-cloudgebaseerde adreslijst en identity management-service.</span><span class="sxs-lookup"><span data-stu-id="d290a-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="d290a-106">Azure zelf gebruikt Azure AD voor de verificatie van zijn klanten, servicebeheerders en organisatie-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d290a-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="d290a-107">De Batch Management .NET-bibliotheek wordt typen voor het werken met de Batch-accounts, toegangscodes, toepassingen en toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="d290a-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="d290a-108">De Batch Management .NET-bibliotheek is een Azure-resource provider-client en wordt gebruikt in combinatie met [Azure Resource Manager] [ resman_overview] voor het beheren van deze resources via een programma.</span><span class="sxs-lookup"><span data-stu-id="d290a-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="d290a-109">Azure AD is vereist voor de verificatie via een Azure-resource provider-client, met inbegrip van de Batch Management .NET-bibliotheek en aanvragen [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="d290a-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="d290a-110">In dit artikel verkennen we using Azure AD om te verifiëren van toepassingen die gebruikmaken van de Batch Management .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="d290a-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="d290a-111">Laten we zien hoe u Azure AD gebruikt om een abonnementsbeheerder of medebeheerder met geïntegreerde verificatie te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="d290a-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="d290a-112">We gebruiken de [AccountManagment] [ acct_mgmt_sample] voorbeeldproject, beschikbaar op GitHub te doorlopen gebruikmaken van Azure AD met de Batch Management .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="d290a-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="d290a-113">Zie voor meer informatie over het gebruik van de Batch Management .NET-bibliotheek en de steekproef AccountManagement, [beheren Batch-accounts en quota's met de Batch-Management-clientbibliotheek voor .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d290a-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="d290a-114">Uw toepassing registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="d290a-114">Register your application with Azure AD</span></span>

<span data-ttu-id="d290a-115">De Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) biedt een programmatische interface naar Azure AD voor gebruik binnen uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="d290a-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="d290a-116">Om aan te roepen ADAL van uw toepassing, moet u uw toepassing registreren in een Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="d290a-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="d290a-117">Wanneer u uw toepassing registreert, kunt u Azure AD met informatie geven over uw toepassing, met inbegrip van een naam voor het in de Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="d290a-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="d290a-118">Vervolgens Azure AD levert een toepassings-ID waarmee u uw toepassing koppelen aan Azure AD tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="d290a-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="d290a-119">Zie voor meer informatie over de toepassings-ID, [toepassing en service-principal objecten in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="d290a-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="d290a-120">Voor het registreren van de voorbeeldtoepassing AccountManagement, volg de stappen in de [een toepassing toe te voegen](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) in sectie [toepassingen integreren met Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="d290a-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="d290a-121">Geef **systeemeigen clienttoepassing** voor het type van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d290a-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="d290a-122">De branche standaard OAuth 2.0-URI voor de **omleidings-URI** is `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="d290a-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="d290a-123">U kunt echter geldige URI opgeven (zoals `http://myaccountmanagementsample`) voor de **omleidings-URI**, zoals het hoeft niet te worden van een echte eindpunt:</span><span class="sxs-lookup"><span data-stu-id="d290a-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="d290a-124">Wanneer u het registratieproces hebt voltooid, ziet u de toepassings-ID en het object (service-principal)-ID voor uw toepassing wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="d290a-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="d290a-125">De Azure Resource Manager-API toegang verlenen tot uw toepassing</span><span class="sxs-lookup"><span data-stu-id="d290a-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="d290a-126">Vervolgens moet u toegang tot uw toepassing om de Azure Resource Manager-API te delegeren.</span><span class="sxs-lookup"><span data-stu-id="d290a-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="d290a-127">De Azure AD-id voor de Resource Manager-API is **Windows Azure Service Management API**.</span><span class="sxs-lookup"><span data-stu-id="d290a-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="d290a-128">Volg deze stappen in de Azure portal:</span><span class="sxs-lookup"><span data-stu-id="d290a-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="d290a-129">Kies in het navigatiedeelvenster links van de Azure portal, **meer Services**, klikt u op **App registraties**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d290a-129">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="d290a-130">Zoeken naar de naam van uw toepassing in de lijst van app-rapporten:</span><span class="sxs-lookup"><span data-stu-id="d290a-130">Search for the name of your application in the list of app registrations:</span></span>

    ![Zoeken naar de toepassingsnaam van uw](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="d290a-132">Weergave de **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="d290a-132">Display the **Settings** blade.</span></span> <span data-ttu-id="d290a-133">In de **API-toegang** sectie **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="d290a-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="d290a-134">Klik op **toevoegen** toevoegen van een nieuwe vereiste machtiging.</span><span class="sxs-lookup"><span data-stu-id="d290a-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="d290a-135">Typ in stap 1, **Windows Azure Service Management API**, selecteert u die API in de lijst met resultaten en klikt u op de **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="d290a-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="d290a-136">In stap 2, schakel het selectievakje in naast **klassieke implementatiemodel van Azure toegang als gebruikers organisatie**, en klik op de **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="d290a-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="d290a-137">Klik op de **gedaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d290a-137">Click the **Done** button.</span></span>

<span data-ttu-id="d290a-138">De **Required Permissions** blade wordt nu weergegeven dat de machtigingen voor uw toepassing worden toegekend aan de ADAL- en het resourcemanager-API's.</span><span class="sxs-lookup"><span data-stu-id="d290a-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="d290a-139">Machtigingen worden verleend adal standaard, wanneer u uw app eerst bij Azure AD registreren.</span><span class="sxs-lookup"><span data-stu-id="d290a-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Machtigingen delegeren aan de API van Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="d290a-141">Azure AD-eindpunten</span><span class="sxs-lookup"><span data-stu-id="d290a-141">Azure AD endpoints</span></span>

<span data-ttu-id="d290a-142">Verificatie van uw Batch-beheeroplossingen met Azure AD, moet u twee bekende eindpunten.</span><span class="sxs-lookup"><span data-stu-id="d290a-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="d290a-143">De **algemene Azure AD-eindpunt** biedt een algemene referentie interface wanneer een specifieke tenant niet is opgegeven, zoals het geval van geïntegreerde verificatie te verzamelen:</span><span class="sxs-lookup"><span data-stu-id="d290a-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="d290a-144">De **Azure Resource Manager-eindpunt** wordt gebruikt voor het verkrijgen van een token voor het verifiëren van aanvragen naar de service Batch management:</span><span class="sxs-lookup"><span data-stu-id="d290a-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="d290a-145">De voorbeeldtoepassing AccountManagement definieert constanten voor deze eindpunten.</span><span class="sxs-lookup"><span data-stu-id="d290a-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="d290a-146">Laat deze constanten ongewijzigd:</span><span class="sxs-lookup"><span data-stu-id="d290a-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="d290a-147">Verwijst naar de toepassings-ID</span><span class="sxs-lookup"><span data-stu-id="d290a-147">Reference your application ID</span></span> 

<span data-ttu-id="d290a-148">De clienttoepassing gebruikt de toepassings-ID (ook wel de client-ID genoemd) voor toegang tot Azure AD tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="d290a-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="d290a-149">Nadat u uw toepassing hebt geregistreerd in de Azure portal, worden uw code voor het gebruik van de toepassings-ID die is opgegeven door Azure AD voor de geregistreerde toepassing bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d290a-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="d290a-150">In de voorbeeldtoepassing AccountManagement kopieert u de toepassings-ID van de Azure-portal op de juiste constante:</span><span class="sxs-lookup"><span data-stu-id="d290a-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="d290a-151">De omleidings-URI die u hebt opgegeven tijdens het registratieproces ook kopiëren.</span><span class="sxs-lookup"><span data-stu-id="d290a-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="d290a-152">Omleidings-URI in uw code opgegeven de moet overeenkomen met de omleidings-URI die u hebt opgegeven bij de registratie van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d290a-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="d290a-153">Een Azure AD-verificatietoken ophalen</span><span class="sxs-lookup"><span data-stu-id="d290a-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="d290a-154">Nadat u het voorbeeld AccountManagement in de Azure AD-tenant registreren en de voorbeeldcode van de bron met de waarden bijwerken, is het voorbeeld gereed om te verifiëren met behulp van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d290a-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="d290a-155">Wanneer u het voorbeeld uitvoert, probeert de ADAL geen verificatietoken ophalen.</span><span class="sxs-lookup"><span data-stu-id="d290a-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="d290a-156">Bij deze stap wordt u gevraagd uw referenties Microsoft:</span><span class="sxs-lookup"><span data-stu-id="d290a-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="d290a-157">Nadat u uw referenties opgeeft, wordt de voorbeeldtoepassing kunt doorgaan met het uitgeven van geverifieerde aanvragen naar de service Batch management.</span><span class="sxs-lookup"><span data-stu-id="d290a-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d290a-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d290a-158">Next steps</span></span>

<span data-ttu-id="d290a-159">Voor meer informatie over die wordt uitgevoerd de [AccountManagement voorbeeldtoepassing][acct_mgmt_sample], Zie [beheren Batch-accounts en quota's met de Batch-Management-clientbibliotheek voor .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d290a-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="d290a-160">Zie voor meer informatie over Azure AD, de [Azure Active Directory-documentatie](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="d290a-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="d290a-161">Gedetailleerde voorbeelden ziet u het gebruik van ADAL zijn beschikbaar in de [Azure codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=active-directory) bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="d290a-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="d290a-162">Als u wilt verifiëren Batch-service-toepassingen met behulp van Azure AD, Zie [oplossingen van de service Batch verifiëren met Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="d290a-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


<span data-ttu-id="d290a-163">[aad_about]: ../active-directory/active-directory-whatis.md "Wat is Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="d290a-163">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="d290a-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Verificatie-scenario's voor Azure AD"</span><span class="sxs-lookup"><span data-stu-id="d290a-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="d290a-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Toepassingen integreren met Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="d290a-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
