---
title: HDInsight - Azure-toepassingen publiceren | Microsoft Docs
description: Informatie over het maken en publiceren van HDInsight-toepassingen.
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
ms.openlocfilehash: 6aa66cac35bc317fc87003e6c3d824544c53de88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-hdinsight-applications-into-the-azure-marketplace"></a>HDInsight-toepassingen publiceren in Azure Marketplace
Een HDInsight-toepassing is een toepassing die gebruikers kunnen installeren op een op Linux gebaseerd HDInsight-cluster. Deze toepassingen kunnen zijn ontwikkeld door Microsoft, door onafhankelijke softwareleveranciers (ISV) of door u zelf. In dit artikel leert u hoe u een HDInsight-toepassing in Azure Marketplace publiceert.  Zie [Een aanbieding publiceren in Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) voor algemene informatie over publiceren in Azure Marketplace.

HDInsight-toepassingen maken gebruik van het *BYOL-model (Bring Your Own License)*. Hierbij is de toepassingsprovider verantwoordelijk voor het verlenen van een licentie voor de toepassing aan eindgebruikers. Azure brengt eindgebruikers alleen kosten in rekening voor de resources die ze maken, zoals het HDInsight-cluster en de bijbehorende virtuele machines/knooppunten. Facturering voor de toepassing zelf wordt op dit moment niet gedaan door Azure.

Ander artikel HDInsight toepassingsgerelateerde:

* [HDInsight-toepassingen installeren](hdinsight-apps-install-applications.md): informatie over het installeren van een HDInsight-toepassing op uw clusters.
* [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md): informatie over het installeren en testen van aangepaste HDInsight-toepassingen.

## <a name="prerequisites"></a>Vereisten
Als u uw aangepaste toepassing op de markt, moet u hebt gemaakt en getest van uw aangepaste toepassing. Zie de volgende artikelen:

* [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md): informatie over het installeren en testen van aangepaste HDInsight-toepassingen.

U moet ook hebt geregistreerd uw ontwikkelaarsaccount. Zie [Een aanbieding publiceren in Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) en [Een Microsoft-ontwikkelaarsaccount maken](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).

## <a name="define-application"></a>Uw toepassing definiëren
Het publiceren van toepassingen in Azure Marketplace verloopt in twee stappen.  Eerst definieert u een **createUiDef.json**-bestand om aan te geven met welke clusters de toepassing compatibel is. Vervolgens publiceert u de sjabloon in Azure Portal. De volgende sectie wordt een voorbeeld van een createUiDef.json-bestand.

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
| typen |De clustertypen waarmee de toepassing compatibel is. |Hadoop, HBase, Storm, Spark (of een combinatie hiervan) |
| lagen |De clusterlagen waarmee de toepassing compatibel is. |Standaard, Premium (of beide) |
| versies |De HDInsight-clustertypen waarmee de toepassing compatibel is. |3.4 |

