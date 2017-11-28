---
title: lokaal aaaInstall Jupyter & verbinding maken met tooan Azure HDInsight Spark-cluster | Microsoft Docs
description: Meer informatie over hoe tooinstall Jupyter-notebook lokaal op uw computer en sluit het tooan Apache Spark-cluster in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a><span data-ttu-id="8fccc-103">Jupyter-notebook installeert op uw computer en sluit u tooApache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fccc-103">Install Jupyter notebook on your computer and connect tooApache Spark on HDInsight</span></span>

<span data-ttu-id="8fccc-104">In dit artikel leert u hoe tooinstall Jupyter-notebook Hello aangepaste PySpark (voor Python) en Spark (voor Scala) kernels met Spark magic, en koppel Hallo notebook tooan HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8fccc-104">In this article you learn how tooinstall Jupyter notebook, with hello custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect hello notebook tooan HDInsight cluster.</span></span> <span data-ttu-id="8fccc-105">Er is een aantal redenen tooinstall Jupyter op uw lokale computer en kunnen er ook enkele uitdagingen.</span><span class="sxs-lookup"><span data-stu-id="8fccc-105">There can be a number of reasons tooinstall Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="8fccc-106">Zie voor meer informatie over dit Hallo sectie [waarom zou ik Jupyter installeren op mijn computer](#why-should-i-install-jupyter-on-my-computer) aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8fccc-106">For more on this, see hello section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at hello end of this article.</span></span>

<span data-ttu-id="8fccc-107">Er zijn drie belangrijke stappen die betrokken zijn bij het installeren van Jupyter en Hallo Spark magic op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8fccc-107">There are three key steps involved in installing Jupyter and hello Spark magic on your computer.</span></span>

* <span data-ttu-id="8fccc-108">Jupyter-notebook installeren</span><span class="sxs-lookup"><span data-stu-id="8fccc-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="8fccc-109">Hallo PySpark en Spark kernels Hello Spark verwerkt Magic-pakket installeren</span><span class="sxs-lookup"><span data-stu-id="8fccc-109">Install hello PySpark and Spark kernels with hello Spark magic</span></span>
* <span data-ttu-id="8fccc-110">Spark magische tooaccess Spark-cluster in HDInsight configureren</span><span class="sxs-lookup"><span data-stu-id="8fccc-110">Configure Spark magic tooaccess Spark cluster on HDInsight</span></span>

