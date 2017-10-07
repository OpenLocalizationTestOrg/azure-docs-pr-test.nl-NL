---
title: aaaHow tootroubleshoot veelvoorkomende problemen tijdens het maken van de VHD | Microsoft Docs
description: Antwoorden toocommon probleemoplossing vragen en problemen tijdens het maken van de VHD.
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: e4ff09a979bdf575badff2d33f2299abb17c947d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-common-issues-encountered-during-vhd-creation"></a>Hoe tootroubleshoot veelvoorkomende problemen aangetroffen tijdens het maken van de VHD
Dit artikel is opgegeven toohelp een Azure Marketplace-uitgever en/of medebeheerder die mogelijk problemen ervaren of Veelgestelde vragen hebben bij het publiceren en beheren van hun oplossing(en) virtuele machine.

1. Hoe wijzig ik Hallo-naam van Hallo host?
   
    Zodra de VM is gemaakt, kunnen gebruikers Hallo-naam van Hallo host niet bijwerken.
2. Hoe Hallo tooreset extern bureaublad-service of het bijbehorende aanmeldingswachtwoord?
   
   * [Naslaginformatie voor Windows VM](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [Naslaginformatie voor virtuele Linux-machine](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. Hoe toogenerate nieuwe ssh certificaten?
   
   Raadpleeg toohello koppeling: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
4. Hoe een VPN-certificaat voor open tooconfigure?
   
   Raadpleeg toohello koppeling: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)
5. Wat is Hallo ondersteuningsbeleid voor het uitvoeren van Microsoft-serversoftware in Hallo Microsoft Azure-omgeving voor virtuele machine (infrastructure-as-a-service)?
   
   Raadpleeg toohello koppeling: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
6. Virtuele Machines is beschikt over een unieke id?
   
   Azure codeert Azure VM unieke ID in elke virtuele machine. Zie de informatie in deze documentatie en blog.
7. In een virtuele machine beheren Hallo-extensie voor aangepaste scripts in Hallo opstarttaak?
   
   Raadpleeg toohello koppeling: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)
8. Hoe toocreate een virtuele machine van Azure portal met behulp van Hallo Hallo VHD die is geüpload toopremium storage?
   
   We bieden deze functie nog geen ondersteuning.
9. Is een 32-bits app in Azure Marketplace Hallo ondersteund?
   
   Raadpleeg toohello koppeling voor meer informatie over het ondersteuningsbeleid Hallo: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
10. Telkens wanneer ik probeer toocreate een installatiekopie van een van mijn VHD's, verschijnt de fout Hallo ". VHD is al geregistreerd bij de installatiekopieopslagplaats als resource Hallo' in PowerShell. Geen afbeelding voordat ik niet hebt gemaakt, noch heeft ik een afbeelding met deze naam vinden in Azure. Hoe kan ik dit oplossen?
    
    Dit is meestal zich voordoen als Hallo gebruiker een virtuele machine uit deze VHD ingericht en er is een vergrendeling op deze VHD. Controleer of er geen virtuele machine vanuit deze VHD toegewezen is. Als Hallo fout behouden blijven, gaat u een ondersteuningsticket via deze koppeling Verhoog of van Hallo portal met betrekking tot dit publiceren (details worden gegeven in Hallo beantwoorden van vraag 11).