## <a name="application-install-script"></a>Het installatiescript toepassing
Wanneer een toepassing is geïnstalleerd op een cluster (een bestaande of een nieuwe) een edge-knooppunt wordt gemaakt en het installatiescript voor de toepassing wordt uitgevoerd op deze.
  > [!IMPORTANT]
  > De naam van het installatiescript voor de toepassing moet uniek zijn voor een bepaald cluster met de volgende indeling.
  > 
  > name": "[concat('hue-install-v0','-' ,uniekestring(‘toepassingsnaam’)]"
  > 
  > Zoals u ziet, heeft de scriptnaam drie onderdelen:
  > 
  > 1. Een voorvoegsel dat de toepassingsnaam bevat of een naam die relevant is voor de toepassing.
  > 2. Een streepje (-) voor de leesbaarheid.
  > 3. Een unieke tekenreeksfunctie met de toepassingsnaam als parameter.
  > 
  > Een voorbeeld van deze drie onderdelen samen ziet er in de lijst met persistente scriptacties als volgt uit: hue-install-v0-4wkahss55hlas. Zie [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json) voor een voorbeeld van JSON-nettolading.
  > 
Het script voor installatie moet de volgende kenmerken:
1. Zorg ervoor dat het script idempotent is. Meerdere aanroepen naar het script moeten hetzelfde resultaat opleveren.
2. Het script moet juist samengesteld. Gebruik een andere locatie voor het script wanneer u upgradet of wijzigingen testen zodat klanten die probeert te installeren van de toepassing worden niet beïnvloed. 
3. Voldoende logboekregistratie toevoegen aan de scripts op elk moment. De script-logboeken zijn meestal de enige manier om problemen met de installatie van de toepassing voor foutopsporing.
4. Zorg ervoor dat aanroepen naar externe services of resources voldoende pogingen zodat de installatie wordt niet beïnvloed door tijdelijke netwerkproblemen.
5. Als uw script services op de knooppunten starten is, zorg ervoor dat de services wordt gecontroleerd en geconfigureerd om automatisch te starten in geval van een knooppunt opnieuw wordt opgestart.

## <a name="package-application"></a>Pakkettoepassing
Maak een ZIP-bestand met alle vereiste bestanden voor het installeren van de HDInsight-toepassingen. U moet het zip-bestand in [toepassing publiceren](#publish-application).

* [createUiDefinition.json](#define-application).
* mainTemplate.json. Bekijk een voorbeeld bij [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md).
* Alle vereiste scripts.

> [!NOTE]
> U vindt de toepassingsbestanden (inclusief webtoepassingsbestanden, indien aanwezig) op elk willekeurig eindpunt dat openbaar toegankelijk is.
> 

## <a name="publish-application"></a>Uw toepassing publiceren
Volg de volgende stappen om een HDInsight- toepassing te publiceren:

1. Meld u aan bij de [Azure Publishing Portal](https://publish.windowsazure.com/).
2. Klik op **Oplossingssjablonen** aan de linkerkant om een nieuwe oplossingssjabloon te maken.
3. Voer een titel in en klik vervolgens op **Een nieuwe oplossingssjabloon maken**.
4. Klik op **Ontwikkelaarscentrumaccount maken en deelnemen aan het Azure-programma** om uw bedrijf te registreren, als u dit nog niet hebt gedaan.  Zie [Een Microsoft-ontwikkelaarsaccount maken](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).
5. Klik op **Topologieën definiëren om aan de slag te gaan**. Een oplossingssjabloon is een 'ouder' alle bijbehorende topologieën. U kunt meerdere topologieën definiëren in één aanbieding/oplossingssjabloon. Wanneer een aanbieding wordt doorgegeven voor fasering, wordt deze doorgegeven met alle bijbehorende topologieën. 
6. Voer een topologienaam in en klik vervolgens op het plusteken.
7. Voer een nieuwe versie in en klik vervolgens op het plusteken.
8. Upload het ZIP-bestand dat u hebt voorbereid bij [Pakkettoepassing](#package-application).  
9. Klik op **Certificering aanvragen**. Het Microsoft-certificeringsteam beoordeelt de bestanden en certificeert de topologie.

## <a name="next-steps"></a>Volgende stappen
* [HDInsight-toepassingen installeren](hdinsight-apps-install-applications.md): informatie over het installeren van een HDInsight-toepassing op uw clusters.
* [Aangepaste HDInsight-toepassingen installeren](hdinsight-apps-install-custom-applications.md): informatie over het implementeren van een niet-gepubliceerde HDInsight-toepassing op HDInsight.
* [Op Linux gebaseerde HDInsight-clusters aanpassen met behulp van een scriptactie](hdinsight-hadoop-customize-cluster-linux.md): informatie over het gebruik van een scriptactie om extra toepassingen te installeren.
* [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md) (Op Linux gebaseerde Hadoop-clusters maken in HDInsight met behulp van Azure Resource Manager-sjablonen): informatie over het aanroepen van Resource Manager-sjablonen om HDInsight-clusters te maken.
* [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) (Lege edge-knooppunten gebruiken in HDInsight): meer informatie over het gebruik van een leeg edge-knooppunt om toegang te krijgen tot het HDInsight-cluster, HDInsight toepassingen te testen en HDInsight-toepassingen te hosten.

