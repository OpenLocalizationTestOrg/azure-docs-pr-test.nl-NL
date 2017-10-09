---
title: de slag met Azure Service Fabric en Azure CLI 2.0 aaaGet
description: Meer informatie over hoe toouse hello Azure Service Fabric-module in versie 2.0 van Azure CLI-opdrachten. Meer informatie over hoe tooconnect tooa cluster, en hoe toomanage toepassingen.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a>Azure Service Fabric en Azure CLI 2.0

Hello Azure-opdrachtregelprogramma (Azure CLI) versie 2.0 bevat opdrachten toohelp beheren van Azure Service Fabric-clusters. Meer informatie over hoe tooget de slag met Azure CLI en Service Fabric.

## <a name="install-azure-cli-20"></a>Azure CLI 2.0 installeren

U kunt Azure CLI 2.0 opdrachten toointeract met gebruiken en beheren van Service Fabric-clusters. tooget hello meest recente versie van Azure CLI, volg Hallo [standaard Azure CLI 2.0-installatieproces](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

Zie voor meer informatie, Hallo [overzicht van Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="azure-cli-syntax"></a>De syntaxis van de Azure CLI

Alle Service Fabric-opdrachten worden voorafgegaan door `az sf` in de Azure CLI. Gebruik voor algemene informatie over Hallo opdrachten kunt u `az sf -h`. Gebruik `az sf <command> -h` voor hulp bij één opdracht.

Service Fabric-opdrachten in de Azure CLI volgen dit naamgevingspatroon:

```azurecli
az sf <object> <action>
```

`<object>`Hallo-doel voor `<action>`.

## <a name="select-a-cluster"></a>Een cluster selecteren

Voordat u bewerkingen uitvoert, moet u een cluster tooconnect te selecteren. Zie voor een voorbeeld Hallo code te volgen. Hallo code verbindt tooan onbeveiligde cluster.

> [!WARNING]
> Gebruik geen niet-beveiligde Service Fabric-clusters in een productieomgeving.

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

Hallo clustereindpunt moet worden voorafgegaan door `http` of `https`. Hallo-poort voor Hallo http-gateway moet bevatten. Hallo-poort en adres zijn hetzelfde zijn als de URL van de Service Fabric Explorer Hallo Hallo.

Voor clusters die zijn beveiligd met een certificaat, kunt u niet-versleutelde .pem-bestanden of .crt- en .key-bestanden gebruiken. Bijvoorbeeld:

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Zie voor meer informatie [Connect tooa beveiligde Azure Service Fabric-cluster](service-fabric-connect-to-secure-cluster.md).

> [!NOTE]
> Hallo `select` opdracht niet reageren op alle aanvragen voordat deze wordt geretourneerd. tooverify u een cluster correct hebt opgegeven een opdracht zoals gebruiken `az sf cluster health`. Controleer of Hallo opdracht retourneert niet eventuele fouten.

## <a name="basic-operations"></a>Basisbewerkingen

De gegevens van een clusterverbinding blijven behouden tussen meerdere Azure CLI-sessies. Nadat u een Service Fabric-cluster selecteert, kunt u een Service Fabric-opdracht kunt uitvoeren op Hallo-cluster.

Bijvoorbeeld tooget Hallo status voor Service Fabric-cluster, Hallo volgende opdracht gebruiken:

```azurecli
az sf cluster health
```

Hallo opdracht resulteert in Hallo volgende uitvoer (ervan uitgaande dat JSON-uitvoer is opgegeven in de configuratie van hello Azure CLI):

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

Mogelijk vindt u nuttige informatie te volgen als u problemen ondervindt tijdens het gebruik van Service Fabric-opdrachten in de Azure CLI Hallo.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Een certificaat van PFX tooPEM-indeling converteren

De Azure CLI ondersteunt clientcertificaten als PEM-bestanden (extensie .pem). Als u PFX-bestanden van Windows gebruikt, moet u deze certificaten tooPEM-indeling converteren. tooconvert een PFX-bestand tooa PEM-bestand Hallo volgende opdracht gebruiken:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Zie voor meer informatie, Hallo [OpenSSL documentatie](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Verbindingsproblemen

Bepaalde bewerkingen mogelijk Hallo volgende bericht te genereren:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Controleer of dat deze Hallo opgegeven clustereindpunt is beschikbaar is en luistert. Controleer ook of die Hallo Service Fabric Explorer UI is beschikbaar op die als host en poort. tooupdate hello eindpunt, gebruik `az sf cluster select`.

### <a name="detailed-logs"></a>Gedetailleerde logboeken

Gedetailleerde logboeken zijn vaak nuttig zijn wanneer u fouten opspoort of een probleem meldt. Azure CLI biedt een algemene `--debug` vlag die wordt verhoogd Hallo uitgebreidheid van logboekbestanden.

### <a name="command-help-and-syntax"></a>Syntaxis van Help-opdracht

Service Fabric-opdrachten Volg Hallo dezelfde conventies als Azure CLI. Gebruik voor hulp bij een bepaalde opdracht of een groep opdrachten, Hallo `-h` vlag:

```azurecli
az sf application -h
```

Hier volgt nog een voorbeeld:

```azurecli
az sf application create -h
```
