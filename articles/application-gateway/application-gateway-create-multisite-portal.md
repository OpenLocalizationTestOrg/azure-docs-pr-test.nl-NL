---
title: aaaHost meerdere sites met Azure Application Gateway | Microsoft Docs
description: Deze pagina bevat instructies tooconfigure aan een bestaande Azure application gateway voor het hosten van meerdere webtoepassingen op Hallo dezelfde gateway Hello Azure-portal.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a>Een bestaande toepassingsgateway voor het hosten van meerdere webtoepassingen configureren

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

Meerdere hosting-site kunt u toodeploy meer dan één webtoepassing op Hallo dezelfde toepassingsgateway. Is afhankelijk van de aanwezigheid van de host-header in Hallo inkomende HTTP-aanvraag, toodetermine welke listener verkeer ontvangt. Hallo-listener stuurt vervolgens verkeer tooappropriate back-endpool zoals geconfigureerd in de definitie van de gateway Hallo Hallo. In webtoepassingen SSL is ingeschakeld, is de toepassingsgateway afhankelijk van Hallo indicatie voor Server-naam (SNI) extensie toochoose Hallo juist listener voor internetverkeer Hallo. Vaak gebruikt voor het hosten van meerdere site is van aanvragen verdelen over tooload voor verschillende web domeinen toodifferent back-end-servergroepen. Op dezelfde manier Hallo meerdere subdomeinen Hallo dezelfde hoofddomein kan ook worden gehost op dezelfde toepassingsgateway.

## <a name="scenario"></a>Scenario

In de Hallo voorbeeld te volgen, toepassingsgateway verkeer voor contoso.com en fabrikam.com bedient met twee back-endserver van toepassingen: contoso-servergroep en fabrikam-servergroep. Vergelijkbare installatie wordt mogelijk gebruikt toohost subdomeinen zoals app.contoso.com en blog.contoso.com.

![scenario voor meerdere locaties][multisite]

## <a name="before-you-begin"></a>Voordat u begint

Dit scenario voegt ondersteuning voor meerdere locaties tooan bestaande toepassingsgateway. toocomplete dit scenario wordt een bestaande toepassingsgateway moet toobe beschikbaar tooconfigure. Ga naar [een toepassingsgateway maken met behulp van de portal Hallo](application-gateway-create-gateway-portal.md) toolearn hoe toocreate een basic-toepassingsgateway in Hallo-portal.

Hallo hieronder vindt u Hallo stappen nodig tooupdate Hallo toepassingsgateway:

1. Maken van back-end-adresgroepen toouse voor elke site.
2. Maak een listener voor elke site toepassingsgateway ondersteunt.
3. Maak regels toomap elke listener voor Hallo juiste back-end.

## <a name="requirements"></a>Vereisten

* **Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers. Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP. FQDN-naam kan ook worden gebruikt.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.
* **Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend. Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.
* **Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze waarden zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert). Voor meerdere locaties ingeschakeld Toepassingsgateways, hostnaam en SNI indicatoren ook worden toegevoegd.
* **Regel:** Hallo regel verbindt Hallo listener, Hallo back-endserverpool, en definieert naar welke back-endserver groep Hallo verkeer moet gerichte toowhen dit bij een bepaalde listener aankomt. Regels worden verwerkt op Hallo volgorde die ze worden weergegeven en verkeer wordt omgeleid via Hallo eerste regel die overeenkomt met ongeacht specifieke karakter. Bijvoorbeeld, als u een regel met een basic-listener en een regel met meerdere sites listener beide op dezelfde poort, regel met Hallo Hallo hebt moet Hallo multi-site-listener worden weergegeven voordat Hallo regel met Hallo basic listener om Hallo multi-site regel toofunction als Er werd verwacht. 
* **Certificaten:** elke listener vereist een uniek certificaat, in dit voorbeeld 2 listeners worden gemaakt voor meerdere locaties. Twee pfx-certificaten en wachtwoorden voor deze Hallo moeten toobe gemaakt.

