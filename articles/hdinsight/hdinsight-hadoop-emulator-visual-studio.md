---
title: aaaData Lake tools voor Visual Studio met Hortonworks Sandbox - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Azure Data Lake tools voor Visual Studio met Hallo Hortonworks sandbox uitgevoerd in een lokale virtuele machine Hallo. U kunt met deze hulpprogramma's, maken en Hive en Pig-taken uitvoeren op Hallo sandbox, en de taakuitvoer weergeven en de geschiedenis.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="260b3-104">Gebruik hello Azure Data Lake tools voor Visual Studio met Hallo Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="260b3-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="260b3-105">Azure Data Lake bevat hulpprogramma's voor het werken met algemene Hadoop-clusters.</span><span class="sxs-lookup"><span data-stu-id="260b3-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="260b3-106">Dit document bevat Hallo stappen nodig Hallo toouse Hallo Data Lake tools met Hortonworks Sandbox uitgevoerd op een lokale virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="260b3-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="260b3-107">Hallo Hortonworks Sandbox met kunt u toowork met Hadoop lokaal op uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="260b3-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="260b3-108">Nadat u een oplossing hebt ontwikkeld en toodeploy wilt dit op grote schaal, kunt u vervolgens tooan HDInsight-cluster te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="260b3-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="260b3-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="260b3-109">Prerequisites</span></span>

