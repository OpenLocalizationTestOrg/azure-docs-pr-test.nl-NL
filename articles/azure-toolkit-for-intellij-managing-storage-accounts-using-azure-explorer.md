---
title: storage-accounts met behulp van aaaManage hello Azure Explorer voor IntelliJ | Microsoft Docs
description: Meer informatie over hoe toomanage uw Azure-opslag gebruikersaccounts met behulp hello Azure Explorer voor IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: b094bdcd2fa2782cb12b67c96ac406fbe4c1aa3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="5a179-103">Storage-accounts beheren met behulp van hello Azure Explorer voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5a179-103">Manage storage accounts by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="5a179-104">Hello Azure Explorer, die deel van hello Azure Toolkit voor IntelliJ uitmaakt, Java-ontwikkelaars met een eenvoudig-en-klare oplossing biedt voor het beheren van opslagaccounts in het Azure-account via binnen Hallo IntelliJ integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="5a179-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="5a179-105">Een opslagaccount in IntelliJ maken</span><span class="sxs-lookup"><span data-stu-id="5a179-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="5a179-106">een opslagaccount met behulp van hello Azure Explorer toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a179-106">toocreate a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="5a179-107">Meld u aan tooyour Azure-account met behulp van Hallo [aanmelden instructies voor het hello Azure Toolkit voor Eclipse].</span><span class="sxs-lookup"><span data-stu-id="5a179-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span> 

2. <span data-ttu-id="5a179-108">In Hallo **Azure Explorer** weergeven, vouwt u Hallo **Azure** knooppunt met de rechtermuisknop op **Opslagaccounts**, en klik vervolgens op **Storage-Account maken**.</span><span class="sxs-lookup"><span data-stu-id="5a179-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Opdracht voor Storage-Account maken][CS01]

3. <span data-ttu-id="5a179-110">In Hallo **Storage-Account maken** dialoogvenster geeft u de Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="5a179-110">In hello **Create Storage Account** dialog box, specify hello following options:</span></span>

   ![Dialoogvenster Nieuw Opslagaccount maken][CS02]

   * <span data-ttu-id="5a179-112">**Naam**: Hiermee geeft u Hallo-naam voor het nieuwe opslagaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a179-112">**Name**: Specifies hello name for hello new storage account.</span></span>

   * <span data-ttu-id="5a179-113">**Account kind**: Hiermee geeft u Hallo type storage account toocreate (bijvoorbeeld ' Blob-opslag').</span><span class="sxs-lookup"><span data-stu-id="5a179-113">**Account kind**: Specifies hello type of storage account toocreate (for example, "Blob storage").</span></span> <span data-ttu-id="5a179-114">Zie voor meer informatie [over Azure storage-accounts].</span><span class="sxs-lookup"><span data-stu-id="5a179-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="5a179-115">**Prestaties**: Hiermee geeft u op welke opslagaccount toouse aanbieding van de geselecteerde uitgever hello (bijvoorbeeld 'Premium').</span><span class="sxs-lookup"><span data-stu-id="5a179-115">**Performance**: Specifies which storage account offering toouse from hello selected publisher (for example, "Premium").</span></span> <span data-ttu-id="5a179-116">Zie voor meer informatie [Azure storage schaalbaarheids- en prestatiedoelen].</span><span class="sxs-lookup"><span data-stu-id="5a179-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="5a179-117">**Replicatie**: Hiermee geeft u de replicatie Hallo voor Hallo storage-account (bijvoorbeeld ' Zone-redundante').</span><span class="sxs-lookup"><span data-stu-id="5a179-117">**Replication**: Specifies hello replication for hello storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="5a179-118">Zie voor meer informatie [Azure storage-replicatie].</span><span class="sxs-lookup"><span data-stu-id="5a179-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="5a179-119">**Abonnement**: Hiermee geeft u hello Azure-abonnement dat u voor het nieuwe opslagaccount hello toouse wilt.</span><span class="sxs-lookup"><span data-stu-id="5a179-119">**Subscription**: Specifies hello Azure subscription that you want toouse for hello new storage account.</span></span>

   * <span data-ttu-id="5a179-120">**Locatie**: Hiermee geeft u Hallo-locatie waar uw storage-account wordt gemaakt (bijvoorbeeld 'West ons').</span><span class="sxs-lookup"><span data-stu-id="5a179-120">**Location**: Specifies hello location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="5a179-121">**Resourcegroep**: Hiermee geeft u de resourcegroep Hallo voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5a179-121">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="5a179-122">Selecteer een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="5a179-122">Select one of hello following options:</span></span>
      * <span data-ttu-id="5a179-123">**Maken van nieuwe**: geeft aan dat u wilt dat toocreate een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="5a179-123">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="5a179-124">**Gebruik bestaande**: Hiermee geeft u op dat u selecteert in een lijst met resourcegroepen die gekoppeld aan uw Azure-account zijn.</span><span class="sxs-lookup"><span data-stu-id="5a179-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="5a179-125">Wanneer u alle Hallo voorgaande opties hebt opgegeven, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a179-125">When you have specified all of hello preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="5a179-126">Storage-container in IntelliJ maken</span><span class="sxs-lookup"><span data-stu-id="5a179-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="5a179-127">een opslagcontainer met behulp van hello Azure Explorer toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a179-127">toocreate a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="5a179-128">Hallo Azure Verkenner-weergave, met de rechtermuisknop op Hallo opslagaccount waar toocreate een container en klik vervolgens op **maken blob-container**.</span><span class="sxs-lookup"><span data-stu-id="5a179-128">In hello Azure Explorer view, right-click hello storage account where you want toocreate a container, and then click **Create blob container**.</span></span>

   ![Opdracht voor blob-container maken][CC01]

