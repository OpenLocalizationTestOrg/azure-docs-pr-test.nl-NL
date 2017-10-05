---
title: Virtuele machines beheren met behulp van de Azure-Explorer voor Eclipse | Microsoft Docs
description: Informatie over het beheren van uw virtuele machines in Azure met behulp van de Azure-Explorer voor Eclipse.
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
ms.openlocfilehash: 9784e8af9c530078afee06f08a23403a44b0762f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="c4af2-103">Virtuele machines beheren met behulp van de Azure-Explorer voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="c4af2-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="c4af2-104">De Azure-Explorer, die deel van de Azure-werkset voor Eclipse uitmaakt, biedt Java ontwikkelaars een oplossing eenvoudig te gebruiken voor het beheren van virtuele machines in de Azure-account uit binnen de Eclipse integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="c4af2-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c4af2-105">Een virtuele machine maken in Eclipse</span><span class="sxs-lookup"><span data-stu-id="c4af2-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="c4af2-106">Voor het maken van een virtuele machine met behulp van de Azure-Explorer, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c4af2-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="c4af2-107">Aanmelden bij uw Azure-account met behulp van de [aanmelden instructies voor de Azure-werkset voor Eclipse].</span><span class="sxs-lookup"><span data-stu-id="c4af2-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="c4af2-108">In de **Azure Explorer** weergeven, vouw de **Azure** knooppunt met de rechtermuisknop op **virtuele Machines**, en klik vervolgens op **VM maken**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="c4af2-109">![De opdracht VM maken][CR01]</span><span class="sxs-lookup"><span data-stu-id="c4af2-109">![The Create VM command][CR01]</span></span>  
   <span data-ttu-id="c4af2-110">De **nieuwe virtuele Machine maken** wizard wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c4af2-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="c4af2-111">In de **Kies een abonnement** venster uw abonnement te selecteren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![De Kies een abonnement-venster][CR02]

4. <span data-ttu-id="c4af2-113">In de **selecteert u de installatiekopie van een virtuele Machine** venster, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c4af2-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="c4af2-114">**Locatie**: Hiermee geeft u op waar uw virtuele machine wordt gemaakt (bijvoorbeeld *VS-West*).</span><span class="sxs-lookup"><span data-stu-id="c4af2-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="c4af2-115">**Publisher**: Hiermee geeft u de uitgever die de afbeelding die u gebruikt voor het maken van uw virtuele machine hebt gemaakt (bijvoorbeeld *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="c4af2-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="c4af2-116">**Bieden**: Hiermee geeft u de virtuele machine biedt van de geselecteerde uitgever te gebruiken (bijvoorbeeld *JDK*).</span><span class="sxs-lookup"><span data-stu-id="c4af2-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="c4af2-117">**SKU**: Hiermee geeft u de SKU (SKU) van de geselecteerde aanbieding te gebruiken (bijvoorbeeld *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="c4af2-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="c4af2-118">**Versie #**: Hiermee geeft u op welke versie van de geselecteerde SKU te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c4af2-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

    ![Selecteer een venster van de installatiekopie van virtuele Machine][CR03]

5. <span data-ttu-id="c4af2-120">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-120">Click **Next**.</span></span>

6. <span data-ttu-id="c4af2-121">In de **basisinstellingen van de virtuele Machine** venster, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c4af2-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="c4af2-122">**Naam van virtuele Machine**: Hiermee geeft u de naam voor uw nieuwe virtuele machine, die moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes.</span><span class="sxs-lookup"><span data-stu-id="c4af2-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="c4af2-123">**De grootte van**: Hiermee geeft u het aantal kernen en het geheugen toewijzen voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c4af2-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="c4af2-124">**Gebruikersnaam**: Hiermee geeft u het administrator-account maken voor het beheren van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c4af2-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="c4af2-125">**Wachtwoord** en **bevestigen**: Hiermee geeft u het wachtwoord voor uw beheerdersaccount.</span><span class="sxs-lookup"><span data-stu-id="c4af2-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

    ![Het venster basisinstellingen van de virtuele Machine][CR04]

