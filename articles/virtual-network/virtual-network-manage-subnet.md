---
title: aaaAdd, wijzigen of verwijderen van een virtueel netwerk van Azure-subnet | Microsoft Docs
description: Meer informatie over hoe tooadd, wijzigen of verwijderen van een virtueel netwerksubnet in Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.openlocfilehash: 0d6d813b7e2fc52a00a87f6c6714ab5b7ca589ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>Toevoegen, wijzigen of een virtueel netwerksubnet verwijderen

Meer informatie over hoe tooadd, wijzigen of verwijderen van een virtueel netwerksubnet. 

Als u niet bekend met virtuele netwerken, bent voordat u toevoegen, wijzigen of verwijderen van een subnet, raden wij aan dat u leest [Azure Virtual Network-overzicht](virtual-networks-overview.md) en [maken, wijzigen of verwijderen van een virtueel netwerk](virtual-network-manage-network.md). Alle Azure-resources geïmplementeerd in een virtueel netwerk worden geïmplementeerd in een subnet binnen een virtueel netwerk. Meestal worden meerdere subnetten in een virtueel netwerk te gemaakt:
- **Filteren van verkeer tussen subnetten**. U kunt toepassen network security groepen toosubnets toofilter binnenkomend en uitgaand netwerkverkeer voor alle bronnen (zoals virtuele machines) die zich in het virtuele netwerk Hallo. toolearn informatie over hoe een netwerkbeveiligingsgroep toocreate zien [netwerkbeveiligingsgroepen maken](virtual-networks-create-nsg-arm-pportal.md).
- **Beheren van routering tussen subnetten**. Azure maakt standaardroutes zodat het verkeer automatisch doorgestuurd tussen subnetten. U kunt Azure standaardroutes onderdrukken door de gebruiker gedefinieerde routes maken. toolearn meer informatie over de gebruiker gedefinieerde routes, Zie [maken van de gebruiker gedefinieerde routes](virtual-network-create-udr-arm-ps.md). 

Dit artikel wordt uitgelegd hoe tooadd, wijzigen en verwijderen van een subnet voor de virtuele netwerken die zijn gemaakt met hello Azure Resource Manager-implementatiemodel.
 
## <a name="before"></a>Voordat u begint

Voordat u Hallo-taken die worden beschreven in dit artikel, voert u Hallo volgende vereisten:

