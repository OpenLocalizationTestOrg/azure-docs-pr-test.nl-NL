---
title: aaaCreate, wijzigen of verwijderen van een virtuele Azure-netwerk | Microsoft Docs
description: Meer informatie over hoe toocreate, wijzigen of verwijderen van een virtueel netwerk in Azure.
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
ms.openlocfilehash: 7dfe6632753182eae2a13bb0327f03f75e03d057
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network"></a>Maken, wijzigen of verwijderen van een virtueel netwerk

Meer informatie over hoe toocreate en delete een virtueel netwerk- en instellingen, zoals DNS-servers en IP-adres spaties, voor een bestaand virtueel netwerk.

Een virtueel netwerk is een weergave van uw eigen netwerk in Hallo cloud. Een virtueel netwerk is een logische isolatie van hello Azure-cloud die is toegewezen tooyour Azure-abonnement. Voor elk virtueel netwerk die u maakt, kunt u het volgende doen:
- Kies een adresruimte tooassign. Een adresruimte bestaat uit een of meer adresbereiken die zijn gedefinieerd met de notatie (Classless Inter-Domain Routing), zoals 10.0.0.0/16.
- Kies toouse hello Azure geleverde DNS-server, of uw eigen DNS-server gebruiken. Alle resources die verbonden toohello virtueel netwerk zijn zijn deze DNS-server tooresolve namen binnen het virtuele netwerk Hallo toegewezen.
- Segment Hallo virtueel netwerk in subnetten, elk met een eigen-adresbereik op in de adresruimte Hallo Hallo virtuele netwerk. hoe toocreate-, wijzigings- en delete-subnetten, Zie toolearn [toevoegen, wijzigen of verwijderen subnetten](virtual-network-manage-subnet.md).

Dit artikel wordt uitgelegd hoe toocreate, wijzigen en verwijderen van virtuele netwerken met hello Azure Resource Manager-implementatiemodel.

## <a name="before"></a>Voordat u begint

Voordat u Hallo-taken die worden beschreven in dit artikel, voert u Hallo volgende vereisten:

