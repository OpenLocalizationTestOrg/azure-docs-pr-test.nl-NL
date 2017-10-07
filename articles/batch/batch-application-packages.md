---
title: toepassingspakketten aaaInstall op rekenknooppunten - Azure Batch | Microsoft Docs
description: Gebruik hello-pakketten toepassingsfunctie van Azure Batch tooeasily beheren meerdere toepassingen en versies voor de installatie van Batch-rekenknooppunten.
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
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a><span data-ttu-id="fafae-103">Implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="fafae-103">Deploy applications toocompute nodes with Batch application packages</span></span>

<span data-ttu-id="fafae-104">Hallo toepassingsfunctie pakketten van Azure Batch maakt eenvoudig beheer van toepassingen van de taak en hun implementatie toohello rekenknooppunten in uw groep.</span><span class="sxs-lookup"><span data-stu-id="fafae-104">hello application packages feature of Azure Batch provides easy management of task applications and their deployment toohello compute nodes in your pool.</span></span> <span data-ttu-id="fafae-105">U kunt met toepassingspakketten kunt uploaden en beheren van meerdere versies van de taken worden uitgevoerd, met inbegrip van hun ondersteunende bestanden Hallo-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="fafae-105">With application packages, you can upload and manage multiple versions of hello applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="fafae-106">Vervolgens kunt u automatisch implementeren een of meer van deze toepassingen toohello rekenknooppunten in uw groep.</span><span class="sxs-lookup"><span data-stu-id="fafae-106">You can then automatically deploy one or more of these applications toohello compute nodes in your pool.</span></span>

