---
title: aaaPublish HDInsight-toepassingen - Azure | Microsoft Docs
description: Meer informatie over hoe toocreate en publiceren van HDInsight-toepassingen.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a>HDInsight-toepassingen in Azure Marketplace Hallo publiceren
Een HDInsight-toepassing is een toepassing die gebruikers kunnen installeren op een op Linux gebaseerd HDInsight-cluster. Deze toepassingen kunnen zijn ontwikkeld door Microsoft, door onafhankelijke softwareleveranciers (ISV) of door u zelf. In dit artikel leert u hoe toopublish een HDInsight-toepassing in hello Azure Marketplace.  Raadpleeg voor algemene informatie over publiceren in Azure Marketplace Hallo [publiceren een aanbieding toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).

HDInsight-toepassingen gebruiken Hallo *Bring Your Own License (BYOL)* model, waarbij toepassingsprovider verantwoordelijk is voor licentieverlening Hallo toepassing tooend-gebruikers en eindgebruikers worden alleen kosten in rekening gebracht door Azure voor Hallo bronnen ze maken, zoals Hallo HDInsight-cluster en de virtuele machines/knooppunten. Facturering voor Hallo toepassing zelf wordt op dit moment niet gedaan door Azure.

Ander artikel HDInsight toepassingsgerelateerde:

* [HDInsight-toepassingen installeren](hdinsight-apps-install-applications.md): meer informatie over hoe tooinstall een tooyour van de toepassing HDInsight-clusters.
* [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md): meer informatie over hoe tooinstall en test aangepaste HDInsight-toepassingen.

## <a name="prerequisites"></a>Vereisten
toosubmit uw aangepaste toepassing toohello marketplace, moet u hebt gemaakt en getest van uw aangepaste toepassing. Zie Hallo artikelen te volgen:

* [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md): meer informatie over hoe tooinstall en test aangepaste HDInsight-toepassingen.

U moet ook hebt geregistreerd uw ontwikkelaarsaccount. Zie [publiceren een aanbieding toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) en [een Microsoft Developer-account maken](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).

## <a name="define-application"></a>Uw toepassing definiëren
Er zijn twee stappen voor het publiceren van toepassingen toohello Azure Marketplace.  Eerst definieert u een **createUiDef.json** bestand tooindicate die clusters de toepassing is compatibel met; en publiceert u de sjabloon Hallo van hello Azure-portal. Hallo volgende sectie wordt een voorbeeld van een createUiDef.json-bestand.

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| Veld | Beschrijving | Mogelijke waarden |
| --- | --- | --- |
| typen |Hallo-clustertypen waarmee Hallo toepassing compatibel is. |Hadoop, HBase, Storm, Spark (of een combinatie hiervan) |
| lagen |Hallo-clusterlagen waarmee Hallo toepassing compatibel is. |Standaard, Premium (of beide) |
| versies |Hallo HDInsight-clustertypen waarmee de toepassing hello compatibel is. |3.4 |

