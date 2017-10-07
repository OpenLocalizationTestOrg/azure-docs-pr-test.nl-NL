---
title: aaaManage domein HDInsight-clusters - Azure | Microsoft Docs
description: Meer informatie over hoe toomanage domein HDInsight-clusters
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a>Domein-HDInsight-clusters (Preview) beheren
Informatie over het Hallo-gebruikers en Hallo rollen in HDInsight domein en hoe toomanage domein HDInsight-clusters.

## <a name="users-of-domain-joined-hdinsight-clusters"></a>Gebruikers van domein HDInsight-clusters
Een HDInsight-cluster is niet domein heeft twee accounts van gebruikers die zijn gemaakt tijdens het Hallo-cluster maken:

* **Ambari admin**: dit account wordt ook wel *Hadoop gebruiker* of *HTTP gebruiker*. Dit account kan worden gebruikt toolog op tooAmbari op https://&lt;clustername >. azurehdinsight.net. Het kan ook gebruikte toorun query's op de Ambari-weergaven worden, -taken via externe hulpprogramma's (dat wil zeggen PowerShell, Templeton, Visual Studio) uitvoeren en verificatie met de Hallo Hive ODBC-stuurprogramma en BI-tools (dat wil zeggen Excel, Power BI of Tableau).
* **SSH-gebruiker**: dit account kan worden gebruikt met SSH en sudo-opdrachten uit te voeren. Hoofdmap bevoegdheden toohello Linux VM's heeft.

Een domein HDInsight-cluster bevat drie nieuwe gebruikers toevoegen tooAmbari Admin en SSH-gebruiker.

* **Zwerver admin**: dit account is lokale Apache Zwerver Hallo-beheeraccount. Het is niet een gebruiker met active directory-domein. Dit account worden gebruikt toosetup beleidsregels en zorgen dat andere gebruikers, beheerders of gedelegeerde beheerders (zodat die gebruikers u beleid beheren kunnen). Hallo-gebruikersnaam is standaard *admin* en Hallo wachtwoord is hetzelfde als het beheerderswachtwoord Ambari Hallo Hallo. Hallo wachtwoord kan worden bijgewerkt vanuit de instellingenpagina Hallo in Zwerver.
* **Gebruiker met beheerdersrechten domein cluster**: dit account is een active directory-domeingebruiker aangewezen als het Hadoop-cluster admin zoals Ambari en Zwerver Hallo. Tijdens het maken van het cluster moet u de referenties van deze gebruiker opgeven. Deze gebruiker heeft Hallo volgende bevoegdheden:

  * Lid worden van domein van machines toohello en plaats deze in Hallo organisatie-eenheid die u tijdens het maken van het cluster opgeeft.
  * Service-principals binnen Hallo organisatie-eenheid die u tijdens het maken van een cluster opgeeft maken.
  * Omgekeerde DNS-vermeldingen te maken.

    Opmerking Hallo andere AD-gebruikers hebben deze rechten.

    Er zijn een aantal eindpunten binnen Hallo-cluster (bijvoorbeeld Templeton) die niet worden beheerd door Zwerver en daarom zijn niet beveiligd. Deze eindpunten zijn vergrendeld voor alle gebruikers behalve Hallo cluster admin domeingebruiker.
* **Reguliere**: tijdens het maken van het cluster, kunt u meerdere active directory-groepen opgeven. Hallo-gebruikers in deze groepen worden gesynchroniseerde tooRanger en Ambari. Deze gebruikers zijn domeingebruikers en heeft toegang tot tooonly Zwerver beheerde eindpunten (bijvoorbeeld Hiveserver2). Alle beleidsregels RBAC Hallo en controle zijn van toepassing toothese gebruikers.

## <a name="roles-of-domain-joined-hdinsight-clusters"></a>Rollen zijn van een domein HDInsight-clusters
HDInsight domein hebben Hallo rollen te volgen:

