---
title: aaaDeploy tooAzure Analysis Services met behulp van SSDT | Microsoft Docs
description: Meer informatie over hoe een model in tabelvorm tooan toodeploy Azure Analysis Services-server met behulp van SSDT.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>Een model implementeren vanuit SSDT
Wanneer u een server in uw Azure-abonnement hebt gemaakt, bent u klaar toodeploy een model in tabelvorm database tooit. U kunt SQL Server Data Tools (SSDT) toobuild gebruiken en implementeren van een model in tabelvorm project waarmee u werkt. 

## <a name="prerequisites"></a>Vereisten
tooget gestart, moet u de:

* **Analysis Services-server** in Azure. toolearn meer, Zie [maken van een Azure Analysis Services-server](analysis-services-create-server.md).
* **Model in tabelvorm project** in SSDT of een bestaande tabellaire model op Hallo 1200 of hoger compatibiliteitsniveau. Nog nooit zo'n project gemaakt? Probeer Hallo [Adventure Works Internet verkoop in tabelvorm modellering zelfstudie](https://msdn.microsoft.com/library/hh231691.aspx).
* **Lokale gateway** -als een of meer gegevensbronnen zich on-premises in het netwerk van uw organisatie, moet u tooinstall een [On-premises gegevensgateway](analysis-services-gateway.md). Hallo-gateway is nodig voor uw server in de cloud Hallo tooyour on-premises gegevensbronnen tooprocess en vernieuwen van gegevens in Hallo model verbinding maken.

> [!TIP]
> Zorg voordat u implementeert, dat kunt u gegevens hello in tabellen verwerken. Klik in SSDT op **Model** > **Process** > **Process All**. Als de verwerking mislukt, kunt u niet implementeren.
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>een model in tabelvorm van SSDT toodeploy

1. Voordat u implementeert, moet u de naam van de server Hallo tooget. In **Azure-portal** > server > **overzicht** > **servernaam**, kopie Hallo servernaam.
   
    ![Servernaam bepalen in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. In SSDT > **Solution Explorer**, klik met de rechtermuisknop Hallo project > **eigenschappen**. Klik dan in **implementatie** > **Server** Hallo servernaam plakken.   
   
    ![Servernaam plakken in de eigenschap Deployment Server](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. Klik in **Solution Explorer** met de rechtermuisknop op **Properties** en klik vervolgens op **Deploy**. Hebt u mogelijk na vragen aan gebruiker toosign in tooAzure.
   
    ![Tooserver implementeren](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    Status van de implementatie wordt weergegeven in beide uitvoervenster Hallo en implementeren.
   
    ![Implementatiestatus](./media/analysis-services-deploy/aas-deploy-status.png)

Dit is alles wat er is tooit!


## <a name="troubleshooting"></a>Problemen oplossen
Als de implementatie mislukt bij het implementeren van metagegevens, is het waarschijnlijk omdat SSDT kan geen verbinding tooyour-server maken. Zorg ervoor dat u kunt verbinding maken met behulp van SSMS tooyour-server. Controleer vervolgens of Hallo implementatieserver-eigenschap voor Hallo project juist is.

Als de implementatie voor een tabel mislukt, is het waarschijnlijk omdat de server kan geen verbinding tooa-gegevensbron maken. Als uw gegevensbron lokale in het netwerk van uw organisatie, moet u ervoor dat tooinstall een [On-premises gegevensgateway](analysis-services-gateway.md).

## <a name="next-steps"></a>Volgende stappen
Nu u uw model in tabelvorm geïmplementeerde tooyour server hebt, bent u klaar tooconnect tooit. U kunt [tooit verbinding met SSMS](analysis-services-manage.md) toomanage deze. En kunt u [verbinding maken met een clienthulpprogramma tooit](analysis-services-connect.md) , zoals Power BI, Power BI Desktop of Excel en start het maken van rapporten.

