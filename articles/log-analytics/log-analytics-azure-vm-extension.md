---
title: aaaConnect virtuele Azure-machines tooLog Analytics | Microsoft Docs
description: Voor Windows en Linux virtuele machines worden uitgevoerd in Azure, Hallo aanbevolen manier van verzamelde logboeken en metrische gegevens is door het installeren van Hallo Log Analytics Azure VM-extensie. U kunt hello Azure-portal of PowerShell tooinstall Hallo logboekanalyse de extensie van de virtuele machine op Azure VM's gebruiken.
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>Virtuele machines in Azure tooLog Analytics verbinden met een agent Log Analytics

Voor Windows en Linux-computers, Hallo aanbevolen methode voor het verzamelen van Logboeken en metrische gegevens is door het Hallo Log Analytics-agent installeren.

Hallo gemakkelijkste manier tooinstall Hallo Log Analytics-agent op virtuele machines in Azure is via Hallo Log Analytics VM-extensie.  Met de extensie Hallo vereenvoudigt het Hallo-installatieproces en configureert automatisch Hallo agent toosend gegevens toohello werkruimte voor logboekanalyse die u opgeeft. Hallo-agent is ook bijgewerkt automatisch, waarbij u ervoor zorgt dat u Hallo nieuwste functies en verbeteringen hebt.

Voor virtuele machines van Windows die u inschakelen Hallo *Microsoft Monitoring Agent* extensie van virtuele machine.
Voor virtuele Linux-machines, u Hallo inschakelen *OMS-Agent voor Linux* extensie van virtuele machine.

