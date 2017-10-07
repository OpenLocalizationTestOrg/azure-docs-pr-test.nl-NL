---
title: aaaX12 bijhouden schema's voor het bewaken van B2B - Azure Logic Apps | Microsoft Docs
description: Gebruik X12 schema's toomonitor B2B-berichten bijhouden van transacties van uw Azure-Account voor integratie.
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: a5413f80-eaad-4bcf-b371-2ad0ef629c3d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed1b338730214dcae12c367ebff025d7122328fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-x12-messages-toomonitor-success-errors-and-message-properties"></a>Begin- of inschakelen bijhouden van X12 berichten toomonitor geslaagd, fouten en berichteigenschappen
U kunt deze X12 bijhouden van schema's in uw integratie van Azure-account toohelp u business-to-business (B2B) transacties bewaken:

* X12 transactie bijhouden schema instellen
* X12 transactie bevestiging bijhouden schema instellen
* X12 interchange bijhouden schema
* X12 interchange bevestiging schema bijhouden
* Functionele X12 groep bijhouden schema
* Functionele X12 groep bevestiging schema bijhouden

## <a name="x12-transaction-set-tracking-schema"></a>X12 transactie bijhouden schema instellen
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "transactionSetControlNumber": "",
                "CorrelationMessageId": "",
                "messageType": "",
                "isMessageFailed": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "needAk2LoopForValidMessages":  "",
                "segmentsCount": ""
            }
    }
````

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| senderPartnerName | Tekenreeks | Naam van de partner van de afzender het bericht X12. (Optioneel) |
| receiverPartnerName | Tekenreeks | Naam van de partner van de ontvanger het bericht X12. (Optioneel) |
| senderQualifier | Tekenreeks | Kwalificatie partner verzenden. (Verplicht) |
| senderIdentifier | Tekenreeks | Verzenden partner-id. (Verplicht) |
| receiverQualifier | Tekenreeks | Ontvangen partner-kwalificatie. (Verplicht) |
| receiverIdentifier | Tekenreeks | Partner-id ontvangen. (Verplicht) |
| agreementName | Tekenreeks | Naam van Hallo X12 overeenkomst toowhich Hallo-berichten worden opgelost. (Optioneel) |
| Richting | Enum | Stroomrichting Hallo-bericht, ontvangen of verzenden. (Verplicht) |
| interchangeControlNumber | Tekenreeks | Controle-aantal Interchange. (Optioneel) |
| functionalGroupControlNumber | Tekenreeks | Functionele besturingselement getal. (Optioneel) |
| transactionSetControlNumber | Tekenreeks | Transactie instellen besturingselement aantal. (Optioneel) |
| correlationMessageId | Tekenreeks | Correlatie-ID. Een combinatie van {AgreementName} {*GroupControlNumber*} {TransactionSetControlNumber}. (Optioneel) |
| messageType | Tekenreeks | Transactie is ingesteld of documenttype. (Optioneel) |
| isMessageFailed | Booleaanse waarde | Hiermee wordt aangegeven of het X12 Hallo-bericht is mislukt. (Verplicht) |
| isTechnicalAcknowledgmentExpected | Booleaanse waarde | Hiermee wordt aangegeven of Hallo technische bevestiging is geconfigureerd in Hallo X12 overeenkomst. (Verplicht) |
| isFunctionalAcknowledgmentExpected | Booleaanse waarde | Hiermee wordt aangegeven of Hallo functionele bevestiging is geconfigureerd in Hallo X12 overeenkomst. (Verplicht) |
| needAk2LoopForValidMessages | Booleaanse waarde | Hiermee wordt aangegeven of Hallo AK2 lus is vereist voor een geldig bericht. (Verplicht) |
| segmentsCount | Geheel getal | Het aantal segmenten in de transactie Hallo X12 ingesteld. (Optioneel) |

## <a name="x12-transaction-set-acknowledgement-tracking-schema"></a>X12 transactie bevestiging bijhouden schema instellen
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "respondingtransactionSetControlNumber": "",
                "respondingTransactionSetId": "",
                "statusCode": "",
                "processingStatus": "",
                "CorrelationMessageId": ""
                "isMessageFailed": "",
                "ak2Segment": "",
                "ak3Segment": "",
                "ak5Segment": ""
            }
    }
