---
title: oplossingen voor aaaUse Azure Active Directory tooauthenticate Azure Batch-service | Microsoft Docs
description: Batch ondersteunt Azure AD voor de verificatie van Hallo Batch-service.
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
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="25dad-103">Verificatie van oplossingen voor Batch-service met Active Directory</span><span class="sxs-lookup"><span data-stu-id="25dad-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="25dad-104">Azure Batch biedt ondersteuning voor verificatie met [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25dad-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="25dad-105">Azure AD is Microsoft multitenant-cloudgebaseerde adreslijst en identity management-service.</span><span class="sxs-lookup"><span data-stu-id="25dad-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="25dad-106">Azure zelf tooauthenticate Azure AD gebruikt, zijn klanten, servicebeheerders en organisatie-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="25dad-106">Azure itself uses Azure AD tooauthenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="25dad-107">Als u Azure AD-verificatie met Azure Batch, kunt u verifiëren op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="25dad-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="25dad-108">Met behulp van **geïntegreerde verificatie** tooauthenticate een gebruiker die de interactie met Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="25dad-108">By using **integrated authentication** tooauthenticate a user that is interacting with hello application.</span></span> <span data-ttu-id="25dad-109">Een toepassing met geïntegreerde verificatie worden verzameld van de referenties van een gebruiker en gebruikt deze referenties tooauthenticate toegang tooBatch resources.</span><span class="sxs-lookup"><span data-stu-id="25dad-109">An application using integrated authentication gathers a user's credentials and uses those credentials tooauthenticate access tooBatch resources.</span></span>
- <span data-ttu-id="25dad-110">Met behulp van een **service-principal** tooauthenticate een toepassing zonder toezicht.</span><span class="sxs-lookup"><span data-stu-id="25dad-110">By using a **service principal** tooauthenticate an unattended application.</span></span> <span data-ttu-id="25dad-111">Een service-principal definieert Hallo beleid en machtigingen voor een toepassing in volgorde toorepresent Hallo toepassing bij het openen van bronnen tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="25dad-111">A service principal defines hello policy and permissions for an application in order toorepresent hello application when accessing resources at runtime.</span></span>

