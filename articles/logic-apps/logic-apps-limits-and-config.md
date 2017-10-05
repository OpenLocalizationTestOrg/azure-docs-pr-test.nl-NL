---
title: Logic App en -configuratie | Microsoft Docs
description: Overzicht van de grenzen van de service en de configuratiewaarden beschikbaar voor Logic Apps.
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: da23bd9fe71a0c41bc236b55bc9f56e123a9d77a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="logic-app-limits-and-configuration"></a>Limieten en configuratie van logische apps

Hieronder vindt u informatie over de huidige limieten en de configuratie-informatie voor Azure Logic Apps.

## <a name="limits"></a>Limieten

### <a name="http-request-limits"></a>Limieten voor HTTP-aanvraag

Hieronder vindt u limieten voor één HTTP-aanvraag en/of de connector aanroep.

#### <a name="timeout"></a>Time-out

|Naam|Limiet|Opmerkingen|
|----|----|----|
|Time-out aanvraag|120 seconden|Een [asynchrone patroon](../logic-apps/logic-apps-create-api-app.md) of [tot lus](logic-apps-loops-and-scopes.md) kunt compenseren indien nodig|

#### <a name="message-size"></a>Berichtgrootte

|Naam|Limiet|Opmerkingen|
|----|----|----|
|Berichtgrootte|100 MB|Sommige connectors en API's mogelijk niet ondersteund op 100 MB |
|Expressie evaluatie limiet|131.072 tekens|`@concat()`, `@base64()`, `string` mag niet langer zijn dan deze limiet|

#### <a name="retry-policy"></a>Beleid voor opnieuw proberen

