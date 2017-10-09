---
title: aaaCreate, wijzigen of verwijderen van een virtueel netwerk van Azure-peering | Microsoft Docs
description: Meer informatie over hoe toocreate, wijzigen of verwijderen van een virtueel netwerk peering.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.openlocfilehash: 70f85364ab23e23533ad276aeec0156cebe89be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network-peering"></a>Maken, wijzigen of een virtueel netwerk-peering verwijderen

Meer informatie over hoe toocreate, wijzigen of verwijderen van een virtueel netwerk peering. Virtueel netwerk peering kunt u tooconnect twee virtuele netwerken in dezelfde Azure-locatie via Hallo hello Azure-backbone-netwerk. Zodra de peer is ingesteld, worden Hallo twee virtuele netwerken nog steeds beheerd als afzonderlijke resources. Resources in een virtueel netwerk communiceert Hallo dezelfde latentie en bandbreedte alsof Hallo resources zich in dezelfde Hallo virtueel netwerk. Als u niet bekend bent met het virtuele netwerk peering bent, raden wij aan lezen Hallo [peering Virtual network-overzicht](virtual-network-peering-overview.md) en voltooien Hallo [maken van een virtueel netwerk peering zelfstudie](virtual-network-create-peering.md), voordat wordt voltooid Hallo-taken in dit artikel.

## <a name="before-you-begin"></a>Voordat u begint

Voer Hallo taken voordat u stappen uitvoert in elke sectie van dit artikel te volgen:

