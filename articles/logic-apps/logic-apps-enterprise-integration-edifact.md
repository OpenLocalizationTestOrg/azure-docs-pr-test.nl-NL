---
title: aaaEDIFACT berichten voor B2B enterprise integration - Azure Logic Apps | Microsoft Docs
description: Exchange EDIFACT berichten in EDI-indeling voor B2B enterprise integratie met Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 2257d2c8-1929-4390-b22c-f96ca8b291bc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/26/2016
ms.author: LADocs; jonfan
ms.openlocfilehash: 496fadcda58de2d36459202b839b0a63c9e5857c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-edifact-messages-for-enterprise-integration-with-logic-apps"></a>Exchange EDIFACT berichten voor enterprise-integratie met logic apps

Voordat u EDIFACT berichten voor Azure Logic Apps uitwisselen kunt, moet u een overeenkomst EDIFACT maken en opslaan van deze overeenkomst in uw account integratie. Hier vindt u stappen voor het Hallo toocreate een overeenkomst EDIFACT.

> [!NOTE]
> Deze pagina wordt ingegaan op Hallo EDIFACT functies voor Azure Logic Apps. Zie voor meer informatie [X12](logic-apps-enterprise-integration-x12.md).

## <a name="before-you-start"></a>Voordat u begint

Hier volgt Hallo items die u nodig:

* Een [integratie account](../logic-apps/logic-apps-enterprise-integration-accounts.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement  
* Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie

> [!NOTE]
> Als u een overeenkomst, de inhoud van de Hallo maakt in Hallo-berichten die u ontvangt of verzendt tooand van Hallo partner moet overeenkomen met de Hallo overeenkomsttype selecteren.

Nadat u [maken van een account integratie](../logic-apps/logic-apps-enterprise-integration-accounts.md) en [partners toevoegen](logic-apps-enterprise-integration-partners.md), kunt u een overeenkomst EDIFACT maken met de volgende stappen.

## <a name="create-an-edifact-agreement"></a>Maken van een overeenkomst EDIFACT 

1.  Meld u aan toohello [Azure-portal](http://portal.azure.com "Azure-portal"). Selecteer in het linkermenu Hallo **meer services**.

    > [!TIP]
    > Als er geen **meer services**, moet u wellicht tooexpand Hallo menu eerst. Selecteer bovenaan Hallo Hallo samengevouwen menu, **weergeven in het menu**.

    ![Selecteer op de linkermenu 'Meer services'](./media/logic-apps-enterprise-integration-edifact/edifact-0.png)

2. Typ in het zoekvak hello, '-integratie"voor uw filter. Selecteer in de lijst met resultaten Hallo **Integratieaccounts**.

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-edifact/edifact-1-3.png)

3. In Hallo **Integratieaccounts** blade die wordt geopend, selecteer Hallo integratie account waar u toocreate Hallo overeenkomst.
Als er geen eventuele integratieaccounts [maken van een eerste](../logic-apps/logic-apps-enterprise-integration-accounts.md "alles over integratieaccounts").  

    ![Selecteer waar toocreate overeenkomst Hallo integratie-account](./media/logic-apps-enterprise-integration-edifact/edifact-1-4.png)

4. Kies Hallo **overeenkomsten** tegel. Als u een tegel overeenkomsten geen hebt, eerst Hallo tegel toevoegen.   

    ![Kies 'Overeenkomsten' tegel](./media/logic-apps-enterprise-integration-edifact/edifact-1-5.png)

5. Kies in de blade Hallo overeenkomsten die wordt geopend, **toevoegen**.

    ![Kies 'Add'](./media/logic-apps-enterprise-integration-edifact/edifact-agreement-2.png)

6. Onder **toevoegen**, voer een **naam** voor de overeenkomst. Voor **type licentieovereenkomst**, selecteer **EDIFACT**. Selecteer Hallo **Host Partner**, **Hostidentiteit**, **Gast Partner**, en **Gast identiteit** voor de overeenkomst.

    ![Geef overeenkomstdetails](./media/logic-apps-enterprise-integration-edifact/edifact-1.png)

    | Eigenschap | Beschrijving |
    | --- | --- |
    | Naam |Naam van de overeenkomst Hallo |
    | Type licentieovereenkomst | EDIFACT moet |
    | Host-Partner |Een overeenkomst moet een host en de Gast-partner. Hallo host partner vertegenwoordigt Hallo organisatie die Hallo overeenkomst configureert. |
    | Identiteit van de host |Een id voor Hallo host partner |
    | Gast Partner |Een overeenkomst moet een host en de Gast-partner. Hallo Gast partner vertegenwoordigt Hallo organisatie die bedrijven met Hallo host partner doet. |
    | Identiteit van de Gast |Een id voor Hallo Gast partner |
    | Instellingen te ontvangen |Deze eigenschappen toepassing tooall-berichten ontvangen door een overeenkomst. |
    | Instellingen verzenden |Deze eigenschappen toepassing tooall berichten is verzonden door een overeenkomst. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configureren hoe uw ingangen overeenkomst berichten ontvangen

Nu dat u de eigenschappen van de overeenkomst Hallo hebt ingesteld, kunt u configureren hoe deze overeenkomst identificeert en binnenkomende berichten ontvangen van uw partner via deze overeenkomst worden verwerkt.

1.  Onder **toevoegen**, selecteer **instellingen ontvangen**.
Deze eigenschappen op basis van uw overeenkomst met Hallo partner die berichten met u uitwisselt configureren. Zie voor eigenschapbeschrijvingen, Hallo tabellen in deze sectie.

    **Ontvangen instellingen** is onderverdeeld in deze secties: id's, bevestiging, schema's, besturingselement getallen, validatie en interne instellingen.

    !['Ontvangen instellingen' configureren](./media/logic-apps-enterprise-integration-edifact/edifact-2.png)  

2. Nadat u bent klaar, zorg ervoor dat toosave uw instellingen door te kiezen **OK**.

Nu uw overeenkomst gereed toohandle binnenkomende is berichten die tooyour voldoen instellingen geselecteerd.

### <a name="identifiers"></a>Id 's

| Eigenschap | Beschrijving |
| --- | --- |
| UNB6.1 (ontvanger verwijzing wachtwoord) |Voer een alfanumerieke waarde opgeven tussen 1 en 14 tekens. |
| UNB6.2 (ontvanger verwijzing kwalificatie) |Voer een alfanumerieke waarde met een minimum van één teken en maximaal twee tekens bestaan. |

### <a name="acknowledgments"></a>Bevestigingen

| Eigenschap | Beschrijving |
| --- | --- |
| Berichtontvangst (CONTRL) |Schakel dit selectievakje tooreturn een afzender technische (CONTRL) bevestiging toohello interchange. Hallo bevestiging verzonden toohello interchange afzender op basis van Hallo instellingen voor verzenden voor Hallo overeenkomst. |
| Bevestiging (CONTRL) |Schakel dit selectievakje tooreturn die een functionele (CONTRL) bevestiging toohello interchange afzender Hallo bevestiging toohello interchange afzender op basis van Hallo instellingen voor verzenden voor Hallo overeenkomst verzonden. |

### <a name="schemas"></a>Schema 's

| Eigenschap | Beschrijving |
| --- | --- |
| UNH2.1 (TYPE) |Selecteer een set transactietype. |
| UNH2.2 (VERSIE) |Voer versienummer Hallo-bericht. (Minimum, één teken; maximum drie tekens). |
| UNH2.3 (VERSIE) |Voer versienummer Hallo-bericht. (Minimum, één teken; maximum drie tekens). |
| UNH2.5 (GEKOPPELDE TOEGEWEZEN CODE) |Hallo toegewezen code invoeren. (Maximaal zes tekens. Moet alfanumerieke). |
| UNG2.1 (APP AFZENDER-ID) |Voer een alfanumerieke waarde met een minimum van één teken en maximaal 35 tekens. |
| UNG2.2 (APP AFZENDER CODE KWALIFICATIE) |Voer een alfanumerieke waarde met een maximum van vier tekens. |
| SCHEMA |Selecteer Hallo geüpload eerder gewenste toouse uit uw account gekoppeld integratie schema. |

### <a name="control-numbers"></a>Besturingselement cijfers
| Eigenschap | Beschrijving |
| --- | --- |
| Controle-aantal Interchange duplicaten weigeren |dubbele uitgewisseld tooblock, selecteert u deze eigenschap. Indien geselecteerd, controleert Hallo EDIFACT decoderen actie Hallo interchange besturingselementnummer (UNB5) voor het uitwisselen van Hallo ontvangen komt niet overeen met een getal eerder verwerkte DIF-besturingselement. Als een overeenkomst wordt gedetecteerd, is vervolgens Hallo interchange niet verwerkt. |
| Controleren op dubbele UNB5 elke (dagen) |Als u toodisallow dubbele interchange besturingselement getallen hebt gekozen, kunt u het aantal dagen wanneer tooperform Hallo controleren door middel van een geschikte waarde Hallo voor deze instelling Hallo opgeven. |
| Dubbele groepscontrolenummers niet toestaan |tooblock uitwisselingen met dubbele groep besturingselement-nummers (UNG5), selecteert u deze eigenschap. |
| Dubbele transactiereekscontrolenummers niet toestaan |tooblock uitwisselingen met dubbele transactie set besturingselement-nummers (UNH1), selecteer deze eigenschap. |
| EDIFACT bevestiging controle-aantal |toodesignate hello transactie ingesteld nummers voor gebruik in een bevestiging, voer een waarde voor het Hallo-voorvoegsel, een bereik van referenties en achtervoegsel. |

### <a name="validations"></a>Validaties

Wanneer elke rij van de validatie is voltooid, wordt automatisch een andere toegevoegd. Als u geen regels opgeeft, gebruikt validatie Hallo 'Default' rij.

| Eigenschap | Beschrijving |
| --- | --- |
| Berichttype |Selecteer Hallo EDI-berichttype. |
| EDI-validatie |EDI-validatie wordt uitgevoerd op gegevenstypen zoals gedefinieerd door het Hallo-schema EDI-eigenschappen, beperkingen voor de lengte, leeg gegevenselementen en afsluitende scheidingstekens. |
| Uitgebreide validatie |Als het gegevenstype Hallo niet EDI, validatie op Hallo element eis en toegestaan herhaling, opsommingen en element lengte gegevensvalidatie (min/max). |
| Voorloop-/ Volg nullen toestaan |Alle aanvullende voorloop- of afsluitende nul behouden en ruimte tekens. Verwijder niet deze tekens bevatten. |
| Trim voorloop-/ Volg nullen |Voorloop- of volgspaties nul en spaties verwijderen. |
| Afsluitende scheidingsteken beleid |Afsluitende scheidingstekens genereren. <p>Selecteer **niet toegestaan** tooprohibit afsluitende scheidingstekens en scheidingstekens in Hallo interchange ontvangen. Als Hallo interchange afsluitende scheidingstekens en scheidingstekens heeft, is Hallo interchange gedeclareerd niet geldig. <p>Selecteer **optioneel** tooaccept uitwisselingen met of zonder een afsluitende scheidingstekens en scheidingstekens. <p>Selecteer **verplichte** wanneer Hallo ontvangen interchange afsluitende scheidingstekens en scheidingstekens moet hebben. |

### <a name="internal-settings"></a>Interne instellingen

| Eigenschap | Beschrijving |
| --- | --- |
| Lege XML-tags maken als volgscheidingstekens zijn toegestaan |Selecteer dit selectievakje toohave Hallo interchange afzender bevatten lege XML-codes voor afsluitende scheidingstekens. |
| Uitwisseling splitsen in transactiereeksen - transactiereeksen onderbreken bij fout|Elke transactie die is ingesteld in een knooppunt in een afzonderlijke XML-document door toe te passen Hallo juiste envelop toohello transactie set parseert. Onderbreken alleen Hallo transactie sets die validatie is mislukt. |
| Uitwisseling splitsen in transactiereeksen - uitwisseling onderbreken bij fout|Elke transactie instellen in een knooppunt in een afzonderlijke XML-document door het toepassen van de juiste envelop Hallo parseert. Hallo gehele uitwisseling onderbreken wanneer een of meer sets transactie in Hallo interchange validatie is mislukt. | 
| Behouden DIF - transactie sets onderbreken bij fout |Hallo interchange intact blijven, maakt een XML-document voor de hele batch uitwisseling Hallo. Onderbreken alleen Hallo transactie sets die validatie is mislukt, maar tooprocess blijft alle andere transactie is ingesteld. |
| Uitwisseling bewaren - uitwisseling onderbreken bij fout |Hallo interchange intact blijven, maakt een XML-document voor de hele batch uitwisseling Hallo. Hallo gehele uitwisseling onderbreken wanneer een of meer sets transactie in Hallo interchange validatie is mislukt. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configureren hoe uw overeenkomst verzendt berichten

U kunt configureren hoe deze overeenkomst identificeert en uitgaande berichten die u tooyour partners via deze overeenkomst verzendt worden verwerkt.

1.  Onder **toevoegen**, selecteer **instellingen voor verzenden**.
Deze eigenschappen op basis van uw overeenkomst met uw partner die berichten worden uitgewisseld met u configureren. Zie voor eigenschapbeschrijvingen, Hallo tabellen in deze sectie.

    **Instellingen verzenden** is onderverdeeld in deze secties: id's, bevestiging, schema's, enveloppen, tekensets en scheidingstekens, Control Numbers en validaties.

    ![Configureer 'Verzenden instellingen'](./media/logic-apps-enterprise-integration-edifact/edifact-3.png)    

2. Nadat u bent klaar, zorg ervoor dat toosave uw instellingen door te kiezen **OK**.

De overeenkomst is nu gereed toohandle uitgaande berichten die tooyour geselecteerd instellingen voldoen.

### <a name="identifiers"></a>Id 's

| Eigenschap | Beschrijving |
| --- | --- |
| UNB1.2 (syntaxis versie) |Selecteer een waarde tussen **1** en **4**. |
| UNB2.3 (omgekeerd routeringsadres van de afzendeer) |Voer een alfanumerieke waarde met een minimum van één teken en maximaal 14 tekens. |
| UNB3.3 (omgekeerd routeringsadres van de ontvanger) |Voer een alfanumerieke waarde met een minimum van één teken en maximaal 14 tekens. |
| UNB6.1 (ontvanger verwijzing wachtwoord) |Voer een alfanumerieke waarde met een minimaal en maximaal 14 tekens. |
| UNB6.2 (ontvanger verwijzing kwalificatie) |Voer een alfanumerieke waarde met een minimum van één teken en maximaal twee tekens bestaan. |
| UNB7 (toepassing verwijzings-ID) |Voer een alfanumerieke waarde met een minimum van één teken en maximaal 14 tekens |

### <a name="acknowledgment"></a>Bevestiging
| Eigenschap | Beschrijving |
| --- | --- |
| Berichtontvangst (CONTRL) |Schakel dit selectievakje in als Hallo gehost partner tooreceive een bevestiging van de technische (CONTRL) verwacht. Deze instelling geeft aan dat partner Hallo gehost, die het Hallo-bericht verzendt, een bevestiging van Hallo Gast partner-aanvragen. |
| Bevestiging (CONTRL) |Schakel dit selectievakje in als Hallo gehost partner tooreceive een functionele (CONTRL) bevestiging verwacht. Deze instelling geeft aan dat partner Hallo gehost, die het Hallo-bericht verzendt, een bevestiging van Hallo Gast partner-aanvragen. |
| SG1/SG4-lus genereren voor geaccepteerde transactiesets |Als u een functionele bevestiging toorequest kiest, selecteert u deze generatie selectievakje tooforce SG1/SG4 lussen in functionele CONTRL bevestigingen voor geaccepteerde transactie sets. |

### <a name="schemas"></a>Schema 's
| Eigenschap | Beschrijving |
| --- | --- |
| UNH2.1 (TYPE) |Selecteer een set transactietype. |
| UNH2.2 (VERSIE) |Voer versienummer Hallo-bericht. |
| UNH2.3 (VERSIE) |Voer versienummer Hallo-bericht. |
| SCHEMA |Selecteer Hallo schema toouse. Schema's bevinden zich in uw account integratie. tooaccess uw schema eerst uw integratie account tooyour logische app koppelen. |

### <a name="envelopes"></a>Enveloppen
| Eigenschap | Beschrijving |
| --- | --- |
| UNB8 (prioriteitscode Processing) |Een alfabetische waarde invoeren die is niet meer dan één teken lang. |
| UNB10 (overeenkomst communicatie) |Voer een alfanumerieke waarde met een minimum van één teken en maximaal 40 tekens. |
| UNB11 (testen Indicator) |Selecteer dit selectievakje tooindicate die Hallo interchange gegenereerde testen gegevens |
| UNA-segment toepassen (advies voor de servicetekenreeks) |Schakel dit selectievakje toogenerate een segment UNA voor Hallo interchange toobe verzonden. |
| UNG-segmenten toepassen (functiegroepheader) |Schakel dit selectievakje toocreate segmenten in Hallo functionele groep-header in Hallo verzonden berichten toohello Gast partner groeperen. Hallo zijn volgende waarden gebruikte toocreate hello UNG segmenten: <p>Voor **UNG1**, voer een alfanumerieke waarde met een minimum van één teken en maximaal zes tekens. <p>Voor **UNG2.1**, voer een alfanumerieke waarde met een minimum van één teken en maximaal 35 tekens. <p>Voor **UNG2.2**, voer een alfanumerieke waarde, met een maximum van vier tekens. <p>Voor **UNG3.1**, voer een alfanumerieke waarde met een minimum van één teken en maximaal 35 tekens. <p>Voor **UNG3.2**, voer een alfanumerieke waarde, met een maximum van vier tekens. <p>Voor **UNG6**, voer een alfanumerieke waarde met een minimaal en maximaal drie tekens bestaan. <p>Voor **UNG7.1**, voer een alfanumerieke waarde met ten minste één teken en maximaal drie tekens bestaan. <p>Voor **UNG7.2**, voer een alfanumerieke waarde met ten minste één teken en maximaal drie tekens bestaan. <p>Voor **UNG7.3**, voer een alfanumerieke waarde met een minimum van 1 teken en maximaal 6 tekens. <p>Voor **UNG8**, voer een alfanumerieke waarde met een minimum van één teken en maximaal 14 tekens. |

### <a name="character-sets-and-separators"></a>Tekensets en scheidingstekens

Andere dan Hallo-tekenset, kunt u een andere set scheidingstekens toobe gebruikt voor elk berichttype. Als een tekenset voor een opgegeven bericht-schema niet is opgegeven, wordt de standaardtekenset Hallo gebruikt.

| Eigenschap | Beschrijving |
| --- | --- |
| UNB1.1 (System Identifier) |Selecteer Hallo EDIFACT teken toobe toegepast op Hallo uitgaande interchange ingesteld. |
| Schema |Selecteer een schema in de vervolgkeuzelijst Hallo. Nadat u elke rij hebt voltooid, wordt er automatisch een nieuwe rij toegevoegd. Voor het geselecteerde schema hello, selecteer Hallo scheidingstekens ingesteld dat u wilt dat toouse, op basis van Hallo volgen beschrijvingen van het scheidingsteken. |
| Invoertype |Selecteer een type invoer in de vervolgkeuzelijst Hallo. |
| Onderdeel scheidingselement |elementen van de samengestelde gegevensbron tooseparate, voer één teken. |
| Gegevens Element scheidingselement |tooseparate eenvoudige gegevenselementen in de elementen van de samengestelde gegevensbron, voert u één teken. |
| Segment eindteken |tooindicate hello einde van een segment EDI Voer één teken. |
| Achtervoegsel |Hallo-teken dat wordt gebruikt met Hallo segment-ID selecteren. Als u een achtervoegsel opgeeft, Hallo kunt segment eindteken gegevenselement niet leeg zijn. Als Hallo segment eindteken leeg wordt gelaten, moet u een achtervoegsel toewijzen. |

### <a name="control-numbers"></a>Besturingselement cijfers
| Eigenschap | Beschrijving |
| --- | --- |
| UNB5 (Interchange controle-aantal) |Een voorvoegsel, een bereik van waarden voor Hallo interchange besturingselement getal en een achtervoegsel invoeren. Deze waarden zijn gebruikte toogenerate een uitgaande knooppunt. Hallo-voor- en achtervoegsel zijn optioneel, terwijl Hallo besturingselement getal vereist is. controle-aantal Hello wordt verhoogd voor elk nieuw bericht; Hallo-voor- en achtervoegsel Hallo blijft hetzelfde. |
| UNG5 (groep controle-aantal) |Een voorvoegsel, een bereik van waarden voor Hallo interchange besturingselement getal en een achtervoegsel invoeren. Deze waarden worden gebruikt toogenerate Hallo groepsnummer besturingselement. Hallo-voor- en achtervoegsel zijn optioneel, terwijl Hallo besturingselement getal vereist is. controle-aantal Hallo wordt voor elk nieuw bericht verhoogd tot Hallo maximumwaarde is bereikt; Hallo-voor- en achtervoegsel Hallo blijft hetzelfde. |
| UNH1 (Message Header referentienummer) |Een voorvoegsel, een bereik van waarden voor Hallo interchange besturingselement getal en een achtervoegsel invoeren. Deze waarden worden gebruikt referentienummer voor toogenerate Hallo-bericht-header. Hallo-voor- en achtervoegsel zijn optioneel, terwijl Hallo referentienummer vereist is. Hallo referentienummer wordt verhoogd voor elk nieuw bericht; Hallo-voor- en achtervoegsel Hallo blijft hetzelfde. |

### <a name="validations"></a>Validaties

Wanneer elke rij van de validatie is voltooid, wordt automatisch een andere toegevoegd. Als u geen regels opgeeft, gebruikt validatie Hallo 'Default' rij.

| Eigenschap | Beschrijving |
| --- | --- |
| Berichttype |Selecteer Hallo EDI-berichttype. |
| EDI-validatie |EDI-validatie wordt uitgevoerd op gegevenstypen zoals gedefinieerd door Hallo EDI-eigenschappen van Hallo schema, beperkingen voor de lengte, leeg gegevenselementen en afsluitende scheidingstekens. |
| Uitgebreide validatie |Als het gegevenstype Hallo niet EDI, validatie op Hallo element eis en toegestaan herhaling, opsommingen en element lengte gegevensvalidatie (min/max). |
| Voorloop-/ Volg nullen toestaan |Alle aanvullende voorloop- of afsluitende nul behouden en ruimte tekens. Verwijder niet deze tekens bevatten. |
| Trim voorloop-/ Volg nullen |Voorloop- of afsluitende nul tekens verwijderen. |
| Afsluitende scheidingsteken beleid |Afsluitende scheidingstekens genereren. <p>Selecteer **niet toegestaan** tooprohibit afsluitende scheidingstekens en scheidingstekens in Hallo interchange verzonden. Als Hallo interchange afsluitende scheidingstekens en scheidingstekens heeft, is Hallo interchange gedeclareerd niet geldig. <p>Selecteer **optioneel** toosend uitwisselingen met of zonder een afsluitende scheidingstekens en scheidingstekens. <p>Selecteer **verplichte** als Hallo verzonden interchange afsluitende scheidingstekens en scheidingstekens nodig hebt. |

## <a name="find-your-created-agreement"></a>De overeenkomst zoeken

1.  Als u klaar bent met het instellen van alle uw overeenkomst-eigenschappen op Hallo **toevoegen** blade kiezen **OK** toofinish maken van de overeenkomst en de blade return tooyour integratie-account.

    Nu uw toegevoegde overeenkomst wordt weergegeven in uw **overeenkomsten** lijst.

2.  U kunt ook uw overeenkomsten weergeven in uw Accountoverzicht integratie. Kies op de blade van het integratie-account **overzicht**, selecteer daarna Hallo **overeenkomsten** tegel. 

    ![Kies 'Overeenkomsten' tegel tooview alle overeenkomsten](./media/logic-apps-enterprise-integration-edifact/edifact-4.png)   

## <a name="view-swagger-file"></a>Swagger-bestand weergeven
tooview hello Swagger voor Hallo EDIFACT connector, Zie [EDIFACT](/connectors/edifact/).

## <a name="learn-more"></a>Meer informatie
* [Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")  

