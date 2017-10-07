---
title: aaaHow toomigrate van een RemoteApp VNET tooan Azure VNET | Microsoft Docs
description: Meer informatie over hoe toomigrate van een RemoteApp VNET tooan Azure VNET
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a>Hoe toomigrate een hybride verzameling van een RemoteApp VNET tooan Azure VNET
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Goed nieuws! We hebben u ingeschakeld toodeploy hybride RemoteApp-collecties rechtstreeks in uw bestaande virtuele Azure-netwerken (vnet's) in plaats van RemoteApp-specifieke VNETs maken. Hiermee kunt u profiteren van Hallo nieuwste VNET-functies (zoals ExpressRoute) en geef uw tooother hybride verzamelingen netwerk met directe toegang tot Azure-services en virtuele machines geïmplementeerd toothat VNET.  (Hiermee haalt u betere prestaties en eenvoudiger instellen dan VNET-naar-VNET-configuraties).

Stel dat u hebt al een hybride RemoteApp-collectie aangeroepen gemaakt *OriginalCollection* aangeroepen met een RemoteApp-VNET *RemoteAppVNET*. Hier volgen Hallo stappen toomigrate deze nieuwe Azure VNET aangeroepen tooa *AzureVNET*.

1. Op Hallo **netwerken** tabblad in Hallo [beheerportal](http://manage.windowsazure.com/), maak een VNET aangeroepen *AzureVNET*met dezelfde locatie, DNS-configuratie en adresruimte (voor ten minste één Hallo Hallo *AzureVNET* subnetten) als u hebt gebruikt voor *RemoteAppVNET*.
2. Configureer *AzureVNET* tooeither hosten of network connectivity toohello Active Directory-implementatie hebt die *OriginalCollection* domein lid is.
3. Op Hallo **instellen om RemoteApps** tabblad, maakt u een nieuwe RemoteApp-collectie aangeroepen *nieuwe verzameling*. (Gebruik Hallo **maken met VNET** optie niet **snelle invoer**.)
4. Configureer *NewCollection* toobe geïmplementeerd tooa subnet in *AzureVNET*.
5. Configureer *NewCollection* toouse Hallo dezelfde installatiekopie en de gegevens voor domeindeelname als u hebt gebruikt voor *OriginalCollection*.
6. Na enkele uren *NewCollection* wordt weergegeven in de verzamelingenlijst met een actieve status heeft.

Nu, als u geen toomigrate gebruikersgegevens uit Hallo oorspronkelijke verzameling toohello nieuwe verzameling, doen deze stappen:

1. Verwijder *OriginalCollection*.
2. Verwijder *RemoteAppVNET*.

En u klaar bent!

U kunt ook als u de gebruikersinformatie toomigrate uit Hallo oorspronkelijke verzameling toohello nieuwe verzameling hoeft, gaat u deze stappen naast:

1. E-mailbericht te verzenden[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) met uw Azure-abonnement-ID, naam van uw oorspronkelijke verzameling en Hallo-naam van de nieuwe verzameling Hallo en vraag deze toomigrate uw gebruikersgegevens.
2. Binnen 2 dagen worden Hallo RemoteApp-team Hallo toegang gebruikerslijst alle gebruikersdocumenten en gebruikersinstellingen verplaatst van Hallo oorspronkelijke verzameling toohello nieuwe verzameling.
3. Verwijder *OriginalCollection*.
4. Verwijder *RemoteAppVNET*.

En u bent nu klaar!

Als u vragen hebt of speciale hulp nodig hebt, kunt u een e-mail [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