````

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| senderPartnerName | Tekenreeks | Naam van de partner van de afzender het bericht X12. (Optioneel) |
| receiverPartnerName | Tekenreeks | Naam van de partner van de ontvanger het bericht X12. (Optioneel) |
| senderQualifier | Tekenreeks | Kwalificatie partner verzenden. (Verplicht) |
| senderIdentifier | Tekenreeks | Verzenden partner-id. (Verplicht) |
| receiverQualifier | Tekenreeks | Ontvangen partner-kwalificatie. (Verplicht) |
| receiverIdentifier | Tekenreeks | Partner-id ontvangen. (Verplicht) |
| agreementName | Tekenreeks | Naam van Hallo X12 overeenkomst toowhich Hallo-berichten worden opgelost. (Optioneel) |
| Richting | Enum | Stroomrichting Hallo-bericht, ontvangen of verzenden. (Verplicht) |
| interchangeControlNumber | Tekenreeks | Interchange besturingselement aantal Hallo functionele bevestiging. Waarde wordt alleen voor Hallo verzendkant waar functionele bevestiging is ontvangen voor Hallo verzonden berichten toopartner gevuld. (Optioneel) |
| functionalGroupControlNumber | Tekenreeks | Functionele groep besturingselement aantal Hallo functionele bevestiging. Waarde wordt alleen voor Hallo verzendkant waar functionele bevestiging is ontvangen voor Hallo verzonden berichten toopartner gevuld. (Optioneel) |
| isaSegment | Tekenreeks | ISA-segment van het Hallo-bericht. Waarde wordt alleen voor Hallo verzendkant waar functionele bevestiging is ontvangen voor Hallo verzonden berichten toopartner gevuld. (Optioneel) |
| gsSegment | Tekenreeks | GS-segment van het Hallo-bericht. Waarde wordt alleen voor Hallo verzendkant waar functionele bevestiging is ontvangen voor Hallo verzonden berichten toopartner gevuld. (Optioneel) |
| respondingfunctionalGroupControlNumber | Tekenreeks | Controle-aantal interchange reageert. (Optioneel) |
| respondingFunctionalGroupId | Tekenreeks | Reageert functionele groeps-ID, die tooAK101 toewijzingen in Hallo bevestiging. (Optioneel) |
| respondingtransactionSetControlNumber | Tekenreeks | Reageert transactie instellen besturingselement aantal. (Optioneel) |
| respondingTransactionSetId | Tekenreeks | Reageert transactie-ID, waarbij tooAK201 in Hallo bevestiging toegewezen ingesteld. (Optioneel) |
| statusCode | Booleaanse waarde | Transactie bevestiging statuscode ingesteld. (Verplicht) |
| segmentsCount | Enum | Statuscode bevestiging. Toegestane waarden zijn **geaccepteerde**, **geweigerd**, en **AcceptedWithErrors**. (Verplicht) |
| Verwerkingsstatusnaam | Enum | De verwerkingsstatus van Hallo bevestiging. Toegestane waarden zijn **ontvangen**, **gegenereerde**, en **verzonden**. (Verplicht) |
| correlationMessageId | Tekenreeks | Correlatie-ID. Een combinatie van {AgreementName} {*GroupControlNumber*} {TransactionSetControlNumber}. (Optioneel) |
| isMessageFailed | Booleaanse waarde | Hiermee wordt aangegeven of het X12 Hallo-bericht is mislukt. (Verplicht) |
| ak2Segment | Tekenreeks | Bevestiging voor een set transactie binnen Hallo ontvangen functionele groep. (Optioneel) |
| ak3Segment | Tekenreeks | Fouten in een gegevenssegment rapporteert. (Optioneel) |
| ak5Segment | Tekenreeks | Rapporten of Hallo transactie ingesteld geïdentificeerde in Hallo AK2 segment wordt goedgekeurd of geweigerd en waarom. (Optioneel) |

## <a name="x12-interchange-tracking-schema"></a>X12 interchange bijhouden schema
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "isa09": "",
                "isa10": "",
                "isa11": "",
                "isa12": "",
                "isa14": "",
                "isa15": "",
                "isa16": ""
            }
    }
````

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| senderPartnerName | Tekenreeks | Naam van de partner van de afzender het bericht X12. (Optioneel) |
| receiverPartnerName | Tekenreeks | Naam van de partner van de ontvanger het bericht X12. (Optioneel) |
| senderQualifier | Tekenreeks | Kwalificatie partner verzenden. (Verplicht) |
| senderIdentifier | Tekenreeks | Verzenden partner-id. (Verplicht) |
| receiverQualifier | Tekenreeks | Ontvangen partner-kwalificatie. (Verplicht) |
| receiverIdentifier | Tekenreeks | Partner-id ontvangen. (Verplicht) |
| agreementName | Tekenreeks | Naam van Hallo X12 overeenkomst toowhich Hallo-berichten worden opgelost. (Optioneel) |
| Richting | Enum | Stroomrichting Hallo-bericht, ontvangen of verzenden. (Verplicht) |
| interchangeControlNumber | Tekenreeks | Controle-aantal Interchange. (Optioneel) |
| isaSegment | Tekenreeks | Bericht ISA-segment. (Optioneel) |
| isTechnicalAcknowledgmentExpected | Booleaanse waarde | Hiermee wordt aangegeven of Hallo technische bevestiging is geconfigureerd in Hallo X12 overeenkomst. (Verplicht) |
| isMessageFailed | Booleaanse waarde | Hiermee wordt aangegeven of het X12 Hallo-bericht is mislukt. (Verplicht) |
| isa09 | Tekenreeks | X12 document interchange datum. (Optioneel) |
| isa10 | Tekenreeks | X12 Documenteer DIF-tijd. (Optioneel) |
| isa11 | Tekenreeks | X12 interchange besturingselement standaarden id. (Optioneel) |
| isa12 | Tekenreeks | X12 interchange besturingselement versienummer. (Optioneel) |
| isa14 | Tekenreeks | X12 bevestiging wordt gevraagd. (Optioneel) |
| isa15 | Tekenreeks | De indicator voor test- en productie. (Optioneel) |
| isa16 | Tekenreeks | Element scheidingsteken. (Optioneel) |

