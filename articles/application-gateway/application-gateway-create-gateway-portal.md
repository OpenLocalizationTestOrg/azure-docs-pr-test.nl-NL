---
title: aaaCreate een Application Gateway - Azure-Portal | Microsoft Docs
description: Meer informatie over hoe toocreate een toepassingsgateway met behulp van de portal Hallo
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a>Een toepassingsgateway maken met Hallo-portal

[Toepassingsgateway](application-gateway-introduction.md) is een toegewezen virtueel apparaat toepassing levering controller (ADC) bieden een service en biedt verschillende laag 7 taakverdeling mogelijkheden voor uw toepassing. In dit artikel leert u Hallo stappen toocreate een toepassingsgateway met behulp van hello Azure-portal en het toevoegen van een bestaande server als een back-end-lid.

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Meld u bij toohello Azure-portal op [http://portal.azure.com](http://portal.azure.com)

## <a name="create-application-gateway"></a>Toepassingsgateway maken

toocreate een toepassingsgateway voltooid Hallo stappen volgen. Toepassingsgateway vereist een eigen subnet. Zorg ervoor dat u laat u genoeg ruimte adres toohave meerdere subnetten bij het maken van een virtueel netwerk. Nadat de toepassingsgateway Hallo geïmplementeerde tooa subnet is, kunnen alleen andere Toepassingsgateways tooit worden toegevoegd.

1. Klik in Hallo Favorieten deelvenster van de portal Hallo op **nieuw**
1. In Hallo **nieuw** blade, klikt u op **Networking**. In Hallo **Networking** blade, klikt u op **Application Gateway**, zoals weergegeven in Hallo installatiekopie te volgen:

    ![Toepassingsgateway maken][1]

1. In Hallo **basisbeginselen** blade die wordt weergegeven, Voer Hallo volgende waarden en klik vervolgens op **OK**:

   | **Instelling** | **Waarde** | **Details**|
   |---|---|---|
   |**Naam**|AdatumAppGateway|naam van de toepassingsgateway Hallo Hallo|
   |**Laag**|Standard|Beschikbare waarden zijn standaard- en WAF. Ga naar [web application firewall](application-gateway-web-application-firewall-overview.md) toolearn meer over WAF.|
   |**SKU-grootte**|Middelgroot|Opties bij het kiezen van de Standard-laag zijn een klein, middelgroot en groot. Bij het kiezen van WAF laag zijn opties alleen Medium en Large.|
   |**Aantal exemplaren**|2|Aantal exemplaren van de toepassingsgateway Hallo voor hoge beschikbaarheid. Het aantal instanties van 1 moeten alleen worden gebruikt voor testdoeleinden.|
   |**Abonnement**|[Uw abonnement]|Selecteer een abonnement toocreate Hallo toepassingsgateway in.|
   |**Resourcegroep**|**Maken van nieuwe:** AdatumAppGatewayRG|Maak een resourcegroep. de naam van resourcegroep Hallo moet uniek zijn binnen het Hallo-abonnement die u hebt geselecteerd. meer informatie over resourcegroepen lezen Hallo toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) overzichtsartikel.|
   |**Locatie**|VS - west||

1. In Hallo **instellingen** blade die wordt weergegeven onder **virtueel netwerk**, klikt u op **Kies een virtueel netwerk**. Hallo **virtueel netwerk kiezen** blade wordt geopend.  Klik op **nieuw** tooopen hello **virtueel netwerk maken** blade.

   ![Kies een virtueel netwerk][2]

1. Op Hallo **de blade virtueel netwerk maken** Voer Hallo volgende waarden en klik vervolgens op **OK**. Hallo **virtueel netwerk maken** en **virtueel netwerk kiezen** blades sluiten. Deze stap vult Hallo **Subnet** op Hallo **instellingen** blade met Hallo subnet gekozen.

   | **Instelling** | **Waarde** | **Details**|
   |---|---|---|
   |**Naam**|AdatumAppGatewayVNET|Naam van de toepassingsgateway Hallo|
   |**Adresruimte**|10.0.0.0/16|Dit is Hallo-adresruimte voor het virtuele netwerk Hallo|
   |**Subnetnaam**|AppGatewaySubnet|Naam van het Hallo-subnet voor Hallo application gateway|
   |**Subnetadresbereik**|10.0.0.0/28|Dit subnet kunt u meer extra subnetten in het virtuele netwerk Hallo groepsleden back-end|

1. Op Hallo **instellingen** blade onder **Frontend IP-configuratie**, kies **openbare** als Hallo **type IP-adres**

1. Op Hallo **instellingen** blade onder **openbaar IP-adres** klikt u op **Kies een openbaar IP-adres**, Hallo **openbare IP-adres kiezen** blade wordt geopend , klik op **nieuw**.

   ![openbare IP-adres kiezen][3]

