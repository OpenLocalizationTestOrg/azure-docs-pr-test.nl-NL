---
title: Toepassingspakketten op rekenknooppunten - Azure Batch installeren | Microsoft Docs
description: Gebruik de functie voor de toepassing-pakketten van Azure Batch eenvoudig beheren meerdere toepassingen en versies voor de installatie van Batch-rekenknooppunten.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: afcc04c80ec15872a22de5d5969a7ef6a583562f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="46a78-103">Toepassingen implementeren op rekenknooppunten met Batch-toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="46a78-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="46a78-104">De functie voor de toepassing-pakketten van Azure Batch biedt eenvoudig beheer van toepassingen van de taak en de implementatie ervan in de rekenknooppunten in uw groep.</span><span class="sxs-lookup"><span data-stu-id="46a78-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="46a78-105">U kunt met toepassingspakketten kunt uploaden en beheren van meerdere versies van de toepassingen die de taken worden uitgevoerd, met inbegrip van hun ondersteunende bestanden.</span><span class="sxs-lookup"><span data-stu-id="46a78-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="46a78-106">U kunt vervolgens automatisch implementeren een of meer van deze toepassingen aan de rekenknooppunten in uw groep.</span><span class="sxs-lookup"><span data-stu-id="46a78-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="46a78-107">In dit artikel leert u hoe uploaden en beheren in de Azure portal-toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="46a78-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="46a78-108">Vervolgens leert u hoe u ze moet installeren op een pool van rekenknooppunten met de [Batch .NET] [ api_net] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="46a78-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="46a78-109">Toepassingspakketten worden ondersteund in alle Batch-pools die na 5 juli 2017 zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46a78-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="46a78-110">De pakketten worden ondersteund in Batch-pools die zijn gemaakt tussen 10 maart 2016 en 5 juli 2017, maar alleen als de pool is gemaakt met behulp van een cloudservice-configuratie.</span><span class="sxs-lookup"><span data-stu-id="46a78-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="46a78-111">Batch-pools die zijn gemaakt vóór 10 maart 2016 bieden geen ondersteuning voor toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="46a78-111">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="46a78-112">De API's voor het maken en beheren van toepassingspakketten deel uitmaken van de [Batch Management .NET] [[api_net_mgmt]] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="46a78-112">The APIs for creating and managing application packages are part of the [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="46a78-113">De API's voor toepassingspakketten installeren op een rekenknooppunt deel uitmaken van de [Batch .NET] [ api_net] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="46a78-113">The APIs for installing application packages on a compute node are part of the [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="46a78-114">De toepassing pakketten functie hier beschreven vervangt de beschikbaar in eerdere versies van de service Batch Apps-functie.</span><span class="sxs-lookup"><span data-stu-id="46a78-114">The application packages feature described here supersedes the Batch Apps feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="46a78-115">Vereisten voor Application-pakket</span><span class="sxs-lookup"><span data-stu-id="46a78-115">Application package requirements</span></span>
<span data-ttu-id="46a78-116">Voor het gebruik van toepassingspakketten, moet u [een Azure Storage-account koppelen](#link-a-storage-account) aan uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="46a78-116">To use application packages, you need to [link an Azure Storage account](#link-a-storage-account) to your Batch account.</span></span>

<span data-ttu-id="46a78-117">Deze functie is geïntroduceerd [Batch REST-API] [ api_rest] versie 2015-12-01.2.2 en de bijbehorende [Batch .NET] [ api_net] library-versie 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="46a78-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="46a78-118">Het is raadzaam dat u de nieuwste API-versie altijd gebruiken bij het werken met de Batch.</span><span class="sxs-lookup"><span data-stu-id="46a78-118">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="46a78-119">Toepassingspakketten worden ondersteund in alle Batch-pools die na 5 juli 2017 zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46a78-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="46a78-120">De pakketten worden ondersteund in Batch-pools die zijn gemaakt tussen 10 maart 2016 en 5 juli 2017, maar alleen als de pool is gemaakt met behulp van een cloudservice-configuratie.</span><span class="sxs-lookup"><span data-stu-id="46a78-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="46a78-121">Batch-pools die zijn gemaakt vóór 10 maart 2016 bieden geen ondersteuning voor toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="46a78-121">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="46a78-122">Over de toepassingen en toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="46a78-122">About applications and application packages</span></span>
<span data-ttu-id="46a78-123">In Azure Batch een *toepassing* verwijst naar een set van samengestelde binaire bestanden gebruikt die automatisch kan worden gedownload op de rekenknooppunten in uw groep.</span><span class="sxs-lookup"><span data-stu-id="46a78-123">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="46a78-124">Een *toepassingspakket* verwijst naar een *specifieke set* van deze binaire bestanden en vertegenwoordigt een gegeven *versie* van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="46a78-124">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="46a78-125">![Op hoog niveau diagram van toepassingen en toepassingspakketten][1]</span><span class="sxs-lookup"><span data-stu-id="46a78-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="46a78-126">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="46a78-126">Applications</span></span>
<span data-ttu-id="46a78-127">Een toepassing in Batch bevat een of meer toepassingen, pakketten en configuratieopties voor de toepassing bevat.</span><span class="sxs-lookup"><span data-stu-id="46a78-127">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="46a78-128">Een toepassing kunt bijvoorbeeld opgeven dat de standaardversie voor het pakket van toepassing te installeren op de rekenknooppunten en of de pakketten kunnen worden bijgewerkt of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="46a78-128">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="46a78-129">Toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="46a78-129">Application packages</span></span>
<span data-ttu-id="46a78-130">Een toepassingspakket is een ZIP-bestand met de binaire bestanden van de toepassing en de ondersteunende bestanden die vereist zijn voor uw taken de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="46a78-130">An application package is a .zip file that contains the application binaries and supporting files that are required for your tasks to run the application.</span></span> <span data-ttu-id="46a78-131">Elke toepassingspakket vertegenwoordigt een specifieke versie van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="46a78-131">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="46a78-132">U kunt toepassingspakketten op het niveau van toepassingen en de taak opgeven.</span><span class="sxs-lookup"><span data-stu-id="46a78-132">You can specify application packages at the pool and task levels.</span></span> <span data-ttu-id="46a78-133">U kunt een of meer van deze pakketten en (optioneel) een versie opgeven wanneer u een groep of een taak maakt.</span><span class="sxs-lookup"><span data-stu-id="46a78-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="46a78-134">**Toepassingspakketten groep** zijn geïmplementeerd op *elke* knooppunt in de pool.</span><span class="sxs-lookup"><span data-stu-id="46a78-134">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="46a78-135">Toepassingen worden geïmplementeerd als een knooppunt aan een pool wordt toegevoegd en wanneer deze wordt opgestart of hersteld met een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="46a78-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="46a78-136">Toepassingspakketten voor toepassingen zijn geschikt wanneer alle knooppunten in een pool van een taak taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="46a78-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="46a78-137">Een of meer toepassingspakketten kunt u opgeven wanneer u een pool maakt en u kunt toevoegen of bijwerken van een bestaande pool-pakketten.</span><span class="sxs-lookup"><span data-stu-id="46a78-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="46a78-138">Als u een bestaande pool toepassingspakketten bijwerkt, moet u de knooppunten voor de installatie van het nieuwe pakket opnieuw.</span><span class="sxs-lookup"><span data-stu-id="46a78-138">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="46a78-139">**Taak toepassingspakketten** zijn alleen geïmplementeerd op een rekenknooppunt uitgevoerd van een taak, net voordat de opdrachtregel van de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="46a78-139">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="46a78-140">Als de opgegeven toepassingspakket en de versie is al op het knooppunt, niet opnieuw gedistribueerd en het bestaande pakket wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="46a78-140">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="46a78-141">Taak toepassingspakketten zijn handig in gedeelde groep omgevingen, waarbij verschillende taken worden uitgevoerd op één groep, en de groep is niet verwijderd wanneer een taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="46a78-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="46a78-142">Als de job minder taken dan knooppunten in de groep heeft, kunnen toepassingspakketten van taken gegevensoverdracht minimaliseren omdat uw toepassing alleen wordt geïmplementeerd op de knooppunten die taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="46a78-142">If your job has fewer tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="46a78-143">Andere scenario's waarin u van de taak toepassingspakketten profiteren kunnen zijn taken met een grote toepassing, maar voor alleen enkele taken.</span><span class="sxs-lookup"><span data-stu-id="46a78-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="46a78-144">Een vooraf verwerken fase of een merge-taak, waarbij de toepassing vooraf verwerken of het samenvoegen van zware is, kan bijvoorbeeld profiteren van het gebruik van de taak toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="46a78-144">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46a78-145">Er gelden beperkingen op het aantal toepassingen en toepassingspakketten in een Batch-account en de maximale grootte van pakket.</span><span class="sxs-lookup"><span data-stu-id="46a78-145">There are restrictions on the number of applications and application packages within a Batch account and on the maximum application package size.</span></span> <span data-ttu-id="46a78-146">Zie [quota en limieten voor de Azure Batch-service](batch-quota-limit.md) voor meer informatie over deze limieten.</span><span class="sxs-lookup"><span data-stu-id="46a78-146">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="46a78-147">Voordelen van toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="46a78-147">Benefits of application packages</span></span>
<span data-ttu-id="46a78-148">Toepassingspakketten kunnen vereenvoudigen de code in uw Batch-oplossing, en verlagen de overhead voor het beheren van de toepassingen die de taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="46a78-148">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="46a78-149">Met toepassingspakketten kunt geen begintaak uw pool een lange lijst met afzonderlijke bronbestanden installeren op de knooppunten opgeven.</span><span class="sxs-lookup"><span data-stu-id="46a78-149">With application packages, your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="46a78-150">U hoeft niet te handmatig beheer van meerdere versies van uw toepassingsbestanden in Azure Storage of op de knooppunten.</span><span class="sxs-lookup"><span data-stu-id="46a78-150">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="46a78-151">En u hoeft niet te hoeven maken over het genereren van [SAS-URL's](../storage/common/storage-dotnet-shared-access-signature-part-1.md) voor toegang tot de bestanden in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="46a78-151">And, you don't need to worry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="46a78-152">Batch werkt op de achtergrond met Azure Storage-toepassingspakketten opslaan en deze rekenknooppunten implementeren.</span><span class="sxs-lookup"><span data-stu-id="46a78-152">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="46a78-153">De totale grootte van een begintaak moet kleiner zijn dan of gelijk zijn aan 32.768 tekens, inclusief bronbestanden en omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="46a78-153">The total size of a start task must be less than or equal to 32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="46a78-154">Als uw begintaak deze limiet overschrijdt, is met behulp van toepassingspakketten een andere optie.</span><span class="sxs-lookup"><span data-stu-id="46a78-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="46a78-155">U kunt ook maken een ZIP-archief met de bronbestanden, uploaden als een blob naar Azure Storage en pak deze vervolgens vanaf de opdrachtregel van de begintaak.</span><span class="sxs-lookup"><span data-stu-id="46a78-155">You can also create a zipped archive containing your resource files, upload it as a blob to Azure Storage, and then unzip it from the command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="46a78-156">Uploaden en beheren van toepassingen</span><span class="sxs-lookup"><span data-stu-id="46a78-156">Upload and manage applications</span></span>
<span data-ttu-id="46a78-157">U kunt de [Azure-portal] [ portal] of de [Batch Management .NET](batch-management-dotnet.md) bibliotheek voor het beheren van de toepassingspakketten in uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="46a78-157">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="46a78-158">In de volgende secties laten we eerst zien hoe een opslagaccount te koppelen en vervolgens bespreken toe te voegen toepassingen en pakketten en deze te beheren met de portal.</span><span class="sxs-lookup"><span data-stu-id="46a78-158">In the next few sections, we first show how to link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="46a78-159">Storage-account koppelen</span><span class="sxs-lookup"><span data-stu-id="46a78-159">Link a Storage account</span></span>
<span data-ttu-id="46a78-160">Voor het gebruik van toepassingspakketten, moet u eerst een Azure Storage-account koppelen aan uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="46a78-160">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="46a78-161">Als u een opslagaccount nog niet hebt geconfigureerd, de Azure-portal wordt weergegeven een waarschuwing de eerste keer dat u op de **toepassingen** -tegel in de **Batch-account** blade.</span><span class="sxs-lookup"><span data-stu-id="46a78-161">If you have not yet configured a Storage account, the Azure portal displays a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46a78-162">Batch ondersteunt momenteel *alleen* de **algemeen** opslagaccounttype zoals beschreven in stap 5, [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)in [over Azure Storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="46a78-162">Batch currently supports *only* the **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="46a78-163">Wanneer u een Azure Storage-account aan uw Batch-account koppelt, een koppeling *alleen* een **algemeen** storage-account.</span><span class="sxs-lookup"><span data-stu-id="46a78-163">When you link an Azure Storage account to your Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="46a78-164">!['Er is geen opslagaccount geconfigureerd' waarschuwing in Azure-portal][9]</span><span class="sxs-lookup"><span data-stu-id="46a78-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="46a78-165">De Batch-service gebruikt het bijbehorende opslagaccount voor het opslaan van uw toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="46a78-165">The Batch service uses the associated Storage account to store your application packages.</span></span> <span data-ttu-id="46a78-166">Nadat u de twee accounts hebt gekoppeld, kan de pakketten die zijn opgeslagen in de gekoppelde Storage-account aan uw rekenknooppunten automatisch implementeren door Batch.</span><span class="sxs-lookup"><span data-stu-id="46a78-166">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="46a78-167">Als u wilt een Storage-account koppelen aan uw Batch-account, klikt u op **instellingen voor de opslag** op de **waarschuwing** blade en klik vervolgens op **Opslagaccount** op de  **Storage-Account** blade.</span><span class="sxs-lookup"><span data-stu-id="46a78-167">To link a Storage account to your Batch account, click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade.</span></span>

<span data-ttu-id="46a78-168">![Kies de blade opslagaccount in Azure-portal][10]</span><span class="sxs-lookup"><span data-stu-id="46a78-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="46a78-169">Het is raadzaam dat u een opslagaccount maken *specifiek* voor gebruik met uw Batch-account en selecteert u deze hier.</span><span class="sxs-lookup"><span data-stu-id="46a78-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="46a78-170">Zie voor meer informatie over het maken van een opslagaccount 'Een opslagaccount maken' [over Azure Storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="46a78-170">For details about how to create a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="46a78-171">Nadat u een opslagaccount hebt gemaakt, kunt u vervolgens deze koppelen aan uw Batch-account met behulp van de **Opslagaccount** blade.</span><span class="sxs-lookup"><span data-stu-id="46a78-171">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="46a78-172">De Batch-service gebruikt Azure Storage voor het opslaan van uw toepassingspakketten als blok-blobs.</span><span class="sxs-lookup"><span data-stu-id="46a78-172">The Batch service uses Azure Storage to store your application packages as block blobs.</span></span> <span data-ttu-id="46a78-173">U bent [in rekening gebracht als normale] [ storage_pricing] voor de blok-blob-gegevens.</span><span class="sxs-lookup"><span data-stu-id="46a78-173">You are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="46a78-174">Moet u rekening met de grootte en het nummer van uw toepassingspakketten en verwijderen periodiek verouderde pakketten om de kosten kunt minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="46a78-174">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="46a78-175">De huidige toepassingen weergeven</span><span class="sxs-lookup"><span data-stu-id="46a78-175">View current applications</span></span>
<span data-ttu-id="46a78-176">U kunt de toepassingen in uw Batch-account op de **toepassingen** menu-item in het menu links tijdens weer te geven de **Batch-account** blade.</span><span class="sxs-lookup"><span data-stu-id="46a78-176">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="46a78-177">![Toepassingen-tegel][2]</span><span class="sxs-lookup"><span data-stu-id="46a78-177">![Applications tile][2]</span></span>

<span data-ttu-id="46a78-178">Met deze optie menu opent de **toepassingen** blade:</span><span class="sxs-lookup"><span data-stu-id="46a78-178">Selecting this menu option opens the **Applications** blade:</span></span>

<span data-ttu-id="46a78-179">![Lijst met toepassingen][3]</span><span class="sxs-lookup"><span data-stu-id="46a78-179">![List applications][3]</span></span>

<span data-ttu-id="46a78-180">De **toepassingen** blade geeft de ID van elke toepassing in uw account en de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="46a78-180">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="46a78-181">**Pakketten**: het aantal versies die zijn gekoppeld aan deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="46a78-181">**Packages**: The number of versions associated with this application.</span></span>
* <span data-ttu-id="46a78-182">**Standaardversie**: de versie van de toepassing wordt geïnstalleerd als u niet een versie aangeven wanneer u de toepassing voor een groep opgeeft.</span><span class="sxs-lookup"><span data-stu-id="46a78-182">**Default version**: The application version installed if you do not indicate a version when you specify the application for a pool.</span></span> <span data-ttu-id="46a78-183">Deze instelling is optioneel.</span><span class="sxs-lookup"><span data-stu-id="46a78-183">This setting is optional.</span></span>
* <span data-ttu-id="46a78-184">**Toestaan dat updates**: de waarde die aangeeft of het pakket updates, verwijderingen en toevoegingen zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="46a78-184">**Allow updates**: The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="46a78-185">Als deze is ingesteld op **Nee**, pakket bijwerken en verwijderen zijn uitgeschakeld voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="46a78-185">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="46a78-186">Alleen nieuwe toepassingspakketversies kunnen worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="46a78-186">Only new application package versions can be added.</span></span> <span data-ttu-id="46a78-187">De standaardwaarde is **Ja**.</span><span class="sxs-lookup"><span data-stu-id="46a78-187">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="46a78-188">Toepassingdetails weergeven</span><span class="sxs-lookup"><span data-stu-id="46a78-188">View application details</span></span>
<span data-ttu-id="46a78-189">Als de blade met de details voor een toepassing, schakelt u de toepassing in de **toepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="46a78-189">To open the blade that includes the details for an application, select the application in the **Applications** blade.</span></span>

<span data-ttu-id="46a78-190">![App-details][4]</span><span class="sxs-lookup"><span data-stu-id="46a78-190">![Application details][4]</span></span>

<span data-ttu-id="46a78-191">In de blade toepassing details kunt u de volgende instellingen configureren voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="46a78-191">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="46a78-192">**Toestaan dat updates**: opgeven of de toepassingspakketten kunnen worden bijgewerkt of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="46a78-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="46a78-193">Zie 'Werken of te verwijderen van een toepassingspakket' verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="46a78-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="46a78-194">**Standaardversie**: Geef een toepassingspakket standaard voor het implementeren van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="46a78-194">**Default version**: Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="46a78-195">**Weergavenaam**: Geef een beschrijvende naam die uw Batch-oplossing gebruiken kunt wanneer er bijvoorbeeld informatie over de toepassing weergegeven in de gebruikersinterface van een service die u voor uw klanten via Batch opgeeft.</span><span class="sxs-lookup"><span data-stu-id="46a78-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about the application, for example, in the UI of a service that you provide to your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="46a78-196">Een nieuwe toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="46a78-196">Add a new application</span></span>
<span data-ttu-id="46a78-197">Een nieuwe toepassing maken, toevoegen van een toepassingspakket en geef een nieuwe, unieke toepassing-ID.</span><span class="sxs-lookup"><span data-stu-id="46a78-197">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="46a78-198">Het eerste toepassingspakket dat u met de nieuwe toepassings-ID toevoegen wordt ook de nieuwe toepassing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46a78-198">The first application package that you add with the new application ID also creates the new application.</span></span>

<span data-ttu-id="46a78-199">Klik op **toevoegen** op de **toepassingen** blade openen de **nieuwe toepassing** blade.</span><span class="sxs-lookup"><span data-stu-id="46a78-199">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="46a78-200">![Blade voor een nieuwe toepassing in Azure-portal][5]</span><span class="sxs-lookup"><span data-stu-id="46a78-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="46a78-201">De **nieuwe toepassing** blade biedt de volgende velden om op te geven van de instellingen van uw nieuwe toepassing en het application-pakket.</span><span class="sxs-lookup"><span data-stu-id="46a78-201">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="46a78-202">**Toepassings-id**</span><span class="sxs-lookup"><span data-stu-id="46a78-202">**Application id**</span></span>

<span data-ttu-id="46a78-203">Dit veld bevat de ID van uw nieuwe toepassing, onderworpen aan de standaardregels voor validatie van Azure Batch-ID is.</span><span class="sxs-lookup"><span data-stu-id="46a78-203">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="46a78-204">De regels voor het ontwikkelen van een toepassings-ID zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="46a78-204">The rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="46a78-205">Op Windows-knooppunten, kan de ID een combinatie van alfanumerieke tekens, afbreekstreepjes en onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="46a78-205">On Windows nodes, the ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="46a78-206">Op Linux-knooppunten mogen alleen alfanumerieke tekens en onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="46a78-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="46a78-207">Kan niet meer dan 64 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="46a78-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="46a78-208">Moet uniek zijn binnen het Batch-account.</span><span class="sxs-lookup"><span data-stu-id="46a78-208">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="46a78-209">Letters behouden blijven en hoofdlettergevoelig is.</span><span class="sxs-lookup"><span data-stu-id="46a78-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="46a78-210">**Versie**</span><span class="sxs-lookup"><span data-stu-id="46a78-210">**Version**</span></span>

<span data-ttu-id="46a78-211">Dit veld geeft u de versie van het toepassingspakket dat u uploadt.</span><span class="sxs-lookup"><span data-stu-id="46a78-211">This field specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="46a78-212">Versietekenreeksen zijn onderworpen aan de volgende validatieregels:</span><span class="sxs-lookup"><span data-stu-id="46a78-212">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="46a78-213">Op Windows-knooppunten, kan de tekenreeks voor elke combinatie van alfanumerieke tekens, streepjes, onderstrepingstekens en punten bevatten.</span><span class="sxs-lookup"><span data-stu-id="46a78-213">On Windows nodes, the version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="46a78-214">Op Linux-knooppunten mag de versietekenreeks alleen alfanumerieke tekens en onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="46a78-214">On Linux nodes, the version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="46a78-215">Kan niet meer dan 64 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="46a78-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="46a78-216">Moet uniek zijn binnen de toepassing.</span><span class="sxs-lookup"><span data-stu-id="46a78-216">Must be unique within the application.</span></span>
* <span data-ttu-id="46a78-217">Letters behouden blijven en hoofdlettergevoelig zijn.</span><span class="sxs-lookup"><span data-stu-id="46a78-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="46a78-218">**Application-pakket**</span><span class="sxs-lookup"><span data-stu-id="46a78-218">**Application package**</span></span>

<span data-ttu-id="46a78-219">Dit veld geeft de ZIP-bestand dat de binaire bestanden van de toepassing bevat en de ondersteunende bestanden die nodig zijn voor de toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="46a78-219">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="46a78-220">Klik op de **selecteert u een bestand** box of het pictogram van de map te bladeren naar en selecteer een ZIP-bestand met de bestanden van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="46a78-220">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="46a78-221">Nadat u een bestand hebt geselecteerd, klikt u op **OK** om te beginnen met het uploaden naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="46a78-221">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="46a78-222">Wanneer het uploaden voltooid is, wordt de portal een melding weergegeven en sluit u de blade.</span><span class="sxs-lookup"><span data-stu-id="46a78-222">When the upload operation is complete, the portal displays a notification and closes the blade.</span></span> <span data-ttu-id="46a78-223">Deze bewerking kan enige tijd duren, afhankelijk van de grootte van het bestand dat u uploadt en de snelheid van uw netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="46a78-223">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="46a78-224">Sluit niet de **nieuwe toepassing** blade voordat het uploaden voltooid is.</span><span class="sxs-lookup"><span data-stu-id="46a78-224">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="46a78-225">In dat geval wordt het uploadproces gestopt.</span><span class="sxs-lookup"><span data-stu-id="46a78-225">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="46a78-226">Een nieuw toepassingspakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="46a78-226">Add a new application package</span></span>
<span data-ttu-id="46a78-227">Selecteer een toepassing in om een nieuwe Pakketversie voor de toepassing van een bestaande toepassing toe de **toepassingen** blade, klikt u op **pakketten**, klikt u vervolgens op **toevoegen** openen de **Toevoegen pakket** blade.</span><span class="sxs-lookup"><span data-stu-id="46a78-227">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="46a78-228">![Toepassing pakket blade toevoegen in Azure-portal][8]</span><span class="sxs-lookup"><span data-stu-id="46a78-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="46a78-229">Zoals u ziet de velden overeenkomen met die van de **nieuwe toepassing** blade, maar de **toepassings-id** selectievakje is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="46a78-229">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="46a78-230">Net als voor de nieuwe toepassing, geef de **versie** voor het nieuwe pakket, blader naar uw **toepassingspakket** ZIP-bestand en klik vervolgens op **OK** voor het uploaden van het pakket.</span><span class="sxs-lookup"><span data-stu-id="46a78-230">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="46a78-231">Bijwerken of verwijderen van een toepassingspakket</span><span class="sxs-lookup"><span data-stu-id="46a78-231">Update or delete an application package</span></span>
<span data-ttu-id="46a78-232">Als u wilt bijwerken of verwijderen van een bestaand toepassingspakket, open de blade met details voor de toepassing, klikt u op **pakketten** openen de **pakketten** blade, klikt u op de **weglatingsteken** in de rij van het toepassingspakket dat u wilt wijzigen, en selecteer de actie die u wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="46a78-232">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="46a78-233">![Bijwerken of verwijderen van pakket in Azure-portal][7]</span><span class="sxs-lookup"><span data-stu-id="46a78-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="46a78-234">**Update**</span><span class="sxs-lookup"><span data-stu-id="46a78-234">**Update**</span></span>

<span data-ttu-id="46a78-235">Wanneer u klikt op **Update**, wordt de *updatepakket* blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="46a78-235">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="46a78-236">Deze blade is vergelijkbaar met de *nieuw toepassingspakket* blade echter alleen het veld pakket is ingeschakeld, zodat u kunt het opgeven van een nieuwe ZIP-bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="46a78-236">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="46a78-237">![Blade voor update-pakket in Azure-portal][11]</span><span class="sxs-lookup"><span data-stu-id="46a78-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="46a78-238">**Verwijderen**</span><span class="sxs-lookup"><span data-stu-id="46a78-238">**Delete**</span></span>

<span data-ttu-id="46a78-239">Wanneer u klikt op **verwijderen**u wordt gevraagd om te bevestigen dat de verwijdering van de Pakketversie en Batch wordt het pakket verwijderd uit Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="46a78-239">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="46a78-240">Als u de standaardversie van een toepassing, verwijdert de **standaardversie** instelling voor de toepassing is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="46a78-240">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="46a78-241">![Toepassing verwijderen][12]</span><span class="sxs-lookup"><span data-stu-id="46a78-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="46a78-242">Toepassingen installeren op rekenknooppunten</span><span class="sxs-lookup"><span data-stu-id="46a78-242">Install applications on compute nodes</span></span>
<span data-ttu-id="46a78-243">Nu dat u met de Azure portal-toepassingspakketten beheren hebt geleerd, kunt implementeren om de rekenknooppunten en ze worden uitgevoerd met Batch-taken besproken.</span><span class="sxs-lookup"><span data-stu-id="46a78-243">Now that you've learned how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="46a78-244">Toepassingspakketten voor toepassingen installeren</span><span class="sxs-lookup"><span data-stu-id="46a78-244">Install pool application packages</span></span>
<span data-ttu-id="46a78-245">Geef een of meer toepassingspakket wilt installeren een toepassingspakket op alle rekenknooppunten in een pool, *verwijzingen* voor de pool.</span><span class="sxs-lookup"><span data-stu-id="46a78-245">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="46a78-246">De toepassingspakketten die u voor een groep van toepassingen opgeeft zijn geïnstalleerd op elk rekenknooppunt wanneer dat knooppunt aan de pool wordt toegevoegd en wanneer het knooppunt is opnieuw opgestart of hersteld met een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="46a78-246">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="46a78-247">Geef een of meer in Batch .NET [CloudPool][net_cloudpool].[ ApplicationPackageReferences] [ net_cloudpool_pkgref] wanneer u een nieuwe groep maakt of voor een bestaande toepassingen.</span><span class="sxs-lookup"><span data-stu-id="46a78-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="46a78-248">De [ApplicationPackageReference] [ net_pkgref] klasse wordt een toepassings-ID en versie te installeren op een pool van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="46a78-248">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="46a78-249">Als de implementatie van een toepassing pakket om welke reden dan ook mislukt, de Batch-service het knooppunt markeert [onbruikbaar][net_nodestate], en er zijn geen taken zijn gepland voor uitvoering op dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="46a78-249">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="46a78-250">In dit geval moet u **opnieuw** het knooppunt voor de pakketimplementatie van het opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="46a78-250">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="46a78-251">Opnieuw opstarten van het knooppunt kan ook taakplanning opnieuw op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="46a78-251">Restarting the node also enables task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="46a78-252">Taak toepassingspakketten installeren</span><span class="sxs-lookup"><span data-stu-id="46a78-252">Install task application packages</span></span>
<span data-ttu-id="46a78-253">Net als bij een groep kunt u opgeven toepassingspakket *verwijzingen* voor een taak.</span><span class="sxs-lookup"><span data-stu-id="46a78-253">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="46a78-254">Wanneer een taak is gepland op een knooppunt worden uitgevoerd, wordt het pakket gedownload en uitgepakt vlak voordat de opdrachtregel van de taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="46a78-254">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="46a78-255">Als een opgegeven pakket en -versie is al geïnstalleerd op het knooppunt, wordt het pakket wordt niet gedownload en wordt het bestaande pakket wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="46a78-255">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="46a78-256">Configureren van de taak voor het installeren van een toepassingspakket taak [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] eigenschap:</span><span class="sxs-lookup"><span data-stu-id="46a78-256">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-the-installed-applications"></a><span data-ttu-id="46a78-257">De geïnstalleerde toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="46a78-257">Execute the installed applications</span></span>
<span data-ttu-id="46a78-258">De pakketten die u hebt opgegeven voor een groep of de taak worden gedownload en uitgepakt naar de map met een naam in de `AZ_BATCH_ROOT_DIR` van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="46a78-258">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="46a78-259">Batch maakt ook een omgevingsvariabele die het pad naar de map met de naam bevat.</span><span class="sxs-lookup"><span data-stu-id="46a78-259">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="46a78-260">Uw taak opdrachtregels gebruikt deze omgevingsvariabele bij verwijzingen naar de toepassing op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="46a78-260">Your task command lines use this environment variable when referencing the application on the node.</span></span> 

<span data-ttu-id="46a78-261">De variabele is op Windows-knooppunten in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="46a78-261">On Windows nodes, the variable is in the following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="46a78-262">De indeling is enigszins verschillen op Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="46a78-262">On Linux nodes, the format is slightly different.</span></span> <span data-ttu-id="46a78-263">Punten (.), afbreekstreepjes (-) en hekjes (#) worden samengevoegd tot onderstrepingstekens in de omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="46a78-263">Periods (.), hypens (-) and number signs (#) are flattened to underscores in the environment variable.</span></span> <span data-ttu-id="46a78-264">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="46a78-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="46a78-265">`APPLICATIONID`en `version` zijn waarden die overeenkomen met de toepassingen en pakketten versie die u hebt opgegeven voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="46a78-265">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="46a78-266">Bijvoorbeeld, als u die versie 2.7 van toepassing opgegeven *blender* moet worden geïnstalleerd op Windows-knooppunten zou uw taak opdrachtregels deze omgevingsvariabele gebruiken voor toegang tot de bestanden:</span><span class="sxs-lookup"><span data-stu-id="46a78-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable to access its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="46a78-267">Geef op Linux-knooppunten, de omgevingsvariabele in deze indeling:</span><span class="sxs-lookup"><span data-stu-id="46a78-267">On Linux nodes, specify the environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="46a78-268">Wanneer u toepassingspakketten uploadt, kunt u een standaardversie voor het implementeren van uw rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="46a78-268">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="46a78-269">Als u een standaardversie voor een toepassing hebt opgegeven, kunt u het versieachtervoegsel weglaten wanneer u verwijst naar de toepassing.</span><span class="sxs-lookup"><span data-stu-id="46a78-269">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="46a78-270">Geef de versie van de toepassing standaard in de Azure-portal op de blade toepassingen, zoals wordt weergegeven in [uploaden en beheren van toepassingen](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="46a78-270">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="46a78-271">Als u '2.7' instellen als de standaardversie voor toepassing bijvoorbeeld *blender*, en uw taken verwijzen naar de volgende omgevingsvariabele, en vervolgens uw Windows-knooppunten versie 2.7 wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="46a78-271">For example, if you set "2.7" as the default version for application *blender*, and your tasks reference the following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="46a78-272">Het volgende codefragment toont een voorbeeld van de taak vanaf de opdrachtregel die wordt gestart van de standaardversie van de *blender* toepassing:</span><span class="sxs-lookup"><span data-stu-id="46a78-272">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="46a78-273">Zie [omgevingsinstellingen voor taken](batch-api-basics.md#environment-settings-for-tasks) in de [overzicht Batch-functies](batch-api-basics.md) voor meer informatie over omgevingsinstellingen compute-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="46a78-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="46a78-274">De toepassingspakketten van een groep bijwerken</span><span class="sxs-lookup"><span data-stu-id="46a78-274">Update a pool's application packages</span></span>
<span data-ttu-id="46a78-275">Als een bestaande pool al is geconfigureerd met een pakket, kunt u een nieuw pakket voor de pool opgeven.</span><span class="sxs-lookup"><span data-stu-id="46a78-275">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="46a78-276">Als u een nieuw pakket verwijzing voor een groep, de volgende van toepassing opgeven:</span><span class="sxs-lookup"><span data-stu-id="46a78-276">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="46a78-277">De Batch-service installeert het zojuist opgegeven pakket op alle nieuwe knooppunten die aan de pool worden toegevoegd en op een bestaande knooppunt dat is opnieuw opgestart of hersteld met een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="46a78-277">The Batch service installs the newly specified package on all new nodes that join the pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="46a78-278">COMPUTE knooppunten die zich al in de groep tijdens het bijwerken van het pakket verwijst naar het nieuwe toepassingspakket niet automatisch installeert.</span><span class="sxs-lookup"><span data-stu-id="46a78-278">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="46a78-279">Deze berekenen knooppunten moeten worden opgestart of hersteld met een installatiekopie voor het ontvangen van het nieuwe pakket.</span><span class="sxs-lookup"><span data-stu-id="46a78-279">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="46a78-280">Wanneer een nieuw pakket wordt geïmplementeerd, weerspiegelen de gemaakte omgevingsvariabelen in de nieuwe toepassing pakket verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="46a78-280">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="46a78-281">In dit voorbeeld is de bestaande toepassingen versie 2.7 van de *blender* toepassing geconfigureerd als een van de [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="46a78-281">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="46a78-282">Voor het bijwerken van de pool knooppunten met versie 2.76b, Geef een nieuwe [ApplicationPackageReference] [ net_pkgref] met de nieuwe versie en de wijziging doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="46a78-282">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="46a78-283">Nu dat de nieuwe versie is geconfigureerd, de Batch-service in een versie 2.76b geïnstalleerd *nieuwe* knooppunt dat aan de pool wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="46a78-283">Now that the new version has been configured, the Batch service installs version 2.76b to any *new* node that joins the pool.</span></span> <span data-ttu-id="46a78-284">2.76b installeren op de knooppunten die *al* starten in de groep of deze installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="46a78-284">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="46a78-285">Houd er rekening mee dat opnieuw opgestart knooppunten de bestanden van eerdere implementaties van het pakket behoudt.</span><span class="sxs-lookup"><span data-stu-id="46a78-285">Note that rebooted nodes retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="46a78-286">Lijst van de toepassingen in een Batch-account</span><span class="sxs-lookup"><span data-stu-id="46a78-286">List the applications in a Batch account</span></span>
<span data-ttu-id="46a78-287">U kunt de toepassingen en hun pakketten in een Batch-account weergeven met behulp van de [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] methode.</span><span class="sxs-lookup"><span data-stu-id="46a78-287">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="46a78-288">Inpakken</span><span class="sxs-lookup"><span data-stu-id="46a78-288">Wrap up</span></span>
<span data-ttu-id="46a78-289">Met toepassingspakketten kunt u uw klanten, selecteer de toepassingen voor hun taken en geef de exacte versie moet worden gebruikt bij het verwerken van taken met de service Batch is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="46a78-289">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="46a78-290">U kunt ook de mogelijkheid voor uw klanten om te uploaden en bijhouden van hun eigen toepassingen in uw service opgeven.</span><span class="sxs-lookup"><span data-stu-id="46a78-290">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46a78-291">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46a78-291">Next steps</span></span>
* <span data-ttu-id="46a78-292">De [Batch REST-API] [ api_rest] biedt ook ondersteuning voor gebruik met toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="46a78-292">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="46a78-293">Zie bijvoorbeeld de [applicationPackageReferences] [ rest_add_pool_with_packages] -element in [een groep toevoegen aan een account] [ rest_add_pool] voor informatie over het opgeven pakketten installeren met behulp van de REST-API.</span><span class="sxs-lookup"><span data-stu-id="46a78-293">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="46a78-294">Zie [toepassingen] [ rest_applications] voor meer informatie over het verkrijgen van informatie over toepassingen met behulp van de Batch REST-API.</span><span class="sxs-lookup"><span data-stu-id="46a78-294">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="46a78-295">Meer informatie over hoe u programmatisch [beheren van Azure Batch-accounts en quota's met Batch Management .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="46a78-295">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="46a78-296">De [Batch Management .NET][api_net_mgmt] bibliotheek account maken en verwijderen-functies voor uw Batch-toepassing of service kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="46a78-296">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Toepassingspakketten op hoog niveau diagram"
[2]: ./media/batch-application-packages/app_pkg_02.png "De tegel toepassingen in Azure-portal"
[3]: ./media/batch-application-packages/app_pkg_03.png "Blade toepassingen in Azure-portal"
[4]: ./media/batch-application-packages/app_pkg_04.png "Toepassing details blade in Azure-portal"
[5]: ./media/batch-application-packages/app_pkg_05.png "Blade voor een nieuwe toepassing in Azure-portal"
[7]: ./media/batch-application-packages/app_pkg_07.png "Bijwerken of verwijderen van pakketten vervolgkeuzelijst in Azure-portal"
[8]: ./media/batch-application-packages/app_pkg_08.png "Nieuwe toepassing pakket blade in Azure-portal"
[9]: ./media/batch-application-packages/app_pkg_09.png "Er is geen gekoppelde Opslagwaarschuwing voor account"
[10]: ./media/batch-application-packages/app_pkg_10.png "Kies de blade opslagaccount in Azure-portal"
[11]: ./media/batch-application-packages/app_pkg_11.png "Blade voor update-pakket in Azure-portal"
[12]: ./media/batch-application-packages/app_pkg_12.png "Dialoogvenster voor bevestiging pakket maken in Azure-portal verwijderen"
