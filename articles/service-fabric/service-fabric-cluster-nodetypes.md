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
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>Hallo-relatie tussen typen Service Fabric-knooppunten en virtuele-Machineschaalsets
Virtuele-Machineschaalsets zijn een Azure Compute resource die u kunt toodeploy gebruiken en beheren van een verzameling van virtuele machines als een set. Elk knooppunttype dat is gedefinieerd in een Service Fabric-cluster is ingesteld als een afzonderlijke VM-Schaalset. Elk knooppunttype kan vervolgens worden uitgebreid of omlaag onafhankelijk, hebben verschillende sets van poorten openen en andere capaciteitsmetrieken kan hebben.

Hallo volgende schermafbeelding ziet u een cluster met twee knooppunttypen: FrontEnd en BackEnd.  Elk knooppunttype heeft vijf knooppunten.

![Schermopname van een cluster met twee knooppunttypen][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a>VM-Schaalset exemplaren toonodes toewijzen
Als u hierboven ziet, Hallo VM-Schaalset exemplaren van 0-exemplaar gestart en wordt vervolgens. Hallo nummering wordt doorgevoerd in Hallo namen. BackEnd_0 is bijvoorbeeld exemplaar 0 Hallo back-end voor VM-Schaalset. Deze bepaalde VM-Schaalset heeft vijf exemplaren, met de naam BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 en BackEnd_4.

Wanneer u een VM-Schaalset opschalen wordt een nieuw exemplaar gemaakt. Hallo nieuwe VM-Schaalset exemplaarnaam wordt doorgaans Hallo VM-Schaalset naam + Hallo volgende exemplaar getal. In ons voorbeeld is het BackEnd_5.

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a>Toewijzing van VM-schaalset laden balancers tooeach knooppunt type/VM-Schaalset bevatten
Als u uw cluster van Hallo-portal hebt geïmplementeerd of Hallo voorbeeld Resource Manager-sjabloon die wordt opgegeven, klikt u vervolgens als u een lijst met alle bronnen van een resourcegroep hebt gebruikt ziet u Hallo load balancers voor elk type VM-Schaalset of het knooppunt.

Hallo naam zou ongeveer: **LB -&lt;NodeType naam&gt;**. Bijvoorbeeld, Load Balancer-sfcluster4doc-0, zoals weergegeven in deze schermafbeelding:

![Resources][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a>Extern verbinding maken met tooa VM-Schaalset exemplaar of een clusterknooppunt
Elk type knooppunt dat is gedefinieerd in een cluster is ingesteld als een afzonderlijke VM-Schaalset.  Dat betekent Hallo knooppunttypen kan worden geschaald omhoog of omlaag onafhankelijk en van andere VM-SKU's kunnen worden gemaakt. In tegenstelling tot één exemplaar van virtuele machines worden een virtueel IP-adres van hun eigen in Hallo VM-Schaalset exemplaren niet ophalen. Zodat deze een bit worden kan verbinding lastig wanneer u een IP zoekt-adres en poort waarmee u tooremote kunt tooa specifieke exemplaar.

Hier volgen Hallo stappen kunt u toodiscover ze.

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a>Stap 1: Informatie over de virtuele IP-adres voor het knooppunttype Hallo Hallo en vervolgens binnenkomende NAT-regels voor RDP
In de volgorde tooget, moet u tooget Hallo binnenkomende NAT waarden die zijn gedefinieerd als onderdeel van de resourcedefinitie Hallo voor regels **Microsoft.Network/loadBalancers**.

Navigeer in Hallo portal toohello Load balancer-blade en vervolgens **instellingen**.

![LBBlade][LBBlade]

In **instellingen**, klikt u op **binnenkomende NAT-regels**. Hiermee geeft u een IP-adres en poort waarmee u tooremote kunt Hallo verbinding maken met toohello eerste exemplaar van de VM-Schaalset. In onderstaande Hallo schermafbeelding, is het **104.42.106.156** en **3389**

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a>Stap 2: Uitzoeken Hallo poort waarmee u kunt tooremote verbinding toohello specifieke VM-Schaalset exemplaar/knooppunt
Eerder in dit document besproken ik hoe Hallo VM-Schaalset exemplaren toohello knooppunten toegewezen. We gebruiken deze toofigure Hallo exacte poort.

Hallo-poorten zijn toegewezen in oplopende volgorde van de VM-Schaalset Hallo-exemplaar. Hallo-poorten voor elk van de vijf exemplaren Hallo zijn dus in mijn voorbeeld voor Hallo FrontEnd knooppunttype Hallo volgende. u nu moet bij toodo dezelfde toewijzing voor uw exemplaar van VM-Schaalset Hallo.

| **VM-Schaalset exemplaar** | **Poort** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a>Stap 3: Extern verbinding toohello specifieke VM-Schaalset-exemplaar
In onderstaande schermafbeelding voor Hallo ik verbinding met extern bureaublad tooconnect toohello FrontEnd_1 gebruiken:

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a>Hoe de waarden voor het bereik van toochange Hallo RDP-poort
### <a name="before-cluster-deployment"></a>Voordat de implementatie van het cluster
Wanneer u Hallo-cluster met een Resource Manager-sjabloon instelt, kunt u Hallo-bereik opgeven in Hallo **inboundNatPools**.

Ga resourcedefinitie toohello voor **Microsoft.Network/loadBalancers**. Onder die u Hallo beschrijving voor vinden **inboundNatPools**.  Vervang Hallo *frontendPortRangeStart* en *frontendPortRangeEnd* waarden.

![InboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>Na implementatie van het cluster
Dit is iets gecompliceerder en kan leiden tot Hallo virtuele machines opnieuw worden gebruikt. U hebt nu de nieuwe waarden tooset met Azure PowerShell. Zorg ervoor dat de Azure PowerShell 1.0 of hoger is geïnstalleerd op uw computer. Als u dit nog niet hebt gedaan, ik raden dat u Hallo die worden beschreven stappen in [hoe tooinstall Azure PowerShell en configureren.](/powershell/azure/overview)

Meld u aan tooyour Azure-account. Als deze PowerShell-opdracht om een bepaalde reden mislukt, moet u controleren of u Azure PowerShell juist is geïnstalleerd hebt.

```
Login-AzureRmAccount
```

Hallo volgende tooget details op de load balancer worden uitgevoerd en u ziet Hallo waarden voor Hallo beschrijving voor **inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

Stel nu *frontendPortRangeEnd* en *frontendPortRangeStart* toohello waarden die u wilt.

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a>Volgende stappen
* [Overzicht van Hallo 'Overal implementatie' functie en een vergelijking met Azure beheerde clusters](service-fabric-deploy-anywhere.md)
* [Clusterbeveiliging](service-fabric-cluster-security.md)
* [Service Fabric SDK en aan de slag](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