* Clusterbeheer
* Cluster-Operator
* Servicebeheerder
* Service-Operator
* Cluster-gebruiker

**toosee hello machtigingen van deze rollen**

1. Open Hallo Ambari Management gebruikersinterface.  Zie [Open Hallo Ambari Management UI](#open-the-ambari-management-ui).
2. In het linkermenu hello, klikt u op **rollen**.
3. Klik op Hallo blauw vraagteken toosee Hallo machtigingen:

    ![HDInsight-rolmachtigingen domein](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a>Hallo Ambari Management UI openen
1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).
2. Open uw HDInsight-cluster in een blade. Zie [lijst en geeft weer clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).
3. Klik op **Dashboard** van Hallo bovenste menu tooopen Ambari.
4. Meld u aan tooAmbari met Hallo cluster administrator domeingebruikersnaam en wachtwoord.
5. Klik op Hallo **Admin** vervolgkeuzemenu van Hallo rechterbovenhoek en klik vervolgens op **Ambari beheren**.

    ![HDInsight domein Ambari beheren](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    Hallo UI ziet eruit als:

    ![Domein HDInsight Ambari de gebruikersinterface voor beheer](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a>Lijst van domeingebruikers Hallo gesynchroniseerd vanuit uw Active Directory
1. Open Hallo Ambari Management gebruikersinterface.  Zie [Open Hallo Ambari Management UI](#open-the-ambari-management-ui).
2. In het linkermenu hello, klikt u op **gebruikers**. U ziet alle Hallo gebruikers synchroniseren met uw Active Directory toohello HDInsight-cluster.

    ![Domein HDInsight Ambari management UI gebruikers weergeven](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a>Lijst Hallo domeingroepen gesynchroniseerd vanuit uw Active Directory
1. Open Hallo Ambari Management gebruikersinterface.  Zie [Open Hallo Ambari Management UI](#open-the-ambari-management-ui).
2. In het linkermenu hello, klikt u op **groepen**. U ziet alle Hallo groepen gesynchroniseerd vanuit uw Active Directory toohello HDInsight-cluster.

    ![Domein HDInsight Ambari-gebruikersinterface lijst beheergroepen](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a>Hive-weergaven machtigingen configureren
1. Open Hallo Ambari Management gebruikersinterface.  Zie [Open Hallo Ambari Management UI](#open-the-ambari-management-ui).
2. In het linkermenu hello, klikt u op **weergaven**.
3. Klik op **HIVE** tooshow Hallo details.

    ![Domein HDInsight Ambari management UI Hive-weergaven](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. Klik op Hallo **Hive-weergave** tooconfigure Hive-weergaven koppelen.
5. Schuif omlaag toohello **machtigingen** sectie.

    ![Domein HDInsight Ambari management UI Hive-weergaven machtigingen configureren](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. Klik op **gebruiker toevoegen** of **groep toevoegen**, en geef vervolgens Hallo gebruikers of groepen die Hive-weergaven kunnen gebruiken.

## <a name="configure-users-for-hello-roles"></a>Gebruikers voor Hallo rollen configureren
 Zie voor een lijst met functies en hun machtigingen toosee [rollen van domein HDInsight-clusters](#roles-of-domain---joined-hdinsight-clusters).

1. Open Hallo Ambari Management gebruikersinterface.  Zie [Open Hallo Ambari Management UI](#open-the-ambari-management-ui).
2. In het linkermenu hello, klikt u op **rollen**.
3. Klik op **gebruiker toevoegen** of **groep toevoegen** tooassign gebruikers en groepen toodifferent rollen.

## <a name="next-steps"></a>Volgende stappen
* Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren) om een HDInsight-cluster te configureren dat is gekoppeld aan een domein.
* Zie [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Hive-beleid configureren voor aan een domein gekoppelde HDInsight-clusters) om Hive-beleid te configureren en Hive-query's uit te voeren.
* Zie voor het uitvoeren van Hive-query's met SSH op domein HDInsight-clusters [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
