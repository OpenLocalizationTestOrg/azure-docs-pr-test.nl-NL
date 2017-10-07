---
title: aaaMigrate van Azure RemoteApp tooCitrix XenApp Essentials | Microsoft Docs
description: Hoe toomigrate van Azure RemoteApp tooCitrix XenApp Essentials
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>Migreren van Azure RemoteApp tooCitrix XenApp Essentials

Als u Azure RemoteApp gebruiken en u toomigrate tooCitrix XenApp Essentials wilt, zijn er enkele vereisten tookeep in gedachten. Lees eerst de Citrix [technische implementatie stapsgewijze handleiding voor Citrix XenApp Essentials](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) en de bijbehorende [online technische bibliotheek](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html). 

## <a name="prerequisite-steps-for-migration"></a>Bepaalde vereiste stappen voor migratie

1. Een nieuw virtueel netwerk maken of bepalen welke Azure-netwerk in Azure Resource Manager waarin u Citrix XenApp Essentials implementeert. Hallo klassieke Azure-portal; maakt gebruik van Azure RemoteApp Citrix XenApp Essentials biedt alleen ondersteuning voor Azure Resource Manager.  
2. Zorg ervoor dat Hallo virtuele netwerk die u hebt geselecteerd netwerken toegang tooyour domeincontroller, omdat de Citrix biedt alleen ondersteuning voor hybride implementaties. Als u een cloudimplementatie van Azure RemoteApp gebruikt, zorg ervoor dat het virtuele netwerk netwerken toegang tooan Active Directory-domeincontroller. U kunt ook Azure Active Directory Domain Services (Azure AD DS) gebruiken. 
3. Zorg ervoor dat Hallo die DNS juist is geconfigureerd voor het virtuele netwerk hello, zodat dit domein voltooid op de eerste poging is. U kunt maken van een virtuele machine (VM) in Hallo virtueel netwerk die u hebt geselecteerd en voer een handmatige domain join tooverify die Hallo DNS en domein werkt zoals verwacht. Dit zorgt ervoor dat u geslaagde Hallo eerst die u Citrix XenApp Essentials implementeert. 
4. Maak een virtueel netwerk tussen een Azure classic portal virtuele netwerk dat u gebruikt met Azure RemoteApp en uw virtuele netwerk van Azure Resource Manager-peering, indien nodig. Dit proces peering werkt als Hallo twee netwerken bevinden zich in Hallo dezelfde regio. Als dat niet het geval is, gebruikt u de site-naar-site VPN-tooconnect Hallo virtuele netwerken voor netwerken. 
5. Indien nodig, lezen [hoe toomigrate gegevens naar en van Azure RemoteApp](remoteapp-migrate.md). 
6. Bijwerken van uw bestaande Azure RemoteApp image tooinclude-Hallo Citrix VDA onderdeel (Zie voor instructies Hallo Citrix documentatie). 
7. Ga toohello Azure Marketplace en Citrix XenApp Essentials implementatie begint.

## <a name="other-considerations"></a>Andere overwegingen

Zich bewust zijn van de volgende aanvullende overwegingen wanneer u migreert Hallo:
- Citrix XenApp Essentials biedt alleen ondersteuning voor hybride implementaties. Met andere woorden, vereist het netwerk toegang tooa-domeincontroller in volgorde tooperform domein. Als u van een cloudimplementatie van Azure RemoteApp gebruikmaakt, Azure AD DS gebruiken of zorg ervoor dat het virtuele netwerk toegang tooActive Directory voor het domein. 
- hoe toomove gebruiker gegevens tooCitrix XenApp Essentials, Zie toolearn [hoe toomigrate gegevens naar en van Azure RemoteApp](remoteapp-migrate.md). 
- Citrix XenApp Essentials biedt alleen ondersteuning voor Active Directory-accounts. Geen biedt ondersteuning voor Microsoft-accounts (zoals outlook.com, msn.com of hotmail.com). 

## <a name="citrix-xenapp-essentials-billing"></a>Citrix XenApp Essentials facturering

Zie voor volledige informatie over prijzen Hallo [Veelgestelde vragen over](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) en [Citrix overzichtsartikel](https://www.citrix.com/global-partners/microsoft/remote-app.html). Er zijn drie facturering onderdelen tooCitrix XenApp Essentials:

- Hallo Citrix servicekosten $ 12 per gebruiker per maand. Net als alle Azure Marketplace-aankopen is dit gefactureerd toohello betalingsmethode die is gekoppeld aan uw Azure-abonnement. Voor klanten met Enterprise Agreement (EA), de Azure-financieel tegoed kunnen niet worden gebruikt. 
- Externe Services (RDS) client access licenses (CAL's). Op dit moment kunt u Hallo Remote Access-kosten die wordt meegeleverd met Hallo Citrix XenApp Essentials betaling voor $6,25 kopen. Als u een EA-klant bent, kunt u toopay Azure financieel tegoed voor dit. Als u uw bestaande RDS CAL's toouse wilt, contact met ons op [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), zodat we deze factuur tooyour kunt toepassen. 
- Azure berekeningen en opslag. Dit is hello Azure opslagkosten en compute-verbruik voor virtuele machines Hallo verbruikt. Let bij het selecteren van de VM-grootte en de gebruiker dichtheid prijzen. Als u een EA-klant bent, kunt u toopay Azure financieel tegoed voor dit.

Als u nog steeds vragen hebt, kunt u:
- Een e-mail sturen naar [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
- [Neem contact op met de ondersteuning van Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Start [openen van een Azure-ondersteuningsaanvraag](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toohelp met de vereiste stappen 1-5. Stap 6-7 contact op met Citrix door het openen van een ondersteuningsticket binnen Hallo Citrix-beheerportal. 
