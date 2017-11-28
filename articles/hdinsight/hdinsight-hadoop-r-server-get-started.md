---
title: aaaGet de slag met R Server op een HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toocreate een Apache Spark in HDInsight-cluster met R Server en het verzenden van een R-script op Hallo-cluster.
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
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="7b927-103">Aan de slag met R Server op HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b927-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="7b927-104">HDInsight bevat een R Server optie toobe geïntegreerd in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7b927-104">HDInsight includes an R Server option toobe integrated into your HDInsight cluster.</span></span> <span data-ttu-id="7b927-105">Deze optie kunt scripts R toouse Spark en MapReduce toorun gedistribueerd berekeningen.</span><span class="sxs-lookup"><span data-stu-id="7b927-105">This option allows R scripts toouse Spark and MapReduce toorun distributed computations.</span></span> <span data-ttu-id="7b927-106">In dit document leert u hoe toocreate een R Server op HDInsight-cluster en klik vervolgens op uitvoeren een R-script dat wordt gedemonstreerd met behulp van Spark voor gedistribueerde R-berekeningen.</span><span class="sxs-lookup"><span data-stu-id="7b927-106">In this document, you learn how toocreate an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7b927-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b927-107">Prerequisites</span></span>

* <span data-ttu-id="7b927-108">**Een Azure-abonnement**: voordat u aan deze zelfstudie begint, moet u beschikken over een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7b927-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="7b927-109">Ga toohello artikel [gratis proefversie van Microsoft Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7b927-109">Go toohello article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="7b927-110">**Een client Secure Shell (SSH)**: een SSH-client wordt gebruikt tooremotely verbinding toohello HDInsight-cluster en uitvoeren van opdrachten rechtstreeks op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="7b927-110">**A Secure Shell (SSH) client**: An SSH client is used tooremotely connect toohello HDInsight cluster and run commands directly on hello cluster.</span></span> <span data-ttu-id="7b927-111">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7b927-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="7b927-112">**SSH-sleutels (optioneel)**: U kunt beveiligen Hallo SSH-account gebruikt tooconnect toohello cluster met een wachtwoord of een openbare sleutel.</span><span class="sxs-lookup"><span data-stu-id="7b927-112">**SSH keys (optional)**: You can secure hello SSH account used tooconnect toohello cluster using either a password or a public key.</span></span> <span data-ttu-id="7b927-113">Met een wachtwoord is eenvoudiger en kunt u tooget gestart zonder toocreate een openbaar/persoonlijk sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="7b927-113">Using a password is easier, and allows you tooget started without having toocreate a public/private key pair.</span></span> <span data-ttu-id="7b927-114">Het gebruik van een sleutel is echter veiliger.</span><span class="sxs-lookup"><span data-stu-id="7b927-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="7b927-115">Hallo stappen in dit document wordt ervan uitgegaan dat u van een wachtwoord gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="7b927-115">hello steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="7b927-116">Automatisch een cluster maken</span><span class="sxs-lookup"><span data-stu-id="7b927-116">Automated cluster creation</span></span>

<span data-ttu-id="7b927-117">U kunt maken van HDInsight R Servers via Azure Resource Manager-sjablonen, Hallo SDK en ook PowerShell Hallo automatiseren.</span><span class="sxs-lookup"><span data-stu-id="7b927-117">You can automate hello creation of HDInsight R Servers using Azure Resource Manager templates, hello SDK, and also PowerShell.</span></span>

* <span data-ttu-id="7b927-118">Zie een R Server met een Azure Resource Management-sjabloon toocreate [een R server HDInsight-cluster implementeren](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="7b927-118">toocreate an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="7b927-119">Zie toocreate een R Server met behulp van de .NET SDK Hallo [maken op basis van Linux-clusters in HDInsight met behulp van Hallo .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7b927-119">toocreate an R Server using hello .NET SDK, see [create Linux-based clusters in HDInsight using hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="7b927-120">toodeploy R Server met behulp van powershell, Zie Hallo-artikel over [een R Server maken in HDInsight met PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7b927-120">toodeploy R Server using powershell, see hello article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a><span data-ttu-id="7b927-121">Hallo-cluster met behulp van hello Azure-portal maken</span><span class="sxs-lookup"><span data-stu-id="7b927-121">Create hello cluster using hello Azure portal</span></span>

1. <span data-ttu-id="7b927-122">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b927-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7b927-123">Selecteer **NIEUW** -> **Intelligence en analyse**, -> **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7b927-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Afbeelding van het maken van een nieuw cluster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="7b927-125">In Hallo **snelle invoer** -ervaring, voer een naam voor de cluster Hallo in Hallo **clusternaam** veld.</span><span class="sxs-lookup"><span data-stu-id="7b927-125">In hello **Quick create** experience, enter a name for hello cluster in hello **Cluster Name** field.</span></span> <span data-ttu-id="7b927-126">Als u meerdere Azure-abonnementen hebt, gebruikt u Hallo **abonnement** vermelding tooselect Hallo een gewenste toouse.</span><span class="sxs-lookup"><span data-stu-id="7b927-126">If you have multiple Azure subscriptions, use hello **Subscription** entry tooselect hello one you want toouse.</span></span>

    ![Clusternaam en geselecteerde abonnementen](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="7b927-128">Selecteer **type Cluster** tooopen hello **clusterconfiguratie** blade.</span><span class="sxs-lookup"><span data-stu-id="7b927-128">Select **Cluster type** tooopen hello **Cluster configuration** blade.</span></span> <span data-ttu-id="7b927-129">Op Hallo **clusterconfiguratie** blade Selecteer Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="7b927-129">On hello **Cluster Configuration** blade, select hello following options:</span></span>

    * <span data-ttu-id="7b927-130">**Clustertype**: R Server</span><span class="sxs-lookup"><span data-stu-id="7b927-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="7b927-131">**Versie**: Selecteer Hallo-versie van tooinstall R Server op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="7b927-131">**Version**: select hello version of R Server tooinstall on hello cluster.</span></span> <span data-ttu-id="7b927-132">Hallo-versie die momenteel beschikbaar is ***R Server 9.1 (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="7b927-132">hello version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="7b927-133">Releaseopmerkingen voor Hallo beschikbare versies van R Server beschikbaar zijn [hier](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="7b927-133">Release notes for hello available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="7b927-134">**R Studio community edition voor op R Server**: deze browser gebaseerde IDE wordt standaard geïnstalleerd op Hallo edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7b927-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on hello edge node.</span></span> <span data-ttu-id="7b927-135">Als u liever toonot hebt geïnstalleerd en schakel het selectievakje Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b927-135">If you would prefer toonot have it installed, then uncheck hello check box.</span></span> <span data-ttu-id="7b927-136">Als u ervoor kiest toohave deze geïnstalleerd, Hallo-URL voor het openen van Hallo RStudio Server-aanmelding is gevonden in een portaltoepassing blade voor uw cluster zodra deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b927-136">If you choose toohave it installed, hello URL for accessing hello RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="7b927-137">Andere opties van Hallo laten op het Hallo-standaardwaarden en hello gebruiken **Selecteer** knoptype toosave Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="7b927-137">Leave hello other options at hello default values and use hello **Select** button toosave hello cluster type.</span></span>

        ![Schermafbeelding van de blade Clustertype](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="7b927-139">Voer een **gebruikersnaam** en **wachtwoord** voor aanmelden bij het cluster in.</span><span class="sxs-lookup"><span data-stu-id="7b927-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="7b927-140">Geef een **SSH-gebruikersnaam** op.</span><span class="sxs-lookup"><span data-stu-id="7b927-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="7b927-141">SSH is gebruikte tooremotely verbinden toohello cluster via een **Secure Shell (SSH)** client.</span><span class="sxs-lookup"><span data-stu-id="7b927-141">SSH is used tooremotely connect toohello cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="7b927-142">U kunt Hallo SSH-gebruiker opgeven in dit dialoogvenster of nadat het Hallo-cluster is gemaakt (in Hallo tabblad van de configuratie voor Hallo cluster).</span><span class="sxs-lookup"><span data-stu-id="7b927-142">You can either specify hello SSH user in this dialog or after hello cluster has been created (in hello Configuration tab for hello cluster).</span></span> <span data-ttu-id="7b927-143">R Server geconfigureerde tooexpect is een **SSH-gebruikersnaam** van 'remoteuser'.</span><span class="sxs-lookup"><span data-stu-id="7b927-143">R Server is configured tooexpect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="7b927-144">**Als u een andere gebruikersnaam gebruikt, moet u een extra stap uitvoeren nadat Hallo-cluster is gemaakt.**</span><span class="sxs-lookup"><span data-stu-id="7b927-144">**If you use a different username, you must perform an additional step after hello cluster is created.**</span></span>

    <span data-ttu-id="7b927-145">Laat de eigenschap Hallo selectievakje is ingeschakeld voor **gebruik hetzelfde wachtwoord als cluster aanmelding** toouse **wachtwoord** als het Hallo verificatie type tenzij u liever gebruik van een openbare sleutel.</span><span class="sxs-lookup"><span data-stu-id="7b927-145">Leave hello box checked for **Use same password as cluster login** toouse **PASSWORD** as hello authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="7b927-146">U moet een openbaar/persoonlijk sleutelpaar tooaccess R Server op Hallo-cluster via een externe client als bijvoorbeeld RTVS, RStudio of een ander bureaublad IDE.</span><span class="sxs-lookup"><span data-stu-id="7b927-146">You need a public/private key pair tooaccess R Server on hello cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="7b927-147">Als u Hallo RStudio Server community edition installeert, moet u een SSH-wachtwoord toochoose.</span><span class="sxs-lookup"><span data-stu-id="7b927-147">If you install hello RStudio Server community edition, you need toochoose an SSH password.</span></span>     

    <span data-ttu-id="7b927-148">toocreate en gebruik een openbaar/persoonlijk sleutelpaar, schakel het selectievakje **gebruik hetzelfde wachtwoord als cluster aanmelding** en selecteer vervolgens **openbare sleutel** en gaat u als volgt.</span><span class="sxs-lookup"><span data-stu-id="7b927-148">toocreate and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="7b927-149">Bij deze instructies wordt ervan uitgegaan dat u Cygwin SSH-keygen of iets gelijkwaardigs hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="7b927-150">Een openbaar/persoonlijk sleutelpaar genereren via de opdrachtprompt Hallo op uw laptop:</span><span class="sxs-lookup"><span data-stu-id="7b927-150">Generate a public/private key pair from hello command prompt on your laptop:</span></span>

        <span data-ttu-id="7b927-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="7b927-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="7b927-152">Volg Hallo vragen tooname een sleutelbestand en voer vervolgens een wachtwoordzin voor extra beveiliging.</span><span class="sxs-lookup"><span data-stu-id="7b927-152">Follow hello prompt tooname a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="7b927-153">Uw scherm ziet er ongeveer als Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b927-153">Your screen should look something like hello following image:</span></span>

        ![SSH-opdrachtregel in Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="7b927-155">Deze opdracht maakt u een bestand met een persoonlijke sleutel en een bestand met een openbare sleutel onder de naam < persoonlijke sleutel bestandsnaam > .pub hello, bijvoorbeeld furiosa en furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="7b927-155">This command creates a private key file and a public key file under hello name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![SSH-dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="7b927-157">Geef vervolgens Hallo bestand openbare sleutel (&#42;. pub) wanneer toewijzen HDI cluster referenties en ten slotte bevestigt de resourcegroep en de regio en selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="7b927-157">Then specify hello public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Blade Referenties](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="7b927-159">Machtigingen op Hallo persoonlijke sleutelbestand op uw laptop wijzigen:</span><span class="sxs-lookup"><span data-stu-id="7b927-159">Change permissions on hello private keyfile on your laptop:</span></span>

        <span data-ttu-id="7b927-160">chmod 600 <bestandsnaam-persoonlijke-sleutel></span><span class="sxs-lookup"><span data-stu-id="7b927-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="7b927-161">Hallo persoonlijke sleutelbestand met SSH gebruiken voor externe aanmelding:</span><span class="sxs-lookup"><span data-stu-id="7b927-161">Use hello private key file with SSH for remote login:</span></span>

        <span data-ttu-id="7b927-162">ssh – i <bestandsnaam-persoonlijke-sleutel> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="7b927-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="7b927-163">Of als onderdeel Hallo definitie van uw Hadoop Spark compute-context voor R Server op Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="7b927-163">Or, as part hello definition of your Hadoop Spark compute context for R Server on hello client.</span></span> <span data-ttu-id="7b927-164">Zie Hallo **met behulp van Microsoft R Server als een Hadoop Client** subsectie [maken van een Compute-Context voor Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span><span class="sxs-lookup"><span data-stu-id="7b927-164">See hello **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="7b927-165">Hallo snelle invoer overgangen die u toohello **opslag** blade tooselect hello opslagaccount instellingen toobe gebruikt voor de primaire locatie Hallo Hallo HDFS bestandssysteem door Hallo cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7b927-165">hello quick create transitions you toohello **Storage** blade tooselect hello storage account settings toobe used for hello primary location of hello HDFS file system used by hello cluster.</span></span> <span data-ttu-id="7b927-166">Selecteer een nieuw of een bestaand Azure Storage-account of een bestaand Data Lake Storage-account.</span><span class="sxs-lookup"><span data-stu-id="7b927-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="7b927-167">Als u een Azure Storage-account selecteert, een bestaand opslagaccount is geselecteerd door te kiezen **Selecteer een opslagaccount** en het Hallo relevante account selecteren.</span><span class="sxs-lookup"><span data-stu-id="7b927-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting hello relevant account.</span></span> <span data-ttu-id="7b927-168">Een nieuwe account maken met Hallo **nieuw** koppeling in Hallo **Selecteer een opslagaccount** sectie.</span><span class="sxs-lookup"><span data-stu-id="7b927-168">Create a new account using hello **Create New** link in hello **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7b927-169">Als u selecteert **nieuw** u moet een naam voor het nieuwe opslagaccount Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="7b927-169">If you select **New** you must enter a name for hello new storage account.</span></span> <span data-ttu-id="7b927-170">Een groen vinkje weergegeven als de naam van de Hallo is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-170">A green check appears if hello name is accepted.</span></span>

      <span data-ttu-id="7b927-171">Hallo **standaard Container** standaardwaarden toohello naam van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="7b927-171">hello **Default Container** defaults toohello name of hello cluster.</span></span> <span data-ttu-id="7b927-172">Laat deze standaardinstelling Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="7b927-172">Leave this default as hello value.</span></span>

      <span data-ttu-id="7b927-173">Als u een nieuwe opslagoptie account hebt geselecteerd een prompt tooselect **locatie** is gegeven tooselect welke regio toocreate Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="7b927-173">If a new storage account option was selected a prompt tooselect **Location** is given tooselect which region toocreate hello storage account.</span></span>  

         ![Blade Gegevensbron](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="7b927-175">Locatie van de HDInsight-cluster Hallo HALLO hallo locatie voor Hallo standaardgegevensbron selecteren ook worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7b927-175">Selecting hello location for hello default data source  also sets hello location of hello HDInsight cluster.</span></span> <span data-ttu-id="7b927-176">Hallo-cluster en het standaard gegevensbron moet Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="7b927-176">hello cluster and default data source must be in hello same region.</span></span>

    - <span data-ttu-id="7b927-177">Als u een bestaande Data Lake Store toouse wilt, selecteer Hallo ADLS storage account toouse en Hallo-cluster toevoegen *toevoegen* identiteit tooyour cluster tooallow toegang tot toohello store.</span><span class="sxs-lookup"><span data-stu-id="7b927-177">If you want toouse an existing Data Lake Store, then select hello ADLS storage account toouse and add hello cluster *ADD* identity tooyour cluster tooallow access toohello store.</span></span> <span data-ttu-id="7b927-178">Raadpleeg [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal) (HDInsight-cluster met Data Lake Store maken met behulp van Azure Portal) voor meer informatie over dit proces.</span><span class="sxs-lookup"><span data-stu-id="7b927-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="7b927-179">Gebruik Hallo **Selecteer** knop toosave Hallo data source-configuratie.</span><span class="sxs-lookup"><span data-stu-id="7b927-179">Use hello **Select** button toosave hello data source configuration.</span></span>


7. <span data-ttu-id="7b927-180">Hallo **samenvatting** blade geeft toovalidate alle instellingen.</span><span class="sxs-lookup"><span data-stu-id="7b927-180">hello **Summary** blade then displays toovalidate all your settings.</span></span> <span data-ttu-id="7b927-181">Hier kunt u uw **clustergrootte** toomodify Hallo aantal servers in het cluster en geeft u ook een **acties Script** gewenste toorun.</span><span class="sxs-lookup"><span data-stu-id="7b927-181">Here you can change your **Cluster size** toomodify hello number of servers in your cluster and also specify any **Script actions** you want toorun.</span></span> <span data-ttu-id="7b927-182">Tenzij u zeker weet dat u een groter cluster nodig hebt, laat u Hallo aantal worker-knooppunten op Hallo standaardwaarde van `4`.</span><span class="sxs-lookup"><span data-stu-id="7b927-182">Unless you know that you need a larger cluster, leave hello number of worker nodes at hello default of `4`.</span></span> <span data-ttu-id="7b927-183">Hallo geschatte kosten van het Hallo-cluster wordt weergegeven in de blade Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b927-183">hello estimated cost of hello cluster is shown within hello blade.</span></span>

    ![clusteroverzicht](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="7b927-185">Indien nodig, u kunt de grootte van uw cluster later via Hallo Portal (**Cluster** -> **instellingen** -> **Scale Cluster**) tooincrease of het aantal worker-knooppunten Hallo verkleinen.</span><span class="sxs-lookup"><span data-stu-id="7b927-185">If needed, you can resize your cluster later through hello Portal (**Cluster** -> **Settings** -> **Scale Cluster**) tooincrease or decrease hello number of worker nodes.</span></span>  <span data-ttu-id="7b927-186">Deze grootte is handig voor stationair omlaag Hallo cluster als deze niet in gebruik of voor het toevoegen van toomeet Hallo capaciteitsbehoeften van grote taken.</span><span class="sxs-lookup"><span data-stu-id="7b927-186">This resizing can be useful for idling down hello cluster when not in use, or for adding capacity toomeet hello needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="7b927-187">Een aantal factoren tookeep rekening moet houden bij het formaat van uw cluster, Hallo gegevensknooppunten en Hallo edge-knooppunt zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="7b927-187">Some factors tookeep in mind when sizing your cluster, hello data nodes, and hello edge node include:</span></span>  

   * <span data-ttu-id="7b927-188">Hallo-prestaties van gedistribueerde R Server analyses op Spark is evenredig toohello aantal worker-knooppunten wanneer Hallo gegevens groot is.</span><span class="sxs-lookup"><span data-stu-id="7b927-188">hello performance of distributed R Server analyses on Spark is proportional toohello number of worker nodes when hello data is large.</span></span>  

   * <span data-ttu-id="7b927-189">Hallo-prestaties van R Server analyses is lineaire Hallo omvang van gegevens wordt geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-189">hello performance of R Server analyses is linear in hello size of data being analyzed.</span></span> <span data-ttu-id="7b927-190">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7b927-190">For example:</span></span>  

     * <span data-ttu-id="7b927-191">Voor kleine toomodest gegevens, prestaties, het wordt aanbevolen wanneer geanalyseerd in de context van een lokale compute op Hallo edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7b927-191">For small toomodest data, performance is best when analyzed in a local compute context on hello edge node.</span></span>  <span data-ttu-id="7b927-192">Voor meer informatie over het Hallo-scenario's waarin Hallo lokale en Spark contexten COMPUTE werken het beste, Compute context opties voor R Server ziet op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b927-192">For more information on hello scenarios under which hello local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="7b927-193">Als u toohello edge-knooppunt aanmelden en uw R-script uitvoeren, wordt alle maar Hallo ScaleR rx-functies worden uitgevoerd <strong>lokaal</strong> op Hallo edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7b927-193">If you log in toohello edge node and run your R script, then all but hello ScaleR rx-functions are executed <strong>locally</strong> on hello edge node.</span></span> <span data-ttu-id="7b927-194">Dus Hallo geheugen en het aantal kernen van Hallo edge-knooppunt dienovereenkomstig moet worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="7b927-194">So hello memory and number of cores of hello edge node should be sized accordingly.</span></span> <span data-ttu-id="7b927-195">Hallo geldt ook als u R Server op HDI als een externe compute-context van uw laptop.</span><span class="sxs-lookup"><span data-stu-id="7b927-195">hello same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Blade Prijscategorieën voor knooppunten](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="7b927-197">Gebruik Hallo **Selecteer** knop toosave Hallo knooppunt configuratie prijzen.</span><span class="sxs-lookup"><span data-stu-id="7b927-197">Use hello **Select** button toosave hello node pricing configuration.</span></span>

   <span data-ttu-id="7b927-198">Er is ook een koppeling **Sjabloon en parameters downloaden**.</span><span class="sxs-lookup"><span data-stu-id="7b927-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="7b927-199">Klik op deze koppeling toodisplay scripts die kunnen worden gebruikt tooautomate Hallo maken van een cluster met geselecteerde Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="7b927-199">Click on this link toodisplay scripts that can be used tooautomate hello creation of a cluster with hello selected configuration.</span></span> <span data-ttu-id="7b927-200">Deze scripts zijn ook beschikbaar is via Azure portal-ingang voor uw cluster Hallo zodra deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b927-200">These scripts are also available from hello Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7b927-201">Het duurt enige tijd Hallo cluster toobe gemaakt, meestal ongeveer 20 minuten.</span><span class="sxs-lookup"><span data-stu-id="7b927-201">It takes some time for hello cluster toobe created, usually around 20 minutes.</span></span> <span data-ttu-id="7b927-202">Hallo-tegel op Hallo Startboard gebruiken of Hallo **meldingen** post op Hallo links van Hallo pagina toocheck op Hallo aanmaakproces.</span><span class="sxs-lookup"><span data-stu-id="7b927-202">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a><span data-ttu-id="7b927-203">Verbinding maken met Server tooRStudio</span><span class="sxs-lookup"><span data-stu-id="7b927-203">Connect tooRStudio Server</span></span>

<span data-ttu-id="7b927-204">Als u tooinclude RStudio Server community edition in de installatie hebt gekozen, kunt u Hallo RStudio aanmelding via twee verschillende methoden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b927-204">If you’ve chosen tooinclude RStudio Server community edition in your installation, then you can access hello RStudio login via two different methods.</span></span>

1. <span data-ttu-id="7b927-205">Ga toohello na URL (waarbij **CLUSTERNAME** Hallo-naam van Hallo-cluster die u hebt gemaakt):</span><span class="sxs-lookup"><span data-stu-id="7b927-205">Go toohello following URL (where **CLUSTERNAME** is hello name of hello cluster you've created):</span></span>

    <span data-ttu-id="7b927-206">https://**CLUSTERNAAM**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="7b927-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="7b927-207">Hallo-vermelding voor uw cluster openen in hello Azure-portal, selecteer Hallo **R Server Dashboards** snelkoppeling en vervolgens te klikken op Hallo **R Studio Dashboard**:</span><span class="sxs-lookup"><span data-stu-id="7b927-207">Open hello entry for your cluster in hello Azure portal, select hello **R Server Dashboards** quick link and then selecting hello **R Studio Dashboard**:</span></span>

     ![Toegang Hallo R studio dashboard](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Toegang Hallo R studio dashboard](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="7b927-210">Hallo-methode die wordt gebruikt, ongeacht de moet hello eerste keer dat u zich aanmeldt u tooauthenticate twee keer.</span><span class="sxs-lookup"><span data-stu-id="7b927-210">Regardless of hello method used, hello first time you log in you need tooauthenticate twice.</span></span>  <span data-ttu-id="7b927-211">Geef op de eerste verificatie Hallo Hallo *cluster Admin userid* en *wachtwoord*.</span><span class="sxs-lookup"><span data-stu-id="7b927-211">At hello first authentication, provide hello *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="7b927-212">Geef op de tweede vraag hello, Hallo *SSH userid* en *wachtwoord*.</span><span class="sxs-lookup"><span data-stu-id="7b927-212">At hello second prompt, provide hello *SSH userid* and *password*.</span></span> <span data-ttu-id="7b927-213">Daaropvolgende logboek modules vereisen alleen Hallo *SSH-wachtwoord* en *userid*.</span><span class="sxs-lookup"><span data-stu-id="7b927-213">Subsequent log ins only require hello *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a><span data-ttu-id="7b927-214">Verbinding maken met toohello edge-knooppunt op R Server</span><span class="sxs-lookup"><span data-stu-id="7b927-214">Connect toohello R Server edge node</span></span>

<span data-ttu-id="7b927-215">Verbinding maken met een rondleiding Server edge-knooppunt van Hallo HDInsight-cluster via SSH met Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="7b927-215">Connect tooR Server edge node of hello HDInsight cluster using SSH with hello command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="7b927-216">U vindt Hallo `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` adres in hello Azure-portal door te selecteren van het cluster vervolgens **alle instellingen** -> **Apps** -> **RServer**.</span><span class="sxs-lookup"><span data-stu-id="7b927-216">You can find hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in hello Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="7b927-217">U ziet nu Hallo SSH Endpoint-informatie voor Hallo edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7b927-217">This displays hello SSH Endpoint information for hello edge node.</span></span>
>
> ![Afbeelding van Hallo SSH-eindpunt voor Hallo edge-knooppunt](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="7b927-219">Als u een wachtwoord toosecure uw SSH gebruikersaccount gebruikt, bent u na vragen aan gebruiker tooenter deze.</span><span class="sxs-lookup"><span data-stu-id="7b927-219">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="7b927-220">Als u een openbare sleutel gebruikt, hebt u mogelijk toouse hello `-i` parameter toospecify Hallo overeenkomende persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="7b927-220">If you used a public key, you may have toouse hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="7b927-221">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7b927-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="7b927-222">Zie voor meer informatie [tooHDInsight (Hadoop) via SSH verbinding](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7b927-222">For more information, see [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="7b927-223">Eenmaal zijn verbonden, wordt u aankomt bij een prompt vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="7b927-223">Once connected, you arrive at a prompt similar toohello following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="7b927-224">Meerdere gelijktijdige gebruikers inschakelen</span><span class="sxs-lookup"><span data-stu-id="7b927-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="7b927-225">U kunt meerdere gelijktijdige gebruikers inschakelen door het toevoegen van meer gebruikers voor Hallo edge-knooppunt op welke Hallo RStudio community-versie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-225">You can enable multiple concurrent users by adding more users for hello edge node on which hello RStudio community version runs.</span></span>

<span data-ttu-id="7b927-226">Wanneer u een HDInsight-cluster maakt, moet u twee gebruikers opgeven, te weten een HTTP-gebruiker en een SSH-gebruiker:</span><span class="sxs-lookup"><span data-stu-id="7b927-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Gelijktijdige gebruiker 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="7b927-228">**Gebruikersnaam voor aanmelding cluster**: een gebruiker met HTTP voor verificatie via Hallo HDInsight gateway die wordt gebruikt tooprotect hello HDInsight-clusters u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b927-228">**Cluster login username**: an HTTP user for authentication through hello HDInsight gateway that is used tooprotect hello HDInsight clusters you created.</span></span> <span data-ttu-id="7b927-229">Deze gebruiker HTTP is gebruikte tooaccess hello Ambari UI, gebruikersinterface van YARN, evenals andere UI-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="7b927-229">This HTTP user is used tooaccess hello Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="7b927-230">**Secure Shell (SSH) gebruikersnaam**: een SSH gebruiker tooaccess Hallo-cluster via secure shell.</span><span class="sxs-lookup"><span data-stu-id="7b927-230">**Secure Shell (SSH) username**: an SSH user tooaccess hello cluster through secure shell.</span></span> <span data-ttu-id="7b927-231">Deze gebruiker is een gebruiker in Hallo Linux-systeem voor alle hoofdknooppunten hello, worker-knooppunten en knooppunten van de rand.</span><span class="sxs-lookup"><span data-stu-id="7b927-231">This user is a user in hello Linux system for all hello head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="7b927-232">Zo kunt u secure shell tooaccess Hallo knooppunten in een RAS-cluster.</span><span class="sxs-lookup"><span data-stu-id="7b927-232">So you can use secure shell tooaccess any of hello nodes in a remote cluster.</span></span>

<span data-ttu-id="7b927-233">Hallo R Studio Server Community-versie die wordt gebruikt in Hallo Microsoft R Server op HDInsight-cluster type accepteert alleen een Linux-gebruikersnaam en wachtwoord als een mechanisme voor aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7b927-233">hello R Studio Server Community version used in hello Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="7b927-234">Doorgegeven tokens worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7b927-234">It does not support passing tokens.</span></span> <span data-ttu-id="7b927-235">Als u een nieuw cluster hebt gemaakt en toouse R Studio tooaccess wilt, moet u toolog in twee keer.</span><span class="sxs-lookup"><span data-stu-id="7b927-235">So if you have created a new cluster and want toouse R Studio tooaccess it, you need toolog in twice.</span></span>

- <span data-ttu-id="7b927-236">Meldt u zich eerst bij het gebruik van de gebruikersreferenties Hallo HTTP via Hallo HDInsight-Gateway:</span><span class="sxs-lookup"><span data-stu-id="7b927-236">First log in using hello HTTP user credentials through hello HDInsight Gateway:</span></span> 

    ![Gelijktijdige gebruiker 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="7b927-238">Gebruik vervolgens Hallo SSH gebruiker referenties toolog in tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="7b927-238">Then use hello SSH user credentials toolog in tooRStudio:</span></span>
  
    ![Gelijktijdige gebruiker 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="7b927-240">Op dit moment kan slechts één SSH gebruikersaccount worden gemaakt tijdens het inrichten van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7b927-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="7b927-241">Dus tooenable meerdere gebruikers tooaccess Microsoft R Server op een HDInsight-clusters, moeten we toocreate extra gebruikers in Hallo Linux-systeem.</span><span class="sxs-lookup"><span data-stu-id="7b927-241">So tooenable multiple users tooaccess Microsoft R Server on HDInsight clusters, we need toocreate additional users in hello Linux system.</span></span>

<span data-ttu-id="7b927-242">Omdat RStudio Server-Community op Hallo van het cluster edge-knooppunt wordt uitgevoerd, zijn er verschillende volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7b927-242">Because RStudio Server Community is running on hello cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="7b927-243">Gebruik Hallo gemaakt SSH gebruiker toolog in toohello edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="7b927-243">Use hello created SSH user toolog in toohello edge node</span></span>
2. <span data-ttu-id="7b927-244">Meer Linux-gebruikers toevoegen in Edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="7b927-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="7b927-245">Hallo gebruiker gemaakt RStudio Community-versie gebruiken</span><span class="sxs-lookup"><span data-stu-id="7b927-245">Use RStudio Community version with hello user created</span></span>

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a><span data-ttu-id="7b927-246">Stap 1: Gebruik Hallo gemaakt SSH gebruiker toolog in toohello edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="7b927-246">Step 1: Use hello created SSH user toolog in toohello edge node</span></span>

<span data-ttu-id="7b927-247">Een SSH-hulpprogramma (zoals Putty) downloaden en gebruiken van Hallo bestaande SSH gebruiker toolog in.</span><span class="sxs-lookup"><span data-stu-id="7b927-247">Download any SSH tool (such as Putty) and use hello existing SSH user toolog in.</span></span> <span data-ttu-id="7b927-248">Volg de instructies Hallo in [tooHDInsight (Hadoop) via SSH verbinding](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess Hallo edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7b927-248">Then follow hello instructions provided in [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello edge node.</span></span> <span data-ttu-id="7b927-249">Hallo edge-knooppuntadres voor R Server op HDInsight-cluster is: *clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="7b927-249">hello edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="7b927-250">Stap 2: meer Linux-gebruikers toevoegen in Edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="7b927-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="7b927-251">een gebruiker toohello edge-knooppunt tooadd Hallo opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7b927-251">tooadd a user toohello edge node, execute hello commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="7b927-252">U ziet de volgende items geretourneerd Hallo:</span><span class="sxs-lookup"><span data-stu-id="7b927-252">You should see hello following items returned:</span></span> 

![Gelijktijdige gebruiker 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="7b927-254">Als u wordt gevraagd ' huidige Kerberos-wachtwoord: ', drukt u op **Enter** tooignore deze.</span><span class="sxs-lookup"><span data-stu-id="7b927-254">When prompted for “Current Kerberos password:”, just press **Enter** tooignore it.</span></span> <span data-ttu-id="7b927-255">Hallo `-m` optie in `useradd` opdracht geeft aan dat hello wordt gemaakt een basismap voor Hallo-gebruiker vereist voor RStudio Community-versie is.</span><span class="sxs-lookup"><span data-stu-id="7b927-255">hello `-m` option in `useradd` command indicates that hello system will create a home folder for hello user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a><span data-ttu-id="7b927-256">Stap 3: Gebruik RStudio Community-versie met Hallo gebruiker gemaakt</span><span class="sxs-lookup"><span data-stu-id="7b927-256">Step 3: Use RStudio Community version with hello user created</span></span>

<span data-ttu-id="7b927-257">Hallo gebruiker gemaakte toolog in tooRStudio gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7b927-257">Use hello user created toolog in tooRStudio:</span></span>

![Gelijktijdige gebruiker 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="7b927-259">Kennisgeving RStudio geeft aan dat u van de nieuwe gebruiker hello gebruikmaakt (hier bijvoorbeeld *sshuser6*) toolog in Hallo-cluster:</span><span class="sxs-lookup"><span data-stu-id="7b927-259">Notice that RStudio indicates that you are using hello new user (here, for example, *sshuser6*) toolog in hello cluster:</span></span> 

![Gelijktijdige gebruiker 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="7b927-261">U kunt ook aanmelden met behulp van de oorspronkelijke referenties hello (dit is standaard *sshuser*) tegelijkertijd uit een ander browservenster.</span><span class="sxs-lookup"><span data-stu-id="7b927-261">You can also log in using hello original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="7b927-262">U kunt een taak met scaleR-functies verzenden.</span><span class="sxs-lookup"><span data-stu-id="7b927-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="7b927-263">Hier volgt een voorbeeld van Hallo-opdrachten gebruikt toorun een taak:</span><span class="sxs-lookup"><span data-stu-id="7b927-263">Here is an example of hello commands used toorun a job:</span></span>

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
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

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="7b927-264">U ziet dat de Hallo taken die worden verzonden onder andere gebruikersnamen in de gebruikersinterface van YARN zijn:</span><span class="sxs-lookup"><span data-stu-id="7b927-264">Notice that hello jobs submitted are under different user names in YARN UI:</span></span>

![Gelijktijdige gebruiker 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="7b927-266">Opmerking ook die Hallo toegevoegde gebruikers hebben geen hoofdmap bevoegdheden in Linux-systeem, maar ze hebben Hallo dezelfde tooall Hallo bestanden in de Hallo externe HDFS en WASB opslag openen.</span><span class="sxs-lookup"><span data-stu-id="7b927-266">Note also that hello newly added users do not have root privileges in Linux system, but they do have hello same access tooall hello files in hello remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a><span data-ttu-id="7b927-267">Hallo R-console gebruiken</span><span class="sxs-lookup"><span data-stu-id="7b927-267">Use hello R console</span></span>

1. <span data-ttu-id="7b927-268">Gebruik van Hallo SSH-sessie, Hallo opdrachtconsole toostart Hallo R te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b927-268">From hello SSH session, use hello following command toostart hello R console:</span></span>  

        R

2. <span data-ttu-id="7b927-269">Hier ziet u uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="7b927-269">You should see output similar toohello following:</span></span>
    
    <span data-ttu-id="7b927-270">R versie 3.2.2 (2015-08-14)--'Fire veiligheid' Copyright (C) 2015 R Foundation Hallo voor statistische Computing Platform: x86_64-pc-linux-gnu (64-bits)</span><span class="sxs-lookup"><span data-stu-id="7b927-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 hello R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="7b927-271">R is gratis software en wordt geleverd ZONDER ENIGE GARANTIE.</span><span class="sxs-lookup"><span data-stu-id="7b927-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="7b927-272">U staat op het Welkom tooredistribute dit onder bepaalde omstandigheden.</span><span class="sxs-lookup"><span data-stu-id="7b927-272">You are welcome tooredistribute it under certain conditions.</span></span>
    <span data-ttu-id="7b927-273">Typ 'license()' of 'licence()' voor distributie-informatie.</span><span class="sxs-lookup"><span data-stu-id="7b927-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="7b927-274">Ondersteuning van natuurlijke taal, maar uitgevoerd in een Engelse landinstelling</span><span class="sxs-lookup"><span data-stu-id="7b927-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="7b927-275">R is een samenwerkingsproject met veel inzenders.</span><span class="sxs-lookup"><span data-stu-id="7b927-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="7b927-276">Typ 'contributors()' voor meer informatie en 'citation()' op hoe toocite R of R-in publicaties pakketten.</span><span class="sxs-lookup"><span data-stu-id="7b927-276">Type 'contributors()' for more information and 'citation()' on how toocite R or R packages in publications.</span></span>

    <span data-ttu-id="7b927-277">Typ 'demo()' voor sommige demo's, voor on line help ' help()' of 'help.start()' voor een HTML-browser interface toohelp.</span><span class="sxs-lookup"><span data-stu-id="7b927-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface toohelp.</span></span>
    <span data-ttu-id="7b927-278">Typ 'q()' tooquit R.</span><span class="sxs-lookup"><span data-stu-id="7b927-278">Type 'q()' tooquit R.</span></span>

    <span data-ttu-id="7b927-279">Microsoft R Server versie 8.0: een verbeterde distributie van R Microsoft-pakketten Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="7b927-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="7b927-280">Typ 'readme()' voor de release-opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="7b927-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="7b927-281">Van Hallo `>` vragen, kunt u R-code invoeren.</span><span class="sxs-lookup"><span data-stu-id="7b927-281">From hello `>` prompt, you can enter R code.</span></span> <span data-ttu-id="7b927-282">R server bevat pakketten waarmee u tooeasily communiceren met Hadoop en gedistribueerde berekeningen uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-282">R server includes packages that allow you tooeasily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="7b927-283">Gebruik bijvoorbeeld Hallo opdracht tooview Hallo hoofdmap van Hallo standaardbestandssysteem voor Hallo HDInsight-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b927-283">For example, use hello following command tooview hello root of hello default file system for hello HDInsight cluster:</span></span>

    <span data-ttu-id="7b927-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="7b927-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="7b927-285">U kunt ook Hallo WASB stijl adressering.</span><span class="sxs-lookup"><span data-stu-id="7b927-285">You can also use hello WASB style addressing.</span></span>

    <span data-ttu-id="7b927-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="7b927-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="7b927-287">R Server op HDI gebruiken vanaf een extern exemplaar van Microsoft R Server of Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="7b927-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="7b927-288">Het is mogelijk tooset up toegang toohello HDI Hadoop Spark compute context van een extern exemplaar van Microsoft R Server of Microsoft R Client uitgevoerd op een desktop of laptop.</span><span class="sxs-lookup"><span data-stu-id="7b927-288">It is possible tooset up access toohello HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="7b927-289">Zie **met behulp van Microsoft R Server als een Hadoop Client** subsectie in Hallo [maken van een Compute-Context voor Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="7b927-289">See **Using Microsoft R Server as a Hadoop Client** subsection in hello [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="7b927-290">toodo u moet dus toospecify Hallo opties te volgen bij het definiëren van Hallo RxSpark compute context op uw laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, en sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="7b927-290">toodo so, you need toospecify hello following options when defining hello RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="7b927-291">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7b927-291">For example:</span></span>


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


## <a name="use-a-compute-context"></a><span data-ttu-id="7b927-292">Een compute-context gebruiken</span><span class="sxs-lookup"><span data-stu-id="7b927-292">Use a compute context</span></span>

<span data-ttu-id="7b927-293">Een compute-context kunt u toocontrol of berekening wordt lokaal uitgevoerd op de edge-knooppunt Hallo of verdeeld over knooppunten Hallo in Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7b927-293">A compute context allows you toocontrol whether computation is performed locally on hello edge node or distributed across hello nodes in hello HDInsight cluster.</span></span>

1. <span data-ttu-id="7b927-294">Gebruik van Hallo R-console (in een SSH-sessie) of RStudio Server Hallo code tooload bijvoorbeeld gegevens te volgen in de Hallo standaard opslag voor HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7b927-294">From RStudio Server or hello R console (in an SSH session), use hello following code tooload example data into hello default storage for HDInsight:</span></span>

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
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

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="7b927-295">Vervolgens laten we enkele info gegevens maken en twee gegevensbronnen definiëren, zodat we met Hallo gegevens werken.</span><span class="sxs-lookup"><span data-stu-id="7b927-295">Next, let's create some data info and define two data sources so that we can work with hello data.</span></span>

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="7b927-296">We gaan een logistic regression via Hallo-gegevens met Hallo lokale compute context worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-296">Let's run a logistic regression over hello data using hello local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="7b927-297">Hier ziet u uitvoer die eindigt op regels vergelijkbare toohello te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b927-297">You should see output that ends with lines similar toohello following:</span></span>

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

4. <span data-ttu-id="7b927-298">Vervolgens gaat uitvoeren Hallo dezelfde logistic regression met Hallo Spark context.</span><span class="sxs-lookup"><span data-stu-id="7b927-298">Next, let's run hello same logistic regression using hello Spark context.</span></span> <span data-ttu-id="7b927-299">Hallo Spark context distribueert Hallo verwerking via alle Hallo worker-knooppunten in Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7b927-299">hello Spark context distributes hello processing over all hello worker nodes in hello HDInsight cluster.</span></span>

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="7b927-300">U kunt ook MapReduce toodistribute berekening over clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="7b927-300">You can also use MapReduce toodistribute computation across cluster nodes.</span></span> <span data-ttu-id="7b927-301">Zie [Opties voor compute-context voor R Server op HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) voor meer informatie over compute-context.</span><span class="sxs-lookup"><span data-stu-id="7b927-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-toomultiple-nodes"></a><span data-ttu-id="7b927-302">R code toomultiple knooppunten distribueren</span><span class="sxs-lookup"><span data-stu-id="7b927-302">Distribute R code toomultiple nodes</span></span>

<span data-ttu-id="7b927-303">R server, u kunt eenvoudig bestaande R-code en deze op meerdere knooppunten in cluster Hallo uitvoeren met behulp van `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="7b927-303">With R Server, you can easily take existing R code and run it across multiple nodes in hello cluster by using `rxExec`.</span></span> <span data-ttu-id="7b927-304">Deze functie is handig bij het uitvoeren van een parameteropschoning of van simulaties.</span><span class="sxs-lookup"><span data-stu-id="7b927-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="7b927-305">Hallo volgende code is een voorbeeld van hoe toouse `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="7b927-305">hello following code is an example of how toouse `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="7b927-306">Als u nog steeds Hallo Spark of MapReduce-context, deze opdracht retourneert Hallo nodename waarde voor de worker-knooppunten Hallo die code Hallo `(Sys.info()["nodename"])` op wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-306">If you are still using hello Spark or MapReduce context, this  command returns hello nodename value for hello worker nodes that hello code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="7b927-307">Bijvoorbeeld: op een cluster met vier knooppunten verwacht tooreceive vergelijkbare toohello volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="7b927-307">For example, on a four node cluster, you expect tooreceive output similar toohello following:</span></span>

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


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="7b927-308">Toegang tot gegevens in Hive en Parquet</span><span class="sxs-lookup"><span data-stu-id="7b927-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="7b927-309">Een functie die beschikbaar zijn in R Server 9.1 kunt directe toegang toodata in Hive en parketvloeren voor gebruik door ScaleR functies in Hallo Spark compute-context.</span><span class="sxs-lookup"><span data-stu-id="7b927-309">A feature available in R Server 9.1 allows direct access toodata in Hive and Parquet for use by ScaleR functions in hello Spark compute context.</span></span> <span data-ttu-id="7b927-310">Deze mogelijkheden zijn beschikbaar via de nieuwe ScaleR bron gegevensfuncties RxHiveData en RxParquetData genoemd die door het gebruik van Spark SQL tooload gegevens rechtstreeks in een Spark-DataFrame voor analyse door ScaleR werken.</span><span class="sxs-lookup"><span data-stu-id="7b927-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL tooload data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="7b927-311">Sommige voorbeeldcode biedt Hallo na code bij het gebruik van nieuwe functies Hallo:</span><span class="sxs-lookup"><span data-stu-id="7b927-311">hello following code provides some sample code on use of hello new functions:</span></span>

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

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="7b927-312">Zie voor meer informatie over het gebruik van deze nieuwe functies Hallo in de online help R Server door het gebruik van Hallo `?RxHivedata` en `?RxParquetData` opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7b927-312">For additional info on use of these new functions see hello online help in R Server through use of hello `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-hello-edge-node"></a><span data-ttu-id="7b927-313">Extra R-pakketten installeren op Hallo edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="7b927-313">Install additional R packages on hello edge node</span></span>

<span data-ttu-id="7b927-314">Als u tooinstall extra R-pakketten op Hallo edge-knooppunt dat wilt, kunt u `install.packages()` rechtstreeks vanuit Hallo R-console wanneer verbonden toohello edge-knooppunt via SSH.</span><span class="sxs-lookup"><span data-stu-id="7b927-314">If you would like tooinstall additional R packages on hello edge node, you can use `install.packages()` directly from within hello R console when connected toohello edge node through SSH.</span></span> <span data-ttu-id="7b927-315">Als u tooinstall R-pakketten op Hallo worker-knooppunten van het Hallo-cluster nodig hebt, moet u echter een scriptactie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b927-315">However, if you need tooinstall R packages on hello worker nodes of hello cluster, you must use a Script Action.</span></span>

<span data-ttu-id="7b927-316">Scriptacties zijn Bash-scripts die gebruikt toomake configuratie wijzigingen toohello HDInsight-cluster of tooinstall aanvullende software, zoals extra R-pakketten zijn.</span><span class="sxs-lookup"><span data-stu-id="7b927-316">Script Actions are Bash scripts that are used toomake configuration changes toohello HDInsight cluster or tooinstall additional software, such as additional R packages.</span></span> <span data-ttu-id="7b927-317">tooinstall extra pakketten met behulp van een scriptactie gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b927-317">tooinstall additional packages using a Script Action, use hello following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b927-318">Met behulp van scriptacties tooinstall aanvullende R-pakketten kan alleen worden gebruikt nadat Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b927-318">Using Script Actions tooinstall additional R packages can only be used after hello cluster has been created.</span></span> <span data-ttu-id="7b927-319">Gebruik deze procedure niet tijdens het maken van het cluster, zoals het Hallo-script is afhankelijk van het R Server wordt volledig geïnstalleerd en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-319">Do not use this procedure during cluster creation, as hello script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="7b927-320">Van Hallo [Azure-portal](https://portal.azure.com), selecteer uw R Server op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7b927-320">From hello [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="7b927-321">Van Hallo **instellingen** blade Selecteer **scriptacties** en vervolgens **nieuwe indienen** toosubmit een nieuwe scriptactie.</span><span class="sxs-lookup"><span data-stu-id="7b927-321">From hello **Settings** blade, select **Script Actions** and then **Submit New** toosubmit a new Script Action.</span></span>

   ![Afbeelding van de blade Scriptacties](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="7b927-323">Van Hallo **scriptactie indienen** blade bieden Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="7b927-323">From hello **Submit script action** blade, provide hello following information:</span></span>

   * <span data-ttu-id="7b927-324">**Naam**: een beschrijvende naam tooidentify dit script</span><span class="sxs-lookup"><span data-stu-id="7b927-324">**Name**: A friendly name tooidentify this script</span></span>

   * <span data-ttu-id="7b927-325">**Bash-script-URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="7b927-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="7b927-326">**Head**: dit item moet zijn **uitgeschakeld**</span><span class="sxs-lookup"><span data-stu-id="7b927-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="7b927-327">**Worker**: dit item moet zijn **ingeschakeld**</span><span class="sxs-lookup"><span data-stu-id="7b927-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="7b927-328">**Edge nodes**: dit item moet zijn **uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="7b927-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="7b927-329">**Zookeeper**: dit item moet zijn **uitgeschakeld**</span><span class="sxs-lookup"><span data-stu-id="7b927-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="7b927-330">**Parameters**: Hallo R-pakketten toobe geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-330">**Parameters**: hello R packages toobe installed.</span></span> <span data-ttu-id="7b927-331">Bijvoorbeeld: `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="7b927-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="7b927-332">**Deze scriptactie opnieuw laten uitvoeren...** : dit item moet zijn **ingeschakeld**</span><span class="sxs-lookup"><span data-stu-id="7b927-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="7b927-333">Standaard worden alle R-pakketten geïnstalleerd vanuit een momentopname van Hallo Microsoft MRAN opslagplaats consistent zijn met het Hallo-versie van het R-Server die is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-333">By default, all R packages are installed from a snapshot of hello Microsoft MRAN repository consistent with hello version of R Server that has been installed.</span></span> <span data-ttu-id="7b927-334">Als u wilt dat tooinstall nieuwere versies van pakketten, is de risico's niet compatibel.</span><span class="sxs-lookup"><span data-stu-id="7b927-334">If you want tooinstall newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="7b927-335">Dit soort installeren is echter mogelijk door te geven `useCRAN` als Hallo eerste element van het pakket hello wilt weergeven, bijvoorbeeld `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="7b927-335">However this kind of install is possible by specifying `useCRAN` as hello first element of hello package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="7b927-336">Voor sommige R-pakketten zijn aanvullende Linux-systeembibliotheken vereist.</span><span class="sxs-lookup"><span data-stu-id="7b927-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="7b927-337">Voor het gemak hebben we Hallo afhankelijkheden die nodig is voor Hallo top 100 meest populaire R-pakketten vooraf geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7b927-337">For convenience, we have pre-installed hello dependencies needed by hello top 100 most popular R packages.</span></span> <span data-ttu-id="7b927-338">Echter als Hallo R pakketten die u installeert bibliotheken afgezien van deze vereist moet vervolgens u downloaden Hallo base script hier gebruikt en stappen tooinstall Hallo systeembibliotheken toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7b927-338">However, if hello R package(s) you install require libraries beyond these then you must download hello base script used here and add steps tooinstall hello system libraries.</span></span> <span data-ttu-id="7b927-339">U moet vervolgens uploaden Hallo gewijzigd script tooa openbare blob-container in Azure-opslag en Hallo gewijzigd script tooinstall hello-pakketten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b927-339">You must then upload hello modified script tooa public blob container in Azure storage and use hello modified script tooinstall hello packages.</span></span>
   >    <span data-ttu-id="7b927-340">Zie [Ontwikkeling van scriptacties](hdinsight-hadoop-script-actions-linux.md) voor meer informatie over het ontwikkelen van scriptacties.</span><span class="sxs-lookup"><span data-stu-id="7b927-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Een scriptactie toevoegen](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="7b927-342">Selecteer **maken** toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="7b927-342">Select **Create** toorun hello script.</span></span> <span data-ttu-id="7b927-343">Zodra het Hallo-script is voltooid, zijn Hallo R-pakketten beschikbaar op alle worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7b927-343">Once hello script completes, hello R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="7b927-344">Microsoft R Server-uitoefening gebruiken</span><span class="sxs-lookup"><span data-stu-id="7b927-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="7b927-345">Wanneer uw gegevens modelleren voltooid is, kunt u Hallo model toomake voorspellingen operationeel te maken.</span><span class="sxs-lookup"><span data-stu-id="7b927-345">When your data modeling is complete, you can operationalize hello model toomake predictions.</span></span> <span data-ttu-id="7b927-346">tooconfigure voor Microsoft R Server uitoefening, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b927-346">tooconfigure for Microsoft R Server operationalization, perform hello following steps:</span></span>

<span data-ttu-id="7b927-347">Eerst ssh in Hallo Edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7b927-347">First, ssh into hello Edge node.</span></span> <span data-ttu-id="7b927-348">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7b927-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="7b927-349">Als u met ssh, map voor relevante Hallo-versie en sudo Hallo dotnet dll-bestand te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="7b927-349">After using ssh, change directory for hello relevant version and sudo hello dotnet dll:</span></span> 

- <span data-ttu-id="7b927-350">Voor Microsoft R Server 9.1:</span><span class="sxs-lookup"><span data-stu-id="7b927-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="7b927-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="7b927-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="7b927-352">Voor Microsoft R Server 9.0:</span><span class="sxs-lookup"><span data-stu-id="7b927-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="7b927-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="7b927-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="7b927-354">tooconfigure Microsoft R Server uitoefening met een 1-box-configuratie Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b927-354">tooconfigure Microsoft R Server operationalization with a One-box configuration do hello following:</span></span>

1. <span data-ttu-id="7b927-355">'R-Server voor uitoefening configureren' selecteren</span><span class="sxs-lookup"><span data-stu-id="7b927-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="7b927-356">Selecteer A.</span><span class="sxs-lookup"><span data-stu-id="7b927-356">Select “A.</span></span> <span data-ttu-id="7b927-357">Alles-in-één (web- + rekenknooppunten)</span><span class="sxs-lookup"><span data-stu-id="7b927-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="7b927-358">Geef een wachtwoord voor Hallo **admin** gebruiker</span><span class="sxs-lookup"><span data-stu-id="7b927-358">Enter a password for hello **admin** user</span></span>

![De optie Alles-in-één](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="7b927-360">Als optionele stap kunt u Diagnostische controles uitvoeren door als volgt een diagnostische test uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="7b927-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="7b927-361">Selecteer 6.</span><span class="sxs-lookup"><span data-stu-id="7b927-361">Select “6.</span></span> <span data-ttu-id="7b927-362">Diagnostische tests uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7b927-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="7b927-363">Selecteer A.</span><span class="sxs-lookup"><span data-stu-id="7b927-363">Select “A.</span></span> <span data-ttu-id="7b927-364">Configuratie testen</span><span class="sxs-lookup"><span data-stu-id="7b927-364">Test configuration”</span></span>
3. <span data-ttu-id="7b927-365">Voer als gebruikersnaam Beheerder in en geef het wachtwoord uit de voorgaande configuratiestap op</span><span class="sxs-lookup"><span data-stu-id="7b927-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="7b927-366">Algehele status bevestigen = geslaagd</span><span class="sxs-lookup"><span data-stu-id="7b927-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="7b927-367">Exit Hallo beheerder hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="7b927-367">Exit hello Admin Utility</span></span>
6. <span data-ttu-id="7b927-368">Sluit SSH</span><span class="sxs-lookup"><span data-stu-id="7b927-368">Exit SSH</span></span>

![De optie Diagnose voor](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="7b927-370">**Lange vertragingen bij het gebruiken van webservice op Spark**</span><span class="sxs-lookup"><span data-stu-id="7b927-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="7b927-371">Als u lange vertragingen optreden als een webservice tooconsume probeert met mrsdeploy functies in de context van een Spark compute gemaakt, moet u mogelijk tooadd sommige ontbrekende mappen.</span><span class="sxs-lookup"><span data-stu-id="7b927-371">If you encounter long delays when trying tooconsume a web service created with mrsdeploy functions in a Spark compute context, you may need tooadd some missing folders.</span></span> <span data-ttu-id="7b927-372">Hallo Spark toepassing behoort tooa gebruiker met de naam '*rserve2*' wanneer deze wordt aangeroepen vanuit mrsdeploy functies met een webservice.</span><span class="sxs-lookup"><span data-stu-id="7b927-372">hello Spark application belongs tooa user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="7b927-373">toowork dit probleem oplossen:</span><span class="sxs-lookup"><span data-stu-id="7b927-373">toowork around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="7b927-374">In deze fase is Hallo-configuratie voor uitoefening voltooid.</span><span class="sxs-lookup"><span data-stu-id="7b927-374">At this stage, hello configuration for Operationalization is complete.</span></span> <span data-ttu-id="7b927-375">Nu kunt u Hallo 'mrsdeploy' pakket op uw RClient tooconnect toohello uitoefening op de edge-knooppunt en gestart met de functies, zoals [uitvoering op afstand](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) en [webservices](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="7b927-375">Now you can use hello ‘mrsdeploy’ package on your RClient tooconnect toohello Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="7b927-376">Afhankelijk van of het cluster is ingesteld op een virtueel netwerk of niet, moet u mogelijk tooset up poort doorsturen van tunneling via SSH-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7b927-376">Depending on whether your cluster is set up on a virtual network or not, you may need tooset up port forward tunneling through SSH login.</span></span> <span data-ttu-id="7b927-377">Hallo volgende secties wordt uitgelegd hoe tooset van deze tunnel.</span><span class="sxs-lookup"><span data-stu-id="7b927-377">hello following sections explain how tooset up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="7b927-378">RServer-cluster in een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="7b927-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="7b927-379">Zorg ervoor dat u toestaat dat verkeer via poort 12800 toohello edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7b927-379">Make sure you allow traffic through port 12800 toohello edge node.</span></span> <span data-ttu-id="7b927-380">Op die manier kunt u Hallo edge-knooppunt tooconnect toohello uitoefening functie.</span><span class="sxs-lookup"><span data-stu-id="7b927-380">That way, you can use hello edge node tooconnect toohello Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="7b927-381">Als hello `remoteLogin()` kan geen verbinding toohello edge-knooppunt, maar kunt u SSH toohello edge-knooppunt, moet u tooverify of Hallo regel tooallow verkeer op poort 12800 goed of niet is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7b927-381">If hello `remoteLogin()` cannot connect toohello edge node, but you can SSH toohello edge node, then you need tooverify whether hello rule tooallow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="7b927-382">Als u tooface Hallo probleem doorgaat, kunt u omzeilen het door het instellen van poort doorsturen van tunneling via SSH.</span><span class="sxs-lookup"><span data-stu-id="7b927-382">If you continue tooface hello issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="7b927-383">Voor instructies raadpleegt u de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b927-383">For instructions, see hello following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="7b927-384">RServer-cluster is niet ingesteld in het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="7b927-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="7b927-385">Als het cluster niet is ingesteld in het virtuele netwerk vnet of als u problemen ondervindt met de connectiviteit via dit netwerk, kunt u forward tunneling via SSH instellen voor de poort:</span><span class="sxs-lookup"><span data-stu-id="7b927-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="7b927-386">U kunt dit ook instellen op Putty.</span><span class="sxs-lookup"><span data-stu-id="7b927-386">On Putty, you can set it up as well.</span></span>

![Putty SSH-verbinding](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="7b927-388">Nadat uw SSH-sessie actief is, doorgestuurd verkeer van uw machine poort 12800 Hallo toohello edge-knooppunt van poort 12800 via SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="7b927-388">Once your SSH session is active, hello traffic from your machine’s port 12800 is forwarded toohello edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="7b927-389">Zorg ervoor dat u `127.0.0.1:12800` gebruikt in de `remoteLogin()`-methode.</span><span class="sxs-lookup"><span data-stu-id="7b927-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="7b927-390">Dit uitoefening toohello rand van het knooppunt via poort doorsturen zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="7b927-390">This logs in toohello edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="7b927-391">Hoe Microsoft R Server uitoefening tooscale rekenknooppunten op HDInsight worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="7b927-391">How tooscale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-hello-worker-nodes"></a><span data-ttu-id="7b927-392">Hallo worker-knooppunten uit bedrijf nemen</span><span class="sxs-lookup"><span data-stu-id="7b927-392">Decommission hello worker node(s)</span></span>

<span data-ttu-id="7b927-393">Microsoft R Server wordt momenteel niet beheerd via Yarn.</span><span class="sxs-lookup"><span data-stu-id="7b927-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="7b927-394">Als Hallo worker-knooppunten niet buiten gebruik wordt gesteld, werkt Hallo Yarn Resource Manager niet zoals verwacht, omdat het niet op de hoogte van Hallo resources in beslag nemen Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="7b927-394">If hello worker nodes are not decommissioned, hello Yarn Resource Manager will not work as expected because it will not be aware of hello resources being taken up by hello server.</span></span> <span data-ttu-id="7b927-395">In de volgorde tooavoid deze situatie wordt aangeraden Hallo worker-knooppunten uit bedrijf nemen voordat u Hallo rekenknooppunten uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="7b927-395">In order tooavoid this situation, we recommend decommissioning hello worker nodes before you scale out hello compute nodes.</span></span>

<span data-ttu-id="7b927-396">Stappen toodecommissioning worker-knooppunten:</span><span class="sxs-lookup"><span data-stu-id="7b927-396">Steps toodecommissioning worker nodes:</span></span>

* <span data-ttu-id="7b927-397">Aanmelden van het cluster tooHDI Ambari-console en klikt u op het tabblad 'hosts'</span><span class="sxs-lookup"><span data-stu-id="7b927-397">Log in tooHDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="7b927-398">Worker-knooppunten (toobe buiten gebruik gesteld) selecteren, klikt u op 'Acties' > 'Geselecteerd Hosts' > "Hosts" > Klik op 'ON onderhoudsmodus inschakelen'.</span><span class="sxs-lookup"><span data-stu-id="7b927-398">Select worker nodes (toobe decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="7b927-399">We hebben bijvoorbeeld wn3 en wn4 toodecommission geselecteerd in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="7b927-399">For example, in hello following image we have selected wn3 and wn4 toodecommission.</span></span>  

   ![worker-knooppunten uit bedrijf nemen](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="7b927-401">Selecteer **Acties** > **Geselecteerde hosts** > **Datanodes** > klik op **Uit bedrijf nemen**</span><span class="sxs-lookup"><span data-stu-id="7b927-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="7b927-402">Selecteer **Acties** > **Geselecteerde hosts** > **NodeManagers** > klik op **Uit bedrijf nemen**</span><span class="sxs-lookup"><span data-stu-id="7b927-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="7b927-403">Selecteer **Acties** > **Geselecteerde hosts** > **Datanodes** > klik op **Stoppen**</span><span class="sxs-lookup"><span data-stu-id="7b927-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="7b927-404">Selecteer **Acties** > **Geselecteerde hosts** > **NodeManagers** > klik op **Stoppen**</span><span class="sxs-lookup"><span data-stu-id="7b927-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="7b927-405">Selecteer **Acties** > **Geselecteerde hosts** > **Hosts** > klik op **Alle onderdelen stoppen**</span><span class="sxs-lookup"><span data-stu-id="7b927-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="7b927-406">Hef de selectie Hallo worker-knooppunten en Hallo hoofdknooppunten selecteren</span><span class="sxs-lookup"><span data-stu-id="7b927-406">Unselect hello worker nodes and select hello head nodes</span></span>
* <span data-ttu-id="7b927-407">Selecteer **Acties** > **Geselecteerde hosts** > **Hosts** > **Alle onderdelen opnieuw starten**</span><span class="sxs-lookup"><span data-stu-id="7b927-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="7b927-408">Rekenknooppunten configureren op elk uit bedrijf genomen worker-knooppunt</span><span class="sxs-lookup"><span data-stu-id="7b927-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="7b927-409">SSH op elk uit bedrijf genomen werkknooppunt.</span><span class="sxs-lookup"><span data-stu-id="7b927-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="7b927-410">Voer het beheerprogramma uit met behulp van `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span><span class="sxs-lookup"><span data-stu-id="7b927-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="7b927-411">Voer '1' tooselect optie 'Configureren R Server voor uitoefening'.</span><span class="sxs-lookup"><span data-stu-id="7b927-411">Enter "1" tooselect option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="7b927-412">Geef "c" tooselect optie 'C.</span><span class="sxs-lookup"><span data-stu-id="7b927-412">Enter "c" tooselect option "C.</span></span> <span data-ttu-id="7b927-413">Rekenknooppunt te selecteren.</span><span class="sxs-lookup"><span data-stu-id="7b927-413">Compute node".</span></span> <span data-ttu-id="7b927-414">Hiermee configureert u Hallo-rekenknooppunt op hello werkrolknooppunt.</span><span class="sxs-lookup"><span data-stu-id="7b927-414">This configures hello compute node on hello worker node.</span></span>
5. <span data-ttu-id="7b927-415">Exit Hallo beheerder hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="7b927-415">Exit hello Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="7b927-416">Details van rekenknooppunten toevoegen op het webknooppunt</span><span class="sxs-lookup"><span data-stu-id="7b927-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="7b927-417">Zodra alle buiten gebruik gestelde worker-knooppunten zijn geconfigureerd toorun rekenknooppunt, keert u terug op Hallo edge-knooppunt en buiten gebruik gestelde worker-knooppunten IP-adressen in Hallo Microsoft web knooppunt op R Server de configuratie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7b927-417">Once all decommissioned worker nodes have been configured toorun compute node, come back on hello edge node and add decommissioned worker nodes' IP addresses in hello Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="7b927-418">SSH in Hallo edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7b927-418">SSH into hello edge node.</span></span>
* <span data-ttu-id="7b927-419">Voer `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json` uit.</span><span class="sxs-lookup"><span data-stu-id="7b927-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="7b927-420">Zoek naar de sectie 'URI' hello en werkrolknooppunt van IP- en poortgegevens toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7b927-420">Look for hello "URIs" section, and add worker node's IP and port details.</span></span>

    ![opdrachtregel worker-knooppunten uit bedrijf nemen](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="7b927-422">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="7b927-422">Troubleshoot</span></span>

<span data-ttu-id="7b927-423">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="7b927-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="7b927-424">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b927-424">Next steps</span></span>

<span data-ttu-id="7b927-425">Nu moet u begrijpen hoe een nieuwe HDInsight-cluster met Hallo R Server en Hallo basisbeginselen van toocreate Hallo R-console van een SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="7b927-425">Now you should understand how toocreate a new HDInsight cluster that includes hello R Server and hello basics of using hello R console from an SSH session.</span></span> <span data-ttu-id="7b927-426">Hallo volgende onderwerpen wordt uitgelegd andere manieren te beheren en werken met op HDInsight R Server:</span><span class="sxs-lookup"><span data-stu-id="7b927-426">hello following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="7b927-427">RStudio Server tooHDInsight toevoegen (indien niet geïnstalleerd tijdens het maken van de cluster)</span><span class="sxs-lookup"><span data-stu-id="7b927-427">Add RStudio Server tooHDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="7b927-428">Opties voor compute-context voor R Server op HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b927-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="7b927-429">Opties voor Azure-opslag voor R Server op HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b927-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
