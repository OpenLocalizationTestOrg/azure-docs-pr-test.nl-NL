---
title: aaaConfigure domein HDInsight-clusters - Azure | Microsoft Docs
description: Meer informatie over hoe tooset omhoog en domein HDInsight-clusters configureren
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 0cbb49cc-0de1-4a1a-b658-99897caf827c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 8c4b3d269a7662d27a49b839e5cd05a3e24f7023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a>Domein-HDInsight-clusters (Preview) configureren

Meer informatie over hoe tooset van een Azure HDInsight-cluster met Azure Active Directory (Azure AD) en [Apache Zwerver](http://hortonworks.com/apache/ranger/) tootake profiteren van sterke authenticatie- en uitgebreide op rollen gebaseerde toegangsbeheer (RBAC) toegangsbeleid.  Domein HDInsight kan alleen worden geconfigureerd op Linux gebaseerde clusters. Zie voor meer informatie [introduceren domein HDInsight-clusters](hdinsight-domain-joined-introduction.md).

> [!IMPORTANT]
> Oozie is niet ingeschakeld op HDInsight domein.

Dit artikel is de eerste zelfstudie Hallo van een serie:

* Maak een HDInsight-cluster aangesloten tooAzure AD (via de mogelijkheid van hello Azure Directory Domain Services) met Apache Zwerver ingeschakeld.
* Maken en Hive-beleid via Apache Zwerver toepassen en toestaan dat gebruikers (bijvoorbeeld gegevenswetenschappers) tooconnect tooHive met behulp van ODBC-hulpprogramma's, zoals Excel, Tableau enzovoort. Microsoft werkt over het toevoegen van andere werkbelastingen verwerken, zoals HBase, Spark, en Storm, die lid zijn van tooDomain HDInsight snel.

Een voorbeeld van de laatste topologie Hallo ziet er als volgt uit:

![Domein-HDInsight-topologie](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Omdat Azure AD op dit moment biedt alleen ondersteuning voor klassieke virtuele netwerken (vnet's) en Linux gebaseerde HDInsight-clusters alleen ondersteuning voor VNets op basis van Azure Resource Manager, HDInsight Azure AD-integratie vereist twee VNets en een peering ertussen. Zie voor Hallo vergelijking informatie tussen Hallo twee implementatiemodellen [Azure Resource Manager versus klassieke implementatie: implementatiemodellen begrijpen en de status van uw resources Hallo](../azure-resource-manager/resource-manager-deployment-model.md). Hallo Hallo twee VNets moet dezelfde regio bevinden als hello Azure AD DS.

Azure-service-namen moeten uniek zijn. Hallo volgende namen worden gebruikt in deze zelfstudie. Contoso is een fictieve naam. U moet vervangen *contoso* met een andere naam wanneer u Hallo zelfstudie gaat. 

**Namen:**

| Eigenschap | Waarde |
| --- | --- |
| Azure AD-VNet |contosoaadvnet |
| Azure AD-Vnet-resourcegroep |contosoaadrg |
| Azure AD-map |contosoaaddirectory |
| Azure AD-domeinnaam |Contoso (contoso.onmicrosoft.com) |
| HDInsight-VNet |contosohdivnet |
| HDInsight VNet resourcegroep |contosohdirg |
| HDInsight-cluster |contosohdicluster |

Deze zelfstudie bevat Hallo stappen voor het configureren van een domein HDInsight-cluster. Elke sectie heeft koppelingen tooother artikelen met achtergrondinformatie over.

## <a name="prerequisite"></a>Voorwaarde:
* Vertrouwd raken met [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) de [prijzen](https://azure.microsoft.com/pricing/details/active-directory-ds/) structuur.
* Zorg ervoor dat uw abonnement wilt plaatsen voor deze openbare preview. U kunt dit doen door een e-mail te sturen toohdipreview@microsoft.com met uw abonnement-ID.
* Een SSL-certificaat dat is ondertekend door een instantie voor het ondertekenen van voor uw domein. Hallo-certificaat is vereist voor het configureren van beveiligde LDAP. Zelfondertekende certificaten kunnen niet worden gebruikt.

## <a name="procedures"></a>Procedures
1. Een Azure classic VNet maken voor uw Azure AD.  
2. Maak en configureer Azure AD en Azure AD DS.
3. Een HDInsight-VNet aanmaken in hello Azure resource management-modus.
4. Peer Hallo twee VNets.
5. Maak een HDInsight-cluster.

> [!NOTE]
> Deze zelfstudie wordt ervan uitgegaan dat u geen een Azure AD hebt. Als u hebt, kunt u overslaan Hallo gedeelte in stap 2.
> 
> 

Er is een PowerShell-script waarmee stap 3 tot en met 7 worden geautomatiseerd.  Zie voor meer informatie [configureren domein HDInsight-clusters Azure PowerShell gebruiken](hdinsight-domain-joined-configure-use-powershell.md).

## <a name="create-an-azure-virtual-network-classic"></a>Een Azure-netwerk (klassiek) maken
In deze sectie maakt u een virtueel netwerk (klassiek) met hello Azure-portal. In de volgende sectie hello schakelt u hello Azure AD DS voor uw Azure AD in Hallo virtueel netwerk. Zie voor meer informatie over Hallo procedure te volgen en het gebruik van andere methoden voor het virtueel netwerk maken, [een virtueel netwerk (klassiek) maken met behulp van Azure-portal Hallo](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

**toocreate een klassiek VNet**

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com). 
2. Klik op **nieuwe** > **Networking** > **virtueel netwerk**.
3. In **een implementatiemodel selecteren**, selecteer **klassieke**, en klik vervolgens op **maken**.
4. Typ of selecteer Hallo volgende waarden:
   
   * **Naam**: contosoaadvnet
   * **Adresruimte**: 10.1.0.0/16
   * **De subnetnaam van het**: Subnet1
   * **Adresbereik van**: 10.1.0.0/24
   * **Abonnement**: (Selecteer een abonnement dat u gebruikt voor het maken van dit VNet.)
   * **ResourceGroup**: contosoaadrg
   * **Locatie**: (Selecteer een regio voor uw HDInsight-cluster.)
     
     > [!IMPORTANT]
     > U moet een locatie die ondersteuning biedt voor Azure AD DS. Zie [Producten beschikbaar per regio](https://azure.microsoft.com/en-us/regions/services/) voor meer informatie. 
     > 
     > Beide Hallo klassiek VNet en hello Resource groep VNet moet Hallo dezelfde regio bevinden als hello Azure AD DS.
     > 
     > 
5. Klik op **maken** toocreate hello VNet.

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a>Maken en configureren van Azure AD DS voor uw Azure AD
U wordt in deze sectie:

1. Maak een Azure AD.
2. Gebruikers van Azure AD maken. Deze gebruikers zijn Domeingebruikers. U de eerste gebruiker Hallo gebruiken voor het configureren van de HDInsight-cluster Hallo Hello Azure AD.  Hallo zijn andere twee gebruikers optioneel voor deze zelfstudie. Ze worden gebruikt [configureren Hive-beleid voor domein-HDInsight-clusters](hdinsight-domain-joined-run-hive.md) wanneer u Apache Zwerver beleid configureert.
3. Hallo AAD DC-beheerdersgroep maken en toevoegen van groep toohello hello Azure AD-gebruiker. U deze gebruiker toocreate Hallo organisatie-eenheid.
4. Azure AD Domain Services (Azure AD DS) voor hello Azure AD in te schakelen.
5. LDAPS voor hello Azure AD configureren. Hallo Lightweight Directory Access Protocol (LDAP) is gebruikte tooread van en schrijven tooAzure AD.

Als u liever toouse een bestaande Azure AD, kunt u stap 1 en 2 overslaan.

**toocreate een Azure AD**

1. Van Hallo [klassieke Azure-portal](https://manage.windowsazure.com), klikt u op **nieuw** > **App Services** > **Active Directory**  >  **Directory** > **aangepast maken**. 
2. Typ of selecteer Hallo volgende waarden:
   
   * **Naam**: contosoaaddirectory
   * **Domeinnaam**: contoso.  Deze naam moet uniek zijn.
   * **Land of regio**: Selecteer uw land of regio.
3. Klik op **Voltooien**.

**Een Azure AD-gebruiker maken**

1. Van Hallo [klassieke Azure-portal](https://manage.windowsazure.com), klikt u op **Active Directory** -> **contosoaaddirectory**. 
2. Klik op **gebruikers** in het bovenste menu Hallo.
3. Klik op **gebruiker toevoegen**.
4. Voer **gebruikersnaam**, en klik vervolgens op **volgende**. 
5. Gebruikersprofiel; configureren In **rol**, selecteer **globale beheerder**; en klik vervolgens op **volgende**.  de globale beheerdersrol Hallo is benodigde toocreate organisatie-eenheden.
6. Klik op **maken** tooget een tijdelijk wachtwoord.
7. Maak een kopie van het Hallo-wachtwoord en klik vervolgens op **Complete**. Verderop in deze zelfstudie gebruikt u deze globale beheerder gebruiker toocreate hello HDInsight-cluster.

Volg Hallo dezelfde procedure toocreate twee meer gebruikers Hello **gebruiker** rol, hiveuser1 en hiveuser2. Hallo volgende gebruikers worden gebruikt voor [configureren Hive-beleid voor domein-HDInsight-clusters](hdinsight-domain-joined-run-hive.md).

**toocreate groep AAD DC Administrators Hallo en een Azure AD-gebruiker toevoegen**

1. Van Hallo [klassieke Azure-portal](https://manage.windowsazure.com), klikt u op **Active Directory** > **contosoaaddirectory**. 
2. Klik op **groepen** in het bovenste menu Hallo.
3. Klik op **een groep toevoegen** of **groep toevoegen**.
4. Typ of selecteer Hallo volgende waarden:
   
   * **Naam**: AAD DC-beheerders.  Hallo groepsnaam worden niet gewijzigd.
   * **Groepstype**: beveiliging.
5. Klik op **Voltooien**.
6. Klik op **AAD DC beheerders** tooopen Hallo groep.
7. Klik op **leden toevoegen**.
8. Hallo eerste gebruiker die u hebt gemaakt in de vorige stap Hallo selecteren en klik vervolgens op **Complete**.
9. Herhaal Hallo dezelfde stappen toocreate een andere groep aangeroepen **HiveUsers**, en Hallo twee Hive toohello gebruikersgroep toevoegen.

Zie voor meer informatie [Azure AD Domain Services (Preview): Maak Hallo 'AAD DC-beheerders' groep](../active-directory-domain-services/active-directory-ds-getting-started.md).

**Azure AD DS tooenable voor uw Azure AD**

1. Van Hallo [klassieke Azure-portal](https://manage.windowsazure.com), klikt u op **Active Directory** > **contosoaaddirectory**. 
2. Klik op **configureren** in het bovenste menu Hallo.
3. Schuif naar beneden te**domeinservices**, en set Hallo de volgende waarden:
   
   * **Domeinservices inschakelen voor deze map**: Ja.
   * **DNS-domeinnaam van domeinservices**: dit Hallo standaard DNS-naam van hello Azure-map bevat. Bijvoorbeeld: contoso.onmicrosoft.com.
   * **Domain services toothis virtueel netwerk verbinden**: Selecteer Hallo klassiek virtueel netwerk dat u eerder hebt gemaakt, dat wil zeggen **contosoaadvnet**.
4. Klik op **opslaan** van Hallo onder Hallo. U ziet **in behandeling...**  volgende te**domeinservices inschakelen voor deze map**.  
5. Wachten tot **in behandeling...**  verdwijnt, en **IP-adres** opgehaald ingevuld. Twee IP-adressen wordt ophalen ingevuld. Dit zijn Hallo IP-adressen van domeincontrollers Hallo ingericht met Domain Services. Elk IP-adres is zichtbaar nadat de overeenkomstige domeincontroller Hallo ingericht en gereed is. Schrijf Hallo twee IP-adressen. U moet ze later.

Zie voor meer informatie [Azure AD Domain Services (Preview) - inschakelen Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md).

**toosynchronize wachtwoord**

Als u uw eigen domein gebruikt, moet u toosynchronize Hallo wachtwoord. Zie [wachtwoord synchronisatie tooAzure AD domain services inschakelt voor een alleen-Azure AD-directory](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md).

**tooconfigure LDAPS voor hello Azure AD**

1. Ophalen van een SSL-certificaat dat is ondertekend door een instantie voor het ondertekenen van voor uw domein. Als u een zelfondertekend certificaat toouse wilt, kunt contact toohdipreview@microsoft.com voor een uitzondering.
2. Van Hallo [klassieke Azure-portal](https://manage.windowsazure.com), klikt u op **Active Directory** > **contosoaaddirectory**. 
3. Klik op **configureren** in het bovenste menu Hallo.
4. Schuif te**domeinservices**.
5. Klik op **configureren certificaat**.
6. Ga als volgt Hallo instructie toospecify Hallo-certificaatbestand en het Hallo wachtwoord. U ziet **in behandeling...**  volgende te**domeinservices inschakelen voor deze map**.  
7. Wachten tot **in behandeling...**  verdwijnt, en **Secure LDAP certificaat** is ingevuld.  Dit kan 10 minuten of langer duren.

> [!NOTE]
> Als een aantal achtergrondtaken zijn op Hallo Azure AD DS wordt uitgevoerd, wordt er een fout opgetreden tijdens het uploaden certificaat - <i>er is een bewerking wordt uitgevoerd voor deze tenant. Probeer het later opnieuw</i>.  Als deze fout zich voordoet, probeer het na enige tijd opnieuw. Hallo tweede domain controller IP kan duren too3 uren toobe ingericht.
> 
> 

Zie voor meer informatie [configureren beveiligde LDAP (LDAPS) gebruiken voor een Azure AD Domain Services beheerd domein](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md).

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a>Een Resource Manager VNet voor HDInsight-cluster maken
In deze sectie maakt u een Azure Resource Manager VNet dat wordt gebruikt voor Hallo HDInsight-cluster. Zie voor meer informatie over het maken van Azure VNET van andere methoden [een virtueel netwerk maken](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)

Na het maken van Hallo VNet, configureert u Hallo Resource Manager VNet toouse Hallo dezelfde DNS-servers als voor hello Azure AD-VNet. Als u de stappen in deze zelfstudie toocreate Hallo gevolgd Hallo-classic VNet en hello Azure AD Hallo DNS-servers zijn 10.1.0.4 en 10.1.0.5.

**een Resource Manager VNet toocreate**

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).
2. Klik op **nieuw**, **Networking**, en vervolgens **virtueel netwerk**. 
3. In **een implementatiemodel selecteren**, selecteer **Resource Manager**, en klik vervolgens op **maken**.
4. Typ of selecteer Hallo volgende waarden:
   
   * **Naam**: contosohdivnet
   * **Adresruimte**: 10.2.0.0/16. Zorg ervoor dat het Hallo-adresbereik niet overlappen met Hallo IP-adresbereik Hallo klassieke VNet.
   * **De subnetnaam van het**: Subnet1
   * **Adresbereik van**: 10.2.0.0/24
   * **Abonnement**: (uw Azure-abonnement selecteren.)
   * **Resourcegroep**: contosohdirg
   * **Locatie**: (Selecteer Hallo dezelfde locatie als Azure AD VNet, dat wil zeggen contosoaadvnet Hallo.)
5. Klik op **Create**.

**tooconfigure DNS voor Hallo Resource Manager VNet**

1. Van Hallo [Azure-portal](https://portal.azure.com), klikt u op **meer services** -> **virtuele netwerken**. Zorg ervoor dat geen tooclick **virtuele netwerken (klassiek)**.
2. Klik op **contosohdivnet**.
3. Klik op **DNS-servers** vanaf de linkerkant van de nieuwe blade Hallo Hallo.
4. Klik op **aangepaste**, en voer vervolgens Hallo volgende waarden:
   
   * 10.1.0.4
   * 10.1.0.5
     
     Deze DNS-server IP-adressen moeten overeenkomen met toohello DNS-servers in hello Azure AD-VNet (klassieke VNet).
5. Klik op **Opslaan**.

## <a name="peer-hello-azure-ad-vnet-and-hello-hdinsight-vnet"></a>Peer hello Azure AD VNet en Hallo HDInsight VNet
**toopeer Hallo twee VNet**

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).
2. Klik op **meer services** in het linkermenu Hallo.
3. Klik op **virtuele netwerken**. Klik niet op **virtuele netwerken (klassiek)**.
4. Klik op **contosohdivnet**.  Dit is Hallo HDInsight VNet.
5. Klik op **Peerings** op Hallo linkermenu van Hallo-blade.
6. Klik op **toevoegen** in het bovenste menu Hallo. Het openen van Hallo **toevoegen peering** blade.
7. Op Hallo **toevoegen peering** blade, instellen of selecteer Hallo volgende waarden:
   
   * **Naam**: ContosoAADHDIVNetPeering
   * **Virtueel netwerk implementatiemodel**: klassieke
   * **Abonnement**: Selecteer de abonnementsnaam van uw voor vnet van Hallo-classic (Azure AD) gebruikt.
   * **Virtueel netwerk**: contosoaadvnet.
   * **Toestaan van toegang tot het virtuele netwerk**: (controleren)
   * **Toestaan van doorgestuurd verkeer**: (Raadpleeg). Laat Hallo andere twee selectievakjes uitgeschakeld.
8. Klik op **OK**.

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
     * **Versie**: HDI 3.6. HDInsight domein wordt alleen ondersteund op HDInsight-cluster versie 3.6.
     * **Type cluster**: PREMIUM
       
       Klik op **Selecteer** toosave Hallo wijzigingen.
   * **Referenties**: Configureer Hallo referenties voor zowel Hallo cluster gebruiker als Hallo SSH-gebruiker.
   * **Gegevensbron**: een nieuw opslagaccount maken of een bestaand opslagaccount gebruiken zoals Hallo Storage-standaardaccount voor Hallo HDInsight-cluster. Hallo-locatie moet hetzelfde zijn als de twee VNets Hallo Hallo.  Hallo-locatie is ook Hallo-locatie van Hallo HDInsight-cluster.
   * **Prijzen**: Selecteer Hallo aantal worker-knooppunten van het cluster.
   * **Geavanceerde configuraties**: 
     
     * **Lid worden van domein & Vnet/Subnet**: 
       
       * **Domeininstellingen**: 
         
         * **Domeinnaam**: contoso.onmicrosoft.com
         * **Domeingebruikersnaam**: Voer de gebruikersnaam van een domein. Dit domein moet beschikken over Hallo volgende bevoegdheden: lid worden van domein van machines toohello op en plaats deze in de organisatie-eenheid Hallo u tijdens het maken van het cluster opgeeft; Maken van de service-principals binnen de organisatie-eenheid Hallo die u tijdens het maken van het cluster opgeeft; Omgekeerde DNS-vermeldingen te maken. Deze domeingebruiker worden Hallo beheerder van dit domein HDInsight-cluster.
         * **Domeinwachtwoord**: Hallo domeingebruikerswachtwoord invoeren.
         * **Organisatie-eenheid**: Hallo DN-naam van organisatie-eenheid die u toouse met HDInsight-cluster wilt Hallo invoeren. Bijvoorbeeld: OU = HDInsightOU, DC = contoso, DC = onmicrosoft gebruikt, DC = com. Als deze organisatie-eenheid niet bestaat, probeert HDInsight-cluster toocreate deze organisatie-eenheid. Controleer of Hallo organisatie-eenheid is al aanwezig of het domeinaccount Hallo machtigingen toocreate heeft een nieuwe. Als u Hallo-domeinaccount dat deel uitmaakt van de beheerders AADDC gebruikt, heeft dit vereiste machtigingen toocreate Hallo organisatie-eenheid.
         * **LDAPS URL**: ldaps://contoso.onmicrosoft.com:636
         * **Gebruikersgroep toegang**: Hallo-beveiligingsgroep die gebruikers opgeven u toosync toohello cluster wilt toevoegen. Bijvoorbeeld: HiveUsers.
           
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
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy tooAzure"></a>
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
   * **Gebruikers clustergroep DNs**: [\"HiveUsers\"]
   * **LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (Enter Hallo beheerder domeingebruikersnaam)
   * **DomainAdminPassword**: (Geef Hallo beheerder domeingebruikerswachtwoord)
   * **Ik ga akkoord toohello voorwaarden bovengenoemde**: (controleren)
   * **Pincode toodashboard**: (controleren)
3. Klik op **Kopen**. U ziet een nieuwe tegel met de titel **Implementatie van sjabloonimplementatie**. Het duurt ongeveer 20 minuten toocreate een cluster. Zodra het Hallo-cluster is gemaakt, klikt u op Hallo cluster-blade in de portal tooopen Hallo deze.

Nadat u Hallo-zelfstudie hebt voltooid, kunt u toodelete Hallo-cluster. Met HDInsight worden uw gegevens opgeslagen in Azure Storage zodat u een cluster veilig kunt verwijderen wanneer deze niet wordt gebruikt. Voor een HDInsight-cluster worden ook kosten in rekening gebracht, zelfs wanneer het niet wordt gebruikt. Aangezien Hallo kosten voor Hallo cluster vaak zoveel hoger zijn dan Hallo kosten voor opslag, is het financieel aantrekkelijk toodelete clusters wanneer ze zich niet in gebruik. Zie voor instructies van het verwijderen van een cluster Hallo [beheren Hadoop-clusters in HDInsight met behulp van Azure-portal Hallo](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Volgende stappen
* Zie [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Hive-beleid configureren voor aan een domein gekoppelde HDInsight-clusters) om Hive-beleid te configureren en Hive-query's uit te voeren.
* Zie voor het gebruik van SSH tooconnect die lid zijn van tooDomain HDInsight-clusters [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Linux, Unix of OS X](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

