---
title: Aan de slag met R Server op HDInsight - Azure | Microsoft Docs
description: Informatie over hoe u een Apache Spark op HDInsight-cluster maakt dat R-Server omvat en over het verzenden van een R-script op het cluster.
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: 14e2a14c74e00709e18a80325fbdd3cbcd71da37
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="9b3db-103">Aan de slag met R Server op HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b3db-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="9b3db-104">HDInsight bevat een R Server-optie die kan worden geïntegreerd in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-104">HDInsight includes an R Server option to be integrated into your HDInsight cluster.</span></span> <span data-ttu-id="9b3db-105">Met deze optie kunnen R-scripts gebruikmaken van Spark en MapReduce om gedistribueerde berekeningen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-105">This option allows R scripts to use Spark and MapReduce to run distributed computations.</span></span> <span data-ttu-id="9b3db-106">In dit document leert u hoe u een R Server op HDInsight-cluster maakt. Vervolgens voert u een R-script uit waarin wordt gedemonstreerd hoe Spark wordt gebruikt voor gedistribueerde R-berekeningen.</span><span class="sxs-lookup"><span data-stu-id="9b3db-106">In this document, you learn how to create an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9b3db-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9b3db-107">Prerequisites</span></span>

* <span data-ttu-id="9b3db-108">**Een Azure-abonnement**: voordat u aan deze zelfstudie begint, moet u beschikken over een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9b3db-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="9b3db-109">Raadpleeg het artikel [Een gratis proefversie van Microsoft Azure krijgen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9b3db-109">Go to the article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="9b3db-110">**Een SSH-client (Secure Shell)**: er wordt een SSH-client gebruikt om extern verbinding te maken met het HDInsight-cluster en om opdrachten rechtstreeks uit te voeren op het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-110">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span></span> <span data-ttu-id="9b3db-111">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9b3db-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="9b3db-112">**SSH-sleutels (optioneel)**: u kunt het SSH-account dat wordt gebruikt om verbinding te maken met het cluster, beveiligen met behulp van een wachtwoord of een openbare sleutel.</span><span class="sxs-lookup"><span data-stu-id="9b3db-112">**SSH keys (optional)**: You can secure the SSH account used to connect to the cluster using either a password or a public key.</span></span> <span data-ttu-id="9b3db-113">Het is eenvoudiger om een wachtwoord te gebruiken. Bovendien kunt u dan aan de slag gaan zonder eerst een openbaar/persoonlijk sleutelpaar te hoeven maken.</span><span class="sxs-lookup"><span data-stu-id="9b3db-113">Using a password is easier, and allows you to get started without having to create a public/private key pair.</span></span> <span data-ttu-id="9b3db-114">Het gebruik van een sleutel is echter veiliger.</span><span class="sxs-lookup"><span data-stu-id="9b3db-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="9b3db-115">Bij de stappen in dit document wordt ervan uitgegaan dat u een wachtwoord gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-115">The steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="9b3db-116">Automatisch een cluster maken</span><span class="sxs-lookup"><span data-stu-id="9b3db-116">Automated cluster creation</span></span>

<span data-ttu-id="9b3db-117">U kunt het maken van HDInsight R Servers automatiseren met Azure Resource Manager-sjablonen, de SDK of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b3db-117">You can automate the creation of HDInsight R Servers using Azure Resource Manager templates, the SDK, and also PowerShell.</span></span>

* <span data-ttu-id="9b3db-118">Zie [Deploy an R-server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/) (Een HDInsight-cluster op basis van R Server implementeren) voor het maken van een R Server met een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="9b3db-118">To create an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="9b3db-119">Zie [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) (In HDInsight op Linux gebaseerde clusters maken met de .NET-SDK) als u een R Server wilt maken met behulp van de .NET-SDK.</span><span class="sxs-lookup"><span data-stu-id="9b3db-119">To create an R Server using the .NET SDK, see [create Linux-based clusters in HDInsight using the .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="9b3db-120">Als u R Server wilt implementeren met PowerShell, raadpleegt u het artikel [Creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) (Een R Server in HDInsight maken met PowerShell).</span><span class="sxs-lookup"><span data-stu-id="9b3db-120">To deploy R Server using powershell, see the article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-the-cluster-using-the-azure-portal"></a><span data-ttu-id="9b3db-121">Het cluster maken met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9b3db-121">Create the cluster using the Azure portal</span></span>

1. <span data-ttu-id="9b3db-122">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b3db-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9b3db-123">Selecteer **NIEUW** -> **Intelligence en analyse**, -> **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9b3db-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Afbeelding van het maken van een nieuw cluster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="9b3db-125">Voer onder **Snel maken** in het veld **Clusternaam** een naam in voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-125">In the **Quick create** experience, enter a name for the cluster in the **Cluster Name** field.</span></span> <span data-ttu-id="9b3db-126">Als u meerdere Azure-abonnementen hebt, gebruikt u de vermelding **Abonnement** om het abonnement te selecteren dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9b3db-126">If you have multiple Azure subscriptions, use the **Subscription** entry to select the one you want to use.</span></span>

    ![Clusternaam en geselecteerde abonnementen](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="9b3db-128">Selecteer **Clustertype** om de blade **Clusterconfiguratie** te openen.</span><span class="sxs-lookup"><span data-stu-id="9b3db-128">Select **Cluster type** to open the **Cluster configuration** blade.</span></span> <span data-ttu-id="9b3db-129">Selecteer op de blade **Clusterconfiguratie** de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="9b3db-129">On the **Cluster Configuration** blade, select the following options:</span></span>

    * <span data-ttu-id="9b3db-130">**Clustertype**: R Server</span><span class="sxs-lookup"><span data-stu-id="9b3db-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="9b3db-131">**Versie**: selecteer de versie van R Server om te installeren op het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-131">**Version**: select the version of R Server to install on the cluster.</span></span> <span data-ttu-id="9b3db-132">De momenteel beschikbare versie is ***R Server 9.1 (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="9b3db-132">The version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="9b3db-133">Releaseopmerkingen voor de beschikbare versies van R Server vindt u [hier](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="9b3db-133">Release notes for the available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="9b3db-134">**R Studio Community-editie voor R Server**: deze IDE op basis van een browser wordt standaard geïnstalleerd op het Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on the edge node.</span></span> <span data-ttu-id="9b3db-135">Schakel het selectievakje uit als u deze liever niet wilt laten installeren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-135">If you would prefer to not have it installed, then uncheck the check box.</span></span> <span data-ttu-id="9b3db-136">Als u ervoor kiest deze wel te laten installeren, bevindt de URL naar de aanmeldingspagina voor RStudio Server zich op een portaltoepassingsblade voor het cluster nadat het is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-136">If you choose to have it installed, the URL for accessing the RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="9b3db-137">Laat bij de andere opties de standaardwaarden staan en gebruik de knop **Selecteren** om clustertype op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9b3db-137">Leave the other options at the default values and use the **Select** button to save the cluster type.</span></span>

        ![Schermafbeelding van de blade Clustertype](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="9b3db-139">Voer een **gebruikersnaam** en **wachtwoord** voor aanmelden bij het cluster in.</span><span class="sxs-lookup"><span data-stu-id="9b3db-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="9b3db-140">Geef een **SSH-gebruikersnaam** op.</span><span class="sxs-lookup"><span data-stu-id="9b3db-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="9b3db-141">SSH wordt gebruikt om extern verbinding te maken met het cluster met behulp van een **SSH-client (Secure Shell)**.</span><span class="sxs-lookup"><span data-stu-id="9b3db-141">SSH is used to remotely connect to the cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="9b3db-142">U kunt de SSH-gebruiker in dit dialoogvenster opgeven of nadat het cluster is gemaakt (in het tabblad Configuratie voor het cluster).</span><span class="sxs-lookup"><span data-stu-id="9b3db-142">You can either specify the SSH user in this dialog or after the cluster has been created (in the Configuration tab for the cluster).</span></span> <span data-ttu-id="9b3db-143">R Server is zo geconfigureerd dat een **SSH-gebruikersnaam** ´remoteuser´ wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="9b3db-143">R Server is configured to expect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="9b3db-144">**Als u een andere gebruikersnaam gebruikt, moet u een extra stap uitvoeren nadat het cluster is gemaakt.**</span><span class="sxs-lookup"><span data-stu-id="9b3db-144">**If you use a different username, you must perform an additional step after the cluster is created.**</span></span>

    <span data-ttu-id="9b3db-145">Als u een **WACHTWOORD** wilt gebruiken als verificatietype, laat u het vakje **Hetzelfde wachtwoord als voor aanmelding bij cluster gebruiken** ingeschakeld, tenzij u liever een openbare sleutel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-145">Leave the box checked for **Use same password as cluster login** to use **PASSWORD** as the authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="9b3db-146">U hebt een openbaar/persoonlijk sleutelpaar nodig voor toegang tot R Server op het cluster via een externe client, bijvoorbeeld RTVS, RStudio of een andere bureaublad-IDE.</span><span class="sxs-lookup"><span data-stu-id="9b3db-146">You need a public/private key pair to access R Server on the cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="9b3db-147">Als u de RStudio Server Community-editie installeert, moet u een SSH-wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="9b3db-147">If you install the RStudio Server community edition, you need to choose an SSH password.</span></span>     

    <span data-ttu-id="9b3db-148">Schakel **Hetzelfde wachtwoord als voor aanmelding bij cluster gebruiken** uit en selecteer vervolgens **OPENBARE SLEUTEL** en volg de aangegeven stappen.</span><span class="sxs-lookup"><span data-stu-id="9b3db-148">To create and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="9b3db-149">Bij deze instructies wordt ervan uitgegaan dat u Cygwin SSH-keygen of iets gelijkwaardigs hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9b3db-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="9b3db-150">Een openbaar/persoonlijk sleutelpaar genereren via de opdrachtprompt op uw laptop:</span><span class="sxs-lookup"><span data-stu-id="9b3db-150">Generate a public/private key pair from the command prompt on your laptop:</span></span>

        <span data-ttu-id="9b3db-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="9b3db-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="9b3db-152">Volg de prompt om een sleutelbestand een naam te geven en voer vervolgens een wachtwoordzin in voor extra beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9b3db-152">Follow the prompt to name a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="9b3db-153">Het scherm moet er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="9b3db-153">Your screen should look something like the following image:</span></span>

        ![SSH-opdrachtregel in Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="9b3db-155">Met deze opdracht maakt u een persoonlijk sleutelbestand en een openbaar sleutelbestand onder de naam <persoonlijke-sleutel-bestandsnaam>.pub, bijvoorbeeld furiosa en furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="9b3db-155">This command creates a private key file and a public key file under the name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![SSH-dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="9b3db-157">Geef vervolgens het openbare sleutelbestand (&#42;.pub) op bij het toewijzen van de referenties voor het HDI-cluster. Ten slotte bevestigt u de resourcegroep en regio, en selecteert u **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9b3db-157">Then specify the public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Blade Referenties](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="9b3db-159">Machtigingen voor het persoonlijke sleutelbestand op uw laptop wijzigen:</span><span class="sxs-lookup"><span data-stu-id="9b3db-159">Change permissions on the private keyfile on your laptop:</span></span>

        <span data-ttu-id="9b3db-160">chmod 600 <bestandsnaam-persoonlijke-sleutel></span><span class="sxs-lookup"><span data-stu-id="9b3db-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="9b3db-161">Het persoonlijke sleutelbestand met SSH gebruiken voor externe aanmelding:</span><span class="sxs-lookup"><span data-stu-id="9b3db-161">Use the private key file with SSH for remote login:</span></span>

        <span data-ttu-id="9b3db-162">ssh – i <bestandsnaam-persoonlijke-sleutel> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="9b3db-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="9b3db-163">Of als onderdeel van de definitie van uw Hadoop Spark-compute-context voor R Server op de client.</span><span class="sxs-lookup"><span data-stu-id="9b3db-163">Or, as part the definition of your Hadoop Spark compute context for R Server on the client.</span></span> <span data-ttu-id="9b3db-164">Zie de subsectie **Using Microsoft R Server as a Hadoop Client** (Microsoft R Server als Hadoop Client gebruiken) [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark) (een Compute-Context voor Spark maken).</span><span class="sxs-lookup"><span data-stu-id="9b3db-164">See the **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="9b3db-165">Via Snel maken wordt u naar de blade **Opslag** geleid om de instellingen voor het opslagaccount voor de primaire locatie van het HDFS-bestandssysteem te selecteren dat wordt gebruikt voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-165">The quick create transitions you to the **Storage** blade to select the storage account settings to be used for the primary location of the HDFS file system used by the cluster.</span></span> <span data-ttu-id="9b3db-166">Selecteer een nieuw of een bestaand Azure Storage-account of een bestaand Data Lake Storage-account.</span><span class="sxs-lookup"><span data-stu-id="9b3db-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="9b3db-167">Als u een Azure Storage-account selecteert, wordt een bestaand opslagaccount geselecteerd door eerst **Een opslagaccount selecteren** te kiezen en vervolgens het relevante account te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting the relevant account.</span></span> <span data-ttu-id="9b3db-168">Maak een nieuw account via de koppeling **Nieuw** in de sectie **Een opslagaccount selecteren**.</span><span class="sxs-lookup"><span data-stu-id="9b3db-168">Create a new account using the **Create New** link in the **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="9b3db-169">Als u **Nieuw** selecteert, moet u een naam invoeren voor het nieuwe opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="9b3db-169">If you select **New** you must enter a name for the new storage account.</span></span> <span data-ttu-id="9b3db-170">Er verschijnt een groen vinkje als de naam wordt geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="9b3db-170">A green check appears if the name is accepted.</span></span>

      <span data-ttu-id="9b3db-171">De **Standaardcontainer** krijgt dezelfde naam als het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-171">The **Default Container** defaults to the name of the cluster.</span></span> <span data-ttu-id="9b3db-172">Laat deze standaardwaarde staan.</span><span class="sxs-lookup"><span data-stu-id="9b3db-172">Leave this default as the value.</span></span>

      <span data-ttu-id="9b3db-173">Als er een nieuwe optie voor het opslagaccount is geselecteerd, ziet u een prompt om de **Locatie** te selecteren, waar u selecteert in welke regio het opslagaccount moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-173">If a new storage account option was selected a prompt to select **Location** is given to select which region to create the storage account.</span></span>  

         ![Blade Gegevensbron](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="9b3db-175">Als u de locatie van de standaardgegevensbron selecteert, wordt ook de locatie van het HDInsight-cluster ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9b3db-175">Selecting the location for the default data source  also sets the location of the HDInsight cluster.</span></span> <span data-ttu-id="9b3db-176">Het cluster en de standaardgegevensbron moeten zich in dezelfde regio bevinden.</span><span class="sxs-lookup"><span data-stu-id="9b3db-176">The cluster and default data source must be in the same region.</span></span>

    - <span data-ttu-id="9b3db-177">Als u een bestaand Data Lake Store-account wilt gebruiken, selecteert u het gewenste ADLS-opslagaccount en voegt u de *ADD*-clusteridentiteit toe aan uw cluster om toegang tot Data Lake Store toe te staan.</span><span class="sxs-lookup"><span data-stu-id="9b3db-177">If you want to use an existing Data Lake Store, then select the ADLS storage account to use and add the cluster *ADD* identity to your cluster to allow access to the store.</span></span> <span data-ttu-id="9b3db-178">Raadpleeg [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal) (HDInsight-cluster met Data Lake Store maken met behulp van Azure Portal) voor meer informatie over dit proces.</span><span class="sxs-lookup"><span data-stu-id="9b3db-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="9b3db-179">Gebruik de knop **Selecteren** om de configuratie van de gegevensbron op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9b3db-179">Use the **Select** button to save the data source configuration.</span></span>


7. <span data-ttu-id="9b3db-180">De blade **Samenvatting** wordt vervolgens weergegeven om al uw instellingen te valideren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-180">The **Summary** blade then displays to validate all your settings.</span></span> <span data-ttu-id="9b3db-181">Hier kunt u de **Clustergrootte** wijzigen om het aantal servers in het cluster te wijzigen, en ook eventuele **Scriptacties** opgeven die u wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-181">Here you can change your **Cluster size** to modify the number of servers in your cluster and also specify any **Script actions** you want to run.</span></span> <span data-ttu-id="9b3db-182">Tenzij u zeker weet dat u een groter cluster nodig hebt, laat u het aantal worker-knooppunten ingesteld op het standaardaantal van `4`.</span><span class="sxs-lookup"><span data-stu-id="9b3db-182">Unless you know that you need a larger cluster, leave the number of worker nodes at the default of `4`.</span></span> <span data-ttu-id="9b3db-183">De geschatte kosten voor het cluster worden in de blade weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9b3db-183">The estimated cost of the cluster is shown within the blade.</span></span>

    ![clusteroverzicht](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="9b3db-185">Indien nodig, kunt u de grootte van het cluster later wijzigen via de portal (**Cluster** -> **Instellingen** -> **Cluster schalen**) om het aantal werkknooppunten te verlagen of te verhogen.</span><span class="sxs-lookup"><span data-stu-id="9b3db-185">If needed, you can resize your cluster later through the Portal (**Cluster** -> **Settings** -> **Scale Cluster**) to increase or decrease the number of worker nodes.</span></span>  <span data-ttu-id="9b3db-186">De grootte aanpassen kan nuttig zijn als u het cluster minder actief wilt maken wanneer het niet wordt gebruikt of om capaciteit toe te voegen wanneer dit nodig is voor grotere taken.</span><span class="sxs-lookup"><span data-stu-id="9b3db-186">This resizing can be useful for idling down the cluster when not in use, or for adding capacity to meet the needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="9b3db-187">Een aantal factoren waarmee u rekening moet houden wanneer u de grootte van het cluster, de gegevensknooppunten en het Edge-knooppunt wijzigt zijn:</span><span class="sxs-lookup"><span data-stu-id="9b3db-187">Some factors to keep in mind when sizing your cluster, the data nodes, and the edge node include:</span></span>  

   * <span data-ttu-id="9b3db-188">De prestaties van gedistribueerde R Server-analyses op Spark zijn gekoppeld aan het aantal worker-knooppunten wanneer er sprake is van grote hoeveelheden gegevens.</span><span class="sxs-lookup"><span data-stu-id="9b3db-188">The performance of distributed R Server analyses on Spark is proportional to the number of worker nodes when the data is large.</span></span>  

   * <span data-ttu-id="9b3db-189">De prestaties van R Server-analyses zijn lineair in de grootte van de gegevens die worden geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="9b3db-189">The performance of R Server analyses is linear in the size of data being analyzed.</span></span> <span data-ttu-id="9b3db-190">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9b3db-190">For example:</span></span>  

     * <span data-ttu-id="9b3db-191">Bij kleine tot gemiddelde hoeveelheden gegevens zijn de prestaties het beste wanneer de gegevens worden geanalyseerd in een lokale compute-context op het Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-191">For small to modest data, performance is best when analyzed in a local compute context on the edge node.</span></span>  <span data-ttu-id="9b3db-192">Zie Opties voor compute-context voor R Server op HDInsight voor meer informatie over de scenario's waarin de lokale compute-context en de Spark-compute-context het beste werken.</span><span class="sxs-lookup"><span data-stu-id="9b3db-192">For more information on the scenarios under which the local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="9b3db-193">Als u zich aanmeldt bij het Edge-knooppunt en uw R-script vervolgens uitvoert, worden alle functies behalve de ScaleR rx-functie <strong>lokaal</strong> uitgevoerd op het Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-193">If you log in to the edge node and run your R script, then all but the ScaleR rx-functions are executed <strong>locally</strong> on the edge node.</span></span> <span data-ttu-id="9b3db-194">Dus moeten het geheugen en het aantal kernen van het Edge-knooppunt dienovereenkomstig worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="9b3db-194">So the memory and number of cores of the edge node should be sized accordingly.</span></span> <span data-ttu-id="9b3db-195">Hetzelfde geldt dat als u R Server op HDI gebruikt als een externe compute-context vanaf uw laptop.</span><span class="sxs-lookup"><span data-stu-id="9b3db-195">The same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Blade Prijscategorieën voor knooppunten](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="9b3db-197">Gebruik de knop **Selecteren** om de prijsconfiguratie voor knooppunten op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9b3db-197">Use the **Select** button to save the node pricing configuration.</span></span>

   <span data-ttu-id="9b3db-198">Er is ook een koppeling **Sjabloon en parameters downloaden**.</span><span class="sxs-lookup"><span data-stu-id="9b3db-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="9b3db-199">Klik op deze koppeling om scripts weer te geven die kunnen worden gebruikt om automatisch een cluster te maken met de geselecteerde configuratie.</span><span class="sxs-lookup"><span data-stu-id="9b3db-199">Click on this link to display scripts that can be used to automate the creation of a cluster with the selected configuration.</span></span> <span data-ttu-id="9b3db-200">Deze scripts zijn ook toegankelijk in Azure Portal-vermelding voor uw cluster zodra het is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-200">These scripts are also available from the Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9b3db-201">Meestal duurt het genereren van het cluster ongeveer 20 minuten.</span><span class="sxs-lookup"><span data-stu-id="9b3db-201">It takes some time for the cluster to be created, usually around 20 minutes.</span></span> <span data-ttu-id="9b3db-202">Gebruik de tegel op het Startboard of de vermelding **Meldingen** aan de linkerkant van de pagina om dit proces te controleren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-202">Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-to-rstudio-server"></a><span data-ttu-id="9b3db-203">Verbinding maken met RStudio Server</span><span class="sxs-lookup"><span data-stu-id="9b3db-203">Connect to RStudio Server</span></span>

<span data-ttu-id="9b3db-204">Als u ervoor hebt gekozen om de RStudio Server Community-editie op te nemen in de installatie, hebt u op twee manieren toegang tot de aanmeldingspagina van RStudio.</span><span class="sxs-lookup"><span data-stu-id="9b3db-204">If you’ve chosen to include RStudio Server community edition in your installation, then you can access the RStudio login via two different methods.</span></span>

1. <span data-ttu-id="9b3db-205">Door naar de volgende URL te gaan (waarbij **CLUSTERNAAM** de naam is van het cluster dat u hebt gemaakt):</span><span class="sxs-lookup"><span data-stu-id="9b3db-205">Go to the following URL (where **CLUSTERNAME** is the name of the cluster you've created):</span></span>

    <span data-ttu-id="9b3db-206">https://**CLUSTERNAAM**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="9b3db-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="9b3db-207">Of door de vermelding voor het cluster te openen in Azure Portal. Selecteer de snelkoppeling naar het **R Server-dashboard** en selecteer vervolgens het **R Studio-dashboard**:</span><span class="sxs-lookup"><span data-stu-id="9b3db-207">Open the entry for your cluster in the Azure portal, select the **R Server Dashboards** quick link and then selecting the **R Studio Dashboard**:</span></span>

     ![Het R Studio-dashboard openen](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Het R Studio-dashboard openen](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="9b3db-210">Ongeacht welke methode u kiest, de eerste keer dat u zich aanmeldt moet u zich twee keer verifiëren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-210">Regardless of the method used, the first time you log in you need to authenticate twice.</span></span>  <span data-ttu-id="9b3db-211">Bij de eerste verificatie geeft u de *gebruikers-id* en het *wachtwoord* voor de beheerder op voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-211">At the first authentication, provide the *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="9b3db-212">Bij de tweede prompt geeft u de *gebruikers-id* en het *wachtwoord* voor SSH op.</span><span class="sxs-lookup"><span data-stu-id="9b3db-212">At the second prompt, provide the *SSH userid* and *password*.</span></span> <span data-ttu-id="9b3db-213">Bij alle volgende aanmeldingen zijn alleen de *gebruikers-id* en het *wachtwoord* voor SSH vereist.</span><span class="sxs-lookup"><span data-stu-id="9b3db-213">Subsequent log ins only require the *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-to-the-r-server-edge-node"></a><span data-ttu-id="9b3db-214">Verbinding maken met het R Server Edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="9b3db-214">Connect to the R Server edge node</span></span>

<span data-ttu-id="9b3db-215">Verbinding maken met het R Server Edge-knooppunt van het HDInsight-cluster met SSH met de opdracht:</span><span class="sxs-lookup"><span data-stu-id="9b3db-215">Connect to R Server edge node of the HDInsight cluster using SSH with the command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="9b3db-216">U kunt het `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`-adres vinden in Azure Portal door uw cluster te selecteren en vervolgens **Alle instellingen** -> **Apps en**  -> **RServer**.</span><span class="sxs-lookup"><span data-stu-id="9b3db-216">You can find the `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in the Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="9b3db-217">U ziet dan de SSH-eindpuntgegevens van het Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-217">This displays the SSH Endpoint information for the edge node.</span></span>
>
> ![Afbeelding van het SSH-eindpunt voor het Edge-knooppunt](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="9b3db-219">Als u een wachtwoord hebt gebruikt om uw SSH gebruikersaccount te beveiligen, wordt u gevraagd het wachtwoord in te voeren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-219">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="9b3db-220">Als u een openbare sleutel hebt gebruikt, moet u mogelijk de `-i`-parameter gebruiken om de overeenkomende persoonlijke sleutel op te geven.</span><span class="sxs-lookup"><span data-stu-id="9b3db-220">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="9b3db-221">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9b3db-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="9b3db-222">Zie voor meer informatie [Verbinding maken met HDInsight (Hadoop) via SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9b3db-222">For more information, see [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="9b3db-223">Zodra er verbinding is gemaakt, wordt er een prompt weergegeven die er ongeveer als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="9b3db-223">Once connected, you arrive at a prompt similar to the following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="9b3db-224">Meerdere gelijktijdige gebruikers inschakelen</span><span class="sxs-lookup"><span data-stu-id="9b3db-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="9b3db-225">U kunt meerdere gelijktijdige gebruikers inschakelen door meer gebruikers voor het Edge-knooppunt toe te voegen waarop de RStudio-community-versie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b3db-225">You can enable multiple concurrent users by adding more users for the edge node on which the RStudio community version runs.</span></span>

<span data-ttu-id="9b3db-226">Wanneer u een HDInsight-cluster maakt, moet u twee gebruikers opgeven, te weten een HTTP-gebruiker en een SSH-gebruiker:</span><span class="sxs-lookup"><span data-stu-id="9b3db-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Gelijktijdige gebruiker 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="9b3db-228">**Gebruikersnaam voor aanmelding cluster**: een HTTP-gebruiker voor verificatie via de HDInsight-gateway die wordt gebruikt voor het beveiligen van de HDInsight-clusters die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-228">**Cluster login username**: an HTTP user for authentication through the HDInsight gateway that is used to protect the HDInsight clusters you created.</span></span> <span data-ttu-id="9b3db-229">Deze HTTP-gebruiker wordt gebruikt voor toegang tot de Ambari-gebruikersinterface, de YARN-gebruikersinterface en andere gebruikersinterfaceonderdelen.</span><span class="sxs-lookup"><span data-stu-id="9b3db-229">This HTTP user is used to access the Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="9b3db-230">**Secure Shell (SSH)-gebruikersnaam**: een SSH-gebruiker voor toegang tot het cluster via Secure Shell.</span><span class="sxs-lookup"><span data-stu-id="9b3db-230">**Secure Shell (SSH) username**: an SSH user to access the cluster through secure shell.</span></span> <span data-ttu-id="9b3db-231">Deze gebruiker is een gebruiker in het Linux-systeem voor alle hoofdknooppunten, werkknooppunten en Edge-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="9b3db-231">This user is a user in the Linux system for all the head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="9b3db-232">U kunt Secure Shell gebruiken voor toegang tot alle knooppunten in een extern cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-232">So you can use secure shell to access any of the nodes in a remote cluster.</span></span>

<span data-ttu-id="9b3db-233">De R Studio Server Community-versie die wordt gebruikt in het clustertype Microsoft R Server op HDInsight accepteert alleen een Linux-gebruikersnaam en -wachtwoord als aanmeldingsmechanisme.</span><span class="sxs-lookup"><span data-stu-id="9b3db-233">The R Studio Server Community version used in the Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="9b3db-234">Doorgegeven tokens worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="9b3db-234">It does not support passing tokens.</span></span> <span data-ttu-id="9b3db-235">Dus als u een nieuw cluster hebt gemaakt en u wilt R Studio gebruiken om dat te openen, moet u zich twee keer aanmelden.</span><span class="sxs-lookup"><span data-stu-id="9b3db-235">So if you have created a new cluster and want to use R Studio to access it, you need to log in twice.</span></span>

- <span data-ttu-id="9b3db-236">Meld u eerst aan met de referenties van de HTTP-gebruiker via de Gateway van HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9b3db-236">First log in using the HTTP user credentials through the HDInsight Gateway:</span></span> 

    ![Gelijktijdige gebruiker 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="9b3db-238">Gebruik vervolgens de referenties van de SSH-gebruiker om u aan te melden bij RStudio:</span><span class="sxs-lookup"><span data-stu-id="9b3db-238">Then use the SSH user credentials to log in to RStudio:</span></span>
  
    ![Gelijktijdige gebruiker 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="9b3db-240">Op dit moment kan slechts één SSH gebruikersaccount worden gemaakt tijdens het inrichten van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="9b3db-241">Om meerdere gebruikers toegang tot Microsoft R Server op HDInsight-clusters te geven, moeten er extra gebruikers in het Linux-systeem worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-241">So to enable multiple users to access Microsoft R Server on HDInsight clusters, we need to create additional users in the Linux system.</span></span>

<span data-ttu-id="9b3db-242">Omdat RStudio Server Community op het Edge-knooppunt van het cluster wordt uitgevoerd, zijn er verschillende stappen:</span><span class="sxs-lookup"><span data-stu-id="9b3db-242">Because RStudio Server Community is running on the cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="9b3db-243">Gebruik de SSH-gebruiker om u aan te melden bij het Edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="9b3db-243">Use the created SSH user to log in to the edge node</span></span>
2. <span data-ttu-id="9b3db-244">Meer Linux-gebruikers toevoegen in Edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="9b3db-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="9b3db-245">RStudio Community-versie gebruiken met de gemaakte gebruiker</span><span class="sxs-lookup"><span data-stu-id="9b3db-245">Use RStudio Community version with the user created</span></span>

### <a name="step-1-use-the-created-ssh-user-to-log-in-to-the-edge-node"></a><span data-ttu-id="9b3db-246">Stap 1: de SSH-gebruiker gebruiken om u aan te melden bij het Edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="9b3db-246">Step 1: Use the created SSH user to log in to the edge node</span></span>

<span data-ttu-id="9b3db-247">Download een SSH-hulpprogramma (zoals Putty) en gebruik de bestaande SSH-gebruiker om u aan te melden.</span><span class="sxs-lookup"><span data-stu-id="9b3db-247">Download any SSH tool (such as Putty) and use the existing SSH user to log in.</span></span> <span data-ttu-id="9b3db-248">Volg de instructies in [Verbinding maken met HDInsight (Hadoop) via SSH](hdinsight-hadoop-linux-use-ssh-unix.md) voor toegang tot het Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-248">Then follow the instructions provided in [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) to access the edge node.</span></span> <span data-ttu-id="9b3db-249">Het adres van het Edge-knooppunt voor R Server op HDInsight-cluster is: *clusternaam-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="9b3db-249">The edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="9b3db-250">Stap 2: meer Linux-gebruikers toevoegen in Edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="9b3db-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="9b3db-251">Om een gebruiker toe te voegen aan het Edge-knooppunt, voert u de volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="9b3db-251">To add a user to the edge node, execute the commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="9b3db-252">De volgende items moeten worden geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="9b3db-252">You should see the following items returned:</span></span> 

![Gelijktijdige gebruiker 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="9b3db-254">Als u wordt gevraagd naar 'Huidig Kerberos-wachtwoord:', drukt u op **Enter** om dit te negeren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-254">When prompted for “Current Kerberos password:”, just press **Enter** to ignore it.</span></span> <span data-ttu-id="9b3db-255">De `-m`-optie in de opdracht `useradd` geeft aan dat het systeem een basismap voor de gebruiker maakt die vereist is voor RStudio Community-versie.</span><span class="sxs-lookup"><span data-stu-id="9b3db-255">The `-m` option in `useradd` command indicates that the system will create a home folder for the user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-the-user-created"></a><span data-ttu-id="9b3db-256">Stap 3: RStudio Community-versie gebruiken met de gemaakte gebruiker</span><span class="sxs-lookup"><span data-stu-id="9b3db-256">Step 3: Use RStudio Community version with the user created</span></span>

<span data-ttu-id="9b3db-257">Gebruik de gebruiker die is gemaakt voor het aanmelden bij RStudio:</span><span class="sxs-lookup"><span data-stu-id="9b3db-257">Use the user created to log in to RStudio:</span></span>

![Gelijktijdige gebruiker 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="9b3db-259">U ziet dat RStudio aangeeft dat u van de nieuwe gebruiker gebruikmaakt (hier bijvoorbeeld *sshuser6*) om u aan te melden in het cluster:</span><span class="sxs-lookup"><span data-stu-id="9b3db-259">Notice that RStudio indicates that you are using the new user (here, for example, *sshuser6*) to log in the cluster:</span></span> 

![Gelijktijdige gebruiker 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="9b3db-261">U kunt u ook tegelijkertijd vanuit een ander browservenster aanmelden met de oorspronkelijke referenties (dit is standaard *sshuser*).</span><span class="sxs-lookup"><span data-stu-id="9b3db-261">You can also log in using the original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="9b3db-262">U kunt een taak met scaleR-functies verzenden.</span><span class="sxs-lookup"><span data-stu-id="9b3db-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="9b3db-263">Hier volgt een voorbeeld van de opdrachten om een taak uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9b3db-263">Here is an example of the commands used to run a job:</span></span>

    # Set the HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data to the tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot to load the data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create the directory.
    rxHadoopMakeDir(inputDir)

    # Copy the data from source to input.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define the HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for the airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all the column names.
    varNames <- names(airlineColInfo)

    # Define the text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define the text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify the formula to use.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define the Spark compute context.
    mySparkCluster <- RxSpark()

    # Set the compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="9b3db-264">U ziet dat de taken die worden verzonden onder andere gebruikersnamen in de gebruikersinterface van YARN worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9b3db-264">Notice that the jobs submitted are under different user names in YARN UI:</span></span>

![Gelijktijdige gebruiker 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="9b3db-266">U ziet ook dat de zojuist toegevoegde gebruikers geen hoofdmapbevoegdheden in het Linux-systeem hebben, maar wel dezelfde toegang tot alle bestanden in de externe HDFS- en WASB-opslag hebben.</span><span class="sxs-lookup"><span data-stu-id="9b3db-266">Note also that the newly added users do not have root privileges in Linux system, but they do have the same access to all the files in the remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-the-r-console"></a><span data-ttu-id="9b3db-267">De R-console gebruiken</span><span class="sxs-lookup"><span data-stu-id="9b3db-267">Use the R console</span></span>

1. <span data-ttu-id="9b3db-268">Gebruik tijdens de SSH-sessie de volgende opdracht om de R-console te starten:</span><span class="sxs-lookup"><span data-stu-id="9b3db-268">From the SSH session, use the following command to start the R console:</span></span>  

        R

2. <span data-ttu-id="9b3db-269">De uitvoer ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="9b3db-269">You should see output similar to the following:</span></span>
    
    <span data-ttu-id="9b3db-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 The R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span><span class="sxs-lookup"><span data-stu-id="9b3db-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 The R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="9b3db-271">R is gratis software en wordt geleverd ZONDER ENIGE GARANTIE.</span><span class="sxs-lookup"><span data-stu-id="9b3db-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="9b3db-272">Het staat u vrij dit onder bepaalde voorwaarden verder te distribueren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-272">You are welcome to redistribute it under certain conditions.</span></span>
    <span data-ttu-id="9b3db-273">Typ 'license()' of 'licence()' voor distributie-informatie.</span><span class="sxs-lookup"><span data-stu-id="9b3db-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="9b3db-274">Ondersteuning van natuurlijke taal, maar uitgevoerd in een Engelse landinstelling</span><span class="sxs-lookup"><span data-stu-id="9b3db-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="9b3db-275">R is een samenwerkingsproject met veel inzenders.</span><span class="sxs-lookup"><span data-stu-id="9b3db-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="9b3db-276">Typ 'contributors()' voor meer informatie en 'citation()' voor het vermelden van R of R-pakketten in publicaties.</span><span class="sxs-lookup"><span data-stu-id="9b3db-276">Type 'contributors()' for more information and 'citation()' on how to cite R or R packages in publications.</span></span>

    <span data-ttu-id="9b3db-277">Typ 'demo()' voor enkele demo's, 'help()' voor de online help of 'help.start()' voor een HTML-browser-interface om u te helpen.</span><span class="sxs-lookup"><span data-stu-id="9b3db-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface to help.</span></span>
    <span data-ttu-id="9b3db-278">Typ 'q()' om R af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="9b3db-278">Type 'q()' to quit R.</span></span>

    <span data-ttu-id="9b3db-279">Microsoft R Server versie 8.0: een verbeterde distributie van R Microsoft-pakketten Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="9b3db-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="9b3db-280">Typ 'readme()' voor de release-opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="9b3db-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="9b3db-281">U kunt de R-code invoeren vanuit de `>`-prompt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-281">From the `>` prompt, you can enter R code.</span></span> <span data-ttu-id="9b3db-282">R-server bevat pakketten waarmee u eenvoudig kunt werken met Hadoop en gedistribueerde berekeningen kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-282">R server includes packages that allow you to easily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="9b3db-283">Gebruik bijvoorbeeld de volgende opdracht om de hoofdmap te bekijken van het standaardbestandssysteem voor het HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="9b3db-283">For example, use the following command to view the root of the default file system for the HDInsight cluster:</span></span>

    <span data-ttu-id="9b3db-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="9b3db-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="9b3db-285">U kunt ook de adressering in WASB-stijl gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9b3db-285">You can also use the WASB style addressing.</span></span>

    <span data-ttu-id="9b3db-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="9b3db-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="9b3db-287">R Server op HDI gebruiken vanaf een extern exemplaar van Microsoft R Server of Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="9b3db-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="9b3db-288">Het is mogelijk toegang in te stellen voor de HDI Hadoop Spark compute-context van een extern exemplaar van Microsoft R Server of Microsoft R Client dat wordt uitgevoerd op een desktop of laptop.</span><span class="sxs-lookup"><span data-stu-id="9b3db-288">It is possible to set up access to the HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="9b3db-289">Zie de subsectie **Using Microsoft R Server as a Hadoop Client** (Microsoft R Server als Hadoop-client gebruiken) in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md) (Een compute-context voor Spark maken).</span><span class="sxs-lookup"><span data-stu-id="9b3db-289">See **Using Microsoft R Server as a Hadoop Client** subsection in the [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="9b3db-290">Hiervoor moet u de volgende opties opgeven wanneer u de RxSpark-compute-context definieert op uw laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches en sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="9b3db-290">To do so, you need to specify the following options when defining the RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="9b3db-291">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9b3db-291">For example:</span></span>


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a><span data-ttu-id="9b3db-292">Een compute-context gebruiken</span><span class="sxs-lookup"><span data-stu-id="9b3db-292">Use a compute context</span></span>

<span data-ttu-id="9b3db-293">Met een compute-context kunt u bepalen of een berekening lokaal op het Edge-knooppunt wordt uitgevoerd of wordt gedistribueerd naar de verschillende knooppunten in het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-293">A compute context allows you to control whether computation is performed locally on the edge node or distributed across the nodes in the HDInsight cluster.</span></span>

1. <span data-ttu-id="9b3db-294">Gebruik vanuit RStudio Server of vanuit de R-console (tijdens een SSH-sessie) de volgende code om voorbeeldgegevens te laden in de standaardopslag voor HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9b3db-294">From RStudio Server or the R console (in an SSH session), use the following code to load example data into the default storage for HDInsight:</span></span>

        # Set the HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data to the tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot to load the data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make the directory
        rxHadoopMakeDir(inputDir)

        # Copy the data from source to input
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="9b3db-295">Hierna gaan we enkele gegevens maken en twee gegevensbronnen definiëren zodat we met de gegevens kunnen werken.</span><span class="sxs-lookup"><span data-stu-id="9b3db-295">Next, let's create some data info and define two data sources so that we can work with the data.</span></span>

        # Define the HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for the airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all the column names
        varNames <- names(airlineColInfo)

        # Define the text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define the text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula to use
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="9b3db-296">We gaan eerst een logistic regression voor de gegevens uitvoeren met behulp van de lokale compute-context.</span><span class="sxs-lookup"><span data-stu-id="9b3db-296">Let's run a logistic regression over the data using the local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="9b3db-297">De uitvoer die u nu ziet, eindigt met regels die er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="9b3db-297">You should see output that ends with lines similar to the following:</span></span>

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. <span data-ttu-id="9b3db-298">Hierna voeren we dezelfde logistic regression uit met behulp van Spark-context.</span><span class="sxs-lookup"><span data-stu-id="9b3db-298">Next, let's run the same logistic regression using the Spark context.</span></span> <span data-ttu-id="9b3db-299">De Spark-context distribueert de verwerking over alle werkknooppunten in het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-299">The Spark context distributes the processing over all the worker nodes in the HDInsight cluster.</span></span>

        # Define the Spark compute context
        mySparkCluster <- RxSpark()

        # Set the compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="9b3db-300">U kunt ook MapReduce gebruiken om de berekening te distribueren naar verschillende clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="9b3db-300">You can also use MapReduce to distribute computation across cluster nodes.</span></span> <span data-ttu-id="9b3db-301">Zie [Opties voor compute-context voor R Server op HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) voor meer informatie over compute-context.</span><span class="sxs-lookup"><span data-stu-id="9b3db-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-to-multiple-nodes"></a><span data-ttu-id="9b3db-302">R-code distribueren naar meerdere knooppunten</span><span class="sxs-lookup"><span data-stu-id="9b3db-302">Distribute R code to multiple nodes</span></span>

<span data-ttu-id="9b3db-303">Met R Server kunt u gemakkelijk bestaande R-code uitvoeren op verschillende knooppunten in het cluster door gebruik te maken van `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="9b3db-303">With R Server, you can easily take existing R code and run it across multiple nodes in the cluster by using `rxExec`.</span></span> <span data-ttu-id="9b3db-304">Deze functie is handig bij het uitvoeren van een parameteropschoning of van simulaties.</span><span class="sxs-lookup"><span data-stu-id="9b3db-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="9b3db-305">Hier volgt een voorbeeldcode van het gebruik van `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="9b3db-305">The following code is an example of how to use `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="9b3db-306">Als u nog steeds de Spark- of MapReduce-context gebruikt, wordt door deze opdracht de knooppuntnaam geretourneerd voor het werkknooppunt waarop de code `(Sys.info()["nodename"])` wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b3db-306">If you are still using the Spark or MapReduce context, this  command returns the nodename value for the worker nodes that the code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="9b3db-307">Bijvoorbeeld: bij een cluster van vier knooppunten verwacht u uitvoer die er ongeveer als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="9b3db-307">For example, on a four node cluster, you expect to receive output similar to the following:</span></span>

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="9b3db-308">Toegang tot gegevens in Hive en Parquet</span><span class="sxs-lookup"><span data-stu-id="9b3db-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="9b3db-309">Dankzij een functie die beschikbaar is in R Server 9.1, hebt u nu direct toegang tot de gegevens in Hive en Parquet, zodat deze kunnen worden gebruikt voor ScaleR-functies in de Spark-compute-context.</span><span class="sxs-lookup"><span data-stu-id="9b3db-309">A feature available in R Server 9.1 allows direct access to data in Hive and Parquet for use by ScaleR functions in the Spark compute context.</span></span> <span data-ttu-id="9b3db-310">Deze mogelijkheden zijn beschikbaar via nieuwe functies voor ScaleR-gegevensbronnen (genaamd RxHiveData en RxParquetData) die gebruikmaken van Spark SQL om gegevens rechtstreeks in Spark DataFrame te laden voor analyse met ScaleR.</span><span class="sxs-lookup"><span data-stu-id="9b3db-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL to load data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="9b3db-311">Hieronder ziet u code met voorbeeldcode bij het gebruik van de nieuwe functies:</span><span class="sxs-lookup"><span data-stu-id="9b3db-311">The following code provides some sample code on use of the new functions:</span></span>

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close the Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="9b3db-312">Raadpleeg de online-Help in R Server via de opdrachten `?RxHivedata` en `?RxParquetData` voor aanvullende informatie over het gebruik van deze nieuwe functies.</span><span class="sxs-lookup"><span data-stu-id="9b3db-312">For additional info on use of these new functions see the online help in R Server through use of the `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-the-edge-node"></a><span data-ttu-id="9b3db-313">Extra R-pakketten op het Edge-knooppunt installeren</span><span class="sxs-lookup"><span data-stu-id="9b3db-313">Install additional R packages on the edge node</span></span>

<span data-ttu-id="9b3db-314">Als u extra R-pakketten wilt installeren op het Edge-knooppunt, kunt u `install.packages()` rechtstreeks vanuit de R-console gebruiken wanneer u via SSH bent verbonden met het Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-314">If you would like to install additional R packages on the edge node, you can use `install.packages()` directly from within the R console when connected to the edge node through SSH.</span></span> <span data-ttu-id="9b3db-315">Als u echter R-pakketten wilt installeren op de worker-knooppunten van het cluster, moet u een scriptactie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9b3db-315">However, if you need to install R packages on the worker nodes of the cluster, you must use a Script Action.</span></span>

<span data-ttu-id="9b3db-316">Scriptacties zijn Bash-scripts die worden gebruikt om configuratiewijzigingen aan te brengen in het HDInsight-cluster of om extra software te installeren, zoals extra R-pakketten.</span><span class="sxs-lookup"><span data-stu-id="9b3db-316">Script Actions are Bash scripts that are used to make configuration changes to the HDInsight cluster or to install additional software, such as additional R packages.</span></span> <span data-ttu-id="9b3db-317">Gebruik de volgende stappen om extra pakketten te installeren met behulp van een scriptactie:</span><span class="sxs-lookup"><span data-stu-id="9b3db-317">To install additional packages using a Script Action, use the following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b3db-318">U kunt scriptacties alleen gebruiken om extra R-pakketten te installeren nadat het cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-318">Using Script Actions to install additional R packages can only be used after the cluster has been created.</span></span> <span data-ttu-id="9b3db-319">Gebruik deze procedure niet tijdens het maken van het cluster, omdat voor een script is vereist dat R Server volledig is geïnstalleerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9b3db-319">Do not use this procedure during cluster creation, as the script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="9b3db-320">Selecteer in [Azure Portal](https://portal.azure.com) het R Server op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3db-320">From the [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="9b3db-321">Selecteer op de blade **Instellingen** de optie **Scriptacties** en vervolgens **Nieuwe verzenden** om een nieuwe scriptactie te verzenden.</span><span class="sxs-lookup"><span data-stu-id="9b3db-321">From the **Settings** blade, select **Script Actions** and then **Submit New** to submit a new Script Action.</span></span>

   ![Afbeelding van de blade Scriptacties](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="9b3db-323">Geef op de blade **Scriptactie verzenden** de volgende informatie op:</span><span class="sxs-lookup"><span data-stu-id="9b3db-323">From the **Submit script action** blade, provide the following information:</span></span>

   * <span data-ttu-id="9b3db-324">**Naam**: een beschrijvende naam om dit script te identificeren</span><span class="sxs-lookup"><span data-stu-id="9b3db-324">**Name**: A friendly name to identify this script</span></span>

   * <span data-ttu-id="9b3db-325">**Bash-script-URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="9b3db-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="9b3db-326">**Head**: dit item moet zijn **uitgeschakeld**</span><span class="sxs-lookup"><span data-stu-id="9b3db-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="9b3db-327">**Worker**: dit item moet zijn **ingeschakeld**</span><span class="sxs-lookup"><span data-stu-id="9b3db-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="9b3db-328">**Edge nodes**: dit item moet zijn **uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="9b3db-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="9b3db-329">**Zookeeper**: dit item moet zijn **uitgeschakeld**</span><span class="sxs-lookup"><span data-stu-id="9b3db-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="9b3db-330">**Parameters**: de R-pakketten die moeten worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9b3db-330">**Parameters**: The R packages to be installed.</span></span> <span data-ttu-id="9b3db-331">Bijvoorbeeld: `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="9b3db-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="9b3db-332">**Deze scriptactie opnieuw laten uitvoeren...** : dit item moet zijn **ingeschakeld**</span><span class="sxs-lookup"><span data-stu-id="9b3db-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="9b3db-333">Standaard worden alle R-pakketten geïnstalleerd vanuit een momentopname van de Microsoft MRAN-opslagplaats, consistent met de R Server-versie die is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9b3db-333">By default, all R packages are installed from a snapshot of the Microsoft MRAN repository consistent with the version of R Server that has been installed.</span></span> <span data-ttu-id="9b3db-334">Als u nieuwere versies van pakketten wilt installeren, is er kans op incompatibiliteit.</span><span class="sxs-lookup"><span data-stu-id="9b3db-334">If you want to install newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="9b3db-335">Dit soort installatie is echter mogelijk door `useCRAN` op te geven als het eerste element van de pakketlijst, bijvoorbeeld `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="9b3db-335">However this kind of install is possible by specifying `useCRAN` as the first element of the package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="9b3db-336">Voor sommige R-pakketten zijn aanvullende Linux-systeembibliotheken vereist.</span><span class="sxs-lookup"><span data-stu-id="9b3db-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="9b3db-337">Voor het gemak hebben we de afhankelijkheden die nodig zijn voor de 100 meest populaire R-pakketten vooraf geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9b3db-337">For convenience, we have pre-installed the dependencies needed by the top 100 most popular R packages.</span></span> <span data-ttu-id="9b3db-338">Als voor de R-pakketten die u wilt installeren, meer bibliotheken zijn vereist, downloadt u het standaardscript dat hier wordt gebruikt, en voegt u stappen toe om de systeembibliotheken te installeren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-338">However, if the R package(s) you install require libraries beyond these then you must download the base script used here and add steps to install the system libraries.</span></span> <span data-ttu-id="9b3db-339">Vervolgens moet u het gewijzigde script uploaden naar een openbare blobcontainer in Azure-opslag en het gewijzigde script gebruiken om de pakketten te installeren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-339">You must then upload the modified script to a public blob container in Azure storage and use the modified script to install the packages.</span></span>
   >    <span data-ttu-id="9b3db-340">Zie [Ontwikkeling van scriptacties](hdinsight-hadoop-script-actions-linux.md) voor meer informatie over het ontwikkelen van scriptacties.</span><span class="sxs-lookup"><span data-stu-id="9b3db-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Een scriptactie toevoegen](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="9b3db-342">Selecteer **Maken** om het script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-342">Select **Create** to run the script.</span></span> <span data-ttu-id="9b3db-343">Nadat het script is voltooid, zijn de R-pakketten beschikbaar op alle werkknooppunten.</span><span class="sxs-lookup"><span data-stu-id="9b3db-343">Once the script completes, the R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="9b3db-344">Microsoft R Server-uitoefening gebruiken</span><span class="sxs-lookup"><span data-stu-id="9b3db-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="9b3db-345">Wanneer de gegevensmodellering is voltooid, kunt u het model uitvoeren om voorspellingen te maken.</span><span class="sxs-lookup"><span data-stu-id="9b3db-345">When your data modeling is complete, you can operationalize the model to make predictions.</span></span> <span data-ttu-id="9b3db-346">Voer de stappen hieronder uit om Microsoft R Server-uitoefening te configureren:</span><span class="sxs-lookup"><span data-stu-id="9b3db-346">To configure for Microsoft R Server operationalization, perform the following steps:</span></span>

<span data-ttu-id="9b3db-347">Ten eerste, SSH op het Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-347">First, ssh into the Edge node.</span></span> <span data-ttu-id="9b3db-348">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9b3db-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="9b3db-349">Nadat u SSH hebt gebruikt, wijzigt u de map voor de relevante versie en sudo in de dotnet-dll:</span><span class="sxs-lookup"><span data-stu-id="9b3db-349">After using ssh, change directory for the relevant version and sudo the dotnet dll:</span></span> 

- <span data-ttu-id="9b3db-350">Voor Microsoft R Server 9.1:</span><span class="sxs-lookup"><span data-stu-id="9b3db-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="9b3db-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="9b3db-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="9b3db-352">Voor Microsoft R Server 9.0:</span><span class="sxs-lookup"><span data-stu-id="9b3db-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="9b3db-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="9b3db-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="9b3db-354">Ga als volgt te werk om Microsoft R Server-uitoefening te configureren met een alles-in-één configuratie:</span><span class="sxs-lookup"><span data-stu-id="9b3db-354">To configure Microsoft R Server operationalization with a One-box configuration do the following:</span></span>

1. <span data-ttu-id="9b3db-355">'R-Server voor uitoefening configureren' selecteren</span><span class="sxs-lookup"><span data-stu-id="9b3db-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="9b3db-356">Selecteer A.</span><span class="sxs-lookup"><span data-stu-id="9b3db-356">Select “A.</span></span> <span data-ttu-id="9b3db-357">Alles-in-één (web- + rekenknooppunten)</span><span class="sxs-lookup"><span data-stu-id="9b3db-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="9b3db-358">Voer een wachtwoord in voor de gebruiker **beheerder**</span><span class="sxs-lookup"><span data-stu-id="9b3db-358">Enter a password for the **admin** user</span></span>

![De optie Alles-in-één](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="9b3db-360">Als optionele stap kunt u Diagnostische controles uitvoeren door als volgt een diagnostische test uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9b3db-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="9b3db-361">Selecteer 6.</span><span class="sxs-lookup"><span data-stu-id="9b3db-361">Select “6.</span></span> <span data-ttu-id="9b3db-362">Diagnostische tests uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9b3db-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="9b3db-363">Selecteer A.</span><span class="sxs-lookup"><span data-stu-id="9b3db-363">Select “A.</span></span> <span data-ttu-id="9b3db-364">Configuratie testen</span><span class="sxs-lookup"><span data-stu-id="9b3db-364">Test configuration”</span></span>
3. <span data-ttu-id="9b3db-365">Voer als gebruikersnaam Beheerder in en geef het wachtwoord uit de voorgaande configuratiestap op</span><span class="sxs-lookup"><span data-stu-id="9b3db-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="9b3db-366">Algehele status bevestigen = geslaagd</span><span class="sxs-lookup"><span data-stu-id="9b3db-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="9b3db-367">Sluit het beheerprogramma</span><span class="sxs-lookup"><span data-stu-id="9b3db-367">Exit the Admin Utility</span></span>
6. <span data-ttu-id="9b3db-368">Sluit SSH</span><span class="sxs-lookup"><span data-stu-id="9b3db-368">Exit SSH</span></span>

![De optie Diagnose voor](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="9b3db-370">**Lange vertragingen bij het gebruiken van webservice op Spark**</span><span class="sxs-lookup"><span data-stu-id="9b3db-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="9b3db-371">Als er lange vertragingen optreden bij het gebruiken van een webservice die is gemaakt met mrsdeploy-functies in een Spark-compute-context, moet u mogelijk een aantal ontbrekende mappen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9b3db-371">If you encounter long delays when trying to consume a web service created with mrsdeploy functions in a Spark compute context, you may need to add some missing folders.</span></span> <span data-ttu-id="9b3db-372">De Spark-toepassing is van een gebruiker met de naam *rserve2* wanneer de toepassing wordt aangeroepen vanuit een webservice met behulp van mrsdeploy-functies.</span><span class="sxs-lookup"><span data-stu-id="9b3db-372">The Spark application belongs to a user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="9b3db-373">Dit probleem omzeilen:</span><span class="sxs-lookup"><span data-stu-id="9b3db-373">To work around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="9b3db-374">In dit stadium is de configuratie voor uitoefening voltooid.</span><span class="sxs-lookup"><span data-stu-id="9b3db-374">At this stage, the configuration for Operationalization is complete.</span></span> <span data-ttu-id="9b3db-375">U kunt nu het pakket mrsdeploy op de RClient gebruiken om verbinding te maken met het Uitoefening op Edge-knooppunt en de bijbehorende functies gaan gebruiken, zoals [externe uitvoering](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) en [webservices](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="9b3db-375">Now you can use the ‘mrsdeploy’ package on your RClient to connect to the Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="9b3db-376">Afhankelijk van of het cluster is ingesteld in een virtueel netwerk of niet, moet u mogelijk forward tunneling via SSH-aanmelding instellen voor de poort.</span><span class="sxs-lookup"><span data-stu-id="9b3db-376">Depending on whether your cluster is set up on a virtual network or not, you may need to set up port forward tunneling through SSH login.</span></span> <span data-ttu-id="9b3db-377">In de volgende secties wordt uitgelegd hoe u deze tunnel instelt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-377">The following sections explain how to set up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="9b3db-378">RServer-cluster in een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="9b3db-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="9b3db-379">Zorg ervoor dat u verkeer via poort 12800 naar het Edge-knooppunt toestaat.</span><span class="sxs-lookup"><span data-stu-id="9b3db-379">Make sure you allow traffic through port 12800 to the edge node.</span></span> <span data-ttu-id="9b3db-380">Op deze manier kunt u het Edge-knooppunt gebruiken om verbinding te maken met de functie Uitoefening.</span><span class="sxs-lookup"><span data-stu-id="9b3db-380">That way, you can use the edge node to connect to the Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="9b3db-381">Als de `remoteLogin()` geen verbinding kan maken met het Edge-knooppunt maar als u wel verbinding hebt via SSH, moet u controleren of de regel op basis waarvan verkeer via poort 12800 is toegestaan, juist is ingesteld of niet.</span><span class="sxs-lookup"><span data-stu-id="9b3db-381">If the `remoteLogin()` cannot connect to the edge node, but you can SSH to the edge node, then you need to verify whether the rule to allow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="9b3db-382">Als dit probleem zich blijft voordoen, kunt u een tijdelijke oplossing gebruiken door forward tunneling via SSH in te stellen voor de poort.</span><span class="sxs-lookup"><span data-stu-id="9b3db-382">If you continue to face the issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="9b3db-383">Raadpleeg de volgende sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9b3db-383">For instructions, see the following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="9b3db-384">RServer-cluster is niet ingesteld in het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="9b3db-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="9b3db-385">Als het cluster niet is ingesteld in het virtuele netwerk vnet of als u problemen ondervindt met de connectiviteit via dit netwerk, kunt u forward tunneling via SSH instellen voor de poort:</span><span class="sxs-lookup"><span data-stu-id="9b3db-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="9b3db-386">U kunt dit ook instellen op Putty.</span><span class="sxs-lookup"><span data-stu-id="9b3db-386">On Putty, you can set it up as well.</span></span>

![Putty SSH-verbinding](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="9b3db-388">Zodra de SSH-sessie actief is, wordt het verkeer bij poort 12800 op uw computer via de SSH-sessie doorgestuurd naar poort 12800 van het Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-388">Once your SSH session is active, the traffic from your machine’s port 12800 is forwarded to the edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="9b3db-389">Zorg ervoor dat u `127.0.0.1:12800` gebruikt in de `remoteLogin()`-methode.</span><span class="sxs-lookup"><span data-stu-id="9b3db-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="9b3db-390">Hierdoor wordt u aangemeld bij de uitoefening van het Edge-knooppunt via doorsturen naar de poort.</span><span class="sxs-lookup"><span data-stu-id="9b3db-390">This logs in to the edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-to-scale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="9b3db-391">Hoe werkt het schalen van rekenknooppunten in Microsoft R Server-uitoefening op worker-knooppunten in HDInsight?</span><span class="sxs-lookup"><span data-stu-id="9b3db-391">How to scale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-the-worker-nodes"></a><span data-ttu-id="9b3db-392">De worker-knooppunten uit bedrijf nemen</span><span class="sxs-lookup"><span data-stu-id="9b3db-392">Decommission the worker node(s)</span></span>

<span data-ttu-id="9b3db-393">Microsoft R Server wordt momenteel niet beheerd via Yarn.</span><span class="sxs-lookup"><span data-stu-id="9b3db-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="9b3db-394">Als de werkknooppunten niet uit bedrijf worden genomen, werkt de resourcemanager Yarn niet zoals verwacht, omdat in dit geval niet wordt gedetecteerd welke resources de server bevat.</span><span class="sxs-lookup"><span data-stu-id="9b3db-394">If the worker nodes are not decommissioned, the Yarn Resource Manager will not work as expected because it will not be aware of the resources being taken up by the server.</span></span> <span data-ttu-id="9b3db-395">Om deze sitatie te voorkomen raden we u aan de werkknooppunten uit bedrijf te nemen voordat u de rekenknooppunten uitschaalt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-395">In order to avoid this situation, we recommend decommissioning the worker nodes before you scale out the compute nodes.</span></span>

<span data-ttu-id="9b3db-396">Stappen voor het uit bedrijf nemen van worker-knooppunten:</span><span class="sxs-lookup"><span data-stu-id="9b3db-396">Steps to decommissioning worker nodes:</span></span>

* <span data-ttu-id="9b3db-397">Meld u bij de Ambari-console van het HDI-cluster en klik op het tabblad Hosts</span><span class="sxs-lookup"><span data-stu-id="9b3db-397">Log in to HDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="9b3db-398">Selecteer de worker-knooppunten (die uit bedrijf moeten worden genomen), klik op Acties > Geselecteerd hosts > Hosts, en klik op Onderhoudsmodus inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9b3db-398">Select worker nodes (to be decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="9b3db-399">In de volgende afbeelding zijn bijvoorbeeld wk3 en wk4 geselecteerd om uit bedrijf te worden genomen.</span><span class="sxs-lookup"><span data-stu-id="9b3db-399">For example, in the following image we have selected wn3 and wn4 to decommission.</span></span>  

   ![worker-knooppunten uit bedrijf nemen](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="9b3db-401">Selecteer **Acties** > **Geselecteerde hosts** > **Datanodes** > klik op **Uit bedrijf nemen**</span><span class="sxs-lookup"><span data-stu-id="9b3db-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="9b3db-402">Selecteer **Acties** > **Geselecteerde hosts** > **NodeManagers** > klik op **Uit bedrijf nemen**</span><span class="sxs-lookup"><span data-stu-id="9b3db-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="9b3db-403">Selecteer **Acties** > **Geselecteerde hosts** > **Datanodes** > klik op **Stoppen**</span><span class="sxs-lookup"><span data-stu-id="9b3db-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="9b3db-404">Selecteer **Acties** > **Geselecteerde hosts** > **NodeManagers** > klik op **Stoppen**</span><span class="sxs-lookup"><span data-stu-id="9b3db-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="9b3db-405">Selecteer **Acties** > **Geselecteerde hosts** > **Hosts** > klik op **Alle onderdelen stoppen**</span><span class="sxs-lookup"><span data-stu-id="9b3db-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="9b3db-406">Hef de selectie van de werkknooppunten op en selecteer de hoofdknooppunten</span><span class="sxs-lookup"><span data-stu-id="9b3db-406">Unselect the worker nodes and select the head nodes</span></span>
* <span data-ttu-id="9b3db-407">Selecteer **Acties** > **Geselecteerde hosts** > **Hosts** > **Alle onderdelen opnieuw starten**</span><span class="sxs-lookup"><span data-stu-id="9b3db-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="9b3db-408">Rekenknooppunten configureren op elk uit bedrijf genomen worker-knooppunt</span><span class="sxs-lookup"><span data-stu-id="9b3db-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="9b3db-409">SSH op elk uit bedrijf genomen werkknooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="9b3db-410">Voer het beheerprogramma uit met behulp van `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span><span class="sxs-lookup"><span data-stu-id="9b3db-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="9b3db-411">Voer '1' in om de optie 'R-Server voor uitoefening configureren' te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-411">Enter "1" to select option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="9b3db-412">Voer C in om optie C.</span><span class="sxs-lookup"><span data-stu-id="9b3db-412">Enter "c" to select option "C.</span></span> <span data-ttu-id="9b3db-413">Rekenknooppunt te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9b3db-413">Compute node".</span></span> <span data-ttu-id="9b3db-414">Hiermee configureert u het rekenknooppunt op het werkknooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-414">This configures the compute node on the worker node.</span></span>
5. <span data-ttu-id="9b3db-415">Sluit het beheerprogramma.</span><span class="sxs-lookup"><span data-stu-id="9b3db-415">Exit the Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="9b3db-416">Details van rekenknooppunten toevoegen op het webknooppunt</span><span class="sxs-lookup"><span data-stu-id="9b3db-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="9b3db-417">Zodra alle uit bedrijf genomen werkknooppunten zijn geconfigureerd om het rekenknooppunt uit te voeren, keert u terug naar het Edge-knooppunt en voegt u de IP-adressen van de uit bedrijf genomen werkknooppunten toe in de configuratie van het Microsoft R Server-webknooppunt:</span><span class="sxs-lookup"><span data-stu-id="9b3db-417">Once all decommissioned worker nodes have been configured to run compute node, come back on the edge node and add decommissioned worker nodes' IP addresses in the Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="9b3db-418">SSH op het Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3db-418">SSH into the edge node.</span></span>
* <span data-ttu-id="9b3db-419">Voer `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json` uit.</span><span class="sxs-lookup"><span data-stu-id="9b3db-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="9b3db-420">Ga naar de sectie URI's en voeg het IP-adres en de poortgegevens van het worker-knooppunt toe.</span><span class="sxs-lookup"><span data-stu-id="9b3db-420">Look for the "URIs" section, and add worker node's IP and port details.</span></span>

    ![opdrachtregel worker-knooppunten uit bedrijf nemen](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="9b3db-422">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="9b3db-422">Troubleshoot</span></span>

<span data-ttu-id="9b3db-423">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="9b3db-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9b3db-424">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b3db-424">Next steps</span></span>

<span data-ttu-id="9b3db-425">Nu zou u moeten weten hoe u een nieuw HDInsight-cluster maakt met de R Server en de basisbeginselen van het gebruik van de R-console van een SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="9b3db-425">Now you should understand how to create a new HDInsight cluster that includes the R Server and the basics of using the R console from an SSH session.</span></span> <span data-ttu-id="9b3db-426">In de volgende onderwerpen worden andere manieren beschreven om R Server op HDInsight te beheren en ermee te werken:</span><span class="sxs-lookup"><span data-stu-id="9b3db-426">The following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="9b3db-427">RStudio Server toevoegen aan HDInsight (indien niet geïnstalleerd tijdens het maken van het cluster)</span><span class="sxs-lookup"><span data-stu-id="9b3db-427">Add RStudio Server to HDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="9b3db-428">Opties voor compute-context voor R Server op HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b3db-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="9b3db-429">Opties voor Azure-opslag voor R Server op HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b3db-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
