---
title: aaaConfigure IP-adressen voor een Azure-netwerk-interface | Microsoft Docs
description: Ontdek hoe tooadd, wijzigen en verwijderen van persoonlijke en openbare IP-adressen voor een netwerkinterface.
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
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 1e5ea6c65d93be9b1fda5d807500a0823c94c89c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-remove-ip-addresses-for-an-azure-network-interface"></a>Toevoegen, wijzigen of verwijderen van IP-adressen voor een Azure-netwerk-interface

Ontdek hoe tooadd, wijzigen en verwijderen van openbare en particuliere IP-adressen voor een netwerkinterface. Privé IP-adressen die zijn toegewezen tooa netwerkinterface inschakelen voor een virtuele machine toocommunicate met andere resources in een Azure-netwerk en verbonden netwerken. Een persoonlijke IP-adres kan ook uitgaande communicatie toohello Internet met behulp van een onvoorspelbare IP-adres. Een [openbaar IP-adres](virtual-network-public-ip-address.md) toegewezen tooa netwerkinterface kan binnenkomende communicatie tooa virtuele machine van Hallo Internet. Hallo-adres kan ook uitgaande communicatie van Hallo virtuele machine toohello Internet met behulp van een voorspelbare IP-adres. Zie voor meer informatie [inzicht in uitgaande verbindingen in Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Als u toocreate moet, wijzigen of verwijderen van een netwerkinterface lezen Hallo [beheren van een netwerkinterface](virtual-network-network-interface.md) artikel. Als u moet tooadd netwerkinterfaces tooor verwijderen netwerkinterfaces van een virtuele machine, Hallo lezen [toevoegen of verwijderen van netwerkinterfaces](virtual-network-network-interface-vm.md) artikel. 


## <a name="before-you-begin"></a>Voordat u begint

Volledige Hallo taken voordat u een volgende stappen in elke sectie van dit artikel:

- Bekijk Hallo [Azure beperkt](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artikel over de limieten voor openbare en particuliere IP-adressen.
- Meld u bij Azure toohello [portal](https://portal.azure.com), Azure-opdrachtregelinterface (CLI) of Azure PowerShell gebruiken met een Azure-account. Als u nog een Azure-account hebt, zich aanmelden voor een [gratis proefaccount](https://azure.microsoft.com/free).
- Als u met behulp van PowerShell-opdrachten toocomplete taken in dit artikel [Azure PowerShell installeren en configureren](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure PowerShell commandlets geïnstalleerd. tooget help voor PowerShell-opdrachten, met voorbeelden, typ `get-help <command> -full`.
- Als u met behulp van Azure-opdrachtregelinterface (CLI) taken in dit artikel toocomplete opdrachten [installeren en configureren van Azure CLI Hallo](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure CLI is geïnstalleerd. tooget help voor CLI-opdrachten, typ `az <command> --help`. In plaats van installatie Hallo CLI en de vereisten, kunt u hello Azure Cloud-Shell. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft. toouse hello Cloud-Shell, klikt u op Hallo Cloud Shell **> _** knop bovenaan Hallo Hallo [portal](https://portal.azure.com).

## <a name="add-ip-addresses"></a>IP-adressen toevoegen

U kunt toevoegen als veel [persoonlijke](#private) en [openbare](#public) [IPv4](#ipv4) adressen als de netwerkinterface nodig tooa binnen de grenzen Hallo worden vermeld in Hallo [Azure limieten ](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artikel. U kunt Hallo portal tooadd een bestaande netwerkinterface van IPv6-adres tooan niet gebruiken (Hoewel u Hallo portal tooadd persoonlijke IPv6-adres, tooa netwerkinterface gebruiken kunt bij het maken van de netwerkinterface Hallo). U kunt gebruik PowerShell of CLI tooadd een persoonlijke IPv6-adres tooone Hallo [secundaire IP-configuratie](#secondary) (zo lang er zijn geen bestaande secundaire IP-configuraties) de interface die niet voor een bestaand netwerk tooa virtuele gekoppeld machine. U kunt elk hulpprogramma tooadd een openbare IPv6-adres tooa-netwerkinterface niet gebruiken. Zie [IPv6](#ipv6) voor meer informatie over het gebruik van IPv6-adressen. 

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *netwerkinterfaces*. Wanneer **netwerkinterfaces** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **netwerkinterfaces** blade die wordt weergegeven, klikt u op Hallo netwerkinterface gewenste tooadd een IPv4-adres voor.
4. Klik op **IP-configuraties** in Hallo **instellingen** sectie van de blade Hallo voor Hallo-netwerkinterface die u hebt geselecteerd.
5. Klik op **+ toevoegen** in Hallo-blade die wordt geopend voor IP-configuraties.
6. Hallo volgende opgeven en klik vervolgens op **OK** tooclose hello **toevoegen IP-configuratie** blade:

    |Instelling|Vereist?|Details|
    |---|---|---|
    |Naam|Ja|Moet uniek zijn voor de netwerkinterface Hallo|
    |Type|Ja|Omdat u een bestaande netwerkinterface van IP-configuratie tooan wilt toevoegen, en elke netwerkinterface moet een [primaire](#primary) IP-configuratie, de enige optie is **secundaire**.|
    |Methode voor het privé IP-adres toewijzen|Ja|[**Dynamische** ](#dynamic) adressen kunnen wijzigen als Hallo virtuele machine opnieuw wordt opgestart nadat in het Hallo (toewijzing ongedaan gemaakt) staat gestopt. Azure wijst een beschikbaar adres uit het Hallo-adresruimte van Hallo subnet Hallo-netwerkinterface is gekoppeld aan. [**Statische** ](#static) adressen worden niet vrijgegeven tot Hallo netwerkinterface worden verwijderd. Geef een IP-adres van Hallo subnet-ruimte adresbereik dat momenteel niet gebruikt door een ander IP-configuratie.|
    |Openbaar IP-adres|Nee|**Uitgeschakeld:** geen openbare IP-adres-resource is momenteel gekoppeld toohello IP-configuratie. **Ingeschakeld:** Selecteer een bestaand openbaar IPv4-IP-adres of een nieuwe maken. hoe een openbaar IP-adres toocreate Lees toolearn hello [openbare IP-adressen](virtual-network-public-ip-address.md#create-a-public-ip-address) artikel.|
7. Secundaire persoonlijke IP-adressen toohello virtuele machine besturingssysteem handmatig toevoegen door te voeren Hallo-instructies in Hallo [toovirtual machine besturingssystemen voor meerdere IP-adressen toewijzen](virtual-network-multiple-ip-addresses-portal.md#os-config) artikel. Zie [persoonlijke](#private) IP-adressen voor speciale overwegingen voor het handmatig toevoegen van IP-adressen tooa virtuele machine-besturingssysteem. Voeg een openbaar IP-adressen toohello virtuele machine besturingssysteem niet.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ netwerk nic ip-configuratie maken](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Voeg AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/add-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-ip-address-settings"></a>Instellingen voor IP-adres wijzigen

Mogelijk moet u toochange Hallo methode voor het toewijzen van een IPv4-adres wijzigen Hallo statische IPv4-adres of wijziging Hallo openbaar IP-adres toegewezen tooa netwerkinterface. Als u Hallo particulier IPv4-adres van een secundaire IP-configuratie die is gekoppeld aan een secundaire netwerkinterface in een virtuele machine wilt wijzigen (meer informatie over [primaire en secundaire netwerkinterfaces](virtual-network-network-interface-vm.md#about)), plaats Hallo virtuele machine in Hallo gestopt (toewijzing ongedaan gemaakt) status voordat voltooid Hallo stappen te volgen: 

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *netwerkinterfaces*. Wanneer **netwerkinterfaces** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **netwerkinterfaces** blade die wordt weergegeven, klikt u op Hallo netwerkinterface u wilt dat tooview of IP-adresinstellingen voor wijzigen.
4. Klik op **IP-configuraties** in Hallo **instellingen** sectie van de blade Hallo voor Hallo-netwerkinterface die u hebt geselecteerd.
5. Klik op de gewenste toomodify in de lijst Hallo in Hallo-blade die wordt geopend voor IP-configuraties van Hallo IP-configuratie.
6. Hallo instellingen wijzigen, indien gewenst, met Hallo informatie over het Hallo-instellingen in stap 6 van Hallo [toevoegen van een IP-configuratie](#create-ip-config) sectie van dit artikel. Klik op **opslaan** tooclose Hallo blade voor Hallo IP-configuratie die u hebt gewijzigd.

>[!NOTE]
>Als de primaire netwerkinterface Hallo meerdere IP-configuraties heeft en u Hallo privé IP-adres van Hallo primaire IP-configuratie wijzigen, moet u handmatig opnieuw toewijzen Hallo primaire en secundaire IP-adressen toohello netwerkinterface in Windows (niet vereist voor Linux). Hallo toomanually toegewezen IP-adressen tooa netwerkinterface binnen een besturingssysteem lezen [meerdere IP-adressen toewijzen toovirtual machines](virtual-network-multiple-ip-addresses-portal.md#os-config) artikel. Zie [persoonlijke](#private) IP-adressen voor speciale overwegingen voor het handmatig toevoegen van IP-adressen tooa virtuele machine-besturingssysteem. Voeg een openbaar IP-adressen toohello virtuele machine besturingssysteem niet.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ netwerk nic IP-configuratie bijwerken](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRMNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="remove-ip-addresses"></a>IP-adressen verwijderen

U kunt verwijderen [persoonlijke](#private) en [openbare](#public) IP-adressen uit een netwerkinterface, maar een netwerkinterface moet altijd ten minste één tooit voor persoonlijke IPv4-adres is toegewezen.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *netwerkinterfaces*. Wanneer **netwerkinterfaces** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **netwerkinterfaces** blade die wordt weergegeven, klikt u op Hallo netwerkinterface gewenste tooremove IP-adressen uit.
4. Klik op **IP-configuraties** in Hallo **instellingen** sectie van de blade Hallo voor Hallo-netwerkinterface die u hebt geselecteerd.
5. Met de rechtermuisknop op een [secundaire](#secondary) IP-configuratie (Hallo kan niet worden verwijderd [primaire](#primary) configuration) toodelete wilt, klikt u **verwijderen**, klikt u vervolgens op **Ja**  tooconfirm Hallo verwijderen. Als Hallo configuratie had een openbare IP-adres resource gekoppeld tooit, Hallo resource is ontkoppeld van Hallo IP-configuratie, maar Hallo resource wordt niet verwijderd.
6. Sluit Hallo **IP-configuraties** blade.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ netwerk nic IP-configuratie verwijderen](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Verwijder AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/remove-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="ip-configurations"></a>IP-configuraties

[Persoonlijke](#private) en (optioneel) [openbare](#public) IP-adressen zijn toegewezen tooone of meer IP-configuraties toegewezen tooa netwerkinterface. Er zijn twee soorten IP-configuraties:

### <a name="primary"></a>Primair

Elke netwerkinterface is één primaire IP-configuratie worden toegewezen. Een primaire IP-configuratie:

- Heeft een [persoonlijke](#private) [IPv4](#ipv4) tooit-adres is toegewezen. U kunt een persoonlijk niet toewijzen [IPv6](#ipv6) adres tooa primaire IP-configuratie.
- Mogelijk beschikt over een [openbare](#public) tooit voor IPv4-adres is toegewezen. U kunt een openbare IPv6-adres tooa primaire of secundaire IP-configuratie niet toewijzen. U kunt wel, een openbare IPv6-adres tooan Azure load balancer, kunt laden toewijzen saldo verkeer tooa virtuele machine van persoonlijke IPv6-adres. Zie voor meer informatie [details en beperkingen voor IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations).

### <a name="secondary"></a>Secundair

Bovendien tooa primaire IP-configuratie, een netwerkinterface kan nul of meer secundaire IP-configuraties hebben tooit toegewezen. Een secundaire IP-configuratie:

- Moet een particulier IPv4- of IPv6-adres is toegewezen tooit hebben. Als Hallo adres IPv6, kan Hallo netwerkinterface slechts één secundaire IP-configuratie hebben. Als Hallo adres IPv4, misschien Hallo netwerkinterface secundaire IP-configuraties met meerdere tooit toegewezen. toolearn meer informatie over hoeveel persoonlijke en openbare IPv4-adressen kunnen worden toegewezen tooa netwerkinterface, Zie Hallo [Azure beperkt](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artikel.  
- Wellicht ook een tooit openbare IPv4-adres is toegewezen als Hallo privé IP-adres IPv4 is. Als het privé IP-adres Hallo IPv6 is, kunt u een openbaar IPv4- of IPv6-toohello IP-adresconfiguratie niet toewijzen. Toewijzen van meerdere IP-adressen tooa-netwerkinterface is nuttig in scenario's, zoals:
    - Het hosten van meerdere websites of services met verschillende IP-adressen en SSL-certificaten op één server.
    - Een virtuele machine fungeert als een virtueel netwerkapparaat, zoals een firewall of een load balancer.
    - Hallo mogelijkheid tooadd van Hallo persoonlijke IPv4-voor een Hallo netwerkinterfaces tooan Azure Load Balancer back-end-adresgroep adressen. In de afgelopen hello, kan alleen Hallo primaire IPv4-adres voor de primaire netwerkinterface Hallo tooa back-end-pool worden toegevoegd. toolearn meer informatie over hoe tooload balans vinden tussen configuraties met meerdere IPv4 Zie Hallo [meerdere IP-configuraties voor taakverdeling](../load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel. 
    - Hallo mogelijkheid tooload saldo één IPv6-adres is toegewezen tooa netwerkinterface. toolearn meer informatie over hoe tooload balans vinden tussen tooa persoonlijke IPv6-adres, Zie Hallo [taakverdeling van IPv6-adressen](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel.


## <a name="address-types"></a>Adrestypen

Kunt u de volgende soorten IP-adressen tooan Hallo toewijzen [IP-configuratie](#ip-configurations):

### <a name="private"></a>Privé

Persoonlijke [IPv4](#ipv4) adressen inschakelen in een virtuele machine toocommunicate met andere resources in een virtueel netwerk of andere aangesloten netwerken. Een virtuele machine kan niet worden gecommuniceerd naar binnenkomende noch kan Hallo virtuele machine communiceren met een particulier uitgaande [IPv6](#ipv6) adres, met één uitzondering. Een virtuele machine kan communiceren met hello Azure load balancer met een IPv6-adres. Zie voor meer informatie [details en beperkingen voor IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations). 

Standaard hello Azure DHCP-servers Hallo particulier IPv4-adres voor Hallo toewijzen [primaire IP-configuratie](#primary) van Hallo network interface toohello netwerkinterface binnen Hallo virtuele machine-besturingssysteem. Tenzij nodig, moet u nooit handmatig instellen Hallo IP-adres van een netwerkinterface in besturingssysteem Hallo virtuele machine. 

> [!WARNING]
> Als het IPv4-adres worden ingesteld omdat Hallo primaire IP-adres van een netwerkinterface in het besturingssysteem van een virtuele machine ooit anders dan Hallo particulier IPv4-adres toegewezen toohello primaire IP-configuratie van de primaire netwerkinterface Hallo Hallo tooa gekoppeld virtuele machine in Azure, verliest u connectiviteit toohello virtuele machine.

Er zijn scenario's waarin het benodigde toomanually set Hallo IP-adres van een netwerkinterface in besturingssysteem Hallo virtuele machine. Bijvoorbeeld, moet u handmatig Hallo primaire en secundaire IP-adressen van een Windows-besturingssysteem instellen bij het toevoegen van meerdere IP-adressen tooan virtuele machine van Azure. Voor een virtuele Linux-machine moet u mogelijk alleen toomanually set Hallo secundaire IP-adressen. Zie [toevoegen IP-adressen tooa VM besturingssysteem](virtual-network-multiple-ip-addresses-portal.md#os-config) voor meer informatie. Wanneer u handmatig Hallo IP-adres binnen het Hallo-besturingssysteem hebt ingesteld, wordt het aanbevolen Hallo adressen toohello IP-configuratie voor een netwerkinterface met statische (plaats dynamische) toewijzingsmethode Hallo steeds toe te wijzen. Met behulp van de statische methode Hallo Hallo-adres toewijst, zorgt u ervoor Hallo-adres verandert niet in Azure. Als u ooit toochange Hallo-adres toegewezen tooan IP-configuratie nodig, het is raadzaam dat u:

1. tooensure hello virtuele machine een adres ontvangt van hello Azure DHCP-servers, Hallo toewijzing van Hallo IP-adres back tooDHCP binnen het Hallo-besturingssysteem en opnieuw opstarten Hallo virtuele machine wijzigen.
2. Gestopt (toewijzing ongedaan maken) Hallo virtuele machine.
3. Wijzig Hallo IP-adres voor Hallo IP-configuratie in Azure.
4. Hallo virtuele machine te starten.
5. [Configureer handmatig](virtual-network-multiple-ip-addresses-portal.md#os-config) Hallo secundaire IP-adressen binnen het Hallo-besturingssysteem (en ook primaire IP-adres binnen Windows hello) toomatch u instellen in Azure.
 
Door de vorige stappen hello te volgen, persoonlijke IP-adres toegewezen toohello netwerkinterface in Azure en binnen een virtuele machine besturingssysteem hello, blijft dezelfde Hallo. tookeep bijhouden welke virtuele machines binnen uw abonnement die u handmatig IP-adressen binnen een besturingssysteem, hebt ingesteld overweegt u het toevoegen van een Azure [tag](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags) toohello virtuele machines. U kunt gebruiken ' IP-adrestoewijzing: statische ', bijvoorbeeld. Op deze manier kunt u gemakkelijk vinden Hallo virtuele machines binnen uw abonnement die u handmatig Hallo IP-adres voor binnen Hallo-besturingssysteem hebt ingesteld.

Bovendien kan tooenabling de toocommunicate van een virtuele machine met andere resources binnen Hallo dezelfde of verbonden virtuele netwerken, een privé-IP-adres ook een virtuele machine toocommunicate uitgaande toohello Internet. Uitgaande verbindingen zijn Bronnetwerk adres vertaald door Azure tooan onvoorspelbare openbaar IP-adres. meer informatie over Azure uitgaande internetverbinding, Hallo lezen toolearn [Azure uitgaande internetverbinding](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel. U kunt privé IP-adres van Hallo Internet inkomende tooa virtuele machine kan niet communiceren.

### <a name="public"></a>Openbaar

Openbare IP-adressen inschakelen voor binnenkomende verbindingen tooa virtuele machine van Hallo Internet. Uitgaande verbindingen toohello Internet gebruiken een voorspelbare IP-adres. Zie [inzicht in uitgaande verbindingen in Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) voor meer informatie. U een openbaar IP-adres tooan IP-configuratie kunt toewijzen, maar zijn niet vereist voor. Als u een openbaar IP-adres tooa virtuele machine niet toewijst, kan nog steeds uitgaande toohello Internet met behulp van de privé IP-adres communiceren. meer informatie over openbare IP-adressen, Hallo lezen toolearn [openbaar IP-adres](virtual-network-public-ip-address.md) artikel.

Er zijn limieten toohello aantal persoonlijke en openbare IP-adressen die u aan tooa toewijzen kunt netwerkinterface. Voor meer informatie lezen Hallo [Azure beperkt](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artikel.

> [!NOTE]
> Azure zet een virtuele machine privé IP-adres tooa openbare IP-adres. Als gevolg hiervan Hallo-besturingssysteem is niet op de hoogte van alle openbare IP-adressen toegewezen tooit, zodat er geen noodzaak tooever handmatig toewijzen een openbaar IP-adres binnen het Hallo-besturingssysteem.

## <a name="assignment-methods"></a>Van toewijzingsmethoden

Openbare en particuliere IP-adressen worden toegewezen met behulp van de volgende toewijzingsmethoden Hallo:

### <a name="dynamic"></a>Dynamisch

Dynamische particuliere IPv4 en IPv6 (optioneel) adressen worden standaard toegewezen. Dynamische adressen kunnen wijzigen als Hallo virtuele machine wordt geplaatst in Hallo gestopt (toewijzing ongedaan gemaakt) staat en vervolgens gestart. Als u geen IPv4-adressen toochange voor Hallo levensduur van Hallo virtuele machine wilt, Hallo adressen toewijzen via Hallo statische methode. U kunt alleen een particulier IPv6-adres met behulp van de dynamische toewijzingsmethode Hallo toewijzen. U kunt een openbare IPv6-adres tooan IP-configuratie met behulp van beide methoden niet toewijzen.

### <a name="static"></a>Statisch

Adressen die zijn toegewezen met behulp van de statische methode Hallo wijzigen niet totdat er een virtuele machine is verwijderd. U toewijzen handmatig een statisch particulier IPv4-tooan IP-adresconfiguratie in de adresruimte Hallo van Hallo subnet Hallo-netwerkinterface van is. U kunt een openbare of particuliere statische IPv4-adres tooan IP-configuratie (optioneel) toewijzen. U kunt een statische openbare of particuliere IPv6-tooan IP-adresconfiguratie niet toewijzen. toolearn meer informatie over hoe Azure statische openbare IPv4-adressen toegewezen Zie Hallo [openbaar IP-adres](virtual-network-public-ip-address.md) artikel.

## <a name="ip-address-versions"></a>IP-adres versies

Hallo versies te volgen bij het toewijzen van adressen, kunt u opgeven:

### <a name="ipv4"></a>IPv4

Elke netwerkinterface moet een hebben [primaire](#primary) IP-configuratie met een toegewezen [persoonlijke](#private) [IPv4](#ipv4) adres. U kunt een of meer toevoegen [secundaire](#secondary) IP-configuraties die elk een particulier IPv4- en (optioneel) een IPv4-hebben [openbare](#public) IP-adres.

### <a name="ipv6"></a>IPv6

U kunt nul of één persoonlijke toewijzen [IPv6](#ipv6) tooone secundaire IP-adresconfiguratie van een netwerkinterface. Hallo-netwerkinterface kan niet alle bestaande secundaire IP-configuraties hebben. U kunt een IP-configuratie niet toevoegen met een IPv6-adres met behulp van Hallo-portal. Gebruik PowerShell of CLI tooadd een IP-configuratie met een persoonlijke IPv6-adres tooan bestaande netwerkinterface Hallo. Hallo-netwerkinterface niet gekoppelde tooan bestaande virtuele machine.

> [!NOTE]
> Hoewel u een netwerkinterface met een IPv6-adres met behulp van de portal hello maken kunt, toevoegen u niet een bestaande netwerk interface tooa nieuwe of bestaande virtuele machine, met behulp van Hallo-portal. Gebruik PowerShell of hello Azure CLI 2.0 toocreate een netwerkinterface met een particulier IPv6-adres en Hallo netwerkinterface koppelen bij het maken van een virtuele machine. U kunt een netwerkinterface niet koppelen met een particulier IPv6-adres toegewezen tooit tooan bestaande virtuele machine. U kunt een persoonlijke IPv6-adres tooan IP-configuratie voor een netwerk interface aangesloten tooa virtuele machine met behulp van hulpprogramma's (portal, CLI of PowerShell) niet toevoegen.

U kunt een openbare IPv6-adres tooa primaire of secundaire IP-configuratie niet toewijzen.

## <a name="next-steps"></a>Volgende stappen
toocreate een virtuele machine met verschillende IP-configuraties, lezen Hallo artikelen te volgen:

|Taak|Hulpprogramma|
|---|---|
|Een virtuele machine met meerdere NIC's maken|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Één NIC VM maken met meerdere IPv4-adressen|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Maak een enkel NIC-VM met een particulier IPv6-adres (achter een Load Balancer van Azure)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Azure Resource Manager-sjabloon](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
