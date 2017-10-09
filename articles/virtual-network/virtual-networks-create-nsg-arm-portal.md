---
title: aaaManage-netwerkbeveiligingsgroepen - Azure-portal | Microsoft Docs
description: Meer informatie over hoe toomanage netwerkbeveiligingsgroepen met hello Azure-portal.
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
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="c7fb6-103">Netwerkbeveiligingsgroepen met hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c7fb6-103">Manage network security groups using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c7fb6-104">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="c7fb6-105">U kunt ook [nsg's maken in het klassieke implementatiemodel Hallo](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c7fb6-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="c7fb6-106">Hallo voorbeeld PowerShell onderstaande opdrachten verwacht een eenvoudige omgeving al gemaakt dat is gebaseerd op Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-106">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="c7fb6-107">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, moet u eerst Hallo testomgeving verder door de implementatie [deze sjabloon](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), klikt u op **tooAzure implementeren**, standaardparameterwaarden Hallo vervangen indien nodig, en volg de instructies in Hallo in Hallo portal.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span> <span data-ttu-id="c7fb6-108">Hallo stappen hieronder gebruik **RG NSG** zoals Hallo-naam van Hallo resource groep Hallo-sjabloon is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-108">hello steps below use **RG-NSG** as hello name of hello resource group hello template was deployed to.</span></span>

## <a name="create-hello-nsg-frontend-nsg"></a><span data-ttu-id="c7fb6-109">Hallo NSG-FrontEnd NSG maken</span><span class="sxs-lookup"><span data-stu-id="c7fb6-109">Create hello NSG-FrontEnd NSG</span></span>
<span data-ttu-id="c7fb6-110">Hallo toocreate **NSG-FrontEnd** NSG zoals weergegeven in de bovenstaande Hallo-scenario Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-110">toocreate hello **NSG-FrontEnd** NSG as shown in hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="c7fb6-111">Navigeer via een browser toohttp://portal.azure.com en, indien nodig, meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-111">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="c7fb6-112">Klik op **Bladeren >** > **Netwerkbeveiligingsgroepen**.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Azure portal - nsg 's](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="c7fb6-114">In Hallo **Netwerkbeveiligingsgroepen** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-114">In hello **Network security groups** blade, click **Add**.</span></span>
   
    ![Azure portal - nsg 's](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="c7fb6-116">In Hallo **netwerkbeveiligingsgroep maken** blade maken van een NSG met de naam *NSG-FrontEnd* in Hallo *RG NSG* resourcegroep en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-116">In hello **Create network security group** blade, create an NSG named *NSG-FrontEnd* in hello *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Azure portal - nsg 's](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="c7fb6-118">Regels maken in een bestaande NSG</span><span class="sxs-lookup"><span data-stu-id="c7fb6-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="c7fb6-119">toocreate regels in een bestaande NSG van hello Azure-portal stappen Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-119">toocreate rules in an existing NSG from hello Azure portal, follow hello steps below.</span></span>

1. <span data-ttu-id="c7fb6-120">Klik op **Bladeren >** > **Netwerkbeveiligingsgroepen**.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="c7fb6-121">Klik in de lijst Hallo van nsg's, op **NSG-FrontEnd** > **beveiligingsregels voor binnenkomende verbindingen**</span><span class="sxs-lookup"><span data-stu-id="c7fb6-121">In hello list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Azure portal - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="c7fb6-123">In de lijst met Hallo **inkomende beveiligingsregels**, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-123">In hello list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Azure-portal - regel toevoegen](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="c7fb6-125">In Hallo **de inkomende beveiligingsregel toevoegen** blade maken van een regel met naam *web regel* met de prioriteit van *200* toegang via *TCP* tooport *80* tooany VM vanaf elke bron en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-125">In hello **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* tooport *80* tooany VM from any source, and then click **OK**.</span></span> <span data-ttu-id="c7fb6-126">U ziet dat de meeste van deze instellingen standaardwaarden al.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-126">Notice that most of these settings are default values already.</span></span>
   
    ![Azure portal - instellingen van de regel](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="c7fb6-128">Na enkele seconden worden er nieuwe regel in het NSG Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-128">After a few seconds you will see hello new rule in hello NSG.</span></span>
   
    ![Azure portal - nieuwe regel](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="c7fb6-130">Herhaal stap too6 toocreate een inkomende regel met de naam *rdp-regel* met een prioriteit van *250* toegang via *TCP* tooport *3389* tooany VM van een andere bron.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-130">Repeat steps  too6 toocreate an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* tooport *3389* tooany VM from any source.</span></span>

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a><span data-ttu-id="c7fb6-131">Hallo NSG toohello FrontEnd subnet koppelen</span><span class="sxs-lookup"><span data-stu-id="c7fb6-131">Associate hello NSG toohello FrontEnd subnet</span></span>
1. <span data-ttu-id="c7fb6-132">Klik op **Bladeren >** > **resourcegroepen** > **RG NSG**.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="c7fb6-133">In Hallo **RG NSG** blade, klikt u op **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-133">In hello **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Azure portal - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="c7fb6-135">In Hallo **instellingen** blade, klikt u op **subnetten** > **FrontEnd** > **netwerkbeveiligingsgroep**  >  **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-135">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Azure portal - subnetinstellingen](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="c7fb6-137">In Hallo **FrontEnd** blade, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-137">In hello **FrontEnd** blade, click **Save**.</span></span>
   
    ![Azure portal - subnetinstellingen](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a><span data-ttu-id="c7fb6-139">Hallo NSG-back-end NSG maken</span><span class="sxs-lookup"><span data-stu-id="c7fb6-139">Create hello NSG-BackEnd NSG</span></span>
<span data-ttu-id="c7fb6-140">Hallo toocreate **NSG-back-end** NSG en koppelt u deze toohello **back-end** subnet, Hallo stappen hieronder.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-140">toocreate hello **NSG-BackEnd** NSG and associate it toohello **BackEnd** subnet, follow hello steps below.</span></span>

1. <span data-ttu-id="c7fb6-141">Hallo Herhaal de stappen in [maken Hallo NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate een NSG met de naam *NSG-back-end*</span><span class="sxs-lookup"><span data-stu-id="c7fb6-141">Repeat hello steps in [Create hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="c7fb6-142">Hallo Herhaal de stappen in [regels maken in een bestaande NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inkomende** regels in Hallo onderstaande tabel.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-142">Repeat hello steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inbound** rules in hello table below.</span></span>
   
   | <span data-ttu-id="c7fb6-143">Regel voor binnenkomende verbindingen</span><span class="sxs-lookup"><span data-stu-id="c7fb6-143">Inbound rule</span></span> | <span data-ttu-id="c7fb6-144">Uitgaande regel</span><span class="sxs-lookup"><span data-stu-id="c7fb6-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Azure portal - regel voor binnenkomende verbindingen](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure portal - uitgaande regel](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="c7fb6-147">Hallo Herhaal de stappen in [hello NSG toohello FrontEnd subnet koppelen](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-back-end** NSG toohello **back-end** subnet.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-147">Repeat hello steps in [Associate hello NSG toohello FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-Backend** NSG toohello **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7fb6-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7fb6-148">Next Steps</span></span>
* <span data-ttu-id="c7fb6-149">Meer informatie over hoe te[bestaande nsg's beheren](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c7fb6-149">Learn how too[manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="c7fb6-150">[Logboekregistratie inschakelen](virtual-network-nsg-manage-log.md) voor nsg's.</span><span class="sxs-lookup"><span data-stu-id="c7fb6-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

