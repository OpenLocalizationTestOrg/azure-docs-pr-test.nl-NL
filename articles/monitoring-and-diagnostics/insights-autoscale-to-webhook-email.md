---
title: aaaUse automatisch schalen acties toosend e-mail en -webhook waarschuwingsmeldingen. | Microsoft Docs
description: 'Zie hoe toouse automatisch schalen acties toocall web-URL''s of verzenden van e-mailmeldingen in de Azure-Monitor. '
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a>Gebruik voor automatisch schalen acties toosend e-mail en -webhook waarschuwingsmeldingen in de Azure-Monitor
Dit artikel ziet u hoe u triggers hebt instelt, zodat u kunt specifieke web-URL's aanroepen of verzenden van e-mailberichten op basis van de acties voor automatisch schalen in Azure.  

## <a name="webhooks"></a>Webhooks.
Webhooks kunt u tooroute hello Azure waarschuwingsmeldingen tooother systemen voor na verwerking of aangepaste meldingen. Bijvoorbeeld een team chat gebruiken of messaging-services de hoogte stellen routering Hallo waarschuwing tooservices dat een binnenkomende web aanvraag toosend SMS, meld bugs kan verwerken, enz. Hallo webhook URI moet een geldige HTTP of HTTPS-eindpunt.

## <a name="email"></a>E-mail
E-mail kan worden verstuurd tooany geldig e-mailadres. Beheerders en medebeheerders van Hallo abonnement waarbij Hallo-regel wordt uitgevoerd, wordt ook gewaarschuwd.

## <a name="cloud-services-and-web-apps"></a>Cloudservices en Web-Apps
U kunt aanmelden van hello Azure-portal voor Cloudservices en serverfarms (Web-Apps).

* Kies Hallo **schalen door** metriek.

![schalen door](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>Virtuele-machineschaalsets
Voor nieuwere virtuele Machines met Resource Manager (virtuele-machineschaalsets) gemaakt, kunt u dit met behulp van REST-API, Resource Manager-sjablonen, PowerShell en CLI. De interface van de portal is nog niet beschikbaar.
Wanneer u Hallo REST-API of Resource Manager-sjabloon, neemt u Hallo meldingen element Hello opties te volgen.

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| Veld | Verplichte? | Beschrijving |
| --- | --- | --- |
| bewerking |Ja |de waarde moet 'Schaal' |
| sendToSubscriptionAdministrator |Ja |waarde moet 'true' of 'false' |
| sendToSubscriptionCoAdministrators |Ja |waarde moet 'true' of 'false' |
| customEmails |Ja |mogelijke waarden zijn null [] of string-matrix van e-mailberichten |
| Webhooks. |Ja |mogelijke waarden zijn null of geldig Uri |
| serviceUri |Ja |een geldige https Uri |
| properties |Ja |waarde moet leeg {} opzoeken of sleutel-waardeparen kan bevatten |

## <a name="authentication-in-webhooks"></a>Verificatie in webhooks.
Hallo webhook kunt verifiëren met behulp van verificatie op basis van tokens opslaglocatie Hallo webhook URI met een token ID als een queryparameter. Bijvoorbeeld: https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue

## <a name="autoscale-notification-webhook-payload-schema"></a>Schema voor automatisch schalen melding webhook nettolading
Wanneer Hallo automatisch schalen melding wordt gegenereerd, is hello volgende metagegevens opgenomen in de nettolading van de webhook Hallo:

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| Veld | Verplichte? | Beschrijving |
| --- | --- | --- |
| status |Ja |Hallo-status die aangeeft dat een actie voor automatisch schalen die is gegenereerd |
| bewerking |Ja |Voor een verhoging van exemplaren zal moeten 'Scale Out' en voor een afname in exemplaren, deze 'Schaal In' |
| Context |Ja |Hallo automatisch schalen actie context |
| tijdstempel |Ja |Tijdstempel wanneer Hallo automatisch schalen actie is geactiveerd |
| id |Ja |Bronnenbeheerder-ID van het Hallo-instelling voor automatisch schalen |
| naam |Ja |Hallo-naam van het Hallo-instelling voor automatisch schalen |
| Meer informatie |Ja |Uitleg van Hallo-actie die automatisch schalen service Hallo heeft ondernomen en Hallo in Hallo-exemplaren wijzigen |
| subscriptionId |Ja |Abonnement-ID van de doelbron Hallo die wordt geschaald |
| resourceGroupName |Ja |Naam van de resourcegroep van Hallo doelresource die wordt geschaald |
| resourceName |Ja |Naam van de doelbron Hallo die wordt geschaald |
| resourceType |Ja |Hallo drie ondersteunde waarden: 'microsoft.classiccompute/domainnames/slots/roles' - functies, 'microsoft.compute/virtualmachinescalesets' - virtuele Machine-Schaalsets, en 'Microsoft.Web/serverfarms' - Web-App Service in de Cloud |
| resourceId |Ja |Bronnenbeheerder-ID van Hallo doelresource die wordt geschaald |
| portalLink |Ja |Azure portal-koppeling toohello overzichtspagina van Hallo doelbron |
| oldCapacity |Ja |Hallo huidige (oude) aantal exemplaren wanneer automatisch schalen een schaalactie heeft |
| newCapacity |Ja |Hallo nieuwe aantal exemplaren dat automatisch schalen Hallo resource te geschaald|
| Eigenschappen |Nee |Optioneel. Reeks < sleutel, waarde > paren (bijvoorbeeld woordenlijst < String, String >). Hallo eigenschappenveld is optioneel. In een aangepaste gebruikersinterface of Logic app op basis van werkstroom, kunt u sleutels en waarden die kunnen worden doorgegeven met Hallo nettolading. Aangepaste eigenschappen toopass toohello uitgaande webhook aanroep back andere manier is toouse hello webhook URI zelf (als queryparameters) |