## <a name="x12-interchange-acknowledgement-tracking-schema"></a>X12 interchange bevestiging schema bijhouden
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "respondingInterchangeControlNumber": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ta102": "",
                "ta103": "",
                "ta105": ""
            }
    }
````

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| senderPartnerName | Tekenreeks | Naam van de partner van de afzender het bericht X12. (Optioneel) |
| receiverPartnerName | Tekenreeks | Naam van de partner van de ontvanger het bericht X12. (Optioneel) |
| senderQualifier | Tekenreeks | Kwalificatie partner verzenden. (Verplicht) |
| senderIdentifier | Tekenreeks | Verzenden partner-id. (Verplicht) |
| receiverQualifier | Tekenreeks | Ontvangen partner-kwalificatie. (Verplicht) |
| receiverIdentifier | Tekenreeks | Partner-id ontvangen. (Verplicht) |
| agreementName | Tekenreeks | Naam van Hallo X12 overeenkomst toowhich Hallo-berichten worden opgelost. (Optioneel) |
| Richting | Enum | Stroomrichting Hallo-bericht, ontvangen of verzenden. (Verplicht) |
| interchangeControlNumber | Tekenreeks | Interchange besturingselement aantal Hallo technische bevestiging dat ontvangen van partners. (Optioneel) |
| isaSegment | Tekenreeks | ISA-segment voor Hallo technische bevestiging dat ontvangen van partners. (Optioneel) |
| respondingInterchangeControlNumber |Tekenreeks | Interchange besturingselementnummer van het voor Hallo technische bevestiging dat ontvangen van partners. (Optioneel) |
| isMessageFailed | Booleaanse waarde | Hiermee wordt aangegeven of het X12 Hallo-bericht is mislukt. (Verplicht) |
| statusCode | Enum | Interchange statuscode bevestiging. Toegestane waarden zijn **geaccepteerde**, **geweigerd**, en **AcceptedWithErrors**. (Verplicht) |
| Verwerkingsstatusnaam | Enum | Status van de bevestiging. Toegestane waarden zijn **ontvangen**, **gegenereerde**, en **verzonden**. (Verplicht) |
| 102 | Tekenreeks | Interchange datum. (Optioneel) |
| ta103 | Tekenreeks | Interchange tijd. (Optioneel) |
| ta105 | Tekenreeks | Interchange Opmerking code. (Optioneel) |

## <a name="x12-functional-group-tracking-schema"></a>Functionele X12 groep bijhouden schema
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "gsSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "gs01": "",
                "gs02": "",
                "gs03": "",
                "gs04": "",
                "gs05": "",
                "gs07": "",
                "gs08": ""
            }
    }
