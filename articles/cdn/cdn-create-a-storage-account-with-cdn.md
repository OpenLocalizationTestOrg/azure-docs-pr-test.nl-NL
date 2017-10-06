---
title: een Azure storage-account met Azure CDN aaaIntegrate | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure inhoud Delivery Network (CDN) toodeliver hoge bandbreedte inhoud door het in cache plaatsen van Azure Storage-blobs.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="7803c-103">Een Azure storage-account integreren met Azure CDN</span><span class="sxs-lookup"><span data-stu-id="7803c-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="7803c-104">CDN kan worden ingeschakeld toocache inhoud in uw Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="7803c-104">CDN can be enabled toocache content from your Azure storage.</span></span> <span data-ttu-id="7803c-105">Het biedt ontwikkelaars een globale oplossing voor hoge bandbreedte inhoud leveren door blobs en statische inhoud van de compute-exemplaren op fysieke knooppunten op Hallo Verenigde Staten, Europa, Azië, Australië en Zuid-Amerika cache te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="7803c-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in hello United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="7803c-106">Stap 1: Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="7803c-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="7803c-107">Hallo te volgen procedure toocreate een nieuw opslagaccount voor een Azure-abonnement gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7803c-107">Use hello following procedure toocreate a new storage account for a Azure subscription.</span></span> <span data-ttu-id="7803c-108">Een opslagaccount biedt toegang tot Azure storage-services.</span><span class="sxs-lookup"><span data-stu-id="7803c-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="7803c-109">Hallo storage-account vertegenwoordigt Hallo hoogste niveau van Hallo naamruimte voor het openen van elk van de onderdelen van een hello Azure storage-service: Blob-services, wachtrijservices en services van de tabel.</span><span class="sxs-lookup"><span data-stu-id="7803c-109">hello storage account represents hello highest level of hello namespace for accessing each of hello Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="7803c-110">Raadpleeg voor meer informatie, toohello [tooMicrosoft inleiding Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7803c-110">For more information, refer toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="7803c-111">toocreate een opslagaccount, moet u Hallo servicebeheerder of medebeheerder voor Hallo gekoppeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="7803c-111">toocreate a storage account, you must be either hello service administrator or a co-administrator for hello associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="7803c-112">Er zijn verschillende methoden kunt u toocreate storage-account, inclusief hello Azure-Portal en Powershell.</span><span class="sxs-lookup"><span data-stu-id="7803c-112">There are several methods you can use toocreate a storage account, including hello Azure Portal and Powershell.</span></span>  <span data-ttu-id="7803c-113">Voor deze zelfstudie worden gebruikt hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="7803c-113">For this tutorial, we'll be using hello Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="7803c-114">**toocreate een opslagaccount voor een Azure-abonnement**</span><span class="sxs-lookup"><span data-stu-id="7803c-114">**toocreate a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="7803c-115">Meld u aan toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7803c-115">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7803c-116">Selecteer in de linkerbovenhoek Hallo **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="7803c-116">In hello upper left corner, select **New**.</span></span> <span data-ttu-id="7803c-117">In Hallo **nieuw** dialoogvenster **gegevens en opslag**, klikt u vervolgens op **opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="7803c-117">In hello **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="7803c-118">Hallo **storage-account maken** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7803c-118">hello **Create storage account** blade appears.</span></span>   

    ![Storage-Account maken][create-new-storage-account]  

