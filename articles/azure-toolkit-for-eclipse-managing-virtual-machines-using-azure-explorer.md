---
title: aaaManage virtuele machines met behulp van Azure Explorer voor Eclipse Hallo | Microsoft Docs
description: Meer informatie over hoe toomanage uw virtuele machines in Azure met behulp van hello Azure Explorer voor Eclipse.
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
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="f096d-103">Virtuele machines beheren met behulp van hello Azure Explorer voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="f096d-103">Manage virtual machines by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="f096d-104">Hello Azure Explorer, die deel van hello Azure Toolkit voor Eclipse uitmaakt, Java-ontwikkelaars met een eenvoudig-en-klare oplossing biedt voor het beheren van virtuele machines in de Azure-account uit binnen Hallo Eclipse IDE integrated development environment ().</span><span class="sxs-lookup"><span data-stu-id="f096d-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="f096d-105">Een virtuele machine maken in Eclipse</span><span class="sxs-lookup"><span data-stu-id="f096d-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="f096d-106">een virtuele machine met behulp van hello Azure Explorer toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="f096d-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="f096d-107">Meld u aan tooyour Azure-account met behulp van Hallo [aanmelden instructies voor het hello Azure Toolkit voor Eclipse].</span><span class="sxs-lookup"><span data-stu-id="f096d-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="f096d-108">In Hallo **Azure Explorer** weergeven, vouwt u Hallo **Azure** knooppunt met de rechtermuisknop op **virtuele Machines**, en klik vervolgens op **VM maken**.</span><span class="sxs-lookup"><span data-stu-id="f096d-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="f096d-109">![Hallo opdracht VM maken][CR01]</span><span class="sxs-lookup"><span data-stu-id="f096d-109">![hello Create VM command][CR01]</span></span>  
   <span data-ttu-id="f096d-110">Hallo **nieuwe virtuele Machine maken** wizard wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f096d-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="f096d-111">In Hallo **Kies een abonnement** venster uw abonnement te selecteren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f096d-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Kies een abonnement venster Hallo][CR02]

