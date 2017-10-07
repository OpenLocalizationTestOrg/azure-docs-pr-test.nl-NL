---
title: aaaCreate een Service Fabric-cluster in Azure | Microsoft Docs
description: Meer informatie over hoe toocreate een Windows- of Linux Service Fabric-cluster in Azure met behulp van PowerShell.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>Een beveiligde cluster maken in Azure met behulp van PowerShell
Deze zelfstudie laat zien hoe toocreate een Service Fabric-cluster (Windows of Linux) wordt uitgevoerd in Azure. Wanneer u klaar bent, hebt u een cluster met in Hallo cloud die u kunt toepassingen implementeren op.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maken van een beveiligde Service Fabric-cluster in Azure met behulp van PowerShell
> * Beveiligde Hallo-cluster met een X.509-certificaat
> * Verbinding maken met behulp van PowerShell toohello-cluster
> * Verwijderen van een cluster

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint:
- Als u geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- Hallo installeren [Service Fabric SDK en PowerShell-module](service-fabric-get-started.md)
- Hallo installeren [Azure Powershell-moduleversie 4.1 of hoger](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

Hallo na procedure maakt een voorbeeld van één knooppunt (één virtuele machine) Service Fabric-cluster. Hallo-cluster wordt beveiligd door een zelfondertekend certificaat dat wordt naast het Hallo-cluster gemaakt en vervolgens in een sleutelkluis geplaatst. Clusters met één knooppunt dan één virtuele machine kunnen niet worden geschaald en clusters preview kunnen niet worden toonewer bijgewerkte versies.

toocalculate kosten door het uitvoeren van een Service Fabric-cluster in Azure gebruik Hallo [Azure Prijscalculator](https://azure.microsoft.com/pricing/calculator/).
Zie voor meer informatie over het maken van Service Fabric-clusters [Service Fabric-cluster maken met behulp van Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="create-hello-cluster-using-azure-powershell"></a>Hallo-cluster met behulp van PowerShell voor Azure maken
1. Downloaden van een lokale kopie van hello Azure Resource Manager-sjabloon en het parameterbestand Hallo van Hallo [Azure Resource Manager-sjabloon voor Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub-opslagplaats.  *azuredeploy.JSON* hello Azure Resource Manager-sjabloon die een Service Fabric-cluster definieert is. *azuredeploy.parameters.JSON* een parameterbestand is voor u toocustomize Hallo Clusterimplementatie.

2. Aanpassen van de volgende parameters in Hallo Hallo *azuredeploy.parameters.json* parameterbestand:

   | Parameter       | Beschrijving | Voorgestelde waarde |
   | --------------- | ----------- | --------------- |
   | clusterLocation | Hello Azure-regio toowhich toodeploy Hallo cluster. | *bijvoorbeeld, westeurope, Oost-Aziatische, eastus* |
   | Clusternaam     | Naam van de cluster Hallo gewenste toocreate. | *bijvoorbeeld, bobs-sfpreviewcluster* |
   | adminUserName   | Hallo lokale beheerdersaccount op Hallo cluster virtuele machines. | *Een geldige gebruikersnaam voor Windows Server* |
   | adminPassword   | Wachtwoord van de lokale beheerdersaccount Hallo op Hallo cluster virtuele machines. | *Een geldig wachtwoord voor Windows Server* |
   | clusterCodeVersion | Hallo Service Fabric-versie toorun. (255.255.X.255 preview-versies zijn). | **255.255.5718.255** |
   | vmInstanceCount | Hallo aantal virtuele machines in uw cluster (kan worden 1 of 3-99). | **1** | *Geef slechts één virtuele machine voor een preview-cluster.* |

3. Open een PowerShell-console, aanmelding tooAzure en selecteer Hallo abonnement die u toodeploy Hallo cluster wilt toevoegen in:

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. Maken en een wachtwoord voor Hallo certificaat toobe die wordt gebruikt door de Service Fabric versleutelen.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Hallo-cluster en het certificaat door het uitvoeren van de volgende opdracht Hallo maken:

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   >Hallo `-CertificateSubjectName` parameter moet worden uitgelijnd met de Hallo clusterName parameter die is opgegeven in het parameterbestand hello, ook als het domein gekoppeld toohello Azure-regio Hallo u hebt gekozen, zoals: `clustername.eastus.cloudapp.azure.com`.

Zodra het Hallo-configuratie is voltooid, wordt deze informatie over het Hallo-cluster gemaakt in Azure. Hallo cluster certificaat toohello - CertificateOutputFolder directory op Hallo-pad voor deze parameter opgegeven worden ook gekopieerd. U moet dit certificaat tooaccess Service Fabric Explorer en bekijk Hallo-status van uw cluster.

Hallo-URL voor uw cluster, die mogelijk vergelijkbare toohello Noteer de volgende URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a>Toegang tot Service Fabric Explorer & Hallo-certificaat wijzigen ##

1. Dubbelklik op Hallo certificaat tooopen Hallo Wizard Certificaat importeren.

2. Standaardinstellingen gebruiken, maar zorg ervoor dat toocheck hello **deze sleutel als exporteerbaar markeren.** of u het selectievakje in Hallo **beveiliging voor persoonlijke sleutels** stap. Visual Studio moet tooexport Hallo certificaat bij het configureren van Azure Container register tooService Fabric-Cluster authenticatie verderop in deze zelfstudie.

3. U kunt nu Service Fabric Explorer openen in een browser. toodo Ga dus toohello **ManagementEndpoint** URL voor uw cluster met een webbrowser en selecteer Hallo-certificaat dat is opgeslagen op uw computer.

>[!NOTE]
>Wanneer u Service Fabric Explorer opent, ziet u een certificaatfout als u een zelfondertekend certificaat gebruikt. In de rand, hebt u tooclick *Details* en vervolgens Hallo *gaat u op de webpagina toohello* koppeling. In Chrome, hebt u tooclick *Geavanceerd* en vervolgens Hallo *gaan* koppeling.

>[!NOTE]
>Als Hallo maken van het cluster is mislukt, kunt u altijd opnieuw uitgevoerd Hallo opdracht Hallo-resources die al is geïmplementeerd werkt. Als een certificaat is gemaakt als onderdeel van de implementatie Hallo is mislukt, wordt een nieuwe gegenereerd. maken van het cluster tootroubleshoot Zie [Service Fabric-cluster maken met behulp van Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="connect-toohello-secure-cluster"></a>Verbinding maken met de beveiligde cluster toohello
Verbinding maken met behulp van Hallo Service Fabric PowerShell-module geïnstalleerd met Hallo Service Fabric SDK toohello-cluster.  Installeer eerst Hallo certificaat in archief van de Hallo persoonlijke (Mijn) van de huidige gebruiker Hallo op uw computer.  Hallo volgende PowerShell-opdracht uitvoeren:

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

U bent nu klaar tooconnect tooyour beveiligde cluster.

Hallo **Service Fabric** PowerShell-module biedt veel cmdlets voor het beheren van Service Fabric-clusters, toepassingen en services.  Gebruik Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello beveiligde cluster. Hallo certificaatvingerafdruk en eindpunt Verbindingsdetails zijn gevonden in het Hallo-uitvoer van de vorige stap.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Controleer of u verbonden bent en Hallo-cluster is in orde Hallo met [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>Resources opschonen

Een cluster is opgebouwd uit andere Azure-resources bovendien toohello clusterbron zelf. Hallo eenvoudigste manier toodelete Hallo cluster en alle Hallo resources verbruikt is toodelete Hallo resourcegroep.

Meld u bij tooAzure en selecteer Hallo abonnements-ID waarmee u tooremove Hallo cluster wilt toevoegen.  U kunt uw abonnements-ID vinden door logboekregistratie in toohello [Azure-portal](http://portal.azure.com). Hallo-resourcegroep en alle Hallo clusterbronnen met behulp van Hallo verwijderen [cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Maken van een Service Fabric-cluster in Azure
> * Beveiligde Hallo-cluster met een X.509-certificaat
> * Verbinding maken met behulp van PowerShell toohello-cluster
> * Verwijderen van een cluster

Vervolgens gaan toohello zelfstudie toolearn hoe na toodeploy een bestaande toepassing.
> [!div class="nextstepaction"]
> [Implementeer een bestaande .NET-toepassing met Docker Compose](service-fabric-host-app-in-a-container.md)
