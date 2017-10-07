---
title: aaaUsing Outlook in Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooconfigure en Outlook gebruiken in Azure RemoteApp | Microsoft Azure
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a>Microsoft Outlook gebruiken in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp biedt ondersteuning voor Microsoft Outlook O365. Lees meer over hoe [Office werkt in Azure RemoteApp](remoteapp-officesubscription.md). Er zijn enkele aanbevolen instellingen voor Outlook bij gebruik in Azure RemoteApp.

## <a name="cached-mode"></a>Cachemodus
Cachemodus is een aanbevolen configuratie wanneer u Outlook gebruikt in Azure RemoteApp. Bij het configureren van een account Outlook 2013 toouse werkt Exchange-modus met cache Outlook 2013 vanuit een lokaal exemplaar van Microsoft Exchange-postvak voor Hallo van de gebruiker die is opgeslagen in een Offlinegegevensbestand (OST-bestand) op de computer van de gebruiker hello, samen met de Hallo offlineadresboek (OAB). in de cache Postvak Hallo en het OAB worden regelmatig bijgewerkt vanuit Hallo O365-service. Lees meer over [verschillen tussen de cachemodus en onlinemodus Hallo](https://technet.microsoft.com/library/jj683103.aspx).

Hallo-gebruiker kunt selecteren **Exchange-modus met cache** of **onlinemodus** tijdens de accountconfiguratie of door Hallo accountinstellingen te wijzigen. U kunt ook een modus of andere Hallo implementeren met behulp van Hallo Office Customization Tool (OCT) of Groepsbeleid.  

Lees [Stapsgewijze instructies over het inschakelen van de cachemodus](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).

## <a name="search"></a>Zoeken
In Azure RemoteApp heeft het zoeken in Outlook beperkingen. Azure RemoteApp maakt gebruik van gegroepeerde virtuele machines tooaccommodate-gebruikerssessies. Zoekindexering is afhankelijk van Hallo machine-id. deze voor verschillende virtuele machines verschilt. Het is mogelijk dat elke keer dat een gebruiker zich aanmeldt bij Azure RemoteApp, ze gerichte tooa zijn nieuwe virtuele machine. Dit betekent dat, als lokaal zoeken, Hallo indexeerfunctie worden uitgevoerd telkens wanneer Hallo machine ID verandert (wanneer Hallo gebruiker zich op een andere virtuele machine). Afhankelijk van de grootte van de Hallo Hallo. OST-bestand Hallo indexeerfunctie kan een toocomplete lang duren en gebruik van bronnen die nodig zijn voor andere apps. Zoeken zou niet alleen traag zijn maar zou misschien geen resultaten opleveren. Met behulp van een accountprofiel onlinemodus zou dit probleem omzeilen, maar zouden de algehele prestaties afnemen vanwege toohello gebrek aan een lokale cache (Zie Hallo hierboven voor meer informatie over het verschil tussen de cachemodus en onlinemodus Hallo koppelen). Geïndexeerd/lokaal zoeken kan echter niet worden uitgeschakeld en online zoeken kan in Outlook 2013 helaas niet standaard worden ingeschakeld.

