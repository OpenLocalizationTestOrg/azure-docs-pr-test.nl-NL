---
title: aaaConnect tooAzure Analysis Services met Power BI | Microsoft Docs
description: Meer informatie over hoe tooconnect tooan Azure Analysis Services-server met behulp van Power BI.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a>Verbinding maken met Power BI

Nadat u hebt een server in Azure gemaakt en geïmplementeerd een model in tabelvorm tooit, gebruikers in uw organisatie zijn gereed tooconnect en deze gegevens te verkennen. 

> [!TIP]
> Ervoor toouse Hallo meest recente versie van [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a>Verbinding maken in Power BI Desktop

1. Klik in Power BI Desktop op **gegevens ophalen** > **Azure** > **Azure Analysis Services-database**.

2. In **Server**, Voer Hallo servernaam. 
    
    Ervoor tooinclude Hallo volledige URL zijn. Bijvoorbeeld: asazure://westcentralus.asazure.windows.net/advworks.

3. In **Database**, als u de naam Hallo van Hallo model in tabelvorm database of het gewenste tooconnect hier plakken naar perspectief kent. Anders kunt u dit veld leeg laten en later een database of perspectief selecteren.

4. Laat de standaardwaarde Hallo **Connect live** optie en druk vervolgens **Connect**. 

5. Als u wordt gevraagd, voert u de aanmeldingsreferenties. 

6. In **Navigator**, vouw Hallo-server uit en selecteer vervolgens Hallo model of perspectief gewenste tooconnect aan, klikt u vervolgens op **Connect**. Klik op een model- of perspectiefparameters tooshow alle Hallo-objecten voor deze weergave.

    Hallo model wordt geopend in Power BI Desktop met een leeg rapport in de rapportweergave. Hallo veldenlijst bevat alle modelobjecten niet-verborgen. Verbindingsstatus wordt weergegeven in de rechterbenedenhoek Hallo.

## <a name="connect-in-power-bi-service"></a>Verbinding maken in Power BI (service)

1. Maak een Power BI Desktop-bestand met een live-verbinding tooyour model op uw server.
2. In [Power BI](https://powerbi.microsoft.com), klikt u op **gegevens ophalen** > **bestanden**. Zoek en selecteer het bestand.



## <a name="see-also"></a>Zie ook
[Verbinding maken met tooAzure Analysis Services](analysis-services-connect.md)   
[Clientbibliotheken](analysis-services-data-providers.md)

