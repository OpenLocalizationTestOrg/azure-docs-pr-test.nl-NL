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
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a>Hallo Tez UI toodebug Tez-taken op HDInsight op basis van Windows gebruiken
Hallo Tez UI is een webpagina die kunnen worden gebruikt toounderstand en foutopsporing taken die Tez als de engine voor het uitvoeren van Hallo op Windows gebaseerde HDInsight-clusters gebruiken. Hallo Tez UI kunt u toovisualize Hallo taak, zoals een grafiek van verbonden items Inzoomen op elk item en statistieken en logboekregistratie informatie ophalen.

> [!IMPORTANT]
> Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Windows. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="prerequisites"></a>Vereisten
* Een Windows gebaseerde HDInsight-cluster. Zie voor instructies over het maken van een nieuw cluster [aan de slag met HDInsight op basis van Windows](hdinsight-hadoop-tutorial-get-started-windows.md).

  > [!IMPORTANT]
  > Hallo Tez UI is alleen beschikbaar op Windows gebaseerde HDInsight-clusters die zijn gemaakt na 8 februari 2016.
  >
  >
* Een extern bureaublad op basis van Windows-client.

## <a name="understanding-tez"></a>Understanding Tez
Tez is een uitbreidbaar framework voor gegevensverwerking in Hadoop. deze groter snelheden dan traditionele MapReduce-verwerking biedt. Voor Windows gebaseerde HDInsight-clusters is een optionele engine die u voor Hive inschakelen kunt met behulp van de volgende opdracht als onderdeel van uw Hive-query Hallo:

    set hive.execution.engine=tez;

Wanneer werk ingediende tooTez is, wordt een omgeleid acyclische grafiek (DAG) die worden beschreven Hallo volgorde van de uitvoering van Hallo acties vereist door Hallo-taak gemaakt. Afzonderlijke acties hoekpunten worden genoemd en het uitvoeren van een stukje Hallo algemene taak. Hallo werkelijke uitvoering van Hallo werk beschreven door een hoekpunt een taak wordt aangeroepen en kan worden verdeeld over meerdere knooppunten in cluster Hallo.

### <a name="understanding-hello-tez-ui"></a>Understanding Hallo Tez UI
Hallo Tez UI is dat een webpagina biedt informatie over de processen die worden uitgevoerd of hebben eerder is uitgevoerd met behulp van Tez. Hiermee kunt u tooview Hallo DAG die worden gegenereerd door de Tez, hoe is verdeeld over de clusters, prestatiemeteritems gebruikt, zoals geheugen die wordt gebruikt door taken en hoekpunten en informatie over de fout. Kan deze u nuttige informatie in de volgende scenario's Hallo aanbieden:

* Bewaking langlopende processen, weer te geven, Hallo voortgang van de kaart en taken te verminderen.
* Historische gegevens voor de geslaagde of mislukte processen toolearn analyseren hoe verwerking kan worden verbeterd of waarom is mislukt.

## <a name="generate-a-dag"></a>Genereren van een DAG
Hallo Tez UI bevat alleen gegevens als een taak die gebruikmaakt van Hallo Tez-engine wordt uitgevoerd of is in de afgelopen Hallo is uitgevoerd. Eenvoudige Hive-query's kunnen doorgaans worden opgelost zonder Tez, maar complexe query's filteren, groeperen, rangschikken, joins, enz. meestal Tez is vereist.

Volgende stappen toorun een Hive-query die wordt uitgevoerd met behulp van Tez hello gebruiken.

