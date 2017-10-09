---
title: "aaaList van toowhitelist poorten en URL's voor Azure RemoteApp geïmplementeerd in het virtuele netwerk van de klant | Microsoft Docs"
description: Informatie over welke poorten en URL's moet u tooconfigure voor communicatie via Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Lijst met URL's en poorten toopermit toegang voor Azure RemoteApp geïmplementeerd in klant virtueel netwerk
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Als u een Azure RemoteApp-cloud of hybride verzameling in een virtueel netwerk (VNET) implementeert, bekijk Hallo poortinformatie te volgen. Lees voor meer informatie over virtuele netwerken [Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md). Als u een netwerkbeveiligingsgroep (NSG) beperken verkeer toohello virtueel netwerkresources in uw verzameling hebt gemaakt, zorg er dan voor dat Hallo volgende poorten zijn toegankelijk is en is toegestaan via Hallo beveiligingsbeleid op Hallo virtueel netwerk. Lees voor meer informatie over netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep? (NSG) ](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a>Azure RemoteApp-subnet moet toegang toothese eindpunten en URL's:
* *. servicebus.windows.net
* *. servicebus.net
* https://*.RemoteApp.windowsazure.com  
* https://www.RemoteApp.windowsazure.com 
* https://*RemoteApp.windowsazure.com  
* https://*.Core.Windows.NET  
* Uitgaand: TCP: TCP: 443, 9351, 9352, 10101 10175 
* Optioneel – UDP: 10201 10275  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a>Azure RemoteApp-clients moeten toegang tot toothese eindpunten en URL's:
Door clients heb Hallo desktops, apparaten enzovoort die mensen die gebruik tooconnect toohello apps geïmplementeerd in hello Azure RemoteApp-verzameling.

* https://telemetry.RemoteApp.windowsazure.com  
* https://*.RemoteApp.windowsazure.com (Hallo optionele UDP-poorten zijn voor dit adres) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.RemoteApp.windowsazure.com 
* https://*.Core.Windows.NET  
* Uitgaand: TCP: 443  
* Optionele - UDP: 3391 

