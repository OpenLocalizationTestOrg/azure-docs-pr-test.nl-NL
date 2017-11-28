---
title: "aaaConfigure privé IP-adressen voor virtuele machines (klassiek) - Azure-portal | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure privé IP-adressen voor virtuele machines (klassiek) met hello Azure-portal."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="516f6-103">Privé IP-adressen voor een virtuele machine (klassiek) met behulp van hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="516f6-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="516f6-104">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="516f6-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="516f6-105">U kunt ook [een statisch privé IP-adres in Hallo Resource Manager-implementatiemodel beheren](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="516f6-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="516f6-106">Hallo voorbeeld volgt verwacht een eenvoudige omgeving al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="516f6-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="516f6-107">Als u toorun Hallo stappen wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een vnet maken](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="516f6-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="516f6-108">Hoe toospecify een statisch privé IP-adres bij het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="516f6-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="516f6-109">een virtuele machine met de naam toocreate *DNS01* in Hallo *FrontEnd* subnet van een VNet met de naam *TestVNet* met een statisch privé IP-adres van *192.168.1.101*, Volg onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="516f6-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="516f6-110">Navigeer via een browser toohttp://portal.azure.com en, indien nodig, meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="516f6-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="516f6-111">Klik op **nieuw** > **Compute** > **Windows Server 2012 R2 Datacenter**, zoals u ziet dat Hallo **een implementatiemodelselecteren** lijst al staat **klassieke**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="516f6-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="516f6-113">In Hallo **VM maken** blade Voer Hallo-naam van Hallo VM toobe gemaakt (*DNS01* in ons scenario), Hallo lokale administrator-account en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="516f6-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="516f6-115">Klik op **optionele configuratie** > **netwerk** > **virtueel netwerk**, en klik vervolgens op **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="516f6-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="516f6-116">Als **TestVNet** is niet beschikbaar is, zorg ervoor dat u gebruikmaakt van Hallo *VS-midden* locatie en het Hallo-testomgeving beschreven op Hallo begin van dit artikel hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="516f6-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="516f6-118">In Hallo **netwerk** blade, zorg ervoor dat Hallo subnet geselecteerde is *FrontEnd*, klikt u vervolgens op **IP-adressen**onder **IP-adrestoewijzing** klikt u op **statische**, en voer vervolgens *192.168.1.101* voor **IP-adres** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="516f6-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="516f6-120">Klik op **OK** in Hallo **IP-adressen** blade, klikt u vervolgens op **OK** in Hallo **netwerk** blade en klik op **OK**in Hallo **optionele configuratie** blade.</span><span class="sxs-lookup"><span data-stu-id="516f6-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="516f6-121">In Hallo **VM maken** blade, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="516f6-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="516f6-122">Kennisgeving Hallo tegel hieronder weergegeven in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="516f6-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="516f6-124">Hoe de gegevens voor een VM voor het adres van tooretrieve statische privé-IP</span><span class="sxs-lookup"><span data-stu-id="516f6-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="516f6-125">tooview Hallo statisch privé IP-adresgegevens voor Hallo VM gemaakt met de bovenstaande stappen voor Hallo Hallo onderstaande stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="516f6-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="516f6-126">Vanuit hello Azure Azure portal, klikt u op **door alles bladeren** > **virtuele machines (klassiek)** > **DNS01**  >   **Alle instellingen** > **IP-adressen** en Let op Hallo van IP-adrestoewijzing en IP-adres, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="516f6-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="516f6-128">Hoe tooremove een statisch privé IP-adres van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="516f6-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="516f6-129">tooremove Hallo statisch privé IP-adres van VM gemaakt, Hallo Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="516f6-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="516f6-130">Van Hallo **IP-adressen** blade hierboven, klikt u op **dynamische** toohello rechts van **IP-adrestoewijzing**, klikt u vervolgens op **opslaan**, en vervolgens Klik op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="516f6-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Virtuele machine maken in Azure-portal](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="516f6-132">Hoe tooadd een statische privé-IP adres tooan bestaande VM</span><span class="sxs-lookup"><span data-stu-id="516f6-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="516f6-133">een statisch privé IP-adres toohello VM gemaakt met behulp van Hallo de bovenstaande stappen tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="516f6-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="516f6-134">Van Hallo **IP-adressen** blade hierboven, klikt u op **statische** toohello rechts van **IP-adrestoewijzing**.</span><span class="sxs-lookup"><span data-stu-id="516f6-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="516f6-135">Type *192.168.1.101* voor **IP-adres**, klikt u vervolgens op **opslaan**, en klik vervolgens op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="516f6-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="516f6-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="516f6-136">Next steps</span></span>
* <span data-ttu-id="516f6-137">Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="516f6-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="516f6-138">Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="516f6-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="516f6-139">Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="516f6-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

