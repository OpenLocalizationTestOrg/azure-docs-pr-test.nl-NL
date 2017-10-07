---
title: "aaaVerify verkeer met Azure-netwerk-Watcher IP-stromen verifiëren - Azure CLI | Microsoft Docs"
description: Dit artikel wordt beschreven hoe toocheck als tooor van een virtuele machine verkeer wordt toegestaan of geweigerd met Azure CLI
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Controleer als verkeer wordt toegestaan of geweigerd tooor van een virtuele machine met het IP-stromen controleren of een onderdeel van Azure-netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST-API](network-watcher-check-ip-flow-verify-rest.md)


IP-stromen controleren is een functie van netwerk-Watcher waarmee u tooverify als verkeer wordt toegestaan tooor van een virtuele machine. Dit scenario is nuttig tooget een huidige status van of een virtuele machine tooan externe bron- of back-end praten kunt. IP-stroom controleren gebruikte tooverify is als uw regels Netwerkbeveiligingsgroep (NSG) juist zijn geconfigureerd en oplossen van stromen die worden geblokkeerd door het NSG-regels. Een andere reden voor het gebruik van IP-stroom controleren die u blokkeren wilt tooensure-verkeer wordt geblokkeerd goed door Hallo NSG.

In dit artikel gebruikt de volgende generatie CLI voor Hallo resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.

tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Voordat u begint

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher of een bestaand exemplaar van netwerk-Watcher hebben. Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.

## <a name="scenario"></a>Scenario

Dit scenario maakt gebruik van IP-stromen controleren tooverify als een virtuele machine tooa bekende praten kunt Bing IP-adres. Als het Hallo-verkeer wordt geweigerd, wordt Hallo beveiligingsregel die dat verkeer wordt geweigerd. toolearn meer informatie over IP-stromen controleren, gaat u naar [overzicht van IP-stromen controleren](network-watcher-ip-flow-verify-overview.md)

## <a name="get-a-vm"></a>Een virtuele machine ophalen

IP-stroom controleren tests verkeer tooor van een IP-adres op een virtuele machine tooor vanaf een externe bestemming. Een Id van een virtuele machine is vereist voor het Hallo-cmdlet. Als u al Hallo-ID van virtuele machine-toouse hello weet, kunt u deze stap overslaan.

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a>Hallo NIC's ophalen

Hallo IP-adres van een NIC op Hallo virtuele machine is vereist, in dit voorbeeld Hallo NIC's op een virtuele machine worden opgehaald. Als u weet al Hallo IP adres die u wilt dat tootest op Hallo virtuele machine, kunt u deze stap overslaan.

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a>Voer IP-stroom controleren

Nu dat we Hallo informatie nodig toorun Hallo cmdlet hebben, voeren we Hallo `az network watcher test-ip-flow` cmdlet tootest Hallo verkeer. In dit voorbeeld gebruiken we Hallo eerste IP-adres op Hallo eerste NIC.

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> IP-stromen controleren vereist dat de VM-resource Hallo toorun wordt toegewezen.

## <a name="review-results"></a>Resultaten bekijken

Nadat u `az network watcher test-ip-flow` Hallo resultaten worden geretourneerd, hello volgende voorbeeld is Hallo resultaten geretourneerd door de voorgaande stap Hallo.

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a>Volgende stappen

Zie als verkeer wordt geblokkeerd en mag geen [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die zijn gedefinieerd.

Meer tooaudit uw NSG-instellingen in via [controle Netwerkbeveiligingsgroep groepen (NSG) met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
