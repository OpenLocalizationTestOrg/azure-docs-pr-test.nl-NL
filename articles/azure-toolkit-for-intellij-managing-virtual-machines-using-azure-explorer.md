---
title: aaaManage virtuele machines met behulp van hello Azure Explorer voor IntelliJ | Microsoft Docs
description: Meer informatie over hoe toomanage uw virtuele machines in Azure met behulp van hello Azure Explorer voor IntelliJ.
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
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="c31db-103">Virtuele machines beheren met behulp van hello Azure Explorer voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c31db-103">Manage virtual machines by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="c31db-104">Hello Azure Explorer, die deel van hello Azure Toolkit voor IntelliJ uitmaakt, Java-ontwikkelaars met een eenvoudig-en-klare oplossing biedt voor het beheren van virtuele machines in de Azure-account uit binnen Hallo IntelliJ integrated development environment (IDE).</span><span class="sxs-lookup"><span data-stu-id="c31db-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="c31db-105">Een virtuele machine maken in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c31db-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c31db-106">een virtuele machine met behulp van hello Azure Explorer toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c31db-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span> 

1. <span data-ttu-id="c31db-107">Meld u aan tooyour Azure-account met behulp van Hallo stappen in Hallo [aanmelden instructies voor hello Azure Toolkit voor IntelliJ] artikel.</span><span class="sxs-lookup"><span data-stu-id="c31db-107">Sign in tooyour Azure account by using hello steps in hello [Sign-in instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="c31db-108">In Hallo **Azure Explorer** weergeven, vouwt u Hallo **Azure** knooppunt met de rechtermuisknop op **virtuele Machines**, en klik vervolgens op **VM maken**.</span><span class="sxs-lookup"><span data-stu-id="c31db-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="c31db-109">![Hallo opdracht VM maken][CR01]</span><span class="sxs-lookup"><span data-stu-id="c31db-109">![hello Create VM command][CR01]</span></span>  
    <span data-ttu-id="c31db-110">Hallo **nieuwe virtuele Machine maken** wizard wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c31db-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="c31db-111">In Hallo **Kies een abonnement** venster uw abonnement te selecteren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c31db-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Kies een abonnement venster Hallo][CR02]

