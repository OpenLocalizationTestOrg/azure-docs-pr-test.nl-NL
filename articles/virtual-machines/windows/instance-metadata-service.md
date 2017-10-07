---
title: aaaAzure exemplaar metagegevens Service voor Windows | Microsoft Docs
description: RESTful-interface tooget informatie over Windows-VM compute, netwerk en toekomstig onderhoud gebeurtenissen.
services: virtual-machines-windows
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a33c26b5e9ed650be639598cdb6895fc19ccb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-windows-vms"></a>Azure-service metagegevens van het exemplaar voor VM's van Windows


Hello Azure exemplaar metagegevens Service biedt informatie over het uitvoeren van de virtuele machine-exemplaren die kunnen worden gebruikt toomanage en configureren van uw virtuele machines.
Dit omvat gegevens zoals SKU netwerkconfiguratie en toekomstig onderhoud gebeurtenissen. Zie voor meer informatie over wat voor soort informatie beschikbaar is, [metagegevens categorieën](#instance-metadata-data-categories).

Azure instantie metagegevens-Service is een REST-eindpunt toegankelijk tooall IaaS VM's die zijn gemaakt via Hallo [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Hallo-eindpunt is beschikbaar op een bekende niet-routeerbare IP-adres (`169.254.169.254`) die kan alleen worden benaderd binnen Hallo VM.



> [!IMPORTANT]
> Deze service is **algemeen beschikbaar** in globale Azure-regio's. Het is openbare Preview voor Government, China en Duitse Azure-Cloud. Het ontvangt regelmatig updates tooexpose nieuwe informatie over exemplaren van de virtuele machine. Deze pagina geeft Hallo up-to-date [gegevenscategorieën](#instance-metadata-data-categories) beschikbaar.



## <a name="service-availability"></a>Beschikbaarheid van de service
Hallo-service is beschikbaar in alle algemeen beschikbaar globale Azure-regio's. Hallo-service zich in de openbare preview in Hallo Government, China of Duitsland regio's.

Regio's                                        | Beschikbaarheid?
-----------------------------------------------|-----------------------------------------------
[Alle in het algemeen beschikbare globale Azure-regio 's](https://azure.microsoft.com/regions/)     | Algemeen beschikbaar 
[Azure Government](https://azure.microsoft.com/overview/clouds/government/)              | Preview-versie 
[Azure China](https://www.azure.cn/)                                                           | Preview-versie
[Azure Duitsland](https://azure.microsoft.com/overview/clouds/germany/)                    | Preview-versie

Deze tabel wordt bijgewerkt zodra Hallo service beschikbaar in andere Azure-clouds.

tootry uit Hallo Service-exemplaar voor metagegevens, maak een VM van [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) of Hallo [Azure-portal](http://portal.azure.com) in Hallo hierboven regio's en volg de volgende Hallo voorbeelden.

## <a name="usage"></a>Gebruik

### <a name="versioning"></a>Versiebeheer voor onderdelen
Hallo metagegevens-Service-exemplaar is samengesteld. Versies zijn verplicht en de huidige versie Hallo is `2017-04-02`.

> [!NOTE] 
> Eerdere versies van de preview van geplande gebeurtenissen {laatste} wordt ondersteund als Hallo api-versie. Deze indeling wordt niet meer ondersteund en in toekomstige hello wordt afgeschaft.

Als er nieuwere versies toevoegt, oudere versies is nog steeds toegankelijk voor compatibiliteit als uw scripts afhankelijk van specifieke gegevensindelingen zijn. Bedenk wel dat Hallo huidige preview version(2017-03-01) mogelijk niet beschikbaar zodra de service Hallo algemeen beschikbaar is.

### <a name="using-headers"></a>Met behulp van headers
Wanneer u query Hallo exemplaar metagegevens Service uitvoert, moet u opgeven Hallo header `Metadata: true` tooensure Hallo verzoek is niet per ongeluk omgeleid.

### <a name="retrieving-metadata"></a>Ophalen van metagegevens

Metagegevens van het exemplaar is beschikbaar voor het uitvoeren van virtuele machines die zijn gemaakt/beheerd met behulp van [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Toegang tot alle gegevenscategorieën voor een exemplaar van de virtuele machine met behulp van de volgende aanvraag Hallo:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> Alle query's voor exemplaar-metagegevens zijn hoofdlettergevoelig.

### <a name="data-output"></a>Data-uitvoer
Standaard Hallo exemplaar metagegevens Service gegevens worden geretourneerd in JSON-indeling (`Content-Type: application/json`). Verschillende API's kunnen echter gegevens in verschillende indelingen geretourneerd als aangevraagd.
Hallo bevat volgende tabel een verwijzing naar andere indelingen met de die API 's kunnen ondersteunen.

API | Standaardindeling voor gegevens | Andere indelingen
--------|---------------------|--------------
/Instance | JSON | Tekst
/scheduledevents | JSON | Geen

een niet-standaard antwoordindeling tooaccess opgeven Hallo aangevraagde indeling als een parameter querystring in Hallo-aanvraag. Bijvoorbeeld:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>Beveiliging
Hallo exemplaar metagegevens Service-eindpunt is alleen toegankelijk vanuit Hallo met een exemplaar van de virtuele machine op een niet-routeerbare IP-adres. Bovendien verzoeken met een `X-Forwarded-For` header is geweigerd door Hallo-service.
Ook aanvragen toocontain moet een `Metadata: true` header tooensure die Hallo werkelijke aanvraag rechtstreeks is bestemd en geen deel uit van onbedoelde omleiding. 

### <a name="error"></a>Fout
Als er een gegevenselement niet gevonden of een onjuist gevormde aanvraag, retourneert Hallo exemplaar metagegevens Service standaard HTTP-fouten. Bijvoorbeeld:

HTTP-statuscode | Reden
----------------|-------
200 OK |
400 onjuiste aanvraag | Ontbrekende `Metadata: true` koptekst
404 – Niet gevonden | Hallo gevraagde element does't bestaan 
405 methode is niet toegestaan | Alleen `GET` en `POST` aanvragen worden ondersteund
429 te veel aanvragen | Hallo-API ondersteunt momenteel maximaal 5 query's per seconde
Fout 500-Service     | Probeer na enige tijd

### <a name="examples"></a>Voorbeelden

> [!NOTE] 
> Alle antwoorden op de API zijn JSON-tekenreeksen. Alle antwoorden op de volgende voorbeeld zijn voor de leesbaarheid pretty afgedrukt.

#### <a name="retrieving-network-information"></a>Bij het ophalen van informatie over het netwerk

**Aanvraag**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**Antwoord**

> [!NOTE] 
> Hallo-antwoord is een JSON-tekenreeks. Hallo volgende voorbeeld van een antwoord is voor de leesbaarheid pretty afgedrukt.

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>Openbaar IP-adres ophalen

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>Ophalen van metagegevens voor een exemplaar van alle

**Aanvraag**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**Antwoord**

> [!NOTE] 
> Hallo-antwoord is een JSON-tekenreeks. Hallo volgende voorbeeld van een antwoord is voor de leesbaarheid pretty afgedrukt.

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>Ophalen van metagegevens van de virtuele machine voor Windows

**Aanvraag**

Metagegevens van het exemplaar kan worden opgehaald in Windows via Hallo PowerShell hulpprogramma `curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

Of via Hallo `Invoke-RestMethod` cmdlet:
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**Antwoord**

> [!NOTE] 
> Hallo-antwoord is een JSON-tekenreeks. Hallo volgende voorbeeld van een antwoord is voor de leesbaarheid pretty afgedrukt.

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>Exemplaar metagegevens gegevenscategorieën
Hallo na gegevenscategorieën zijn beschikbaar via Hallo exemplaar metagegevens Service:

Gegevens | Beschrijving
-----|------------
location | Azure regio Hallo VM wordt uitgevoerd
naam | Naam van Hallo VM 
Aanbieding | Informatie voor de VM-installatiekopie Hallo bieden. Deze waarde is alleen aanwezig voor afbeeldingen van afbeelding voor Azure-galerie geïmplementeerd.
Uitgever | Uitgever van de VM-installatiekopie Hallo
SKU | Specifieke SKU voor Hallo VM-installatiekopie  
Versie | Versie van de VM-installatiekopie Hallo 
besturingssysteemtype | Linux- of Windows 
platformUpdateDomain |  [Updatedomein](manage-availability.md) Hallo VM wordt uitgevoerd in
platformFaultDomain | [Foutdomein](manage-availability.md) Hallo VM wordt uitgevoerd in
vmId | [De unieke id](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) voor Hallo VM
vmSize | [VM-grootte](sizes.md)
IPv4/privateIpAddress | Lokale IPv4-adres van Hallo VM 
IPv4/publicIpAddress | Openbare IPv4-adres van Hallo VM
subnetadres / | Subnetadres Hallo VM
subnetvoorvoegsel / | Subnetvoorvoegsel, voorbeeld 24
IPv6/IP-adres | Lokale IPv6-adres van Hallo VM
MAC-adres | Mac-adres van VM 
scheduledevents | Op dit moment in de openbare Preview Zie [scheduledevents](scheduled-events.md)

## <a name="example-scenarios-for-usage"></a>Voorbeeldscenario's voor gebruik  

### <a name="tracking-vm-running-on-azure"></a>Uitgevoerd op Azure VM bijhouden

Als een serviceprovider gewenste tootrack Hallo aantal virtuele machines met uw software of agenten die tootrack uniekheid Hallo VM nodig hebt. toobe kunnen tooget een unieke ID voor een virtuele machine, gebruik Hallo `vmId` veld van metagegevens-Service-exemplaar.

**Aanvraag**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**Antwoord**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>Plaatsing van containers domein veroorzaakt of bij te werken op basis van gegevens partities 

Voor bepaalde scenario's, de plaatsing van replica's van verschillende gegevens is van primair belang. Bijvoorbeeld: [HDFS replica plaatsing](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) of plaatsing van de container via een [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) mogelijk tooknow hello `platformFaultDomain` en `platformUpdateDomain` Hallo VM wordt uitgevoerd op.
U kunt deze gegevens rechtstreeks via Hallo exemplaar metagegevens Service opvragen.

**Aanvraag**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**Antwoord**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>Meer informatie over Hallo VM tijdens ondersteuningsaanvraag ophalen 

Als een serviceprovider mogelijk dat u een telefoongesprek ondersteuning waar u wilt tooknow meer informatie over Hallo VM. Hallo klant tooshare vragen kunt Hallo compute metagegevens basisinformatie voor Hallo ondersteuning professional tooknow over Hallo-type van de virtuele machine in Azure. 

**Aanvraag**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**Antwoord**

> [!NOTE] 
> Hallo-antwoord is een JSON-tekenreeks. Hallo volgende voorbeeld van een antwoord is voor de leesbaarheid pretty afgedrukt.

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>Voorbeelden van het aanroepen van metagegevensservice met behulp van verschillende talen in Hallo VM 

Taal | Voorbeeld 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.RB
Ga Lan   | https://github.com/Microsoft/azureimds/BLOB/master/imdssample.go            
python   | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.PY
C++      | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample-Windows.cpp
C#       | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.cs
Javascript | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.js
PowerShell | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.sh
    

## <a name="faq"></a>Veelgestelde vragen
1. Ik krijg Hallo fout `400 Bad Request, Required metadata header not specified`. Wat betekent dit?
   * Hallo exemplaar metagegevens Service Hallo header vereist `Metadata: true` toobe doorgegeven in Hallo-aanvraag. Deze header doorgeven in een REST-aanroep hello, kunt access toohello exemplaar metagegevens Service. 
2. Waarom niet krijg ik compute-informatie voor mijn VM?
   * Hallo exemplaar metagegevens Service ondersteunt momenteel alleen exemplaren gemaakt met Azure Resource Manager. In toekomstige hello, kunnen we ondersteuning voor virtuele machines van Cloud Service toevoegen.
3. Ik heb mijn virtuele Machine via Azure Resource Manager een tijd terug gemaakt. Waarom kan ik geen Zie compute-metagegevens?
   * Voor alle virtuele machines na Sep 2016 is gemaakt, voegt u een [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart zien compute-metagegevens. Voor oudere virtuele machines (gemaakt vóór Sep-2016), software-extensies of gegevens schijven toohello VM toorefresh metagegevens.
4. Waarom krijg ik Hallo fout `500 Internal Server Error`?
   * Probeer uw aanvraag op basis van de exponentiële back uit het systeem. Neem contact op met de ondersteuning van Azure als Hallo probleem zich blijft voordoen.
5. Waar kan ik aanvullende vragen/opmerkingen delen
   * Uw opmerkingen over http://feedback.azure.com verzenden.
7. Dit werkt voor virtuele Machine Scale ingesteld exemplaar, zou?
   * Ja is metagegevens-service beschikbaar voor Scale-exemplaren instellen. 
6. Hoe krijg ik ondersteuning voor Hallo-service
   * tooget ondersteuning voor het Hallo-service een probleem maken in Azure portal voor Hallo VM waar u zich niet kunnen tooget metagegevens antwoord na lang pogingen 

   ![Ondersteuning voor Instance Metagegevens](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>Volgende stappen

- Meer informatie over Hallo [gepland gebeurtenissen](scheduled-events.md) API **openbare preview** geleverd door Hallo service-exemplaar metagegevens.
