---
title: aaaValidate hello Azure VNET toouse met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toomake ervoor dat uw Azure VNET is gereed toouse met Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a>Hello Azure VNET toouse met Azure RemoteApp valideren
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Voordat u een Azure-VNET met Azure RemoteApp gebruiken, kunt u toovalidate hello VNET. Hiermee voorkomt u problemen met de connectiviteit.

toovalidate uw Azure-VNET Hallo te volgen:

1. Maak een virtuele machine van Azure binnen Hallo subnet van hello Azure VNET gewenste toouse met Azure RemoteApp.
2. Toothat VM verbinding via Hallo **Connect** optie in Hallo-beheerportal.
3. Hallo virtuele machine toohello deelnemen aan hetzelfde domein dat u wilt dat toouse met Azure RemoteApp. Als u een hybride verzameling die tooyour on-premises netwerk verbindt, lid worden van Hallo virtuele machine tooyour lokale domein.

Als dit lukt, is hello Azure VNET gereed toouse met RemoteApp.

Zie voor meer informatie over Hallo end-to-end hybride verzameling werkstroom Hallo artikelen te volgen:

* [Hoe tooplan het virtuele netwerk voor Azure RemoteApp](remoteapp-planvnet.md)
* [Een hybride verzameling maken](remoteapp-create-hybrid-deployment.md)
* [Azure RemoteApp-collectie tooyour Azure Virtual Network (met ondersteuning voor ExpressRoute) implementeren](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

