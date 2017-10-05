---
title: Maken of bijwerken van een Azure-toepassingsgateway met web application firewall | Microsoft Docs
description: Informatie over het maken van een toepassingsgateway met web application firewall via de portal
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 650f26d19615d27a94f3947aad7b7904b6c1fabc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-the-portal"></a>Een toepassingsgateway maken met web application firewall via de portal

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure-CLI](application-gateway-web-application-firewall-cli.md)

Informatie over het maken van een toepassingsgateway web application firewall is ingeschakeld.

De web application firewall (WAF) in Azure Application Gateway beveiligt webtoepassingen van algemene web gebaseerde aanvallen, zoals SQL-injectie, cross-site scripting aanvallen en sessie hijacks. Webtoepassing beschermd tegen veel van de OWASP bovenste 10 veelvoorkomende web beveiligingslekken.

## <a name="scenarios"></a>Scenario's

Er zijn twee scenario's in dit artikel:

Het eerste scenario, leert u [een toepassingsgateway maken met web application firewall](#create-an-application-gateway-with-web-application-firewall)

Het tweede scenario leert u [web application firewall toevoegen aan een bestaande toepassingsgateway](#add-web-application-firewall-to-an-existing-application-gateway).

![Voorbeeldscenario][scenario]

> [!NOTE]
> Aanvullende configuratie van de toepassingsgateway, met inbegrip van aangepaste health tests, adressen van de groep back-end en extra regels worden geconfigureerd nadat de toepassingsgateway is geconfigureerd en niet tijdens de eerste installatie.

## <a name="before-you-begin"></a>Voordat u begint

Azure Application Gateway vereist een eigen subnet. Zorg ervoor dat u onvoldoende adresruimte voor meerdere subnetten hebben laten bij het maken van een virtueel netwerk. Wanneer u een toepassingsgateway met een subnet implementeert, kunnen alleen andere Toepassingsgateways worden toegevoegd aan het subnet.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Web application firewall toevoegen aan een bestaande application gateway

In dit voorbeeld wordt een bestaande toepassingsgateway ter ondersteuning van web application firewall in de modus voor preventie bijwerken.

1. Klik in het deelvenster **Favorieten** van Azure Portal op **Alle resources**. Klik op de bestaande toepassingsgateway in de **alle resources** blade. Als het abonnement dat u hebt geselecteerd al verschillende bronnen heeft, kunt u de naam in de **filteren op naam...** voor eenvoudige toegang tot de DNS-zone.

   ![Toepassingsgateway maken][1]

1. Klik op **Web application firewall** en werk de instellingen voor de toepassingsgateway. Klik wanneer u klaar **opslaan**

    De instellingen voor het bijwerken van een bestaande toepassingsgateway ter ondersteuning van web application firewall zijn:

   | **Instelling** | **Waarde** | **Details**
   |---|---|---|
   |**Upgrade naar WAF laag**| Geselecteerd | Hiermee stelt u de laag van de toepassingsgateway aan de laag WAF.|
   |**Firewall-status**| Ingeschakeld | Deze instelling schakelt u de firewall op de WAF.|
   |**Firewall-modus** | Preventie | Deze instelling is hoe web application firewall omgaat met schadelijk verkeer. **Detectie** modus alleen de legt gebeurtenissen vast in, waarbij **preventie** modus legt de gebeurtenissen en de schadelijk verkeer stopt.|
   |**Regelset**|3.0|Deze instelling bepaalt de [core regelset](application-gateway-web-application-firewall-overview.md#core-rule-sets) die wordt gebruikt voor het beveiligen van de leden van de groep back-end.|
   |**Uitgeschakelde regels configureren**|Varieert|Om te voorkomen dat mogelijk valse positieven, deze instelling kunt u bepaalde uitschakelen [regels en regelgroepen](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > Bij het bijwerken van een bestaande toepassingsgateway op de SKU WAF, de SKU-grootte verandert in **gemiddeld**. Dit kan worden geconfigureerd nadat de configuratie voltooid is.

    ![Basisinstellingen voor blade weergeven][2-1]

    > [!NOTE]
    > Web application firewall om Logboeken te raadplegen, diagnostics moet zijn ingeschakeld en ApplicationGatewayFirewallLog geselecteerd. Een aantal exemplaren van 1 worden gekozen voor testdoeleinden. Het is belangrijk te weten dat alle exemplaren onder twee exemplaren niet wordt gedekt door de SLA en worden daarom niet aanbevolen. Kleine gateways zijn niet beschikbaar bij gebruik van web application firewall.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Een toepassingsgateway maken met web application firewall

Dit scenario wordt:

* Maak een toepassingsgateway gemiddeld web application firewall met twee exemplaren.
* Maak een virtueel netwerk met de naam AdatumAppGatewayVNET met een gereserveerd CIDR-blok van 10.0.0.0/16.
* Maakt u een subnet met de naam Appgatewaysubnet dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.
* Een certificaat voor SSL-offload configureren.

1. Meld u aan bij [Azure Portal](https://portal.azure.com). Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie van één maand](https://azure.microsoft.com/free)
1. Klik in het deelvenster Favorieten van de portal op **nieuw**
1. Klik op de blade **Nieuw** op **Netwerken**. In de **Networking** blade, klikt u op **Application Gateway**, zoals wordt weergegeven in de volgende afbeelding:
1. Navigeer naar de Azure-portal, klikt u op **nieuw** > **Networking** > **Application Gateway**

    ![Toepassingsgateway maken][1]

1. In de **basisbeginselen** blade die wordt weergegeven, voer de volgende waarden en klik vervolgens op **OK**:

   | **Instelling** | **Waarde** | **Details**
   |---|---|---|
   |**Naam**|AdatumAppGateway|De naam van de toepassingsgateway|
   |**Laag**|WAF|Beschikbare waarden zijn standaard- en WAF. Ga naar [web application firewall](application-gateway-web-application-firewall-overview.md) voor meer informatie over WAF.|
   |**SKU-grootte**|Middelgroot|Opties bij het kiezen van de Standard-laag zijn een klein, middelgroot en groot. Bij het kiezen van WAF laag zijn opties alleen Medium en Large.|
   |**Aantal exemplaren**|2|Aantal exemplaren van de toepassingsgateway voor hoge beschikbaarheid. Het aantal instanties van 1 moeten alleen worden gebruikt voor testdoeleinden.|
   |**Abonnement**|[Uw abonnement]|Selecteer het abonnement waarin u de toepassingsgateway wilt maken.|
   |**Resourcegroep**|**Maken van nieuwe:** AdatumAppGatewayRG|Maak een resourcegroep. De naam van de resourcegroep moet uniek zijn binnen het abonnement dat u hebt geselecteerd. Lees het overzichtsartikel over [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) voor meer informatie over resourcegroepen.|
   |**Locatie**|VS - west||

   ![Basisinstellingen voor blade weergeven][2-2]

1. In de **instellingen** blade die wordt weergegeven onder **virtueel netwerk**, klikt u op **Kies een virtueel netwerk**. Deze stap wordt geopend Voer de **virtueel netwerk kiezen** blade.  Klik op **nieuw** openen de **virtueel netwerk maken** blade.

   ![Kies een virtueel netwerk][2]

1. Op de **de blade virtueel netwerk maken** Voer de volgende waarden en klik vervolgens op **OK**. Deze stap wordt gesloten de **virtueel netwerk maken** en **virtueel netwerk kiezen** blades. Dit vult de **Subnet** op de **instellingen** blade met het gekozen subnet.

   |**Instelling** | **Waarde** | **Details** |
   |---|---|---|
   |**Naam**|AdatumAppGatewayVNET|Naam van de toepassingsgateway|
   |**Adresruimte**|10.0.0.0/16| Deze waarde is de adresruimte voor het virtuele netwerk|
   |**Subnetnaam**|AppGatewaySubnet|Naam van het subnet voor de toepassingsgateway|
   |**Subnetadresbereik**|10.0.0.0/28 | Dit subnet kunt u meer extra subnetten in het virtuele netwerk backend groepsleden|

1. Op de **instellingen** blade onder **Frontend IP-configuratie**, kies **openbare** als de **type IP-adres**

1. Op de **instellingen** blade onder **openbaar IP-adres**, klikt u op **Kies een openbaar IP-adres**, deze stap wordt geopend de **openbare IP-adres kiezen** blade, klikt u op **nieuw**.

   ![openbare IP-adres kiezen][3]

1. Op de **openbare IP-adres maken** blade, accepteer de standaardwaarde, en klik op **OK**. Deze stap wordt gesloten de **openbare IP-adres kiezen** blade de **openbare IP-adres maken** blade en vullen **openbaar IP-adres** met het openbare IP-adres dat is gekozen.

1. Op de **instellingen** blade onder **listenerconfiguratie**, klikt u op **HTTP** onder **Protocol**. Gebruik **https**, is een certificaat vereist. De persoonlijke sleutel van het certificaat is vereist zodat een .pfx-bestand exporteren van het certificaat moet worden opgegeven en het wachtwoord voor het bestand.

1. Configureer de **WAF** specifieke instellingen.

   |**Instelling** | **Waarde** | **Details** |
   |---|---|---|
   |**Firewall-status**| Ingeschakeld| Deze instelling schakelt WAF in- of uitschakelen.|
   |**Firewall-modus** | Preventie| Deze instelling bepaalt dat de acties WAF neemt schadelijk verkeer. Als **detectie** is gekozen, wordt alleen verkeer vastgelegd.  Als **preventie** is gekozen, verkeer is geregistreerd en is gestopt met een niet-geautoriseerde 403-antwoord.|


1. Controleer de pagina Samenvatting en klik op **OK**.  De toepassingsgateway is nu in de wachtrij geplaatst en gemaakt.

1. Nadat de toepassingsgateway is gemaakt, gaat u aan in de portal om door te gaan met de configuratie van de toepassingsgateway.

    ![Application Gateway resource weergeven][10]

Deze stappen maken een basic-toepassingsgateway met standaardinstellingen voor de listener, back-endpool, back-end-http-instellingen en -regels U kunt deze instellingen aanpassen aan uw implementatie wanneer het inrichten voltooid is wijzigen

> [!NOTE]
> Toepassingsgateways gemaakt met de basic web application firewall-configuratie zijn geconfigureerd met CRS 3.0 voor beveiliging.

## <a name="next-steps"></a>Volgende stappen

Vervolgens maakt u kunt informatie over het configureren van een aangepast domeinalias voor de [openbaar IP-adres](../dns/dns-custom-domain.md#public-ip-address) met behulp van Azure DNS- of een andere DNS-provider.

Informatie over het configureren van diagnostische gegevens vastleggen voor de gebeurtenissen die zijn gedetecteerd of voorkomen met web application firewall logboekregistratie in via [Application Gateway Diagnostics](application-gateway-diagnostics.md)

Informatie over het maken van aangepaste statuscontroles in via [een aangepaste health test maken](application-gateway-create-probe-portal.md)

Informatie over het configureren van SSL-Offloading en nemen de kostbare SSL-ontsleuteling uit uw webservers in via [SSL-Offload configureren](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
