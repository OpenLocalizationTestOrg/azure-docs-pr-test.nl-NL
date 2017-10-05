---
title: Office gebruiken met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe Office en Azure RemoteApp samenwerken
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a776d877c764109f15c1025db2be3114eea2130a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Office gebruiken met Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Hebt u twee mogelijkheden voor het hosten van Office-toepassingen in Azure RemoteApp: Office 365 ProPlus of Office 2013 Professional Plus proefversie.

**Hey, wist u dat we hebben een nieuwe, betere artikel dat dit snel vervangen? Bekijk [het gebruik van uw Office 365-abonnement met Azure RemoteApp](remoteapp-officesubscription.md). Deze heeft alle informatie die u nodig voor het gebruik van Office 365 + Azure RemoteApp.**

## <a name="office-365-proplus"></a>Office 365 ProPlus
U kunt een RemoteApp-collectie met behulp van de Office 365 ProPlus-sjablooninstallatiekopie maken. Deze optie kunt u uw Office 365-service kunt uitbreiden met RemoteApp. U moet een bestaand abonnement-abonnement hebben en uw gebruikers moeten voor de Office 365 ProPlus-service, als zelfstandig product een licentie hebben of service via de Office 365-abonnementen.

RemoteApp biedt ondersteuning voor gedeelde computeractivering van Office 365. Als u gedeelde computeractivering inschakelen en gebruiken de [Office Deployment tool](http://www.microsoft.com/download/details.aspx?id=36778) voor de installatie, Office 365 ProPlus installeren zonder wordt geactiveerd. Wanneer een gebruiker zich in een verzameling met Office 365, Office gecontroleerd als de gebruiker is ingericht voor Office 365 ProPlus. Als u dus Office tijdelijk Hiermee activeert u Office 365 ProPlus - persistente deze activering tot dat gebruikers zich buiten de service.

Om de activering van Office 365 gedeelde Computer gebruikt, moet u maken een [aangepaste sjabloon](remoteapp-create-custom-image.md) en Office 365 ProPlus installeren, [deze richtingen](https://technet.microsoft.com/library/dn782858.aspx).

U kunt Office 365-licenties aan uw gebruikers beheren de [Office 365-beheerportal](https://portal.office365.com/). Meer informatie lezen over [service-abonnementen voor Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>De evaluatieversie van Office 2013 Professional Plus
Tijdens een 30-daagse evaluatieversie van RemoteApp, kunt u de installatiekopie van Office 2013 Professional Plus (evaluatieversie) sjabloon om een RemoteApp-verzameling te maken. U kunt gebruikers toewijzen aan deze proefversie verzameling op basis van hun Azure Active Directory-accounts voor werk of de Microsoft-accounts. Er is geen aanvullende abonnement is vereist.

Dit is een geweldige optie voor het starten van de functie en een goede gevoel voor Office in RemoteApp ophalen. Deze optie is echter bedoeld voor evaluatie en testen alleen. RemoteApp-verzamelingen die zijn gemaakt met behulp van de installatiekopie van Office 2013 Professional Plus (evaluatieversie) sjabloon kunnen niet worden overgezet naar de productiemodus en aan het einde van de proefperiode wordt uitgeschakeld.

## <a name="switching-from-trial-to-production"></a>Overschakelen van de evaluatieversie naar productie
Wanneer u uw gratis proefabonnement van 30 dagen begint, ziet een opmerking in de RemoteApp-sectie van de portal u hoe lang u de proefversie hebt verlaten voordat u de overgang naar een betaald account wilt. U kunt uw account activeren en overschakelen naar de productiemodus op de koppeling in deze opmerking.

Wanneer u uw account activeert, heeft dit invloed op alle RemoteApp-verzamelingen in uw account.

* Verzamelingen die worden uitgevoerd met Windows Server 2012 R2 of Office 365 ProPlus sjablooninstallatiekopieën wordt naadloos overgang naar productie. Alle gebruikersgegevens en -instellingen, inclusief actieve sessies, blijven behouden.
* Als u installatiekopieën van een aangepaste sjabloon hebt geüpload, overgang verzamelingen met behulp van deze installatiekopieën ook naadloos.
* De sjablooninstallatiekopie van Office 2013 Professional Plus (evaluatieversie) is bedoeld voor alleen-evaluatie. Verzamelingen die worden uitgevoerd met de installatiekopie van deze sjabloon kunnen niet worden overgegaan naar productie. Ze worden in "uitgeschakeld" status worden geplaatst.

Als u bent niet worden overgezet naar productiemodus door de vervaldatum van de proefversie, kunt u uw RemoteApp-collecties wordt uitgeschakeld. U hoeft niet - uw instellingen en gegevens van gebruikers worden opgeslagen voor een andere 90 dagen, zodat u kunt nog steeds activeren van uw service en naar de productiemodus zonder dat er gegevens verloren overschakelen.

