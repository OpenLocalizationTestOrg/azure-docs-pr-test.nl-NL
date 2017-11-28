---
title: Hadoop-clusters aanpassen voor het Team gegevens wetenschap proces | Microsoft Docs
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
ms.openlocfilehash: 53ff04ee66b08ae36f3550536c659a547c658fd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-the-team-data-science-process"></a><span data-ttu-id="c4e24-103">Azure HDInsight Hadoop-clusters aanpassen voor Team Data Science Process</span><span class="sxs-lookup"><span data-stu-id="c4e24-103">Customize Azure HDInsight Hadoop clusters for the Team Data Science Process</span></span>
<span data-ttu-id="c4e24-104">In dit artikel beschrijft hoe een HDInsight Hadoop-cluster aanpassen door het 64-bits Anaconda (Python 2.7) installeren op elk knooppunt wanneer het cluster is ingericht als een HDInsight-service.</span><span class="sxs-lookup"><span data-stu-id="c4e24-104">This article describes how to customize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when the cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="c4e24-105">Ook ziet u hoe voor toegang tot de headnode voor het verzenden van aangepaste taken aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="c4e24-105">It also shows how to access the headnode to submit custom jobs to the cluster.</span></span> <span data-ttu-id="c4e24-106">Deze aanpassing wordt veel populaire Python-modules, die zijn opgenomen in Anaconda, gemakkelijk beschikbaar voor gebruik in de gebruiker gedefinieerde functies (UDF's) die zijn ontworpen voor het verwerken van Hive-records in het cluster.</span><span class="sxs-lookup"><span data-stu-id="c4e24-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed to process Hive records in the cluster.</span></span> <span data-ttu-id="c4e24-107">Zie voor instructies voor de procedures in dit scenario gebruikt, [het indienen van Hive-query's](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="c4e24-107">For instructions on the procedures used in this scenario, see [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="c4e24-108">De volgende menukoppelingen naar onderwerpen waarin wordt beschreven hoe u voor het instellen van de verschillende gegevens wetenschappelijke omgevingen die worden gebruikt door de [Team gegevens wetenschap proces (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4e24-108">The following menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="c4e24-109"><a name="customize"></a>Azure HDInsight Hadoop-Cluster aanpassen</span><span class="sxs-lookup"><span data-stu-id="c4e24-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="c4e24-110">Voor het maken van aangepaste HDInsight Hadoop-cluster, starten door in te loggen bij [ **klassieke Azure-portal**](https://manage.windowsazure.com/), klikt u op **nieuw** op de links linksonder en selecteer vervolgens DATA SERVICES - > HDINSIGHT -> **aangepast maken** online zetten van de **Clusterdetails** venster.</span><span class="sxs-lookup"><span data-stu-id="c4e24-110">To create a customized HDInsight Hadoop cluster, start by logging on to [**Azure classic portal**](https://manage.windowsazure.com/), click **New** at the left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** to bring up the **Cluster Details** window.</span></span> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="c4e24-112">De naam van het cluster moet worden gemaakt op de configuratiepagina 1 invoeren en accepteer de standaardwaarden voor de andere velden.</span><span class="sxs-lookup"><span data-stu-id="c4e24-112">Input the name of the cluster to be created on configuration page 1, and accept default values for the other fields.</span></span> <span data-ttu-id="c4e24-113">Klik op de pijl naar de volgende pagina van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="c4e24-113">Click the arrow to go to the next configuration page.</span></span> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="c4e24-115">Voer het aantal op de configuratiepagina 2 **GEGEVENSKNOOPPUNTEN**, selecteer de **regio/VIRTUEEL netwerk**, en selecteert u de grootte van de **HOOFDKNOOPPUNT** en de **gegevens KNOOPPUNT**.</span><span class="sxs-lookup"><span data-stu-id="c4e24-115">On configuration page 2, input the number of **DATA NODES**, select the **REGION/VIRTUAL NETWORK**, and select the sizes of the **HEAD NODE** and the **DATA NODE**.</span></span> <span data-ttu-id="c4e24-116">Klik op de pijl naar de volgende pagina van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="c4e24-116">Click the arrow to go to the next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="c4e24-117">De **regio/VIRTUEEL netwerk** moet hetzelfde zijn als de regio van het opslagaccount dat u wilt worden gebruikt voor het HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4e24-117">The **REGION/VIRTUAL NETWORK** has to be the same as the region of the storage account that is going to be used for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="c4e24-118">Anders in de vierde pagina van de configuratie van het opslagaccount wordt niet weergegeven op de vervolgkeuzelijst van **accountnaam**.</span><span class="sxs-lookup"><span data-stu-id="c4e24-118">Otherwise, in the fourth configuration page, the storage account will not appear on the dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="c4e24-120">Geef een gebruikersnaam en wachtwoord voor het HDInsight Hadoop-cluster op de configuratiepagina 3.</span><span class="sxs-lookup"><span data-stu-id="c4e24-120">On configuration page 3, provide a user name and password for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="c4e24-121">**Geen** selecteert u de *Voer de Hive/Oozie-Metastore*.</span><span class="sxs-lookup"><span data-stu-id="c4e24-121">**Do not** select the *Enter the Hive/Oozie Metastore*.</span></span> <span data-ttu-id="c4e24-122">Klik vervolgens op de pijl naar de volgende pagina van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="c4e24-122">Then, click the arrow to go to the next configuration page.</span></span> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="c4e24-124">Geef de naam van het opslagaccount, de standaardcontainer van HDInsight Hadoop-cluster op de configuratiepagina 4.</span><span class="sxs-lookup"><span data-stu-id="c4e24-124">On configuration page 4, specify the storage account name, the default container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="c4e24-125">Als u selecteert *maken standaardcontainer* in de **STANDAARDCONTAINER** dropdown wilt weergeven, een container met dezelfde naam als het cluster wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4e24-125">If you select *Create default container* in the **DEFAULT CONTAINER** dropdown list, a container with the same name as the cluster will be created.</span></span> <span data-ttu-id="c4e24-126">Klik op de pijl om door te gaan naar de laatste configuratiepagina.</span><span class="sxs-lookup"><span data-stu-id="c4e24-126">Click the arrow to go to the last configuration page.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="c4e24-128">Op het uiteindelijke **scriptacties** configuratiepagina, klikt u op **scriptactie toevoegen** knop en de tekstvelden vullen met de volgende waarden.</span><span class="sxs-lookup"><span data-stu-id="c4e24-128">On the final **Script Actions** configuration page, click **add script action** button, and fill the text fields with the following values.</span></span>

* <span data-ttu-id="c4e24-129">**NAAM** -elke tekenreeks als de naam van deze scriptactie</span><span class="sxs-lookup"><span data-stu-id="c4e24-129">**NAME** - any string as the name of this script action</span></span>
* <span data-ttu-id="c4e24-130">**KNOOPPUNTTYPE** : Selecteer **alle knooppunten**</span><span class="sxs-lookup"><span data-stu-id="c4e24-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="c4e24-131">**SCRIPT-URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="c4e24-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="c4e24-132">*publicscripts* is een openbare container in het opslagaccount</span><span class="sxs-lookup"><span data-stu-id="c4e24-132">*publicscripts* is a public container in the storage account</span></span> 
  * <span data-ttu-id="c4e24-133">*getgoing* wij gebruiken voor het delen van bestanden van de PowerShell-script wilt vergemakkelijken werk van de gebruiker in Azure</span><span class="sxs-lookup"><span data-stu-id="c4e24-133">*getgoing* we use to share PowerShell script files to facilitate users' work in Azure</span></span>
* <span data-ttu-id="c4e24-134">**PARAMETERS** -(leeg laten)</span><span class="sxs-lookup"><span data-stu-id="c4e24-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="c4e24-135">Tot slot klikt u op het vinkje voor het starten van het maken van aangepaste HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4e24-135">Finally, click the check mark to start the creation of the customized HDInsight Hadoop cluster.</span></span> 

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="c4e24-137"><a name="headnode"></a>Toegang tot het hoofdknooppunt van Hadoop-Cluster</span><span class="sxs-lookup"><span data-stu-id="c4e24-137"><a name="headnode"></a> Access the Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="c4e24-138">Voordat u toegang hebt tot het hoofdknooppunt van het Hadoop-cluster via RDP, moet u externe toegang tot het Hadoop-cluster in Azure inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c4e24-138">You must enable remote access to the Hadoop cluster in Azure before you can access the head node of the Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="c4e24-139">Meld u aan bij de [ **klassieke Azure-portal**](https://manage.windowsazure.com/), selecteer **HDInsight** aan de linkerkant Hadoop-cluster in de lijst met clusters, klik op de **configuratie**  tabblad en klik vervolgens op de **externe inschakelen** pictogram aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="c4e24-139">Log in to the [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on the left, select your Hadoop cluster from the list of clusters, click the **CONFIGURATION** tab, and then click the **ENABLE REMOTE** icon at the bottom of the page.</span></span>
   
    ![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="c4e24-141">In de **extern bureaublad configureren** venster de velden gebruikersnaam en wachtwoord invoeren en selecteer de vervaldatum voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="c4e24-141">In the **Configure Remote Desktop** window, enter the USER NAME and PASSWORD fields, and select the expiration date for remote access.</span></span> <span data-ttu-id="c4e24-142">Klik vervolgens op het vinkje om de externe toegang met het hoofdknooppunt van het Hadoop-cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="c4e24-142">Then click the check mark to enable the remote access to the head node of the Hadoop cluster.</span></span>
   
    ![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="c4e24-144">De gebruikersnaam en wachtwoord voor de externe toegang zijn niet de gebruikersnaam en wachtwoord op dat u bij het maken van het Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="c4e24-144">The user name and password for the remote access are not the user name and password that you use when you created the Hadoop cluster.</span></span> <span data-ttu-id="c4e24-145">Dit is een afzonderlijke set referenties.</span><span class="sxs-lookup"><span data-stu-id="c4e24-145">This is a separate set of credentials.</span></span> <span data-ttu-id="c4e24-146">Daarnaast heeft de vervaldatum van de RAS-binnen 7 dagen vanaf de huidige datum.</span><span class="sxs-lookup"><span data-stu-id="c4e24-146">Also, the expiration date of the remote access has to be within 7 days from the current date.</span></span>
> 
> 

<span data-ttu-id="c4e24-147">Nadat u externe toegang is ingeschakeld, klikt u op **CONNECT** aan de onderkant van de pagina op afstand verbinding met het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="c4e24-147">After remote access is enabled, click **CONNECT** at the bottom of the page to remote into the head node.</span></span> <span data-ttu-id="c4e24-148">U aanmelden met het hoofdknooppunt van het Hadoop-cluster door te voeren van de referenties voor de RAS-gebruiker die u eerder hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c4e24-148">You log on to the head node of the Hadoop cluster by entering the credentials for the remote access user that you specified earlier.</span></span>

![Werkruimte maken](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="c4e24-150">De volgende stappen in het proces geavanceerde analyses zijn toegewezen de [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) en bevatten mogelijk stappen die gegevens in HDInsight, verplaatsen en vervolgens verwerken en het voorbeeld ter voorbereiding van het leren van de gegevens met Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c4e24-150">The next steps in the advanced analytics process are mapped in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

<span data-ttu-id="c4e24-151">Zie [het indienen van Hive-query's](machine-learning-data-science-move-hive-tables.md#submit) voor instructies over het toegang krijgen tot de Python-modules die zijn opgenomen in Anaconda van het hoofdknooppunt van het cluster in de gebruiker gedefinieerde functies (UDF's) die worden gebruikt voor het verwerken van Hive-records die zijn opgeslagen in de cluster.</span><span class="sxs-lookup"><span data-stu-id="c4e24-151">See [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how to access the Python modules that are included in Anaconda from the head node of the cluster in user-defined functions (UDFs) that are used to process Hive records stored in the cluster.</span></span>

