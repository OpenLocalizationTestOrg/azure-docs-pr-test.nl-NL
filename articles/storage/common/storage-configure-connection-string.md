---
title: Een verbindingsreeks configureren voor Azure Storage | Microsoft Docs
description: "Configureer een verbindingsreeks voor Azure storage-account. Een verbindingsreeks bevat de informatie die nodig zijn voor het verifiëren van toegang tot een opslagaccount van uw toepassing tijdens runtime."
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
ms.openlocfilehash: 4b21e75fde55f195362809ce486a2615954ff93c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="60e84-104">Azure Storage-verbindingsreeksen configureren</span><span class="sxs-lookup"><span data-stu-id="60e84-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="60e84-105">Een verbindingsreeks bevat de verificatiegegevens die nodig zijn voor uw toepassing voor toegang tot gegevens in een Azure Storage-account tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="60e84-105">A connection string includes the authentication information required for your application to access data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="60e84-106">U kunt de verbindingsreeksen om te configureren:</span><span class="sxs-lookup"><span data-stu-id="60e84-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="60e84-107">Verbinding maken met de Azure-opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="60e84-107">Connect to the Azure storage emulator.</span></span>
* <span data-ttu-id="60e84-108">Toegang tot een opslagaccount in Azure.</span><span class="sxs-lookup"><span data-stu-id="60e84-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="60e84-109">Toegang tot de opgegeven resources in Azure via een shared access signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="60e84-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="60e84-110">Opslaan van de verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="60e84-110">Storing your connection string</span></span>
<span data-ttu-id="60e84-111">Uw toepassing moet toegang tot de verbindingsreeks in runtime te verifiëren van aanvragen voor Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="60e84-111">Your application needs to access the connection string at runtime to authenticate requests made to Azure Storage.</span></span> <span data-ttu-id="60e84-112">U hebt verschillende mogelijkheden voor het opslaan van de verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="60e84-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="60e84-113">De verbindingsreeks in kan worden opgeslagen in een toepassing wordt uitgevoerd op het bureaublad of op een apparaat een **app.config** of **web.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="60e84-113">An application running on the desktop or on a device can store the connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="60e84-114">Toevoegen van de verbindingsreeks naar de **AppSettings** sectie in deze bestanden.</span><span class="sxs-lookup"><span data-stu-id="60e84-114">Add the connection string to the **AppSettings** section in these files.</span></span>
* <span data-ttu-id="60e84-115">Een toepassing die wordt uitgevoerd in een Azure-cloud-service kan opslaan van de verbindingsreeks in de [Azure-service-configuratiebestand (.cscfg) schema](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="60e84-115">An application running in an Azure cloud service can store the connection string in the [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="60e84-116">Toevoegen van de verbindingsreeks naar de **ConfigurationSettings** gedeelte van het configuratiebestand van de service.</span><span class="sxs-lookup"><span data-stu-id="60e84-116">Add the connection string to the **ConfigurationSettings** section of the service configuration file.</span></span>
* <span data-ttu-id="60e84-117">Rechtstreeks in uw code kunt u de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="60e84-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="60e84-118">We raden echter aan de verbindingsreeks op te slaan in een configuratiebestand in de meeste scenario's.</span><span class="sxs-lookup"><span data-stu-id="60e84-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="60e84-119">De verbindingstekenreeks opslaan in een configuratiebestand, kunt u gemakkelijk bijwerken van de verbindingsreeks in te schakelen tussen de opslagemulator en Azure storage-account in de cloud.</span><span class="sxs-lookup"><span data-stu-id="60e84-119">Storing your connection string in a configuration file makes it easy to update the connection string to switch between the storage emulator and an Azure storage account in the cloud.</span></span> <span data-ttu-id="60e84-120">Alleen moet u de verbindingsreeks om te verwijzen naar de doelomgeving.</span><span class="sxs-lookup"><span data-stu-id="60e84-120">You only need to edit the connection string to point to your target environment.</span></span>

<span data-ttu-id="60e84-121">U kunt de [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) voor toegang tot de verbindingsreeks in runtime ongeacht waar uw toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="60e84-121">You can use the [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) to access your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-the-storage-emulator"></a><span data-ttu-id="60e84-122">Maken van een verbindingsreeks voor de opslagemulator</span><span class="sxs-lookup"><span data-stu-id="60e84-122">Create a connection string for the storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="60e84-123">Zie voor meer informatie over de opslagemulator [de Azure-opslagemulator gebruiken voor ontwikkeling en tests](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="60e84-123">For more information about the storage emulator, see [Use the Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="60e84-124">Een verbindingsreeks voor Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="60e84-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="60e84-125">Gebruik de volgende notatie voor het maken van een verbindingsreeks voor uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="60e84-125">To create a connection string for your Azure storage account, use the following format.</span></span> <span data-ttu-id="60e84-126">Aangeven of u wilt verbinding maken met het opslagaccount via HTTPS (aanbevolen) of HTTP-, vervangen door `myAccountName` met de naam van uw opslagaccount en vervang `myAccountKey` door uw toegangssleutel voor account:</span><span class="sxs-lookup"><span data-stu-id="60e84-126">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="60e84-127">De verbindingsreeks er ongeveer als:</span><span class="sxs-lookup"><span data-stu-id="60e84-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="60e84-128">Hoewel Azure Storage zowel HTTP als HTTPS in een verbindingsreeks ondersteunt *HTTPS wordt nadrukkelijk aanbevolen*.</span><span class="sxs-lookup"><span data-stu-id="60e84-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="60e84-129">U vindt de verbindingsreeksen uw storage-account in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60e84-129">You can find your storage account's connection strings in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="60e84-130">Navigeer naar **instellingen** > **toegangssleutels** in uw opslagaccount menu blade verbindingsreeksen voor beide primaire en secundaire sneltoetsen te zien.</span><span class="sxs-lookup"><span data-stu-id="60e84-130">Navigate to **SETTINGS** > **Access keys** in your storage account's menu blade to see connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="60e84-131">Een verbindingsreeks met behulp van een shared access signature maken</span><span class="sxs-lookup"><span data-stu-id="60e84-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="60e84-132">Een verbindingsreeks voor een eindpunt expliciete opslag maken</span><span class="sxs-lookup"><span data-stu-id="60e84-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="60e84-133">U kunt expliciete service-eindpunten in de verbindingsreeks in plaats van de Standaardeindpunten opgeven.</span><span class="sxs-lookup"><span data-stu-id="60e84-133">You can specify explicit service endpoints in your connection string instead of using the default endpoints.</span></span> <span data-ttu-id="60e84-134">Geef het volledige service-eindpunt voor elke service, inclusief de specificatie van het protocol (HTTPS (aanbevolen) of HTTP) in de volgende notatie voor het maken van een verbindingsreeks die Hiermee geeft u een expliciete eindpunt:</span><span class="sxs-lookup"><span data-stu-id="60e84-134">To create a connection string that specifies an explicit endpoint, specify the complete service endpoint for each service, including the protocol specification (HTTPS (recommended) or HTTP), in the following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="60e84-135">Een scenario waarin u wilt mogelijk een expliciete eindpunt opgeven is wanneer u het eindpunt van de Blob-opslag naar hebt toegewezen een [aangepast domein](../blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="60e84-135">One scenario where you might wish to specify an explicit endpoint is when you've mapped your Blob storage endpoint to a [custom domain](../blobs/storage-custom-domain-name.md).</span></span> <span data-ttu-id="60e84-136">In dat geval kunt u uw aangepaste eindpunt voor Blob storage in de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="60e84-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="60e84-137">Als uw toepassing worden gebruikt, kunt u eventueel de Standaardeindpunten voor de andere services opgeven.</span><span class="sxs-lookup"><span data-stu-id="60e84-137">You can optionally specify the default endpoints for the other services if your application uses them.</span></span>

<span data-ttu-id="60e84-138">Hier volgt een voorbeeld van een verbindingsreeks waarmee een expliciete eindpunt voor de Blob-service:</span><span class="sxs-lookup"><span data-stu-id="60e84-138">Here is an example of a connection string that specifies an explicit endpoint for the Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="60e84-139">In dit voorbeeld geeft expliciet eindpunten voor alle services, met inbegrip van een aangepast domein voor de Blob-service:</span><span class="sxs-lookup"><span data-stu-id="60e84-139">This example specifies explicit endpoints for all services, including a custom domain for the Blob service:</span></span>

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

<span data-ttu-id="60e84-140">De eindpunt-waarden in een verbindingsreeks worden gebruikt voor het maken van de aanvraag-URI's voor de storage-services en dicteren de vorm van een URI's die worden geretourneerd aan uw code.</span><span class="sxs-lookup"><span data-stu-id="60e84-140">The endpoint values in a connection string are used to construct the request URIs to the storage services, and dictate the form of any URIs that are returned to your code.</span></span>

<span data-ttu-id="60e84-141">Als u een eindpunt opslag hebt toegewezen aan een aangepast domein en dat eindpunt van een verbindingsreeks weglaat, klikt zich u niet kunnen deze verbindingsreeks gebruiken voor toegang tot gegevens in die service vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="60e84-141">If you've mapped a storage endpoint to a custom domain and omit that endpoint from a connection string, then you will not be able to use that connection string to access data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60e84-142">Service-eindpunt waarden in de verbindingsreeksen moeten juist opgemaakte URI's, met inbegrip van `https://` (aanbevolen) of `http://`.</span><span class="sxs-lookup"><span data-stu-id="60e84-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="60e84-143">Omdat Azure Storage nog geen HTTPS voor aangepaste domeinen ondersteunt u *moet* Geef `http://` voor een willekeurig eindpunt-URI die naar een aangepast domein verwijst.</span><span class="sxs-lookup"><span data-stu-id="60e84-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points to a custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="60e84-144">Een verbindingsreeks met het achtervoegsel van een eindpunt maken</span><span class="sxs-lookup"><span data-stu-id="60e84-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="60e84-145">Gebruik de indeling van de volgende verbindingsreeks voor het maken van een verbindingsreeks voor een service-opslag in regio's of exemplaren met verschillende eindpunt achtervoegsels, zoals voor Azure China of Azure Government.</span><span class="sxs-lookup"><span data-stu-id="60e84-145">To create a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use the following connection string format.</span></span> <span data-ttu-id="60e84-146">Aangeven of u wilt verbinding maken met het opslagaccount via HTTPS (aanbevolen) of HTTP-, vervangen door `myAccountName` vervangen door de naam van uw opslagaccount, `myAccountKey` met uw toegangssleutel en vervangen `mySuffix` met het achtervoegsel URI:</span><span class="sxs-lookup"><span data-stu-id="60e84-146">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with the URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="60e84-147">Hier volgt een voorbeeld van de verbindingsreeks voor storage-services in Azure voor China:</span><span class="sxs-lookup"><span data-stu-id="60e84-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="60e84-148">Een verbindingsreeks te parseren</span><span class="sxs-lookup"><span data-stu-id="60e84-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="60e84-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="60e84-149">Next steps</span></span>
* [<span data-ttu-id="60e84-150">De Azure-opslagemulator gebruiken voor ontwikkeling en testen</span><span class="sxs-lookup"><span data-stu-id="60e84-150">Use the Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="60e84-151">Azure Storage explorers</span><span class="sxs-lookup"><span data-stu-id="60e84-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="60e84-152">Met behulp van Shared Access Signatures (SAS)</span><span class="sxs-lookup"><span data-stu-id="60e84-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

