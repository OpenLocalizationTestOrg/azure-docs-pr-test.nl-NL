---
title: Tez-gebruikersinterface gebruiken met HDInsight op basis van Windows - Azure | Microsoft Docs
description: Informatie over het gebruik van de UI Tez fouten opsporen in Tez-taken in HDInsight HDInsight op basis van Windows.
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
ms.openlocfilehash: 3889fa1c3523eb0330cbe3b7640fd8590a5ceadf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="7f3b7-103">De UI Tez gebruiken om op te sporen Tez-taken in HDInsight op basis van Windows</span><span class="sxs-lookup"><span data-stu-id="7f3b7-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="7f3b7-104">De UI Tez is een webpagina die kunnen worden gebruikt om te begrijpen en foutopsporing van taken die Tez als de engine voor het uitvoeren op Windows gebaseerde HDInsight-clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="7f3b7-105">De UI Tez kunt u de taak als een grafiek van verbonden items visualiseren, Inzoomen op elk item en statistieken en logboekregistratie informatie ophalen.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f3b7-106">De stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Windows.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="7f3b7-107">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7f3b7-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f3b7-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7f3b7-109">Prerequisites</span></span>
* <span data-ttu-id="7f3b7-110">Een Windows gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="7f3b7-111">Zie voor instructies over het maken van een nieuw cluster [aan de slag met HDInsight op basis van Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="7f3b7-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7f3b7-112">De UI Tez is alleen beschikbaar op Windows gebaseerde HDInsight-clusters die zijn gemaakt na 8 februari 2016.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="7f3b7-113">Een extern bureaublad op basis van Windows-client.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="7f3b7-114">Understanding Tez</span><span class="sxs-lookup"><span data-stu-id="7f3b7-114">Understanding Tez</span></span>
<span data-ttu-id="7f3b7-115">Tez is een uitbreidbaar framework voor gegevensverwerking in Hadoop. deze groter snelheden dan traditionele MapReduce-verwerking biedt.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="7f3b7-116">Voor Windows gebaseerde HDInsight-clusters is een optionele-engine die u voor Hive inschakelen kunt met behulp van de volgende opdracht als onderdeel van uw Hive-query:</span><span class="sxs-lookup"><span data-stu-id="7f3b7-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="7f3b7-117">Wanneer het werk is verzonden naar Tez, wordt een omgeleid acyclische grafiek (DAG) die worden beschreven de volgorde van de uitvoering van de acties die vereist zijn voor de taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="7f3b7-118">Afzonderlijke acties hoekpunten worden genoemd, en een onderdeel van de algehele taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="7f3b7-119">De werkelijke uitvoering van het werk dat is beschreven door een hoekpunt een taak wordt aangeroepen en kan worden verdeeld over meerdere knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="7f3b7-120">Inzicht in de gebruikersinterface Tez</span><span class="sxs-lookup"><span data-stu-id="7f3b7-120">Understanding the Tez UI</span></span>
<span data-ttu-id="7f3b7-121">De UI Tez is dat een webpagina biedt informatie over de processen die worden uitgevoerd of hebben eerder is uitgevoerd met behulp van Tez.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="7f3b7-122">Hiermee kunt u bekijken van de DAG die worden gegenereerd door de Tez, hoe is verdeeld over de clusters, prestatiemeteritems gebruikt, zoals geheugen die wordt gebruikt door taken en hoekpunten en informatie over de fout.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="7f3b7-123">Dit kan nuttige informatie in de volgende scenario's bieden:</span><span class="sxs-lookup"><span data-stu-id="7f3b7-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="7f3b7-124">Bewaking van langlopende verwerkt, wordt de voortgang van de kaart weergeven en taken te verminderen.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="7f3b7-125">Analyse van historische gegevens voor de geslaagde of mislukte processen voor meer informatie over hoe de verwerking kan worden verbeterd of waarom is mislukt.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="7f3b7-126">Genereren van een DAG</span><span class="sxs-lookup"><span data-stu-id="7f3b7-126">Generate a DAG</span></span>
<span data-ttu-id="7f3b7-127">De UI Tez bevat alleen gegevens als een taak die is gebruikt de Tez-engine wordt uitgevoerd of is uitgevoerd in het verleden.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="7f3b7-128">Eenvoudige Hive-query's kunnen doorgaans worden opgelost zonder Tez, maar complexe query's filteren, groeperen, rangschikken, joins, enz. meestal Tez is vereist.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="7f3b7-129">Gebruik de volgende stappen uitvoeren van een Hive-query die wordt uitgevoerd met behulp van Tez.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="7f3b7-130">Navigeer in een webbrowser naar https://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** is de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="7f3b7-131">Selecteer in het menu aan de bovenkant van de pagina de **Hive-Editor**.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="7f3b7-132">Hiermee wordt een pagina met de volgende voorbeeldquery weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="7f3b7-133">Wissen van de voorbeeldquery en vervang deze door de volgende.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="7f3b7-134">Selecteer de **indienen** knop.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-134">Select the **Submit** button.</span></span> <span data-ttu-id="7f3b7-135">De **taak sessie** sectie aan de onderkant van de pagina wordt de status van de query weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="7f3b7-136">Zodra de status gewijzigd in **voltooid**, selecteer de **Details weergeven** koppeling om de resultaten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="7f3b7-137">De **Taakuitvoer** moet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="7f3b7-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="7f3b7-138">De Tez-gebruikersinterface gebruiken</span><span class="sxs-lookup"><span data-stu-id="7f3b7-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="7f3b7-139">De UI Tez is alleen beschikbaar vanaf het bureaublad van de clusterknooppunten head, dus moet u extern bureaublad verbinding maken met de hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="7f3b7-140">Van de [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="7f3b7-141">Vanaf de bovenkant van de HDInsight-blade, selecteer de **extern bureaublad** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="7f3b7-142">Hiermee wordt de blade voor extern bureaublad weergegeven</span><span class="sxs-lookup"><span data-stu-id="7f3b7-142">This will display the remote desktop blade</span></span>

    ![Pictogram voor extern bureaublad](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="7f3b7-144">Selecteer in de blade extern bureaublad **Connect** verbinding maken met het hoofdknooppunt van het cluster.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="7f3b7-145">Wanneer u wordt gevraagd, gebruikt u de cluster extern bureaublad-gebruikersnaam en wachtwoord om de verbinding te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![Pictogram externe bureaublad](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="7f3b7-147">Als u extern bureaublad-verbinding niet hebt ingeschakeld, Geef een gebruikersnaam, wachtwoord en vervaldatum en selecteer vervolgens **inschakelen** extern bureaublad inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="7f3b7-148">Zodra deze is ingeschakeld, moet u de vorige stappen gebruiken om verbinding te.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="7f3b7-149">Eenmaal zijn verbonden, opent u Internet Explorer op het externe bureaublad, selecteert u het pictogram tandwielpictogram in de rechterbovenhoek van de browser en selecteer vervolgens **instellingen voor de Compatibiliteitsweergave**.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="7f3b7-150">Van de onderkant van **instellingen voor de Compatibiliteitsweergave**, schakel het selectievakje voor **intranetsites worden weergegeven in de Compatibiliteitsweergave** en **gebruik Microsoft hardware compatibility List**, en Selecteer vervolgens **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="7f3b7-151">Ga in Internet Explorer naar tezui-http://headnodehost:8188 / #/.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="7f3b7-152">Hiermee wordt de Tez UI weergegeven</span><span class="sxs-lookup"><span data-stu-id="7f3b7-152">This will display the Tez UI</span></span>

    ![Tez-gebruikersinterface](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="7f3b7-154">Wanneer de Tez UI wordt geladen, ziet u een lijst van dag's die momenteel worden uitgevoerd, of zijn uitgevoerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="7f3b7-155">De standaardweergave omvat de Dag Name, -Id, Submitter, Status, begintijd, eindtijd, duur, toepassings-ID en wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="7f3b7-156">Meer kolommen kunnen worden toegevoegd aan de rechterkant van de pagina met behulp van het pictogram tandwielpictogram.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="7f3b7-157">Als u slechts één vermelding hebt, zal zijn voor de query die u in de vorige sectie hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="7f3b7-158">Als u meerdere vermeldingen hebt, kunt u zoeken door te voeren zoekcriteria in de velden van de dag's vervolgens bereikt **Enter**.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="7f3b7-159">Selecteer de **Dag Name** voor de meest recente DAG-vermelding.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="7f3b7-160">Hiermee wordt informatie over de DAG, evenals de optie voor het downloaden van een zip van JSON-bestanden die informatie over de DAG bevatten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![Details van de DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="7f3b7-162">Boven de **DAG Details** zijn enkele koppelingen die kan worden gebruikt om informatie weer over de DAG.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="7f3b7-163">**DAG tellers** tellers geeft informatie weer voor deze DAG.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="7f3b7-164">**Grafische weergave** een grafische weergave van deze DAG.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="7f3b7-165">**Alle hoekpunten** geeft een overzicht van de hoekpunten in deze DAG.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="7f3b7-166">**Alle taken** geeft een overzicht van de taken voor alle hoekpunten in deze DAG.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="7f3b7-167">**Alle TaskAttempts** geeft informatie weer over de pogingen tot het uitvoeren van taken voor deze DAG.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7f3b7-168">Als u de kolomweergave voor hoekpunten, taken en TaskAttempts schuift, zoals u ziet dat er koppelingen naar de weergave zijn **tellers** en **weergeven of downloaden van logboeken** voor elke rij.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="7f3b7-169">Als er een fout is opgetreden met de taak, wordt de status mislukt, met koppelingen naar informatie over de mislukte taak weergegeven in de Details van de DAG.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="7f3b7-170">Diagnostische gegevens weergegeven onder de details van de DAG.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="7f3b7-171">Selecteer **grafische weergave**.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-171">Select **Graphical View**.</span></span> <span data-ttu-id="7f3b7-172">U ziet nu een grafische weergave van de DAG.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="7f3b7-173">U kunt de muis plaatsen op elke hoekpunt in de weergave om informatie daarover weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Grafische weergave](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="7f3b7-175">Te klikken op een hoekpunt laadt de **hoekpunt Details** voor dat het item.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="7f3b7-176">Klik op de **kaart 1** hoekpunt om details van dit item weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="7f3b7-177">Selecteer **bevestigen** om te bevestigen dat de navigatie.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-177">Select **Confirm** to confirm the navigation.</span></span>

    ![Hoekpunt details](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="7f3b7-179">Houd er rekening mee dat u hebt nu koppelingen aan de bovenkant van de pagina die betrekking hebben op de hoekpunten en taken.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7f3b7-180">U kunt ook op deze pagina binnenkomen gaat u terug naar **DAG Details**, selecteren **hoekpunt Details**, en vervolgens te klikken op de **kaart 1** hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="7f3b7-181">**Hoekpunt tellers** teller geeft informatie weer voor deze hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="7f3b7-182">**Taken** taken voor dit hoekpunt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="7f3b7-183">**Taak pogingen** geeft informatie weer over de pogingen tot het uitvoeren van taken voor dit hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="7f3b7-184">**Gegevensbronnen & Sinks** gegevensbronnen weergeeft en de sinks voor dit hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7f3b7-185">Als met de vorige menu, kunt u de kolom weergeven voor taken, taak pogingen, en bronnen & Sinks__ koppelingen naar meer informatie voor elk item weergeven schuiven.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="7f3b7-186">Selecteer **taken**, en selecteer vervolgens het item met de naam **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="7f3b7-187">Hiermee wordt weergegeven **taakdetails** voor deze taak.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="7f3b7-188">In dit scherm kunt u weergeven **taak tellers** en **taak pogingen**.</span><span class="sxs-lookup"><span data-stu-id="7f3b7-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Taakdetails](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="7f3b7-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f3b7-190">Next Steps</span></span>
<span data-ttu-id="7f3b7-191">U hebt geleerd hoe u de weergave Tez, meer informatie over [met behulp van Hive in HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="7f3b7-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="7f3b7-192">Zie voor meer technische informatie over Tez, de [Tez-pagina op Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="7f3b7-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
