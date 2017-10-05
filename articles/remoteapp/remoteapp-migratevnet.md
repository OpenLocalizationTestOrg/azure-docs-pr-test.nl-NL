---
title: Het migreren van een RemoteApp VNET een Azure vnet | Microsoft Docs
description: Meer informatie over het migreren van een RemoteApp VNET naar een Azure-VNET
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
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a>Een hybride verzameling van een RemoteApp-VNET migreren naar een Azure-VNET
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Goed nieuws! We hebben u hybride RemoteApp-verzamelingen rechtstreeks in uw bestaande virtuele Azure-netwerken (vnet's) in plaats van het maken van RemoteApp-specifieke VNETs implementeren ingeschakeld. Hiermee kunt u profiteren van de nieuwste functies van VNET (zoals ExpressRoute) en uw hybride verzamelingen met directe netwerktoegang geven tot andere Azure-services en virtuele machines die aan dit VNET zijn geïmplementeerd.  (Hiermee haalt u betere prestaties en eenvoudiger instellen dan VNET-naar-VNET-configuraties).

Stel dat u hebt al een hybride RemoteApp-collectie aangeroepen gemaakt *OriginalCollection* aangeroepen met een RemoteApp-VNET *RemoteAppVNET*. Hier volgen de stappen voor het migreren naar een nieuwe Azure VNET aangeroepen *AzureVNET*.

1. Op de **netwerken** tabblad de [beheerportal](http://manage.windowsazure.com/), maak een VNET aangeroepen *AzureVNET*, met behulp van de dezelfde locatie, de DNS-configuratie en -adresruimte (voor ten minste één van de *AzureVNET* subnetten) als u hebt gebruikt voor *RemoteAppVNET*.
2. Configureer *AzureVNET* hosten of netwerkverbinding met de Active Directory-implementatie hebt die *OriginalCollection* domein wordt gekoppeld aan.
3. Op de **instellen om RemoteApps** tabblad, maakt u een nieuwe RemoteApp-collectie aangeroepen *nieuwe verzameling*. (Gebruik de **maken met VNET** optie niet **snelle invoer**.)
4. Configureer *NewCollection* worden geïmplementeerd voor een subnet in *AzureVNET*.
5. Configureer *NewCollection* de dezelfde installatiekopie en de gegevens voor domeindeelname te gebruiken als u hebt gebruikt voor *OriginalCollection*.
6. Na enkele uren *NewCollection* wordt weergegeven in de verzamelingenlijst met een actieve status heeft.

Nu, als u hoeft niet te migreren van gebruikersgegevens uit de oorspronkelijke verzameling naar de nieuwe verzameling, gaat u als volgt vervolgens:

1. Verwijder *OriginalCollection*.
2. Verwijder *RemoteAppVNET*.

En u klaar bent!

Ook als u migreren van gebruikersgegevens uit de oorspronkelijke verzameling naar de nieuwe verzameling wilt, gaat u als volgt naast:

1. Een e-mail sturen naar [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) met uw Azure-abonnement-ID, de naam van uw oorspronkelijke verzameling en de naam van de nieuwe verzameling en vraag om uw gebruikersgegevens te migreren.
2. Binnen 2 dagen verplaatst de RemoteApp-team de lijst met gebruikers toegang tot alle gebruikersdocumenten en gebruikersinstellingen uit de oorspronkelijke verzameling naar de nieuwe verzameling.
3. Verwijder *OriginalCollection*.
4. Verwijder *RemoteAppVNET*.

En u bent nu klaar!

Als u vragen hebt of speciale hulp nodig hebt, kunt u een e-mail [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

