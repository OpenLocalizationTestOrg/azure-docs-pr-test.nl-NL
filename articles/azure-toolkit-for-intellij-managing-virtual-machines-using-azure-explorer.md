---
title: Virtuele machines beheren met behulp van de Azure-Explorer voor IntelliJ | Microsoft Docs
description: Informatie over het beheren van uw virtuele machines in Azure met behulp van de Azure-Explorer voor IntelliJ.
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
ms.openlocfilehash: 9197580407b3509fbf9a842e1fee1e6348478c34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="b3923-103">Virtuele machines beheren met behulp van de Azure-Explorer voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b3923-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="b3923-104">De Azure-Explorer, die deel van de Azure-werkset voor IntelliJ uitmaakt, biedt Java ontwikkelaars een oplossing eenvoudig te gebruiken voor het beheren van virtuele machines in de Azure-account uit binnen de IntelliJ integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="b3923-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="b3923-105">Een virtuele machine maken in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b3923-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b3923-106">Voor het maken van een virtuele machine met behulp van de Azure-Explorer, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="b3923-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="b3923-107">Aanmelden bij uw Azure-account met behulp van de stappen in de [aanmelden instructies voor de Azure-Toolkit voor IntelliJ] artikel.</span><span class="sxs-lookup"><span data-stu-id="b3923-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="b3923-108">In de **Azure Explorer** weergeven, vouw de **Azure** knooppunt met de rechtermuisknop op **virtuele Machines**, en klik vervolgens op **VM maken**.</span><span class="sxs-lookup"><span data-stu-id="b3923-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="b3923-109">![De opdracht VM maken][CR01]</span><span class="sxs-lookup"><span data-stu-id="b3923-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="b3923-110">De **nieuwe virtuele Machine maken** wizard wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="b3923-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="b3923-111">In de **Kies een abonnement** venster uw abonnement te selecteren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b3923-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![De Kies een abonnement-venster][CR02]

