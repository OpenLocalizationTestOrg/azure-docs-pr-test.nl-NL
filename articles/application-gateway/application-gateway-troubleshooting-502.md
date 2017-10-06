---
title: Azure Application Gateway ongeldige Gateway (502)-fouten aaaTroubleshoot | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Application Gateway 502-fouten
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>Ongeldige gateway-probleemoplossing in Application Gateway

Meer informatie over hoe tootroubleshoot Ongeldige gateway (502) fouten ontvangen wanneer u de toepassingsgateway.

## <a name="overview"></a>Overzicht

Na het configureren van een application gateway is een Hallo fouten die gebruikers kunnen ondervinden ' Server-fout: 502 - in webserver heeft een ongeldig antwoord ontvangen terwijl deze fungeerde als gateway of proxy '. Deze fout kan optreden vanwege de volgende toohello belangrijkste redenen:

* Azure Application Gateway van [back-end-adresgroep is niet geconfigureerd of lege](#empty-backendaddresspool).
* Geen van de Hallo virtuele machines of exemplaren in [VM-Schaalset zijn in orde](#unhealthy-instances-in-backendaddresspool).
* Back-end-VM's of exemplaren van het VM-Schaalset zijn [reageert niet toohello standaard health test](#problems-with-default-health-probe.md).
* Ongeldige of onjuiste [configuratie van aangepaste statuscontroles](#problems-with-custom-health-probe.md).
* [Aanvraag-time-out- of verbindingsproblemen](#request-time-out) met aanvragen van gebruikers.

## <a name="empty-backendaddresspool"></a>Lege BackendAddressPool

### <a name="cause"></a>Oorzaak

Als Hallo Application Gateway geen VM's heeft of VM-Schaalset geconfigureerd in het back-end-adresgroep hello, kan niet alle klantaanvraag routeren en een ongeldige gateway-fout genereert.

### <a name="solution"></a>Oplossing

Zorg ervoor dat Hallo back-end-adresgroep is niet leeg. Dit kan worden gedaan hetzij via PowerShell, CLI of -portal.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

Hallo-uitvoer van Hallo voorafgaand aan de cmdlet moet niet-lege back-end-adresgroep bevatten. Hieronder volgt een voorbeeld waarin twee groepen worden geretourneerd die zijn geconfigureerd met de FQDN-naam of IP-adressen voor back-end virtuele machines. Hallo Inrichtingsstatus Hallo BackendAddressPool moet worden 'is voltooid'.

BackendAddressPoolsText:

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a>Slechte exemplaren in BackendAddressPool

### <a name="cause"></a>Oorzaak

Als alle Hallo exemplaren van BackendAddressPool niet in orde zijn, klikt u vervolgens Application Gateway geen een back-end tooroute gebruikersaanvraag tot. Dit kan ook Hallo geval zijn wanneer back-end-exemplaren in orde zijn, maar nog geen toepassing hello vereist die zijn geïmplementeerd.

### <a name="solution"></a>Oplossing

Zorg ervoor dat Hallo exemplaren zijn in orde en Hallo toepassing correct is geconfigureerd. Selectievakje Hallo als Hallo back-end-exemplaren kunnen toorespond tooa ping uit een andere virtuele machine in hetzelfde VNet. Als met een openbaar eindpunt is geconfigureerd, zorg ervoor dat een webtoepassing browser aanvraag toohello geschikte is.

## <a name="problems-with-default-health-probe"></a>Problemen met standaard health test

### <a name="cause"></a>Oorzaak

502 fouten kunnen ook worden regelmatig indicatoren die Hallo standaard health test is niet mogelijk tooreach back-end virtuele machines. Wanneer een exemplaar van Application Gateway is geconfigureerd, configureert het automatisch een standaard health test tooeach BackendAddressPool met behulp van de eigenschappen van Hallo BackendHttpSetting. Er is geen gebruikersinvoer is vereist tooset deze test. In het bijzonder wanneer een taakverdelingsregel is geconfigureerd, wordt een koppeling gemaakt tussen een BackendHttpSetting en BackendAddressPool. Een standaard-test is geconfigureerd voor elk van deze koppelingen en Application Gateway initieert een periodieke controle verbinding tooeach exemplaar in Hallo BackendAddressPool op Hallo opgegeven poort in Hallo BackendHttpSetting element. Volgende tabel bevat Hallo waarden die zijn gekoppeld aan Hallo standaard health test.

| Test-eigenschap | Waarde | Beschrijving |
| --- | --- | --- |
| WebTest-URL |http://127.0.0.1/ |URL-pad |
| Interval |30 |Testinterval in seconden |
| Time-out |30 |Test time-out in seconden |
| Drempelwaarde voor onjuiste status |3 |Aantal nieuwe pogingen-test. Hallo back-end-server is gemarkeerd als niet actief nadat Hallo opeenvolgende test foutentelling Hallo slecht drempel bereikt. |

### <a name="solution"></a>Oplossing

* Zorg ervoor dat een standaard-site is geconfigureerd en luistert naar de 127.0.0.1.
* Als BackendHttpSetting is opgegeven voor een andere poort dan 80, moet standaardsite Hallo geconfigureerde toolisten op deze poort.
* Hallo moet aanroep toohttp://127.0.0.1:port retourneren de resultaatcode van een HTTP 200. Dit moet worden geretourneerd binnen de time-outperiode voor Hallo 30 seconden.
* Zorg ervoor dat poort geconfigureerd open is en dat er zijn geen firewallregels of Azure-Netwerkbeveiligingsgroepen, dit blokkeren van binnenkomend of uitgaand verkeer op Hallo poort geconfigureerd.
* Als Azure classic VM's of een Cloudservice met de FQDN-naam of het openbare IP-adres wordt gebruikt, zorg ervoor dat Hallo er overeenkomende [eindpunt](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) wordt geopend.
* Als Hallo VM via Azure Resource Manager is geconfigureerd en buiten Hallo VNet waar Application Gateway wordt geïmplementeerd, [Netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) moet worden geconfigureerd tooallow toegang op Hallo gewenst poort.

## <a name="problems-with-custom-health-probe"></a>Problemen met aangepaste health test

### <a name="cause"></a>Oorzaak

Aangepaste statuscontroles kunnen extra flexibiliteit toohello standaard probing gedrag. Wanneer u aangepaste tests, kunnen gebruikers het testinterval hello, Hallo-URL, en pad tootest en hoeveel mislukte reacties tooaccept configureren voordat Hallo back-end-pool exemplaar als beschadigd gemarkeerd. Hallo volgende extra eigenschappen worden toegevoegd.

| Test-eigenschap | Beschrijving |
| --- | --- |
| Naam |Naam van het Hallo-test. Deze naam wordt gebruikt toorefer toohello test in de back-end-HTTP-instellingen. |
| Protocol |Protocol gebruikt toosend Hallo test. Hallo test gebruikt Hallo-protocol gedefinieerd in Hallo back-end-HTTP-instellingen |
| Host |Host naam toosend Hallo test. Alleen van toepassing wanneer meerdere locaties op Application Gateway is geconfigureerd. Dit wijkt af van de VM-hostnaam. |
| Pad |Relatieve pad van het Hallo-test. Hallo geldig pad wordt gestart vanuit '/'. Hallo-test wordt verzonden, te\<protocol\>://\<host\>:\<poort\>\<pad\> |
| Interval |WebTest interval in seconden. Dit is de tijdsinterval Hallo tussen twee opeenvolgende tests. |
| Time-out |WebTest time-outwaarde in seconden. Als een geldig antwoord niet binnen deze time-outperiode ontvangen is, wordt Hallo test als mislukt gemarkeerd. |
| Drempelwaarde voor onjuiste status |Aantal nieuwe pogingen-test. Hallo back-end-server is gemarkeerd als niet actief nadat Hallo opeenvolgende test foutentelling Hallo slecht drempel bereikt. |

### <a name="solution"></a>Oplossing

Valideren dat aangepaste Health test correct is geconfigureerd als de voorgaande tabel Hallo Hallo. Bovendien toohello voorgaande probleemoplossingsstappen, zorg er ook voor Hallo volgende:

* Controleer dat test Hallo juist is opgegeven volgens Hallo [handleiding](application-gateway-create-probe-ps.md).
* Als Application Gateway is geconfigureerd voor een enkele site, door standaard Hallo Host moet naam worden opgegeven als '127.0.0.1', tenzij anders is geconfigureerd in aangepaste test.
* Zorg ervoor dat een aanroep van toohttp: / /\<host\>:\<poort\>\<pad\> retourneert de resultaatcode van een HTTP 200.
* Zorg ervoor dat Interval, Time-out en UnhealtyThreshold binnen acceptabele Hallo-adresbereiken.
* Als via een HTTPS-test, ervoor zorgen dat back-endserver Hallo geen SNI vereist door een fallback-certificaat op Hallo back-endserver zelf configureren. 
* Zorg ervoor dat Interval, Time-out en UnhealtyThreshold binnen acceptabele Hallo-adresbereiken.

## <a name="request-time-out"></a>Time-out aanvraag

### <a name="cause"></a>Oorzaak

Wanneer een gebruikersaanvraag wordt ontvangen, wordt Application Gateway is van toepassing hello geconfigureerd regels toohello aanvraag en tooa back-end-pool exemplaar doorgestuurd. Er wordt gewacht op een configureerbare tijdsinterval op een reactie van Hallo back-end-exemplaar. Dit interval is standaard **30 seconden**. Als Application Gateway geen reactie van de back-endtoepassing in dit interval ontvangen heeft, ziet aanvraag van de gebruiker een 502-fout.

### <a name="solution"></a>Oplossing

Toepassingsgateway kan gebruikers tooconfigure deze instelling via BackendHttpSetting die kan worden en toodifferent pools toegepast. Verschillende groepen van de back-end kunnen hebben verschillende BackendHttpSetting en daarom verschillende aanvraag time-outwaarde is geconfigureerd.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>Volgende stappen

Als hello voorgaande stappen probleem niet hello verhelpen, opent u een [ondersteunen ticket](https://azure.microsoft.com/support/options/).