````

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| senderPartnerName | Tekenreeks | Naam van de partner van de afzender het bericht X12. (Optioneel) |
| receiverPartnerName | Tekenreeks | Naam van de partner van de ontvanger het bericht X12. (Optioneel) |
| senderQualifier | Tekenreeks | Kwalificatie partner verzenden. (Verplicht) |
| senderIdentifier | Tekenreeks | Verzenden partner-id. (Verplicht) |
| receiverQualifier | Tekenreeks | Ontvangen partner-kwalificatie. (Verplicht) |
| receiverIdentifier | Tekenreeks | Partner-id ontvangen. (Verplicht) |
| agreementName | Tekenreeks | Naam van Hallo X12 overeenkomst toowhich Hallo-berichten worden opgelost. (Optioneel) |
| Richting | Enum | Stroomrichting Hallo-bericht, ontvangen of verzenden. (Verplicht) |
| interchangeControlNumber | Tekenreeks | Controle-aantal Interchange. (Optioneel) |
| functionalGroupControlNumber | Tekenreeks | Functionele besturingselement getal. (Optioneel) |
| gsSegment | Tekenreeks | GS-berichtsegment. (Optioneel) |
| isTechnicalAcknowledgmentExpected | Booleaanse waarde | Hiermee wordt aangegeven of Hallo technische bevestiging is geconfigureerd in Hallo X12 overeenkomst. (Verplicht) |
| isFunctionalAcknowledgmentExpected | Booleaanse waarde | Hiermee wordt aangegeven of Hallo functionele bevestiging is geconfigureerd in Hallo X12 overeenkomst. (Verplicht) |
| isMessageFailed | Booleaanse waarde | Hiermee wordt aangegeven of het X12 Hallo-bericht is mislukt. (Verplicht)|
| gs01 | Tekenreeks | Functionele identificatiecode. (Optioneel) |
| gs02 | Tekenreeks | De code van de afzender van de toepassing. (Optioneel) |
| gs03 | Tekenreeks | De code van de ontvanger van de toepassing. (Optioneel) |
| gs04 | Tekenreeks | Functionele groep datum. (Optioneel) |
| gs05 | Tekenreeks | Functionele groep tijd. (Optioneel) |
| gs07 | Tekenreeks | Verantwoordelijk agency code. (Optioneel) |
| gs08 | Tekenreeks | Release-versie/bedrijfstak-id-code. (Optioneel) |

## <a name="x12-functional-group-acknowledgement-tracking-schema"></a>Functionele X12 groep bevestiging schema bijhouden
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ak903": "",
                "ak904": "",
                "ak9Segment": ""
            }
    }
````

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| senderPartnerName | Tekenreeks | Naam van de partner van de afzender het bericht X12. (Optioneel) |
| receiverPartnerName | Tekenreeks | Naam van de partner van de ontvanger het bericht X12. (Optioneel) |
| senderQualifier | Tekenreeks | Kwalificatie partner verzenden. (Verplicht) |
| senderIdentifier | Tekenreeks | Verzenden partner-id. (Verplicht) |
| receiverQualifier | Tekenreeks | Ontvangen partner-kwalificatie. (Verplicht) |
| receiverIdentifier | Tekenreeks | Partner-id ontvangen. (Verplicht) |
| agreementName | Tekenreeks | Naam van Hallo X12 overeenkomst toowhich Hallo-berichten worden opgelost. (Optioneel) |
| Richting | Enum | Stroomrichting Hallo-bericht, ontvangen of verzenden. (Verplicht) |
| interchangeControlNumber | Tekenreeks | Controle-aantal voor Hallo verzendkant gevuld wanneer u een technische bevestiging is ontvangen van partners Interchange. (Optioneel) |
| functionalGroupControlNumber | Tekenreeks | Functionele groep besturingselement aantal Hallo technische bevestiging, die wordt gevuld voor Hallo verzenden aan clientzijde wanneer een technische bevestiging is ontvangen van partners. (Optioneel) |
| isaSegment | Tekenreeks | Zelfde als interchange getal, maar alleen in bijzondere gevallen ingevuld beheren. (Optioneel) |
| gsSegment | Tekenreeks | Zelfde als functionele groep aantal, maar alleen in bijzondere gevallen ingevuld bepalen. (Optioneel) |
| respondingfunctionalGroupControlNumber | Tekenreeks | Aantal Hallo oorspronkelijke functionele groep beheren. (Optioneel) |
| respondingFunctionalGroupId | Tekenreeks | Maps tooAK101 in Hallo bevestiging functionele groep-ID. (Optioneel) |
| isMessageFailed | Booleaanse waarde | Hiermee wordt aangegeven of het X12 Hallo-bericht is mislukt. (Verplicht) |
| statusCode | Enum | Statuscode bevestiging. Toegestane waarden zijn **geaccepteerde**, **geweigerd**, en **AcceptedWithErrors**. (Verplicht) |
| Verwerkingsstatusnaam | Enum | De verwerkingsstatus van Hallo bevestiging. Toegestane waarden zijn **ontvangen**, **gegenereerde**, en **verzonden**. (Verplicht) |
| ak903 | Tekenreeks | Het aantal transactie sets ontvangen. (Optioneel) |
| ak904 | Tekenreeks | Aantal transactie sets geaccepteerd in Hallo geïdentificeerd functionele groep. (Optioneel) |
| ak9Segment | Tekenreeks | Of Hallo functionele-groep geïdentificeerd in Hallo AK1 segment wordt goedgekeurd of geweigerd en waarom. (Optioneel) |

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [B2B-berichten controleren](logic-apps-monitor-b2b-message.md).
* Meer informatie over [AS2 bijhouden schema's](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md).
* Meer informatie over [B2B aangepaste schema's bijhouden](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md).
* Meer informatie over [B2B-berichten in de Operations Management Suite-portal Hallo traceren](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Meer informatie over Hallo [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).  
