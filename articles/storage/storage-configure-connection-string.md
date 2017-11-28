---
title: aaaConfigure een verbindingsreeks voor Azure Storage | Microsoft Docs
description: Configureer een verbindingsreeks voor Azure storage-account. Een verbindingsreeks bevat Hallo informatie nodig tooauthenticate toegang krijgen tot tooa storage-account van uw toepassing tijdens runtime.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 80c38a6f8f0d4f06b99e7c487647b984e01d1772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="62978-104">Azure Storage-verbindingsreeksen configureren</span><span class="sxs-lookup"><span data-stu-id="62978-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="62978-105">Een verbindingsreeks bevat Hallo verificatie-informatie is vereist voor uw toepassing tooaccess gegevens in een Azure Storage-account tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="62978-105">A connection string includes hello authentication information required for your application tooaccess data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="62978-106">U kunt de verbindingsreeksen om te configureren:</span><span class="sxs-lookup"><span data-stu-id="62978-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="62978-107">Verbinding maken met Azure-opslagemulator toohello.</span><span class="sxs-lookup"><span data-stu-id="62978-107">Connect toohello Azure storage emulator.</span></span>
* <span data-ttu-id="62978-108">Toegang tot een opslagaccount in Azure.</span><span class="sxs-lookup"><span data-stu-id="62978-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="62978-109">Toegang tot de opgegeven resources in Azure via een shared access signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="62978-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="62978-110">Opslaan van de verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="62978-110">Storing your connection string</span></span>
<span data-ttu-id="62978-111">Uw toepassing moet tooaccess Hallo-verbindingsreeks in runtime tooauthenticate aanvragen tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="62978-111">Your application needs tooaccess hello connection string at runtime tooauthenticate requests made tooAzure Storage.</span></span> <span data-ttu-id="62978-112">U hebt verschillende mogelijkheden voor het opslaan van de verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="62978-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="62978-113">Hallo-verbindingsreeks in kan worden opgeslagen in een toepassing wordt uitgevoerd op Hallo bureaublad of op een apparaat een **app.config** of **web.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="62978-113">An application running on hello desktop or on a device can store hello connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="62978-114">Toevoegen van Hallo connection string toohello **AppSettings** sectie in deze bestanden.</span><span class="sxs-lookup"><span data-stu-id="62978-114">Add hello connection string toohello **AppSettings** section in these files.</span></span>
* <span data-ttu-id="62978-115">Een toepassing die wordt uitgevoerd in een Azure cloudservice Hallo verbindingsreeks kunt opslaan in Hallo [Azure-service-configuratiebestand (.cscfg) schema](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="62978-115">An application running in an Azure cloud service can store hello connection string in hello [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="62978-116">Toevoegen van Hallo connection string toohello **ConfigurationSettings** gedeelte van configuratiebestand Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="62978-116">Add hello connection string toohello **ConfigurationSettings** section of hello service configuration file.</span></span>
* <span data-ttu-id="62978-117">Rechtstreeks in uw code kunt u de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="62978-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="62978-118">We raden echter aan de verbindingsreeks op te slaan in een configuratiebestand in de meeste scenario's.</span><span class="sxs-lookup"><span data-stu-id="62978-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="62978-119">De verbindingstekenreeks opslaan in een configuratiebestand maakt het eenvoudig tooupdate Hallo connection string tooswitch tussen Hallo opslagemulator en een Azure storage-account in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="62978-119">Storing your connection string in a configuration file makes it easy tooupdate hello connection string tooswitch between hello storage emulator and an Azure storage account in hello cloud.</span></span> <span data-ttu-id="62978-120">U hoeft alleen tooedit Hallo connection string toopoint tooyour met doelomgeving.</span><span class="sxs-lookup"><span data-stu-id="62978-120">You only need tooedit hello connection string toopoint tooyour target environment.</span></span>

<span data-ttu-id="62978-121">U kunt Hallo [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess uw connection string tijdens runtime, ongeacht waar uw toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="62978-121">You can use hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-hello-storage-emulator"></a><span data-ttu-id="62978-122">Een verbindingsreeks voor de opslagemulator Hallo maken</span><span class="sxs-lookup"><span data-stu-id="62978-122">Create a connection string for hello storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="62978-123">Zie voor meer informatie over de opslagemulator hello [hello Azure-opslagemulator gebruiken voor ontwikkeling en tests](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="62978-123">For more information about hello storage emulator, see [Use hello Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="62978-124">Een verbindingsreeks voor Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="62978-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="62978-125">toocreate een verbindingsreeks voor uw Azure storage-account, gebruik Hallo volgende-indeling.</span><span class="sxs-lookup"><span data-stu-id="62978-125">toocreate a connection string for your Azure storage account, use hello following format.</span></span> <span data-ttu-id="62978-126">Aangeven of u wilt dat tooconnect toohello storage-account via HTTPS (aanbevolen) of HTTP-, vervangen door `myAccountName` met de naam van uw opslagaccount en vervang Hallo `myAccountKey` door uw toegangssleutel voor account:</span><span class="sxs-lookup"><span data-stu-id="62978-126">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="62978-127">De verbindingsreeks er ongeveer als:</span><span class="sxs-lookup"><span data-stu-id="62978-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="62978-128">Hoewel Azure Storage zowel HTTP als HTTPS in een verbindingsreeks ondersteunt *HTTPS wordt nadrukkelijk aanbevolen*.</span><span class="sxs-lookup"><span data-stu-id="62978-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="62978-129">U vindt uw storage-account verbindingsreeksen in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="62978-129">You can find your storage account's connection strings in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="62978-130">Navigeer te**instellingen** > **toegangssleutels** in uw opslagaccount menu blade toosee verbindingsreeksen voor beide primaire en secundaire toegangstoetsen.</span><span class="sxs-lookup"><span data-stu-id="62978-130">Navigate too**SETTINGS** > **Access keys** in your storage account's menu blade toosee connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="62978-131">Een verbindingsreeks met behulp van een shared access signature maken</span><span class="sxs-lookup"><span data-stu-id="62978-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="62978-132">Een verbindingsreeks voor een eindpunt expliciete opslag maken</span><span class="sxs-lookup"><span data-stu-id="62978-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="62978-133">U kunt expliciete service-eindpunten in de verbindingsreeks in plaats van de Standaardeindpunten Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="62978-133">You can specify explicit service endpoints in your connection string instead of using hello default endpoints.</span></span> <span data-ttu-id="62978-134">Hallo volledige service-eindpunt voor elke service, inclusief Hallo protocol specification (HTTPS (aanbevolen) of HTTP) toocreate een verbindingsreeks die Hiermee geeft u een expliciete eindpunt opgeven in Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="62978-134">toocreate a connection string that specifies an explicit endpoint, specify hello complete service endpoint for each service, including hello protocol specification (HTTPS (recommended) or HTTP), in hello following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="62978-135">Een scenario waar u toospecify een expliciete eindpunt wilt mogelijk is wanneer u uw tooa eindpunt van Blob-opslag hebt toegewezen [aangepast domein](storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="62978-135">One scenario where you might wish toospecify an explicit endpoint is when you've mapped your Blob storage endpoint tooa [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="62978-136">In dat geval kunt u uw aangepaste eindpunt voor Blob storage in de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="62978-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="62978-137">U kunt eventueel opgeven Hallo Standaardeindpunten voor Hallo andere services als uw toepassing worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="62978-137">You can optionally specify hello default endpoints for hello other services if your application uses them.</span></span>

<span data-ttu-id="62978-138">Hier volgt een voorbeeld van een verbindingsreeks waarmee een expliciete eindpunt voor Hallo Blob-service:</span><span class="sxs-lookup"><span data-stu-id="62978-138">Here is an example of a connection string that specifies an explicit endpoint for hello Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="62978-139">In dit voorbeeld geeft expliciet eindpunten voor alle services, met inbegrip van een aangepast domein voor Hallo Blob-service:</span><span class="sxs-lookup"><span data-stu-id="62978-139">This example specifies explicit endpoints for all services, including a custom domain for hello Blob service:</span></span>

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="62978-140">Hallo eindpunt waarden in een verbindingsreeks zijn gebruikte tooconstruct Hallo aanvragen URI's toohello storage-services en dicteren Hallo vorm van een URI's die worden geretourneerd tooyour code.</span><span class="sxs-lookup"><span data-stu-id="62978-140">hello endpoint values in a connection string are used tooconstruct hello request URIs toohello storage services, and dictate hello form of any URIs that are returned tooyour code.</span></span>

<span data-ttu-id="62978-141">Als u een aangepast domein voor opslag eindpunt tooa hebt toegewezen en dat eindpunt van een verbindingsreeks weglaat, wordt u niet kunt toouse tekenreeks die verbinding tooaccess gegevens in die service vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="62978-141">If you've mapped a storage endpoint tooa custom domain and omit that endpoint from a connection string, then you will not be able toouse that connection string tooaccess data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62978-142">Service-eindpunt waarden in de verbindingsreeksen moeten juist opgemaakte URI's, met inbegrip van `https://` (aanbevolen) of `http://`.</span><span class="sxs-lookup"><span data-stu-id="62978-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="62978-143">Omdat Azure Storage nog geen HTTPS voor aangepaste domeinen ondersteunt u *moet* Geef `http://` voor een willekeurig eindpunt-URI die het aangepaste domein tooa verwijst.</span><span class="sxs-lookup"><span data-stu-id="62978-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points tooa custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="62978-144">Een verbindingsreeks met het achtervoegsel van een eindpunt maken</span><span class="sxs-lookup"><span data-stu-id="62978-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="62978-145">toocreate een verbinding de tekenreeks voor een service-opslag in regio's of exemplaren met verschillende eindpunt achtervoegsels, zoals voor Azure China of Azure Government, gebruik Hallo indeling voor een verbindingsreeks te volgen.</span><span class="sxs-lookup"><span data-stu-id="62978-145">toocreate a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use hello following connection string format.</span></span> <span data-ttu-id="62978-146">Aangeven of u wilt dat tooconnect toohello storage-account via HTTPS (aanbevolen) of HTTP-, vervangen door `myAccountName` vervangen met de naam van uw opslagaccount hello `myAccountKey` met uw toegangssleutel en vervangen `mySuffix` Hello URI achtervoegsel:</span><span class="sxs-lookup"><span data-stu-id="62978-146">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with hello URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="62978-147">Hier volgt een voorbeeld van de verbindingsreeks voor storage-services in Azure voor China:</span><span class="sxs-lookup"><span data-stu-id="62978-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="62978-148">Een verbindingsreeks te parseren</span><span class="sxs-lookup"><span data-stu-id="62978-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="62978-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62978-149">Next steps</span></span>
* [<span data-ttu-id="62978-150">Hello Azure-opslagemulator gebruiken voor ontwikkeling en testen</span><span class="sxs-lookup"><span data-stu-id="62978-150">Use hello Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="62978-151">Azure Storage explorers</span><span class="sxs-lookup"><span data-stu-id="62978-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="62978-152">Met behulp van Shared Access Signatures (SAS)</span><span class="sxs-lookup"><span data-stu-id="62978-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

