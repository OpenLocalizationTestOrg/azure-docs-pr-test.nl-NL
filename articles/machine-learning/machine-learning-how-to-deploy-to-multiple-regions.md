---
title: aaaHow toodeploy een webservice toomultiple regio's | Microsoft Docs
description: "Stappen toodeploy (kopiëren) een nieuwe webservice tooother regio's."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a>Hoe een webservice toodeploy toomultiple regio's
Hallo nieuwe Azure Web Services kunt u tooeasily een web service toomultiple regio's implementeren zonder meerdere abonnementen of werkruimten. 

Prijzen is regio specifiek, dat daarom moet u een abonnement voor elke regio waarin u Hallo webservice implementeren.

## <a name="toocreate-a-plan-in-another-region"></a>toocreate een plan in een andere regio
1. Meld u aan bij [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/).
2. Klik op Hallo **plannen** menuoptie.
3. Op Hallo plannen via de pagina weergeven, klikt u op **nieuw**.
4. Van Hallo **abonnement** vervolgkeuzelijst, selecteer Hallo-abonnement in welke Hallo nieuw plan moet worden gebruikt.
5. Van Hallo **regio** vervolgkeuzelijst, selecteer een regio voor nieuwe Hallo-abonnement. Hallo opties plannen voor de geselecteerde regio hello wordt weergegeven in Hallo **opties plannen** sectie van Hallo pagina.
6. Van Hallo **resourcegroep** vervolgkeuzelijst, selecteer een resourcegroep voor Hallo plan. Zie voor meer informatie over resourcegroepen [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
7. In **naam** Hallo typenaam van Hallo plan.
8. Onder **Plan opties**, klikt u op de facturering niveau Hallo voor nieuwe Hallo-abonnement.
9. Klik op **Create**.

## <a name="deploying-hello-web-service-tooanother-region"></a>Hallo web service tooanother regio implementeren
1. Klik op Hallo **webservices** menuoptie.
2. Selecteer Hallo webservice u tooa nieuwe regio implementeert.
3. Klik op **kopie**.
4. In **Webservicenaam**, typt u een nieuwe naam voor het Hallo-webservice.
5. In **Web servicebeschrijving**, typ een beschrijving voor het Hallo-webservice.
6. Van Hallo **abonnement** vervolgkeuzelijst, selecteer Hallo-abonnement in welke Hallo nieuwe webservice moet worden gebruikt.
7. Van Hallo **resourcegroep** vervolgkeuzelijst, selecteer een resourcegroep voor Hallo-webservice. Zie voor meer informatie over resourcegroepen [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. Van Hallo **regio** vervolgkeuzelijst, selecteer Hallo regio in welke toodeploy Hallo-webservice.
9. Van Hallo **opslagaccount** vervolgkeuzelijst, selecteer een opslagaccount in welke toostore Hallo-webservice.
10. Van Hallo **prijs Plan** dropdown, selecteert u een plan in Hallo regio die u hebt geselecteerd in stap 8.
11. Klik op **kopie**.

