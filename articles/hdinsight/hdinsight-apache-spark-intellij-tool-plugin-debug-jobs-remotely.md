---
title: Toolkit voor IntelliJ - toepassingen voor foutopsporing op afstand op HDInsight Spark aaaAzure | Microsoft Docs
description: Meer informatie over hoe HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ tooremotely foutopsporing toepassingen die worden uitgevoerd op HDInsight Spark-clusters via VPN-verbinding gebruiken.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>Gebruik Azure Toolkit voor IntelliJ toodebug toepassingen op afstand op HDInsight Spark via VPN-verbinding

Het wordt aangeraden de Hallo manier voor foutopsporing spark applicaltion op afstand via ssh. Zie voor instructies [op afstand fouten opsporen in Spark scala-toepassingen op een HDInsight-cluster in Azure werkset voor IntelliJ via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

Dit artikel bevat stapsgewijze instructies over hoe toouse hello HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ toosubmit een taak Spark in HDInsight Spark-cluster en op afstand debug vanaf uw computer. toodo geval is, moet u Hallo volgende geavanceerde stappen uitvoeren:

1. Maak een site-naar-site of een punt-naar-site Azure Virtual Network. Hallo stappen in dit document wordt ervan uitgegaan dat u een site-naar-site-netwerk.
2. Een Spark-cluster maken in Azure HDInsight die deel uitmaakt van Hallo site-naar-site Azure Virtual Network.
3. Controleer de Hallo connectiviteit tussen Hallo cluster headnode en uw bureaublad.
4. Een toepassing Scala in IntelliJ IDEA maken en configureren voor foutopsporing op afstand.
5. Voer en fouten opsporen in Hallo-toepassing.

## <a name="prerequisites"></a>Vereisten
* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development kit. Kunt u het installeren van [hier](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IntelliJ IDEA. In dit artikel gebruikt versie 2017.1. Kunt u het installeren van [hier](https://www.jetbrains.com/idea/download/).
* HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ. HDInsight tools voor IntelliJ beschikbaar zijn als onderdeel van hello Azure Toolkit voor IntelliJ. Zie voor instructies over hoe tooinstall Azure Toolkit hello, [installeren hello Azure Toolkit voor IntelliJ](../azure-toolkit-for-intellij-installation.md).
* Meld u aan bij uw Azure-abonnement van IntelliJ IDEA. Volg de instructies Hallo [hier](hdinsight-apache-spark-intellij-tool-plugin.md).
* Tijdens het uitvoeren van Spark Scala-toepassing voor foutopsporing op afstand op een Windows-computer, krijgt u mogelijk een uitzondering zoals toegelicht in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) dit het geval is vanwege het ontbreken van tooa WinUtils.exe in Windows. toowork om deze fout, moet u [Hallo uitvoerbare downloaden vanaf hier](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa locatie, zoals **C:\WinUtils\bin**. Vervolgens moet u een omgevingsvariabele toevoegen **HADOOP_HOME** en stelt u Hallo-waarde van variabele hello te**C\WinUtils**.

## <a name="step-1-create-an-azure-virtual-network"></a>Stap 1: Een Azure-netwerk maken
Hallo instructies volgt in Hallo onderstaande koppelingen toocreate een Azure-netwerk en controleer vervolgens of Hallo connectiviteit tussen Hallo bureaublad en Azure Virtual Network.

* [Maak een VNet met een site-naar-site VPN-verbinding met Azure Portal](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Maak een VNet met een site-naar-site VPN-verbinding met behulp van PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [Configureren van een punt-naar-site-verbinding tooa virtueel netwerk met behulp van PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>Stap 2: Een HDInsight Spark-cluster maken
U moet ook een Apache Spark-cluster maken op Azure HDInsight die deel uitmaakt van hello Azure Virtual Network die u hebt gemaakt. Gebruik Hallo-informatie beschikbaar op [clusters in HDInsight op basis van Linux maken](hdinsight-hadoop-provision-linux-clusters.md). Selecteer hello Azure Virtual Network die u in de vorige stap Hallo gemaakt als onderdeel van de optionele configuratie.

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>Stap 3: Controleren of de Hallo verbinding tussen Hallo cluster headnode en uw bureaublad
1. Hallo IP-adres van Hallo headnode ophalen. Open Ambari UI voor Hallo-cluster. Cluster-blade hello, klikt u op **Dashboard**.

    ![Headnode IP zoeken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. Hallo Ambari UI van rechterbovenhoek hello, klik op **Hosts**.

    ![Headnode IP zoeken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. U ziet een lijst met headnodes worker-knooppunten en zookeeper-knooppunten. Hallo headnodes hebben Hallo **hn*** voorvoegsel. Klik op de eerste headnode Hallo.

    ![Headnode IP zoeken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. Hallo Hallo pagina die wordt geopend, van Hallo onderaan in **samenvatting** vak kopie Hallo IP-adres van Hallo headnode en Hallo-hostnaam.

    ![Headnode IP zoeken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Hallo IP-adres en hostnaam Hallo van Hallo headnode toohello **hosts** bestand op de computer Hallo van waar toorun en foutopsporing op afstand Hallo Spark taken. Hierdoor kunt u toocommunicate met Hallo headnode met Hallo IP-adres zoals Hallo hostnaam.

   1. Open een Kladblok met verhoogde machtigingen. Hallo bestandsmenu en klik op **Open** en navigeer vervolgens toohello locatie van Hallo hosts-bestand. Op een Windows-computer is `C:\Windows\System32\Drivers\etc\hosts`.
   2. Hallo na toohello toevoegen **hosts** bestand.

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. Controleer of dat u beide Hallo headnodes met Hallo IP-adres zoals Hallo hostnaam kunt pingen vanaf de computer Hallo waarmee u verbonden toohello virtuele Azure-netwerk dat wordt gebruikt door Hallo HDInsight-cluster.
7. SSH in Hallo cluster headnode Hallo-instructies op [Connect tooan HDInsight-cluster via SSH](hdinsight-hadoop-linux-use-ssh-unix.md). Ping Hallo IP-adres van de desktopcomputer Hallo van Hallo cluster headnode. U moet verbinding tooboth Hallo IP-adressen toegewezen toohello computer, één voor de netwerkverbinding Hallo testen en Hallo andere voor hello Azure Virtual Network die Hallo van computer is verbonden met.
8. Herhaal stappen Hallo voor Hallo ook andere headnode.

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>Stap 4: Een Spark Scala-toepassing hello HDInsight Tools met in Azure Toolkit voor IntelliJ maken en configureren voor foutopsporing op afstand
1. IntelliJ IDEA Start en een nieuw project maken. Controleer in Hallo het dialoogvenster new project, Hallo volgende keuzes en klik vervolgens op **volgende**.

    ![Spark Scala-toepassing maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * Selecteer in het linkerdeelvenster Hallo **HDInsight**.
   * Selecteer in het rechterdeelvenster Hallo **Spark in HDInsight (Scala)**.
   * Klik op **Volgende**.
2. Geef in het volgende venster Hallo Hallo volgende projectdetails, en klik op **voltooien**.  
   - Geef een naam van het project en de projectlocatie.
   - Voor **Project SDK**, Java 1.8 voor spark-cluster 2.x, Java 1.7 voor spark 1.x-cluster gebruiken.
   - Voor **Spark versie**, Scala-wizard voor het maken van project integreert de juiste versie voor Spark SDK en Scala SDK. Als Hallo spark-cluster versie 2.0 lager is, kiest u 1.x spark. Selecteer anders spark2.x. In dit voorbeeld wordt Spark2.0.2 (Scala 2.11.8).
       ![Spark Scala-toepassing maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. Hallo Spark project wordt automatisch een artefact voor u gemaakt. toosee hello artefacten, als volgt te werk.

   1. Van Hallo **bestand** menu, klikt u op **projectstructuur**.
   2. In Hallo **projectstructuur** in het dialoogvenster, klikt u op **artefacten** toosee Hallo standaard artefacten die wordt gemaakt.
   ![JAR maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      U kunt ook uw eigen artefacten maken te klikken op Hallo bly  **+**  pictogram, gemarkeerd in Hallo afbeelding hierboven.

4. Bibliotheken tooyour project toevoegen. tooadd een bibliotheek met de rechtermuisknop op de projectnaam Hallo in de structuur van de Hallo-project en klik vervolgens op **Open Module-instellingen**. In Hallo **projectstructuur** in het dialoogvenster in het linkerdeelvenster hello, klikt u op **bibliotheken**hello (+)-symbool op en klik vervolgens op **van Maven**.

    ![Bibliotheek toevoegen](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    In Hallo **bibliotheek downloaden uit de opslagplaats Maven** dialoogvenster, zoeken en toe te voegen Hallo bibliotheken te volgen.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. Kopiëren `yarn-site.xml` en `core-site.xml` van Hallo headnode cluster en voeg deze toohello project. Hallo volgende opdrachten toocopy Hallo bestanden gebruiken. U kunt [Cygwin](https://cygwin.com/install.html) toorun Hallo volgende `scp` toocopy Hallo-bestanden van Hallo cluster headnodes-opdrachten.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Omdat we Hallo cluster headnode IP-adres en de hostnamen voor Hallo hosts-bestand op Hallo bureaublad al hebt toegevoegd, kunnen we hello gebruiken **scp** opdrachten in Hallo manier te volgen.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Deze bestanden tooyour-project toevoegen door deze te kopiëren onder Hallo **/src** map in de projectstructuur van uw, bijvoorbeeld `<your project directory>\src`.
6. Update Hallo `core-site.xml` toomake Hallo wijzigingen te volgen.

   1. `core-site.xml`Hallo versleuteld sleutel toohello storage-account gekoppeld Hallo cluster bevat. In Hallo `core-site.xml` dat u toohello project vervangen Hallo versleutelde sleutel met de werkelijke opslagsleutel Hallo die zijn gekoppeld aan het standaardopslagaccount Hallo toegevoegd. Zie [beheren van uw toegangssleutels voor opslag](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Verwijderen van de volgende vermeldingen uit Hallo Hallo `core-site.xml`.

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. Hallo-bestand opslaan.
7. Hallo Main-klasse voor uw toepassing toevoegen. Van Hallo **Projectverkenner**, met de rechtermuisknop op **src**, wijst u te**nieuw**, en klik vervolgens op **Scala klasse**.

    ![Broncode toevoegen](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. In Hallo **nieuwe Scala klasse maken** dialoogvenster Geef een naam voor **soort** Selecteer **Object**, en klik vervolgens op **OK**.

    ![Broncode toevoegen](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. In Hallo `MyClusterAppMain.scala` bestand, plak Hallo code te volgen. Deze code maakt Hallo Spark context en start een `executeJob` methode van Hallo `SparkSample` object.

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. Herhaal stap 8 en 9 boven een nieuw Scala-object aangeroepen tooadd `SparkSample`. toothis klasse toevoegen Hallo code te volgen. Deze code Hallo gegevens leest uit Hallo HVAC.csv (beschikbaar op alle HDInsight Spark-clusters), haalt Hallo rijen met slechts één cijfer in Hallo zevende kolom in Hallo CSV en schrijft Hallo uitvoer te**/HVACOut** onder Hallo-standaard Storage-container voor Hallo-cluster.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. Herhaal stap 8 en 9 hierboven tooadd aangeroepen voor een nieuwe klasse `RemoteClusterDebugging`. Deze klasse implementeert Hallo Spark testframework die wordt gebruikt voor het opsporen van toepassingen. Hallo na code toohello toevoegen `RemoteClusterDebugging` klasse.

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     Het paar belangrijke zaken toonote hier:

   * Voor `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, zorg ervoor dat Hallo Spark assembly JAR is beschikbaar op de clusteropslag Hallo op Hallo opgegeven pad.
   * Voor `setJars`, geef Hallo-locatie waar Hallo artefact jar wordt gemaakt. Dit is meestal `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.
12. In Hallo `RemoteClusterDebugging` klasse, met de rechtermuisknop op Hallo `test` sleutelwoord en selecteer **RemoteClusterDebugging configuratie maken**.

    ![Externe configuratie maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. In het dialoogvenster hello, Geef een naam op voor de configuratie van Hallo en selecteer Hallo **testen soort** als **testnaam**. Laat alle andere waarden als standaard, klikt u op **toepassen**, en klik vervolgens op **OK**.

    ![Externe configuratie maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. U ziet nu een **extern uitvoeren** configuratie vervolgkeuzelijst in de menubalk Hallo.

    ![Externe configuratie maken](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>Stap 5: Hallo toepassing uitvoeren in de foutopsporingsmodus
1. Open in uw project IntelliJ IDEA `SparkSample.scala` en maak een onderbrekingspunt volgende too'val rdd1'. Selecteer in het pop-upmenu voor het maken van een onderbrekingspunt Hallo **regel in de functie executeJob**.

    ![Een onderbrekingspunt toevoegen](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Klik op Hallo **foutopsporing uitvoeren** knop volgende toohello **extern uitvoeren** configuratie vervolgkeuzelijst toostart Hallo toepassing uitvoert.

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Wanneer de programma-uitvoering Hallo Hallo onderbrekingspunt bereikt, ziet u een **foutopsporingsprogramma** tabblad in Hallo onderste deelvenster.

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Klik op Hallo (**+**) pictogram tooadd een controle zoals weergegeven in onderstaande Hallo-afbeelding.

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    Omdat de toepassing hello heeft overschreden voordat Hallo variabele hier `rdd1` is gemaakt met behulp van deze controle we zien wat zijn de eerste 5 rijen in de variabele Hallo Hallo `rdd`. Druk op **ENTER**.

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    Wat u ziet in Hallo afbeelding hierboven is dat terrabytes van gegevens en foutopsporing tijdens runtime kan opvragen hoe de voortgang van uw toepassing. Bijvoorbeeld in Hallo uitvoer wordt weergegeven in Hallo afbeelding hierboven, ziet u dat Hallo eerste rij van Hallo uitvoer is een koptekst. Op basis hiervan kunt u uw toepassing code tooskip Hallo veldnamenrij wijzigen, indien nodig.
5. U kunt nu klikken op Hallo **hervatten programma** pictogram tooproceed met uw toepassing uitvoeren.

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Als de toepassing hello voltooid is, ziet u uitvoer Hallo volgende.

    ![Hallo-programma uitvoeren in de foutopsporingsmodus](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demo
* Scala-Project (Video) te maken: [Spark Scala-toepassingen maken](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Foutopsporing op afstand (Video): [gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand op HDInsight-Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [HDInsight-hulpprogramma's gebruiken in Azure Toolkit voor IntelliJ toocreate en het verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [HDInsight-hulpprogramma's gebruiken in Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)
