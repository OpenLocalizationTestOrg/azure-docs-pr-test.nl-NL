---
title: aaaDeploy QuickBooks in Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooshare QuickBooks met Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>Hoe implementeer u QuickBooks in Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Hallo informatie tooshare QuickBooks volgen als een app in Azure RemoteApp gebruiken.

U kunt QuickBooks 2015 Enterprise delen met Azure RemoteApp in verzameling voor een hybride of de cloud. Hallo-bedrijfsbestand moet zich bevinden op een virtuele machine met QuickBooks databaseserver die is gescheiden van hello Azure RemoteApp-servers. Nooit Hallo bedrijfsbestand opslaat op uw Azure RemoteApp image - gegevens verloren gaan als u dit doet wordt verwacht. Alleen de QuickBooks Enterprise ondersteunt hosting Hallo QuickBooks bestand op een externe share met QuickBooks databaseserver toegankelijk via de standaard Windows-netwerken.   

> [!IMPORTANT]
> Hallo QuickBooks databaseserver die als host voor Hallo bedrijfsbestand fungeert moet zich bevinden op een afzonderlijke virtuele machine binnen Hallo hetzelfde VNET als hello Azure RemoteApp-verzameling.  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a>Stappen toodeploy QuickBooks
1. Maken van een virtuele machine van Azure en QuickBooks, databaseserver QuickBooks, installeren en plaats Hallo bedrijfsbestand op een virtuele machine in Azure.  Zorg ervoor dat tooproperly firewallregels configureren.
2. QuickBooks installeren op een [aangepaste installatiekopie](remoteapp-imageoptions.md) en maak een [Azure RemoteApp-verzameling](remoteapp-collections.md), cloud of hybride binnen Hallo exact hetzelfde VNET waar Hallo VM hosting Hallo QuickBooks database-server met bedrijfsbestanden zich bevindt. 
3. [Publiceren](remoteapp-publish.md) QuickBooks app toousers
4. Hallo QuickBooks gehost Azure RemoteApp-client start, navigeren met behulp van standaard Windows-toohello VM hosting Hallo QuickBooks databaseserver en Hallo bedrijfsbestand opent. 

## <a name="documentation-references"></a>Documentatie-verwijzingen
* QuickBooks [ondersteunde configuraties](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* QuickBooks [implementatieopties](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

U kunt ook controleren uit mijn presentatie Ignite [basisprincipes van Microsoft Azure RemoteApp-Management en beheer](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -vooruit too1:02:45 tooget toohello QuickBooks onderdeel.

## <a name="deployment-architecture"></a>Architectuur voor implementatie
![QuickBooks + Azure RemoteApp-implementatie](./media/remoteapp-quickbooks/ra-quickbooks.png)

