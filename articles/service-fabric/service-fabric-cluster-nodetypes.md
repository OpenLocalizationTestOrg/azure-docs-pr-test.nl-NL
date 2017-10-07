---
title: aaaService Fabric knooppunttypen en VM-Schaalsets | Microsoft Docs
description: Beschrijft hoe Service Fabric-knooppunttypen tooVM Schaalsets gerelateerd en hoe tooremote verbinding tooa VM-Schaalset exemplaar of een clusterknooppunt.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="ec714-103">Hallo-relatie tussen typen Service Fabric-knooppunten en virtuele-Machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="ec714-103">hello relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="ec714-104">Virtuele-Machineschaalsets zijn een Azure Compute resource die u kunt toodeploy gebruiken en beheren van een verzameling van virtuele machines als een set.</span><span class="sxs-lookup"><span data-stu-id="ec714-104">Virtual Machine Scale Sets are an Azure Compute resource you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="ec714-105">Elk knooppunttype dat is gedefinieerd in een Service Fabric-cluster is ingesteld als een afzonderlijke VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="ec714-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="ec714-106">Elk knooppunttype kan vervolgens worden uitgebreid of omlaag onafhankelijk, hebben verschillende sets van poorten openen en andere capaciteitsmetrieken kan hebben.</span><span class="sxs-lookup"><span data-stu-id="ec714-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="ec714-107">Hallo volgende schermafbeelding ziet u een cluster met twee knooppunttypen: FrontEnd en BackEnd.</span><span class="sxs-lookup"><span data-stu-id="ec714-107">hello following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="ec714-108">Elk knooppunttype heeft vijf knooppunten.</span><span class="sxs-lookup"><span data-stu-id="ec714-108">Each node type has five nodes each.</span></span>

