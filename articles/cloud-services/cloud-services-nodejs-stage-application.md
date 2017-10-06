---
title: aaaStage een cloud service-implementatie (Node.js) | Microsoft Docs
description: Meer informatie over hoe toodeploy uw Azure-toepassing tooa staging-omgeving, implementeert u tooa productie-omgeving met virtuele IP-adres (VIP) voor wisselen.
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d65d26a6-b424-49cd-a88c-7ef46bb112a8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 0656c84ac444a10f152f441265f85141347bf1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="staging-an-application-in-azure"></a>Gefaseerde installatie van een toepassing in Azure
Een verpakte toepassing kan worden geïmplementeerd toohello staging-omgeving in Azure toobe getest voordat u deze toohello productie verplaatst in welke Hallo toepassing toegankelijk via Internet Hallo is omgeving. De testomgeving is precies zoals Hallo-productieomgeving, behalve dat u kunt alleen toegang Hallo gefaseerde toepassing met een verborgen-URL die wordt gegenereerd door Azure. Nadat u hebt gecontroleerd of uw toepassing correct werkt, kunt het geïmplementeerde toohello productie-omgeving zijn door het uitvoeren van een virtueel IP-adres (VIP) voor wisselen.

> [!NOTE]
> Hallo stappen in dit artikel zijn alleen van toepassing toonode toepassingen die worden gehost als een Azure Cloud Service.
> 
> 

## <a name="step-1-stage-an-application"></a>Stap 1: Voorbereiden van een toepassing
Deze taak bevat informatie over hoe een toepassing met behulp van toostage Hallo **Microsoft Azure PowerShell**.

1. Bij het publiceren van een service gewoon Hallo doorgeven **-sleuf** parameter op Hallo van **Publish-AzureServiceProject** cmdlet.
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. Meld u aan toohello [klassieke Azure-portal] en selecteer **Cloudservices**. Na het Hallo-cloudservice wordt gemaakt en Hallo **fasering** kolom status is bijgewerkt te**met**, klikt u op Hallo servicenaam.
   
   ![weergeven van een actieve service portal][cloud-service]
3. Selecteer Hallo **Dashboard**, en selecteer vervolgens **fasering**.
   
   ![cloud service-dashboard][cloud-service-dashboard]
4. Houd er rekening mee Hallo-waarde in Hallo **Site-URL** vermelding toohello rechts. Hallo DNS-naam is een verborgen interne ID die Azure gegenereerd.
   
    ![site-url][cloud-service-staging-url]

U kunt nu controleren Hallo toepassing correct werkt in Hallo staging-omgeving met behulp van Hallo staging-site-URL.

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>Stap 2: Een toepassing in productie door wisselen VIP's bijwerken
Nadat u de bijgewerkte versie Hallo van een toepassing in de testomgeving hebt gecontroleerd, kunt u snel maken het beschikbaar in productie door wisselen Hallo virtuele IP-adressen (VIP's) van Hallo fasering en productie-omgevingen.

> [!NOTE]
> Deze stap wordt ervan uitgegaan dat u hebt al een toepassing tooproduction geïmplementeerd en voorbereid Hallo bijgewerkte versie van de toepassing.
> 
> 

1. Meld u aan bij Hallo [klassieke Azure-portal], klikt u op **Cloudservices** en selecteer vervolgens de naam van de service Hallo.
2. Van Hallo **Dashboard**, selecteer **fasering**, en klik vervolgens op **wisselen** Hallo Hallo pagina onderaan in. Hallo VIP's wisselen dialoogvenster wordt geopend.
   
   ![VIP wisselen dialoogvenster][vip-swap-dialog]
3. Hallo-informatie bekijken en klik vervolgens op **OK**. Hallo twee implementaties beginnen met het bijwerken als Hallo implementatie switches tooproduction en Hallo productie-implementatie switches toostaging voor fasering.

U hebt voorbereid, een implementatie en een productie-implementatie door VIP's wisselen met Hallo-implementatie in fasering bijgewerkt.

## <a name="additional-resources"></a>Aanvullende resources
* [Hoe tooDeploy een tooProduction Service bijwerken door VIP's wisselen in Azure]

[klassieke Azure-portal]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[Hoe tooDeploy een tooProduction Service bijwerken door VIP's wisselen in Azure]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
