---
title: 'Logic Apps B2B lijst met fouten en oplossingen: Azure App Service | Microsoft Docs'
description: Logic Apps B2B lijst met fouten en oplossingen
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
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Logic Apps B2B lijst met fouten en oplossingen  
In dit artikel helpt u bij het oplossen van fouten die mogelijk in Logic Apps B2B-scenario's en stelt de nodige acties voor het oplossen van deze fouten.


## <a name="agreement-resolution"></a>Omzetting van de overeenkomst

### <a name="no-agreement-found"></a>* Geen overeenkomst gevonden 

|   |   |  
|---|---|
| Foutbeschrijving | Er is geen overeenkomst gevonden met de overeenkomst resolutie Parameters|    
| Gebruikersactie | Hallo overeenkomst moet worden toegevoegd als toohello integratie account met overeengekomen business identiteiten.</br> Hallo business identiteiten moeten overeenkomen met toohello invoerbericht-id 's|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>* Geen overeenkomst gevonden met identiteiten

|   |   | 
|---|---|
| Foutbeschrijving | Er is geen overeenkomst gevonden met identiteiten: 'AS2Identity':: 'Partner1' en 'AS2Identity':: 'Partner3'| 
| Gebruikersactie | Ongeldige AS2-uit of AS2-tooconfigured voor overeenkomst. </br> Juiste AS2 bericht AS2-uit of AS2-tooheaders of overeenkomst toomatch AS2-id's in AS2 bericht headers met de configuraties van de overeenkomst |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>* AS2 berichtkoppen ontbreekt  

|   |   |  
|---|---|
| Foutbeschrijving| Ongeldige AS2-headers. Een van de ' AS2-aan ' of ' AS2-van ' headers zijn leeg| 
| Gebruikersactie | Een AS2-bericht is ontvangen die geen Hallo AS2 bevat-uit of AS2-tooor beide headers. </br> Controleer AS2 bericht AS2-vanaf en AS2-tooheaders en corrigeer deze op basis van overeenkomst configuratie |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>* Ontbrekende AS2 berichttekst en -koppen    

|   |   |  
|---|---|
| Foutbeschrijving| Hallo aanvraaginhoud is null of leeg | 
| Gebruikersactie | Een AS2-bericht is ontvangen die geen berichttekst Hallo bevat |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>* Ontsleutelingsfout AS2-bericht

|   |   | 
|---|---|
| Foutbeschrijving |  [verwerkt/fout: ontsleuteling is mislukt] | 
| Gebruikersactie | Voeg @base64ToBinary tooAS2Message voordat toopartner worden verzonden 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a>* MDN ontsleutelingsfout

|   |   | 
|---|---|
| Foutbeschrijving |  [verwerkt/fout: ontsleuteling is mislukt] | 
| Gebruikersactie | Voeg @base64ToBinary tooMDN voordat toopartner worden verzonden 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a>* Handtekeningcertificaat ontbreekt

|   |   |  
|---|---|
| Foutbeschrijving| Hallo is certificaat voor ondertekening niet geconfigureerd voor AS2 partij. </br> AS2-vanaf: partner1 AS2-te: partner2 | 
| Gebruikersactie | AS2-overeenkomst instellingen configureren met het juiste certificaat voor handtekening |
|  |  | 

## <a name="x12-and-edifact"></a>X12 en EDIFACT

### <a name="-leading-or-trailing-space-found"></a>* Voorloop- of een afsluitende spatie gevonden    
    
|   |   | 
|---|---|
| Foutbeschrijving | Fout opgetreden tijdens het parseren. Edifact-transactie ingesteld met de id ' 123456 'opgenomen in de DIF (zonder groep) met id ' 987654' Hallo, met afzender-id 'Partner1', 'Partner2'-id van de ontvanger is onderbroken met de volgende fouten: voorloopspaties afsluitende scheidingsteken gevonden |
| Gebruikersactie | Hallo overeenkomst instellingen toobe geconfigureerd tooallow voorloopspaties en afsluitende spatie. </br> Overeenkomst instellingen tooallow voorloopspaties en afsluitende spatie bewerken |
|   |   |

![ruimte](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a>* Dubbele selectievakje is ingeschakeld in Hallo overeenkomst

|   |   | 
|---|---| 
| Foutbeschrijving | Dubbele controle-aantal |
| Gebruikersactie | Deze fout geeft aan ontvangen Hallo-bericht heeft dubbele besturingselement cijfers. </br> Corrigeer Hallo besturingselementnummer en het Hallo-bericht te verzenden |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a>* Ontbrekende schema in Hallo overeenkomst

|   |   | 
|---|---| 
| Foutbeschrijving | Fout opgetreden tijdens het parseren. Hallo X12 transactie set met id '564220001' opgenomen in functionele groep met id '56422', in het knooppunt met id '000056422' met afzender-id ' 12345678', ' 87654321-id van de ontvanger' wordt onderbroken met de volgende fouten 'Hallo-bericht heeft een onbekende document ty PE en tooany Hallo bestaande schema's geconfigureerd in de overeenkomst Hallo wordt niet omgezet ' |
| Gebruikersactie | Schema in Hallo overeenkomst instellingen configureren  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a>* Onjuist schema in Hallo overeenkomst

|   |   | 
|---|---| 
| Foutbeschrijving | Hallo-bericht heeft een onbekend documenttype en tooany Hallo bestaande schema's geconfigureerd in de overeenkomst Hallo niet is opgelost. |
| Gebruikersactie | Juiste schema in Hallo overeenkomst instellingen configureren  |
|   |   |

## <a name="flat-file"></a>Plat bestand

### <a name="-input-message-with-no-body"></a>* Invoerbericht bij geen instantie

|   |   | 
|---|---|
| Foutbeschrijving | InvalidTemplate. Kan geen tooprocess sjabloontaalexpressies in de invoer van de actie 'Flat_File_Decoding' op regel '1' en kolom '1902': ' eigenschap 'inhoud' verwacht een waarde maar kreeg null vereist. Pad '.'. |
| Gebruikersactie | Deze fout geeft aan dat invoer het Hallo-bericht bevat geen hoofdtekst |
|   |   | 

## <a name="learn-more"></a>Meer informatie
[Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md)
