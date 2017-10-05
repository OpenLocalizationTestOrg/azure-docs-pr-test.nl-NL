---
title: Een Azure storage-account integreren met Azure CDN | Microsoft Docs
description: Informatie over het gebruik van Azure inhoud Delivery Network (CDN) hoge bandbreedte inhoud leveren door blobs uit Azure Storage cache te plaatsen.
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
ms.openlocfilehash: 511076935d06ed0908341044e37069e74530be49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="0d2b6-103">Een Azure storage-account integreren met Azure CDN</span><span class="sxs-lookup"><span data-stu-id="0d2b6-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="0d2b6-104">CDN worden ingeschakeld voor het cache-inhoud van uw Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-104">CDN can be enabled to cache content from your Azure storage.</span></span> <span data-ttu-id="0d2b6-105">Het biedt ontwikkelaars een globale oplossing voor hoge bandbreedte inhoud leveren door blobs en statische inhoud van de compute-exemplaren op fysieke knooppunten in de Verenigde Staten, Europa, Azië, Australië en Zuid-Amerika cache te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="0d2b6-106">Stap 1: Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="0d2b6-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="0d2b6-107">Gebruik de volgende procedure voor het maken van een nieuw opslagaccount voor een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-107">Use the following procedure to create a new storage account for a Azure subscription.</span></span> <span data-ttu-id="0d2b6-108">Een opslagaccount biedt toegang tot Azure storage-services.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="0d2b6-109">Het opslagaccount vertegenwoordigt het hoogste niveau van de naamruimte voor het openen van elk van de onderdelen van de Azure storage-service: Blob-services, wachtrijservices en services van de tabel.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="0d2b6-110">Raadpleeg voor meer informatie de [Inleiding tot Microsoft Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0d2b6-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="0d2b6-111">Voor het maken van een opslagaccount, moet u de servicebeheerder of medebeheerder voor het gekoppelde abonnement.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="0d2b6-112">Er zijn verschillende methoden die u gebruiken kunt voor het maken van een opslagaccount, met inbegrip van de Azure Portal en Powershell.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span></span>  <span data-ttu-id="0d2b6-113">Voor deze zelfstudie worden gebruikt de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-113">For this tutorial, we'll be using the Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="0d2b6-114">**Een opslagaccount voor een Azure-abonnement maken**</span><span class="sxs-lookup"><span data-stu-id="0d2b6-114">**To create a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="0d2b6-115">Meld u aan bij [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d2b6-115">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0d2b6-116">Selecteer in de linkerbovenhoek **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-116">In the upper left corner, select **New**.</span></span> <span data-ttu-id="0d2b6-117">In de **nieuw** dialoogvenster **gegevens en opslag**, klikt u vervolgens op **opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="0d2b6-118">De **storage-account maken** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-118">The **Create storage account** blade appears.</span></span>   

    ![Storage-Account maken][create-new-storage-account]  

3. <span data-ttu-id="0d2b6-120">In de **naam** veld, typt u de subdomeinnaam.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-120">In the **Name** field, type a subdomain name.</span></span> <span data-ttu-id="0d2b6-121">Deze vermelding kan 3 tot 24 kleine letters en cijfers bevatten.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="0d2b6-122">Deze waarde wordt de hostnaam van de in de URI die wordt gebruikt om Blob, wachtrij of tabel bronnen voor het abonnement.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span></span> <span data-ttu-id="0d2b6-123">Om een container-bron in de Blob-service op te lossen, zou u een URI gebruikt in de volgende indeling waar  *&lt;StorageAccountLabel&gt;*  verwijst naar de waarde die u hebt opgegeven in **Voer een URL**:</span><span class="sxs-lookup"><span data-stu-id="0d2b6-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="0d2b6-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="0d2b6-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="0d2b6-125">**Belangrijk:** de URL label formulieren het subdomein van de URI van het opslagaccount en moet uniek zijn alle gehoste services in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="0d2b6-126">Deze waarde wordt ook gebruikt als de naam van dit opslagaccount in de portal of bij het openen van dit account via een programma.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="0d2b6-127">Laat de standaardwaarden voor **implementatiemodel**, **Account kind**, **prestaties**, en **replicatie**.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="0d2b6-128">Selecteer de **abonnement** die met de storage-account worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-128">Select the **Subscription** that the storage account will be used with.</span></span>
6. <span data-ttu-id="0d2b6-129">Selecteer of maak een **resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="0d2b6-130">Zie [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="0d2b6-131">Selecteer een locatie voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="0d2b6-132">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-132">Click **Create**.</span></span> <span data-ttu-id="0d2b6-133">Het proces van het maken van het opslagaccount kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-133">The process of creating the storage account might take several minutes to complete.</span></span>

## <a name="step-2-enable-cdn-for-the-storage-account"></a><span data-ttu-id="0d2b6-134">Stap 2: CDN inschakelen voor het opslagaccount</span><span class="sxs-lookup"><span data-stu-id="0d2b6-134">Step 2: Enable CDN for the storage account</span></span>

<span data-ttu-id="0d2b6-135">Met de nieuwste integratie kunt u nu CDN inschakelen voor uw opslagaccount zonder de uitbreiding van uw storage-portal.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-135">With the newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="0d2b6-136">Selecteer het opslagaccount, zoeken naar 'CDN' of schuif omlaag in het menu linkernavigatievenster aan en klik vervolgens op 'Azure CDN'.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-136">Select the storage account, search "CDN" or scroll down from the left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="0d2b6-137">De **Azure CDN** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-137">The **Azure CDN** blade appears.</span></span>

    ![CDN inschakelen navigatie][cdn-enable-navigation]
    
2. <span data-ttu-id="0d2b6-139">Maken van een nieuw eindpunt door te voeren van de vereiste informatie</span><span class="sxs-lookup"><span data-stu-id="0d2b6-139">Create a new endpoint by entering the required information</span></span>
    - <span data-ttu-id="0d2b6-140">**CDN-profiel**: U kunt een nieuwe maken of een bestaand profiel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="0d2b6-141">**Prijscategorie**: U hoeft alleen een prijscategorie selecteren als u een nieuw CDN-profiel maakt.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-141">**Pricing tier**: You only need to select a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="0d2b6-142">**De naam van de CDN-eindpunt**: Voer de naam van een eindpunt per uw keuze.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="0d2b6-143">Het gemaakte CDN-eindpunt wordt standaard de hostnaam van uw storage-account gebruikt als oorsprong.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-143">The created CDN endpoint uses the hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="0d2b6-144">! [cdn-eindpunt maken van nieuwe] [cdn--eindpunt-maken van nieuwe]</span><span class="sxs-lookup"><span data-stu-id="0d2b6-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="0d2b6-145">Na het maken, wordt het nieuwe eindpunt weergegeven in de bovenstaande endpoint-lijst.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-145">After creation, the new endpoint will show up in the endpoint list above.</span></span>

    ![storage-nieuwe CDN-eindpunt][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="0d2b6-147">U kunt ook gaan naar de extensie Azure CDN CDN inschakelen. [Zelfstudie](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="0d2b6-147">You can also go to Azure CDN extension to enable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="0d2b6-148">Stap 3: Extra CDN-functies inschakelen</span><span class="sxs-lookup"><span data-stu-id="0d2b6-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="0d2b6-149">Blade 'Azure CDN' opslagaccount, klik op het CDN-eindpunt in de lijst om CDN configuratie blade te openen.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-149">From storage account "Azure CDN" blade, click the CDN endpoint from the list to open CDN configuration blade.</span></span> <span data-ttu-id="0d2b6-150">U kunt aanvullende CDN-functies inschakelen voor uw levering, zoals compressie, queryreeks geo filteren.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="0d2b6-151">U kunt ook aangepaste domein toewijzing aan uw CDN-eindpunt toevoegen en inschakelen van aangepast domein HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-151">You can also add custom domain mapping to your CDN endpoint and enable custom domain HTTPS.</span></span>
    
![CDN-opslagconfiguratie cdn][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="0d2b6-153">Stap 4: Toegang tot CDN-inhoud</span><span class="sxs-lookup"><span data-stu-id="0d2b6-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="0d2b6-154">Gebruik voor toegang tot de inhoud in cache op de CDN moet de CDN-URL in de portal.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-154">To access cached content on the CDN, use the CDN URL provided in the portal.</span></span> <span data-ttu-id="0d2b6-155">Het adres van een blob in de cache is vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="0d2b6-155">The address for a cached blob will be similar to the following:</span></span>

<span data-ttu-id="0d2b6-156">http://<*EndpointName*\>.azureedge.net/ <*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="0d2b6-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="0d2b6-157">Wanneer u CDN toegang tot een opslagaccount hebt ingeschakeld, zijn alle openbaar beschikbare objecten in aanmerking komen voor CDN edge cache.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-157">Once you enable CDN access to a storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="0d2b6-158">Als u een object dat momenteel in cache in de CDN wijzigt, de nieuwe inhoud wordt niet meer beschikbaar via de CDN totdat de CDN wordt de inhoud vernieuwd wanneer het in cache opgeslagen inhoud time-to-live-periode is verstreken.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-158">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-the-cdn"></a><span data-ttu-id="0d2b6-159">Stap 5: De inhoud van het CDN verwijderen</span><span class="sxs-lookup"><span data-stu-id="0d2b6-159">Step 5: Remove content from the CDN</span></span>
<span data-ttu-id="0d2b6-160">Als u niet langer in de cache van een object in de Azure Content Delivery Network (CDN) wenst, kunt u een van de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0d2b6-160">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span></span>

* <span data-ttu-id="0d2b6-161">Kunt u de container private in plaats van openbaar.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-161">You can make the container private instead of public.</span></span> <span data-ttu-id="0d2b6-162">Zie [Anonieme leestoegang tot containers en blobs beheren](../storage/blobs/storage-manage-access-to-resources.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-162">See [Manage anonymous read access to containers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="0d2b6-163">U kunt uitschakelen of verwijderen van het CDN-eindpunt met behulp van de beheerportal.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-163">You can disable or delete the CDN endpoint using the Management Portal.</span></span>
* <span data-ttu-id="0d2b6-164">U kunt uw gehoste service niet meer reageren op aanvragen voor het object wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-164">You can modify your hosted service to no longer respond to requests for the object.</span></span>

<span data-ttu-id="0d2b6-165">Een object dat al in de cache in de CDN blijft in de cache totdat de time-to-live voor het object zijn verstreken of het eindpunt wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-165">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span></span> <span data-ttu-id="0d2b6-166">Wanneer de time-to-live-periode is verstreken, wordt de CDN gecontroleerd om te zien of het CDN-eindpunt nog geldig is en het object nog steeds anoniem toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-166">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span></span> <span data-ttu-id="0d2b6-167">Als dit niet het geval is, klikt u vervolgens het object wordt niet langer in de cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0d2b6-167">If it is not, then the object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d2b6-168">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0d2b6-168">Additional resources</span></span>
* [<span data-ttu-id="0d2b6-169">CDN-inhoud toewijzen aan een aangepast domein</span><span class="sxs-lookup"><span data-stu-id="0d2b6-169">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="0d2b6-170">HTTPS inschakelen voor uw aangepaste domein</span><span class="sxs-lookup"><span data-stu-id="0d2b6-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
