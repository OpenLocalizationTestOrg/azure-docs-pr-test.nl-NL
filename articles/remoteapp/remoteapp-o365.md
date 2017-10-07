---
title: aaaUsing Office met Azure RemoteApp | Microsoft Docs
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
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Office gebruiken met Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Hebt u twee mogelijkheden voor het hosten van Office-toepassingen in Azure RemoteApp: Office 365 ProPlus of Office 2013 Professional Plus proefversie.

**Hey, wist u dat we hebben een nieuwe, betere artikel dat dit snel vervangen? Bekijk [hoe toouse uw Office 365-abonnement met Azure RemoteApp](remoteapp-officesubscription.md). Dekt alle Hallo info u moet voor het gebruik van Office 365 + Azure RemoteApp.**

## <a name="office-365-proplus"></a>Office 365 ProPlus
U kunt een RemoteApp-collectie met behulp van Office 365 ProPlus Hallo-sjablooninstallatiekopie maken. Deze optie kunt u tooextend uw tooRemoteApp Office 365-service. U moet een bestaand abonnement abonnement en uw gebruikers moeten bovendien een licentie voor Office 365 ProPlus-service, als zelfstandige Hallo of via Hallo Office 365-service-abonnementen.

RemoteApp biedt ondersteuning voor gedeelde computeractivering van Office 365. Als u gedeelde computeractivering inschakelen en gebruiken Hallo [Office Deployment tool](http://www.microsoft.com/download/details.aspx?id=36778) voor de installatie, Office 365 ProPlus installeren zonder wordt geactiveerd. Wanneer een gebruiker zich in een verzameling met Office 365, controleert Office toosee als Hallo gebruiker is ingericht voor Office 365 ProPlus. Als u dus Office tijdelijk Hiermee activeert u Office 365 ProPlus - persistente deze activering tot dat gebruikers zich buiten het Hallo-service.

toouse gedeelde computeractivering van Office 365, moet u toocreate een [aangepaste sjabloon](remoteapp-create-custom-image.md) en Office 365 ProPlus installeren, [deze richtingen](https://technet.microsoft.com/library/dn782858.aspx).

U kunt Office 365-licenties voor uw gebruikers op Hallo beheren [Office 365-beheerportal](https://portal.office365.com/). Meer informatie lezen over [service-abonnementen voor Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>De evaluatieversie van Office 2013 Professional Plus
Tijdens een 30-daagse evaluatieversie van RemoteApp, kunt u Hallo Office 2013 Professional Plus (evaluatieversie) sjabloon installatiekopie toocreate een RemoteApp-collectie. U kunt gebruikers toothis proefversie verzameling op basis van hun Azure Active Directory-accounts voor werk of de Microsoft-accounts toewijzen. Er is geen aanvullende abonnement is vereist.

Dit is een geweldige optie tookick Hallo-functie en een goede gevoel voor Office in RemoteApp ophalen. Deze optie is echter bedoeld voor evaluatie en testen alleen. RemoteApp-verzamelingen die zijn gemaakt met behulp van de installatiekopie van de sjabloon Hallo Office 2013 Professional Plus (evaluatieversie) kunnen niet worden overgezet tooproduction modus en aan einde van de proefperiode Hallo Hallo wordt uitgeschakeld.

## <a name="switching-from-trial-tooproduction"></a>Overschakelen van de evaluatieversie tooproduction
Wanneer u uw gratis proefabonnement van 30 dagen begint, een opmerking in RemoteApp-sectie van de portal Hallo Hallo laat u weten hoe lang u Hallo proefversie hebt verlaten voordat u tootransition tooa betaald account nodig. U kunt uw account en switch tooproduction modus via Hallo-koppeling in deze opmerking activeren.

Wanneer u uw account activeert, heeft dit invloed op alle Hallo RemoteApp-verzamelingen in uw account.

* Verzamelingen die worden uitgevoerd met Windows Server 2012 R2 Hallo of Office 365 ProPlus sjablooninstallatiekopieën Hallo overgang tooproduction naadloos. Alle gebruikersgegevens en -instellingen, inclusief actieve sessies, blijven behouden.
* Als u installatiekopieën van een aangepaste sjabloon hebt geüpload, overgang verzamelingen met behulp van deze installatiekopieën ook naadloos.
* Hallo Office 2013 Professional Plus (evaluatieversie)-sjablooninstallatiekopie is bedoeld voor alleen-evaluatie. Verzamelingen die worden uitgevoerd met de installatiekopie van deze sjabloon kunnen niet tooproduction is overgegaan. Ze worden in "uitgeschakeld" status worden geplaatst.

Als tooproduction-modus kan niet worden overgezet door Hallo vervaldatum van de proefversie, kunt u uw RemoteApp-collecties wordt uitgeschakeld. U hoeft niet - uw instellingen en gegevens van gebruikers worden opgeslagen voor een andere 90 dagen, zodat u de service en de switch tooproduction modus zonder verlies van gegevens nog steeds kunt activeren.

