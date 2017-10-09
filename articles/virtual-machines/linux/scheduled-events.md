---
title: aaaScheduled gebeurtenissen voor virtuele Linux-machines in Azure | Microsoft Docs
description: Geplande gebeurtenissen met Hallo metagegevens van de Azure-service voor op uw virtuele Linux-machines.
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: e153c8854725330acefd67d0ef542f6149170a7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a>Azure Service metagegevens: Geplande gebeurtenissen (Preview) voor virtuele Linux-machines

> [!NOTE] 
> Voorbeelden zijn beschikbaar tooyou er op Hallo voorwaarde toohello gebruiksvoorwaarden gaat u akkoord. Zie [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews (Microsoft Azure Aanvullende gebruiksvoorwaarden voor Microsoft Azure-previews)](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) voor meer informatie.
>

Geplande gebeurtenissen is een van de Hallo subservices onder hello Azure metagegevens Service. Is verantwoordelijk voor bepaalde informatie over toekomstige gebeurtenissen (bijvoorbeeld opstarten vereist) zodat uw toepassing kunt voor ze voorbereiden en beperkt wordt onderbroken. Het is beschikbaar voor alle virtuele Machine van Azure-typen, met inbegrip van PaaS en IaaS. Geplande gebeurtenissen geeft uw virtuele Machine tijd tooperform preventieve taken toominimize Hallo effect van een gebeurtenis. 

