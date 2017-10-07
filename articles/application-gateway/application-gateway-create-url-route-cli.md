---
title: een toepassingsgateway met URL-routering regels - aaaCreate Azure CLI 2.0 | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, een Azure-toepassingsgateway met behulp van regels voor URL-routering configureren
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a>Een toepassingsgateway met pad gebaseerde routering met Azure CLI 2.0 maken

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

URL-pad gebaseerde routering, kunt u tooassociate routes op basis van Hallo URL-pad van een Http-aanvraag. Het wordt gecontroleerd of er een route tooa back-end-adresgroep geconfigureerd voor Hallo-URL die zijn gepresenteerd in Hallo Application Gateway is en verzendt Hallo netwerkverkeer toohello gedefinieerd back-end-pool. Vaak gebruikt voor het doorsturen van op basis van een URL is tooload van aanvragen verdelen over voor andere typen inhoud toodifferent back-end-servergroepen.

URL gebaseerde routering introduceert een nieuwe regel type tooapplication gateway. Toepassingsgateway heeft twee regeltypen: basic en PathBasedRouting. Basic regeltype biedt round robin-service voor Hallo back-end opslaggroepen tijdens PathBasedRouting bovendien tooround robin distributie, ook rekening wordt gehouden pad patroon van de aanvraag-URL Hallo daarbij Hallo back-end-pool.

## <a name="scenario"></a>Scenario

In Hallo voorbeeld te volgen, Application Gateway verkeer voor contoso.com bedient met twee back-endserver van toepassingen: een servergroep standaard en een installatiekopie-servergroep.

Aanvragen voor http://contoso.com/image * worden gerouteerd servergroep tooimage (imagesBackendPool), als hello komt niet overeen met het pad, een server standaardgroep (appGatewayBackendPool) is geselecteerd.

![URL-route](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Open Hallo **Microsoft Azure-opdrachtprompt**, en zich aanmelden. 

```azurecli
az login -u "username"
```

> [!NOTE]
> U kunt ook `az login` zonder Hallo switch voor apparaat aanmelding waarvoor een code op aka.ms/devicelogin invoert.

Wanneer u Hallo voorgaande voorbeeld typt, wordt een code opgegeven. Navigeer toohttps://aka.ms/devicelogin in een browser toocontinue Hallo aanmeldingsproces.

![cmd tonen apparaat aanmelding][1]

Voer in de browser Hallo Hallo-code die u hebt ontvangen. U staat op de aanmeldingspagina omgeleide tooa.

![browser tooenter code][2]

Zodra het Hallo-code is ingevoerd u bent aangemeld, sluiten Hallo browser toocontinue op met de Hallo scenario.

![aangemeld][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a>Een regel op basis van het pad tooan bestaande toepassingsgateway toevoegen

Een toepassingsgateway maken met een padregel gedefinieerd

### <a name="create-a-new-back-end-pool"></a>Een nieuwe back-end-pool maken

Configureren van de instelling voor application gateway **imagesBackendPool** voor Hallo taakverdeling netwerkverkeer in Hallo back-endpool. In dit voorbeeld kunt u instellingen van de andere back-end-adresgroep voor de nieuwe back-end-pool Hallo configureren. Elke back-endpool kan een eigen instelling van de back-endpool hebben.  Back-end-HTTP-instellingen worden gebruikt door regels tooroute verkeer toohello juiste back-end-groepsleden. Hiermee bepaalt u het Hallo-protocol en poort die wordt gebruikt bij het verzenden van verkeer toohello back-end-groepsleden. Op basis van het cookie sessies worden ook bepaald door Hallo back-end-HTTP-instellingen.  Bij inschakeling sessie cookies gebaseerde affiniteit verkeer toohello verzendt dezelfde back-end als de vorige aanvragen voor elk pakket.

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a>Maak een nieuwe front-endpoort

Hallo front-endpoort voor een toepassingsgateway configureren. Hallo front-endpoort configuration-object wordt gebruikt door een listener toodefine wat Hallo Application Gateway luistert naar verkeer op Hallo listener-poort.

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a>Maak een nieuwe listener

Hallo-listener configureren. Deze stap configureert u Hallo-listener voor Hallo openbaar IP-adres en poort gebruikt tooreceive binnenkomend netwerkverkeer. Hallo volgt duurt Hallo eerder geconfigureerde front-end-IP-configuratie, front-endpoort configuratie en een protocol (http of https) en Hallo listener configureert. Hallo-listener luistert in dit voorbeeld tooHTTP verkeer op poort 82 van het openbare IP-adres hello, dat eerder is gemaakt.

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a>Overzicht van Hallo Url-pad maken

URL-regel paden voor back-end-adresgroepen Hallo configureren. Deze stap configureert u Hallo relatieve pad dat wordt gebruikt door application gateway toodefine Hallo toewijzing tussen URL-pad en welke back-end-pool toohandle Hallo binnenkomend verkeer is toegewezen.

> [!IMPORTANT]
> Elk pad moet beginnen met / en Hallo enige plaats waar een '\*' is toegestaan, Hallo einde. Voorbeelden van geldige zijn/xyz, /xyz* of xyz / *. Hallo tekenreeks ingevoerd toohello pad matcher heeft geen tekst bevatten na Hallo eerst '? ' of '#' en deze tekens zijn niet toegestaan. 

Hallo volgende voorbeeld maakt u één regel voor ' / installatiekopieën / * ' pad routering verkeer tooback-end 'imagesBackendPool'. Deze regel zorgt ervoor dat verkeer voor elke set van URL's gerouteerde toohello back-end. Bijvoorbeeld: http://adatum.com/images/figure1.jpg gaat te 'imagesBackendPool'. Als het pad Hallo komt niet overeen met de vooraf gedefinieerde padregels hello, configureert pad Hallo-kaart regelconfiguratie ook een standaard back-end-adresgroep. Http://adatum.com/shoppingcart/test.html geldt bijvoorbeeld toopool1 zoals deze is gedefinieerd als de standaardgroep Hallo voor niet-overeenkomende verkeer.

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a>Volgende stappen

Als u toolearn over Secure Sockets Layer (SSL)-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl-cli.md).


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
