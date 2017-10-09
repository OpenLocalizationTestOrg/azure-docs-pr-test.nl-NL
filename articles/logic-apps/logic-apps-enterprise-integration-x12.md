---
title: aaaX12 berichten voor B2B enterprise integration - Azure Logic Apps | Microsoft Docs
description: Exchange X12 berichten in EDI-indeling voor B2B enterprise integratie met Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 7422d2d5-b1c7-4a11-8c9b-0d8cfa463164
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 20a077b299875a16ada66a500d5f1c8f9972d309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-x12-messages-for-enterprise-integration-with-logic-apps"></a>Exchange X12 berichten voor enterprise-integratie met logic apps

Voordat u kunt X12 uitwisselen berichten voor Azure Logic Apps, moet u een X12 overeenkomst en op te slaan die overeenkomst in uw account integratie. Hier vindt u stappen voor het Hallo toocreate een X12 overeenkomst.

> [!NOTE]
> Deze pagina wordt ingegaan op Hallo X12 functies voor Azure Logic Apps. Zie voor meer informatie [EDIFACT](logic-apps-enterprise-integration-edifact.md).

## <a name="before-you-start"></a>Voordat u begint

Hier volgt Hallo items die u nodig:

* Een [integratie account](../logic-apps/logic-apps-enterprise-integration-accounts.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement
* Ten minste twee [partners](../logic-apps/logic-apps-enterprise-integration-partners.md) die zijn gedefinieerd in uw account integratie en geconfigureerd met de id Hallo X12 onder **Business identiteiten**    
* Een vereiste [schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) voor het uploaden van tooyour [integratie-account](../logic-apps/logic-apps-enterprise-integration-accounts.md)

Nadat u [maken van een account integratie](../logic-apps/logic-apps-enterprise-integration-accounts.md), [partners toevoegen](logic-apps-enterprise-integration-partners.md), en hebben een [schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) die u toouse, kunt u een X12 overeenkomst met de volgende stappen.

## <a name="create-an-x12-agreement"></a>Maken van een X12 overeenkomst

1.  Meld u aan toohello [Azure-portal](http://portal.azure.com "Azure-portal"). Selecteer in het linkermenu Hallo **meer services**. 

    > [!TIP]
    > Als er geen **meer services**, moet u wellicht tooexpand Hallo menu eerst. Selecteer bovenaan Hallo Hallo samengevouwen menu, **weergeven in het menu**.

    ![Selecteer op de linkermenu 'Meer services'](./media/logic-apps-enterprise-integration-x12/account-1.png)

2.  Typ in het zoekvak hello, "-integratie" als filter. Selecteer in de lijst met resultaten Hallo **Integratieaccounts**.  

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-x12/account-2.png)

3. In Hallo **Integratieaccounts** blade die wordt geopend, selecteer Hallo integratie account waar u tooadd Hallo overeenkomst.
Als er geen eventuele integratieaccounts [maken van een eerste](../logic-apps/logic-apps-enterprise-integration-accounts.md "alles over integratieaccounts").

    ![Selecteer waar toocreate overeenkomst Hallo integratie-account](./media/logic-apps-enterprise-integration-x12/account-3.png)

4. Selecteer **overzicht**, selecteer daarna Hallo **overeenkomsten** tegel. Als u een tegel overeenkomsten geen hebt, eerst Hallo tegel toevoegen. 

    ![Kies 'Overeenkomsten' tegel](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. Kies in de blade Hallo overeenkomsten die wordt geopend, **toevoegen**.

    ![Kies 'Add'](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)     

6. Onder **toevoegen**, voer een **naam** voor de overeenkomst. Selecteer Hallo overeenkomsttype **X12**. Selecteer Hallo **Host Partner**, **Hostidentiteit**, **Gast Partner**, en **Gast identiteit** voor de overeenkomst. Zie voor meer eigenschapdetails Hallo-tabel in deze stap.

    ![Geef overeenkomstdetails](./media/logic-apps-enterprise-integration-x12/x12-1.png)  

    | Eigenschap | Beschrijving |
    | --- | --- |
    | Naam |Naam van de overeenkomst Hallo |
    | Type licentieovereenkomst | Moet X12 |
    | Host-Partner |Een overeenkomst moet een host en de Gast-partner. Hallo host partner vertegenwoordigt Hallo organisatie die Hallo overeenkomst configureert. |
    | Identiteit van de host |Een id voor Hallo host partner |
    | Gast Partner |Een overeenkomst moet een host en de Gast-partner. Hallo Gast partner vertegenwoordigt Hallo organisatie die bedrijven met Hallo host partner doet. |
    | Identiteit van de Gast |Een id voor Hallo Gast partner |
    | Instellingen te ontvangen |Deze eigenschappen toepassing tooall-berichten ontvangen door een overeenkomst. |
    | Instellingen verzenden |Deze eigenschappen toepassing tooall berichten is verzonden door een overeenkomst. |  

  > [!NOTE]
  > De resolutie van X12 overeenkomst is afhankelijk van overeenkomende Hallo afzender kwalificatie en -id en Hallo ontvanger kwalificatie en gedefinieerd in Hallo partner en het binnenkomende bericht-id. Als deze waarden voor uw partner wijzigen, kunt u Hallo overeenkomst bijwerken.

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configureren hoe uw ingangen overeenkomst berichten ontvangen

Nu dat u de eigenschappen van de overeenkomst Hallo hebt ingesteld, kunt u configureren hoe deze overeenkomst identificeert en binnenkomende berichten ontvangen van uw partner via deze overeenkomst worden verwerkt.

1.  Onder **toevoegen**, selecteer **instellingen ontvangen**.
Deze eigenschappen op basis van uw overeenkomst met Hallo partner die berichten met u uitwisselt configureren. Zie voor eigenschapbeschrijvingen, Hallo tabellen in deze sectie.

    **Ontvangen instellingen** is onderverdeeld in deze secties: id's, bevestiging, schema's, enveloppen, besturingselement getallen, validaties en interne instellingen.

2. Nadat u bent klaar, zorg ervoor dat toosave uw instellingen door te kiezen **OK**.

Nu uw overeenkomst gereed toohandle binnenkomende is berichten die tooyour voldoen instellingen geselecteerd.

### <a name="identifiers"></a>Id 's

![Id-eigenschappen instellen](./media/logic-apps-enterprise-integration-x12/x12-2.png)  

| Eigenschap | Beschrijving |
| --- | --- |
| ISA1 (autorisatie kwalificatie) |Selecteer Hallo autorisatie kwalificatiewaarde in de vervolgkeuzelijst Hallo. |
| ISA2 |Optioneel. Geef autorisatie-informatie-waarde. Als u hebt opgegeven voor ISA1 Hallo-waarde dan 00 is, voert u minimaal één alfanumeriek teken en maximaal 10. |
| ISA3 (beveiliging kwalificatie) |Selecteer Hallo beveiliging kwalificatiewaarde in de vervolgkeuzelijst Hallo. |
| ISA4 |Optioneel. Hallo-beveiligingswaarde informatie invoeren. Als u hebt opgegeven voor ISA3 Hallo-waarde dan 00 is, voert u minimaal één alfanumeriek teken en maximaal 10. |

### <a name="acknowledgment"></a>Bevestiging

![Bevestiging eigenschappen instellen](./media/logic-apps-enterprise-integration-x12/x12-3.png) 

| Eigenschap | Beschrijving |
| --- | --- |
| TA1 verwacht |Retourneert een bevestiging van de technische toohello DIF-afzender |
| VA verwacht |Retourneert een functionele bevestiging toohello DIF-afzender. Vervolgens Selecteer of u Hallo 997 of 999 bevestigingen wilt, gebaseerd op Hallo schemaversie |
| AK2/IK2 lus opnemen |Het genereren van AK2 lussen kunnen in functionele bevestigingen van geaccepteerde transactie instellen |

### <a name="schemas"></a>Schema 's

Selecteer een schema voor elke transactietype (ST1) en de afzender-toepassing (GS2). Hallo ontvangen pijplijn Hallo binnenkomend bericht ontleed door overeenkomende Hallo waarden voor ST1 en GS2 in binnenkomende Hallo-bericht met de Hallo waarden die u hebt hier set en Hallo-schema van inkomende hello-bericht met Hallo schema u hier instelt.

![Selecteer schema](./media/logic-apps-enterprise-integration-x12/x12-33.png) 

| Eigenschap | Beschrijving |
| --- | --- |
| Versie |Hallo X12 versie selecteren |
| Transactietype (ST01) |Hallo transactietype selecteren |
| Afzender-toepassing (GS02) |Hallo afzender-toepassing selecteren |
| Schema |Selecteer Hallo schemabestand gewenste toouse. Schema's zijn tooyour integratie account toegevoegd. |

> [!NOTE]
> Hallo vereist configureren [Schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) die geüploade tooyour [integratie account](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Enveloppen

![Hallo scheidingsteken opgeven in een set met transactie: standaard-id of herhaling scheidingsteken kiezen](./media/logic-apps-enterprise-integration-x12/x12-34.png)

| Eigenschap | Beschrijving |
| --- | --- |
| Gebruik ISA11 |Hiermee geeft u Hallo scheidingsteken toouse in een set met transactie: <p>Selecteer **standaard identifier** toouse een punt (.) voor decimale notatie in plaats van de decimale notatie Hallo van inkomende hello-document in Hallo EDI pijplijn ontvangen. <p>Selecteer **herhaling scheidingsteken** toospecify Hallo scheidingsteken voor herhaalde exemplaren van een eenvoudige gegevenselement of een herhaalde gegevensstructuur. Bijvoorbeeld, wordt meestal hello karaat (^) als scheidingsteken gebruikt Hallo herhaling. U kunt alleen Hallo karaat HIPAA schema's gebruiken. |

### <a name="control-numbers"></a>Besturingselement cijfers

![Selecteer hoe toohandle nummer duplicaten bepalen](./media/logic-apps-enterprise-integration-x12/x12-35.png) 

| Eigenschap | Beschrijving |
| --- | --- |
| Controle-aantal Interchange duplicaten weigeren |Dubbele uitgewisseld blokkeren. Hallo interchange besturingselementnummer (ISA13) voor Hallo ontvangen interchange controle-aantal controleert. Als een overeenkomst wordt gedetecteerd, Hallo ontvangen pijplijn Hallo interchange niet verwerken. U kunt opgeven dat Hallo aantal dagen voor het uitvoeren van de controle van de Hallo door middel van een waarde voor *controleren op dubbele ISA13 elke (dagen)*. |
| Dubbele groepscontrolenummers niet toestaan |Blok uitwisselingen met dubbele groep besturingselement nummers. |
| Dubbele transactiereekscontrolenummers niet toestaan |Blok uitwisselingen met dubbele transactie set besturingselement nummers. |

### <a name="validations"></a>Validaties

![Validatie-eigenschappen instellen voor ontvangen berichten](./media/logic-apps-enterprise-integration-x12/x12-36.png) 

Wanneer elke rij van de validatie is voltooid, wordt automatisch een andere toegevoegd. Als u geen regels opgeeft, gebruikt validatie Hallo 'Default' rij.

| Eigenschap | Beschrijving |
| --- | --- |
| Berichttype |Selecteer Hallo EDI-berichttype. |
| EDI-validatie |EDI-validatie wordt uitgevoerd op gegevenstypen zoals gedefinieerd door het Hallo-schema EDI-eigenschappen, beperkingen voor de lengte, leeg gegevenselementen en afsluitende scheidingstekens. |
| Uitgebreide validatie |Als het gegevenstype Hallo niet EDI, validatie op Hallo element eis en toegestaan herhaling, opsommingen en element lengte gegevensvalidatie (min/max). |
| Voorloop-/ Volg nullen toestaan |Alle aanvullende voorloop- of afsluitende nul behouden en ruimte tekens. Verwijder niet deze tekens bevatten. |
| Trim voorloop-/ Volg nullen |Voorloop- of volgspaties nul en spaties verwijderen. |
| Afsluitende scheidingsteken beleid |Afsluitende scheidingstekens genereren. <p>Selecteer **niet toegestaan** tooprohibit afsluitende scheidingstekens en scheidingstekens in Hallo interchange ontvangen. Als Hallo interchange afsluitende scheidingstekens en scheidingstekens heeft, is Hallo interchange gedeclareerd niet geldig. <p>Selecteer **optioneel** tooaccept uitwisselingen met of zonder een afsluitende scheidingstekens en scheidingstekens. <p>Selecteer **verplichte** wanneer Hallo interchange afsluitende scheidingstekens en scheidingstekens moet hebben. |

### <a name="internal-settings"></a>Interne instellingen

![Instellingen voor interne selecteren](./media/logic-apps-enterprise-integration-x12/x12-37.png) 

| Eigenschap | Beschrijving |
| --- | --- |
| Impliciete decimale notatie 'Mm' tooa grondtal 10 numerieke waarde converteren |Converteert een getal EDI die is opgegeven met de Hallo indeling 'Mm' in een numerieke waarde grondtal 10 |
| Lege XML-tags maken als volgscheidingstekens zijn toegestaan |Selecteer dit selectievakje toohave Hallo interchange afzender bevatten lege XML-codes voor afsluitende scheidingstekens. |
| Uitwisseling splitsen in transactiereeksen - transactiereeksen onderbreken bij fout|Elke transactie die is ingesteld in een knooppunt in een afzonderlijke XML-document door toe te passen Hallo juiste envelop toohello transactie set parseert. Onderbreekt alleen Hallo transacties waarbij Hallo-validatie is mislukt. |
| Uitwisseling splitsen in transactiereeksen - uitwisseling onderbreken bij fout|Elke transactie instellen in een knooppunt in een afzonderlijke XML-document door het toepassen van de juiste envelop Hallo parseert. Onderbreekt de gehele uitwisseling wanneer een of meer sets transactie in Hallo interchange validatie is mislukt. | 
| Behouden DIF - transactie sets onderbreken bij fout |Hallo interchange intact blijven, maakt een XML-document voor de hele batch uitwisseling Hallo. Alleen Hallo transactie sets die niet voldoen aan validatie, maar blijft tooprocess onderbreekt de sets van alle andere transactie. |
| Uitwisseling bewaren - uitwisseling onderbreken bij fout |Hallo interchange intact blijven, maakt een XML-document voor de hele batch uitwisseling Hallo. Onderbreekt de gehele uitwisseling Hallo wanneer een of meer sets transactie in Hallo interchange validatie is mislukt. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configureren hoe uw overeenkomst verzendt berichten

U kunt configureren hoe deze overeenkomst identificeert en uitgaande berichten die u tooyour partner via deze overeenkomst verzendt worden verwerkt.

1.  Onder **toevoegen**, selecteer **instellingen voor verzenden**.
Deze eigenschappen op basis van uw overeenkomst met uw partner die berichten worden uitgewisseld met u configureren. Zie voor eigenschapbeschrijvingen, Hallo tabellen in deze sectie.

    **Instellingen verzenden** is onderverdeeld in deze secties: id's, bevestiging, schema's, enveloppen, tekensets en scheidingstekens, Control Numbers en validatie.

2. Nadat u bent klaar, zorg ervoor dat toosave uw instellingen door te kiezen **OK**.

De overeenkomst is nu gereed toohandle uitgaande berichten die tooyour geselecteerd instellingen voldoen.

### <a name="identifiers"></a>Id 's

![Id-eigenschappen instellen](./media/logic-apps-enterprise-integration-x12/x12-4.png)  

| Eigenschap | Beschrijving |
| --- | --- |
| Autorisatie kwalificatie (ISA1) |Selecteer Hallo autorisatie kwalificatiewaarde in de vervolgkeuzelijst Hallo. |
| ISA2 |Geef autorisatie-informatie-waarde. Als deze waarde dan 00 is, en voer vervolgens een minimum van een alfanumeriek teken en maximaal 10. |
| Beveiliging-kwalificatie (ISA3) |Selecteer Hallo beveiliging kwalificatiewaarde in de vervolgkeuzelijst Hallo. |
| ISA4 |Hallo-beveiligingswaarde informatie invoeren. Als deze waarde is dan 00 voor tekstvak Hallo-waarde (ISA4), en voer vervolgens een alfanumerieke waarde minimaal en maximaal 10. |

### <a name="acknowledgment"></a>Bevestiging

![Bevestiging eigenschappen instellen](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Eigenschap | Beschrijving |
| --- | --- |
| TA1 verwacht |Retourneert een technische bevestiging (TA1) toohello DIF-afzender. Deze instelling geeft die Hallo host partner die aanvragen voor Hallo-bericht een bevestiging van Hallo Gast partner in Hallo overeenkomst verzendt. Deze bevestigingen worden door Hallo host partner op basis van Hallo instellingen ontvangen van de overeenkomst Hallo verwacht. |
| VA verwacht |Retourneert een functionele bevestiging (VA) toohello DIF-afzender. Selecteer of u Hallo 997 of 999 bevestigingen, op basis van Hallo schema versies die u met werkt. Deze bevestigingen worden door Hallo host partner op basis van Hallo instellingen ontvangen van de overeenkomst Hallo verwacht. |
| VA-versie |Hallo VA versie selecteren |

### <a name="schemas"></a>Schema 's

![Schema toouse selecteren](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Eigenschap | Beschrijving |
| --- | --- |
| Versie |Hallo X12 versie selecteren |
| Transactietype (ST01) |Hallo transactietype selecteren |
| SCHEMA |Selecteer Hallo schema toouse. Schema's bevinden zich in uw account integratie. Als u eerst schema selecteert, configureert het automatisch versie en transactie type  |

> [!NOTE]
> Hallo vereist configureren [Schema](../logic-apps/logic-apps-enterprise-integration-schemas.md) die geüploade tooyour [integratie account](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Enveloppen

![Hallo scheidingsteken opgeven in een set met transactie: standaard-id of herhaling scheidingsteken kiezen](./media/logic-apps-enterprise-integration-x12/x12-6.png) 

| Eigenschap | Beschrijving |
| --- | --- |
| Gebruik ISA11 |Hiermee geeft u Hallo scheidingsteken toouse in een set met transactie: <p>Selecteer **standaard identifier** toouse een punt (.) voor decimale notatie in plaats van de decimale notatie Hallo van inkomende hello-document in Hallo EDI pijplijn ontvangen. <p>Selecteer **herhaling scheidingsteken** toospecify Hallo scheidingsteken voor herhaalde exemplaren van een eenvoudige gegevenselement of een herhaalde gegevensstructuur. Bijvoorbeeld, wordt meestal hello karaat (^) als scheidingsteken gebruikt Hallo herhaling. U kunt alleen Hallo karaat HIPAA schema's gebruiken. |

### <a name="control-numbers"></a>Besturingselement cijfers

![Controle-aantal eigenschappen opgeven](./media/logic-apps-enterprise-integration-x12/x12-8.png) 

| Eigenschap | Beschrijving |
| --- | --- |
| Het versienummer besturingselement (ISA12) |Hallo Hallo X12 standard-versie selecteren |
| Gebruiksindicator (ISA15) |Selecteer Hallo context van een knooppunt.  Hallo-waarden zijn informatie productiegegevens, of gegevens te testen |
| Schema |Genereert Hallo GS en ST segmenten voor een knooppunt X12-codering verzendt toohello pijplijn verzenden |
| GS1 |Optioneel, selecteert u een waarde voor de functionele code uit de vervolgkeuzelijst Hallo Hallo |
| GS2 |Optioneel, toepassing afzender |
| GS3 |Optioneel, toepassing ontvanger |
| GS4 |Optioneel, selecteer CCYYMMDD of JJMMDD |
| GS5 |Optioneel, selecteer UUMM, UUMMSS of HHMMSSdd |
| GS7 |Optioneel, selecteert u een waarde voor Hallo verantwoordelijk agency uit de vervolgkeuzelijst Hallo |
| GS8 |Optioneel, versie van Hallo document |
| Interchange besturingselementnummer (ISA13) |Vereist, Voer in een bereik van waarden voor Hallo interchange controle-aantal. Geef een numerieke waarde met een minimum van 1 en 999999999 maximaal |
| Besturingselement groepsnummer (GS06) |Vereist is, voer een bereik van de getallen voor Hallo besturingselement groepsnummer. Geef een numerieke waarde met een minimum van 1 en 999999999 maximaal |
| Transactie besturingselementnummer (ST02) |Vereist is, voer een bereik van de getallen voor Hallo transactie ingesteld controle-aantal. Geef een bereik van de numerieke waarden met een minimum van 1 en 999999999 maximaal |
| Voorvoegsel |Optioneel, aangewezen voor Hallo bereik van de transactie set besturingselement getallen in de bevestiging gebruikt. Voer een numerieke waarde voor de middelste twee velden Hallo en een alfanumerieke waarde (indien gewenst) voor Hallo-voor- en achtervoegsel velden. Hallo middelste velden zijn vereist en Hallo minimale en maximale waarden voor de controle-aantal Hallo bevatten |
| Achtervoegsel |Optionele, toegewezen voor Hallo bereik van de transactie set besturingselement getallen gebruikt in een bevestiging. Voer een numerieke waarde voor de middelste twee velden Hallo en een alfanumerieke waarde (indien gewenst) voor Hallo-voor- en achtervoegsel velden. Hallo middelste velden zijn vereist en Hallo minimale en maximale waarden voor de controle-aantal Hallo bevatten |

### <a name="character-sets-and-separators"></a>Tekensets en scheidingstekens

Andere dan Hallo-tekenset, kunt u een andere set scheidingstekens voor elk berichttype. Als een tekenset voor een opgegeven bericht-schema niet is opgegeven, wordt de standaardtekenset Hallo gebruikt.

![Geef de scheidingstekens voor berichttypen](./media/logic-apps-enterprise-integration-x12/x12-9.png) 

| Eigenschap | Beschrijving |
| --- | --- |
| Teken Set toobe gebruikt |toovalidate hello eigenschappen, selecteer Hallo X12 tekenset. Hallo-opties zijn Basic, uitgebreid en UTF8. |
| Schema |Selecteer een schema in de vervolgkeuzelijst Hallo. Nadat u elke rij hebt voltooid, wordt er automatisch een nieuwe rij toegevoegd. Voor het geselecteerde schema hello, selecteer Hallo scheidingstekens ingesteld dat u wilt dat toouse, op basis van Hallo volgen beschrijvingen van het scheidingsteken. |
| Invoertype |Selecteer een type invoer in de vervolgkeuzelijst Hallo. |
| Onderdeel scheidingselement |elementen van de samengestelde gegevensbron tooseparate, voer één teken. |
| Gegevens Element scheidingselement |tooseparate eenvoudige gegevenselementen in de elementen van de samengestelde gegevensbron, voert u één teken. |
| Vervangend teken |Voer een vervangend teken dat wordt gebruikt voor het vervangen van alle scheidingstekens in Hallo nettolading gegevens bij het genereren van het uitgaande X12 Hallo-bericht. |
| Segment eindteken |tooindicate hello einde van een segment EDI Voer één teken. |
| Achtervoegsel |Hallo-teken dat wordt gebruikt met Hallo segment-ID selecteren. Als u een achtervoegsel opgeeft, Hallo kunt segment eindteken gegevenselement niet leeg zijn. Als Hallo segment eindteken leeg wordt gelaten, moet u een achtervoegsel toewijzen. |

> [!TIP]
> tooprovide speciaal tekenwaarden, Hallo overeenkomst als JSON bewerken en Hallo ASCII-waarde opgeven voor Hallo speciaal teken.

### <a name="validation"></a>Validatie

![Validatie-eigenschappen instellen voor het verzenden van berichten](./media/logic-apps-enterprise-integration-x12/x12-10.png) 

Wanneer elke rij van de validatie is voltooid, wordt automatisch een andere toegevoegd. Als u geen regels opgeeft, gebruikt validatie Hallo 'Default' rij.

| Eigenschap | Beschrijving |
| --- | --- |
| Berichttype |Selecteer Hallo EDI-berichttype. |
| EDI-validatie |EDI-validatie wordt uitgevoerd op gegevenstypen zoals gedefinieerd door het Hallo-schema EDI-eigenschappen, beperkingen voor de lengte, leeg gegevenselementen en afsluitende scheidingstekens. |
| Uitgebreide validatie |Als het gegevenstype Hallo niet EDI, validatie op Hallo element eis en toegestaan herhaling, opsommingen en element lengte gegevensvalidatie (min/max). |
| Voorloop-/ Volg nullen toestaan |Alle aanvullende voorloop- of afsluitende nul behouden en ruimte tekens. Verwijder niet deze tekens bevatten. |
| Trim voorloop-/ Volg nullen |Voorloop- of afsluitende nul tekens verwijderen. |
| Afsluitende scheidingsteken beleid |Afsluitende scheidingstekens genereren. <p>Selecteer **niet toegestaan** tooprohibit afsluitende scheidingstekens en scheidingstekens in Hallo interchange verzonden. Als Hallo interchange afsluitende scheidingstekens en scheidingstekens heeft, is Hallo interchange gedeclareerd niet geldig. <p>Selecteer **optioneel** toosend uitwisselingen met of zonder een afsluitende scheidingstekens en scheidingstekens. <p>Selecteer **verplichte** als Hallo verzonden interchange afsluitende scheidingstekens en scheidingstekens nodig hebt. |

## <a name="find-your-created-agreement"></a>De overeenkomst zoeken

1.  Als u klaar bent met het instellen van alle uw overeenkomst-eigenschappen op Hallo **toevoegen** blade kiezen **OK** toofinish maken van de overeenkomst en de blade return tooyour integratie-account.

    Nu uw toegevoegde overeenkomst wordt weergegeven in uw **overeenkomsten** lijst.

2.  U kunt ook uw overeenkomsten weergeven in uw Accountoverzicht integratie. Kies op de blade van het integratie-account **overzicht**, selecteer daarna Hallo **overeenkomsten** tegel.

    ![Kies 'Overeenkomsten' tegel tooview alle overeenkomsten](./media/logic-apps-enterprise-integration-x12/x12-1-5.png)   

## <a name="view-hello-swagger"></a>Weergave Hallo swagger
Zie Hallo [swagger details](/connectors/x12/). 

## <a name="learn-more"></a>Meer informatie
* [Meer informatie over Enterprise Integration Pack Hallo](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")  

