---
title: aaaOverride HTTP gedrag met hello Azure CDN regelengine | Microsoft Docs
description: "Hallo regels-engine kunt u toocustomize hoe HTTP-aanvragen worden verwerkt door Azure CDN, zoals een blokkade Hallo levering van bepaalde typen inhoud, een cachebeleid definiëren en HTTP-headers wijzigen."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>HTTP-gedrag met hello Azure CDN regelengine overschrijven
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Overzicht
Hallo-engine voor regels kunt u toocustomize hoe HTTP-aanvragen worden verwerkt, zoals Hallo levering van bepaalde typen inhoud blokkeren, een cachebeleid definiëren en HTTP-headers wijzigen.  Deze zelfstudie wordt gedemonstreerd Hallo cachegedrag van CDN activa maken van een regel die wordt gewijzigd.  Er is ook video-inhoud beschikbaar in Hallo '[Zie ook](#see-also)' sectie.

   > [!TIP] 
   > Zie voor een syntaxis van de toohello verwijzing in detail [regels Engine verwijzing](cdn-rules-engine-reference.md).
   > 


## <a name="tutorial"></a>Zelfstudie
1. Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.
   
    ![Knop blade CDN-profiel beheren](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    Hallo CDN-beheerportal geopend.
2. Klik op Hallo **HTTP grote** tabblad, gevolgd door **regelengine**.
   
    Opties voor een nieuwe regel worden weergegeven.
   
    ![Opties voor nieuwe CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > Hallo volgorde meerdere regels zijn van invloed op hoe ze worden verwerkt. Een volgende regel mogen Hallo handelingen die zijn opgegeven door een vorige regel overschrijven.
   > 
   > 
3. Voer een naam in Hallo **naam / beschrijving** textbox.
4. Identificeer Hallo type aanvragen Hallo regel van toepassing.  Standaard Hallo **altijd** overeen voorwaarde is geselecteerd.  U **altijd** voor deze zelfstudie, dus laat die geselecteerd.
   
   ![CDN overeen voorwaarde](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > Er zijn veel soorten overeen beschikbaar in de vervolgkeuzelijst Hallo voorwaarden.  Te klikken op Hallo blauw pictogram informatief toohello wordt links van Hallo overeen voorwaarde Hallo geselecteerde voorwaarde in detail uitgelegd.
   > 
   >  Zie voor volledige lijst van voorwaardelijke expressies in detail Hallo [regels Engine voorwaardelijke expressies](cdn-rules-engine-reference-match-conditions.md).
   >  
   > Zie voor volledige lijst van voorwaarden van de overeenkomst in detail Hallo [regels overeenkomen met motor](cdn-rules-engine-reference-match-conditions.md).
   > 
   > 
5. Klik op Hallo  **+**  knop naast te**functies** tooadd een nieuwe functie.  Selecteer in de vervolgkeuzelijst aan de linkerkant Hallo Hallo **Force interne-maximumleeftijd**.  Voer in het tekstvak Hallo die wordt weergegeven, **300**.  Laat Hallo resterende standaardwaarden.
   
   ![CDN-functie](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > Omdat met de voorwaarden van de overeenkomst, te klikken op Hallo blauw pictogram informatief toohello Hallo nieuwe weergegeven functie details over deze functie.  In geval van Hallo **Force interne-maximumleeftijd**, zijn we van Hallo actief overschrijven **Cache-Control** en **verloopt** headers toocontrol wanneer Hallo CDN edge-knooppunt wordt Hallo vernieuwen Asset vanuit Hallo oorsprong.  Het voorbeeld van 300 seconden betekent Hallo CDN edge-knooppunt wordt in de cache Hallo asset vijf minuten vóór vernieuwen Hallo asset vanuit de oorsprong.
   > 
   > Zie voor een volledige lijst met functies in detail Hallo [regels Engine functie Details](cdn-rules-engine-reference-features.md).
   > 
   > 
6. Klik op Hallo **toevoegen** knop toosave Hallo nieuwe regel.  de nieuwe regel Hallo nu wacht op goedkeuring. Zodra deze is goedgekeurd, Hallo status verandert van **in behandeling XML** te**Active XML**.
   
   > [!IMPORTANT]
   > Up too90 minuten toopropagate via Hallo CDN kan duren voordat wijzigingen in regels.
   > 
   > 

## <a name="see-also"></a>Zie ook
* [Overzicht van Azure CDN](cdn-overview.md)
* [Regels Engine verwijzing](cdn-rules-engine-reference.md)
* [De overeenkomst motor regels](cdn-rules-engine-reference-match-conditions.md)
* [Regels Engine voorwaardelijke expressies](cdn-rules-engine-reference-conditional-expressions.md)
* [Regels Engine functies](cdn-rules-engine-reference-features.md)
* [Standaardgedrag HTTP met Hallo regelengine](cdn-rules-engine.md)
* [Azure vrijdag: Azure CDN krachtige nieuwe Premiumfuncties](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)