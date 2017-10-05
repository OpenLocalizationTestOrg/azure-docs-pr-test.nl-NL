---
title: Domein Azure HDInsight-architectuur | Microsoft Docs
description: Meer informatie over het plannen van aan domein gekoppelde HDInsight.
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
ms.openlocfilehash: 7e34f47f09466a40993b4cc797ff1cad2bdaeafe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>Azure Hadoop-clusters in aan domein gekoppelde HDInsight plannen

Het traditionele Hadoop is een cluster met één gebruiker. Dit is geschikt voor de meeste bedrijven met kleinere toepassingsteams die workloads met veel gegevens maken. Naarmate Hadoop populairder wordt, stappen veel bedrijven over op een model waarin clusters worden beheerd door IT-teams en meerdere toepassingsteams clusters delen. Daarom zijn functies met clusters voor meerdere gebruikers onder de meest gevraagde functies in Azure HDInsight.

In plaats van het bouwen van een eigen voor meerdere gebruikers verificatie en autorisatie is HDInsight is afhankelijk van de meest populaire id-provider--Active Directory (AD). De krachtige beveiligingsfuncties in AD kan worden gebruikt voor het beheren van meerdere gebruikers autorisatie in HDInsight. Door te integreren HDInsight met AD, kunt u communiceren met de clusters met behulp van uw AD-referenties. Een AD-gebruiker wordt HDInsight toegewezen aan een gebruiker met lokale Hadoop, zodat alle services die worden uitgevoerd op HDInsight (Ambari, Hive-server, Zwerver, Spark thrift-server en andere) naadloos voor de geverifieerde gebruiker.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>HDInsight integreren met AD- en AD op IaaS VM

Door te integreren HDInsight met Azure AD of AD op Iaas VM, zijn de clusterknooppunten HDInsight domein is gekoppeld aan een domein. HDInsight maakt service-principals voor het Hadoop-services uitgevoerd op het cluster en binnen een opgegeven organisatie-eenheid (OE) in Azure AD of AD op IaaS VM geplaatst. HDInsight maakt ook omgekeerde DNS-toewijzingen in het domein voor de IP-adressen van de knooppunten die zijn gekoppeld aan het domein.

U kunt deze configuratie bereiken met behulp van verschillende architecturen. U kunt kiezen uit de volgende architecturen.

**HDInsight is geïntegreerd met AD uitgevoerd op Azure IaaS**

Dit is de eenvoudigste architectuur om HDInsight te integreren met Active Directory. De AD-domeincontroller wordt uitgevoerd op een (of meerdere) virtuele machines (VM's) in Azure. Deze VM's bevinden zich meestal in een virtueel netwerk. U stelt een ander virtueel netwerk in voor het HDInsight-cluster. Voor HDInsight om een regel zicht naar Active Directory, moet u deze virtuele netwerken met behulp van peer [VNet-naar-VNet-peering](../virtual-network/virtual-network-create-peering.md). Als u de Active Directory in ARM maakt, klikt u vervolgens kunt u de Active Directory en HDInsight maken in hetzelfde VNet en u hoeft niet te doen peering. 

![Topologie van aan domein gekoppeld HDInsight-cluster](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> In deze architectuur kunt u Azure Data Lake Store niet gebruiken met HDInsight-cluster.


Vereisten voor Active Directory:

* Er moet een [organisatie-eenheid](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) worden gemaakt waarin u de VM's van het HDInsight-cluster en de service-principals die door het cluster worden gebruikt, plaatst.
* [Lightweight Directory Access protocollen](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAPs) moeten worden ingesteld voor communicatie met AD. Het certificaat dat voor het instellen van LDAPS wordt gebruikt, moet een echt certificaat zijn (niet een zelfondertekend certificaat).
* Er moeten omgekeerde DNS-zones in het domein worden gemaakt voor het IP-adresbereik van het HDInsight-subnet (bijvoorbeeld 10.2.0.0/24 in de vorige afbeelding).
* Een service-account of gebruikersaccount is vereist. Gebruik dit account om de HDInsight-cluster te maken. Dit account moet de volgende machtigingen hebben:

    - Machtigingen om service-principal- en machineobjecten in de organisatie-eenheid te maken
    - Machtigingen om regels voor omgekeerde DNS-proxy's te maken.
    - Machtigingen om machines lid te maken van het Active Directory-domein

**HDInsight geïntegreerd met een alleen-cloud Azure AD**

Configureer een domeincontroller voor alleen-cloud Azure AD, zodat HDInsight kan worden geïntegreerd met Azure AD. Dit wordt bereikt door middel [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS). Azure AD DS maakt domeincontrollermachines in de cloud en biedt de IP-adressen van deze machines. Voor maximale beschikbaarheid worden er twee domeincontrollers gemaakt.

Azure AD DS bestaat op dit moment alleen in klassieke virtuele netwerken. Het is alleen toegankelijk via de klassieke Azure-portal. Het virtuele netwerk van HDInsight bestaat in Azure Portal, die met behulp van VNet-naar-VNet-peering moet worden gepeerd met het klassieke virtuele netwerk.

> [!NOTE]
> Voor peering tussen een klassiek virtueel netwerk en een virtueel netwerk van Azure Resource Manager moeten beide virtuele netwerken zich in dezelfde regio bevinden en hetzelfde Azure-abonnement hebben.

![Topologie van aan domein gekoppeld HDInsight-cluster](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Vereisten voor Azure AD:

* Er moet een [organisatie-eenheid](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) worden gemaakt waarin u de VM's van het HDInsight-cluster en de service-principals die door het cluster worden gebruikt, plaatst.
* Tijdens de configuratie van Azure AD DS moet [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) worden ingesteld. Het certificaat dat voor het instellen van LDAPS wordt gebruikt, moet een echt certificaat zijn (niet een zelfondertekend certificaat).
* Er moeten omgekeerde DNS-zones in het domein worden gemaakt voor het IP-adresbereik van het HDInsight-subnet (bijvoorbeeld 10.2.0.0/24 in de vorige afbeelding).
* [Wachtwoord-hashes](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) moeten vanuit Azure AD worden gesynchroniseerd met Azure AD DS.
* Een service-account of gebruikersaccount is vereist. Gebruik dit account om de HDInsight-cluster te maken. Dit account moet de volgende machtigingen hebben:

    - Machtigingen om service-principal- en machineobjecten in de organisatie-eenheid te maken
    - Machtigingen om regels voor omgekeerde DNS-proxy's te maken.
    - Machtigingen om machines lid te maken van het Azure AD-domein

## <a name="next-steps"></a>Volgende stappen
* Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren) om een HDInsight-cluster te configureren dat is gekoppeld aan een domein.
* Zie [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Aan een domein gekoppelde HDInsight-clusters beheren) om HDInsight-clusters te beheren die zijn gekoppeld aan een domein.
* Zie [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Hive-beleid configureren voor aan een domein gekoppelde HDInsight-clusters) om Hive-beleid te configureren en Hive-query's uit te voeren.
* Zie voor informatie over het uitvoeren van Hive-query's met behulp van SSH op HDInsight-clusters domein [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
