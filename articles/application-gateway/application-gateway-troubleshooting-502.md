---
title: Azure Application Gateway ongeldige Gateway (502) fouten oplossen | Microsoft Docs
description: Meer informatie over het oplossen van Application Gateway 502-fouten
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
ms.openlocfilehash: cbf9c552c4818b3925f449081539f1db6d61918e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>Ongeldige gateway-probleemoplossing in Application Gateway

Informatie over het oplossen van problemen met ongeldige gateway (502) fouten die zijn ontvangen wanneer u de toepassingsgateway.

## <a name="overview"></a>Overzicht

Na het configureren van een application gateway is een van de fouten die gebruikers kunnen ondervinden ' Server-fout: 502 - in webserver heeft een ongeldig antwoord ontvangen terwijl deze fungeerde als gateway of proxy '. Deze fout kan optreden als gevolg van de belangrijkste oorzaken:

* Azure Application Gateway van [back-end-adresgroep is niet geconfigureerd of lege](#empty-backendaddresspool).
* Geen van de virtuele machines of exemplaren in [VM-Schaalset zijn in orde](#unhealthy-instances-in-backendaddresspool).
* Back-end-VM's of exemplaren van het VM-Schaalset zijn [reageert niet op de standaard health test](#problems-with-default-health-probe.md).
* Ongeldige of onjuiste [configuratie van aangepaste statuscontroles](#problems-with-custom-health-probe.md).
* [Aanvraag-time-out- of verbindingsproblemen](#request-time-out) met aanvragen van gebruikers.

## <a name="empty-backendaddresspool"></a>Lege BackendAddressPool

### <a name="cause"></a>Oorzaak

Als de toepassingsgateway heeft geen virtuele machines of VM-Schaalset in de back-end-adresgroep geconfigureerd, kan niet alle klantaanvraag routeren en een ongeldige gateway-fout genereert.

### <a name="solution"></a>Oplossing

Zorg ervoor dat de back-end-adresgroep is niet leeg. Dit kan worden gedaan hetzij via PowerShell, CLI of -portal.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

De uitvoer van de voorgaande cmdlet moet niet-lege back-end-adresgroep bevatten. Hieronder volgt een voorbeeld waarin twee groepen worden geretourneerd die zijn geconfigureerd met de FQDN-naam of IP-adressen voor back-end virtuele machines. De Inrichtingsstatus van de BackendAddressPool moet worden 'is voltooid'.

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

Als alle exemplaren van BackendAddressPool niet in orde zijn, klikt u vervolgens Application Gateway geen een back-end kan route gebruikersaanvraag tot. Dit mogelijk ook het geval wanneer back-end-exemplaren in orde zijn, maar niet de vereiste toepassing geïmplementeerd hebben.

### <a name="solution"></a>Oplossing

Zorg ervoor dat de exemplaren in orde zijn en de toepassing correct is geconfigureerd. Controleer of de back-end-exemplaren kunnen reageren op een ping naar een andere virtuele machine in hetzelfde VNet zijn. Als met een openbaar eindpunt is geconfigureerd, moet u zorgen dat de aanvraag van een browser naar de webtoepassing geschikte.

## <a name="problems-with-default-health-probe"></a>Problemen met standaard health test

### <a name="cause"></a>Oorzaak

502 fouten kunnen ook worden regelmatig indicatoren de standaard health test is niet kunnen bereiken back-end virtuele machines. Wanneer een exemplaar van Application Gateway is geconfigureerd, configureert het automatisch een standaard health test naar elke BackendAddressPool met behulp van de eigenschappen van de BackendHttpSetting. Er is geen gebruikersinvoer is vereist voor het instellen van deze test. In het bijzonder wanneer een taakverdelingsregel is geconfigureerd, wordt een koppeling gemaakt tussen een BackendHttpSetting en BackendAddressPool. Een standaard-test is geconfigureerd voor elk van deze koppelingen en Application Gateway een periodieke controle-verbinding met elk exemplaar in de BackendAddressPool op de opgegeven poort in het element BackendHttpSetting initieert. Volgende tabel bevat de waarden die zijn gekoppeld aan de standaard health test.

| Test-eigenschap | Waarde | Beschrijving |
| --- | --- | --- |
| WebTest-URL |http://127.0.0.1/ |URL-pad |
| Interval |30 |Testinterval in seconden |
| Time-out |30 |Test time-out in seconden |
| Drempelwaarde voor onjuiste status |3 |Aantal nieuwe pogingen-test. De back-endserver is gemarkeerd als niet actief nadat de foutentelling opeenvolgende test heeft de drempelwaarde voor onjuiste status bereikt. |

### <a name="solution"></a>Oplossing

* Zorg ervoor dat een standaard-site is geconfigureerd en luistert naar de 127.0.0.1.
* Als BackendHttpSetting is opgegeven voor een andere poort dan 80, moet u de standaardsite geconfigureerd om te luisteren op poort.
* De aanroep van http://127.0.0.1:port moet de resultaatcode van een HTTP 200 retourneren. Dit moet worden geretourneerd binnen de time-outperiode van 30 seconden.
* Zorg ervoor dat poort geconfigureerd open is en dat er zijn geen firewallregels of Azure-Netwerkbeveiligingsgroepen, dit blokkeren van binnenkomend of uitgaand verkeer op de poort die is geconfigureerd.
* Als Azure classic VM's of een Cloudservice met de FQDN-naam of het openbare IP-adres wordt gebruikt, zorg ervoor dat de bijbehorende [eindpunt](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) wordt geopend.
* Als de virtuele machine via Azure Resource Manager is geconfigureerd en buiten het VNet waar Application Gateway wordt geïmplementeerd ligt, [Netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) moet worden geconfigureerd voor toegang op de gewenste poort.

## <a name="problems-with-custom-health-probe"></a>Problemen met aangepaste health test

### <a name="cause"></a>Oorzaak

Aangepaste statuscontroles kunnen extra flexibiliteit op de standaardwaarde probing gedrag. Wanneer u aangepaste tests, kunnen gebruikers de testinterval, de URL en pad voor het testen en hoeveel mislukte reacties op accepteren voordat de back-endpool-instantie als beschadigd gemarkeerd configureren. De volgende aanvullende eigenschappen worden toegevoegd.

| Test-eigenschap | Beschrijving |
| --- | --- |
| Naam |Naam van de test. Deze naam wordt gebruikt om te verwijzen naar de instellingen voor back-end-HTTP-test. |
| Protocol |Het protocol dat wordt gebruikt voor het verzenden van de test. De test wordt gebruikt voor het protocol dat is gedefinieerd in de back-end-HTTP-instellingen |
| Host |De hostnaam voor het verzenden van de test. Alleen van toepassing wanneer meerdere locaties op Application Gateway is geconfigureerd. Dit wijkt af van de VM-hostnaam. |
| Pad |Relatieve pad van de test. Het pad geldig wordt gestart vanuit '/'. De test wordt verzonden naar \<protocol\>://\<host\>:\<poort\>\<pad\> |
| Interval |WebTest interval in seconden. Dit is het interval tussen twee opeenvolgende tests. |
| Time-out |WebTest time-outwaarde in seconden. Als een geldig antwoord niet binnen deze time-outperiode ontvangen is, wordt de test als mislukt gemarkeerd. |
| Drempelwaarde voor onjuiste status |Aantal nieuwe pogingen-test. De back-endserver is gemarkeerd als niet actief nadat de foutentelling opeenvolgende test heeft de drempelwaarde voor onjuiste status bereikt. |

### <a name="solution"></a>Oplossing

Valideren dat de aangepaste Health test is geconfigureerd als de voorgaande tabel. Naast de voorgaande stappen voor probleemoplossing, zorg er ook voor het volgende:

* Zorg ervoor dat de test juist is opgegeven conform de [handleiding](application-gateway-create-probe-ps.md).
* Als Application Gateway is geconfigureerd voor een enkele site, standaard ingesteld op de Host moet naam worden opgegeven als '127.0.0.1', tenzij anders is geconfigureerd in aangepaste test.
* Zorg ervoor dat een aanroep naar http://\<host\>:\<poort\>\<pad\> retourneert de resultaatcode van een HTTP 200.
* Zorg ervoor dat Interval, Time-out en UnhealtyThreshold in het acceptabele bereik liggen.
* Als via een HTTPS-test, ervoor zorgen dat de back-endserver SNI geen vereist door een fallback-certificaat op de back-endserver zelf configureren. 
* Zorg ervoor dat Interval, Time-out en UnhealtyThreshold in het acceptabele bereik liggen.

## <a name="request-time-out"></a>Time-out aanvraag

### <a name="cause"></a>Oorzaak

Wanneer een gebruikersaanvraag wordt ontvangen, wordt Application Gateway de geconfigureerde regels van toepassing is op de aanvraag en doorgestuurd naar een exemplaar van de back-end-pool. Er wordt gewacht op een configureerbare tijdsinterval op een reactie van de back-end-exemplaar. Dit interval is standaard **30 seconden**. Als Application Gateway geen reactie van de back-endtoepassing in dit interval ontvangen heeft, ziet aanvraag van de gebruiker een 502-fout.

### <a name="solution"></a>Oplossing

Toepassingsgateway kan gebruikers deze instelling via BackendHttpSetting, die vervolgens kan worden toegepast op verschillende groepen wilt configureren. Verschillende groepen van de back-end kunnen hebben verschillende BackendHttpSetting en daarom verschillende aanvraag time-outwaarde is geconfigureerd.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>Volgende stappen

Als de voorgaande stappen het probleem niet verhelpen, opent u een [ondersteunen ticket](https://azure.microsoft.com/support/options/).

