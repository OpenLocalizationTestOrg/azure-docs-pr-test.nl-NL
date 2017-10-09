---
title: aaaEncode of decoderen platte bestanden in Azure logic apps | Microsoft Docs
description: Hoe toouse Hallo bestand bestand encoder of decoder in Enterprise Integration Pack Hallo in logic apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a>Overzicht van enterprise-integratie met platte bestanden

U kunt tooencode XML-inhoud voordat u deze tooa zakelijke partner in een scenario met business-to-business (B2B) verzendt. In een logische app, kunt u Hallo plat bestand connector toodo dit codering. Hallo logische app die u maakt kan de XML inhoud ophalen van een groot aantal bronnen, met inbegrip van na de trigger van een HTTP-aanvraag van een andere toepassing of zelfs op een van de Hallo veel [connectors](../connectors/apis-list.md). Zie voor meer informatie over logische apps Hallo [logic apps documentatie](logic-apps-what-are-logic-apps.md "meer informatie over logische apps").  

## <a name="create-hello-flat-file-encoding-connector"></a>Hallo plat bestand-codering connector maken
Volg deze stappen tooadd een plat bestand codering connector tooyour logische app.

1. Een logische app maken en [tooyour integratie account een koppeling](logic-apps-enterprise-integration-accounts.md "toolink een integratie account tooa logische app meer"). Dit account bevat Hallo schema gebruikt u tooencode Hallo XML-gegevens.  
2. Voeg een **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** trigger tooyour logische app.  
   ![Schermafbeelding van de trigger tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
3. Hallo platte bestandscodering actie, als volgt toevoegen:
   
    a. Selecteer Hallo **plus** aanmelding.
   
    b. Selecteer Hallo **een actie toevoegen** koppeling (wordt weergegeven nadat u hebt geselecteerd Hallo plus -teken).
   
    c. Voer in het zoekvak Hallo *platte* toofilter alle acties toohello een gewenste toouse Hallo.
   
    d. Selecteer Hallo **platte bestandscodering** optie in lijst Hallo.   
   ![Schermopname van platte bestandscodering optie](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
4. Op Hallo **platte bestandscodering** dialoogvenster, selecteer Hallo **inhoud** in het tekstvak.  
   ![Schermopname van inhoud in het tekstvak](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)  
5. Hallo hoofdtekst label als Hallo inhoud die u wilt dat tooencode selecteren. Hallo body code wordt gevuld veld Hallo-inhoud.     
   ![Schermopname van hoofdtekst tag](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. Selecteer Hallo **schemanaam** keuzelijst en kies de gewenste toouse tooencode Hallo Hallo-schema invoer inhoud.    
   ![Schermafbeelding van de naam van de Schema-keuzelijst](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)  
7. Sla uw werk op.   
   ![Pictogram schermafbeelding opslaan](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

Op dit moment bent u klaar instellen van uw codering plat bestand-connector. U kunt in een toepassing concrete toostore Hallo gecodeerde gegevens in een line-of-business-toepassing, zoals Salesforce. Of u kunt dat gecodeerde gegevens tooa trading partner verzenden. U kunt actie toosend Hallo uitvoer van de actie tooSalesforce of tooyour trading partner codering met behulp van een Hallo Hallo eenvoudig andere connectors opgegeven toevoegen.

U kunt nu uw connector testen door te maken van een aanvraag toohello HTTP-eindpunt en met inbegrip van Hallo XML-inhoud in de hoofdtekst Hallo van Hallo-aanvraag.  

## <a name="create-hello-flat-file-decoding-connector"></a>Hallo plat bestand decoderen connector maken

> [!NOTE]
> toocomplete deze stappen, moet u een schemabestand al geüpload rekening u integratie toohave.

1. Voeg een **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** trigger tooyour logische app.  
   ![Schermafbeelding van de trigger tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
2. Hallo plat bestand decoderen actie, als volgt toevoegen:
   
    a. Selecteer Hallo **plus** aanmelding.
   
    b. Selecteer Hallo **een actie toevoegen** koppeling (wordt weergegeven nadat u hebt geselecteerd Hallo plus -teken).
   
    c. Voer in het zoekvak Hallo *platte* toofilter alle acties toohello een gewenste toouse Hallo.
   
    d. Selecteer Hallo **plat bestand decoderen** optie in lijst Hallo.   
   ![Schermopname van plat bestand decoderen optie](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
3. Selecteer Hallo **inhoud** besturingselement. Dit resulteert in een lijst met inhoud van de eerdere stappen die u als de inhoud toodecode Hallo gebruiken kunt Hallo. U ziet dat Hallo *hoofdtekst* van Hallo inkomende HTTP-aanvraag is beschikbaar toobe als inhoud toodecode Hallo gebruikt. U kunt ook inhoud toodecode Hallo rechtstreeks invoeren in Hallo **inhoud** besturingselement.     
4. Selecteer Hallo *hoofdtekst* label. Kennisgeving Hallo body-tag bevindt zich nu in Hallo **inhoud** besturingselement.
5. Hallo-naam van het Hallo-schema dat u wilt dat toouse toodecode Hallo inhoud selecteren. Hallo volgende schermafbeelding ziet u dat *OrderFile* is de naam van de geselecteerde schema Hallo. De naam van dit schema had eerder geüpload Hallo integratie rekening.
   
   ![Schermopname van plat bestand decoderen van het dialoogvenster](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. Sla uw werk op.  
   ![Pictogram schermafbeelding opslaan](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

Op dit moment bent u klaar instellen van uw plat bestand decoderen van connector. U kunt in een toepassing concrete toostore Hallo gedecodeerd gegevens in een line-of-business-toepassing zoals Salesforce. U kunt eenvoudig een actie toosend Hallo uitvoer Hallo actie tooSalesforce decoderen toevoegen.

U kunt nu uw connector testen door het maken van een aanvraag toohello HTTP-eindpunt en inclusief Hallo XML-inhoud die u wilt toodecode in Hallo hoofdtekst van Hallo-aanvraag.  

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack").  

