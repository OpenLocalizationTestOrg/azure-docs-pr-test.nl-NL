---
title: een Batch-account in Azure-portal Hallo aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Azure Batch-account in Azure portal toorun Hallo grootschalige parallelle workloads in Hallo cloud
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="0a49d-103">Een Batch-account maken met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0a49d-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a49d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0a49d-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="0a49d-105">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="0a49d-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="0a49d-106">Meer informatie over hoe toocreate een Azure Batch-account in Hallo [Azure-portal][azure_portal], en kies Hallo accounteigenschappen die aansluiten bij uw rekenscenario.</span><span class="sxs-lookup"><span data-stu-id="0a49d-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="0a49d-107">Meer informatie over waar de belangrijke accounteigenschappen toofind zoals toegangstoetsen en account-URL's.</span><span class="sxs-lookup"><span data-stu-id="0a49d-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="0a49d-108">Zie voor achtergrondinformatie over Batch-accounts en scenario's, Hallo [functie overzicht](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="0a49d-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="0a49d-109">Batch-account maken</span><span class="sxs-lookup"><span data-stu-id="0a49d-109">Create a Batch account</span></span>

<span data-ttu-id="0a49d-110">Hallo portal toocreate een Batch-account gebruiken in een van twee Hallo *groep toewijzing modi*: **Batch-service** modus of nieuwere Hallo **gebruikerabonnement** modus, die meer vereist de configuratie.</span><span class="sxs-lookup"><span data-stu-id="0a49d-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="0a49d-111">Zie voor informatie over deze twee modi Hallo [functie overzicht](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="0a49d-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="0a49d-112">Voor de onderdelen van de gebruikersmodus abonnement hello, Zie ook Hallo [blogbericht](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="0a49d-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="0a49d-113">Modus Batch-service</span><span class="sxs-lookup"><span data-stu-id="0a49d-113">Batch service mode</span></span>



1. <span data-ttu-id="0a49d-114">Meld u aan toohello [Azure-portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="0a49d-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="0a49d-115">Klik op **Nieuw** > **Berekenen** > **Batch-service**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Batch in Hallo Marketplace][marketplace_portal]
3. <span data-ttu-id="0a49d-117">Hallo **nieuw Batch-Account** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0a49d-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="0a49d-118">Zie de beschrijvingen Hallo hieronder van elk blade-element.</span><span class="sxs-lookup"><span data-stu-id="0a49d-118">See hello descriptions below of each blade element.</span></span>

    ![Batch-account maken][account_portal]

    <span data-ttu-id="0a49d-120">a.</span><span class="sxs-lookup"><span data-stu-id="0a49d-120">a.</span></span> <span data-ttu-id="0a49d-121">**Accountnaam**: Batch-accountnaam Hallo u kiest moet uniek zijn binnen hello Azure-regio waar Hallo-account wordt gemaakt (Zie **locatie** hieronder).</span><span class="sxs-lookup"><span data-stu-id="0a49d-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="0a49d-122">Hallo-accountnaam mag alleen kleine letters of cijfers bevatten en moet 3 tot 24 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="0a49d-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="0a49d-123">b.</span><span class="sxs-lookup"><span data-stu-id="0a49d-123">b.</span></span> <span data-ttu-id="0a49d-124">**Abonnement**: Hallo-abonnement in welke toocreate Hallo Batch-account.</span><span class="sxs-lookup"><span data-stu-id="0a49d-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="0a49d-125">Als u slechts één abonnement hebt, is het standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0a49d-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="0a49d-126">c.</span><span class="sxs-lookup"><span data-stu-id="0a49d-126">c.</span></span> <span data-ttu-id="0a49d-127">**Groepstoewijzingsmodus**: selecteer **Batch-service**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="0a49d-128">c.</span><span class="sxs-lookup"><span data-stu-id="0a49d-128">c.</span></span> <span data-ttu-id="0a49d-129">**Resourcegroep**: Selecteer een bestaande resourcegroep voor het nieuwe Batch-account. U kunt er ook voor kiezen om een nieuwe resourcegroep te maken.</span><span class="sxs-lookup"><span data-stu-id="0a49d-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="0a49d-130">d.</span><span class="sxs-lookup"><span data-stu-id="0a49d-130">d.</span></span> <span data-ttu-id="0a49d-131">**Locatie**: hello Azure-regio in welke toocreate Hallo Batch-account.</span><span class="sxs-lookup"><span data-stu-id="0a49d-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="0a49d-132">Alleen Hallo-regio's wordt ondersteund door uw abonnement en resourcegroep worden als opties weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0a49d-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="0a49d-133">e.</span><span class="sxs-lookup"><span data-stu-id="0a49d-133">e.</span></span> <span data-ttu-id="0a49d-134">**Opslagaccount** (optioneel): een Azure Storage-account voor algemeen gebruik dat u koppelt aan het Batch-account.</span><span class="sxs-lookup"><span data-stu-id="0a49d-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="0a49d-135">Dit wordt aanbevolen voor de meeste Batch-accounts.</span><span class="sxs-lookup"><span data-stu-id="0a49d-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="0a49d-136">Zie [Gekoppeld Azure Storage-account](#linked-azure-storage-account) verderop in dit artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0a49d-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="0a49d-137">Klik op **maken** toocreate Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="0a49d-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="0a49d-138">Hallo portal geeft de implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0a49d-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="0a49d-139">Na voltooiing wordt de melding **Implementaties geslaagd** weergegeven in **Meldingen**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="0a49d-140">Modus Gebruikersabonnement</span><span class="sxs-lookup"><span data-stu-id="0a49d-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="0a49d-141">Azure Batch tooaccess Hallo-abonnement (eenmalige bewerking) toestaan</span><span class="sxs-lookup"><span data-stu-id="0a49d-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="0a49d-142">Bij het maken van uw eerste Batch-account in de gebruikersmodus abonnement, uw abonnement met Batch uitvoeren Hallo tooregister stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="0a49d-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="0a49d-143">(Als u eerder dit hebt gedaan, toohello volgende sectie overslaan.)</span><span class="sxs-lookup"><span data-stu-id="0a49d-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="0a49d-144">Meld u aan toohello [Azure-portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="0a49d-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="0a49d-145">Klik op **meer Services** > **abonnementen**, en klikt u op Hallo abonnement toouse voor gewenste Hallo Batch-account.</span><span class="sxs-lookup"><span data-stu-id="0a49d-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="0a49d-146">In Hallo **abonnement** blade, klikt u op **toegangsbeheer (IAM)** > **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Toegangsbeheer voor abonnement][subscription_access]

4. <span data-ttu-id="0a49d-148">Op Hallo **machtigingen toevoegen** blade, selecteer Hallo **Inzender** rol, zoekt u Hallo Batch-API.</span><span class="sxs-lookup"><span data-stu-id="0a49d-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="0a49d-149">Zoeken naar elk van deze tekenreeksen totdat u Hallo-API:</span><span class="sxs-lookup"><span data-stu-id="0a49d-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="0a49d-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="0a49d-151">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="0a49d-152">Nieuwere Azure AD-tenants kunnen deze naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0a49d-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="0a49d-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** Hallo-id voor Hallo Batch-API.</span><span class="sxs-lookup"><span data-stu-id="0a49d-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="0a49d-154">Als u Hallo Batch-API hebt gevonden, te selecteren en op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![Batch-machtigingen toevoegen][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="0a49d-156">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="0a49d-156">Create a key vault</span></span>
<span data-ttu-id="0a49d-157">In de gebruikersmodus-abonnement, een Azure sleutelkluis is vereist dat toothe hoort dezelfde resourcegroep als Hallo Batch-account toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0a49d-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="0a49d-158">Zorg ervoor dat Hallo resourcegroep bevindt zich in een regio waar de Batch is [beschikbaar](https://azure.microsoft.com/regions/services/) en die ondersteuning biedt voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="0a49d-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="0a49d-159">In Hallo [Azure-portal][azure_portal], klikt u op **nieuw** > **beveiliging en identiteit** > **Sleutelkluis** .</span><span class="sxs-lookup"><span data-stu-id="0a49d-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="0a49d-160">In Hallo **Sleutelkluis maken** blade een naam voor de sleutelkluis hello en een resourcegroep in Hallo regio die u voor uw Batch-account wilt maken.</span><span class="sxs-lookup"><span data-stu-id="0a49d-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="0a49d-161">Laat Hallo resterende instellingen op de standaardwaarden en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="0a49d-162">Batch-account maken</span><span class="sxs-lookup"><span data-stu-id="0a49d-162">Create a Batch account</span></span>

1. <span data-ttu-id="0a49d-163">In Hallo [Azure-portal][azure_portal], klikt u op **nieuw** > **Compute** > **voorBatch-Service**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Batch in Hallo Marketplace][marketplace_portal]
3. <span data-ttu-id="0a49d-165">Hallo **nieuw Batch-Account** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0a49d-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="0a49d-166">Zie de beschrijvingen Hallo hieronder van elk blade-element.</span><span class="sxs-lookup"><span data-stu-id="0a49d-166">See hello descriptions below of each blade element.</span></span>

    ![Batch-account maken][account_portal_byos]

    <span data-ttu-id="0a49d-168">a.</span><span class="sxs-lookup"><span data-stu-id="0a49d-168">a.</span></span> <span data-ttu-id="0a49d-169">**Accountnaam**: Batch-accountnaam Hallo u kiest moet uniek zijn binnen hello Azure-regio waar Hallo-account wordt gemaakt (Zie **locatie** hieronder).</span><span class="sxs-lookup"><span data-stu-id="0a49d-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="0a49d-170">Hallo-accountnaam mag alleen kleine letters of cijfers bevatten en moet 3 tot 24 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="0a49d-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="0a49d-171">b.</span><span class="sxs-lookup"><span data-stu-id="0a49d-171">b.</span></span> <span data-ttu-id="0a49d-172">**Abonnement**: als u meer dan één abonnement hebt, selecteert u Hallo-abonnement dat u bij Hallo Batch-service geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="0a49d-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="0a49d-173">c.</span><span class="sxs-lookup"><span data-stu-id="0a49d-173">c.</span></span> <span data-ttu-id="0a49d-174">**Groepstoewijzingsmodus**: selecteer **Gebruikersabonnement**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="0a49d-175">d.</span><span class="sxs-lookup"><span data-stu-id="0a49d-175">d.</span></span> <span data-ttu-id="0a49d-176">**Sleutelkluis**: Selecteer Hallo sleutelkluis u hebt gemaakt voor uw Batch-account in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="0a49d-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="0a49d-177">Maak desgewenst een nieuwe sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="0a49d-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="0a49d-178">Selecteer na het selecteren van de kluis Hallo Hallo selectievakje toogrant Azure Batch toegang toohello sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="0a49d-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="0a49d-179">c.</span><span class="sxs-lookup"><span data-stu-id="0a49d-179">c.</span></span> <span data-ttu-id="0a49d-180">**Resourcegroep**: Selecteer Hallo resourcegroep waarin u Hallo sleutelkluis hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0a49d-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="0a49d-181">d.</span><span class="sxs-lookup"><span data-stu-id="0a49d-181">d.</span></span> <span data-ttu-id="0a49d-182">**Locatie**: hello Azure-regio waarin u de sleutelkluis Hallo voor Hallo Batch-account hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0a49d-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="0a49d-183">e.</span><span class="sxs-lookup"><span data-stu-id="0a49d-183">e.</span></span> <span data-ttu-id="0a49d-184">**Opslagaccount** (optioneel): een Azure Storage-account voor algemeen gebruik dat u koppelt aan het Batch-account.</span><span class="sxs-lookup"><span data-stu-id="0a49d-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="0a49d-185">Dit wordt aanbevolen voor de meeste Batch-accounts.</span><span class="sxs-lookup"><span data-stu-id="0a49d-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="0a49d-186">Zie [Gekoppeld Azure Storage-account](#linked-azure-storage-account) hieronder voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0a49d-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="0a49d-187">Klik op **maken** toocreate Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="0a49d-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="0a49d-188">Hallo portal geeft de implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0a49d-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="0a49d-189">Na voltooiing wordt de melding **Implementaties geslaagd** weergegeven in **Meldingen**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="0a49d-190">Eigenschappen van Batch-account weergeven</span><span class="sxs-lookup"><span data-stu-id="0a49d-190">View Batch account properties</span></span>
<span data-ttu-id="0a49d-191">Wanneer het Hallo-account is gemaakt, kunt u Hallo openen **blade van de Batch-account** tooaccess de instellingen en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0a49d-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="0a49d-192">U kunt toegang tot alle instellingen en eigenschappen via Hallo linkermenu van blade Hallo Batch-account.</span><span class="sxs-lookup"><span data-stu-id="0a49d-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Blade Batch-account in Azure Portal][account_blade]

* <span data-ttu-id="0a49d-194">**Batch-account-URL**: wanneer u een toepassing Hello ontwikkelt [Batch-API's](batch-apis-tools.md#azure-accounts-for-batch-development), moet u een account URL tooaccess uw Batch-resources.</span><span class="sxs-lookup"><span data-stu-id="0a49d-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="0a49d-195">De URL van een Batch-account heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="0a49d-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![Batch-account-URL in de portal][account_url]

* <span data-ttu-id="0a49d-197">**Toegangssleutels** (modus voor Batch-service): tooauthenticate toegang tooyour Batch-account van uw toepassing, moet u een toegangssleutel voor het account.</span><span class="sxs-lookup"><span data-stu-id="0a49d-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="0a49d-198">(Deze instelling is niet beschikbaar in de modus Gebruikersabonnement, waarin u Azure Active Directory-verificatie gebruikt.)</span><span class="sxs-lookup"><span data-stu-id="0a49d-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="0a49d-199">tooview of opnieuw genereren toegangssleutels van uw Batch-account, voer `keys` in het linkermenu Hallo **Search** vak op de blade Hallo Batch-account en selecteer vervolgens **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Batch-accountsleutels in Azure Portal][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="0a49d-201">Gekoppeld Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="0a49d-201">Linked Azure Storage account</span></span>

<span data-ttu-id="0a49d-202">U kunt desgewenst een algemeen Azure Storage-account tooyour Batch-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="0a49d-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="0a49d-203">Hallo [toepassingspakketten](batch-application-packages.md) functie van Batch gebruikt Azure Blob storage, doet Hallo [Batch bestand conventies .NET](batch-task-output.md) bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="0a49d-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="0a49d-204">Deze optionele functies helpt u bij de implementatie Hallo-toepassingen die uw Batch-taken worden uitgevoerd en persistent maken Hallo-gegevens die ze produceren.</span><span class="sxs-lookup"><span data-stu-id="0a49d-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="0a49d-205">U wordt aangeraden een nieuw opslagaccount te maken dat alleen wordt gebruikt voor het Batch-account.</span><span class="sxs-lookup"><span data-stu-id="0a49d-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Een opslagaccount voor algemeen gebruik maken][storage_account]

> [!NOTE]
> <span data-ttu-id="0a49d-207">Azure Batch ondersteunt momenteel alleen Hallo algemeen type Opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0a49d-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="0a49d-208">Dit accounttype wordt beschreven in stap 5 [Een opslagaccount maken] (../ storage/common/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0a49d-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="0a49d-209">Wees voorzichtig met het Hallo toegangssleutels van een gekoppelde opslagaccount opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="0a49d-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="0a49d-210">Slechts één opslagaccountsleutel opnieuw genereren en klik op **sleutels synchroniseren** op Hallo gekoppeld blade Opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0a49d-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="0a49d-211">Wacht vijf minuten tooallow Hallo sleutels toopropagate toohello rekenknooppunten in uw pools en vervolgens opnieuw genereren en synchroniseren Hallo andere sleutel indien nodig.</span><span class="sxs-lookup"><span data-stu-id="0a49d-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="0a49d-212">Als u opnieuw beide genereert sleutels op Hallo dezelfde tijd, uw rekenknooppunten kunnen toosynchronize van sleutel, en worden ze toegang toohello Storage-account verliest.</span><span class="sxs-lookup"><span data-stu-id="0a49d-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="0a49d-213">![Sleutels van opslagaccounts opnieuw genereren][4]</span><span class="sxs-lookup"><span data-stu-id="0a49d-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="0a49d-214">Quota en limieten voor Batch-service</span><span class="sxs-lookup"><span data-stu-id="0a49d-214">Batch service quotas and limits</span></span>
<span data-ttu-id="0a49d-215">Houd er rekening mee dat als met uw Azure-abonnement en andere Azure-services, bepaalde u zich [quota en limieten](batch-quota-limit.md) tooBatch accounts van toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a49d-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="0a49d-216">De huidige quota voor een Batch-account worden weergegeven in Hallo account Hallo Portal **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="0a49d-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Batch-accountquota in Azure Portal][quotas]



<span data-ttu-id="0a49d-218">Veel van deze quota kunnen bovendien worden verhoogd met een gratis product ondersteuningsaanvraag verzonden in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0a49d-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="0a49d-219">Zie [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md) voor meer informatie over het aanvragen van quota toeneemt.</span><span class="sxs-lookup"><span data-stu-id="0a49d-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="0a49d-220">Andere beheeropties voor uw Batch-account</span><span class="sxs-lookup"><span data-stu-id="0a49d-220">Other Batch account management options</span></span>
<span data-ttu-id="0a49d-221">Bovendien toousing hello Azure-portal, kunt u ook maken en beheren van Batch-accounts met Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="0a49d-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="0a49d-222">Batch-PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="0a49d-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="0a49d-223">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0a49d-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="0a49d-224">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="0a49d-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="0a49d-225">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0a49d-225">Next steps</span></span>
* <span data-ttu-id="0a49d-226">Zie Hallo [overzicht Batch-functies](batch-api-basics.md) toolearn meer over de concepten van de Batch-service en -functies.</span><span class="sxs-lookup"><span data-stu-id="0a49d-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="0a49d-227">Hallo artikel Hallo primaire Batch-resources zoals pools, rekenknooppunten, jobs en taken besproken en u vindt een overzicht van Hallo servicefuncties waarmee grootschalige rekenworkloads kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0a49d-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="0a49d-228">Leer de basisbeginselen Hallo van het ontwikkelen van een Batch-toepassing hello met [clientbibliotheek Batch .NET](batch-dotnet-get-started.md) of [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0a49d-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="0a49d-229">Deze inleidende artikelen helpen u bij een werkende toepassing die gebruikmaakt van Hallo Batch-service tooexecute een workload op meerdere rekenknooppunten en omvat het gebruik van Azure Storage voor het Faseren en ophalen.</span><span class="sxs-lookup"><span data-stu-id="0a49d-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Sleutels van opslagaccounts opnieuw genereren"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
