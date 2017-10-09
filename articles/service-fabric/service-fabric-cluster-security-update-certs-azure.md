---
title: aaaManage certificaten in een Azure Service Fabric-cluster | Microsoft Docs
description: Beschrijft hoe nieuwe certificaten tooadd, rollovercertificaat en verwijderen van het certificaat tooor van een Service Fabric-cluster.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>Toevoegen of verwijderen van certificaten voor een Service Fabric-cluster in Azure
Het is raadzaam dat u raken met het Service Fabric X.509-certificaten gebruikt en vertrouwd met de Hallo zijn [security scenario's](service-fabric-cluster-security.md). U moet begrijpen wat een certificaat in het cluster is en wat wordt gebruikt voor, voordat u verder.

Service fabric kunt die u opgeven dat twee certificaten, een primaire en een secundaire cluster bij het configureren van beveiliging certificate tijdens het maken van het cluster in toevoeging tooclient certificaten. Raadpleeg te[maken van een azure-cluster via de portal](service-fabric-cluster-creation-via-portal.md) of [maken van een azure-cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) voor meer informatie over het instellen op voor het maken. Als u slechts één cluster certificaat opgeeft op voor het maken, klikt u vervolgens die wordt gebruikt als het primaire certificaat voor Hallo. U kunt een nieuw certificaat na het maken van het cluster toevoegen als een secundaire database.

> [!NOTE]
> Voor een beveiligde cluster, moet u altijd ten minste één geldig (niet ingetrokken en niet verlopen)-cluster-certificaat (primair of secundair) geïmplementeerd (zo niet, Hallo cluster niet meer werkt). 90 dagen voordat alle geldige certificaten verlopen, bereiken Hallo system genereert een waarschuwing trace en ook een waarschuwingsgebeurtenis health op Hallo-knooppunt. Er is momenteel geen e-mail of andere berichten naar service fabric worden verzonden over dit onderwerp. 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a>Een secundaire cluster-certificaat met behulp van de portal Hallo toevoegen

Secundaire cluster certificaat kan niet worden toegevoegd via hello Azure-portal. U hebt toouse Azure powershell voor die. Hallo proces wordt verderop in dit document beschreven.

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a>Hallo clustercertificaten met behulp van de portal Hallo uitwisselen

Nadat u hebt een certificaat secundaire cluster is geïmplementeerd als u wilt dat tooswap Hallo primaire en secundaire, vervolgens toohello beveiliging blade navigeren, en selecteer Hallo 'Wisseling met primaire' optie van Hallo context menu tooswap Hallo secundaire cert met Hallo primaire cert.

![Swap-certificaat][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a>Het certificaat voor een cluster met Hallo portal verwijderen

Voor een beveiligde cluster, moet u altijd ten minste één geldig (niet ingetrokken en niet verlopen)-certificaat (primair of secundair) geïmplementeerd zo niet, Hallo cluster niet meer werkt.

tooremove een secundair certificaat worden gebruikt voor clusterbeveiliging, navigeren toohello beveiliging blade en selecteer Hallo 'Delete' optie in het contextmenu Hallo op Hallo secundair certificaat.

Als uw bedoeling is tooremove Hallo certificaat dat is gemarkeerd als primaire, moet u tooswap met eerst secundaire Hallo en verwijder vervolgens de Hallo secundaire nadat het Hallo-upgrade is voltooid.

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>Toevoegen van een secundair certificaat met behulp van Resource Manager Powershell

Deze stappen wordt ervan uitgegaan dat u bekend bent met de werking van Resource Manager en ten minste één Service Fabric-cluster met een Resource Manager-sjabloon hebt geïmplementeerd en Hallo-sjabloon die u hebt gebruikt tooset Hallo cluster handige hebt. Ook wordt ervan uitgegaan dat u vertrouwd met een JSON bent.

> [!NOTE]
> Als u zoekt naar een voorbeeldsjabloon en parameters waarmee u toofollow langs of als uitgangspunt kunt, klikt u vervolgens het downloaden van deze [git-opslagplaats](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample). 
> 
> 

### <a name="edit-your-resource-manager-template"></a>De Resource Manager-sjabloon bewerken

Voorbeeld 5-VM-1-NodeTypes-Secure_Step2.JSON bevat voor een eenvoudige van volgende langs alle Hallo bewerkingen we brengen. Hallo-voorbeeld is beschikbaar op [git-opslagplaats](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).

**Zorg ervoor dat toofollow alle Hallo stappen**

**Stap 1:** Open Hallo Resource Manager-sjabloon gebruikt van toodeploy die u in de Cluster. (Als u Hallo voorbeeld van Hallo hierboven opslagplaats hebt gedownload, gebruikt u 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy een beveiligde cluster en opent u dat de sjabloon).

**Stap 2:** toevoegen **twee nieuwe parameters** 'secCertificateThumbprint' en 'secCertificateUrlValue' van het type 'string' toohello parameter gedeelte van uw sjabloon. U kunt Hallo volgende codefragment kopiëren en deze toohello sjabloon toevoegen. Afhankelijk van het Hallo-bron van de sjabloon, kunnen u al deze gedefinieerd, als dit het geval de volgende stap toohello verplaatsen. 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**Stap 3:** wijzigingen aanbrengen toohello **Microsoft.ServiceFabric/clusters** resource - Hallo 'Microsoft.ServiceFabric/clusters' resourcedefinitie niet vinden in de sjabloon. Onder de eigenschappen van deze definitie van vindt u 'Certificaat' JSON tag, die u moet er ongeveer als Hallo volgende JSON-fragment:

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Voeg een nieuwe tag 'thumbprintSecondary' en hieraan een waarde '[parameters('secCertificateThumbprint')]'.  

In dat geval nu resourcedefinitie Hallo als in de volgende hello eruitzien moet (afhankelijk van de bron van de sjabloon hello, deze mogelijk niet precies zoals Hallo codefragment hieronder). 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Als u wilt dat te**rollover HALLO cert**, geef vervolgens het nieuwe certificaat Hallo als primaire en verplaatsen Hallo huidige primaire als secundaire. Dit resulteert in Hallo overschakeling van uw huidige primaire toohello nieuwe certificaat in één stap van de implementatie.

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**Stap 4:** te wijzigingen aanbrengen**alle** hello **Microsoft.Compute/virtualMachineScaleSets** resourcedefinities - Hallo Microsoft.Compute/virtualMachineScaleSets bron vinden definitie. Schuif toohello 'publisher': 'Microsoft.Azure.ServiceFabric' onder 'virtualMachineProfile'.

In de instellingen voor Hallo service fabric publisher ziet u er ongeveer als volgt.

![Json_Pub_Setting1][Json_Pub_Setting1]

Hallo nieuwe cert vermeldingen tooit toevoegen

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

Hallo eigenschappen ziet er nu als volgt

![Json_Pub_Setting2][Json_Pub_Setting2]

Als u wilt dat te**rollover HALLO cert**, geef vervolgens het nieuwe certificaat Hallo als primaire en verplaatsen Hallo huidige primaire als secundaire. Dit resulteert in Hallo overschakeling van uw huidige toohello nieuwe certificaat in één stap van de implementatie. 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
Hallo eigenschappen ziet er nu als volgt

![Json_Pub_Setting3][Json_Pub_Setting3]


**Stap 5:** aanbrengen te**alle** hello **Microsoft.Compute/virtualMachineScaleSets** resourcedefinities - Hallo Microsoft.Compute/virtualMachineScaleSets bron vinden definitie. Schuif toohello 'vaultCertificates':, onder 'OSProfile'. Dit ziet er ongeveer als volgt.


![Json_Pub_Setting4][Json_Pub_Setting4]

Hallo secCertificateUrlValue tooit toevoegen. Hallo codefragment volgende gebruiken:

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
Nu Hallo resulterende Json moet als volgt uitzien.
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> Zorg ervoor dat u stap 4 en 5 hebt herhaald voor alle Hallo Nodetypes/Microsoft.Compute/virtualMachineScaleSets resourcedefinities in de sjabloon. Als u een van beide mist, Hallo certificaat wordt niet geïnstalleerd op deze VMSS en moet u onvoorspelbare resultaten in het cluster, met inbegrip van Hallo cluster tijdelijk niet beschikbaar (als u uiteindelijk geen geldige certificaten dat cluster Hallo kunt gebruiken voor beveiliging. Zo Controleer, voordat u doorgaat.
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a>Uw bestand tooreflect Hallo nieuwe Sjabloonparameters u die hierboven staan vermeld bewerken
Als u van Hallo voorbeeld Hallo gebruikmaakt [git-opslagplaats](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow samen, kunt u wijzigingen toomake starten in 5 in voorbeeld van Hallo-bestanden-VM-1-NodeTypes-Secure.paramters_Step2.JSON 

De parameter-bestand voor uw Resource Manager-sjabloon bewerken, Hallo twee nieuwe parameters voor secCertificateThumbprint en secCertificateUrlValue toevoegen. 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a>Hallo sjabloon tooAzure implementeren

- U zijn nu gereed toodeploy uw tooAzure sjabloon. Open een opdrachtprompt voor Azure PS-versie 1 +.
- Log in tooyour Azure-Account en selecteer Hallo specifieke azure-abonnement. Dit is een belangrijke stap voor mensen die toegang toomore dan één azure-abonnement hebben.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

Hallo sjabloon voorafgaande toodeploying test deze. Gebruik dezelfde resourcegroep die uw cluster wordt momenteel geïmplementeerd op Hallo.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

Hallo sjabloon tooyour resourcegroep implementeren. Gebruik dezelfde resourcegroep die uw cluster wordt momenteel geïmplementeerd op Hallo. Hallo New-AzureRmResourceGroupDeployment opdracht uitvoeren. U hoeft niet toospecify Hallo-modus, aangezien Hallo standaardwaarde **incrementele**.

> [!NOTE]
> Als u de modus tooComplete instelt, kunt u de resources die zich niet in uw sjabloon per ongeluk verwijderen. Dus gebruik deze niet in dit scenario.
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

Hier volgt een gevulde uit voorbeeld Hallo dezelfde powershell.

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

Zodra het Hallo-implementatie is voltooid, verbinding maken met behulp van tooyour-cluster Hallo nieuw certificaat en enkele query's uit te voeren. Als u kunnen toodo. Vervolgens kunt u het oude certificaat Hallo verwijderen. 

Als u een zelfondertekend certificaat gebruikt, vergeet niet tooimport bij uw lokale TrustedPeople-certificaatarchief.

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
Voor naslag is hier Hallo opdracht tooconnect tooa beveiligde cluster 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
Voor naslag is hier Hallo opdracht tooget cluster status

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a>Toepassing certificaten toohello-cluster implementeren.

U kunt dezelfde stappen zoals wordt beschreven in stap 5 hierboven toohave Hallo certificaten op basis van een keyvault toohello knooppunten geïmplementeerd hello gebruiken. u moet alleen definiëren en andere parameters gebruikt.


## <a name="adding-or-removing-client-certificates"></a>Het toevoegen of verwijderen van clientcertificaten

U kunt in toevoeging toohello clustercertificaten, client certificaten tooperform beheerbewerkingen op een service fabric-cluster toevoegen.

U kunt twee soorten clientcertificaten - beheerder toevoegen of alleen-lezen. Deze kunnen vervolgens worden gebruikt toocontrol toegang toohello bewerkingen en zoekopdrachten op Hallo-cluster. Standaard worden clustercertificaten hello toohello Admin certificaten lijst met toegestane toegevoegd.

u kunt een willekeurig aantal clientcertificaten opgeven. Elke toevoeging/verwijdering resulteert in een configuratie update toohello service fabric-cluster


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>Clientcertificaten - beheerder toe te voegen of alleen-lezen via de portal

1. Navigeer toohello beveiliging blade en selecteer Hallo '+ verificatie' knop boven op Hallo beveiliging blade.
2. Kies op de blade 'Authentication toevoegen' Hallo Hallo 'Verificatietype' - 'Client alleen-lezen' of 'Admin client'
3. Hallo-autorisatiemethode nu kiezen. Dit tooService Fabric geeft aan of het opzoeken van dit certificaat met behulp van de onderwerpnaam Hallo of Hallo vingerafdruk. Het is in het algemeen geen goed beveiligd practice toouse Hallo autorisatiemethode van de onderwerpnaam. 

![Clientcertificaat toevoegen][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a>Verwijderen van clientcertificaten - beheer of met behulp van alleen-lezen Hallo portal

tooremove een secundair certificaat voor clusterbeveiliging, navigeren toohello beveiliging blade en selecteer Hallo 'Delete' optie in het contextmenu Hallo op Hallo specifiek certificaat kan worden gebruikt.



## <a name="next-steps"></a>Volgende stappen
Lees deze artikelen voor meer informatie over het Clusterbeheer:

* [Het upgradeproces service Fabric-Cluster en de verwachtingen van u](service-fabric-cluster-upgrade.md)
* [Op rollen gebaseerde toegang instellen voor clients](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