4. <span data-ttu-id="f096d-113">In Hallo **selecteert u de installatiekopie van een virtuele Machine** venster Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="f096d-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="f096d-114">**Locatie**: Hiermee geeft u op waar uw virtuele machine wordt gemaakt (bijvoorbeeld *VS-West*).</span><span class="sxs-lookup"><span data-stu-id="f096d-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="f096d-115">**Publisher**: Hiermee geeft u op Hallo publisher dat u uw virtuele machine gaat gebruiken voor toocreate Hallo-installatiekopie heeft gemaakt (bijvoorbeeld *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="f096d-115">**Publisher**: Specifies hello publisher that created hello image you'll use toocreate your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="f096d-116">**Bieden**: Hiermee geeft u op Hallo virtuele machine toouse aanbieding van de geselecteerde uitgever Hallo (bijvoorbeeld *JDK*).</span><span class="sxs-lookup"><span data-stu-id="f096d-116">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="f096d-117">**SKU**: Hiermee geeft u op Hallo SKU (SKU's) toouse van de geselecteerde serviceaanbieding Hallo (bijvoorbeeld *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="f096d-117">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="f096d-118">**Versie #**: Hiermee geeft u op welke versie van Hallo geselecteerd SKU toouse.</span><span class="sxs-lookup"><span data-stu-id="f096d-118">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

    ![Hallo selecteert u het venster van een installatiekopie van virtuele Machine][CR03]

5. <span data-ttu-id="f096d-120">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f096d-120">Click **Next**.</span></span>

6. <span data-ttu-id="f096d-121">In Hallo **basisinstellingen van de virtuele Machine** venster Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="f096d-121">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="f096d-122">**Naam van virtuele Machine**: Hiermee geeft u de naam Hallo voor uw nieuwe virtuele machine die moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes.</span><span class="sxs-lookup"><span data-stu-id="f096d-122">**Virtual Machine Name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="f096d-123">**De grootte van**: Hiermee geeft u Hallo aantal kernen en geheugen tooallocate voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f096d-123">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="f096d-124">**Gebruikersnaam**: Hiermee geeft u op Hallo beheerder account toocreate voor het beheren van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f096d-124">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="f096d-125">**Wachtwoord** en **bevestigen**: Hallo wachtwoord voor uw beheerdersaccount.</span><span class="sxs-lookup"><span data-stu-id="f096d-125">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

    ![Hallo basisinstellingen van de virtuele Machine venster][CR04]

7. <span data-ttu-id="f096d-127">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f096d-127">Click **Next**.</span></span>

8. <span data-ttu-id="f096d-128">In Hallo **nieuw Opslagaccount maken** venster Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="f096d-128">In hello **Create New Storage Account** window, enter hello following information:</span></span>

   * <span data-ttu-id="f096d-129">**Resourcegroep**: Hiermee geeft u de resourcegroep Hallo voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f096d-129">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="f096d-130">Selecteer een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="f096d-130">Select one of hello following options:</span></span>
      * <span data-ttu-id="f096d-131">**Maken van nieuwe**: geeft aan dat u wilt dat toocreate een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f096d-131">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="f096d-132">**Gebruik bestaande**: geeft aan dat u wilt dat tooselect een resourcegroep die al is gekoppeld aan uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f096d-132">**Use existing**: Specifies that you want tooselect a resource group that is already associated with your Azure account.</span></span>

      ![dialoogvenster voor Hallo nieuw Opslagaccount maken][CR05]

   * <span data-ttu-id="f096d-134">**Storage-account**: Hiermee geeft u op Hallo storage account toouse voor het opslaan van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f096d-134">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="f096d-135">U kunt een bestaand opslagaccount gebruiken of een nieuw account maken.</span><span class="sxs-lookup"><span data-stu-id="f096d-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="f096d-136">**Virtueel netwerk** en **Subnet**: Hiermee geeft u op Hallo virtueel netwerk en subnet dat uw virtuele machine maakt verbinding met.</span><span class="sxs-lookup"><span data-stu-id="f096d-136">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="f096d-137">U kunt een bestaand netwerk en subnet of kunt u een nieuw netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="f096d-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="f096d-138">Als u selecteert **nieuw**, Hallo volgen in het dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="f096d-138">If you select **Create new**, hello following dialog box is displayed:</span></span>

      ![dialoogvenster voor Hallo nieuw virtueel netwerk maken][CR06]

9. <span data-ttu-id="f096d-140">In Hallo **Resources die zijn gekoppeld** venster Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="f096d-140">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="f096d-141">**Openbaar IP-adres**: Hiermee geeft u een extern gerichte IP-adres voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f096d-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="f096d-142">U kunt toocreate een nieuw IP-adres of, als uw virtuele machine een openbaar IP-adres niet hebt wordt, kunt u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="f096d-142">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="f096d-143">**Netwerkbeveiligingsgroep**: Hiermee geeft u een optionele netwerken firewall voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f096d-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="f096d-144">Kunt u een firewall of, als uw virtuele machine niet voor een netwerkfirewall gebruikt wordt, kunt u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="f096d-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="f096d-145">**Beschikbaarheidsset**: Hiermee geeft u een optionele beschikbaarheidsset dat deel van uw virtuele machine uitmaken kunnen.</span><span class="sxs-lookup"><span data-stu-id="f096d-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="f096d-146">U kunt een bestaande beschikbaarheidsset selecteren of maken van een nieuwe beschikbaarheidsset of, als uw virtuele machine niet tooan beschikbaarheidsset hoort, kunt u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="f096d-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong tooan availability set, you can select **(None)**.</span></span>

   ![venster van de Resources die zijn gekoppeld Hallo][CR07]

9. <span data-ttu-id="f096d-148">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f096d-148">Click **Finish**.</span></span>  
  <span data-ttu-id="f096d-149">Uw nieuwe virtuele machine wordt weergegeven in het venster hello Azure Explorer-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="f096d-149">Your new virtual machine is displayed in hello Azure Explorer tool window.</span></span>

   ![Nieuwe virtuele Machine][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="f096d-151">Opnieuw opstarten van een virtuele machine in Eclipse</span><span class="sxs-lookup"><span data-stu-id="f096d-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="f096d-152">een virtuele machine met behulp van hello Azure Explorer in Eclipse toorestart Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="f096d-152">toorestart a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="f096d-153">In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo virtuele machine en selecteer vervolgens **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="f096d-153">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![de opdracht Hallo virtuele machines opnieuw starten][RE01]

2. <span data-ttu-id="f096d-155">Klik in het bevestigingsvenster hello, **Ja**.</span><span class="sxs-lookup"><span data-stu-id="f096d-155">In hello confirmation window, click **Yes**.</span></span>

   ![Hallo herstart bevestigingsvenster][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="f096d-157">Een virtuele machine in Eclipse afsluiten</span><span class="sxs-lookup"><span data-stu-id="f096d-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="f096d-158">tooshut omlaag een actieve virtuele machine met behulp van hello Azure Explorer in Eclipse Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="f096d-158">tooshut down a running virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="f096d-159">In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo virtuele machine en selecteer vervolgens **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="f096d-159">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![Hallo afsluitopdracht van virtuele machines][SH01]

2. <span data-ttu-id="f096d-161">Klik in het bevestigingsvenster hello, **Ja**.</span><span class="sxs-lookup"><span data-stu-id="f096d-161">In hello confirmation window, click **Yes**.</span></span>

   ![Hallo virtuele machines afsluiten bevestigingsvenster][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="f096d-163">Een virtuele machine in Eclipse verwijderen</span><span class="sxs-lookup"><span data-stu-id="f096d-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="f096d-164">een virtuele machine met behulp van hello Azure Explorer in Eclipse toodelete Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="f096d-164">toodelete a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="f096d-165">In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo virtuele machine en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="f096d-165">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![opdracht voor Hallo virtuele machines verwijderen][DE01]

2. <span data-ttu-id="f096d-167">Klik in het bevestigingsvenster hello, **Ja**.</span><span class="sxs-lookup"><span data-stu-id="f096d-167">In hello confirmation window, click **Yes**.</span></span>

   ![Hallo verwijderen van een virtuele machine bevestigingsvenster][DE02]

## <a name="next-steps"></a><span data-ttu-id="f096d-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f096d-169">Next steps</span></span>
<span data-ttu-id="f096d-170">Zie voor meer informatie over Azure grootten voor virtuele machines en prijzen Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="f096d-170">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="f096d-171">Azure grootten voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f096d-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="f096d-172">[Grootten voor Windows virtuele machines in Azure]</span><span class="sxs-lookup"><span data-stu-id="f096d-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="f096d-173">[Grootten voor virtuele Linux-machines in Azure]</span><span class="sxs-lookup"><span data-stu-id="f096d-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="f096d-174">Prijzen voor Azure virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f096d-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="f096d-175">[Prijzen van virtuele machines in Windows]</span><span class="sxs-lookup"><span data-stu-id="f096d-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="f096d-176">[Prijzen van Linux virtuele machines]</span><span class="sxs-lookup"><span data-stu-id="f096d-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="f096d-177">Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="f096d-177">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="f096d-178">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f096d-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f096d-179">[Wat is er nieuw in hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f096d-179">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f096d-180">[Hello Azure Toolkit voor Eclipse installeren]</span><span class="sxs-lookup"><span data-stu-id="f096d-180">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f096d-181">[aanmelden instructies voor het hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f096d-181">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f096d-182">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f096d-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="f096d-183">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f096d-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f096d-184">[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f096d-184">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f096d-185">[Hello Azure Toolkit voor IntelliJ installeren]</span><span class="sxs-lookup"><span data-stu-id="f096d-185">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f096d-186">[Aanmelden instructies voor hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f096d-186">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f096d-187">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f096d-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="f096d-188">Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="f096d-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

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

[Grootten voor Windows virtuele machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Grootten voor virtuele Linux-machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Prijzen van virtuele machines in Windows]: /pricing/details/virtual-machines/windows/
[Prijzen van Linux virtuele machines]: /pricing/details/virtual-machines/linux/

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
