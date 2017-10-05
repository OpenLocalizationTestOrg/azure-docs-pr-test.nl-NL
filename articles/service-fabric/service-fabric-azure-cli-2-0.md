---
title: Aan de slag met Azure Service Fabric en Azure CLI 2.0
description: Informatie over het gebruik van de Azure Service Fabric-opdrachtenmodule in Azure CLI versie 2.0. Informatie over verbinding maken met een cluster en het beheren van toepassingen.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ee3302b984ca2f5509755dc17b0a5fd06ace0afe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a>Azure Service Fabric en Azure CLI 2.0

Het Azure-opdrachtregelprogramma (Azure CLI) versie 2.0 bevat opdrachten voor het beheren van Azure Service Fabric-clusters. Lees hoe u aan de slag kunt gaan met Azure Service Fabric en Azure CLI 2.0.

## <a name="install-azure-cli-20"></a>Azure CLI 2.0 installeren

U kunt Azure CLI 2.0-opdrachten gebruiken voor het beheren en manipuleren van Service Fabric-clusters. Volg voor de nieuwste versie van Azure CLI het [standaardinstallatieproces van Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

Zie [Overzicht van Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview) voor meer informatie.

## <a name="azure-cli-syntax"></a>De syntaxis van de Azure CLI

Alle Service Fabric-opdrachten worden voorafgegaan door `az sf` in de Azure CLI. Voor algemene informatie over de opdrachten die u kunt gebruiken, gebruikt u `az sf -h`. Gebruik `az sf <command> -h` voor hulp bij één opdracht.

Service Fabric-opdrachten in de Azure CLI volgen dit naamgevingspatroon:

```azurecli
az sf <object> <action>
```

`<object>` is het doel voor `<action>`.

## <a name="select-a-cluster"></a>Een cluster selecteren

U kunt pas bewerkingen uitvoeren nadat u een cluster hebt geselecteerd waarmee u verbinding wilt maken. Zie de volgende code voor een voorbeeld. De code maakt verbinding met een niet-beveiligd cluster.

> [!WARNING]
> Gebruik geen niet-beveiligde Service Fabric-clusters in een productieomgeving.

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

Het clustereindpunt moet worden voorafgegaan door `http` of `https`. Het moet de poort voor de HTTP-gateway bevatten. De poort en het adres komen overeen met de Service Fabric Explorer-URL.

Voor clusters die zijn beveiligd met een certificaat, kunt u niet-versleutelde .pem-bestanden of .crt- en .key-bestanden gebruiken. Bijvoorbeeld:

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Zie [Verbinding maken met een beveiligd Azure Service Fabric-cluster](service-fabric-connect-to-secure-cluster.md) voor meer informatie.

> [!NOTE]
> De `select`-opdracht reageert niet op aanvragen voordat deze wordt geretourneerd. Gebruik een opdracht als `az sf cluster health` om te controleren of u een cluster correct hebt opgegeven. Controleer of de opdracht niet eventuele fouten retourneert.

## <a name="basic-operations"></a>Basisbewerkingen

De gegevens van een clusterverbinding blijven behouden tussen meerdere Azure CLI-sessies. Nadat u een Service Fabric-cluster hebt geselecteerd, kunt u elke Service Fabric-opdracht in het cluster uitvoeren.

Als u bijvoorbeeld de status van het Service Fabric-cluster wilt weten, voert u de volgende opdracht uit:

```azurecli
az sf cluster health
```

De opdracht levert de volgende uitvoer op (ervan uitgaande dat JSON-uitvoer is opgegeven in de configuratie van de Azure CLI):

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

U kunt de volgende informatie handig vinden als u problemen ondervindt tijdens het gebruik van Service Fabric-opdrachten in de Azure CLI.

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a>Een certificaat converteren van PFX- naar PEM-indeling

De Azure CLI ondersteunt clientcertificaten als PEM-bestanden (extensie .pem). Als u PFX-bestanden van Windows gebruikt, moet u deze certificaten converteren naar PEM-indeling. Gebruik de volgende opdracht om een PFX-bestand te converteren naar een PEM-bestand:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Voor meer informatie raadpleegt u de [OpenSSL-documentatie](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Verbindingsproblemen

Bepaalde bewerkingen genereren mogelijk het volgende bericht:

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

Controleer of het opgegeven clustereindpunt beschikbaar is en luistert. Controleer ook of de gebruikersinterface van Service Fabric Explorer beschikbaar is op die host en poort. Gebruik `az sf cluster select` om het eindpunt bij te werken.

### <a name="detailed-logs"></a>Gedetailleerde logboeken

Gedetailleerde logboeken zijn vaak nuttig zijn wanneer u fouten opspoort of een probleem meldt. De Azure CLI bevat een algemene `--debug`-vlag waarmee het detailniveau van logboeken wordt verhoogd.

### <a name="command-help-and-syntax"></a>Syntaxis van Help-opdracht

De Service Fabric-opdrachten volgen dezelfde conventie als de Azure CLI. Als u hulp nodig hebt met een specifieke opdracht of een groep opdrachten, gebruikt u de `-h`-vlag:

```azurecli
az sf application -h
```

Hier volgt nog een voorbeeld:

```azurecli
az sf application create -h
```
