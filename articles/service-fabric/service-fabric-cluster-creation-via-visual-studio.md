---
title: aaaSetting van een Service Fabric-cluster met behulp van Visual Studio | Microsoft Docs
description: Hierin wordt beschreven hoe tooset van een Service Fabric-cluster met behulp van Azure Resource Manager-sjabloon is gemaakt door een Azure Resource Group-project in Visual Studio
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Een Service Fabric-cluster instellen met behulp van Visual Studio
Dit artikel wordt beschreven hoe tooset van een Azure Service Fabric-cluster met behulp van Visual Studio en een Azure Resource Manager-sjabloon. Een Visual Studio Azure resource group toocreate Hallo projectsjabloon zullen worden gebruikt. Nadat het Hallo-sjabloon is gemaakt, kan worden geïmplementeerd rechtstreeks tooAzure vanuit Visual Studio. Het kan ook worden gebruikt vanuit een script of als onderdeel van de faciliteit continue integratie (CI).

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Een sjabloon voor Service Fabric-cluster met behulp van een Azure-resourcegroepproject maken
tooget gestart, opent u Visual Studio en maak een Azure-resourcegroepproject (beschikbaar in Hallo **Cloud** map):

![Het dialoogvenster Nieuw Project met de Azure-resourcegroepproject geselecteerd][1]

U kunt een nieuwe Visual Studio-oplossing voor dit project maken of bestaande oplossing tooan toevoegen.

