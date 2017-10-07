---
title: de gegevensbronnen aaaAccess on-premises voor Azure Logic Apps | Microsoft Docs
description: Hallo lokale gegevensgateway instellen, zodat u toegang hebt tot gegevensbronnen on-premises vanuit logic apps
keywords: toegang tot gegevens, op de lokale, gegevensoverdracht, versleuteling en gegevensbronnen
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a>Toegang tot gegevensbronnen on-premises vanuit logic apps met Hallo lokale gegevensgateway

de gegevensbronnen tooaccess on-premises van logic apps, instellen van een lokale gegevensgateway die logische apps met ondersteunde connectors kunnen gebruiken. Hallo gateway fungeert als een brug waarmee snelle gegevensoverdracht en -versleuteling tussen gegevensbronnen on-premises en uw logische apps. Hallo gateway doorstuurt gegevens van lokale bronnen op gecodeerde kanalen via hello Azure Service Bus. Al het verkeer afkomstig is als beveiligde uitgaand verkeer van Hallo gateway agent. Meer informatie over [de werking van de gegevensgateway Hallo](logic-apps-gateway-install.md#gateway-cloud-service). 

Hallo-gateway ondersteunt verbindingen toothese gegevensbronnen on-premises:

*   BizTalk Server 2016
*   DB2  
*   Bestandssysteem
*   Informix
*   MQ
*   MySQL
*   Oracle Database
*   PostgreSQL
*   SAP-toepassingsserver 
*   SAP-berichtenserver
*   SharePoint
*   SQL Server
*   Teradata

Deze stappen laten zien hoe tooset up Hallo lokale gegevens gateway toowork met uw logische apps. Zie voor meer informatie over ondersteunde connectors [Connectors voor Azure Logic Apps](../connectors/apis-list.md). 

Zie voor informatie over hoe toouse Hallo gateway met andere services, deze artikelen:

*   [Microsoft Power BI lokale gegevensgateway](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure Analysis Services op locatie gegevensgateway](../analysis-services/analysis-services-gateway.md)
*   [Microsoft-Flow lokale gegevensgateway](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Microsoft PowerApps lokale gegevensgateway](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>Vereisten

* U moet al hebben [Hallo data gateway geïnstalleerd op een lokale computer](logic-apps-gateway-install.md).

* Wanneer u zich aanmeldt toohello Azure-portal, hebt u toouse Hallo dezelfde werk- of schoolaccount dat is gebruikt te[Hallo lokale gegevensgateway installeren](logic-apps-gateway-install.md#requirements). Uw account moet ook een Azure-abonnement toouse hebben wanneer u een gateway-resource in hello Azure-portal voor uw gateway-installatie maakt.

* De gateway-installatie kan niet al door een Azure-gateway-resource wordt geclaimd. U kunt uw gateway installatie tooonly één Azure-gateway resource koppelen. Claim gebeurt wanneer u Hallo gateway resource maken zodat Hallo-installatie niet beschikbaar voor andere bronnen is.

## <a name="set-up-hello-data-gateway-connection"></a>Hallo data gateway-verbinding instellen

### <a name="1-install-hello-on-premises-data-gateway"></a>1. Hallo lokale gegevensgateway installeren

Als u nog niet gedaan hebt, volgt u Hallo [stappen tooinstall Hallo lokale gegevensgateway](logic-apps-gateway-install.md). Voordat u met de Hallo doorgaat andere stappen, zorgt u ervoor dat u Hallo data gateway geïnstalleerd op een lokale computer.

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a>2. Een Azure-resource voor Hallo lokale gegevensgateway maken

Nadat u Hallo gateway geïnstalleerd op een lokale computer, moet u uw data gateway maken als een resource in Azure. Uw gateway-resource koppelt in deze stap ook aan uw Azure-abonnement.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com "Azure-portal"). Zorg ervoor dat toouse Hallo dezelfde Azure werk of school e-mailadres tooinstall Hallo gateway gebruikt.

2. Op Hallo linkermenu in Azure, kiest u **nieuw** > **Enterprise Integration** > **On-premises gegevensgateway** als volgt te werk:

   !['On-premises data gateway' vinden](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. Op Hallo **verbinding-gateway maken** blade bieden deze toocreate details van uw data gateway resource:

    * **Naam**: Voer een naam voor uw gateway-resource. 

    * **Abonnement**: Selecteer Hallo tooassociate Azure-abonnement met uw gateway-resource. 
    Dit abonnement moet hetzelfde abonnement als uw logische app Hallo.
   
      Hallo standaardabonnement is gebaseerd op Hallo Azure-account waarmee u toosign in.

    * **Resourcegroep**: een resourcegroep maken of een bestaande resourcegroep selecteren voor het implementeren van uw gateway-resource. 
    Resourcegroepen kunnen u gerelateerde Azure activa beheren als een verzameling.

    * **Locatie**: Azure beperkt deze locatie toohello dezelfde regio die is geselecteerd voor het gateway-cloudservice Hallo tijdens [gateway-installatie](logic-apps-gateway-install.md). 

      > [!NOTE]
      > Zorg ervoor dat Hallo gateway Resourcelocatie overeenkomt met Hallo gateway cloud servicelocatie. De gateway-installatie mogelijk anders niet weergegeven in de lijst met de Hallo geïnstalleerd gateways voor u tooselect in de volgende stap Hallo.
      > 
      > U kunt verschillende regio's gebruiken voor uw gateway-resource en voor uw logische app.

    * **De naam van de installatie**: als uw gateway-installatie niet is geselecteerd, selecteert u Hallo-gateway die u eerder hebt geïnstalleerd. 

    tooadd hello gateway resource tooyour Azure-dashboard, kies **pincode toodashboard**. 
    Als u bent klaar, kiest u **maken**.

    Bijvoorbeeld:

    ![Geef details toocreate uw on-premises gegevensgateway](./media/logic-apps-gateway-connection/createblade.png)

    toofind of weergave uw data gateway op elk gewenst moment in hello Azure links hoofdmenu te gaan **meer Services** > **Enterprise Integration** > **On-premises gegevens Gateways**.

    ![Ga te 'Meer services', 'Enterprise Integration', 'On-premises gegevensgateways'](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a>3. Verbinding maken met uw logische app toohello lokale gegevensgateway

Nu dat u hebt uw data gateway resource gemaakt en die uw Azure-abonnement is gekoppeld aan deze resource, maak een verbinding tussen uw logische app en Hallo data gateway.

> [!NOTE]
> De locatie van uw gateway verbinding moet aanwezig zijn in Hallo dezelfde regio bevinden als uw logische app, maar u kunt een data gateway die voorkomt in een andere regio.

1. Maak in hello Azure-portal, of open uw logische app in Logic App-ontwerper.

2. Toevoegen van een connector die ondersteuning biedt voor lokale verbindingen, zoals SQL Server.

3. Hallo-volgorde wordt weergegeven, selecteert u **verbinden via lokale gegevensgateway**, Geef een unieke verbindingsnaam Hallo vereiste informatie en selecteer Hallo data gateway resource die u toouse wilt. Als u bent klaar, kiest u **maken**.

   > [!TIP]
   > Een unieke verbindingsnaam kunt u gemakkelijk herkennen die verbinding later, vooral wanneer u meerdere verbindingen maken. Indien van toepassing, moet u ook Hallo gekwalificeerde domeinnaam voor uw gebruikersnaam bevatten. 

   ![Verbinding maken tussen logic app en data gateway](./media/logic-apps-gateway-connection/blankconnection.png)

Gefeliciteerd, uw gatewayverbinding is nu gereed voor uw logische app toouse.

## <a name="edit-your-gateway-connection-settings"></a>De instellingen voor de gateway-verbinding bewerken

Nadat u een gatewayverbinding voor uw logische app maakt, kunt u toolater update Hallo-instellingen voor die specifieke verbinding.

1. toofind hello gatewayverbinding:

   * Op Hallo logic app blade onder **ontwikkelingsprogramma's**, selecteer **API verbindingen**. 
   
     Hallo **API verbindingen** deelvenster ziet u alle API-verbindingen die zijn gekoppeld aan uw logische app, inclusief gatewayverbindingen.

     ![Ga tooyour logische app, selecteert u 'API verbindingen'](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * Of Ga te hello Azure links hoofdmenu en **meer Services** > **Web- en Mobile Services** > **API verbindingen** voor alle API-verbindingen inclusief gatewayverbindingen die gekoppeld aan uw Azure-abonnement zijn. 

   * Of Ga te op Hallo belangrijkste Azure linkermenu**alle resources** voor alle API-verbindingen, inclusief gatewayverbindingen die gekoppeld aan uw Azure-abonnement zijn.

2. Selecteer Hallo gatewayverbinding wilt tooview of bewerken en kies **API bewerken verbinding**.

   > [!TIP]
   > Als u de updates worden niet doorgevoerd, probeert u [stoppen en opnieuw starten van de gatewayservice Windows hello](./logic-apps-gateway-install.md#restart-gateway).

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>Schakelt u of uw lokale gegevens gateway bron verwijderen

toocreate een andere gateway-resource, uw gateway koppelen aan een andere resource of Hallo gateway resource verwijdert, kunt u Hallo gateway resource verwijderen zonder gevolgen voor Hallo gateway-installatie. 

1. Hello Azure links hoofdmenu en ga te**alle resources**. 
2. Zoek en selecteer uw data gateway-resource.
3. Kies **On-premises Data Gateway**, en kies op Hallo resource werkbalk **verwijderen**.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Veelgestelde vragen

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>Volgende stappen

* [Uw logische apps beveiligen](./logic-apps-securing-a-logic-app.md)
* [Algemene voorbeelden en scenario's voor logic apps](./logic-apps-examples-and-scenarios.md)