1. Op Hallo **openbare IP-adres maken** blade Hallo standaardwaarde accepteren en klik op **OK**. Hallo-blade wordt gesloten en gevuld Hallo **openbaar IP-adres** met Hallo openbare IP-adres is gekozen.

1. Op Hallo **instellingen** blade onder **listenerconfiguratie**, klikt u op **HTTP** onder **Protocol**. Voer Hallo poort toouse in Hallo **poort** veld.

2. Klik op **OK** op Hallo **instellingen** blade toocontinue.

1. Controleer de instellingen Hallo op Hallo **samenvatting** blade en klik op **OK** toostart maken van een toepassingsgateway Hallo. Een toepassingsgateway maken, is een langlopende taak en tijd toocomplete duurt.

## <a name="add-servers-toobackend-pools"></a>Servers toobackend groepen toevoegen

Wanneer u de toepassingsgateway Hallo maakt, moeten Hallo-systemen die als host Hallo toepassing toobe taakverdeling fungeren nog steeds toobe toegevoegde toohello toepassingsgateway. Hallo IP-adressen, FQDN-naam of NIC's van deze servers worden toegevoegd toohello back-end-adresgroepen.

### <a name="ip-address-or-fqdn"></a>IP-adres of FQDN-naam

1. Met de Hallo toepassingsgateway gemaakt in Azure-portal Hallo **Favorieten** deelvenster, klikt u op **alle resources**. Klik op Hallo **AdatumAppGateway** toepassingsgateway in alle bronnen blade Hallo. Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u **AdatumAppGateway** in Hallo **filteren op naam...** vak tooeasily toegang Hallo toepassingsgateway.

1. Hallo-toepassingsgateway die u hebt gemaakt, wordt weergegeven. Klik op **back-endpools**, en selecteert u de huidige back-endpool hello **appGatewayBackendPool**, Hallo **appGatewayBackendPool** blade wordt geopend.

   ![Back-end van de toepassingsgroepen-Gateway][4]

1. Klik op **doel toevoegen** tooadd IP-adressen van de FQDN-waarden. Kies **IP-adres of FQDN-naam** als Hallo **Type** en voer uw IP-adres of FQDN-naam in Hallo-veld. Herhaal deze stap voor aanvullende back-end-groepsleden. Klik wanneer klaar **opslaan**.

### <a name="virtual-machine-and-nic"></a>Virtuele Machine en NIC

U kunt ook NIC's voor virtuele Machine toevoegen als leden van back-end-adresgroep. Alleen virtuele machines in hetzelfde virtuele netwerk als Hallo Application Gateway zijn beschikbaar via Hallo Hallo vervolgkeuzelijst.

1. Met de Hallo toepassingsgateway gemaakt in Azure-portal Hallo **Favorieten** deelvenster, klikt u op **alle resources**. Klik op Hallo **AdatumAppGateway** toepassingsgateway in alle bronnen blade Hallo. Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u **AdatumAppGateway** in Hallo **filteren op naam...** vak tooeasily toegang Hallo toepassingsgateway.

1. Hallo-toepassingsgateway die u hebt gemaakt, wordt weergegeven. Klik op **back-endpools**, en selecteert u de huidige back-endpool hello **appGatewayBackendPool**, Hallo **appGatewayBackendPool** blade wordt geopend.

   ![Back-end van de toepassingsgroepen-Gateway][5]

1. Klik op **doel toevoegen** tooadd IP-adressen van de FQDN-waarden. Kies **virtuele Machine** als Hallo **Type** en Hallo virtuele machine en NIC toouse selecteren. Klik wanneer klaar **opslaan**

   > [!NOTE]
   > Alleen virtuele machines in Hallo hetzelfde virtuele netwerk, zoals Hallo toepassingsgateway zijn beschikbaar in de vervolgkeuzelijst Hallo.

## <a name="clean-up-resources"></a>Resources opschonen

Wanneer deze niet langer nodig is, resourcegroep hello, toepassingsgateway en alle gerelateerde resources verwijderd. Hallo resourcegroep toodo dus selecteren in Hallo application gateway blade en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In dit scenario moet u een application gateway wordt geïmplementeerd en een back-end server toohello toegevoegd. de volgende stappen Hallo zijn tooconfigure Hallo toepassingsgateway door instellingen aanpassen en aanpassen van de regels in het Hallo-gateway. Deze stappen vindt u door naar Hallo artikelen na te gaan:

Meer informatie over hoe toocreate aangepaste statuscontroles in via [een aangepaste health test maken](application-gateway-create-probe-portal.md)

Meer informatie over hoe tooconfigure SSL-Offloading en los het Hallo kostbare SSL ontsleuteling uitgeschakeld in uw webservers in via [SSL-Offload configureren](application-gateway-ssl-portal.md)

Meer informatie over hoe tooprotect uw toepassingen met [Web Application Firewall](application-gateway-webapplicationfirewall-overview.md) een functie van de toepassingsgateway.

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
