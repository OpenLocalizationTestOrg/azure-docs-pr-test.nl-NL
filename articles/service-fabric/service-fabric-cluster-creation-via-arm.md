---
title: aaaCreate een Azure Service Fabric-cluster van een sjabloon | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van een beveiligde Service Fabric-cluster in Azure met behulp van Azure Resource Manager en Azure Key Vault Azure Active Directory (Azure AD) voor clientverificatie.
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>Maken van een Service Fabric-cluster met behulp van Azure Resource Manager
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Azure Portal](service-fabric-cluster-creation-via-portal.md)
>
>

Deze stapsgewijze handleiding helpt u bij het instellen van een beveiligde Azure Service Fabric-cluster in Azure met Azure Resource Manager. We erkennen dat artikel Hallo lang is. Tenzij u al grondig bekend met Hallo inhoud bent, worden echter zeker toofollow elke stap zorgvuldig.

Hallo handleiding wordt ingegaan op Hallo procedures te volgen:

* Een Azure sleutelkluis tooupload certificaten voor een cluster en de toepassing beveiliging instellen
* Maken van een beveiligde cluster in Azure met Azure Resource Manager
* Verifiëren van gebruikers met behulp van Azure Active Directory (Azure AD) voor Clusterbeheer

Een beveiligde cluster is een cluster waarmee wordt voorkomen onbevoegde toegang toomanagement bewerkingen dat. Dit omvat implementeren, bijwerken, en verwijderen toepassingen, services en Hallo gegevens die ze bevatten. Een niet-beveiligde cluster is een cluster iedereen kan verbinding maken met tooat elk gewenst moment en beheerbewerkingen uitvoeren. Hoewel het mogelijk toocreate een niet-beveiligde cluster, raden we u aan een beveiligde cluster te maken van Hallo begin. Omdat een niet-beveiligde cluster later niet kan worden beveiligd, kan een nieuw cluster moet worden gemaakt.

