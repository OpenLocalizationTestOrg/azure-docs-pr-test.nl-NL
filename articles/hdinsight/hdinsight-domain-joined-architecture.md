---
title: Azure HDInsight-architectuur die lid zijn van aaaDomain | Microsoft Docs
description: Meer informatie over hoe tooplan domein HDInsight.
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
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>Azure Hadoop-clusters in aan domein gekoppelde HDInsight plannen

Hallo is traditionele Hadoop een cluster met één gebruiker. Dit is geschikt voor de meeste bedrijven met kleinere toepassingsteams die workloads met veel gegevens maken. Naarmate Hadoop populairder wordt, stappen veel bedrijven over op een model waarin clusters worden beheerd door IT-teams en meerdere toepassingsteams clusters delen. Dus Hallo functies met betrekking tot clusters met meerdere gebruikers zijn een van de meest aangevraagde functies in Azure HDInsight.

In plaats van het bouwen van een eigen voor meerdere gebruikers verificatie en autorisatie is HDInsight is afhankelijk van Hallo populairste id-provider--Active Directory (AD). Hallo krachtige beveiliging functie in AD kan worden gebruikt voor meerdere gebruikers autorisatie gebruikte toomanage in HDInsight. Door te integreren HDInsight met AD, kunt u communiceren met Hallo clusters met behulp van uw AD-referenties. HDInsight een AD gebruiker tooa lokale Hadoop gebruiker toegewezen, zodat alle services die worden uitgevoerd op HDInsight Hallo (Ambari, Hive-server, Zwerver, Spark thrift-server en andere) werken naadloos voor Hallo geverifieerde gebruiker.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>HDInsight integreren met AD- en AD op IaaS VM

Door te integreren HDInsight met Azure AD of AD op Iaas VM, zijn Hallo HDInsight clusterknooppunten van een domein tooa domein. HDInsight Hadoop-services uitgevoerd op Hallo cluster voor service-principals voor het Hallo maakt en binnen een opgegeven organisatie-eenheid (OE) in Azure AD of AD op IaaS VM geplaatst. HDInsight maakt ook omgekeerde DNS-toewijzingen in domein voor Hallo Hallo IP-adressen van Hallo knooppunten die lid toohello domein.

U kunt deze configuratie bereiken met behulp van verschillende architecturen. U kunt kiezen uit Hallo architecturen te volgen.

**HDInsight is geïntegreerd met AD uitgevoerd op Azure IaaS**

Dit is de eenvoudigste architectuur Hallo voor HDInsight integreren met Active Directory. Hallo AD-domeincontroller wordt uitgevoerd op een (of meerdere) virtuele machines (VM's) in Azure. Deze VM's bevinden zich meestal in een virtueel netwerk. U instellen een ander virtueel netwerk voor Hallo HDInsight-cluster. Voor HDInsight toohave een regel zicht tooActive Directory, moet u toopeer deze virtuele netwerken met behulp van [VNet-naar-VNet-peering](../virtual-network/virtual-network-create-peering.md). Als u Active Directory in ARM, Hallo vervolgens kunt u Hallo Active Directory en HDInsight in hetzelfde VNet Hallo en hoeft u geen toodo peering. 

![Topologie van aan domein gekoppeld HDInsight-cluster](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> In deze architectuur kunt u Azure Data Lake Store niet gebruiken met Hallo HDInsight-cluster.


Vereisten voor Active Directory:

* Een [organisatie-eenheid](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) moet worden gemaakt in die u plaatsen Hallo HDInsight-cluster virtuele machines en service-principals die zijn gebruikt door de cluster Hallo Hallo.
* [Lightweight Directory Access protocollen](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAPs) moeten worden ingesteld voor communicatie met AD. Hallo certificaat gebruikt tooset up LDAPS moet een echte certificaat (niet een zelfondertekend certificaat).
* Omgekeerde DNS-zones moeten worden gemaakt op Hallo domein voor Hallo IP-adresbereik van Hallo HDInsight subnet (bijvoorbeeld 10.2.0.0/24 in de vorige afbeelding Hallo).
* Een service-account of gebruikersaccount is vereist. Gebruik dit account toocreate hello HDInsight-cluster. Dit account moet beschikken over Hallo volgende machtigingen:

    - Machtigingen toocreate service principal en machineobjecten binnen de organisatie-eenheid Hallo
    - Machtigingen toocreate omgekeerde DNS-proxy regels
    - Machtigingen toojoin machines toohello Active Directory-domein

**HDInsight geïntegreerd met een alleen-cloud Azure AD**

Configureer een domeincontroller voor alleen-cloud Azure AD, zodat HDInsight kan worden geïntegreerd met Azure AD. Dit wordt bereikt door middel [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS). Azure AD DS domain controller machines op Hallo cloud maken en IP-adressen voor deze biedt. Voor maximale beschikbaarheid worden er twee domeincontrollers gemaakt.

Azure AD DS bestaat op dit moment alleen in klassieke virtuele netwerken. Dit is alleen toegankelijk via Hallo klassieke Azure-portal. Hallo HDInsight virtueel netwerk bestaat in hello Azure-portal, die toobe moet brengen met Hallo klassiek virtueel netwerk met behulp van VNet-naar-VNet-peering.

> [!NOTE]
> Peering tussen een klassiek virtueel netwerk en een Azure Resource Manager virtueel netwerk is vereist dat beide virtuele netwerken zich in dezelfde regio Hallo en Hallo onder dezelfde Azure-abonnement.

![Topologie van aan domein gekoppeld HDInsight-cluster](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Vereisten voor Azure AD:

* Een [organisatie-eenheid](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) moet worden gemaakt binnen die u plaatsen Hallo HDInsight-cluster virtuele machines en service-principals die zijn gebruikt door de cluster Hallo Hallo.
* Tijdens de configuratie van Azure AD DS moet [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) worden ingesteld. Hallo certificaat gebruikt tooset up LDAPS moet een echte certificaat (niet een zelfondertekend certificaat).
* Omgekeerde DNS-zones moeten worden gemaakt op Hallo domein voor Hallo IP-adresbereik van Hallo HDInsight subnet (bijvoorbeeld 10.2.0.0/24 in de vorige afbeelding Hallo).
* [Wachtwoord-hashes](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) moet worden gesynchroniseerd vanuit Azure AD tooAzure AD DS.
* Een service-account of gebruikersaccount is vereist. Gebruik dit account toocreate hello HDInsight-cluster. Dit account moet beschikken over Hallo volgende machtigingen:

    - Machtigingen toocreate service principal en machineobjecten binnen de organisatie-eenheid Hallo
    - Machtigingen toocreate omgekeerde DNS-proxy regels
    - Machtigingen toojoin machines toohello Azure AD-domein

## <a name="next-steps"></a>Volgende stappen
* Zie voor een domein HDInsight-cluster tooconfigure [HDInsight-clusters domein configureren](hdinsight-domain-joined-configure.md).
* toomanage domein HDInsight-clusters, Zie [domein HDInsight-clusters beheren](hdinsight-domain-joined-manage.md).
* Zie tooconfigure Hive-beleid en voer Hive-query's [configureren Hive-beleid voor HDInsight-clusters domein](hdinsight-domain-joined-run-hive.md).
* Zie toorun Hive-query's met behulp van SSH op HDInsight-clusters domein [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