7. <span data-ttu-id="c4af2-127">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-127">Click **Next**.</span></span>

8. <span data-ttu-id="c4af2-128">In de **nieuw Opslagaccount maken** venster, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c4af2-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="c4af2-129">**Resourcegroep**: Hiermee geeft u de resourcegroep voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c4af2-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="c4af2-130">Selecteer een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="c4af2-130">Select one of the following options:</span></span>
      * <span data-ttu-id="c4af2-131">**Maken van nieuwe**: geeft aan dat u wilt maken van een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c4af2-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="c4af2-132">**Gebruik bestaande**: geeft aan dat u wilt een resourcegroep die al is gekoppeld aan uw Azure-account selecteren.</span><span class="sxs-lookup"><span data-stu-id="c4af2-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

      ![Het dialoogvenster Nieuw Opslagaccount maken][CR05]

   * <span data-ttu-id="c4af2-134">**Storage-account**: Hiermee geeft u het opslagaccount moet worden gebruikt voor het opslaan van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c4af2-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="c4af2-135">U kunt een bestaand opslagaccount gebruiken of een nieuw account maken.</span><span class="sxs-lookup"><span data-stu-id="c4af2-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="c4af2-136">**Virtueel netwerk** en **Subnet**: Hiermee geeft u het virtuele netwerk en subnet dat uw virtuele machine maakt verbinding met.</span><span class="sxs-lookup"><span data-stu-id="c4af2-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="c4af2-137">U kunt een bestaand netwerk en subnet of kunt u een nieuw netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="c4af2-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="c4af2-138">Als u selecteert **nieuw**, het volgende dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="c4af2-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![Het dialoogvenster Nieuw virtueel netwerk maken][CR06]

9. <span data-ttu-id="c4af2-140">In de **Resources die zijn gekoppeld** venster, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c4af2-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="c4af2-141">**Openbaar IP-adres**: Hiermee geeft u een extern gerichte IP-adres voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c4af2-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="c4af2-142">U kunt een nieuw IP-adres maken of, als uw virtuele machine een openbaar IP-adres niet hebt wordt, kunt u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="c4af2-143">**Netwerkbeveiligingsgroep**: Hiermee geeft u een optionele netwerken firewall voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c4af2-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="c4af2-144">Kunt u een firewall of, als uw virtuele machine niet voor een netwerkfirewall gebruikt wordt, kunt u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="c4af2-145">**Beschikbaarheidsset**: Hiermee geeft u een optionele beschikbaarheidsset dat deel van uw virtuele machine uitmaken kunnen.</span><span class="sxs-lookup"><span data-stu-id="c4af2-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="c4af2-146">U kunt een bestaande beschikbaarheidsset selecteren of maken van een nieuwe beschikbaarheidsset of de virtuele machine hoort niet bij een beschikbaarheidsset, kunt u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![Het venster Resources die zijn gekoppeld][CR07]

