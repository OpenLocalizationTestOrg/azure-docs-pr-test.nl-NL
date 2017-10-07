---
title: aaaWhat toodo in geval van een onderbreking van de Azure-service die invloed hebben op Azure Virtual Networks Hallo | Microsoft Docs
description: Meer informatie over welke toodo in Hallo-gebeurtenis van een onderbreking van de Azure-service die invloed hebben op Azure Virtual Networks.
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a>Virtueel netwerk – bedrijfscontinuïteit
## <a name="overview"></a>Overzicht
Een virtueel netwerk (VNet) is een logische representatie van uw netwerk in Hallo cloud. Hiermee kunt u uw eigen persoonlijke IP-adres en het segment Hallo netwerk in subnetten toodefine. VNets fungeert als een grens vertrouwensrelatie toohost uw rekenresources zoals Azure Virtual Machines en Cloud-Services (web/werkrollen). Een VNet maakt directe particuliere IP-communicatie mogelijk tussen Hallo-middelen gehost in het. Een virtueel netwerk kan ook worden gekoppelde tooan on-premises netwerk via een Hallo hybride opties, zoals een VPN-Gateway of ExpressRoute.

Een VNet wordt gemaakt binnen Hallo bereik van een regio. Kunt u VNets met dezelfde adresruimte in twee verschillende regio's (dat wil zeggen VS-Oost en VS-West, maar ze tooone kan geen verbinding rechtstreeks andere). 

## <a name="business-continuity"></a>Bedrijfscontinuïteit
Er zijn verschillende manieren dat uw toepassing kan worden onderbroken. Een bepaald gebied kan worden volledig afgekapt vanwege tooa natuurramp of een gedeeltelijke noodgeval vanwege fout tooa van meerdere apparaten/services. Hallo impact op Hallo VNet service verschilt in elk van deze situaties.

**V: wat moet u doen in geval van een storing tooan hele regio Hallo? dat wil zeggen als een regio volledig ingestelde vanwege tooa natuurramp is? Wat gebeurt er toohello virtuele netwerken die worden gehost in Hallo regio?**

A: Hallo virtuele netwerk en Hallo resources in Hallo van invloed op een regio systeemcache is niet toegankelijk tijdens Hallo van Hallo service wordt onderbroken.

![Eenvoudige virtuele-netwerkdiagram](./media/virtual-network-disaster-recovery-guidance/vnet.png)

**V: wat kan ik toodo opnieuw maken Hallo hetzelfde virtuele netwerk in een andere regio?**

A: virtueel netwerk (VNet) is redelijk lightweight bron. U kunt Azure-API's toocreate een VNet aanroepen Hello dezelfde adresruimte in een andere regio. toore-Hallo maken dezelfde omgeving die aanwezig in Hallo was van invloed op een regio, hebt u toomake API-aanroepen toore-Implementeer uw Cloudservices (web/werkrollen) en virtuele Machines die u had. U moet ook toospin-up maken van een VPN-Gateway en tooyour on-premises netwerk verbinding maken als u had lokale connectiviteit (zoals in een hybride implementatie).

vindt u instructies voor het maken van een VNet Hello [hier](virtual-networks-create-vnet-arm-pportal.md). 

**V: kan een replica van een VNet in een bepaald gebied niet opnieuw worden gemaakt in een andere regio tevoren?**

A: Ja, kunt u twee VNets Hallo met hetzelfde privé-IP-adresruimte en resources in twee verschillende regio's voor tijd. Als een klant internetgericht services in Hallo VNet host is, kunnen ze hebben ingesteld toogeo Traffic Manager-route verkeer toohello regio die actief is. Echter, een klant twee VNets kan geen verbinding met de Hallo dezelfde ruimte tootheir on-premises netwerk adres zoals dit routering problemen veroorzaakt. Aan het Hallo-tijd van een noodgeval en verlies van een VNet in één regio, een klant verbinding kan maken Hallo van andere VNet in Hallo beschikbare regio met overeenkomende adresruimte tootheir on-premises netwerk.

vindt u instructies voor het maken van een VNet Hello [hier](virtual-networks-create-vnet-arm-pportal.md).