<span data-ttu-id="fafae-107">In dit artikel leert u hoe tooupload en toepassingspakketten in hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="fafae-107">In this article, you will learn how tooupload and manage application packages in hello Azure portal.</span></span> <span data-ttu-id="fafae-108">Vervolgens leert u hoe tooinstall ze op een groep rekenknooppunten met Hallo [Batch .NET] [ api_net] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="fafae-108">You will then learn how tooinstall them on a pool's compute nodes with hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="fafae-109">Toepassingspakketten worden ondersteund in alle Batch-pools die na 5 juli 2017 zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fafae-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="fafae-110">Ze worden ondersteund in de Batch-pools tussen 10 maart 2016 en 5 juli 2017 alleen gemaakt als Hallo-groep is gemaakt met behulp van de configuratie van een Service in de Cloud.</span><span class="sxs-lookup"><span data-stu-id="fafae-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="fafae-111">Batch-pools gemaakt voorafgaande too10 maart 2016 bieden geen ondersteuning voor toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="fafae-111">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="fafae-112">Hallo-API's voor het maken en beheren van toepassingspakketten deel uitmaken van Hallo [Batch Management .NET] [[api_net_mgmt]] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="fafae-112">hello APIs for creating and managing application packages are part of hello [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="fafae-113">Hallo-API's voor toepassingspakketten installeren op een rekenknooppunt deel uitmaken van Hallo [Batch .NET] [ api_net] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="fafae-113">hello APIs for installing application packages on a compute node are part of hello [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="fafae-114">hello-pakketten toepassingsfunctie hier beschreven vervangt Hallo Batch Apps-functie die beschikbaar zijn in eerdere versies van het Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="fafae-114">hello application packages feature described here supersedes hello Batch Apps feature available in previous versions of hello service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="fafae-115">Vereisten voor Application-pakket</span><span class="sxs-lookup"><span data-stu-id="fafae-115">Application package requirements</span></span>
<span data-ttu-id="fafae-116">toepassingspakketten toouse, moet u te[een Azure Storage-account koppelen](#link-a-storage-account) tooyour Batch-account.</span><span class="sxs-lookup"><span data-stu-id="fafae-116">toouse application packages, you need too[link an Azure Storage account](#link-a-storage-account) tooyour Batch account.</span></span>

<span data-ttu-id="fafae-117">Deze functie is geïntroduceerd [Batch REST-API] [ api_rest] versie 2015-12-01.2.2 en de bijbehorende van Hallo [Batch .NET] [ api_net] library-versie 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="fafae-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and hello corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="fafae-118">Het is raadzaam de nieuwste API-versie Hallo altijd te gebruiken bij het werken met de Batch.</span><span class="sxs-lookup"><span data-stu-id="fafae-118">We recommend that you always use hello latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="fafae-119">Toepassingspakketten worden ondersteund in alle Batch-pools die na 5 juli 2017 zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fafae-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="fafae-120">Ze worden ondersteund in de Batch-pools tussen 10 maart 2016 en 5 juli 2017 alleen gemaakt als Hallo-groep is gemaakt met behulp van de configuratie van een Service in de Cloud.</span><span class="sxs-lookup"><span data-stu-id="fafae-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="fafae-121">Batch-pools gemaakt voorafgaande too10 maart 2016 bieden geen ondersteuning voor toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="fafae-121">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="fafae-122">Over de toepassingen en toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="fafae-122">About applications and application packages</span></span>
<span data-ttu-id="fafae-123">In Azure Batch een *toepassing* tooa set samengestelde binaire bestanden die automatisch gedownloade toohello rekenknooppunten in uw pool worden kunnen verwijst.</span><span class="sxs-lookup"><span data-stu-id="fafae-123">Within Azure Batch, an *application* refers tooa set of versioned binaries that can be automatically downloaded toohello compute nodes in your pool.</span></span> <span data-ttu-id="fafae-124">Een *toepassingspakket* verwijst tooa *specifieke set* van deze binaire bestanden en vertegenwoordigt een gegeven *versie* van Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fafae-124">An *application package* refers tooa *specific set* of those binaries and represents a given *version* of hello application.</span></span>

<span data-ttu-id="fafae-125">![Op hoog niveau diagram van toepassingen en toepassingspakketten][1]</span><span class="sxs-lookup"><span data-stu-id="fafae-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="fafae-126">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="fafae-126">Applications</span></span>
<span data-ttu-id="fafae-127">Een toepassing in Batch bevat een of meer toepassingen, pakketten en configuratieopties voor de toepassing hello geeft.</span><span class="sxs-lookup"><span data-stu-id="fafae-127">An application in Batch contains one or more application packages and specifies configuration options for hello application.</span></span> <span data-ttu-id="fafae-128">Een toepassing kan bijvoorbeeld Hallo standaard toepassing pakket versie tooinstall opgeven op de rekenknooppunten en of de pakketten kunnen worden bijgewerkt of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fafae-128">For example, an application can specify hello default application package version tooinstall on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="fafae-129">Toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="fafae-129">Application packages</span></span>
<span data-ttu-id="fafae-130">Een toepassingspakket is een ZIP-bestand met Hallo toepassing binaire bestanden en ondersteunende bestanden die vereist voor uw taken toorun Hallo-toepassing zijn.</span><span class="sxs-lookup"><span data-stu-id="fafae-130">An application package is a .zip file that contains hello application binaries and supporting files that are required for your tasks toorun hello application.</span></span> <span data-ttu-id="fafae-131">Elke toepassingspakket vertegenwoordigt een specifieke versie van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="fafae-131">Each application package represents a specific version of hello application.</span></span>

<span data-ttu-id="fafae-132">U kunt toepassingspakketten op Hallo van toepassingen en taak niveaus opgeven.</span><span class="sxs-lookup"><span data-stu-id="fafae-132">You can specify application packages at hello pool and task levels.</span></span> <span data-ttu-id="fafae-133">U kunt een of meer van deze pakketten en (optioneel) een versie opgeven wanneer u een groep of een taak maakt.</span><span class="sxs-lookup"><span data-stu-id="fafae-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="fafae-134">**Toepassingspakketten groep** te worden geïmplementeerd*elke* knooppunt in de pool Hallo.</span><span class="sxs-lookup"><span data-stu-id="fafae-134">**Pool application packages** are deployed too*every* node in hello pool.</span></span> <span data-ttu-id="fafae-135">Toepassingen worden geïmplementeerd als een knooppunt aan een pool wordt toegevoegd en wanneer deze wordt opgestart of hersteld met een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="fafae-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="fafae-136">Toepassingspakketten voor toepassingen zijn geschikt wanneer alle knooppunten in een pool van een taak taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fafae-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="fafae-137">Een of meer toepassingspakketten kunt u opgeven wanneer u een pool maakt en u kunt toevoegen of bijwerken van een bestaande pool-pakketten.</span><span class="sxs-lookup"><span data-stu-id="fafae-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="fafae-138">Als u een bestaande pool toepassingspakketten bijwerkt, moet u de knooppunten tooinstall Hallo nieuw pakket opnieuw.</span><span class="sxs-lookup"><span data-stu-id="fafae-138">If you update an existing pool's application packages, you must restart its nodes tooinstall hello new package.</span></span>
* <span data-ttu-id="fafae-139">**Taak toepassingspakketten** alleen tooa rekenknooppunt gepland toorun een taak, net voordat de opdrachtregel van Hallo taak uitgevoerd worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="fafae-139">**Task application packages** are deployed only tooa compute node scheduled toorun a task, just before running hello task's command line.</span></span> <span data-ttu-id="fafae-140">Als Hallo opgegeven toepassingspakket en versie is al op Hallo knooppunt niet opnieuw gedistribueerd en Hallo bestaand pakket wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fafae-140">If hello specified application package and version is already on hello node, it is not redeployed and hello existing package is used.</span></span>
  
    <span data-ttu-id="fafae-141">Taak toepassingspakketten zijn handig in gedeelde groep omgevingen, waarbij verschillende taken worden uitgevoerd op één groep en het Hallo-groep is niet verwijderd wanneer een taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="fafae-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and hello pool is not deleted when a job is completed.</span></span> <span data-ttu-id="fafae-142">Als uw project minder taken dan knooppunten in de groep hello heeft, minimaliseren taak toepassingspakketten gegevensoverdracht sinds de toepassing is geïmplementeerd alleen toohello knooppunten die taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fafae-142">If your job has fewer tasks than nodes in hello pool, task application packages can minimize data transfer since your application is deployed only toohello nodes that run tasks.</span></span>
  
    <span data-ttu-id="fafae-143">Andere scenario's waarin u van de taak toepassingspakketten profiteren kunnen zijn taken met een grote toepassing, maar voor alleen enkele taken.</span><span class="sxs-lookup"><span data-stu-id="fafae-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="fafae-144">Een vooraf verwerken fase of een merge-taak, waarbij de toepassing vooraf verwerken of samenvoegen Hallo zware is, kan bijvoorbeeld profiteren van het gebruik van de taak toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="fafae-144">For example, a pre-processing stage or a merge task, where hello pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fafae-145">Er gelden beperkingen op Hallo aantal toepassingen en toepassingspakketten in een Batch-account en op Hallo maximale pakketgrootte.</span><span class="sxs-lookup"><span data-stu-id="fafae-145">There are restrictions on hello number of applications and application packages within a Batch account and on hello maximum application package size.</span></span> <span data-ttu-id="fafae-146">Zie [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md) voor meer informatie over deze limieten.</span><span class="sxs-lookup"><span data-stu-id="fafae-146">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="fafae-147">Voordelen van toepassingspakketten</span><span class="sxs-lookup"><span data-stu-id="fafae-147">Benefits of application packages</span></span>
<span data-ttu-id="fafae-148">Toepassingspakketten kunnen vereenvoudigen Hallo-code in uw Batch-oplossing en de lagere Hallo overhead vereist toomanage Hallo toepassingen die de taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fafae-148">Application packages can simplify hello code in your Batch solution and lower hello overhead required toomanage hello applications that your tasks run.</span></span>

<span data-ttu-id="fafae-149">Met toepassingspakketten kunt uw pool begintaak beschikt niet over toospecify een lange lijst met afzonderlijke resource bestanden tooinstall op Hallo knooppunten.</span><span class="sxs-lookup"><span data-stu-id="fafae-149">With application packages, your pool's start task doesn't have toospecify a long list of individual resource files tooinstall on hello nodes.</span></span> <span data-ttu-id="fafae-150">U hebt geen toomanually beheer van meerdere versies van uw toepassingsbestanden in Azure Storage of op de knooppunten.</span><span class="sxs-lookup"><span data-stu-id="fafae-150">You don't have toomanually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="fafae-151">En u hoeft niet tooworry over het genereren van [SAS-URL's](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello-bestanden in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="fafae-151">And, you don't need tooworry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello files in your Storage account.</span></span> <span data-ttu-id="fafae-152">Batch-werkt op de achtergrond Hallo met Azure Storage toostore toepassingspakketten en deze toocompute knooppunten te implementeren.</span><span class="sxs-lookup"><span data-stu-id="fafae-152">Batch works in hello background with Azure Storage toostore application packages and deploy them toocompute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="fafae-153">Hallo totale grootte van een begintaak moet kleiner zijn dan of gelijk too32768 tekens, inclusief bronbestanden en omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="fafae-153">hello total size of a start task must be less than or equal too32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="fafae-154">Als uw begintaak deze limiet overschrijdt, is met behulp van toepassingspakketten een andere optie.</span><span class="sxs-lookup"><span data-stu-id="fafae-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="fafae-155">U kunt ook een ZIP-archief met de resource-bestanden maken, uploaden als een tooAzure blob Storage en pak deze vervolgens vanaf de opdrachtregel Hallo van de begintaak.</span><span class="sxs-lookup"><span data-stu-id="fafae-155">You can also create a zipped archive containing your resource files, upload it as a blob tooAzure Storage, and then unzip it from hello command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="fafae-156">Uploaden en beheren van toepassingen</span><span class="sxs-lookup"><span data-stu-id="fafae-156">Upload and manage applications</span></span>
<span data-ttu-id="fafae-157">U kunt Hallo [Azure-portal] [ portal] of Hallo [Batch Management .NET](batch-management-dotnet.md) bibliotheek toomanage Hallo-toepassingspakketten in uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="fafae-157">You can use hello [Azure portal][portal] or hello [Batch Management .NET](batch-management-dotnet.md) library toomanage hello application packages in your Batch account.</span></span> <span data-ttu-id="fafae-158">In Hallo naast enkele secties, laten we eerst zien hoe toolink een opslagaccount worden besproken toe te voegen toepassingen en pakketten en het beheer ervan met Hallo portal.</span><span class="sxs-lookup"><span data-stu-id="fafae-158">In hello next few sections, we first show how toolink a Storage account, then discuss adding applications and packages and managing them with hello portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="fafae-159">Storage-account koppelen</span><span class="sxs-lookup"><span data-stu-id="fafae-159">Link a Storage account</span></span>
<span data-ttu-id="fafae-160">toepassingspakketten toouse, moet u eerst een Azure Storage-account tooyour Batch-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="fafae-160">toouse application packages, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="fafae-161">Als u een opslagaccount nog niet hebt geconfigureerd, hello Azure-portal geeft een waarschuwing Hallo eerste keer dat u op Hallo **toepassingen** -tegel in Hallo **Batch-account** blade.</span><span class="sxs-lookup"><span data-stu-id="fafae-161">If you have not yet configured a Storage account, hello Azure portal displays a warning hello first time you click hello **Applications** tile in hello **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fafae-162">Batch ondersteunt momenteel *alleen* hello **algemeen** opslagaccounttype zoals beschreven in stap 5, [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)in [over Azure Storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="fafae-162">Batch currently supports *only* hello **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="fafae-163">Als u een Azure Storage-account tooyour Batch-account koppelt, koppelt *alleen* een **algemeen** storage-account.</span><span class="sxs-lookup"><span data-stu-id="fafae-163">When you link an Azure Storage account tooyour Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="fafae-164">!['Er is geen opslagaccount geconfigureerd' waarschuwing in Azure-portal][9]</span><span class="sxs-lookup"><span data-stu-id="fafae-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="fafae-165">Hallo gekoppelde Batch-service gebruikt Hallo Storage-account toostore uw toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="fafae-165">hello Batch service uses hello associated Storage account toostore your application packages.</span></span> <span data-ttu-id="fafae-166">Nadat u hebt twee accounts Hallo gekoppeld, kunt Batch hello-pakketten die zijn opgeslagen in tooyour rekenknooppunten voor Hallo gekoppelde Storage-account automatisch implementeren.</span><span class="sxs-lookup"><span data-stu-id="fafae-166">After you've linked hello two accounts, Batch can automatically deploy hello packages stored in hello linked Storage account tooyour compute nodes.</span></span> <span data-ttu-id="fafae-167">toolink een Storage account tooyour Batch-account, klikt u op **instellingen voor de opslag** op Hallo **waarschuwing** blade en klik vervolgens op **Opslagaccount** op Hallo **Opslagaccount** blade.</span><span class="sxs-lookup"><span data-stu-id="fafae-167">toolink a Storage account tooyour Batch account, click **Storage account settings** on hello **Warning** blade, and then click **Storage Account** on hello **Storage Account** blade.</span></span>

<span data-ttu-id="fafae-168">![Kies de blade opslagaccount in Azure-portal][10]</span><span class="sxs-lookup"><span data-stu-id="fafae-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="fafae-169">Het is raadzaam dat u een opslagaccount maken *specifiek* voor gebruik met uw Batch-account en selecteert u deze hier.</span><span class="sxs-lookup"><span data-stu-id="fafae-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="fafae-170">Voor meer informatie over hoe u een opslagaccount toocreate Zie 'Een opslagaccount maken' in [over Azure Storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="fafae-170">For details about how toocreate a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="fafae-171">Nadat u een opslagaccount hebt gemaakt, kunt u vervolgens deze koppelen tooyour Batch-account met behulp van Hallo **Opslagaccount** blade.</span><span class="sxs-lookup"><span data-stu-id="fafae-171">After you've created a Storage account, you can then link it tooyour Batch account by using hello **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="fafae-172">Hallo Batch-service gebruikt Azure Storage toostore uw toepassingspakketten als blok-blobs.</span><span class="sxs-lookup"><span data-stu-id="fafae-172">hello Batch service uses Azure Storage toostore your application packages as block blobs.</span></span> <span data-ttu-id="fafae-173">U bent [in rekening gebracht als normale] [ storage_pricing] voor Hallo blok-blob-gegevens.</span><span class="sxs-lookup"><span data-stu-id="fafae-173">You are [charged as normal][storage_pricing] for hello block blob data.</span></span> <span data-ttu-id="fafae-174">Ervoor tooconsider Hallo grootte en het aantal van uw toepassingspakketten zijn en verwijderen periodiek verouderde pakketten toominimize kosten.</span><span class="sxs-lookup"><span data-stu-id="fafae-174">Be sure tooconsider hello size and number of your application packages, and periodically remove deprecated packages toominimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="fafae-175">De huidige toepassingen weergeven</span><span class="sxs-lookup"><span data-stu-id="fafae-175">View current applications</span></span>
<span data-ttu-id="fafae-176">tooview hello toepassingen in uw Batch-account, klikt u op Hallo **toepassingen** menu-item in het menu aan de linkerkant Hallo terwijl u bekijkt hello **Batch-account** blade.</span><span class="sxs-lookup"><span data-stu-id="fafae-176">tooview hello applications in your Batch account, click hello **Applications** menu item in hello left menu while viewing hello **Batch account** blade.</span></span>

<span data-ttu-id="fafae-177">![Toepassingen-tegel][2]</span><span class="sxs-lookup"><span data-stu-id="fafae-177">![Applications tile][2]</span></span>

<span data-ttu-id="fafae-178">Met deze optie menu opent Hallo **toepassingen** blade:</span><span class="sxs-lookup"><span data-stu-id="fafae-178">Selecting this menu option opens hello **Applications** blade:</span></span>

<span data-ttu-id="fafae-179">![Lijst met toepassingen][3]</span><span class="sxs-lookup"><span data-stu-id="fafae-179">![List applications][3]</span></span>

<span data-ttu-id="fafae-180">Hallo **toepassingen** blade geeft Hallo ID van elke toepassing in uw account en Hallo van de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="fafae-180">hello **Applications** blade displays hello ID of each application in your account and hello following properties:</span></span>

* <span data-ttu-id="fafae-181">**Pakketten**: Hallo aantal versies die zijn gekoppeld aan deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="fafae-181">**Packages**: hello number of versions associated with this application.</span></span>
* <span data-ttu-id="fafae-182">**Standaardversie**: Hallo toepassingsversie geïnstalleerd als u niet een versie aangeven wanneer u Hallo-toepassing voor een groep opgeeft.</span><span class="sxs-lookup"><span data-stu-id="fafae-182">**Default version**: hello application version installed if you do not indicate a version when you specify hello application for a pool.</span></span> <span data-ttu-id="fafae-183">Deze instelling is optioneel.</span><span class="sxs-lookup"><span data-stu-id="fafae-183">This setting is optional.</span></span>
* <span data-ttu-id="fafae-184">**Toestaan dat updates**: Hallo-waarde die aangeeft of het pakket updates, verwijderingen en toevoegingen zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="fafae-184">**Allow updates**: hello value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="fafae-185">Als dit te is ingesteld**Nee**, pakket bijwerken en verwijderen voor de toepassing hello zijn uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fafae-185">If this is set too**No**, package updates and deletions are disabled for hello application.</span></span> <span data-ttu-id="fafae-186">Alleen nieuwe toepassingspakketversies kunnen worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="fafae-186">Only new application package versions can be added.</span></span> <span data-ttu-id="fafae-187">Hallo standaardwaarde is **Ja**.</span><span class="sxs-lookup"><span data-stu-id="fafae-187">hello default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="fafae-188">Toepassingdetails weergeven</span><span class="sxs-lookup"><span data-stu-id="fafae-188">View application details</span></span>
<span data-ttu-id="fafae-189">tooopen hello blade met details voor een toepassing, selecteer Hallo-toepassing hello in Hallo **toepassingen** blade.</span><span class="sxs-lookup"><span data-stu-id="fafae-189">tooopen hello blade that includes hello details for an application, select hello application in hello **Applications** blade.</span></span>

<span data-ttu-id="fafae-190">![App-details][4]</span><span class="sxs-lookup"><span data-stu-id="fafae-190">![Application details][4]</span></span>

<span data-ttu-id="fafae-191">Hallo toepassing details blade kunt u de volgende instellingen voor uw toepassing hello configureren.</span><span class="sxs-lookup"><span data-stu-id="fafae-191">In hello application details blade, you can configure hello following settings for your application.</span></span>

* <span data-ttu-id="fafae-192">**Toestaan dat updates**: opgeven of de toepassingspakketten kunnen worden bijgewerkt of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fafae-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="fafae-193">Zie 'Werken of te verwijderen van een toepassingspakket' verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="fafae-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="fafae-194">**Standaardversie**: een standaard application-pakket toodeploy toocompute-knooppunten opgeven.</span><span class="sxs-lookup"><span data-stu-id="fafae-194">**Default version**: Specify a default application package toodeploy toocompute nodes.</span></span>
* <span data-ttu-id="fafae-195">**Weergavenaam**: Geef een beschrijvende naam die uw oplossing kunt gebruiken bij deze geeft informatie weer over toepassing hello, bijvoorbeeld in de gebruikersinterface van een service die u opgeeft dat klanten via Batch tooyour Hallo Batch.</span><span class="sxs-lookup"><span data-stu-id="fafae-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about hello application, for example, in hello UI of a service that you provide tooyour customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="fafae-196">Een nieuwe toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="fafae-196">Add a new application</span></span>
<span data-ttu-id="fafae-197">toocreate een nieuwe toepassing toevoegen van een toepassingspakket en geef een nieuwe, unieke toepassing-ID.</span><span class="sxs-lookup"><span data-stu-id="fafae-197">toocreate a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="fafae-198">Hallo eerste toepassingspakket dat u met de nieuwe toepassings-ID Hallo toevoegen maakt ook een nieuwe toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="fafae-198">hello first application package that you add with hello new application ID also creates hello new application.</span></span>

<span data-ttu-id="fafae-199">Klik op **toevoegen** op Hallo **toepassingen** blade tooopen hello **nieuwe toepassing** blade.</span><span class="sxs-lookup"><span data-stu-id="fafae-199">Click **Add** on hello **Applications** blade tooopen hello **New application** blade.</span></span>

<span data-ttu-id="fafae-200">![Blade voor een nieuwe toepassing in Azure-portal][5]</span><span class="sxs-lookup"><span data-stu-id="fafae-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="fafae-201">Hallo **nieuwe toepassing** blade biedt de volgende Hallo velden toospecify Hallo-instellingen van uw nieuwe toepassing en het application-pakket.</span><span class="sxs-lookup"><span data-stu-id="fafae-201">hello **New application** blade provides hello following fields toospecify hello settings of your new application and application package.</span></span>

<span data-ttu-id="fafae-202">**Toepassings-id**</span><span class="sxs-lookup"><span data-stu-id="fafae-202">**Application id**</span></span>

<span data-ttu-id="fafae-203">Dit veld bevat Hallo-ID van uw nieuwe toepassing, onderwerp toohello standaard Azure Batch-ID-validatieregels.</span><span class="sxs-lookup"><span data-stu-id="fafae-203">This field specifies hello ID of your new application, which is subject toohello standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="fafae-204">Hallo-regels voor het ontwikkelen van een toepassings-ID zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="fafae-204">hello rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="fafae-205">Op Windows-knooppunten kan Hallo-ID een combinatie van alfanumerieke tekens, afbreekstreepjes en onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="fafae-205">On Windows nodes, hello ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="fafae-206">Op Linux-knooppunten mogen alleen alfanumerieke tekens en onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="fafae-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="fafae-207">Kan niet meer dan 64 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="fafae-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="fafae-208">Moet uniek zijn binnen Hallo Batch-account.</span><span class="sxs-lookup"><span data-stu-id="fafae-208">Must be unique within hello Batch account.</span></span>
* <span data-ttu-id="fafae-209">Letters behouden blijven en hoofdlettergevoelig is.</span><span class="sxs-lookup"><span data-stu-id="fafae-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="fafae-210">**Versie**</span><span class="sxs-lookup"><span data-stu-id="fafae-210">**Version**</span></span>

<span data-ttu-id="fafae-211">Dit veld geeft Hallo-versie van Hallo-toepassingspakket die wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="fafae-211">This field specifies hello version of hello application package you are uploading.</span></span> <span data-ttu-id="fafae-212">Versietekenreeksen zijn onderwerp toohello validatieregels te volgen:</span><span class="sxs-lookup"><span data-stu-id="fafae-212">Version strings are subject toohello following validation rules:</span></span>

* <span data-ttu-id="fafae-213">Op Windows-knooppunten kan Hallo versietekenreeks een combinatie van alfanumerieke tekens, streepjes, onderstrepingstekens en punten bevatten.</span><span class="sxs-lookup"><span data-stu-id="fafae-213">On Windows nodes, hello version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="fafae-214">Op Linux-knooppunten mag Hallo versietekenreeks alleen alfanumerieke tekens en onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="fafae-214">On Linux nodes, hello version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="fafae-215">Kan niet meer dan 64 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="fafae-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="fafae-216">Moet uniek zijn binnen het Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fafae-216">Must be unique within hello application.</span></span>
* <span data-ttu-id="fafae-217">Letters behouden blijven en hoofdlettergevoelig zijn.</span><span class="sxs-lookup"><span data-stu-id="fafae-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="fafae-218">**Application-pakket**</span><span class="sxs-lookup"><span data-stu-id="fafae-218">**Application package**</span></span>

<span data-ttu-id="fafae-219">Dit veld geeft Hallo ZIP-bestand met binaire waarden Hallo van toepassingen en ondersteunende bestanden die vereist tooexecute Hallo-toepassing zijn.</span><span class="sxs-lookup"><span data-stu-id="fafae-219">This field specifies hello .zip file that contains hello application binaries and supporting files that are required tooexecute hello application.</span></span> <span data-ttu-id="fafae-220">Klik op Hallo **selecteert u een bestand** box of Hallo map pictogram toobrowse tooand Selecteer een ZIP-bestand met de bestanden van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="fafae-220">Click hello **Select a file** box or hello folder icon toobrowse tooand select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="fafae-221">Nadat u een bestand hebt geselecteerd, klikt u op **OK** toobegin Hallo uploaden tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="fafae-221">After you've selected a file, click **OK** toobegin hello upload tooAzure Storage.</span></span> <span data-ttu-id="fafae-222">Wanneer Hallo uploaden voltooid is, wordt Hallo portal een melding weergegeven en wordt gesloten Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="fafae-222">When hello upload operation is complete, hello portal displays a notification and closes hello blade.</span></span> <span data-ttu-id="fafae-223">Deze bewerking kan enige tijd duren, afhankelijk van de grootte van de Hallo van Hallo-bestand dat u uploadt en Hallo snelheid van uw netwerkverbinding zijn.</span><span class="sxs-lookup"><span data-stu-id="fafae-223">Depending on hello size of hello file that you are uploading and hello speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="fafae-224">Hallo niet sluiten **nieuwe toepassing** blade voordat Hallo uploaden voltooid is.</span><span class="sxs-lookup"><span data-stu-id="fafae-224">Do not close hello **New application** blade before hello upload operation is complete.</span></span> <span data-ttu-id="fafae-225">In dat geval wordt het uploadproces Hallo gestopt.</span><span class="sxs-lookup"><span data-stu-id="fafae-225">Doing so will stop hello upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="fafae-226">Een nieuw toepassingspakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="fafae-226">Add a new application package</span></span>
<span data-ttu-id="fafae-227">een nieuwe Pakketversie voor de toepassing van een bestaande toepassing tooadd een toepassing selecteren in Hallo **toepassingen** blade, klikt u op **pakketten**, klikt u vervolgens op **toevoegen** tooopen Hallo **toevoegen pakket** blade.</span><span class="sxs-lookup"><span data-stu-id="fafae-227">tooadd a new application package version for an existing application, select an application in hello **Applications** blade, click **Packages**, then click **Add** tooopen hello **Add package** blade.</span></span>

<span data-ttu-id="fafae-228">![Toepassing pakket blade toevoegen in Azure-portal][8]</span><span class="sxs-lookup"><span data-stu-id="fafae-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="fafae-229">Zoals u ziet, Hallo velden overeenkomen met de Hallo **nieuwe toepassing** blade, maar Hallo **toepassings-id** selectievakje is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fafae-229">As you can see, hello fields match those of hello **New application** blade, but hello **Application id** box is disabled.</span></span> <span data-ttu-id="fafae-230">Net als voor de nieuwe toepassing hello, geef Hallo **versie** bladeren voor het nieuwe pakket tooyour **toepassingspakket** ZIP-bestand en klik vervolgens op **OK** tooupload Hallo het pakket.</span><span class="sxs-lookup"><span data-stu-id="fafae-230">As you did for hello new application, specify hello **Version** for your new package, browse tooyour **Application package** .zip file, then click **OK** tooupload hello package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="fafae-231">Bijwerken of verwijderen van een toepassingspakket</span><span class="sxs-lookup"><span data-stu-id="fafae-231">Update or delete an application package</span></span>
<span data-ttu-id="fafae-232">tooupdate of verwijder een bestaande toepassingspakket, open Hallo details blade voor de toepassing hello, klikt u op **pakketten** tooopen hello **pakketten** blade, klikt u op Hallo **weglatingsteken**in de rij Hallo van Hallo toepassingspakket dat u toomodify wilt en Hallo-actie die u tooperform wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="fafae-232">tooupdate or delete an existing application package, open hello details blade for hello application, click **Packages** tooopen hello **Packages** blade, click hello **ellipsis** in hello row of hello application package that you want toomodify, and select hello action that you want tooperform.</span></span>

<span data-ttu-id="fafae-233">![Bijwerken of verwijderen van pakket in Azure-portal][7]</span><span class="sxs-lookup"><span data-stu-id="fafae-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="fafae-234">**Update**</span><span class="sxs-lookup"><span data-stu-id="fafae-234">**Update**</span></span>

<span data-ttu-id="fafae-235">Wanneer u klikt op **Update**, Hallo *updatepakket* blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fafae-235">When you click **Update**, hello *Update package* blade is displayed.</span></span> <span data-ttu-id="fafae-236">Deze blade is vergelijkbaar toohello *nieuw toepassingspakket* blade echter alleen Hallo pakket selectie-veld is ingeschakeld, zodat u een nieuwe ZIP-bestand tooupload toospecify.</span><span class="sxs-lookup"><span data-stu-id="fafae-236">This blade is similar toohello *New application package* blade, however only hello package selection field is enabled, allowing you toospecify a new ZIP file tooupload.</span></span>

<span data-ttu-id="fafae-237">![Blade voor update-pakket in Azure-portal][11]</span><span class="sxs-lookup"><span data-stu-id="fafae-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="fafae-238">**Verwijderen**</span><span class="sxs-lookup"><span data-stu-id="fafae-238">**Delete**</span></span>

<span data-ttu-id="fafae-239">Wanneer u klikt op **verwijderen**tooconfirm Hallo verwijdering van de Pakketversie hello wordt u gevraagd en Batch Hallo pakket verwijderd uit Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fafae-239">When you click **Delete**, you are asked tooconfirm hello deletion of hello package version, and Batch deletes hello package from Azure Storage.</span></span> <span data-ttu-id="fafae-240">Als u de standaardversie Hallo van een toepassing verwijdert, Hallo **standaardversie** instelling voor de toepassing hello is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fafae-240">If you delete hello default version of an application, hello **Default version** setting is removed for hello application.</span></span>

<span data-ttu-id="fafae-241">![Toepassing verwijderen][12]</span><span class="sxs-lookup"><span data-stu-id="fafae-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="fafae-242">Toepassingen installeren op rekenknooppunten</span><span class="sxs-lookup"><span data-stu-id="fafae-242">Install applications on compute nodes</span></span>
<span data-ttu-id="fafae-243">Nu dat u hebt geleerd hoe toomanage toepassingspakketten Hello Azure-portal, bespreken we hoe toodeploy ze toocompute knooppunten en ze worden uitgevoerd met de Batch-taken.</span><span class="sxs-lookup"><span data-stu-id="fafae-243">Now that you've learned how toomanage application packages with hello Azure portal, we can discuss how toodeploy them toocompute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="fafae-244">Toepassingspakketten voor toepassingen installeren</span><span class="sxs-lookup"><span data-stu-id="fafae-244">Install pool application packages</span></span>
<span data-ttu-id="fafae-245">tooinstall een toepassingspakket op alle rekenknooppunten in een pool, geeft u een of meer toepassingspakket *verwijzingen* voor Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="fafae-245">tooinstall an application package on all compute nodes in a pool, specify one or more application package *references* for hello pool.</span></span> <span data-ttu-id="fafae-246">Hallo-toepassingspakketten die u voor een groep van toepassingen opgeeft zijn geïnstalleerd op elk rekenknooppunt wanneer dat knooppunt aan Hallo-pool wordt toegevoegd en wanneer het Hallo-knooppunt wordt opnieuw opgestart of hersteld met een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="fafae-246">hello application packages that you specify for a pool are installed on each compute node when that node joins hello pool, and when hello node is rebooted or reimaged.</span></span>

<span data-ttu-id="fafae-247">Geef een of meer in Batch .NET [CloudPool][net_cloudpool].[ ApplicationPackageReferences] [ net_cloudpool_pkgref] wanneer u een nieuwe groep maakt of voor een bestaande toepassingen.</span><span class="sxs-lookup"><span data-stu-id="fafae-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="fafae-248">Hallo [ApplicationPackageReference] [ net_pkgref] klasse geeft een toepassings-ID en versie tooinstall op een pool van rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="fafae-248">hello [ApplicationPackageReference][net_pkgref] class specifies an application ID and version tooinstall on a pool's compute nodes.</span></span>

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="fafae-249">Als de implementatie van een toepassing pakket om welke reden dan ook mislukt, Hallo Batch-service aanhalingstekens knooppunt Hallo [onbruikbaar][net_nodestate], en er zijn geen taken zijn gepland voor uitvoering op dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="fafae-249">If an application package deployment fails for any reason, hello Batch service marks hello node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="fafae-250">In dit geval moet u **opnieuw** Hallo knooppunt tooreinitiate Hallo pakketimplementatie.</span><span class="sxs-lookup"><span data-stu-id="fafae-250">In this case, you should **restart** hello node tooreinitiate hello package deployment.</span></span> <span data-ttu-id="fafae-251">Opnieuw te starten Hallo knooppunt kan ook taakplanning opnieuw op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="fafae-251">Restarting hello node also enables task scheduling again on hello node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="fafae-252">Taak toepassingspakketten installeren</span><span class="sxs-lookup"><span data-stu-id="fafae-252">Install task application packages</span></span>
<span data-ttu-id="fafae-253">Vergelijkbare tooa groep, geef toepassingspakket *verwijzingen* voor een taak.</span><span class="sxs-lookup"><span data-stu-id="fafae-253">Similar tooa pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="fafae-254">Wanneer een taak geplande toorun op een knooppunt is, wordt Hallo pakket gedownload en uitgepakt vlak voordat de opdrachtregel van Hallo taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fafae-254">When a task is scheduled toorun on a node, hello package is downloaded and extracted just before hello task's command line is executed.</span></span> <span data-ttu-id="fafae-255">Als u een specifiek pakket en de versie is al geïnstalleerd op Hallo-knooppunt, Hallo pakket wordt niet gedownload en Hallo bestaand pakket wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fafae-255">If a specified package and version is already installed on hello node, hello package is not downloaded and hello existing package is used.</span></span>

<span data-ttu-id="fafae-256">een toepassingspakket taak tooinstall configureren van de taak Hallo [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] eigenschap:</span><span class="sxs-lookup"><span data-stu-id="fafae-256">tooinstall a task application package, configure hello task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

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

## <a name="execute-hello-installed-applications"></a><span data-ttu-id="fafae-257">Hallo geïnstalleerd toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="fafae-257">Execute hello installed applications</span></span>
<span data-ttu-id="fafae-258">hello-pakketten die u hebt opgegeven voor een groep of de taak zijn gedownload en uitgepakt tooa met de naam map binnen Hallo `AZ_BATCH_ROOT_DIR` van Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="fafae-258">hello packages that you've specified for a pool or task are downloaded and extracted tooa named directory within hello `AZ_BATCH_ROOT_DIR` of hello node.</span></span> <span data-ttu-id="fafae-259">Batch maakt ook een omgevingsvariabele die Hallo pad toohello map met de naam bevat.</span><span class="sxs-lookup"><span data-stu-id="fafae-259">Batch also creates an environment variable that contains hello path toohello named directory.</span></span> <span data-ttu-id="fafae-260">Uw taak opdrachtregels gebruikt deze omgevingsvariabele bij verwijzingen naar de toepassing hello op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="fafae-260">Your task command lines use this environment variable when referencing hello application on hello node.</span></span> 

<span data-ttu-id="fafae-261">Op Windows-knooppunten heeft Hallo variabele Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="fafae-261">On Windows nodes, hello variable is in hello following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="fafae-262">Op Linux-knooppunten is Hallo indeling enigszins anders.</span><span class="sxs-lookup"><span data-stu-id="fafae-262">On Linux nodes, hello format is slightly different.</span></span> <span data-ttu-id="fafae-263">Punten (.), afbreekstreepjes (-) en hekjes (#) zijn platte toounderscores in Hallo-omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="fafae-263">Periods (.), hypens (-) and number signs (#) are flattened toounderscores in hello environment variable.</span></span> <span data-ttu-id="fafae-264">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="fafae-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="fafae-265">`APPLICATIONID`en `version` zijn waarden die overeenkomen met toohello toepassing en het Pakketversie u hebt opgegeven voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="fafae-265">`APPLICATIONID` and `version` are values that correspond toohello application and package version you've specified for deployment.</span></span> <span data-ttu-id="fafae-266">Bijvoorbeeld, als u die versie 2.7 van toepassing opgegeven *blender* moet worden geïnstalleerd op Windows-knooppunten, uw taak opdrachtregels gebruikt deze omgeving variabele tooaccess de bestanden:</span><span class="sxs-lookup"><span data-stu-id="fafae-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable tooaccess its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="fafae-267">Geef op Linux-knooppunten Hallo omgevingsvariabele in deze indeling:</span><span class="sxs-lookup"><span data-stu-id="fafae-267">On Linux nodes, specify hello environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="fafae-268">Wanneer u toepassingspakketten uploadt, geeft u een standaard versie toodeploy tooyour rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="fafae-268">When you upload an application package, you can specify a default version toodeploy tooyour compute nodes.</span></span> <span data-ttu-id="fafae-269">Als u een standaardversie voor een toepassing hebt opgegeven, kunt u Hallo versieachtervoegsel weglaten wanneer u verwijst naar de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="fafae-269">If you have specified a default version for an application, you can omit hello version suffix when you reference hello application.</span></span> <span data-ttu-id="fafae-270">Kunt u de standaardversie toepassing hello opgeven in hello Azure-portal op de blade Hallo toepassingen, zoals wordt weergegeven in [uploaden en beheren van toepassingen](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="fafae-270">You can specify hello default application version in hello Azure portal, on hello Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="fafae-271">Als u '2.7' ingesteld als de standaardversie Hallo voor toepassing bijvoorbeeld *blender*, en uw taken verwijzen naar Hallo volgende omgevingsvariabele, en vervolgens uw Windows-knooppunten versie 2.7 wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="fafae-271">For example, if you set "2.7" as hello default version for application *blender*, and your tasks reference hello following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="fafae-272">Hallo volgende codefragment toont een voorbeeld van de taak vanaf de opdrachtregel waarmee wordt gestart Hallo standaardversie van Hallo *blender* toepassing:</span><span class="sxs-lookup"><span data-stu-id="fafae-272">hello following code snippet shows an example task command line that launches hello default version of hello *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="fafae-273">Zie [omgevingsinstellingen voor taken](batch-api-basics.md#environment-settings-for-tasks) in Hallo [overzicht Batch-functies](batch-api-basics.md) voor meer informatie over omgevingsinstellingen compute-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="fafae-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in hello [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="fafae-274">De toepassingspakketten van een groep bijwerken</span><span class="sxs-lookup"><span data-stu-id="fafae-274">Update a pool's application packages</span></span>
<span data-ttu-id="fafae-275">Als een bestaande pool al is geconfigureerd met een pakket, kunt u een nieuw pakket voor Hallo van toepassingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="fafae-275">If an existing pool has already been configured with an application package, you can specify a new package for hello pool.</span></span> <span data-ttu-id="fafae-276">Als u een nieuw pakket verwijzing voor een groep opgeeft, wordt de volgende Hallo toepassen:</span><span class="sxs-lookup"><span data-stu-id="fafae-276">If you specify a new package reference for a pool, hello following apply:</span></span>

* <span data-ttu-id="fafae-277">Hallo Batch-service installeert Hallo zojuist opgegeven pakket op alle nieuwe knooppunten die Hallo adresgroep toevoegen en op een bestaande knooppunt dat is opnieuw opgestart of hersteld met een installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="fafae-277">hello Batch service installs hello newly specified package on all new nodes that join hello pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="fafae-278">COMPUTE knooppunten die al in de groep Hallo tijdens het bijwerken van Hallo pakket met verwijzingen niet automatisch nieuwe toepassingspakket Hallo geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="fafae-278">Compute nodes that are already in hello pool when you update hello package references do not automatically install hello new application package.</span></span> <span data-ttu-id="fafae-279">Deze berekenen knooppunten moeten opnieuw worden opgestart of hersteld met een installatiekopie tooreceive Hallo nieuw pakket.</span><span class="sxs-lookup"><span data-stu-id="fafae-279">These compute nodes must be rebooted or reimaged tooreceive hello new package.</span></span>
* <span data-ttu-id="fafae-280">Wanneer een nieuw pakket wordt geïmplementeerd, weerspiegelen Hallo omgevingsvariabelen gemaakt Hallo nieuwe toepassing pakket verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="fafae-280">When a new package is deployed, hello created environment variables reflect hello new application package references.</span></span>

<span data-ttu-id="fafae-281">In dit voorbeeld heeft Hallo bestaande toepassingen versie 2.7 Hallo *blender* toepassing geconfigureerd als een van de [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="fafae-281">In this example, hello existing pool has version 2.7 of hello *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="fafae-282">tooupdate hello groep knooppunten met versie 2.76b, Geef een nieuwe [ApplicationPackageReference] [ net_pkgref] met de nieuwe versie Hallo en doorvoeren Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fafae-282">tooupdate hello pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with hello new version, and commit hello change.</span></span>

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

<span data-ttu-id="fafae-283">Nu dat hello nieuwe versie is geconfigureerd, Hallo Batch-service wordt geïnstalleerd versie 2.76b tooany *nieuwe* knooppunt dat aan Hallo-pool wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="fafae-283">Now that hello new version has been configured, hello Batch service installs version 2.76b tooany *new* node that joins hello pool.</span></span> <span data-ttu-id="fafae-284">tooinstall 2.76b op Hallo knooppunten die zijn *al* in de groep hello, opnieuw opstarten of deze installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="fafae-284">tooinstall 2.76b on hello nodes that are *already* in hello pool, reboot or reimage them.</span></span> <span data-ttu-id="fafae-285">Houd er rekening mee dat opnieuw opgestart knooppunten Hallo-bestanden van eerdere implementaties van het pakket behouden.</span><span class="sxs-lookup"><span data-stu-id="fafae-285">Note that rebooted nodes retain hello files from previous package deployments.</span></span>

## <a name="list-hello-applications-in-a-batch-account"></a><span data-ttu-id="fafae-286">Lijst Hallo toepassingen in een Batch-account</span><span class="sxs-lookup"><span data-stu-id="fafae-286">List hello applications in a Batch account</span></span>
<span data-ttu-id="fafae-287">U kunt Hallo toepassingen en hun pakketten in een Batch-account weergeven met behulp van Hallo [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] methode.</span><span class="sxs-lookup"><span data-stu-id="fafae-287">You can list hello applications and their packages in a Batch account by using hello [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List hello applications and their application packages in hello Batch account.
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

## <a name="wrap-up"></a><span data-ttu-id="fafae-288">Inpakken</span><span class="sxs-lookup"><span data-stu-id="fafae-288">Wrap up</span></span>
<span data-ttu-id="fafae-289">Met toepassingspakketten kunt u uw klanten Hallo-toepassingen voor hun werk selecteert en Hallo exacte versie toouse opgeven bij het verwerken van taken met de service Batch is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fafae-289">With application packages, you can help your customers select hello applications for their jobs and specify hello exact version toouse when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="fafae-290">U kunt ook Hallo mogelijkheid bieden voor uw klanten tooupload en hun eigen toepassingen in uw service bijhouden.</span><span class="sxs-lookup"><span data-stu-id="fafae-290">You might also provide hello ability for your customers tooupload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fafae-291">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fafae-291">Next steps</span></span>
* <span data-ttu-id="fafae-292">Hallo [Batch REST-API] [ api_rest] biedt ook ondersteuning toowork toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="fafae-292">hello [Batch REST API][api_rest] also provides support toowork with application packages.</span></span> <span data-ttu-id="fafae-293">Zie bijvoorbeeld Hallo [applicationPackageReferences] [ rest_add_pool_with_packages] -element in [toevoegen van een account voor toepassingsgroep tooan] [ rest_add_pool] voor informatie over het toospecify tooinstall met behulp van REST-API hello-pakketten.</span><span class="sxs-lookup"><span data-stu-id="fafae-293">For example, see hello [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool tooan account][rest_add_pool] for information about how toospecify packages tooinstall by using hello REST API.</span></span> <span data-ttu-id="fafae-294">Zie [toepassingen] [ rest_applications] voor meer informatie over hoe de toepassingsinformatie tooobtain met behulp van Batch REST-API Hallo.</span><span class="sxs-lookup"><span data-stu-id="fafae-294">See [Applications][rest_applications] for details about how tooobtain application information by using hello Batch REST API.</span></span>
* <span data-ttu-id="fafae-295">Meer informatie over hoe tooprogrammatically [beheren van Azure Batch-accounts en quota's met Batch Management .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="fafae-295">Learn how tooprogrammatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="fafae-296">Hallo [Batch Management .NET][api_net_mgmt] bibliotheek account maken en verwijderen-functies voor uw Batch-toepassing of service kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fafae-296">hello [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

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
