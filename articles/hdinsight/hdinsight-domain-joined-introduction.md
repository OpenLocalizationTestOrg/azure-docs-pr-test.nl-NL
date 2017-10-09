---
title: aaaHadoop security - HDInsight-clusters domein - Azure | Microsoft Docs
description: Meer informatie...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/31/2016
ms.author: saurinsh
ms.openlocfilehash: 5a9469402a61bcba4017e1ff4bd06dfba23ac963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toohadoop-security-with-domain-joined-hdinsight-clusters-preview"></a>Een inleiding tooHadoop-beveiliging met HDInsight-clusters domein (Preview)

Tot nu toe werd in Azure HDInsight alleen ondersteuning geboden voor één lokale beheerder voor gebruikers. Dit werkte heel goed voor kleinere toepassingsteams of afdelingen. Klasse-mogelijkheden, zoals active directory verificatie, ondersteuning voor meerdere gebruikers en rollen gebaseerd toegangsbeheer gebaseerde is geworden als Hadoop op basis werkbelastingen die is opgedaan meer populariteit in Hallo enterprise sector hello nodig hebt voor enterprise steeds belangrijker. Domein-HDInsight-clusters gebruikt, kunt u een HDInsight-cluster die lid zijn van tooan Active Directory-domein maken, een lijst met werknemers van Hallo enterprise die kunnen worden geverifieerd via Azure Active Directory-toolog op tooHDInsight cluster configureren. Iedereen buiten de onderneming Hallo kan niet aanmelden of Hallo HDInsight-cluster. Hallo ondernemingsadministrator kunt configureren op rollen gebaseerd toegangsbeheer voor het gebruik van Hive-beveiliging [Apache Zwerver](http://hortonworks.com/apache/ranger/), dus beperken van toegang tot toodata tooonly zoveel nodig. Ten slotte Hallo beheerder toegang tot gegevens door werknemers Hallo kunt controleren en eventuele wijzigingen die zijn gedaan tooaccess toegangsbeheerbeleid, dus een hoge mate van toezicht van hun zakelijke bronnen te bereiken.

> [!NOTE]
> Hallo nieuwe functies die worden beschreven in dit voorbeeld zijn alleen beschikbaar op Linux gebaseerde HDInsight-clusters voor Hive-werkbelasting. Hallo van andere werkbelastingen, zoals HBase, Spark, Storm en Kafka, worden ingeschakeld in toekomstige releases.

> [!IMPORTANT]
> Oozie is niet ingeschakeld op HDInsight domein.

## <a name="benefits"></a>Voordelen
Bedrijfsbeveiliging bestaat uit vier kernonderdelen: perimeterbeveiliging, verificatie, autorisatie en versleuteling.

![De voordelen van HDInsight-clusters die zijn gekoppeld aan een domein](./media/hdinsight-domain-joined-introduction/hdinsight-domain-joined-four-pillars.png).

### <a name="perimeter-security"></a>Perimeterbeveiliging
Perimeterbeveiliging in HDInsight wordt bereikt met virtuele netwerken en de Gateway-service. Vandaag de dag kunt een ondernemingsadministrator maken van een HDInsight-cluster in een virtueel netwerk en Netwerkbeveiligingsgroepen (inkomend of uitgaand firewallregels) toorestrict toegang toohello virtueel netwerk gebruiken. Alleen hello IP-adressen die zijn gedefinieerd in Hallo inkomende worden firewall-regels kunnen toocommunicate met Hallo HDInsight-cluster, zodat de beveiliging van de. Een andere perimeterbeveiligingslaag wordt tot stand gebracht via de Gateway-service. Hallo Gateway is Hallo-service die als de eerste regel verdediging voor elke inkomende aanvraag toohello HDInsight-cluster fungeert. Het Hallo-aanvraag heeft geaccepteerd, wordt deze gevalideerd en kan alleen dan Hallo aanvraag toopass toohello andere knooppunten in cluster, zodat beveiliging tooother naam en het gegevenstype knooppunten in cluster Hallo.

### <a name="authentication"></a>Authentication
Met deze openbare preview-versie kan een bedrijfsbeheerder in een [virtueel netwerk](https://azure.microsoft.com/services/virtual-network/) een HDInsight-cluster inrichten dat is toegevoegd aan een domein. Hallo-knooppunten van het HDInsight-cluster Hallo worden gekoppelde toohello domein worden beheerd door Hallo enterprise. Dit wordt bewerkstelligd via [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md). Alle Hallo knooppunten in cluster Hallo zijn van een domein gekoppelde tooa die Hallo enterprise beheert. Met deze instellingen kunnen Hallo enterprise werknemers zich aanmelden op clusterknooppunten toohello met hun domeinreferenties. Ze kunnen ook hun referenties domein tooauthenticate gebruiken met andere goedgekeurde eindpunten zoals Hue, Ambari-weergaven, ODBC, JDBC, PowerShell en REST-API's toointeract met Hallo-cluster. Hallo beheerder heeft volledige controle over het beperken van het aantal gebruikers interactie met Hallo-cluster via deze eindpunten Hallo.

### <a name="authorization"></a>Autorisatie
Aanbevolen gevolgd door de meeste bedrijven is dat niet alle werknemers toegang tooall ondernemingsresources heeft. Hallo beheerder kunt ook met deze release definiëren op rollen gebaseerd beleid voor toegangsbeheer voor Hallo clusterbronnen. Bijvoorbeeld Hallo beheerder kan configureren [Apache Zwerver](http://hortonworks.com/apache/ranger/) tooset toegangscontrolebeleid voor Hive. Deze functionaliteit ervoor te zorgen dat werknemers alleen kunnen tooaccess worden net zoveel gegevens naar toobe geslaagde in hun werk behoefte. SSH toegang toohello cluster is ook beperkte alleen toohello-beheerder.

### <a name="auditing"></a>Controleren
Samen met het beveiligen van Hallo HDInsight clusterbronnen tegen onbevoegde gebruikers en de beveiliging van gegevens van hello, controle van alle toegang tot de clusterbronnen toohello en Hallo gegevens nodig tootrack zijn niet-geautoriseerde of met opzet toegang van Hallo resources. Met deze preview Hallo beheerder weergeven en alle toegang tot toohello HDInsight-clusterbronnen en gegevens te rapporteren. Hallo beheerder kunt weergeven en alle wijzigingen toohello toegangscontrolebeleid gedaan in Apache Zwerver rapport eindpunten ondersteund. Hallo bekend Apache Zwerver UI toosearch controlelogboeken maakt gebruik van een domein HDInsight-cluster. Op de back-end van Hallo Zwerver gebruikt [Apache Solr](http://hortonworks.com/apache/solr/) voor het opslaan en doorzoeken Hallo Logboeken.

### <a name="encryption"></a>Versleuteling
Beveiligen van gegevens is belangrijk voor beveiliging van de organisatie vergadering en nalevingsvereisten en samen met het beperken van toegang toodata van niet-geautoriseerde werknemers, deze moet ook zijn beveiligd door deze te coderen. Beide Hallo gegevensarchieven voor HDInsight-clusters, Azure Storage-Blob en Azure Data Lake Storage ondersteuning voor transparante serverzijde [versleuteling van gegevens](../storage/common/storage-service-encryption.md) in rust. Beveiligde HDInsight-clusters werken naadloos samen met deze mogelijkheid tot versleuteling van data-at-rest aan de serverzijde.

## <a name="next-steps"></a>Volgende stappen
* Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren) om een HDInsight-cluster te configureren dat is gekoppeld aan een domein.
* Zie [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Aan een domein gekoppelde HDInsight-clusters beheren) om HDInsight-clusters te beheren die zijn gekoppeld aan een domein.
* Zie [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Hive-beleid configureren voor aan een domein gekoppelde HDInsight-clusters) om Hive-beleid te configureren en Hive-query's uit te voeren.
* Zie voor het uitvoeren van Hive-query's met SSH op domein HDInsight-clusters [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
