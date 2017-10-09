---
title: aaaDeploy Azure API Management services-toomultiple Azure regio's | Microsoft Docs
description: Meer informatie over hoe toodeploy een Azure API Management service-exemplaar toomultiple Azure regio's.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a>Hoe toodeploy een Azure API Management service-exemplaar toomultiple Azure regio's
API Management biedt ondersteuning voor meerdere landen/regio-implementatie die Hiermee kunt API uitgevers toodistribute een enkele API management-service op een willekeurig aantal gewenste Azure-regio's. Dit vermindert de latentie waargenomen door geografisch verspreid API consumenten en verbetert tevens de servicebeschikbaarheid als één regio offline gaat. 

Wanneer u een API Management-service in eerste instantie is gemaakt, bevat deze slechts één [eenheid] [ unit] en bevindt zich op één Azure-regio, die is opgegeven als primaire regio Hallo. Extra gebieden kunnen eenvoudig worden toegevoegd via hello Azure-Portal. Een API Management gateway-server is geïmplementeerde tooeach regio en aanroep verkeer worden gerouteerd toohello dichtstbijzijnde gateway. Als een regio offline gaat, is het Hallo-verkeer automatisch opnieuw gerichte toohello volgende dichtstbijzijnde gateway. 

> [!IMPORTANT]
> Implementatie van meerdere landen/regio is alleen beschikbaar in Hallo  **[Premium] [ Premium]**  laag.
> 
> 

## <a name="add-region"></a>Implementeren van een API Management-service-exemplaar tooa nieuwe regio
> [!NOTE]
> Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.
> 
> 

Navigeer in Azure Portal Hallo toohello **schaal en prijzen** pagina voor uw API Management-service-exemplaar. 

![Tabblad schaal][api-management-scale-service]

toodeploy tooa nieuwe regio, klik op **+ toevoegen regio** Hallo werkbalk van.

![Regio toevoegen][api-management-add-region]

Selecteer Hallo locatie in de vervolgkeuzelijst Hallo en Hallo aantal eenheden voor met Hallo schuifregelaar ingesteld.

![Geef de eenheden][api-management-select-location-units]

Klik op **toevoegen** tooplace uw selectie in Hallo locaties tabel. 

Herhaal dit proces totdat u alle geconfigureerde locaties en klik op **opslaan** van Hallo werkbalk toostart Hallo-implementatieproces.

## <a name="remove-region"></a>Verwijderen van exemplaar van API Management-service van een locatie
Navigeer in Azure Portal Hallo toohello **schaal en prijzen** pagina voor uw API Management-service-exemplaar. 

![Tabblad schaal][api-management-scale-service]

Voor Hallo locatie die u wilt dat openen tooremove contextmenu Hallo Hallo met **...**  knop aan de rechterkant Hallo van Hallo tabel. Selecteer Hallo **verwijderen** optie.

![Regio verwijderen][api-management-remove-region]

Hallo bevestigen en klikt u op **opslaan** tooapply Hallo wijzigingen.

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