4. <span data-ttu-id="b3923-113">In de **selecteert u de installatiekopie van een virtuele Machine** venster, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="b3923-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="b3923-114">**Locatie**: Hiermee geeft u op waar uw virtuele machine wordt gemaakt (bijvoorbeeld *VS-West*).</span><span class="sxs-lookup"><span data-stu-id="b3923-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="b3923-115">**Afbeelding aanbevolen**: Hiermee geeft u op dat u een installatiekopie van een verkorte lijst van veelgebruikte installatiekopieën kiest.</span><span class="sxs-lookup"><span data-stu-id="b3923-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="b3923-116">**Aangepaste installatiekopie**: Hiermee geeft u op dat u een aangepaste installatiekopie kiest op basis van de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="b3923-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="b3923-117">**Publisher**: Hiermee geeft u de uitgever die de afbeelding die u voor uw virtuele machine gebruiken wilt hebt gemaakt (bijvoorbeeld *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="b3923-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="b3923-118">**Bieden**: Hiermee geeft u de virtuele machine biedt van de geselecteerde uitgever te gebruiken (bijvoorbeeld *JDK*).</span><span class="sxs-lookup"><span data-stu-id="b3923-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="b3923-119">**SKU**: Hiermee geeft u de SKU (SKU) van de geselecteerde aanbieding te gebruiken (bijvoorbeeld *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="b3923-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="b3923-120">**Versie #**: Hiermee geeft u op welke versie van de geselecteerde SKU te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b3923-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![Selecteer een venster van de installatiekopie van virtuele Machine][CR03]

5. <span data-ttu-id="b3923-122">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b3923-122">Click **Next**.</span></span> 

6. <span data-ttu-id="b3923-123">In de **basisinstellingen van de virtuele Machine** venster, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="b3923-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="b3923-124">**Naam van virtuele machine**: Hiermee geeft u de naam voor uw nieuwe virtuele machine, die moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes.</span><span class="sxs-lookup"><span data-stu-id="b3923-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="b3923-125">**De grootte van**: Hiermee geeft u het aantal kernen en het geheugen toewijzen voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b3923-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="b3923-126">**Gebruikersnaam**: Hiermee geeft u het administrator-account maken voor het beheren van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b3923-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="b3923-127">**Wachtwoord** en **bevestigen**: Hiermee geeft u het wachtwoord voor uw beheerdersaccount.</span><span class="sxs-lookup"><span data-stu-id="b3923-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![Het venster basisinstellingen van de virtuele Machine][CR04]

7. <span data-ttu-id="b3923-129">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b3923-129">Click **Next**.</span></span> 

8. <span data-ttu-id="b3923-130">In de **Resources die zijn gekoppeld** venster, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="b3923-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="b3923-131">**Resourcegroep**: Hiermee geeft u de resourcegroep voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b3923-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="b3923-132">Selecteer een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="b3923-132">Select one of the following options:</span></span>
      * <span data-ttu-id="b3923-133">**Maken van nieuwe**: geeft aan dat u wilt maken van een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="b3923-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="b3923-134">**Gebruik bestaande**: geeft aan dat u wilt selecteren in een lijst met resourcegroepen die gekoppeld aan uw Azure-account zijn.</span><span class="sxs-lookup"><span data-stu-id="b3923-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![Het venster Resources die zijn gekoppeld][CR07]

   * <span data-ttu-id="b3923-136">**Storage-account**: Hiermee geeft u het opslagaccount moet worden gebruikt voor het opslaan van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b3923-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="b3923-137">U kunt ervoor kiezen een bestaand opslagaccount of maak een nieuw account.</span><span class="sxs-lookup"><span data-stu-id="b3923-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="b3923-138">Als u ervoor kiest **nieuw**, het volgende dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b3923-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![Het dialoogvenster Storage-Account maken][CR05]

   * <span data-ttu-id="b3923-140">**Virtueel netwerk** en **Subnet**: Hiermee geeft u het virtuele netwerk en subnet dat uw virtuele machine maakt verbinding met.</span><span class="sxs-lookup"><span data-stu-id="b3923-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="b3923-141">U kunt een bestaand netwerk en subnet of kunt u een nieuw netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="b3923-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="b3923-142">Als u selecteert **nieuw**, het volgende dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b3923-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![Het dialoogvenster Virtueel netwerk maken][CR06]

   * <span data-ttu-id="b3923-144">**Openbaar IP-adres**: Hiermee geeft u een extern gerichte IP-adres voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b3923-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="b3923-145">U kunt een nieuw IP-adres maken of, als uw virtuele machine een openbaar IP-adres niet hebt wordt, kunt u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="b3923-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="b3923-146">**Netwerkbeveiligingsgroep**: Hiermee geeft u een optionele netwerken firewall voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b3923-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="b3923-147">Kunt u een firewall of, als uw virtuele machine niet voor een netwerkfirewall gebruikt wordt, kunt u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="b3923-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="b3923-148">**Beschikbaarheidsset**: Hiermee geeft u een optionele beschikbaarheidsset dat deel van uw virtuele machine uitmaken kunnen.</span><span class="sxs-lookup"><span data-stu-id="b3923-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="b3923-149">U kunt een bestaande beschikbaarheidsset, een nieuwe beschikbaarheidsset maken of, als uw virtuele machine niet bij een beschikbaarheidsset hoort wordt, selecteert u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="b3923-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="b3923-150">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b3923-150">Click **Finish**.</span></span>  
    <span data-ttu-id="b3923-151">Uw nieuwe virtuele machine wordt weergegeven in het venster van het hulpprogramma Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="b3923-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![Nieuwe virtuele machine in de weergave Azure Explorer][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="b3923-153">Opnieuw opstarten van een virtuele machine in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b3923-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b3923-154">Als u wilt een virtuele machine opstarten met behulp van de Azure-Explorer in IntelliJ, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="b3923-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="b3923-155">In de **Azure Explorer** bekijken, met de rechtermuisknop op de virtuele machine en selecteer vervolgens **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="b3923-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![De opdracht van de virtuele machine opnieuw starten][RE01]

2. <span data-ttu-id="b3923-157">Klik in het bevestigingsvenster **Ja**.</span><span class="sxs-lookup"><span data-stu-id="b3923-157">In the confirmation window, click **Yes**.</span></span> 

   ![Het venster van de virtuele machine bevestiging voor het opnieuw opstarten][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="b3923-159">Een virtuele machine in IntelliJ afsluiten</span><span class="sxs-lookup"><span data-stu-id="b3923-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b3923-160">Ga als volgt te werk om een actieve virtuele machine met behulp van de Azure-Explorer in IntelliJ afsluiten:</span><span class="sxs-lookup"><span data-stu-id="b3923-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="b3923-161">In de **Azure Explorer** bekijken, met de rechtermuisknop op de virtuele machine en selecteer vervolgens **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="b3923-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![De opdracht van virtuele machines afsluiten][SH01]

2. <span data-ttu-id="b3923-163">Klik in het bevestigingsvenster **Ja**.</span><span class="sxs-lookup"><span data-stu-id="b3923-163">In the confirmation window, click **Yes**.</span></span> 

   ![De afsluiten bevestigingsvenster van de virtuele machine][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="b3923-165">Een virtuele machine in IntelliJ verwijderen</span><span class="sxs-lookup"><span data-stu-id="b3923-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b3923-166">Als u wilt verwijderen van een virtuele machine met behulp van de Azure-Explorer in IntelliJ, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="b3923-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="b3923-167">In de **Azure Explorer** bekijken, met de rechtermuisknop op de virtuele machine en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b3923-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![De opdracht van de virtuele machine verwijderen][DE01]

2. <span data-ttu-id="b3923-169">Klik in het bevestigingsvenster **Ja**.</span><span class="sxs-lookup"><span data-stu-id="b3923-169">In the confirmation window, click **Yes**.</span></span> 

   ![Het venster van de virtuele machine bevestiging voor het verwijderen][DE02]

## <a name="next-steps"></a><span data-ttu-id="b3923-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b3923-171">Next steps</span></span>
<span data-ttu-id="b3923-172">Zie de volgende bronnen voor meer informatie over Azure grootten voor virtuele machines en prijzen:</span><span class="sxs-lookup"><span data-stu-id="b3923-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="b3923-173">Azure grootten voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="b3923-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="b3923-174">[Grootten voor Windows virtuele machines in Azure]</span><span class="sxs-lookup"><span data-stu-id="b3923-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="b3923-175">[Grootten voor virtuele Linux-machines in Azure]</span><span class="sxs-lookup"><span data-stu-id="b3923-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="b3923-176">Prijzen voor Azure virtuele machines</span><span class="sxs-lookup"><span data-stu-id="b3923-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="b3923-177">[Prijzen van virtuele machines in Windows]</span><span class="sxs-lookup"><span data-stu-id="b3923-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="b3923-178">[Prijzen van Linux virtuele machines]</span><span class="sxs-lookup"><span data-stu-id="b3923-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="b3923-179">Zie de volgende bronnen voor meer informatie over de Azure-Toolkits voor IDE voor Java:</span><span class="sxs-lookup"><span data-stu-id="b3923-179">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="b3923-180">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b3923-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b3923-181">[Wat is er nieuw in de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b3923-181">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b3923-182">[Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="b3923-182">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b3923-183">[Aanmelden instructies voor de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b3923-183">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b3923-184">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b3923-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="b3923-185">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="b3923-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b3923-186">[Wat is er nieuw in de Azure-werkset voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b3923-186">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b3923-187">[Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="b3923-187">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b3923-188">[aanmelden instructies voor de Azure-Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b3923-188">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b3923-189">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b3923-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="b3923-190">Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b3923-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="b3923-191">[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="b3923-191">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="b3923-192">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="b3923-192">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="b3923-193">[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="b3923-193">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="b3923-194">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="b3923-194">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="b3923-195">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="b3923-195">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="b3923-196">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="b3923-196">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="b3923-197">[Aanmelden instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="b3923-197">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="b3923-198">[aanmelden instructies voor de Azure-Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="b3923-198">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="b3923-199">[Wat is er nieuw in de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="b3923-199">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="b3923-200">[Wat is er nieuw in de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="b3923-200">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="b3923-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="b3923-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="b3923-202">[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="b3923-202">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="b3923-203">[Grootten voor Windows virtuele machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="b3923-203">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="b3923-204">[Grootten voor virtuele Linux-machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="b3923-204">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="b3923-205">[Prijzen van virtuele machines in Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="b3923-205">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="b3923-206">[Prijzen van Linux virtuele machines]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="b3923-206">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
