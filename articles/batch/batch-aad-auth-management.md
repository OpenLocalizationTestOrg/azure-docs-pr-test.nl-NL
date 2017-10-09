---
title: aaaUse Azure Active Directory tooauthenticate Batch beheeroplossingen | Microsoft Docs
description: "Toepassingen die zijn gebouwd met Azure resourcemanager en Hallo Batch-resourceprovider zich verifiëren met Azure AD."
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
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="8db54-103">Verificatie van oplossingen voor het beheer van de Batch met Active Directory</span><span class="sxs-lookup"><span data-stu-id="8db54-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="8db54-104">Toepassingen die hello Azure Batch Management-service aanroepen verifiëren met [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8db54-104">Applications that call hello Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="8db54-105">Azure AD is Microsoft multitenant-cloudgebaseerde adreslijst en identity management-service.</span><span class="sxs-lookup"><span data-stu-id="8db54-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="8db54-106">Azure zelf gebruikt Azure AD voor de verificatie van Hallo van zijn klanten, servicebeheerders en organisatie-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8db54-106">Azure itself uses Azure AD for hello authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="8db54-107">Hallo Batch Management .NET-bibliotheek wordt typen voor het werken met de Batch-accounts, toegangscodes, toepassingen en toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="8db54-107">hello Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="8db54-108">Hallo Batch Management .NET-bibliotheek is een Azure-resource provider-client en wordt gebruikt in combinatie met [Azure Resource Manager] [ resman_overview] toomanage deze resources via een programma.</span><span class="sxs-lookup"><span data-stu-id="8db54-108">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage these resources programmatically.</span></span> <span data-ttu-id="8db54-109">Azure AD is vereist tooauthenticate aanvragen via een Azure-resource provider client, waaronder Hallo Batch Management .NET-bibliotheek, en via [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="8db54-109">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="8db54-110">In dit artikel wordt besproken voor het gebruik van Azure AD-tooauthenticate uit toepassingen die gebruikmaken van Hallo Batch Management .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="8db54-110">In this article, we explore using Azure AD tooauthenticate from applications that use hello Batch Management .NET library.</span></span> <span data-ttu-id="8db54-111">Laten we zien hoe toouse Azure AD-tooauthenticate de abonnementsbeheerder van een of CO-beheerder, met behulp van verificatie geïntegreerde.</span><span class="sxs-lookup"><span data-stu-id="8db54-111">We show how toouse Azure AD tooauthenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="8db54-112">We gebruiken Hallo [AccountManagment] [ acct_mgmt_sample] voorbeeldproject, beschikbaar op GitHub, toowalk via met behulp van Azure AD met Hallo Batch Management .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="8db54-112">We use hello [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, toowalk through using Azure AD with hello Batch Management .NET library.</span></span>

<span data-ttu-id="8db54-113">toolearn meer over het gebruik van Hallo Batch Management .NET-bibliotheek en voorbeeld van de AccountManagement hello, Zie [beheren Batch-accounts en quota's met Hallo Batch Management-clientbibliotheek voor .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8db54-113">toolearn more about using hello Batch Management .NET library and hello AccountManagement sample, see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="8db54-114">Uw toepassing registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="8db54-114">Register your application with Azure AD</span></span>

<span data-ttu-id="8db54-115">Hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) biedt een programmeerinterface tooAzure AD voor gebruik binnen uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8db54-115">hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface tooAzure AD for use within your applications.</span></span> <span data-ttu-id="8db54-116">toocall ADAL van uw toepassing, moet u uw toepassing registreren in een Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8db54-116">toocall ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="8db54-117">Wanneer u uw toepassing registreert, kunt u Azure AD met informatie geven over uw toepassing, met inbegrip van een naam voor het binnen hello Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8db54-117">When you register your application, you supply Azure AD with information about your application, including a name for it within hello Azure AD tenant.</span></span> <span data-ttu-id="8db54-118">Vervolgens Azure AD levert een toepassings-ID dat u tooassociate uw toepassing met Azure AD tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="8db54-118">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="8db54-119">toolearn meer informatie over het Hallo-toepassings-ID, Zie [toepassing en service-principal objecten in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="8db54-119">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="8db54-120">tooregister hello AccountManagement voorbeeldtoepassing Hallo stappen in Hallo [een toepassing toe te voegen](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) in sectie [toepassingen integreren met Azure Active Directory] [ aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="8db54-120">tooregister hello AccountManagement sample application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="8db54-121">Geef **systeemeigen clienttoepassing** voor Hallo-type van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8db54-121">Specify **Native Client Application** for hello type of application.</span></span> <span data-ttu-id="8db54-122">Hallo bedrijfstak standaard OAuth 2.0-URI voor Hallo **omleidings-URI** is `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="8db54-122">hello industry standard OAuth 2.0 URI for hello **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="8db54-123">U kunt echter geldige URI opgeven (zoals `http://myaccountmanagementsample`) voor Hallo **omleidings-URI**, zoals niet toobe een echte eindpunt hoeft:</span><span class="sxs-lookup"><span data-stu-id="8db54-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for hello **Redirect URI**, as it does not need toobe a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="8db54-124">Nadat u het registratieproces Hallo hebt voltooid, u ziet dat Hallo toepassings-ID en Hallo object (service-principal)-ID van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="8db54-124">Once you complete hello registration process, you'll see hello application ID and hello object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a><span data-ttu-id="8db54-125">Hello Azure Resource Manager-API toegang tooyour toepassing verlenen</span><span class="sxs-lookup"><span data-stu-id="8db54-125">Grant hello Azure Resource Manager API access tooyour application</span></span>

<span data-ttu-id="8db54-126">Vervolgens moet u toodelegate toegang tooyour toepassing toohello Azure Resource Manager-API.</span><span class="sxs-lookup"><span data-stu-id="8db54-126">Next, you'll need toodelegate access tooyour application toohello Azure Resource Manager API.</span></span> <span data-ttu-id="8db54-127">Hello Azure AD-id voor Hallo Resource Manager-API is **Windows Azure Service Management API**.</span><span class="sxs-lookup"><span data-stu-id="8db54-127">hello Azure AD identifier for hello Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="8db54-128">Volg deze stappen in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="8db54-128">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="8db54-129">Kies in Hallo links navigatievenster van hello Azure-portal, **meer Services**, klikt u op **App registraties**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8db54-129">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="8db54-130">Hallo-naam van uw toepassing in de lijst Hallo van app-registraties zoeken:</span><span class="sxs-lookup"><span data-stu-id="8db54-130">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Zoeken naar de toepassingsnaam van uw](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="8db54-132">Weergave Hallo **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="8db54-132">Display hello **Settings** blade.</span></span> <span data-ttu-id="8db54-133">In Hallo **API-toegang** sectie **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="8db54-133">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="8db54-134">Klik op **toevoegen** tooadd een nieuwe vereiste machtiging.</span><span class="sxs-lookup"><span data-stu-id="8db54-134">Click **Add** tooadd a new required permission.</span></span> 
5. <span data-ttu-id="8db54-135">Typ in stap 1, **Windows Azure Service Management API**, selecteer die API van Hallo lijst met resultaten en klikt u op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="8db54-135">In step 1, enter **Windows Azure Service Management API**, select that API from hello list of results, and click hello **Select** button.</span></span>
6. <span data-ttu-id="8db54-136">In stap 2, selecteer Hallo selectievakje in naast te**klassieke implementatiemodel van Azure toegang als gebruikers organisatie**, en klik op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="8db54-136">In step 2, select hello check box next too**Access Azure classic deployment model as organization users**, and click hello **Select** button.</span></span>
7. <span data-ttu-id="8db54-137">Klik op Hallo **gedaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8db54-137">Click hello **Done** button.</span></span>

<span data-ttu-id="8db54-138">Hallo **Required Permissions** blade nu toont dat machtigingen tooyour toepassing tooboth worden toegekend Hallo ADAL en Resource Manager-API's.</span><span class="sxs-lookup"><span data-stu-id="8db54-138">hello **Required Permissions** blade now shows that permissions tooyour application are granted tooboth hello ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="8db54-139">Machtigingen worden verleend tooADAL standaard wanneer u uw app eerst bij Azure AD registreren.</span><span class="sxs-lookup"><span data-stu-id="8db54-139">Permissions are granted tooADAL by default when you first register your app with Azure AD.</span></span>

![Delegeren van machtigingen toohello Azure Resource Manager-API](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="8db54-141">Azure AD-eindpunten</span><span class="sxs-lookup"><span data-stu-id="8db54-141">Azure AD endpoints</span></span>

<span data-ttu-id="8db54-142">tooauthenticate uw Batch-Management-oplossingen in Azure AD, moet u twee bekende eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8db54-142">tooauthenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="8db54-143">Hallo **algemene Azure AD-eindpunt** biedt een algemene referentie interface verzamelen als een specifieke tenant niet is opgegeven, net als bij Hallo geïntegreerde verificatie:</span><span class="sxs-lookup"><span data-stu-id="8db54-143">hello **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in hello case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="8db54-144">Hallo **Azure Resource Manager-eindpunt** gebruikte tooacquire is een token voor het verifiëren van aanvragen toohello Batch management-service:</span><span class="sxs-lookup"><span data-stu-id="8db54-144">hello **Azure Resource Manager endpoint** is used tooacquire a token for authenticating requests toohello Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="8db54-145">Hallo AccountManagement voorbeeldtoepassing definieert constanten voor deze eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8db54-145">hello AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="8db54-146">Laat deze constanten ongewijzigd:</span><span class="sxs-lookup"><span data-stu-id="8db54-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="8db54-147">Verwijst naar de toepassings-ID</span><span class="sxs-lookup"><span data-stu-id="8db54-147">Reference your application ID</span></span> 

<span data-ttu-id="8db54-148">Uw clienttoepassing gebruikmaakt van Hallo toepassing-ID (ook waarnaar wordt verwezen tooas Hallo client-ID) tooaccess Azure AD tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="8db54-148">Your client application uses hello application ID (also referred tooas hello client ID) tooaccess Azure AD at runtime.</span></span> <span data-ttu-id="8db54-149">Nadat u uw toepassing in hello Azure-portal hebt geregistreerd, worden uw code toouse Hallo toepassings-ID opgegeven door Azure AD voor de geregistreerde toepassing bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8db54-149">Once you've registered your application in hello Azure portal, update your code toouse hello application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="8db54-150">In Hallo AccountManagement voorbeeldtoepassing, kopieert u de toepassings-ID van hello Azure portal toohello juiste constante:</span><span class="sxs-lookup"><span data-stu-id="8db54-150">In hello AccountManagement sample application, copy your application ID from hello Azure portal toohello appropriate constant:</span></span>

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="8db54-151">Hallo omleidings-URI die u hebt opgegeven tijdens het registratieproces Hallo ook kopiëren.</span><span class="sxs-lookup"><span data-stu-id="8db54-151">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="8db54-152">Hallo redirect die URI in uw code opgegeven moet overeenkomen met de Hallo omleidings-URI die u hebt opgegeven bij de registratie van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="8db54-152">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application.</span></span>

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="8db54-153">Een Azure AD-verificatietoken ophalen</span><span class="sxs-lookup"><span data-stu-id="8db54-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="8db54-154">Nadat u Hallo AccountManagement voorbeeld in hello Azure AD-tenant registreren en voorbeeldcode Hallo met de waarden bijwerken, is een voorbeeld van Hallo gereed tooauthenticate gebruikmaken van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8db54-154">After you register hello AccountManagement sample in hello Azure AD tenant and update hello sample source code with your values, hello sample is ready tooauthenticate using Azure AD.</span></span> <span data-ttu-id="8db54-155">Wanneer u Hallo voorbeeld uitvoert, probeert Hallo ADAL tooacquire geen verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="8db54-155">When you run hello sample, hello ADAL attempts tooacquire an authentication token.</span></span> <span data-ttu-id="8db54-156">Bij deze stap wordt u gevraagd uw referenties Microsoft:</span><span class="sxs-lookup"><span data-stu-id="8db54-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="8db54-157">Nadat u uw referenties opgeeft, kan de voorbeeldtoepassing Hallo tooissue geverifieerde aanvragen toohello Batch management-service kunt doorgaan.</span><span class="sxs-lookup"><span data-stu-id="8db54-157">After you provide your credentials, hello sample application can proceed tooissue authenticated requests toohello Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8db54-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8db54-158">Next steps</span></span>

<span data-ttu-id="8db54-159">Voor meer informatie over het uitvoeren van Hallo [AccountManagement voorbeeldtoepassing][acct_mgmt_sample], Zie [beheren Batch-accounts en quota's met Hallo Batch Management-clientbibliotheek voor .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8db54-159">For more information on running hello [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="8db54-160">toolearn meer informatie over Azure AD, Zie Hallo [Azure Active Directory-documentatie](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="8db54-160">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="8db54-161">Gedetailleerde voorbeelden ziet u hoe toouse ADAL zijn beschikbaar in Hallo [Azure codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=active-directory) bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="8db54-161">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="8db54-162">Zie tooauthenticate Batch-service-toepassingen die gebruikmaken van Azure AD [oplossingen van de service Batch verifiëren met Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="8db54-162">tooauthenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]: ../active-directory/active-directory-whatis.md "Wat is Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Verificatie-scenario's voor Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Toepassingen integreren met Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
