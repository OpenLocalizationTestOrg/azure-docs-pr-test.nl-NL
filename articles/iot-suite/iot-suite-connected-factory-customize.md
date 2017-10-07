---
title: Azure IoT Suite aaaCustomize verbonden factory | Microsoft Docs
description: Een beschrijving van hoe toocustomize Hallo gedrag van Hallo factory verbonden vooraf geconfigureerde oplossing.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Aanpassen hoe Hallo factory oplossing geeft gegevens van uw servers OPC UA verbonden

## <a name="introduction"></a>Inleiding

Hallo verbonden factory oplossing samenvoegt en gegevens uit Hallo OPC UA servers verbonden toohello oplossing worden weergegeven. U kunt bladeren en het verzenden van de opdrachten toohello OPC UA servers in uw oplossing. Zie voor meer informatie over OPC UA Hallo [verbonden factory Veelgestelde vragen over](iot-suite-faq-cf.md).

Voorbeelden van geaggregeerde gegevens in het Hallo-oplossing zijn Hallo algehele apparatuur efficiëntie (OEE) en de Key Performance Indicators (KPI's) die u in het Hallo-dashboard Hallo factory-, lijn- en station niveaus bekijken kunt. Hallo volgende schermafbeelding ziet u Hallo OEE en KPI-waarden voor Hallo **Assembly** station op **productie-regel 1**, in Hallo **München** factory:

![Voorbeeld van OEE en KPI waarden in Hallo-oplossing][img-oee-kpi]

Hallo-oplossing kunt u tooview gedetailleerde gegevens van specifieke gegevensitems uit Hallo OPC UA-servers, zogenaamde *stations*. Hallo ziet volgende schermafbeelding curve van Hallo aantal geproduceerde items van een specifiek station:

![Curve van het aantal geproduceerde artikelen][img-manufactured-items]

Als u klikt op een van de grafieken hello, vindt u Hallo gegevens verder met Time Series Insights (TSI):

![Gegevens met behulp van de Time Series Insights verkennen][img-tsi]

Dit artikel wordt beschreven:

- Hoe bestaat gegevens Hallo beschikbaar toohello verschillende weergaven in Hallo-oplossing.
- Het aanpassen van Hallo manier Hallo oplossing Hallo gegevens weergegeven.

## <a name="data-sources"></a>Gegevensbronnen

Hallo verbonden factory-oplossing worden gegevens uit Hallo OPC UA servers verbonden toohello oplossing. Hallo standaardinstallatie bevat verschillende OPC UA-servers met een factory simulatie. U kunt uw eigen servers OPC UA toevoegen die [verbinding maken via een gateway] [ lnk-connect-cf] tooyour oplossing.

U kunt bladeren Hallo gegevensitems verbonden OPC UA-server kunt tooyour oplossing in een dashboard Hallo verzenden:

1. Navigeer toohello **selecteert u een server OPC UA** weergeven:

    ![Selecteer een weergave van de server OPC UA toohello navigeren][img-select-server]

1. Selecteer een server en klik op **Connect**. Klik op **doorgaan** wanneer Hallo beveiligingswaarschuwing wordt weergegeven.

    > [!NOTE]
    > Deze waarschuwing alleen verschijnt eenmaal voor elke server en er wordt een vertrouwensrelatie tussen Hallo oplossing dashboard en Hallo-server.

1. U kunt nu bladeren Hallo-gegevensitems die server Hallo toohello oplossing kunnen verzenden. Items die worden verzonden toohello oplossing hebben een groen vinkje:

    ![Gepubliceerde items][img-published]

1. Als u een *beheerder* in Hallo-oplossing, kunt u toopublish een item gegevens toomake deze beschikbaar zijn in Hallo verbonden factory-oplossing. U kunt ook Hallo-waarde van gegevensitems wijzigen en methoden aanroepen in Hallo OPC UA-server als beheerder.

## <a name="map-hello-data"></a>Hallo kaartgegevens

Hallo verbonden factory oplossing maps en statistische functies Hallo gepubliceerde gegevensitems van Hallo OPC UA-server toohello verschillende weergaven in Hallo-oplossing. Hallo implementeert verbonden factory-oplossing tooyour Azure-account wanneer u Hallo oplossing inricht. Een JSON-bestand in Visual Studio verbonden factory-oplossing Hallo slaat deze informatie over de Identiteitstoewijzing. U kunt weergeven en wijzigen van dit JSON-configuratiebestand in Hallo verbonden fabriek Visual Studio-oplossing. U kunt de Hallo oplossing opnieuw te implementeren nadat u een wijziging aanbrengt.

U kunt Hallo-configuratiebestand te gebruiken:

- Hallo bestaande gesimuleerde fabrieken, de regels voor productie en de stations bewerken.
- Gegevens van echte OPC UA-servers dat u verbinding toohello oplossing maakt toewijzen.

een kopie van Hallo tooclone verbonden factory Visual Studio-oplossing, gebruik Hallo volgende git-opdracht:

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

Hallo bestand **ContosoTopologyDescription.json** Hallo toewijzing van Hallo OPC UA-servergegevens items toohello weergaven in Hallo verbonden factory oplossing dashboard definieert. U vindt dit configuratiebestand in Hallo **Contoso\Topology** map in Hallo **WebApp** -project in Visual Studio-oplossing Hallo.

Hallo-inhoud van het Hallo JSON-bestand is ingedeeld als een hiërarchie van de factory-, productie-lijn- en station knooppunten. Deze hiërarchie definieert Hallo navigatiehiërarchie in Hallo verbonden factory dashboard. Waarden op elk knooppunt van de hiërarchie Hallo bepalen Hallo informatie die wordt weergegeven in het Hallo-dashboard. Hallo JSON-bestand bevat bijvoorbeeld Hallo waarden voor Hallo München factory te volgen:

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

Hallo-naam, beschrijving en locatie worden weergegeven op deze weergave in Hallo dashboard:

![München gegevens in Hallo-dashboard][img-munich]

Elke factory-, productie-lijn- en station hebt een eigenschap van de afbeelding. U vindt deze JPEG-bestanden in Hallo **Content\img** map in Hallo **WebApp** project. Deze installatiekopiebestanden weergeven in Hallo verbonden factory dashboard.

Elk station bevat verschillende gedetailleerde eigenschappen waarmee Hallo toewijzing van Hallo OPC UA gegevensitems definiëren. Deze eigenschappen worden beschreven in Hallo uit te voeren:

### <a name="opcuri"></a>OpcUri

Hallo **OpcUri** waarde Hallo OPC UA toepassing URI die een unieke identificatie van Hallo OPC UA-server is. Bijvoorbeeld, Hallo **OpcUri** Hallo assembly station op productie regel 1 in München ziet eruit als Hallo volgende waarde: **urn: scada2194:ua:munich:productionline0:assemblystation**.

Hallo URI's van Hallo verbonden OPC UA servers vindt u in het dashboard van de oplossing Hallo:

![Het OPC UA-server URI's weergeven][img-server-uris]

### <a name="simulation"></a>Simulatie

informatie in Hallo Hallo **simulatie** knooppunt is specifiek toohello OPC UA simulatie die wordt uitgevoerd in Hallo OPC UA-servers die standaard zijn ingericht. Dit wordt niet gebruikt voor een echte OPC UA-server.

### <a name="kpi1-and-kpi2"></a>Kpi1 en Kpi2

Deze knooppunten wordt beschreven hoe gegevens van Hallo station bijdraagt toohello twee KPI-waarden in Hallo-dashboard. Deze KPI-waarden zijn in een standaardimplementatie eenheden per uur en kWh per uur. Hallo oplossing berekent de waarden van de KPI op Hallo niveau van een station en ze aggregeert Hallo productieregel en factory niveaus.

Elke KPI heeft een minimum, maximum- en doel-waarde. Elke KPI-waarde kunt ook meldingen voor Hallo verbonden factory oplossing tooperform definiëren. Hallo volgende fragment toont Hallo KPI definities voor Hallo assembly station op productie-regel 1 in München:

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

Hallo volgende schermafbeelding ziet u Hallo KPI-gegevens in Hallo-dashboard.

![KPI-gegevens in Hallo-dashboard][lnk-kpi]

### <a name="opcnodes"></a>OpcNodes

Hallo **OpcNodes** knooppunten identificeren Hallo gepubliceerde-gegevensitems van Hallo OPC UA-server en opgeven hoe tooprocess die gegevens.

Hallo **NodeId** waarde identificeert Hallo specifieke OPC UA NodeID van Hallo OPC UA-server. Hallo eerste knooppunt in Hallo assembly station voor productie-regel 1 in München heeft een waarde **ns = 2; ik 385 =**. Een **NodeId** waarde geeft aan Hallo gegevens item tooread van Hallo OPC UA-server en Hallo **symbolische naam** biedt een gebruiksvriendelijke naam toouse in Hallo dashboard voor die gegevens.

Andere waarden die zijn gekoppeld aan elk knooppunt worden samengevat in de volgende tabel Hallo:

| Waarde | Beschrijving |
| ----- | ----------- |
| Relevantie  | Hallo KPI en OEE waarden deze gegevens draagt bij aan. |
| OpCode     | Hoe Hallo gegevens worden samengevoegd. |
| Eenheden      | Hallo eenheden toouse in Hallo-dashboard.  |
| Zichtbaar    | Of toodisplay deze waarde in Hallo-dashboard. Sommige waarden worden gebruikt voor berekeningen, maar niet weergegeven.  |
| Maximum    | Hallo maximumwaarde die een waarschuwing in Hallo dashboard activeert. |
| MaximumAlertActions | Een actie tootake in antwoord tooan waarschuwing. Bijvoorbeeld: een opdracht tooa station verzenden. |
| ConstValue | Een constante waarde die wordt gebruikt in een berekening. |

## <a name="deploy-hello-changes"></a>Hallo wijzigingen implementeren

Wanneer u toohello wijzigingen hebt aangebracht **ContosoTopologyDescription.json** -bestand, die u moet implementeren Hallo verbonden factory oplossing tooyour Azure-account.

Hallo **azure-iot-verbonden-factory** opslagplaats bevat een **build.ps1** PowerShell-script kunt u toorebuild gebruiken en Hallo oplossing implementeren.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over Hallo verbonden factory vooraf geconfigureerde oplossing door lezen Hallo artikelen te volgen:

* [Overzicht van de vooraf geconfigureerde oplossing voor verbonden factory's][lnk-rm-walkthrough]
* [Implementeer een gateway voor verbonden factory][lnk-connect-cf]
* [Machtigingen op Hallo azureiotsuite.com site][lnk-permissions]
* [Veelgestelde vragen over verbonden factory's](iot-suite-faq-cf.md)
* [FAQ][lnk-faq]


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md