<span data-ttu-id="8fccc-111">Zie voor meer informatie over aangepaste kernels Hallo en Hallo Spark magic beschikbaar voor Jupyter-notebooks met HDInsight-cluster [beschikbare Kernels voor Jupyter-notebooks met Apache Spark Linux-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="8fccc-111">For more information about hello custom kernels and hello Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fccc-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8fccc-112">Prerequisites</span></span>
<span data-ttu-id="8fccc-113">Hallo-vereisten die hier worden vermeld, zijn niet voor het installeren van Jupyter.</span><span class="sxs-lookup"><span data-stu-id="8fccc-113">hello prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="8fccc-114">Dit zijn voor maken van verbinding Hallo Jupyter-notebook tooan HDInsight-cluster nadat Hallo notebook is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8fccc-114">These are for connecting hello Jupyter notebook tooan HDInsight cluster once hello notebook is installed.</span></span>

* <span data-ttu-id="8fccc-115">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8fccc-115">An Azure subscription.</span></span> <span data-ttu-id="8fccc-116">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8fccc-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="8fccc-117">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8fccc-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="8fccc-118">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8fccc-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="8fccc-119">Jupyter-notebook op uw computer installeren</span><span class="sxs-lookup"><span data-stu-id="8fccc-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="8fccc-120">Voordat u de Jupyter-notebooks kunt installeren, moet u Python installeren.</span><span class="sxs-lookup"><span data-stu-id="8fccc-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="8fccc-121">Zowel Python en Jupyter zijn beschikbaar als onderdeel van Hallo [Anaconda distributie](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="8fccc-121">Both Python and Jupyter are available as part of hello [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="8fccc-122">Als u Anaconda installeert, installeert u een distributiepunt van Python.</span><span class="sxs-lookup"><span data-stu-id="8fccc-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="8fccc-123">Nadat Anaconda is geïnstalleerd, voegt u Hallo Jupyter installatie door de juiste opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8fccc-123">Once Anaconda is installed, you add hello Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="8fccc-124">Hallo downloaden [Anaconda-installatieprogramma](https://www.continuum.io/downloads) voor uw platform en Voer Hallo setup.</span><span class="sxs-lookup"><span data-stu-id="8fccc-124">Download hello [Anaconda installer](https://www.continuum.io/downloads) for your platform and run hello setup.</span></span> <span data-ttu-id="8fccc-125">Tijdens het actieve Hallo-installatiewizard, moet dat u Hallo optie tooadd Anaconda tooyour padvariabele selecteren.</span><span class="sxs-lookup"><span data-stu-id="8fccc-125">While running hello setup wizard, make sure you select hello option tooadd Anaconda tooyour PATH variable.</span></span>
2. <span data-ttu-id="8fccc-126">Hallo na de opdracht tooinstall Jupyter worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8fccc-126">Run hello following command tooinstall Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="8fccc-127">Zie voor meer informatie over het installeren van Jupyter [installeren Jupyter met Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="8fccc-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-hello-kernels-and-spark-magic"></a><span data-ttu-id="8fccc-128">Hallo kernels en Spark verwerkt Magic-pakket installeren</span><span class="sxs-lookup"><span data-stu-id="8fccc-128">Install hello kernels and Spark magic</span></span>

<span data-ttu-id="8fccc-129">Voor instructies over hoe tooinstall Hallo Spark magic, Hallo PySpark en Spark-kernels Hallo installatie-instructies in Hallo volgen [sparkmagic documentatie](https://github.com/jupyter-incubator/sparkmagic#installation) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="8fccc-129">For instructions on how tooinstall hello Spark magic, hello PySpark and Spark kernels, follow hello installation instructions in hello [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="8fccc-130">Hallo eerste stap bij het Hallo Spark magische documentatie wordt u gevraagd tooinstall Spark magic.</span><span class="sxs-lookup"><span data-stu-id="8fccc-130">hello first step in hello Spark magic documentation asks you tooinstall Spark magic.</span></span> <span data-ttu-id="8fccc-131">Deze eerste stap bij het Hallo-koppeling vervangen door Hallo-opdrachten, afhankelijk van de versie Hallo van Hallo maakt u verbinding met HDInsight-cluster te volgen.</span><span class="sxs-lookup"><span data-stu-id="8fccc-131">Replace that first step in hello link with hello following commands, depending on hello version of hello HDInsight cluster you will connect to.</span></span> <span data-ttu-id="8fccc-132">Volg daarna Hallo resterende stappen in Hallo Spark magische documentatie.</span><span class="sxs-lookup"><span data-stu-id="8fccc-132">After that, follow hello remaining steps in hello Spark magic documentation.</span></span> <span data-ttu-id="8fccc-133">Als u wilt dat tooinstall Hallo verschillende kernels, voert u stap 3 in Hallo sectie Spark magische installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="8fccc-133">If you want tooinstall hello different kernels, you must perform Step 3 in hello Spark magic installation instructions section.</span></span>

* <span data-ttu-id="8fccc-134">Voor clusters v3.4, installeert u sparkmagic 0.2.3 door te voeren`pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="8fccc-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="8fccc-135">Installeren voor clusters v3.5 en v3.6 sparkmagic 0.11.2 door`pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="8fccc-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a><span data-ttu-id="8fccc-136">Spark magische tooconnect tooHDInsight Spark-cluster configureren</span><span class="sxs-lookup"><span data-stu-id="8fccc-136">Configure Spark magic tooconnect tooHDInsight Spark cluster</span></span>

<span data-ttu-id="8fccc-137">In deze sectie configureert u Hallo Spark magic die u eerder tooconnect tooan Apache Spark-cluster dat moet u al hebt gemaakt in Azure HDInsight geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8fccc-137">In this section you configure hello Spark magic that you installed earlier tooconnect tooan Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="8fccc-138">Hallo Jupyter-configuratie-informatie wordt meestal opgeslagen in de basismap Hallo-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8fccc-138">hello Jupyter configuration information is typically stored in hello users home directory.</span></span> <span data-ttu-id="8fccc-139">de opdrachten toolocate uw basismap op een besturingssysteem of platform, type hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="8fccc-139">toolocate your home directory on any OS platform, type hello following commands.</span></span>

    <span data-ttu-id="8fccc-140">Hallo Python shell starten.</span><span class="sxs-lookup"><span data-stu-id="8fccc-140">Start hello Python shell.</span></span> <span data-ttu-id="8fccc-141">Typ op een opdrachtvenster Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="8fccc-141">On a command window, type hello following:</span></span>

        python

    <span data-ttu-id="8fccc-142">Voer op Hallo Python-shell, Hallo toofind opdracht out Hallo basismap te volgen.</span><span class="sxs-lookup"><span data-stu-id="8fccc-142">On hello Python shell, enter hello following command toofind out hello home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="8fccc-143">Navigeer toohello basismap en maak een map **.sparkmagic** als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="8fccc-143">Navigate toohello home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="8fccc-144">Maak een bestand met de naam in de map Hallo, **config.json** en Hallo JSON-fragment in het volgende toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="8fccc-144">Within hello folder, create a file called **config.json** and add hello following JSON snippet inside it.</span></span>

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. <span data-ttu-id="8fccc-145">Vervang **{USERNAME}**, **{CLUSTERDNSNAME}**, en **{BASE64ENCODEDPASSWORD}** met de juiste waarden.</span><span class="sxs-lookup"><span data-stu-id="8fccc-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="8fccc-146">U kunt een aantal hulpprogramma's in uw favoriete programmeertaal of online toogenerate een met base64 gecodeerde wachtwoord gebruiken om uw huidige wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="8fccc-146">You can use a number of utilities in your favorite programming language or online toogenerate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="8fccc-147">Hallo rechts heartbeatinstellingen configureren in `config.json`.</span><span class="sxs-lookup"><span data-stu-id="8fccc-147">Configure hello right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="8fccc-148">U moet deze instellingen toevoegen op hetzelfde niveau als Hallo Hallo `kernel_python_credentials` en `kernel_scala_credentials` codefragmenten uw toegevoegde eerder.</span><span class="sxs-lookup"><span data-stu-id="8fccc-148">You should add these settings at hello same level as hello `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="8fccc-149">Zie voor een voorbeeld van hoe en waar tooadd heartbeat-instellingen Hallo [voorbeeld config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="8fccc-149">For an example on how and where tooadd hello heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="8fccc-150">Voor `sparkmagic 0.2.3` (clusters met v3.4) omvatten:</span><span class="sxs-lookup"><span data-stu-id="8fccc-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="8fccc-151">Voor `sparkmagic 0.11.2` (clusters v3.5 en v3.6), zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="8fccc-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="8fccc-152">Heartbeats worden verzonden tooensure sessies niet gelekt.</span><span class="sxs-lookup"><span data-stu-id="8fccc-152">Heartbeats are sent tooensure that sessions are not leaked.</span></span> <span data-ttu-id="8fccc-153">Wanneer een computer toosleep gaat of wordt afgesloten, Hallo heartbeat is niet verzonden, wat resulteert in het Hallo-sessie wordt opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="8fccc-153">When a computer goes toosleep or is shut down, hello heartbeat is not sent, resulting in hello session being cleaned up.</span></span> <span data-ttu-id="8fccc-154">Voor clusters v3.4, indien toodisable dit gedrag gewenst kunt u instellen Hallo Livy config `livy.server.interactive.heartbeat.timeout` te`0` van Hallo Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="8fccc-154">For clusters v3.4, if you wish toodisable this behavior, you can set hello Livy config `livy.server.interactive.heartbeat.timeout` too`0` from hello Ambari UI.</span></span> <span data-ttu-id="8fccc-155">Voor clusters v3.5, als u geen Hallo 3.5 configuratie bovenstaande instelt worden Hallo sessie niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8fccc-155">For clusters v3.5, if you do not set hello 3.5 configuration above, hello session will not be deleted.</span></span>

6. <span data-ttu-id="8fccc-156">Jupyter starten.</span><span class="sxs-lookup"><span data-stu-id="8fccc-156">Start Jupyter.</span></span> <span data-ttu-id="8fccc-157">Gebruiken de volgende opdracht uit via de opdrachtprompt Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8fccc-157">Use hello following command from hello command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="8fccc-158">Controleer of u kunt verbinding maken met Jupyter-notebook Hallo en dat u kunt Hallo Spark magic beschikbaar met Hallo kernels toohello-cluster.</span><span class="sxs-lookup"><span data-stu-id="8fccc-158">Verify that you can connect toohello cluster using hello Jupyter notebook and that you can use hello Spark magic available with hello kernels.</span></span> <span data-ttu-id="8fccc-159">Hallo stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8fccc-159">Perform hello following steps.</span></span>

    <span data-ttu-id="8fccc-160">a.</span><span class="sxs-lookup"><span data-stu-id="8fccc-160">a.</span></span> <span data-ttu-id="8fccc-161">Maak een nieuwe notebook.</span><span class="sxs-lookup"><span data-stu-id="8fccc-161">Create a new notebook.</span></span> <span data-ttu-id="8fccc-162">Vanuit de rechterhoek hello, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="8fccc-162">From hello right-hand corner, click **New**.</span></span> <span data-ttu-id="8fccc-163">U ziet Hallo standaard kernel **Python2** en twee nieuwe kernels die u installeert, Hallo **PySpark** en **Spark**.</span><span class="sxs-lookup"><span data-stu-id="8fccc-163">You should see hello default kernel **Python2** and hello two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="8fccc-164">Klik op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="8fccc-164">Click **PySpark**.</span></span>

    <span data-ttu-id="8fccc-165">![Kernels in Jupyter-notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter-notebook")</span><span class="sxs-lookup"><span data-stu-id="8fccc-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="8fccc-166">b.</span><span class="sxs-lookup"><span data-stu-id="8fccc-166">b.</span></span> <span data-ttu-id="8fccc-167">Hallo volgende codefragment worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8fccc-167">Run hello following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="8fccc-168">Als u Hallo uitvoer met succes ophalen kunt, wordt uw verbinding toohello HDInsight-cluster getest.</span><span class="sxs-lookup"><span data-stu-id="8fccc-168">If you can successfully retrieve hello output, your connection toohello HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="8fccc-169">Als u tooupdate Hallo notebook configuratie tooconnect tooa naar een cluster wilt, moet u Hallo config.json bijwerken met Hallo nieuwe set waarden, zoals u in stap 3 hierboven.</span><span class="sxs-lookup"><span data-stu-id="8fccc-169">If you want tooupdate hello notebook configuration tooconnect tooa different cluster, update hello config.json with hello new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="8fccc-170">Waarom zou ik Jupyter installeren op mijn computer?</span><span class="sxs-lookup"><span data-stu-id="8fccc-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="8fccc-171">Er is een getal van redenen waarom u mogelijk tooinstall Jupyter op uw computer wilt en klikt u vervolgens verbinding maken met tooa Spark in HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8fccc-171">There can be a number of reasons why you might want tooinstall Jupyter on your computer and then connect it tooa Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="8fccc-172">Hoewel Jupyter-notebooks al beschikbaar op Hallo Spark-cluster in Azure HDInsight zijn, biedt Jupyter installeert op uw computer u Hallo optie toocreate uw notitieblokken lokaal, uw toepassing testen op een actief cluster en vervolgens uploaden Hallo laptops toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="8fccc-172">Even though Jupyter notebooks are already available on hello Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you hello option toocreate your notebooks locally, test your application against a running cluster, and then upload hello notebooks toohello cluster.</span></span> <span data-ttu-id="8fccc-173">tooupload hello notitieblokken toohello cluster, kunt u ofwel uploaden dat ze met behulp van Hallo Jupyter-notebook die wordt uitgevoerd of Hallo cluster of toohello /HdiNotebooks map opslaan in Hallo storage-account is gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8fccc-173">tooupload hello notebooks toohello cluster, you can either upload them using hello Jupyter notebook that is running or hello cluster, or save them toohello /HdiNotebooks folder in hello storage account associated with hello cluster.</span></span> <span data-ttu-id="8fccc-174">Zie voor meer informatie over hoe notitieblokken op Hallo cluster worden opgeslagen, [waar zijn Jupyter-notebooks opgeslagen](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="8fccc-174">For more information on how notebooks are stored on hello cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="8fccc-175">Met Hallo-laptops beschikbaar lokaal, kunt u toodifferent Spark-clusters op basis van uw vereisten voor toepassingsimplementatie.</span><span class="sxs-lookup"><span data-stu-id="8fccc-175">With hello notebooks available locally, you can connect toodifferent Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="8fccc-176">U kunt GitHub tooimplement een bronbeheersysteem en versiebeheer voor Hallo notitieblokken hebt.</span><span class="sxs-lookup"><span data-stu-id="8fccc-176">You can use GitHub tooimplement a source control system and have version control for hello notebooks.</span></span> <span data-ttu-id="8fccc-177">U kunt ook een samenwerkingsomgeving waar meerdere gebruikers met Hallo dezelfde werken kunnen hebben notebook.</span><span class="sxs-lookup"><span data-stu-id="8fccc-177">You can also have a collaborative environment where multiple users can work with hello same notebook.</span></span>
* <span data-ttu-id="8fccc-178">U kunt lokaal werken met notitieblokken zonder zelfs een cluster van.</span><span class="sxs-lookup"><span data-stu-id="8fccc-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="8fccc-179">U hoeft alleen een cluster tootest uw notitieblokken tegen, niet toomanually beheren uw notitieblokken of een ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="8fccc-179">You only need a cluster tootest your notebooks against, not toomanually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="8fccc-180">Het is mogelijk beter tooconfigure uw eigen lokale ontwikkelingsomgeving dan tooconfigure hello Jupyter-installatie op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8fccc-180">It may be easier tooconfigure your own local development environment than it is tooconfigure hello Jupyter installation on hello cluster.</span></span>  <span data-ttu-id="8fccc-181">U kunt profiteren van alle Hallo-software die u lokaal hebt geïnstalleerd zonder het configureren van een of meer externe clusters.</span><span class="sxs-lookup"><span data-stu-id="8fccc-181">You can take advantage of all hello software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="8fccc-182">Met Jupyter op uw lokale computer geïnstalleerd, kunnen meerdere gebruikers Hallo uitvoeren dezelfde notebook op dezelfde Spark-cluster op Hallo Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="8fccc-182">With Jupyter installed on your local computer, multiple users can run hello same notebook on hello same Spark cluster at hello same time.</span></span> <span data-ttu-id="8fccc-183">In een dergelijke situatie worden meerdere Livy sessies gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8fccc-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="8fccc-184">Als u een probleem ondervindt toodebug dat, moeten een complexe taak tootrack welke sessie Livy toowhich gebruiker behoort.</span><span class="sxs-lookup"><span data-stu-id="8fccc-184">If you run into an issue and want toodebug that, it will be a complex task tootrack which Livy session belongs toowhich user.</span></span>
>
>

## <span data-ttu-id="8fccc-185"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="8fccc-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="8fccc-186">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fccc-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="8fccc-187">Scenario's</span><span class="sxs-lookup"><span data-stu-id="8fccc-187">Scenarios</span></span>
* [<span data-ttu-id="8fccc-188">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="8fccc-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="8fccc-189">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="8fccc-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="8fccc-190">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="8fccc-190">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="8fccc-191">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="8fccc-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="8fccc-192">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fccc-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="8fccc-193">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8fccc-193">Create and run applications</span></span>
* [<span data-ttu-id="8fccc-194">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="8fccc-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="8fccc-195">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="8fccc-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="8fccc-196">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="8fccc-196">Tools and extensions</span></span>
* [<span data-ttu-id="8fccc-197">De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="8fccc-197">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="8fccc-198">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="8fccc-198">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="8fccc-199">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fccc-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="8fccc-200">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fccc-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="8fccc-201">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="8fccc-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="8fccc-202">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="8fccc-202">Manage resources</span></span>
* [<span data-ttu-id="8fccc-203">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8fccc-203">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="8fccc-204">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="8fccc-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
