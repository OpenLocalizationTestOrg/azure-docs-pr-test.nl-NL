---
title: aaaCreate of een Azure-toepassingsgateway bijwerken met web application firewall | Microsoft Docs
description: Meer informatie over hoe toocreate een toepassingsgateway met web application firewall via de portal Hallo
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
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a>Een toepassingsgateway met web application firewall maken met behulp van Hallo-portal

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure-CLI](application-gateway-web-application-firewall-cli.md)

Meer informatie over hoe toocreate web application firewall toepassingsgateway ingeschakeld.

Hallo web application firewall (WAF) in Azure Application Gateway beveiligt webtoepassingen van algemene web gebaseerde aanvallen, zoals SQL-injectie, cross-site scripting aanvallen en sessie hijacks. Webtoepassing beschermd tegen veel Hallo OWASP bovenste 10 veelvoorkomende web beveiligingslekken.

## <a name="scenarios"></a>Scenario's

Er zijn twee scenario's in dit artikel:

In het eerste scenario hello, leert u te[een toepassingsgateway maken met web application firewall](#create-an-application-gateway-with-web-application-firewall)

In het tweede scenario hello, leert u te[web application firewall tooan bestaande toepassingsgateway toevoegen](#add-web-application-firewall-to-an-existing-application-gateway).

![Voorbeeldscenario][scenario]

> [!NOTE]
> Aanvullende configuratie van de toepassingsgateway hello, met inbegrip van aangepaste health tests, adressen van de groep back-end en extra regels worden geconfigureerd nadat de toepassingsgateway Hallo is geconfigureerd en niet tijdens de eerste installatie.

## <a name="before-you-begin"></a>Voordat u begint

Azure Application Gateway vereist een eigen subnet. Zorg ervoor dat u laat u genoeg ruimte adres toohave meerdere subnetten bij het maken van een virtueel netwerk. Wanneer u een subnet toepassingsgateway tooa implementeert, enige extra toepassingsgateways kunnen toobe toegevoegd worden toohello subnet.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Web application firewall tooan bestaande toepassingsgateway toevoegen

In dit voorbeeld werkt een application gateway toosupport web application firewall in de modus te voorkomen.

1. In de Azure-portal Hallo **Favorieten** deelvenster, klikt u op **alle resources**. Klik op bestaande Application Gateway in Hallo Hallo **alle resources** blade. Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u de naam van de Hallo opgeven in Hallo **filteren op naam...** vak tooeasily toegang Hallo DNS-zone.

   ![Toepassingsgateway maken][1]

1. Klik op **Web application firewall** en instellingen voor de toepassingsgateway Hallo bijwerken. Klik wanneer u klaar **opslaan**

    Hallo instellingen tooupdate een application gateway toosupport web application firewall zijn:

   | **Instelling** | **Waarde** | **Details**
   |---|---|---|
   |**Upgrade tooWAF laag**| Geselecteerd | Hiermee stelt u Hallo laag van Hallo application gateway toohello WAF laag.|
   |**Firewall-status**| Ingeschakeld | Deze instelling schakelt u de firewall Hallo op Hallo WAF.|
   |**Firewall-modus** | Preventie | Deze instelling is hoe web application firewall omgaat met schadelijk verkeer. **Detectie** modus alleen Hallo legt gebeurtenissen vast in, waarbij **preventie** modus legt Hallo gebeurtenissen en stopt Hallo schadelijk verkeer.|
   |**Regelset**|3.0|Deze instelling bepaalt u Hallo [core regelset](application-gateway-web-application-firewall-overview.md#core-rule-sets) die gebruikte tooprotect Hallo back-end groepsleden.|
   |**Uitgeschakelde regels configureren**|Varieert|mogelijke valse positieven tooprevent, deze instelling kunt u toodisable bepaalde [regels en regelgroepen](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > Bij het bijwerken van een bestaande toepassing gateway toohello WAF SKU, Hallo SKU wijzigingen grootte te**gemiddeld**. Dit kan worden geconfigureerd nadat de configuratie voltooid is.

    ![Basisinstellingen voor blade weergeven][2-1]

    > [!NOTE]
    > tooview web application firewall Logboeken, diagnostics moeten zijn ingeschakeld en ApplicationGatewayFirewallLog geselecteerd. Een aantal exemplaren van 1 worden gekozen voor testdoeleinden. Het is belangrijk dat elke instantie onder twee exemplaren tellen tooknow niet wordt gedekt door Hallo SLA en worden daarom niet aanbevolen. Kleine gateways zijn niet beschikbaar bij gebruik van web application firewall.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Een toepassingsgateway maken met web application firewall

Dit scenario wordt:

* Maak een toepassingsgateway gemiddeld web application firewall met twee exemplaren.
* Maak een virtueel netwerk met de naam AdatumAppGatewayVNET met een gereserveerd CIDR-blok van 10.0.0.0/16.
* Maakt u een subnet met de naam Appgatewaysubnet dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.
* Een certificaat voor SSL-offload configureren.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com). Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie van één maand](https://azure.microsoft.com/free)
1. Klik in Hallo Favorieten deelvenster van de portal Hallo op **nieuw**
1. In Hallo **nieuw** blade, klikt u op **Networking**. In Hallo **Networking** blade, klikt u op **Application Gateway**, zoals weergegeven in Hallo installatiekopie te volgen:
1. Navigeer toohello Azure-portal, klikt u op **nieuw** > **Networking** > **Application Gateway**

    ![Toepassingsgateway maken][1]

1. In Hallo **basisbeginselen** blade die wordt weergegeven, Voer Hallo volgende waarden en klik vervolgens op **OK**:

   | **Instelling** | **Waarde** | **Details**
   |---|---|---|
   |**Naam**|AdatumAppGateway|naam van de toepassingsgateway Hallo Hallo|
   |**Laag**|WAF|Beschikbare waarden zijn standaard- en WAF. Ga naar [web application firewall](application-gateway-web-application-firewall-overview.md) toolearn meer over WAF.|
   |**SKU-grootte**|Middelgroot|Opties bij het kiezen van de Standard-laag zijn een klein, middelgroot en groot. Bij het kiezen van WAF laag zijn opties alleen Medium en Large.|
   |**Aantal exemplaren**|2|Aantal exemplaren van de toepassingsgateway Hallo voor hoge beschikbaarheid. Het aantal instanties van 1 moeten alleen worden gebruikt voor testdoeleinden.|
   |**Abonnement**|[Uw abonnement]|Selecteer een abonnement toocreate Hallo toepassingsgateway in.|
   |**Resourcegroep**|**Maken van nieuwe:** AdatumAppGatewayRG|Maak een resourcegroep. de naam van resourcegroep Hallo moet uniek zijn binnen het Hallo-abonnement die u hebt geselecteerd. meer informatie over resourcegroepen lezen Hallo toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) overzichtsartikel.|
   |**Locatie**|VS - west||

   ![Basisinstellingen voor blade weergeven][2-2]

1. In Hallo **instellingen** blade die wordt weergegeven onder **virtueel netwerk**, klikt u op **Kies een virtueel netwerk**. Deze stap wordt geopend Voer Hallo **virtueel netwerk kiezen** blade.  Klik op **nieuw** tooopen hello **virtueel netwerk maken** blade.

   ![Kies een virtueel netwerk][2]

1. Op Hallo **de blade virtueel netwerk maken** Voer Hallo volgende waarden en klik vervolgens op **OK**. Deze stap wordt gesloten Hallo **virtueel netwerk maken** en **virtueel netwerk kiezen** blades. Hierdoor wordt gevuld Hallo **Subnet** op Hallo **instellingen** blade met Hallo subnet gekozen.

   |**Instelling** | **Waarde** | **Details** |
   |---|---|---|
   |**Naam**|AdatumAppGatewayVNET|Naam van de toepassingsgateway Hallo|
   |**Adresruimte**|10.0.0.0/16| Deze waarde is Hallo-adresruimte voor het virtuele netwerk Hallo|
   |**Subnetnaam**|AppGatewaySubnet|Naam van het Hallo-subnet voor Hallo application gateway|
   |**Subnetadresbereik**|10.0.0.0/28 | Dit subnet kunt u meer extra subnetten in het virtuele netwerk Hallo groepsleden back-end|

1. Op Hallo **instellingen** blade onder **Frontend IP-configuratie**, kies **openbare** als Hallo **type IP-adres**

1. Op Hallo **instellingen** blade onder **openbaar IP-adres**, klikt u op **Kies een openbaar IP-adres**, deze stap wordt geopend Hallo **Kies openbaar IP-adres**blade, klikt u op **nieuw**.

   ![openbare IP-adres kiezen][3]

1. Op Hallo **openbare IP-adres maken** blade Hallo standaardwaarde accepteren en klik op **OK**. Deze stap wordt gesloten Hallo **openbare IP-adres kiezen** blade, Hallo **openbare IP-adres maken** blade en vullen **openbaar IP-adres** met Hallo openbare IP-adres is gekozen.

1. Op Hallo **instellingen** blade onder **listenerconfiguratie**, klikt u op **HTTP** onder **Protocol**. toouse **https**, is een certificaat vereist. Hallo persoonlijke sleutel van het Hallo-certificaat is vereist zodat een .pfx-export van Hallo certificaat toobe opgegeven moet en Hallo wachtwoord voor het Hallo-bestand.

1. Hallo configureren **WAF** specifieke instellingen.

   |**Instelling** | **Waarde** | **Details** |
   |---|---|---|
   |**Firewall-status**| Ingeschakeld| Deze instelling schakelt WAF in- of uitschakelen.|
   |**Firewall-modus** | Preventie| Deze instelling bepaalt Hallo acties die WAF schadelijk verkeer neemt. Als **detectie** is gekozen, wordt alleen verkeer vastgelegd.  Als **preventie** is gekozen, verkeer is geregistreerd en is gestopt met een niet-geautoriseerde 403-antwoord.|


1. Controleer de overzichtspagina Hallo en klik op **OK**.  Hallo application gateway is nu in de wachtrij geplaatst en gemaakt.

1. Nadat de toepassingsgateway Hallo is gemaakt, gaat u tooit in Hallo portal toocontinue configuratie van de toepassingsgateway Hallo.

    ![Application Gateway resource weergeven][10]

Deze stappen maken een basic-toepassingsgateway met standaardinstellingen voor het Hallo-listener, back-endpool, back-end-http-instellingen en -regels U kunt deze instellingen toosuit uw implementatie wanneer Hallo inrichten voltooid is

> [!NOTE]
> Toepassingsgateways gemaakt met de Hallo basic web application firewall-configuratie zijn geconfigureerd met CRS 3.0 voor beveiliging.

## <a name="next-steps"></a>Volgende stappen

Vervolgens leert u hoe de alias van een aangepast domein voor Hallo tooconfigure [openbaar IP-adres](../dns/dns-custom-domain.md#public-ip-address) met behulp van Azure DNS- of een andere DNS-provider.

Meer informatie over hoe tooconfigure Diagnostische logboekregistratie, toolog Hallo gebeurtenissen die zijn gedetecteerd of voorkomen met web application firewall in via [Application Gateway Diagnostics](application-gateway-diagnostics.md)

Meer informatie over hoe toocreate aangepaste statuscontroles in via [een aangepaste health test maken](application-gateway-create-probe-portal.md)

Meer informatie over hoe tooconfigure SSL-Offloading en los het Hallo kostbare SSL ontsleuteling uitgeschakeld in uw webservers in via [SSL-Offload configureren](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