2. <span data-ttu-id="5a179-130">In Hallo **maken blob-container** in het dialoogvenster Hallo naam opgeven voor de container en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a179-130">In hello **Create blob container** dialog box, specify hello name for your container, and then click **OK**.</span></span> <span data-ttu-id="5a179-131">Zie voor meer informatie over de naamgeving van storage-containers [Naming en verwijzen naar containers, blobs en metagegevens].</span><span class="sxs-lookup"><span data-stu-id="5a179-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Dialoogvenster Storage-Container maken][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="5a179-133">Een opslagcontainer voor in IntelliJ verwijderen</span><span class="sxs-lookup"><span data-stu-id="5a179-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="5a179-134">een opslagcontainer met behulp van hello Azure Explorer toodelete Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a179-134">toodelete a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="5a179-135">Met de rechtermuisknop op Hallo storage-container in hello Azure Verkenner-weergave, en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="5a179-135">In hello Azure Explorer view, right-click hello storage container, and then click **Delete**.</span></span>

   ![Storage-container opdracht verwijderen][DC01]

2. <span data-ttu-id="5a179-137">Klik in het bevestigingsvenster hello, **Ja**.</span><span class="sxs-lookup"><span data-stu-id="5a179-137">In hello confirmation window, click **Yes**.</span></span>

   ![Storage-container bevestigingsvenster verwijderen][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="5a179-139">Een opslagaccount in IntelliJ verwijderen</span><span class="sxs-lookup"><span data-stu-id="5a179-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="5a179-140">een opslagaccount met behulp van hello Azure Explorer toodelete Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a179-140">toodelete a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="5a179-141">In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo storage-account en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="5a179-141">In hello **Azure Explorer** view, right-click hello storage account, and then select **Delete**.</span></span>

   ![Menu voor storage-account verwijderen][DS01]

2. <span data-ttu-id="5a179-143">Klik in het bevestigingsvenster hello, **Ja**.</span><span class="sxs-lookup"><span data-stu-id="5a179-143">In hello confirmation window, click **Yes**.</span></span>

   ![Bevestigingsvenster storage-account verwijderen][DS02]

## <a name="next-steps"></a><span data-ttu-id="5a179-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a179-145">Next steps</span></span>
<span data-ttu-id="5a179-146">Zie voor meer informatie over Azure storage-accounts, grootten en prijzen Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a179-146">For more information about Azure storage accounts, sizes, and pricing, see hello following resources:</span></span>

* <span data-ttu-id="5a179-147">[Inleiding tooMicrosoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="5a179-147">[Introduction tooMicrosoft Azure Storage]</span></span>
* <span data-ttu-id="5a179-148">[over Azure storage-accounts]</span><span class="sxs-lookup"><span data-stu-id="5a179-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="5a179-149">Grootten van Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="5a179-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="5a179-150">[Grootten voor Windows storage-accounts in Azure]</span><span class="sxs-lookup"><span data-stu-id="5a179-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="5a179-151">[Grootten voor Linux-accounts voor opslag in Azure]</span><span class="sxs-lookup"><span data-stu-id="5a179-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="5a179-152">Prijzen voor Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="5a179-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="5a179-153">[Prijzen voor Windows storage-account]</span><span class="sxs-lookup"><span data-stu-id="5a179-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="5a179-154">[Prijzen voor Linux-opslagaccount]</span><span class="sxs-lookup"><span data-stu-id="5a179-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="5a179-155">Zie voor meer informatie over Azure Toolkits voor IDE voor Java Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="5a179-155">For more information about Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="5a179-156">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5a179-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5a179-157">[Wat is er nieuw in hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5a179-157">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5a179-158">[Hello Azure Toolkit voor Eclipse installeren]</span><span class="sxs-lookup"><span data-stu-id="5a179-158">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5a179-159">[aanmelden instructies voor het hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5a179-159">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5a179-160">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5a179-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="5a179-161">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5a179-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5a179-162">[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5a179-162">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5a179-163">[Hello Azure Toolkit voor IntelliJ installeren]</span><span class="sxs-lookup"><span data-stu-id="5a179-163">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5a179-164">[Aanmelden instructies voor hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5a179-164">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5a179-165">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5a179-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="5a179-166">Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="5a179-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Azure Toolkit voor Eclipse installeren]: ./azure-toolkit-for-eclipse-installation.md
[Hello Azure Toolkit voor IntelliJ installeren]: ./azure-toolkit-for-intellij-installation.md
[aanmelden instructies voor het hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Aanmelden instructies voor hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

[Inleiding tooMicrosoft Azure Storage]: /azure/storage/storage-introduction
[over Azure storage-accounts]: /azure/storage/storage-create-storage-account
[Azure storage-replicatie]: /azure/storage/storage-redundancy
[Schaalbaarheid van de Azure-opslag- en prestatiedoelen]: /azure/storage/storage-scalability-targets
[Naming en verwijzen naar containers, blobs en metagegevens]: http://go.microsoft.com/fwlink/?LinkId=255555

[Grootten voor Windows storage-accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Grootten voor Linux-accounts voor opslag in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Prijzen voor Windows storage-account]: /pricing/details/virtual-machines/windows/
[Prijzen voor Linux-opslagaccount]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