Hallo-concept van het maken van beveiligde clusters is Hallo hetzelfde, ongeacht of deze Windows- of Linux-clusters. Zie voor meer informatie en helper scripts voor het maken van beveiligde Linux-clusters, [maken van beveiligde clusters onder Linux](#secure-linux-clusters).

## <a name="sign-in-tooyour-azure-account"></a>Meld u aan tooyour Azure-account
Maakt gebruik van deze handleiding [Azure PowerShell][azure-powershell]. Wanneer u een nieuwe PowerShell-sessie start, meld u aan tooyour Azure-account en uw abonnement te selecteren voordat u Azure-opdrachten uitvoeren.

Meld u aan tooyour Azure-account:

```powershell
Login-AzureRmAccount
```

Selecteer uw abonnement:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>Een sleutelkluis instellen
Deze sectie wordt beschreven voor het maken van een sleutelkluis voor een Service Fabric-cluster in Azure en voor Service Fabric-toepassingen. Raadpleeg voor een volledige handleiding tooAzure Sleutelkluis, toohello [Sleutelkluis instructiehandleiding][key-vault-get-started].

Service Fabric gebruikt x.509-certificaten toosecure een cluster en beveiligingsfuncties van toepassing. U Sleutelkluis toomanage certificaten gebruiken voor Service Fabric-clusters in Azure. Wanneer een cluster wordt geïmplementeerd in Azure, worden de hello Azure-resourceprovider die verantwoordelijk is voor het maken van Service Fabric-clusters certificaten ophaalt uit Sleutelkluis en installeert ze op Hallo cluster virtuele machines.

Hallo illustreert volgende diagram Hallo relatie tussen Azure Sleutelkluis, een Service Fabric-cluster en hello Azure-resourceprovider die gebruikmaakt van certificaten die zijn opgeslagen in een sleutelkluis bij het maken van een cluster:

![Diagram van de installatie van het certificaat][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Een resourcegroep maken
de eerste stap Hallo is toocreate een resourcegroep specifiek voor uw sleutelkluis. Het is raadzaam dat u de sleutelkluis Hallo in een eigen resourcegroep geplaatst. Deze actie kunt u Hallo berekenings- en resourcegroepen, met inbegrip van Hallo resourcegroep die uw Service Fabric-cluster bevat zonder verlies van uw sleutels en geheimen verwijderen. Hallo-resourcegroep met de sleutelkluis _Hallo moet dezelfde regio_ als Hallo-cluster dat wordt gebruikt.

Als u van plan toodeploy clusters in meerdere regio's bent, het is raadzaam dat u de resourcegroep Hallo en Hallo sleutelkluis op een manier die welke regio hoort aangeeft bij de naam.  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
Hallo-uitvoer ziet er als volgt:

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>Een sleutelkluis maken in de nieuwe resourcegroep Hallo
Hallo sleutelkluis _moet zijn ingeschakeld voor de implementatie van_ tooallow compute resource provider tooget certificaten van het Hallo en installeer deze op de virtuele machine-exemplaren:

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

Hallo-uitvoer ziet er als volgt:

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
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
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a>Gebruik een bestaande sleutelkluis

een bestaande sleutelkluis toouse u _moet inschakelen voor de implementatie van_ tooallow Hallo compute resource provider tooget certificaten uit en installeer deze op de clusterknooppunten:

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>Certificaten tooyour sleutelkluis toevoegen

Certificaten worden gebruikt in Service Fabric tooprovide verificatie en versleuteling toosecure verschillende aspecten van een cluster en de toepassingen. Zie voor meer informatie over hoe de certificaten worden gebruikt in Service Fabric, [scenario's voor beveiliging van Service Fabric-cluster][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Cluster en de server-certificaat (vereist)
Dit certificaat is vereist toosecure een cluster en te voorkomen dat onbevoegde toegang tooit. Dit biedt een clusterbeveiliging op twee manieren:

* Cluster-verificatie: knooppunt naar communicatie voor cluster federation verifieert. Alleen knooppunten die u hun identiteit met dit certificaat bewijzen kunnen kunnen Hallo-cluster toevoegen.
* Server-verificatie: verifieert Hallo cluster management eindpunten tooa management-client, zodat hello Beheerclient weet het echte cluster toohello communiceert. Dit certificaat biedt ook een met SSL voor Hallo HTTPS beheer-API en voor Service Fabric Explorer via HTTPS.

tooserve deze doeleinden Hallo certificaat moet voldoen aan Hallo volgens de vereisten:

* Hallo-certificaat moet een persoonlijke sleutel bevatten.
* Hallo-certificaat moet worden gemaakt voor sleuteluitwisseling exporteerbaar tooa Personal Information Exchange (.pfx)-bestand is.
* de onderwerpnaam van het Hallo-certificaat moet overeenkomen met de Hallo-domein dat u tooaccess Hallo Service Fabric-cluster. Deze overeenkomst is vereist tooprovide een met SSL voor eindpunten voor beheer van het cluster Hallo-HTTPS en de Service Fabric Explorer. U kunt een SSL-certificaat kan niet verkrijgen van een certificeringsinstantie (CA) voor Hallo. cloudapp.azure.com domein. U moet een aangepaste domeinnaam voor uw cluster. Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, hello onderwerpnaam van het certificaat moet overeenkomen met Hallo aangepaste domeinnaam die u voor uw cluster gebruikt.

### <a name="application-certificates-optional"></a>Toepassingscertificaten (optioneel)
Een willekeurig aantal extra certificaten kan worden geïnstalleerd op een cluster om beveiligingsredenen toepassing. Voordat u uw cluster maakt, overweeg Hallo scenario's voor Toepassingsbeveiliging waarvoor een certificaat toobe geïnstalleerd op Hallo knooppunten, zoals:

* Versleuteling en ontsleuteling van configuratiewaarden die van toepassing.
* Codering van gegevens over knooppunten tijdens de replicatie.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Certificaten voor Azure-resource provider opmaak
U kunt toevoegen en gebruiken van persoonlijke sleutel (PFX-bestanden) rechtstreeks via de sleutelkluis. Hello Azure compute resourceprovider vereist echter sleutels toobe opgeslagen in een speciale notatie JSON (JavaScript Object)-indeling. Hallo-indeling bevat Hallo pfx-bestand als een base 64 gecodeerde tekenreeks zijn en Hallo-wachtwoord voor persoonlijke sleutel. tooaccommodate vault voor deze vereisten, Hallo sleutels moeten worden geplaatst in een JSON-tekenreeks en vervolgens als 'geheimen' hello sleutel worden opgeslagen.

toomake dit eenvoudiger, verwerkt een [PowerShell-module is beschikbaar op GitHub][service-fabric-rp-helpers]. toouse Hallo-module, Hallo te volgen:

1. Hallo volledige inhoud van de opslagplaats Hallo downloaden naar een lokale map.
2. Ga toohello lokale map.
2. Hallo ServiceFabricRPHelpers module in uw PowerShell-venster importeren:

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

Hallo `Invoke-AddCertToKeyVault` opdracht in deze PowerShell-module automatisch de persoonlijke sleutel van een certificaat in een JSON-tekenreeks indelingen en toohello sleutelkluis geüpload. Hallo opdracht tooadd Hallo cluster certificaat en een sleutelkluis voor extra toepassing certificaten toohello gebruiken. Herhaal deze stap voor elke extra certificaten tooinstall in uw cluster.

#### <a name="uploading-an-existing-certificate"></a>Een bestaand certificaat uploaden

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

Als er een fout optreedt, zoals Hallo een weergegeven, betekent dit meestal dat er een conflict resource-URL. tooresolve hello conflict Hallo sleutelkluis-naam wijzigen.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Nadat het Hallo-conflict is opgelost, er Hallo uitvoer als volgt:

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>U moet Hallo drie voorgaande tekenreeksen, CertificateThumbprint SourceVault en CertificateURL, tooset van een beveiligde Service Fabric-cluster en de tooobtain toepassingscertificaten die u voor de beveiliging van toepassingen gebruikt. Als u niet Hallo tekenreeksen opslaat, kan het moeilijk tooretrieve ze een query uitgevoerd op Hallo key later Vault zijn.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>Een zelfondertekend certificaat maken en uploaden toohello sleutelkluis

Als u al uw certificaten toohello-sleutelkluis hebt geüpload, moet u deze stap overslaan. Deze stap is voor een nieuw zelfondertekend certificaat genereren en uploaden tooyour sleutelkluis. Nadat u parameters in het volgende script Hallo Hallo wijzigen en vervolgens uit te voeren, moet u worden gevraagd om het wachtwoord voor een certificaat.  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

Als er een fout optreedt, zoals Hallo een weergegeven, betekent dit meestal dat er een conflict resource-URL. tooresolve Hallo conflict wijziging Hallo sleutelkluisnaam, de naam van de RG, enzovoort.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Nadat het Hallo-conflict is opgelost, er Hallo uitvoer als volgt:

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>U moet Hallo drie voorgaande tekenreeksen, CertificateThumbprint SourceVault en CertificateURL, tooset van een beveiligde Service Fabric-cluster en de tooobtain toepassingscertificaten die u voor de beveiliging van toepassingen gebruikt. Als u niet Hallo tekenreeksen opslaat, kan het moeilijk tooretrieve ze een query uitgevoerd op Hallo key later Vault zijn.

 Op dit moment hebt u Hallo elementen in plaats te volgen:

* Hallo sleutelkluis resourcegroep.
* Hallo sleutelkluis en de URL (SourceVault in Hallo voorafgaand aan de uitvoer van PowerShell genoemd).
* Hallo cluster certificaat voor serververificatie en de bijbehorende URL in de sleutelkluis Hallo.
* Hallo toepassingscertificaten en de URL's in de sleutelkluis Hallo.


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>Azure Active Directory instellen voor clientverificatie

Azure AD kan organisaties (ook wel tenants) toomanage gebruiker toegang tooapplications. Toepassingen worden onderverdeeld in die met een webgebaseerde gebruikersinterface voor aanmelding en die een native client-ervaring. In dit artikel gaan we ervan uit dat u al een tenant hebt gemaakt. Als u niet hebt, starten door te lezen [hoe tooget een Azure Active Directory-tenant][active-directory-howto-tenant].

Een Service Fabric-cluster biedt verschillende vermelding punten tooits beheerfunctionaliteit, met inbegrip van Hallo webgebaseerde [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] en [Visual Studio] [service-fabric-manage-application-in-visual-studio]. Als gevolg hiervan, maakt u twee Azure AD-toepassingen toocontrol toegang toohello cluster, een webtoepassing en een systeemeigen toepassing.

toosimplify bepaalde Hallo stappen betrokken bij de Azure AD configureren met een Service Fabric-cluster, hebben wij een set Windows PowerShell-scripts.

> [!NOTE]
> Hallo volgende stappen uit voordat u Hallo-cluster maakt, moet u voltooien. Omdat Hallo scripts verwacht dat de clusternamen van de- en eindpunten, wordt Hallo waarden moeten worden gepland en niet de waarden die u al hebt gemaakt.

1. [Hallo-scripts downloaden] [ sf-aad-ps-script-download] tooyour computer.
2. Klik met de rechtermuisknop Hallo zip-bestand, selecteer **eigenschappen**, selecteer Hallo **blokkering** selectievakje en klik vervolgens op **toepassen**.
3. Pak het zip-bestand Hallo.
4. Voer `SetupApplications.ps1`, en geef Hallo TenantId, ClusterName en WebApplicationReplyUrl als parameters. Bijvoorbeeld:

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    U vindt uw TenantId door het uitvoeren van PowerShell-opdracht Hallo `Get-AzureSubscription`. Uitvoeren van deze opdracht geeft Hallo TenantId voor elk abonnement.

    Clusternaam is gebruikte tooprefix hello Azure AD-toepassingen die zijn gemaakt door Hallo-script. Hoeft niet de naam van de werkelijke cluster Hallo toomatch exact. Het beoogde alleen toomake is het eenvoudiger toomap Azure AD-artefacten toohello Service Fabric-cluster dat ze worden gebruikt met.

    WebApplicationReplyUrl is Hallo standaardeindpunt die Azure AD tooyour gebruikers retourneert nadat ze Voltooi de aanmelding. Dit eindpunt als Hallo Service Fabric Explorer eindpunt voor uw cluster, dat standaard is ingesteld:

    https://&lt;cluster_domain&gt;: 19080/Explorer

    U bent na vragen aan gebruiker toosign in tooan-account met voor hello Azure AD-tenant beheerdersbevoegdheden. Nadat u zich aanmeldt, Hallo script maakt Hallo web- en systeemeigen toepassingen toorepresent Service Fabric-cluster. Als u hello-tenant-toepassingen in Hallo bekijkt [klassieke Azure-portal][azure-classic-portal], ziet u twee nieuwe vermeldingen:

   * *Clusternaam*\_Cluster
   * *Clusternaam*\_Client

   Hallo-script wordt afgedrukt Hallo JSON vereist door hello Azure Resource Manager-sjabloon wanneer u Hallo-cluster in de volgende sectie hello, maakt dus is het een goed idee tookeep Hallo PowerShell-venster openen.

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>Een Service Fabric-cluster Resource Manager-sjabloon maken
In deze sectie levert Hallo Hallo voorgaande PowerShell-opdrachten in het Resource Manager-sjabloon van een Service Fabric-cluster worden gebruikt.

Voorbeeld Resource Manager-sjablonen zijn beschikbaar in Hallo [Azure snel starten-sjablonengalerie op GitHub][azure-quickstart-templates]. Deze sjablonen kunnen worden gebruikt als een beginpunt voor uw cluster-sjabloon.

### <a name="create-hello-resource-manager-template"></a>Hallo Resource Manager-sjabloon maken
Deze handleiding gebruikt Hallo [beveiligde 5 knooppunten] [ service-fabric-secure-cluster-5-node-1-nodetype] voorbeeldsjabloon en sjabloonparameters. Download `azuredeploy.json` en `azuredeploy.parameters.json` tooyour computer en opent u beide bestanden in uw favoriete teksteditor.

### <a name="add-certificates"></a>Certificaten toevoegen
U kunt certificaten tooa cluster Resource Manager-sjabloon toevoegen door te verwijzen naar Hallo sleutelkluis waarin de certificaatsleutels Hallo. Het is raadzaam dat u Hallo sleutelkluis waarden in een Resource Manager-sjabloonbestand parameters plaatsen. In dat geval houdt Hallo Resource Manager sjabloonbestand herbruikbare en gratis waarden specifieke tooa implementatie.

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>Alle certificaten toohello virtuele-machineschaalset osProfile toevoegen
Elk certificaat dat geïnstalleerd in Hallo cluster moet worden geconfigureerd in Hallo osProfile sectie van Hallo scale set resource (Microsoft.Compute/virtualMachineScaleSets). Deze actie geïnstrueerd Hallo resource provider tooinstall Hallo certificaat op Hallo van virtuele machines. Deze installatie omvat zowel Hallo cluster certificaat als een toepassing beveiligingscertificaten dat u van plan toouse voor uw toepassingen bent:

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>Hallo Service Fabric-cluster certificaat configureren
certificaat voor clientverificatie Hallo-cluster moet worden geconfigureerd in beide Hallo Service Fabric-cluster-bron (Microsoft.ServiceFabric/clusters) en Hallo Service Fabric-extensie voor de virtuele-machineschaalset stelt in Hallo scale set virtuelemachinebron. Deze benadering kunt Hallo Service Fabric resource provider tooconfigure voor gebruik voor verificatie van de cluster en serververificatie voor eindpunten voor beheer.

##### <a name="virtual-machine-scale-set-resource"></a>Virtuele-machineschaalset resource:
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a>Service Fabric-resource:
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a>Invoegen van de configuratie van Azure AD
Hello Azure AD-configuratie die u eerder hebt gemaakt, kan worden ingevoegd rechtstreeks in het Resource Manager-sjabloon. Echter, raden wij dat u eerst Hallo waarden voor het uitpakken naar een herbruikbare parameters bestand tookeep Hallo Resource Manager-sjabloon en implementatie van de specifieke tooa waarden.

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### < een ' configureren-arm"></a>Sjabloonparameters Resource Manager configureren
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
Gebruik tot slot Hallo uitvoerwaarden uit de sleutelkluis Hallo en Azure AD PowerShell-opdrachten toopopulate Hallo-parameterbestand:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
Op dit moment hebt u Hallo elementen in plaats te volgen:

* Sleutelkluis-resourcegroep
  * Key Vault
  * Certificaat voor serververificatie cluster
  * Gegevens uitwisselen certificaat
* Azure Active Directory-tenant
  * Azure AD-toepassing voor het web gebaseerde beheer en de Service Fabric Explorer
  * Azure AD-toepassing voor beheer van native client
  * Gebruikers en hun rollen
* Service Fabric-cluster Resource Manager-sjabloon
  * Certificaten die zijn geconfigureerd met behulp van de sleutelkluis
  * Azure Active Directory wordt uitgevoerd

Hallo volgende diagram ziet u waar uw sleutelkluis en de configuratie van Azure AD in uw Resource Manager-sjabloon inpassen.

![Afhankelijkheidskaart van Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>Hallo-cluster maken
U bent nu klaar toocreate Hallo cluster met behulp van [Azure-resource sjabloonimplementatie][resource-group-template-deploy].

#### <a name="test-it"></a>Testen
Gebruik Hallo volgende PowerShell-opdracht tootest Resource Manager-sjabloon met een parameterbestand:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>Implementeren
Als Hallo Resource Manager-sjabloon test is geslaagd, gebruikt u Hallo volgende PowerShell-opdracht toodeploy Resource Manager-sjabloon met een parameterbestand met:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>Gebruikers tooroles toewijzen
Nadat u Hallo toepassingen toorepresent uw cluster hebt gemaakt, uw gebruikers toewijzen toohello rollen die worden ondersteund door Service Fabric: alleen-lezen en de beheerder. U kunt Hallo rollen toewijzen met behulp van Hallo [klassieke Azure-portal][azure-classic-portal].

1. Ga in de Azure-portal hello, tooyour tenant en selecteer vervolgens **toepassingen**.
2. Selecteer de webtoepassing hello, heeft een naam zoals `myTestCluster_Cluster`.
3. Klik op Hallo **gebruikers** tabblad.
4. Selecteer een gebruiker tooassign en klik vervolgens op Hallo **toewijzen** knop Hallo onder welkomstscherm aan.

    ![Gebruikers tooroles knop toewijzen][assign-users-to-roles-button]
5. Selecteer Hallo rol tooassign toohello gebruiker.

    ![In het dialoogvenster 'Gebruikers toewijzen'][assign-users-to-roles-dialog]

> [!NOTE]
> Zie voor meer informatie over functies in Service Fabric [toegangsbeheer op basis van rollen voor Service Fabric-clients](service-fabric-cluster-security-roles.md).
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>Beveiligde clusters onder Linux maken
toomake hello proces eenvoudiger, die we hebt opgegeven een [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux). Voordat u dit script helper gebruiken, zorg ervoor dat u al Azure-opdrachtregelinterface (CLI) geïnstalleerd en is in het pad. Zorg ervoor dat Hallo script tooexecute machtigingen door te voeren heeft `chmod +x cert_helper.py` nadat deze is gedownload. de eerste stap Hallo is toosign in tooyour Azure-account met CLI Hello `azure login` opdracht. Na het aanmelden tooyour Azure-account, gebruik Hallo helper script met de Certificeringsinstantie certificaat heeft ondertekend, als de volgende opdracht toont Hallo:

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

Hallo - ifile parameter kan duren voordat een pfx-bestand of een .pem-bestand als invoer met Hallo certificaattype (pfx of pem of ss als het een zelf-ondertekend certificaat).
Hallo parameter -h wordt afgedrukt Hallo help-tekst.


Met deze opdracht retourneert Hallo na drie tekenreeksen als Hallo uitvoer:

* SourceVaultID die Hallo-id voor Hallo nieuwe KeyVault ResourceGroup deze voor u gemaakt
* CertificateUrl voor toegang tot Hallo certificaat
* CertificateThumbprint die wordt gebruikt voor verificatie

Hallo volgende voorbeeld ziet u hoe toouse Hallo opdracht:

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
Hallo voorafgaand aan de opdracht geeft u drie tekenreeksen als volgt Hallo uitvoeren:

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

de onderwerpnaam van het Hallo-certificaat moet overeenkomen met de Hallo-domein dat u tooaccess Hallo Service Fabric-cluster. Deze overeenkomst is vereist tooprovide een met SSL voor eindpunten voor beheer van het cluster Hallo-HTTPS en de Service Fabric Explorer. U kunt een SSL-certificaat kan niet verkrijgen van een Certificeringsinstantie voor Hallo `.cloudapp.azure.com` domein. U moet een aangepaste domeinnaam voor uw cluster. Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, hello onderwerpnaam van het certificaat moet overeenkomen met Hallo aangepaste domeinnaam die u voor uw cluster gebruikt.

Deze onderwerpnamen zijn Hallo vermeldingen moet u toocreate beveiligde Service Fabric-cluster (zonder Azure AD), zoals beschreven op [configureren Resource Manager-Sjabloonparameters](#configure-arm). Beveiligde cluster toohello verbinding kan maken door Hallo instructies voor [verificatie van client access tooa cluster](service-fabric-connect-to-secure-cluster.md). Preview-Linux-clusters bieden geen ondersteuning voor Azure AD-verificatie. U kunt admin en client rollen toewijzen, zoals beschreven in Hallo [toewijzen van rollen toousers](#assign-roles) sectie. Wanneer u de beheerder en client rollen voor een Linux-preview-cluster opgeven, hebt u tooprovide certificaatvingerafdrukken voor verificatie. (U bieden geen onderwerpnaam hello, omdat geen validatie van certificaatketen of certificaatintrekkingslijst wordt uitgevoerd in deze preview-versie.)

Als u wilt dat toouse een zelfondertekend certificaat voor het testen, kunt u hetzelfde script toogenerate een Hallo. Vervolgens kunt u Hallo tooyour sleutelkluis-certificaat uploaden door Hallo vlag `ss` in plaats van het pad en de certificaat-naam van certificaat Hallo bieden. Zie bijvoorbeeld Hallo opdracht voor het maken en uploaden van een zelfondertekend certificaat te volgen:

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
Met deze opdracht retourneert Hallo dezelfde drie tekenreeksen: SourceVault CertificateUrl en CertificateThumbprint. U kunt vervolgens Hallo tekenreeksen toocreate zowel een beveiligde Linux-cluster en een locatie waar de zelf-ondertekend certificaat Hallo is geplaatst. U moet Hallo zelf-ondertekend certificaat tooconnect toohello cluster. Beveiligde cluster toohello verbinding kan maken door Hallo instructies voor [verificatie van client access tooa cluster](service-fabric-connect-to-secure-cluster.md).

de onderwerpnaam van het Hallo-certificaat moet overeenkomen met de Hallo-domein dat u tooaccess Hallo Service Fabric-cluster. Deze overeenkomst is vereist tooprovide een met SSL voor eindpunten voor beheer van het cluster Hallo-HTTPS en de Service Fabric Explorer. U kunt een SSL-certificaat kan niet verkrijgen van een Certificeringsinstantie voor Hallo `.cloudapp.azure.com` domein. U moet een aangepaste domeinnaam voor uw cluster. Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, hello onderwerpnaam van het certificaat moet overeenkomen met Hallo aangepaste domeinnaam die u voor uw cluster gebruikt.

U kunt ook opgeven Hallo parameters van Hallo helper script in hello Azure-portal, zoals beschreven in Hallo [een cluster maken in Azure-portal Hallo](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) sectie.

## <a name="next-steps"></a>Volgende stappen
U hebt op dit moment een beveiligde cluster met Azure Active Directory verstrekken management-verificatie. Vervolgens [tooyour cluster verbinding](service-fabric-connect-to-secure-cluster.md) en meer informatie over hoe te[toepassing geheimen beheren](service-fabric-application-secret-management.md).

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>Problemen met Azure Active Directory in te stellen voor clientverificatie
Als u een probleem ondervindt terwijl u Azure AD voor clientverificatie instelt, raadpleegt u Hallo mogelijke oplossingen in deze sectie.

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>Service Fabric Explorer vraagt u een certificaat tooselect
#### <a name="problem"></a>Probleem
Nadat u zich aanmeldt met succes tooAzure AD in Service Fabric Explorer, Hallo browser retourneert toohello startpagina, maar wordt gevraagd of u een certificaat tooselect.

![Dialoogvenster voor SFX certificaat selecteren][sfx-select-certificate-dialog]

#### <a name="reason"></a>Reden
Hallo-gebruiker is niet een rol in Azure AD-cluster toepassing hello toegewezen. Azure AD-verificatie mislukt dus bij Service Fabric-cluster. Service Fabric Explorer terugvalt toocertificate verificatie.

#### <a name="solution"></a>Oplossing
Hallo-instructies voor het instellen van Azure AD en gebruikersrollen toewijzen. Ook wordt aangeraden dat u 'Gebruiker toewijzing vereist tooaccess app' inschakelt als `SetupApplications.ps1` biedt.

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>Verbinding met PowerShell mislukt met een fout: 'hello opgegeven referenties zijn ongeldig'
#### <a name="problem"></a>Probleem
Wanneer u PowerShell tooconnect toohello cluster met behulp van 'AzureActiveDirectory' beveiligingsmodus, nadat u zich aanmeldt met succes tooAzure AD, Hallo verbinding is mislukt met een fout: "hello opgegeven referenties zijn ongeldig."

#### <a name="solution"></a>Oplossing
Deze oplossing is dezelfde zijn als een voorgaande Hallo Hallo.

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>Service Fabric Explorer een fout retourneert wanneer u zich aanmeldt: 'AADSTS50011'
#### <a name="problem"></a>Probleem
Wanneer u toosign in tooAzure AD in Service Fabric Explorer, Hallo pagina een fout geretourneerd: ' AADSTS50011: Hallo antwoordadres &lt;url&gt; komt niet overeen met de Hallo antwoordadressen is geconfigureerd voor de toepassing hello: &lt;guid&gt;."

![Antwoordadres SFX komt niet overeen met][sfx-reply-address-not-match]

#### <a name="reason"></a>Reden
Hallo-cluster (web)-toepassing waarmee de Service Fabric Explorer probeert tooauthenticate met Azure AD en als onderdeel van de aanvraag Hallo biedt Hallo omleiding retour-URL. Maar Hallo-URL wordt niet vermeld in de toepassing hello Azure AD **antwoord-URL** lijst.

#### <a name="solution"></a>Oplossing
Op Hallo **configureren** tabblad Hallo (webtoepassing)-cluster, het toevoegen van Hallo-URL van de Service Fabric Explorer toohello **antwoord-URL** lijst of een van de items in de lijst Hallo Hallo vervangt. Wanneer u klaar bent, sla de wijziging.

![Web application antwoord-url][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>Hallo-cluster met behulp van Azure AD-verificatie via PowerShell verbinding
tooconnect hello Service Fabric-cluster gebruiken Hallo voorbeeld van de PowerShell-opdracht te volgen:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

Zie toolearn over Hallo Connect-ServiceFabricCluster cmdlet [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>Kan ik Hallo dezelfde Azure AD-tenant in meerdere clusters gebruiken?
Ja. Maar vergeet niet tooadd Hallo-URL van de Service Fabric Explorer tooyour cluster (web)-toepassing. Service Fabric Explorer anders werkt niet.

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>Waarom moet ik een servercertificaat terwijl Azure AD is ingeschakeld?
FabricClient en FabricGateway uitvoeren een wederzijdse verificatie. Tijdens de verificatie van Azure AD, Azure AD-integratie biedt een client toohello identiteitsserver en is de identiteit van de server Hallo gebruikte tooverify Hallo-servercertificaat. Zie voor meer informatie over Service Fabric-certificaten [X.509-certificaten en Service Fabric][x509-certificates-and-service-fabric].

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

