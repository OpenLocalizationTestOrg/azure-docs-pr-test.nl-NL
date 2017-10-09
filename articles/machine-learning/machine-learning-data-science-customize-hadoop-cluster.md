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
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a><span data-ttu-id="ab99e-103">Azure HDInsight Hadoop-clusters voor Hallo Team gegevens wetenschap proces aanpassen</span><span class="sxs-lookup"><span data-stu-id="ab99e-103">Customize Azure HDInsight Hadoop clusters for hello Team Data Science Process</span></span>
<span data-ttu-id="ab99e-104">Dit artikel wordt beschreven hoe toocustomize een HDInsight Hadoop-cluster met 64-bits Anaconda (Python 2.7) installeren op elk knooppunt wanneer Hallo-cluster is ingericht als een HDInsight-service.</span><span class="sxs-lookup"><span data-stu-id="ab99e-104">This article describes how toocustomize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when hello cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="ab99e-105">U ziet ook hoe tooaccess Hallo headnode toosubmit aangepaste taken toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="ab99e-105">It also shows how tooaccess hello headnode toosubmit custom jobs toohello cluster.</span></span> <span data-ttu-id="ab99e-106">Deze aanpassing veel populaire Python-modules, die zijn opgenomen in Anaconda maakt, gemakkelijk beschikbaar voor gebruik in de gebruiker gedefinieerde functies (UDF's) die zijn ontworpen tooprocess Hive-records in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ab99e-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed tooprocess Hive records in hello cluster.</span></span> <span data-ttu-id="ab99e-107">Zie voor instructies over het Hallo-procedures in dit scenario gebruikt, [hoe toosubmit Hive-query's](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="ab99e-107">For instructions on hello procedures used in this scenario, see [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="ab99e-108">Hallo volgende menu koppelingen tootopics waarin wordt beschreven hoe tooset up Hallo verschillende gegevens wetenschappelijke omgevingen gebruikt door Hallo [Team gegevens wetenschap proces (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab99e-108">hello following menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="ab99e-109"><a name="customize"></a>Azure HDInsight Hadoop-Cluster aanpassen</span><span class="sxs-lookup"><span data-stu-id="ab99e-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="ab99e-110">toocreate een aangepaste HDInsight Hadoop-cluster door logboekregistratie op te starten[**klassieke Azure-portal**](https://manage.windowsazure.com/), klikt u op **nieuw** op Hallo links hoek beneden en selecteer vervolgens DATA SERVICES HDINSIGHT -> -> **aangepast maken** toobring up Hallo **Clusterdetails** venster.</span><span class="sxs-lookup"><span data-stu-id="ab99e-110">toocreate a customized HDInsight Hadoop cluster, start by logging on too[**Azure classic portal**](https://manage.windowsazure.com/), click **New** at hello left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** toobring up hello **Cluster Details** window.</span></span> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="ab99e-112">Hallo-naam van Hallo cluster toobe gemaakt op de configuratiepagina 1 invoeren en accepteer de standaardwaarden voor Hallo andere velden.</span><span class="sxs-lookup"><span data-stu-id="ab99e-112">Input hello name of hello cluster toobe created on configuration page 1, and accept default values for hello other fields.</span></span> <span data-ttu-id="ab99e-113">Klik op Hallo pijl toogo toohello volgende configuratiepagina.</span><span class="sxs-lookup"><span data-stu-id="ab99e-113">Click hello arrow toogo toohello next configuration page.</span></span> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="ab99e-115">Op de configuratiepagina 2 invoer Hallo aantal **GEGEVENSKNOOPPUNTEN**, selecteer Hallo **regio/VIRTUEEL netwerk**, en selecteer Hallo grootten Hallo **HOOFDKNOOPPUNT** en Hallo **GEGEVENSKNOOPPUNT**.</span><span class="sxs-lookup"><span data-stu-id="ab99e-115">On configuration page 2, input hello number of **DATA NODES**, select hello **REGION/VIRTUAL NETWORK**, and select hello sizes of hello **HEAD NODE** and hello **DATA NODE**.</span></span> <span data-ttu-id="ab99e-116">Klik op Hallo pijl toogo toohello volgende configuratiepagina.</span><span class="sxs-lookup"><span data-stu-id="ab99e-116">Click hello arrow toogo toohello next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="ab99e-117">Hallo **regio/VIRTUEEL netwerk** toobe Hallo dezelfde als Hallo gebied van Hallo storage-account dat wordt gebruikt voor Hallo HDInsight Hadoop-cluster toobe heeft.</span><span class="sxs-lookup"><span data-stu-id="ab99e-117">hello **REGION/VIRTUAL NETWORK** has toobe hello same as hello region of hello storage account that is going toobe used for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="ab99e-118">Anders in Hallo vierde configuratiepagina van Hallo storage-account wordt niet weergegeven op de vervolgkeuzelijst Hallo van **accountnaam**.</span><span class="sxs-lookup"><span data-stu-id="ab99e-118">Otherwise, in hello fourth configuration page, hello storage account will not appear on hello dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="ab99e-120">Geef een gebruikersnaam en wachtwoord voor Hallo HDInsight Hadoop-cluster op de configuratiepagina 3.</span><span class="sxs-lookup"><span data-stu-id="ab99e-120">On configuration page 3, provide a user name and password for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="ab99e-121">**Geen** Selecteer Hallo *Enter Hallo Hive/Oozie-Metastore*.</span><span class="sxs-lookup"><span data-stu-id="ab99e-121">**Do not** select hello *Enter hello Hive/Oozie Metastore*.</span></span> <span data-ttu-id="ab99e-122">Klik vervolgens op Hallo pijl toogo toohello volgende configuratiepagina.</span><span class="sxs-lookup"><span data-stu-id="ab99e-122">Then, click hello arrow toogo toohello next configuration page.</span></span> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="ab99e-124">Geef op de configuratiepagina 4 Hallo-opslagaccountnaam, de standaardcontainer Hallo Hallo HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="ab99e-124">On configuration page 4, specify hello storage account name, hello default container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="ab99e-125">Als u selecteert *maken standaardcontainer* in Hallo **STANDAARDCONTAINER** vervolgkeuzelijst wordt weergegeven, een container met Hallo dezelfde naam als het Hallo-cluster wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ab99e-125">If you select *Create default container* in hello **DEFAULT CONTAINER** dropdown list, a container with hello same name as hello cluster will be created.</span></span> <span data-ttu-id="ab99e-126">Klik op Hallo pijl toogo toohello laatste configuratiepagina.</span><span class="sxs-lookup"><span data-stu-id="ab99e-126">Click hello arrow toogo toohello last configuration page.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="ab99e-128">Op Hallo laatste **scriptacties** configuratiepagina, klikt u op **scriptactie toevoegen** knop en vullen tekstvelden Hallo Hallo waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="ab99e-128">On hello final **Script Actions** configuration page, click **add script action** button, and fill hello text fields with hello following values.</span></span>

* <span data-ttu-id="ab99e-129">**NAAM** -elke tekenreeks als Hallo-naam van de scriptactie</span><span class="sxs-lookup"><span data-stu-id="ab99e-129">**NAME** - any string as hello name of this script action</span></span>
* <span data-ttu-id="ab99e-130">**KNOOPPUNTTYPE** : Selecteer **alle knooppunten**</span><span class="sxs-lookup"><span data-stu-id="ab99e-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="ab99e-131">**SCRIPT-URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="ab99e-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="ab99e-132">*publicscripts* is een openbare container in Hallo storage-account</span><span class="sxs-lookup"><span data-stu-id="ab99e-132">*publicscripts* is a public container in hello storage account</span></span> 
  * <span data-ttu-id="ab99e-133">*getgoing* gebruiken we tooshare PowerShell script bestanden toofacilitate werk van de gebruiker in Azure</span><span class="sxs-lookup"><span data-stu-id="ab99e-133">*getgoing* we use tooshare PowerShell script files toofacilitate users' work in Azure</span></span>
* <span data-ttu-id="ab99e-134">**PARAMETERS** -(leeg laten)</span><span class="sxs-lookup"><span data-stu-id="ab99e-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="ab99e-135">Tot slot op Hallo vinkje toostart Hallo maken van aangepaste Hallo HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="ab99e-135">Finally, click hello check mark toostart hello creation of hello customized HDInsight Hadoop cluster.</span></span> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="ab99e-137"><a name="headnode"></a>Toegang tot Hallo Head knooppunt van Hadoop-Cluster</span><span class="sxs-lookup"><span data-stu-id="ab99e-137"><a name="headnode"></a> Access hello Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="ab99e-138">Voordat u toegang hebt tot Hallo hoofdknooppunt van Hallo Hadoop-cluster via RDP, moet u externe toegang toohello Hadoop-cluster in Azure inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ab99e-138">You must enable remote access toohello Hadoop cluster in Azure before you can access hello head node of hello Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="ab99e-139">Meld u bij toohello [ **klassieke Azure-portal**](https://manage.windowsazure.com/), selecteer **HDInsight** aan de linkerkant hello, selecteert u de Hadoop-cluster in Hallo-lijst van clusters, klikt u op Hallo  **CONFIGURATIE** tabblad en klik vervolgens op Hallo **externe inschakelen** pictogram Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="ab99e-139">Log in toohello [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on hello left, select your Hadoop cluster from hello list of clusters, click hello **CONFIGURATION** tab, and then click hello **ENABLE REMOTE** icon at hello bottom of hello page.</span></span>
   
    ![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="ab99e-141">In Hallo **extern bureaublad configureren** venster Voer Hallo gebruikersnaam en wachtwoordvelden in en selecteer de vervaldatum Hallo voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="ab99e-141">In hello **Configure Remote Desktop** window, enter hello USER NAME and PASSWORD fields, and select hello expiration date for remote access.</span></span> <span data-ttu-id="ab99e-142">Klik vervolgens op Hallo vinkje tooenable Hallo RAS toohello hoofdknooppunt van Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="ab99e-142">Then click hello check mark tooenable hello remote access toohello head node of hello Hadoop cluster.</span></span>
   
    ![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="ab99e-144">Hallo-gebruikersnaam en wachtwoord voor externe toegang Hallo zijn niet Hallo-gebruikersnaam en wachtwoord die u gebruikt wanneer u Hallo Hadoop-cluster gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ab99e-144">hello user name and password for hello remote access are not hello user name and password that you use when you created hello Hadoop cluster.</span></span> <span data-ttu-id="ab99e-145">Dit is een afzonderlijke set referenties.</span><span class="sxs-lookup"><span data-stu-id="ab99e-145">This is a separate set of credentials.</span></span> <span data-ttu-id="ab99e-146">Hallo-vervaldatum van externe toegang Hallo heeft ook toobe binnen 7 dagen van Hallo huidige datum.</span><span class="sxs-lookup"><span data-stu-id="ab99e-146">Also, hello expiration date of hello remote access has toobe within 7 days from hello current date.</span></span>
> 
> 

<span data-ttu-id="ab99e-147">Nadat u externe toegang is ingeschakeld, klikt u op **CONNECT** onderaan Hallo Hallo pagina tooremote in Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="ab99e-147">After remote access is enabled, click **CONNECT** at hello bottom of hello page tooremote into hello head node.</span></span> <span data-ttu-id="ab99e-148">U zich aanmeldt toohello hoofdknooppunt van het Hadoop-cluster Hallo Hallo referenties invoeren voor Hallo RAS-gebruiker die u eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ab99e-148">You log on toohello head node of hello Hadoop cluster by entering hello credentials for hello remote access user that you specified earlier.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="ab99e-150">Hello zijn de volgende stappen in Hallo advanced analytics-proces toegewezen in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) en stappen voor het verplaatsen van gegevens in HDInsight, en vervolgens verwerken en het voorbeeld ter voorbereiding van het leren van Hallo gegevens bevatten mogelijk met Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="ab99e-150">hello next steps in hello advanced analytics process are mapped in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

<span data-ttu-id="ab99e-151">Zie [hoe toosubmit Hive-query's](machine-learning-data-science-move-hive-tables.md#submit) voor instructies over hoe tooaccess Python-modules die zijn opgenomen in Anaconda van het hoofdknooppunt van Hallo-cluster in de gebruiker gedefinieerde functies (UDF's) die gebruikt tooprocess zijn Hallo Hallo Hive-records die zijn opgeslagen in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ab99e-151">See [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how tooaccess hello Python modules that are included in Anaconda from hello head node of hello cluster in user-defined functions (UDFs) that are used tooprocess Hive records stored in hello cluster.</span></span>

