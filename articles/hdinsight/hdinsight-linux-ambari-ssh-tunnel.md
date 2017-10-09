---
title: aaaUse SSH tunneling tooaccess Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe een SSH-tunnel toosecurely toouse bladeren webbronnen gehost op uw HDInsight op basis van Linux-knooppunten.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a>SSH-Tunneling tooaccess Ambari-webgebruikersinterface, JobHistory, NameNode, Oozie en andere web UI gebruiken

Linux gebaseerde HDInsight-clusters bieden toegang tooAmbari webgebruikersinterface via Internet hello, maar sommige functies van Hallo gebruikersinterface zijn niet. Bijvoorbeeld, Hallo-webgebruikersinterface voor andere services die via Ambari worden opgehaald. Voor volledige functionaliteit van Hallo Ambari-webgebruikersinterface, moet u een SSH-tunnel toohello cluster head.

## <a name="why-use-an-ssh-tunnel"></a>Waarom gebruikt een SSH-tunnel

Een aantal menu's Hallo in Ambari werken alleen via een SSH-tunnel. Deze menu's zijn afhankelijk van websites en services worden uitgevoerd op andere knooppunttypen zoals worker-knooppunten. Vaak deze websites zijn niet beveiligd, zodat het niet veilig toodirectly zichtbaar Hallo ze op internet.

Hallo Web UI na vereisen een SSH-tunnel:

* JobHistory
* NameNode
* Thread-Stacks
* Oozie-webgebruikersinterface
* HBase hoofd- en logboeken gebruikersinterface

Als u uw cluster scriptacties toocustomize gebruiken, vereisen geen services of hulpprogramma's die u installeert die een web-UI zichtbaar een SSH-tunnel. Bijvoorbeeld, als u Hue met behulp van een scriptactie installeren, moet u een SSH-tunnel tooaccess Hallo Hue-webgebruikersinterface.

> [!IMPORTANT]
> Als u directe toegang tooHDInsight via een virtueel netwerk hebt, hoeft u geen toouse SSH-tunnels. Zie voor een voorbeeld van rechtstreeks toegang hebben tot HDInsight via een virtueel netwerk, Hallo [verbinding maken met HDInsight tooyour on-premises netwerk](connect-on-premises-network.md) document.

## <a name="what-is-an-ssh-tunnel"></a>Wat is een SSH-tunnel

[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) tooa poort verzonden op uw lokale werkstation verkeer gerouteerd. Hallo-verkeer wordt gerouteerd via een SSH-verbinding tooyour HDInsight-cluster hoofdknooppunt. Hallo-aanvraag is opgelost, alsof deze afkomstig van het hoofdknooppunt Hallo is. antwoord Hallo wordt vervolgens doorgestuurd teruggestuurd via Hallo tunnel tooyour werkstation.

## <a name="prerequisites"></a>Vereisten

* Een SSH-client. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

* Een webbrowser die kan worden geconfigureerd toouse SOCKS5 proxy.

    > [!WARNING]
    > Hallo SOCKS-proxy-ondersteuning is ingebouwd in Windows biedt geen ondersteuning voor SOCKS5 en werkt niet met Hallo stappen in dit document. Hallo volgende browsers zijn afhankelijk van de proxy-instellingen voor Windows, en niet op dit moment werken met Hallo stappen in dit document:
    >
    > * Microsoft Edge
    > * Microsoft Internet Explorer
    >
    > Google Chrome is ook afhankelijk van Hallo Windows proxy-instellingen. U kunt echter de uitbreidingen die ondersteuning bieden voor SOCKS5 installeren. Het is raadzaam [FoxyProxy standaard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).

## <a name="usessh"></a>Hallo SSH-opdracht met een tunnel maken

Gebruik Hallo volgende opdracht toocreate een SSH-tunnel met Hallo `ssh` opdracht. Vervang **gebruikersnaam** met een SSH-gebruiker voor uw HDInsight-cluster en vervang **CLUSTERNAME** met Hallo-naam van uw HDInsight-cluster:

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

Deze opdracht maakt u een verbinding die verkeer toolocal poort 9876 toohello cluster via SSH van routes. Hallo-opties zijn:

* **D 9876** -lokale poort waarmee verkeer via de tunnel Hallo Hallo.
* **C** -alle gegevens te comprimeren omdat webverkeer voornamelijk tekst is.
* **2** -force SSH tootry protocolversie 2 alleen.
* **q** -stille modus.
* **T** -toewijzing van de pseudo-tty uitschakelen omdat we zojuist een poort doorstuurt.
* **n**-Voorkomen dat het lezen van STDIN, aangezien we zojuist een poort doorstuurt.
* **N** -een externe opdracht niet uitvoeren omdat er slechts een poort doorstuurt.
* **f** -Hallo achtergrond uitvoeren.

Zodra het Hallo-opdracht is voltooid, is verkeer dat wordt verzonden tooport 9876 op de lokale computer Hallo gerouteerde toohello cluster hoofdknooppunt.

## <a name="useputty"></a>Maken van een tunnel met PuTTY

[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) een grafische SSH-client voor Windows. Hallo stappen toocreate na een SSH-tunnel met PuTTY gebruiken:

1. PuTTY opent en voert u de verbindingsgegevens. Als u niet bekend met PuTTY bent, raadpleegt u Hallo [PuTTY-documentatie (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).

2. In Hallo **categorie** sectie toohello links van dialoogvenster hello, vouw **verbinding**, vouw **SSH**, en selecteer vervolgens **Tunnels**.

3. Bieden de volgende informatie op Hallo Hallo **opties voor SSH-poort doorsturen** vorm:
   
   * **Bronpoort** -Hallo poort op de gewenste tooforward Hallo-client. Bijvoorbeeld: **9876**.

   * **Bestemming** -Hallo SSH-adres voor Hallo Linux gebaseerde HDInsight-cluster. Bijvoorbeeld **mijncluster-ssh.azurehdinsight.net**.

   * **Dynamisch**: hiermee schakelt u de dynamische routering van SOCKS-proxy's in.
     
     ![afbeelding van de opties-tunneling](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. Klik op **toevoegen** tooadd Hallo instellingen en klik vervolgens op **Open** tooopen een SSH-verbinding.

5. Wanneer u wordt gevraagd, meld u bij toohello-server.

## <a name="use-hello-tunnel-from-your-browser"></a>Hallo-tunnel vanuit de browser gebruiken

> [!IMPORTANT]
> Hallo stappen in deze sectie gebruik Hallo Mozilla FireFox browser, aangezien deze Hallo dezelfde proxy-instellingen voor alle platforms biedt. Andere moderne browsers, zoals Google Chrome moet mogelijk een extensie zoals FoxyProxy toowork met Hallo-tunnel.

1. Configureer Hallo browser toouse **localhost** en het Hallo-poort die u hebt gebruikt toen maken Hallo tunnel als een **SOCKS v5** proxy. Hier ziet u hoe Hallo Firefox instellingen eruit. Als u een andere poort dan 9876 gebruikt, wijzigen Hallo poort toohello die u gebruikt:
   
    ![afbeelding van Firefox instellingen](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > Selecteren **externe DNS** wordt omgezet Domain Name System (DNS)-aanvragen via Hallo HDInsight-cluster. Deze instelling wordt omgezet DNS met Hallo hoofdknooppunt van Hallo-cluster.

2. Controleer of deze tunnel Hallo werkt via een site, zoals [http://www.whatismyip.com/](http://www.whatismyip.com/). Hallo IP geretourneerd een dient te worden door Microsoft Azure-datacenter Hallo.

## <a name="verify-with-ambari-web-ui"></a>Controleer met Ambari-webgebruikersinterface

Zodra het Hallo-cluster is ingesteld, gebruikt u hello te volgen stappen tooverify dat u service-web UI vanaf Hallo Ambari Web openen kunt:

1. Ga in uw browser toohttp://headnodehost:8080. Hallo `headnodehost` adres wordt verzonden via Hallo tunnel toohello cluster en toohello headnode die Ambari wordt uitgevoerd op te lossen. Wanneer u wordt gevraagd, typt u Hallo-beheerdersgebruikersnaam (admin) en het wachtwoord voor uw cluster. U wordt mogelijk gevraagd een tweede maal door Hallo Ambari-webgebruikersinterface. Als dit het geval is, voert u Hallo gegevens opnieuw.

   > [!NOTE]
   > Wanneer u Hallo http://headnodehost:8080 adres tooconnect toohello cluster gebruikt, wordt u verbinding maakt via Hallo-tunnel. Communicatie wordt beveiligd met Hallo SSH-tunnel in plaats van HTTPS. tooconnect meer dan Hallo internet met behulp van HTTPS, gebruikt u https://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** Hallo-naam van Hallo-cluster.

2. Selecteer in de lijst Hallo op Hallo links van de pagina Hallo Hallo Ambari-Webgebruikersinterface, HDFS.

    ![Afbeelding met HDFS geselecteerd](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. Wanneer Hallo HDFS-service-informatie wordt weergegeven, selecteert u **snelkoppelingen**. Een lijst van head clusterknooppunten hello wordt weergegeven. Selecteer een van de hoofdknooppunten Hallo en selecteer vervolgens **NameNode UI**.

    ![De installatiekopie met de Hallo QuickLinks menu uitgevouwen](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > Wanneer u selecteert __snelkoppelingen__, krijgt u mogelijk een indicator wacht. Dit probleem kan optreden als u een trage internetverbinding hebben. Wacht een minuut of twee Hallo gegevens toobe ontvangen van Hallo-server en probeer het opnieuw Hallo-lijst.
   >
   > Een aantal invoergegevens in Hallo **snelkoppelingen** menu kan worden genegeerd door de rechterkant Hallo van welkomstscherm. Zo ja, vouw Hallo menu met de muis en gebruiken van Hallo pijl naar rechts sleutel tooscroll Hallo scherm toohello juiste toosee Hallo rest van Hallo-menu.

4. Een pagina vergelijkbaar toohello volgende afbeelding wordt weergegeven:

    ![Afbeelding van Hallo NameNode UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > Let op Hallo-URL voor deze pagina. moet vergelijkbaar te**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**. Deze URI gebruikt Hallo interne volledig gekwalificeerde domeinnaam (FQDN) van Hallo-knooppunt en is alleen toegankelijk wanneer u een SSH-tunnel.

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toocreate en gebruikt een SSH-tunnel Hallo volgende document voor andere manieren toouse Ambari zien:

* [HDInsight-clusters beheren met Ambari](hdinsight-hadoop-manage-ambari.md)

Zie voor meer informatie over het gebruik van SSH met HDInsight [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