3. <span data-ttu-id="7803c-120">In Hallo **naam** veld, typt u de subdomeinnaam.</span><span class="sxs-lookup"><span data-stu-id="7803c-120">In hello **Name** field, type a subdomain name.</span></span> <span data-ttu-id="7803c-121">Deze vermelding kan 3 tot 24 kleine letters en cijfers bevatten.</span><span class="sxs-lookup"><span data-stu-id="7803c-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="7803c-122">Deze waarde wordt Hallo hostnaam binnen Hallo URI die wordt gebruikt om Blob, wachtrij of tabel resources voor Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7803c-122">This value becomes hello host name within hello URI that is used to address Blob, Queue, or Table resources for hello subscription.</span></span> <span data-ttu-id="7803c-123">Om een containerresource in Hallo Blob-service op te lossen, gebruikt u een URI in Hallo-indeling te volgen waarbij  *&lt;StorageAccountLabel&gt;*  toohello-waarde die u hebt getypt in verwijst **Voer een URL**:</span><span class="sxs-lookup"><span data-stu-id="7803c-123">To address a container resource in hello Blob service, you would use a URI in hello following format, where *&lt;StorageAccountLabel&gt;* refers toohello value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="7803c-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="7803c-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="7803c-125">**Belangrijk:** Hallo URL label formulieren Hallo subdomein van het opslagaccount Hallo URI en moet uniek zijn alle gehoste services in Azure.</span><span class="sxs-lookup"><span data-stu-id="7803c-125">**Important:** hello URL label forms hello subdomain of hello storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="7803c-126">Deze waarde wordt ook gebruikt als Hallo-naam van dit opslagaccount in de portal Hallo of bij het openen van dit account via een programma.</span><span class="sxs-lookup"><span data-stu-id="7803c-126">This value is also used as hello name of this storage account in hello portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="7803c-127">Laat de standaardwaarden voor Hallo **implementatiemodel**, **Account kind**, **prestaties**, en **replicatie**.</span><span class="sxs-lookup"><span data-stu-id="7803c-127">Leave hello defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="7803c-128">Selecteer Hallo **abonnement** Hallo storage-account wordt gebruikt met.</span><span class="sxs-lookup"><span data-stu-id="7803c-128">Select hello **Subscription** that hello storage account will be used with.</span></span>
6. <span data-ttu-id="7803c-129">Selecteer of maak een **resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="7803c-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="7803c-130">Zie [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="7803c-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="7803c-131">Selecteer een locatie voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7803c-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="7803c-132">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7803c-132">Click **Create**.</span></span> <span data-ttu-id="7803c-133">Hallo-proces voor het maken van Hallo storage-account kan toocomplete van enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="7803c-133">hello process of creating hello storage account might take several minutes toocomplete.</span></span>

## <a name="step-2-enable-cdn-for-hello-storage-account"></a><span data-ttu-id="7803c-134">Stap 2: CDN inschakelen voor Hallo storage-account</span><span class="sxs-lookup"><span data-stu-id="7803c-134">Step 2: Enable CDN for hello storage account</span></span>

<span data-ttu-id="7803c-135">Met de nieuwste integratie hello, kunt u nu CDN inschakelen voor uw opslagaccount zonder de uitbreiding van uw storage-portal.</span><span class="sxs-lookup"><span data-stu-id="7803c-135">With hello newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="7803c-136">Selecteer Hallo opslagaccount, 'CDN' of blader naar beneden zoeken in Hallo linkernavigatievenster menu aan en klik vervolgens op 'Azure CDN'.</span><span class="sxs-lookup"><span data-stu-id="7803c-136">Select hello storage account, search "CDN" or scroll down from hello left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="7803c-137">Hallo **Azure CDN** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7803c-137">hello **Azure CDN** blade appears.</span></span>

    ![CDN inschakelen navigatie][cdn-enable-navigation]
    
