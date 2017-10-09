---
title: 'aaaTroubleshoot RemoteApp cloudverzamelingen: maken | Microsoft Docs'
description: Meer informatie over hoe tootroubleshoot RemoteApp cloud fouten bij het maken van de verzameling
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
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>Verzamelingen van de cloud maken RemoteApp oplossen
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Als u hebt met het maken van een cloudverzameling problemen, Raadpleeg Hallo informatie te volgen.

## <a name="your-image-is-invalid"></a>Uw installatiekopie is ongeldig
Als u een bericht zoals 'GoldImageInvalid' ziet wanneer u Azure tooprovision uw verzameling wacht, betekent dit dat de installatiekopie van uw sjabloon Hallo voldoet niet aan [installatiekopie vereisten gedefinieerd](remoteapp-imagereqs.md). Ja, Ga lezen die [vereisten](remoteapp-imagereqs.md). Corrigeer de afbeelding, en probeer toocreate uw verzameling opnieuw.

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>Veelvoorkomende fouten in hello Azure Management portal weergegeven.
    DNS server could not be reached
    ProvisioningTimeout

Verzamelingen vaak cloud is mislukt tijdens het maken van vanwege u gebruikmaakt van aangepaste installatiekopieën.  Als u een Hallo hierboven fouten ziet en u een aangepaste installatiekopie toocreate Hallo verzameling gebruikt, controleert u Hallo dingen te volgen:

* Zorg ervoor dat Hallo aangepaste installatiekopie die u hebt geüpload voldoet aan de installatiekopie.
* Meest voorkomende Hallo probleem is dat die Hallo-installatiekopie is niet goed syspreped.  
* Controleer of Hallo installatiekopie kunt opstarten in Hyper-V of proberen te maken van een IAAS VM rechtstreeks in uw Azure-abonnement met Hallo-installatiekopie. Als Hallo VM tooboot en niet starten mislukt, klikt u vervolgens duidt dit meestal dat die Hallo aangepaste installatiekopie is niet correct voorbereid.  Controleer of de aangepaste installatiekopie Hallo is opgebouwd na Hallo hoe toocreate een aangepaste sjablooninstallatiekopie voor RemoteApp

Als u van een van Hallo Microsoft installatiekopieën zijn opgenomen in uw abonnement gebruikmaakt, probeert u opnieuw toocreate Hallo-verzameling. Als Hallo probleem zich blijft voordoen vervolgens Neem contact op met Microsoft ondersteuning.

    PlatformImageTrialModeOnly

Als u deze fout ziet dit betekent meestal dat u bijgewerkt tooa betaald account en u probeert een installatiekopie van Microsoft die geldig is tijdens de proefmodus van Hallo service Hallo toouse. In dit geval probeert toocreate uw cloudverzameling opnieuw worden echter zeker toospecify Hallo juiste installatiekopie.

