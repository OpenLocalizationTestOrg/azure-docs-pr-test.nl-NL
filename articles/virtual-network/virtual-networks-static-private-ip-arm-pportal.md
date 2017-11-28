---
title: "Privé IP-adressen voor virtuele machines - Azure-portal configureren | Microsoft Docs"
description: "Informatie over het configureren van privé IP-adressen voor virtuele machines met de Azure-portal."
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
ms.openlocfilehash: 672462fad715758e50680fa5bade4b1f9d50e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="4fab8-103">Privé IP-adressen voor een virtuele machine met de Azure portal configureren</span><span class="sxs-lookup"><span data-stu-id="4fab8-103">Configure private IP addresses for a virtual machine using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fab8-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4fab8-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="4fab8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fab8-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="4fab8-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="4fab8-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="4fab8-107">Azure-portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="4fab8-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="4fab8-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="4fab8-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="4fab8-109">Azure CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="4fab8-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="4fab8-110">Dit artikel is van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="4fab8-110">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="4fab8-111">U kunt ook [statisch privé IP-adres in het klassieke implementatiemodel beheren](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="4fab8-111">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="4fab8-112">De volgende stappen uit het voorbeeld verwacht een eenvoudige omgeving al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4fab8-112">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="4fab8-113">Als u wilt de stappen uitvoeren, zoals ze worden weergegeven in dit document, eerst de testomgeving wordt beschreven in bouwen [een vnet maken](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="4fab8-113">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-to-create-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="4fab8-114">Het maken van een virtuele machine voor het testen van statisch privé IP-adressen</span><span class="sxs-lookup"><span data-stu-id="4fab8-114">How to create a VM for testing static private IP addresses</span></span>
<span data-ttu-id="4fab8-115">U kunt een statisch privé IP-adres niet instellen tijdens het maken van een virtuele machine in de implementatiemodus Resource Manager-met behulp van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4fab8-115">You cannot set a static private IP address during the creation of a VM in the Resource Manager deployment mode by using the Azure portal.</span></span> <span data-ttu-id="4fab8-116">U moet eerst de virtuele machine maken, tehn stelt u de privé-IP statisch.</span><span class="sxs-lookup"><span data-stu-id="4fab8-116">You must create the VM first, tehn set its private IP to be static.</span></span>

<span data-ttu-id="4fab8-117">Maken van een virtuele machine met de naam *DNS01* in de *FrontEnd* subnet van een VNet met de naam *TestVNet*, volg de onderstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="4fab8-117">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet*, follow the steps below.</span></span>

1. <span data-ttu-id="4fab8-118">Navigeer via een browser naar http://portal.azure.com en log, indien nodig, in met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="4fab8-118">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="4fab8-119">Klik op **nieuw** > **Compute** > **Windows Server 2012 R2 Datacenter**, zoals u ziet de **een implementatiemodel selecteren** lijst al staat **Resource Manager**, en klik vervolgens op **maken**, zoals in de afbeelding hieronder.</span><span class="sxs-lookup"><span data-stu-id="4fab8-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in the figure below.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="4fab8-121">In de **basisbeginselen** blade, voer de naam van de virtuele machine moet worden gemaakt (*DNS01* in ons scenario), wordt het lokale administrator-account en wachtwoord, zoals te zien is in de afbeelding hieronder.</span><span class="sxs-lookup"><span data-stu-id="4fab8-121">In the **Basics** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password, as seen in the figure below.</span></span>
   
    ![Blade Grondbeginselen](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="4fab8-123">Zorg ervoor dat de **locatie** geselecteerd is *VS-midden*, klikt u vervolgens op **Selecteer een bestaande** onder **resourcegroep**, klikt u vervolgens op **resourcegroep** opnieuw in en klik vervolgens op *TestRG*, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fab8-123">Make sure the **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Blade Grondbeginselen](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="4fab8-125">In de **een grootte kiezen** blade Selecteer **A1 standaard**, en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="4fab8-125">In the **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Kies een blade grootte](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="4fab8-127">In de **instellingen** blade, zorg ervoor dat de volgende eigenschappen worden ingesteld met de onderstaande waarden zijn ingesteld en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fab8-127">In teh **Settings** blade, make sure the following properties are set are set with the values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="4fab8-128">-**Storage-account**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="4fab8-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="4fab8-129">**Netwerk**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="4fab8-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="4fab8-130">**Subnet**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="4fab8-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Kies een blade grootte](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="4fab8-132">In de **samenvatting** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fab8-132">In the **Summary** blade, click **OK**.</span></span> <span data-ttu-id="4fab8-133">Let op de tegel weergegeven in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="4fab8-133">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="4fab8-135">Het statische privé IP-adresgegevens voor een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="4fab8-135">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="4fab8-136">Als u wilt weergeven in het statische privé IP-adresgegevens voor de virtuele machine gemaakt met de bovenstaande stappen, de onderstaande stappen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4fab8-136">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="4fab8-137">Klik in het Azure-Azure-portal op **door alles bladeren** > **virtuele machines** > **DNS01** > **alle instellingen** > **netwerkinterfaces** en klik vervolgens op de alleen-netwerkinterface vermeld.</span><span class="sxs-lookup"><span data-stu-id="4fab8-137">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on the only network interface listed.</span></span>
   
    ![VM-tegel implementeren](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="4fab8-139">In de **netwerkinterface** blade, klikt u op **alle instellingen** > **IP-adressen** en Let op de **toewijzing** en **IP-adres** waarden.</span><span class="sxs-lookup"><span data-stu-id="4fab8-139">In the **Network interface** blade, click **All settings** > **IP addresses** and notice the **Assignment** and **IP address** values.</span></span>
   
    ![VM-tegel implementeren](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="4fab8-141">Een statisch privé IP-adres toevoegen aan een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="4fab8-141">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="4fab8-142">Als een statisch privé IP-adres aan de virtuele machine gemaakt met behulp van de bovenstaande stappen toevoegen, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="4fab8-142">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="4fab8-143">Van de **IP-adressen** blade hierboven, klikt u op **statische** onder **toewijzing**.</span><span class="sxs-lookup"><span data-stu-id="4fab8-143">From the **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="4fab8-144">Type *192.168.1.101* voor **IP-adres**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4fab8-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="4fab8-146">Als na klikken **opslaan** merkt u dat de toewijzing nog is ingesteld op **dynamische**, betekent dit dat het opgegeven IP-adres al in gebruik is.</span><span class="sxs-lookup"><span data-stu-id="4fab8-146">If after clicking **Save** you notice that the assignment is still set to **Dynamic**, it means that the IP address you typed is already in use.</span></span> <span data-ttu-id="4fab8-147">Probeer een ander IP-adres.</span><span class="sxs-lookup"><span data-stu-id="4fab8-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="4fab8-148">Een statisch privé IP-adres van een virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="4fab8-148">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="4fab8-149">Als u wilt verwijderen van het statische privé IP-adres van de virtuele machine die eerder is gemaakt, voert u de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="4fab8-149">To remove the static private IP address from the VM created above, complete the following step:</span></span>

<span data-ttu-id="4fab8-150">Van de **IP-adressen** blade hierboven, klikt u op **dynamische** onder **toewijzing**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4fab8-150">From the **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fab8-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4fab8-151">Next steps</span></span>
* <span data-ttu-id="4fab8-152">Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="4fab8-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="4fab8-153">Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="4fab8-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="4fab8-154">Raadpleeg de [gereserveerd IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="4fab8-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