Meer informatie over [virtuele machine van Azure-extensies](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en Hallo [Linux-agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Wanneer u de verzameling op basis van een agent voor logboekgegevens gebruikt, moet u configureren [gegevensbronnen in logboekanalyse](log-analytics-data-sources.md) toospecify Hallo logboeken en metrische gegevens die u toocollect wilt.

> [!IMPORTANT]
> Als u de logboekgegevens van logboekanalyse tooindex met behulp van configureren [Azure diagnostics](log-analytics-azure-storage.md), en u Hallo agent toocollect Hallo dezelfde zich aanmeldt, configureren en vervolgens Hallo logboeken tweemaal worden bijgehouden. Worden in rekening gebracht voor beide gegevensbronnen. Als er Hallo-agent is geïnstalleerd, logboekgegevens verzamelen met behulp van alleen Hallo agent - logboekanalyse toocollect-logboekgegevens van Azure diagnostics niet configureren.
>
>

Er zijn drie manieren extensie tooenable Hallo Log Analytics-virtuele machine:

* Met behulp van hello Azure-portal
* Met behulp van Azure PowerShell
* Met behulp van een Azure Resource Manager-sjabloon

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>VM-extensie in de Azure-portal Hallo Hallo inschakelen
U kunt installeren Hallo-agent voor logboekanalyse en verbinding maken met Azure virtuele machine die op wordt uitgevoerd met behulp van Hallo Hallo [Azure-portal](https://portal.azure.com).

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall Hallo Log Analytics-agent en maak verbinding Hallo virtuele machine tooa-werkruimte voor logboekanalyse
1. Meld u aan bij Hallo [Azure-portal](http://portal.azure.com).
2. Selecteer **Bladeren** op Hallo linkerkant Hallo portal en ga vervolgens te**logboekanalyse (OMS)** en selecteer deze.
3. Selecteer in de lijst met Log Analytics-werkruimten Hallo een gewenste toouse Hello Azure VM.  
   ![OMS werkruimten](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. Onder **Meld analytics management**, selecteer **virtuele machines**.  
   ![Virtuele machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. In de lijst met Hallo **virtuele machines**, selecteer Hallo virtuele machine waarop u wilt gebruiken voor tooinstall Hallo agent. Hallo **OMS verbindingsstatus** voor Hallo VM geeft aan dat deze is **niet verbonden**.  
   ![Virtuele machine niet verbonden](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. Selecteer in het Hallo-details voor de virtuele machine, **Connect**. Hallo-agent wordt automatisch geïnstalleerd en geconfigureerd voor uw werkruimte voor logboekanalyse. Dit proces duurt een paar minuten, tijdens deze periode Hallo OMS verbindingsstatus is *verbinding maken...*  
   ![Verbinding maken met virtuele machine](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. Na het installeren en verbinding maken met agent Hallo Hallo **OMS verbinding** status worden bijgewerkte tooshow **deze werkruimte**.  
   ![Verbonden](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>Hallo VM-extensie met behulp van PowerShell inschakelen
Wanneer u uw virtuele machine met behulp van PowerShell configureert, moet u tooprovide hello **workspaceId** en **workspaceKey**. Hallo-eigenschapsnamen in uw json-configuratie zijn **hoofdlettergevoelig**.

U kunt zoeken Hallo Id en sleutel op Hallo **instellingen** van Hallo OMS-portal of met behulp van PowerShell, zoals wordt weergegeven in het voorgaande voorbeeld Hallo.

![Werkruimte-ID en de primaire sleutel](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

Er zijn verschillende opdrachten voor virtuele machines van Azure classic en Resource Manager virtuele machines. Hieronder vindt u voorbeelden voor zowel klassieke als Resource Manager virtuele machines.

Gebruik voor klassieke virtuele machines Hallo PowerShell-voorbeeld te volgen:

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

Voor Resource Manager Linux VM's met behulp van de volgende CLI Hallo
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

Gebruik voor Resource Manager virtuele machines, Hallo PowerShell-voorbeeld te volgen:

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a>Hallo VM-extensie met een sjabloon implementeren
Met behulp van Azure Resource Manager kunt u een sjabloon (in JSON-indeling) die Hallo-implementatie en configuratie van uw toepassing bepaalt. Deze sjabloon wordt aangeduid als Resource Manager-sjabloon en biedt een declaratieve manier toodefine-implementatie. U kunt herhaaldelijk implementeren van uw toepassing gedurende de levenscyclus van apps Hallo en erop vertrouwen dat uw resources worden geïmplementeerd in een consistente status, met behulp van een sjabloon.

Door op te nemen Hallo logboekanalyse agent als onderdeel van de Resource Manager-sjabloon, kunt u ervoor zorgen dat elke virtuele machine vooraf geconfigureerd tooreport tooyour Log Analytics-werkruimte is.

Zie voor meer informatie over de Resource Manager-sjablonen, [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).

Hier volgt een voorbeeld van een Resource Manager-sjabloon die wordt gebruikt voor het implementeren van een virtuele machine met Windows Hello uitbreiding van Microsoft Monitoring Agent geïnstalleerd. Deze sjabloon is een standaard virtuele-machinesjabloon Hello volgende toevoegingen:

* workspaceId en workspaceName parameters
* Sectie Microsoft.EnterpriseCloud.Monitoring resource-uitbreiding
* Uitvoer toolook hello workspaceId en workspaceSharedKey

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

U kunt een sjabloon implementeren met behulp van Hallo volgende PowerShell-opdracht:

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>Het oplossen van problemen Hallo Log Analytics VM-extensie
U ontvangt meestal een bericht wanneer dingen niet, uit de Azure portal of Azure powershell werken.

1. Meld u aan bij Hallo [Azure-portal](http://portal.azure.com).
2. Hallo VM zoeken en opent u de details van de virtuele machine.
3. Klik op **extensies** toocheck als OMS-extensie is ingeschakeld.

   ![VM-extensie weergeven](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. Klik op Hallo *MicrosoftMonitoringAgent*(Windows) of *OmsAgentForLinux*(Linux)-uitbreiding en de weergave details. 

   ![Details van de VM-extensie](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>Het oplossen van virtuele Machines van Windows
Als hello *Microsoft Monitoring Agent* VM-agent-extensie is niet geïnstalleerd of rapportage, kunt u stappen tootroubleshoot Hallo na Hallo uitvoeren.

1. Controleer of het hello Azure VM-agent is geïnstalleerd en werken goed met behulp van Hallo stappen in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).
   * U kunt ook Hallo VM-agent logboekbestand bekijken`C:\WindowsAzure\logs\WaAppAgent.log`
   * Als het Hallo-logboek niet bestaat, wordt Hallo VM-agent is niet geïnstalleerd.
     * [Hello Azure VM-Agent installeren op klassieke virtuele machines](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. Bevestig Hallo Microsoft Monitoring Agent-extensie heartbeat-taak wordt uitgevoerd met behulp van Hallo stappen te volgen:
   * Meld u bij toohello virtuele machine
   * Open Taakplanner en Hallo zoeken `update_azureoperationalinsight_agent_heartbeat` taak
   * Hallo-taak is ingeschakeld en wordt uitgevoerd elke één minuut bevestigen
   * Hallo heartbeat logfile inchecken`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. Raadpleeg Hallo Microsoft Monitoring Agent VM-extensie-logboekbestanden in`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. Zorg ervoor dat Hallo virtuele machine kunt PowerShell-scripts uitvoeren
5. Zorg ervoor dat de machtigingen op C:\Windows\temp nog niet zijn gewijzigd.
6. Hallo-status van Hallo Microsoft Monitoring Agent weergeven door te typen Hallo volgende opdracht in een PowerShell-venster met verhoogde bevoegdheid op Hallo virtuele machine`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. Raadpleeg Hallo Microsoft Monitoring Agent setup-logboekbestanden in`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

Zie voor meer informatie [probleemoplossing van Windows-uitbreidingen](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="troubleshooting-linux-virtual-machines"></a>Het oplossen van virtuele Linux-Machines
Als hello *OMS-Agent voor Linux* VM-agent-extensie is niet geïnstalleerd of rapportage, kunt u stappen tootroubleshoot Hallo na Hallo uitvoeren.

1. Als de status van de extensie Hallo *onbekende* Controleer of de hello Azure VM-agent is geïnstalleerd en correct werkt aan de hand van Hallo VM-agent-logboekbestand`/var/log/waagent.log`
   * Als het Hallo-logboek niet bestaat, wordt Hallo VM-agent is niet geïnstalleerd.
   * [Hello Azure VM-Agent installeren op virtuele Linux-machines](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Voor andere slechte status controleren Hallo OMS-Agent voor Linux VM-extensie de logboekbestanden worden opgeslagen `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` en`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. Als Hallo Extensiestatus in orde is, maar de gegevens niet worden er geüpload Hallo OMS-Agent te controleren voor Linux-logboekbestanden`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>Volgende stappen
* Configureer [gegevensbronnen in logboekanalyse](log-analytics-data-sources.md) toospecify hello toocollect van Logboeken en metrische gegevens.
* gegevens van virtuele machines toogather [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).
* [Gegevens verzamelen met behulp van Azure Diagnostics](log-analytics-azure-storage.md) voor andere resources die worden uitgevoerd in Azure.

Voor computers die zich niet in Azure, kunt u Hallo Log Analytics-agent installeren met behulp van Hallo-methoden die worden beschreven in de volgende artikelen Hallo:

* [Verbinding maken met Windows-computers tooLog Analytics](log-analytics-windows-agents.md)
* [Linux-computers tooLog Analytics verbinden](log-analytics-linux-agents.md)