Geplande gebeurtenissen is beschikbaar voor zowel Windows als een virtuele Linux-machines. Zie voor meer informatie over gebeurtenissen in Windows gepland [gepland gebeurtenissen voor VM's van Windows](../windows/scheduled-events.md).

## <a name="why-scheduled-events"></a>Waarom gebeurtenissen gepland?

Met gebeurtenissen voor gepland, kunt u stappen ondernemen toolimit Hallo gevolgen van het platform intiated onderhoud of acties gebruiker gestart op uw service. 

Meerdere exemplaren werkbelastingen die gebruikmaken van replicatiestatus technieken toomaintain, is mogelijk kwetsbaar toooutages plaatsvinden voor meerdere exemplaren. Zoals storingen mogelijk dure taken (bijvoorbeeld herbouwen indexen) of zelfs een verlies van de replica. 

In veel andere gevallen hello algemene beschikbaarheid van de service kan worden verbeterd door te voeren, zoals een reeks correct afsluiten voltooit (of annuleren)-onderweg transacties, opnieuw toewijzen van taken tooother virtuele machines in Hallo-cluster (handmatige failover) of hello te verwijderen Virtuele Machine uit een groep met network load balancer. 

Er zijn ook gevallen waarbij hulp van een beheerder over een aanstaande gebeurtenis of een dergelijke gebeurtenis logboekregistratie helpen Hallo onderhoudsvriendelijkheid van toepassingen die worden gehost in de cloud Hallo verbeteren.

Azure Metadata verwerkingsinformatie gepland gebeurtenissen van de Service in de volgende Hallo gebruiksvoorbeelden:
-   Platform geïnitieerd onderhoud (bijvoorbeeld Host-OS-implementatie)
-   Gebruiker gestart aanroepen (bijvoorbeeld gebruiker opnieuw wordt opgestart of redeploys een virtuele machine)


## <a name="hello-basics"></a>Hallo-basisbeginselen  

Azure service van de metagegevens wordt informatie over het uitvoeren van virtuele Machines met een REST-eindpunt toegankelijk vanuit Hallo VM. Hallo informatie is beschikbaar via een niet-routeerbare IP-adres, zodat deze niet buiten Hallo VM weergegeven wordt.

### <a name="scope"></a>Bereik
Geplande gebeurtenissen zijn opgehaald tooall virtuele Machines in een cloudservice of tooall virtuele Machines in een Beschikbaarheidsset. Als gevolg hiervan moet u controleren Hallo `Resources` veld Hallo gebeurtenis tooidentify die virtuele machines toobe beïnvloed gaat. 

### <a name="discovering-hello-endpoint"></a>Hallo-eindpunt detecteren
In geval Hallo waarop een virtuele Machine is gemaakt vanuit een virtueel netwerk (VNet) Hallo metagegevensservice is beschikbaar via een statische niet-routeerbare IP-adres `169.254.169.254`.
Als Hallo virtuele Machine niet vanuit een virtueel netwerk, Hallo standaard gevallen voor cloudservices en klassieke virtuele machines gemaakt is, is extra logica vereist toodiscover Hallo eindpunt toouse. Raadpleeg toothis voorbeeld toolearn hoe te[Hallo host-eindpunt detecteren](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).

### <a name="versioning"></a>Versiebeheer voor onderdelen 
Hallo metagegevens-Service-exemplaar is samengesteld. Versies zijn verplicht en de huidige versie Hallo is `2017-03-01`.

> [!NOTE] 
> Eerdere versies van de preview van geplande gebeurtenissen {laatste} wordt ondersteund als Hallo api-versie. Deze indeling wordt niet meer ondersteund en in toekomstige hello wordt afgeschaft.

### <a name="using-headers"></a>Met behulp van headers
Wanneer u query Hallo Metadata Service uitvoert, moet u opgeven Hallo header `Metadata: true` tooensure Hallo verzoek is niet per ongeluk omgeleid.

### <a name="enabling-scheduled-events"></a>Geplande gebeurtenissen inschakelen
Hallo schakelt eerste keer dat u een aanvraag voor geplande gebeurtenissen Azure impliciet Hallo functie in op de virtuele Machine. U moet een vertraagde antwoord als gevolg hiervan verwacht in de eerste aanroep van up tootwo minuten.

### <a name="user-initiated-maintenance"></a>Onderhoud van de gebruiker gestarte
Gebruiker gestart onderhoud op virtuele machines via hello Azure-portal API, CLI of PowerShell resulteert in een geplande gebeurtenis. Hiermee kunt u tootest Hallo onderhoud voorbereiding logica in uw toepassing te kunnen uw toepassing tooprepare voor onderhoud van de gebruiker gestarte.

Een virtuele machine opnieuw plant u een gebeurtenis met type `Reboot`. Een virtuele machine opnieuw plant u een gebeurtenis met type `Redeploy`.

> [!NOTE] 
> Op dit moment kan maximaal 10 gebruiker gestarte onderhoudsbewerkingen worden tegelijkertijd gepland. Deze limiet wordt minder streng worden gemaakt vóór de algemene beschikbaarheid van gebeurtenissen voor gepland.

> [!NOTE] 
> Gebruiker gestarte onderhoud gepland gebeurtenissen ertoe kan momenteel niet worden geconfigureerd. Configuratiemogelijkheden is gepland voor een toekomstige release.

## <a name="using-hello-api"></a>Hallo-API gebruiken

### <a name="query-for-events"></a>Query voor gebeurtenissen
U kunt een query voor geplande gebeurtenissen gewoon doordat Hallo volgende aanroepen:

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

Een antwoord bevat een matrix van geplande gebeurtenissen. Een lege matrix betekent zijn momenteel geen gebeurtenissen die zijn gepland.
In geval van Hallo wanneer er geplande gebeurtenissen, Hallo-antwoord bevat een matrix van gebeurtenissen: 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>Eigenschappen van gebeurtenis
|Eigenschap  |  Beschrijving |
| - | - |
| Gebeurtenis-id | Globaal unieke id voor deze gebeurtenis. <br><br> Voorbeeld: <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| EventType | Impact die deze gebeurtenis wordt veroorzaakt. <br><br> Waarden: <br><ul><li> `Freeze`: Hallo virtuele Machine is geplande toopause voor enkele seconden. Hallo CPU is onderbroken, maar er zijn geen gevolgen voor geheugen, open bestanden of netwerkverbindingen. <li>`Reboot`: Hallo virtuele Machine is gepland voor opnieuw opstarten (niet-permanente geheugen is verloren gegaan). <li>`Redeploy`: Hallo virtuele Machine is geplande toomove tooanother knooppunt (kortstondige schijven gaan verloren). |
| ResourceType | Type resource dat van invloed is op deze gebeurtenis. <br><br> Waarden: <ul><li>`VirtualMachine`|
| Resources| Lijst met bronnen die van invloed is op deze gebeurtenis. Dit kan toocontain machines gegarandeerd van maximaal één [Updatedomein](manage-availability.md), maar mag niet alle machines in Hallo UD bevatten. <br><br> Voorbeeld: <br><ul><li> ['FrontEnd_IN_0', 'BackEnd_IN_0'] |
| Gebeurtenisstatus | Status van deze gebeurtenis. <br><br> Waarden: <ul><li>`Scheduled`: Deze gebeurtenis is geplande toostart na Hallo tijd die is opgegeven in Hallo `NotBefore` eigenschap.<li>`Started`: Deze gebeurtenis is gestart.</ul> Geen `Completed` of soortgelijke status ooit wordt geleverd; Hallo gebeurtenis wordt niet langer worden geretourneerd wanneer het Hallo-gebeurtenis is voltooid.
| NotBefore| De tijd waarna deze gebeurtenis wordt gestart. <br><br> Voorbeeld: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Gebeurtenis plannen
Elke gebeurtenis is gepland de minimale hoeveelheid tijd in toekomstige Hallo op basis van gebeurtenistype. Deze tijd wordt weergegeven in een gebeurtenis `NotBefore` eigenschap. 

|EventType  | Minimale kennisgeving |
| - | - |
| Blokkeren| 15 minuten |
| Opnieuw opstarten | 15 minuten |
| Opnieuw implementeren | 10 minuten |

### <a name="starting-an-event"></a>Een gebeurtenis wordt gestart 

Zodra u hebt geleerd van een aanstaande gebeurtenis en de logica voor het correct afsluiten voltooid, kunt u Hallo openstaande gebeurtenis goedkeuren door het maken van een `POST` toohello metagegevensservice Hello aanroepen `EventId`. Dit geeft aan dat het Hallo minimale melding kunt inkorten tooAzure tijd (indien mogelijk). 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> Een gebeurtenis zijn bevestigd Hallo gebeurtenis tooproceed staat voor alle `Resources` in Hallo-gebeurtenis niet alleen Hallo virtuele machine die Hallo-gebeurtenis rechthebbenden. U kunt daarom ervoor kiezen tooelect een opvulteken toocoordinate Hallo bevestiging, die mogelijk net zo eenvoudig als eerste machine Hallo in Hallo `Resources` veld.




## <a name="python-sample"></a>Python-voorbeeld 

Hallo volgende voorbeeldquery's Hallo metagegevensservice voor geplande gebeurtenissen en keurt deze goed elke openstaande gebeurtenis.

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Volgende stappen 

- Meer informatie over beschikbare API's in Hallo Hallo [service-exemplaar metagegevens](instance-metadata-service.md).
- Meer informatie over [gepland onderhoud voor Linux virtuele machines in Azure](planned-maintenance.md).