9. <span data-ttu-id="c4af2-148">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-148">Click **Finish**.</span></span>  
  <span data-ttu-id="c4af2-149">Uw nieuwe virtuele machine wordt weergegeven in het venster van het hulpprogramma Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="c4af2-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

   ![Nieuwe virtuele Machine][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c4af2-151">Opnieuw opstarten van een virtuele machine in Eclipse</span><span class="sxs-lookup"><span data-stu-id="c4af2-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="c4af2-152">Als u wilt een virtuele machine opstarten met behulp van de Azure-Explorer in Eclipse, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c4af2-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="c4af2-153">In de **Azure Explorer** bekijken, met de rechtermuisknop op de virtuele machine en selecteer vervolgens **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![De opdracht van de virtuele machine opnieuw starten][RE01]

2. <span data-ttu-id="c4af2-155">Klik in het bevestigingsvenster **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-155">In the confirmation window, click **Yes**.</span></span>

   ![Het bevestigingsvenster opnieuw opstarten][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c4af2-157">Een virtuele machine in Eclipse afsluiten</span><span class="sxs-lookup"><span data-stu-id="c4af2-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="c4af2-158">Als u wilt afsluiten een actieve virtuele machine met behulp van de Azure-Explorer in Eclipse, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c4af2-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="c4af2-159">In de **Azure Explorer** bekijken, met de rechtermuisknop op de virtuele machine en selecteer vervolgens **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![De opdracht van virtuele machines afsluiten][SH01]

2. <span data-ttu-id="c4af2-161">Klik in het bevestigingsvenster **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-161">In the confirmation window, click **Yes**.</span></span>

   ![Het bevestigingsvenster virtuele machines afsluiten][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c4af2-163">Een virtuele machine in Eclipse verwijderen</span><span class="sxs-lookup"><span data-stu-id="c4af2-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="c4af2-164">Als u wilt verwijderen van een virtuele machine met behulp van de Azure-Explorer in Eclipse, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c4af2-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="c4af2-165">In de **Azure Explorer** bekijken, met de rechtermuisknop op de virtuele machine en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![De opdracht van de virtuele machine verwijderen][DE01]

2. <span data-ttu-id="c4af2-167">Klik in het bevestigingsvenster **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c4af2-167">In the confirmation window, click **Yes**.</span></span>

   ![Het verwijderen van een virtuele machine bevestigingsvenster][DE02]

## <a name="next-steps"></a><span data-ttu-id="c4af2-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4af2-169">Next steps</span></span>
<span data-ttu-id="c4af2-170">Zie de volgende bronnen voor meer informatie over Azure grootten voor virtuele machines en prijzen:</span><span class="sxs-lookup"><span data-stu-id="c4af2-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="c4af2-171">Azure grootten voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="c4af2-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="c4af2-172">[Grootten voor Windows virtuele machines in Azure]</span><span class="sxs-lookup"><span data-stu-id="c4af2-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="c4af2-173">[Grootten voor virtuele Linux-machines in Azure]</span><span class="sxs-lookup"><span data-stu-id="c4af2-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="c4af2-174">Prijzen voor Azure virtuele machines</span><span class="sxs-lookup"><span data-stu-id="c4af2-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="c4af2-175">[Prijzen van virtuele machines in Windows]</span><span class="sxs-lookup"><span data-stu-id="c4af2-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="c4af2-176">[Prijzen van Linux virtuele machines]</span><span class="sxs-lookup"><span data-stu-id="c4af2-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="c4af2-177">Zie de volgende bronnen voor meer informatie over de Azure-Toolkits voor IDE voor Java:</span><span class="sxs-lookup"><span data-stu-id="c4af2-177">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="c4af2-178">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c4af2-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c4af2-179">[Wat is er nieuw in de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c4af2-179">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c4af2-180">[Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="c4af2-180">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c4af2-181">[aanmelden instructies voor de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c4af2-181">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c4af2-182">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c4af2-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="c4af2-183">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c4af2-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c4af2-184">[Wat is er nieuw in de Azure-werkset voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c4af2-184">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c4af2-185">[Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="c4af2-185">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c4af2-186">[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c4af2-186">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c4af2-187">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c4af2-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="c4af2-188">Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="c4af2-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="c4af2-189">[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="c4af2-189">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="c4af2-190">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c4af2-190">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="c4af2-191">[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="c4af2-191">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="c4af2-192">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="c4af2-192">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="c4af2-193">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="c4af2-193">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="c4af2-194">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="c4af2-194">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="c4af2-195">[aanmelden instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="c4af2-195">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="c4af2-196">[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="c4af2-196">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="c4af2-197">[Wat is er nieuw in de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="c4af2-197">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="c4af2-198">[Wat is er nieuw in de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="c4af2-198">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="c4af2-199">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="c4af2-199">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="c4af2-200">[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="c4af2-200">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="c4af2-201">[Grootten voor Windows virtuele machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="c4af2-201">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="c4af2-202">[Grootten voor virtuele Linux-machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="c4af2-202">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="c4af2-203">[Prijzen van virtuele machines in Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="c4af2-203">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="c4af2-204">[Prijzen van Linux virtuele machines]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="c4af2-204">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
