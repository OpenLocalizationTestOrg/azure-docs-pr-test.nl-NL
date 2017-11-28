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
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="07394-104">Virtuele machines in Azure tooLog Analytics verbinden met een agent Log Analytics</span><span class="sxs-lookup"><span data-stu-id="07394-104">Connect Azure virtual machines tooLog Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="07394-105">Voor Windows en Linux-computers, Hallo aanbevolen methode voor het verzamelen van Logboeken en metrische gegevens is door het Hallo Log Analytics-agent installeren.</span><span class="sxs-lookup"><span data-stu-id="07394-105">For Windows and Linux computers, hello recommended method for collecting logs and metrics is by installing hello Log Analytics agent.</span></span>

<span data-ttu-id="07394-106">Hallo gemakkelijkste manier tooinstall Hallo Log Analytics-agent op virtuele machines in Azure is via Hallo Log Analytics VM-extensie.</span><span class="sxs-lookup"><span data-stu-id="07394-106">hello easiest way tooinstall hello Log Analytics agent on Azure virtual machines is through hello Log Analytics VM Extension.</span></span>  <span data-ttu-id="07394-107">Met de extensie Hallo vereenvoudigt het Hallo-installatieproces en configureert automatisch Hallo agent toosend gegevens toohello werkruimte voor logboekanalyse die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="07394-107">Using hello extension simplifies hello installation process and automatically configures hello agent toosend data toohello Log Analytics workspace that you specify.</span></span> <span data-ttu-id="07394-108">Hallo-agent is ook bijgewerkt automatisch, waarbij u ervoor zorgt dat u Hallo nieuwste functies en verbeteringen hebt.</span><span class="sxs-lookup"><span data-stu-id="07394-108">hello agent is also upgraded automatically, ensuring that you have hello latest features and fixes.</span></span>

