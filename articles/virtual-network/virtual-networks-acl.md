---
title: aaaWhat is een netwerk van Azure access control list?
description: Meer informatie over toegangscontrolelijsten in Azure
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 83d66c84-8f6b-4388-8767-cd2de3e72d76
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a2681af035d162362771e6df9864bbe838f16352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-endpoint-access-control-list"></a>Wat is er een eindpunt-ACL's?

> [!IMPORTANT]
> Azure heeft twee verschillende [implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) voor het maken en werken met resources: Resource Manager en classic. In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties Hallo Resource Manager-implementatiemodel gebruiken. 

Een eindpunt toegangsbeheerlijst (ACL) is een beveiligingsverbetering beschikbaar voor uw Azure-implementatie. Een ACL biedt Hallo mogelijkheid tooselectively toestaan of weigeren van verkeer voor het eindpunt van een virtuele machine. Deze pakketten filteren mogelijkheid biedt een extra beveiligingslaag. U kunt de netwerk-ACL's voor eindpunten alleen opgeven. U kunt een ACL voor een virtueel netwerk of een specifiek subnet opgenomen in een virtueel netwerk niet opgeven. Het verdient aanbeveling toouse netwerkbeveiligingsgroepen (nsg's) in plaats van ACL's, indien mogelijk. toolearn meer informatie over het nsg's, Zie [netwerk beveiligingsoverzicht van groep](virtual-networks-nsg.md)

ACL's kunnen worden geconfigureerd met behulp van PowerShell of hello Azure-portal. tooconfigure een ACL-netwerk met behulp van PowerShell, Zie [toegangsbeheerlijsten voor eindpunten met behulp van PowerShell beheren](virtual-networks-acl-powershell.md). tooconfigure een ACL-netwerk met behulp van Azure portal, Zie Hallo [hoe tooset eindpunten tooa virtuele machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Met de netwerk-ACL's, kunt u doen Hallo volgende:

* Selectief toestaan of weigeren van inkomend verkeer op basis van een extern subnet IPv4-adresbereik tooa virtuele machine invoereindpunt.
* Blacklist IP-adressen
* Meerdere regels per eindpunt van de virtuele machine maken
* Regel ordening tooensure Hallo juiste reeks regels worden toegepast op een opgegeven virtuele machine-eindpunt (laagste toohighest) gebruiken
* Geef een ACL voor een specifieke extern subnet IPv4-adres.

Zie Hallo [Azure beperkt](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) artikel voor ACL-limieten.

## <a name="how-acls-work"></a>De werking van ACL 's
Een ACL is een object dat een lijst met regels bevat. Wanneer u een ACL te maken en deze eindpunt van de virtuele machine tooa toe te passen, pakket voor het filteren van plaatsvindt op Hallo hostknooppunt van uw virtuele machine. Dit betekent dat het Hallo-verkeer van externe IP-adressen wordt gefilterd op Hallo hostknooppunt voor de overeenkomende ACL-regels in plaats van op de virtuele machine. Dit voorkomt dat uw virtuele machine Hallo kostbare CPU-cycli uitgaven voor het filteren van netwerkpakketten.

Wanneer een virtuele machine is gemaakt, wordt standaard ACL plaatsen in plaats tooblock alle binnenkomend verkeer. Echter, als een eindpunt is gemaakt voor (poort 3389), vervolgens Hallo-standaard-ACL is gewijzigd tooallow alle binnenkomend verkeer voor dat eindpunt. Binnenkomend verkeer van een extern subnet wordt vervolgens de toegestane toothat eindpunt en geen firewall inrichting is vereist. Alle andere poorten worden geblokkeerd voor binnenkomend verkeer, tenzij eindpunten voor deze poorten worden gemaakt. Standaard is uitgaand verkeer toegestaan.

**Standaard ACL voorbeeldtabel**

| **Regel #** | **Extern Subnet** | **Eindpunt** | **Toestaan/weigeren** |
| --- | --- | --- | --- |
| 100 |0.0.0.0/0 |3389 |Toestaan |

## <a name="permit-and-deny"></a>Toestaan en weigeren
U kunt selectief toestaan of weigeren voor een virtuele machine-invoereindpunt verkeer door regels die specificeren 'toestaan' of 'niet toestaan' te maken. Het is belangrijk toonote dat standaard, wanneer een eindpunt is gemaakt, al het verkeer is toegestaan toohello eindpunt. Daarom is het belangrijk toounderstand hoe toocreate regels toestaan/weigeren en plaats deze in de juiste volgorde van prioriteit Hallo als u wilt dat gedetailleerde controle over Hallo netwerk verkeer die u kiest tooallow tooreach Hallo het eindpunt van virtuele machine.

Tooconsider punten:

1. **Er is geen ACL-** standaard wanneer een eindpunt is gemaakt, we verlenen voor Hallo-eindpunt.
2. **Toestaan -** wanneer u een of meer 'toestaan' bereiken toevoegt, weigert u alle andere bereiken standaard. Alleen de pakketten van Hallo toegestane IP-bereik worden kunnen toocommunicate met het eindpunt van de virtuele machine Hallo.
3. **DENY -** wanneer u een of meer 'niet toestaan' bereiken toevoegt, verleent u andere bereiken van het verkeer standaard.
4. **Combinatie van toestaan en weigeren -** kunt u een combinatie van 'toestaan' en 'niet toestaan' als u wilt dat toocarve uit een specifiek IP-adres bereik toobe toegestaan of geweigerd.

## <a name="rules-and-rule-precedence"></a>Regels en de prioriteit van regels
Netwerk-ACL's kunnen worden ingesteld op de eindpunten van specifieke virtuele machine. U kunt bijvoorbeeld een netwerk-ACL voor een RDP-eindpunt gemaakt op een virtuele machine welke vergrendelingen de toegang voor bepaalde IP-adressen opgeven. Hallo onderstaande tabel ziet u een manier toogrant toegang toopublic virtuele IP-adressen (VIP's) van een bepaalde bereik toopermit toegang voor RDP. Alle andere externe IP-adressen geweigerd. Er volgt een *laagste voorrang* regel volgorde.

### <a name="multiple-rules"></a>Meerdere regels
In onderstaande Hallo voorbeeld, als u wilt dat tooallow toegang toohello RDP-eindpunt alleen via twee openbare IPv4-adresbereiken (65.0.0.0/8 en 159.0.0.0/8), u kunt dit doen door op te geven dat twee *toestaan* regels. Aangezien RDP standaard voor een virtuele machine wordt gemaakt, kunt u in dit geval toolock omlaag toohello RDP toegangspoort op basis van een extern subnet. Hallo volgende voorbeeld ziet u een manier toogrant toegang toopublic virtuele IP-adressen (VIP's) van een bepaalde bereik toopermit toegang voor RDP. Alle andere externe IP-adressen geweigerd. Dit werkt omdat netwerk ACL's kan worden ingesteld voor een specifieke virtuele machine-eindpunt en standaard toegang is geweigerd.

**Voorbeeld: meerdere regels**

| **Regel #** | **Extern Subnet** | **Eindpunt** | **Toestaan/weigeren** |
| --- | --- | --- | --- |
| 100 |65.0.0.0/8 |3389 |Toestaan |
| 200 |159.0.0.0/8 |3389 |Toestaan |

### <a name="rule-order"></a>De regelvolgorde van de
Omdat meerdere regels kunnen worden opgegeven voor een eindpunt, moet er een manier tooorganize regels in volgorde toodetermine welke regels voorrang. Hallo regelvolgorde geeft prioriteit. Netwerk-ACL's Volg een *laagste voorrang* regel volgorde. In Hallo onderstaand voorbeeld Hallo-eindpunt op poort 80 selectief tooonly toegang verleend bepaalde IP-adresbereiken. tooconfigure, hebben we een regel voor weigeren (regel \# 100) voor adressen in Hallo 175.1.0.1/24 ruimte. Een tweede regel is vervolgens met prioriteit 200 of kunnen inhoud toegang hebt tot tooall andere adressen onder 175.0.0.0/8 opgegeven.

**Voorbeeld: de prioriteit van regels**

| **Regel #** | **Extern Subnet** | **Eindpunt** | **Toestaan/weigeren** |
| --- | --- | --- | --- |
| 100 |175.1.0.1/24 |80 |Weigeren |
| 200 |175.0.0.0/8 |80 |Toestaan |

## <a name="network-acls-and-load-balanced-sets"></a>Netwerk-ACL's en taakverdeling sets laden
Netwerk-ACL's kunnen worden opgegeven op een eindpunt van de set taakverdeling. Als een ACL voor een set met gelijke taakverdeling is opgegeven, is het Hallo netwerk ACL toegepaste tooall virtuele machines in die set met gelijke taakverdeling. Bijvoorbeeld, als een set met gelijke taakverdeling met 'Poort 80' is gemaakt en Hallo set met gelijke taakverdeling 3 VM's, Hallo netwerk ACL op eindpunt bevat gemaakt 'Poort 80' van een die virtuele machine automatisch wordt toepassen toohello andere virtuele machines.

![Netwerk-ACL's en taakverdeling sets laden](./media/virtual-networks-acl/IC674733.png)

## <a name="next-steps"></a>Volgende stappen
[Toegangsbeheerlijsten voor eindpunten met behulp van PowerShell beheren](virtual-networks-acl-powershell.md)

