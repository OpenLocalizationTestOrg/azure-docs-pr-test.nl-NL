---
title: RStudio met R Server op HDInsight - Azure installeren | Microsoft Docs
description: Klik hier voor meer informatie over het installeren van RStudio met op HDInsight R Server.
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 416420d855505508735ebd8526e93efdb230ad53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="6dc57-103">RStudio met op HDInsight R Server installeren</span><span class="sxs-lookup"><span data-stu-id="6dc57-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="6dc57-104">In dit artikel beschrijft het installeren van de community (gratis) versie van [RStudio Server](https://www.rstudio.com/products/rstudio-server/) op de edge-knooppunt van een cluster met een aangepast script.</span><span class="sxs-lookup"><span data-stu-id="6dc57-104">This article describes how to install the community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on the edge node of a cluster using a custom script.</span></span> <span data-ttu-id="6dc57-105">RStudio Server voorziet in een browser gebaseerde IDE voor gebruik door externe clients en wordt veel gebruikt op Linux.</span><span class="sxs-lookup"><span data-stu-id="6dc57-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="6dc57-106">Er zijn meerdere geïntegreerde ontwikkelomgevingen (IDE) beschikbaar voor R vandaag, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="6dc57-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="6dc57-107">Microsoft [R-Tools voor Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span><span class="sxs-lookup"><span data-stu-id="6dc57-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="6dc57-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="6dc57-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="6dc57-109">Walware de Eclipse gebaseerde [StatET](http://www.walware.de/goto/statet).</span><span class="sxs-lookup"><span data-stu-id="6dc57-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="6dc57-110">Het voordeel van RStudio Server installeren op de edge-knooppunt van een HDInsight-cluster is dat u een volledige IDE-ervaring voor de ontwikkeling en uitvoering van scripts R met R Server op het cluster.</span><span class="sxs-lookup"><span data-stu-id="6dc57-110">The advantage of installing RStudio Server on the edge node of an HDInsight cluster is that it provides a full IDE experience for the development and execution of R scripts with R Server on the cluster.</span></span> <span data-ttu-id="6dc57-111">Deze configuratie kunt productiever aanzienlijk dan standaard gebruik van de R-Console.</span><span class="sxs-lookup"><span data-stu-id="6dc57-111">This configuration can be considerably more productive than default use of the R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="6dc57-112">De procedure in dit artikel is alleen relevant als u geen RStudio Server community editie installeren tijdens het inrichten van uw cluster hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="6dc57-112">The procedure described in this article is only relevant if you did not select to install RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="6dc57-113">Als u dit hebt toegevoegd tijdens het inrichten en om deze te openen die u vervolgens op de **R Server Dashboards** tegel in de Azure portal-vermelding voor uw cluster, klik op de **R Studio Server** tegel.</span><span class="sxs-lookup"><span data-stu-id="6dc57-113">If you added it during provisioning, then to access it you click on the **R Server Dashboards** tile in the Azure portal entry for your cluster, then on the **R Studio Server** tile.</span></span> 

<span data-ttu-id="6dc57-114">Als u liever de commercieel gelicentieerde Pro-versie van RStudio Server te gebruiken, moet u de installatie-instructies uit volgen [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="6dc57-114">If you prefer to use the commercially licensed Pro version of RStudio Server, you must follow the installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="6dc57-115">Als u een HDInsight-cluster waarvoor R is geïnstalleerd met de [R scriptactie installeren](hdinsight-hadoop-r-scripts-linux.md), de stappen in dit document werkt niet correct ze nodig hebben een R Server op het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6dc57-115">If you are using an HDInsight cluster for which R was installed using the [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), the steps in this document will not work correctly as they require an R Server on the HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="6dc57-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6dc57-116">Prerequisites</span></span>

* <span data-ttu-id="6dc57-117">Een Azure HDInsight-cluster met R Server geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6dc57-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="6dc57-118">Zie voor instructies [aan de slag met R Server op HDInsight-clusters](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6dc57-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="6dc57-119">Een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="6dc57-119">An SSH client.</span></span> <span data-ttu-id="6dc57-120">Voor Linux en Unix-distributies of Macintosh OS X de `ssh` opdracht is opgegeven met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="6dc57-120">For Linux and Unix distributions or Macintosh OS X, the `ssh` command is provided with the operating system.</span></span> <span data-ttu-id="6dc57-121">Voor Windows, raden wij aan [Cygwin](http://www.redhat.com/services/custom/cygwin/) met de [OpenSSH-optie](https://www.youtube.com/watch?v=CwYSvvGaiWU), of [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="6dc57-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with the [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a><span data-ttu-id="6dc57-122">RStudio installeren op het cluster met een aangepast script</span><span class="sxs-lookup"><span data-stu-id="6dc57-122">Install RStudio on the cluster using a custom script</span></span>

<span data-ttu-id="6dc57-123">Dit zijn de stappen:</span><span class="sxs-lookup"><span data-stu-id="6dc57-123">Here are the steps:</span></span>

1. <span data-ttu-id="6dc57-124">Identificeer het edge-knooppunt van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6dc57-124">Identify the edge node of the cluster.</span></span> <span data-ttu-id="6dc57-125">Voor een HDInsight-cluster met R Server volgt de naamconventie voor het hoofdknooppunt en edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="6dc57-125">For an HDInsight cluster with R Server, following is the naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="6dc57-126">Hoofdknooppunt`CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="6dc57-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="6dc57-127">Edge-knooppunt`CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="6dc57-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="6dc57-128">Voeg SSH toe aan het edge-knooppunt van het cluster met behulp van het naamgevingspatroon vindt u in stap 1.</span><span class="sxs-lookup"><span data-stu-id="6dc57-128">SSH into the edge node of the cluster using the naming pattern provided in step 1.</span></span> <span data-ttu-id="6dc57-129">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6dc57-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="6dc57-130">Nadat u verbonden bent, worden een Hoofdgebruiker op het cluster.</span><span class="sxs-lookup"><span data-stu-id="6dc57-130">Once you are connected, become a root user on the cluster.</span></span> <span data-ttu-id="6dc57-131">In de SSH-sessie, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6dc57-131">In the SSH session, use the following command:</span></span>

        sudo su -

4. <span data-ttu-id="6dc57-132">De aangepaste scripts voor het installeren van RStudio downloaden.</span><span class="sxs-lookup"><span data-stu-id="6dc57-132">Download the custom script to install RStudio.</span></span> <span data-ttu-id="6dc57-133">Gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6dc57-133">Use the following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="6dc57-134">Wijzig de machtigingen voor het bestand aangepast script en voer het script.</span><span class="sxs-lookup"><span data-stu-id="6dc57-134">Change the permissions on the custom script file and run the script.</span></span> <span data-ttu-id="6dc57-135">Gebruik de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="6dc57-135">Use the following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="6dc57-136">Als u een SSH-wachtwoord tijdens het maken van een HDInsight-cluster met R Server gebruikt, kunt u deze stap overslaan en doorgaan naar de volgende.</span><span class="sxs-lookup"><span data-stu-id="6dc57-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed to the next.</span></span> <span data-ttu-id="6dc57-137">Als u een SSH-sleutel in plaats daarvan gebruikt om de cluster te maken, moet u een wachtwoord instellen voor uw SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6dc57-137">If you used an SSH key instead to create the cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="6dc57-138">U hebt dit wachtwoord nodig bij het verbinden met RStudio.</span><span class="sxs-lookup"><span data-stu-id="6dc57-138">You need this password when connecting to RStudio.</span></span> <span data-ttu-id="6dc57-139">Voer de volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="6dc57-139">Run the following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="6dc57-140">Als u wordt gevraagd **huidige Kerberos-wachtwoord**, drukt u op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="6dc57-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="6dc57-141">Let op: u moet vervangen `USERNAME` met een SSH-gebruiker voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6dc57-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="6dc57-142">Als u uw wachtwoord is ingesteld, ziet u het volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="6dc57-142">If your password is successfully set, you should see the following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="6dc57-143">De SSH-sessie af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="6dc57-143">Exit the SSH session.</span></span>

8. <span data-ttu-id="6dc57-144">Maken van een SSH-tunnel naar het cluster via het toewijzen van `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` op het HDInsight-cluster naar de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="6dc57-144">Create an SSH tunnel to the cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on the HDInsight cluster to the client machine.</span></span> <span data-ttu-id="6dc57-145">Voordat u een nieuwe browsersessie opent, moet u een SSH-tunnel maken.</span><span class="sxs-lookup"><span data-stu-id="6dc57-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="6dc57-146">Op een Linux-client of een Windows-client met [Cygwin](http://www.redhat.com/services/custom/cygwin/), open een terminalsessie en gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6dc57-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use the following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="6dc57-147">Vervang **gebruikersnaam** met een SSH-gebruiker voor uw HDInsight-cluster en vervang **CLUSTERNAME** met de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6dc57-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>
       <span data-ttu-id="6dc57-148">U kunt ook een SSH-sleutel in plaats van een wachtwoord gebruiken door toe te voegen `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="6dc57-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="6dc57-149">Als een Windows-client met PuTTY vervolgens</span><span class="sxs-lookup"><span data-stu-id="6dc57-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="6dc57-150">PuTTY opent en voert u de verbindingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="6dc57-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="6dc57-151">In de **categorie** sectie aan de linkerkant van het dialoogvenster uit, vouw **verbinding**, vouw **SSH**, en selecteer vervolgens **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="6dc57-151">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="6dc57-152">Geef de volgende informatie op de **opties voor SSH-poort doorsturen** vorm:</span><span class="sxs-lookup"><span data-stu-id="6dc57-152">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="6dc57-153">**Bronpoort**: de poort op de client die u wilt doorsturen.</span><span class="sxs-lookup"><span data-stu-id="6dc57-153">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="6dc57-154">Bijvoorbeeld: **8787**.</span><span class="sxs-lookup"><span data-stu-id="6dc57-154">For example, **8787**.</span></span>
        * <span data-ttu-id="6dc57-155">**Bestemming** -de bestemming die moet worden toegewezen aan de lokale clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="6dc57-155">**Destination** - The destination that must be mapped to the local client machine.</span></span> <span data-ttu-id="6dc57-156">Bijvoorbeeld: **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="6dc57-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="6dc57-157">![Maken van een SSH-tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "maken van een SSH-tunnel")</span><span class="sxs-lookup"><span data-stu-id="6dc57-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="6dc57-158">Klik op **toevoegen** toevoegen van de instellingen en klik vervolgens op **openen** een SSH-verbinding openen.</span><span class="sxs-lookup"><span data-stu-id="6dc57-158">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>
     5. <span data-ttu-id="6dc57-159">Wanneer u wordt gevraagd, moet u zich aanmelden bij de server voor het maken van een SSH-sessie de tunnel ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6dc57-159">When prompted, log in to the server to establish an SSH session and enable the tunnel.</span></span>

9. <span data-ttu-id="6dc57-160">Open een webbrowser en voer de volgende URL op basis van de poort die u hebt ingevoerd voor de tunnel:</span><span class="sxs-lookup"><span data-stu-id="6dc57-160">Open a web browser and enter the following URL based on the port you entered for the tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="6dc57-161">U wordt gevraagd naar de SSH-gebruikersnaam en wachtwoord opgeven om verbinding met het cluster.</span><span class="sxs-lookup"><span data-stu-id="6dc57-161">You are prompted to enter the SSH username and password to connect to the cluster.</span></span> <span data-ttu-id="6dc57-162">Als u een SSH-sleutel gebruikt bij het maken van het cluster, moet u het wachtwoord dat u in stap 5 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6dc57-162">If you used an SSH key while creating the cluster, you must enter the password you created in step 5.</span></span>

    <span data-ttu-id="6dc57-163">![Verbinding maken met R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "maken van een SSH-tunnel")</span><span class="sxs-lookup"><span data-stu-id="6dc57-163">![Connect to R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="6dc57-164">Als u wilt testen of de RStudio-installatie voltooid is, kunt u een testscript dat wordt uitgevoerd op basis van R MapReduce en Spark taken op het cluster kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6dc57-164">To test whether the RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on the cluster.</span></span> <span data-ttu-id="6dc57-165">Het testscript in RStudio uit te voeren downloaden, gaat u terug naar de SSH-console en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="6dc57-165">To download the test script to run in RStudio, go back to the SSH console and enter the following commands:</span></span>

    *    <span data-ttu-id="6dc57-166">Als u een Hadoop-cluster met R gemaakt, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="6dc57-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="6dc57-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="6dc57-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="6dc57-168">Als u een Spark-cluster met R gemaakt, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="6dc57-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="6dc57-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="6dc57-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="6dc57-170">In RStudio ziet u het testscript die u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="6dc57-170">In RStudio, you see the test script you downloaded.</span></span> <span data-ttu-id="6dc57-171">Dubbelklik op het bestand te openen, selecteert u de inhoud van het bestand en klik vervolgens op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="6dc57-171">Double-click the file to open it, select the contents of the file, and then click **Run**.</span></span> <span data-ttu-id="6dc57-172">U ziet de uitvoer in de **Console** deelvenster:</span><span class="sxs-lookup"><span data-stu-id="6dc57-172">You should see the output in the **Console** pane:</span></span>

   <span data-ttu-id="6dc57-173">![De installatie testen](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "de installatie testen")</span><span class="sxs-lookup"><span data-stu-id="6dc57-173">![Test the installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test the installation")</span></span>

<span data-ttu-id="6dc57-174">Een andere optie zou worden naar het type `source(testhdi.r)` of `source(testhdi_spark.r)` het script wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6dc57-174">Another option would be to type `source(testhdi.r)` or `source(testhdi_spark.r)` to execute the script.</span></span>

## <a name="see-also"></a><span data-ttu-id="6dc57-175">Zie ook</span><span class="sxs-lookup"><span data-stu-id="6dc57-175">See also</span></span>

* [<span data-ttu-id="6dc57-176">COMPUTE context opties voor R Server op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="6dc57-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="6dc57-177">Opties voor Azure-opslag voor R Server op HDInsight</span><span class="sxs-lookup"><span data-stu-id="6dc57-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