> [!NOTE]
> Als u de Azure resourcegroepproject Hallo onder Hallo Cloud knooppunt niet ziet, hebt u geen hello Azure SDK is geïnstalleerd. Starten van de Web Platform Installer ([nu installeren](http://www.microsoft.com/web/downloads/platform.aspx) als u nog niet gedaan hebt), en zoek naar 'Azure SDK voor .NET' en installeer Hallo-versie die compatibel is met uw versie van Visual Studio.
> 
> 

Nadat u de knop OK voor Hallo raakt, wordt Visual Studio u gevraagd tooselect Hallo Resource Manager-sjabloon die u wilt dat toocreate:

![Dialoogvenster van de Azure-sjabloon selecteren met de geselecteerde sjabloon voor Service Fabric-Cluster][2]

Selecteer Hallo Service Fabric-Cluster sjabloon en treffers Hallo OK knop opnieuw. Hallo-project en Hallo Resource Manager-sjabloon hebt nu gemaakt.

## <a name="prepare-hello-template-for-deployment"></a>Hallo-sjabloon voor de implementatie voorbereiden
Voordat het Hallo-sjabloon is geïmplementeerde toocreate Hallo cluster, moet u waarden opgeven voor de sjabloonparameters Hallo vereist. Deze parameterwaarden worden gelezen uit Hallo `ServiceFabricCluster.parameters.json` bestand, dat zich in Hallo bevindt `Templates` map van het resourcegroepproject Hallo. Hallo-bestand openen en geef Hallo volgende waarden:

| Parameternaam | Beschrijving |
| --- | --- |
| adminUserName |Hallo-naam van Hallo administrator-account voor Service Fabric-machines (knooppunten). |
| certificateThumbprint |Hallo vingerafdruk van certificaat Hallo Hallo cluster beveiligt. |
| sourceVaultResourceId |Hallo *resource-ID* van Hallo sleutelkluis waar Hallo-certificaat dat Hallo cluster beveiligt wordt opgeslagen. |
| certificateUrlValue |Hallo-URL van beveiligingscertificaat Hallo-cluster. |

Hallo Visual Studio Service Fabric Resource Manager-sjabloon maakt u een beveiligde cluster dat wordt beveiligd door een certificaat. Dit certificaat wordt geïdentificeerd door Hallo laatste drie sjabloonparameters (`certificateThumbprint`, `sourceVaultValue`, en `certificateUrlValue`), en deze moet bestaan in een **Azure Key Vault**. Zie voor meer informatie over hoe toocreate cluster beveiligingscertificaat hello, [scenario's voor beveiliging van Service Fabric-cluster](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) artikel.

## <a name="optional-change-hello-cluster-name"></a>Optioneel: Wijzig de naam van de cluster Hallo
Elke Service Fabric-cluster heeft een naam. Wanneer een Fabric-cluster is gemaakt in Azure, clusternaam (samen met hello Azure-regio) bepaalt Hallo Domain Name System (DNS)-naam voor Hallo-cluster. Bijvoorbeeld, als u uw cluster naam `myBigCluster`, en Hallo locatie (Azure-regio) van de resourcegroep Hallo die als host voor het nieuwe cluster Hallo fungeert VS-Oost, is Hallo DNS-naam van de cluster Hallo `myBigCluster.eastus.cloudapp.azure.com`.

Standaard Hallo clusternaam automatisch gegenereerd en door het koppelen van een willekeurig achtervoegsel tooa 'cluster' voorvoegsel uniek gemaakt. Dit maakt het heel eenvoudig toouse Hallo sjabloon als onderdeel van een **continue integratie** (CI) systeem. Als u wilt dat toouse een specifieke naam voor uw cluster, een zinvolle tooyou Hallo waarde Hallo `clusterName` variabele in Hallo Resource Manager-sjabloonbestand (`ServiceFabricCluster.json`) tooyour gekozen naam. Is het eerste Hallo-variabele gedefinieerd in dat bestand.

## <a name="optional-add-public-application-ports"></a>Optioneel: openbare toepassing poorten toevoegen
U kunt ook toochange Hallo openbare toepassing poorten voor Hallo cluster voordat u deze implementeert. Standaard wordt Hallo sjabloon geopend slechts twee openbare TCP-poorten (80 en 8081). Als u meer voor uw toepassingen moet, wijzigt u hello Azure Load Balancer-definitie in Hallo sjabloon. Hallo-definitie wordt opgeslagen in de belangrijkste sjabloonbestand hello (`ServiceFabricCluster.json`). Open dit bestand en zoek naar `loadBalancedAppPort`. Elke poort is gekoppeld aan de drie onderdelen:

1. Een sjabloonvariabele die Hallo TCP-poortwaarde voor Hallo-poort definieert:
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. Een *test* die definieert hoe vaak en hoe lang hello Azure load balancer toouse een specifieke Service Fabric-knooppunt voordat deze is mislukt via tooanother een probeert. Hallo-tests uitmaken deel van Hallo Load Balancer-resource. Hier volgt Hallo test definitie voor Hallo eerste toepassing standaardpoort:
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. Een *taakverdeling regel* die samen bindt Hallo poort en het Hallo-test, zodat taakverdeling over een set van clusterknooppunten voor Service Fabric:
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   Als Hallo-toepassingen dat u van plan toodeploy toohello cluster bent meer poorten moeten, kunt u ze kunt toevoegen door het maken van aanvullende test en regeldefinities load balancing. Voor meer informatie over het toowork met Azure Load Balancer via Resource Manager-sjablonen, Zie [maken van een interne load balancer met een sjabloon aan de slag](../load-balancer/load-balancer-get-started-ilb-arm-template.md).

## <a name="deploy-hello-template-by-using-visual-studio"></a>Hallo-sjabloon implementeren met Visual Studio
Nadat u hebt opgeslagen Hallo alle vereiste parameter-waarden in de`ServiceFabricCluster.param.dev.json` -bestand, u bent gereed toodeploy Hallo sjabloon en een Service Fabric-cluster maken. Hallo resourcegroepproject in Visual Studio Solution Explorer met de rechtermuisknop en kies **implementeren | Nieuwe implementatie...** . Indien nodig, Visual Studio Hallo ziet **tooResource groep implementeren** in het dialoogvenster waarin u wordt gevraagd tooauthenticate tooAzure:

![Dialoogvenster van de groep tooResource implementeren][3]

Hallo-dialoogvenster kunt u een bestaande resourcegroep voor Resource Manager voor het Hallo-cluster en geeft u een nieuwe optie toocreate Hallo kiezen. Normaal gesproken maakt zin toouse een afzonderlijke resourcegroep voor een Service Fabric-cluster.

Nadat u Hallo implementeren knop raakt, wordt Visual Studio u gevraagd tooconfirm Hallo sjabloonparameterwaarden. Treffers Hallo **opslaan** knop. Één parameter heeft geen een persistente waarde: Hallo beheerdersrechten accountwachtwoord voor Hallo-cluster. U moet tooprovide een waarde van het wachtwoord als Visual Studio wordt u gevraagd om een.

> [!NOTE]
> Visual Studio starten met Azure SDK 2.9, ondersteunt lezen wachtwoorden van **Azure Key Vault** tijdens de implementatie. U ziet dat Hallo in Hallo sjabloon parametersdialoogvenster `adminPassword` tekstvak parameter heeft een weinig 'sleutel'-pictogram op de juiste Hallo. Dit pictogram kunt u een bestaande sleutelkluis geheim tooselect als beheerderswachtwoord voor de cluster Hallo Hallo. Zorg ervoor dat toofirst Azure Resource Manager-toegang voor de sjabloonimplementatie in Hallo geavanceerde toegangsbeleid van de sleutelkluis. 
> 
> 

U kunt voortgang Hallo van Hallo-implementatieproces in Visual Studio-uitvoervenster Hallo. Zodra de sjabloonimplementatie Hallo is voltooid, is het nieuwe cluster gereed toouse!

> [!NOTE]
> Als PowerShell nooit gebruikte tooadminister Azure vanaf Hallo-machine die u nu gebruikt is, moet u toodo wat housekeeping.
> 
> 1. PowerShell-scripting door het uitvoeren van Hallo inschakelen [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) opdracht. 'Onbeperkte' beleid is voor ontwikkeling machines, doorgaans acceptabel.
> 2. Bepaal of tooallow diagnostische gegevens verzamelen van Azure PowerShell-opdrachten en voer [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) of [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) indien nodig. Hiermee worden onnodige prompts voorkomen tijdens de sjabloonimplementatie van de.
> 
> 

Als er fouten zijn, gaat u toohello [Azure-portal](https://portal.azure.com/) en open Hallo resourcegroep die u geïmplementeerd. Klik op **alle instellingen**, klikt u vervolgens op **implementaties** op de blade instellingen Hallo. Een mislukte implementatie van de resourcegroep blijven er gedetailleerde diagnostische informatie.

> [!NOTE]
> Service Fabric-clusters vereisen van een bepaald aantal knooppunten toobe toomaintain beschikbaar en het behouden van status - waarnaar wordt verwezen tooas 'onderhoud quorum'. Het is daarom niet veilig tooshut omlaag alle machines in de cluster Hallo Hallo tenzij u eerst hebt uitgevoerd een [volledige back-up van de staat](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over het instellen van Service Fabric-cluster met behulp van hello Azure-portal](service-fabric-cluster-creation-via-portal.md)
* [Meer informatie over hoe toomanage en implementeren van Service Fabric-toepassingen met Visual Studio](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