## <a name="application-install-script"></a>Het installatiescript toepassing
Wanneer een toepassing is geïnstalleerd op een cluster (een bestaande of een nieuwe) een edge-knooppunt wordt gemaakt en installatiescript Hallo-toepassing wordt uitgevoerd op deze.
  > [!IMPORTANT]
  > Hallo-naam van het installatiescript voor toepassing hello moet uniek zijn voor een bepaald cluster Hello na indeling.
  > 
  > name": "[concat('hue-install-v0','-' ,uniekestring(‘toepassingsnaam’)]"
  > 
  > Let op: Er zijn drie onderdelen toohello-scriptnaam:
  > 
  > 1. Een voorvoegsel, die de naam van de toepassing hello of een toepassing van de relevante toohello naam omvat.
  > 2. Een streepje (-) voor de leesbaarheid.
  > 3. Een unieke tekenreeksfunctie met Hallo toepassingsnaam als parameter Hallo.
  > 
  > Een voorbeeld is de bovenstaande Hallo eindigt steeds: hue-install-v0-4wkahss55hlas in Hallo persistent script actielijst. Zie [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json) voor een voorbeeld van JSON-nettolading.
  > 
Hallo installatiescript moet beschikken over Hallo volgende kenmerken:
1. Zorg ervoor dat Hallo script idempotent is. Meerdere aanroepen toohello script moet produceren Hallo hetzelfde resultaat.
2. Hallo script moet juist samengesteld. Gebruik een andere locatie voor Hallo script wanneer u upgradet of wijzigingen testen zodat klanten die tooinstall Hallo toepassing probeert worden niet beïnvloed. 
3. Voldoende logboekregistratie toohello scripts toevoegen op elk moment. Meestal Hallo script logboeken zijn de enige manier toodebug Hallo problemen met de installatie van de toepassing.
4. Zorg ervoor dat aanroepen tooexternal services of resources voldoende pogingen zodat Hallo-installatie wordt niet beïnvloed door tijdelijke netwerkproblemen.
5. Als uw script services op Hallo knooppunten starten is, zorg ervoor dat Hallo-services worden bewaakt en geconfigureerd toostart automatisch in geval van een knooppunt opnieuw wordt opgestart.

## <a name="package-application"></a>Pakkettoepassing
Maak een ZIP-bestand met alle vereiste bestanden voor het installeren van de HDInsight-toepassingen. U moet het zipbestand in Hallo [toepassing publiceren](#publish-application).

* [createUiDefinition.json](#define-application).
* mainTemplate.json. Bekijk een voorbeeld bij [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md).
* Alle vereiste scripts.

> [!NOTE]
> Hallo toepassingsbestanden (inclusief webtoepassingsbestanden indien deze aanwezig is) kan zich bevinden op een eindpunt dat openbaar toegankelijk.
> 

## <a name="publish-application"></a>Uw toepassing publiceren
Voer de volgende stappen toopublish een HDInsight-toepassing hello:

1. Meld u aan bij toohello [Azure Publishing portal](https://publish.windowsazure.com/).
2. Klik op **oplossingssjablonen** van Hallo links toocreate een nieuwe oplossingssjabloon.
3. Voer een titel in en klik vervolgens op **Een nieuwe oplossingssjabloon maken**.
4. Klik op **ontwikkelaarscentrumaccount maken en deelnemen aan de Azure-programma Hallo** tooregister van uw bedrijf als u dit nog niet hebt gedaan.  Zie [Een Microsoft-ontwikkelaarsaccount maken](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).
5. Klik op **definiëren van een aantal topologieën tooget gestart**. Een oplossingssjabloon is een 'parent' tooall bijbehorende topologieën. U kunt meerdere topologieën definiëren in één aanbieding/oplossingssjabloon. Wanneer een aanbieding wordt doorgegeven toostaging, wordt deze doorgegeven met alle bijbehorende topologieën. 
6. Voer een naam voor de topologie en klik vervolgens op Hallo plus -teken.
7. Voer een nieuwe versie en klik vervolgens op Hallo plusteken (+).
8. Zip-bestand voor het uploaden van Hallo is voorbereid [pakkettoepassing](#package-application).  
9. Klik op **Certificering aanvragen**. Microsoft-certificeringsteam Hallo Hallo bestanden beoordelen en certificeren Hallo-topologie.

## <a name="next-steps"></a>Volgende stappen
* [HDInsight-toepassingen installeren](hdinsight-apps-install-applications.md): meer informatie over hoe tooinstall een tooyour van de toepassing HDInsight-clusters.
* [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md): meer informatie over hoe een niet-gepubliceerde HDInsight-toepassing tooHDInsight toodeploy.
* [Met behulp van de scriptactie Linux gebaseerde HDInsight-clusters aanpassen](hdinsight-hadoop-customize-cluster-linux.md): meer informatie over hoe toouse scriptactie tooinstall aanvullende toepassingen.
* [Maken van Linux gebaseerde Hadoop-clusters in HDInsight met behulp van Azure Resource Manager-sjablonen](hdinsight-hadoop-create-linux-clusters-arm-templates.md): meer informatie over hoe toocall Resource Manager-sjablonen toocreate HDInsight-clusters.
* [Lege edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md): meer informatie over hoe toouse een lege edge-knooppunt voor toegang tot HDInsight-cluster, HDInsight-toepassingen testen en hosten van HDInsight-toepassingen.

