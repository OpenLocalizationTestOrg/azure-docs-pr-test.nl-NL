---
title: 'Routefilters voor Azure ExpressRoute Microsoft-peering configureren: PowerShell | Microsoft Docs'
description: Dit artikel wordt beschreven hoe tooconfigure routefilters voor Microsoft-Peering met behulp van PowerShell
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Routefilters voor Microsoft-peering configureren

Routefilters zijn een manier tooconsume een subset van de ondersteunde services via Microsoft-peering. Hallo stappen in dit artikel helpen u te configureren en beheren van routefilters voor ExpressRoute-circuits.

Dynamics 365-services en Office 365-services zoals Exchange Online, SharePoint Online en Skype voor bedrijven, zijn toegankelijk via Hallo Microsoft-peering. Wanneer Microsoft-peering in een ExpressRoute-circuit is geconfigureerd, worden alle voorvoegsels gerelateerde toothese-services worden geadverteerd via Hallo BGP-sessies die zijn gemaakt. Een BGP-communitywaarde is aangesloten tooevery voorvoegsel tooidentify Hallo service die wordt aangeboden via Hallo voorvoegsel. Zie voor een lijst met Hallo BGP-Communitywaarden en deze worden toegewezen aan Hallo-services, [BGP-community's](expressroute-routing.md#bgp).

Als u connectiviteit tooall services vereist, wordt een groot aantal voorvoegsels worden geadverteerd via BGP. Dit aanzienlijk groter Hallo Hallo routetabellen onderhouden door routers in uw netwerk. Als u van plan tooconsume slechts een subset van services die worden aangeboden bent via Microsoft-peering, kunt u de grootte van uw routetabellen op twee manieren Hallo reduceren. U kunt:

- Filter ongewenste voorvoegsels door routefilters zijn toegepast op de BGP-community's. Dit is een standaardprocedure voor netwerken en meestal wordt gebruikt binnen meerdere netwerken.

- Routefilters definiëren en ze tooyour ExpressRoute-circuit toepassen. Een routefilter is een nieuwe resource dat u kunt aangeven Hallo lijst met services die u van plan bent tooconsume via Microsoft-peering. ExpressRoute-routers verzenden alleen Hallo lijst met voorvoegsels die deel uitmaken van toohello services in Hallo routefilter geïdentificeerd.

### <a name="about"></a>Over routefilters

Wanneer Microsoft-peering is geconfigureerd op uw ExpressRoute-circuit, opzetten Hallo Microsoft randrouters een combinatie van BGP-sessies met Hallo-randrouters (jouw e-mailadres of uw connectiviteitsprovider). Er is geen routes worden aangekondigd tooyour netwerk. tooenable route-advertisements tooyour netwerk, moet u een routefilter koppelen.

Een routefilter kunt u identificeren van de services die u wilt dat tooconsume via Microsoft-peering voor uw ExpressRoute-circuit. Het is in wezen een witte lijst van alle Hallo BGP-Communitywaarden. Wanneer een bron routeren filter wordt gedefinieerd en tooan ExpressRoute-circuit gekoppeld, zijn alle voorvoegsels die zijn toegewezen toohello BGP-Communitywaarden aangekondigd tooyour netwerk.

toobe kunnen tooattach routefilters met Office 365-services zich bevinden, moet u autorisatie tooconsume Office 365-services via ExpressRoute hebben. Als u geen geautoriseerde tooconsume Office 365-services via ExpressRoute bent, mislukt de Hallo bewerking tooattach routefilters. Zie voor meer informatie over het autorisatieproces Hallo [Azure ExpressRoute voor Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Connectiviteit tooDynamics 365 services is niet vereist voor alle toestemming.

> [!IMPORTANT]
> Eerdere tooAugust 1 Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd, 2017 hebben alle service voorvoegsels die worden geadverteerd via Microsoft-peering, zelfs als routefilters zijn niet gedefinieerd. Microsoft-peering van ExpressRoute-circuits die zijn geconfigureerd op of na 1 augustus 2017 geen geen voorvoegsels aangekondigd totdat een routefilter wordt aangesloten toohello circuit.
> 
> 

### <a name="workflow"></a>Werkstroom

toobe kunnen toosuccessfully tooservices verbinding via Microsoft-peering, moet u de volgende configuratiestappen Hallo uitvoeren:

- U moet een actief ExpressRoute-circuit met Microsoft-peering ingerichte hebben. U kunt deze taken Hallo tooaccomplish instructies te volgen:
  - [Maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat. Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld.
  - [Microsoft-peering maken](expressroute-circuit-peerings.md) als u rechtstreeks Hallo BGP-sessie beheren. Of vraag uw connectiviteitsprovider Microsoft-peering voor uw circuit inrichten.

-  U moet maken en configureren van een routefilter.
    - Identificeren Hallo services die u met tooconsume via Microsoft-peering
    - Lijst van BGP-Communitywaarden die zijn gekoppeld aan services Hallo Hallo identificeren
    - Maak een regel tooallow Hallo voorvoegsel lijst overeenkomende Hallo BGP-Communitywaarden

-  Hallo route filter toohello ExpressRoute-circuit, moet u koppelen.

## <a name="before-you-begin"></a>Voordat u begint

Voordat u begint met de configuratie, zorg er dan voor dat u voldoet aan Hallo volgende criteria:

 - Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets. Zie voor meer informatie [installeren en configureren van Azure PowerShelll](/powershell/azure/install-azurerm-ps).

  > [!NOTE]
  > Download de nieuwste versie Hallo bij Hallo PowerShell Gallery in plaats van met behulp van Hallo installatieprogramma. Hallo installatieprogramma momenteel biedt geen ondersteuning voor cmdlets Hallo vereist.
  > 

 - Bekijk Hallo [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.

 - U moet een actief ExpressRoute-circuit hebben. Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat. Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld.

 - U hebt een actieve Microsoft-peering. Volg de instructies op [maken en wijzigen van peeringconfiguratie](expressroute-circuit-peerings.md)

### <a name="log-in-tooyour-azure-account"></a>Meld u bij tooyour Azure-account

Voordat u deze configuratie, moet u zich aanmeldt tooyour Azure-account. Hallo-cmdlet wordt u gevraagd om de aanmeldingsreferenties Hallo voor uw Azure-account. Na het aanmelden, downloadt het instellingen van uw account, zodat ze beschikbaar tooAzure PowerShell.

Open de PowerShell-console met verhoogde bevoegdheden en tooyour-account koppelen. Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:

```powershell
Login-AzureRmAccount
```

Als u meerdere Azure-abonnementen hebt, controleert u Hallo abonnementen voor Hallo-account.

```powershell
Get-AzureRmSubscription
```

Hallo-abonnement dat u wilt dat toouse opgeven.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="prefixes"></a>Stap 1. Een lijst met voorvoegsels en BGP-Communitywaarden ophalen

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Een lijst met waarden van BGP-community

Gebruik Hallo cmdlet tooget Hallo lijst met BGP-Communitywaarden die zijn gekoppeld aan services toegankelijk zijn via Microsoft-peering te volgen en Hallo lijst met voorvoegsels die zijn gekoppeld:

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Maak een lijst van Hallo waarden die u toouse wilt

Maak een lijst van BGP-Communitywaarden die u wilt dat toouse in Hallo routefilter. Hallo BGP-communitywaarde voor Dynamics 365 services is een voorbeeld: 12076:5040.

## <a name="filter"></a>Stap 2. Maak een routefilter en een filterregel

Een routefilter kan slechts één regel, en Hallo regel moet van het type 'Toestaan'. Deze regel kan een lijst met BGP-Communitywaarden die zijn gekoppeld hebben.

### <a name="1-create-a-route-filter"></a>1. Maken van een routefilter

Maak eerst Hallo routefilter. Hallo-opdracht 'New-AzureRmRouteFilter' wordt alleen een bron routeren filter. Nadat u Hallo bron maakt, moet u vervolgens maakt u een regel en koppelt u dit object toohello route-filter. Voer Hallo opdracht toocreate na een bron routeren filter:

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a>2. Een filterregel maken

U kunt een set van BGP-community's opgeven als een lijst door komma's gescheiden zoals weergegeven in Hallo voorbeeld. Voer Hallo opdracht toocreate na een nieuwe regel:
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a>3. Hallo regel toohello route-filter toevoegen

Voer Hallo opdracht tooadd Hallo regel toohello route datumfilter te volgen:
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="attach"></a>Stap 3. Hallo route filter tooan ExpressRoute-circuit koppelen

Voer Hallo opdracht tooattach Hallo route filter toohello ExpressRoute-circuit, ervan uitgaande dat u hebt alleen Microsoft-peering te volgen:

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="getproperties"></a>tooget hello eigenschappen van een routefilter

tooget hello eigenschappen van een routefilter, gebruik Hallo stappen te volgen:

1. Voer Hallo opdracht tooget Hallo route filter resource te volgen:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. Hallo route filterregels voor Hallo route-filter resource ophalen door het uitvoeren van de volgende opdracht Hallo:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <a name="updateproperties"></a>tooupdate hello eigenschappen van een routefilter

Als Hallo routefilter is al gekoppeld tooa circuit, lijst met updates toohello BGP-community automatisch doorgegeven wijzigingen van de juiste voorvoegsel aankondiging via de BGP-sessies Hallo tot stand gebracht. U kunt Hallo BGP-community lijst van de routefilter met behulp van de volgende opdracht Hallo bijwerken:

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="detach"></a>een routefilter van een ExpressRoute-circuit toodetach

Zodra een routefilter wordt losgekoppeld van Hallo ExpressRoute-circuit, worden er geen voorvoegsels zijn geadverteerd via Hallo BGP-sessie. U kunt een routefilter van een ExpressRoute-circuit met behulp van de volgende opdracht Hallo loskoppelen:
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="delete"></a>een routefilter toodelete

U kunt alleen verwijderen routefilter als het is niet gekoppeld tooany circuit. Zorg ervoor dat Hallo route-filter is niet gekoppeld tooany circuit voordat u probeert toodelete deze. U kunt een routefilter met behulp van de volgende opdracht Hallo verwijderen:

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).
