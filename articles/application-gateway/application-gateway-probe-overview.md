---
title: overzicht van bewaking voor Azure Application Gateway aaaHealth | Microsoft Docs
description: Meer informatie over Hallo bewakingsmogelijkheden in Azure Application Gateway
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 5091d80394a354ff849ce7ccee8cc9d2fd0456db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-health-monitoring-overview"></a>Overzicht van Application Gateway health monitoring

Azure Application Gateway standaard bewaakt Hallo status van alle resources in de back-end-pool en worden alle bronnen die niet in orde beschouwd uit Hallo groep automatisch verwijderd. Toepassingsgateway blijft toomonitor Hallo slecht exemplaren en voegt deze toe back-toohello goede back-end-pool zodra deze beschikbaar komen en reageren toohealth-tests. Toepassingsgateway verzendt Hallo statuscontroles Hello dezelfde poort die is gedefinieerd in Hallo back-end-HTTP-instellingen. Deze configuratie zorgt ervoor dat Hallo-test is het testen van Hallo dezelfde poort dat klanten tooconnect toohello back-end gebruikt.

![Voorbeeld van de test Application gateway][1]

In de toevoeging toousing standaard health test bewaking, kunt u ook aanpassen Hallo health test toosuit vereisten van uw toepassing. In dit artikel, zowel standaard en aangepaste statuscontroles vallen.

> [!NOTE]
> Als er een NSG op Application Gateway-subnet, moeten poortbereiken 65503 65534 geopend zijn op Hallo Application Gateway-subnet voor binnenkomend verkeer. Deze poorten zijn vereist voor Hallo back-end health API toowork.

## <a name="default-health-probe"></a>Standaard health test

Een application gateway wordt een standaard health test automatisch geconfigureerd wanneer u een aangepaste test-configuratie niet instellen. bewaking van gedrag Hallo werkt door maken die een HTTP-aanvraag toohello IP-adressen geconfigureerd voor back-end-pool Hallo. Voor standaard tests als Hallo back-end-HTTP-instellingen zijn geconfigureerd voor HTTPS, Hallo test maakt gebruik van HTTPS als de status goed tootest van Hallo back-ends.

Bijvoorbeeld: U uw toepassing gateway toouse back-endservers A, B en C tooreceive HTTP-netwerkverkeer op poort 80 configureren. Hallo standaard statuscontrole test Hallo drie servers elke 30 seconden voor een goede HTTP-antwoord. Een gezonde HTTP-antwoord heeft een [statuscode](https://msdn.microsoft.com/library/aa287675.aspx) tussen 200 en 399.

Als Hallo standaard test controle voor server A mislukt, toepassingsgateway hello, wordt deze verwijderd uit de back-end-pool en netwerkverkeer stopt stromende toothis-server. Hallo standaard test blijft toocheck voor server nog steeds een elke 30 seconden. Wanneer een server met succes tooone aanvraag van een standaard health test reageert, wordt deze weer toegevoegd als in orde toohello back-end-pool en het verkeer wordt gestart toohello server opnieuw.

### <a name="default-health-probe-settings"></a>Standaardinstellingen health test

| Test-eigenschap | Waarde | Beschrijving |
| --- | --- | --- |
| WebTest-URL |http://127.0.0.1:\<poort\>/ |URL-pad |
| Interval |30 |Testinterval in seconden |
| Time-out |30 |Test time-out in seconden |
| Drempelwaarde voor onjuiste status |3 |Aantal nieuwe pogingen-test. Hallo back-end-server is gemarkeerd als niet actief nadat Hallo opeenvolgende test foutentelling Hallo slecht drempel bereikt. |

> [!NOTE]
> Hallo poort is Hallo dezelfde poort als Hallo back-end-HTTP-instellingen.

Hallo standaard test wordt bekeken alleen http://127.0.0.1:\<poort\> toodetermine gezondheidsstatus. Als u tooconfigure Hallo health test toogo tooa aangepaste URL moet of andere instellingen te wijzigen, moet u aangepaste tests gebruiken zoals beschreven in Hallo stappen te volgen:

## <a name="custom-health-probe"></a>Aangepaste health test

Aangepaste tests kunnen u een gedetailleerdere controle over het Hallo-statuscontrole toohave. Wanneer u aangepaste tests, kunt u het testinterval Hallo Hallo-URL en het pad tootest en hoeveel mislukte reacties tooaccept voordat Hallo back-end-pool exemplaar als beschadigd gemarkeerd.

### <a name="custom-health-probe-settings"></a>Instellingen voor de test aangepaste status

Hallo bevat volgende tabel definities voor Hallo eigenschappen van een aangepaste health test.

| Test-eigenschap | Beschrijving |
| --- | --- |
| Naam |Naam van het Hallo-test. Deze naam wordt gebruikt toorefer toohello test in de back-end-HTTP-instellingen. |
| Protocol |Protocol gebruikt toosend Hallo test. Hallo test gebruikt Hallo-protocol gedefinieerd in Hallo back-end-HTTP-instellingen |
| Host |Host naam toosend Hallo test. Van toepassing alleen als er meerdere locaties is geconfigureerd op Application Gateway, of gebruik anders '127.0.0.1'. Deze waarde verschilt van de VM-hostnaam. |
| Pad |Relatieve pad van het Hallo-test. Hallo geldig pad wordt gestart vanuit '/'. |
| Interval |WebTest interval in seconden. Deze waarde is Hallo tijdsinterval tussen twee opeenvolgende tests. |
| Time-out |WebTest time-outwaarde in seconden. Als een geldig antwoord niet binnen deze time-outperiode ontvangen is, wordt Hallo test als mislukt gemarkeerd.  |
| Drempelwaarde voor onjuiste status |Aantal nieuwe pogingen-test. Hallo back-end-server is gemarkeerd als niet actief nadat Hallo opeenvolgende test foutentelling Hallo slecht drempel bereikt. |

> [!IMPORTANT]
> Als Application Gateway is geconfigureerd voor een enkele site, door standaard Hallo Host moet naam worden opgegeven als '127.0.0.1', tenzij anders is geconfigureerd in aangepaste test.
> Ter referentie een aangepaste test te verzonden\<protocol\>://\<host\>:\<poort\>\<pad\>. Hallo-poort die gebruikt worden dezelfde poort Hallo zoals gedefinieerd in Hallo back-end-HTTP-instellingen.

## <a name="next-steps"></a>Volgende stappen
Nadat de informatie over Application Gateway statuscontrole, kunt u configureren een [aangepaste health test](application-gateway-create-probe-portal.md) in hello Azure-portal of een [aangepaste health test](application-gateway-create-probe-ps.md) met PowerShell en hello Azure Resource Manager implementatiemodel.

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png
