---
title: Netwerkbeveiligingsgroepen - Azure-portal beheren | Microsoft Docs
description: Informatie over het beheren van netwerkbeveiligingsgroepen met de Azure portal.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ecb4fb4608628f5a1bd54fac6af19fecfa4508f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="3bf04-103">Netwerkbeveiligingsgroepen met de Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="3bf04-103">Manage network security groups using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="3bf04-104">Dit artikel is van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3bf04-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="3bf04-105">U kunt ook [nsg's maken in het klassieke implementatiemodel](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3bf04-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="3bf04-106">Het voorbeeld PowerShell onderstaande opdrachten een eenvoudige omgeving al gemaakt verwacht op basis van de bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="3bf04-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="3bf04-107">Als u wilt de opdrachten uitvoeren zoals ze worden weergegeven in dit document, moet u eerst de testomgeving verder door de implementatie [deze sjabloon](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), klikt u op **implementeren in Azure**, vervangt u de standaardwaarden voor parameters indien nodig en volg de instructies in de portal.</span><span class="sxs-lookup"><span data-stu-id="3bf04-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="3bf04-108">De stappen hieronder gebruik **RG NSG** als de naam van de resourcegroep voor de sjabloon is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3bf04-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span></span>

## <a name="create-the-nsg-frontend-nsg"></a><span data-ttu-id="3bf04-109">Het NSG NSG-FrontEnd maken</span><span class="sxs-lookup"><span data-stu-id="3bf04-109">Create the NSG-FrontEnd NSG</span></span>
<span data-ttu-id="3bf04-110">Maken van de **NSG-FrontEnd** NSG zoals weergegeven in het bovenstaande scenario Volg de onderstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="3bf04-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="3bf04-111">Navigeer via een browser naar http://portal.azure.com en log, indien nodig, in met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="3bf04-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="3bf04-112">Klik op **Bladeren >** > **Netwerkbeveiligingsgroepen**.</span><span class="sxs-lookup"><span data-stu-id="3bf04-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Azure portal - nsg 's](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="3bf04-114">In de **Netwerkbeveiligingsgroepen** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3bf04-114">In the **Network security groups** blade, click **Add**.</span></span>
   
    ![Azure portal - nsg 's](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="3bf04-116">In de **netwerkbeveiligingsgroep maken** blade maken van een NSG met de naam *NSG-FrontEnd* in de *RG NSG* resourcegroep en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="3bf04-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Azure portal - nsg 's](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="3bf04-118">Regels maken in een bestaande NSG</span><span class="sxs-lookup"><span data-stu-id="3bf04-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="3bf04-119">Voor het maken van regels in een bestaande NSG vanuit de Azure-portal, de volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3bf04-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span></span>

1. <span data-ttu-id="3bf04-120">Klik op **Bladeren >** > **Netwerkbeveiligingsgroepen**.</span><span class="sxs-lookup"><span data-stu-id="3bf04-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="3bf04-121">Klik in de lijst van nsg's op **NSG-FrontEnd** > **beveiligingsregels voor binnenkomende verbindingen**</span><span class="sxs-lookup"><span data-stu-id="3bf04-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Azure portal - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="3bf04-123">In de lijst met **inkomende beveiligingsregels**, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3bf04-123">In the list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Azure-portal - regel toevoegen](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="3bf04-125">In de **de inkomende beveiligingsregel toevoegen** blade maken van een regel met naam *web regel* met de prioriteit van *200* toegang via *TCP* op poort *80* naar een virtuele machine uit een bron en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3bf04-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span></span> <span data-ttu-id="3bf04-126">U ziet dat de meeste van deze instellingen standaardwaarden al.</span><span class="sxs-lookup"><span data-stu-id="3bf04-126">Notice that most of these settings are default values already.</span></span>
   
    ![Azure portal - instellingen van de regel](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="3bf04-128">Na enkele seconden ziet u de nieuwe regel in de NSG.</span><span class="sxs-lookup"><span data-stu-id="3bf04-128">After a few seconds you will see the new rule in the NSG.</span></span>
   
    ![Azure portal - nieuwe regel](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="3bf04-130">Herhaal stap 6 voor het maken van een inkomende regel met de naam *rdp-regel* met een prioriteit van *250* toegang via *TCP* op poort *3389* naar een virtuele machine uit een andere bron.</span><span class="sxs-lookup"><span data-stu-id="3bf04-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span></span>

## <a name="associate-the-nsg-to-the-frontend-subnet"></a><span data-ttu-id="3bf04-131">De NSG aan het FrontEnd-subnet koppelen</span><span class="sxs-lookup"><span data-stu-id="3bf04-131">Associate the NSG to the FrontEnd subnet</span></span>
1. <span data-ttu-id="3bf04-132">Klik op **Bladeren >** > **resourcegroepen** > **RG NSG**.</span><span class="sxs-lookup"><span data-stu-id="3bf04-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="3bf04-133">In de **RG NSG** blade, klikt u op **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="3bf04-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Azure portal - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="3bf04-135">In de **instellingen** blade, klikt u op **subnetten** > **FrontEnd** > **netwerkbeveiligingsgroep** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="3bf04-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Azure portal - subnetinstellingen](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="3bf04-137">In de **FrontEnd** blade, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3bf04-137">In the **FrontEnd** blade, click **Save**.</span></span>
   
    ![Azure portal - subnetinstellingen](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a><span data-ttu-id="3bf04-139">Maken van de NSG NSG-back-end</span><span class="sxs-lookup"><span data-stu-id="3bf04-139">Create the NSG-BackEnd NSG</span></span>
<span data-ttu-id="3bf04-140">Maken van de **NSG-back-end** NSG en koppel deze aan de **back-end** subnet, volg de onderstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="3bf04-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span></span>

1. <span data-ttu-id="3bf04-141">Herhaal de stappen in [maken het NSG NSG-FrontEnd](#Create-the-NSG-FrontEnd-NSG) voor het maken van een NSG met de naam *NSG-back-end*</span><span class="sxs-lookup"><span data-stu-id="3bf04-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="3bf04-142">Herhaal de stappen in [regels maken in een bestaande NSG](#Create-rules-in-an-existing-NSG) maken de **inkomende** regels in de onderstaande tabel.</span><span class="sxs-lookup"><span data-stu-id="3bf04-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span></span>
   
   | <span data-ttu-id="3bf04-143">Regel voor binnenkomende verbindingen</span><span class="sxs-lookup"><span data-stu-id="3bf04-143">Inbound rule</span></span> | <span data-ttu-id="3bf04-144">Uitgaande regel</span><span class="sxs-lookup"><span data-stu-id="3bf04-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Azure portal - regel voor binnenkomende verbindingen](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure portal - uitgaande regel](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="3bf04-147">Herhaal de stappen in [het NSG aan het subnet FrontEnd koppelt](#Associate-the-NSG-to-the-FrontEnd-subnet) koppelen de **NSG-back-end** NSG aan de **back-end** subnet.</span><span class="sxs-lookup"><span data-stu-id="3bf04-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bf04-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3bf04-148">Next Steps</span></span>
* <span data-ttu-id="3bf04-149">Meer informatie over hoe [bestaande nsg's beheren](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3bf04-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="3bf04-150">[Logboekregistratie inschakelen](virtual-network-nsg-manage-log.md) voor nsg's.</span><span class="sxs-lookup"><span data-stu-id="3bf04-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

