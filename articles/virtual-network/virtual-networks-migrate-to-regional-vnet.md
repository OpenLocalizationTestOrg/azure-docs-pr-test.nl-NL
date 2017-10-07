---
title: een Azure-netwerk (klassiek) van een affiniteitsgroep tooa regio aaaMigrate | Microsoft Docs
description: Meer informatie over hoe een virtueel netwerk (klassiek) uit een affiniteit toomigrate tooa regio groepeert.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a>Een virtueel netwerk (klassiek) migreren van een affiniteitsgroep tooa regio

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties Hallo Resource Manager-implementatiemodel gebruiken.

Affiniteitsgroepen ervoor dat resources gemaakt binnen Hallo dezelfde affiniteitsgroep fysiek op servers die zich dicht bij elkaar inschakelen van deze resources toocommunicate sneller worden gehost. In de Hallo is afgelopen waren affiniteitsgroepen een vereiste voor het maken van virtuele netwerken (klassiek). Op dat moment werken Hallo manager netwerkservice die beheerd virtuele netwerken (klassiek) kan alleen binnen een set van fysieke servers of schaaleenheid. Architectuur verbeteringen toegenomen Hallo bereik van netwerk management tooa regio.

Als gevolg van deze architectuur verbeteringen zijn affiniteitsgroepen niet langer aanbevolen of vereist zijn voor virtuele netwerken (klassiek). Hallo gebruik van affiniteitsgroepen voor virtuele netwerken (klassiek) wordt vervangen door de regio's. Regionale virtuele netwerken, virtuele netwerken (klassiek) die gekoppeld aan de regio's zijn worden genoemd.

Het is raadzaam dat u in het algemeen affiniteitsgroepen niet gebruikt. Behalve Hallo virtueel netwerk vereiste, affiniteitsgroepen is ook belangrijk toouse tooensure resources, zoals berekeningen (klassiek) en opslag (klassiek), in de buurt van elkaar zijn geplaatst. Met de huidige Azure-netwerkarchitectuur hello zijn niet langer deze vereisten plaatsing vereist.

> [!IMPORTANT]
> Hoewel het technisch nog steeds mogelijk toocreate een virtueel netwerk dat is gekoppeld aan een affiniteitsgroep, is er geen dwingende redenen toodo dus. Veel functies van virtueel netwerk, zoals netwerkbeveiligingsgroepen, zijn alleen beschikbaar wanneer u een regionaal virtueel netwerk en zijn niet beschikbaar voor virtuele netwerken die gekoppeld aan affiniteitsgroepen zijn.
> 
> 

## <a name="edit-hello-network-configuration-file"></a>Hallo netwerk configuratiebestand bewerken

1. Hallo netwerk configuratiebestand exporteren. Zie toolearn hoe tooexport netwerkconfiguratie bestand met PowerShell of Azure-opdrachtregelinterface (CLI) 1.0, Hallo [configureren van een virtueel netwerk met een netwerk-configuratiebestand](virtual-networks-using-network-configuration-file.md#export).
2. Hallo netwerkconfiguratiebestand bewerken vervangen **AffinityGroup** met **locatie**. Geef van een Azure [regio](https://azure.microsoft.com/regions) voor **locatie**.
   
   > [!NOTE]
   > Hallo **locatie** Hallo regio die u hebt opgegeven voor affiniteitsgroep Hallo die is gekoppeld aan het virtuele netwerk (klassiek). Als het virtuele netwerk (klassiek) is gekoppeld aan een affiniteitsgroep die zich in VS-West, wanneer u migreert, bijvoorbeeld uw **locatie** tooWest VS moet verwijzen. 
   > 
   > 
   
    Hallo volgende regels in het configuratiebestand van uw netwerk, waarbij Hallo waarden vervangt door uw eigen bewerken: 
   
    **Oude waarde:** \<VirtualNetworkSitename = 'VNetUSWest' AffinityGroup = "VNetDemoAG"\> 
   
    **Nieuwe waarde:** \<VirtualNetworkSitename = "VNetUSWest" locatie 'VS-West' =\>
3. Uw wijzigingen hebt opgeslagen en [importeren](virtual-networks-using-network-configuration-file.md#import) Hallo van network configuration tooAzure.

> [!NOTE]
> Deze migratie veroorzaakt geen downtime tooyour services.
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a>Welke toodo als u een virtuele machine (klassiek) in een affiniteitsgroep hebt
VMs (klassiek) die momenteel in een affiniteitsgroep nodig toobe verwijderd uit de affiniteitsgroep Hallo is niet. Als een virtuele machine is geïmplementeerd, is het geïmplementeerde tooa één schaaleenheid. Affiniteitsgroepen kunt beperken Hallo set beschikbare VM-grootten voor een nieuwe VM-implementatie, maar er is al een bestaande virtuele machine die wordt geïmplementeerd beperkt toohello set van VM-groottes beschikbaar in Hallo schaaleenheid in welke Hallo VM is geïmplementeerd. Omdat Hallo die VM al is geïmplementeerd tooa schaaleenheid, heeft een virtuele machine verwijderen uit een affiniteitsgroep geen effect op Hallo VM.