<span data-ttu-id="25dad-112">toolearn meer informatie over Azure AD, Zie Hallo [Azure Active Directory-documentatie](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="25dad-112">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="25dad-113">Verificatie- en groep toewijzing-modus</span><span class="sxs-lookup"><span data-stu-id="25dad-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="25dad-114">Wanneer u een Batch-account maakt, kunt u opgeven waar de groepen die zijn gemaakt voor dat account moeten worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="25dad-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="25dad-115">U kunt groepen tooallocate in Hallo standaard Batch-service-abonnement of in een gebruikerabonnement.</span><span class="sxs-lookup"><span data-stu-id="25dad-115">You can choose tooallocate pools either in hello default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="25dad-116">Uw keuze is van invloed op hoe u toegang tooresources in het account verifiëren.</span><span class="sxs-lookup"><span data-stu-id="25dad-116">Your choice affects how you authenticate access tooresources in that account.</span></span>

- <span data-ttu-id="25dad-117">**Batch-service-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="25dad-117">**Batch service subscription**.</span></span> <span data-ttu-id="25dad-118">Batch-pools worden standaard toegewezen in een Batch-service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="25dad-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="25dad-119">Als u deze optie kiest, kunt u verifiëren toegang tooresources in het account met [gedeelde sleutel](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) of met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25dad-119">If you choose this option, you can authenticate access tooresources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="25dad-120">**Gebruikerabonnement.**</span><span class="sxs-lookup"><span data-stu-id="25dad-120">**User subscription.**</span></span> <span data-ttu-id="25dad-121">U kunt tooallocate Batch-pools in een gebruikerabonnement die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="25dad-121">You can choose tooallocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="25dad-122">Als u deze optie kiest, moet u verifiëren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25dad-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="25dad-123">Eindpunten voor verificatie</span><span class="sxs-lookup"><span data-stu-id="25dad-123">Endpoints for authentication</span></span>

<span data-ttu-id="25dad-124">tooauthenticate Batch-toepassingen met Azure AD, moet u tooinclude sommige bekende eindpunten in uw code.</span><span class="sxs-lookup"><span data-stu-id="25dad-124">tooauthenticate Batch applications with Azure AD, you need tooinclude some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="25dad-125">Azure AD-eindpunt</span><span class="sxs-lookup"><span data-stu-id="25dad-125">Azure AD endpoint</span></span>

<span data-ttu-id="25dad-126">Hallo base Azure AD authority-eindpunt is:</span><span class="sxs-lookup"><span data-stu-id="25dad-126">hello base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="25dad-127">tooauthenticate met Azure AD, u dit eindpunt samen met de Hallo tenant-ID (directory-ID).</span><span class="sxs-lookup"><span data-stu-id="25dad-127">tooauthenticate with Azure AD, you use this endpoint together with hello tenant ID (directory ID).</span></span> <span data-ttu-id="25dad-128">Hallo tenant-ID identificeert hello Azure AD-tenant toouse voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="25dad-128">hello tenant ID identifies hello Azure AD tenant toouse for authentication.</span></span> <span data-ttu-id="25dad-129">tooretrieve Hallo tenant-ID, Hallo stappen die worden beschreven in [hello tenant-ID niet ophalen voor uw Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="25dad-129">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="25dad-130">Hallo tenantspecifieke eindpunt is vereist wanneer u verifiëren met behulp van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="25dad-130">hello tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="25dad-131">Hallo tenantspecifieke eindpunt is optioneel wanneer u verifiëren met behulp van geïntegreerde verificatie, maar aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="25dad-131">hello tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="25dad-132">U kunt echter ook algemene hello Azure AD-eindpunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25dad-132">However, you can also use hello Azure AD common endpoint.</span></span> <span data-ttu-id="25dad-133">Hallo gemeenschappelijk eindpunt biedt een algemene referentie interface verzamelen als een specifieke tenant is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="25dad-133">hello common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="25dad-134">algemene Hallo-eindpunt is `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="25dad-134">hello common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="25dad-135">Zie voor meer informatie over Azure AD-eindpunten [verificatie scenario's voor Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="25dad-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="25dad-136">Eindpunt voor batch-resource</span><span class="sxs-lookup"><span data-stu-id="25dad-136">Batch resource endpoint</span></span>

<span data-ttu-id="25dad-137">Gebruik Hallo **endpoint van Azure Batch-resource** tooacquire een token voor het verifiëren van aanvragen toohello Batch-service:</span><span class="sxs-lookup"><span data-stu-id="25dad-137">Use hello **Azure Batch resource endpoint** tooacquire a token for authenticating requests toohello Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="25dad-138">Uw toepassing registreren met een tenant</span><span class="sxs-lookup"><span data-stu-id="25dad-138">Register your application with a tenant</span></span>

<span data-ttu-id="25dad-139">eerste stap bij het gebruik van Azure AD tooauthenticate Hello wordt uw toepassing registreren in een Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="25dad-139">hello first step in using Azure AD tooauthenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="25dad-140">Registreren van uw toepassing kunt u toocall hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="25dad-140">Registering your application enables you toocall hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="25dad-141">Hallo ADAL biedt een API voor de verificatie met Azure AD van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="25dad-141">hello ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="25dad-142">Registreren van uw toepassing is vereist, of u van plan toouse geïntegreerde verificatie of een service-principal bent.</span><span class="sxs-lookup"><span data-stu-id="25dad-142">Registering your application is required whether you plan toouse integrated authentication or a service principal.</span></span>

<span data-ttu-id="25dad-143">Wanneer u uw toepassing registreert, kunt u informatie opgeven over uw toepassing tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="25dad-143">When you register your application, you supply information about your application tooAzure AD.</span></span> <span data-ttu-id="25dad-144">Vervolgens Azure AD levert een toepassings-ID dat u tooassociate uw toepassing met Azure AD tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="25dad-144">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="25dad-145">toolearn meer informatie over het Hallo-toepassings-ID, Zie [toepassing en service-principal objecten in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="25dad-145">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="25dad-146">tooregister uw Batch-toepassing hello Volg de stappen in Hallo [een toepassing toe te voegen](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) in sectie [toepassingen integreren met Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="25dad-146">tooregister your Batch application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="25dad-147">Als u uw toepassing als een systeemeigen toepassing registreren, kunt u een geldige URI voor Hallo **omleidings-URI**.</span><span class="sxs-lookup"><span data-stu-id="25dad-147">If you register your application as a Native Application, you can specify any valid URI for hello **Redirect URI**.</span></span> <span data-ttu-id="25dad-148">Hoeft niet toobe een echte-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="25dad-148">It does not need toobe a real endpoint.</span></span>

<span data-ttu-id="25dad-149">Nadat u uw toepassing hebt geregistreerd, ziet u Hallo toepassings-ID:</span><span class="sxs-lookup"><span data-stu-id="25dad-149">After you've registered your application, you'll see hello application ID:</span></span>

![De Batch-toepassing registreren met Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="25dad-151">Zie voor meer informatie over het registreren van een toepassing met Azure AD [verificatie scenario's voor Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="25dad-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-hello-tenant-id-for-your-active-directory"></a><span data-ttu-id="25dad-152">Hallo tenant-ID niet ophalen voor uw Active Directory</span><span class="sxs-lookup"><span data-stu-id="25dad-152">Get hello tenant ID for your Active Directory</span></span>

<span data-ttu-id="25dad-153">Hallo tenant-ID identificeert hello Azure AD-tenant waarmee verificatie services tooyour-toepassing.</span><span class="sxs-lookup"><span data-stu-id="25dad-153">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="25dad-154">tooget Hallo tenant-ID, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="25dad-154">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="25dad-155">Selecteer in hello Azure-portal, de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25dad-155">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="25dad-156">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="25dad-156">Click **Properties**.</span></span>
3. <span data-ttu-id="25dad-157">Kopieer Hallo GUID-waarde opgegeven voor Hallo directory-ID.</span><span class="sxs-lookup"><span data-stu-id="25dad-157">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="25dad-158">Deze waarde is een afkorting Hallo tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="25dad-158">This value is also called hello tenant ID.</span></span>

![Kopieer Hallo map-ID](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="25dad-160">Gebruik van geïntegreerde verificatie</span><span class="sxs-lookup"><span data-stu-id="25dad-160">Use integrated authentication</span></span>

<span data-ttu-id="25dad-161">tooauthenticate met geïntegreerde verificatie, moet u toogrant na uw toepassing machtigingen tooconnect toohello API van Batch-service.</span><span class="sxs-lookup"><span data-stu-id="25dad-161">tooauthenticate with integrated authentication, you need toogrant your application permissions tooconnect toohello Batch service API.</span></span> <span data-ttu-id="25dad-162">Deze stap kunt uw toepassing tooauthenticate aanroepen toohello Batch-service API met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25dad-162">This step enables your application tooauthenticate calls toohello Batch service API with Azure AD.</span></span>

<span data-ttu-id="25dad-163">Zodra u hebt [geregistreerd van uw toepassing](#register-your-application-with-an-azure-ad-tenant), als volgt te werk in hello Azure portal toogrant deze toegang hebben tot toohello Batch-service:</span><span class="sxs-lookup"><span data-stu-id="25dad-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in hello Azure portal toogrant it access toohello Batch service:</span></span>

1. <span data-ttu-id="25dad-164">Kies in Hallo links navigatievenster van hello Azure-portal, **meer Services**, klikt u op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="25dad-164">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="25dad-165">Hallo-naam van uw toepassing in de lijst Hallo van app-registraties zoeken:</span><span class="sxs-lookup"><span data-stu-id="25dad-165">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Zoeken naar de toepassingsnaam van uw](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="25dad-167">Open Hallo **instellingen** blade voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="25dad-167">Open hello **Settings** blade for your application.</span></span> <span data-ttu-id="25dad-168">In Hallo **API-toegang** sectie **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="25dad-168">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="25dad-169">In Hallo **vereist machtigingen** blade, klikt u op Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="25dad-169">In hello **Required permissions** blade, click hello **Add** button.</span></span>
5. <span data-ttu-id="25dad-170">In stap 1, zoekt u Hallo Batch-API.</span><span class="sxs-lookup"><span data-stu-id="25dad-170">In step 1, search for hello Batch API.</span></span> <span data-ttu-id="25dad-171">Zoeken naar elk van deze tekenreeksen totdat u Hallo-API:</span><span class="sxs-lookup"><span data-stu-id="25dad-171">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="25dad-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="25dad-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="25dad-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="25dad-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="25dad-174">Nieuwere Azure AD-tenants kunnen deze naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25dad-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="25dad-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** Hallo-id voor Hallo Batch-API.</span><span class="sxs-lookup"><span data-stu-id="25dad-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 
6. <span data-ttu-id="25dad-176">Als u Hallo Batch-API hebt gevonden, te selecteren en op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="25dad-176">Once you find hello Batch API, select it and click hello **Select** button.</span></span>
6. <span data-ttu-id="25dad-177">In stap 2, selecteer Hallo selectievakje in naast te**Access Azure Batch-Service** en klik op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="25dad-177">In step 2, select hello check box next too**Access Azure Batch Service** and click hello **Select** button.</span></span>
7. <span data-ttu-id="25dad-178">Klik op Hallo **gedaan** knop.</span><span class="sxs-lookup"><span data-stu-id="25dad-178">Click hello **Done** button.</span></span>

<span data-ttu-id="25dad-179">Hallo **Required Permissions** blade nu blijkt dat uw Azure AD-toepassing heeft toegang tooboth ADAL tot en Hallo API van Batch-service.</span><span class="sxs-lookup"><span data-stu-id="25dad-179">hello **Required Permissions** blade now shows that your Azure AD application has access tooboth ADAL and hello Batch service API.</span></span> <span data-ttu-id="25dad-180">Machtigingen worden verleend tooADAL automatisch wanneer u uw app eerst bij Azure AD registreren.</span><span class="sxs-lookup"><span data-stu-id="25dad-180">Permissions are granted tooADAL automatically when you first register your app with Azure AD.</span></span>

![Machtigingen verlenen API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="25dad-182">Gebruik van een service-principal</span><span class="sxs-lookup"><span data-stu-id="25dad-182">Use a service principal</span></span> 

<span data-ttu-id="25dad-183">een toepassing die wordt uitgevoerd zonder toezicht tooauthenticate, dat u een service-principal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25dad-183">tooauthenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="25dad-184">Nadat u uw toepassing hebt geregistreerd, als volgt in hello Azure portal tooconfigure een service-principal:</span><span class="sxs-lookup"><span data-stu-id="25dad-184">After you've registered your application, follow these steps in hello Azure portal tooconfigure a service principal:</span></span>

1. <span data-ttu-id="25dad-185">Vraagt u een geheime sleutel voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="25dad-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="25dad-186">Een toepassing RBAC-rol tooyour toewijzen.</span><span class="sxs-lookup"><span data-stu-id="25dad-186">Assign an RBAC role tooyour application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="25dad-187">Vraagt u een geheime sleutel voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="25dad-187">Request a secret key for your application</span></span>

<span data-ttu-id="25dad-188">Als uw toepassing wordt geverifieerd met een service-principal, verzendt de zowel Hallo toepassings-ID en een geheime sleutel tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="25dad-188">When your application authenticates with a service principal, it sends both hello application ID and a secret key tooAzure AD.</span></span> <span data-ttu-id="25dad-189">U moet toocreate en geheime sleutel toouse Hallo kopiëren vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="25dad-189">You'll need toocreate and copy hello secret key toouse from your code.</span></span>

<span data-ttu-id="25dad-190">Volg deze stappen in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="25dad-190">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="25dad-191">Kies in Hallo links navigatievenster van hello Azure-portal, **meer Services**, klikt u op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="25dad-191">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="25dad-192">Zoeken naar Hallo-naam van uw toepassing in de lijst Hallo van app-registraties.</span><span class="sxs-lookup"><span data-stu-id="25dad-192">Search for hello name of your application in hello list of app registrations.</span></span>
3. <span data-ttu-id="25dad-193">Weergave Hallo **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="25dad-193">Display hello **Settings** blade.</span></span> <span data-ttu-id="25dad-194">In Hallo **API-toegang** sectie **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="25dad-194">In hello **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="25dad-195">toocreate een sleutel is, voer een beschrijving voor Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="25dad-195">toocreate a key, enter a description for hello key.</span></span> <span data-ttu-id="25dad-196">Selecteer vervolgens een duur voor de sleutel Hallo van één of twee jaar.</span><span class="sxs-lookup"><span data-stu-id="25dad-196">Then select a duration for hello key of either one or two years.</span></span> 
5. <span data-ttu-id="25dad-197">Klik op Hallo **opslaan** knop toocreate en Hallo sleutel weer te geven.</span><span class="sxs-lookup"><span data-stu-id="25dad-197">Click hello **Save** button toocreate and display hello key.</span></span> <span data-ttu-id="25dad-198">Gekopieerd Hallo sleutelwaarde tooa veilige plaats, zoals tooaccess kunnen niet worden het opnieuw nadat u laat Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="25dad-198">Copy hello key value tooa safe place, as you won't be able tooaccess it again after you leave hello blade.</span></span> 

    ![Maken van een geheime sleutel](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a><span data-ttu-id="25dad-200">Een toepassing RBAC-rol tooyour toewijzen</span><span class="sxs-lookup"><span data-stu-id="25dad-200">Assign an RBAC role tooyour application</span></span>

<span data-ttu-id="25dad-201">tooauthenticate met een service-principal moet u een toepassing RBAC-rol tooyour tooassign.</span><span class="sxs-lookup"><span data-stu-id="25dad-201">tooauthenticate with a service principal, you need tooassign an RBAC role tooyour application.</span></span> <span data-ttu-id="25dad-202">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="25dad-202">Follow these steps:</span></span>

1. <span data-ttu-id="25dad-203">Navigeer in hello Azure-portal, toohello Batch-account wordt gebruikt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="25dad-203">In hello Azure portal, navigate toohello Batch account used by your application.</span></span>
2. <span data-ttu-id="25dad-204">In Hallo **instellingen** blade voor Hallo Batch-account, selecteer **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="25dad-204">In hello **Settings** blade for hello Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="25dad-205">Klik op Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="25dad-205">Click hello **Add** button.</span></span> 
4. <span data-ttu-id="25dad-206">Van Hallo **rol** vervolgkeuzelijst, kiest u beide Hallo _Inzender_ of _lezer_ rol voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="25dad-206">From hello **Role** drop-down, choose either hello _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="25dad-207">Zie voor meer informatie over deze rollen [aan de slag met toegangsbeheer op basis van rollen in Azure-portal Hallo](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="25dad-207">For more information on these roles, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="25dad-208">In Hallo **Selecteer** Hallo- naam van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="25dad-208">In hello **Select** field, enter hello name of your application.</span></span> <span data-ttu-id="25dad-209">Selecteer uw toepassing uit Hallo lijst en klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="25dad-209">Select your application from hello list, and click **Save**.</span></span>

<span data-ttu-id="25dad-210">Uw toepassing wordt nu weergegeven in de instellingen voor toegangsbeheer met een RBAC-rol die is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="25dad-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Een toepassing RBAC-rol tooyour toewijzen](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="25dad-212">Hallo tenant-ID niet ophalen voor uw Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25dad-212">Get hello tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="25dad-213">Hallo tenant-ID identificeert hello Azure AD-tenant waarmee verificatie services tooyour-toepassing.</span><span class="sxs-lookup"><span data-stu-id="25dad-213">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="25dad-214">tooget Hallo tenant-ID, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="25dad-214">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="25dad-215">Selecteer in hello Azure-portal, de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25dad-215">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="25dad-216">Klik op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="25dad-216">Click **Properties**.</span></span>
3. <span data-ttu-id="25dad-217">Kopieer Hallo GUID-waarde opgegeven voor Hallo directory-ID.</span><span class="sxs-lookup"><span data-stu-id="25dad-217">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="25dad-218">Deze waarde is een afkorting Hallo tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="25dad-218">This value is also called hello tenant ID.</span></span>

![Kopieer Hallo map-ID](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="25dad-220">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="25dad-220">Code examples</span></span>

<span data-ttu-id="25dad-221">Hallo-codevoorbeelden in deze sectie hoe tooauthenticate met Azure AD via verificatie geïntegreerde, en met een service-principal weergeven.</span><span class="sxs-lookup"><span data-stu-id="25dad-221">hello code examples in this section show how tooauthenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="25dad-222">Deze codevoorbeelden .NET gebruiken, maar Hallo concepten zijn vergelijkbaar voor andere talen.</span><span class="sxs-lookup"><span data-stu-id="25dad-222">These code examples use .NET, but hello concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="25dad-223">Een Azure AD authentication-token verloopt na één uur.</span><span class="sxs-lookup"><span data-stu-id="25dad-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="25dad-224">Wanneer u een lange levensduur **BatchClient** object, het is raadzaam dat u een token ophalen van ADAL op elke aanvraag tooensure hebt u altijd een geldig token.</span><span class="sxs-lookup"><span data-stu-id="25dad-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request tooensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="25dad-225">tooachieve dit in .NET schrijven van een methode dat haalt Hallo-token van Azure AD en doorgeven die methode tooa **BatchTokenCredentials** object als een gemachtigde.</span><span class="sxs-lookup"><span data-stu-id="25dad-225">tooachieve this in .NET, write a method that retrieves hello token from Azure AD and pass that method tooa **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="25dad-226">Hallo gemachtigdenmethode is aangeroepen voor elke aanvraag toohello Batch-service tooensure die wordt geleverd met een geldig token.</span><span class="sxs-lookup"><span data-stu-id="25dad-226">hello delegate method is called on every request toohello Batch service tooensure that a valid token is provided.</span></span> <span data-ttu-id="25dad-227">Standaard ADAL in de cache opgeslagen tokens, zodat een nieuw token is opgehaald uit Azure AD alleen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="25dad-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="25dad-228">Zie voor meer informatie over tokens in Azure AD [verificatie scenario's voor Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="25dad-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="25dad-229">Voorbeeld: met behulp van Azure AD geïntegreerde verificatie met Batch .NET</span><span class="sxs-lookup"><span data-stu-id="25dad-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="25dad-230">tooauthenticate met geïntegreerde verificatie in Batch .NET verwijzing Hallo [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) pakket en Hallo [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pakket.</span><span class="sxs-lookup"><span data-stu-id="25dad-230">tooauthenticate with integrated authentication from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="25dad-231">Neem de volgende Hallo `using` instructies in uw code:</span><span class="sxs-lookup"><span data-stu-id="25dad-231">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="25dad-232">Verwijzing hello Azure AD-eindpunt in uw code, met inbegrip van Hallo tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="25dad-232">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="25dad-233">tooretrieve Hallo tenant-ID, Hallo stappen die worden beschreven in [hello tenant-ID niet ophalen voor uw Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="25dad-233">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="25dad-234">Verwijzen naar Hallo Batch service-eindpunt voor resource:</span><span class="sxs-lookup"><span data-stu-id="25dad-234">Reference hello Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="25dad-235">Verwijzen naar uw Batch-account:</span><span class="sxs-lookup"><span data-stu-id="25dad-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="25dad-236">Hallo toepassings-ID (client-ID) voor uw toepassing opgeven.</span><span class="sxs-lookup"><span data-stu-id="25dad-236">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="25dad-237">Hallo toepassings-ID is beschikbaar via de registratie van uw app in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="25dad-237">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="25dad-238">Hallo omleidings-URI die u hebt opgegeven tijdens het registratieproces Hallo ook kopiëren.</span><span class="sxs-lookup"><span data-stu-id="25dad-238">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="25dad-239">Hallo redirect die URI in uw code opgegeven moet overeenkomen met de Hallo omleidings-URI die u hebt opgegeven bij de registratie van de toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="25dad-239">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="25dad-240">Verificatietoken voor een retouraanroep methode tooacquire Hallo schrijven van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25dad-240">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="25dad-241">Hallo **GetAuthenticationTokenAsync** een gebruiker die de interactie met de toepassing hello-aanroepen ADAL tooauthenticate retouraanroepmethode hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="25dad-241">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL tooauthenticate a user who is interacting with hello application.</span></span> <span data-ttu-id="25dad-242">Hallo **AcquireTokenAsync** methode opgegeven door ADAL Hallo wordt u gevraagd de gebruiker om hun referenties en het Hallo-toepassing wordt voortgezet eenmaal Hallo gebruiker biedt deze (tenzij deze al in de cache referenties opgeslagen is):</span><span class="sxs-lookup"><span data-stu-id="25dad-242">hello **AcquireTokenAsync** method provided by ADAL prompts hello user for their credentials, and hello application proceeds once hello user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="25dad-243">Samen een **BatchTokenCredentials** object waarvoor Hallo gemachtigde als parameter.</span><span class="sxs-lookup"><span data-stu-id="25dad-243">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="25dad-244">Gebruik deze referenties tooopen een **BatchClient** object.</span><span class="sxs-lookup"><span data-stu-id="25dad-244">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="25dad-245">U kunt die **BatchClient** object voor verdere bewerkingen tegen Hallo Batch-service:</span><span class="sxs-lookup"><span data-stu-id="25dad-245">You can use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

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

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="25dad-246">Voorbeeld: met behulp van een Azure AD-service-principal met Batch .NET</span><span class="sxs-lookup"><span data-stu-id="25dad-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="25dad-247">tooauthenticate met een service-principal in Batch .NET verwijzing Hallo [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) pakket en Hallo [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pakket.</span><span class="sxs-lookup"><span data-stu-id="25dad-247">tooauthenticate with a service principal from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="25dad-248">Neem de volgende Hallo `using` instructies in uw code:</span><span class="sxs-lookup"><span data-stu-id="25dad-248">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="25dad-249">Verwijzing hello Azure AD-eindpunt in uw code, met inbegrip van Hallo tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="25dad-249">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="25dad-250">Wanneer u een service-principal gebruikt, moet u een eindpunt tenantspecifieke opgeven.</span><span class="sxs-lookup"><span data-stu-id="25dad-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="25dad-251">tooretrieve Hallo tenant-ID, Hallo stappen die worden beschreven in [hello tenant-ID niet ophalen voor uw Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="25dad-251">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="25dad-252">Verwijzen naar Hallo Batch service-eindpunt voor resource:</span><span class="sxs-lookup"><span data-stu-id="25dad-252">Reference hello Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="25dad-253">Verwijzen naar uw Batch-account:</span><span class="sxs-lookup"><span data-stu-id="25dad-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="25dad-254">Hallo toepassings-ID (client-ID) voor uw toepassing opgeven.</span><span class="sxs-lookup"><span data-stu-id="25dad-254">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="25dad-255">Hallo toepassings-ID is beschikbaar via de registratie van uw app in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="25dad-255">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="25dad-256">Geef Hallo geheime sleutel die u hebt gekopieerd uit hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="25dad-256">Specify hello secret key that you copied from hello Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="25dad-257">Verificatietoken voor een retouraanroep methode tooacquire Hallo schrijven van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25dad-257">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="25dad-258">Hallo **GetAuthenticationTokenAsync** retouraanroepmethode aanroepen ADAL voor verificatie zonder toezicht hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="25dad-258">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="25dad-259">Samen een **BatchTokenCredentials** object waarvoor Hallo gemachtigde als parameter.</span><span class="sxs-lookup"><span data-stu-id="25dad-259">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="25dad-260">Gebruik deze referenties tooopen een **BatchClient** object.</span><span class="sxs-lookup"><span data-stu-id="25dad-260">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="25dad-261">Vervolgens kunt u die **BatchClient** object voor verdere bewerkingen tegen Hallo Batch-service:</span><span class="sxs-lookup"><span data-stu-id="25dad-261">You can then use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="25dad-262">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25dad-262">Next steps</span></span>

<span data-ttu-id="25dad-263">toolearn meer informatie over Azure AD, Zie Hallo [Azure Active Directory-documentatie](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="25dad-263">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="25dad-264">Gedetailleerde voorbeelden ziet u hoe toouse ADAL zijn beschikbaar in Hallo [Azure codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=active-directory) bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="25dad-264">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="25dad-265">Zie toolearn meer informatie over service-principals [toepassing en service-principal objecten in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="25dad-265">toolearn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="25dad-266">een service principal met toocreate hello Azure portal, Zie [portal toocreate Active Directory-toepassing en service-principal die toegang bronnen tot gebruiken](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25dad-266">toocreate a service principal using hello Azure portal, see [Use portal toocreate Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="25dad-267">U kunt ook een service-principal maken met PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="25dad-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="25dad-268">Zie tooauthenticate Batch Management toepassingen die gebruikmaken van Azure AD [oplossingen voor het beheer van Batch verifiëren met Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="25dad-268">tooauthenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

[aad_about]: ../active-directory/active-directory-whatis.md "Wat is Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Verificatie-scenario's voor Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Toepassingen integreren met Azure Active Directory"
[azure_portal]: http://portal.azure.com
