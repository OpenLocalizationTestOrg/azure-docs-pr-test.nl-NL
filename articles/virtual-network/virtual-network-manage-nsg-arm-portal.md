---
title: aaaManage nsg's met behulp van hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toomanage bestaande hello Azure-portal met nsg's.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="1a387-103">Nsg's met Hallo portal beheren</span><span class="sxs-lookup"><span data-stu-id="1a387-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a387-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1a387-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="1a387-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a387-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="1a387-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="1a387-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="1a387-107">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1a387-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1a387-108">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a387-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="1a387-109">Informatie ophalen</span><span class="sxs-lookup"><span data-stu-id="1a387-109">Retrieve Information</span></span>
<span data-ttu-id="1a387-110">U kunt uw bestaande nsg's weergeven, regels voor een bestaande NSG ophalen en weten welke resources een NSG is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="1a387-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="1a387-111">Bestaande nsg's weergeven</span><span class="sxs-lookup"><span data-stu-id="1a387-111">View existing NSGs</span></span>

<span data-ttu-id="1a387-112">tooview alle bestaande nsg's in een abonnement, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a387-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-113">Navigeer via een browser toohttp://portal.azure.com en, indien nodig, meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="1a387-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="1a387-114">Klik op **Bladeren >** > **Netwerkbeveiligingsgroepen**.</span><span class="sxs-lookup"><span data-stu-id="1a387-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="1a387-116">Controleer Hallo lijst met nsg's in Hallo **Netwerkbeveiligingsgroepen** blade.</span><span class="sxs-lookup"><span data-stu-id="1a387-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="1a387-118">Nsg's weergeven in een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="1a387-118">View NSGs in a resource group</span></span>

<span data-ttu-id="1a387-119">tooview hello lijst met nsg's in Hallo **RG NSG** resourcegroep, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a387-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-120">Klik op **resourcegroepen >** > **RG NSG** > **...** .</span><span class="sxs-lookup"><span data-stu-id="1a387-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="1a387-122">In de lijst met resources Hallo zoeken naar objecten Hallo NSG pictogram weergegeven zoals in Hallo **Resources** blade hieronder.</span><span class="sxs-lookup"><span data-stu-id="1a387-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="1a387-124">Lijst met alle regels voor een NSG</span><span class="sxs-lookup"><span data-stu-id="1a387-124">List all rules for an NSG</span></span>

<span data-ttu-id="1a387-125">tooview hello regels van een NSG met de naam **NSG-FrontEnd**, volledige Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="1a387-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-126">Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="1a387-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="1a387-127">In Hallo **instellingen** tabblad **inkomende beveiligingsregels**.</span><span class="sxs-lookup"><span data-stu-id="1a387-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="1a387-129">Hallo **inkomende beveiligingsregels** blade wordt weergegeven zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1a387-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="1a387-131">In Hallo **instellingen** tabblad **uitgaande beveiligingsregels** toosee Hallo uitgaande regels.</span><span class="sxs-lookup"><span data-stu-id="1a387-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a387-132">Standaardregels tooview, klikt u op Hallo **regels standaard** pictogram Hallo boven aan het Hallo-blade waarmee de Hallo regels worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1a387-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="1a387-133">Nsg's koppelingen weergeven</span><span class="sxs-lookup"><span data-stu-id="1a387-133">View NSGs associations</span></span>

<span data-ttu-id="1a387-134">tooview welke resources Hallo **NSG-FrontEnd** NSG is met, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a387-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-135">Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="1a387-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="1a387-136">In Hallo **instellingen** tabblad **subnetten** tooview welke subnetten zijn toohello NSG die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="1a387-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="1a387-138">In Hallo **instellingen** tabblad **netwerkinterfaces** tooview wat NIC's gekoppeld zijn toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="1a387-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="1a387-139">Regels beheren</span><span class="sxs-lookup"><span data-stu-id="1a387-139">Manage rules</span></span>
<span data-ttu-id="1a387-140">U kunt regels tooan bestaande NSG toevoegen, bestaande regels bewerken en regels te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1a387-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="1a387-141">Een regel toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a387-141">Add a rule</span></span>
<span data-ttu-id="1a387-142">tooadd een regel waarmee **inkomende** verkeer tooport **443** van een machine toohello **NSG-FrontEnd** NSG, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a387-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-143">Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="1a387-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="1a387-144">In Hallo **instellingen** tabblad **inkomende beveiligingsregels**.</span><span class="sxs-lookup"><span data-stu-id="1a387-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="1a387-145">In Hallo **inkomende beveiligingsregels** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1a387-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="1a387-146">Klik op Hallo **de inkomende beveiligingsregel toevoegen** blade Hallo waarden doorvoeren, zoals hieronder wordt weergegeven en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1a387-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="1a387-148">Let na enkele seconden op nieuwe regel in Hallo Hallo **inkomende beveiligingsregels** blade.</span><span class="sxs-lookup"><span data-stu-id="1a387-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="1a387-150">Een regel wijzigen</span><span class="sxs-lookup"><span data-stu-id="1a387-150">Change a rule</span></span>
<span data-ttu-id="1a387-151">toochange hello regel bovenstaande tooallow binnenkomend verkeer van Hallo **Internet** alleen en volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a387-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-152">Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="1a387-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="1a387-153">In Hallo **instellingen** en klik op Hallo regel die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1a387-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="1a387-154">In Hallo **toestaan https** blade, wijziging Hallo **bron** eigenschap zoals hieronder wordt weergegeven en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1a387-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="1a387-156">Een regel verwijderen</span><span class="sxs-lookup"><span data-stu-id="1a387-156">Delete a rule</span></span>

