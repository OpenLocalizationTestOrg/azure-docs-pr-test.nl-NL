---
title: aaaIntroduction tooweb application firewall (WAF) voor Azure Application Gateway | Microsoft Docs
description: Deze pagina bevat een overzicht van Web Application Firewall (WAF) voor Application Gateway
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 04b362bc-6653-4765-86f6-55ee8ec2a0ff
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: amsriva
ms.openlocfilehash: 5a42ce0fb2bd12a391844099e2de8fa2571195e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="web-application-firewall-waf"></a>Web Application Firewall (WAF)

Web Application Firewall (WAF) is een functie van Application Gateway die gecentraliseerde beveiliging van uw webtoepassingen tegen algemene aanvallen en beveiligingsproblemen biedt. 

Web application firewall is gebaseerd op regels uit Hallo [regelsets voor OWASP core](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 of 2.2.9. Webtoepassingen zijn in toenemende mate het doel van aanvallen die gebruikmaken van veelvoorkomende bekende beveiligingsproblemen. Algemene tussen deze aanvallen zijn SQL-injectieaanvallen, tooname enkele cross-site scripting aanvallen. Zo wordt voorkomen dat dergelijke aanvallen in toepassingscode kan lastig zijn en vereisen mogelijk strengere onderhoud, patchen en de controle op meerdere lagen van Hallo Toepassingstopologie. Een gecentraliseerde web application firewall zorgt er beveiligingsbeheer veel eenvoudiger en biedt betere zekerheid tooapplication beheerders tegen bedreigingen of beveiligingsrisico's. Een WAF oplossing kan ook beveiligingsrisico tooa sneller reageren door een bekend beveiligingsprobleem met een centrale locatie en beveiliging van elk van de afzonderlijke webtoepassingen patchen. Bestaande toepassingsgateways kunnen eenvoudig toepassingsgateway voor geconverteerde tooa web application firewall is ingeschakeld worden.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/WAF1.png)

Application Gateway wordt uitgevoerd als een toepassing levering controller en aanbiedingen SSL-beëindiging, sessie cookies gebaseerde affiniteit, round-robinbelastingverdeling, inhoud gebaseerde routering, de mogelijkheid toohost meerdere websites en beveiligingsverbeteringen. Verbeteringen in de beveiliging die worden aangeboden door Application Gateway bevatten beheer van SSL, einde tooend ondersteuning voor SSL. Toepassingsbeveiliging is nu versterkt door WAF (web application firewall) rechtstreeks geïntegreerd in Hallo ADC aanbieding. Dit biedt een centrale locatie eenvoudig tooconfigure toomanage en beveiligen van uw webtoepassingen tegen veelvoorkomende web beveiligingslekken.

## <a name="benefits"></a>Voordelen

Hallo volgen Hallo belangrijkste voordelen van Application Gateway en web application firewall bieden:

### <a name="protection"></a>Beveiliging

* Uw webtoepassing beschermen tegen aanvallen zonder wijziging toobackend code en web beveiligingsproblemen.

* Beveiligen van meerdere web applications op Hallo dezelfde tijd achter een toepassingsgateway. Toepassingsgateway biedt ondersteuning voor hosting van websites too20 achter een enkele gateway die kan worden alle beschermd tegen aanvallen via Internet met WAF.

### <a name="monitoring"></a>Bewaking

* U controleert op aanvallen tegen de webtoepassing door een real-time logboek van WAF te raadplegen. Dit logboek is geïntegreerd met [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md) tootrack WAF waarschuwingen en logboeken en trends gemakkelijk bewaken.

* WAF zal binnenkort worden geïntegreerd met Azure Security Center. Azure Security Center kunt u een centrale weergave van Hallo beveiligingsstatus van alle Azure-resources.

### <a name="customization"></a>Aanpassing

* Hallo mogelijkheid toocustomize WAF regels en regel groepen toosuit uw toepassingsvereisten en fout-positieven te elimineren.

## <a name="features"></a>Functies

Web application firewall is vooraf geconfigureerd met CRS 3.0 standaard of kunt u toouse 2.2.9. Het voordeel van CRS 3.0 is dat er minder fout-positieven worden geregistreerd dan met 2.2.9. de mogelijkheid te Hallo[regels toosuit aanpassen de behoeften van uw](application-gateway-customize-waf-rules-portal.md) is opgegeven. Aantal Hallo veelvoorkomende web beveiligingslekken welke web application firewall wordt beschermd tegen omvat:

* Beveiliging tegen SQL-injecties
* Beveiliging tegen scripting op meerdere sites
* Beveiliging tegen veelvoorkomende aanvallen via internet, zoals opdrachtinjectie, het smokkelen van HTTP-aanvragen, het uitsplitsen van HTTP-antwoorden en aanvallen waarbij een extern bestand wordt ingesloten
* Beveiliging tegen schendingen van het HTTP-protocol
* Beveiliging tegen afwijkingen van het HTTP-protocol, zoals een gebruikersagent voor de host en Accept-headers die ontbreken
* Beveiliging tegen bots, crawlers en scanners
* Detectie van veelvoorkomende onjuiste configuraties van toepassingen (Apache, IIS, enzovoort)

Voor een gedetailleerde lijst met regels en hun beschermingsmaatregelen Zie Hallo volgende [regelsets Core](#core-rule-sets).

### <a name="core-rule-sets"></a>Core Rule Sets

Application Gateway ondersteunt twee regelsets, CRS 3.0 en CRS 2.2.9. Deze Core Rule Sets zijn verzamelingen regels die uw webtoepassingen beschermen tegen schadelijke activiteiten.

#### <a name="owasp30"></a>OWASP_3.0

Hallo 3.0 regel kernset opgegeven heeft 13 regelgroepen zoals weergegeven in de volgende tabel Hallo. Elk van deze regelgroepen bevat meerdere regels, die desgewenst kunnen worden uitgeschakeld.

|Regelgroep|Beschrijving|
|---|---|
|**[REQUEST-910-IP-REPUTATION](application-gateway-crs-rulegroups-rules.md#crs910)**|Regels tooprotect tegen bekende afzenders van spam of schadelijke activiteiten bevat.|
|**[REQUEST-911-METHOD-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs911)**|Bevat de regels toolock methoden (PUT, PATCH <...)|
|**[REQUEST-912-DOS-PROTECTION](application-gateway-crs-rulegroups-rules.md#crs912)**| Bevat de regels tooprotect tegen aanvallen Denial of Service (DoS).|
|**[REQUEST-913-SCANNER-DETECTION](application-gateway-crs-rulegroups-rules.md#crs913)**| Bevat de regels tooprotect tegen scanners poort en de omgeving.|
|**[REQUEST-920-PROTOCOL-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs920)**|Bevat de regels tooprotect tegen protocol en de codering van problemen.|
|**[REQUEST-921-PROTOCOL-ATTACK](application-gateway-crs-rulegroups-rules.md#crs921)**|Bevat de regels tooprotect tegen header injectie, smokkelen aanvraag en antwoord splitsen|
|**[REQUEST-930-APPLICATION-ATTACK-LFI](application-gateway-crs-rulegroups-rules.md#crs930)**|Bevat de regels tooprotect tegen aanvallen van bestands- en pad.|
|**[REQUEST-931-APPLICATION-ATTACK-RFI](application-gateway-crs-rulegroups-rules.md#crs931)**|Bevat de regels tooprotect op basis van het externe bestand opnemen (RFI)|
|**[REQUEST-932-APPLICATION-ATTACK-RCE](application-gateway-crs-rulegroups-rules.md#crs932)**|Bevat de regels tooprotect opnieuw externe Code kan worden uitgevoerd.|
|**[REQUEST-933-APPLICATION-ATTACK-PHP](application-gateway-crs-rulegroups-rules.md#crs933)**|Bevat de regels tooprotect tegen injectieaanvallen PHP.|
|**[REQUEST-941-APPLICATION-ATTACK-XSS](application-gateway-crs-rulegroups-rules.md#crs941)**|Bevat regels om te beveiligen tegen het uitvoeren van scripts op meerdere sites.|
|**[REQUEST-942-APPLICATION-ATTACK-SQLI](application-gateway-crs-rulegroups-rules.md#crs942)**|Bevat regels om te beveiligen tegen aanvallen via SQL-injectie.|
|**[REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION](application-gateway-crs-rulegroups-rules.md#crs943)**|Bevat de regels tooprotect tegen aanvallen van sessie-vastlegging.|

#### <a name="owasp229"></a>OWASP_2.2.9

Hallo 2.2.9 regel kernset opgegeven heeft 10 regelgroepen zoals weergegeven in de volgende tabel Hallo. Elk van deze regelgroepen bevat meerdere regels, die desgewenst kunnen worden uitgeschakeld.

|Regelgroep|Beschrijving|
|---|---|
|**[crs_20_protocol_violations](application-gateway-crs-rulegroups-rules.md#crs20)**|Bevat de regels tooprotect tegen protocol schendingen (ongeldige tekens, GET met een aanvraagtekst, enz.)|
|**[crs_21_protocol_anomalies](application-gateway-crs-rulegroups-rules.md#crs21)**|Regels tooprotect tegen onjuist berichtkopinformatie bevat.|
|**[crs_23_request_limits](application-gateway-crs-rulegroups-rules.md#crs23)**|Bevat de regels tooprotect tegen argumenten of bestanden die groter is dan beperkingen.|
|**[crs_30_http_policy](application-gateway-crs-rulegroups-rules.md#crs30)**|Bevat de regels tooprotect tegen beperkte methoden, kopteksten en bestandstypen. |
|**[crs_35_bad_robots](application-gateway-crs-rulegroups-rules.md#crs35)**|Regels tooprotect tegen webcrawlers en scanners bevat.|
|**[crs_40_generic_attacks](application-gateway-crs-rulegroups-rules.md#crs40)**|Bevat de regels tooprotect tegen algemene aanvallen (sessie vastlegging, extern bestand opnemen, PHP injectie, enz.)|
|**[crs_41_sql_injection_attacks](application-gateway-crs-rulegroups-rules.md#crs41sql)**|Bevat de regels tooprotect tegen injectieaanvallen SQL|
|**[crs_41_xss_attacks](application-gateway-crs-rulegroups-rules.md#crs41xss)**|Bevat de regels tooprotect tegen scripting op meerdere sites.|
|**[crs_42_tight_security](application-gateway-crs-rulegroups-rules.md#crs42)**|Bevat een regel tooprotect tegen pad traversal-aanvallen|
|**[crs_45_trojans](application-gateway-crs-rulegroups-rules.md#crs45)**|Bevat de regels tooprotect tegen Trojaanse paarden worden geïnstalleerd.|

### <a name="waf-modes"></a>WAF-modi

Application Gateway WAF zijn geconfigureerde toorun in Hallo na twee modi:

* **Modus voor detectie** – wanneer geconfigureerde toorun in de modus voor detectie, Application Gateway WAF bewaakt en alle threat waarschuwingen wordt geregistreerd in het logboekbestand tooa. Logboekregistratie van diagnostische gegevens voor Application Gateway moeten worden ingeschakeld met behulp van Hallo **Diagnostics** sectie. U moet ook tooensure die WAF Hallo logboek is geselecteerd en ingeschakeld. In de detectiemodus worden binnenkomende verzoeken niet geblokkeerd door Web Application Firewall.
* **Preventie modus** – wanneer geconfigureerde toorun in de modus voor preventie, Application Gateway actief blokkeert aanvallen en indringers gedetecteerd door de regels. Hallo aanvaller ontvangt een 403 uitzondering voor onbevoegde toegang en Hallo verbinding is verbroken. Preventie modus blijft toolog dergelijke aanvallen in Hallo WAF Logboeken.

### <a name="application-gateway-waf-reports"></a>Bewaking met WAF

Hallo-status van uw toepassingsgateway bewaken is belangrijk. Hallo-status van uw firewall en Hallo webtoepassingen die het beveiligt worden geleverd via logboekregistratie en integratie met Azure Monitor-, Azure Security Center (binnenkort)- en Log Analytics.

![diagnostische gegevens](./media/application-gateway-web-application-firewall-overview/diagnostics.png)

#### <a name="azure-monitor"></a>Azure Monitor

Elke toepassingsgateway is geïntegreerd met [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md).  Hiermee kunt u tootrack diagnostische gegevens, inclusief WAF meldingen en Logboeken.  Deze mogelijkheid is opgegeven in Hallo Application Gateway resource in Hallo-beheerportal onder Hallo **Diagnostics** tabblad of de service rechtstreeks via hello Azure Monitor. informatie over het inschakelen van diagnostische logboeken voor application gateway bezoeken toolearn [Application Gateway diagnostische gegevens](application-gateway-diagnostics.md)

#### <a name="azure-security-center"></a>Azure Security Center

[Azure Security Center](../security-center/security-center-intro.md) helpt u te voorkomen, detecteren, en toothreats reageren met een verhoogde zichtbaarheid van en controle over Hallo beveiliging van uw Azure-resources. Toepassingsgateway nu [geïntegreerd in Azure Security Center](application-gateway-integration-security-center.md). Azure Security Center scant uw omgeving toodetect onbeveiligd-webtoepassingen. Deze kunt application gateway WAF tooprotect nu deze kwetsbaar resources aanbevelen. U kunt rechtstreeks application gateway WAF maken van hello Azure Security Center.  Deze instanties WAF zijn geïntegreerd met Azure Security Center en stuurt waarschuwingen en statusinformatie back-tooAzure Security Center voor rapportage.

![afbeelding 1](./media/application-gateway-web-application-firewall-overview/figure1.png)

#### <a name="logging"></a>Logboekregistratie

Application Gateway WAF biedt gedetailleerde rapporten voor elke bedreiging die wordt gedetecteerd. Logboekregistratie is geïntegreerd met de logboeken van Azure Diagnostics en waarschuwingen worden vastgelegd in de JSON-indeling. Deze logboeken kunnen worden geïntegreerd met [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).

![imageURLroute](./media/application-gateway-web-application-firewall-overview/waf2.png)

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

## <a name="application-gateway-waf-sku-pricing"></a>Prijzen voor de Application Gateway WAF-voorraadeenheid

Web Application Firewall is beschikbaar onder een nieuwe WAF-SKU. De SKU is alleen in de inrichting model van Azure Resource Manager en niet onder het klassieke implementatiemodel Hallo beschikbaar. Bovendien is de WAF-SKU alleen leverbaar in de middelgrote en grote varianten van de toepassingsgateway. Alle Hallo limieten voor application gateway toohello WAF SKU ook van toepassing. De prijzen variëren naargelang de kosten per gateway-uur en de kosten voor gegevensverwerking. De prijzen voor gateway-uren voor de WAF-SKU verschillen van de kosten voor Basic-SKU's. Zie [Prijzen van Application Gateway](https://azure.microsoft.com/pricing/details/application-gateway/) voor meer informatie. Gegevensverwerking kosten blijven Hallo dezelfde. Er worden geen kosten per regel of regelgroep in rekening gebracht. U kunt meerdere webtoepassingen beveiligen achter Hallo van dezelfde web application firewall en er zijn geen extra kosten voor de ondersteuning van meerdere toepassingen. 

Omdat facturering voor WAF begint effectief 5-5/2017 tot vervolgens Hallo WAF SKU gateways blijft toobe in rekening gebracht tegen standaardtarieven.

## <a name="next-steps"></a>Volgende stappen

Nadat u meer leren over Hallo-mogelijkheden van WAF, gaat u naar [hoe tooconfigure web application firewall op Application Gateway](application-gateway-web-application-firewall-portal.md).