4. <span data-ttu-id="c31db-113">In Hallo **selecteert u de installatiekopie van een virtuele Machine** venster Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c31db-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="c31db-114">**Locatie**: Hiermee geeft u op waar uw virtuele machine wordt gemaakt (bijvoorbeeld *VS-West*).</span><span class="sxs-lookup"><span data-stu-id="c31db-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="c31db-115">**Afbeelding aanbevolen**: Hiermee geeft u op dat u een installatiekopie van een verkorte lijst van veelgebruikte installatiekopieën kiest.</span><span class="sxs-lookup"><span data-stu-id="c31db-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="c31db-116">**Aangepaste installatiekopie**: Hiermee geeft u een aangepaste installatiekopie dankzij de volgende informatie hello te kiezen:</span><span class="sxs-lookup"><span data-stu-id="c31db-116">**Custom image**: Specifies that you will choose a custom image by providing hello following information:</span></span>

      * <span data-ttu-id="c31db-117">**Publisher**: Hiermee geeft u op Hallo publisher dat Hallo-installatiekopie die u voor uw virtuele machine gebruiken wilt gemaakt (bijvoorbeeld *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="c31db-117">**Publisher**: Specifies hello publisher that created hello image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="c31db-118">**Bieden**: Hiermee geeft u op Hallo virtuele machine toouse aanbieding van de geselecteerde uitgever Hallo (bijvoorbeeld *JDK*).</span><span class="sxs-lookup"><span data-stu-id="c31db-118">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="c31db-119">**SKU**: Hiermee geeft u op Hallo SKU (SKU's) toouse van de geselecteerde serviceaanbieding Hallo (bijvoorbeeld *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="c31db-119">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="c31db-120">**Versie #**: Hiermee geeft u op welke versie van Hallo geselecteerd SKU toouse.</span><span class="sxs-lookup"><span data-stu-id="c31db-120">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

   ![Hallo selecteert u het venster van een installatiekopie van virtuele Machine][CR03]

5. <span data-ttu-id="c31db-122">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c31db-122">Click **Next**.</span></span> 

6. <span data-ttu-id="c31db-123">In Hallo **basisinstellingen van de virtuele Machine** venster Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c31db-123">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="c31db-124">**Naam van virtuele machine**: Hiermee geeft u de naam Hallo voor uw nieuwe virtuele machine die moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes.</span><span class="sxs-lookup"><span data-stu-id="c31db-124">**Virtual machine name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="c31db-125">**De grootte van**: Hiermee geeft u Hallo aantal kernen en geheugen tooallocate voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c31db-125">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="c31db-126">**Gebruikersnaam**: Hiermee geeft u op Hallo beheerder account toocreate voor het beheren van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c31db-126">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="c31db-127">**Wachtwoord** en **bevestigen**: Hallo wachtwoord voor uw beheerdersaccount.</span><span class="sxs-lookup"><span data-stu-id="c31db-127">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

   ![Hallo basisinstellingen van de virtuele Machine venster][CR04]

7. <span data-ttu-id="c31db-129">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c31db-129">Click **Next**.</span></span> 

8. <span data-ttu-id="c31db-130">In Hallo **Resources die zijn gekoppeld** venster Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c31db-130">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="c31db-131">**Resourcegroep**: Hiermee geeft u de resourcegroep Hallo voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c31db-131">**Resource group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="c31db-132">Selecteer een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="c31db-132">Select one of hello following options:</span></span>
      * <span data-ttu-id="c31db-133">**Maken van nieuwe**: geeft aan dat u wilt dat toocreate een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c31db-133">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="c31db-134">**Gebruik bestaande**: geeft aan dat u wilt tooselect uit een lijst met resourcegroepen die gekoppeld aan uw Azure-account zijn.</span><span class="sxs-lookup"><span data-stu-id="c31db-134">**Use existing**: Specifies that you want tooselect from a list of resource groups that are associated with your Azure account.</span></span>

       ![venster van de Resources die zijn gekoppeld Hallo][CR07]

   * <span data-ttu-id="c31db-136">**Storage-account**: Hiermee geeft u op Hallo storage account toouse voor het opslaan van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c31db-136">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="c31db-137">U kunt ervoor kiezen een bestaand opslagaccount of maak een nieuw account.</span><span class="sxs-lookup"><span data-stu-id="c31db-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="c31db-138">Als u ervoor kiest **nieuw**, Hallo volgen in het dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="c31db-138">If you choose **Create New**, hello following dialog box appears:</span></span>

      ![dialoogvenster Hallo-Storage-Account maken][CR05]

   * <span data-ttu-id="c31db-140">**Virtueel netwerk** en **Subnet**: Hiermee geeft u op Hallo virtueel netwerk en subnet dat uw virtuele machine maakt verbinding met.</span><span class="sxs-lookup"><span data-stu-id="c31db-140">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="c31db-141">U kunt een bestaand netwerk en subnet of kunt u een nieuw netwerk en subnet.</span><span class="sxs-lookup"><span data-stu-id="c31db-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="c31db-142">Als u selecteert **nieuw**, Hallo volgen in het dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="c31db-142">If you select **Create new**, hello following dialog box appears:</span></span>

      ![dialoogvenster voor Hallo virtueel netwerk maken][CR06]

   * <span data-ttu-id="c31db-144">**Openbaar IP-adres**: Hiermee geeft u een extern gerichte IP-adres voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c31db-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="c31db-145">U kunt toocreate een nieuw IP-adres of, als uw virtuele machine een openbaar IP-adres niet hebt wordt, kunt u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="c31db-145">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="c31db-146">**Netwerkbeveiligingsgroep**: Hiermee geeft u een optionele netwerken firewall voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c31db-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="c31db-147">Kunt u een firewall of, als uw virtuele machine niet voor een netwerkfirewall gebruikt wordt, kunt u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="c31db-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="c31db-148">**Beschikbaarheidsset**: Hiermee geeft u een optionele beschikbaarheidsset dat deel van uw virtuele machine uitmaken kunnen.</span><span class="sxs-lookup"><span data-stu-id="c31db-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="c31db-149">U kunt een bestaande beschikbaarheidsset, een nieuwe beschikbaarheidsset maken of, als uw virtuele machine geen deel van tooan beschikbaarheidsset uitmaakt, selecteert u **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="c31db-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong tooan availability set, select **(None)**.</span></span>

9. <span data-ttu-id="c31db-150">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c31db-150">Click **Finish**.</span></span>  
    <span data-ttu-id="c31db-151">Uw nieuwe virtuele machine weergegeven in hello Azure Explorer hulpprogramma venster.</span><span class="sxs-lookup"><span data-stu-id="c31db-151">Your new virtual machine appears in hello Azure Explorer tool window.</span></span> 

   ![Nieuwe virtuele machine in hello Azure Verkenner-weergave][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="c31db-153">Opnieuw opstarten van een virtuele machine in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c31db-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c31db-154">een virtuele machine met behulp van hello Azure Explorer in IntelliJ, toorestart Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c31db-154">toorestart a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="c31db-155">In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo virtuele machine en selecteer vervolgens **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="c31db-155">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![de opdracht Hallo virtuele machines opnieuw starten][RE01]

2. <span data-ttu-id="c31db-157">Klik in het bevestigingsvenster hello, **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c31db-157">In hello confirmation window, click **Yes**.</span></span> 

   ![Hallo bevestigingsvenster van de virtuele machine opnieuw opstarten][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="c31db-159">Een virtuele machine in IntelliJ afsluiten</span><span class="sxs-lookup"><span data-stu-id="c31db-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c31db-160">tooshut omlaag een actieve virtuele machine met behulp van hello Azure Explorer in IntelliJ, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c31db-160">tooshut down a running virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="c31db-161">In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo virtuele machine en selecteer vervolgens **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="c31db-161">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![Hallo afsluitopdracht van virtuele machines][SH01]

2. <span data-ttu-id="c31db-163">Klik in het bevestigingsvenster hello, **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c31db-163">In hello confirmation window, click **Yes**.</span></span> 

   ![Hallo bevestigingsvenster van de virtuele machine afsluiten][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="c31db-165">Een virtuele machine in IntelliJ verwijderen</span><span class="sxs-lookup"><span data-stu-id="c31db-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c31db-166">een virtuele machine met behulp van hello Azure Explorer in IntelliJ, toodelete Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c31db-166">toodelete a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="c31db-167">In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo virtuele machine en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c31db-167">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![opdracht voor Hallo virtuele machines verwijderen][DE01]

2. <span data-ttu-id="c31db-169">Klik in het bevestigingsvenster hello, **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c31db-169">In hello confirmation window, click **Yes**.</span></span> 

   ![Hallo bevestigingsvenster van de virtuele machine verwijderen][DE02]

## <a name="next-steps"></a><span data-ttu-id="c31db-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c31db-171">Next steps</span></span>
<span data-ttu-id="c31db-172">Zie voor meer informatie over Azure grootten voor virtuele machines en prijzen Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="c31db-172">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="c31db-173">Azure grootten voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="c31db-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="c31db-174">[Grootten voor Windows virtuele machines in Azure]</span><span class="sxs-lookup"><span data-stu-id="c31db-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="c31db-175">[Grootten voor virtuele Linux-machines in Azure]</span><span class="sxs-lookup"><span data-stu-id="c31db-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="c31db-176">Prijzen voor Azure virtuele machines</span><span class="sxs-lookup"><span data-stu-id="c31db-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="c31db-177">[Prijzen van virtuele machines in Windows]</span><span class="sxs-lookup"><span data-stu-id="c31db-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="c31db-178">[Prijzen van Linux virtuele machines]</span><span class="sxs-lookup"><span data-stu-id="c31db-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="c31db-179">Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="c31db-179">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="c31db-180">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c31db-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c31db-181">[Wat is er nieuw in hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c31db-181">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c31db-182">[Hello Azure Toolkit voor Eclipse installeren]</span><span class="sxs-lookup"><span data-stu-id="c31db-182">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c31db-183">[Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c31db-183">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c31db-184">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c31db-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="c31db-185">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c31db-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c31db-186">[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c31db-186">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c31db-187">[Hello Azure Toolkit voor IntelliJ installeren]</span><span class="sxs-lookup"><span data-stu-id="c31db-187">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c31db-188">[aanmelden instructies voor hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c31db-188">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c31db-189">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c31db-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="c31db-190">Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="c31db-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Azure Toolkit voor Eclipse installeren]: ./azure-toolkit-for-eclipse-installation.md
[Hello Azure Toolkit voor IntelliJ installeren]: ./azure-toolkit-for-intellij-installation.md
[Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[aanmelden instructies voor hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

[Grootten voor Windows virtuele machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Grootten voor virtuele Linux-machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Prijzen van virtuele machines in Windows]: /pricing/details/virtual-machines/windows/
[Prijzen van Linux virtuele machines]: /pricing/details/virtual-machines/linux/


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
