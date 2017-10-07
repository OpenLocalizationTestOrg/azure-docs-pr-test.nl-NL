---
title: adressen van de beheerserver aaaAzure App Service-omgeving
description: Adressen van de lijsten Hallo beheerserver gebruikt toocommand een App-serviceomgeving
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a>Adressen van de beheerserver App Service-omgeving

Hallo-App Service Environment(ASE) is een implementatie van hello Azure App Service in een subnet in uw Azure Virtual Network (VNet).  Hallo as-omgeving moet toegankelijk is vanaf hello Azure App Service, zodat deze kan worden beheerd.  Deze as-omgeving beheer van verkeer passeert Hallo gebruiker beheerd netwerk.  Het is afkomstig uit Azure App Service management servers toohello openbare VIP die is gekoppeld aan het Hallo-as-omgeving.  Voor meer informatie over Hallo as-omgeving networking afhankelijkheden lezen [-overwegingen en Hallo App Service-omgeving][networking].  Voor algemene informatie over het Hallo-as-omgeving kunt u beginnen met [inleiding toohello App Service-omgeving][intro].

Dit document worden Hallo bron, IP-adressen voor beheer van verkeer toohello as-omgeving. U kunt deze adressen toocreate Netwerkbeveiligingsgroepen toolock omlaag binnenkomend verkeer gebruiken of in routetabellen gebruiken, indien nodig.  toouse deze informatie moet u toouse:

* Hallo IP-adressen die worden vermeld voor alle regio 's
* Hallo IP-adressen die overeenkomen toohello regio die uw as-omgeving is geïmplementeerd in.

Hallo binnenkomende beheer van verkeer binnenkomt van deze IP-adressen tooports 454 en 455.

| Regio | Adressen |
|--------|-----------|
| Alle regio 's | 70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141 |
| Zuid-centraal VS & Noord-centraal VS | 23.102.188.65, 191.236.154.88 |
| Australië-Zuidoost & Australië Oost | 23.101.234.41, 104.210.90.65 |
| VS West & VS Oost | 104.45.227.37, 191.236.60.72 |
| West-Europa & Noord-Europa | 191.233.94.45, 191.237.222.191 |
| West-Centraal VS & VS-West 2 | 13.78.148.75, 13.66.225.188 |
| VS-midden & VS-Oost 2 | 104.43.165.73, 104.46.108.135 |
| Oost-Azië & Zuidoost-Azië | 23.99.115.5, 104.215.158.33 |
| Japan-Oost & Japan-West | 104.41.185.116, 191.239.104.48 |
| Canada-midden & Canada Oost | 40.85.230.101, 40.86.229.100 |
| VK West & VK Zuid | 51.141.8.34, 51.140.185.75 |
| Zuid-Korea & Korea-centraal | 52.231.200.177, 52.231.32.117 |
| Brazilië-Zuid & Zuid-centraal VS| 104.41.46.178, 23.102.188.65 |
| Centrale India en India Zuid | 104.211.98.24, 104.211.225.66 |
| West, India en India Zuid | 104.211.160.229, 104.211.225.66 |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
