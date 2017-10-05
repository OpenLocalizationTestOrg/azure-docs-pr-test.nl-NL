---
title: Storage-accounts beheren met behulp van de Azure-Explorer voor Eclipse | Microsoft Docs
description: Informatie over het beheren van uw Azure storage-accounts met behulp van de Azure-Explorer voor Eclipse.
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
ms.openlocfilehash: 5b3014b5aca368be8ea46863c83665abde10fed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="3f3c0-103">Storage-accounts beheren met behulp van de Azure-Explorer voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f3c0-103">Manage storage accounts by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="3f3c0-104">De Azure-Explorer, die deel van de Azure-werkset voor Eclipse uitmaakt, biedt Java ontwikkelaars een oplossing eenvoudig te gebruiken voor het beheren van storage-accounts in de Azure-account uit binnen de Eclipse integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="3f3c0-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="3f3c0-105">Een opslagaccount in Eclipse maken</span><span class="sxs-lookup"><span data-stu-id="3f3c0-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="3f3c0-106">Voor het maken van een opslagaccount met behulp van de Azure-Explorer, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="3f3c0-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3f3c0-107">Aanmelden bij uw Azure-account met behulp van de [aanmelden instructies voor de Azure-werkset voor Eclipse].</span><span class="sxs-lookup"><span data-stu-id="3f3c0-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="3f3c0-108">In de **Azure Explorer** weergeven, vouw de **Azure** knooppunt met de rechtermuisknop op **Opslagaccounts**, en klik vervolgens op **Storage-Account maken**.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Opdracht voor Storage-Account maken][CS01]

3. <span data-ttu-id="3f3c0-110">In de **Storage-Account maken** dialoogvenster geeft u de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="3f3c0-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Dialoogvenster Nieuw Opslagaccount maken][CS02]

   * <span data-ttu-id="3f3c0-112">**Naam**: Hiermee geeft u de naam voor het nieuwe opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="3f3c0-113">**Abonnement**: Hiermee geeft u de Azure-abonnement dat u wilt gebruiken voor het nieuwe opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-113">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="3f3c0-114">**Resourcegroep**: Hiermee geeft u de resourcegroep voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-114">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="3f3c0-115">Selecteer een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="3f3c0-115">Select one of the following options:</span></span>
      * <span data-ttu-id="3f3c0-116">**Maken van nieuw**: geeft aan dat u wilt maken van een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-116">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="3f3c0-117">**Gebruik bestaande**: Hiermee geeft u op dat u selecteert in een lijst met resourcegroepen die gekoppeld aan uw Azure-account zijn.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="3f3c0-118">**Regio**: Hiermee geeft u de locatie waar uw storage-account wordt gemaakt (bijvoorbeeld 'West ons').</span><span class="sxs-lookup"><span data-stu-id="3f3c0-118">**Region**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="3f3c0-119">**Account kind**: geeft het type opslagaccount maken (bijvoorbeeld 'Blob storage').</span><span class="sxs-lookup"><span data-stu-id="3f3c0-119">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="3f3c0-120">Zie voor meer informatie [over Azure storage-accounts].</span><span class="sxs-lookup"><span data-stu-id="3f3c0-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="3f3c0-121">**Prestaties**: Hiermee geeft u op welke storage-account met gebruik van de geselecteerde uitgever (bijvoorbeeld 'Premium').</span><span class="sxs-lookup"><span data-stu-id="3f3c0-121">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="3f3c0-122">Zie voor meer informatie [Azure storage schaalbaarheids- en prestatiedoelen].</span><span class="sxs-lookup"><span data-stu-id="3f3c0-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="3f3c0-123">**Replicatie**: Hiermee geeft u de replicatie voor het opslagaccount (bijvoorbeeld ' Zone-redundante').</span><span class="sxs-lookup"><span data-stu-id="3f3c0-123">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="3f3c0-124">Zie voor meer informatie [Azure storage-replicatie].</span><span class="sxs-lookup"><span data-stu-id="3f3c0-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="3f3c0-125">Wanneer u alle van de voorgaande opties hebt opgegeven, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-125">When you have specified all of the preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="3f3c0-126">Storage-container in Eclipse maken</span><span class="sxs-lookup"><span data-stu-id="3f3c0-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="3f3c0-127">Voor het maken van een storage-container met de Verkenner Azure, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="3f3c0-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3f3c0-128">In de **Azure Explorer** weergeven, met de rechtermuisknop op het opslagaccount waar u een container maken en klik vervolgens op **maken blob-container**.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-128">In the **Azure Explorer** view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Opdracht voor blob-container maken][CC01]

2. <span data-ttu-id="3f3c0-130">In de **maken blob-container** in het dialoogvenster geeft de naam voor de container en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="3f3c0-131">Zie voor meer informatie over de naamgeving van storage-containers [Naming en verwijzen naar containers, blobs en metagegevens].</span><span class="sxs-lookup"><span data-stu-id="3f3c0-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Dialoogvenster voor blob-container maken][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="3f3c0-133">Een opslagcontainer voor in Eclipse verwijderen</span><span class="sxs-lookup"><span data-stu-id="3f3c0-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="3f3c0-134">Als u wilt een opslagcontainer verwijderen met behulp van de Azure-Explorer, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="3f3c0-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3f3c0-135">In de **Azure Explorer** weergeven, met de rechtermuisknop op de storage-container en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-135">In the **Azure Explorer** view, right-click the storage container, and then click **Delete**.</span></span>

   ![Storage-container opdracht verwijderen][DC01]

