---
title: aaaAdd network interfaces tooor verwijderen uit de virtuele machines in Azure | Microsoft Docs
description: Meer informatie over hoe tooadd network interfaces tooor netwerkinterfaces van virtuele machines verwijderen.
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
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: eb564b94932b9242f29bc23234b08b0c76ac23a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-network-interfaces-tooor-remove-from-virtual-machines"></a>Netwerkinterfaces tooor verwijderen van virtuele machines toevoegen

Meer informatie over hoe tooadd een bestaand netwerk interface bij het maken van een virtuele machine of toevoegen of verwijderen van netwerkinterfaces van een bestaande virtuele machine in Hallo gestopt (toewijzing ongedaan gemaakt) staat. Een netwerkinterface kan een toocommunicate Azure virtuele Machine (VM) met Internet, Azure en lokale bronnen. Een virtuele machine kan een of meer netwerkinterfaces hebben. 

Als u tooadd moet, wijzigen of verwijderen van IP-adressen voor een netwerkinterface lezen Hallo [network interface-IP-adressen beheren](virtual-network-network-interface-addresses.md) artikel. Als u toocreate moet, wijzigen of verwijderen van netwerkinterfaces, lezen Hallo [beheren netwerkinterfaces](virtual-network-network-interface.md) artikel.

## <a name="before"></a>Voordat u begint

Volledige Hallo taken voordat u een volgende stappen in elke sectie van dit artikel:

