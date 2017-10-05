---
title: Migreren van Azure RemoteApp naar Citrix XenApp Essentials | Microsoft Docs
description: Het migreren van Azure RemoteApp met Citrix XenApp Essentials
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
ms.openlocfilehash: fcd96a466d1c0dad17d7012308281ef868463b19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-from-azure-remoteapp-to-citrix-xenapp-essentials"></a>Migreren van Azure RemoteApp naar Citrix XenApp Essentials

Als u Azure RemoteApp gebruiken en u wilt migreren naar Citrix XenApp Essentials, zijn er enkele vereisten rekening moet houden. Lees eerst de Citrix [technische implementatie stapsgewijze handleiding voor Citrix XenApp Essentials](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) en de bijbehorende [online technische bibliotheek](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html). 

## <a name="prerequisite-steps-for-migration"></a>Bepaalde vereiste stappen voor migratie

1. Een nieuw virtueel netwerk maken of bepalen welke Azure-netwerk in Azure Resource Manager waarin u Citrix XenApp Essentials implementeert. Azure RemoteApp maakt gebruik van de klassieke Azure portal; Citrix XenApp Essentials biedt alleen ondersteuning voor Azure Resource Manager.  
2. Zorg ervoor dat het virtuele netwerk dat u hebt geselecteerd netwerk toegang tot uw domeincontroller heeft omdat Citrix biedt alleen ondersteuning voor hybride implementaties. Als u een cloudimplementatie van Azure RemoteApp gebruikt, zorg ervoor dat het virtuele netwerk toegang tot een Active Directory-domeincontroller. U kunt ook Azure Active Directory Domain Services (Azure AD DS) gebruiken. 
3. Zorg ervoor dat de DNS-server correct is geconfigureerd voor het virtuele netwerk, zodat dit domein voltooid op de eerste poging is. U kunt maken van een virtuele machine (VM) in het virtuele netwerk dat u hebt geselecteerd, en een handmatige domein om te controleren dat de DNS- en het domein deelnemen aan werkt zoals verwacht. Dit zorgt ervoor dat u bent geslaagd de eerste keer dat u Citrix XenApp Essentials implementeert. 
4. Maak een virtueel netwerk tussen een Azure classic portal virtuele netwerk dat u gebruikt met Azure RemoteApp en uw virtuele netwerk van Azure Resource Manager-peering, indien nodig. Dit proces peering werkt als de twee netwerken bevinden zich in dezelfde regio. Als dat niet het geval is, gebruikt u site-naar-site VPN-verbinding van de virtuele netwerken voor netwerken. 
5. Indien nodig, lezen [het migreren van gegevens naar en van Azure RemoteApp](remoteapp-migrate.md). 
6. Bijwerken van uw bestaande Azure RemoteApp-installatiekopie zodanig dat het onderdeel Citrix VDA (Zie voor instructies de Citrix-documentatie). 
7. Ga naar de Azure Marketplace en Citrix XenApp Essentials implementatie begint.

## <a name="other-considerations"></a>Andere overwegingen

Wanneer u migreert, worden op de hoogte van de volgende aanvullende overwegingen:
- Citrix XenApp Essentials biedt alleen ondersteuning voor hybride implementaties. Toegang tot het netwerk naar een domeincontroller is met andere woorden, vereist om uit te voeren aan domein toevoegen. Als u van een cloudimplementatie van Azure RemoteApp gebruikmaakt, Azure AD DS gebruiken of zorg ervoor dat het virtuele netwerk toegang tot Active Directory voor het domein heeft. 
- Zie voor meer informatie over het verplaatsen van gebruikersgegevens naar Citrix XenApp Essentials, [het migreren van gegevens naar en van Azure RemoteApp](remoteapp-migrate.md). 
- Citrix XenApp Essentials biedt alleen ondersteuning voor Active Directory-accounts. Geen biedt ondersteuning voor Microsoft-accounts (zoals outlook.com, msn.com of hotmail.com). 

## <a name="citrix-xenapp-essentials-billing"></a>Citrix XenApp Essentials facturering

Zie voor volledige informatie over prijzen de [Veelgestelde vragen over](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) en [Citrix overzichtsartikel](https://www.citrix.com/global-partners/microsoft/remote-app.html). Er zijn drie facturering onderdelen met Citrix XenApp Essentials:

- De Citrix-service kosten, namelijk $12 per gebruiker per maand. Net als alle Azure Marketplace-aankopen, wordt dit in rekening gebracht op de betalingsmethode die is gekoppeld aan uw Azure-abonnement. Voor klanten met Enterprise Agreement (EA), de Azure-financieel tegoed kunnen niet worden gebruikt. 
- Externe Services (RDS) client access licenses (CAL's). Op dit moment kunt u de Remote Access-kosten die wordt meegeleverd met de betaling Citrix XenApp Essentials voor $6,25 kopen. Als u een EA-klant bent, kunt u Azure-financieel tegoed om dit te betalen. Als u uw bestaande RDS CAL's gebruiken wilt, contact met ons op [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), zodat we dit op uw factuur kunt toepassen. 
- Azure berekeningen en opslag. Dit zijn de kosten van Azure storage en compute-verbruik voor de virtuele machines gebruikt. Let bij het selecteren van de VM-grootte en de gebruiker dichtheid prijzen. Als u een EA-klant bent, kunt u Azure-financieel tegoed om dit te betalen.

Als u nog steeds vragen hebt, kunt u:
- Een e-mail sturen naar [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
- [Neem contact op met de ondersteuning van Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Start [openen van een Azure-ondersteuningsaanvraag](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) om te helpen bij de vereiste stappen 1-5. Stap 6-7 contact op met Citrix door het openen van een ondersteuningsticket binnen de Citrix-beheerportal. 
