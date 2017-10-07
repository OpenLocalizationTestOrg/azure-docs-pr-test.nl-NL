---
title: aaaCreate Service Fabric-cluster in hello Azure-portal | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset een beveiligde Service Fabric-cluster in Azure worden verkregen met hello Azure portal en Azure Sleutelkluis.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>Een Service Fabric-cluster maken in Azure met behulp van hello Azure-portal
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Azure Portal](service-fabric-cluster-creation-via-portal.md)
> 
> 

Dit is een stapsgewijze handleiding die u bij het Hallo-stappen helpt voor het instellen van een beveiligde Service Fabric-cluster in Azure met behulp van hello Azure-portal. Deze handleiding wordt u begeleid bij Hallo stappen te volgen:

* Sleutelkluis toomanage sleutels voor clusterbeveiliging instellen.
* Een beveiligde cluster in Azure maken via hello Azure-portal.
* Beheerders met behulp van certificaten verifiëren.

> [!NOTE]
> Voor meer geavanceerde beveiligingsopties, zoals gebruikersverificatie met Azure Active Directory en het instellen van certificaten voor Toepassingsbeveiliging, [maken van het cluster met Azure Resource Manager][create-cluster-arm].
> 
> 

Een beveiligde cluster is een cluster waarmee wordt voorkomen dat onbevoegde toegang toomanagement bewerkingen, waaronder implementeren, bijwerken en verwijderen van toepassingen, services en Hallo gegevens die ze bevatten. Een niet-beveiligde cluster is een cluster iedereen kan verbinding maken met tooat elk gewenst moment en beheerbewerkingen uitvoeren. Hoewel het mogelijk toocreate een niet-beveiligde cluster, is **toocreate sterk aanbevolen een beveiligde cluster**. Een niet-beveiligde cluster **later niet kan worden beveiligd** -een nieuw cluster moet worden gemaakt.