1. Navigeer in een webbrowser, toohttps://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** Hallo-naam van uw HDInsight-cluster.
2. Selecteer Hallo Hallo menu bovenaan Hallo Hallo pagina **Hive-Editor**. Hiermee wordt een pagina weergegeven met de volgende voorbeeldquery Hallo.

        Select * from hivesampletable

    Hallo voorbeeldquery wissen en vervang deze door de volgende Hallo.

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. Selecteer Hallo **indienen** knop. Hallo **taak sessie** sectie onderaan Hallo Hallo pagina Hallo status van Hallo query worden weergegeven. Hallo statuswijzigingen één keer te**voltooid**, selecteer Hallo **Details weergeven** tooview Hallo resultaten koppelen. Hallo **Taakuitvoer** moet vergelijkbaar toohello volgende:

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a>Hallo Tez UI gebruiken
> [!NOTE]
> Hallo Tez UI is alleen beschikbaar vanuit Hallo bureaublad van de head clusterknooppunten hello, dus moet u extern bureaublad tooconnect toohello hoofdknooppunten.
>
>

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster. Selecteer Hallo Hallo bovenaan Hallo HDInsight blade **extern bureaublad** pictogram. Hallo-blade met extern bureaublad wordt weergegeven

    ![Pictogram voor extern bureaublad](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. Selecteer in de blade Hallo extern bureaublad **Connect** tooconnect toohello cluster hoofdknooppunt. Wanneer u wordt gevraagd, gebruiken Hallo cluster gebruiker naam en het wachtwoord tooauthenticate Hallo verbinding met extern bureaublad.

    ![Pictogram externe bureaublad](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > Als u extern bureaublad-verbinding niet hebt ingeschakeld, Geef een gebruikersnaam, wachtwoord en vervaldatum en selecteer vervolgens **inschakelen** tooenable extern bureaublad. Zodra is ingeschakeld, gebruikt u de vorige stappen tooconnect Hallo.
   >
   >
3. Eenmaal zijn verbonden, opent u Internet Explorer op Hallo extern bureaublad, selecteer Hallo tandwielpictogram pictogram in de rechterbovenhoek Hallo van Hallo browser, en selecteer vervolgens **instellingen voor de Compatibiliteitsweergave**.
4. Van Hallo onder **instellingen voor de Compatibiliteitsweergave**Schakel Hallo selectievakje in voor **intranetsites worden weergegeven in de Compatibiliteitsweergave** en **gebruik Microsoft hardware compatibility List**, en selecteer vervolgens **sluiten**.
5. Blader in Internet Explorer, toohttp://headnodehost:8188/tezui / #/. Hallo Tez UI wordt weergegeven

    ![Tez-gebruikersinterface](./media/hdinsight-debug-tez-ui/tezui.png)

    Wanneer Hallo Tez UI wordt geladen, ziet u een lijst van dag's die momenteel worden uitgevoerd, of zijn uitgevoerd op Hallo-cluster. de standaardweergave Hallo omvat Hallo Dag Name, -Id, Submitter, Status, begintijd, eindtijd, duur, toepassings-ID en wachtrij. Meer kolommen kunnen worden toegevoegd met behulp van Hallo tandwielpictogram pictogram op Hallo van Hallo pagina.

    Als u slechts één vermelding hebt, zal zijn voor Hallo-query die u in de vorige sectie Hallo hebt uitgevoerd. Als u meerdere vermeldingen hebt, kunt u zoeken door te voeren zoekcriteria in Hallo-velden boven Hallo dag's vervolgens bereikt **Enter**.
6. Selecteer Hallo **Dag Name** voor de meest recente DAG vermelding Hallo. Hiermee wordt informatie over Hallo DAG, evenals Hallo optie toodownload een zip van JSON-bestanden die informatie over Hallo DAG bevatten weergegeven.

    ![Details van de DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. Hierboven Hallo **DAG Details** verschillende koppelingen die gebruikt toodisplay informatie over Hallo DAG worden kunnen.

   * **DAG tellers** tellers geeft informatie weer voor deze DAG.
   * **Grafische weergave** een grafische weergave van deze DAG.
   * **Alle hoekpunten** geeft een overzicht van Hallo hoekpunten in deze DAG.
   * **Alle taken** geeft een lijst met taken voor alle hoekpunten Hallo in deze DAG.
   * **Alle TaskAttempts** geeft informatie weer over Hallo probeert toorun taken voor deze DAG.

     > [!NOTE]
     > Als u weergeven van de kolommen voor hoekpunten, taken en TaskAttempts hello schuift, er worden koppelingen tooview **tellers** en **weergeven of downloaden van logboeken** voor elke rij.
     >
     >

     Als er een fout opgetreden met de Hallo-taak is, worden Hallo Details van de DAG een status mislukt, samen met koppelingen tooinformation over de mislukte taak Hallo weergegeven. Diagnostische gegevens weergegeven onder Hallo DAG details.
8. Selecteer **grafische weergave**. U ziet nu een grafische weergave van Hallo DAG. U kunt Hallo muis op elke hoekpunt Hallo weergave toodisplay informatie over het plaatsen.

    ![Grafische weergave](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. Hallo te klikken op een hoekpunt laadt **hoekpunt Details** voor dat het item. Klik op Hallo **kaart 1** hoekpunt toodisplay details voor dit item. Selecteer **bevestigen** tooconfirm Hallo navigatie.

    ![Hoekpunt details](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. Houd er rekening mee dat u hebt nu koppelingen bovenaan Hallo Hallo pagina gerelateerde toovertices en taken.

    > [!NOTE]
    > U kunt ook op deze pagina bereikt door te terug te gaan**DAG Details**, selecteren **hoekpunt Details**, en vervolgens te klikken op Hallo **kaart 1** hoekpunt.
    >
    >

    * **Hoekpunt tellers** teller geeft informatie weer voor deze hoekpunt.
    * **Taken** taken voor dit hoekpunt weergegeven.
    * **Taak pogingen** geeft informatie weer over pogingen toorun taken voor dit hoekpunt.
    * **Gegevensbronnen & Sinks** gegevensbronnen weergeeft en de sinks voor dit hoekpunt.

      > [!NOTE]
      > Als met de vorige menu hello, u weergeven van de kolommen voor taken Hallo schuiven kunt, koppelingen taak pogingen, en bronnen & Sinks__ toodisplay toomore-informatie voor elk item.
      >
      >
11. Selecteer **taken**, en vervolgens selecteert Hallo item met de naam **00_000000**. Hiermee wordt weergegeven **taakdetails** voor deze taak. In dit scherm kunt u weergeven **taak tellers** en **taak pogingen**.

    ![Taakdetails](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>Volgende stappen
U hebt geleerd hoe toouse hello Tez bekijken, meer informatie over [met behulp van Hive in HDInsight](hdinsight-use-hive.md).

Zie voor meer technische informatie op Tez hello [Tez-pagina op Hortonworks](http://hortonworks.com/hadoop/tez/).