![Schermopname van een cluster met twee knooppunttypen][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a><span data-ttu-id="ec714-110">VM-Schaalset exemplaren toonodes toewijzen</span><span class="sxs-lookup"><span data-stu-id="ec714-110">Mapping VM Scale Set instances toonodes</span></span>
<span data-ttu-id="ec714-111">Als u hierboven ziet, Hallo VM-Schaalset exemplaren van 0-exemplaar gestart en wordt vervolgens.</span><span class="sxs-lookup"><span data-stu-id="ec714-111">As you can see above, hello VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="ec714-112">Hallo nummering wordt doorgevoerd in Hallo namen.</span><span class="sxs-lookup"><span data-stu-id="ec714-112">hello numbering is reflected in hello names.</span></span> <span data-ttu-id="ec714-113">BackEnd_0 is bijvoorbeeld exemplaar 0 Hallo back-end voor VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="ec714-113">For example, BackEnd_0 is instance 0 of hello BackEnd VM Scale Set.</span></span> <span data-ttu-id="ec714-114">Deze bepaalde VM-Schaalset heeft vijf exemplaren, met de naam BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 en BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="ec714-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="ec714-115">Wanneer u een VM-Schaalset opschalen wordt een nieuw exemplaar gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ec714-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="ec714-116">Hallo nieuwe VM-Schaalset exemplaarnaam wordt doorgaans Hallo VM-Schaalset naam + Hallo volgende exemplaar getal.</span><span class="sxs-lookup"><span data-stu-id="ec714-116">hello new VM Scale Set instance name will typically be hello VM Scale Set name + hello next instance number.</span></span> <span data-ttu-id="ec714-117">In ons voorbeeld is het BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="ec714-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a><span data-ttu-id="ec714-118">Toewijzing van VM-schaalset laden balancers tooeach knooppunt type/VM-Schaalset bevatten</span><span class="sxs-lookup"><span data-stu-id="ec714-118">Mapping VM scale set load balancers tooeach node type/VM Scale Set</span></span>
<span data-ttu-id="ec714-119">Als u uw cluster van Hallo-portal hebt geïmplementeerd of Hallo voorbeeld Resource Manager-sjabloon die wordt opgegeven, klikt u vervolgens als u een lijst met alle bronnen van een resourcegroep hebt gebruikt ziet u Hallo load balancers voor elk type VM-Schaalset of het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ec714-119">If you have deployed your cluster from hello portal or have used hello sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see hello load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="ec714-120">Hallo naam zou ongeveer: **LB -&lt;NodeType naam&gt;**.</span><span class="sxs-lookup"><span data-stu-id="ec714-120">hello name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="ec714-121">Bijvoorbeeld, Load Balancer-sfcluster4doc-0, zoals weergegeven in deze schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="ec714-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Resources][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="ec714-123">Extern verbinding maken met tooa VM-Schaalset exemplaar of een clusterknooppunt</span><span class="sxs-lookup"><span data-stu-id="ec714-123">Remote connect tooa VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="ec714-124">Elk type knooppunt dat is gedefinieerd in een cluster is ingesteld als een afzonderlijke VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="ec714-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="ec714-125">Dat betekent Hallo knooppunttypen kan worden geschaald omhoog of omlaag onafhankelijk en van andere VM-SKU's kunnen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ec714-125">That means hello node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="ec714-126">In tegenstelling tot één exemplaar van virtuele machines worden een virtueel IP-adres van hun eigen in Hallo VM-Schaalset exemplaren niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="ec714-126">Unlike single instance VMs, hello VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="ec714-127">Zodat deze een bit worden kan verbinding lastig wanneer u een IP zoekt-adres en poort waarmee u tooremote kunt tooa specifieke exemplaar.</span><span class="sxs-lookup"><span data-stu-id="ec714-127">So it can be a bit challenging when you are looking for an IP address and port that you can use tooremote connect tooa specific instance.</span></span>

<span data-ttu-id="ec714-128">Hier volgen Hallo stappen kunt u toodiscover ze.</span><span class="sxs-lookup"><span data-stu-id="ec714-128">Here are hello steps you can follow toodiscover them.</span></span>

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="ec714-129">Stap 1: Informatie over de virtuele IP-adres voor het knooppunttype Hallo Hallo en vervolgens binnenkomende NAT-regels voor RDP</span><span class="sxs-lookup"><span data-stu-id="ec714-129">Step 1: Find out hello virtual IP address for hello node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="ec714-130">In de volgorde tooget, moet u tooget Hallo binnenkomende NAT waarden die zijn gedefinieerd als onderdeel van de resourcedefinitie Hallo voor regels **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="ec714-130">In order tooget that, you need tooget hello inbound NAT rules values that were defined as a part of hello resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="ec714-131">Navigeer in Hallo portal toohello Load balancer-blade en vervolgens **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ec714-131">In hello portal, navigate toohello Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="ec714-133">In **instellingen**, klikt u op **binnenkomende NAT-regels**.</span><span class="sxs-lookup"><span data-stu-id="ec714-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="ec714-134">Hiermee geeft u een IP-adres en poort waarmee u tooremote kunt Hallo verbinding maken met toohello eerste exemplaar van de VM-Schaalset.</span><span class="sxs-lookup"><span data-stu-id="ec714-134">This now gives you hello IP address and port that you can use tooremote connect toohello first VM Scale Set instance.</span></span> <span data-ttu-id="ec714-135">In onderstaande Hallo schermafbeelding, is het **104.42.106.156** en **3389**</span><span class="sxs-lookup"><span data-stu-id="ec714-135">In hello screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a><span data-ttu-id="ec714-137">Stap 2: Uitzoeken Hallo poort waarmee u kunt tooremote verbinding toohello specifieke VM-Schaalset exemplaar/knooppunt</span><span class="sxs-lookup"><span data-stu-id="ec714-137">Step 2: Find out hello port that you can use tooremote connect toohello specific VM Scale Set instance/node</span></span>
<span data-ttu-id="ec714-138">Eerder in dit document besproken ik hoe Hallo VM-Schaalset exemplaren toohello knooppunten toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ec714-138">Earlier in this document, I talked about how hello VM Scale Set instances map toohello nodes.</span></span> <span data-ttu-id="ec714-139">We gebruiken deze toofigure Hallo exacte poort.</span><span class="sxs-lookup"><span data-stu-id="ec714-139">We will use that toofigure out hello exact port.</span></span>

<span data-ttu-id="ec714-140">Hallo-poorten zijn toegewezen in oplopende volgorde van de VM-Schaalset Hallo-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="ec714-140">hello ports are allocated in ascending order of hello VM Scale Set instance.</span></span> <span data-ttu-id="ec714-141">Hallo-poorten voor elk van de vijf exemplaren Hallo zijn dus in mijn voorbeeld voor Hallo FrontEnd knooppunttype Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="ec714-141">so in my example for hello FrontEnd node type, hello ports for each of hello five instances are hello following.</span></span> <span data-ttu-id="ec714-142">u nu moet bij toodo dezelfde toewijzing voor uw exemplaar van VM-Schaalset Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec714-142">you now need toodo hello same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="ec714-143">**VM-Schaalset exemplaar**</span><span class="sxs-lookup"><span data-stu-id="ec714-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="ec714-144">**Poort**</span><span class="sxs-lookup"><span data-stu-id="ec714-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="ec714-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="ec714-145">FrontEnd_0</span></span> |<span data-ttu-id="ec714-146">3389</span><span class="sxs-lookup"><span data-stu-id="ec714-146">3389</span></span> |
| <span data-ttu-id="ec714-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="ec714-147">FrontEnd_1</span></span> |<span data-ttu-id="ec714-148">3390</span><span class="sxs-lookup"><span data-stu-id="ec714-148">3390</span></span> |
| <span data-ttu-id="ec714-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="ec714-149">FrontEnd_2</span></span> |<span data-ttu-id="ec714-150">3391</span><span class="sxs-lookup"><span data-stu-id="ec714-150">3391</span></span> |
| <span data-ttu-id="ec714-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="ec714-151">FrontEnd_3</span></span> |<span data-ttu-id="ec714-152">3392</span><span class="sxs-lookup"><span data-stu-id="ec714-152">3392</span></span> |
| <span data-ttu-id="ec714-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="ec714-153">FrontEnd_4</span></span> |<span data-ttu-id="ec714-154">3393</span><span class="sxs-lookup"><span data-stu-id="ec714-154">3393</span></span> |
| <span data-ttu-id="ec714-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="ec714-155">FrontEnd_5</span></span> |<span data-ttu-id="ec714-156">3394</span><span class="sxs-lookup"><span data-stu-id="ec714-156">3394</span></span> |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a><span data-ttu-id="ec714-157">Stap 3: Extern verbinding toohello specifieke VM-Schaalset-exemplaar</span><span class="sxs-lookup"><span data-stu-id="ec714-157">Step 3: Remote connect toohello specific VM Scale Set instance</span></span>
<span data-ttu-id="ec714-158">In onderstaande schermafbeelding voor Hallo ik verbinding met extern bureaublad tooconnect toohello FrontEnd_1 gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ec714-158">In hello screenshot below I use Remote Desktop Connection tooconnect toohello FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a><span data-ttu-id="ec714-160">Hoe de waarden voor het bereik van toochange Hallo RDP-poort</span><span class="sxs-lookup"><span data-stu-id="ec714-160">How toochange hello RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="ec714-161">Voordat de implementatie van het cluster</span><span class="sxs-lookup"><span data-stu-id="ec714-161">Before cluster deployment</span></span>
<span data-ttu-id="ec714-162">Wanneer u Hallo-cluster met een Resource Manager-sjabloon instelt, kunt u Hallo-bereik opgeven in Hallo **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="ec714-162">When you are setting up hello cluster using an Resource Manager template, you can specify hello range in hello **inboundNatPools**.</span></span>

<span data-ttu-id="ec714-163">Ga resourcedefinitie toohello voor **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="ec714-163">Go toohello resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="ec714-164">Onder die u Hallo beschrijving voor vinden **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="ec714-164">Under that you find hello description for **inboundNatPools**.</span></span>  <span data-ttu-id="ec714-165">Vervang Hallo *frontendPortRangeStart* en *frontendPortRangeEnd* waarden.</span><span class="sxs-lookup"><span data-stu-id="ec714-165">Replace hello *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![InboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="ec714-167">Na implementatie van het cluster</span><span class="sxs-lookup"><span data-stu-id="ec714-167">After cluster deployment</span></span>
<span data-ttu-id="ec714-168">Dit is iets gecompliceerder en kan leiden tot Hallo virtuele machines opnieuw worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ec714-168">This is a bit more involved and may result in hello VMs getting recycled.</span></span> <span data-ttu-id="ec714-169">U hebt nu de nieuwe waarden tooset met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec714-169">You will now have tooset new values using Azure PowerShell.</span></span> <span data-ttu-id="ec714-170">Zorg ervoor dat de Azure PowerShell 1.0 of hoger is geïnstalleerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ec714-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="ec714-171">Als u dit nog niet hebt gedaan, ik raden dat u Hallo die worden beschreven stappen in [hoe tooinstall Azure PowerShell en configureren.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="ec714-171">If you have not done this before, I strongly suggest that you follow hello steps outlined in [How tooinstall and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="ec714-172">Meld u aan tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ec714-172">Sign in tooyour Azure account.</span></span> <span data-ttu-id="ec714-173">Als deze PowerShell-opdracht om een bepaalde reden mislukt, moet u controleren of u Azure PowerShell juist is geïnstalleerd hebt.</span><span class="sxs-lookup"><span data-stu-id="ec714-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="ec714-174">Hallo volgende tooget details op de load balancer worden uitgevoerd en u ziet Hallo waarden voor Hallo beschrijving voor **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="ec714-174">Run hello following tooget details on your load balancer and you see hello values for hello description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="ec714-175">Stel nu *frontendPortRangeEnd* en *frontendPortRangeStart* toohello waarden die u wilt.</span><span class="sxs-lookup"><span data-stu-id="ec714-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* toohello values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="ec714-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec714-176">Next steps</span></span>
* [<span data-ttu-id="ec714-177">Overzicht van Hallo 'Overal implementatie' functie en een vergelijking met Azure beheerde clusters</span><span class="sxs-lookup"><span data-stu-id="ec714-177">Overview of hello "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="ec714-178">Clusterbeveiliging</span><span class="sxs-lookup"><span data-stu-id="ec714-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="ec714-179">Service Fabric SDK en aan de slag</span><span class="sxs-lookup"><span data-stu-id="ec714-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