<span data-ttu-id="1a387-157">toodelete hello regel hierboven gemaakte, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a387-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-158">Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="1a387-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="1a387-159">In Hallo **instellingen** en klik op Hallo regel die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1a387-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="1a387-160">In Hallo **toestaan https** blade, klikt u op **verwijderen**, en klik vervolgens op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="1a387-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="1a387-162">Koppelingen beheren</span><span class="sxs-lookup"><span data-stu-id="1a387-162">Manage associations</span></span>
<span data-ttu-id="1a387-163">U kunt een NSG toosubnets en NIC's kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="1a387-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="1a387-164">U kunt ook een NSG van elke bron die deze gekoppeld ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="1a387-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="1a387-165">Een NSG tooa NIC koppelen</span><span class="sxs-lookup"><span data-stu-id="1a387-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="1a387-166">Hallo tooassociate **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a387-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-167">Van Hallo **Netwerkbeveiligingsgroepen** blade of Hallo **Resources** blade hierboven, klikt u op **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="1a387-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="1a387-168">In Hallo **instellingen** tabblad **netwerkinterfaces** > **koppelen** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="1a387-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="1a387-170">Een NSG van een NIC ontkoppelen</span><span class="sxs-lookup"><span data-stu-id="1a387-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="1a387-171">Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **TestNICWeb1** NIC, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a387-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-172">Hallo Azure-portal, klik op **resourcegroepen >** > **RG NSG** > **...**   >  **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="1a387-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="1a387-173">In Hallo **TestNICWeb1** blade, klikt u op **beveiliging wijzigen...**   >  **Geen**.</span><span class="sxs-lookup"><span data-stu-id="1a387-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="1a387-175">U kunt ook deze blade tooassociate Hallo NIC tooany bestaande NSG gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a387-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="1a387-176">Een NSG van een subnet ontkoppelen</span><span class="sxs-lookup"><span data-stu-id="1a387-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="1a387-177">Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **FrontEnd** subnet, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a387-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-178">Hallo Azure-portal, klik op **resourcegroepen >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="1a387-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="1a387-179">In Hallo **instellingen** blade, klikt u op **subnetten** > **FrontEnd** > **netwerkbeveiligingsgroep**  >  **Geen**.</span><span class="sxs-lookup"><span data-stu-id="1a387-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="1a387-181">In Hallo **FrontEnd** blade, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1a387-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="1a387-183">Een NSG tooa subnet koppelen</span><span class="sxs-lookup"><span data-stu-id="1a387-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="1a387-184">Hallo tooassociate **NSG-FrontEnd** NSG toohello **FronEnd** opnieuw subnet, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1a387-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="1a387-185">Hallo Azure-portal, klik op **resourcegroepen >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="1a387-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="1a387-186">In Hallo **instellingen** blade, klikt u op **subnetten** > **FrontEnd** > **netwerkbeveiligingsgroep**  >  **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="1a387-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="1a387-187">In Hallo **FrontEnd** blade, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1a387-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="1a387-188">U kunt ook een subnet van de NSG tooa uit thh NSG van koppelen **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="1a387-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="1a387-189">Een NSG verwijderen</span><span class="sxs-lookup"><span data-stu-id="1a387-189">Delete an NSG</span></span>
<span data-ttu-id="1a387-190">U kunt een NSG alleen verwijderen als het tooany resource niet is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="1a387-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="1a387-191">toodelete een NSG, volledige Hallo volgende stappen uit:.</span><span class="sxs-lookup"><span data-stu-id="1a387-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="1a387-192">Hallo Azure-portal, klik op **resourcegroepen >** > **RG NSG** > **...**   >  **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="1a387-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="1a387-193">In Hallo **instellingen** blade, klikt u op **netwerkinterfaces**.</span><span class="sxs-lookup"><span data-stu-id="1a387-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="1a387-194">Als er NIC's die worden vermeld, klikt u op Hallo NIC en volgt u stap 2 in [ontkoppelen van een NSG van een NIC](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="1a387-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="1a387-195">Herhaal stap 3 voor elke NIC.</span><span class="sxs-lookup"><span data-stu-id="1a387-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="1a387-196">In Hallo **instellingen** blade, klikt u op **subnetten**.</span><span class="sxs-lookup"><span data-stu-id="1a387-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="1a387-197">Als er subnetten die worden vermeld, klikt u op Hallo subnet en volg de stappen 2 en 3 in [een NSG van een subnet ontkoppelen](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="1a387-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="1a387-198">Toohello links schuift **NSG-FrontEnd** blade, klikt u vervolgens op **verwijderen** > **Ja**.</span><span class="sxs-lookup"><span data-stu-id="1a387-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Azure portal - nsg 's](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="1a387-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a387-200">Next steps</span></span>
* <span data-ttu-id="1a387-201">[Logboekregistratie inschakelen](virtual-network-nsg-manage-log.md) voor nsg's.</span><span class="sxs-lookup"><span data-stu-id="1a387-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
