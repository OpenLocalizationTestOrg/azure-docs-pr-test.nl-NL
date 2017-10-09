---
title: aaaSchemas voor XML-validatie - Azure Logic Apps | Microsoft Docs
description: XML-documenten met schema's voor Azure Logic Apps en Enterprise Integration Pack valideren
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a>XML-validatie met schema's voor Azure Logic Apps en Hallo Enterprise Integration Pack

Schema's bevestigen dat Hallo XML-documenten die u ontvangt geldig zijn en Hallo gegevens in een vooraf gedefinieerde indeling verwachte. Schema's kunnen ook berichten die worden uitgewisseld in een B2B-scenario te valideren.

## <a name="add-a-schema"></a>Een schema toevoegen

1. Selecteer in de Azure-portal hello, **meer services**.

    ![Azure-portal 'Meer services'](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. Voer in het zoekvak Hallo-filter, **integratie**, en selecteer **Integratieaccounts** uit de lijst met resultaten Hallo.

    ![Zoekvak filteren](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. Selecteer Hallo **integratie account** waar u tooadd Hallo schema.

    ![Lijst met integratieaccounts](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. Kies Hallo **schema's** tegel.

    ![Voorbeeld van de integratie-account, 'Schema'](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a>Toevoegen van een schemabestand dat kleiner is dan 2 MB

1. In Hallo **schema's** blade die wordt geopend (van Hallo vorige stappen), kiest **toevoegen**.

    ![Schema's blade "Toevoegen"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. Voer een naam voor uw schema. Hallo-schema-bestand uploaden door het selecteren van Hallo map pictogram volgende toohello **Schema** vak. Nadat het uploadproces Hallo is voltooid, selecteert u **OK**.

    ![Schermopname van 'Toevoegen Schema', met 'Kleine file' gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a>Een schemabestand groter is dan 2 MB (omhoog too8 MB maximaal) toevoegen

Deze stappen verschillen op basis van het toegangsniveau voor Hallo blob-container: **openbare** of **geen anonieme toegang**.

**toodetermine dit toegangsniveau**

1.  Open **Azure Opslagverkenner**. 

2.  Onder **Blob-Containers**, selecteer Hallo gewenste blob-container. 

3.  Selecteer **beveiliging**, **toegangsniveau**.

Als Hallo blob beveiligingsniveau toegang is **openbare**, als volgt te werk.

![Azure Storage Explorer met de 'Blob-Containers', 'Beveiliging' en 'Openbare' gemarkeerd](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. Hallo schema tooyour storage-account uploaden en kopieer Hallo URI.

    ![Storage-account met URI gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. In **Schema toevoegen**, selecteer **groot bestand**, en geef Hallo URI in Hallo **inhoud URI** in het tekstvak.

    ![Schema's met de knop 'Toevoegen' en 'Grote file' gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

Als Hallo blob beveiligingsniveau toegang is **geen anonieme toegang**, als volgt te werk.

![Azure Storage Explorer met de 'Blob-Containers', 'Beveiliging' en 'Geen anonieme toegang' gemarkeerd](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. Hallo schema tooyour storage-account uploaden.

    ![Storage-account](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. Een shared access signature voor Hallo schema genereren.

    ![Storage-account met gedeelde toegang handtekeningen tabblad gemarkeerd](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. In **Schema toevoegen**, selecteer **groot bestand**, en geef Hallo shared access signature URI voor in Hallo **inhoud URI** in het tekstvak.

    ![Schema's met de knop 'Toevoegen' en 'Grote file' gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. In Hallo **schema's** blade van uw account voor de integratie van uw zojuist toegevoegde schema moet worden weergegeven.

    ![Uw account integratie met 'Schema' en de nieuwe schema Hallo gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a>Schema's bewerken

1. Kies Hallo **schema's** tegel.

2. Na het Hallo **schema's** blade wordt geopend, selecteer Hallo-schema dat u wilt dat tooedit.

3. Op Hallo **schema's** blade kiezen **bewerken**.

    ![Schema's-blade](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. Selecteer Hallo schemabestand dat u wilt dat tooedit en selecteer **Open**.

    ![Open schema bestand tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

Azure toont een bericht dat Hallo schema zijn geüpload.

## <a name="delete-schemas"></a>Schema's verwijderen

1. Kies Hallo **schema's** tegel.

2. Na het Hallo **schema's** blade wordt geopend, selecteer Hallo schema gewenste toodelete.

3. Op Hallo **schema's** blade kiezen **verwijderen**.

    ![Schema's-blade](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. schema dat u wilt dat toodelete hello tooconfirm hebt geselecteerd, kiest u **Ja**.

    ![Bevestigingsbericht 'Schema verwijderen'](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    In Hallo **schema's** blade Hallo schema lijst wordt vernieuwd en bevat niet langer Hallo-schema dat u hebt verwijderd.

    ![Uw integratie met 'Schema' gemarkeerd-Account](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md "meer informatie over Hallo enterprise integration pack").  

