---
title: aaaCustomize Hadoop-clusters voor Hallo Team gegevens wetenschap proces | Microsoft Docs
description: Populaire Python-modules beschikbaar gesteld in aangepaste Azure HDInsight Hadoop-clusters.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a>Azure HDInsight Hadoop-clusters voor Hallo Team gegevens wetenschap proces aanpassen
Dit artikel wordt beschreven hoe toocustomize een HDInsight Hadoop-cluster met 64-bits Anaconda (Python 2.7) installeren op elk knooppunt wanneer Hallo-cluster is ingericht als een HDInsight-service. U ziet ook hoe tooaccess Hallo headnode toosubmit aangepaste taken toohello cluster. Deze aanpassing veel populaire Python-modules, die zijn opgenomen in Anaconda maakt, gemakkelijk beschikbaar voor gebruik in de gebruiker gedefinieerde functies (UDF's) die zijn ontworpen tooprocess Hive-records in het Hallo-cluster. Zie voor instructies over het Hallo-procedures in dit scenario gebruikt, [hoe toosubmit Hive-query's](machine-learning-data-science-move-hive-tables.md#submit).

Hallo volgende menu koppelingen tootopics waarin wordt beschreven hoe tooset up Hallo verschillende gegevens wetenschappelijke omgevingen gebruikt door Hallo [Team gegevens wetenschap proces (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>Azure HDInsight Hadoop-Cluster aanpassen
toocreate een aangepaste HDInsight Hadoop-cluster door logboekregistratie op te starten[**klassieke Azure-portal**](https://manage.windowsazure.com/), klikt u op **nieuw** op Hallo links hoek beneden en selecteer vervolgens DATA SERVICES HDINSIGHT -> -> **aangepast maken** toobring up Hallo **Clusterdetails** venster. 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Hallo-naam van Hallo cluster toobe gemaakt op de configuratiepagina 1 invoeren en accepteer de standaardwaarden voor Hallo andere velden. Klik op Hallo pijl toogo toohello volgende configuratiepagina. 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Op de configuratiepagina 2 invoer Hallo aantal **GEGEVENSKNOOPPUNTEN**, selecteer Hallo **regio/VIRTUEEL netwerk**, en selecteer Hallo grootten Hallo **HOOFDKNOOPPUNT** en Hallo **GEGEVENSKNOOPPUNT**. Klik op Hallo pijl toogo toohello volgende configuratiepagina.

> [!NOTE]
> Hallo **regio/VIRTUEEL netwerk** toobe Hallo dezelfde als Hallo gebied van Hallo storage-account dat wordt gebruikt voor Hallo HDInsight Hadoop-cluster toobe heeft. Anders in Hallo vierde configuratiepagina van Hallo storage-account wordt niet weergegeven op de vervolgkeuzelijst Hallo van **accountnaam**.
> 
> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

Geef een gebruikersnaam en wachtwoord voor Hallo HDInsight Hadoop-cluster op de configuratiepagina 3. **Geen** Selecteer Hallo *Enter Hallo Hive/Oozie-Metastore*. Klik vervolgens op Hallo pijl toogo toohello volgende configuratiepagina. 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

Geef op de configuratiepagina 4 Hallo-opslagaccountnaam, de standaardcontainer Hallo Hallo HDInsight Hadoop-cluster. Als u selecteert *maken standaardcontainer* in Hallo **STANDAARDCONTAINER** vervolgkeuzelijst wordt weergegeven, een container met Hallo dezelfde naam als het Hallo-cluster wordt gemaakt. Klik op Hallo pijl toogo toohello laatste configuratiepagina.

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

Op Hallo laatste **scriptacties** configuratiepagina, klikt u op **scriptactie toevoegen** knop en vullen tekstvelden Hallo Hallo waarden te volgen.

* **NAAM** -elke tekenreeks als Hallo-naam van de scriptactie
* **KNOOPPUNTTYPE** : Selecteer **alle knooppunten**
* **SCRIPT-URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts* is een openbare container in Hallo storage-account 
  * *getgoing* gebruiken we tooshare PowerShell script bestanden toofacilitate werk van de gebruiker in Azure
* **PARAMETERS** -(leeg laten)

Tot slot op Hallo vinkje toostart Hallo maken van aangepaste Hallo HDInsight Hadoop-cluster. 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a>Toegang tot Hallo Head knooppunt van Hadoop-Cluster
Voordat u toegang hebt tot Hallo hoofdknooppunt van Hallo Hadoop-cluster via RDP, moet u externe toegang toohello Hadoop-cluster in Azure inschakelen. 

1. Meld u bij toohello [ **klassieke Azure-portal**](https://manage.windowsazure.com/), selecteer **HDInsight** aan de linkerkant hello, selecteert u de Hadoop-cluster in Hallo-lijst van clusters, klikt u op Hallo  **CONFIGURATIE** tabblad en klik vervolgens op Hallo **externe inschakelen** pictogram Hallo Hallo pagina onderaan in.
   
    ![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. In Hallo **extern bureaublad configureren** venster Voer Hallo gebruikersnaam en wachtwoordvelden in en selecteer de vervaldatum Hallo voor externe toegang. Klik vervolgens op Hallo vinkje tooenable Hallo RAS toohello hoofdknooppunt van Hallo Hadoop-cluster.
   
    ![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> Hallo-gebruikersnaam en wachtwoord voor externe toegang Hallo zijn niet Hallo-gebruikersnaam en wachtwoord die u gebruikt wanneer u Hallo Hadoop-cluster gemaakt. Dit is een afzonderlijke set referenties. Hallo-vervaldatum van externe toegang Hallo heeft ook toobe binnen 7 dagen van Hallo huidige datum.
> 
> 

Nadat u externe toegang is ingeschakeld, klikt u op **CONNECT** onderaan Hallo Hallo pagina tooremote in Hallo hoofdknooppunt. U zich aanmeldt toohello hoofdknooppunt van het Hadoop-cluster Hallo Hallo referenties invoeren voor Hallo RAS-gebruiker die u eerder hebt opgegeven.

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

Hello zijn de volgende stappen in Hallo advanced analytics-proces toegewezen in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) en stappen voor het verplaatsen van gegevens in HDInsight, en vervolgens verwerken en het voorbeeld ter voorbereiding van het leren van Hallo gegevens bevatten mogelijk met Azure Machine Learning.

Zie [hoe toosubmit Hive-query's](machine-learning-data-science-move-hive-tables.md#submit) voor instructies over hoe tooaccess Python-modules die zijn opgenomen in Anaconda van het hoofdknooppunt van Hallo-cluster in de gebruiker gedefinieerde functies (UDF's) die gebruikt tooprocess zijn Hallo Hallo Hive-records die zijn opgeslagen in het Hallo-cluster.

