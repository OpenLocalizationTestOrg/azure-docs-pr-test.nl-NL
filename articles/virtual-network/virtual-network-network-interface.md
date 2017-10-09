---
title: aaaCreate, wijzigen of verwijderen van een Azure-netwerk-interface | Microsoft Docs
description: Informatie over wat de netwerkinterface wordt en hoe de toocreate, instellingen voor wijzigen en verwijderen.
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
ms.openlocfilehash: dcb6cdbd73bc0d0ca4efb9d972d370cf2d54abb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-network-interface"></a>Maken, wijzigen of verwijderen van een netwerkinterface

Ontdek hoe toocreate, instellingen voor wijzigen en verwijderen van een netwerkinterface. Een netwerkinterface kan een virtuele Machine van Azure toocommunicate met Internet, Azure en lokale bronnen. Bij het maken van een virtuele machine met hello Azure-portal maakt Hallo portal één netwerkinterface met de standaardinstellingen voor u. U kunt in plaats daarvan kiezen toocreate netwerkinterfaces met aangepaste instellingen en een of meer network interfaces tooa virtuele machine toevoegen wanneer u deze maakt. U kunt ook toochange standaard netwerkinterface-instellingen voor een bestaande netwerkinterface. Dit artikel wordt uitgelegd hoe toocreate een netwerkinterface met aangepaste instellingen bestaande instellingen, zoals de toewijzing van netwerken filter (netwerkbeveiligingsgroep), subnettoewijzing, DNS-serverinstellingen en doorsturen via IP, wijzigen en verwijderen van een netwerkinterface.

Als u tooadd moet, wijzigen of verwijderen van IP-adressen voor een netwerkinterface lezen Hallo [beheren IP-adressen](virtual-network-network-interface-addresses.md) artikel. Als u tooadd netwerkinterfaces moet of netwerkinterfaces van virtuele machines verwijdert, leest u Hallo [toevoegen of verwijderen van netwerkinterfaces](virtual-network-network-interface-vm.md) artikel.


## <a name="before-you-begin"></a>Voordat u begint

Volledige Hallo taken voordat u een volgende stappen in elke sectie van dit artikel:

- Bekijk Hallo [Azure beperkt](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artikel over de limieten voor netwerkinterfaces.
- Meld u bij Azure toohello [portal](https://portal.azure.com), Azure-opdrachtregelinterface (CLI) of Azure PowerShell gebruiken met een Azure-account. Als u nog een Azure-account hebt, zich aanmelden voor een [gratis proefaccount](https://azure.microsoft.com/free).
- Als u met behulp van PowerShell-opdrachten toocomplete taken in dit artikel [Azure PowerShell installeren en configureren](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure PowerShell commandlets geïnstalleerd. tooget help voor PowerShell-opdrachten, met voorbeelden, typ `get-help <command> -full`.
- Als u met behulp van Azure-opdrachtregelinterface (CLI) taken in dit artikel toocomplete opdrachten [installeren en configureren van Azure CLI Hallo](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure CLI is geïnstalleerd. tooget help voor CLI-opdrachten, typ `az <command> --help`. In plaats van installatie Hallo CLI en de vereisten, kunt u hello Azure Cloud-Shell. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft. toouse hello Cloud-Shell, klikt u op Hallo Cloud Shell **> _** knop bovenaan Hallo Hallo [portal](https://portal.azure.com).

## <a name="create-a-network-interface"></a>Een netwerkinterface maken

Bij het maken van een virtuele machine met hello Azure-portal maakt Hallo portal een netwerkinterface met de standaardinstellingen voor u. Als u liever uw instellingen voor de interface netwerk instelt, kunt u een netwerkinterface met aangepaste instellingen maken en Hallo network interface tooa virtuele machine koppelen bij het maken van Hallo virtuele machine (met PowerShell of hello Azure CLI). U kunt ook een netwerkinterface maken en toe te voegen tooan bestaande virtuele machine (met PowerShell of hello Azure CLI). hoe toocreate een virtuele machine met een bestaande-interface of tooadd op het netwerk of verwijderen van netwerkinterfaces van bestaande virtuele machines gelezen Hallo toolearn [toevoegen of verwijderen van netwerkinterfaces](virtual-network-network-interface-vm.md) artikel. Voordat u een netwerkinterface maakt, hebt u een bestaande [virtueel netwerk](virtual-networks-create-vnet-arm-pportal.md) in dezelfde locatie en abonnement maken van een netwerkinterface in Hallo.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *netwerkinterfaces*. Wanneer **netwerkinterfaces** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **netwerkinterfaces** blade die wordt weergegeven, klikt u op **+ toevoegen**.
4. In Hallo **netwerkinterface maken** blade die wordt weergegeven, invoeren, of Selecteer waarden voor Hallo na instellingen en klik vervolgens op **maken**:

    |Instelling|Vereist?|Details|
    |---|---|---|
    |Naam|Ja|Hallo-naam moet uniek zijn binnen het Hallo-resourcegroep die u selecteert. Na verloop van tijd waarschijnlijk hebt u verschillende netwerkinterfaces in uw Azure-abonnement. Lees Hallo [naamconventies](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) artikel voor suggesties voor het maken van een naming convention toomake het beheer van meerdere netwerkinterfaces eenvoudiger. Hallo-naam kan niet worden gewijzigd nadat Hallo-netwerkinterface is gemaakt.|
    |Virtueel netwerk|Ja|Hallo virtueel netwerk voor de netwerkinterface Hallo selecteert. U kunt alleen een network interface tooa virtueel netwerk dat in Hallo dezelfde bestaat toewijzen abonnement en de locatie als Hallo-netwerkinterface. Zodra een netwerkinterface is gemaakt, kunt u Hallo virtueel netwerk die wordt toegewezen aan niet wijzigen. Hallo virtuele machine die u toevoegt Hallo network interface toomust tevens aanwezig zijn in Hallo dezelfde locatie en abonnement als Hallo-netwerkinterface.|
    |Subnet|Ja|Selecteer een subnet binnen Hallo virtueel netwerk die u hebt geselecteerd. U kunt wijzigen Hallo subnet Hallo-netwerkinterface is toegewezen tooafter deze gemaakt.|
    |Privé IP-adrestoewijzing|Ja| Deze instelling kiezen Hallo toewijzingsmethode voor Hallo IPv4-adres. Kies in de volgende toewijzingsmethoden Hallo: **dynamische:** wanneer u deze optie selecteert, Azure wijst automatisch een beschikbaar adres van de adresruimte Hallo van Hallo subnet dat u hebt geselecteerd. Azure kan de netwerkinterface van een ander adres tooa toewijzen wanneer Hallo virtuele machine zich in wordt gestart nadat in het Hallo (toewijzing ongedaan gemaakt) staat gestopt. Hallo adres blijft Hallo dezelfde als Hallo virtuele machine opnieuw wordt opgestart zonder dat in Hallo (toewijzing ongedaan gemaakt) staat gestopt. **Statische:** wanneer u deze optie selecteert, moet u handmatig een beschikbaar IP-adres uit in de adresruimte Hallo van Hallo subnet geselecteerde toewijzen. Statische adressen wijzigen niet totdat u ze wijzigen of Hallo netwerkinterface wordt verwijderd. U kunt methode voor het toewijzen van Hallo wijzigen nadat Hallo-netwerkinterface is gemaakt. Hello Azure DHCP-server, wijst dit adres toohello netwerkinterface in besturingssysteem Hallo van Hallo virtuele machine.|
    |Netwerkbeveiligingsgroep|Nee| Laat ingesteld te**geen**, selecteer een bestaande [netwerkbeveiligingsgroep](virtual-networks-nsg.md), of [maken van een netwerkbeveiligingsgroep](virtual-networks-create-nsg-arm-pportal.md). Netwerkbeveiligingsgroepen inschakelen toofilter netwerkverkeer naar en vanuit een netwerkinterface. U kunt nul of één netwerk beveiliging groep tooa netwerkinterface toepassen. Nul of één netwerkbeveiligingsgroep kan ook worden toegepast toohello subnet Hallo-netwerkinterface is toegewezen aan. Wanneer een netwerkbeveiligingsgroep is toegepaste tooa netwerkinterface en Hallo subnet Hallo-netwerkinterface is toegewezen, soms onverwachte resultaten optreden. Hallo tootroubleshoot netwerk beveiligingsgroepen toegepaste toonetwork interfaces en subnetten, lezen [netwerkbeveiligingsgroepen oplossen](virtual-network-nsg-troubleshoot-portal.md#nsg) artikel.|
    |Abonnement|Ja|Selecteer een van uw Azure [abonnementen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). Hallo virtuele machine koppelen van een network interface tooand Hallo virtueel netwerk u verbinding maken met toomust aanwezig zijn in Hallo hetzelfde abonnement.|
    |Privé IP-adres (IPv6)|Nee| Als u dit selectievakje inschakelt, een IPv6-adres is toegewezen toohello netwerkinterface, Daarnaast toohello IPv4-adres toegewezen toohello netwerkinterface. Zie Hallo [IPv6](#IPv6) sectie van dit artikel voor belangrijke informatie over het gebruik van IPv6 met netwerkinterfaces. U kunt een methode voor het toewijzen voor Hallo IPv6-adres niet selecteren. Als u op een IPv6-adres tooassign kiest, wordt het toegewezen met Hallo dynamische methode.
    |IPv6-naam (wordt alleen weergegeven als hello **particuliere IP-adres (IPv6)** selectievakje is ingeschakeld) |Ja, als hello **particuliere IP-adres (IPv6)** selectievakje is ingeschakeld.| Deze naam wordt tooa secundaire IP-configuratie voor netwerkinterface Hallo toegewezen. Meer informatie over IP-configuraties in Hallo [netwerkinterface-instellingen bekijken](#view-network-interface-settings) sectie van dit artikel.|
    |Resourcegroep|Ja|Selecteer een bestaande [resourcegroep](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) of maak een. Een netwerkinterface kan bestaan in Hallo dezelfde of een andere resourcegroep, dan Hallo virtuele machine koppelt, of Hallo virtuele netwerk u verbinding te maken.|
    |Locatie|Ja|Hallo virtuele machine koppelen van een network interface tooand Hallo virtueel netwerk u verbinding maken met toomust aanwezig zijn in Hallo dezelfde [locatie](https://azure.microsoft.com/regions), ook wel aangeduid tooas een regio.|

Hallo-portal biedt niet Hallo optie tooassign openbare IP-adres, toohello netwerkinterface bij het maken, hoewel Hallo portal een openbaar IP-adres maken en deze netwerkinterface tooa toewijzen bij het maken van een virtuele machine met behulp van Hallo-portal. hoe tooadd een openbaar IP-adres toohello netwerk hebt gemaakt en interface lezen Hallo toolearn [beheren IP-adressen](virtual-network-network-interface-addresses.md) artikel. Als u toocreate een netwerkinterface met een openbaar IP-adres wilt, moet u Hallo CLI of PowerShell toocreate Hallo netwerkinterface.

>[!Note]
> Azure wordt toegewezen die de MAC-adres toohello netwerkinterface pas nadat het Hallo-netwerkinterface is aangesloten tooa virtuele machine en Hallo virtuele machine wordt gestart Hallo eerst. U kunt Hallo MAC-adres dat Azure toohello netwerkinterface wijst niet opgeven. Hallo toohello netwerkinterface voor MAC-adres toegewezen blijven totdat Hallo-netwerkinterface is verwijderd of Hallo privé IP-adres toegewezen toohello primaire IP-configuratie van de primaire netwerkinterface hello wordt gewijzigd. meer informatie over IP-adressen en IP-configuraties, Hallo lezen toolearn [beheren IP-adressen](virtual-network-network-interface-addresses.md) artikel.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ netwerk nic maken](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Nieuwe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>Netwerkinterface-instellingen weergeven

U kunt weergeven en wijzigen van de meeste instellingen voor een netwerkinterface nadat deze gemaakt.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *netwerkinterfaces*. Wanneer **netwerkinterfaces** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **netwerkinterfaces** blade die wordt weergegeven, klikt u op Hallo netwerkinterface u tooview of wijzig de instellingen voor.
4. Hallo worden volgende instellingen vermeld in het Hallo-blade die wordt weergegeven voor de netwerkinterface Hallo die u hebt geselecteerd:
    - **Overzicht:** bevat informatie over de netwerkinterface hello, zoals Hallo IP-adressen tooit toegewezen en Hallo virtuele machine Hallo-netwerkinterface is gekoppeld, te Hallo virtueel netwerksubnet Hallo-netwerkinterface is toegewezen aan (if het gekoppeld tooone). Hallo volgende afbeelding ziet u Hallo overzicht de instellingen voor een netwerkinterface met de naam **mywebserver256**: ![Network interface-overzicht](./media/virtual-network-network-interface/nic-overview.png) kunt u een network interface tooa andere resourcegroep verplaatsen of abonnement door te klikken (**wijzigen**) volgende toohello **resourcegroep** of **naam abonnement**. Als u de netwerkinterface Hallo verplaatst, moet u alle resources gerelateerde toohello netwerkinterface met het verplaatsen. Als Hallo netwerkinterface gekoppelde tooa virtuele machine is, bijvoorbeeld, moet u ook verplaatsen Hallo virtuele machine en andere bronnen betrekking hebben op virtuele machine. toomove een netwerkinterface lezen Hallo [resource tooa nieuwe resourcegroep of abonnement verplaatsen](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal) artikel. Hallo artikel bevat een overzicht van vereisten, en hoe toomove resources met behulp van hello Azure-portal, PowerShell en Azure CLI Hallo.
    - **IP-configuraties:** openbare en persoonlijke IPv4 en IPv6-adressen toegewezen tooIP configuraties worden hier vermeld. Als een IPv6-adres is toegewezen tooan IP-configuratie, de Hallo-adres niet wordt weergegeven. Meer informatie over IP-configuraties en hoe tooadd en wordt verwijderd, IP-adressen in Hallo [configureren IP-adressen voor een Azure-netwerk-interface](virtual-network-network-interface-addresses.md) artikel. Doorsturen via IP en subnettoewijzing zijn ook in deze sectie geconfigureerd. meer informatie over deze instellingen worden gelezen Hallo toolearn [in- of uitschakelen van doorsturen via IP](#enable-or-disable-ip-forwarding) en [subnettoewijzing wijzigen](#change-subnet-assignment) secties van dit artikel.
    - **DNS-servers:** kunt u opgeven welke DNS-server een netwerkinterface wordt toegewezen door hello Azure DHCP-servers. Hallo netwerkinterface kunt Hallo-instelling overnemen van Hallo virtueel netwerk Hallo-netwerkinterface is toegewezen aan of hebt u een aangepaste instelling die Hallo-instelling voor Hallo virtueel netwerk wordt aan toegewezen. toomodify wat wordt weergegeven, stappen voor voltooid Hallo Hallo [wijziging DNS-servers](#change-dns-servers) sectie van dit artikel.
    - **Netwerkbeveiligingsgroep (NSG):** geeft dit NSG is gekoppeld toohello netwerkinterface (indien aanwezig). Een NSG bevat regels voor binnenkomende en uitgaande toofilter netwerkverkeer voor de netwerkinterface Hallo. Als een NSG gekoppeld toohello netwerkinterface, de naam van de Hallo Hallo die gekoppelde NSG wordt weergegeven is. toomodify wat wordt weergegeven, stappen voor voltooid Hallo Hallo [beheren netwerk groep beveiligingskoppelingen](virtual-network-manage-nsg-arm-portal.md#manage-associations) artikel.
    - **Eigenschappen:** geeft belangrijke instellingen over van de netwerkinterface hello, met inbegrip van het MAC-adres (leeg als Hallo-netwerkinterface niet gekoppelde tooa virtuele machine) en Hallo abonnement deze voorkomt in.
    - **Effectieve beveiligingsregels:** beveiligingsregels worden vermeld als Hallo netwerkinterface gekoppelde tooa virtuele machine actief is en een NSG is gekoppeld toohello netwerkinterface of Hallo-subnet aan toegewezen. toolearn meer informatie over wat wordt weergegeven, lezen Hallo [netwerkbeveiligingsgroepen oplossen](virtual-network-nsg-troubleshoot-portal.md#nsg) artikel. meer informatie over nsg's, Hallo lezen toolearn [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md) artikel.
    - **Effectieve routes:** Routes worden vermeld als Hallo netwerkinterface gekoppelde tooa virtuele machine wordt uitgevoerd. Hallo routes zijn een combinatie van hello Azure standaardroutes, eventuele door de gebruiker gedefinieerde routes (UDR) en een BGP-routes die zich voordoen kunnen voor Hallo subnet Hallo-netwerkinterface is toegewezen aan. toolearn meer informatie over wat wordt weergegeven, lezen Hallo [routes oplossen](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface) artikel. meer informatie over Azure standaard en udr's, Hallo lezen toolearn [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md) artikel.
    - **Algemene instellingen van Azure Resource Manager:** toolearn meer informatie over algemene instellingen van Azure Resource Manager, Hallo lezen [activiteitenlogboek](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs), [toegangsbeheer (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control), [labels ](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags), [Vergrendelt](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json), en [automatiseringsscript](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group) artikelen.

**Opdrachten**

Als een IPv6-adres is toegewezen tooa netwerkinterface, retourneert Hallo uitvoer van PowerShell Hallo fact dat Hallo adres wordt toegewezen, maar deze retourneert Hallo toegewezen adres niet. Op deze manier Hallo CLI retourneert Hallo feit dat Hallo adres is toegewezen, maar retourneert *null* in de uitvoer voor Hallo-adres.

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[lijst met AZ netwerken nic](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list) tooview netwerkinterfaces in Hallo-abonnement. [az netwerk nic weergeven](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooview-instellingen voor een netwerkinterface|
|PowerShell|[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) tooview netwerkinterfaces in Hallo abonnement of de weergave-instellingen voor een netwerkinterface|

## <a name="change-dns-servers"></a>DNS-servers wijzigen

Hallo DNS-server is door hello Azure DHCP-server toohello netwerkinterface in besturingssysteem Hallo-virtuele machine toegewezen. Hallo DNS-server toegewezen is ongeacht Hallo DNS-serverinstellingen voor een netwerkinterface. Zie toolearn meer informatie over instellingen voor het omzetten van de naam voor een netwerkinterface [naamomzetting voor virtuele machines](virtual-networks-name-resolution-for-vms-and-role-instances.md). Hallo-netwerkinterface kunt Hallo-instellingen overnemen van het virtuele netwerk hello of een eigen unieke instellingen gebruiken die Hallo-instelling voor het virtuele netwerk Hallo onderdrukken.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *netwerkinterfaces*. Wanneer **netwerkinterfaces** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **netwerkinterfaces** blade die wordt weergegeven, klikt u op Hallo netwerkinterface u tooview of wijzig de instellingen voor.
4. Hallo-blade voor Hallo-netwerkinterface die u hebt geselecteerd, klikt u op **DNS-servers** onder **instellingen**.
5. Klik op een:
    - **Overnemen van een virtueel netwerk (standaard)**: Kies deze optie tooinherit Hallo DNS-serverinstelling gedefinieerd voor Hallo virtueel netwerk Hallo-netwerkinterface is toegewezen aan. Niveau Hallo virtueel netwerk, is een aangepaste DNS-server of een hello Azure DNS-server gedefinieerd. Hello Azure DNS-server kan omzetten hostnamen voor resources die zijn toegewezen toohello hetzelfde virtuele netwerk. FQDN-naam moet de gebruikte tooresolve voor resources toodifferent virtuele netwerken die zijn toegewezen.
    - **Aangepaste**: U kunt uw eigen DNS-server tooresolve namen over meerdere virtuele netwerken configureren. Voer Hallo IP-adres van de server Hallo gewenste toouse als een DNS-server. Hallo DNS-serveradres die u opgeeft, wordt alleen toothis netwerkinterface en onderdrukkingen die alle DNS-instellingen voor de netwerkinterface van Hallo virtueel netwerk Hallo is toegewezen aan toegewezen.
6. Klik op **Opslaan**.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ netwerk nic-update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>In- of uitschakelen van doorsturen via IP

Doorsturen via IP kunt Hallo virtuele machine die een netwerkinterface is gekoppeld aan:
- Ontvangen netwerkverkeer niet bestemd is voor een Hallo IP-adressen toegewezen tooany van Hallo IP-configuraties toohello netwerkinterface toegewezen.
- Verzenden van netwerkverkeer met een ander IP-adres dan Hallo één toegewezen tooone van een netwerkinterface-IP-configuraties.

Hallo-instelling moet worden ingeschakeld voor elke netwerkinterface die is aangesloten toohello virtuele machine die verkeer dat de virtuele machine moet tooforward Hallo ontvangt. Een virtuele machine kan verkeer doorsturen of er meerdere netwerkinterfaces of een netwerk met één interface aangesloten tooit. Doorsturen via IP is een Azure-instelling, moet Hallo virtuele machine ook een toepassing kunnen tooforward Hallo-verkeer, zoals firewall, WAN-optimalisatie en taakverdeling van toepassingen uitgevoerd. Wanneer een virtuele machine wordt uitgevoerd netwerktoepassingen, is Hallo virtuele machine het vaak waarnaar wordt verwezen tooas een virtueel netwerkapparaat. U kunt een lijst met virtuele netwerkapparaten gereed toodeploy weergeven in Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). Doorsturen via IP wordt doorgaans gebruikt met de gebruiker gedefinieerde routes. meer informatie over de gebruiker gedefinieerde routes, Hallo lezen toolearn [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md) artikel.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *netwerkinterfaces*. Wanneer **netwerkinterfaces** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **netwerkinterfaces** blade die wordt weergegeven, klikt u op Hallo netwerkinterface of wilt u tooenable doorsturen via IP voor uitschakelen.
4. Hallo-blade voor Hallo-netwerkinterface die u hebt geselecteerd, klikt u op **IP-configuraties** in Hallo **instellingen** sectie.
5. Klik op **ingeschakeld** of **uitgeschakelde** (standaardinstelling) toochange Hallo-instelling.
6. Klik op **Opslaan**.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ netwerk nic-update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>Subnettoewijzing wijzigen

U kunt wijzigen Hallo subnet, maar niet Hallo virtueel netwerk, dat een netwerkinterface is toegewezen aan.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *netwerkinterfaces*. Wanneer **netwerkinterfaces** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **netwerkinterfaces** blade die wordt weergegeven, klikt u op Hallo netwerkinterface u tooview of wijzig de instellingen voor.
4. Klik op **IP-configuraties** onder **instellingen** Hallo blade voor Hallo-netwerkinterface die u hebt geselecteerd. Als een particuliere IP-adressen voor alle IP-configuraties vermeld **(statische)** volgende toothem, moet u Hallo IP-adres toewijzing methode toodynamic wijzigen via Hallo stappen volgen. Alle particuliere IP-adressen moeten worden toegewezen aan Hallo dynamische toewijzing methode toochange Hallo subnettoewijzing voor de netwerkinterface Hallo. Als het Hallo-adressen zijn toegewezen met dynamische methode hello, gaat u verder toostep vijf. Als een IPv4-adressen zijn toegewezen met de statische toewijzingsmethode hello, voert u Hallo stappen toochange Hallo toewijzing methode toodynamic te volgen:
    - Klik op de gewenste toochange Hallo IPv4-adres toewijzingsmethode voor uit Hallo lijst met IP-configuraties van Hallo IP-configuratie.
    - Hallo blade die wordt weergegeven voor Hallo IP-configuratie, klikt u op **dynamische** voor Hallo **toewijzing** methode. U kunt een IPv6-adres niet toewijzen met Hallo statische toewijzingsmethode.
    - Klik op **Opslaan**.
5. Selecteer Hallo subnet gewenste tooconnect Hallo network interface toofrom hello **Subnet** vervolgkeuzelijst.
6. Klik op **Opslaan**. Nieuwe dynamische adressen worden toegewezen uit Hallo subnet adresbereik voor Hallo nieuwe subnet. Na het toewijzen van Hallo interface tooa nieuwe netwerksubnet, kunt u een statisch IPv4-adres uit nieuwe subnet Hallo-adresbereik toewijzen als u ervoor kiest. meer informatie over het toevoegen, wijzigen en verwijderen van IP-adressen voor een netwerkinterface lezen Hallo toolearn [beheren IP-adressen](virtual-network-network-interface-addresses.md) artikel.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ netwerk nic IP-configuratie bijwerken](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>Verwijderen van een netwerkinterface

U kunt een netwerkinterface verwijderen zolang het is niet aangesloten tooa virtuele machine. Als het gekoppelde tooa virtuele machine, moet u de eerste plaats Hallo virtuele machine in Hallo gestopt (toewijzing opgeheven) staat, losmaken Hallo-netwerkinterface van Hallo virtuele machine, voordat u de netwerkinterface Hallo kunt verwijderen. toodetach een netwerkinterface van een virtuele machine, stappen voor voltooid Hallo Hallo [loskoppelen van een netwerkinterface van een virtuele machine](virtual-network-network-interface-vm.md#vm-remove-nic) sectie Hallo [toevoegen of verwijderen van netwerkinterfaces](virtual-network-network-interface-vm.md) artikel. Verwijderen van een virtuele machine wordt losgekoppeld van alle network interfaces gekoppelde tooit, maar niet Hallo netwerkinterfaces verwijdert.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *netwerkinterfaces*. Wanneer **netwerkinterfaces** wordt weergegeven in zoekresultaten hello, klik erop.
3. Klik met de rechtermuisknop Hallo netwerkinterface toodelete en klik op **verwijderen**.
4. Klik op **Ja** tooconfirm verwijdering van Hallo-netwerkinterface.

Wanneer u een netwerkinterface, eventuele MAC verwijderen of IP-adressen toegewezen tooit worden vrijgegeven.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[nic-AZ netwerk het verwijderen](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Verwijder AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Volgende stappen
toocreate een virtuele machine met meerdere netwerkinterfaces of het IP-adressen, lezen Hallo artikelen te volgen:

**Opdrachten**

|Taak|Hulpprogramma|
|---|---|
|Een virtuele machine met meerdere NIC's maken|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Één NIC VM maken met meerdere IPv4-adressen|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Maak een enkel NIC-VM met een particulier IPv6-adres (achter een Load Balancer van Azure)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Azure Resource Manager-sjabloon](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
