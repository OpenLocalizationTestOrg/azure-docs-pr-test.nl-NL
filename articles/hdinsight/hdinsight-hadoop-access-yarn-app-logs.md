---
title: aaaAccess Hadoop YARN toepassing Logboeken programmatisch - Azure | Microsoft Docs
description: De toegangstoepassing aanmeldt via een programma een Hadoop-cluster in HDInsight.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>Toegang toepassingslogboeken YARN op HDInsight op basis van Windows
Dit onderwerp wordt uitgelegd hoe tooaccess Hallo logboeken voor YARN (nog een andere Resource onderhandelaar)-toepassingen die u opgegeven op een Windows gebaseerde Hadoop-cluster in Azure HDInsight hebt

> [!IMPORTANT]
> Hallo-informatie in dit document is van toepassing alleen op basis van tooWindows HDInsight-clusters. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie. Zie voor informatie over YARN toegang tot op Linux gebaseerde HDInsight-clusters Logboeken, [toepassingslogboeken op Linux gebaseerde Hadoop op HDInsight YARN toegang](hdinsight-hadoop-access-yarn-app-logs-linux.md)
>


### <a name="prerequisites"></a>Vereisten
* Een Windows gebaseerde HDInsight-cluster.  Zie [Windows maken op basis van een Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="yarn-timeline-server"></a>YARN tijdlijn Server
Hallo <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN tijdlijn Server</a> bevat algemene informatie over het voltooide toepassingen ook als framework-specifieke toepassingsinformatie via twee verschillende interfaces. Specifiek:

* Opslaan en ophalen van informatie over algemene toepassing op HDInsight-clusters is ingeschakeld met versie 3.1.1.374 of hoger.
* Hallo framework-specifieke informatie toepassingsonderdeel Hallo tijdlijn Server is momenteel niet beschikbaar op HDInsight-clusters.

Algemene informatie over toepassingen bevat Hallo soorten gegevens te volgen:

* Hallo toepassings-ID, een unieke id van een toepassing
* Hallo-gebruiker die de toepassing hello heeft gestart
* Informatie over pogingen gedaan toocomplete Hallo toepassing
* Hallo-containers die worden gebruikt door een bepaalde toepassing poging

Op uw HDInsight-clusters, wordt deze informatie wordt opgeslagen door Azure Resource Manager tooa geschiedenis opslaan in de standaardcontainer Hallo van uw Azure Storage-standaardaccount. Deze algemene gegevens voor voltooide toepassingen kan worden opgehaald via een REST-API:

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>Logboeken en YARN-toepassingen
YARN biedt ondersteuning voor meerdere programmeermodellen (MapReduce wordt een van beide) door ontkoppeling bronbeheer van toepassing planning/bewaking. Dit wordt gedaan door een globale *ResourceManager* (RM) per worker-knooppunten *NodeManagers* (NMs) en per toepassing *ApplicationMasters* (AMs). Hallo onderhandelt per toepassing AM resources (CPU, geheugen, schijf-, netwerk) voor het uitvoeren van uw toepassing met Hallo RM. Hallo RM werkt met NMs toogrant deze resources die worden verleend als *containers*. Hallo AM is verantwoordelijk voor het volgen van Hallo voortgang van Hallo containers toegewezen tooit door Hallo RM. Een toepassing mogelijk veel containers, afhankelijk van de aard van de toepassing hello Hallo vereisen.

Bovendien elke toepassing kan bestaan uit meerdere *toepassing pogingen* in volgorde toofinish in Hallo aanwezigheid van het vastlopen of vervaldatum toohello verlies van communicatie tussen een uur en een RM. Daarom containers tooa specifieke poging van een toepassing krijgen. In een zin een container biedt Hallo context voor basic-eenheid van uitgevoerd door een toepassing YARN werk en al het werk dat wordt uitgevoerd binnen de context van een container hello wordt uitgevoerd op één werkrolknooppunt Hallo op welke Hallo container is toegewezen. Zie [YARN concepten] [ YARN-concepts] voor verdere verwijzing.

Logboeken voor toepassingen Logboeken (en die zijn gekoppeld Hallo container) zijn essentieel bij het opsporen van fouten problematisch Hadoop-toepassingen. YARN biedt een nice framework voor het verzamelen, aggregeren en opslaan van de toepassingslogboeken van de Hello [logboek aggregatie] [ log-aggregation] functie. Hallo logboek aggregatie functie kunt u toegang tot toepassingslogboeken meer deterministische naar Logboeken hierbij op alle containers op een knooppunt van de werknemer en worden opgeslagen als een samengevoegde logboekbestand per knooppunt van de werknemer op Hallo standaardbestandssysteem nadat een toepassing is voltooid. Toepassingen kan gebruikmaken van honderden of duizenden containers logboeken voor alle containers worden uitgevoerd op een enkele werkrolknooppunt altijd worden echter geaggregeerde tooa enkel bestand, wat resulteert in één logboek per werkrolknooppunt gebruikt door de toepassing. Aggregatie van logboek is standaard ingeschakeld op HDInsight-clusters (versie 3.0 en hoger), en geaggregeerde logboeken kunnen worden gevonden in de standaardcontainer Hallo van uw cluster op Hallo locatie te volgen:

    wasb:///app-logs/<user>/logs/<applicationId>

Op die locatie *gebruiker* Hallo naam is van het Hallo-gebruiker die het Hallo-toepassing is gestart en *applicationId* is de unieke id van de Hallo van een toepassing die is toegewezen door Hallo YARN RM.

Hallo geaggregeerde logboeken zijn niet rechtstreeks kan worden gelezen, zoals ze zijn geschreven in een [TFile][T-file], [binaire indeling] [ binary-format] geïndexeerd door de container. YARN biedt toodump van CLI-hulpprogramma's voor deze logboeken als tekst zonder opmaak voor toepassingen of containers van belang. U kunt deze logboeken als tekst zonder opmaak weergeven door het uitvoeren van een van de Hallo YARN opdrachten rechtstreeks op de clusterknooppunten hello (na tooit verbinden via RDP) te volgen:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>Gebruikersinterface van YARN ResourceManager
Hallo gebruikersinterface van YARN-ResourceManager op Hallo cluster headnode wordt uitgevoerd en toegankelijk zijn via hello Azure-portaldashboard:

1. Aanmelden te[Azure-portal](https://portal.azure.com/).
2. Klik op Hallo linkermenu **Bladeren**, klikt u op **HDInsight-Clusters**, klikt u op een cluster op basis van Windows die u wilt tooaccess Hallo YARN-Logboeken.
3. Klik op het bovenste menu Hallo **Dashboard**. Ziet u een pagina in een nieuwe browser geopend tabblad aangeroepen **HDInsight Query Console**.
4. Van **HDInsight Query Console**, klikt u op **gebruikersinterface van Yarn**.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