## <a name="create-back-end-pools-for-each-site"></a>Back-end-adresgroepen voor elke site maken

Een back-end van toepassingen voor elke site of toepassing gateway ondersteunt is vereist, in dit geval 2 worden gemaakt voor contoso11.com en één voor fabrikam11.com.

### <a name="step-1"></a>Stap 1

Navigeer tooan bestaande toepassingsgateway in hello Azure-portal (https://portal.azure.com). Selecteer **back-endpools** en klik op **toevoegen**

![back-endpools toevoegen][7]

### <a name="step-2"></a>Stap 2

Vul Hallo voor back-end-pool Hallo **pool1**, Hallo IP-adressen of FQDN-namen voor Hallo back-end-servers toe te voegen en klik op **OK**

![back-end-groepsinstellingen pool1][8]

### <a name="step-3"></a>Stap 3

Klik op Hallo back-end-adresgroepen blade **toevoegen** tooadd een aanvullende back-end-adresgroep **pool2**, Hallo IP-adressen of FQDN-namen voor Hallo back-end-servers toe te voegen en klik op **OK**

![back-end pool2 groepsinstellingen][9]

## <a name="create-listeners-for-each-back-end"></a>Listeners voor elke back-end maken

Application Gateway is afhankelijk van HTTP 1.1 host headers toohost meer dan één website op Hallo hetzelfde openbare IP-adres en poort. basic Hallo-listener gemaakt in de portal Hallo bevat deze eigenschap niet.

### <a name="step-1"></a>Stap 1

Klik op **Listeners** op Hallo van bestaande application gateway en klikt u op **multi-site** tooadd Hallo eerste listener.

![overzichtsblade listeners][1]

### <a name="step-2"></a>Stap 2

Hallo-informatie voor Hallo-listener vult. In dit voorbeeld SSL beëindiging is geconfigureerd, maakt u een nieuwe frontend-poort. Hallo pfx-certificaat toobe gebruikt voor SSL-beëindiging uploaden. Hallo enige verschil op deze blade vergeleken toohello standaard basic listener-blade is Hallo hostnaam.

![listener eigenschappenblade][2]

### <a name="step-3"></a>Stap 3

Klik op **multi-site** en een ander listener te maken, zoals beschreven in de vorige stap voor de tweede site Hallo Hallo. Zorg ervoor dat toouse een ander certificaat voor de tweede listener Hallo. Hallo enige verschil op deze blade vergeleken toohello standaard basic listener-blade is Hallo hostnaam. Hallo-informatie voor Hallo-listener vult en u op **OK**.

![listener eigenschappenblade][3]

> [!NOTE]
> Maken van luisteraars in hello Azure-portal voor application gateway is een langlopende taak op. Dit kan enige tijd toocreate Hallo twee listeners in dit scenario. Wanneer volledige Hallo listeners in Hallo portal weergeven zoals gezien in Hallo installatiekopie te volgen:

![overzicht van de listener][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a>Regels toomap listeners toobackend groepen maken

### <a name="step-1"></a>Stap 1

Navigeer tooan bestaande toepassingsgateway in hello Azure-portal (https://portal.azure.com). Selecteer **regels** en kiest u de bestaande standaardregel Hallo **rule1** en klik op **bewerken**.

### <a name="step-2"></a>Stap 2

Hallo regels blade invullen zoals gezien in Hallo installatiekopie te volgen. Eerste Hallo-listener en eerste groep kiezen en te klikken op **opslaan** wanneer u klaar.

![Bewerk de bestaande regel][6]

### <a name="step-3"></a>Stap 3

Klik op **Basic regel** toocreate Hallo tweede regel. Hallo-formulier met Hallo tweede listener en tweede back-endpool invullen en klik op **OK** toosave.

![blade basic regel toevoegen][10]

Dit scenario is voltooid op een bestaande toepassingsgateway configureren met ondersteuning voor meerdere locaties via hello Azure-portal.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooprotect uw websites met [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
