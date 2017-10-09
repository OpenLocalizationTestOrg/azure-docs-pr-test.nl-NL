---
title: domein-HDInsight-clusters met behulp van PowerShell - Azure aaaConfigure | Microsoft Docs
description: Meer informatie over hoe tooset omhoog en domein HDInsight-clusters met Azure PowerShell configureren
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a13b2f7a-612d-4800-bc92-7fc0524f3e89
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 49da3439513d1e51171f0f7f7f9c3d967d55cb7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview-using-azure-powershell"></a>Domein-HDInsight-clusters (Preview) met Azure PowerShell configureren
Meer informatie over hoe tooset van een Azure HDInsight-cluster met Azure Active Directory (Azure AD) en [Apache Zwerver](http://hortonworks.com/apache/ranger/) met Azure PowerShell. Een Azure PowerShell-script wordt verstrekt toomake Hallo configuratie sneller en minder foutgevoelig. Domein HDInsight kan alleen worden geconfigureerd op Linux gebaseerde clusters. Zie voor meer informatie [introduceren domein HDInsight-clusters](hdinsight-domain-joined-introduction.md).

> [!IMPORTANT]
> Oozie is niet ingeschakeld op HDInsight domein.

Een typische configuratie van de domein-HDInsight-cluster omvat Hallo stappen te volgen:

1. Een Azure classic VNet maken voor uw Azure AD.  
2. Maak en configureer Azure AD en Azure AD DS.
3. Toevoegen van een VM-toohello klassiek VNet en voor het maken van de organisatie-eenheid. 
4. Maak een organisatie-eenheid voor Azure AD DS.
5. Een HDInsight-VNet aanmaken in hello Azure resource management-modus.
6. Het instellen van omgekeerde DNS-zones voor hello Azure AD DS.
7. Peer Hallo twee VNets.
8. Maak een HDInsight-cluster.

Hallo opgegeven PowerShell-script voert de stappen 3 tot 7. U moet handmatig stap 1 en 2 doorlopen.  Als u liever niet toouse Azure PowerShell, Zie [configureren domein HDInsight-clusters](hdinsight-domain-joined-configure.md). 

Een voorbeeld van de laatste topologie Hallo ziet er als volgt uit:

![Domein-HDInsight-topologie](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Omdat Azure AD op dit moment biedt alleen ondersteuning voor klassieke virtuele netwerken (vnet's) en Linux gebaseerde HDInsight-clusters alleen ondersteuning voor VNets op basis van Azure Resource Manager, HDInsight Azure AD-integratie vereist twee VNets en een peering ertussen. Zie voor Hallo vergelijking informatie tussen Hallo twee implementatiemodellen [Azure Resource Manager versus klassieke implementatie: implementatiemodellen begrijpen en de status van uw resources Hallo](../azure-resource-manager/resource-manager-deployment-model.md). Hallo Hallo twee VNets moet dezelfde regio bevinden als hello Azure AD DS.

> [!NOTE]
> Deze zelfstudie wordt ervan uitgegaan dat u geen een Azure AD hebt. Als u hebt, kunt u overslaan Hallo gedeelte in stap 2.
> 
> 

## <a name="prerequisites"></a>Vereisten
Hiervoor hebt u Hallo toogo items voor deze zelfstudie te volgen:

* Vertrouwd raken met [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) de [prijzen](https://azure.microsoft.com/pricing/details/active-directory-ds/) structuur.
* Zorg ervoor dat uw abonnement wilt plaatsen voor deze openbare preview. U kunt dit doen door een e-mail te sturen toohdipreview@microsoft.com met uw abonnement-ID.
* Een SSL-certificaat dat is ondertekend door een instantie voor het ondertekenen van voor uw domein. Hallo-certificaat is vereist voor het configureren van beveiligde LDAP. Zelfondertekende certificaten kunnen niet worden gebruikt.
* Azure PowerShell.  Zie [installeren en configureren van Azure PowerShell](/powershell/azure/overview).

## <a name="create-an-azure-classic-vnet-for-your-azure-ad"></a>Een Azure classic VNet maken voor uw Azure AD.
Zie voor instructies Hallo [hier](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic).

## <a name="create-and-configure-azure-ad-and-azure-ad-ds"></a>Maak en configureer Azure AD en Azure AD DS.
Zie voor instructies Hallo [hier](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).

## <a name="run-hello-powershell-script"></a>Hallo PowerShell-script uitvoeren
Hallo PowerShell-script kan worden gedownload vanaf [GitHub](https://github.com/hdinsight/DomainJoinedHDInsight). Haal de Hallo zip-bestand en Hallo bestanden lokaal opslaan.

**tooedit hello PowerShell-script**

1. Open run.ps1 met Windows PowerShell ISE of een teksteditor.
2. Vul Hallo waarden voor Hallo variabelen te volgen:
   
   * **$SubscriptionName** – hello naam van het hello Azure-abonnement waar u toocreate uw HDInsight-cluster. U al een klassiek virtueel netwerk hebt gemaakt in dit abonnement en maken van een virtueel netwerk van Azure Resource Manager voor HDInsight-cluster Hallo onder abonnement.
   * **$ClassicVNetName** -Hallo klassiek virtueel netwerk waarin hello Azure AD DS. Dit virtuele netwerk moet zich in Hallo hetzelfde abonnement dat hierboven is opgegeven. Dit virtuele netwerk moet worden gemaakt met hello Azure-portal en niet met klassieke portal. Als u de aanwijzingen in Hallo volgt [configureren domein HDInsight-clusters (Preview)](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic), Hallo standaardnaam is contosoaadvnet.
   * **$ClassicResourceGroupName** – Hallo Resource Manager-groepsnaam voor Hallo klassiek virtueel netwerk dat hierboven wordt genoemd. Bijvoorbeeld contosoaadrg. 
   * **$ArmResourceGroupName** – hello Resourcegroepnaam binnen die u wilt dat toocreate hello HDInsight-cluster. U kunt Hallo dezelfde resourcegroep als $ArmResourceGroupName.  Als de resourcegroep Hallo niet bestaat, maakt Hallo script Hallo resourcegroep.
   * **$ArmVNetName** -Hallo Resource Manager virtuele-netwerknaam in waarin u wilt dat toocreate hello HDInsight-cluster. Dit virtuele netwerk worden opgenomen in $ArmResourceGroupName.  Als Hallo VNet niet bestaat, wordt deze door Hallo PowerShell-script maken. Als deze bestaat, moeten deze deel uitmaken van Hallo resourcegroep die u hierboven hebt opgeven.
   * **$AddressVnetAddressSpace** – hello netwerkadresruimte voor Hallo Resource Manager virtuele netwerk. Zorg ervoor dat deze adresruimte beschikbaar is. Deze adresruimte kan adresruimte Hallo klassieke van het virtuele netwerk niet overlappen. Bijvoorbeeld '10.1.0.0/16'
   * **$ArmVnetSubnetName** -Hallo Resource Manager virtuele subnet-netwerknaam in waarin u wilt dat tooplace hello HDInsight-cluster virtuele machines. Als Hallo subnet niet bestaat, wordt deze door Hallo PowerShell-script maken. Als deze bestaat, moeten deze deel uitmaken van Hallo virtueel netwerk dat u hierboven opgeeft.
   * **$AddressSubnetAddressSpace** – Hallo-adresbereik voor virtueel netwerksubnet van Hallo Resource Manager-netwerk. Hallo HDInsight-cluster VM IP-adressen uit het adresbereik van dit subnet worden zullen. Bijvoorbeeld '10.1.0.0/24'.
   * **$ActiveDirectoryDomainName** – hello Azure AD-domeinnaam die u wilt dat toojoin hello HDInsight-cluster VM's. Bijvoorbeeld 'contoso.onmicrosoft.com'
   * **$ClusterUsersGroups** – Hallo algemene naam van de beveiligingsgroepen Hallo van uw AD dat u wilt dat toosync toohello HDInsight-cluster. Hallo-gebruikers in deze beveiligingsgroep worden kunnen toolog op toohello cluster-dashboard met behulp van de referenties voor het active directory-domein. Deze beveiligingsgroepen moeten in active directory Hallo bestaan. Bijvoorbeeld 'hiveusers' of 'clusteroperatorusers'.
   * **$OrganizationalUnitName** -organisatie-eenheid in Hallo domein, waarin u tooplace hello HDInsight-cluster virtuele machines wilt toevoegen en service-principals die zijn gebruikt door de cluster Hallo HALLO hallo. Hallo PowerShell-script zal deze organisatie-eenheid maken als deze niet bestaat. Bijvoorbeeld 'HDInsightOU'.
3. Hallo wijzigingen opslaan.

**toorun hello script**

1. Voer **Windows PowerShell** als administrator.
2. De map toohello van run.ps1 bladeren. 
3. Hallo-script uitvoeren door het Hallo-bestand de naam te typen en druk op **ENTER**.  Het verschijnt 3-in-dialoogvensters:
   
   1. **Meld u aan in de klassieke portal tooAzure** – Voer uw referenties waarmee u toosign in de klassieke portal tooAzure. U moet hello Azure AD en Azure AD DS met behulp van deze referenties hebt gemaakt.
   2. **Meld u aan de Resource Manager-portal tooAzure** – Voer uw referenties waarmee u toosign in tooAzure Resource Manager-portal.
   3. **Domeingebruikersnaam** – Geef referenties op Hallo van Hallo domeingebruikersnaam dat u wilt dat toobe een beheerder op Hallo HDInsight-cluster. Als u een Azure AD hebt gemaakt vanaf het begin, moet hebt u deze gebruiker met behulp van deze documentatie gemaakt. 
      
      > [!IMPORTANT]
      > Hallo gebruikersnaam invoeren in deze indeling: 
      > 
      > Domeinnaam\gebruikersnaam (bijvoorbeeld contoso.onmicrosoft.com\clusteradmin)
      > 
      > 
      
      Deze gebruiker moet 3 bevoegdheden hebben: toojoin machines toohello opgegeven Active Directory-domein. service-principals toocreate en machineobjecten binnen Hallo opgegeven organisatie-eenheid; en tooadd omgekeerde DNS-proxy regels.

Tijdens het maken omgekeerde DNS-zones, Hallo script wordt u gevraagd tooenter een netwerk-id. Dit netwerk-ID moet adresvoorvoegsel Hallo Resource Manager van het virtuele netwerk. Bijvoorbeeld, als uw virtuele netwerk voor Resource Manager subnetadresruimte 10.2.0.0/24, voert 10.2.0.0/24 als Hallo hulpprogramma wordt u gevraagd om Hallo netwerk-ID. 

## <a name="create-hdinsight-cluster"></a>HDInsight-cluster maken
In deze sectie maakt u een Linux gebaseerde Hadoop-cluster in HDInsight met behulp van beide hello Azure-portal of [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md). Voor andere methoden voor het maken van cluster en inzicht Hallo-instellingen, Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md). Zie voor meer informatie over het gebruik van Resource Manager-sjabloon toocreate Hadoop-clusters in HDInsight, [maken Hadoop-clusters in HDInsight met behulp van Resource Manager-sjablonen](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

**een domein HDInsight-cluster met toocreate hello Azure-portal**

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).
2. Klik op **nieuw**, **Intelligence en analyse**, en vervolgens **HDInsight**.
3. Van Hallo **nieuwe HDInsight-cluster** blade invoeren of selecteren Hallo volgende waarden:
   
   * **Clusternaam**: Voer een nieuwe clusternaam voor Hallo domein HDInsight-cluster.
   * **Abonnement**: Selecteer een Azure-abonnement gebruikt voor het maken van dit cluster.
   * **Configuratie van het cluster**:
     
     * **Type cluster**: Hadoop. Domein HDInsight is momenteel alleen ondersteund op Hadoop-clusters.
     * **Besturingssysteem**: Linux.  HDInsight domein wordt alleen ondersteund op Linux gebaseerde HDInsight-clusters.
     * **Versie**: Hadoop punt 2.7.3 (HDI 3.5). HDInsight domein wordt alleen ondersteund op HDInsight-cluster versie 3.5.
     * **Type cluster**: PREMIUM
       
       Klik op **Selecteer** toosave Hallo wijzigingen.
   * **Referenties**: Configureer Hallo referenties voor zowel Hallo cluster gebruiker als Hallo SSH-gebruiker.
   * **Gegevensbron**: een nieuw opslagaccount maken of een bestaand opslagaccount gebruiken zoals Hallo Storage-standaardaccount voor Hallo HDInsight-cluster. Hallo-locatie moet hetzelfde zijn als de twee VNets Hallo Hallo.  Hallo-locatie is ook Hallo-locatie van Hallo HDInsight-cluster.
   * **Prijzen**: Selecteer Hallo aantal worker-knooppunten van het cluster.
   * **Geavanceerde configuraties**: 
     
     * **Lid worden van domein & Vnet/Subnet**: 
       
       * **Domeininstellingen**: 
         
         * **Domeinnaam**: contoso.onmicrosoft.com
         * **Domeingebruikersnaam**: Voer de gebruikersnaam van een domein. Dit domein moet beschikken over Hallo volgende bevoegdheden: lid worden van domein van machines toohello op en plaats deze in de organisatie-eenheid Hallo u eerder; hebt geconfigureerd Service-principals binnen Hallo u eerder; hebt geconfigureerd organisatie-eenheid maken Omgekeerde DNS-vermeldingen te maken. Deze domeingebruiker worden Hallo beheerder van dit domein HDInsight-cluster.
         * **Domeinwachtwoord**: Hallo domeingebruikerswachtwoord invoeren.
         * **Organisatie-eenheid**: Geef Hallo DN-naam van Hallo organisatie-eenheid die u eerder hebt geconfigureerd. Bijvoorbeeld: OU = HDInsightOU, DC = contoso, DC = onmicrosoft gebruikt, DC = com
         * **LDAPS URL**: ldaps://contoso.onmicrosoft.com:636
         * **Gebruikersgroep toegang**: Geef Hallo beveiligingsgroep waarvan u gebruikers toosync toohello cluster. Bijvoorbeeld: HiveUsers.
           
           Klik op **Selecteer** toosave Hallo wijzigingen.
           
           ![HDInsight-portal domein configureren domeininstelling](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **Virtueel netwerk**: contosohdivnet
       * **Subnet**: Subnet1
         
         Klik op **Selecteer** toosave Hallo wijzigingen.        
         Klik op **Selecteer** toosave Hallo wijzigingen.
   * **Resourcegroep**: Selecteer Hallo resourcegroep gebruikt voor Hallo HDInsight VNet (contosohdirg).
4. Klik op **Create**.  

Een andere optie voor het maken van domein HDInsight-cluster is toouse Azure Resource Management-sjabloon. Hallo na procedure ziet u hoe:

**toocreate een domein HDInsight-cluster met een Resource Management-sjabloon**

1. Klik op Hallo installatiekopie tooopen Resource Manager-sjabloon in hello Azure-portal te volgen. Hallo Resource Manager-sjabloon bevindt zich in een openbare blob-container. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure-use-powershell/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Van Hallo **Parameters** blade Voer Hallo volgende waarden:
   
   * **Abonnement**: (Selecteer uw Azure-abonnement).
   * **Resourcegroep**: klik op **gebruik bestaande**, en geef Hallo dezelfde resourcegroep die u hebt gebruikt.  Bijvoorbeeld contosohdirg. 
   * **Locatie**: Geef de locatie van een resourcegroep.
   * **Clusternaam**: Voer een naam voor Hallo Hadoop-cluster dat u maakt. Bijvoorbeeld contosohdicluster.
   * **Type cluster**: een cluster selecteren.  de standaardwaarde Hallo is **hadoop**.
   * **Locatie**: Selecteer een locatie voor het Hallo-cluster.  Hallo standaardopslagaccount gebruikt Hallo dezelfde locatie.
   * **Aantal Worker-knooppunten cluster**: Selecteer Hallo aantal worker-knooppunten.
   * **Cluster-aanmeldingsnaam en wachtwoord**: Hallo standaardaanmeldnaam is **admin**.
   * **SSH-gebruikersnaam en wachtwoord**: de standaardgebruikersnaam Hallo **sshuser**.  U kunt de naam wijzigen. 
   * **Virtueel netwerk-Id**: /subscriptions/&lt;abonnements-id > /resourceGroups/&lt;ResourceGroupName > /providers/Microsoft.Network/virtualNetworks/&lt;VNetName >
   * **Virtueel netwerksubnet**: /subscriptions/&lt;abonnements-id > /resourceGroups/&lt;ResourceGroupName > /providers/Microsoft.Network/virtualNetworks/&lt;VNetName >/subnetten/Subnet1
   * **Domeinnaam**: contoso.onmicrosoft.com
   * **DN-naam van organisatie-eenheid**: OU = HDInsightOU, DC = contoso, DC = onmicrosoft gebruikt, DC = com
   * **Gebruikers clustergroep D Ns**: '\"CN HiveUsers, OU = AADDC Users, DC = =<DomainName>, DC = onmicrosoft gebruikt, DC = com\"'
   * **LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (Enter Hallo beheerder domeingebruikersnaam)
   * **DomainAdminPassword**: (Geef Hallo beheerder domeingebruikerswachtwoord)
   * **Ik ga akkoord toohello voorwaarden bovengenoemde**: (controleren)
   * **Pincode toodashboard**: (controleren)
3. Klik op **Kopen**. U ziet een nieuwe tegel met de titel **Implementatie van sjabloonimplementatie**. Het duurt ongeveer 20 minuten toocreate een cluster. Zodra het Hallo-cluster is gemaakt, klikt u op Hallo cluster-blade in de portal tooopen Hallo deze.

Nadat u Hallo-zelfstudie hebt voltooid, kunt u toodelete Hallo-cluster. Met HDInsight worden uw gegevens opgeslagen in Azure Storage zodat u een cluster veilig kunt verwijderen wanneer deze niet wordt gebruikt. Voor een HDInsight-cluster worden ook kosten in rekening gebracht, zelfs wanneer het niet wordt gebruikt. Aangezien Hallo kosten voor Hallo cluster vaak zoveel hoger zijn dan Hallo kosten voor opslag, is het financieel aantrekkelijk toodelete clusters wanneer ze zich niet in gebruik. Zie voor instructies van het verwijderen van een cluster Hallo [beheren Hadoop-clusters in HDInsight met behulp van Azure-portal Hallo](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Volgende stappen

* Zie [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Hive-beleid configureren voor aan een domein gekoppelde HDInsight-clusters) om Hive-beleid te configureren en Hive-query's uit te voeren.
* Zie voor het gebruik van SSH tooconnect die lid zijn van tooDomain HDInsight-clusters [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

