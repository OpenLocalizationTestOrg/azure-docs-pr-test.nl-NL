---
title: aaaInstall RStudio met R Server op een HDInsight - Azure | Microsoft Docs
description: Hoe tooinstall RStudio met op HDInsight R Server.
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
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="2c9d8-103">RStudio met op HDInsight R Server installeren</span><span class="sxs-lookup"><span data-stu-id="2c9d8-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="2c9d8-104">Dit artikel wordt beschreven hoe tooinstall community (gratis) versie van Hallo [RStudio Server](https://www.rstudio.com/products/rstudio-server/) op Hallo edge-knooppunt van een cluster met een aangepast script.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-104">This article describes how tooinstall hello community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on hello edge node of a cluster using a custom script.</span></span> <span data-ttu-id="2c9d8-105">RStudio Server voorziet in een browser gebaseerde IDE voor gebruik door externe clients en wordt veel gebruikt op Linux.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="2c9d8-106">Er zijn meerdere geïntegreerde ontwikkelomgevingen (IDE) beschikbaar voor R vandaag, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="2c9d8-107">Microsoft [R-Tools voor Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span><span class="sxs-lookup"><span data-stu-id="2c9d8-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="2c9d8-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="2c9d8-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="2c9d8-109">Walware de Eclipse gebaseerde [StatET](http://www.walware.de/goto/statet).</span><span class="sxs-lookup"><span data-stu-id="2c9d8-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="2c9d8-110">Hallo profiteren van RStudio Server installeren op Hallo edge-knooppunt van een HDInsight-cluster is dat u een volledige IDE-ervaring voor Hallo ontwikkeling en uitvoering van scripts R met R Server op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-110">hello advantage of installing RStudio Server on hello edge node of an HDInsight cluster is that it provides a full IDE experience for hello development and execution of R scripts with R Server on hello cluster.</span></span> <span data-ttu-id="2c9d8-111">Deze configuratie kunt productiever aanzienlijk dan standaard gebruik van Hallo R-Console.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-111">This configuration can be considerably more productive than default use of hello R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="2c9d8-112">Hallo-procedure wordt beschreven in dit artikel is alleen relevant als u geen tooinstall RStudio Server community edition hebt geselecteerd bij het inrichten van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-112">hello procedure described in this article is only relevant if you did not select tooinstall RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="2c9d8-113">Als u dit hebt toegevoegd tijdens het inrichten, klikt u vervolgens tooaccess deze u klikt u op Hallo **R Server Dashboards** tegel in Azure portal-vermelding voor uw cluster, klikt u op Hallo Hallo **R Studio Server** tegel.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-113">If you added it during provisioning, then tooaccess it you click on hello **R Server Dashboards** tile in hello Azure portal entry for your cluster, then on hello **R Studio Server** tile.</span></span> 

<span data-ttu-id="2c9d8-114">Als u liever toouse Hallo commercieel in licentie gegeven Pro-versie van RStudio Server, moet u installatie-instructies Hallo van volgen [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span><span class="sxs-lookup"><span data-stu-id="2c9d8-114">If you prefer toouse hello commercially licensed Pro version of RStudio Server, you must follow hello installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="2c9d8-115">Als u een HDInsight-cluster waarvoor R is geïnstalleerd met behulp van Hallo [R scriptactie installeren](hdinsight-hadoop-r-scripts-linux.md), Hallo stappen in dit document werkt niet correct ze nodig hebben een R Server op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-115">If you are using an HDInsight cluster for which R was installed using hello [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), hello steps in this document will not work correctly as they require an R Server on hello HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="2c9d8-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2c9d8-116">Prerequisites</span></span>

* <span data-ttu-id="2c9d8-117">Een Azure HDInsight-cluster met R Server geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="2c9d8-118">Zie voor instructies [aan de slag met R Server op HDInsight-clusters](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2c9d8-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="2c9d8-119">Een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-119">An SSH client.</span></span> <span data-ttu-id="2c9d8-120">Voor Linux en Unix-distributies of Macintosh OS X, Hallo `ssh` opdracht wordt verstrekt met Hallo-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-120">For Linux and Unix distributions or Macintosh OS X, hello `ssh` command is provided with hello operating system.</span></span> <span data-ttu-id="2c9d8-121">Voor Windows, raden wij aan [Cygwin](http://www.redhat.com/services/custom/cygwin/) Hello [OpenSSH-optie](https://www.youtube.com/watch?v=CwYSvvGaiWU), of [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="2c9d8-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a><span data-ttu-id="2c9d8-122">RStudio installeren op Hallo-cluster met een aangepast script</span><span class="sxs-lookup"><span data-stu-id="2c9d8-122">Install RStudio on hello cluster using a custom script</span></span>

<span data-ttu-id="2c9d8-123">Hier volgen Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-123">Here are hello steps:</span></span>

1. <span data-ttu-id="2c9d8-124">Edge-knooppunt op Hallo van Hallo cluster identificeren.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-124">Identify hello edge node of hello cluster.</span></span> <span data-ttu-id="2c9d8-125">Voor een HDInsight-cluster met R Server volgt Hallo naamgevingsconventie voor hoofdknooppunt en edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-125">For an HDInsight cluster with R Server, following is hello naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="2c9d8-126">Hoofdknooppunt`CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="2c9d8-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="2c9d8-127">Edge-knooppunt`CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="2c9d8-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="2c9d8-128">SSH in edge-knooppunt op Hallo van Hallo-cluster met behulp van een naamgevingspatroon Hallo vindt u in stap 1.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-128">SSH into hello edge node of hello cluster using hello naming pattern provided in step 1.</span></span> <span data-ttu-id="2c9d8-129">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="2c9d8-130">Nadat u verbonden bent, worden een Hoofdgebruiker op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-130">Once you are connected, become a root user on hello cluster.</span></span> <span data-ttu-id="2c9d8-131">In Hallo SSH-sessie, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-131">In hello SSH session, use hello following command:</span></span>

        sudo su -

4. <span data-ttu-id="2c9d8-132">Hallo aangepast script tooinstall RStudio downloaden.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-132">Download hello custom script tooinstall RStudio.</span></span> <span data-ttu-id="2c9d8-133">Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-133">Use hello following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="2c9d8-134">Hallo-machtigingen voor Hallo aangepast scriptbestand wijzigen en Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-134">Change hello permissions on hello custom script file and run hello script.</span></span> <span data-ttu-id="2c9d8-135">Hallo volgende opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-135">Use hello following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="2c9d8-136">Als u een SSH-wachtwoord tijdens het maken van een HDInsight-cluster met R Server gebruikt, kunt u deze stap overslaan en doorgaan toohello naast.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed toohello next.</span></span> <span data-ttu-id="2c9d8-137">Als u een SSH-sleutel in plaats daarvan toocreate Hallo cluster gebruikt, moet u een wachtwoord instellen voor uw SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-137">If you used an SSH key instead toocreate hello cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="2c9d8-138">U hebt dit wachtwoord nodig om verbinding te maken tooRStudio.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-138">You need this password when connecting tooRStudio.</span></span> <span data-ttu-id="2c9d8-139">Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-139">Run hello following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="2c9d8-140">Als u wordt gevraagd **huidige Kerberos-wachtwoord**, drukt u op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="2c9d8-141">Let op: u moet vervangen `USERNAME` met een SSH-gebruiker voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="2c9d8-142">Als uw wachtwoord is correct ingesteld, worden er Hallo volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-142">If your password is successfully set, you should see hello following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="2c9d8-143">Hallo SSH-sessie af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-143">Exit hello SSH session.</span></span>

8. <span data-ttu-id="2c9d8-144">Maken van een SSH-tunnel toohello cluster door toe te wijzen `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` op Hallo HDInsight cluster toohello client-computer.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-144">Create an SSH tunnel toohello cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on hello HDInsight cluster toohello client machine.</span></span> <span data-ttu-id="2c9d8-145">Voordat u een nieuwe browsersessie opent, moet u een SSH-tunnel maken.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="2c9d8-146">Op een Linux-client of een Windows-client met [Cygwin](http://www.redhat.com/services/custom/cygwin/), open een terminalsessie en gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use hello following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="2c9d8-147">Vervang **gebruikersnaam** met een SSH-gebruiker voor uw HDInsight-cluster en vervang **CLUSTERNAME** met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>
       <span data-ttu-id="2c9d8-148">U kunt ook een SSH-sleutel in plaats van een wachtwoord gebruiken door toe te voegen `-i id_rsa_key`.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="2c9d8-149">Als een Windows-client met PuTTY vervolgens</span><span class="sxs-lookup"><span data-stu-id="2c9d8-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="2c9d8-150">PuTTY opent en voert u de verbindingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="2c9d8-151">In Hallo **categorie** sectie toohello links van dialoogvenster hello, vouw **verbinding**, vouw **SSH**, en selecteer vervolgens **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-151">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="2c9d8-152">Bieden de volgende informatie op Hallo Hallo **opties voor SSH-poort doorsturen** vorm:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-152">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="2c9d8-153">**Bronpoort** -Hallo poort op de gewenste tooforward Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-153">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="2c9d8-154">Bijvoorbeeld: **8787**.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-154">For example, **8787**.</span></span>
        * <span data-ttu-id="2c9d8-155">**Bestemming** - hello doel dat moet worden toegewezen toohello lokale client-computer.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-155">**Destination** - hello destination that must be mapped toohello local client machine.</span></span> <span data-ttu-id="2c9d8-156">Bijvoorbeeld: **localhost:8787**.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="2c9d8-157">![Maken van een SSH-tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "maken van een SSH-tunnel")</span><span class="sxs-lookup"><span data-stu-id="2c9d8-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="2c9d8-158">Klik op **toevoegen** tooadd Hallo instellingen en klik vervolgens op **Open** tooopen een SSH-verbinding.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-158">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>
     5. <span data-ttu-id="2c9d8-159">Meld u desgevraagd in toohello server tooestablish een SSH-sessie en schakel Hallo-tunnel.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-159">When prompted, log in toohello server tooestablish an SSH session and enable hello tunnel.</span></span>

9. <span data-ttu-id="2c9d8-160">Open een webbrowser en voert u Hallo URL op basis van Hallo-poort die u hebt opgegeven voor het Hallo-tunnel te volgen:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-160">Open a web browser and enter hello following URL based on hello port you entered for hello tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="2c9d8-161">U bent na vragen aan gebruiker tooenter Hallo SSH gebruikersnaam en wachtwoord tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-161">You are prompted tooenter hello SSH username and password tooconnect toohello cluster.</span></span> <span data-ttu-id="2c9d8-162">Als u een SSH-sleutel gebruikt tijdens het Hallo-cluster maken, moet u Hallo wachtwoord dat u in stap 5 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-162">If you used an SSH key while creating hello cluster, you must enter hello password you created in step 5.</span></span>

    <span data-ttu-id="2c9d8-163">![Rondleiding Studio verbinding](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "maken van een SSH-tunnel")</span><span class="sxs-lookup"><span data-stu-id="2c9d8-163">![Connect tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="2c9d8-164">tootest of Hallo RStudio installatie voltooid is, kunt u een testscript dat wordt uitgevoerd op basis van R MapReduce en Spark taken op Hallo cluster kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-164">tootest whether hello RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on hello cluster.</span></span> <span data-ttu-id="2c9d8-165">toodownload hello test script toorun in RStudio, Ga terug toohello SSH-console en Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-165">toodownload hello test script toorun in RStudio, go back toohello SSH console and enter hello following commands:</span></span>

    *    <span data-ttu-id="2c9d8-166">Als u een Hadoop-cluster met R gemaakt, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="2c9d8-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="2c9d8-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="2c9d8-168">Als u een Spark-cluster met R gemaakt, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="2c9d8-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="2c9d8-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="2c9d8-170">U ziet in RStudio, Hallo testen script die u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-170">In RStudio, you see hello test script you downloaded.</span></span> <span data-ttu-id="2c9d8-171">Dubbelklik op Hallo bestand tooopen, selecteert u de inhoud Hallo van Hallo-bestand en klik vervolgens op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-171">Double-click hello file tooopen it, select hello contents of hello file, and then click **Run**.</span></span> <span data-ttu-id="2c9d8-172">Hallo-uitvoer in Hallo **Console** deelvenster:</span><span class="sxs-lookup"><span data-stu-id="2c9d8-172">You should see hello output in hello **Console** pane:</span></span>

   <span data-ttu-id="2c9d8-173">![Hallo-installatie testen](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Hallo-installatie testen")</span><span class="sxs-lookup"><span data-stu-id="2c9d8-173">![Test hello installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello installation")</span></span>

<span data-ttu-id="2c9d8-174">Een andere optie zijn tootype `source(testhdi.r)` of `source(testhdi_spark.r)` tooexecute Hallo script.</span><span class="sxs-lookup"><span data-stu-id="2c9d8-174">Another option would be tootype `source(testhdi.r)` or `source(testhdi_spark.r)` tooexecute hello script.</span></span>

## <a name="see-also"></a><span data-ttu-id="2c9d8-175">Zie ook</span><span class="sxs-lookup"><span data-stu-id="2c9d8-175">See also</span></span>

* [<span data-ttu-id="2c9d8-176">COMPUTE context opties voor R Server op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="2c9d8-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="2c9d8-177">Opties voor Azure-opslag voor R Server op HDInsight</span><span class="sxs-lookup"><span data-stu-id="2c9d8-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