- Als u nieuwe tooworking met virtuele netwerken, wij raden u Hallo Oefening in [maken van uw eerste virtuele Azure-netwerk](virtual-network-get-started-vnet-subnet.md). In deze oefening kunt u vertrouwd raken met virtuele netwerken.
- toolearn over de limieten voor virtuele netwerken, Bekijk [Azure limieten](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Meld u aan toohello Azure-portal, Azure-opdrachtregelprogramma (Azure CLI) of Azure PowerShell Hallo met behulp van uw Azure-account. Als u geen Azure-account hebt, zich aanmelden voor een [gratis proefaccount](https://azure.microsoft.com/free).
- Als u van plan toouse PowerShell-toocomplete Hallo taken die worden beschreven in dit artikel bent opdrachten, moet u eerst [Azure PowerShell installeren en configureren](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u de meest recente versie Hallo van hello Azure PowerShell-cmdlets die zijn geïnstalleerd. tooget help voor PowerShell-opdrachten in de voorbeelden hello, voer `get-help <command> -full`.
- Als u van plan toouse die Azure CLI-toocomplete Hallo taken die worden beschreven in dit artikel bent opdrachten, moet u een van:
    - [Installeren en configureren van Azure CLI Hallo](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u de meest recente versie Hallo van Azure CLI is geïnstalleerd.
    - Hello Azure Cloud Shell gebruiken. U kunt in plaats van installatie Hallo CLI en de bijbehorende afhankelijkheden, hello Azure Cloud Shell gebruiken. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft. toouse hello Cloud-Shell, klikt u op Hallo Cloud Shell (**> _**) pictogram bovenaan Hallo hello Azure-portal. 

  Voer tooget hulp bij de Azure CLI-opdrachten `az <command> --help`.

## <a name="create-subnet"></a>Een subnet toevoegen

een subnet tooadd:

1. Meld u aan toohello [portal](https://portal.azure.com) met een account met machtigingen voor Hallo netwerk rol van inzender (minimaal) voor uw abonnement is toegewezen. toolearn meer informatie over het toewijzen van rollen en machtigingen tooaccounts, Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Voer in de portal zoekvak Hallo **virtuele netwerken**. Klik in de zoekresultaten Hallo **virtuele netwerken**.
3. Op Hallo **virtuele netwerken** blade, klikt u op de virtuele netwerk Hallo tooadd een subnet gewenste.
4. Klik op de blade virtueel netwerk hello, **subnetten**.
5. Klik op **+ Subnet**.
6. Op Hallo **subnet toevoegen** blade Voer waarden in voor Hallo volgende parameters:
    - **Naam**: Hallo-naam moet uniek zijn binnen het virtuele netwerk Hallo.
    - **-Adresbereik**: Hallo bereik moet uniek zijn binnen het Hallo-adresruimte voor het virtuele netwerk Hallo. Hallo bereik kan niet overlappen met adresbereiken van andere subnet binnen het virtuele netwerk Hallo. Hallo-adresruimte moet worden opgegeven met behulp van notatie (Classless Inter-Domain Routing). U kunt bijvoorbeeld een subnet-adresruimte van 10.0.0.0/24 definiëren in een virtueel netwerk met adresruimte 10.0.0.0/16. Hallo kleinste bereik die kunt u opgeven is slechts/29, waarmee u acht IP-adressen voor Hallo subnet. Azure reserves eerst Hallo en los deze laatste in elk subnet voor het protocol overeenstemming. Drie extra adressen zijn gereserveerd voor gebruik van Azure service. Als gevolg hiervan definiëren van een subnet met een/29 adres bereik resulteert in drie bruikbare IP-adressen in het Hallo-subnet. Als u een VPN-gateway van virtueel netwerk tooa tooconnect plant, moet u een gatewaysubnet maken. Meer informatie over [specifiek adresbereik overwegingen voor het gateway-subnetten](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). U kunt Hallo-adresbereik wijzigen nadat Hallo subnet is toegevoegd, klikt u onder bepaalde omstandigheden. hoe een adresbereik subnet toochange zien toolearn [subnetinstellingen wijzigen](#change-subnet) in dit artikel.
    - **Netwerkbeveiligingsgroep**: u kunt desgewenst een bestaande netwerkbeveiligingsgroep koppelen aan Hallo subnet toocontrol binnenkomend en uitgaand netwerkverkeer filteren voor Hallo subnet. Hallo netwerkbeveiligingsgroep moet aanwezig zijn in Hallo hetzelfde abonnement en de locatie als Hallo virtuele netwerk. Deze moet ook worden gemaakt met Hallo Resource Manager-implementatiemodel. toolearn informatie over hoe een netwerkbeveiligingsgroep toocreate zien [Netwerkbeveiligingsgroepen](virtual-networks-create-nsg-arm-pportal.md).
    - **Routetabel**: u kunt desgewenst een bestaande routetabel koppelen aan Hallo subnet toocontrol netwerkverkeer routering tooother netwerken. Hallo routetabel moet aanwezig zijn in Hallo hetzelfde abonnement en de locatie als Hallo virtuele netwerk. Deze moet ook worden gemaakt met Hallo Resource Manager-implementatiemodel. toolearn informatie over hoe toocreate routetabellen, Zie [gebruiker gedefinieerde routes](virtual-network-create-udr-arm-ps.md).
    - **Gebruikers**: U kunt toegang toohello subnet beheren met behulp van ingebouwde rollen of uw eigen aangepaste rollen. toolearn meer informatie over het toewijzen van rollen en gebruikers tooaccess Hallo subnet, Zie [rol toewijzing toomanage toegang tooyour Azure gebruiken resources](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access).
7. tooadd hello subnet toohello virtueel netwerk dat u hebt geselecteerd, klikt u op **OK**.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|Azure CLI|[AZ network vnet subnet maken](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Nieuwe AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json), [toevoegen AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>De subnet-wijzigingsinstellingen

U kunt netwerkbeveiligingsgroepen, routetabellen en gebruiker toegang tooa subnet wijzigen door het beheer van bronnen die zich in een subnet. toolearn over deze instellingen in [een subnet toevoegen](#create-subnet), Zie stap 6. Als u toochange Hallo-adresruimte van een subnet wilt, moet u eerst alle bronnen die zich in Hallo subnet te verwijderen. Hallo u stappen ondernemen toodelete is een resource afhankelijk van Hallo resource. toolearn hoe toodelete resources die zich in subnetten, lees Hallo-documentatie voor elke resource type, dat u wilt dat toodelete. Hallo adresbereik toochange voor een subnet:

1. Meld u aan toohello [portal](https://portal.azure.com) met een account met machtigingen voor Hallo netwerk rol van inzender (minimaal) voor uw abonnement is toegewezen. toolearn meer informatie over het toewijzen van rollen en machtigingen tooaccounts, Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Voer in de portal zoekvak Hallo **virtuele netwerken**. Klik in de zoekresultaten Hallo **virtuele netwerken**.
3. Op Hallo **virtuele netwerken** blade, klikt u op Hallo virtueel netwerk waarvoor u toochange een subnet-adresbereik wilt.
4. Klik op Hallo-subnet waarvoor u toochange Hallo-adresbereik wilt.
5. Op Hallo subnet blade in Hallo **-adresbereik** Voer Hallo nieuwe-adresbereik. Hallo bereik moet uniek zijn binnen het Hallo-adresruimte voor het virtuele netwerk Hallo. Hallo bereik kan niet overlappen met adresbereiken van andere subnet binnen het virtuele netwerk Hallo. Hallo-adresruimte moet worden opgegeven met behulp van de CIDR-notatie. U kunt bijvoorbeeld een subnet-adresruimte van 10.0.0.0/24 definiëren in een virtueel netwerk met adresruimte 10.0.0.0/16. Hallo kleinste bereik die kunt u opgeven is slechts/29, waarmee u acht IP-adressen voor Hallo subnet. Azure reserves eerst Hallo en los deze laatste in elk subnet voor het protocol overeenstemming. Drie extra adressen zijn gereserveerd voor gebruik van Azure service. Als gevolg hiervan, een subnet met een/29-adresbereik heeft drie bruikbare IP-adressen. Als u een VPN-gateway van virtueel netwerk tooa tooconnect plant, moet u een gatewaysubnet maken. Meer informatie over [specifiek adresbereik overwegingen voor het gateway-subnetten](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). U kunt Hallo-adresbereik wijzigen nadat Hallo subnet is gemaakt, klikt u onder bepaalde omstandigheden. hoe een adresbereik subnet toochange zien toolearn [subnetinstellingen wijzigen](#change-subnet) in dit artikel.
6. Klik op **Opslaan**.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|Azure CLI|[AZ network vnet subnet bijwerken](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>Een subnet verwijderen

U kunt een subnet alleen verwijderen als er geen resources in Hallo subnet zijn. Als er bronnen in Hallo subnet, moet u Hallo-resources die Hallo subnet voordat u kunt Hallo subnet verwijderen verwijderen. Hallo u stappen ondernemen toodelete is een resource afhankelijk van Hallo resource. toolearn hoe toodelete resources die zich in subnetten, lees Hallo-documentatie voor elke resource type, dat u wilt dat toodelete. een subnet toodelete:

1. Meld u aan toohello [portal](https://portal.azure.com) met een account met machtigingen voor Hallo netwerk rol van inzender (minimaal) voor uw abonnement is toegewezen. toolearn meer informatie over het toewijzen van rollen en machtigingen tooaccounts, Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Voer in de portal zoekvak Hallo **virtuele netwerken**. Klik in de zoekresultaten Hallo **virtuele netwerken**.
3. Op Hallo **virtuele netwerken** blade, klikt u op de virtuele netwerk Hallo gewenste toodelete een subnet uit.
4. Op Hallo virtuele netwerk blade onder **instellingen**, klikt u op **subnetten**.
5. Hallo-lijst met subnetten dat op Hallo subnetten blade met de rechtermuisknop op Hallo subnet verschijnt wilt toodelete, klikt u op **verwijderen**, en klik vervolgens op **Ja** toodelete Hallo subnet.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|Azure CLI|[vnet-AZ netwerk het verwijderen](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Verwijder AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Volgende stappen

Zie voor een virtuele machine in een subnet, toocreate [een virtueel netwerk maken en implementeren van virtuele machines in Hallo subnet](virtual-network-get-started-vnet-subnet.md#create-vms).
