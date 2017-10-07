---
title: aaaAdd Azure Automation-runbooks toorecovery plannen in de Azure Site Recovery | Microsoft Docs
description: Meer informatie over hoe Azure Site Recovery kunt herstelplannen met behulp van Azure Automation uitbreiden. Meer informatie over hoe toocomplete complexe taken tijdens herstel tooAzure.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>Toevoegen van Azure Automation-runbooks toorecovery plannen
In dit artikel wordt beschreven hoe Azure Site Recovery kan worden geïntegreerd met Azure Automation toohelp uitbreiden van uw plannen voor herstel. Plannen voor herstel kunnen herstel van virtuele machines die zijn beveiligd met Site Recovery indelen. Plannen voor herstel werkt zowel voor replicatie tooa secundaire cloud, en voor replicatie tooAzure. Herstelplannen ook zorgt u ervoor dat Hallo herstel **accuraat**, **herhaalbare**, en **geautomatiseerde**. Als u uw virtuele machines tooAzure failover, uitgebreid integratie met Azure Automation uw plannen voor herstel. U kunt deze gebruiken tooexecute runbooks die krachtige automatiseringstaken bieden.

Als u nieuwe tooAzure Automation bent, kunt u [aanmelden](https://azure.microsoft.com/services/automation/) en [voorbeeldscripts downloaden](https://azure.microsoft.com/documentation/scripts/). Voor meer informatie en toolearn hoe tooorchestrate herstel tooAzure met behulp van [herstelplannen](https://azure.microsoft.com/blog/?p=166264), Zie [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).

In dit artikel wordt beschreven hoe u Azure Automation-runbooks kunt integreren in uw plannen voor herstel. We gebruiken voorbeelden tooautomate basistaken die voorheen handmatige interventie nodig. We beschrijven ook hoe tooconvert een herstel van meerdere stappen tooa één-op-herstelbewerking.

## <a name="customize-hello-recovery-plan"></a>Hallo herstelplan aanpassen
1. Ga toohello **siteherstel** recovery plan resource-blade. In dit voorbeeld heeft Hallo herstelplan twee virtuele machines toegevoegd tooit, voor herstel. toobegin toevoegen van een runbook, klikt u op Hallo **aanpassen** tabblad.

    ![Klik op de knop aanpassen Hallo](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. Met de rechtermuisknop op **groep 1: Start**, en selecteer vervolgens **post actie toevoegen**.

    ![Klik met de rechtermuisknop groep 1: Start en post actie toevoegen](media/site-recovery-runbook-automation-new/customize-rp.png)

3. Klik op **kiest u een script**.

4. Op Hallo **bijwerken actie** blade, naam Hallo script **Hallo wereld**.

    ![Hallo Update actie blade](media/site-recovery-runbook-automation-new/update-rp.png)

5. Voer de naam van een Automation-account.
    >[!NOTE]
    > Hallo Automation-account kan zich in een Azure-regio. Hallo Automation-account moet zich in Hallo hetzelfde abonnement als hello Azure Site Recovery-kluis.

6. Selecteer een runbook in uw Automation-account. Dit runbook is Hallo-script dat wordt uitgevoerd tijdens de uitvoering van de Hallo van het herstelplan hello, na het herstel van de eerste groep Hallo Hallo.

7. toosave hello script, klikt u op **OK**. Hallo-script wordt toegevoegd, te**groep 1: na stappen**.

    ![Groep na acties 1:Start](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>Overwegingen voor het toevoegen van een script

* Voor opties te**verwijderen van een stap** of **Hallo updatescript**, met de rechtermuisknop op het Hallo-script.
* Een script kunt uitvoeren in Azure tijdens de failover vanuit een lokale machine tooAzure. Deze kunt ook uitvoeren op Azure als een primaire site script voordat wordt afgesloten, tijdens de failback vanuit Azure tooan lokale machine.
* Wanneer een script wordt uitgevoerd, injects deze de context van een herstel plan. Hallo volgende voorbeeld ziet u een variabele context:

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    Hallo volgende tabel geeft een lijst Hallo naam en beschrijving van iedere variabele in het Hallo-context.

    | **Naam variabele** | **Beschrijving** |
    | --- | --- |
    | RecoveryPlanName |Hallo-naam van Hallo-planning wordt uitgevoerd. Deze variabele kunt u verschillende acties op basis van naam Hallo herstel uitvoeren. U kunt ook Hallo script hergebruiken. |
    | FailoverType |Hiermee geeft u op of Hallo failover een test is, gepland of ongepland. |
    | FailoverDirection |Geeft aan of herstel tooa primaire of secundaire site. |
    | Groeps-id |Identificeert in het herstelplan Hallo Hallo groepsnummer wanneer Hallo plan wordt uitgevoerd. |
    | VmMap |Een matrix met alle VM's in het Hallo-groep. |
    | VMMap sleutel |Een unieke sleutel (GUID) voor elke virtuele machine. De Hallo zelfde als ID van Azure Virtual Machine Manager (VMM) Hallo Hallo VM, indien van toepassing. |
    | SubscriptionId |Hello Azure-abonnement-ID in welke Hallo VM is gemaakt. |
    | Rolnaam |Hallo-naam van hello Azure virtuele machine die wordt hersteld. |
    | CloudServiceName |Hello Azure cloud servicenaam waaronder Hallo VM is gemaakt. |
    | resourceGroupName|Hello Azure Resourcegroepnaam waaronder Hallo VM is gemaakt. |
    | RecoveryPointId|Hallo tijdstempel voor wanneer Hallo VM is hersteld. |

* Zorg ervoor dat Hallo Automation-account heeft Hallo modules te volgen:
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

Alle modules moeten van compatibele versies. Een eenvoudige manier tooensure alle modules zijn compatibel is toouse Hallo nieuwste versies van alle Hallo-modules.

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>Toegang tot alle virtuele machines van Hallo VMMap in een lus
Hallo code tooloop volgen over alle VM's van Microsoft VMMap hello gebruiken:

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> Hallo resource groep en de rol naamwaarden zijn leeg als Hallo-script een groep van de opstartinstallatiekopie tooa vooraf in te grijpen is. Hallo-waarden worden ingevuld alleen als Hallo VM van die groep tijdens failover slaagt. Hallo-script is een na actie van Hallo opstarten groep.

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>Gebruik dezelfde Hallo Automation-runbook in meerdere herstelplannen

U kunt één script gebruiken in meerdere herstelplannen met behulp van externe variabelen. U kunt [Azure Automation-variabelen](../automation/automation-variables.md) toostore parameters die u voor een herstel doorgeven kunt uitvoeren plannen. U kunt afzonderlijke variabelen voor elke herstelplan maken door Hallo herstelnaam als een voorvoegsel toohello variabele toe te voegen. Gebruik vervolgens Hallo variabelen als parameters. U kunt een parameter wijzigen zonder het Hallo-script wijzigen, maar wijziging Hallo Hallo nog steeds manier werkt.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Een eenvoudige string-variabele in een runbookscript gebruiken

In dit voorbeeld wordt een script Hallo invoer van een Netwerkbeveiligingsgroep (NSG) en toegepast toohello VM's van een herstelplan.

Gebruik voor Hallo script toodetect welk herstelplan wordt uitgevoerd, Hallo recovery plan context:

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

een bestaande NSG tooapply, u moet weten Hallo NSG naam en het Hallo NSG Resourcegroepnaam. Deze variabelen gebruiken als invoer voor herstel plan scripts. toodo deze twee variabelen in Hallo activa van Automation-account maken. Hallo-naam van het herstelplan Hallo die u Hallo parameters voor als voorvoegsel toohello variabelenaam maakt toevoegen.

1. Maak een variabele toostore hello NSG-naam. Voorvoegsel toohello naam van een variabele toevoegen met behulp van de naam van het herstelplan Hallo Hallo.

    ![Maak een NSG naamvariabele](media/site-recovery-runbook-automation-new/var1.png)

2. Naam van een variabele toostore hello NSG een resourcegroep maken. Voorvoegsel toohello naam van een variabele toevoegen met behulp van de naam van het herstelplan Hallo Hallo.

    ![De groepsnaam van een NSG-resource maken](media/site-recovery-runbook-automation-new/var2.png)


3.  In Hallo-script gebruiken Hallo verwijzing code tooget Hallo waarden van variabelen te volgen:

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Gebruik Hallo variabelen in Hallo runbook tooapply hello NSG toohello netwerkinterface Hallo failover VM:

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

Voor elke herstelplan onafhankelijke variabelen te maken zodat u Hallo script opnieuw kunt gebruiken. Een voorvoegsel toevoegen met behulp van naam Hallo recovery-abonnement. Zie voor een script is voltooid, end-to-end voor dit scenario, [toevoegen van een openbare IP-adres en het NSG tooVMs tijdens de testfailover van een herstelplan Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).


### <a name="use-a-complex-variable-toostore-more-information"></a>Gebruik een complex variabele toostore meer informatie

Overweeg een scenario waarin u wilt dat een tooturn één script op een openbaar IP-adres op specifieke virtuele machines. In een ander scenario kunt u tooapply verschillende nsg's op verschillende virtuele machines (niet op alle VM's). U kunt een script dat opnieuw kan worden gebruikt voor een herstelplan maken. Elke herstelplan kan een variabele aantal VM's hebben. Een SharePoint-herstelbewerking heeft bijvoorbeeld twee front-ends. Een basic line-of-business (LOB)-toepassing heeft slechts één front-end. U kunt afzonderlijke variabelen voor elke herstelplan kan niet maken. 

In Hallo voorbeeld te volgen, wordt een nieuwe techniek gebruiken en maak een [complex variabele](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation-account activa. U doet dit door geven meerdere waarden. U moet Azure PowerShell toocomplete Hallo stappen te volgen:

1. Aanmelden tooyour Azure-abonnement in PowerShell:

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. Hallo complex variabele maken toostore Hallo-parameters, met behulp van de naam van het herstelplan Hallo Hallo:

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. In deze variabele complex **VMDetails** Hallo VM-ID is voor de Hallo beveiligd VM. tooget hello VM-ID in de Azure-portal Hallo Hallo VM-eigenschappen weergeven. Hallo volgende schermafbeelding ziet u een variabele die in details op Hallo van twee virtuele machines worden opgeslagen:

    ![Hallo VM-ID gebruiken zoals Hallo GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. Gebruik deze variabele in uw runbook. Als Hallo dat VM GUID is gevonden in de context van Hallo recovery plan aangegeven, van toepassing hello NSG op Hallo VM:

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. Doorlopen Hallo VM's van Hallo recovery plan context in uw runbook. Controleer of Hallo VM bestaat in **$VMDetailsObj**. Als dit bestaat, toegang tot de eigenschappen Hallo Hallo variabele tooapply Hallo NSG:

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

U kunt Hallo dezelfde script gebruiken voor andere herstelplannen. Geef andere parameters door op te slaan Hallo-waarde die overeenkomt met het herstelplan tooa in verschillende variabelen.

## <a name="sample-scripts"></a>Voorbeeldscripts

toodeploy voorbeeld scripts tooyour Automation-account, klikt u op Hallo **tooAzure implementeren** knop.

[![TooAzure implementeren](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

Zie voor een ander voorbeeld Hallo video te volgen. Dit laat zien hoe toorecover een tooAzure met twee lagen WordPress toepassing:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>Aanvullende bronnen
* [Azure Automation-service uitvoeren als-account](../automation/automation-sec-configure-azure-runas-account.md)
* [Overzicht van Azure Automation](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure Automation-overzicht")
* [Azure Automation-voorbeeldscripts](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure Automation-voorbeeldscripts")
