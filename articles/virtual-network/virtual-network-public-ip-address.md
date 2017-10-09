---
title: aaaCreate, wijzigen of verwijderen van een Azure openbare IP-adres | Microsoft Docs
description: Meer informatie over hoe toocreate, wijzigen of verwijderen van een openbaar IP-adres.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>Maken, wijzigen of verwijderen van een openbaar IP-adres

Meer informatie over een openbare IP-adres en hoe toocreate, wijzigen en verwijderen van een. Een openbaar IP-adres is een resource met een eigen configureerbare instellingen. Toewijzen van een openbare IP-adres tooother Azure-resources kunt:
- Inkomende Internet connectiviteit tooresources zoals Azure virtuele Machines (VM), Azure virtuele Machine-Schaalsets, Azure VPN-Gateway, Toepassingsgateways en internetgerichte Azure Load Balancers. Azure-resources kunnen niet ontvangen van binnenkomende communicatie van Hallo Internet zonder een toegewezen openbare IP-adres. Hoewel sommige Azure-resources inherent toegankelijk zijn via openbare IP-adressen, moeten de andere bronnen openbare IP-adressen toegewezen toothem toobe toegankelijk is vanaf Internet Hallo hebben.
- Uitgaande verbinding toohello Internet met behulp van een voorspelbare IP-adres. Bijvoorbeeld: een virtuele machine uitgaande toohello Internet zonder een openbare IP-adres toegewezen tooit kan communiceren, maar het adres is netwerkadres vertaald door Azure tooan onvoorspelbare openbaar adres. Een openbaar IP-adres tooa resource toe te wijzen, kunt u tooknow welk IP-adres wordt gebruikt voor Hallo uitgaande verbinding. Hoewel voorspelbare, kunt Hallo adres wijzigen, afhankelijk van de gekozen methode Hallo toewijzing. Zie voor meer informatie [maken van een openbaar IP-adres](#create-a-public-ip-address). meer informatie over uitgaande verbindingen van Azure-resources, lees Hallo toolearn [begrijpen uitgaande verbindingen](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel.

## <a name="before-you-begin"></a>Voordat u begint

Volledige Hallo taken voordat u een volgende stappen in elke sectie van dit artikel:

- Bekijk Hallo [Azure beperkt](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artikel over de limieten voor openbare IP-adressen.
- Meld u bij Azure toohello [portal](https://portal.azure.com), Azure-opdrachtregelinterface (CLI) of Azure PowerShell gebruiken met een Azure-account. Als u nog een Azure-account hebt, zich aanmelden voor een [gratis proefaccount](https://azure.microsoft.com/free).
- Als u met behulp van PowerShell-opdrachten toocomplete taken in dit artikel [Azure PowerShell installeren en configureren](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure PowerShell commandlets geïnstalleerd. tooget help voor PowerShell-opdrachten, met voorbeelden, typ `get-help <command> -full`.
- Als u met behulp van Azure-opdrachtregelinterface (CLI) taken in dit artikel toocomplete opdrachten [installeren en configureren van Azure CLI Hallo](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Zorg ervoor dat u hebt de meest recente versie Hallo van hello Azure CLI is geïnstalleerd. tooget help voor CLI-opdrachten, typ `az <command> --help`. In plaats van installatie Hallo CLI en de vereisten, kunt u hello Azure Cloud-Shell. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft. toouse hello Cloud-Shell, klikt u op Hallo Cloud Shell **> _** knop bovenaan Hallo Hallo [portal](https://portal.azure.com).

Openbare IP-adressen hebben nominaal kosten met zich mee. Hallo tooview Hallo prijzen lezen [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. 

## <a name="create-a-public-ip-address"></a>Een openbaar IP-adres maken

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *openbaar IP-adres*. Wanneer **openbare IP-adressen** wordt weergegeven in zoekresultaten hello, klik erop.
3. Klik op **+ toevoegen** in Hallo **openbaar IP-adres** blade die wordt weergegeven.
4. Typ of Selecteer waarden voor de volgende instellingen in Hallo Hallo **openbare IP-adres maken** blade die wordt weergegeven, klikt u vervolgens op **maken**:

    |Instelling|Vereist?|Details|
    |---|---|---|
    |Naam|Ja|Hallo-naam moet uniek zijn binnen het Hallo-resourcegroep die u selecteert.|
    |IP-versie|Ja| Selecteer IPv4 of IPv6. Tijdens het openbare IPv4 adressen kunnen worden toegewezen tooseveral Azure-resources, kan een IPv6-openbare IP-adres alleen worden toegewezen tooan internetgerichte load balancer. Hallo load balancer kunt laden saldo IPv6-verkeer tooAzure virtuele machines. Meer informatie over [taakverdeling IPv6-verkeer toovirtual machines](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
    |IP-adrestoewijzing|Ja|**Dynamische:** dynamische adressen alleen nadat Hallo openbare IP-adres gekoppeld is tooa NIC tooa VM gekoppeld en hello VM is gestart voor Hallo eerst worden toegewezen. Dynamische adressen kunnen wijzigen als Hallo VM Hallo NIC gekoppelde toois gestopt (toewijzing opgeheven). Hallo adres blijft Hallo dezelfde als hello VM wordt opnieuw opgestart of gestopt (maar niet de toewijzing ongedaan gemaakt). **Statische:** statische adressen worden toegewezen als Hallo openbaar IP-adres wordt gemaakt. Statische adressen komen niet wijzigen zelfs dat als hello VM wordt geplaatst in Hallo gestopt (toewijzing opgeheven) staat. Hallo-adres wordt alleen vrijgegeven wanneer Hallo NIC wordt verwijderd. U kunt de toewijzingsmethode Hallo wijzigen nadat Hallo NIC is gemaakt. Als u IPv6 voor Hallo **IP-versie**, is de enige beschikbare toewijzingsmethode Hallo **dynamische**.|
    |Time-out voor inactiviteit (minuten)|Nee|Hoeveel minuten een TCP- of HTTP-verbinding open zonder afhankelijk te zijn van keepalive-berichten van clients toosend tookeep. Als u IPv6 voor selecteert **IP-versie**, deze waarde kan niet worden gewijzigd. |
    |Label van DNS-naam|Nee|Moet uniek zijn binnen hello Azure-locatie voor het maken van de Hallo-naam in (voor alle abonnementen en alle klanten). Hello Azure openbare DNS-service automatisch geregistreerd Hallo naam en IP-adres zodat tooa resource met de naam van de Hallo verbinding kunnen maken. Azure voegt *location.cloudapp.azure.com* (waarbij locatie Hallo locatie die u selecteert) toohello die u opgeeft toocreate Hallo volledig gekwalificeerde DNS-naam. Als u ervoor toocreate beide versies van het adres kiest, hello dezelfde DNS-naam toegewezen tooboth Hallo IPv4 en IPv6-adressen. Hello Azure DNS-service bevat zowel IPv4 A en AAAA IPv6-records van naam en reageert met beide records wanneer Hallo DNS-naam wordt opgezocht. Hallo client kiezen welke adres (IPv4 of IPv6) toocommunicate met.|
    |Een IPv6-(of IPv4)-adres maken|Nee| Of IPv6- of IPv4 wordt weergegeven is afhankelijk van wat u selecteren voor **IP-versie**. Als u bijvoorbeeld **IPv4** voor **IP-versie**, **IPv6** hier weergegeven.
    |De naam (alleen zichtbaar als u dit selectievakje Hallo inschakelt **een adres IPv6 (of IPv4) maakt** selectievakje)|Ja, als u Hallo **maken van een IPv6** (of IPv4) selectievakje.|Hallo naam moet anders zijn dan de naam van de Hallo u Hallo eerst invoeren **naam** in deze lijst. Als u toocreate zowel een IPv4- als een IPv6-adres kiest, maakt Hallo portal twee afzonderlijke openbare IP-adresbronnen, één met elk IP-adresversie tooit toegewezen.|
    |IP-adrestoewijzing (alleen zichtbaar als u dit selectievakje Hallo inschakelt **een adres IPv6 (of IPv4) maakt** selectievakje)|Ja, als u Hallo **maken van een IPv6** (of IPv4) selectievakje.|Als er op Hallo selectievakje **maken van een IPv4-adres**, kunt u een methode voor het toewijzen. Als er op Hallo selectievakje **maken van een IPv6-adres**, u kunt geen een methode voor het toewijzen, zoals het moet selecteren **dynamische**.|
    |Abonnement|Ja|Moet bestaan in Hallo dezelfde [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) Hallo resource dat u wilt tooassociate Hallo openbaar IP-adres op.|
    |Resourcegroep|Ja|Kan bestaan in Hallo dezelfde of verschillende, [resourcegroep](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) Hallo resource dat u wilt tooassociate Hallo openbaar IP-adres op.|
    |Locatie|Ja|Moet bestaan in Hallo dezelfde [locatie](https://azure.microsoft.com/regions), tooas regio, wordt ook wel aangeduid als Hallo-bron die u wilt dat tooassociate Hallo openbaar IP-adres op.|

**Opdrachten**

Hoewel Hallo portal biedt Hallo optie toocreate twee openbare IP-adresbronnen (één IPv4- en één IPv6), maken Hallo CLI PowerShell-opdrachten en na één resource met een adres voor één IP-versie of Hallo andere. Als u wilt dat twee openbare IP-adresbronnen, één voor elk IP-versie, moet u Hallo opdracht twee keer uitvoeren opgeven van verschillende namen en versies voor Hallo openbare IP-adresbronnen. 

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ netwerk openbare ip-maken](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Nieuwe AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>Weergeven, instellingen voor wijzigen of verwijderen van een openbaar IP-adres

1. Meld u bij toohello [Azure-portal](https://portal.azure.com) met een account dat is toegewezen (minimaal) machtigingen voor Hallo Network Contributor rol voor uw abonnement. Lees Hallo [ingebouwde functies voor op rollen gebaseerd toegangsbeheer van Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artikel toolearn meer over het toewijzen van rollen en machtigingen tooaccounts.
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *openbaar IP-adres*. Wanneer **openbare IP-adressen** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **openbare IP-adressen** blade die wordt weergegeven, klikt u op naam Hallo Hallo openbare IP-adres wilt tooview, instellingen voor wijzigen of verwijderen.
4. Hallo-blade die wordt weergegeven voor Hallo openbare IP-adres, volledige één Hallo volgend opties, afhankelijk van of u tooview, wilt verwijderen of wijzigen van Hallo openbaar IP-adres.
    - **Weergave**: Hallo **overzicht** sectie van de blade Hallo wordt registersleutelinstellingen voor Hallo openbare IP-adres, zoals Hallo netwerkinterface bijbehorende te (als Hallo adres netwerkinterface gekoppeld tooa). Hallo portal weergegeven Hallo-versie van het Hallo-adres (IPv4 of IPv6) niet. tooview hello versie-informatie Hallo Gebruik PowerShell of CLI opdracht tooview Hallo openbaar IP-adres. Als Hallo IP-adresversie IPv6 is, wordt niet Hallo-adres toegewezen door het Hallo-portal, PowerShell of CLI Hallo weergegeven. 
    - **Verwijderen**: toodelete Hallo openbare IP-adres, klikt u op **verwijderen** in Hallo **overzicht** sectie van het Hallo-blade. Als het Hallo-adres is momenteel gekoppeld tooan IP-configuratie, kan niet worden verwijderd. Als het Hallo-adres is momenteel gekoppeld aan een configuratie, klikt u op **Dissociate** toodissociate Hallo-adres van Hallo IP-configuratie.
    - **Wijziging**: klik op **configuratie**. De instellingen wijzigen met Hallo informatie in stap 4 van Hallo [maken van een openbaar IP-adres](#create-a-public-ip-address) sectie van dit artikel. toochange hello toewijzing voor een IPv4-adres van de statische toodynamic, moet u eerst Hallo openbaar IPv4-adres van deze gekoppeld aan de IP-configuratie Hallo ontkoppelen. U kunt vervolgens Hallo toewijzing methode toodynamic wijzigen en klik op **koppelen** tooassociate Hallo IP-adres toohello hetzelfde IP-configuratie, een andere configuratie, of u kunt laten ontkoppeld. een openbaar IP-adres in Hallo toodissociate **overzicht** sectie, klikt u op **Dissociate**.

>[!WARNING]
>Als u Hallo methode voor het toewijzen van vaste toodynamic wijzigt, verliest u Hallo IP-adres dat toohello openbaar IP-adres is toegewezen. Terwijl hello Azure openbare DNS-servers onderhouden van een toewijzing tussen statische of dynamische adressen en elk label DNS-naam (als u een gedefinieerd), wordt een dynamisch IP-adres kunt wijzigen als Hallo VM wordt opgestart nadat in Hallo (toewijzing ongedaan gemaakt) staat gestopt. tooprevent Hallo-adres van de te wijzigen, een statisch IP-adres toewijzen.

**Opdrachten**

|Hulpprogramma|Opdracht|
|---|---|
|CLI|[AZ lijst van een openbaar ip-netwerk](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist openbare IP-adressen, [az netwerk openbare-ip-weergeven](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow instellingen. [az netwerk openbare ip-update](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update) tooupdate; [az netwerk openbare ip-verwijderen](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete) toodelete|
|PowerShell|[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve een openbaar IP-adres object op te lossen en de instellingen weergeven [Set AzureRmPublicIpAddress](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooupdate instellingen. [Verwijderen AzureRmPublicIpAddress](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>Volgende stappen
Openbare IP-adressen toewijzen bij het maken van hello Azure-resources te volgen:

- [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtuele machines
- [Internetgerichte Azure Load Balancer](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure Application Gateway](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Site-naar-site-verbinding met een Azure VPN-Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure virtuele-Machineschaalset](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