<span data-ttu-id="07394-109">Voor virtuele machines van Windows die u inschakelen Hallo *Microsoft Monitoring Agent* extensie van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07394-109">For Windows virtual machines, you enable hello *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="07394-110">Voor virtuele Linux-machines, u Hallo inschakelen *OMS-Agent voor Linux* extensie van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07394-110">For Linux virtual machines, you enable hello *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="07394-111">Meer informatie over [virtuele machine van Azure-extensies](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en Hallo [Linux-agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="07394-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and hello [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="07394-112">Wanneer u de verzameling op basis van een agent voor logboekgegevens gebruikt, moet u configureren [gegevensbronnen in logboekanalyse](log-analytics-data-sources.md) toospecify Hallo logboeken en metrische gegevens die u toocollect wilt.</span><span class="sxs-lookup"><span data-stu-id="07394-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics that you want toocollect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07394-113">Als u de logboekgegevens van logboekanalyse tooindex met behulp van configureren [Azure diagnostics](log-analytics-azure-storage.md), en u Hallo agent toocollect Hallo dezelfde zich aanmeldt, configureren en vervolgens Hallo logboeken tweemaal worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="07394-113">If you configure Log Analytics tooindex log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure hello agent toocollect hello same logs, then hello logs are collected twice.</span></span> <span data-ttu-id="07394-114">Worden in rekening gebracht voor beide gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="07394-114">You are charged for both data sources.</span></span> <span data-ttu-id="07394-115">Als er Hallo-agent is geïnstalleerd, logboekgegevens verzamelen met behulp van alleen Hallo agent - logboekanalyse toocollect-logboekgegevens van Azure diagnostics niet configureren.</span><span class="sxs-lookup"><span data-stu-id="07394-115">If you have hello agent installed, then collect log data by using only hello agent - don't configure Log Analytics toocollect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="07394-116">Er zijn drie manieren extensie tooenable Hallo Log Analytics-virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="07394-116">There are three easy ways tooenable hello Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="07394-117">Met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="07394-117">By using hello Azure portal</span></span>
* <span data-ttu-id="07394-118">Met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="07394-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="07394-119">Met behulp van een Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="07394-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a><span data-ttu-id="07394-120">VM-extensie in de Azure-portal Hallo Hallo inschakelen</span><span class="sxs-lookup"><span data-stu-id="07394-120">Enable hello VM extension in hello Azure portal</span></span>
<span data-ttu-id="07394-121">U kunt installeren Hallo-agent voor logboekanalyse en verbinding maken met Azure virtuele machine die op wordt uitgevoerd met behulp van Hallo Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07394-121">You can install hello agent for Log Analytics and connect hello Azure virtual machine that it runs on by using hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a><span data-ttu-id="07394-122">tooinstall Hallo Log Analytics-agent en maak verbinding Hallo virtuele machine tooa-werkruimte voor logboekanalyse</span><span class="sxs-lookup"><span data-stu-id="07394-122">tooinstall hello Log Analytics agent and connect hello virtual machine tooa Log Analytics workspace</span></span>
1. <span data-ttu-id="07394-123">Meld u aan bij Hallo [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07394-123">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="07394-124">Selecteer **Bladeren** op Hallo linkerkant Hallo portal en ga vervolgens te**logboekanalyse (OMS)** en selecteer deze.</span><span class="sxs-lookup"><span data-stu-id="07394-124">Select **Browse** on hello left side of hello portal, and then go too**Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="07394-125">Selecteer in de lijst met Log Analytics-werkruimten Hallo een gewenste toouse Hello Azure VM.</span><span class="sxs-lookup"><span data-stu-id="07394-125">In your list of Log Analytics workspaces, select hello one that you want toouse with hello Azure VM.</span></span>  
   ![OMS werkruimten](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="07394-127">Onder **Meld analytics management**, selecteer **virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="07394-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="07394-128">![Virtuele machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="07394-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="07394-129">In de lijst met Hallo **virtuele machines**, selecteer Hallo virtuele machine waarop u wilt gebruiken voor tooinstall Hallo agent.</span><span class="sxs-lookup"><span data-stu-id="07394-129">In hello list of **Virtual machines**, select hello virtual machine on which you want tooinstall hello agent.</span></span> <span data-ttu-id="07394-130">Hallo **OMS verbindingsstatus** voor Hallo VM geeft aan dat deze is **niet verbonden**.</span><span class="sxs-lookup"><span data-stu-id="07394-130">hello **OMS connection status** for hello VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="07394-131">![Virtuele machine niet verbonden](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="07394-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="07394-132">Selecteer in het Hallo-details voor de virtuele machine, **Connect**.</span><span class="sxs-lookup"><span data-stu-id="07394-132">In hello details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="07394-133">Hallo-agent wordt automatisch geïnstalleerd en geconfigureerd voor uw werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="07394-133">hello agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="07394-134">Dit proces duurt een paar minuten, tijdens deze periode Hallo OMS verbindingsstatus is *verbinding maken...*</span><span class="sxs-lookup"><span data-stu-id="07394-134">This process takes a few minutes, during which time hello OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="07394-135">![Verbinding maken met virtuele machine](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="07394-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="07394-136">Na het installeren en verbinding maken met agent Hallo Hallo **OMS verbinding** status worden bijgewerkte tooshow **deze werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="07394-136">After you install and connect hello agent, hello **OMS connection** status will be updated tooshow **This workspace**.</span></span>  
   <span data-ttu-id="07394-137">![Verbonden](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="07394-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-hello-vm-extension-using-powershell"></a><span data-ttu-id="07394-138">Hallo VM-extensie met behulp van PowerShell inschakelen</span><span class="sxs-lookup"><span data-stu-id="07394-138">Enable hello VM extension using PowerShell</span></span>
<span data-ttu-id="07394-139">Wanneer u uw virtuele machine met behulp van PowerShell configureert, moet u tooprovide hello **workspaceId** en **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="07394-139">When you configure your virtual machine by using PowerShell, you need tooprovide hello **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="07394-140">Hallo-eigenschapsnamen in uw json-configuratie zijn **hoofdlettergevoelig**.</span><span class="sxs-lookup"><span data-stu-id="07394-140">hello property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="07394-141">U kunt zoeken Hallo Id en sleutel op Hallo **instellingen** van Hallo OMS-portal of met behulp van PowerShell, zoals wordt weergegeven in het voorgaande voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="07394-141">You can find hello Id and key on hello **Settings** page of hello OMS portal, or by using PowerShell as shown in hello preceding example.</span></span>

![Werkruimte-ID en de primaire sleutel](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="07394-143">Er zijn verschillende opdrachten voor virtuele machines van Azure classic en Resource Manager virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="07394-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="07394-144">Hieronder vindt u voorbeelden voor zowel klassieke als Resource Manager virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="07394-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="07394-145">Gebruik voor klassieke virtuele machines Hallo PowerShell-voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="07394-145">For classic virtual machines, use hello following PowerShell example:</span></span>

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

<span data-ttu-id="07394-146">Voor Resource Manager Linux VM's met behulp van de volgende CLI Hallo</span><span class="sxs-lookup"><span data-stu-id="07394-146">For Resource Manager Linux VMs using hello following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="07394-147">Gebruik voor Resource Manager virtuele machines, Hallo PowerShell-voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="07394-147">For Resource Manager virtual machines, use hello following PowerShell example:</span></span>

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


## <a name="deploy-hello-vm-extension-using-a-template"></a><span data-ttu-id="07394-148">Hallo VM-extensie met een sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="07394-148">Deploy hello VM extension using a template</span></span>
<span data-ttu-id="07394-149">Met behulp van Azure Resource Manager kunt u een sjabloon (in JSON-indeling) die Hallo-implementatie en configuratie van uw toepassing bepaalt.</span><span class="sxs-lookup"><span data-stu-id="07394-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines hello deployment and configuration of your application.</span></span> <span data-ttu-id="07394-150">Deze sjabloon wordt aangeduid als Resource Manager-sjabloon en biedt een declaratieve manier toodefine-implementatie.</span><span class="sxs-lookup"><span data-stu-id="07394-150">This template is known as a Resource Manager template and provides a declarative way toodefine deployment.</span></span> <span data-ttu-id="07394-151">U kunt herhaaldelijk implementeren van uw toepassing gedurende de levenscyclus van apps Hallo en erop vertrouwen dat uw resources worden geïmplementeerd in een consistente status, met behulp van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="07394-151">By using a template, you can repeatedly deploy your application throughout hello app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="07394-152">Door op te nemen Hallo logboekanalyse agent als onderdeel van de Resource Manager-sjabloon, kunt u ervoor zorgen dat elke virtuele machine vooraf geconfigureerd tooreport tooyour Log Analytics-werkruimte is.</span><span class="sxs-lookup"><span data-stu-id="07394-152">By including hello Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured tooreport tooyour Log Analytics workspace.</span></span>

<span data-ttu-id="07394-153">Zie voor meer informatie over de Resource Manager-sjablonen, [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="07394-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="07394-154">Hier volgt een voorbeeld van een Resource Manager-sjabloon die wordt gebruikt voor het implementeren van een virtuele machine met Windows Hello uitbreiding van Microsoft Monitoring Agent geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="07394-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with hello Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="07394-155">Deze sjabloon is een standaard virtuele-machinesjabloon Hello volgende toevoegingen:</span><span class="sxs-lookup"><span data-stu-id="07394-155">This template is a typical virtual machine template, with hello following additions:</span></span>

* <span data-ttu-id="07394-156">workspaceId en workspaceName parameters</span><span class="sxs-lookup"><span data-stu-id="07394-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="07394-157">Sectie Microsoft.EnterpriseCloud.Monitoring resource-uitbreiding</span><span class="sxs-lookup"><span data-stu-id="07394-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="07394-158">Uitvoer toolook hello workspaceId en workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="07394-158">Outputs toolook up hello workspaceId and workspaceSharedKey</span></span>

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

<span data-ttu-id="07394-159">U kunt een sjabloon implementeren met behulp van Hallo volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="07394-159">You can deploy a template by using hello following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a><span data-ttu-id="07394-160">Het oplossen van problemen Hallo Log Analytics VM-extensie</span><span class="sxs-lookup"><span data-stu-id="07394-160">Troubleshooting hello Log Analytics VM extension</span></span>
<span data-ttu-id="07394-161">U ontvangt meestal een bericht wanneer dingen niet, uit de Azure portal of Azure powershell werken.</span><span class="sxs-lookup"><span data-stu-id="07394-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="07394-162">Meld u aan bij Hallo [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07394-162">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="07394-163">Hallo VM zoeken en opent u de details van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07394-163">Find hello VM and open VM details.</span></span>
3. <span data-ttu-id="07394-164">Klik op **extensies** toocheck als OMS-extensie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="07394-164">Click **Extensions** toocheck if OMS extension is enabled or not.</span></span>

   ![VM-extensie weergeven](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="07394-166">Klik op Hallo *MicrosoftMonitoringAgent*(Windows) of *OmsAgentForLinux*(Linux)-uitbreiding en de weergave details.</span><span class="sxs-lookup"><span data-stu-id="07394-166">Click hello *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Details van de VM-extensie](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="07394-168">Het oplossen van virtuele Machines van Windows</span><span class="sxs-lookup"><span data-stu-id="07394-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="07394-169">Als hello *Microsoft Monitoring Agent* VM-agent-extensie is niet geïnstalleerd of rapportage, kunt u stappen tootroubleshoot Hallo na Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="07394-169">If hello *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="07394-170">Controleer of het hello Azure VM-agent is geïnstalleerd en werken goed met behulp van Hallo stappen in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="07394-170">Check if hello Azure VM agent is installed and working correctly by using hello steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="07394-171">U kunt ook Hallo VM-agent logboekbestand bekijken`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="07394-171">You can also review hello VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="07394-172">Als het Hallo-logboek niet bestaat, wordt Hallo VM-agent is niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="07394-172">If hello log does not exist, hello VM agent is not installed.</span></span>
     * [<span data-ttu-id="07394-173">Hello Azure VM-Agent installeren op klassieke virtuele machines</span><span class="sxs-lookup"><span data-stu-id="07394-173">Install hello Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="07394-174">Bevestig Hallo Microsoft Monitoring Agent-extensie heartbeat-taak wordt uitgevoerd met behulp van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="07394-174">Confirm hello Microsoft Monitoring Agent extension heartbeat task is running using hello following steps:</span></span>
   * <span data-ttu-id="07394-175">Meld u bij toohello virtuele machine</span><span class="sxs-lookup"><span data-stu-id="07394-175">Log in toohello virtual machine</span></span>
   * <span data-ttu-id="07394-176">Open Taakplanner en Hallo zoeken `update_azureoperationalinsight_agent_heartbeat` taak</span><span class="sxs-lookup"><span data-stu-id="07394-176">Open task scheduler and find hello `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="07394-177">Hallo-taak is ingeschakeld en wordt uitgevoerd elke één minuut bevestigen</span><span class="sxs-lookup"><span data-stu-id="07394-177">Confirm hello task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="07394-178">Hallo heartbeat logfile inchecken`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="07394-178">Check hello heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="07394-179">Raadpleeg Hallo Microsoft Monitoring Agent VM-extensie-logboekbestanden in`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="07394-179">Review hello Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="07394-180">Zorg ervoor dat Hallo virtuele machine kunt PowerShell-scripts uitvoeren</span><span class="sxs-lookup"><span data-stu-id="07394-180">Ensure hello virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="07394-181">Zorg ervoor dat de machtigingen op C:\Windows\temp nog niet zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="07394-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="07394-182">Hallo-status van Hallo Microsoft Monitoring Agent weergeven door te typen Hallo volgende opdracht in een PowerShell-venster met verhoogde bevoegdheid op Hallo virtuele machine`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="07394-182">View hello status of hello Microsoft Monitoring Agent by typing hello following command in an elevated PowerShell window on hello virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="07394-183">Raadpleeg Hallo Microsoft Monitoring Agent setup-logboekbestanden in`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="07394-183">Review hello Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="07394-184">Zie voor meer informatie [probleemoplossing van Windows-uitbreidingen](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="07394-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="07394-185">Het oplossen van virtuele Linux-Machines</span><span class="sxs-lookup"><span data-stu-id="07394-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="07394-186">Als hello *OMS-Agent voor Linux* VM-agent-extensie is niet geïnstalleerd of rapportage, kunt u stappen tootroubleshoot Hallo na Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="07394-186">If hello *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="07394-187">Als de status van de extensie Hallo *onbekende* Controleer of de hello Azure VM-agent is geïnstalleerd en correct werkt aan de hand van Hallo VM-agent-logboekbestand`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="07394-187">If hello extension status is *Unknown* check if hello Azure VM agent is installed and working correctly by reviewing hello VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="07394-188">Als het Hallo-logboek niet bestaat, wordt Hallo VM-agent is niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="07394-188">If hello log does not exist, hello VM agent is not installed.</span></span>
   * [<span data-ttu-id="07394-189">Hello Azure VM-Agent installeren op virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="07394-189">Install hello Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="07394-190">Voor andere slechte status controleren Hallo OMS-Agent voor Linux VM-extensie de logboekbestanden worden opgeslagen `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` en`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="07394-190">For other unhealthy statuses, review hello OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="07394-191">Als Hallo Extensiestatus in orde is, maar de gegevens niet worden er geüpload Hallo OMS-Agent te controleren voor Linux-logboekbestanden`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="07394-191">If hello extension status is healthy, but data is not being uploaded review hello OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="07394-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07394-192">Next steps</span></span>
* <span data-ttu-id="07394-193">Configureer [gegevensbronnen in logboekanalyse](log-analytics-data-sources.md) toospecify hello toocollect van Logboeken en metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="07394-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics toocollect.</span></span>
* <span data-ttu-id="07394-194">gegevens van virtuele machines toogather [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="07394-194">toogather data from virtual machines [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="07394-195">[Gegevens verzamelen met behulp van Azure Diagnostics](log-analytics-azure-storage.md) voor andere resources die worden uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="07394-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="07394-196">Voor computers die zich niet in Azure, kunt u Hallo Log Analytics-agent installeren met behulp van Hallo-methoden die worden beschreven in de volgende artikelen Hallo:</span><span class="sxs-lookup"><span data-stu-id="07394-196">For computers that are not in Azure, you can install hello Log Analytics agent by using hello methods that are described in hello following articles:</span></span>

* [<span data-ttu-id="07394-197">Verbinding maken met Windows-computers tooLog Analytics</span><span class="sxs-lookup"><span data-stu-id="07394-197">Connect Windows computers tooLog Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="07394-198">Linux-computers tooLog Analytics verbinden</span><span class="sxs-lookup"><span data-stu-id="07394-198">Connect Linux computers tooLog Analytics</span></span>](log-analytics-linux-agents.md)
