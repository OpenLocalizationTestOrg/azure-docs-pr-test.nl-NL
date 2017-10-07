---
title: aaaIntroduction tooresource probleemoplossing in Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van de mogelijkheden van Hallo netwerk-Watcher resource voor probleemoplossing
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a>Inleiding tooresource probleemoplossing in Azure-netwerk-Watcher

Virtuele netwerkgateways bieden connectiviteit tussen lokale bronnen en andere virtuele netwerken in Azure. Bewaking van deze gateways en hun verbindingen is essentieel tooensuring communicatie is niet verbroken. Netwerk-Watcher Hallo mogelijkheid tootroubleshoot biedt virtuele netwerkgateways en verbindingen. Dit kan worden aangeroepen via Hallo-portal, PowerShell, CLI of REST-API. Als deze wordt aangeroepen, diagnoses netwerk-Watcher Hallo status van de virtuele netwerkgateway Hallo of verbinding en return Hallo juiste resultaten. Deze aanvraag is een langdurige transactie, worden Hallo resultaten geretourneerd wanneer Hallo diagnose voltooid is.

![portal][2]

## <a name="results"></a>Resultaten

Hallo voorlopige resultaten geretourneerd geven een overzicht van Hallo-status van het Hallo-resource. Meer gedetailleerde informatie kan worden opgegeven voor resources, zoals wordt weergegeven in de volgende sectie Hallo:

Hallo volgende lijst bevat Hallo waarden geretourneerd met de Hallo API oplossen:

* **startTime** -deze waarde is Hallo tijd Hallo oplossen API-aanroep is gestart.
* **endTime** -deze waarde is Hallo tijd waarop het oplossen van Hallo is beëindigd.
* **code** -deze waarde is niet in orde, als er een fout één diagnose.
* **resultaten** -resultaten is een verzameling van resultaten op Hallo verbinding of Hallo virtuele netwerkgateway.
    * **id** -deze waarde is het fouttype Hallo.
    * **Samenvatting** -deze waarde is een overzicht van Hallo veroorzaakt.
    * **gedetailleerde** -deze waarde bevat een gedetailleerde beschrijving van het Hallo-fout.
    * **recommendedActions** -deze eigenschap is een verzameling aanbevolen acties tootake.
      * **actionText** -deze waarde bevat Hallo beschrijvende tekst voor welke tootake in te grijpen.
      * **actionUri** -Hallo URI toodocumentation vindt u deze waarde voor het tooact.
      * **actionUriText** -deze waarde is een korte beschrijving van Hallo actietekst.

Hallo volgende tabellen tonen Hallo verschillende domeinen met fouten typen (id onder de resultaten van de voorgaande lijst Hallo) die beschikbaar zijn en als Hallo veroorzaakt Logboeken maakt.

### <a name="gateway"></a>Gateway

| Fouttype | Reden | Logboek|
|---|---|---|
| NoFault | Wanneer er geen fout wordt gedetecteerd. |Ja|
| GatewayNotFound | Kan de Gateway of Gateway niet is ingericht niet vinden. |Nee|
| PlannedMaintenance |  Gateway-instantie is in onderhoud.  |Nee|
| UserDrivenUpdate | Wanneer een gebruiker wordt bijgewerkt. Dit wordt mogelijk een bewerking formaat wijzigen. | Nee |
| VipUnResponsive | Kan de primaire instantie Hallo Hallo Gateway niet bereiken. Dit gebeurt wanneer Hallo health test is mislukt. | Nee |
| PlatformInActive | Er is een probleem met het Hallo-platform. | Nee|
| ServiceNotRunning | Hallo onderliggende service is niet uitgevoerd. | Nee|
| NoConnectionsFoundForGateway | Er bestaat geen verbindingen op Hallo-gateway. Dit is alleen een waarschuwing.| Nee|
| ConnectionsNotConnected | Verbindingen zijn niet verbonden. Dit is alleen een waarschuwing.| Ja|
| GatewayCPUUsageExceeded | de huidige Gateway CPU-gebruik Hallo is > 95%. | Ja |

### <a name="connection"></a>Verbinding

