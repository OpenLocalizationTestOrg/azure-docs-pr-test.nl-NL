---
title: "aaaConfigure privé IP-adressen voor virtuele machines - Azure-portal | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure privé IP-adressen voor virtuele machines met hello Azure-portal."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="c0f49-103">Privé IP-adressen voor een virtuele machine met behulp van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="c0f49-103">Configure private IP addresses for a virtual machine using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0f49-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c0f49-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="c0f49-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0f49-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="c0f49-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="c0f49-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="c0f49-107">Azure-portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="c0f49-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="c0f49-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="c0f49-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="c0f49-109">Azure CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="c0f49-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c0f49-110">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="c0f49-110">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="c0f49-111">U kunt ook [statisch privé IP-adres in het klassieke implementatiemodel Hallo beheren](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c0f49-111">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="c0f49-112">Hallo voorbeeld volgt verwacht een eenvoudige omgeving al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c0f49-112">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="c0f49-113">Als u toorun Hallo stappen wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een vnet maken](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c0f49-113">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="c0f49-114">Hoe toocreate een virtuele machine voor het testen van statische privé-IP-adressen</span><span class="sxs-lookup"><span data-stu-id="c0f49-114">How toocreate a VM for testing static private IP addresses</span></span>
<span data-ttu-id="c0f49-115">U kunt een statisch privé IP-adres niet instellen tijdens het maken van een virtuele machine in de modus voor Resource Manager deployment Hallo Hallo via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c0f49-115">You cannot set a static private IP address during hello creation of a VM in hello Resource Manager deployment mode by using hello Azure portal.</span></span> <span data-ttu-id="c0f49-116">U moet eerst Hallo VM maken, tehn stelt de privé IP-toobe statische.</span><span class="sxs-lookup"><span data-stu-id="c0f49-116">You must create hello VM first, tehn set its private IP toobe static.</span></span>

<span data-ttu-id="c0f49-117">een virtuele machine met de naam toocreate *DNS01* in Hallo *FrontEnd* subnet van een VNet met de naam *TestVNet*, volgt u onderstaande stappen voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0f49-117">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet*, follow hello steps below.</span></span>

1. <span data-ttu-id="c0f49-118">Navigeer via een browser toohttp://portal.azure.com en, indien nodig, meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c0f49-118">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="c0f49-119">Klik op **nieuw** > **Compute** > **Windows Server 2012 R2 Datacenter**, zoals u ziet dat Hallo **een implementatiemodelselecteren** lijst al staat **Resource Manager**, en klik vervolgens op **maken**, zoals in onderstaande afbeelding ziet Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0f49-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="c0f49-121">In Hallo **basisbeginselen** blade Voer Hallo-naam van Hallo VM toobe gemaakt (*DNS01* in ons scenario), Hallo lokale administrator-account en wachtwoord, zoals weergegeven in onderstaande afbeelding ziet Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0f49-121">In hello **Basics** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password, as seen in hello figure below.</span></span>
   
    ![Blade Grondbeginselen](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="c0f49-123">Zorg ervoor dat Hallo **locatie** geselecteerd is *VS-midden*, klikt u vervolgens op **Selecteer een bestaande** onder **resourcegroep**, klikt u vervolgens op **Resourcegroep** opnieuw in en klik vervolgens op *TestRG*, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0f49-123">Make sure hello **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Blade Grondbeginselen](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="c0f49-125">In Hallo **een grootte kiezen** blade Selecteer **A1 standaard**, en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="c0f49-125">In hello **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Kies een blade grootte](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="c0f49-127">In de **instellingen** blade, zorg ervoor dat Hallo volgende eigenschappen worden ingesteld met de onderstaande Hallo-waarden zijn ingesteld en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0f49-127">In teh **Settings** blade, make sure hello following properties are set are set with hello values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="c0f49-128">-**Storage-account**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="c0f49-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="c0f49-129">**Netwerk**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="c0f49-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="c0f49-130">**Subnet**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="c0f49-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Kies een blade grootte](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="c0f49-132">In Hallo **samenvatting** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0f49-132">In hello **Summary** blade, click **OK**.</span></span> <span data-ttu-id="c0f49-133">Kennisgeving Hallo tegel hieronder weergegeven in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="c0f49-133">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="c0f49-135">Hoe de gegevens voor een VM voor het adres van tooretrieve statische privé-IP</span><span class="sxs-lookup"><span data-stu-id="c0f49-135">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="c0f49-136">tooview Hallo statisch privé IP-adresgegevens voor Hallo VM gemaakt met de bovenstaande stappen voor Hallo Hallo onderstaande stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c0f49-136">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="c0f49-137">Vanuit hello Azure Azure portal, klikt u op **door alles bladeren** > **virtuele machines** > **DNS01** > **alle instellingen** > **netwerkinterfaces** en klik vervolgens op Hallo alleen netwerkinterface vermeld.</span><span class="sxs-lookup"><span data-stu-id="c0f49-137">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on hello only network interface listed.</span></span>
   
    ![VM-tegel implementeren](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="c0f49-139">In Hallo **netwerkinterface** blade, klikt u op **alle instellingen** > **IP-adressen** en kennisgeving Hallo **toewijzing** en **IP-adres** waarden.</span><span class="sxs-lookup"><span data-stu-id="c0f49-139">In hello **Network interface** blade, click **All settings** > **IP addresses** and notice hello **Assignment** and **IP address** values.</span></span>
   
    ![VM-tegel implementeren](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="c0f49-141">Hoe tooadd een statische privé-IP adres tooan bestaande VM</span><span class="sxs-lookup"><span data-stu-id="c0f49-141">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="c0f49-142">een statisch privé IP-adres toohello VM gemaakt met behulp van Hallo de bovenstaande stappen tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="c0f49-142">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="c0f49-143">Van Hallo **IP-adressen** blade hierboven, klikt u op **statische** onder **toewijzing**.</span><span class="sxs-lookup"><span data-stu-id="c0f49-143">From hello **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="c0f49-144">Type *192.168.1.101* voor **IP-adres**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c0f49-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="c0f49-146">Als na het klikken op **opslaan** merkt u Hallo toewijzing nog steeds te ingesteld**dynamische**, betekent dit Hallo opgegeven IP-adres is al in gebruik.</span><span class="sxs-lookup"><span data-stu-id="c0f49-146">If after clicking **Save** you notice that hello assignment is still set too**Dynamic**, it means that hello IP address you typed is already in use.</span></span> <span data-ttu-id="c0f49-147">Probeer een ander IP-adres.</span><span class="sxs-lookup"><span data-stu-id="c0f49-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="c0f49-148">Hoe tooremove een statisch privé IP-adres van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c0f49-148">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="c0f49-149">tooremove Hallo statisch privé IP-adres van VM gemaakt, Hallo Hallo stap voltooien:</span><span class="sxs-lookup"><span data-stu-id="c0f49-149">tooremove hello static private IP address from hello VM created above, complete hello following step:</span></span>

<span data-ttu-id="c0f49-150">Van Hallo **IP-adressen** blade hierboven, klikt u op **dynamische** onder **toewijzing**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c0f49-150">From hello **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0f49-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c0f49-151">Next steps</span></span>
* <span data-ttu-id="c0f49-152">Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="c0f49-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="c0f49-153">Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="c0f49-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="c0f49-154">Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0f49-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

