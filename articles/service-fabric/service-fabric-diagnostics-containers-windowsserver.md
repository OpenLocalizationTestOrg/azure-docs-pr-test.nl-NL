---
title: aaaAzure Service Fabric-Containers controle en diagnostische gegevens | Microsoft Docs
description: Meer informatie over hoe toomonitor en containers op Microsoft Azure Service Fabric wordt beheerd met de OMS-Containers oplossing onderzoeken.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a>Bewaking van Windows Server-containers met OMS

## <a name="oms-containers-solution"></a>OMS Containers oplossing

Hallo Operations Management Suite (OMS)-team heeft een oplossing Containers voor diagnostische gegevens en de bewaking voor containers gepubliceerd. Deze oplossing is samen met hun Service Fabric-oplossing een uitstekend hulpprogramma toomonitor containerimplementaties gedirigeerd op Service Fabric. Hier volgt een eenvoudig voorbeeld van welke Hallo-dashboard in Hallo oplossing ziet als eruit:

![Basic OMS-Dashboard](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

Verzamelt ook verschillende soorten logboeken die in Hallo OMS Log Analytics hulpmiddel kunnen worden opgevraagd en gebruikte toovisualize mag geen metrische gegevens of gebeurtenissen wordt gegenereerd. Hallo logboek typen die zijn verzameld zijn:

1. ContainerInventory: geeft informatie over de containerlocatie, naam en installatiekopieën
2. ContainerImageInventory: informatie over geïmplementeerde installatiekopieën, met inbegrip van id's of grootten
3. ContainerLog: specifieke foutenlogboeken, docker-Logboeken (stdout, enzovoort) en andere items
4. ContainerServiceLog: docker-daemon opdrachten die zijn uitgevoerd
5. Prestaties: prestatiemeteritems met inbegrip van container cpu, geheugen, netwerkverkeer, schijf-i/o en aangepaste metrische gegevens van Hallo machines hosten

In dit artikel bevat informatie over Hallo stappen vereist tooset up container bewaking voor uw cluster. meer informatie over de OMS-Containers oplossing toolearn uitchecken hun [documentatie](../log-analytics/log-analytics-containers.md).

## <a name="1-set-up-a-service-fabric-cluster"></a>1. Een Service Fabric-cluster instellen

Maak een cluster met Azure Resource Manager-sjabloon Hallo gevonden [hier](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample). Zorg ervoor dat tooadd een unieke naam van de OMS-werkruimte. Deze sjabloon wordt ook standaard toodeploying bouwen van een cluster Hallo Preview-versie van Service Fabric (v255.255), wat betekent dat deze kan niet worden gebruikt in productie, en kan niet worden bijgewerkt tooa andere Service Fabric-versie. Als u besluit toouse van deze sjabloon voor lange termijn of productie, wijzigt u tooa Hallo-stabiele versie versienummer.

Zodra Hallo-cluster is ingesteld, bevestig het juiste certificaat Hallo hebt geïnstalleerd en controleer of dat u kunt tooconnect toohello cluster zijn.

Bevestig dat de resourcegroep correct is ingesteld door de kop toohello [Azure-portal](https://portal.azure.com/) en Hallo-implementatie te zoeken. Hallo-resourcegroep moet alle Hallo Service Fabric-bronnen bevatten en hebben een Log Analytics-oplossing, evenals een Service Fabric-oplossing.

Voor het wijzigen van een bestaand Service Fabric-cluster:
* Controleer of de diagnostische gegevens is ingeschakeld (als dit niet het geval is, het inschakelen via [Hallo virtuele-machineschaalset bijwerken](/rest/api/virtualmachinescalesets/create-or-update-a-set))
* Een OMS-werkruimte toevoegen door te maken van een oplossing 'Service Fabric Analytics' via hello Azure Marketplace
* Hallo-gegevensbronnen van Hallo Service Fabric-oplossing toopick van gegevens uit Hallo juiste Azure Storage-tabellen (ingesteld door af) in Hallo brongroep die de cluster Hallo wordt bewerken
* Toevoegen van Hallo agent als een [extensie toohello virtuele-machineschaalset](/powershell/module/azurerm.compute/add-azurermvmssextension) via PowerShell of via Hallo virtuele-machineschaalset (dezelfde koppeling als hierboven, toomodify Hallo Resource Manager-sjabloon) bijwerken

## <a name="2-deploy-a-container"></a>2. Een container implementeren

Zodra de Hallo cluster gereed is en u hebt gecontroleerd of u toegang hebt, implementeert u een tooit container. Als u toouse Hallo preview-versie zoals ingesteld door Hallo sjabloon kiest, kunt u ook nieuwe Service-Fabric-docker verkennen functionaliteit opstellen. Voorzien zijn er rekening mee dat de eerste keer een installatiekopie van een container Hallo geïmplementeerde tooa cluster is, duurt het enkele minuten toodownload Hallo afbeelding, afhankelijk van de grootte.

## <a name="3-add-hello-containers-solution"></a>3. Hallo Containers oplossing toevoegen

In Azure-portal Hallo, maakt u een bron Containers (onder controle + Management Hallo categorie) via Azure Marketplace. 

![Containers oplossing toevoegen](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

In stap Hallo maken vraagt het een OMS-werkruimte. Selecteer Hallo die zijn met de bovenstaande Hallo-implementatie gemaakt. Deze stap voegt een oplossing Containers in de OMS-werkruimte en wordt automatisch gedetecteerd door Hallo OMS-agent is geïmplementeerd door Hallo-sjabloon. Hallo-agent wordt gestart met het verzamelen van gegevens op Hallo containers processen in Hallo-cluster en in ongeveer 10-15 minuten, ziet u Hallo oplossing lichte up met gegevens zoals in afbeelding Hallo van Hallo dashboard hierboven.

## <a name="4-next-steps"></a>4. Volgende stappen

OMS biedt verschillende hulpprogramma's in Hallo werkruimte toomake als nuttiger voor u. Bekijk Hallo opties toocustomize Hallo oplossing tooyour behoeften te volgen:
- Hello ophalen familiarized [zoeken en uitvoeren van query's in logboek registreren](../log-analytics/log-analytics-log-searches.md) functies die worden aangeboden als onderdeel van logboekanalyse
- Configureer Hallo OMS-agent toopick van specifieke prestatiemeteritems (toohello werkruimte startpagina gaan > Instellingen > gegevens > Windows-prestatiemeteritems)
- Configureren van OMS tooset up [geautomatiseerde waarschuwingen](../log-analytics/log-analytics-alerts.md) regels tooaid in detecteren en diagnostische gegevens