2. <span data-ttu-id="3f3c0-137">Klik in het bevestigingsvenster **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-137">In the confirmation window, click **OK**.</span></span>

   ![Storage-container bevestigingsvenster verwijderen][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="3f3c0-139">Een opslagaccount in Eclipse verwijderen</span><span class="sxs-lookup"><span data-stu-id="3f3c0-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="3f3c0-140">Als u wilt een opslagaccount verwijderen met behulp van de Azure-Explorer, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="3f3c0-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3f3c0-141">In de **Azure Explorer** weergeven, met de rechtermuisknop op het storage-account en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-141">In the **Azure Explorer** view, right-click the storage account, and then click **Delete**.</span></span>

   ![Opdracht voor storage-account verwijderen][DS01]

2. <span data-ttu-id="3f3c0-143">Klik in het bevestigingsvenster **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f3c0-143">In the confirmation window, click **OK**.</span></span>

   ![Bevestigingsvenster storage-account verwijderen][DS02]

## <a name="next-steps"></a><span data-ttu-id="3f3c0-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f3c0-145">Next steps</span></span>
<span data-ttu-id="3f3c0-146">Zie de volgende bronnen voor meer informatie over Azure storage-accounts, grootten en prijzen:</span><span class="sxs-lookup"><span data-stu-id="3f3c0-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="3f3c0-147">[Inleiding tot Microsoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="3f3c0-148">[over Azure storage-accounts]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="3f3c0-149">Grootten van Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="3f3c0-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="3f3c0-150">[Grootten voor Windows storage-accounts in Azure]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="3f3c0-151">[Grootten voor Linux-accounts voor opslag in Azure]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="3f3c0-152">Prijzen voor Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="3f3c0-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="3f3c0-153">[Prijzen voor Windows storage-account]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="3f3c0-154">[Prijzen voor Linux-opslagaccount]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="3f3c0-155">Zie de volgende bronnen voor meer informatie over Azure Toolkits voor IDE voor Java:</span><span class="sxs-lookup"><span data-stu-id="3f3c0-155">For more information about Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="3f3c0-156">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f3c0-157">[Wat is er nieuw in de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-157">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f3c0-158">[Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="3f3c0-158">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f3c0-159">[aanmelden instructies voor de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-159">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f3c0-160">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="3f3c0-161">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="3f3c0-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f3c0-162">[Wat is er nieuw in de Azure-werkset voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-162">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f3c0-163">[Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="3f3c0-163">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f3c0-164">[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-164">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f3c0-165">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f3c0-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="3f3c0-166">Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="3f3c0-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="3f3c0-167">[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="3f3c0-167">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="3f3c0-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="3f3c0-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="3f3c0-169">[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="3f3c0-169">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="3f3c0-170">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="3f3c0-170">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="3f3c0-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="3f3c0-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="3f3c0-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="3f3c0-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="3f3c0-173">[aanmelden instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="3f3c0-173">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="3f3c0-174">[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="3f3c0-174">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="3f3c0-175">[Wat is er nieuw in de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="3f3c0-175">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="3f3c0-176">[Wat is er nieuw in de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="3f3c0-176">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="3f3c0-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="3f3c0-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="3f3c0-178">[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="3f3c0-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="3f3c0-179">[Inleiding tot Microsoft Azure Storage]: /azure/storage/storage-introduction</span><span class="sxs-lookup"><span data-stu-id="3f3c0-179">[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction</span></span>
<span data-ttu-id="3f3c0-180">[over Azure storage-accounts]: /azure/storage/storage-create-storage-account</span><span class="sxs-lookup"><span data-stu-id="3f3c0-180">[About Azure storage accounts]: /azure/storage/storage-create-storage-account</span></span>
<span data-ttu-id="3f3c0-181">[Azure storage-replicatie]: /azure/storage/storage-redundancy</span><span class="sxs-lookup"><span data-stu-id="3f3c0-181">[Azure storage replication]: /azure/storage/storage-redundancy</span></span>
<span data-ttu-id="3f3c0-182">[Schaalbaarheid van de Azure-opslag- en prestatiedoelen]: /azure/storage/storage-scalability-targets</span><span class="sxs-lookup"><span data-stu-id="3f3c0-182">[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets</span></span>
<span data-ttu-id="3f3c0-183">[Naming en verwijzen naar containers, blobs en metagegevens]: http://go.microsoft.com/fwlink/?LinkId=255555</span><span class="sxs-lookup"><span data-stu-id="3f3c0-183">[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555</span></span>

<span data-ttu-id="3f3c0-184">[Grootten voor Windows storage-accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="3f3c0-184">[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="3f3c0-185">[Grootten voor Linux-accounts voor opslag in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="3f3c0-185">[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="3f3c0-186">[Prijzen voor Windows storage-account]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="3f3c0-186">[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="3f3c0-187">[Prijzen voor Linux-opslagaccount]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="3f3c0-187">[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
