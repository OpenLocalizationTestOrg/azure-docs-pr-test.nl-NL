---
title: aaaReplicate Hyper-V-machines met PowerShell en Azure Resource Manager | Microsoft Docs
description: Hallo replicatie van Hyper-V-machines tooAzure automatiseren met behulp van PowerShell en Azure Resource Manager van Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>On-premises Hyper-V virtuele machines en Azure repliceren met behulp van PowerShell en Azure Resource Manager
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Klassieke portal](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>Overzicht
Azure Site Recovery draagt bij aan tooyour zakelijke continuïteit en noodherstel strategie door replicatie, failovers en herstel van virtuele machines in een aantal implementatiescenario's te organiseren. Zie voor een volledige lijst van implementatiescenario's voor Hallo [Azure Site Recovery-overzicht](site-recovery-overview.md).

Azure PowerShell is een module die cmdlets toomanage Azure via Windows PowerShell biedt. Samenwerking met twee typen modules: Hallo module profiel Azure of hello Azure Resource Manager-module.

Site Recovery PowerShell-cmdlets beschikbaar met Azure PowerShell voor Azure Resource Manager helpen u bij het beveiligen en herstellen van uw servers in Azure.

Dit artikel wordt beschreven hoe Windows PowerShell, samen met Azure Resource Manager, toodeploy siteherstel tooconfigure toouse en server protection tooAzure stroomlijnen. Hallo-voorbeeld gebruikt in dit artikel ziet u hoe tooprotect, failover en virtuele machines op een Hyper-V-host-tooAzure herstellen met behulp van Azure PowerShell met Azure Resource Manager.

> [!NOTE]
> Hallo Site Recovery PowerShell-cmdlets op dit moment kunt u tooconfigure hello te volgen: één tooanother voor Virtual Machine Manager-site, een tooAzure Virtual Machine Manager-site en een tooAzure Hyper-V-site.
>
>

U hoeft niet toobe een PowerShell-deskundige toouse in dit artikel, maar hoeft u toounderstand Hallo basisconcepten, zoals modules, cmdlets en sessies. Zie [Aan de slag met Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx) voor meer informatie over Windows PowerShell.

U kunt ook meer informatie over [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).

> [!NOTE]
> Microsoft-partners die deel van Hallo Cloud Solution Provider (CSP) programma uitmaken kunnen configureren en beheren van de beveiliging van hun klanten servers tootheir klanten respectieve CSP abonnementen (tenant-abonnementen).
>
>

## <a name="before-you-start"></a>Voordat u begint
Zorg ervoor dat u deze vereisten hebt voldaan:

* Een [Microsoft Azure](https://azure.microsoft.com/) account. U kunt beginnen met een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). U kunt bovendien lezen over [prijzen van Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Azure PowerShell 1.0. Voor informatie over deze release en hoe tooinstall, Zie [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* Hallo [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) en [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules. Kunt u de nieuwste versies Hallo van deze modules krijgen via Hallo [PowerShell gallery](https://www.powershellgallery.com/)

Dit artikel wordt beschreven hoe toouse Azure Powershell met Azure Resource Manager tooconfigure en beveiliging van uw servers beheren. Hallo-voorbeeld gebruikt in dit artikel ziet u hoe een virtuele machine worden uitgevoerd op een Hyper-V-host tooAzure tooprotect. Hallo volgende vereisten zijn specifiek toothis voorbeeld. Verschillende scenario's voor Site Recovery, Raadpleeg voor een uitgebreidere set vereisten voor Hallo toohello documentatie die betrekking hebben toothat scenario.

* Een Hyper-V-host waarop Windows Server 2012 R2 of Microsoft Hyper-V Server 2012 R2 met een of meer virtuele machines.
* Hyper-V-servers verbonden toohello Internet, rechtstreeks of via een proxy.
* Hallo moet virtuele machines die u wilt dat tooprotect voldoen aan [vereisten voor virtuele Machine](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="step-1-sign-in-tooyour-azure-account"></a>Stap 1: Registreren in tooyour Azure-account
1. Open een PowerShell-console en voer deze opdracht toosign in tooyour Azure-account. Hallo-cmdlet wordt een webpagina waarop u om referenties voor uw account vraagt.

        Login-AzureRmAccount

    U kunt u ook referenties van uw account kan opnemen als een parameter toohello `Login-AzureRmAccount` cmdlet, met behulp van Hallo `-Credential` parameter.

    Als u CSP partner werken namens een tenant, opgeven Hallo klant als een tenant met de naam van de primaire domeincontroller tenantID of tenant.

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. Een account kan meerdere abonnementen hebben, dus moet u Hallo abonnement u toouse met Hallo-account wilt koppelen.

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. Controleer of uw abonnement geregistreerde toouse hello Azure providers voor Recovery Services- en Site Recovery met behulp van de volgende opdrachten Hallo:

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   In de uitvoer van deze opdrachten, als Hallo Hallo **RegistrationState** te is ingesteld,**geregistreerde**, kunt u doorgaan tooStep 2. Als dat niet het geval is, moet u ontbrekende provider Hallo registreren in uw abonnement.

   tooregister hello Azure-provider voor de Site Recovery en de Recovery Services, Hallo volgende opdrachten uitvoeren:

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   Controleer of Hallo providers is geregistreerd met behulp van de volgende opdrachten Hallo: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` en `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.

## <a name="step-2-set-up-hello-recovery-services-vault"></a>Stap 2: Hallo die Recovery Services-kluis instellen
1. Maak een Azure Resource Manager-resourcegroep waarin u zult Hallo-kluis maken, of gebruik een bestaande resourcegroep. U kunt een nieuwe resourcegroep maken met behulp van de volgende opdracht Hallo:

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    Indien Hallo $ResourceGroupName variabele Hallo-naam van de resourcegroep Hallo bevat gewenste toocreate en Hallo $Geo variabele bevat hello Azure regio in de resourcegroep van welke toocreate hello (bijvoorbeeld ' Brazilië-Zuid').

    U kunt een lijst met resourcegroepen in uw abonnement verkrijgen via Hallo `Get-AzureRmResourceGroup` cmdlet.
2. Maak een nieuwe Azure Recovery Services-kluis als volgt:

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    U kunt een lijst met bestaande kluizen ophalen met behulp van Hallo `Get-AzureRmRecoveryServicesVault` cmdlet.

> [!NOTE]
> Als u tooperform bewerkingen op de Site Recovery-kluizen gemaakt met de klassieke portal Hallo of hello Azure Service Management PowerShell-module wenst, kunt u een lijst met dergelijke kluizen ophalen met behulp van Hallo `Get-AzureRmSiteRecoveryVault` cmdlet. Maak een nieuwe Recovery Services-kluis voor alle nieuwe activiteiten. Hallo Site Recovery kluizen die u eerder hebt gemaakt worden ondersteund, maar geen Hallo nieuwste functies.
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Stap 3: Stel Hallo Recovery Services-kluis context
1. Hallo kluis context door het uitvoeren van de volgende opdracht Hallo instellen:

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>Stap 4: Een Hyper-V-site maken en een nieuwe kluisregistratiesleutel voor Hallo site genereren.
1. Maak een nieuwe Hyper-V-site als volgt:

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    Deze cmdlet wordt een siteherstel taak toocreate Hallo site gestart en retourneert een taakobject Site Recovery. Wachten op Hallo taak toocomplete en controleer of deze Hallo-taak is voltooid.

    U kunt Hallo-taakobject worden opgehaald en Hallo huidige status van taak hello, waardoor controleren met behulp van de cmdlet Get-AzureRmSiteRecoveryJob Hallo.
2. Genereren en download een registratiesleutel voor Hallo-site, als volgt:

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    Kopiëren Hallo gedownload sleutel toohello Hyper-V-host. U moet Hallo sleutel tooregister Hallo Hyper-V-host toohello site.

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>Stap 5: Hello Azure Site Recovery provider en de Azure Recovery Services-Agent installeren op uw Hyper-V-host
1. Hallo installatieprogramma downloaden voor de meest recente versie Hallo van Hallo-provider van de [Microsoft](https://aka.ms/downloaddra).
2. Voer Hallo installer op de Hyper-V-host en achter Hallo Hallo-installatie voortgezet toohello registratiestap.
3. Geef desgevraagd Hallo site registratiecode en voltooid de registratie van Hallo Hyper-V-host toohello site gedownload.
4. Controleren dat die Hallo Hyper-V-host is geregistreerd toohello site met behulp van de volgende opdracht Hallo:

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>Stap 6: Een replicatiebeleid maken en deze koppelen aan de beveiligingscontainer Hallo
1. Maak een beleid voor wachtwoordreplicatie als volgt:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    Selectievakje hello taak tooensure die Hallo replicatie beleid aanmaak slaagt geretourneerd.

   > [!IMPORTANT]
   > Hallo opgegeven opslagaccount moet zich in dezelfde Azure-regio als de Recovery Services-kluis Hallo en moet geo-replicatie is ingeschakeld.
   >
   > * Als Hallo opgegeven Recovery storage-account van het type Azure Storage (klassiek is), beveiligde failover Hallo machines herstellen Hallo machine tooAzure IaaS (klassiek).
   > * Als Hallo opgegeven Recovery storage-account is van het type Azure Storage (Azure Resource Manager), beveiligde failover Hallo machines herstellen Hallo machine tooAzure IaaS (Azure Resource Manager).
   >
   >
2. Hallo beveiliging container bijbehorende toohello site, als volgt ophalen:

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. Start Hallo koppeling van de beveiligingscontainer Hallo met replicatiebeleid hello, als volgt:

     $Policy = get-AzureRmSiteRecoveryPolicy - FriendlyName $PolicyName $associationJob = Start AzureRmSiteRecoveryPolicyAssociationJob-beleid $Policy - PrimaryProtectionContainer $protectionContainer

   Wacht tot Hallo koppeling taak toocomplete en zorg ervoor dat het met succes voltooid.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Stap 7: Beveiliging voor virtuele machines inschakelen
1. Haal Hallo beveiliging entiteit bijbehorende toohello VM die u wilt dat tooprotect, als volgt:

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. Beginnen met het beveiligen van Hallo virtuele machine, als volgt:

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > Hallo opgegeven opslagaccount moet zich in dezelfde Azure-regio als de Recovery Services-kluis Hallo en moet geo-replicatie is ingeschakeld.
   >
   > * Als Hallo opgegeven Recovery storage-account van het type Azure Storage (klassiek is), beveiligde failover Hallo machines herstellen Hallo machine tooAzure IaaS (klassiek).
   > * Als Hallo opgegeven Recovery storage-account is van het type Azure Storage (Azure Resource Manager), beveiligde failover Hallo machines herstellen Hallo machine tooAzure IaaS (Azure Resource Manager).
   >
   > Als Hallo VM die u beveiligt meer dan één schijf gekoppelde tooit bevat, besturingssysteemschijf Hallo opgeven met behulp van Hallo *OSDiskName* parameter.
   >
   >
3. Wachten op Hallo virtuele machines tooreach een beveiligde status na de initiële replicatie Hallo. Dit kan duren, afhankelijk van factoren zoals de hoeveelheid gegevens toobe gerepliceerd Hallo en beschikbare bandbreedte van de upstream-tooAzure Hallo. Hallo taakstatus en StateDescription bijgewerkt als volgt bij Hallo VM een beveiligde status bereikt.

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. Herstel-eigenschappen, zoals Hallo grootte VM-rol en hello Azure-netwerk tooattach Hallo van network interface-kaarten tooupon failover van virtuele machine bijwerken.

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>Stap 8: Een testfailover uitvoeren
1. Een testtaak voor failover als volgt uitvoeren:

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Controleer of Hallo test die virtuele machine wordt gemaakt in Azure. (Hallo test failover-taak wordt onderbroken, na het maken van Hallo test virtuele machine in Azure. Hallo-taak is voltooid door het opruimen van artefacten Hallo gemaakt bij het Hallo-taak hervatten, zoals geïllustreerd in de volgende stap Hallo.)
3. Volledige Hallo failover, als volgt testen:

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>Volgende stappen
[Lees meer](https://msdn.microsoft.com/library/azure/mt637930.aspx) over Azure Site Recovery met Azure Resource Manager PowerShell-cmdlets.