- Bekijk Hallo [Azure beperkt](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artikel over de limieten voor peering.
- Meld u bij toohello Azure-portal, Azure-opdrachtregelinterface (CLI) of Azure PowerShell met een Azure-account. Als u nog een Azure-account hebt, zich aanmelden voor een [gratis proefaccount](https://azure.microsoft.com/free).
- Als u met behulp van PowerShell-opdrachten toocomplete taken in dit artikel [Azure PowerShell installeren en configureren](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat er Hallo meest recente versie van hello Azure PowerShell-cmdlets is geïnstalleerd. tooget help voor PowerShell-opdrachten, met voorbeelden, typ `get-help <command> -full`.
- Als u met behulp van Azure-opdrachtregelinterface (CLI) taken in dit artikel toocomplete opdrachten [installeren en configureren van Azure CLI Hallo](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure CLI is geïnstalleerd. tooget help voor CLI-opdrachten, typ `az <command> --help`. In plaats van installatie Hallo CLI en de vereisten, kunt u hello Azure Cloud-Shell. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hallo Cloud Shell heeft hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account. toouse hello Cloud-Shell, klikt u op Hallo Cloud Shell **> _** knop bovenaan Hallo Hallo [portal](https://portal.azure.com). 

## <a name="create-a-peering"></a>Een peering maken

>[!NOTE]
>Er zijn verschillende vereisten, beperkingen en overwegingen toosuccessfully maken van een virtueel netwerk peering. Voordat u maakt een peering, zorg ervoor dat u zelf hebt familiarized Hello [vereisten en beperkingen](#requirements-and-constraints) en [vereist machtigingen](#permissions).
>

1. Meld u bij toohello [portal](https://portal.azure.com) met een account dat is toegewezen Hallo nodig [rol of machtiging](#permissions).
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *virtuele netwerken*. Wanneer **virtuele netwerken** wordt weergegeven in zoekresultaten hello, klik erop. Selecteer niet **virtuele netwerken (klassiek)** als deze wordt weergegeven in de lijst hello, als u een peering van een virtueel netwerk te implementeren via het klassieke implementatiemodel Hallo niet maken.
3. In Hallo **virtuele netwerken** blade die wordt weergegeven, klikt u op Hallo virtueel netwerk die u wilt dat toocreate een peering voor.
4. Klik in deelvenster Hallo die wordt weergegeven voor Hallo virtuele netwerk die u hebt geselecteerd op **Peerings** in Hallo **instellingen** sectie.
5. Klik op **+ toevoegen**. 
6. <a name="add-peering"></a>In Hallo **toevoegen peering** blade invoeren of selecteren van waarden voor Hallo volgende instellingen:
    - **Naam:** Hallo-naam voor het Hallo-peering moet uniek zijn binnen het virtuele netwerk Hallo.
    - **Virtueel netwerk implementatiemodel:** selecteren welke deployment model Hallo virtuele netwerk dat u wilt dat toopeer met via is geïmplementeerd.
    - **Ik weet mijn resource-ID:** als u leestoegang toohello virtueel netwerk toopeer met gewenste hebt, laat u dit selectievakje uitgeschakeld. Als u geen leestoegang toohello virtuele netwerk of de gewenste toopeer met abonnement hebt, kunt u dit selectievakje inschakelen. Voer de volledige resource-ID van het virtuele netwerk van Hallo toopeer met in Hallo gewenste Hallo **Resource-ID** vak die werden weergegeven wanneer u Hallo selectievakje ingeschakeld. Hallo-resource-ID u moet voor een virtueel netwerk dat bestaat in dezelfde Azure Hallo [locatie](https://azure.microsoft.com/regions) als dit virtuele netwerk. Hallo volledige resource-ID lijkt vergelijkbaarte/abonnementen/<Id>/resourceGroups/ < resource-group-name > /providers/Microsoft.Network/virtualNetworks/ < virtuele-netwerk-name >. U kunt Hallo resource-ID ophalen voor een virtueel netwerk door het Hallo-eigenschappen voor een virtueel netwerk weer te geven. hoe tooview Hallo eigenschappen voor een virtueel netwerk, Zie toolearn [virtuele netwerken beheren](virtual-network-manage-network.md#view-vnet).
    - **Abonnement:** Selecteer Hallo [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) Hallo virtueel netwerk dat u wilt dat toopeer met. Een of meer abonnementen worden vermeld, afhankelijk van hoeveel abonnementen uw account leestoegang tot heeft. Als u dit selectievakje Hallo inschakelt **Resource-ID** selectievakje, deze instelling is niet beschikbaar. Als beide virtuele netwerken via Resource Manager zijn gemaakt, kunt u virtuele netwerken tot verschillende abonnementen behoren peer. Hallo mogelijkheid toopeer voor abonnementen die zijn gemaakt via verschillende implementatiemodellen is in de preview-versie. Registreren voor preview Hallo voordat het maken van een peering tussen virtuele netwerken die zijn geïmplementeerd via verschillende implementatiemodellen die bestaan uit verschillende abonnementen. Meer informatie over het tooregister voor Hallo preview en [peer virtuele netwerken die zijn gemaakt via verschillende implementatiemodellen tot verschillende abonnementen behoren](create-peering-different-deployment-models-subscriptions.md).
    - **Virtueel netwerk:** Selecteer Hallo virtueel netwerk dat u wilt dat toopeer met. U kunt een virtueel netwerk gemaakt via de Azure-implementatiemodel selecteren, maar Hallo virtuele netwerk moet zich in dezelfde locatie als Hallo virtueel netwerk u bent bezig met starten Hallo-peering van Hallo. U moet leestoegang toegang toohello virtueel netwerk voor toobe zichtbaar is in de lijst Hallo. Als een virtueel netwerk wordt weergegeven, maar niet-beschikbaar, is het mogelijk is het Hallo adresruimte voor het virtuele netwerk Hallo overlapt met adresruimte Hallo voor dit virtuele netwerk. Als het virtuele netwerk adresruimten elkaar overlappen, ze kunnen niet worden ingesteld als peer. Als u dit selectievakje Hallo inschakelt **Resource-ID** selectievakje, deze instelling is niet beschikbaar.
    - **Toestaan van toegang tot het virtuele netwerk:** Selecteer **ingeschakeld** (standaard) als u wilt dat tooenable communicatie tussen Hallo twee virtuele netwerken. Resources die zijn verbonden voor het inschakelen van communicatie tussen virtuele netwerken kunt tooeither virtueel netwerk toocommunicate met elkaar met dezelfde bandbreedte en latentie Hallo alsof ze verbonden toohello hetzelfde virtuele netwerk. Alle communicatie tussen bronnen in twee virtuele netwerken Hallo is via hello Azure particuliere netwerk. Hallo **VirtualNetwork** standaardlabel voor netwerkbeveiligingsgroepen omvat Hallo virtueel netwerk en virtuele netwerken peer is ingesteld. Hallo toolearn informatie over het netwerk beveiliging groep standaardtags lezen [netwerk beveiligingsgroepen overzicht](virtual-networks-nsg.md#default-tags) artikel.  Selecteer **uitgeschakelde** als u niet wilt dat verkeer tooflow toohello brengen virtueel netwerk. U kunt bijvoorbeeld selecteren **uitgeschakelde** als u een virtueel netwerk met een ander virtueel netwerk hebt brengen, maar soms toodisable netwerkverkeer tussen virtuele netwerken Hallo twee wilt. U kunt in-/ uitschakelen handiger vindt dan verwijderen en opnieuw maken van peerings. Wanneer deze instelling is uitgeschakeld, niet verkeersstroom tussen Hallo brengen virtuele netwerken.
    - **Toestaan van doorgestuurd verkeer:** Controleer dit vak tooallow doorgestuurd verkeer toohello brengen virtueel netwerk (verkeer dat afkomstig is niet in het virtuele netwerk Hallo brengen) tooflow toothis virtueel netwerk. Doorsturen van verkeer is gebruikelijk dat wanneer u een virtueel netwerkapparaat in het virtuele netwerk Hallo u bent peering met en de gebruiker gedefinieerde routes tooforward verkeer via virtuele netwerkapparaat Hallo gemaakt hebt geïmplementeerd. Als u laat dit selectievakje uitgeschakeld (standaard), kan niet doorgestuurd vanaf Hallo brengen virtueel netwerk verkeersstroom toothis virtueel netwerk. Inschakelen van deze mogelijkheid kunt u de Hallo doorgestuurd verkeer via het Hallo-peering, deze niet alle door de gebruiker gedefinieerde routes maken of virtuele apparaten. Gebruiker gedefinieerde routes en virtuele netwerkapparaten worden afzonderlijk gemaakt. Meer informatie over [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md).
    - **Gateway-doorvoer toestaan:** Schakel dit selectievakje in als u een virtueel netwerk gateway gekoppelde toothis virtueel netwerk hebt en wilt tooallow verkeer van Hallo tooflow virtueel netwerk via Hallo-gateway brengen. Dit virtuele netwerk is bijvoorbeeld mogelijk gekoppelde tooan on-premises netwerk via een virtuele netwerkgateway. In dit vak kunt verkeer van Hallo controleren brengen tooflow virtueel netwerk via Hallo gateway gekoppelde toothis virtueel netwerk. Als u dit selectievakje inschakelt, geen virtueel netwerk Hallo brengen een gateway is geconfigureerd. Hallo brengen virtuele netwerk moet hebben Hallo **externe gateway gebruiken** selectievakje wordt ingeschakeld wanneer andere virtuele netwerk toothis virtueel netwerk instellen van het Hallo-peering van Hallo. Als u laat dit selectievakje uitgeschakeld (standaard), verkeer van het virtuele netwerk Hallo brengen wel loopt toothis virtueel netwerk, maar kan niet door een virtueel netwerk voor virtueel netwerk gateway gekoppelde toothis stromen. Meer informatie over [virtuele netwerkgateways](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#s2smulti). 
    
    U kunt deze optie niet inschakelen als u een virtueel netwerk (Resource Manager) met een virtueel netwerk (klassiek) bent peering. Hoewel Hallo tussen twee virtuele netwerken hello verkeersstromen, kan niet Hallo virtuele netwerk (klassiek) verkeersstroom via een netwerk gateway gekoppelde toohello virtueel netwerk (Resource Manager).
    - **Externe gateways gebruiken:** dit vak tooallow verkeer van deze tooflow virtueel netwerk via een virtueel netwerk gateway gekoppelde toohello virtueel netwerk u bent peering met controleren. Hallo virtueel netwerk die u bent peering met heeft bijvoorbeeld een VPN-gateway gekoppeld waarmee communicatie tooan on-premises netwerk.  Dit selectievakje inschakelt, kunt verkeer van dit virtuele netwerk tooflow via Hallo VPN-gateway gekoppelde toohello brengen virtueel netwerk. Als u dit selectievakje inschakelt, Hallo brengen virtueel netwerk moet een virtueel netwerk gateway gekoppeld tooit hebben en moet Hallo **toestaan gateway onderweg** selectievakje ingeschakeld. Als u laat dit selectievakje uitgeschakeld (standaard), van virtueel netwerk Hallo brengen kunnen nog steeds verkeersstroom toothis virtuele netwerk, maar kan niet door een virtueel netwerk voor virtueel netwerk gateway gekoppelde toothis stromen. 
    
    U kunt deze optie niet inschakelen als u een virtueel netwerk (Resource Manager) met een virtueel netwerk (klassiek) bent peering. Hoewel Hallo tussen twee virtuele netwerken hello verkeersstromen, kan niet Hallo virtueel netwerk (Resource Manager) verkeersstroom via een netwerk gateway gekoppelde toohello virtueel netwerk (klassiek).
7. Klik op Hallo **OK** knop tooadd Hallo subnet toohello virtueel netwerk u hebt geselecteerd.

### <a name="commands"></a>Opdrachten

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ network vnet-peering maken](/cli/azure/network/vnet/peering#create?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Voeg AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|


### <a name="scenarios"></a>Scenario's

Een virtueel netwerk peering wordt gemaakt tussen virtuele netwerken die zijn gemaakt via Hallo dezelfde of verschillende implementatiemodellen die aanwezig zijn in dezelfde of verschillende abonnementen Hallo. Een stapsgewijze zelfstudie voor een van de volgende scenario's Hallo voltooien:
 
|Azure-implementatiemodel  | Abonnement  |
|---------|---------|
|Beide in Resource Manager |[Hetzelfde](virtual-network-create-peering.md)|
| |[Verschillend](create-peering-different-subscriptions.md)|
|Eén in Resource Manager, één klassiek     |[Hetzelfde](create-peering-different-deployment-models.md)|
| |[Verschillend](create-peering-different-deployment-models-subscriptions.md)|

## <a name="view-or-change-peering-settings"></a>Peering instellingen weergeven of wijzigen

1. Meld u bij toohello [portal](https://portal.azure.com) met een account dat is toegewezen Hallo nodig [rol of machtiging](#permissions).
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *virtuele netwerken*. Wanneer **virtuele netwerken** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **virtuele netwerken** blade die wordt weergegeven, klikt u op Hallo virtueel netwerk die u wilt dat toocreate een peering voor.
4. Klik in deelvenster Hallo die wordt weergegeven voor Hallo virtuele netwerk die u hebt geselecteerd op **Peerings** in Hallo **instellingen** sectie.
5. Klik op Hallo peering u tooview of wijzig de instellingen voor.
6. De juiste instelling Hallo wijzigen. Meer informatie over opties voor elke instelling in Hallo [stap 6](#add-peering) Hallo maakt u een peering sectie van dit artikel. 

    >[!NOTE]
    >Er zijn verschillende vereisten, beperkingen en overwegingen toosuccessfully maken van een virtueel netwerk peering. Voordat u maakt een peering, zorg ervoor dat u zelf hebt familiarized Hello [vereisten en beperkingen](#requirements-and-constraints) en [vereist machtigingen](#permissions).
    >

7. Klik op **Opslaan**.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ vnet peering lijst met netwerken](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist peerings voor een virtueel netwerk [az network vnet-peering weergeven](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow-instellingen voor een specifieke peering en [az netwerk vnet-peering update](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#update) toochange peering instellingen.|
|PowerShell|[Get-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/get-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve peering instellingen weergeven en [Set AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/set-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) toochange instellingen.|

## <a name="delete-a-peering"></a>Een peering verwijderen
Wanneer een peering wordt verwijderd, loopt verkeer van een virtueel netwerk niet langer toohello brengen virtueel netwerk. Wanneer u virtuele netwerken die zijn geïmplementeerd via Resource Manager brengen, heeft elke virtuele netwerk een peering toohello andere virtuele netwerk. Hoewel verwijderen Hallo-peering van een virtueel netwerk Hallo communicatie tussen virtuele netwerken Hallo uitschakelt, worden niet verwijderd Hallo-peering van Hallo andere virtuele netwerk. Hallo peering status voor peering die Hallo in Hallo bestaat andere virtueel netwerk is **verbroken**. Kan niet opnieuw maken Hallo peering totdat u opnieuw Hallo peering in het eerste virtuele netwerk Hallo maken en Hallo peering status voor beide virtuele wijzigingen te netwerken*verbonden*. 

Als u wilt dat virtuele netwerken toocommunicate soms, maar in plaats van het verwijderen van een peering, kunt u niet altijd Hallo instellen **toestaan van toegang tot het virtuele netwerk** instellen te**uitgeschakelde** in plaats daarvan. toolearn lezen hoe stap 6 van Hallo [maken van een peering](#create-peering) sectie van dit artikel. Wellicht eenvoudiger dan verwijderd en opnieuw gemaakt peerings netwerktoegang en uitschakelen.

1. Meld u bij toohello [portal](https://portal.azure.com) met een account dat is toegewezen Hallo nodig [rol of machtiging](#permissions).
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *virtuele netwerken*. Wanneer **virtuele netwerken** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **virtuele netwerken** blade die wordt weergegeven, klikt u op Hallo virtueel netwerk die u wilt dat toodelete een peering van.
4. Hallo blade die wordt weergegeven voor Hallo virtuele netwerk die u hebt geselecteerd, klikt u op **Peerings** onder **instellingen**.
5. In de lijst Hallo van peerings die wordt weergegeven in de blade Hallo peerings, klik met de rechtermuisknop Hallo peering u toodelete wilt, klikt u op **verwijderen**, klikt u vervolgens **Ja** toodelete hello peering van Hallo eerste virtuele netwerk.
6. Volledige Hallo vorige stappen toodelete hello peering van Hallo andere virtuele netwerk in het Hallo-peering.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ network vnet peering verwijderen](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Verwijder AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/remove-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="requirements-and-constraints"></a>Vereisten en beperkingen 

- Hallo virtuele netwerken die u peer moeten niet-overlappende IP-adresruimtes hebben.
- U kan adresruimten voor toevoegen, of adresruimten uit een virtueel netwerk verwijderen nadat een virtueel netwerk is gekoppeld aan een ander virtueel netwerk. adresruimten tooadd of verwijderen, verwijder Hallo peering, toevoegen of verwijder Hallo adresruimten en opnieuw maken Hallo-peering. tooadd-adresruimten aan of verwijder adresruimten van virtuele netwerken gelezen Hallo [maken, wijzigen of verwijderen, virtuele netwerken](virtual-network-manage-network.md#add-address-spaces) artikel. 
- U kunt twee virtuele netwerken te implementeren via Resource Manager of een virtueel netwerk is geïmplementeerd via Resource Manager met een virtueel netwerk te implementeren via het klassieke implementatiemodel Hallo peer. U kunt geen twee virtuele netwerken die zijn gemaakt via de klassieke implementatiemodel Hallo peer. Als u niet bekend met Azure-implementatiemodellen bent, leest u Hallo [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel. U kunt een [VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect twee virtuele netwerken via de klassieke implementatiemodel Hallo is gemaakt.
- Wanneer twee virtuele netwerken die zijn gemaakt via Resource Manager-peering, moet een peering worden geconfigureerd voor elke virtuele netwerk in het Hallo-peering. Wanneer u Hallo peering toohello tweede virtueel netwerk met de eerste virtuele netwerk hello maken, is het Hallo peering status *gestarte*.  Wanneer u het Hallo-peering van Hallo tweede virtuele netwerk toohello eerste virtuele netwerk maakt, wordt de status van de peering wordt *verbonden*. Als u Hallo peering status voor de eerste virtuele netwerk Hallo bekijkt, ziet u de status ervan is gewijzigd van *gestarte* te*verbonden*. Hallo-peering is niet tot stand gebracht totdat Hallo peering status voor beide virtuele netwerk peerings *verbonden*. 
- Wanneer u een virtueel netwerk via Resource Manager gemaakt met een virtueel netwerk gemaakt via de klassieke implementatiemodel Hallo-peering, configureer u alleen een peering voor Hallo virtueel netwerk geïmplementeerd via Resource Manager. U kunt niet configureren voor een virtueel netwerk (klassiek) of tussen twee virtuele netwerken die zijn geïmplementeerd via de klassieke implementatiemodel Hallo-peering. Wanneer u het Hallo-peering van Hallo virtueel netwerk (Resource Manager) toohello virtueel netwerk (klassiek) maakt, Hallo peering status is *Updating*, snel verandert vervolgens te*verbonden*.   
- Een peering tot stand is gebracht tussen twee virtuele netwerken. Peerings zijn niet transitief. Als u peerings tussen maakt:
    - VirtualNetwork1 & VirtualNetwork2
    - VirtualNetwork2 & VirtualNetwork3

  Er is geen peering tussen VirtualNetwork1 en VirtualNetwork3 via VirtualNetwork2. Als u een virtueel netwerk peering tussen VirtualNetwork1 en VirtualNetwork3 toocreate wilt, hebt u toocreate een peering tussen VirtualNetwork1 en VirtualNetwork3.
- Namen in virtuele netwerken peer is ingesteld met standaard Azure-naamomzetting kan niet worden omgezet. tooresolve namen in andere virtuele netwerken, moet u een aangepaste DNS-server. hoe tooset van uw eigen DNS-server, lees toolearn hello [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) artikel.
- Bronnen in beide virtuele netwerken in het Hallo-peering kunnen communiceren met elkaar Hello dezelfde bandbreedte en de latentie alsof ze zich in dezelfde Hallo virtueel netwerk. De grootte van elke virtuele machine heeft echter een eigen maximale netwerkbandbreedte. meer informatie over maximale netwerkbandbreedte voor andere virtuele machine-groottes lezen Hallo toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikelen de grootte van virtuele machine.
- U kunt virtuele netwerken zijn geïmplementeerd via Resource Manager die zijn in Hallo dezelfde peer of verschillende abonnementen behoren.
- U kunt virtuele netwerken die zijn geïmplementeerd via verschillende implementatiemodellen, zijn in Hallo dezelfde peer of verschillende abonnementen (preview). 
- Hallo abonnementen die beide virtuele netwerken in moeten zijn gekoppeld toohello dezelfde Azure Active Directory-tenant. Als u nog een AD-tenant hebt, kunt u snel [maken van een](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). U kunt een [VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect twee virtuele netwerken die bestaan uit verschillende abonnementen die zijn gekoppeld toodifferent Active Directory-tenants.
- Een virtueel netwerk kan worden ingesteld als peer tooanother virtueel netwerk, en ook verbonden tooanother virtueel netwerk met een virtueel netwerk van Azure-gateway. Wanneer u virtuele netwerken zijn verbonden via peering en een gateway, wordt verkeer tussen virtuele netwerken Hallo loopt via Hallo peeringconfiguratie in plaats van Hallo-gateway.
- Er wordt een nominaal bedrag in rekening gebracht voor inkomend en uitgaand verkeer dat gebruikmaakt van een virtueel netwerk-peering. Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/virtual-network).


## <a name="permissions"></a>Machtigingen

Hallo-accounts gebruiken van een virtueel netwerk peering toocreate beschikken Hallo benodigde rol of machtigingen. Bijvoorbeeld, als u twee virtuele netwerken met de naam myVnetA en myVnetB zijn peering, moet uw account worden toegewezen Hallo minimale rol of machtiging voor elke virtuele netwerk te volgen:
    
|Virtueel netwerk|Implementatiemodel|Rol|Machtigingen|
|---|---|---|---|
|myVnetA|Resource Manager|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Klassiek|[Inzender voor klassieke netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N.v.t.|
|myVnetB|Resource Manager|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Klassiek|[Inzender voor klassieke netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Meer informatie over [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) en het toewijzen van specifieke machtigingen te[aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (alleen voor Resource Manager).

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toocreate een [hub en spoke-netwerktopologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
