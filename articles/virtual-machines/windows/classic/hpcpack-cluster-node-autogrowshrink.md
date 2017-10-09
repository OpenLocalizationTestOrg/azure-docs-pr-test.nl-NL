---
title: aaaAutoscale HPC Pack clusterknooppunten | Microsoft Docs
description: Automatisch vergroten of verkleinen Hallo aantal HPC Pack cluster-rekenknooppunten in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>Automatisch vergroten of verkleinen Hallo HPC Pack clusterbronnen in Azure op basis van toohello clusterbelasting
Als u Azure 'burst' knooppunten in het cluster HPC Pack implementeert, of u een cluster HPC Pack in Azure VM's maakt, kunt u een manier om automatisch vergroten of verkleinen Hallo clusterbronnen zoals knooppunten of kernen volgens Hallo werkbelasting op Hallo-cluster. Hallo-clusterbronnen schaling op deze manier kunt u toouse uw Azure-resources efficiënter en hun kosten te verifiëren.

Dit artikel ziet u twee manieren waarop HPC Pack tooautoscale rekenresources biedt:

* Hallo HPC Pack cluster eigenschap **AutoGrowShrink**

* Hallo **AzureAutoGrowShrink.ps1** HPC PowerShell-script

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Momenteel kunt u alleen automatisch vergroten of verkleinen van HPC Pack rekenknooppunten waarop een Windows-serverbesturingssysteem.


## <a name="set-hello-autogrowshrink-cluster-property"></a>Hallo AutoGrowShrink cluster eigenschap instellen
### <a name="prerequisites"></a>Vereisten