- Als u nieuwe tooworking met virtuele netwerken, wij raden u Hallo Oefening in [maken van uw eerste virtuele Azure-netwerk](virtual-network-get-started-vnet-subnet.md). In deze oefening kunt u vertrouwd raken met virtuele netwerken.
- toolearn over de limieten voor virtuele netwerken, Bekijk [Azure limieten](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Meld u aan toohello Azure-portal, Azure-opdrachtregelprogramma (Azure CLI) of Azure PowerShell Hallo met behulp van uw Azure-account. Als u geen Azure-account hebt, zich aanmelden voor een [gratis proefaccount](https://azure.microsoft.com/free).
- Als u van plan toouse PowerShell-toocomplete Hallo taken die worden beschreven in dit artikel bent opdrachten, moet u eerst [Azure PowerShell installeren en configureren](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u de meest recente versie Hallo van hello Azure PowerShell-cmdlets die zijn geïnstalleerd. tooget help voor PowerShell-opdrachten in de voorbeelden hello, voer `get-help <command> -full`.
- Als u van plan toouse Azure CLI-toocomplete Hallo taken die worden beschreven in dit artikel bent opdrachten, moet u eerst [Azure CLI installeren en configureren](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u de meest recente versie Hallo van Azure CLI is geïnstalleerd. Voer tooget hulp bij de Azure CLI-opdrachten `az <command> --help`.


## <a name="create-vnet"></a>Een virtueel netwerk maken

een virtueel netwerk toocreate:

1. Meld u aan toohello [portal](https://portal.azure.com) met een account met machtigingen voor Hallo netwerk rol van inzender (minimaal) voor uw abonnement is toegewezen. toolearn meer informatie over het toewijzen van rollen en machtigingen tooaccounts, Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Klik op **nieuw** > **Networking** > **virtueel netwerk**.
3. Op Hallo **virtueel netwerk** blade in Hallo **een implementatiemodel selecteren** vak, laat u **Resource Manager** geselecteerd en klik vervolgens op **maken**.
4. Op Hallo **virtueel netwerk maken** blade invoeren of Selecteer waarden voor Hallo na instellingen en klik vervolgens op **maken**:
    - **Naam**: Hallo-naam moet uniek zijn in Hallo [resourcegroep](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) dat u selecteert toocreate Hallo virtuele netwerk in. U kunt Hallo-naam niet wijzigen nadat Hallo virtueel netwerk is gemaakt. U kunt meerdere virtuele netwerken maken gedurende een bepaalde periode. Zie voor de naamgeving van suggesties [naamconventies](/azure/architecture/best-practices/naming-conventions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions). Na een naamgevingsconventie kan ervoor zorgen dat het eenvoudiger toomanage meerdere virtuele netwerken.
    - **Adresruimte**: Hallo-adresruimte opgeven in CIDR-notatie. Hallo-adresruimte die u definieert mag public of private (RFC 1918). Of u Hallo-adresruimte gedefinieerd als openbare of particuliere, is Hallo-adresruimte bereikbaar alleen via binnen Hallo virtueel netwerk, uit onderling verbonden virtuele netwerken, en een on-premises netwerken dat u toohello virtueel netwerk hebt verbonden. U kunt geen Hallo adresruimten volgende toevoegen:
        - 224.0.0.0/4 (Multicast)
        - 255.255.255.255/32 (Broadcast)
        - 127.0.0.0/8 (Loopback)
        - 169.254.0.0/16 (Link-local)
        - 168.63.129.16/32 (interne DNS)

      Hoewel u slechts één adresruimte definiëren kunt wanneer u Hallo virtueel netwerk maken, kunt u meer adresruimten toevoegen nadat Hallo virtueel netwerk is gemaakt. toolearn hoe een adres tooadd ruimte tooan bestaand virtueel netwerk, Zie [toevoegen of verwijderen van een adresruimte](#add-address-spaces) in dit artikel.

      >[!WARNING]
      >Als een virtueel netwerk adresruimten die met een ander virtueel netwerk of on-premises netwerk bevat overlappen, kunnen niet Hallo twee netwerken worden verbonden. Voordat u een adresruimte definiëren, moet u rekening houden of u tooconnect Hallo virtueel netwerk tooother virtuele netwerken of on-premises netwerken in Hallo toekomstige wilt misschien.
      >
      >

    - **De subnetnaam van het**: Hallo subnetnaam moet uniek zijn binnen het virtuele netwerk Hallo. U kunt Hallo subnetnaam niet wijzigen nadat het Hallo-subnet wordt gemaakt. Hallo-portal vereist dat u één subnet definieert bij het maken van een virtueel netwerk, zelfs als een virtueel netwerk is niet vereist toohave subnetten. U kunt slechts één subnet in Hallo-portal definiëren wanneer u een virtueel netwerk maken. U kunt later meer subnetten toohello virtueel netwerk toevoegen nadat Hallo virtueel netwerk is gemaakt. Zie voor een subnet tooa virtueel netwerk, tooadd [een subnet maken](virtual-network-manage-subnet.md#create-subnet) in [maken, wijzigen of verwijderen subnetten](virtual-network-manage-subnet.md). U kunt een virtueel netwerk met meerdere subnetten met behulp van Azure CLI of PowerShell maken.

      >[!TIP]
      >Soms maken beheerders verschillende subnetten toofilter of besturingselement verkeer routering tussen Hallo subnetten. Voordat u subnetten definiëren, houd rekening met hoe u mogelijk wilt toofilter en verkeer routeren tussen uw subnetten. toolearn meer informatie over het filteren van verkeer tussen subnetten, Zie [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md). Azure automatisch routes verkeer tussen subnetten, maar u kunt onderdrukken Azure standaardroutes. toolearn hoe toooverride Azure standaardroutering subnet verkeer, Zie [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md).
      >

    - **Adresbereik van**: Hallo bereik moet zich binnen het Hallo-adresruimte die u hebt ingevoerd voor het virtuele netwerk Hallo. Hallo kleinste bereik die kunt u opgeven is slechts/29, waarmee u acht IP-adressen voor Hallo subnet. Azure reserves eerst Hallo en los deze laatste in elk subnet voor het protocol overeenstemming. Drie extra adressen zijn gereserveerd voor gebruik van Azure service. Als gevolg hiervan is een virtueel netwerk met een adresbereik subnet van slechts/29 slechts drie bruikbare IP-adressen. Als u een VPN-gateway van virtueel netwerk tooa tooconnect plant, moet u een gatewaysubnet maken. Meer informatie over [specifiek adresbereik overwegingen voor het gateway-subnetten](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). U kunt Hallo-adresbereik wijzigen nadat Hallo subnet is gemaakt, klikt u onder bepaalde omstandigheden. hoe een adresbereik subnet toochange zien toolearn [subnetinstellingen wijzigen](#change-subnet) in [toevoegen, wijzigen of verwijderen subnetten](virtual-network-manage-subnet.md).
    - **Abonnement**: Selecteer een [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). U kunt geen hello gebruiken hetzelfde virtuele netwerk in meer dan één Azure-abonnement. U kunt echter een virtueel netwerk in een abonnement toovirtual-netwerken in andere abonnementen verbinden. virtuele netwerken tot verschillende abonnementen behoren, tooconnect gebruik Azure VPN-Gateway of virtueel netwerk peering. Een Azure-resource dat u verbinding toohello virtueel netwerk maakt moet zich in Hallo hetzelfde abonnement als Hallo virtuele netwerk.
    - **Resourcegroep**: Selecteer een bestaande [resourcegroep](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) of maak een nieuwe. Een Azure-resource dat u verbinding toohello virtueel netwerk maakt mag in Hallo dezelfde resourcegroep als Hallo virtueel netwerk of in een andere resourcegroep.
    - **Locatie**: Selecteer een Azure [locatie](https://azure.microsoft.com/regions/), ook wel aangeduid als een regio. Een virtueel netwerk kan slechts één Azure-locatie liggen. U kunt echter een virtueel netwerk in één locatie tooa virtueel netwerk in een andere locatie verbinden via een VPN-gateway. Een Azure-resource dat u verbinding toohello virtueel netwerk maakt moet zich in Hallo dezelfde locatie als Hallo virtuele netwerk.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|Azure CLI|[AZ network vnet maken](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Nieuwe-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name = "view-vnet"></a>Virtuele netwerken weergeven en instellingen

tooview virtuele netwerken en instellingen voor:

1. Meld u aan toohello [portal](https://portal.azure.com) met een account met machtigingen voor Hallo netwerk rol van inzender (minimaal) voor uw abonnement is toegewezen. toolearn meer informatie over het toewijzen van rollen en machtigingen tooaccounts, Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Voer in de portal zoekvak Hallo **virtuele netwerken**. Klik in de zoekresultaten Hallo **virtuele netwerken**.
3. Op Hallo **virtuele netwerken** blade, klikt u op Hallo virtueel netwerk dat u wilt dat instellingen voor tooview.
4. Hallo worden volgende instellingen weergegeven op de blade Hallo voor Hallo virtueel netwerk die u hebt geselecteerd:
    - **Overzicht**: bevat informatie over Hallo virtueel netwerk, met inbegrip van adresruimte en DNS-servers. Hallo volgende schermafbeelding ziet u Hallo overzicht van instellingen voor een virtueel netwerk met de naam **MyVNet**:

        ![Network interface-overzicht](./media/virtual-network-manage-network/vnet-overview.png)

      Op Hallo **overzicht** blade kunt u een virtueel netwerk tooa andere abonnement of resourcegroep groep verplaatsen. hoe toomove een virtueel netwerk, Zie toolearn [verplaatsen van resources tooa andere resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Hallo artikel bevat een overzicht van vereisten en hoe toomove resources met behulp van hello Azure-portal, PowerShell en Azure CLI. Alle resources die verbonden toohello virtueel netwerk zijn moeten verplaatsen met Hallo virtueel netwerk.
    - **Adresruimte**: Hallo adresruimten die zijn toegewezen toohello virtueel netwerk staan. hoe tooadd en verwijderen van een adresruimte voltooid toolearn Hallo stappen in [toevoegen of verwijderen van een adresruimte](#address-spaces) in dit artikel.
    - **Verbonden apparaten**: alle bronnen die verbonden toohello virtueel netwerk zijn staan. In Hallo voorgaande schermafbeelding, zijn drie netwerkinterfaces en één load balancer verbonden toohello virtueel netwerk. De nieuwe resources die u maakt en toohello virtueel netwerk verbinden worden weergegeven. Als u een resource die verbonden toohello virtueel netwerk is verwijdert, worden deze niet meer weergegeven in het Hallo-lijst.
    - **Subnetten**: een lijst met subnetten die in het virtuele netwerk hello voorkomen wordt weergegeven. hoe tooadd en wordt verwijderd, een subnet, Zie toolearn [een subnet maken](virtual-network-manage-subnet.md#create-subnet) en [verwijderen van een subnet](virtual-network-manage-subnet.md#delete-subnet) in [toevoegen, wijzigen of verwijderen subnetten](virtual-network-manage-subnet.md).
    - **DNS-servers**: U kunt opgeven of hello Azure interne DNS-server of een aangepaste DNS-server biedt naamomzetting voor apparaten die verbonden toohello virtueel netwerk zijn. Wanneer u een virtueel netwerk met behulp van hello Azure-portal maakt, worden de Azure DNS-servers voor naamomzetting binnen een virtueel netwerk standaard gebruikt. toomodify hello DNS-servers, volledige Hallo stappen in [toevoegen, wijzigen of verwijderen van een DNS-server](#dns-servers) in dit artikel.
    - **Peerings**: als er bestaande peerings in Hallo abonnement, worden deze hier weergegeven. U kunt instellingen voor bestaande peerings weergeven of maken, wijzigen of verwijderen van peerings. toolearn meer informatie over de peerings, Zie [virtuele netwerk peering](virtual-network-peering-overview.md).
    - **Eigenschappen**: geeft instellingen over Hallo virtueel netwerk, met inbegrip van de resource-ID Hallo van het virtuele netwerk en hello Azure-abonnement in.
    - **Diagram**: Hallo diagram biedt een visuele representatie van alle apparaten die verbonden toohello virtueel netwerk zijn. Hallo diagram heeft enkele belangrijke informatie over het Hallo-apparaten. een apparaat in deze weergave in Hallo diagram toomanage klikt u op Hallo-apparaat.
    - **Algemene instellingen voor Azure**: toolearn meer informatie over algemene instellingen van Azure, Zie Hallo volgende informatie:
        *   [Activiteitenlogboek](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)
        *   [Toegangsbeheer (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)
        *   [Tags](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)
        *   [Hiermee vergrendelt u](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
        *   [Automatiseringsscript](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|Azure CLI|[AZ network vnet show](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork/?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="add-address-spaces"></a>Toevoegen of verwijderen van een adresruimte

U kunt toevoegen en verwijderen van adresruimten voor virtueel netwerk. Een adresruimte moet worden opgegeven in CIDR-notatie en kan niet overlappen met andere adresruimten binnen Hallo hetzelfde virtuele netwerk. Hallo-adresruimten die u definieert mag public of private (RFC 1918). Of u Hallo-adresruimte gedefinieerd als openbare of particuliere, is Hallo-adresruimte bereikbaar alleen via binnen Hallo virtueel netwerk, uit onderling verbonden virtuele netwerken, en een on-premises netwerken dat u toohello virtueel netwerk hebt verbonden. U kunt geen Hallo adresruimten volgende toevoegen:

- 224.0.0.0/4 (Multicast)
- 255.255.255.255/32 (Broadcast)
- 127.0.0.0/8 (Loopback)
- 169.254.0.0/16 (Link-local)
- 168.63.129.16/32 (interne DNS)

tooadd of verwijder een adresruimte:

1. Meld u aan toohello [portal](https://portal.azure.com) met een account met machtigingen voor Hallo netwerk rol van inzender (minimaal) voor uw abonnement is toegewezen. toolearn meer informatie over het toewijzen van rollen en machtigingen tooaccounts, Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Voer in de portal zoekvak Hallo **virtuele netwerken**. Selecteer in de zoekresultaten hello, **virtuele netwerken**.
3. Op Hallo **virtuele netwerken** blade, klikt u op Hallo virtueel netwerk waarvoor u wilt dat tooadd of verwijderen van een adresruimte.
4. Op Hallo virtuele netwerk blade onder **instellingen**, klikt u op **adresruimte**.
5. Op Hallo blade voor Hallo-adresruimte, voert u een Hallo volgende opties:
    - **Voeg een adresruimte**: nieuwe adresruimte Hallo invoeren. Hallo-adresruimte kan niet overlappen met een bestaande adresruimte die is gedefinieerd voor het virtuele netwerk Hallo.
    - **Verwijderen van een adresruimte**: met de rechtermuisknop op een adresruimte en klik vervolgens op **verwijderen**. Als een subnet in de adresruimte hello bestaat, kunt u het Hallo-adresruimte niet verwijderen. een adresruimte tooremove, moet u eerst verwijderen subnetten (en alle bronnen die verbonden toohello subnetten zijn) die zijn opgenomen in het Hallo-adresruimte.
6. Klik op **Opslaan**.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|Azure CLI|Alleen Resource Manager|[AZ network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="dns-servers"></a>Toevoegen, wijzigen of verwijderen van een DNS-server

Alle virtuele machines die verbonden toohello virtueel netwerk zijn registreren met Hallo DNS-servers die u voor het virtuele netwerk Hallo opgeeft. Gebruiken ze ook Hallo opgegeven DNS-server voor naamomzetting. Elke netwerkinterface (NIC) in een virtuele machine kan hebben een eigen DNS-serverinstellingen. Als een NIC een eigen DNS-serverinstellingen heeft, overschrijven ze Hallo DNS-serverinstellingen voor Hallo virtueel netwerk. toolearn meer informatie over NIC DNS-instellingen, Zie [Network interface-taken en instellingen](virtual-network-network-interface.md#change-dns-servers). toolearn meer informatie over naamomzetting voor VM's en rolinstanties in Azure Cloud Services, Zie [naamomzetting voor VM's en rolexemplaren](virtual-networks-name-resolution-for-vms-and-role-instances.md). tooadd, wijzigen of verwijderen van een DNS-server:

1. Meld u aan toohello [portal](https://portal.azure.com) met een account met machtigingen voor Hallo netwerk rol van inzender (minimaal) voor uw abonnement is toegewezen. toolearn meer informatie over het toewijzen van rollen en machtigingen tooaccounts, Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Typ in de portal zoekvak Hallo **virtuele netwerken**. Selecteer in de zoekresultaten hello, **virtuele netwerken**.
3. Op Hallo **virtuele netwerken** blade, klikt u op Hallo virtuele netwerk die u wilt dat toochange DNS-instellingen voor.
4. Op Hallo virtuele netwerk blade onder **instellingen**, klikt u op **DNS-servers**.
5. Selecteer een van de volgende opties op het Hallo-blade met een lijst met DNS-servers Hallo:
    - **Standaard (Azure verschafte)**: alle resourcenamen en privé IP-adressen automatisch worden geregistreerd toohello Azure DNS-servers zijn. U kunt omzetten van namen tussen alle bronnen die verbonden toohello zijn hetzelfde virtuele netwerk. U kunt deze tooresolve optienamen niet gebruiken in virtuele netwerken. de namen van de tooresolve tussen virtuele netwerken, moet u een aangepaste DNS-server.
    - **Aangepaste**: U kunt een of meer servers toevoegen, up toohello Azure beperken voor een virtueel netwerk. toolearn meer informatie over DNS-server-limieten, Zie [Azure limieten](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#virtual-networking-limits-classic). Hebt u Hallo volgende opties:
        - **Toevoegen van een adres**: Hallo tooyour virtueel netwerk DNS-servers serverlijst wordt toegevoegd. Deze optie wordt ook Hallo DNS-server registreren met Azure. Als u hebt al een DNS-server geregistreerd met Azure, kunt u die DNS-server in de lijst Hallo.
        - **Verwijder een adres**: klik op volgende toohello-server die u wilt tooremove, **X**. Hallo-server verwijdert verwijderen Hallo-server alleen uit deze lijst virtueel netwerk. Hallo DNS-server blijft geregistreerd in Azure voor uw andere virtuele netwerken toouse.
        - **DNS-serveradressen rangschikken**: het is belangrijk tooverify weer te geven die uw DNS-servers in Hallo corrigeren volgorde voor uw omgeving. Een lijst met DNS-server worden gebruikt in Hallo volgorde waarin ze worden opgegeven. Ze werken niet als de installatie van een round robin. Als eerste DNS-server in de lijst Hallo Hallo kan worden bereikt, gebruikt Hallo-client die DNS-server, ongeacht of Hallo DNS-server correct werkt. Verwijder alle Hallo DNS-servers die worden vermeld en vervolgens weer in de gewenste volgorde Hallo toe te voegen.
        - **Een adres wijzigen**: Hallo DNS-server in de lijst Hallo markeren en voer vervolgens de nieuwe naam Hallo.
6. Klik op **Opslaan**.
7. Opnieuw opstarten Hallo virtuele machines die verbonden toohello virtueel netwerk, zijn zodat ze Hallo nieuwe DNS-serverinstellingen worden toegewezen. Virtuele machines blijven toouse hun huidige DNS-instellingen totdat ze opnieuw worden gestart.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|Azure CLI|[AZ network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="delete-vnet"></a>Een virtueel netwerk verwijderen

U kunt een virtueel netwerk alleen verwijderen als er geen verbonden tooit resources zijn. Als er resources verbonden tooany subnet binnen het virtuele netwerk hello, moet u eerst Hallo-resources die verbonden tooall subnetten in het virtuele netwerk Hallo zijn verwijderen. Hallo u stappen ondernemen toodelete is een resource afhankelijk van Hallo resource. hoe toodelete-resources die zijn verbonden toosubnets Lees toolearn Hallo documentatie voor elk resourcetype die u wilt toodelete. een virtueel netwerk toodelete:

1. Meld u aan toohello [portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. toolearn meer informatie over het toewijzen van rollen en machtigingen tooaccounts, Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Voer in de portal zoekvak Hallo **virtuele netwerken**. Klik in de zoekresultaten Hallo **virtuele netwerken**.
3. Op Hallo **virtuele netwerken** blade, selecteer Hallo virtueel netwerk gewenste toodelete.
4. Op de blade virtueel netwerk hello, verbonden tooconfirm er zijn geen apparaten toohello virtueel netwerk, onder **instellingen**, klikt u op **verbonden apparaten**. Als er verbonden apparaten, moet u deze verwijderen voordat u het virtuele netwerk Hallo kunt verwijderen. Als er geen verbonden apparaten zijn, klikt u op **overzicht**.
5. Klik op Hallo Hallo bovenaan de blade Hallo in **verwijderen** pictogram.
6. tooconfirm hello verwijdering van Hallo virtueel netwerk, klikt u op **Ja**.


**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|Azure CLI|[Azure network vnet verwijderen](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetwork](/powershell/module/azurerm.network/remove-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="next-steps"></a>Volgende stappen

- een virtuele machine toocreate en sluit u het virtuele netwerk tooa, Zie [een virtueel netwerk maken en verbinding maken met virtuele machines](virtual-network-get-started-vnet-subnet.md#create-vms).
- toofilter netwerkverkeer tussen subnetten binnen een virtueel netwerk, Zie [netwerkbeveiligingsgroepen maken](virtual-networks-create-nsg-arm-pportal.md).
- Zie voor een virtueel netwerk tooanother virtueel netwerk, toopeer [peering van een virtueel netwerk maken](virtual-network-create-peering.md#portal).
- Zie toolearn over opties voor het verbinden van een virtueel netwerk tooan on-premises netwerk [over VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams).