|Naam|Limiet|Opmerkingen|
|----|----|----|
|Nieuwe pogingen|10| De standaardwaarde is 4. Kunt configureren met de [parameter van het beleid opnieuw](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|
|Maximale tijd tussen elke poging|1 uur|Kunt configureren met de [parameter van het beleid opnieuw](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|
|Tijd tussen elke poging min|5 per seconde|Kunt configureren met de [parameter van het beleid opnieuw](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|

### <a name="run-duration-and-retention"></a>Voer duur en retentie

Hier volgen de limieten voor een enkele logische-app uitvoeren.

|Naam|Limiet|Opmerkingen|
|----|----|----|
|Duur uitvoering|90 dagen||
|Bewaren van opslag|90 dagen|De begintijd voor uitvoeren vanaf|
|Terugkeerpatroon min|1 per seconde|| 15 seconden voor logic apps met App Service-Plan
|Maximale terugkeerpatroon|500 dagen||

Als u van plan bent maximaal uitvoeren duration of bewaren opslaglimieten in normale verwerking stroom, [contact met ons opnemen](mailto://logicappsemail@microsoft.com) zodat we bij uw behoeften helpen kan.


### <a name="looping-and-debatching-limits"></a>Lussen en limieten debatching

Hieronder vindt u limieten voor een enkele logische-app uitvoeren.

|Naam|Limiet|Opmerkingen|
|----|----|----|
|ForEach-items|100,000|U kunt de [query actie](../connectors/connectors-native-query.md) voor het filteren van grotere matrices indien nodig|
|Pas iteraties|5,000||
|SplitOn items|100,000||
|ForEach parallelle uitvoering|50| De standaardwaarde is 20. U kunt instellen op een sequentiële foreach door toe te voegen `"operationOptions": "Sequential"` naar de `foreach` actie of een specifiek niveau van het gebruik van parallelle uitvoering`runtimeConfiguration`|


### <a name="throughput-limits"></a>Doorvoerlimieten

Hieronder vindt u limieten voor een enkele logic app-exemplaar. 

|Naam|Limiet|Opmerkingen|
|----|----|----|
|Acties uitvoeringen per 5 minuten |100,000|Werkbelasting kunt voor meerdere apps naar behoefte distribueren|
|Acties gelijktijdige uitgaande oproepen |~2,500|Verminder het aantal gelijktijdige aanvragen of verkorten indien nodig|
|Runtime-eindpunt gelijktijdige binnenkomende oproepen |~1,000|Verminder het aantal gelijktijdige aanvragen of verkorten indien nodig|
|Runtime-eindpunt lezen aanroepen per 5 minuten |60,000|Werkbelasting kunt voor meerdere apps naar behoefte distribueren|
|Runtime-eindpunt aanroepen aanroepen per 5 minuten |45,000|Werkbelasting kunt voor meerdere apps naar behoefte distribueren|

Als u verwacht dat deze limiet in normale verwerking overschrijdt of willen uitvoeren load tests die overschrijdt deze limiet voor een periode, misschien [contact met ons opnemen](mailto://logicappsemail@microsoft.com) zodat we bij uw behoeften helpen kan.

### <a name="definition-limits"></a>Definitie-limieten

Hieronder vindt u limieten voor een definitie van één logische app.

|Naam|Limiet|Opmerkingen|
|----|----|----|
|Acties per werkstroom|500|U kunt geneste werkstromen om uit te breiden deze limiet naar behoefte toevoegen|
|Diepte van het nesten actie toegestaan|8|U kunt geneste werkstromen om uit te breiden deze limiet naar behoefte toevoegen|
|Werkstromen per regio per abonnement|1000||
|Triggers per werkstroom|10||
|Switch bereik gevallen limiet|25||
|Aantal variabelen per werkstroom|250||
|Maximum aantal tekens per expressie|8.192||
|Maximale `trackedProperties` grootte in tekens|16,000|
|`action`/`trigger`limiet voor de naam|80||
|`description`lengtelimiet|256||
|`parameters`limiet|50||
|`outputs`limiet|10||

### <a name="integration-account-limits"></a>Limieten van integratie

Hieronder vindt u limieten voor artefacten toegevoegd aan de integratie van Account

|Naam|Limiet|Opmerkingen|
|----|----|----|
|Schema|8 MB|U kunt [blob-URI](logic-apps-enterprise-integration-schemas.md) voor het uploaden van bestanden groter dan 2 MB |
|Kaart (XSLT-bestand)|2 MB| |
|Runtime-eindpunt lezen aanroepen per 5 minuten |60,000|Werkbelasting kunt verdelen over meerdere accounts zo nodig|
|Runtime-eindpunt aanroepen aanroepen per 5 minuten |45,000|Werkbelasting kunt verdelen over meerdere accounts zo nodig|
|Runtime-eindpunt bijhouden aanroepen per 5 minuten |45,000|Werkbelasting kunt verdelen over meerdere accounts zo nodig|
|Runtime-eindpunt voor het blokkeren van gelijktijdige aanroepen |~1,000|Verminder het aantal gelijktijdige aanvragen of verkorten indien nodig|

### <a name="b2b-protocols-as2-x12-edifact-message-size"></a>Berichtgrootte B2B-protocollen (AS2, X12, EDIFACT)

Hieronder vindt u de limieten voor B2B-protocollen

|Naam|Limiet|Opmerkingen|
|----|----|----|
|AS2|50 MB|Van toepassing op decoderen en coderen|
|X12|50 MB|Van toepassing op decoderen en coderen|
|EDIFACT|50 MB|Van toepassing op decoderen en coderen|

## <a name="configuration"></a>Configuratie

### <a name="ip-address"></a>IP-adres

#### <a name="logic-app-service"></a>Logic App Service

Aanroepen vanuit een logische app rechtstreeks (dat wil zeggen, via [HTTP](../connectors/connectors-native-http.md) of [HTTP + Swagger](../connectors/connectors-native-http-swagger.md)) of andere HTTP-aanvragen die afkomstig zijn van het IP-adres dat is opgegeven in de volgende lijst:

|Logic App regio|Uitgaande IP|
|-----|----|
|Australië - oost|13.75.153.66, 104.210.89.222, 104.210.89.244, 13.75.149.4, 104.210.91.55, 104.210.90.241|
|Australië - zuidoost|13.73.115.153, 40.115.78.70, 40.115.78.237, 13.73.114.207, 13.77.3.139, 13.70.159.205|
|Brazilië - zuid|191.235.86.199, 191.235.95.229, 191.235.94.220, 191.235.82.221, 191.235.91.7, 191.234.182.26|
|Canada - midden|52.233.29.92, 52.228.39.241, 52.228.39.244|
|Canada - oost|52.232.128.155, 52.229.120.45, 52.229.126.25|
|Centraal-India|52.172.157.194, 52.172.184.192, 52.172.191.194, 52.172.154.168, 52.172.186.159, 52.172.185.79|
|VS - midden|13.67.236.76, 40.77.111.254, 40.77.31.87, 13.67.236.125, 104.208.25.27, 40.122.170.198|
|Oost-Azië|168.63.200.173, 13.75.89.159, 23.97.68.172, 13.75.94.173, 40.83.127.19, 52.175.33.254|
|VS - oost|137.135.106.54, 40.117.99.79, 40.117.100.228, 13.92.98.111, 40.121.91.41, 40.114.82.191|
|VS - oost 2|40.84.25.234, 40.79.44.7, 40.84.59.136, 40.84.30.147, 104.208.155.200, 104.208.158.174|
|Japan - oost|13.71.146.140, 13.78.84.187, 13.78.62.130, 13.71.158.3, 13.73.4.207, 13.71.158.120|
|Japan - west|40.74.140.173, 40.74.81.13, 40.74.85.215, 40.74.140.4, 104.214.137.243, 138.91.26.45|
|Noord-centraal VS|168.62.249.81, 157.56.12.202, 65.52.211.164, 168.62.248.37, 157.55.210.61, 157.55.212.238|
|Noord-Europa|13.79.173.49, 52.169.218.253, 52.169.220.174, 40.113.12.95, 52.178.165.215, 52.178.166.21|
|Zuid-centraal VS|13.65.98.39, 13.84.41.46, 13.84.43.45, 104.210.144.48, 13.65.82.17, 13.66.52.232|
|Zuidoost-Azië|52.163.93.214, 52.187.65.81, 52.187.65.155, 13.76.133.155, 52.163.228.93, 52.163.230.166|
|Zuid-India|52.172.9.47, 52.172.49.43, 52.172.51.140, 52.172.50.24, 52.172.55.231, 52.172.52.0|
|West-Europa|13.95.155.53, 52.174.54.218, 52.174.49.6, 40.68.222.65, 40.68.209.23, 13.95.147.65|
|West-India|104.211.164.112, 104.211.165.81, 104.211.164.25, 104.211.164.80, 104.211.162.205, 104.211.164.136|
|VS - west|52.160.90.237, 138.91.188.137, 13.91.252.184, 52.160.92.112, 40.118.244.241, 40.118.241.243|
|Verenigd Koninkrijk Zuid|51.140.74.14, 51.140.73.85, 51.140.78.44|
|Verenigd Koninkrijk West|51.141.54.185, 51.141.45.238, 51.141.47.136|

#### <a name="connectors"></a>Connectors

Aanroepen vanuit een [connector](../connectors/apis-list.md) afkomstig zijn van het IP-adres dat is opgegeven in de volgende lijst:

|Logic App regio|Uitgaande IP|
|-----|----|
|Australië - oost|40.126.251.213|
|Australië - zuidoost|40.127.80.34|
|Brazilië - zuid|191.232.38.129|
|Canada - midden|52.233.31.197, 52.228.42.205, 52.228.33.76, 52.228.34.13|
|Canada - oost|52.229.123.98, 52.229.120.178, 52.229.126.202, 52.229.120.52|
|Centraal-India|104.211.98.164|
|VS - midden|40.122.49.51|
|Oost-Azië|23.99.116.181|
|VS - oost|191.237.41.52|
|VS - oost 2|104.208.233.100|
|Japan - oost|40.115.186.96|
|Japan - west|40.74.130.77|
|Noord-centraal VS|65.52.218.230|
|Noord-Europa|104.45.93.9|
|Zuid-centraal VS|104.214.70.191|
|Zuidoost-Azië|13.76.231.68|
|Zuid-India|104.211.227.225|
|West-Europa|40.115.50.13|
|West-India|104.211.161.203|
|VS - west|104.40.51.248|
|Verenigd Koninkrijk Zuid|51.140.80.51|
|Verenigd Koninkrijk West|51.141.47.105|


## <a name="next-steps"></a>Volgende stappen  

- Om te beginnen met Logic Apps, volgt u de [een logische App maken](../logic-apps/logic-apps-create-a-logic-app.md) zelfstudie.  
- [Algemene voorbeelden en scenario's weergeven](../logic-apps/logic-apps-examples-and-scenarios.md)
- [Met Logic Apps kunt u bedrijfsprocessen automatiseren](http://channel9.msdn.com/Events/Build/2016/T694) 
- [Meer informatie over hoe u Logic Apps kunt integreren in uw systemen](http://channel9.msdn.com/Events/Build/2016/P462)
