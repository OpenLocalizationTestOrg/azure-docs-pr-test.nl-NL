---
title: aaaValidate XML is - Azure Logic Apps | Microsoft Docs
description: XML-validatie met schema's voor Azure Logic Apps en B2B-scenario's met behulp van Enterprise Integration Pack Hallo
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a>XML-validatie voor enterprise-integratie

Vaak in B2B-scenario's, moeten Hallo partners in een overeenkomst ervoor zorgen dat Hallo-berichten ze wisselen geldig zijn voordat u kunt beginnen met het verwerken van gegevens. U kunt documenten tegen een vooraf gedefinieerd schema valideren met behulp van Hallo gebruik Hallo XML-validatie-connector in Hallo Enterprise Integration Pack.

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>Een document met Hallo XML-validatie connector valideren

1. Een logische app maken en [Hallo app toohello integratie account koppelen](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink een integratie account tooa logische app meer") waarvoor Hallo schema gewenste toouse voor het valideren van XML-gegevens.

2. Voeg een **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** trigger tooyour logische app.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. Hallo tooadd **XML-validatie** actie, kies **een actie toevoegen**.

4. alle acties toohello die u wilt, Hallo toofilter Voer *xml* in het zoekvak Hallo. Kies **XML-validatie**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. Selecteer toospecify Hallo XML-inhoud die u toovalidate wilt, **inhoud**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. Hallo hoofdtekst label als Hallo inhoud die u wilt dat toovalidate selecteren.

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. toospecify hello schema gewenste toouse voor het valideren van de vorige Hallo *inhoud* invoeren, kies **SCHEMANAAM**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. Sla uw werk  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

Nu bent u klaar met het instellen van uw validatie-connector. U kunt in een toepassing concrete toostore Hallo gevalideerd gegevens in een line-of-business (LOB)-app zoals SalesForce. toosend Hallo geverifieerde uitvoer tooSalesforce, een actie toevoegen.

tootest uw actie validatie maken van een aanvraag toohello HTTP-eindpunt.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over Enterprise Integration Pack Hallo](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")   