- Meer informatie over hoeveel netwerkinterfaces elke Linux- en Windows-VM-grootte aan de hand van Hallo ondersteunt [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM-groottes artikelen.
- Meld u bij Azure toohello [portal](https://portal.azure.com), Azure-opdrachtregelinterface (CLI) of Azure PowerShell gebruiken met een Azure-account. Als u nog een Azure-account hebt, zich aanmelden voor een [gratis proefaccount](https://azure.microsoft.com/free).
- Als u met behulp van PowerShell-opdrachten toocomplete taken in dit artikel [Azure PowerShell installeren en configureren](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure PowerShell commandlets geïnstalleerd. tooget help voor PowerShell-opdrachten, met voorbeelden, typ `get-help <command> -full`.
- Als u met behulp van Azure-opdrachtregelinterface (CLI) taken in dit artikel toocomplete opdrachten [installeren en configureren van Azure CLI Hallo](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure CLI is geïnstalleerd. tooget help voor CLI-opdrachten, typ `az <command> --help`. In plaats van installatie Hallo CLI en de vereisten, kunt u hello Azure Cloud-Shell. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft. toouse hello Cloud-Shell, klikt u op Hallo Cloud Shell **> _** knop bovenaan Hallo Hallo [portal](https://portal.azure.com).

## <a name="about"></a>Over netwerkinterfaces en virtuele machines

U kunt toevoegen (koppeling) een bestaande netwerk interface tooa VM bij het maken van Hallo VM, mits het Hallo-netwerkinterface is momenteel niet gekoppeld tooanother VM. U kunt een netwerkinterface om te toevoegen of verwijderen (loskoppelen) een netwerk interface toofrom een bestaande VM opgegeven Hallo VM is in Hallo gestopt (toewijzing ongedaan gemaakt) staat. Als u een virtuele machine met hello Azure-portal maken, Hallo portal een netwerkinterface met de standaardinstellingen voor u gemaakt. Hallo portal niet toe dat u naar:

- Een bestaande netwerk interface tooadd bij het maken van VM Hallo opgeven
- Een virtuele machine met meerdere netwerkinterfaces maken
- Geef een naam voor de netwerkinterface hello (Hallo portal maakt Hallo netwerkinterface met de naam van een standaard)

U kunt Azure PowerShell of Hallo CLI toocreate een netwerkinterface of virtuele machine gebruiken met alle Hallo vorige kenmerken die u Hallo-portal voor niet gebruiken. Houd rekening met Hallo volgende voordat u taken in de volgende secties Hallo hello, gedrag en beperkingen:

- Alle VM-groottes ondersteuning ten minste twee netwerkinterfaces, maar sommige VM-grootten ondersteuning van meer dan twee netwerkinterfaces. In Hallo voorbij enkele VM ondersteund grootten alleen voor een netwerkinterface. toolearn hoeveel netwerkinterfaces die ondersteuning biedt voor elke VM-grootte, lezen Hallo [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM-groottes artikelen. 
- Netwerkinterfaces kunnen Hallo is afgelopen, alleen toegevoegde tooVMs meerdere netwerkinterfaces worden ondersteund en zijn gemaakt met ten minste twee netwerkinterfaces worden. U kan een network interface tooa VM die is gemaakt met één netwerkinterface niet toevoegen, zelfs als er meerdere netwerkinterfaces Hallo VM-grootte wordt ondersteund. Als u daarentegen netwerkinterfaces kan alleen worden verwijderd van een virtuele machine met ten minste drie netwerkinterfaces, omdat virtuele machines die zijn gemaakt met ten minste twee netwerkinterfaces altijd toohave heeft ten minste twee netwerkinterfaces. Geen van deze beperkingen meer van toepassing. U kunt nu een virtuele machine maken met een willekeurig aantal netwerkinterfaces (omhoog toohello dat wordt ondersteund door Hallo VM-grootte) en toevoegen of verwijderen van een willekeurig aantal netwerkinterfaces (van virtuele machines in Hallo gestopt (toewijzing opgeheven)-status), zolang Hallo VM altijd ten minste één netwerkinterface heeft.
- Standaard Hallo eerste netwerkinterface in een virtuele machine is gedefinieerd als Hallo *primaire* netwerkinterface. Alle andere netwerkinterfaces in Hallo VM zijn *secundaire* netwerkinterfaces.
- Primaire netwerkinterfaces standaardgateway door hello Azure DHCP-servers zijn toegewezen, maar secundaire netwerkinterfaces zijn niet. Omdat secundaire netwerkinterfaces zijn niet standaardgateway toegewezen, niet kunnen ze communiceren met bronnen buiten hun subnet standaard. tooenable secundaire netwerkinterfaces in een virtuele machine van Windows-toocommunicate met bronnen buiten hun subnet toohello-besturingssysteem voor de routes met behulp van Hallo toevoegen `route add` opdracht vanaf een Windows-opdrachtregel. Voor virtuele Linux-machines, omdat Hallo standaardgedrag maakt gebruik van zwakke host routering, wordt geadviseerd om verkeer voor secundaire interfaces tooa één netwerksubnet beperkt. Als u connectiviteit buiten Hallo subnet vereist voor de secundaire netwerkinterfaces, inschakelen op beleid gebaseerde routering tooensure dat inkomende en uitgaande verkeer Hallo gebruikt netwerkinterface dezelfde.
- Standaard wordt al het uitgaande verkeer van Hallo die VM Hallo IP-adres wordt verzonden toohello primaire IP-configuratie van de primaire netwerkinterface Hallo toegewezen. U bepalen welk IP-adres wordt gebruikt voor uitgaand verkeer in het besturingssysteem Hallo van de virtuele machine, maar deze is standaard via de primaire netwerkinterface Hallo.
- In Hallo voorbij alle virtuele machines binnen Hallo waren dezelfde beschikbaarheidsset vereist toohave een enkele of meerdere netwerkinterfaces. Virtuele machines met een willekeurig aantal network interfaces kunnen nu bestaan in dezelfde beschikbaarheidsset up toohello dat wordt ondersteund door VM-grootte Hallo Hallo. U kunt alleen een VM tooan beschikbaarheidsset als deze al gemaakt toevoegen. meer informatie over beschikbaarheidssets lezen Hallo toolearn [Hallo beschikbaarheid van virtuele machines in Azure beheren](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) artikel.
- Hoewel netwerkinterfaces hello dezelfde virtuele machine kan worden verbonden toodifferent subnetten binnen een VNet, Hallo netwerkinterfaces moeten verbonden toohello hetzelfde VNet.
- U kunt elk IP-adres voor alle IP-configuratie van een primaire of secundaire netwerk interface tooan Azure Load Balancer back-end-adresgroep toevoegen. In de afgelopen hello, kan alleen Hallo primaire IP-adres voor de primaire netwerkinterface Hallo tooa back-end-pool worden toegevoegd. meer informatie over IP-adressen en configuraties, Hallo lezen toolearn [toevoegen, wijzigen of verwijderen IP-adressen](virtual-network-network-interface-addresses.md) artikel.
- Als een virtuele machine, verwijdert Hallo netwerkinterfaces die aangesloten tooit zijn niet verwijderd. Wanneer een virtuele machine wordt verwijderd, worden de netwerkinterfaces Hallo losgekoppeld van Hallo VM. U kunt Hallo network interfaces toodifferent VM's toevoegen of verwijderen.
- Als een netwerkinterface een persoonlijke tooit van IPv6-adres is toegewezen heeft, kunt u deze koppelen als tooa VM bij het maken van Hallo VM. U kunt een netwerkinterface met een toegewezen IPv6-adres tooa VM niet koppelen nadat Hallo VM is gemaakt. Als u een netwerkinterface met een toegewezen persoonlijke IPv6-adres koppelt bij het maken van een virtuele machine, kunt u alleen die network interface toohello virtuele machine, ongeacht hoeveel netwerkinterfaces die ondersteuning biedt voor VM-grootte Hallo koppelen. Zie [Network interface-IP-adressen](virtual-network-network-interface-addresses.md) toolearn meer informatie over het toewijzen van IP-adressen toonetwork interfaces.

## <a name="vm-create"></a>Toevoegen van de bestaande netwerkinterfaces tooa nieuwe virtuele machine

Wanneer u een virtuele machine via Hallo portal maakt, wordt Hallo portal een netwerkinterface maken met de standaardinstellingen en wordt toohello VM voor u gekoppeld. U kunt geen bestaande netwerkinterfaces tooa toevoegen nieuwe virtuele machine, of een virtuele machine maken met meerdere netwerkinterfaces met hello Azure-portal. U kunt beide doen met behulp van Hallo CLI of PowerShell. U kunt toevoegen als veel interfaces tooa VM-netwerk als Hallo VM-grootte die u ondersteunt. toolearn meer informatie over hoeveel network interfaces elke VM grootte ondersteunt, Hallo lezen [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM-groottes artikelen. Hallo-netwerkinterfaces toevoegen van tooa VM kunnen momenteel niet gekoppelde tooanother VM. meer over het maken van de netwerkinterfaces, Hallo lezen toolearn [beheren netwerkinterfaces](virtual-network-network-interface.md#create-a-network-interface) artikel.

> [!WARNING]
> Als een netwerkinterface een persoonlijke IPv6-adres toegewezen tooit heeft, kunt u alleen Hallo network interface toohello virtuele machine toevoegen bij het maken van Hallo virtuele machine. U kunt meer dan één virtuele machine van de netwerk-interface toohello niet koppelen wanneer u Hallo virtuele machine maakt, of na Hallo virtuele machine wordt gemaakt, als een IPv6-adres tooa network interface aangesloten tooa virtuele machine is toegewezen. Zie [Network interface-IP-adressen](virtual-network-network-interface-addresses.md) toolearn meer informatie over het toewijzen van IP-adressen toonetwork interfaces.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ vm maken](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Nieuwe-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>Een bestaande netwerk interface tooan bestaande virtuele machine toevoegen

U kunt als veel interfaces tooa VM-netwerk als Hallo VM-grootte die u toevoegt network interfaces toosupports toevoegen. toolearn hoeveel netwerkinterfaces die ondersteuning biedt voor elke VM-grootte, lezen Hallo [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM-groottes artikelen. Hallo VM die u wilt dat tooadd een network interface-toomust ondersteunen Hallo aantal netwerkinterfaces die u wilt tooadd en moet in Hallo gestopt (toewijzing opgeheven) staat. Hallo-netwerkinterfaces die u wilt dat tooadd kunnen momenteel niet gekoppelde tooanother VM. U kunt geen network interfaces tooan VM hello Azure-portal met bestaande toevoegen. tooadd netwerkinterfaces tooan bestaande virtuele machine, moet u Hallo CLI of PowerShell gebruiken. 

> [!WARNING]
> Als een netwerkinterface een persoonlijke IPv6-adres toegewezen tooit heeft, niet kan worden deze tooan bestaande virtuele machine toegevoegd. Wanneer u een virtuele machine maakt, kunt u alleen een netwerkinterface met een toegewezen persoonlijke IPv6-adres tooa virtuele machine toevoegen. Zie [Network interface-IP-adressen](virtual-network-network-interface-addresses.md) toolearn meer informatie over het toewijzen van IP-adressen toonetwork interfaces.

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ vm nic toevoegen](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add) (verwijzing) of [gedetailleerde stappen](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Voeg AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (verwijzing) of [gedetailleerde stappen](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a>Netwerkinterfaces van de weergave voor een virtuele machine

U kunt Hallo network interfaces op dat moment gekoppelde tooa VM toolearn over de configuratie van elke netwerkinterface bekijken en Hallo IP-adressen toegewezen tooeach netwerkinterface. 

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat de eigenaar, bijdrager of Network Contributor rol Hallo voor uw abonnement is toegewezen. toolearn meer informatie over het toewijzen van rollen tooaccounts, Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *virtuele machines*. Wanneer **virtuele machines** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **virtuele machines** blade die wordt weergegeven, klikt u op Hallo-naam van Hallo tooview netwerkinterfaces van gewenste VM.
4. In Hallo **instellingen** sectie van Hallo virtuele machineblade die wordt weergegeven voor Hallo VM die u hebt geselecteerd, klikt u op **netwerkinterfaces**. toolearn over netwerkinterface-instellingen en hoe toochange ze, leest hello [beheren netwerkinterfaces](virtual-network-network-interface.md) artikel. toolearn over het toevoegen, wijzigen of verwijderen van IP-adressen toegewezen tooa netwerkinterface, Zie [beheren IP-adressen](virtual-network-network-interface-addresses.md).

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ vm weergeven](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a>Een netwerkinterface van een virtuele machine verwijderen

Hallo moet VM die u wilt dat tooremove (of loskoppelen) een netwerkinterface van Hallo gestopt (toewijzing ongedaan gemaakt) en moeten momenteel hebben ten minste twee netwerkinterfaces gekoppeld tooit. U kunt een netwerkinterface verwijderen, maar Hallo VM moet altijd ten minste één netwerk interface aangesloten tooit hebben. Als u een primaire netwerkinterface verwijdert, wijst Azure Hallo primaire kenmerk toohello netwerkinterface die aangesloten toohello VM Hallo langste is. 

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat de eigenaar, bijdrager of Network Contributor rol Hallo voor uw abonnement is toegewezen. toolearn meer informatie over het toewijzen van rollen tooaccounts, Zie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *virtuele machines*. Wanneer **virtuele machines** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **virtuele machines** blade die wordt weergegeven, klikt u op naam Hallo Hallo VM die u wilt dat tooremove een netwerkinterface voor.
4. In Hallo **instellingen** sectie van Hallo virtuele machineblade die wordt weergegeven voor Hallo VM die u hebt geselecteerd, klikt u op **netwerkinterfaces**. toolearn over netwerkinterface-instellingen en hoe toochange ze, leest hello [beheren netwerkinterfaces](virtual-network-network-interface.md) artikel. toolearn over het toevoegen, wijzigen of verwijderen van IP-adressen toegewezen tooa netwerkinterface, Zie [beheren IP-adressen](virtual-network-network-interface-addresses.md).
5. Hallo network interfaces blade die wordt weergegeven, klikt u op Hallo **...**  toohello rechts van de netwerkinterface Hallo dat u wilt dat toodetach.
6. Klik op **loskoppelen**. Als er slechts één netwerk interface aangesloten toohello virtuele machine, Hallo **Detach** optie niet beschikbaar. Klik op **Ja** in Hallo bevestigen dat wordt weergegeven.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[verwijderen van AZ vm nic](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove) (verwijzing) of [gedetailleerde stappen](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Verwijder AzureRMVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (verwijzing) of [gedetailleerde stappen](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>Volgende stappen
toocreate een virtuele machine met meerdere netwerkinterfaces of IP-adressen, lezen Hallo artikelen te volgen:

**Opdrachten**

|Taak|Hulpprogramma|
|---|---|
|Een virtuele machine met meerdere NIC's maken|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Één NIC VM maken met meerdere IPv4-adressen|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Maak een enkel NIC-VM met een particulier IPv6-adres (achter een Load Balancer van Azure)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Azure Resource Manager-sjabloon](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
