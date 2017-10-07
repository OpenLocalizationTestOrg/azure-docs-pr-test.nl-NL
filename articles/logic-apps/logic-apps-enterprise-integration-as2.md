---
title: aaaAS2 berichten voor B2B enterprise integration - Azure Logic Apps | Microsoft Docs
description: Exchange AS2-berichten voor B2B enterprise integratie met Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a>Exchange AS2-berichten voor enterprise-integratie met logic apps

Voordat u AS2 berichten voor Azure Logic Apps uitwisselen kunt, moet u een AS2-overeenkomst maken en opslaan van deze overeenkomst in uw account integratie. Hier vindt u stappen voor het Hallo toocreate een AS2-overeenkomst.

## <a name="before-you-start"></a>Voordat u begint

Hier volgt Hallo items die u nodig:

* Een [integratie account](../logic-apps/logic-apps-enterprise-integration-accounts.md) die al is gedefinieerd en die zijn gekoppeld aan uw Azure-abonnement
* Ten minste twee [partners](logic-apps-enterprise-integration-partners.md) die al zijn gedefinieerd in uw account integratie en geconfigureerd met de kwalificatie Hallo AS2 onder **Business identiteiten**

> [!NOTE]
> Wanneer u een overeenkomst maakt, moet de Hallo inhoud in Hallo overeenkomst bestand overeenkomen met Hallo overeenkomsttype selecteren.    

Nadat u [maken van een account integratie](../logic-apps/logic-apps-enterprise-integration-accounts.md) en [partners toevoegen](logic-apps-enterprise-integration-partners.md), kunt u een AS2-overeenkomst met de volgende stappen.

## <a name="create-an-as2-agreement"></a>Maken van een AS2-overeenkomst