* **HPC Pack 2012 R2 Update 2 of hoger cluster** -hoofdknooppunt Hallo-cluster kan worden geïmplementeerd on-premises of in een Azure VM. Zie [een hybride-cluster met HPC Pack instellen](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget gestart met het hoofdknooppunt van een lokale en Azure 'burst' knooppunten. Zie Hallo [HPC Pack IaaS-implementatiescript](hpcpack-cluster-powershell-script.md) tooquickly een HPC Pack cluster in Azure VM's implementeren.

* **Voor een cluster met een hoofdknooppunt in Azure (Resource Manager-implementatiemodel)** - vanaf HPC Pack 2016, certificaatverificatie in een Azure Active Directory-toepassing wordt gebruikt voor het automatisch groeiende en comprimeren cluster virtuele machines geïmplementeerd met Azure Resource Manager. Een certificaat als volgt configureren:

  1. Na implementatie van het cluster, verbinding maken met extern bureaublad tooone hoofdknooppunt.

  2. Hallo-certificaat (PFX-indeling met persoonlijke sleutel) tooeach hoofdknooppunt uploaden en installeer tooCert:\LocalMachine\My en Cert: \LocalMachine\Root.

  3. Open Azure PowerShell als beheerder en Voer Hallo opdrachten op één hoofdknooppunt volgen:

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    Als uw account meer dan één Azure Active Directory-tenant of Azure-abonnement is, kunt u de volgende Hallo uitvoeren opdracht tooselect Hallo juiste tenant en -abonnement:
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    Na de opdracht tooview Hallo geselecteerde Hallo momenteel uitvoeren tenant en -abonnement:
    
    ```powershell
        Get-AzureRMContext
    ```

  4. Hallo na script uitvoeren

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    waar

    **DisplayName** -weergavenaam van de Azure Active-toepassing. Als de toepassing hello niet bestaat, wordt deze gemaakt in Azure Active Directory.

    **Startpagina** -startpagina Hallo van Hallo-toepassing. U kunt een dummy-URL, zoals in het voorgaande voorbeeld Hallo configureren.

    **IdentifierUri** -id van de toepassing hello. U kunt een dummy-URL, zoals in het voorgaande voorbeeld Hallo configureren.

    **CertificateThumbprint** -vingerafdruk van certificaat Hallo dat u op Hallo hoofdknooppunt in stap 1 hebt geïnstalleerd.

    **TenantId** -Tenant-ID van uw Azure Active Directory. U kunt Hallo Tenant-ID ophalen van hello Azure Active Directory-beheerportal **eigenschappen** pagina.

    Voor meer informatie over **ConfigARMAutoGrowShrinkCert.ps1**, voert `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.


* **Voor een cluster met een hoofdknooppunt in Azure (klassieke implementatiemodel)** : als u Hallo HPC Pack IaaS implementatie script toocreate Hallo-cluster in Hallo klassieke implementatiemodel inschakelen Hallo gebruiken **AutoGrowShrink** cluster de eigenschap door Hallo AutoGrowShrink optie in het configuratiebestand Hallo-cluster. Zie voor meer informatie, Hallo documentatie bij Hallo [script downloaden](https://www.microsoft.com/download/details.aspx?id=44949).

    U kunt ook inschakelen Hallo **AutoGrowShrink** cluster eigenschap nadat u Hallo-cluster implementeren met behulp van HPC PowerShell-opdrachten in Hallo volgende sectie beschreven. tooprepare voor deze eerste volledige Hallo volgende stappen:

  1. Een Azure-beheercertificaat configureren op het hoofdknooppunt hello en in hello Azure-abonnement. U kunt voor een testimplementatie Hallo standaard Microsoft HPC Azure zelf-ondertekend certificaat gebruiken dat HPC Pack wordt geïnstalleerd op het hoofdknooppunt Hallo en vervolgens uploaden dat certificaat tooyour Azure-abonnement. Zie voor opties en stappen Hallo [TechNet-bibliotheek richtlijnen](https://technet.microsoft.com/library/gg481759.aspx).

  2. Voer **regedit** op het hoofdknooppunt hello, gaat u tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo en voeg een string-waarde. Waardenaam hello te ingesteld 'Vingerafdruk' en waarde gegevens toohello vingerafdruk van certificaat Hallo in stap 1.

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>HPC PowerShell-opdrachten tooset hello AutoGrowShrink-eigenschap
Hieronder vindt u voorbeeld HPC PowerShell-opdrachten tooset **AutoGrowShrink** en tootune het gedrag met extra parameters. Zie [AutoGrowShrink parameters](#AutoGrowShrink-parameters) verderop in dit artikel voor Hallo volledige lijst met instellingen.

toorun deze opdrachten, HPC PowerShell Hallo hoofdknooppunt van cluster start als beheerder.

**tooenable hello AutoGrowShrink eigenschap**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**toodisable hello AutoGrowShrink eigenschap**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**toochange hello toenemen interval in minuten**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**Hallo toochange verkleinen interval in minuten**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**tooview hello huidige configuratie van AutoGrowShrink**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**tooexclude knooppuntgroepen van AutoGrowShrink**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> Deze parameter wordt ondersteund vanaf HPC Pack 2016
>

### <a name="autogrowshrink-parameters"></a>AutoGrowShrink parameters
Hallo volgen AutoGrowShrink parameters die u aanpassen kunt met behulp van Hallo **Set HpcClusterProperty** opdracht.

* **EnableGrowShrink** - tooenable Switch- of uitschakelen van Hallo **AutoGrowShrink** eigenschap.
* **ParamSweepTasksPerCore** -aantal parametrische taken toogrow één kern. Hallo standaardwaarde is één kern toogrow per taak.

  > [!NOTE]
  > HPC Pack QFE KB3134307 wijzigingen **ParamSweepTasksPerCore** te**TasksPerResourceUnit**. Dit is gebaseerd op Hallo taak brontype en kan dit knooppunt, socket of core.
  >
  >
* **GrowThreshold** -drempelwaarde van taken in de wachtrij tootrigger automatische groei. Hallo standaardwaarde is 1, wat dat betekent als er 1 of meer taken in Hallo in de wachtrij staat, worden automatisch vergroot knooppunten.
* **GrowInterval** -Interval in minuten tootrigger automatische groei. Hallo interval is standaard 5 minuten.
* **ShrinkInterval** -Interval in minuten tootrigger automatische verkleinen. Hallo-interval is standaard 5 minuten. |
* **ShrinkIdleTimes** -aantal continue controles tooshrink tooindicate Hallo knooppunten niet actief zijn. Hallo standaardinstelling is 3 maal. Bijvoorbeeld, als hello **ShrinkInterval** is 5 minuten, HPC Pack controleert of Hallo knooppunt niet actief is om de 5 minuten. Als Hallo knooppunten zich in niet-actieve status Hallo nadat 3 continue gecontroleerd (15 minuten), verkleint HPC Pack dat knooppunt.
* **ExtraNodesGrowRatio** -extra percentage van de knooppunten toogrow voor Message Passing Interface (MPI)-taken. Hallo-standaardwaarde is 1, wat betekent dat HPC Pack knooppunten 1% voor MPI-taken groeit.
* **GrowByMin** -tooindicate Switch of Hallo autogrow beleid is gebaseerd op Hallo minimale resources die vereist zijn voor Hallo-taak. Hallo standaardwaarde is ONWAAR, wat betekent dat HPC Pack knooppunten voor taken die zijn gebaseerd op Hallo maximale resources die vereist zijn voor Hallo taken groeit.
* **SoaJobGrowThreshold** -drempelwaarde van binnenkomende SOA-aanvragen tootrigger Hallo automatische proces groeien. de standaardwaarde Hallo is 50000.

  > [!NOTE]
  > Deze parameter wordt ondersteund vanaf HPC Pack 2012 R2 Update 3.
  >
  >
* **SoaRequestsPerCore** -het aantal inkomende SOA aanvragen toogrow één kern. de standaardwaarde Hallo is 20000.

  > [!NOTE]
  > Deze parameter wordt ondersteund vanaf HPC Pack 2012 R2 Update 3.
  >
* **ExcludeNodeGroups** – knooppunten in Hallo opgegeven knooppuntgroepen niet automatisch vergroten of verkleinen.
  
  > [!NOTE]
  > Deze parameter wordt ondersteund vanaf HPC Pack 2016.
  >

### <a name="mpi-example"></a>MPI-voorbeeld
Standaard HPC Pack 1% groeit extra knooppunten voor MPI-jobs (**ExtraNodesGrowRatio** too1 is ingesteld). Hallo reden is dat MPI kan meerdere knooppunten zijn vereist, en Hallo taak kan alleen worden uitgevoerd als alle knooppunten klaar bent. Wanneer Azure knooppunten is gestart, soms één knooppunt mogelijk meer tijd toostart dan andere andere knooppunten van niet-actieve tijdens het wachten op dat knooppunt tooget gereed toobe veroorzaakt. Extra knooppunten groeiende HPC Pack vermindert de wachttijd voor deze resource en bespaart u mogelijk kosten. percentage van de tooincrease Hallo van extra knooppunten voor MPI-taken (bijvoorbeeld too10%), een vergelijkbaar met opdracht uitvoeren

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>SOA-voorbeeld
Standaard **SoaJobGrowThreshold** too50000 is ingesteld en **SoaRequestsPerCore** too200000 is ingesteld. Als u één SOA-taak met 70000 aanvragen indient, er is een taak die in de wachtrij en inkomende aanvragen zijn 70000. In dit geval HPC Pack 1 core groeit voor Hallo taak in de wachtrij en (70000 50000) voor binnenkomende aanvragen groeit / 20000 = 1 core daarom in totaal 2 kernen voor deze taak SOA groeit.

## <a name="run-hello-azureautogrowshrinkps1-script"></a>Hallo AzureAutoGrowShrink.ps1 script uitvoeren
### <a name="prerequisites"></a>Vereisten

* **HPC Pack 2012 R2 Update 1 of hoger cluster** - hello **AzureAutoGrowShrink.ps1** script in Hallo % CCP_HOME % bin-map is geïnstalleerd. hoofdknooppunt Hallo-cluster kan worden geïmplementeerd on-premises of in een Azure VM. Zie [een hybride-cluster met HPC Pack instellen](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget gestart met het hoofdknooppunt van een lokale en Azure 'burst' knooppunten. Zie Hallo [HPC Pack IaaS-implementatiescript](hpcpack-cluster-powershell-script.md) tooquickly een HPC Pack cluster in Azure VM's implementeren of gebruik een [snelstartsjabloon met de Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).
* **Azure PowerShell 1.4.0** -Hallo script momenteel is afhankelijk van deze specifieke versie van Azure PowerShell.
* **Voor een cluster met Azure burst knooppunten** -Hallo-script uitvoeren op een clientcomputer waarop HPC Pack is geïnstalleerd of op Hallo hoofdknooppunt. Als dit wordt uitgevoerd op een clientcomputer, zorg ervoor dat u ingesteld Hallo variabele $env: CCP_SCHEDULER toopoint toohello hoofdknooppunt. Hello Azure 'burst' knooppunten toohello cluster moeten worden toegevoegd, maar kunnen ze zich in Hallo status niet geïmplementeerd.
* **Voor een cluster dat is geïmplementeerd in Azure Virtual machines (Resource Manager-implementatiemodel)** -voor een cluster van Azure VM's geïmplementeerd in de Resource Manager-implementatiemodel Hallo Hallo script ondersteunt twee methoden voor verificatie op Azure: aanmelden tooyour Azure-account toorun hello script telkens (door het uitvoeren van `Login-AzureRmAccount`, of een service-principal tooauthenticate configureren met een certificaat. HPC Pack Hallo script biedt **ConfigARMAutoGrowShrinkCert.ps** toocreate een service-principal met certificaat. Hallo script maakt een toepassing Azure Active Directory (Azure AD) en een service-principal en wijst Hallo Inzender rol toohello service-principal. toorun Hallo script, start u Azure PowerShell als administrator en Voer Hallo volgende opdrachten:

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    Voor meer informatie over **ConfigARMAutoGrowShrinkCert.ps1**, voert `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,

* **Voor een cluster dat is geïmplementeerd in Azure Virtual machines (klassieke implementatiemodel)** -Hallo-script uitvoeren op Hallo hoofdknooppunt VM, omdat deze afhankelijk Hallo **Start HpcIaaSNode.ps1** en **Stop-HpcIaaSNode.ps1**scripts die zijn geïnstalleerd. Deze scripts Bovendien vereisen een Azure-beheercertificaat of bestand publicatie-instellingen (Zie [rekenknooppunten beheren in een Pack HPC-cluster in Azure](hpcpack-cluster-node-manage.md)). Zorg ervoor dat alle Hallo compute knooppunt u moet virtuele machines toohello cluster al zijn toegevoegd. Ze mogelijk Hallo status gestopt.



### <a name="syntax"></a>Syntaxis
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>Parameters
* **NodeTemplates** -namen van Hallo knooppunt sjablonen toodefine Hallo bereik voor Hallo knooppunten toogrow en te verkleinen. Als niet wordt opgegeven (Hallo standaardwaarde is @()), alle knooppunten in Hallo **AzureNodes** knooppunt groep zijn wanneer het in bereik **NodeType** heeft een waarde van AzureNodes en alle knooppunten in Hallo **ComputeNodes** knooppunt groep zijn wanneer het in bereik **NodeType** een waarde heeft van ComputeNodes.
* **JobTemplates** -namen van Hallo sjablonen toodefine Hallo bereik voor Hallo knooppunten toogrow taak.
* **NodeType** - type knooppunt toogrow Hallo en verkleinen. Ondersteunde waarden zijn:

  * **AzureNodes** : voor Azure PaaS (burst) knooppunten in een on-premises of Azure IaaS-cluster.
  * **ComputeNodes** : voor het rekenknooppunt VM's alleen in een Azure IaaS-cluster.

* **NumOfQueuedJobsPerNodeToGrow** -aantal taken in de wachtrij is vereist toogrow één knooppunt.
* **NumOfQueuedJobsToGrowThreshold** -Hallo drempelwaarde voor aantal wachtrijtaken toostart Hallo proces groeien.
* **NumOfActiveQueuedTasksPerNodeToGrow** -Hallo aantal actieve taken in de wachtrij is vereist toogrow één knooppunt. Als **NumOfQueuedJobsPerNodeToGrow** wordt opgegeven met een waarde groter dan 0, worden deze parameter wordt genegeerd.
* **NumOfActiveQueuedTasksToGrowThreshold** -Hallo drempelwaarde voor aantal actieve taken in de wachtrij toostart Hallo proces groeien.
* **NumOfInitialNodesToGrow** - hello minimum aantal knooppunten toogrow initiële als alle Hallo knooppunten in het bereik zijn **niet geïmplementeerd** of **gestopt (Deallocated)**.
* **GrowCheckIntervalMins** -hello-interval in minuten tussen toogrow controleert.
* **ShrinkCheckIntervalMins** -hello-interval in minuten tussen tooshrink controleert.
* **ShrinkCheckIdleTimes** -Hallo continue verkleinen controles (gescheiden door **ShrinkCheckIntervalMins**) tooindicate Hallo knooppunten niet actief zijn.
* **UseLastConfigurations** -Hallo vorige configuraties in Hallo argument bestand opgeslagen.
* **ArgFile**- naam van Hallo argument bestand dat wordt gebruikt toosave Hallo en Hallo configuraties toorun Hallo updatescript.
* **LogFilePrefix** -naam van het voorvoegsel van het logboekbestand Hallo Hallo. U kunt een pad opgeven. Hallo-logboek is standaard de huidige werkmap toohello geschreven.

### <a name="example-1"></a>Voorbeeld 1
Hallo configureert volgende voorbeeld hello Azure burst knooppunten die zijn geïmplementeerd met de standaardsjabloon AzureNode toogrow en automatisch verkleinen. Als alle knooppunten in eerste instantie in Hallo **niet geïmplementeerd** staat, ten minste 3 knooppunten worden gestart. Als het aantal taken in de wachtrij Hallo groter is dan 8, Hallo script knooppunten begint, totdat hun aantal Hallo ratio van opdrachten in de wachtrij overschrijdt **NumOfQueuedJobsPerNodeToGrow**. Als een knooppunt toobe 3 opeenvolgende niet-actieve tijd inactief gevonden wordt, wordt het gestopt.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>Voorbeeld 2
Hallo configureert volgende voorbeeld hello Azure compute knooppunt virtuele machines die zijn geïmplementeerd met Hallo standaardsjabloon ComputeNode toogrow en automatisch verkleinen.
Hallo-taken die zijn geconfigureerd door de taak standaardsjabloon Hallo definiëren Hallo bereik van de werkbelasting op Hallo cluster. Als alle knooppunten van het Hallo in eerste instantie zijn gestopt, worden ten minste 5 knooppunten gestart. Als het aantal actieve taken in de wachtrij Hallo groter is dan 15, Hallo script knooppunten begint, totdat hun aantal Hallo ratio van actieve taken in de wachtrij te overschrijdt**NumOfActiveQueuedTasksPerNodeToGrow**. Als een knooppunt toobe 10 opeenvolgende niet-actieve tijd inactief gevonden wordt, wordt het gestopt.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
