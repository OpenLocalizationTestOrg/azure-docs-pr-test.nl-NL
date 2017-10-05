---
title: "Lijst met poorten en URL's voor goedgekeurde IP-adressen voor Azure RemoteApp geïmplementeerd in het virtuele netwerk van de klant | Microsoft Docs"
description: Meer informatie over welke poorten en URL's u wilt configureren voor communicatie via Azure RemoteApp.
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
ms.openlocfilehash: c17ff8d5441ca92f7b893edb541a1e9730c2a847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Lijst met poorten en URL's om toegang te verlenen voor Azure RemoteApp geïmplementeerd in klant virtueel netwerk
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Als u een Azure RemoteApp-cloud of hybride verzameling in een virtueel netwerk (VNET) implementeert, raadpleegt u de volgende poortinformatie. Lees voor meer informatie over virtuele netwerken [Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md). Als u verkeer beperkt tot de resources van het virtuele netwerk in uw verzameling een netwerkbeveiligingsgroep (NSG) hebt gemaakt, zorg er dan voor dat de volgende poorten zijn toegankelijk is en is toegestaan door het beveiligingsbeleid op het virtuele netwerk. Lees voor meer informatie over netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep? (NSG) ](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a>Azure RemoteApp-subnet moet toegang tot deze eindpunten en URL's:
* *. servicebus.windows.net
* *. servicebus.net
* https://*.RemoteApp.windowsazure.com  
* https://www.RemoteApp.windowsazure.com 
* https://*RemoteApp.windowsazure.com  
* https://*.Core.Windows.NET  
* Uitgaand: TCP: TCP: 443, 9351, 9352, 10101 10175 
* Optioneel – UDP: 10201 10275  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a>Azure RemoteApp-clients moeten toegang tot deze eindpunten en URL's:
Door clients dat ik de desktops, enzovoort. die mensen gebruiken om de apps die worden geïmplementeerd in de Azure RemoteApp-verzameling met apparaten.

* https://telemetry.RemoteApp.windowsazure.com  
* https://*.RemoteApp.windowsazure.com (de optionele UDP-poorten zijn voor dit adres) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.RemoteApp.windowsazure.com 
* https://*.Core.Windows.NET  
* Uitgaand: TCP: 443  
* Optionele - UDP: 3391 

