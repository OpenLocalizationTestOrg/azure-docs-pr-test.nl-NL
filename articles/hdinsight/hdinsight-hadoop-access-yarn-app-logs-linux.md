---
title: aaaAccess Hadoop YARN toepassing Logboeken op Linux gebaseerde HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooaccess YARN toepassingslogboeken op een HDInsight (Hadoop) op basis van Linux-cluster met behulp van Hallo opdrachtregelprogramma en een webbrowser.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>Toegang toepassingslogboeken YARN op Linux gebaseerde HDInsight

Meer informatie over hoe tooaccess Hallo logboeken voor toepassingen op een Hadoop-cluster in Azure HDInsight YARN (nog een andere Resource onderhandelaar).

> [!IMPORTANT]
> Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie voor meer informatie [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="YARNTimelineServer"></a>YARN tijdlijn Server

Hallo [YARN tijdlijn Server](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) bevat algemene informatie over het voltooide toepassingen en framework-specifieke toepassingsinformatie via twee verschillende interfaces. Specifiek:

* Opslaan en ophalen van informatie over algemene toepassing op HDInsight-clusters is ingeschakeld met versie 3.1.1.374 of hoger.
* Hallo framework-specifieke informatie toepassingsonderdeel Hallo tijdlijn Server is momenteel niet beschikbaar op HDInsight-clusters.

Algemene informatie over toepassingen bevat Hallo type gegevens te volgen:

* Hallo toepassings-ID, een unieke id van een toepassing
* Hallo-gebruiker die de toepassing hello heeft gestart
* Informatie over pogingen gedaan toocomplete Hallo toepassing
* Hallo-containers die worden gebruikt door een bepaalde toepassing poging

## <a name="YARNAppsAndLogs"></a>Logboeken en YARN-toepassingen

YARN biedt ondersteuning voor meerdere programmeermodellen (MapReduce wordt een van beide) door ontkoppeling bronbeheer van toepassing planning/bewaking. YARN maakt gebruik van een globale *ResourceManager* (RM) per worker-knooppunten *NodeManagers* (NMs) en per toepassing *ApplicationMasters* (AMs). Hallo onderhandelt per toepassing AM resources (CPU, geheugen, schijf-, netwerk) voor het uitvoeren van uw toepassing met Hallo RM. Hallo RM werkt met NMs toogrant deze resources die worden verleend als *containers*. Hallo AM is verantwoordelijk voor het volgen van Hallo voortgang van Hallo containers toegewezen tooit door Hallo RM. Een toepassing mogelijk veel containers, afhankelijk van de aard van de toepassing hello Hallo vereisen.

Elke toepassing kan bestaan uit meerdere *toepassing pogingen*. Als een toepassing mislukt, wordt deze opnieuw uitgevoerd als een nieuwe poging. Elke poging wordt uitgevoerd in een container. In een zin biedt een container Hallo context voor basic-eenheid van het werk dat door een YARN-toepassing uitgevoerd. Al het werk dat wordt uitgevoerd binnen de context van een container hello wordt uitgevoerd op één werkrolknooppunt Hallo op welke Hallo container is toegewezen. Zie [YARN concepten] [ YARN-concepts] voor verdere verwijzing.

Logboeken voor toepassingen Logboeken (en die zijn gekoppeld Hallo container) zijn essentieel bij het opsporen van fouten problematisch Hadoop-toepassingen. YARN biedt een nice framework voor het verzamelen, aggregeren en opslaan van de toepassingslogboeken van de Hello [logboek aggregatie] [ log-aggregation] functie. Hallo logboek aggregatie functie stelt de toegang tot toepassingslogboeken meer deterministische. Deze logboeken hierbij op alle containers op een knooppunt van de werknemer en worden opgeslagen als een samengevoegde logboekbestand per werkrolknooppunt. Hallo-logboek is opgeslagen op het standaardbestandssysteem Hallo nadat een toepassing is voltooid. Toepassingen kan gebruikmaken van honderden of duizenden containers, maar de logboeken voor alle containers die worden uitgevoerd op een knooppunt één werknemer zijn enkel bestand altijd geaggregeerde tooa. Er is daarom alleen 1 logboek per werkrolknooppunt gebruikt door de toepassing. Aggregatie van logboek is standaard op HDInsight-clusters versie 3.0 en hoger. Samengevoegde logboeken bevinden zich in de opslag van de standaard voor Hallo-cluster. in het pad naar Hallo is Hallo HDFS pad toohello Logboeken:

    /app-logs/<user>/logs/<applicationId>

In het vak Hallo pad `user` Hallo-naam van Hallo-gebruiker die de toepassing hello heeft gestart. Hallo `applicationId` is Hallo unieke id toegewezen tooan toepassing door Hallo YARN RM.

Hallo geaggregeerde logboeken zijn niet rechtstreeks kan worden gelezen, zoals ze zijn geschreven in een [TFile][T-file], [binaire indeling] [ binary-format] geïndexeerd door de container. Hallo die resourcemanager YARN-Logboeken of tooview van CLI-hulpprogramma's voor deze Logboeken gebruiken als tekst zonder opmaak voor toepassingen of containers van belang.

## <a name="yarn-cli-tools"></a>YARN CLI-hulpprogramma 's

toouse hello YARN CLI-hulpprogramma's, moet u eerst toohello HDInsight-cluster via SSH verbinden. Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

U kunt deze logboeken als tekst zonder opmaak weergeven door een van de volgende opdrachten Hallo uitgevoerd:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

Geef Hallo &lt;applicationId >, &lt;-die-slag-de-gebruikerstoepassing >, &lt;containerId >, en &lt;worker-knooppunt-adres > informatie wanneer deze opdrachten uit te voeren.

## <a name="yarn-resourcemanager-ui"></a>Gebruikersinterface van YARN ResourceManager

Hallo gebruikersinterface van YARN-ResourceManager op Hallo cluster headnode wordt uitgevoerd. Deze is toegankelijk via Hallo Ambari-webgebruikersinterface. Gebruik hello te volgen stappen tooview hello YARN-Logboeken:

1. Navigeer in uw webbrowser toohttps://CLUSTERNAME.azurehdinsight.net. Vervang CLUSTERNAME door Hallo-naam van uw HDInsight-cluster.
2. Selecteer in de lijst met services aan de linkerkant Hallo Hallo **YARN**.

    ![Yarn service geselecteerd](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. Van Hallo **snelkoppelingen** vervolgkeuzelijst, selecteer een van de hoofdknooppunten Hallo-cluster en selecteer vervolgens **ResourceManager logboek**.

    ![Yarn snelle koppelingen](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    Krijgt u een lijst met koppelingen tooYARN Logboeken.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
