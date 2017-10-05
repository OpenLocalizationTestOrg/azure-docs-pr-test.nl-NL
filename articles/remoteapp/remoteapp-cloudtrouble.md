---
title: Problemen met RemoteApp-collecties voor cloud - maken | Microsoft Docs
description: Meer informatie over het oplossen van fouten bij RemoteApp cloud verzameling maken
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>Verzamelingen van de cloud maken RemoteApp oplossen
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Als u hebt met het maken van een cloudverzameling problemen, Raadpleeg de volgende informatie.

## <a name="your-image-is-invalid"></a>Uw installatiekopie is ongeldig
Als u een bericht zoals 'GoldImageInvalid' ziet wanneer u Azure voor het inrichten van uw verzameling wacht, betekent dit dat de installatiekopie van uw sjabloon voldoet niet aan de [installatiekopie vereisten gedefinieerd](remoteapp-imagereqs.md). Ja, Ga lezen die [vereisten](remoteapp-imagereqs.md). Corrigeer de afbeelding, en probeer uw verzameling opnieuw maken.

## <a name="common-errors-seen-in-the-azure-management-portal"></a>Veelvoorkomende fouten in de Azure Management portal weergegeven.
    DNS server could not be reached
    ProvisioningTimeout

Verzamelingen vaak cloud is mislukt tijdens het maken van vanwege u gebruikmaakt van aangepaste installatiekopieën.  Als u een van de bovenstaande fouten ziet en u een aangepaste installatiekopie gebruikt om de verzameling te maken, controleert u de volgende zaken:

* Zorg ervoor dat de aangepaste installatiekopie die u hebt geüpload voldoet aan de installatiekopie.
* Meestal is het algemene probleem dat de installatiekopie niet goed syspreped is.  
* Controleer of de installatiekopie kunt opstarten in Hyper-V of proberen te maken van een IAAS VM rechtstreeks in uw Azure-abonnement met behulp van de installatiekopie. Als de virtuele machine niet kan worden opgestart en wordt niet gestart, klikt u vervolgens dit geeft meestal aan dat de aangepaste installatiekopie niet juist is voorbereid.  Controleer of de aangepaste installatiekopie is gemaakt met het volgende op de manier waarop de installatiekopie van een aangepaste sjabloon maken voor RemoteApp

Als u van een van de Microsoft-installatiekopieën die deel uitmaakt van uw abonnement gebruikmaakt, kunt u de verzameling opnieuw maken. Als het probleem zich blijft voordoen vervolgens Neem contact op met Microsoft ondersteuning.

    PlatformImageTrialModeOnly

Als u deze fout ziet dit betekent meestal dat die u naar een betaald account is bijgewerkt, maar u probeert een afbeelding van Microsoft die geldig alleen tijdens de proefmodus van de service te gebruiken. In dit geval probeert te maken van uw cloudverzameling opnieuw, maar zorg ervoor dat u de juiste installatiekopie.