* <span data-ttu-id="260b3-110">Hello Hortonworks Sandbox, in een virtuele machine wordt uitgevoerd op uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="260b3-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="260b3-111">Dit document is geschreven en getest met de Hallo sandbox in Oracle VirtualBox uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="260b3-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="260b3-112">Zie voor informatie over het instellen van de sandbox Hallo Hallo [aan de slag met Hallo Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="260b3-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="260b3-113">document.</span><span class="sxs-lookup"><span data-stu-id="260b3-113">document.</span></span>

* <span data-ttu-id="260b3-114">Visual Studio 2013, Visual Studio 2015 of Visual Studio 2017 (alle versies).</span><span class="sxs-lookup"><span data-stu-id="260b3-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="260b3-115">Hallo [Azure SDK voor .NET](https://azure.microsoft.com/downloads/) 2.7.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="260b3-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="260b3-116">Hallo [Azure Data Lake tools voor Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="260b3-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="260b3-117">Wachtwoorden voor Hallo sandbox configureren</span><span class="sxs-lookup"><span data-stu-id="260b3-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="260b3-118">Zorg ervoor dat Hallo die hortonworks Sandbox wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="260b3-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="260b3-119">Volg de stappen Hallo in Hallo [aan de slag in Hallo Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span><span class="sxs-lookup"><span data-stu-id="260b3-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="260b3-120">Met deze stappen configureert Hallo wachtwoord voor Hallo SSH `root` account en Hallo Ambari `admin` account.</span><span class="sxs-lookup"><span data-stu-id="260b3-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="260b3-121">Deze wachtwoorden worden gebruikt wanneer u verbinding toohello sandbox vanuit Visual Studio maakt.</span><span class="sxs-lookup"><span data-stu-id="260b3-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="260b3-122">Verbinding maken met de Hallo extra toohello sandbox</span><span class="sxs-lookup"><span data-stu-id="260b3-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="260b3-123">Open Visual Studio, selecteer **weergave**, en selecteer vervolgens **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="260b3-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="260b3-124">Van **Server Explorer**, klik met de rechtermuisknop Hallo **HDInsight** vermelding en selecteer vervolgens **tooHDInsight Emulator verbinding**.</span><span class="sxs-lookup"><span data-stu-id="260b3-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![Schermopname van Server Explorer, met Connect tooHDInsight Emulator gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="260b3-126">Van Hallo **tooHDInsight Emulator verbinding** dialoogvenster Voer Hallo wachtwoord die u hebt geconfigureerd voor Ambari.</span><span class="sxs-lookup"><span data-stu-id="260b3-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![Schermopname van dialoogvenster met wachtwoord tekstvak gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="260b3-128">Selecteer **volgende** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="260b3-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="260b3-129">Gebruik Hallo **wachtwoord** veld tooenter Hallo wachtwoord die u hebt geconfigureerd voor Hallo `root` account.</span><span class="sxs-lookup"><span data-stu-id="260b3-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="260b3-130">Laat Hallo andere velden Hallo-standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="260b3-130">Leave hello other fields at hello default value.</span></span>

    ![Schermopname van dialoogvenster met wachtwoord tekstvak gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="260b3-132">Selecteer **volgende** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="260b3-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="260b3-133">Validatie van Hallo services toofinish wacht.</span><span class="sxs-lookup"><span data-stu-id="260b3-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="260b3-134">In sommige gevallen validatie mislukt en wordt u gevraagd tooupdate Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="260b3-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="260b3-135">Als validatie mislukt, selecteert u **Update**, en wachten op het Hallo-configuratie en controle voor Hallo service toofinish.</span><span class="sxs-lookup"><span data-stu-id="260b3-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![Schermopname van dialoogvenster met de knop bijwerken gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="260b3-137">Hallo updateproces Ambari toomodify hello Hortonworks Sandbox configuratie toowhat wordt verwacht door Hallo Data Lake tools voor Visual Studio gebruikt.</span><span class="sxs-lookup"><span data-stu-id="260b3-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="260b3-138">Nadat de validatie is voltooid, selecteert u **voltooien** toocomplete configuratie.</span><span class="sxs-lookup"><span data-stu-id="260b3-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="260b3-139">![Schermopname van dialoogvenster met de knop Voltooien gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="260b3-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="260b3-140">Afhankelijk van Hallo snelheid van uw ontwikkelomgeving en Hallo en de hoeveelheid geheugen toegewezen toohello virtuele machine, kan het tooconfigure van enkele minuten duren en Hallo services valideren.</span><span class="sxs-lookup"><span data-stu-id="260b3-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="260b3-141">Na deze stappen uitvoert, hebt u nu een **lokale HDInsight-cluster** vermelding in Server Explorer, onder Hallo **HDInsight** sectie.</span><span class="sxs-lookup"><span data-stu-id="260b3-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="260b3-142">Een Hive-query schrijven</span><span class="sxs-lookup"><span data-stu-id="260b3-142">Write a Hive query</span></span>

<span data-ttu-id="260b3-143">Hive biedt een SQL-achtige query language (HiveQL) voor het werken met gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="260b3-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="260b3-144">Volgende stappen toolearn hoe toorun op aanvraag een query op de lokale cluster Hallo Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="260b3-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="260b3-145">In **Server Explorer**, met de rechtermuisknop op het Hallo-vermelding voor het lokale cluster Hallo die u eerder hebt toegevoegd en selecteer vervolgens **een Hive-Query schrijven**.</span><span class="sxs-lookup"><span data-stu-id="260b3-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Schermopname van Server Explorer en schrijven naar een Hive-Query gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="260b3-147">Een nieuwe queryvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="260b3-147">A new query window appears.</span></span> <span data-ttu-id="260b3-148">Hier kunt u snel schrijven en het verzenden van een query toohello lokaal cluster.</span><span class="sxs-lookup"><span data-stu-id="260b3-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="260b3-149">Voer in het nieuwe queryvenster hello, Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="260b3-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="260b3-150">toorun hello query, selecteer **indienen** Hallo boven aan het Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="260b3-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="260b3-151">Laat Hallo andere waarden (**Batch** en servernaam) op Hallo standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="260b3-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![Schermafbeelding van de query-venster met de knop verzenden Hallo gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="260b3-153">U kunt ook de vervolgkeuzelijst Hallo naast te**indienen** tooselect **Geavanceerd**.</span><span class="sxs-lookup"><span data-stu-id="260b3-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="260b3-154">Geavanceerde opties kunnen u extra opties tooprovide wanneer u de taak Hallo indient.</span><span class="sxs-lookup"><span data-stu-id="260b3-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![Schermopname van Submit Script dialoogvenster](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="260b3-156">Nadat u Hallo query verzonden, wordt de taakstatus Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="260b3-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="260b3-157">Hallo taakstatus geeft informatie weer over Hallo taak terwijl deze wordt verwerkt door Hadoop.</span><span class="sxs-lookup"><span data-stu-id="260b3-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="260b3-158">**Taakstatus** Hallo Hallo taak status bevat.</span><span class="sxs-lookup"><span data-stu-id="260b3-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="260b3-159">Hallo status wordt regelmatig bijgewerkt of u kunt de status van Hallo vernieuwen pictogram toorefresh Hallo handmatig gebruiken.</span><span class="sxs-lookup"><span data-stu-id="260b3-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![Schermafbeelding van de weergave van de taak in het dialoogvenster met de status van de taak is gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="260b3-161">Na het Hallo **taakstatus** wijzigingen te**voltooid**, een omgeleid acyclische grafiek (DAG) wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="260b3-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="260b3-162">Dit diagram beschrijft Hallo uitvoeringspad dat is bepaald door de Tez bij het verwerken van Hallo Hive-query.</span><span class="sxs-lookup"><span data-stu-id="260b3-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="260b3-163">Tez is Hallo standaard engine voor het uitvoeren voor Hive op Hallo lokale cluster.</span><span class="sxs-lookup"><span data-stu-id="260b3-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="260b3-164">Tez is ook Hallo standaard wanneer u van Linux gebaseerde HDInsight-clusters gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="260b3-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="260b3-165">Het is niet standaard op HDInsight op basis van Windows hello.</span><span class="sxs-lookup"><span data-stu-id="260b3-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="260b3-166">toouse deze er, moet u Hallo regel toevoegen `set hive.execution.engine = tez;` toohello begin van uw Hive-query.</span><span class="sxs-lookup"><span data-stu-id="260b3-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="260b3-167">Gebruik Hallo **Taakuitvoer** tooview Hallo uitvoer koppelen.</span><span class="sxs-lookup"><span data-stu-id="260b3-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="260b3-168">In dit geval is het 823, Hallo aantal rijen in Hallo sample_08 tabel.</span><span class="sxs-lookup"><span data-stu-id="260b3-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="260b3-169">U kunt diagnostische gegevens over Hallo-taak weergeven met behulp van Hallo **taaklogboek** en **YARN-logboek downloaden** koppelingen.</span><span class="sxs-lookup"><span data-stu-id="260b3-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="260b3-170">U kunt ook Hive-taken interactief uitvoeren wijzigen Hallo **Batch** veld te**interactief**.</span><span class="sxs-lookup"><span data-stu-id="260b3-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="260b3-171">Selecteer vervolgens **Execute**.</span><span class="sxs-lookup"><span data-stu-id="260b3-171">Then select **Execute**.</span></span>

    ![Schermopname van interactieve en Execute knoppen gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="260b3-173">Een interactieve query streams Hallo logboek gegenereerd tijdens de verwerking toohello **HiveServer2 uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="260b3-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="260b3-174">Hallo informatie is Hallo dezelfde die beschikbaar is via Hallo **taaklogboek** koppelen nadat een taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="260b3-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![Schermopname van het uitvoerlogboek](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="260b3-176">Een Hive-project maken</span><span class="sxs-lookup"><span data-stu-id="260b3-176">Create a Hive project</span></span>

<span data-ttu-id="260b3-177">U kunt ook een project met meerdere Hive-scripts maken.</span><span class="sxs-lookup"><span data-stu-id="260b3-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="260b3-178">Een project gebruiken wanneer u scripts gerelateerde of toostore scripts in een versiebeheersysteem wilt.</span><span class="sxs-lookup"><span data-stu-id="260b3-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="260b3-179">Selecteer in Visual Studio **bestand**, **nieuw**, en vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="260b3-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="260b3-180">Vouw vanuit Hallo lijst met projecten, **sjablonen**, vouw **Azure Data Lake**, en selecteer vervolgens **HIVE (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="260b3-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="260b3-181">Selecteer in de lijst met sjablonen Hallo **Hive-voorbeeldquery**.</span><span class="sxs-lookup"><span data-stu-id="260b3-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="260b3-182">Voer een naam en locatie en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="260b3-182">Enter a name and location, and then select **OK**.</span></span>

    ![Schermopname van nieuw Project-venster met Azure Data Lake, HIVE, Hive-voorbeeldquery en OK gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="260b3-184">Hallo **Hive-voorbeeldquery** -project bevat twee scripts **WebLogAnalysis.hql** en **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="260b3-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="260b3-185">Dient u deze scripts met behulp van dezelfde Hallo **indienen** knop Hallo boven aan het Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="260b3-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="260b3-186">Een Pig-project maken</span><span class="sxs-lookup"><span data-stu-id="260b3-186">Create a Pig project</span></span>

<span data-ttu-id="260b3-187">Terwijl Hive een SQL-achtige taal bevat voor het werken met gestructureerde gegevens, werkt de Pig door transformaties uitvoeren op gegevens.</span><span class="sxs-lookup"><span data-stu-id="260b3-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="260b3-188">Pig biedt een taal (Pig Latin) waarmee u toodevelop een pijplijn van transformaties.</span><span class="sxs-lookup"><span data-stu-id="260b3-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="260b3-189">toouse Pig met het lokale cluster hello, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="260b3-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="260b3-190">Open Visual Studio en selecteer **bestand**, **nieuw**, en vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="260b3-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="260b3-191">Vouw vanuit Hallo lijst met projecten, **sjablonen**, vouw **Azure Data Lake**, en selecteer vervolgens **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="260b3-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="260b3-192">Selecteer in de lijst met sjablonen Hallo **Pig toepassing**.</span><span class="sxs-lookup"><span data-stu-id="260b3-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="260b3-193">Voer een naam en locatie en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="260b3-193">Enter a name, location, and then select **OK**.</span></span>

    ![Schermopname van nieuw Project-venster met Azure Data Lake, Pig, Pig-toepassing en OK gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="260b3-195">Voer na de tekst hello inhoud Hallo Hallo **script.pig** -bestand dat is gemaakt met dit project.</span><span class="sxs-lookup"><span data-stu-id="260b3-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="260b3-196">Pig gebruikmaakt van een andere taal dan Hive, hoe u Hallo taken uitvoeren is consistent tussen de beide talen, via Hallo **indienen** knop.</span><span class="sxs-lookup"><span data-stu-id="260b3-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="260b3-197">Selecteren Hallo-omlaag naast **indienen** wordt een dialoogvenster Geavanceerd verzenden voor Pig.</span><span class="sxs-lookup"><span data-stu-id="260b3-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Schermopname van Submit Script dialoogvenster](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="260b3-199">Hallo taakstatus en de uitvoer wordt weergegeven, dezelfde Hallo als een Hive-query.</span><span class="sxs-lookup"><span data-stu-id="260b3-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![Schermafbeelding van een voltooide Pig-taak](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="260b3-201">Taken weergeven</span><span class="sxs-lookup"><span data-stu-id="260b3-201">View jobs</span></span>

<span data-ttu-id="260b3-202">Data Lake tools kunnen u ook informatie over taken die zijn uitgevoerd op Hadoop tooeasily weergeven.</span><span class="sxs-lookup"><span data-stu-id="260b3-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="260b3-203">Volgende stappen toosee Hallo taken die zijn uitgevoerd op de lokale cluster Hallo Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="260b3-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="260b3-204">Van **Server Explorer**, met de rechtermuisknop op het lokale cluster Hallo en selecteer vervolgens **taken weergeven**.</span><span class="sxs-lookup"><span data-stu-id="260b3-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="260b3-205">Een lijst met taken die ingediend toohello cluster zijn wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="260b3-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![Schermopname van Server Explorer met de weergave taken die zijn gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="260b3-207">Hallo-lijst met taken, selecteer in een tooview Hallo taakdetails.</span><span class="sxs-lookup"><span data-stu-id="260b3-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![Schermopname van Job Browser met een Hallo-taken die zijn gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="260b3-209">Hallo-informatie weergegeven is vergelijkbaar toowhat die u na het uitvoeren van een query Hive of Pig, inclusief koppelingen tooview Hallo uitvoer en logboekbestanden informatie zien.</span><span class="sxs-lookup"><span data-stu-id="260b3-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="260b3-210">U kunt ook wijzigen en opnieuw indienen Hallo taak hier.</span><span class="sxs-lookup"><span data-stu-id="260b3-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="260b3-211">Weergave Hive-databases</span><span class="sxs-lookup"><span data-stu-id="260b3-211">View Hive databases</span></span>

1. <span data-ttu-id="260b3-212">In **Server Explorer**, vouw Hallo **lokale HDInsight-cluster** -item, en vouw vervolgens **Hive-Databases**.</span><span class="sxs-lookup"><span data-stu-id="260b3-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="260b3-213">Hallo **standaard** en **xademo** databases op de lokale cluster Hallo worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="260b3-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="260b3-214">Uitbreiden van een database bevat Hallo tabellen binnen Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="260b3-214">Expanding a database shows hello tables within hello database.</span></span>

    ![Schermopname van Server Explorer met uitgebreide databases](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="260b3-216">Uitbreiden van een tabel, worden Hallo kolommen voor die tabel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="260b3-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="260b3-217">Hallo gegevens van tooquickly weergeven met de rechtermuisknop op een tabel en selecteer **View Top 100 rijen**.</span><span class="sxs-lookup"><span data-stu-id="260b3-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Schermopname van Server Explorer met tabel uitgebreid en View Top 100 rijen geselecteerd](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="260b3-219">Eigenschappen van de database en tabel</span><span class="sxs-lookup"><span data-stu-id="260b3-219">Database and table properties</span></span>

<span data-ttu-id="260b3-220">U kunt de eigenschappen van een database of tabel Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="260b3-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="260b3-221">Selecteren **eigenschappen** worden in het venster Eigenschappen Hallo details voor Hallo geselecteerd item weergegeven.</span><span class="sxs-lookup"><span data-stu-id="260b3-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="260b3-222">Zie bijvoorbeeld Hallo-informatie die wordt weergegeven in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="260b3-222">For example, see hello information shown in hello following screenshot:</span></span>

![Schermopname van eigenschappen venster](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="260b3-224">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="260b3-224">Create a table</span></span>

<span data-ttu-id="260b3-225">toocreate een tabel met de rechtermuisknop op een database en selecteer vervolgens **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="260b3-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![Schermopname van Server Explorer, met Create Table gemarkeerd](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="260b3-227">Vervolgens kunt u met behulp van een formulier Hallo-tabel maken.</span><span class="sxs-lookup"><span data-stu-id="260b3-227">You can then create hello table using a form.</span></span> <span data-ttu-id="260b3-228">Hallo onderaan Hallo volgende schermafbeelding ziet u Hallo onbewerkte HiveQL die gebruikte toocreate Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="260b3-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![Schermopname van Hallo formulier toocreate een tabel die wordt gebruikt](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="260b3-230">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="260b3-230">Next steps</span></span>

* [<span data-ttu-id="260b3-231">Learning Hallo kabels Hallo Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="260b3-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="260b3-232">Hadoop-zelfstudie - aan de slag met HDP</span><span class="sxs-lookup"><span data-stu-id="260b3-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
