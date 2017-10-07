---
title: aaaAdd Azure automation-runbooks toorecovery plannen in de klassieke portal Hallo | Microsoft Docs
description: Dit artikel wordt beschreven hoe Azure Site Recovery kunt u nu tooextend herstelplannen met behulp van Azure Automation toocomplete complexe taken tijdens herstel tooAzure
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a>Azure automation-runbooks toorecovery plannen in de klassieke portal Hallo toevoegen
Deze zelfstudie wordt beschreven hoe Azure Site Recovery kan worden geïntegreerd met Azure Automation tooprovide uitbreidbaarheid toorecovery plannen. Plannen voor herstel kunnen herstel van uw virtuele machines die zijn beveiligd met Azure Site Recovery voor replicatie toosecondary cloud- en replicatie tooAzure scenario's te organiseren. Ze ook helpen bij het maken van Hallo herstel **accuraat**, **herhaalbare**, en **geautomatiseerde**. Als u via uw virtuele machines tooAzure mislukken, worden de integratie met Azure Automation breidt de herstelplannen en biedt u de mogelijkheid tooexecute runbooks, zodat krachtige automatiseringstaken.

Als u niet gehoord over Azure Automation nog, meldt u [hier](https://azure.microsoft.com/services/automation/) en hun voorbeeldscripts downloaden [hier](https://azure.microsoft.com/documentation/scripts/). Lees meer over [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) en hoe tooorchestrate herstel tooAzure met recovery plan [hier](https://azure.microsoft.com/blog/?p=166264).

In deze korte zelfstudie kijken we hoe u Azure Automation-runbooks in herstelplannen integreren kunt. We eenvoudige taken die eerder handmatige interventie vereist automatiseren en Zie hoe een multi-tooconvert herstel stap in een herstelactie met één klik. Ook kijken we hoe u een eenvoudig script oplossen kunt, als deze fout gaat.

## <a name="protect-hello-application-tooazure"></a>Hallo toepassing tooAzure beveiligen
Laten we beginnen met een eenvoudige toepassing die bestaat uit twee virtuele machines. Hier, hebben we een HRweb-toepassing van Fabrikam. Fabrikam-HRweb-front-end- en Fabrikam-Hrweb-back-end zijn Hallo twee virtuele machines beveiligd tooAzure met Azure Site Recovery. tooprotect hello virtuele machines met Azure Site Recovery stappen Hallo volgende.

1. Schakel de beveiliging voor uw virtuele machines.
2. Zorg ervoor dat Hallo virtuele machines eerste replicatie is voltooid en repliceert.
3. Wacht tot Hallo initiële replicatie is voltooid en Hallo replicatiestatus beveiligd zegt.

## ![](media/site-recovery-runbook-automation/01.png)
We gaan een herstelplan voor Hallo Fabrikam HRweb toepassing toofailover Hallo toepassing tooAzure maken in deze zelfstudie. We gaan deze vervolgens integreren met een runbook dat een eindpunt op Hallo failover van virtuele machine van Azure tooserve webpagina's op poort 80, wordt gemaakt.

Eerst gaan we een herstelplan voor onze toepassing maken.

## <a name="create-hello-recovery-plan"></a>Hallo herstelplan maken
toorecover hello toepassing tooAzure, moet u een herstelplan toocreate.
Met behulp van een herstelplan dat kunt u de volgorde Hallo van herstel van de virtuele machines. Hallo virtuele machine in de groep 1 geplaatst worden herstellen eerst worden gestart en vervolgens Hallo virtuele machine in de groep 2 opvolgt.

Maak een herstelplan dat op hieronder lijkt.

![](media/site-recovery-runbook-automation/12.png)

meer informatie over plannen voor herstel, documentatie te lezen tooread [hier](https://msdn.microsoft.com/library/azure/dn788799.aspx "hier").

Vervolgens maken we Hallo nodig artefacten in Azure Automation.

## <a name="create-hello-automation-account-and-its-assets"></a>Hallo automation-account en bijbehorende assets maken
U moet een Azure Automation-account toocreate-runbooks. Als u nog geen account, gaat u tooAzure Automation tabblad aangegeven met ![](media/site-recovery-runbook-automation/02.png)en maak een nieuwe account.

1. Hallo-account een naam tooidentify met geven.
2. Geef een geografische regio waar u tooplace Hallo-account.

Het verdient aanbeveling tooplace Hallo-account in Hallo dezelfde regio bevinden als Hallo ASR kluis.

![](media/site-recovery-runbook-automation/03.png)

Maak vervolgens Hallo activa in Hallo Account te volgen.

### <a name="add-a-subscription-name-as-asset"></a>De naam van een abonnement toevoegen als asset
1. Voeg een nieuwe instelling ![](media/site-recovery-runbook-automation/04.png) Hallo in Azure Automation activa en te selecteren![](media/site-recovery-runbook-automation/05.png)
2. Selecteer Hallo variabeletype als **tekenreeks**
3. Geef een naam op als **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. Geef de werkelijke naam van uw Azure-abonnement als Hallo variabelewaarde.

   ![](media/site-recovery-runbook-automation/07_1.png)

Hallo-naam van uw abonnement op de instellingenpagina Hallo van uw account op Hallo Azure-portal, kunt u identificeren.

### <a name="add-an-azure-login-credential-as-asset"></a>Toevoegen van een referentie voor de Azure-aanmelding als asset
Azure Automation maakt gebruik van Azure PowerShell tooconnect toothe abonnement en werkt met er Hallo-artefacten. Hiervoor moet u verifiëren met behulp van uw Microsoft-account of een werk- of schoolaccount.
U kunt Hallo accountreferenties opslaan in een asset toobe veilig door Hallo runbook gebruikt.

1. Voeg een nieuwe instelling ![](media/site-recovery-runbook-automation/04.png) hello Azure Automation activa in en selecteer![](media/site-recovery-runbook-automation/09.png)
2. Selecteer Hallo referentietype als **Windows PowerShell-referentie**
3. Geef de naam Hallo als **AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. Hallo-gebruikersnaam en wachtwoord toosign in met opgeven.

Beide deze instellingen zijn nu beschikbaar in uw assets.

![](media/site-recovery-runbook-automation/11.png)

Meer informatie over hoe tooconnect tooyour abonnement via PowerShell krijgt [hier](/powershell/azure/overview).

Vervolgens maakt u een runbook in Azure Automation die een eindpunt voor Hallo front-virtuele machine na een failover kunt toevoegen.

## <a name="azure-automation-context"></a>Azure automation-context
ASR geeft een context variabele toohello runbook toohelp u deterministische scripts schrijven. Een kan stellen Hallo namen van Hallo Cloudservice en Hallo virtuele Machine zijn voorspelbaar, maar er gebeurt dat is het niet altijd Hallo geval ten gevolge van toocertain scenario's zoals Hallo een waar Hallo-naam van de naam van de virtuele machine Hallo mogelijk gewijzigd vanwege toounsupported tekens in Azure. Deze informatie is daarom toohello ASR herstelplan doorgegeven als onderdeel van Hallo *context*.

Hieronder volgt een voorbeeld van hoe Hallo context variabele eruitziet.

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


Hallo in de volgende tabel bevat de naam en beschrijving voor iedere variabele in het Hallo-context.

| **Naam variabele** | **Beschrijving** |
| --- | --- |
| RecoveryPlanName |Naam van de planning wordt uitgevoerd. Helpt u maatregelen nemen op basis van de naam met behulp van dezelfde Hallo script |
| FailoverType |Hiermee geeft u op of Hallo failover is testen, gepland of ongepland. |
| FailoverDirection |Geef op of herstel tooprimary of secundaire site |
| Groeps-id |Hallo groepsnummer binnen Hallo herstelplan identificeren wanneer Hallo plan wordt uitgevoerd |
| VmMap |Matrix van alle Hallo virtuele machines in de groep Hallo |
| VMMap sleutel |Unieke sleutel (GUID) voor elke virtuele machine. Deze heeft Hallo hetzelfde zijn als de VMM-ID van de VM Hallo Hallo indien van toepassing. |
| Rolnaam |Naam van de virtuele machine van Azure die wordt hersteld Hallo |
| CloudServiceName |Azure Cloud Service-naam onder welke Hallo virtuele machine wordt gemaakt. |

tooidentify hello VmMap Key in de context van Hallo u kan ook toohello VM eigenschappenpagina in ASR en bekijkt hello VM GUID-eigenschap.

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>De auteur van een Automation-runbook
Hallo runbook tooopen poort 80 op Hallo front-virtuele machine nu gemaakt.

1. Een nieuw runbook maken in Azure Automation-account met de naam van de Hallo Hallo **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. Navigeer toohello weergave van Hallo runbook auteur en Hallo conceptmodus invoeren.
3. Geef eerst Hallo variabele toouse als Hallo recovery plan context

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. Toohello abonnement Hallo referentie en abonnement op met de volgende keer verbinding

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   Let erop dat u hello Azure gebruikt activa – **AzureCredential** en **AzureSubscriptionName** hier.
5. Nu Hallo endpoint details opgeven en Hallo GUID van Hallo virtuele machine waarvoor u tooexpose Hallo eindpunt wilt. Case Hallo front-virtuele machine.

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   Hiermee geeft u hello Azure-eindpunt protocol, lokale poort op Hallo VM en de bijbehorende toegewezen openbare poort. Deze variabelen zijn parameters vereist zijn voor hello Azure opdrachten die eindpunten tooVMs toevoegt. Hallo VMGUID bevat Hallo GUID van Hallo virtuele machine, moet u toooperate op.
6. Hallo script wordt nu Hallo context voor Hallo VM GUID opgegeven uitpakken en een eindpunt op Hallo virtuele machine waarnaar wordt verwezen door deze te maken.

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. Zodra dit voltooid is, klik op publiceren ![](media/site-recovery-runbook-automation/20.png) tooallow uw script toobe beschikbaar voor uitvoering.

Hallo volledige script hieronder voor referentiedoeleinden

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a>Hallo script toohello herstelplan toevoegen
Zodra Hallo script gereed is, kunt u deze toevoegen toohello herstelplan die u eerder hebt gemaakt.

1. In de Hallo herstelplan die u hebt gemaakt, kiest u tooadd een script achter de groep 2. ![](media/site-recovery-runbook-automation/15.png)
2. Geef de scriptnaam van een. Dit is slechts een beschrijvende naam voor dit script voor weergeven in het herstelplan Hallo.
3. Selecteer in de Hallo failover tooAzure script – hello Azure Automation-accountnaam.
4. Hallo Azure Runbooks, selecteer Hallo runbook die u geschreven.

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>Scripts op de primaire
Wanneer u een failover-tooAzure uitvoert, kunt u ook kiezen tooexecute scripts op de primaire. Deze scripts worden uitgevoerd op de VMM-server Hallo tijdens failover.
Scripts op de primaire zijn alleen beschikbaar voor vooraf afsluiten en boeken afsluiten fasen. Dit is omdat we Hallo primaire site toobe doorgaans niet beschikbaar verwachten wanneer een noodgeval biedt.
Tijdens een niet-geplande failover alleen als u-in voor bewerkingen van de primaire site opt, wordt geprobeerd toorun Hallo primaire kant scripts. Als ze zijn niet bereikbaar, of een time-out opgetreden, Hallo failover wordt voortgezet Hallo toorecover virtuele machines.
Scripts op de primaire zijn niet beschikbaar voor VMware/fysiek/Hyper-v-Sites zonder VMM beveiligd tooAzure - terwijl u failover tooAzure.
Echter, wanneer u failback vanuit Azure tooon-premises, scripts (Runbooks) op primaire kan worden gebruikt voor alle doelen behalve VMware.

## <a name="test-hello-recovery-plan"></a>Testplan Hallo herstel
Nadat u hebt toegevoegd Hallo runbook toohello plan kunt u een testfailover initiëren en in actie weergeven. Het is altijd aanbevolen toorun een test failover tootest uw toepassing en Hallo recovery plan tooensure er zijn geen fouten.

1. Selecteer Hallo herstelplan en start een testfailover.
2. Tijdens het uitvoeren van Hallo-abonnement ziet u of Hallo runbook is uitgevoerd of niet via de status ervan.

   ![](media/site-recovery-runbook-automation/17.png)
3. U ziet ook Hallo gedetailleerde status van de runbook-uitvoering op Hallo Azure Automation-taken pagina voor het Hallo-runbook.

   ![](media/site-recovery-runbook-automation/18.png)
4. Nadat Hallo failover is voltooid, wordt naast Hallo runbook resultaat van uitvoering, ziet u of het Hallo-uitvoering is voltooid of niet door de virtuele machine van Azure-pagina Hallo bezoeken en bekijkt hello eindpunten.

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>Voorbeeldscripts
Terwijl we doorlopen een vaak automatiseren taak van het toevoegen van een eindpunt tooan virtuele machine van Azure in deze zelfstudie gebruikt, kunt u een aantal andere krachtige automatiseringstaken met behulp van Azure automation doen. Microsoft en hello Azure Automation-community bieden voorbeeldrunbooks waarmee u kunt aan de slag maken van uw eigen oplossingen en hulpprogramma runbooks, die u kunt gebruiken als bouwstenen voor grotere automatiseringstaken. Aan de slag met ze uit de galerie Hallo en bouwen van krachtige één muisklik herstelplannen voor uw toepassingen met Azure Site Recovery.

## <a name="additional-resources"></a>Aanvullende resources
[Overzicht van Azure Automation](http://msdn.microsoft.com/library/azure/dn643629.aspx "overzicht van Azure Automation")

[Voorbeeld van Azure automatiseringsscripts](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "steekproef Azure automatiseringsscripts")
