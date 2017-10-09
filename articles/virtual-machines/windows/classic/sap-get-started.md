---
title: aaaUsing SAP op Windows virtuele machines | Microsoft Docs
description: Schakel over het gebruik van SAP op virtuele machines (VM's) in Microsoft Azure
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a>SAP gebruiken op Windows virtuele machines in Azure
Cloudcomputing is een veelgebruikte term die meer belang binnen Hallo IT-sector van kleine bedrijven up toolarge en meertalige ondernemingen winnen wordt. Microsoft Azure is Hallo Services Cloudplatform van Microsoft een breed scala aan nieuwe mogelijkheden biedt. Klanten zijn nu kunnen toorapidly leveren en intrekken toepassingen als Cloud-Services, zodat ze niet beperkt tootechnical of budget beperkingen zijn. In plaats van de tijd en geld investeren in hardware-infrastructuur, bedrijven kunnen zich concentreren op de toepassing hello, bedrijfsprocessen en de voordelen voor klanten en gebruikers.

Met Microsoft Azure virtuele machines biedt Microsoft een uitgebreide infrastructuur als een Service (IaaS)-platform. SAP NetWeaver-toepassingen worden ondersteund op virtuele Azure-machines (IaaS). Hallo whitepapers hieronder wordt beschreven hoe tooplan en SAP NetWeaver implementeren op basis van toepassingen op Windows virtuele machines in Azure. U kunt ook SAP NetWeaver op basis van toepassingen implementeren op [virtuele Linux-machines](../../linux/classic/sap-get-started.md).

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a>SAP NetWeaver op Azure - HA
titel: aaaSAP NetWeaver op Azure - Clustering SAP ASC's / SCS exemplaren die gebruikmaken van Windows Server Failover Cluster in Azure met SIOS DataKeeper

Overzicht: ' dit document wordt beschreven hoe toouse SIOS DataKeeper tooset van een maximaal beschikbare configuratie voor SAP ASC's / SCS op Azure. SAP beveiligt hun storingspunt fout onderdelen, zoals SAP ASC's / SCS of in de wachtrij plaatsen replicatie Services met Windows Server Failover Cluster-configuraties waarvoor de gedeelde schijven. Deze SAP-onderdelen zijn essentieel voor het Hallo-functionaliteit van een SAP-systeem. Hoge beschikbaarheid functionaliteit behoeften toobe plaatsen in plaats daarom toomake ervoor dat deze onderdelen een storing van een server of een virtuele machine tolereren kunnen terwijl u doen met Windows clusterconfiguraties voor bare metal- en Hyper-V-omgevingen. Vanaf augustus 2015 kan geen Azure op zichzelf leveren gedeelde schijven die vereist voor Windows hello zijn op basis van maximaal beschikbare configuraties die nodig zijn voor deze kritieke SAP-onderdelen. Aan de hand van de Hallo van Hallo product DataKeeper door SIOS, kunnen echter Failover-Cluster van Windows Server-configuraties die nodig zijn voor SAP ASC's / SCS worden gebaseerd op Hallo Azure IaaS-platform. Dit artikel wordt beschreven in een benadering stap-voor-stap hoe tooinstall een Failover-Cluster van Windows Server-configuratie met gedeelde schijf geleverd door SIOS Datakeeper in Azure. Hallo artikel uitgelegd details in configuraties hello Azure, Windows en SAP-zijde waardoor de configuratie voor hoge beschikbaarheid Hallo op optimale wijze werken. Hallo papier aanvullingen hello SAP-documentatie voor installatie- en SAP-opmerkingen Hallo primaire bronnen voor installaties en implementaties van software op SAP vertegenwoordigen gegeven platforms.

Bijgewerkte: Augustus 2015

[Deze handleiding nu downloaden](http://go.microsoft.com/fwlink/?LinkId=613056)