2. <span data-ttu-id="7803c-139">Maak een nieuwe eindpunt Hallo vereist gegevens invoeren</span><span class="sxs-lookup"><span data-stu-id="7803c-139">Create a new endpoint by entering hello required information</span></span>
    - <span data-ttu-id="7803c-140">**CDN-profiel**: U kunt een nieuwe maken of een bestaand profiel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7803c-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="7803c-141">**Prijscategorie**: U hoeft alleen tooselect een prijscategorie als u een nieuw CDN-profiel maakt.</span><span class="sxs-lookup"><span data-stu-id="7803c-141">**Pricing tier**: You only need tooselect a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="7803c-142">**De naam van de CDN-eindpunt**: Voer de naam van een eindpunt per uw keuze.</span><span class="sxs-lookup"><span data-stu-id="7803c-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="7803c-143">CDN-eindpunt gemaakt Hallo standaard Hallo hostnaam van uw storage-account als oorsprong.</span><span class="sxs-lookup"><span data-stu-id="7803c-143">hello created CDN endpoint uses hello hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="7803c-144">! [cdn-eindpunt maken van nieuwe] [cdn--eindpunt-maken van nieuwe]</span><span class="sxs-lookup"><span data-stu-id="7803c-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="7803c-145">Na het maken, wordt nieuw Hallo-eindpunt weergegeven in bovenstaande Hallo endpoint-lijst.</span><span class="sxs-lookup"><span data-stu-id="7803c-145">After creation, hello new endpoint will show up in hello endpoint list above.</span></span>

    ![storage-nieuwe CDN-eindpunt][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="7803c-147">U kunt ook tooAzure CDN extensie tooenable CDN gaan. [Zelfstudie](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="7803c-147">You can also go tooAzure CDN extension tooenable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="7803c-148">Stap 3: Extra CDN-functies inschakelen</span><span class="sxs-lookup"><span data-stu-id="7803c-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="7803c-149">Klik in de 'Azure CDN' blade opslagaccount Hallo CDN-eindpunt op Hallo lijst tooopen CDN configuratie blade.</span><span class="sxs-lookup"><span data-stu-id="7803c-149">From storage account "Azure CDN" blade, click hello CDN endpoint from hello list tooopen CDN configuration blade.</span></span> <span data-ttu-id="7803c-150">U kunt aanvullende CDN-functies inschakelen voor uw levering, zoals compressie, queryreeks geo filteren.</span><span class="sxs-lookup"><span data-stu-id="7803c-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="7803c-151">U kunt ook aangepaste domein toewijzing tooyour CDN-eindpunt toevoegen en inschakelen van aangepast domein HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7803c-151">You can also add custom domain mapping tooyour CDN endpoint and enable custom domain HTTPS.</span></span>
    
![CDN-opslagconfiguratie cdn][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="7803c-153">Stap 4: Toegang tot CDN-inhoud</span><span class="sxs-lookup"><span data-stu-id="7803c-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="7803c-154">tooaccess in de cache inhoud op CDN hello, gebruik Hallo CDN-URL opgegeven in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="7803c-154">tooaccess cached content on hello CDN, use hello CDN URL provided in hello portal.</span></span> <span data-ttu-id="7803c-155">Hallo-adres voor een blob-cache is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="7803c-155">hello address for a cached blob will be similar toohello following:</span></span>

<span data-ttu-id="7803c-156">http://<*EndpointName*\>.azureedge.net/ <*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="7803c-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="7803c-157">Wanneer u CDN toegang tooa storage-account hebt ingeschakeld, zijn alle openbaar beschikbare objecten in aanmerking komen voor CDN edge cache.</span><span class="sxs-lookup"><span data-stu-id="7803c-157">Once you enable CDN access tooa storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="7803c-158">Als u een object dat momenteel in cache in Hallo CDN wijzigt, wordt Hallo nieuwe inhoud pas beschikbaar via Hallo CDN Hallo CDN wordt de inhoud vernieuwd wanneer Hallo in de cache opgeslagen inhoud time-to-live-periode is verstreken.</span><span class="sxs-lookup"><span data-stu-id="7803c-158">If you modify an object that is currently cached in hello CDN, hello new content will not be available via hello CDN until hello CDN refreshes its content when hello cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a><span data-ttu-id="7803c-159">Stap 5: Verwijder de inhoud uit CDN Hallo</span><span class="sxs-lookup"><span data-stu-id="7803c-159">Step 5: Remove content from hello CDN</span></span>
<span data-ttu-id="7803c-160">Als u niet langer wenst toocache een object in hello Azure Content Delivery Network (CDN), kunt u een van de volgende stappen uit Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7803c-160">If you no longer wish toocache an object in hello Azure Content Delivery Network (CDN), you can take one of hello following steps:</span></span>

* <span data-ttu-id="7803c-161">Kunt u Hallo private in plaats van een openbare container.</span><span class="sxs-lookup"><span data-stu-id="7803c-161">You can make hello container private instead of public.</span></span> <span data-ttu-id="7803c-162">Zie [anonieme leestoegang toocontainers en blobs beheren](../storage/blobs/storage-manage-access-to-resources.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7803c-162">See [Manage anonymous read access toocontainers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="7803c-163">U kunt uitschakelen of verwijderen van Hallo CDN-eindpunt met behulp van Hallo-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="7803c-163">You can disable or delete hello CDN endpoint using hello Management Portal.</span></span>
* <span data-ttu-id="7803c-164">U kunt uw gehoste service toono langer reageren toorequests voor Hallo object wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7803c-164">You can modify your hosted service toono longer respond toorequests for hello object.</span></span>

<span data-ttu-id="7803c-165">Een object dat al in de cache in Hallo CDN blijft in cache totdat Hallo time to live voor Hallo-object zijn verstreken of Hallo-eindpunt wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7803c-165">An object already cached in hello CDN will remain cached until hello time-to-live period for hello object expires or until hello endpoint is purged.</span></span> <span data-ttu-id="7803c-166">Wanneer Hallo time-to-live-periode is verstreken, controleert Hallo CDN toosee of Hallo CDN-eindpunt nog geldig is en Hallo-object is nog steeds anoniem toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="7803c-166">When hello time-to-live period expires, hello CDN will check toosee whether hello CDN endpoint is still valid and hello object still anonymously accessible.</span></span> <span data-ttu-id="7803c-167">Als dit niet het geval is, klikt u vervolgens Hallo-object wordt niet langer in de cache.</span><span class="sxs-lookup"><span data-stu-id="7803c-167">If it is not, then hello object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7803c-168">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7803c-168">Additional resources</span></span>
* [<span data-ttu-id="7803c-169">Hoe tooMap CDN inhoud tooa aangepaste domeinen</span><span class="sxs-lookup"><span data-stu-id="7803c-169">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="7803c-170">HTTPS inschakelen voor uw aangepaste domein</span><span class="sxs-lookup"><span data-stu-id="7803c-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
