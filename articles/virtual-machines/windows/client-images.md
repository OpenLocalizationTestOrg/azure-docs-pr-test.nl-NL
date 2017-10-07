---
title: "aaaUse Windows client-installatiekopieën in Azure | Microsoft Docs"
description: Hoe toouse Visual Studio-abonnement voordelen biedt voor toodeploy Windows 7, Windows 8 of Windows 10 in Azure voor scenario's ontwikkelen en testen
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>Windows-client in Azure gebruiken voor scenario's ontwikkelen en testen
U kunt Windows 7, Windows 8 of Windows 10 in Azure voor ontwikkel-/ Testscenario's geleverde dat een juiste Visual Studio (voorheen MSDN)-abonnement hebt. In dit artikel bevat een overzicht van Hallo in aanmerking komt vereisten voor het uitvoeren van Windows-client in Azure en het gebruik van Hallo galerie van Azure-installatiekopieën.

## <a name="subscription-eligibility"></a>Abonnement welke in aanmerking komen
Actieve Visual Studio-abonnees (personen die een licentie Visual Studio-abonnement hebt aangeschaft) kunnen u Windows-client gebruiken voor ontwikkeling en voor testdoeleinden. Windows-client kan worden gebruikt op uw eigen hardware- en Azure virtuele machines die worden uitgevoerd in elk type Azure-abonnement. Windows-client mogelijk geen geïmplementeerde tooor gebruikt in Azure voor gebruik in productieomgevingen normale of gebruikt door personen die geen actieve Visual Studio-abonnees.

Voor uw gemak we hebben aangebracht bepaalde Windows 10-installatiekopieën beschikbaar vanuit de Azure-galerie Hallo binnen [in aanmerking komende ontwikkelen en testen biedt](#eligible-offers). Visual Studio-abonnees binnen elk type aanbieding kunnen ook [voldoende voorbereiden en maken](prepare-for-upload-vhd-image.md) een 64-bits installatiekopie voor Windows 7, Windows 8 of Windows 10 en vervolgens [tooAzure uploaden](upload-generalized-managed.md). Hallo gebruik blijft beperkt toodev en testen door actieve Visual Studio-abonnees.

## <a name="eligible-offers"></a>In aanmerking komende aanbiedingen
na de tabel details Hallo Hallo bieden-id's in aanmerking komende toodeploy Windows 10 via Hallo galerie van Azure. Hallo Windows 10-installatiekopieën zijn alleen zichtbaar toohello aanbiedingen te volgen. Visual Studio-abonnees die moet toorun Windows-client in een andere aanbiedingtype hoeft te[voldoende voorbereiden en maken](prepare-for-upload-vhd-image.md) een 64-bits installatiekopie voor Windows 7, Windows 8 of Windows 10 en [vervolgens uploaden tooAzure](upload-generalized-managed.md).

| Naam van aanbieding: | Nummer van de aanbieding | Beschikbare client-installatiekopieën |
|:--- |:---:|:---:|
| [Betalen naar gebruik ontwikkelen en testen](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Abonnees van Visual Studio Enterprise (MPN)](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Visual Studio Professional-abonnees](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Visual Studio Test Professional-abonnees](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium met MSDN (voordeel)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Abonnees van Visual Studio Enterprise](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Abonnees van Visual Studio Enterprise (BizSpark)](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Enterprise ontwikkelen en testen](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Controleer uw Azure-abonnement
Als u uw aanbieding-ID niet weet, kunt u deze kunt verkrijgen via hello Azure-portal op een van deze twee manieren:  

- Op Hallo 'Abonnementen' blade:

  ![Details van de ID van de aanbieding van hello Azure-portal](./media/client-images/offer-id-azure-portal.png) 

- Of klik op **facturering** en klik vervolgens op uw abonnement-ID. Hallo aanbieding-ID wordt weergegeven in de blade facturering Hallo.

U kunt ook weergeven Hallo aanbieding-ID van Hallo [tabblad 'Abonnementen'](http://account.windowsazure.com/Subscriptions) van Hallo-Account Azure-portal:

![Details van de ID van de aanbieding van hello Azure-Account-portal](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>Volgende stappen
U kunt nu uw virtuele machines met implementeren [PowerShell](quick-create-powershell.md), [Resource Manager-sjablonen](ps-template.md), of [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