Hallo concepten zijn hetzelfde voor het maken van beveiligde clusters of Hallo clusters Linux-clusters of clusters met Windows hello. Zie voor meer informatie en helper scripts voor het maken van beveiligde Linux-clusters, [maken van beveiligde clusters onder Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters). Hallo parameters die zijn verkregen door het Hallo helper-script dat kunnen worden ingevoerd rechtstreeks in de portal Hallo zoals beschreven in de sectie Hallo [een cluster maken in Azure-portal Hallo](#create-cluster-portal).

## <a name="log-in-tooazure"></a>Meld u bij tooAzure
Maakt gebruik van deze handleiding [Azure PowerShell][azure-powershell]. Bij het starten van een nieuwe PowerShell-sessie tooyour aanmelden met Azure-account en selecteer uw abonnement voordat u Azure opdrachten uitvoert.

Meld u bij tooyour azure-account:

```powershell
Login-AzureRmAccount
```

Selecteer uw abonnement:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>Key Vault instellen
Dit deel van Hallo handleiding helpt u bij het maken van een Sleutelkluis voor een Service Fabric-cluster in Azure en voor Service Fabric-toepassingen. Zie voor een volledige handleiding op Sleutelkluis hello [Sleutelkluis instructiehandleiding][key-vault-get-started].

Service Fabric maakt gebruik van x.509-certificaten toosecure een cluster. Azure Sleutelkluis is toomanage gebruikte certificaten voor Service Fabric-clusters in Azure. Wanneer een cluster wordt geïmplementeerd in Azure, hello Azure resourceprovider verantwoordelijk voor het maken van Service Fabric-clusters certificaten ophaalt uit Sleutelkluis en installeert ze op Hallo cluster virtuele machines.

Hallo illustreert volgende diagram Hallo relatie tussen de Sleutelkluis, een Service Fabric-cluster en hello Azure-resourceprovider die gebruikmaakt van certificaten die zijn opgeslagen in de Sleutelkluis bij het maken van een cluster:

![Installatie van het certificaat][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Een resourcegroep maken
de eerste stap Hallo is toocreate een nieuwe resourcegroep specifiek voor Sleutelkluis. Als Sleutelkluis in een eigen resourcegroep wordt aanbevolen zodat u kunt resourcegroepen berekenings- en - zoals de resourcegroep die uw Service Fabric-cluster heeft Hallo - verwijderen zonder verlies van uw sleutels en geheimen. Hallo-resourcegroep met uw Sleutelkluis moet Hallo dezelfde regio bevinden als het Hallo-cluster dat wordt gebruikt.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>Sleutelkluis maken
Een Sleutelkluis maken in de nieuwe resourcegroep Hallo. Hallo Sleutelkluis **moet zijn ingeschakeld voor de implementatie van** tooallow Service Fabric resource provider tooget certificaten van het Hallo en installeren op clusterknooppunten:

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

Als u een bestaande Sleutelkluis hebt, kunt u dit inschakelen voor implementatie met behulp van Azure CLI:

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>Certificaten tooKey kluis toevoegen
Certificaten worden gebruikt in Service Fabric tooprovide verificatie en versleuteling toosecure verschillende aspecten van een cluster en de toepassingen. Zie voor meer informatie over hoe de certificaten worden gebruikt in Service Fabric, [scenario's voor beveiliging van Service Fabric-cluster][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Cluster en de server-certificaat (vereist)
Dit certificaat is vereist toosecure een cluster en te voorkomen dat onbevoegde toegang tooit. Biedt clusterbeveiliging in een aantal manieren:

* **Cluster-verificatie:** knooppunt naar communicatie voor cluster federation verifieert. Alleen knooppunten die u hun identiteit met dit certificaat bewijzen kunnen kunnen Hallo-cluster toevoegen.
* **Server-verificatie:** verifieert Hallo cluster management eindpunten tooa management-client, zodat hello Beheerclient weet het echte cluster toohello communiceert. Dit certificaat biedt ook SSL voor Hallo HTTPS beheer-API en voor Service Fabric Explorer via HTTPS.

tooserve deze doeleinden Hallo certificaat moet voldoen aan Hallo volgens de vereisten:

* Hallo-certificaat moet een persoonlijke sleutel bevatten.
* Hallo-certificaat moet worden gemaakt voor sleuteluitwisseling, exporteerbaar tooa Personal Information Exchange (.pfx)-bestand.
* Hallo onderwerpnaam van het certificaat moet overeenkomen met Hallo domein gebruikt tooaccess Hallo Service Fabric-cluster. Dit is vereiste tooprovide SSL voor het HTTPS-eindpunten voor beheer en de Service Fabric Explorer Hallo-cluster. U kunt een SSL-certificaat kan niet verkrijgen van een certificeringsinstantie (CA) voor Hallo `.cloudapp.azure.com` domein. Verkrijgen van een aangepaste domeinnaam voor uw cluster. Wanneer u aanvragen hebben een certificaat van de onderwerpnaam van een CA Hallo-certificaat moet overeenkomen met aangepaste domeinnaam Hallo gebruikt voor uw cluster.

### <a name="client-authentication-certificates"></a>Certificaten voor clientverificatie
Aanvullende clientcertificaten verifiëren van beheerders voor beheertaken cluster. Service Fabric heeft twee toegangsniveaus: **admin** en **alleen-lezengebruiker**. Ten minste moet één certificaat voor beheerderstoegang worden gebruikt. Voor extra beveiliging op gebruikersniveau toegang, moet u een afzonderlijk certificaat opgegeven. Zie voor meer informatie over toegang tot rollen [toegangsbeheer op basis van rollen voor Service Fabric-clients][service-fabric-cluster-security-roles].

U hoeft niet tooupload Client verificatie certificaten tooKey kluis toowork met Service Fabric. Deze certificaten moeten alleen toobe opgegeven toousers die zijn gemachtigd voor Clusterbeheer. 

> [!NOTE]
> Azure Active Directory is Hallo aanbevolen manier tooauthenticate clients voor cluster beheerbewerkingen. toouse Azure Active Directory, moet u [maken van een cluster met Azure Resource Manager][create-cluster-arm].
> 
> 

### <a name="application-certificates-optional"></a>Toepassingscertificaten (optioneel)
Een willekeurig aantal extra certificaten kan worden geïnstalleerd op een cluster om beveiligingsredenen toepassing. Voordat u uw cluster maakt, overweeg Hallo scenario's voor Toepassingsbeveiliging waarvoor een certificaat toobe geïnstalleerd op Hallo knooppunten, zoals:

* Versleuteling en ontsleuteling van configuratiewaarden die van toepassing
* Versleuteling van gegevens over knooppunten tijdens de replicatie 

Toepassingscertificaten kunnen niet worden geconfigureerd wanneer u een cluster via hello Azure-portal. tooconfigure toepassingscertificaten tijdens de installatie cluster, moet u [maken van een cluster met Azure Resource Manager][create-cluster-arm]. U kunt ook een toepassing certificaten toohello cluster toevoegen nadat deze is gemaakt.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Certificaten voor Azure-resource provider opmaak
Bestanden met persoonlijke sleutel (.pfx) kunnen worden toegevoegd en gebruikt rechtstreeks via de Sleutelkluis. Hello Azure-resourceprovider vereist echter sleutels toobe opgeslagen in een speciale JSON-indeling die Hallo .pfx als een Base64-gecodeerde tekenreeks en Hallo wachtwoord voor persoonlijke sleutel bevat. tooaccommodate deze vereisten, sleutels moeten worden geplaatst in een JSON-tekenreeks en vervolgens wordt opgeslagen als *geheimen* in de Sleutelkluis.

toomake dit eenvoudiger verwerken, een PowerShell-module is [beschikbaar op GitHub][service-fabric-rp-helpers]. Volg deze stappen toouse Hallo-module:

1. Hallo volledige inhoud van de opslagplaats Hallo downloaden naar een lokale map. 
2. Hallo-module in uw PowerShell-venster importeren:

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

Hallo `Invoke-AddCertToKeyVault` opdracht in deze PowerShell-module automatisch de persoonlijke sleutel van een certificaat in een JSON-tekenreeks indelingen en tooKey kluis geüpload. Gebruik deze tooadd Hallo cluster certificaat en een extra toepassing certificaten tooKey kluis. Herhaal deze stap voor elke extra certificaten tooinstall in uw cluster.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

Dit zijn alle Hallo Sleutelkluis-vereisten voor het configureren van een Service Fabric-cluster Resource Manager-sjabloon die certificaten voor verificatie, eindpuntbeveiliging management en verificatie en eventuele aanvullende Toepassingsbeveiliging installeert functies die gebruikmaken van X.509-certificaten. U hebt op dit moment nu Hallo na de installatie in Azure:

* Sleutelkluis-resourcegroep
  * Key Vault
    * Certificaat voor serververificatie cluster

< /a "maken-cluster-portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>Cluster maken in hello Azure-portal
### <a name="search-for-hello-service-fabric-cluster-resource"></a>Zoeken naar Hallo Service Fabric-cluster-bron
![zoeken naar Service Fabric-cluster sjabloon op Hallo Azure-portal.][SearchforServiceFabricClusterTemplate]

1. Meld u aan toohello [Azure-portal][azure-portal].
2. Klik op **nieuw** tooadd een nieuwe resource-sjabloon. Zoeken naar Hallo Service Fabric-Cluster sjabloon in Hallo **Marketplace** onder **Alles**.
3. Selecteer **Service Fabric-Cluster** uit Hallo-lijst.
4. Navigeer toohello **Service Fabric-Cluster** blade, klikt u op **maken**,
5. Hallo **maken Service Fabric-cluster** blade bevat Hallo vier stappen te volgen.

#### <a name="1-basics"></a>1. Basisbeginselen
![Schermopname van het maken van een nieuwe resourcegroep.][CreateRG]

In de blade grondbeginselen Hallo moet u tooprovide Hallo basisdetails voor uw cluster.

1. Voer Hallo-naam van het cluster.
2. Voer een **gebruikersnaam** en **wachtwoord** voor extern bureaublad voor Hallo virtuele machines.
3. Zorg ervoor dat tooselect hello **abonnement** dat uw cluster toobe geïmplementeerd, met name als u meerdere abonnementen hebt.
4. Maak een **nieuwe resourcegroep**. Het is aanbevolen toogive het Hallo dezelfde naam als het Hallo-cluster, omdat het helpt bij het vinden ze later, vooral wanneer u toomake wijzigingen tooyour implementatie probeert of verwijder uw cluster.
   
   > [!NOTE]
   > U kunt ervoor kiezen een bestaande resourcegroep toouse, is maar het een toocreate raadzaam om een nieuwe resourcegroep. Dit maakt het eenvoudig toodelete-clusters die u niet nodig hebt.
   > 
   > 
5. Selecteer Hallo **regio** waarin u toocreate Hallo cluster wilt toevoegen. Hallo dezelfde regio die uw sleutel Vault heeft, moet u gebruiken.

#### <a name="2-cluster-configuration"></a>2. Configuratie van het cluster
![Een knooppunttype maken][CreateNodeType]

Configureer de clusterknooppunten. Knooppunttypen definiëren Hallo VM-grootten, Hallo aantal virtuele machines en hun eigenschappen. Uw cluster kan er meer dan één knooppunttype, maar het primaire knooppunttype hello (eerste is die u op Hallo portal definieert Hallo) moet ten minste vijf virtuele machines, omdat dit knooppunttype Hallo waar de Service Fabric-systeemservices worden geplaatst. Configureer geen **plaatsingseigenschappen** omdat een standaardeigenschap van de plaatsing van 'NodeTypeName' wordt automatisch toegevoegd.

> [!NOTE]
> Een veelvoorkomend scenario voor typen met meerdere knooppunten is een toepassing met een front-end-service en een back-endservice. Gewenste tooput Hallo front-end-service op kleinere virtuele machines (VM-grootten zoals D2) met poorten open toohello Internet, maar u tooput Hallo back-end-service op grotere virtuele machines (met VM-grootten zoals D4, D6 en D15) zonder internetverbinding poorten geopend.
> 
> 

1. Kies een naam voor uw knooppunttype (1 too12 tekens die alleen letters en cijfers bevatten).
2. Hallo minimale **grootte** van virtuele machines voor het primaire knooppunt Hallo type wordt aangedreven door Hallo **duurzaamheid** laag die u voor Hallo-cluster kiest. Hallo standaard voor Hallo duurzaamheid laag is Brons. Zie voor meer informatie over duurzaamheid [hoe toochoose Hallo Service Fabric-cluster betrouwbaarheid en duurzaamheid][service-fabric-cluster-capacity].
3. Selecteer Hallo VM-grootte en de prijscategorie. D-reeks VMs SSD-stations hebben en worden sterk aanbevolen voor stateful toepassingen. Geen gebruik van een VM SKU gedeeltelijke kernen heeft of kleiner zijn dan 7 GB aan beschikbare schijfruimte capaciteit. 
4. Hallo minimale **getal** van virtuele machines voor het primaire knooppunt Hallo type wordt aangedreven door Hallo **betrouwbaarheid** laag die u kiest. Hallo standaardwaarde voor de betrouwbaarheidslaag Hallo is Zilver. Zie voor meer informatie over de betrouwbaarheid, [hoe toochoose Hallo Service Fabric-cluster betrouwbaarheid en duurzaamheid][service-fabric-cluster-capacity].
5. Hallo aantal virtuele machines voor het knooppunttype Hallo kiezen. U kunt omhoog of omlaag Hallo aantal virtuele machines in een knooppunttype later op schalen, maar op het primaire knooppunttype hello, minimale hello wordt aangedreven door Hallo betrouwbaarheid niveau dat u hebt gekozen. Andere knooppunttypen kunnen een minimum van 1 VM hebben.
6. Aangepaste eindpunten configureren. Dit veld kunt u een door komma's gescheiden lijst met poorten die u wilt dat tooexpose via hello Azure Load Balancer toohello tooenter openbare Internet voor uw toepassingen. Bijvoorbeeld, als u van plan een cluster met web application tooyour toodeploy bent, typt u '80' hier tooallow verkeer op poort 80 in uw cluster. Zie voor meer informatie over eindpunten [communiceren met toepassingen][service-fabric-connect-and-communicate-with-services]
7. Configureren van cluster **diagnostics**. Diagnostische gegevens zijn standaard ingeschakeld op uw cluster tooassist met het oplossen van problemen. Als u wilt dat toodisable diagnostics wijzigen Hallo **Status** te schakelen**uit**. Het uitschakelen van diagnostische gegevens is **niet** aanbevolen.
8. Selecteer Hallo Fabric upgrademodus u wilt instellen van uw cluster op. Selecteer **automatische**, als u wilt dat Hallo system tooautomatically ophalen Hallo meest recente versie en probeer het tooupgrade uw cluster tooit. Hallo-modus te instellen**handmatige**, als u wilt dat toochoose een ondersteunde versie.

> [!NOTE]
> Wij ondersteunen alleen clusters die met een ondersteunde versie van service Fabric. Door het selecteren van Hallo **handmatige** modus u onderneemt op Hallo verantwoordelijkheid tooupgrade uw versie van cluster tooa ondersteund. Zie voor meer informatie op Hallo Fabric upgrademodus Hallo [service fabric-cluster upgrade-document.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3. Beveiliging
![Schermopname van beveiligingsconfiguraties op Azure-portal.][SecurityConfigs]

de laatste stap Hallo is tooprovide certificaat informatie toosecure Hallo cluster Hallo Sleutelkluis en certificaat informatie eerder hebt gemaakt.

* Hallo primaire certificaat voor velden te vullen met Hallo uitvoer ontleend aan het uploaden van Hallo **cluster certificaat** tooKey met behulp van kluis Hallo `Invoke-AddCertToKeyVault` PowerShell-opdracht.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Controleer Hallo **geavanceerde instellingen configureren** tooenter voor clientcertificaten voor vak **Beheerclient** en **alleen-lezen client**. Voer in deze velden Hallo vingerafdruk van het clientcertificaat admin en Hallo vingerafdruk van het certificaat alleen-lezengebruiker in, indien van toepassing. Wanneer beheerders tooconnect toohello cluster proberen, krijgen ze toegang alleen als ze beschikken over een certificaat met een vingerafdruk die overeenkomt met de Hallo vingerafdruk waarden die u hier opgeeft.  

#### <a name="4-summary"></a>4. Samenvatting
![Schermopname van Hallo start board weergeven "Deploying Service Fabric-Cluster." ][Notifications]

toocomplete hello cluster maken, klikt u op **samenvatting** toosee Hallo configuraties die u hebt opgegeven of downloaden hello Azure Resource Manager-sjabloon dat die toodeploy uw cluster gebruikt. Nadat u de instellingen verplicht voor Hallo hebt opgegeven, Hallo **OK** knop wordt groen en kunt u Hallo cluster maken van het proces starten door erop te klikken.

Voortgang van het Hallo maken in kennisgevingen hello, kunt u zien. (Klik op Hallo ' ' belpictogram bijna Hallo statusbalk Hallo rechterbovenhoek van het scherm). Als u hebt geklikt **pincode tooStartboard** tijdens het Hallo-cluster maken, ziet u **Service Fabric-Cluster implementeren** vastgemaakt toohello **Start** mededelingenbord.

### <a name="view-your-cluster-status"></a>De clusterstatus van uw bekijken
![Schermopname van het clusterdetails in Hallo-dashboard.][ClusterDashboard]

Als uw cluster is gemaakt, kunt u uw cluster in Hallo portal controleren:

1. Ga te**Bladeren** en klik op **Service Fabric-Clusters**.
2. Zoek uw cluster en klik erop.
3. U ziet nu Hallo details van het cluster in Hallo-dashboard, met inbegrip van het cluster Hallo openbaar eindpunt en een koppeling tooService Fabric Explorer.

Hallo **knooppunt Monitor** sectie op Hallo van het cluster dashboard blade Hallo aantal virtuele machines die in orde en niet in orde zijn aangeeft. U vindt meer informatie over de status van het cluster Hallo op [Service Fabric health model inleiding][service-fabric-health-introduction].

> [!NOTE]
> Service Fabric-clusters vereisen van een bepaald aantal knooppunten toobe altijd toomaintain beschikbaar en het behouden van status - waarnaar wordt verwezen tooas 'onderhouden quorum'. Therfore, het is doorgaans niet veilig tooshut omlaag alle machines in de cluster Hallo tenzij u eerst hebt uitgevoerd een [volledige back-up van de staat][service-fabric-reliable-services-backup-restore].
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>Extern verbinding maken met virtuele-Machineschaalset tooa-exemplaar of een clusterknooppunt
Elk Hallo NodeTypes geeft u in uw cluster resultaten in een virtuele-Machineschaalset ophalen van de installatie. Zie [extern verbinding tooa virtuele-Machineschaalset exemplaar] [ remote-connect-to-a-vm-scale-set] voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
U hebt op dit moment een beveiligde cluster dat gebruik van certificaten voor beheer-verificatie. Vervolgens [tooyour cluster verbinding](service-fabric-connect-to-secure-cluster.md) en meer informatie over hoe te[toepassing geheimen beheren](service-fabric-application-secret-management.md).  Ook meer informatie over [Service Fabric-ondersteuningsopties](service-fabric-support.md).

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
