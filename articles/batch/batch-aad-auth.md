---
title: "Azure Active Directory gebruiken om te verifiëren van Azure Batch serviceoplossingen | Microsoft Docs"
description: Batch ondersteunt Azure AD voor de verificatie van de Batch-service.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 9c03bde919c46cd301229255c0b12ee69dda6f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="ed71a-103">Verificatie van oplossingen voor Batch-service met Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed71a-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="ed71a-104">Azure Batch biedt ondersteuning voor verificatie met [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed71a-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="ed71a-105">Azure AD is Microsoft multitenant-cloudgebaseerde adreslijst en identity management-service.</span><span class="sxs-lookup"><span data-stu-id="ed71a-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="ed71a-106">Azure zelf Azure AD gebruikt voor verificatie van zijn klanten, servicebeheerders en organisatie-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ed71a-106">Azure itself uses Azure AD to authenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="ed71a-107">Als u Azure AD-verificatie met Azure Batch, kunt u verifiëren op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="ed71a-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="ed71a-108">Met behulp van **geïntegreerde verificatie** een gebruiker die de interactie is met de toepassing te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="ed71a-108">By using **integrated authentication** to authenticate a user that is interacting with the application.</span></span> <span data-ttu-id="ed71a-109">Een toepassing met geïntegreerde verificatie van de gebruiker referenties moeten worden verzameld en gebruikt deze referenties voor het verifiëren van toegang tot de Batch-resources.</span><span class="sxs-lookup"><span data-stu-id="ed71a-109">An application using integrated authentication gathers a user's credentials and uses those credentials to authenticate access to Batch resources.</span></span>
- <span data-ttu-id="ed71a-110">Met behulp van een **service-principal** om te verifiëren van een toepassing zonder toezicht.</span><span class="sxs-lookup"><span data-stu-id="ed71a-110">By using a **service principal** to authenticate an unattended application.</span></span> <span data-ttu-id="ed71a-111">Een service-principal definieert het beleid en de machtigingen voor een toepassing om de toepassing te vertegenwoordigen wanneer toegang tot bronnen tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="ed71a-111">A service principal defines the policy and permissions for an application in order to represent the application when accessing resources at runtime.</span></span>

<span data-ttu-id="ed71a-112">Zie voor meer informatie over Azure AD, de [Azure Active Directory-documentatie](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="ed71a-112">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="ed71a-113">Verificatie- en groep toewijzing-modus</span><span class="sxs-lookup"><span data-stu-id="ed71a-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="ed71a-114">Wanneer u een Batch-account maakt, kunt u opgeven waar de groepen die zijn gemaakt voor dat account moeten worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ed71a-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="ed71a-115">U kunt groepen in het standaard Batch-service-abonnement of in een gebruikerabonnement toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ed71a-115">You can choose to allocate pools either in the default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="ed71a-116">Uw keuze is van invloed op hoe u toegang tot bronnen in het account te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="ed71a-116">Your choice affects how you authenticate access to resources in that account.</span></span>

- <span data-ttu-id="ed71a-117">**Batch-service-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-117">**Batch service subscription**.</span></span> <span data-ttu-id="ed71a-118">Batch-pools worden standaard toegewezen in een Batch-service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ed71a-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="ed71a-119">Als u deze optie kiest, u toegang tot bronnen in het account kunt verifiëren met [gedeelde sleutel](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) of met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed71a-119">If you choose this option, you can authenticate access to resources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="ed71a-120">**Gebruikerabonnement.**</span><span class="sxs-lookup"><span data-stu-id="ed71a-120">**User subscription.**</span></span> <span data-ttu-id="ed71a-121">U kunt kiezen om toe te wijzen Batch-pools in een gebruikerabonnement die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="ed71a-121">You can choose to allocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="ed71a-122">Als u deze optie kiest, moet u verifiëren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed71a-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="ed71a-123">Eindpunten voor verificatie</span><span class="sxs-lookup"><span data-stu-id="ed71a-123">Endpoints for authentication</span></span>

<span data-ttu-id="ed71a-124">Om te verifiëren Batch-toepassingen met Azure AD, moet u een aantal bekende eindpunten opnemen in uw code.</span><span class="sxs-lookup"><span data-stu-id="ed71a-124">To authenticate Batch applications with Azure AD, you need to include some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="ed71a-125">Azure AD-eindpunt</span><span class="sxs-lookup"><span data-stu-id="ed71a-125">Azure AD endpoint</span></span>

<span data-ttu-id="ed71a-126">De base Azure AD authority-eindpunt is:</span><span class="sxs-lookup"><span data-stu-id="ed71a-126">The base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="ed71a-127">Om te verifiëren met Azure AD, moet u dit eindpunt samen met de tenant-ID (directory-ID) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed71a-127">To authenticate with Azure AD, you use this endpoint together with the tenant ID (directory ID).</span></span> <span data-ttu-id="ed71a-128">De tenant-ID identificeert de Azure AD-tenant wilt gebruiken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="ed71a-128">The tenant ID identifies the Azure AD tenant to use for authentication.</span></span> <span data-ttu-id="ed71a-129">Volg de stappen in voor het ophalen van de tenant-ID, [de tenant-ID niet ophalen voor uw Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="ed71a-129">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="ed71a-130">Het eindpunt tenantspecifieke is vereist wanneer u verifiëren met behulp van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="ed71a-130">The tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="ed71a-131">Het eindpunt tenantspecifieke is optioneel wanneer u verifiëren met behulp van geïntegreerde verificatie, maar aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="ed71a-131">The tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="ed71a-132">U kunt echter ook het Azure AD gemeenschappelijk eindpunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed71a-132">However, you can also use the Azure AD common endpoint.</span></span> <span data-ttu-id="ed71a-133">Het algemene eindpunt biedt een algemene referentie interface verzamelen als een specifieke tenant is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ed71a-133">The common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="ed71a-134">Het eindpunt van de algemene heeft `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="ed71a-134">The common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="ed71a-135">Zie voor meer informatie over Azure AD-eindpunten [verificatie scenario's voor Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="ed71a-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="ed71a-136">Eindpunt voor batch-resource</span><span class="sxs-lookup"><span data-stu-id="ed71a-136">Batch resource endpoint</span></span>

<span data-ttu-id="ed71a-137">Gebruik de **endpoint van Azure Batch-resource** te verkrijgen van een token voor het verifiëren van aanvragen voor de Batch-service:</span><span class="sxs-lookup"><span data-stu-id="ed71a-137">Use the **Azure Batch resource endpoint** to acquire a token for authenticating requests to the Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="ed71a-138">Uw toepassing registreren met een tenant</span><span class="sxs-lookup"><span data-stu-id="ed71a-138">Register your application with a tenant</span></span>

<span data-ttu-id="ed71a-139">De eerste stap bij het gebruik van Azure AD om te verifiëren, is uw toepassing registreren in een Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="ed71a-139">The first step in using Azure AD to authenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="ed71a-140">Registreren van uw toepassing, kunt u de Azure aanroepen [Active Directory Authentication Library] [ aad_adal] (ADAL) vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="ed71a-140">Registering your application enables you to call the Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="ed71a-141">De ADAL biedt een API voor de verificatie met Azure AD van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-141">The ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="ed71a-142">Registreren van uw toepassing is vereist of u van plan bent om geïntegreerde verificatie of een service-principal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed71a-142">Registering your application is required whether you plan to use integrated authentication or a service principal.</span></span>

<span data-ttu-id="ed71a-143">Wanneer u uw toepassing registreert, kunt u informatie opgeven over uw toepassing naar Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed71a-143">When you register your application, you supply information about your application to Azure AD.</span></span> <span data-ttu-id="ed71a-144">Vervolgens Azure AD levert een toepassings-ID waarmee u uw toepassing koppelen aan Azure AD tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="ed71a-144">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="ed71a-145">Zie voor meer informatie over de toepassings-ID, [toepassing en service-principal objecten in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="ed71a-145">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="ed71a-146">Voor het registreren van uw Batch-toepassing, volg de stappen in de [een toepassing toe te voegen](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) in sectie [toepassingen integreren met Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="ed71a-146">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="ed71a-147">Als u uw toepassing als een systeemeigen toepassing registreren, kunt u een geldige URI voor de **omleidings-URI**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-147">If you register your application as a Native Application, you can specify any valid URI for the **Redirect URI**.</span></span> <span data-ttu-id="ed71a-148">Dit hoeft niet te worden van een echte-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ed71a-148">It does not need to be a real endpoint.</span></span>

<span data-ttu-id="ed71a-149">Nadat u uw toepassing hebt geregistreerd, ziet u de toepassings-ID:</span><span class="sxs-lookup"><span data-stu-id="ed71a-149">After you've registered your application, you'll see the application ID:</span></span>

![De Batch-toepassing registreren met Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="ed71a-151">Zie voor meer informatie over het registreren van een toepassing met Azure AD [verificatie scenario's voor Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="ed71a-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-the-tenant-id-for-your-active-directory"></a><span data-ttu-id="ed71a-152">De tenant-ID niet ophalen voor uw Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed71a-152">Get the tenant ID for your Active Directory</span></span>

<span data-ttu-id="ed71a-153">De tenant-ID identificeert de Azure AD-tenant waarmee verificatieservices voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-153">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="ed71a-154">Als u de tenant-ID, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ed71a-154">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="ed71a-155">Selecteer uw Active Directory in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ed71a-155">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="ed71a-156">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-156">Click **Properties**.</span></span>
3. <span data-ttu-id="ed71a-157">Kopieer de GUID-waarde opgegeven voor de map-ID.</span><span class="sxs-lookup"><span data-stu-id="ed71a-157">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="ed71a-158">Deze waarde wordt ook aangeroepen voor de tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="ed71a-158">This value is also called the tenant ID.</span></span>

![Kopieer de map-ID](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="ed71a-160">Gebruik van geïntegreerde verificatie</span><span class="sxs-lookup"><span data-stu-id="ed71a-160">Use integrated authentication</span></span>

<span data-ttu-id="ed71a-161">Om te verifiëren met geïntegreerde verificatie, moet u de machtigingen van uw toepassing verbinding maken met de API van Batch-service.</span><span class="sxs-lookup"><span data-stu-id="ed71a-161">To authenticate with integrated authentication, you need to grant your application permissions to connect to the Batch service API.</span></span> <span data-ttu-id="ed71a-162">Deze stap kunt uw toepassing om te verifiëren van aanroepen naar de API van Batch-service met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed71a-162">This step enables your application to authenticate calls to the Batch service API with Azure AD.</span></span>

<span data-ttu-id="ed71a-163">Zodra u hebt [geregistreerd van uw toepassing](#register-your-application-with-an-azure-ad-tenant), als volgt te werk in de Azure portal naar het toegang geven tot de Batch-service:</span><span class="sxs-lookup"><span data-stu-id="ed71a-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in the Azure portal to grant it access to the Batch service:</span></span>

1. <span data-ttu-id="ed71a-164">Kies in het navigatiedeelvenster links van de Azure portal, **meer Services**, klikt u op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-164">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="ed71a-165">Zoeken naar de naam van uw toepassing in de lijst van app-rapporten:</span><span class="sxs-lookup"><span data-stu-id="ed71a-165">Search for the name of your application in the list of app registrations:</span></span>

    ![Zoeken naar de toepassingsnaam van uw](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="ed71a-167">Open de **instellingen** blade voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-167">Open the **Settings** blade for your application.</span></span> <span data-ttu-id="ed71a-168">In de **API-toegang** sectie **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-168">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="ed71a-169">In de **vereist machtigingen** blade, klikt u op de **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ed71a-169">In the **Required permissions** blade, click the **Add** button.</span></span>
5. <span data-ttu-id="ed71a-170">In stap 1, zoekt u de Batch-API.</span><span class="sxs-lookup"><span data-stu-id="ed71a-170">In step 1, search for the Batch API.</span></span> <span data-ttu-id="ed71a-171">Zoek deze tekenreeksen totdat u de API hebt gevonden:</span><span class="sxs-lookup"><span data-stu-id="ed71a-171">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="ed71a-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="ed71a-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="ed71a-174">Nieuwere Azure AD-tenants kunnen deze naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed71a-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="ed71a-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is de id voor de Batch-API.</span><span class="sxs-lookup"><span data-stu-id="ed71a-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 
6. <span data-ttu-id="ed71a-176">Als u de Batch-API hebt gevonden, selecteert u deze en klikt u op de **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="ed71a-176">Once you find the Batch API, select it and click the **Select** button.</span></span>
6. <span data-ttu-id="ed71a-177">In stap 2, schakel het selectievakje in naast **Access Azure Batch-Service** en klik op de **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="ed71a-177">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span></span>
7. <span data-ttu-id="ed71a-178">Klik op de **gedaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ed71a-178">Click the **Done** button.</span></span>

<span data-ttu-id="ed71a-179">De **Required Permissions** blade nu service bevat die uw Azure AD-toepassing toegang tot zowel ADAL als de Batch heeft-API.</span><span class="sxs-lookup"><span data-stu-id="ed71a-179">The **Required Permissions** blade now shows that your Azure AD application has access to both ADAL and the Batch service API.</span></span> <span data-ttu-id="ed71a-180">Machtigingen worden verleend aan ADAL automatisch wanneer u uw app eerst bij Azure AD registreren.</span><span class="sxs-lookup"><span data-stu-id="ed71a-180">Permissions are granted to ADAL automatically when you first register your app with Azure AD.</span></span>

![Machtigingen verlenen API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="ed71a-182">Gebruik van een service-principal</span><span class="sxs-lookup"><span data-stu-id="ed71a-182">Use a service principal</span></span> 

<span data-ttu-id="ed71a-183">Verificatie van een toepassing die wordt uitgevoerd zonder toezicht, moet u een service-principal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed71a-183">To authenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="ed71a-184">Nadat u uw toepassing hebt geregistreerd, volg deze stappen in de Azure portal voor het configureren van een service-principal:</span><span class="sxs-lookup"><span data-stu-id="ed71a-184">After you've registered your application, follow these steps in the Azure portal to configure a service principal:</span></span>

1. <span data-ttu-id="ed71a-185">Vraagt u een geheime sleutel voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="ed71a-186">RBAC-rol toewijzen aan uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-186">Assign an RBAC role to your application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="ed71a-187">Vraagt u een geheime sleutel voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="ed71a-187">Request a secret key for your application</span></span>

<span data-ttu-id="ed71a-188">Als uw toepassing zich met een service-principal verifieert, worden zowel de toepassings-ID en een geheime sleutel naar Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed71a-188">When your application authenticates with a service principal, it sends both the application ID and a secret key to Azure AD.</span></span> <span data-ttu-id="ed71a-189">U moet maken en kopieer de geheime sleutel van uw code te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed71a-189">You'll need to create and copy the secret key to use from your code.</span></span>

<span data-ttu-id="ed71a-190">Volg deze stappen in de Azure portal:</span><span class="sxs-lookup"><span data-stu-id="ed71a-190">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="ed71a-191">Kies in het navigatiedeelvenster links van de Azure portal, **meer Services**, klikt u op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-191">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="ed71a-192">Zoek de naam van uw toepassing in de lijst van app-registraties.</span><span class="sxs-lookup"><span data-stu-id="ed71a-192">Search for the name of your application in the list of app registrations.</span></span>
3. <span data-ttu-id="ed71a-193">Weergave de **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="ed71a-193">Display the **Settings** blade.</span></span> <span data-ttu-id="ed71a-194">In de **API-toegang** sectie **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-194">In the **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="ed71a-195">Voer een beschrijving voor de sleutel voor het maken van een sleutel.</span><span class="sxs-lookup"><span data-stu-id="ed71a-195">To create a key, enter a description for the key.</span></span> <span data-ttu-id="ed71a-196">Selecteer vervolgens een duur voor de sleutel van één of twee jaar.</span><span class="sxs-lookup"><span data-stu-id="ed71a-196">Then select a duration for the key of either one or two years.</span></span> 
5. <span data-ttu-id="ed71a-197">Klik op de **opslaan** knop maken en weergeven van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="ed71a-197">Click the **Save** button to create and display the key.</span></span> <span data-ttu-id="ed71a-198">De sleutelwaarde kopiëren naar een veilige plaats als het niet mogelijk toegang tot het opnieuw nadat u de blade laat.</span><span class="sxs-lookup"><span data-stu-id="ed71a-198">Copy the key value to a safe place, as you won't be able to access it again after you leave the blade.</span></span> 

    ![Maken van een geheime sleutel](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-to-your-application"></a><span data-ttu-id="ed71a-200">Een RBAC-rol toewijzen aan uw toepassing</span><span class="sxs-lookup"><span data-stu-id="ed71a-200">Assign an RBAC role to your application</span></span>

<span data-ttu-id="ed71a-201">Om te verifiëren met een service-principal, moet u een RBAC-rol toewijzen aan uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-201">To authenticate with a service principal, you need to assign an RBAC role to your application.</span></span> <span data-ttu-id="ed71a-202">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="ed71a-202">Follow these steps:</span></span>

1. <span data-ttu-id="ed71a-203">Ga in de Azure-portal naar het Batch-account wordt gebruikt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-203">In the Azure portal, navigate to the Batch account used by your application.</span></span>
2. <span data-ttu-id="ed71a-204">In de **instellingen** blade voor het Batch-account, selecteer **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-204">In the **Settings** blade for the Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="ed71a-205">Klik op de **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ed71a-205">Click the **Add** button.</span></span> 
4. <span data-ttu-id="ed71a-206">Van de **rol** vervolgkeuzelijst, kiest u de _Inzender_ of _lezer_ rol voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-206">From the **Role** drop-down, choose either the _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="ed71a-207">Zie voor meer informatie over deze rollen [aan de slag met toegangsbeheer op basis van rollen in Azure portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="ed71a-207">For more information on these roles, see [Get started with Role-Based Access Control in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="ed71a-208">In de **Selecteer** en voer de naam van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-208">In the **Select** field, enter the name of your application.</span></span> <span data-ttu-id="ed71a-209">Selecteer uw toepassing uit de lijst en klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-209">Select your application from the list, and click **Save**.</span></span>

<span data-ttu-id="ed71a-210">Uw toepassing wordt nu weergegeven in de instellingen voor toegangsbeheer met een RBAC-rol die is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ed71a-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Een RBAC-rol toewijzen aan uw toepassing](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="ed71a-212">De tenant-ID niet ophalen voor uw Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed71a-212">Get the tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="ed71a-213">De tenant-ID identificeert de Azure AD-tenant waarmee verificatieservices voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-213">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="ed71a-214">Als u de tenant-ID, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ed71a-214">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="ed71a-215">Selecteer uw Active Directory in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ed71a-215">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="ed71a-216">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="ed71a-216">Click **Properties**.</span></span>
3. <span data-ttu-id="ed71a-217">Kopieer de GUID-waarde opgegeven voor de map-ID.</span><span class="sxs-lookup"><span data-stu-id="ed71a-217">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="ed71a-218">Deze waarde wordt ook aangeroepen voor de tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="ed71a-218">This value is also called the tenant ID.</span></span>

![Kopieer de map-ID](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="ed71a-220">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="ed71a-220">Code examples</span></span>

<span data-ttu-id="ed71a-221">De codevoorbeelden in deze sectie laten zien hoe om te verifiëren met Azure AD dat gebruikmaakt van geïntegreerde verificatie en met een service-principal.</span><span class="sxs-lookup"><span data-stu-id="ed71a-221">The code examples in this section show how to authenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="ed71a-222">Deze codevoorbeelden .NET gebruiken, maar de concepten zijn vergelijkbaar voor andere talen.</span><span class="sxs-lookup"><span data-stu-id="ed71a-222">These code examples use .NET, but the concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="ed71a-223">Een Azure AD authentication-token verloopt na één uur.</span><span class="sxs-lookup"><span data-stu-id="ed71a-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="ed71a-224">Wanneer u een lange levensduur **BatchClient** object, het is raadzaam dat u een token van ADAL bij elke aanvraag om te controleren of er altijd een geldig token ophalen.</span><span class="sxs-lookup"><span data-stu-id="ed71a-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="ed71a-225">Om dit te bereiken in .NET, schrijven van een methode die het token opgehaald uit Azure AD en geeft deze methode een **BatchTokenCredentials** object als een gemachtigde.</span><span class="sxs-lookup"><span data-stu-id="ed71a-225">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="ed71a-226">De gemachtigdenmethode wordt aangeroepen bij elke aanvraag naar de Batch-service om ervoor te zorgen dat een geldig token moet worden verstrekt.</span><span class="sxs-lookup"><span data-stu-id="ed71a-226">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span></span> <span data-ttu-id="ed71a-227">Standaard ADAL in de cache opgeslagen tokens, zodat een nieuw token is opgehaald uit Azure AD alleen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="ed71a-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="ed71a-228">Zie voor meer informatie over tokens in Azure AD [verificatie scenario's voor Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="ed71a-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="ed71a-229">Voorbeeld: met behulp van Azure AD geïntegreerde verificatie met Batch .NET</span><span class="sxs-lookup"><span data-stu-id="ed71a-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="ed71a-230">Om te verifiëren met geïntegreerde verificatie van de Batch .NET, verwijst naar de [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) pakket en de [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pakket.</span><span class="sxs-lookup"><span data-stu-id="ed71a-230">To authenticate with integrated authentication from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="ed71a-231">De volgende `using` instructies in uw code:</span><span class="sxs-lookup"><span data-stu-id="ed71a-231">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="ed71a-232">Verwijzing naar de Azure AD-eindpunt in uw code, met inbegrip van de tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="ed71a-232">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="ed71a-233">Volg de stappen in voor het ophalen van de tenant-ID, [de tenant-ID niet ophalen voor uw Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="ed71a-233">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="ed71a-234">Verwijzen naar het eindpunt van Batch-service resource:</span><span class="sxs-lookup"><span data-stu-id="ed71a-234">Reference the Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="ed71a-235">Verwijzen naar uw Batch-account:</span><span class="sxs-lookup"><span data-stu-id="ed71a-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="ed71a-236">Geef de toepassings-ID (client-ID) voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-236">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="ed71a-237">De toepassings-ID is beschikbaar via de registratie van uw app in de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="ed71a-237">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="ed71a-238">De omleidings-URI die u hebt opgegeven tijdens het registratieproces ook kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ed71a-238">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="ed71a-239">Omleidings-URI in uw code opgegeven de moet overeenkomen met de omleidings-URI die u hebt opgegeven bij de registratie van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="ed71a-239">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="ed71a-240">Schrijven van een callback-methode te verkrijgen van het verificatietoken van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed71a-240">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="ed71a-241">De **GetAuthenticationTokenAsync** retouraanroepmethode aanroepen ADAL voor verificatie van een gebruiker die de interactie is met de toepassing hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ed71a-241">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL to authenticate a user who is interacting with the application.</span></span> <span data-ttu-id="ed71a-242">De **AcquireTokenAsync** methode geleverd door ADAL vraagt de gebruiker om hun referenties en de toepassing voortgezet nadat de gebruiker deze heeft (tenzij deze al in de cache referenties opgeslagen is):</span><span class="sxs-lookup"><span data-stu-id="ed71a-242">The **AcquireTokenAsync** method provided by ADAL prompts the user for their credentials, and the application proceeds once the user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="ed71a-243">Samen een **BatchTokenCredentials** object waarmee de gemachtigde als parameter.</span><span class="sxs-lookup"><span data-stu-id="ed71a-243">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="ed71a-244">Deze referenties gebruiken om te openen een **BatchClient** object.</span><span class="sxs-lookup"><span data-stu-id="ed71a-244">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="ed71a-245">U kunt die **BatchClient** object voor verdere bewerkingen op basis van de Batch-service:</span><span class="sxs-lookup"><span data-stu-id="ed71a-245">You can use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="ed71a-246">Voorbeeld: met behulp van een Azure AD-service-principal met Batch .NET</span><span class="sxs-lookup"><span data-stu-id="ed71a-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="ed71a-247">Om te verifiëren met een service-principal in Batch .NET, verwijst naar de [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) pakket en de [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pakket.</span><span class="sxs-lookup"><span data-stu-id="ed71a-247">To authenticate with a service principal from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="ed71a-248">De volgende `using` instructies in uw code:</span><span class="sxs-lookup"><span data-stu-id="ed71a-248">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="ed71a-249">Verwijzing naar de Azure AD-eindpunt in uw code, met inbegrip van de tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="ed71a-249">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="ed71a-250">Wanneer u een service-principal gebruikt, moet u een eindpunt tenantspecifieke opgeven.</span><span class="sxs-lookup"><span data-stu-id="ed71a-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="ed71a-251">Volg de stappen in voor het ophalen van de tenant-ID, [de tenant-ID niet ophalen voor uw Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="ed71a-251">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="ed71a-252">Verwijzen naar het eindpunt van Batch-service resource:</span><span class="sxs-lookup"><span data-stu-id="ed71a-252">Reference the Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="ed71a-253">Verwijzen naar uw Batch-account:</span><span class="sxs-lookup"><span data-stu-id="ed71a-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="ed71a-254">Geef de toepassings-ID (client-ID) voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed71a-254">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="ed71a-255">De toepassings-ID is beschikbaar via de registratie van uw app in de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="ed71a-255">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="ed71a-256">Geef de geheime sleutel die u hebt gekopieerd uit de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="ed71a-256">Specify the secret key that you copied from the Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="ed71a-257">Schrijven van een callback-methode te verkrijgen van het verificatietoken van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed71a-257">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="ed71a-258">De **GetAuthenticationTokenAsync** retouraanroepmethode aanroepen ADAL voor verificatie zonder toezicht hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ed71a-258">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="ed71a-259">Samen een **BatchTokenCredentials** object waarmee de gemachtigde als parameter.</span><span class="sxs-lookup"><span data-stu-id="ed71a-259">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="ed71a-260">Deze referenties gebruiken om te openen een **BatchClient** object.</span><span class="sxs-lookup"><span data-stu-id="ed71a-260">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="ed71a-261">Vervolgens kunt u die **BatchClient** object voor verdere bewerkingen op basis van de Batch-service:</span><span class="sxs-lookup"><span data-stu-id="ed71a-261">You can then use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="ed71a-262">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ed71a-262">Next steps</span></span>

<span data-ttu-id="ed71a-263">Zie voor meer informatie over Azure AD, de [Azure Active Directory-documentatie](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="ed71a-263">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="ed71a-264">Gedetailleerde voorbeelden ziet u het gebruik van ADAL zijn beschikbaar in de [Azure codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=active-directory) bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="ed71a-264">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="ed71a-265">Zie voor meer informatie over service-principals, [toepassing en service-principal objecten in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="ed71a-265">To learn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="ed71a-266">Zie het maken van een service-principal met de Azure portal [portal gebruik maken van Active Directory-toepassing en service-principal die toegang bronnen tot](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ed71a-266">To create a service principal using the Azure portal, see [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="ed71a-267">U kunt ook een service-principal maken met PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ed71a-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="ed71a-268">Om te verifiëren met behulp van Azure AD Batch beheertoepassingen, Zie [oplossingen voor het beheer van Batch verifiëren met Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="ed71a-268">To authenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

<span data-ttu-id="ed71a-269">[aad_about]: ../active-directory/active-directory-whatis.md "Wat is Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="ed71a-269">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="ed71a-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Verificatie-scenario's voor Azure AD"</span><span class="sxs-lookup"><span data-stu-id="ed71a-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="ed71a-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Toepassingen integreren met Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="ed71a-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[azure_portal]: http://portal.azure.com
