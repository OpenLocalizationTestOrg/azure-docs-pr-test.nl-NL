---
title: aaaCreate een Analysis Services-server in Azure | Microsoft Docs
description: Meer informatie over hoe toocreate een Analysis Services-server-instantie in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>Een Azure Analysis Services-server maken in Azure portal
Dit artikel begeleidt u bij het maken van een resource van Analysis Services-server in uw Azure-abonnement.

## <a name="before-you-begin"></a>Voordat u begint
toocomplete deze snelstartgids die u nodig:

* **Azure-abonnement**: Ga naar [gratis proefversie van Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate een account.
* **Azure Active Directory**: uw abonnement moet worden gekoppeld aan een Azure Active Directory-tenant. En moet u toobe tooAzure aangemeld met een account in dat Azure Active Directory. Microsoft-accounts worden niet ondersteund. toolearn meer, Zie [verificatie en gebruikersmachtigingen](analysis-services-manage-users.md).
* **Resourcegroep**: een resourcegroep die u al hebt gebruikt of [Maak een nieuwe](../azure-resource-manager/resource-group-overview.md).

> [!NOTE]
> Het maken van een server kan zorgen voor een nieuwe factureerbare service. toolearn meer, Zie [Analysis Services-prijzen](https://azure.microsoft.com/pricing/details/analysis-services/).
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>toocreate een server in Azure-portal
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).  
2. Klik op **+ nieuw** > **gegevens en analyse** > **Analysis Services**.
3. In Hallo **Analysis Services** blade Vul Hallo vereiste velden in en druk vervolgens op **maken**.
   
    ![Server maken](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **Servernaam**: Typ een unieke naam gebruikt tooreference Hallo-server.
   * **Abonnement**: Hallo abonnement deze server te stuklijsten selecteren.
   * **Resourcegroep**: deze containers worden ontworpen toohelp u een verzameling Azure-resources beheren. toolearn meer, Zie [resourcegroepen](../azure-resource-manager/resource-group-overview.md).
   * **Locatie**: deze Azure datacenter locatie hosts Hallo server. Kies een locatie dichtstbijzijnde uw grootste gebruikersgroep.
   * **Prijscategorie**: een prijscategorie selecteren. Modellen in tabelvorm up too400 GB worden ondersteund. toolearn meer, Zie [Azure Analysis Services-prijzen](https://azure.microsoft.com/pricing/details/analysis-services/).
4. Klik op **Create**.

Maak gewoonlijk duurt minder dan een minuut; vaak slechts enkele seconden. Als u hebt geselecteerd **tooPortal toevoegen**, navigeer tooyour portal toosee uw nieuwe server. Of Ga te**meer services** > **Analysis Services** toosee als de server klaar is.

 ![Dashboard](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>Volgende stappen
Nadat u uw server hebt gemaakt, kunt u [implementeert een model](analysis-services-deploy.md) tooit met behulp van SSDT of met SSMS.

Als een model u tooyour-server implementeren verbinding tooon-premises gegevensbronnen, moet u tooinstall een [On-premises gegevensgateway](analysis-services-gateway.md) op een computer in uw netwerk.

