---
title: aaaCreate partners voor berichten in business-to-business (B2B) - Azure Logic Apps | Microsoft Docs
description: Meer informatie over hoe tooadd partners tooyour integratie met Enterprise Integration Pack Hallo en Logic Apps-account
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a>Toevoegen of bijwerken van partners in uw werkstroom business-to-business-overeenkomsten

Partners zijn entiteiten die deelnemen aan business-to-business (B2B) transacties en uitwisselen van berichten tussen elkaar. Voordat u partners die u en een andere organisatie deze transacties vertegenwoordigen maken kunt, moet u beide delen van gegevens die u identificeert en berichten is verzonden door elkaar worden gevalideerd. Nadat u deze gegevens worden behandeld en u klaar toostart uw zakelijke relatie bent, kunt u partners in uw account integratie toorepresent u beide.

## <a name="what-roles-do-partners-have-in-your-integration-account"></a>Welke rollen hebt partners in uw integratie-account?

toodefine informatie over het Hallo-berichten uitgewisseld tussen partners, maakt u overeenkomsten tussen de partners. Echter, voordat u een overeenkomst maken kunt, moet u hebben toegevoegd ten minste twee partners tooyour integratie-account. Uw organisatie moet deel uitmaken van de overeenkomst Hallo als Hallo **host partner**. Hallo andere partner of **Gast partner** vertegenwoordigt Hallo organisatie die berichten met uw organisatie worden uitgewisseld. Hallo Gast partner kan zijn van een ander bedrijf, of zelfs een afdeling in uw eigen organisatie.

Nadat u deze partners hebt toegevoegd, kunt u een overeenkomst kunt maken.

Ontvangen en verzenden van de instellingen zijn gericht uit oogpunt Hallo Hallo gehoste Partner. Bijvoorbeeld, Hallo instellingen in een overeenkomst ontvangen bepalen hoe Hallo gehost partner ontvangt berichten die worden verzonden vanaf een partner Gast. Op dezelfde manier Hallo verzendinstellingen op Hallo overeenkomst aangeven hoe Hallo gehost partner verzendt berichten toohello Gast partner.

## <a name="how-toocreate-a-partner"></a>Hoe toocreate een partner?

1. Selecteer in de Azure-portal hello, **Bladeren**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Voer in het zoekvak Hallo-filter, **integratie**, selecteer daarna **Integratieaccounts** in de lijst met resultaten Hallo.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Selecteer Hallo integratie account waar u tooadd uw partners.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Selecteer Hallo **Partners** tegel.

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. Kies in de blade Hallo Partners **toevoegen**.

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. Voer een naam voor uw partner en selecteer vervolgens een **kwalificatie**. Voer ten slotte een **waarde** toohelp documenten die worden geleverd in uw apps bepalen.

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. toosee hello uitgevoerd voor uw partner-maakproces Selecteer Hallo *bel* meldingspictogram.

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. tooconfirm die uw nieuwe partners zijn toegevoegd, selecteer Hallo **Partners** tegel.

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    Nadat u Hallo Partners tegel selecteert, ziet u ook toegevoegde partners Hallo Partners blade.

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a>Hoe tooedit bestaande partners in uw account integratie

1. Selecteer Hallo **Partners** tegel.
2. Nadat het Hallo Partners blade wordt geopend, selecteert u Hallo partner die u wilt dat tooedit.
3. Op Hallo **Update Partner** tegel, breng uw wijzigingen.
4. Nadat u bent klaar, kiest u **opslaan**, of selecteert u uw wijzigingen toocancel **negeren**.

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a>Hoe toodelete een partner

1. Selecteer Hallo **Partners** tegel.
2. Nadat het Hallo Partner blade wordt geopend, selecteert u Hallo partner die u toodelete wilt.
3. Kies **verwijderen**.

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over de overeenkomsten](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  

