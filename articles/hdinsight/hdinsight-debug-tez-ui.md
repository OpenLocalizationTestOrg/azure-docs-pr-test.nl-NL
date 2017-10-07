---
title: aaaUse Tez UI met HDInsight op basis van Windows - Azure | Microsoft Docs
description: Meer informatie over hoe toouse hello Tez UI toodebug Tez taken in HDInsight HDInsight op basis van Windows.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="d9e65-103">Hallo Tez UI toodebug Tez-taken op HDInsight op basis van Windows gebruiken</span><span class="sxs-lookup"><span data-stu-id="d9e65-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="d9e65-104">Hallo Tez UI is een webpagina die kunnen worden gebruikt toounderstand en foutopsporing taken die Tez als de engine voor het uitvoeren van Hallo op Windows gebaseerde HDInsight-clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9e65-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d9e65-105">Hallo Tez UI kunt u toovisualize Hallo taak, zoals een grafiek van verbonden items Inzoomen op elk item en statistieken en logboekregistratie informatie ophalen.</span><span class="sxs-lookup"><span data-stu-id="d9e65-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9e65-106">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Windows.</span><span class="sxs-lookup"><span data-stu-id="d9e65-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="d9e65-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d9e65-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d9e65-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d9e65-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9e65-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d9e65-109">Prerequisites</span></span>
* <span data-ttu-id="d9e65-110">Een Windows gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9e65-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="d9e65-111">Zie voor instructies over het maken van een nieuw cluster [aan de slag met HDInsight op basis van Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="d9e65-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d9e65-112">Hallo Tez UI is alleen beschikbaar op Windows gebaseerde HDInsight-clusters die zijn gemaakt na 8 februari 2016.</span><span class="sxs-lookup"><span data-stu-id="d9e65-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="d9e65-113">Een extern bureaublad op basis van Windows-client.</span><span class="sxs-lookup"><span data-stu-id="d9e65-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="d9e65-114">Understanding Tez</span><span class="sxs-lookup"><span data-stu-id="d9e65-114">Understanding Tez</span></span>
<span data-ttu-id="d9e65-115">Tez is een uitbreidbaar framework voor gegevensverwerking in Hadoop. deze groter snelheden dan traditionele MapReduce-verwerking biedt.</span><span class="sxs-lookup"><span data-stu-id="d9e65-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="d9e65-116">Voor Windows gebaseerde HDInsight-clusters is een optionele engine die u voor Hive inschakelen kunt met behulp van de volgende opdracht als onderdeel van uw Hive-query Hallo:</span><span class="sxs-lookup"><span data-stu-id="d9e65-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="d9e65-117">Wanneer werk ingediende tooTez is, wordt een omgeleid acyclische grafiek (DAG) die worden beschreven Hallo volgorde van de uitvoering van Hallo acties vereist door Hallo-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d9e65-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="d9e65-118">Afzonderlijke acties hoekpunten worden genoemd en het uitvoeren van een stukje Hallo algemene taak.</span><span class="sxs-lookup"><span data-stu-id="d9e65-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="d9e65-119">Hallo werkelijke uitvoering van Hallo werk beschreven door een hoekpunt een taak wordt aangeroepen en kan worden verdeeld over meerdere knooppunten in cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9e65-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="d9e65-120">Understanding Hallo Tez UI</span><span class="sxs-lookup"><span data-stu-id="d9e65-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="d9e65-121">Hallo Tez UI is dat een webpagina biedt informatie over de processen die worden uitgevoerd of hebben eerder is uitgevoerd met behulp van Tez.</span><span class="sxs-lookup"><span data-stu-id="d9e65-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="d9e65-122">Hiermee kunt u tooview Hallo DAG die worden gegenereerd door de Tez, hoe is verdeeld over de clusters, prestatiemeteritems gebruikt, zoals geheugen die wordt gebruikt door taken en hoekpunten en informatie over de fout.</span><span class="sxs-lookup"><span data-stu-id="d9e65-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="d9e65-123">Kan deze u nuttige informatie in de volgende scenario's Hallo aanbieden:</span><span class="sxs-lookup"><span data-stu-id="d9e65-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="d9e65-124">Bewaking langlopende processen, weer te geven, Hallo voortgang van de kaart en taken te verminderen.</span><span class="sxs-lookup"><span data-stu-id="d9e65-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="d9e65-125">Historische gegevens voor de geslaagde of mislukte processen toolearn analyseren hoe verwerking kan worden verbeterd of waarom is mislukt.</span><span class="sxs-lookup"><span data-stu-id="d9e65-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="d9e65-126">Genereren van een DAG</span><span class="sxs-lookup"><span data-stu-id="d9e65-126">Generate a DAG</span></span>
<span data-ttu-id="d9e65-127">Hallo Tez UI bevat alleen gegevens als een taak die gebruikmaakt van Hallo Tez-engine wordt uitgevoerd of is in de afgelopen Hallo is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9e65-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="d9e65-128">Eenvoudige Hive-query's kunnen doorgaans worden opgelost zonder Tez, maar complexe query's filteren, groeperen, rangschikken, joins, enz. meestal Tez is vereist.</span><span class="sxs-lookup"><span data-stu-id="d9e65-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="d9e65-129">Volgende stappen toorun een Hive-query die wordt uitgevoerd met behulp van Tez hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9e65-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="d9e65-130">Navigeer in een webbrowser, toohttps://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9e65-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="d9e65-131">Selecteer Hallo Hallo menu bovenaan Hallo Hallo pagina **Hive-Editor**.</span><span class="sxs-lookup"><span data-stu-id="d9e65-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="d9e65-132">Hiermee wordt een pagina weergegeven met de volgende voorbeeldquery Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9e65-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="d9e65-133">Hallo voorbeeldquery wissen en vervang deze door de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9e65-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="d9e65-134">Selecteer Hallo **indienen** knop.</span><span class="sxs-lookup"><span data-stu-id="d9e65-134">Select hello **Submit** button.</span></span> <span data-ttu-id="d9e65-135">Hallo **taak sessie** sectie onderaan Hallo Hallo pagina Hallo status van Hallo query worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9e65-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="d9e65-136">Hallo statuswijzigingen één keer te**voltooid**, selecteer Hallo **Details weergeven** tooview Hallo resultaten koppelen.</span><span class="sxs-lookup"><span data-stu-id="d9e65-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="d9e65-137">Hallo **Taakuitvoer** moet vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="d9e65-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="d9e65-138">Hallo Tez UI gebruiken</span><span class="sxs-lookup"><span data-stu-id="d9e65-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="d9e65-139">Hallo Tez UI is alleen beschikbaar vanuit Hallo bureaublad van de head clusterknooppunten hello, dus moet u extern bureaublad tooconnect toohello hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="d9e65-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="d9e65-140">Van Hallo [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9e65-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="d9e65-141">Selecteer Hallo Hallo bovenaan Hallo HDInsight blade **extern bureaublad** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d9e65-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="d9e65-142">Hallo-blade met extern bureaublad wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="d9e65-142">This will display hello remote desktop blade</span></span>

    ![Pictogram voor extern bureaublad](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="d9e65-144">Selecteer in de blade Hallo extern bureaublad **Connect** tooconnect toohello cluster hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="d9e65-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="d9e65-145">Wanneer u wordt gevraagd, gebruiken Hallo cluster gebruiker naam en het wachtwoord tooauthenticate Hallo verbinding met extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="d9e65-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![Pictogram externe bureaublad](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="d9e65-147">Als u extern bureaublad-verbinding niet hebt ingeschakeld, Geef een gebruikersnaam, wachtwoord en vervaldatum en selecteer vervolgens **inschakelen** tooenable extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="d9e65-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="d9e65-148">Zodra is ingeschakeld, gebruikt u de vorige stappen tooconnect Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9e65-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="d9e65-149">Eenmaal zijn verbonden, opent u Internet Explorer op Hallo extern bureaublad, selecteer Hallo tandwielpictogram pictogram in de rechterbovenhoek Hallo van Hallo browser, en selecteer vervolgens **instellingen voor de Compatibiliteitsweergave**.</span><span class="sxs-lookup"><span data-stu-id="d9e65-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="d9e65-150">Van Hallo onder **instellingen voor de Compatibiliteitsweergave**Schakel Hallo selectievakje in voor **intranetsites worden weergegeven in de Compatibiliteitsweergave** en **gebruik Microsoft hardware compatibility List**, en selecteer vervolgens **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="d9e65-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="d9e65-151">Blader in Internet Explorer, toohttp://headnodehost:8188/tezui / #/.</span><span class="sxs-lookup"><span data-stu-id="d9e65-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="d9e65-152">Hallo Tez UI wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="d9e65-152">This will display hello Tez UI</span></span>

    ![Tez-gebruikersinterface](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="d9e65-154">Wanneer Hallo Tez UI wordt geladen, ziet u een lijst van dag's die momenteel worden uitgevoerd, of zijn uitgevoerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9e65-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="d9e65-155">de standaardweergave Hallo omvat Hallo Dag Name, -Id, Submitter, Status, begintijd, eindtijd, duur, toepassings-ID en wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d9e65-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="d9e65-156">Meer kolommen kunnen worden toegevoegd met behulp van Hallo tandwielpictogram pictogram op Hallo van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="d9e65-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="d9e65-157">Als u slechts één vermelding hebt, zal zijn voor Hallo-query die u in de vorige sectie Hallo hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9e65-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="d9e65-158">Als u meerdere vermeldingen hebt, kunt u zoeken door te voeren zoekcriteria in Hallo-velden boven Hallo dag's vervolgens bereikt **Enter**.</span><span class="sxs-lookup"><span data-stu-id="d9e65-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="d9e65-159">Selecteer Hallo **Dag Name** voor de meest recente DAG vermelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9e65-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="d9e65-160">Hiermee wordt informatie over Hallo DAG, evenals Hallo optie toodownload een zip van JSON-bestanden die informatie over Hallo DAG bevatten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9e65-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![Details van de DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="d9e65-162">Hierboven Hallo **DAG Details** verschillende koppelingen die gebruikt toodisplay informatie over Hallo DAG worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="d9e65-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="d9e65-163">**DAG tellers** tellers geeft informatie weer voor deze DAG.</span><span class="sxs-lookup"><span data-stu-id="d9e65-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="d9e65-164">**Grafische weergave** een grafische weergave van deze DAG.</span><span class="sxs-lookup"><span data-stu-id="d9e65-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="d9e65-165">**Alle hoekpunten** geeft een overzicht van Hallo hoekpunten in deze DAG.</span><span class="sxs-lookup"><span data-stu-id="d9e65-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="d9e65-166">**Alle taken** geeft een lijst met taken voor alle hoekpunten Hallo in deze DAG.</span><span class="sxs-lookup"><span data-stu-id="d9e65-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="d9e65-167">**Alle TaskAttempts** geeft informatie weer over Hallo probeert toorun taken voor deze DAG.</span><span class="sxs-lookup"><span data-stu-id="d9e65-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="d9e65-168">Als u weergeven van de kolommen voor hoekpunten, taken en TaskAttempts hello schuift, er worden koppelingen tooview **tellers** en **weergeven of downloaden van logboeken** voor elke rij.</span><span class="sxs-lookup"><span data-stu-id="d9e65-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="d9e65-169">Als er een fout opgetreden met de Hallo-taak is, worden Hallo Details van de DAG een status mislukt, samen met koppelingen tooinformation over de mislukte taak Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9e65-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="d9e65-170">Diagnostische gegevens weergegeven onder Hallo DAG details.</span><span class="sxs-lookup"><span data-stu-id="d9e65-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="d9e65-171">Selecteer **grafische weergave**.</span><span class="sxs-lookup"><span data-stu-id="d9e65-171">Select **Graphical View**.</span></span> <span data-ttu-id="d9e65-172">U ziet nu een grafische weergave van Hallo DAG.</span><span class="sxs-lookup"><span data-stu-id="d9e65-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="d9e65-173">U kunt Hallo muis op elke hoekpunt Hallo weergave toodisplay informatie over het plaatsen.</span><span class="sxs-lookup"><span data-stu-id="d9e65-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![Grafische weergave](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="d9e65-175">Hallo te klikken op een hoekpunt laadt **hoekpunt Details** voor dat het item.</span><span class="sxs-lookup"><span data-stu-id="d9e65-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="d9e65-176">Klik op Hallo **kaart 1** hoekpunt toodisplay details voor dit item.</span><span class="sxs-lookup"><span data-stu-id="d9e65-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="d9e65-177">Selecteer **bevestigen** tooconfirm Hallo navigatie.</span><span class="sxs-lookup"><span data-stu-id="d9e65-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![Hoekpunt details](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="d9e65-179">Houd er rekening mee dat u hebt nu koppelingen bovenaan Hallo Hallo pagina gerelateerde toovertices en taken.</span><span class="sxs-lookup"><span data-stu-id="d9e65-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9e65-180">U kunt ook op deze pagina bereikt door te terug te gaan**DAG Details**, selecteren **hoekpunt Details**, en vervolgens te klikken op Hallo **kaart 1** hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="d9e65-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="d9e65-181">**Hoekpunt tellers** teller geeft informatie weer voor deze hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="d9e65-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="d9e65-182">**Taken** taken voor dit hoekpunt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d9e65-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="d9e65-183">**Taak pogingen** geeft informatie weer over pogingen toorun taken voor dit hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="d9e65-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="d9e65-184">**Gegevensbronnen & Sinks** gegevensbronnen weergeeft en de sinks voor dit hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="d9e65-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d9e65-185">Als met de vorige menu hello, u weergeven van de kolommen voor taken Hallo schuiven kunt, koppelingen taak pogingen, en bronnen & Sinks__ toodisplay toomore-informatie voor elk item.</span><span class="sxs-lookup"><span data-stu-id="d9e65-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="d9e65-186">Selecteer **taken**, en vervolgens selecteert Hallo item met de naam **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="d9e65-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="d9e65-187">Hiermee wordt weergegeven **taakdetails** voor deze taak.</span><span class="sxs-lookup"><span data-stu-id="d9e65-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="d9e65-188">In dit scherm kunt u weergeven **taak tellers** en **taak pogingen**.</span><span class="sxs-lookup"><span data-stu-id="d9e65-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Taakdetails](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="d9e65-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d9e65-190">Next Steps</span></span>
<span data-ttu-id="d9e65-191">U hebt geleerd hoe toouse hello Tez bekijken, meer informatie over [met behulp van Hive in HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="d9e65-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="d9e65-192">Zie voor meer technische informatie op Tez hello [Tez-pagina op Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="d9e65-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
