---
title: aaaLogic Apps B2B edifact decoderen oplossen UNH2.5 - Azure Logic Apps | Microsoft Docs
description: Azure Logic Apps B2B edifact decoderen oplossen UNH2.5
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a>Hoe toohandle EDIFACT documenten met UNH2.5 segment
Wanneer UNH2.5 op Hallo EDIFACT document aanwezig is, wordt deze gebruikt voor het opzoeken van het schema. 

Voorbeeld: Hallo UNH veld is **EAN008** in EDIFACT het Hallo-bericht  
UNH + SSDD1 + ORDERS: D: 03B: ONGEDAAN MAKEN:**EAN008**'  

Stappen toofollow toohandle Hallo-bericht 
1. Hallo-schema bijwerken
2. Controleer de instellingen van de overeenkomst Hallo  

## <a name="update-hello-schema"></a>Hallo-schema bijwerken
tooprocess het Hallo-bericht, moet u een schema met de naam hoofdknooppunt Hallo UNH2.5 toodeploy.  Voor een voorbeeld gegeven, hoofdnaam Hallo-schema zou worden **EFACT_D03B_ORDERS_EAN008**  

Voor elke D03B_ORDERS met een andere UNH2.5 segment hebt u toodeploy een afzonderlijk schema.  

## <a name="add-schema-toohello-edifact-agreement"></a>Schema toohello EDIFACT overeenkomst toevoegen
### <a name="edifact-decode"></a>EDIFACT decoderen
tooDecode Hallo binnenkomend bericht, Hallo schema configureren in Hallo EDIFACT ontvangen overeenkomst instellingen
1. Hallo schema toohello integratie account toevoegen    
2. Hallo-schema configureren in Hallo EDIFACT ontvangen overeenkomst instellingen. 
3. Selecteer EDIFACT overeenkomst en klik op **bewerken als JSON**.  UNH2.5 waarde toevoegen in Hallo ontvangen overeenkomst **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)

### <a name="edifact-encode"></a>EDIFACT coderen
tooEncode Hallo binnenkomend bericht, Hallo schema in Hallo EDIFACT overeenkomst verzendinstellingen configureren
1. Hallo schema toohello integratie account toevoegen    
2. Hallo-schema in Hallo EDIFACT overeenkomst verzendinstellingen configureren. 
3. Selecteer EDIFACT overeenkomst en klik op **bewerken als JSON**.  UNH2.5 waarde toevoegen in Hallo overeenkomst verzenden **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over de integratie account overeenkomsten](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  