| Fouttype | Reden | Logboek|
|---|---|---|
| NoFault | Wanneer er geen fout wordt gedetecteerd. |Ja|
| GatewayNotFound | Kan de Gateway of Gateway niet is ingericht niet vinden. |Nee|
| PlannedMaintenance | Gateway-instantie is in onderhoud.  |Nee|
| UserDrivenUpdate | Wanneer een gebruiker wordt bijgewerkt. Dit wordt mogelijk een bewerking formaat wijzigen.  | Nee |
| VipUnResponsive | Kan de primaire instantie Hallo Hallo Gateway niet bereiken. Dit gebeurt als Hallo health test is mislukt. | Nee |
| ConnectionEntityNotFound | Verbindingsconfiguratie ontbreekt. | Nee |
| ConnectionIsMarkedDisconnected | Hallo verbinding is gemarkeerd als 'verbinding verbroken'. |Nee|
| ConnectionNotConfiguredOnGateway | onderliggende Hallo-service heeft geen Hallo-verbinding geconfigureerd. | Ja |
| ConnectionMarkedStandy | Hallo onderliggende service is gemarkeerd als stand-by.| Ja|
| Authentication | Vooraf gedeelde sleutel komt niet overeen. | Ja|
| PeerReachability | Hallo peer gateway is niet bereikbaar. | Ja|
| IkePolicyMismatch | Hallo peer gateway heeft IKE-beleidsregels die worden niet ondersteund door Azure. | Ja|
| WfpParse fout | Er is een fout opgetreden bij het parseren Hallo WFP-logboek. |Ja|

## <a name="supported-gateway-types"></a>Ondersteunde gatewaytypen

Hallo volgende lijst bevat Hallo ondersteuning ziet u welke gateways en verbindingen worden ondersteund bij het oplossen van netwerk-Watcher.
|  |  |
|---------|---------|
|**Gatewaytypen**   |         |
|VPN      | Ondersteund        |
|ExpressRoute | Niet ondersteund |
|Hypernet | Niet ondersteund|
|**VPN-typen** | |
|Route gebaseerd | Ondersteund|
|Op basis van beleid | Niet ondersteund|
|**Verbindingstypen**||
|IPSec| Ondersteund|
|VNet2Vnet| Ondersteund|
|ExpressRoute| Niet ondersteund|
|Hypernet| Niet ondersteund|
|VPNClient| Niet ondersteund|

## <a name="log-files"></a>Logboekbestanden

Hallo resource voor probleemoplossing logboekbestanden worden opgeslagen in een opslagaccount nadat de resource probleemoplossing is voltooid. Hallo toont volgende afbeelding Hallo voorbeeld van de inhoud van een aanroep van dat heeft geresulteerd in een fout opgetreden.

![ZIP-bestand][1]

> [!NOTE]
> In sommige gevallen wordt alleen een subset van de logboekbestanden Hallo toostorage geschreven.

Voor instructies over het downloaden van bestanden van azure storage-accounts, Raadpleeg te[aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer. Meer informatie over Opslagverkenner vindt u hier op Hallo koppeling: [Opslagverkenner](http://storageexplorer.com/)

### <a name="connectionstatstxt"></a>ConnectionStats.txt

Hallo **ConnectionStats.txt** bestand bevat de algemene statistieken Hallo-verbinding, met inbegrip van inkomende en uitgaande bytes, de status van de verbinding en Hallo tijd Hallo verbinding tot stand is gebracht.

> [!NOTE]
> Als Hallo aanroep toohello probleemoplossing API in orde retourneert, Hallo geretourneerd in het zip-bestand Hallo heeft alleen een **ConnectionStats.txt** bestand.

Hallo-inhoud van dit bestand zijn vergelijkbaar toohello voorbeeld te volgen:

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a>CPUStats.txt

Hallo **CPUStats.txt** -bestand bevat CPU-gebruik en geheugen beschikbaar op Hallo tijdstip van de testen.  Hallo-inhoud van dit bestand is vergelijkbaar toohello voorbeeld te volgen:

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a>IKEErrors.txt

Hallo **IKEErrors.txt** bestand bevat alle IKE-fouten die zijn gevonden tijdens de bewaking.

Hallo ziet volgende voorbeeld Hallo inhoud van een bestand IKEErrors.txt. Uw fouten kunnen afwijken, afhankelijk van Hallo probleem.

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a>Verwijderd wfpdiag.txt

Hallo **Scrubbed wfpdiag.txt** logboekbestand Hallo wfp-logboek bevat. Dit logboek bevat de logboekregistratie van het pakket verwijderen en IKE/AuthIP fouten.

Hallo ziet volgende voorbeeld Hallo inhoud van Hallo Scrubbed wfpdiag.txt bestand. In dit voorbeeld is Hallo gedeelde sleutel van een verbinding niet juist kan worden afgeleid uit 3e regel Hallo van Hallo onder. Hallo volgende voorbeeld is alleen een fragment van de hele logboek Hallo, zoals Hallo logboek langdurige, afhankelijk van Hallo probleem kan worden.

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a>wfpdiag.txt.Sum

Hallo **wfpdiag.txt.sum** bestand is een logboek met Hallo buffers en gebeurtenissen verwerkt.

Hallo is volgende voorbeeld Hallo inhoud van een bestand wfpdiag.txt.sum.
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toodiagnose VPN-Gateways en verbindingen via portal Hallo in via [Gateway probleemoplossing - Azure-portal](network-watcher-troubleshoot-manage-portal.md).
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
