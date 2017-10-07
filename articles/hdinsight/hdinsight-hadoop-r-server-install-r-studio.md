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
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>RStudio met op HDInsight R Server installeren

Dit artikel wordt beschreven hoe tooinstall community (gratis) versie van Hallo [RStudio Server](https://www.rstudio.com/products/rstudio-server/) op Hallo edge-knooppunt van een cluster met een aangepast script. RStudio Server voorziet in een browser gebaseerde IDE voor gebruik door externe clients en wordt veel gebruikt op Linux. Er zijn meerdere geïntegreerde ontwikkelomgevingen (IDE) beschikbaar voor R vandaag, met inbegrip van:

- Microsoft [R-Tools voor Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) 
- [RStudio Server](https://www.rstudio.com/products/rstudio-server/) 
- Walware de Eclipse gebaseerde [StatET](http://www.walware.de/goto/statet).

Hallo profiteren van RStudio Server installeren op Hallo edge-knooppunt van een HDInsight-cluster is dat u een volledige IDE-ervaring voor Hallo ontwikkeling en uitvoering van scripts R met R Server op Hallo-cluster. Deze configuratie kunt productiever aanzienlijk dan standaard gebruik van Hallo R-Console.

> [!NOTE]
> Hallo-procedure wordt beschreven in dit artikel is alleen relevant als u geen tooinstall RStudio Server community edition hebt geselecteerd bij het inrichten van uw cluster. Als u dit hebt toegevoegd tijdens het inrichten, klikt u vervolgens tooaccess deze u klikt u op Hallo **R Server Dashboards** tegel in Azure portal-vermelding voor uw cluster, klikt u op Hallo Hallo **R Studio Server** tegel. 

Als u liever toouse Hallo commercieel in licentie gegeven Pro-versie van RStudio Server, moet u installatie-instructies Hallo van volgen [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).

> [!NOTE]
> Als u een HDInsight-cluster waarvoor R is geïnstalleerd met behulp van Hallo [R scriptactie installeren](hdinsight-hadoop-r-scripts-linux.md), Hallo stappen in dit document werkt niet correct ze nodig hebben een R Server op Hallo HDInsight-cluster.
>
> 

## <a name="prerequisites"></a>Vereisten

* Een Azure HDInsight-cluster met R Server geïnstalleerd. Zie voor instructies [aan de slag met R Server op HDInsight-clusters](hdinsight-hadoop-r-server-get-started.md).
* Een SSH-client. Voor Linux en Unix-distributies of Macintosh OS X, Hallo `ssh` opdracht wordt verstrekt met Hallo-besturingssysteem. Voor Windows, raden wij aan [Cygwin](http://www.redhat.com/services/custom/cygwin/) Hello [OpenSSH-optie](https://www.youtube.com/watch?v=CwYSvvGaiWU), of [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a>RStudio installeren op Hallo-cluster met een aangepast script

Hier volgen Hallo stappen:

1. Edge-knooppunt op Hallo van Hallo cluster identificeren. Voor een HDInsight-cluster met R Server volgt Hallo naamgevingsconventie voor hoofdknooppunt en edge-knooppunt.
   * Hoofdknooppunt`CLUSTERNAME-ssh.azurehdinsight.net`
   * Edge-knooppunt`CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. SSH in edge-knooppunt op Hallo van Hallo-cluster met behulp van een naamgevingspatroon Hallo vindt u in stap 1. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

3. Nadat u verbonden bent, worden een Hoofdgebruiker op Hallo-cluster. In Hallo SSH-sessie, gebruikt u Hallo volgende opdracht:

        sudo su -

4. Hallo aangepast script tooinstall RStudio downloaden. Hallo volgende opdracht gebruiken:

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. Hallo-machtigingen voor Hallo aangepast scriptbestand wijzigen en Hallo-script uitvoeren. Hallo volgende opdrachten gebruiken:

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. Als u een SSH-wachtwoord tijdens het maken van een HDInsight-cluster met R Server gebruikt, kunt u deze stap overslaan en doorgaan toohello naast. Als u een SSH-sleutel in plaats daarvan toocreate Hallo cluster gebruikt, moet u een wachtwoord instellen voor uw SSH-gebruiker. U hebt dit wachtwoord nodig om verbinding te maken tooRStudio. Voer Hallo volgende opdrachten:

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. Als u wordt gevraagd **huidige Kerberos-wachtwoord**, drukt u op **ENTER**.  Let op: u moet vervangen `USERNAME` met een SSH-gebruiker voor uw HDInsight-cluster. Als uw wachtwoord is correct ingesteld, worden er Hallo volgende bericht:

        passwd: password updated successfully

    Hallo SSH-sessie af te sluiten.

8. Maken van een SSH-tunnel toohello cluster door toe te wijzen `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` op Hallo HDInsight cluster toohello client-computer. Voordat u een nieuwe browsersessie opent, moet u een SSH-tunnel maken.

   * Op een Linux-client of een Windows-client met [Cygwin](http://www.redhat.com/services/custom/cygwin/), open een terminalsessie en gebruik Hallo volgende opdracht:

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       Vervang **gebruikersnaam** met een SSH-gebruiker voor uw HDInsight-cluster en vervang **CLUSTERNAME** met Hallo-naam van uw HDInsight-cluster.
       U kunt ook een SSH-sleutel in plaats van een wachtwoord gebruiken door toe te voegen `-i id_rsa_key`.        
   * Als een Windows-client met PuTTY vervolgens

     1. PuTTY opent en voert u de verbindingsgegevens.
     2. In Hallo **categorie** sectie toohello links van dialoogvenster hello, vouw **verbinding**, vouw **SSH**, en selecteer vervolgens **Tunnels**.
     3. Bieden de volgende informatie op Hallo Hallo **opties voor SSH-poort doorsturen** vorm:

        * **Bronpoort** -Hallo poort op de gewenste tooforward Hallo-client. Bijvoorbeeld: **8787**.
        * **Bestemming** - hello doel dat moet worden toegewezen toohello lokale client-computer. Bijvoorbeeld: **localhost:8787**.

            ![Maken van een SSH-tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "maken van een SSH-tunnel")

     4. Klik op **toevoegen** tooadd Hallo instellingen en klik vervolgens op **Open** tooopen een SSH-verbinding.
     5. Meld u desgevraagd in toohello server tooestablish een SSH-sessie en schakel Hallo-tunnel.

9. Open een webbrowser en voert u Hallo URL op basis van Hallo-poort die u hebt opgegeven voor het Hallo-tunnel te volgen:

        http://localhost:8787/ 

10. U bent na vragen aan gebruiker tooenter Hallo SSH gebruikersnaam en wachtwoord tooconnect toohello cluster. Als u een SSH-sleutel gebruikt tijdens het Hallo-cluster maken, moet u Hallo wachtwoord dat u in stap 5 hebt gemaakt.

    ![Rondleiding Studio verbinding](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "maken van een SSH-tunnel")

11. tootest of Hallo RStudio installatie voltooid is, kunt u een testscript dat wordt uitgevoerd op basis van R MapReduce en Spark taken op Hallo cluster kunt uitvoeren. toodownload hello test script toorun in RStudio, Ga terug toohello SSH-console en Voer Hallo volgende opdrachten:

    *    Als u een Hadoop-cluster met R gemaakt, gebruikt u deze opdracht:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    Als u een Spark-cluster met R gemaakt, gebruikt u deze opdracht:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. U ziet in RStudio, Hallo testen script die u hebt gedownload. Dubbelklik op Hallo bestand tooopen, selecteert u de inhoud Hallo van Hallo-bestand en klik vervolgens op **uitvoeren**. Hallo-uitvoer in Hallo **Console** deelvenster:

   ![Hallo-installatie testen](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Hallo-installatie testen")

Een andere optie zijn tootype `source(testhdi.r)` of `source(testhdi_spark.r)` tooexecute Hallo script.

## <a name="see-also"></a>Zie ook

* [COMPUTE context opties voor R Server op HDInsight-clusters](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opties voor Azure-opslag voor R Server op HDInsight](hdinsight-hadoop-r-server-storage.md)