1.  Meld u aan toohello [Azure-portal](http://portal.azure.com "Azure-portal").  

2.  Selecteer in het linkermenu Hallo **meer services**. Voer in het zoekvak Hallo **integratie** als filter. Selecteer in de lijst met resultaten Hallo **Integratieaccounts**.

    > [!TIP]
    > Als er geen **meer services**, moet u wellicht tooexpand Hallo menu eerst. Selecteer bovenaan Hallo Hallo samengevouwen menu, **weergeven in het menu**.

    ![Meer services, filter op "-integratie", selecteren "Integratieaccounts"](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. In Hallo **Integratieaccounts** blade die wordt geopend, selecteer Hallo integratie account waar u toocreate Hallo overeenkomst.
Als er geen eventuele integratieaccounts [maken van een eerste](../logic-apps/logic-apps-enterprise-integration-accounts.md "alles over integratieaccounts").  

    ![Hallo-integratie account waar toocreate overeenkomst Hallo selecteren](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Kies Hallo **overeenkomsten** tegel. Als u een tegel overeenkomsten geen hebt, eerst Hallo tegel toevoegen.

    ![Kies 'Overeenkomsten' tegel](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. Kies in de blade Hallo overeenkomsten die wordt geopend, **toevoegen**.

    ![Kies 'Add'](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. Onder **toevoegen**, voer een **naam** voor de overeenkomst. Voor **type licentieovereenkomst**, selecteer **AS2**. Selecteer Hallo **Host Partner**, **Hostidentiteit**, **Gast Partner**, en **Gast identiteit** voor de overeenkomst.

    ![Geef overeenkomstdetails](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | Eigenschap | Beschrijving |
    | --- | --- |
    | Naam |Naam van de overeenkomst Hallo |
    | Type licentieovereenkomst | AS2 moet |
    | Host-Partner |Een overeenkomst moet een host en de Gast-partner. Hallo host partner vertegenwoordigt Hallo organisatie die Hallo overeenkomst configureert. |
    | Identiteit van de host |Een id voor Hallo host partner |
    | Gast Partner |Een overeenkomst moet een host en de Gast-partner. Hallo Gast partner vertegenwoordigt Hallo organisatie die bedrijven met Hallo host partner doet. |
    | Identiteit van de Gast |Een id voor Hallo Gast partner |
    | Instellingen te ontvangen |Deze eigenschappen toepassing tooall-berichten ontvangen door een overeenkomst. |
    | Instellingen verzenden |Deze eigenschappen toepassing tooall berichten is verzonden door een overeenkomst. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configureren hoe uw ingangen overeenkomst berichten ontvangen

Nu dat u de eigenschappen van de overeenkomst Hallo hebt ingesteld, kunt u configureren hoe deze overeenkomst identificeert en binnenkomende berichten ontvangen van uw partner via deze overeenkomst worden verwerkt.

1.  Onder **toevoegen**, selecteer **instellingen ontvangen**.
Deze eigenschappen op basis van uw overeenkomst met Hallo partner die berichten met u uitwisselt configureren. Zie voor eigenschapbeschrijvingen, Hallo-tabel in deze sectie.

    !['Ontvangen instellingen' configureren](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. U kunt eventueel Hallo eigenschappen van binnenkomende berichten overschrijven door te selecteren **overschrijven berichteigenschappen**.

3. toorequire alle binnenkomende berichten toobe ondertekend, selecteert u **bericht moet worden ondertekend**. Van Hallo **certificaat** , selecteert u een bestaande [Gast partner openbaar certificaat](../logic-apps/logic-apps-enterprise-integration-certificates.md) voor het valideren van de handtekening Hallo op Hallo-berichten. Of maak Hallo certificaat, als u niet hebt.

4.  alle binnenkomende berichten toobe versleuteld, selecteert u toorequire **bericht moet worden versleuteld**. Van Hallo **certificaat** , selecteert u een bestaande [host partner persoonlijk certificaat](../logic-apps/logic-apps-enterprise-integration-certificates.md) voor het ontsleutelen van binnenkomende berichten. Of maak Hallo certificaat, als u niet hebt.

5. toorequire berichten toobe gecomprimeerd, selecteer **bericht moet worden gecomprimeerd**.

6. Selecteer toosend een synchrone disposition melding (MDN) voor ontvangen berichten **MDN verzenden**.

7. toosend ondertekend MDNs ontvangen berichten, selecteer **verzenden ondertekend MDN**.

8. asynchrone MDNs voor ontvangen berichten, selecteert u toosend **verzenden van asynchrone MDN**.

9. Nadat u bent klaar, zorg ervoor dat toosave uw instellingen door te kiezen **OK**.

Nu uw overeenkomst gereed toohandle binnenkomende is berichten die tooyour voldoen instellingen geselecteerd.

| Eigenschap | Beschrijving |
| --- | --- |
| Berichteigenschappen van het overschrijven |Hiermee wordt aangegeven dat eigenschappen ontvangen berichten kunnen worden genegeerd. |
| Het bericht moet ondertekend zijn |Vereist berichten toobe digitaal zijn ondertekend. Configureer Hallo Gast partner openbaar certificaat voor handtekeningverificatie.  |
| Het bericht moet worden versleuteld |Berichten toobe versleuteld vereist. Niet-versleutelde berichten worden geweigerd. Hallo host partner persoonlijk certificaat voor het ontsleutelen van Hallo-berichten configureren.  |
| Het bericht moet worden gecomprimeerd |Berichten toobe gecomprimeerd vereist. Niet-gecomprimeerde berichten worden geweigerd. |
| MDN tekst |Hallo standaard bericht disposition melding (MDN) toobe afzender toohello-bericht verzonden. |
| MDN verzenden |Vereist MDNs toobe verzonden. |
| Ondertekende MDN verzenden |Vereist MDNs toobe ondertekend. |
| MIC-algoritme |Selecteer Hallo algoritme toouse voor het ondertekenen van berichten. |
| Asynchrone MDN verzenden | Vereist berichten toobe asynchroon worden verzonden. |
| URL | Geef waar toosend MDNs Hallo Hallo-URL. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configureren hoe uw overeenkomst verzendt berichten

U kunt configureren hoe deze overeenkomst identificeert en uitgaande berichten die u tooyour partners via deze overeenkomst verzendt worden verwerkt.

1.  Onder **toevoegen**, selecteer **instellingen voor verzenden**.
Deze eigenschappen op basis van uw overeenkomst met Hallo partner die berichten met u uitwisselt configureren. Zie voor eigenschapbeschrijvingen, Hallo-tabel in deze sectie.

    ![Hallo 'Instellingen verzenden' eigenschappen instellen](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. toosend ondertekende berichten tooyour partner, selecteer **inschakelen ondertekenen van berichten**. Voor het ondertekenen van Hallo-berichten in Hallo **MIC algoritme** lijst, selecteer Hallo *host partner persoonlijk certificaat MIC algoritme*. En in Hallo **certificaat** , selecteert u een bestaande [host partner persoonlijk certificaat](../logic-apps/logic-apps-enterprise-integration-certificates.md).

3. toosend versleutelde berichten toohello partner, selecteer **berichtversleuteling inschakelen**. Voor het versleutelen van Hallo-berichten in Hallo **versleutelingsalgoritme** lijst, selecteer Hallo *Gast partner openbaar certificaat algoritme*.
En in Hallo **certificaat** , selecteert u een bestaande [Gast partner openbaar certificaat](../logic-apps/logic-apps-enterprise-integration-certificates.md).

4. toocompress Hallo-bericht, selecteer **bericht compressie inschakelen**.

5. toounfold hello HTTP content-type-header in één regel, selecteer **uitgevouwen HTTP-headers**.

6. tooreceive synchrone MDNs voor Hallo verzonden berichten, selecteer **MDN aanvragen**.

7. tooreceive ondertekend MDNs voor Hallo verzonden berichten, selecteer **aanvraag ondertekend MDN**.

8. tooreceive asynchrone MDNs voor Hallo verzonden berichten, selecteer **aanvragen asynchrone MDN**. Als u deze optie selecteert, moet u Hallo-URL opgeven voor waar toosend MDNs Hallo.

9. toorequire niet-afwijzing van ontvangst, selecteer **NRR inschakelen**.  

10. toospecify algoritme indeling toouse in Hallo MIC of aanmelden Hallo uitgaande kopteksten van AS2 Hallo-bericht of MDN, selecteert u **SHA2 algoritme indeling**.  

11. Nadat u bent klaar, zorg ervoor dat toosave uw instellingen door te kiezen **OK**.

De overeenkomst is nu gereed toohandle uitgaande berichten die tooyour geselecteerd instellingen voldoen.

| Eigenschap | Beschrijving |
| --- | --- |
| Ondertekenen van berichten inschakelen |Vereist dat alle berichten die worden verzonden vanuit Hallo overeenkomst toobe ondertekend. |
| MIC-algoritme |Hallo-algoritme toouse voor het ondertekenen van berichten. Hallo host partner persoonlijk certificaat MIC-algoritme configureert voor het ondertekenen van Hallo-berichten. |
| Certificaat |Selecteer Hallo certificaat toouse voor het ondertekenen van berichten. Hallo host partner persoonlijk certificaat voor ondertekening van Hallo-berichten configureert. |
| Berichtcodering inschakelen |Versleuteling van alle berichten die worden verzonden vanuit deze overeenkomst is vereist. Hallo Gast partner openbaar certificaat algoritme voor het versleutelen van Hallo-berichten configureert. |
| Versleutelingsalgoritme |Hallo versleuteling algoritme toouse voor berichtversleuteling. Hallo Gast partner openbaar certificaat voor het versleutelen van Hallo-berichten configureert. |
| Certificaat |Hallo certificaat toouse tooencrypt berichten. Hallo Gast partner persoonlijk certificaat voor het versleutelen van Hallo-berichten configureert. |
| Bericht compressie inschakelen |Compressie van alle berichten die worden verzonden vanuit deze overeenkomst is vereist. |
| HTTP-headers uitgevouwen |Hallo HTTP content-type-header op één regel plaatst. |
| Aanvraag MDN |Vereist een MDN voor alle berichten die van deze overeenkomst worden verzonden. |
| Aanvraag MDN ondertekend |Vereist dat alle MDNs die toothis overeenkomsten toobe worden verzonden. |
| Asynchrone MDN aanvraag |Asynchrone MDNs toobe verzonden toothis overeenkomst is vereist. |
| URL |Geef waar toosend MDNs Hallo Hallo-URL. |
| NRR inschakelen |Vereist dat niet-afwijzing van ontvangst (NRR), een communicatiekenmerk dat die gegevens Hallo bewijst geadresseerd is ontvangen. |
| SHA2 algoritme-indeling |Algoritme indeling toouse in Hallo MIC of aanmelden Hallo uitgaande kopteksten van AS2 het Hallo-bericht of MDN selecteren |

## <a name="find-your-created-agreement"></a>De overeenkomst zoeken

1.  Als u klaar bent met het instellen van alle uw overeenkomst-eigenschappen op Hallo **toevoegen** blade kiezen **OK** toofinish maken van de overeenkomst en de blade return tooyour integratie-account.

    Nu uw toegevoegde overeenkomst wordt weergegeven in uw **overeenkomsten** lijst.

2.  U kunt ook uw overeenkomsten weergeven in uw Accountoverzicht integratie. Kies op de blade van het integratie-account **overzicht**, selecteer daarna Hallo **overeenkomsten** tegel. 

    ![Kies 'Overeenkomsten' tegel tooview alle overeenkomsten](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a>Weergave Hallo swagger
Zie Hallo [swagger details](/connectors/as2/). 

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")  
