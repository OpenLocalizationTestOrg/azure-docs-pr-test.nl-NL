---
title: aaaGet de slag met Azure Service Fabric CLI (sfctl)
description: Meer informatie over hoe toouse hello Azure Service Fabric CLI. Meer informatie over hoe tooconnect tooa cluster, en hoe toomanage toepassingen.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a>Azure Service Fabric-opdrachtregel

Hello Azure Service Fabric CLI (sfctl) is een opdrachtregelprogramma voor interactie en beheren van Azure Service Fabric-entiteiten. Sfctl kan worden gebruikt met Windows- of Linux-clusters. Sfctl kan worden uitgevoerd op elk platform dat ondersteuning biedt voor python.

## <a name="prerequisites"></a>Vereisten

Eerdere tooinstallation Zorg ervoor dat uw omgeving heeft python en via pip geïnstalleerd. Voor meer informatie, bekijk Hallo [Quick Start-documentatie pip](https://pip.pypa.io/en/latest/quickstart/), en officiële [python installeren documentatie](https://wiki.python.org/moin/BeginnersGuide/Download).

Beide python 2.7 en 3.6 worden wel ondersteund, is het raadzaam toouse python 3.6.

## <a name="install"></a>Installeren

Hello Azure Service Fabric CLI (sfctl) wordt geleverd als een python-pakket. tooinstall hello meest recente versie uitvoeren:

```bash
pip install sfctl
```

Na de installatie voert `sfctl -h` tooget informatie over beschikbare opdrachten.

## <a name="cli-syntax"></a>De syntaxis van de CLI

Opdrachten worden altijd voorafgegaan door `sfctl`. Voor algemene informatie over alle opdrachten die u kunt gebruiken, gebruikt u `sfctl -h`. Gebruik `sfctl <command> -h` voor hulp bij één opdracht.

Opdrachten Volg een herhaalbare-structuur met doel Hallo Hallo opdracht voorgaande Hallo-term of actie:

```azurecli
sfctl <object> <action>
```

In dit voorbeeld `<object>` is Hallo doel voor `<action>`.

## <a name="select-a-cluster"></a>Een cluster selecteren

Voordat u bewerkingen uitvoert, moet u een cluster tooconnect te selecteren. Bijvoorbeeld Hallo na tooselect uitvoeren en toohello cluster verbinding met de naam van de Hallo `testcluster.com`.

> [!WARNING]
> Gebruik geen niet-beveiligde Service Fabric-clusters in een productieomgeving.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

Hallo clustereindpunt moet worden voorafgegaan door `http` of `https`. Hallo-poort voor Hallo http-gateway moet bevatten. Hallo-poort en adres zijn hetzelfde zijn als de URL van de Service Fabric Explorer Hallo Hallo.

Voor clusters die zijn beveiligd met een certificaat, kunt u een met PEM gecodeerd certificaat opgeven. Hallo-certificaat kan worden opgegeven als een enkel bestand of het certificaat en de sleutelpaar.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Zie voor meer informatie [Connect tooa beveiligde Azure Service Fabric-cluster](service-fabric-connect-to-secure-cluster.md).

## <a name="basic-operations"></a>Basisbewerkingen

De gegevens van een clusterverbinding blijven behouden tussen meerdere sfctl-sessies. Nadat u een Service Fabric-cluster selecteert, kunt u een Service Fabric-opdracht kunt uitvoeren op Hallo-cluster.

Bijvoorbeeld tooget Hallo status voor Service Fabric-cluster, Hallo volgende opdracht gebruiken:

```azurecli
sfctl cluster health
```

Hallo opdracht resulteert in Hallo volgende uitvoer:

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a>Tips en probleemoplossing

Enkele suggesties en tips voor het oplossen van veelvoorkomende problemen.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Een certificaat van PFX tooPEM-indeling converteren

Hallo Service Fabric CLI ondersteunt certificaten vanaf de client als PEM (.pem extensie)-bestanden. Als u PFX-bestanden van Windows gebruikt, moet u deze certificaten tooPEM-indeling converteren. tooconvert een PFX-bestand tooa PEM-bestand de volgende opdracht gebruiken:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Zie voor meer informatie, Hallo [OpenSSL documentatie](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Verbindingsproblemen

Bepaalde bewerkingen mogelijk Hallo volgende bericht te genereren:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Controleer of dat deze Hallo opgegeven clustereindpunt is beschikbaar is en luistert. Controleer ook of die Hallo Service Fabric Explorer UI is beschikbaar op die als host en poort. tooupdate hello eindpunt, gebruik `sfctl cluster select`.

### <a name="detailed-logs"></a>Gedetailleerde logboeken

Gedetailleerde logboeken zijn vaak nuttig zijn wanneer u fouten opspoort of een probleem meldt. Er is een globale `--debug` vlag die wordt verhoogd Hallo uitgebreidheid van logboekbestanden.

### <a name="command-help-and-syntax"></a>Syntaxis van Help-opdracht

Gebruik voor hulp bij een bepaalde opdracht of een groep opdrachten, Hallo `-h` vlag:

```azurecli
sfctl application -h
```

Nog een voorbeeld:

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a>Volgende stappen

* [Implementeer een toepassing met hello Azure Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md)
* [Aan de slag met Service Fabric in Linux](service-fabric-get-started-linux.md)
