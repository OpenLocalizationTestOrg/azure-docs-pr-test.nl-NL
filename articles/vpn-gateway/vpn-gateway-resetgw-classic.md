---
title: Opnieuw instellen van een Azure VPN-gateway tooreestablish IPsec-tunnels | Microsoft Docs
description: Dit artikel begeleidt u bij het opnieuw instellen van uw Azure VPN-Gateway tooreestablish IPsec-tunnels. Hallo-artikel geldt tooVPN gateways in Hallo-classic en Hallo Resource Manager-implementatiemodel.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a>Een VPN Gateway opnieuw instellen

Het opnieuw instellen van een Azure VPN-gateway is handig als u cross-premises VPN-connectiviteit verliest in een of meer Site-to-Site VPN-tunnels. In dit geval uw on-premises VPN-apparaten zijn alle naar behoren werkt, maar er kan geen tooestablish IPsec-tunnels met hello Azure VPN-gateways zijn. In dit artikel helpt u bij uw VPN-gateway opnieuw instellen.

### <a name="what-happens-during-a-reset"></a>Wat er gebeurt tijdens het opnieuw instellen?

Een VPN-gateway bestaat uit twee VM-instanties uitgevoerd in een actief/stand-byconfiguratie. Wanneer u opnieuw Hallo-gateway, Hallo-gateway opnieuw opgestart en vervolgens opnieuw toegepast Hallo cross-premises configuraties tooit. Hallo gateway houdt Hallo openbaar IP-adres al heeft. Dit betekent dat u hoeft niet tooupdate Hallo VPN-routerconfiguratie met een nieuw openbaar IP-adres voor de Azure VPN-gateway.

Wanneer u Hallo opdracht tooreset Hallo gateway verzendt, Hallo huidige instantie van hello Azure VPN-gateway wordt onmiddellijk opnieuw opgestart. Er is een korte onderbreking tijdens de failover van Hallo van Hallo actieve instantie (opnieuw wordt opgestart), toohello stand-by-exemplaar. Hallo onderbreking moet minder dan een minuut.

Als het Hallo-verbinding is niet hersteld na de eerste keer opnieuw opstarten hello, probleem Hallo dezelfde opdracht opnieuw tooreboot Hallo tweede VM-instantie (Hallo nieuwe actieve gateway). Als twee keer opnieuw opstarten Hallo aangevraagde back tooback, zal er iets langer waar beide VM-instanties (actieve en stand-by) worden opnieuw opgestart. Hierdoor wordt een gap langer op Hallo VPN-verbinding van too2 too4 minuten voordat VMs toocomplete Hallo opnieuw wordt opgestart.

Na twee keer opnieuw opstarten als u steeds cross-premises connectiviteitsproblemen ondervindt nog, opent u een verzoek om ondersteuning van hello Azure-portal.

## <a name="before"></a>Voordat u begint

Voordat u de gateway opnieuw instelt, moet u controleren Hallo essentiële items voor elke IPsec-Site-naar-Site (S2S) VPN-tunnel hieronder vermeld. Hallo verbinding verbreken van de S2S VPN-tunnels leidt ertoe dat Hallo items niet overeenkomen. Controleren en te corrigeren Hallo configuraties voor uw on-premises en Azure VPN-gateways voorkomt dat u onnodig opnieuw moet opstarten en onderbrekingen voor Hallo andere werkende verbindingen op Hallo gateways.

Controleer of de volgende items voordat het opnieuw instellen van uw gateway Hallo:

* Hallo Internet-IP-adressen (VIP's) voor beide hello Azure VPN-gateway en Hallo on-premises VPN-gateway correct zijn geconfigureerd in beide hello Azure en Hallo lokale VPN-beleid.
* Hallo vooraf gedeelde sleutel moet hetzelfde zijn op zowel Azure en on-premises VPN-gateways Hallo.
* Als u specifieke IPsec/IKE-configuratie toepassen, zoals versleuteling, hash-algoritmen en PFS (Perfect Forward Secrecy), zorg ervoor dat beide hello Azure en lokale VPN-gateways Hallo hebben dezelfde configuraties.

## <a name="portal"></a>Azure-portal

U kunt een Resource Manager-VPN-gateway met behulp van hello Azure-portal opnieuw instellen. Als u tooreset een klassieke gateway wilt, Zie Hallo [PowerShell](#resetclassic) stappen.

### <a name="resource-manager-deployment-model"></a>Resource Manager-implementatiemodel

1. Open Hallo [Azure-portal](https://portal.azure.com) en navigeer toohello Resource Manager virtuele netwerkgateway die u tooreset wilt.
2. Klik op 'Herstellen' op de blade voor de virtuele netwerkgateway Hallo Hallo.

  ![Opnieuw instellen van VPN-Gateway-blade](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. Op Hallo blade, klikt u op Hallo **opnieuw** knop.

## <a name="ps"></a>PowerShell

### <a name="resource-manager-deployment-model"></a>Resource Manager-implementatiemodel

Hallo cmdlet voor opnieuw instellen van een gateway is **Reset AzureRmVirtualNetworkGateway**. Voordat u een reset uitvoert, zorg ervoor dat u beschikt over de nieuwste versie van de Hallo Hallo [Resource Manager PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0). Hallo wordt volgende voorbeeld een virtuele netwerkgateway met de naam VNet1GW in Hallo TestRG1 resourcegroep:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

Resultaat:

Wanneer u een resultaat geretourneerd ontvangt, kunt u aannemen Hallo gateway opnieuw instellen is voltooid. Maar is er niets in Hallo return resultaat die expliciet aangeeft dat Hallo opnieuw instellen is voltooid. Als u wilt dat toolook nauw op Hallo geschiedenis toosee precies wanneer Hallo-gateway opnieuw instellen is opgetreden, kunt u die informatie weergeven in Hallo [Azure-portal](https://portal.azure.com). Navigeer te in Hallo portal**'GatewayName' -> resourcestatus**.

### <a name="resetclassic"></a>Klassieke implementatiemodel

Hallo cmdlet voor opnieuw instellen van een gateway is **Reset-AzureVNetGateway**. Voordat u een reset uitvoert, zorg ervoor dat u beschikt over de nieuwste versie van de Hallo Hallo [Service Management (SM) PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0). Hallo hersteld volgende voorbeeld Hallo gateway voor een virtueel netwerk met de naam 'ContosoVNet':

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

Resultaat:

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <a name="cli"></a>Azure CLI

Gebruik Hallo-gateway Hallo tooreset [az vnet-netwerkgateway opnieuw](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) opdracht. Hallo wordt volgende voorbeeld een virtuele netwerkgateway met de naam VNet5GW in Hallo TestRG5 resourcegroep:

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

Resultaat:

Wanneer u een resultaat geretourneerd ontvangt, kunt u aannemen Hallo gateway opnieuw instellen is voltooid. Maar is er niets in Hallo return resultaat die expliciet aangeeft dat Hallo opnieuw instellen is voltooid. Als u wilt dat toolook nauw op Hallo geschiedenis toosee precies wanneer Hallo-gateway opnieuw instellen is opgetreden, kunt u die informatie weergeven in Hallo [Azure-portal](https://portal.azure.com). Navigeer te in Hallo portal**'GatewayName' -> resourcestatus**.
