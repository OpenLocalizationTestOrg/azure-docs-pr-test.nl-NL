---
title: aaaAzure virtuele-machineschaalsets Veelgestelde vragen | Microsoft Docs
description: Toofrequently van antwoorden op veelgestelde vragen over virtuele-machineschaalsets ophalen.
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="14a2d-103">Azure virtuele-machineschaalsets Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="14a2d-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="14a2d-104">Vind antwoorden op veelgestelde vragen over virtuele-machineschaalset toofrequently Hiermee stelt u in Azure.</span><span class="sxs-lookup"><span data-stu-id="14a2d-104">Get answers toofrequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="14a2d-105">Automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="14a2d-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="14a2d-106">Wat zijn de aanbevolen procedures voor het Azure-automatisch schalen?</span><span class="sxs-lookup"><span data-stu-id="14a2d-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="14a2d-107">Zie voor aanbevolen procedures voor automatisch schalen [aanbevolen procedures voor automatisch schalen virtuele machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="14a2d-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="14a2d-108">Waar vind ik metrische namen voor automatisch schalen die gebruikmaakt van de host gebaseerde metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="14a2d-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="14a2d-109">Zie voor namen van meetwaarde voor automatisch schalen die gebruikmaakt van de host gebaseerde metrische gegevens [ondersteund met een Azure-Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="14a2d-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="14a2d-110">Zijn er geen voorbeelden van automatisch schalen op basis van een Azure Service Bus-onderwerp en wachtrij-lengte?</span><span class="sxs-lookup"><span data-stu-id="14a2d-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="14a2d-111">Ja.</span><span class="sxs-lookup"><span data-stu-id="14a2d-111">Yes.</span></span> <span data-ttu-id="14a2d-112">Zie voor voorbeelden van automatisch schalen op basis van een Azure Service Bus-onderwerp en wachtrij-lengte [Azure Monitor automatisch schalen algemene metrische gegevens](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="14a2d-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="14a2d-113">Gebruik voor een Service Bus-wachtrij Hallo JSON te volgen:</span><span class="sxs-lookup"><span data-stu-id="14a2d-113">For a Service Bus queue, use hello following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="14a2d-114">Gebruik voor een opslagwachtrij Hallo JSON te volgen:</span><span class="sxs-lookup"><span data-stu-id="14a2d-114">For a storage queue, use hello following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="14a2d-115">Van de voorbeeldwaarden vervangt door uw resource Uniform Resource-id's (URI).</span><span class="sxs-lookup"><span data-stu-id="14a2d-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="14a2d-116">Moet ik automatisch schalen met behulp van metrische gegevens op de host of een extensie voor diagnostische gegevens?</span><span class="sxs-lookup"><span data-stu-id="14a2d-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="14a2d-117">Op een VM toouse hostniveau metrische gegevens of Gast OS gebaseerde metrische gegevens kunt u een instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-117">You can create an autoscale setting on a VM toouse host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="14a2d-118">Zie voor een lijst van ondersteunde metrische gegevens [Azure Monitor automatisch schalen algemene metrische gegevens](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="14a2d-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="14a2d-119">Zie voor een volledige voorbeeld voor virtuele-machineschaalsets [geavanceerde automatisch schalen configureren met behulp van Resource Manager-sjablonen voor virtuele-machineschaalsets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="14a2d-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="14a2d-120">Hallo-voorbeeld gebruikt Hallo hostniveau CPU metriek en een aantal bericht metriek.</span><span class="sxs-lookup"><span data-stu-id="14a2d-120">hello sample uses hello host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="14a2d-121">Hoe stel waarschuwingsregels op een virtuele-machineschaalset?</span><span class="sxs-lookup"><span data-stu-id="14a2d-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="14a2d-122">U kunt waarschuwingen maken op de metrische gegevens voor de virtuele-machineschaalsets via PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="14a2d-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="14a2d-123">Zie voor meer informatie [Azure Monitor PowerShell snel starten voorbeelden](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) en [Azure Monitor platformoverschrijdende CLI snel starten voorbeelden](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="14a2d-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="14a2d-124">Hallo TargetResourceId van Hallo virtuele-machineschaalset ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="14a2d-124">hello TargetResourceId of hello virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="14a2d-125">/Subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.COMPUTE/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="14a2d-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="14a2d-126">Kunt u een VM-prestatiemeteritem als Hallo metrische tooset een waarschuwing voor.</span><span class="sxs-lookup"><span data-stu-id="14a2d-126">You can choose any VM performance counter as hello metric tooset an alert for.</span></span> <span data-ttu-id="14a2d-127">Zie voor meer informatie [Gastbesturingssysteem metrische gegevens voor VM's van Windows Resource Manager gebaseerde](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) en [Gastbesturingssysteem metrische gegevens voor virtuele Linux-machines](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in Hallo [Azure Monitor automatisch schalen algemene metrische gegevens](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)artikel.</span><span class="sxs-lookup"><span data-stu-id="14a2d-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="14a2d-128">Hoe stel ik automatisch schalen op een virtuele-machineschaalset ingesteld met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="14a2d-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="14a2d-129">tooset up automatisch schalen op een virtuele-machineschaalset ingesteld met behulp van PowerShell, Zie Hallo blogbericht [hoe tooadd automatisch schalen tooan schaal van de virtuele machine van Azure instelt](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="14a2d-129">tooset up autoscale on a virtual machine scale set by using PowerShell, see hello blog post [How tooadd autoscale tooan Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="14a2d-130">Certificaten</span><span class="sxs-lookup"><span data-stu-id="14a2d-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a><span data-ttu-id="14a2d-131">Hoe ik een certificaat toohello VM veilig verzenden?</span><span class="sxs-lookup"><span data-stu-id="14a2d-131">How do I securely ship a certificate toohello VM?</span></span> <span data-ttu-id="14a2d-132">Hoe ik inrichten met een virtuele machine scale set toorun een website waar hello SSL voor Hallo website wordt verzonden veilig vanuit de configuratie van een certificaat?</span><span class="sxs-lookup"><span data-stu-id="14a2d-132">How do I provision a virtual machine scale set toorun a website where hello SSL for hello website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="14a2d-133">(Hallo algemene rotatie certificaatbewerking zou worden bijna Hallo hetzelfde als de bewerking configuratie bijwerken.) Hebt u een voorbeeld van hoe toodo dit?</span><span class="sxs-lookup"><span data-stu-id="14a2d-133">(hello common certificate rotation operation would be almost hello same as a configuration update operation.) Do you have an example of how toodo this?</span></span> 

<span data-ttu-id="14a2d-134">toosecurely een certificaat toohello VM verzenden, kunt u een klant-certificaat installeren rechtstreeks in een Windows-certificaatarchief van de sleutelkluis van de klant Hallo.</span><span class="sxs-lookup"><span data-stu-id="14a2d-134">toosecurely ship a certificate toohello VM, you can install a customer certificate directly into a Windows certificate store from hello customer's key vault.</span></span>

<span data-ttu-id="14a2d-135">Hallo JSON volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="14a2d-135">Use hello following JSON:</span></span>

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

<span data-ttu-id="14a2d-136">Hallo code biedt ondersteuning voor Windows en Linux.</span><span class="sxs-lookup"><span data-stu-id="14a2d-136">hello code supports Windows and Linux.</span></span>

<span data-ttu-id="14a2d-137">Zie voor meer informatie [maken of bijwerken een virtuele-machineschaalset](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="14a2d-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="14a2d-138">Voorbeeld van een zelfondertekend certificaat</span><span class="sxs-lookup"><span data-stu-id="14a2d-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="14a2d-139">Een zelfondertekend certificaat maken in een sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="14a2d-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="14a2d-140">Hallo volgende PowerShell-opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="14a2d-140">Use hello following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="14a2d-141">Deze opdracht kunt u Hallo invoer voor hello Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="14a2d-141">This command gives you hello input for hello Azure Resource Manager template.</span></span>

    <span data-ttu-id="14a2d-142">Voor een voorbeeld van hoe toocreate een zelfondertekend certificaat in een sleutelkluis zien [scenario's voor beveiliging van Service Fabric-cluster](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="14a2d-142">For an example of how toocreate a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="14a2d-143">Hallo Resource Manager-sjabloon wijzigen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-143">Change hello Resource Manager template.</span></span>

    <span data-ttu-id="14a2d-144">Deze eigenschap te toevoegen**virtualMachineProfile**, als onderdeel van Hallo stelt de virtuele-machineschaalset resource:</span><span class="sxs-lookup"><span data-stu-id="14a2d-144">Add this property too**virtualMachineProfile**, as part of hello virtual machine scale set resource:</span></span>

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="14a2d-145">Kan ik een SSH-sleutelpaar toouse voor SSH-verificatie opgeven met een Linux-virtuele machine schaal van Resource Manager-sjabloon instellen?</span><span class="sxs-lookup"><span data-stu-id="14a2d-145">Can I specify an SSH key pair toouse for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="14a2d-146">Ja.</span><span class="sxs-lookup"><span data-stu-id="14a2d-146">Yes.</span></span> <span data-ttu-id="14a2d-147">Hallo REST-API voor **osProfile** is vergelijkbaar toohello standard VM REST-API.</span><span class="sxs-lookup"><span data-stu-id="14a2d-147">hello REST API for **osProfile** is similar toohello standard VM REST API.</span></span> 

<span data-ttu-id="14a2d-148">Omvatten **osProfile** in uw sjabloon:</span><span class="sxs-lookup"><span data-stu-id="14a2d-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
<span data-ttu-id="14a2d-149">Dit blok JSON wordt gebruikt in [Hallo 101-vm-SSH-sleutelbestand GitHub snel starten sjabloon](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="14a2d-149">This JSON block is used in [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="14a2d-150">Hallo besturingssysteemprofiel wordt ook gebruikt bij [hello grelayhost.json GitHub quick start sjabloon](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="14a2d-150">hello OS profile also is used in [hello grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="14a2d-151">Zie voor meer informatie [maken of bijwerken een virtuele-machineschaalset](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="14a2d-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="14a2d-152">Hoe kan ik afgeschaft certificaten verwijderen?</span><span class="sxs-lookup"><span data-stu-id="14a2d-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="14a2d-153">tooremove afgeschaft verwijderen Hallo Oud certificaat van de lijst van certificaten kluis Hallo-certificaten.</span><span class="sxs-lookup"><span data-stu-id="14a2d-153">tooremove deprecated certificates, remove hello old certificate from hello vault certificates list.</span></span> <span data-ttu-id="14a2d-154">Alle Hallo certificaten dat u op uw computer in de lijst Hallo tooremain wilt laten.</span><span class="sxs-lookup"><span data-stu-id="14a2d-154">Leave all hello certificates that you want tooremain on your computer in hello list.</span></span> <span data-ttu-id="14a2d-155">Hallo-certificaat wordt niet verwijderd uit alle virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="14a2d-155">This does not remove hello certificate from all your VMs.</span></span> <span data-ttu-id="14a2d-156">Deze ook voegt geen Hallo certificaat toonew virtuele machines die zijn gemaakt in Hallo virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="14a2d-156">It also does not add hello certificate toonew VMs that are created in hello virtual machine scale set.</span></span> 

<span data-ttu-id="14a2d-157">tooremove hello certificaat van de bestaande virtuele machines, een aangepast script schrijven extensie toomanually verwijderen Hallo certificaten uit het certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="14a2d-157">tooremove hello certificate from existing VMs, write a custom script extension toomanually remove hello certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="14a2d-158">Hoe ik een bestaande openbare SSH-sleutel invoeren in Hallo virtuele machine scale set SSH-laag tijdens het inrichten?</span><span class="sxs-lookup"><span data-stu-id="14a2d-158">How do I inject an existing SSH public key into hello virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="14a2d-159">Ik toostore Hallo SSH openbare sleutelwaarden in Azure Sleutelkluis wilt en deze vervolgens in mijn Resource Manager-sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="14a2d-159">I want toostore hello SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="14a2d-160">Als u virtuele machines Hallo alleen met een openbare SSH-sleutel biedt, hoeft u geen tooput Hallo openbare sleutels in de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="14a2d-160">If you are providing hello VMs only with a public SSH key, you don't need tooput hello public keys in Key Vault.</span></span> <span data-ttu-id="14a2d-161">Openbare sleutels zijn niet geheim.</span><span class="sxs-lookup"><span data-stu-id="14a2d-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="14a2d-162">Wanneer u een Linux-VM maakt, kunt u openbare SSH-sleutels als tekst zonder opmaak bieden:</span><span class="sxs-lookup"><span data-stu-id="14a2d-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
<span data-ttu-id="14a2d-163">linuxConfiguration elementnaam</span><span class="sxs-lookup"><span data-stu-id="14a2d-163">linuxConfiguration element name</span></span> | <span data-ttu-id="14a2d-164">Vereist</span><span class="sxs-lookup"><span data-stu-id="14a2d-164">Required</span></span> | <span data-ttu-id="14a2d-165">Type</span><span class="sxs-lookup"><span data-stu-id="14a2d-165">Type</span></span> | <span data-ttu-id="14a2d-166">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="14a2d-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="14a2d-167">SSH</span><span class="sxs-lookup"><span data-stu-id="14a2d-167">ssh</span></span> | <span data-ttu-id="14a2d-168">Nee</span><span class="sxs-lookup"><span data-stu-id="14a2d-168">No</span></span> | <span data-ttu-id="14a2d-169">Verzameling</span><span class="sxs-lookup"><span data-stu-id="14a2d-169">Collection</span></span> | <span data-ttu-id="14a2d-170">Hiermee geeft u op Hallo SSH-sleutel configuratie voor een Linux-besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="14a2d-170">Specifies hello SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="14a2d-171">Pad</span><span class="sxs-lookup"><span data-stu-id="14a2d-171">path</span></span> | <span data-ttu-id="14a2d-172">Ja</span><span class="sxs-lookup"><span data-stu-id="14a2d-172">Yes</span></span> | <span data-ttu-id="14a2d-173">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="14a2d-173">String</span></span> | <span data-ttu-id="14a2d-174">Hiermee geeft u Hallo Linux-bestandspad waar Hallo SSH-sleutels of het certificaat moet zich bevinden</span><span class="sxs-lookup"><span data-stu-id="14a2d-174">Specifies hello Linux file path where hello SSH keys or certificate should be located</span></span>
<span data-ttu-id="14a2d-175">keyData</span><span class="sxs-lookup"><span data-stu-id="14a2d-175">keyData</span></span> | <span data-ttu-id="14a2d-176">Ja</span><span class="sxs-lookup"><span data-stu-id="14a2d-176">Yes</span></span> | <span data-ttu-id="14a2d-177">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="14a2d-177">String</span></span> | <span data-ttu-id="14a2d-178">Hiermee geeft u een base64-gecodeerd openbare SSH-sleutel</span><span class="sxs-lookup"><span data-stu-id="14a2d-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="14a2d-179">Zie voor een voorbeeld [Hallo 101-vm-SSH-sleutelbestand GitHub snel starten sjabloon](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="14a2d-179">For an example, see [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a><span data-ttu-id="14a2d-180">Wanneer ik uitvoeren `Update-AzureRmVmss` na het toevoegen van meer dan één certificaat uit Hallo sleutel kluis, zie ik Hallo volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="14a2d-180">When I run `Update-AzureRmVmss` after adding more than one certificate from hello same key vault, I see hello following message:</span></span>
 
><span data-ttu-id="14a2d-181">Update-AzureRmVmss: Lijst geheim bevat herhaalde exemplaren van /subscriptions/ < Mijn-abonnement-id > / resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev die niet is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="14a2d-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="14a2d-182">Dit kan gebeuren als u toore probeert-Hallo dezelfde kluis in plaats van een nieuw certificaat voor de kluis voor bestaande bronkluis Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-182">This can happen if you try toore-add hello same vault instead of using a new vault certificate for hello existing source vault.</span></span> <span data-ttu-id="14a2d-183">Hallo `Add-AzureRmVmssSecret` opdracht werkt niet goed als u extra geheimen toevoegt.</span><span class="sxs-lookup"><span data-stu-id="14a2d-183">hello `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="14a2d-184">tooadd meer geheimen van Hallo dezelfde sleutelkluis, update Hallo $vmss.properties.osProfile.secrets[0].vaultCertificates lijst.</span><span class="sxs-lookup"><span data-stu-id="14a2d-184">tooadd more secrets from hello same key vault, update hello $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="14a2d-185">Zie voor Hallo invoerstructuur verwacht, [maken of bijwerken wordt ingesteld door een virtuele machine](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="14a2d-185">For hello expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="14a2d-186">Hallo-geheim niet vinden in Hallo virtuele machine scale set object dat zich in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="14a2d-186">Find hello secret in hello virtual machine scale set object that is in hello key vault.</span></span> <span data-ttu-id="14a2d-187">Vervolgens voegt u uw verwijzing (Hallo-URL en de naam van de geheime store Hallo) toohello lijst met certificaten die zijn gekoppeld aan het Hallo-kluis.</span><span class="sxs-lookup"><span data-stu-id="14a2d-187">Then, add your certificate reference (hello URL and hello secret store name) toohello list associated with hello vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="14a2d-188">U verwijderen niet op dit moment certificaten uit de virtuele machines met behulp van Hallo virtuele machine scale set API.</span><span class="sxs-lookup"><span data-stu-id="14a2d-188">Currently, you cannot remove certificates from VMs by using hello virtual machine scale set API.</span></span>
>

<span data-ttu-id="14a2d-189">Nieuwe virtuele machines geen Hallo oude certificaat.</span><span class="sxs-lookup"><span data-stu-id="14a2d-189">New VMs will not have hello old certificate.</span></span> <span data-ttu-id="14a2d-190">Virtuele machines die Hallo certificaat hebben en die al zijn geïmplementeerd hebben echter Hallo oude certificaat.</span><span class="sxs-lookup"><span data-stu-id="14a2d-190">However, VMs that have hello certificate and which are already deployed will have hello old certificate.</span></span>
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a><span data-ttu-id="14a2d-191">Kan ik push certificaten toohello virtuele-machineschaalset instellen zonder Hallo-wachtwoord als Hallo certificaat in Hallo geheime store?</span><span class="sxs-lookup"><span data-stu-id="14a2d-191">Can I push certificates toohello virtual machine scale set without providing hello password, when hello certificate is in hello secret store?</span></span>

<span data-ttu-id="14a2d-192">U hoeft niet toohard code wachtwoorden in scripts.</span><span class="sxs-lookup"><span data-stu-id="14a2d-192">You do not need toohard-code passwords in scripts.</span></span> <span data-ttu-id="14a2d-193">U kunt dynamisch ophalen van wachtwoorden met Hallo machtigingen u toorun Hallo-implementatiescript gebruiken.</span><span class="sxs-lookup"><span data-stu-id="14a2d-193">You can dynamically retrieve passwords with hello permissions you use toorun hello deployment script.</span></span> <span data-ttu-id="14a2d-194">Als u een script dat een certificaat van Hallo geheime store sleutelkluis verplaatst hebt, Hallo geheime store `get certificate` opdracht levert ook wachtwoord op Hallo van Hallo pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="14a2d-194">If you have a script that moves a certificate from hello secret store key vault, hello secret store `get certificate` command also outputs hello password of hello .pfx file.</span></span>
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a><span data-ttu-id="14a2d-195">Hoe Hallo geheimen eigenschap van virtualMachineProfile.osProfile voor een virtuele-machineschaalset werk instellen?</span><span class="sxs-lookup"><span data-stu-id="14a2d-195">How does hello Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="14a2d-196">Waarom moet ik Hallo sourceVault waarde wanneer ik heb toospecify absolute URI voor een certificaat met behulp van Hallo certificateUrl eigenschap Hallo?</span><span class="sxs-lookup"><span data-stu-id="14a2d-196">Why do I need hello sourceVault value when I have toospecify hello absolute URI for a certificate by using hello certificateUrl property?</span></span> 

<span data-ttu-id="14a2d-197">Een verwijzing van Windows Remote Management (WinRM)-certificaat moet aanwezig zijn in Hallo geheimen-eigenschap van het Hallo-besturingssysteemprofiel.</span><span class="sxs-lookup"><span data-stu-id="14a2d-197">A Windows Remote Management (WinRM) certificate reference must be present in hello Secrets property of hello OS profile.</span></span> 

<span data-ttu-id="14a2d-198">Hallo doel Hallo bronkluis aangegeven is tooenforce toegangsbeheerlijst (ACL) toegangscontrolebeleid die aanwezig zijn in Azure Cloud Service-model van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="14a2d-198">hello purpose of indicating hello source vault is tooenforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="14a2d-199">Als Hallo bronkluis is niet opgegeven, worden gebruikers die u geen machtigingen voor toegang tot of toodeploy geheimen tooa sleutelkluis hebt kunnen toothrough Compute Resource Provider (CRP).</span><span class="sxs-lookup"><span data-stu-id="14a2d-199">If hello source vault isn't specified, users who do not have permissions toodeploy or access secrets tooa key vault would be able toothrough a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="14a2d-200">ACL's bestaan zelfs voor bronnen die niet bestaan.</span><span class="sxs-lookup"><span data-stu-id="14a2d-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="14a2d-201">Als u een onjuiste bron kluis-ID, maar een geldige sleutelkluis-URL opgeeft, wordt er een fout gerapporteerd bij het pollen van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="14a2d-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll hello operation.</span></span>
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="14a2d-202">Als ik geheimen tooan bestaande virtuele-machineschaalset toevoegt, worden geheimen Hallo ingevoegd in de bestaande virtuele machines, of alleen nieuwe?</span><span class="sxs-lookup"><span data-stu-id="14a2d-202">If I add secrets tooan existing virtual machine scale set, are hello secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="14a2d-203">Certificaten worden toegevoegd tooall uw virtuele machines, zelfs al bestaande elementen zijn.</span><span class="sxs-lookup"><span data-stu-id="14a2d-203">Certificates are added tooall your VMs, even preexisting ones.</span></span> <span data-ttu-id="14a2d-204">Als u uw virtuele-machineschaalset upgradePolicy eigenschap ingesteld te**handmatige**, Hallo certificaat toohello VM wordt toegevoegd wanneer u een handmatige update op Hallo VM uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="14a2d-204">If your virtual machine scale set upgradePolicy property is set too**manual**, hello certificate is added toohello VM when you perform a manual update on hello VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="14a2d-205">Waar ik certificaten plaatsen voor virtuele Linux-machines?</span><span class="sxs-lookup"><span data-stu-id="14a2d-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="14a2d-206">hoe toodeploy certificaten voor Linux VM's, Zie toolearn [tooVMs certificaten van een door de klant beheerd sleutelkluis implementeren](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="14a2d-206">toolearn how toodeploy certificates for Linux VMs, see [Deploy certificates tooVMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a><span data-ttu-id="14a2d-207">Hoe kan ik een nieuwe kluis certificaat tooa nieuw certificaatobject toevoegen</span><span class="sxs-lookup"><span data-stu-id="14a2d-207">How do I add a new vault certificate tooa new certificate object?</span></span>

<span data-ttu-id="14a2d-208">tooadd een kluis certificaat tooan bestaande geheim, Zie Hallo PowerShell-voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-208">tooadd a vault certificate tooan existing secret, see hello following PowerShell example.</span></span> <span data-ttu-id="14a2d-209">Gebruik slechts één geheime object.</span><span class="sxs-lookup"><span data-stu-id="14a2d-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a><span data-ttu-id="14a2d-210">Wat gebeurt er toocertificates als installatiekopie van een virtuele machine?</span><span class="sxs-lookup"><span data-stu-id="14a2d-210">What happens toocertificates if you reimage a VM?</span></span>

<span data-ttu-id="14a2d-211">Als u een virtuele machine installatiekopie, worden certificaten verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14a2d-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="14a2d-212">Verwijderingen Hallo gehele besturingssysteemschijf teruggezet.</span><span class="sxs-lookup"><span data-stu-id="14a2d-212">Reimaging deletes hello entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a><span data-ttu-id="14a2d-213">Wat gebeurt er als u een certificaat uit de sleutelkluis Hallo verwijderen?</span><span class="sxs-lookup"><span data-stu-id="14a2d-213">What happens if you delete a certificate from hello key vault?</span></span>

<span data-ttu-id="14a2d-214">Als Hallo geheim wordt verwijderd uit de sleutelkluis hello en u voert `stop deallocate` voor alle VM's en start deze opnieuw, wordt er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="14a2d-214">If hello secret is deleted from hello key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="14a2d-215">Hallo-fout treedt op omdat Hallo CRP tooretrieve Hallo geheimen van de sleutelkluis hello heeft, maar niet kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="14a2d-215">hello failure occurs because hello CRP needs tooretrieve hello secrets from hello key vault, but it cannot.</span></span> <span data-ttu-id="14a2d-216">In dit scenario kunt u certificaten Hallo verwijderen uit Hallo virtuele machine scale set model.</span><span class="sxs-lookup"><span data-stu-id="14a2d-216">In this scenario, you can delete hello certificates from hello virtual machine scale set model.</span></span> 

<span data-ttu-id="14a2d-217">Hallo CRP onderdeel geheimen van de klant niet bewaard is gebleven.</span><span class="sxs-lookup"><span data-stu-id="14a2d-217">hello CRP component does not persist customer secrets.</span></span> <span data-ttu-id="14a2d-218">Als u `stop deallocate` voor alle virtuele machines in Hallo virtuele-machineschaalset, Hallo-cache wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14a2d-218">If you run `stop deallocate` for all VMs in hello virtual machine scale set, hello cache is deleted.</span></span> <span data-ttu-id="14a2d-219">In dit scenario worden geheimen opgehaald uit de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="14a2d-219">In this scenario, secrets are retrieved from hello key vault.</span></span>

<span data-ttu-id="14a2d-220">U kunt dit probleem niet tegenkomen wanneer uitbreiden, omdat er een cachekopie van Hallo geheim in Azure Service Fabric (in Hallo één fabric tenant model).</span><span class="sxs-lookup"><span data-stu-id="14a2d-220">You don't encounter this problem when scaling out because there is a cached copy of hello secret in Azure Service Fabric (in hello single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="14a2d-221">Waarom hebt toospecify Hallo exacte locatie voor Hallo certificaat-URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), zoals aangegeven in [scenario's voor beveiliging van Service Fabric-cluster](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="14a2d-221">Why do I have toospecify hello exact location for hello certificate URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="14a2d-222">Hello Azure Key Vault documentatie wordt aangegeven dat Hallo die geheim REST-API ophalen Hallo meest recente versie van Hallo geheim retourneren moet als Hallo-versie is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="14a2d-222">hello Azure Key Vault documentation states that hello Get Secret REST API should return hello latest version of hello secret if hello version is not specified.</span></span>
 
<span data-ttu-id="14a2d-223">Methode</span><span class="sxs-lookup"><span data-stu-id="14a2d-223">Method</span></span> | <span data-ttu-id="14a2d-224">URL</span><span class="sxs-lookup"><span data-stu-id="14a2d-224">URL</span></span>
--- | ---
<span data-ttu-id="14a2d-225">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="14a2d-225">GET</span></span> | <span data-ttu-id="14a2d-226">https://mykeyvault.Vault.Azure.NET/secrets/ {geheim name} / {geheim versie}? api-version = {api-versie}</span><span class="sxs-lookup"><span data-stu-id="14a2d-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="14a2d-227">Vervang {*geheim naam*} met de naam van de Hallo en vervangen {*geheim versie*} met Hallo-versie van Hallo geheim gewenste tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="14a2d-227">Replace {*secret-name*} with hello name, and replace {*secret-version*} with hello version of hello secret you want tooretrieve.</span></span> <span data-ttu-id="14a2d-228">Hallo geheime versie kan worden uitgesloten.</span><span class="sxs-lookup"><span data-stu-id="14a2d-228">hello secret version might be excluded.</span></span> <span data-ttu-id="14a2d-229">In dat geval wordt wordt de huidige versie hello opgehaald.</span><span class="sxs-lookup"><span data-stu-id="14a2d-229">In that case, hello current version is retrieved.</span></span>
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="14a2d-230">Waarom heb ik toospecify Hallo certificaatversie bij het gebruik van Sleutelkluis?</span><span class="sxs-lookup"><span data-stu-id="14a2d-230">Why do I have toospecify hello certificate version when I use Key Vault?</span></span>

<span data-ttu-id="14a2d-231">Hallo-doel van Hallo Sleutelkluis vereiste toospecify Hallo certificaatversie is toomake het toohello gebruiker wissen welk certificaat wordt geïmplementeerd op hun virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="14a2d-231">hello purpose of hello Key Vault requirement toospecify hello certificate version is toomake it clear toohello user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="14a2d-232">Als u een virtuele machine maken en werk vervolgens het geheim in de sleutelkluis hello, wordt Hallo nieuwe certificaat is niet gedownload tooyour virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="14a2d-232">If you create a VM and then update your secret in hello key vault, hello new certificate is not downloaded tooyour VMs.</span></span> <span data-ttu-id="14a2d-233">Maar uw virtuele machines worden weergegeven en nieuwe virtuele machines ophalen van het nieuwe geheim Hallo tooreference.</span><span class="sxs-lookup"><span data-stu-id="14a2d-233">But your VMs appear tooreference it, and new VMs get hello new secret.</span></span> <span data-ttu-id="14a2d-234">tooavoid, bent u vereiste tooreference een geheime versie.</span><span class="sxs-lookup"><span data-stu-id="14a2d-234">tooavoid this, you are required tooreference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a><span data-ttu-id="14a2d-235">Mijn team werkt met verschillende certificaten die worden gedistribueerd toous als cer openbare sleutels.</span><span class="sxs-lookup"><span data-stu-id="14a2d-235">My team works with several certificates that are distributed toous as .cer public keys.</span></span> <span data-ttu-id="14a2d-236">Wat is de aanbevolen aanpak voor het implementeren van deze certificaten tooa virtuele-machineschaalset Hallo?</span><span class="sxs-lookup"><span data-stu-id="14a2d-236">What is hello recommended approach for deploying these certificates tooa virtual machine scale set?</span></span>

<span data-ttu-id="14a2d-237">toodeploy .cer openbare sleutels tooa virtuele-machineschaalset, kunt u een .pfx-bestand met CER-bestanden genereren.</span><span class="sxs-lookup"><span data-stu-id="14a2d-237">toodeploy .cer public keys tooa virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="14a2d-238">toodo dit, gebruik `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="14a2d-238">toodo this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="14a2d-239">Bijvoorbeeld Hallo cer-bestand laden als een object x509Certificate2 in C# of PowerShell en vervolgens Hallo-methode aanroepen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-239">For example, load hello .cer file as an x509Certificate2 object in C# or PowerShell, and then call hello method.</span></span> 

<span data-ttu-id="14a2d-240">Zie voor meer informatie [X509Certificate.Export methode (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="14a2d-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="14a2d-241">Ik zie een optie om gebruikers toopass in certificaten niet als base64-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-241">I do not see an option for users toopass in certificates as base64 strings.</span></span> <span data-ttu-id="14a2d-242">De meeste andere resourceproviders hebt deze optie.</span><span class="sxs-lookup"><span data-stu-id="14a2d-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="14a2d-243">tooemulate doorgeven in een certificaat als een base64-tekenreeks kan u Hallo laatste samengestelde URL in het Resource Manager-sjabloon extraheren.</span><span class="sxs-lookup"><span data-stu-id="14a2d-243">tooemulate passing in a certificate as a base64 string, you can extract hello latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="14a2d-244">Hallo JSON-eigenschap in de Resource Manager-sjabloon volgende omvatten:</span><span class="sxs-lookup"><span data-stu-id="14a2d-244">Include hello following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="14a2d-245">Heb ik toowrap certificaten in JSON-objecten in sleutelkluizen?</span><span class="sxs-lookup"><span data-stu-id="14a2d-245">Do I have toowrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="14a2d-246">In de virtuele-machineschaalsets en virtuele machines moeten certificaten worden verpakt in JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="14a2d-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="14a2d-247">We bieden ook ondersteuning Hallo inhoudstype application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="14a2d-247">We also support hello content type application/x-pkcs12.</span></span> <span data-ttu-id="14a2d-248">Zie voor instructies over het gebruik van de x-toepassing-pkcs12 [PFX-certificaten in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="14a2d-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="14a2d-249">We ondersteunen momenteel geen cer-bestanden.</span><span class="sxs-lookup"><span data-stu-id="14a2d-249">We currently do not support .cer files.</span></span> <span data-ttu-id="14a2d-250">toouse .cer-bestanden, exporteert u ze in pfx-containers.</span><span class="sxs-lookup"><span data-stu-id="14a2d-250">toouse .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="14a2d-251">Naleving</span><span class="sxs-lookup"><span data-stu-id="14a2d-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="14a2d-252">Zijn de virtuele-machineschaalsets PCI-compatibel?</span><span class="sxs-lookup"><span data-stu-id="14a2d-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="14a2d-253">Virtuele-machineschaalsets zijn een thin API-laag bovenop Hallo CRP.</span><span class="sxs-lookup"><span data-stu-id="14a2d-253">Virtual machine scale sets are a thin API layer on top of hello CRP.</span></span> <span data-ttu-id="14a2d-254">Beide onderdelen maken deel uit van Hallo compute-platform in hello Azure service-structuur.</span><span class="sxs-lookup"><span data-stu-id="14a2d-254">Both components are part of hello compute platform in hello Azure service tree.</span></span>

<span data-ttu-id="14a2d-255">Virtuele-machineschaalsets zijn vanuit het oogpunt van naleving van een fundamenteel onderdeel van hello Azure compute-platform.</span><span class="sxs-lookup"><span data-stu-id="14a2d-255">From a compliance perspective, virtual machine scale sets are a fundamental part of hello Azure compute platform.</span></span> <span data-ttu-id="14a2d-256">Ze delen een team, hulpprogramma's, processen, implementatiemethode, beveiligingsmechanismen, just in time (Just in time) compilatie, bewaking, waarschuwingen, enzovoort, met Hallo CRP zelf.</span><span class="sxs-lookup"><span data-stu-id="14a2d-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with hello CRP itself.</span></span> <span data-ttu-id="14a2d-257">Virtuele-machineschaalsets zijn Payment Card Industry (PCI)-compatibele omdat Hallo CRP deel uitmaakt van het huidige PCI Data Security Standard (DSS) attestation Hallo.</span><span class="sxs-lookup"><span data-stu-id="14a2d-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because hello CRP is part of hello current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="14a2d-258">Zie voor meer informatie [Microsoft Trust Center Hallo](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="14a2d-258">For more information, see [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="14a2d-259">Extensies</span><span class="sxs-lookup"><span data-stu-id="14a2d-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="14a2d-260">Hoe verwijder ik een virtuele machine uitbreiding van de schaal</span><span class="sxs-lookup"><span data-stu-id="14a2d-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="14a2d-261">een virtuele-machineschaalset toodelete instellen-uitbreiding, gebruik Hallo volgende PowerShell-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="14a2d-261">toodelete a virtual machine scale set extension, use hello following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="14a2d-262">U vindt Hallo Extensienaam waarde in `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="14a2d-262">You can find hello extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="14a2d-263">Er is dat een virtuele-machineschaalset voorbeeldsjabloon die met Operations Management Suite integreert?</span><span class="sxs-lookup"><span data-stu-id="14a2d-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="14a2d-264">Zie voor een virtuele-machineschaalset ingesteld voorbeeld van de sjabloon die in combinatie met Operations Management Suite, Hallo tweede voorbeeld in [een Azure Service Fabric-cluster implementeren en schakel de bewaking met behulp van logboekanalyse](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="14a2d-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see hello second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a><span data-ttu-id="14a2d-265">Extensies lijken toorun parallel op virtuele-machineschaalsets.</span><span class="sxs-lookup"><span data-stu-id="14a2d-265">Extensions seem toorun in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="14a2d-266">Dit zorgt ervoor dat mijn toofail aangepast script-extensie.</span><span class="sxs-lookup"><span data-stu-id="14a2d-266">This causes my custom script extension toofail.</span></span> <span data-ttu-id="14a2d-267">Wat kan ik doen toofix dit?</span><span class="sxs-lookup"><span data-stu-id="14a2d-267">What can I do toofix this?</span></span>

<span data-ttu-id="14a2d-268">toolearn over sequentiëren uitbreiding in virtuele-machineschaalsets, Zie [sequentiëren uitbreiding in virtuele Azure-machine-schaalsets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="14a2d-268">toolearn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="14a2d-269">Hoe stel ik Hallo wachtwoord voor virtuele machines in mijn virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="14a2d-269">How do I reset hello password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="14a2d-270">tooreset hello wachtwoord voor virtuele machines in uw virtuele-machineschaalset instellen, gebruikt u uitbreidingen voor toegang tot VM.</span><span class="sxs-lookup"><span data-stu-id="14a2d-270">tooreset hello password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="14a2d-271">Gebruik Hallo PowerShell-voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="14a2d-271">Use hello following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="14a2d-272">Hoe kan ik een extensie tooall VM's in mijn virtuele-machineschaalset toevoegen</span><span class="sxs-lookup"><span data-stu-id="14a2d-272">How do I add an extension tooall VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="14a2d-273">Als updatebeleid te is ingesteld**automatische**, Hallo-sjabloon opnieuw te implementeren met eigenschappen van nieuwe extensie Hallo updates alle virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="14a2d-273">If update policy is set too**automatic**, redeploying hello template with hello new extension properties updates all VMs.</span></span>

<span data-ttu-id="14a2d-274">Als updatebeleid te is ingesteld**handmatige**werk eerst Hallo-extensie en alle exemplaren in uw virtuele machines vervolgens handmatig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="14a2d-274">If update policy is set too**manual**, first update hello extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a><span data-ttu-id="14a2d-275">Als het Hallo-extensies die zijn gekoppeld aan een bestaande virtuele-machineschaalset zijn bijgewerkt, zijn de bestaande virtuele machines die van invloed op een?</span><span class="sxs-lookup"><span data-stu-id="14a2d-275">If hello extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="14a2d-276">(Dat wil zeggen, virtuele machines wordt Hallo *niet* overeen Hallo virtuele machine scale set model?) Of worden ze genegeerd?</span><span class="sxs-lookup"><span data-stu-id="14a2d-276">(That is, will hello VMs *not* match hello virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="14a2d-277">Wanneer een bestaande virtuele machine is service moeten worden hersteld of worden hersteld met een installatiekopie, Hallo-scripts die momenteel zijn geconfigureerd op Hallo virtuele-machineschaalset uitgevoerd, of worden Hallo-scripts die zijn geconfigureerd als Hallo die VM voor het eerst werd gemaakt gebruikt?</span><span class="sxs-lookup"><span data-stu-id="14a2d-277">When an existing machine is service-healed or reimaged, are hello scripts that are currently configured on hello virtual machine scale set executed, or are hello scripts that were configured when hello VM was first created used?</span></span>

<span data-ttu-id="14a2d-278">Als Hallo uitbreidingsdefinitie in het virtuele-machineschaalset Hallo ingesteld model wordt bijgewerkt en Hallo upgradePolicy eigenschap is ingesteld op te**automatische**, Hallo VM's worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="14a2d-278">If hello extension definition in hello virtual machine scale set model is updated and hello upgradePolicy property is set too**automatic**, it updates hello VMs.</span></span> <span data-ttu-id="14a2d-279">Als Hallo upgradePolicy eigenschap is ingesteld, te**handmatige**, extensies zijn gemarkeerd als niet overeenkomt met Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="14a2d-279">If hello upgradePolicy property is set too**manual**, extensions are flagged as not matching hello model.</span></span> 

<span data-ttu-id="14a2d-280">Als een bestaande VM-service moeten worden hersteld, wordt deze weergegeven als een herstart en Hallo-extensies worden niet opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="14a2d-280">If an existing VM is service-healed, it appears as a reboot, and hello extensions are not rerun.</span></span> <span data-ttu-id="14a2d-281">Als deze wordt teruggezet, is het zoals Hallo OS station vervangen door de broninstallatiekopie Hallo.</span><span class="sxs-lookup"><span data-stu-id="14a2d-281">If it is reimaged, it's like replacing hello OS drive with hello source image.</span></span> <span data-ttu-id="14a2d-282">Alle specialisatie uit de meest recente model hello, zoals-extensies worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="14a2d-282">Any specialization from hello latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a><span data-ttu-id="14a2d-283">Hoe ik deelnemen aan een virtuele machine scale set tooan Azure AD-domein?</span><span class="sxs-lookup"><span data-stu-id="14a2d-283">How do I join a virtual machine scale set tooan Azure AD domain?</span></span>

<span data-ttu-id="14a2d-284">toojoin een virtuele machine scale set tooan Azure Active Directory (Azure AD)-domein, kunt u een uitbreiding definiëren.</span><span class="sxs-lookup"><span data-stu-id="14a2d-284">toojoin a virtual machine scale set tooan Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="14a2d-285">een uitbreiding toodefine gebruikt Hallo JsonADDomainExtension eigenschap:</span><span class="sxs-lookup"><span data-stu-id="14a2d-285">toodefine an extension, use hello JsonADDomainExtension property:</span></span>

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="14a2d-286">De extensie scale set van mijn virtuele machine probeert tooinstall iets dat moet worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="14a2d-286">My virtual machine scale set extension is trying tooinstall something that requires a reboot.</span></span> <span data-ttu-id="14a2d-287">Bijvoorbeeld 'commandToExecute': ' powershell.exe - ExecutionPolicy Unrestricted Install-WindowsFeature – naam FS-Resource-Manager – IncludeManagementTools '</span><span class="sxs-lookup"><span data-stu-id="14a2d-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="14a2d-288">Als uw scale set-extensie van virtuele machine tooinstall iets dat moet worden opgestart probeert, kunt u hello Azure Automation Desired State Configuration (DSC Automation)-extensie.</span><span class="sxs-lookup"><span data-stu-id="14a2d-288">If your virtual machine scale set extension is trying tooinstall something that requires a reboot, you can use hello Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="14a2d-289">Als Hallo besturingssysteem Windows Server 2012 R2, wordt Azure ophaalt in Hallo Windows Management Framework (WMF) 5.0 setup opnieuw is opgestart, en vervolgens verder met de Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="14a2d-289">If hello operating system is Windows Server 2012 R2, Azure pulls in hello Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with hello configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="14a2d-290">Hoe kan ik antimalware inschakelen in mijn virtuele-machineschaalset?</span><span class="sxs-lookup"><span data-stu-id="14a2d-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="14a2d-291">tooturn op anti-malware op uw virtuele-machineschaalset instellen, gebruikt u Hallo PowerShell-voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="14a2d-291">tooturn on antimalware on your virtual machine scale set, use hello following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="14a2d-292">Ik heb nodig tooexecute een aangepast script dat wordt gehost in een persoonlijke storage-account.</span><span class="sxs-lookup"><span data-stu-id="14a2d-292">I need tooexecute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="14a2d-293">Hallo-script met succes wordt uitgevoerd wanneer Hallo opslag openbaar is, maar wanneer ik probeer toouse Shared Access Signature (SAS), is mislukt.</span><span class="sxs-lookup"><span data-stu-id="14a2d-293">hello script runs successfully when hello storage is public, but when I try toouse a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="14a2d-294">Dit bericht wordt weergegeven: 'Verplichte parameters ontbreekt voor geldige Shared Access Signature'.</span><span class="sxs-lookup"><span data-stu-id="14a2d-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="14a2d-295">Koppeling + SAS werkt prima vanuit Mijn lokale browser.</span><span class="sxs-lookup"><span data-stu-id="14a2d-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="14a2d-296">een aangepast script dat wordt gehost in een persoonlijke opslagaccount tooexecute beveiligde instellingen met de Hallo opslagaccountsleutel en de naam instellen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-296">tooexecute a custom script that's hosted in a private storage account, set up protected settings with hello storage account key and name.</span></span> <span data-ttu-id="14a2d-297">Zie voor meer informatie [aangepast Script uitbreiding voor Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="14a2d-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="14a2d-298">Netwerken</span><span class="sxs-lookup"><span data-stu-id="14a2d-298">Networking</span></span>
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a><span data-ttu-id="14a2d-299">Is het mogelijk tooassign een Netwerkbeveiligingsgroep (NSG) tooa schaal instellen, zodat de tooall Hallo VM NIC's in de verzameling hello wordt toegepast?</span><span class="sxs-lookup"><span data-stu-id="14a2d-299">Is it possible tooassign a Network Security Group (NSG) tooa scale set, so that it will apply tooall hello VM NICs in hello set?</span></span>

<span data-ttu-id="14a2d-300">Ja.</span><span class="sxs-lookup"><span data-stu-id="14a2d-300">Yes.</span></span> <span data-ttu-id="14a2d-301">Een Netwerkbeveiligingsgroep kunnen direct tooa schaalset door ernaar wordt verwezen in Hallo networkInterfaceConfigurations sectie Hallo netwerkprofiel worden aangebracht.</span><span class="sxs-lookup"><span data-stu-id="14a2d-301">A Network Security Group can be applied directly tooa scale set by referencing it in hello networkInterfaceConfigurations section of hello network profile.</span></span> <span data-ttu-id="14a2d-302">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="14a2d-302">Example:</span></span>

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a><span data-ttu-id="14a2d-303">Hoe kan ik dat doen geen VIP's wisselen voor virtuele-machineschaalsets in Hallo dezelfde abonnement en dezelfde regio?</span><span class="sxs-lookup"><span data-stu-id="14a2d-303">How do I do a VIP swap for virtual machine scale sets in hello same subscription and same region?</span></span>

<span data-ttu-id="14a2d-304">Als er twee virtuele-machineschaalsets met de front-ends van Azure Load Balancer en ze zich in hetzelfde abonnement en dezelfde regio Hallo, kan u Hallo openbare IP-adressen van elkaar ongedaan en toohello andere toewijzen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in hello same subscription and region, you could deallocate hello public IP addresses from each one, and assign toohello other.</span></span> <span data-ttu-id="14a2d-305">Zie [VIP's wisselen: blauw groen implementatie in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="14a2d-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="14a2d-306">Dit betekent dat er een vertraging al als Hallo resources worden weergegeven ongedaan/toegewezen op Hallo niveau.</span><span class="sxs-lookup"><span data-stu-id="14a2d-306">This does imply a delay though as hello resources are deallocated/allocated at hello network level.</span></span> <span data-ttu-id="14a2d-307">Een optie voor snellere is toouse Azure Application Gateway met twee back-endpools en een regel voor doorsturen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-307">A faster option is toouse Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="14a2d-308">U kunt ook u uw toepassing met kan host [-Azure App service](https://azure.microsoft.com/en-us/services/app-service/) die ondersteuning biedt voor het snel overschakelen tussen sites omwisselen fasering en productie.</span><span class="sxs-lookup"><span data-stu-id="14a2d-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a><span data-ttu-id="14a2d-309">Hoe geef ik een bereik van particuliere IP-adressen toouse voor statische privé IP-adrestoewijzing</span><span class="sxs-lookup"><span data-stu-id="14a2d-309">How do I specify a range of private IP addresses toouse for static private IP address allocation?</span></span>

<span data-ttu-id="14a2d-310">IP-adressen zijn geselecteerd uit een subnet op dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="14a2d-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="14a2d-311">Hallo toewijzingsmethode van virtuele machine scale set IP-adressen is altijd 'dynamische' hoeft niet, maar dat dat deze IP-adressen kunnen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-311">hello allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="14a2d-312">In dit geval betekent 'dynamische' alleen dat u geen Hallo IP-adres in een PUT-aanvraag opgeven.</span><span class="sxs-lookup"><span data-stu-id="14a2d-312">In this case, "dynamic" only means that you do not specify hello IP address in a PUT request.</span></span> <span data-ttu-id="14a2d-313">Hallo statische instellen via het Hallo-subnet opgeven.</span><span class="sxs-lookup"><span data-stu-id="14a2d-313">Specify hello static set by using hello subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a><span data-ttu-id="14a2d-314">Hoe implementeer ik een virtuele machine scale set tooan bestaande Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="14a2d-314">How do I deploy a virtual machine scale set tooan existing Azure virtual network?</span></span> 

<span data-ttu-id="14a2d-315">een virtuele-machineschaalset toodeploy tooan bestaande virtuele Azure-netwerk, raadpleegt u [implementeren van een virtuele machine scale set tooan bestaande virtuele netwerk](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="14a2d-315">toodeploy a virtual machine scale set tooan existing Azure virtual network, see [Deploy a virtual machine scale set tooan existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a><span data-ttu-id="14a2d-316">Hoe toevoegen Hallo IP-adres van Hallo eerste virtuele machine in een virtuele-machineschaalset toohello uitvoer van een sjabloon ingesteld?</span><span class="sxs-lookup"><span data-stu-id="14a2d-316">How do I add hello IP address of hello first VM in a virtual machine scale set toohello output of a template?</span></span>

<span data-ttu-id="14a2d-317">tooadd hello IP-adres van Hallo eerste virtuele machine in een virtuele machine scale set toohello uitvoer van een sjabloon, Zie [ARM: ophalen VMSS van privé IP-adressen](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="14a2d-317">tooadd hello IP address of hello first VM in a virtual machine scale set toohello output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="14a2d-318">Kan ik schaalsets met versnelde toegang gebruiken?</span><span class="sxs-lookup"><span data-stu-id="14a2d-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="14a2d-319">Ja.</span><span class="sxs-lookup"><span data-stu-id="14a2d-319">Yes.</span></span> <span data-ttu-id="14a2d-320">toouse versnelde netwerken, instellingen voor enableAcceleratedNetworking tootrue in uw scale set van networkInterfaceConfigurations.</span><span class="sxs-lookup"><span data-stu-id="14a2d-320">toouse accelerated networking, set enableAcceleratedNetworking tootrue in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="14a2d-321">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="14a2d-321">E.g.</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="14a2d-322">Hoe kan ik Hallo DNS-servers die worden gebruikt door een schaalset configureren?</span><span class="sxs-lookup"><span data-stu-id="14a2d-322">How can I configure hello DNS servers used by a scale set?</span></span>

<span data-ttu-id="14a2d-323">toocreate een VM-schaalset met een aangepaste DNS-configuratie, voeg dat een dnsSettings JSON pakket toohello schaalset networkInterfaceConfigurations-sectie.</span><span class="sxs-lookup"><span data-stu-id="14a2d-323">toocreate a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="14a2d-324">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="14a2d-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a><span data-ttu-id="14a2d-325">Hoe kan ik een scale set tooassign een openbare IP-adres tooeach VM configureren?</span><span class="sxs-lookup"><span data-stu-id="14a2d-325">How can I configure a scale set tooassign a public IP address tooeach VM?</span></span>

<span data-ttu-id="14a2d-326">een VM-die schaalset toocreate wijst een openbare IP-adres tooeach VM, zorg ervoor dat Hallo API-versie van Hallo Microsoft.Compute/virtualMAchineScaleSets resource 2017-03-30 en toevoegen een _publicipaddressconfiguration_ JSON-pakket toohello schaalset ipConfigurations-sectie.</span><span class="sxs-lookup"><span data-stu-id="14a2d-326">toocreate a VM scale set that assigns a public IP address tooeach VM, make sure hello API version of hello Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="14a2d-327">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="14a2d-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a><span data-ttu-id="14a2d-328">Kan ik een scale set toowork met meerdere Toepassingsgateways configureren?</span><span class="sxs-lookup"><span data-stu-id="14a2d-328">Can I configure a scale set toowork with multiple Application Gateways?</span></span>

<span data-ttu-id="14a2d-329">Ja.</span><span class="sxs-lookup"><span data-stu-id="14a2d-329">Yes.</span></span> <span data-ttu-id="14a2d-330">U kunt Hallo resource-id's voor meerdere pools toohello van de toepassingsgateway back-end-adres toevoegen _applicationGatewayBackendAddressPools_ lijst in Hallo _ipConfigurations_ gedeelte van uw schaalset netwerkprofiel.</span><span class="sxs-lookup"><span data-stu-id="14a2d-330">You can add hello resource id's for multiple Application Gateway backend address pools toohello _applicationGatewayBackendAddressPools_ list in hello _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="14a2d-331">Schalen</span><span class="sxs-lookup"><span data-stu-id="14a2d-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="14a2d-332">In welk geval zou ik een virtuele-machineschaalset ingesteld met minder dan twee virtuele machines maken?</span><span class="sxs-lookup"><span data-stu-id="14a2d-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="14a2d-333">Een reden toocreate een virtuele machine schaalset met minder dan twee virtuele machines wordt toouse Hallo elastische eigenschappen van een virtuele-machineschaalset ingesteld.</span><span class="sxs-lookup"><span data-stu-id="14a2d-333">One reason toocreate a virtual machine scale set with fewer than two VMs would be toouse hello elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="14a2d-334">Bijvoorbeeld, kan u een virtuele-machineschaalset weergeven met nul toodefine VMs uw infrastructuur implementeren zonder VM gebruikskosten betaalt.</span><span class="sxs-lookup"><span data-stu-id="14a2d-334">For example, you could deploy a virtual machine scale set with zero VMs toodefine your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="14a2d-335">Wanneer u klaar toodeploy virtuele machines bent, verhogen vervolgens capaciteit' Hallo' van Hallo aantal virtuele machines scale set toohello productie-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="14a2d-335">Then, when you are ready toodeploy VMs, increase hello “capacity” of hello virtual machine scale set toohello production instance count.</span></span>

<span data-ttu-id="14a2d-336">Een andere reden dat u een virtuele-machineschaalset ingesteld met minder dan twee virtuele machines kunt maken, is als u zich zorgen over minder dan de beschikbaarheid in met behulp van een beschikbaarheidsset met discrete virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="14a2d-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="14a2d-337">Virtuele-machineschaalsets bieden u een toowork manier met niet gedifferentieerde compute-eenheden die vervangbare zijn.</span><span class="sxs-lookup"><span data-stu-id="14a2d-337">Virtual machine scale sets give you a way toowork with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="14a2d-338">Deze uniformiteit is een belangrijke onderscheid voor virtuele-machineschaalsets versus beschikbaarheidssets.</span><span class="sxs-lookup"><span data-stu-id="14a2d-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="14a2d-339">Veel staatloze werkbelastingen volgen afzonderlijke eenheden niet.</span><span class="sxs-lookup"><span data-stu-id="14a2d-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="14a2d-340">Als de werkbelasting Hallo komt, kunt u terugschroeven tooone compute-eenheid en opschalen toomany wanneer Hallo werkbelasting toeneemt.</span><span class="sxs-lookup"><span data-stu-id="14a2d-340">If hello workload drops, you can scale down tooone compute unit, and then scale up toomany when hello workload increases.</span></span>

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="14a2d-341">Hoe wijzig ik Hallo aantal VM's in een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="14a2d-341">How do I change hello number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="14a2d-342">Zie toochange Hallo aantal VM's in een virtuele-machineschaalset [wijzigen Hallo-exemplaren van een virtuele-machineschaalset](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="14a2d-342">toochange hello number of VMs in a virtual machine scale set, see [Change hello instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="14a2d-343">Hoe ik aangepaste waarschuwingen voor als bepaalde drempelwaarden zijn bereikt definiëren?</span><span class="sxs-lookup"><span data-stu-id="14a2d-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="14a2d-344">Hebt u enige flexibiliteit in hoe u waarschuwingen voor de opgegeven drempelwaarden verwerken.</span><span class="sxs-lookup"><span data-stu-id="14a2d-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="14a2d-345">U kunt bijvoorbeeld aangepaste webhooks definiëren.</span><span class="sxs-lookup"><span data-stu-id="14a2d-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="14a2d-346">Hallo na webhook voorbeeld is van een Resource Manager-sjabloon:</span><span class="sxs-lookup"><span data-stu-id="14a2d-346">hello following webhook example is from a Resource Manager template:</span></span>

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

<span data-ttu-id="14a2d-347">In dit voorbeeld wordt een waarschuwing tooPagerduty.com wanneer een drempelwaarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="14a2d-347">In this example, an alert goes tooPagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="14a2d-348">Patching en bewerkingen</span><span class="sxs-lookup"><span data-stu-id="14a2d-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="14a2d-349">Hoe maak ik een schaal instellen in een bestaande resourcegroep</span><span class="sxs-lookup"><span data-stu-id="14a2d-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="14a2d-350">Schaalsets maken in een bestaande resource groep is nog niet mogelijk hello Azure-portal, maar u kunt een bestaande resourcegroep opgeven bij het implementeren van een schaal van een Azure Resource Manager-sjabloon instellen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-350">Creating scale sets in an existing resource group is not yet possible from hello Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="14a2d-351">U kunt ook een bestaande resourcegroep opgeven bij het maken van een schaal ingesteld met Azure PowerShell of CLI.</span><span class="sxs-lookup"><span data-stu-id="14a2d-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a><span data-ttu-id="14a2d-352">Kan verplaatsen we dat een schaalset tooanother resourcegroep?</span><span class="sxs-lookup"><span data-stu-id="14a2d-352">Can we move a scale set tooanother resource group?</span></span>

<span data-ttu-id="14a2d-353">Ja, kunt u scale set resources tooa nieuw abonnement of resourcegroep verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-353">Yes, you can move scale set resources tooa new subscription or resource group.</span></span>

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a><span data-ttu-id="14a2d-354">Hoe tooI bijwerken mijn virtuele-machineschaalset tooa nieuwe installatiekopie?</span><span class="sxs-lookup"><span data-stu-id="14a2d-354">How tooI update my virtual machine scale set tooa new image?</span></span> <span data-ttu-id="14a2d-355">Hoe u beheer patchen?</span><span class="sxs-lookup"><span data-stu-id="14a2d-355">How do I manage patching?</span></span>

<span data-ttu-id="14a2d-356">tooupdate instellen voor uw virtuele-machineschaalset tooa nieuwe installatiekopie en toomanage patchen, Zie [upgraden van een virtuele-machineschaalset](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="14a2d-356">tooupdate your virtual machine scale set tooa new image, and toomanage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a><span data-ttu-id="14a2d-357">Kan ik Hallo terugzetten van de installatiekopie bewerking tooreset een virtuele machine gebruiken zonder Hallo afbeelding te wijzigen?</span><span class="sxs-lookup"><span data-stu-id="14a2d-357">Can I use hello reimage operation tooreset a VM without changing hello image?</span></span> <span data-ttu-id="14a2d-358">(Dat wil zeggen, ik wil opnieuw een VM toofactory-instellingen in plaats van de nieuwe installatiekopie tooa.)</span><span class="sxs-lookup"><span data-stu-id="14a2d-358">(That is, I want reset a VM toofactory settings rather than tooa new image.)</span></span>

<span data-ttu-id="14a2d-359">Ja, kunt u Hallo terugzetten van de installatiekopie bewerking tooreset een virtuele machine zonder Hallo afbeelding te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-359">Yes, you can use hello reimage operation tooreset a VM without changing hello image.</span></span> <span data-ttu-id="14a2d-360">Echter, als uw virtuele-machineschaalset verwijst naar een platforminstallatiekopie met `version = latest`, uw virtuele machine kunt bijwerken tooa hoger OS-installatiekopie bij het aanroepen van `reimage`.</span><span class="sxs-lookup"><span data-stu-id="14a2d-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update tooa later OS image when you call `reimage`.</span></span>

<span data-ttu-id="14a2d-361">Zie voor meer informatie [beheren van alle VM's in een virtuele-machineschaalset](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="14a2d-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="14a2d-362">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="14a2d-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="14a2d-363">Hoe schakel ik op diagnostische gegevens over opstarten?</span><span class="sxs-lookup"><span data-stu-id="14a2d-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="14a2d-364">tooturn op diagnostische gegevens over opstarten, maak eerst een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="14a2d-364">tooturn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="14a2d-365">Zet dit JSON-blok in uw virtuele-machineschaalset **virtualMachineProfile**, en Hallo virtuele-machineschaalset bijwerken:</span><span class="sxs-lookup"><span data-stu-id="14a2d-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update hello virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="14a2d-366">Wanneer een nieuwe virtuele machine wordt gemaakt, ziet u Hallo InstanceView eigenschap Hallo VM Hallo details voor Hallo schermafbeelding, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="14a2d-366">When a new VM is created, hello InstanceView property of hello VM shows hello details for hello screenshot, and so on.</span></span> <span data-ttu-id="14a2d-367">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="14a2d-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="14a2d-368">Eigenschappen van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="14a2d-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="14a2d-369">Hoe krijg eigenschapsinformatie voor elke virtuele machine zonder dat meerdere aanroepen?</span><span class="sxs-lookup"><span data-stu-id="14a2d-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="14a2d-370">Bijvoorbeeld, hoe ik krijgt Hallo foutdomein voor elk Hallo 100 virtuele machines in mijn virtuele-machineschaalset?</span><span class="sxs-lookup"><span data-stu-id="14a2d-370">For example, how would I get hello fault domain for each of hello 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="14a2d-371">tooget eigenschapsinformatie voor elke virtuele machine zonder dat meerdere aanroepen, u kunt aanroepen `ListVMInstanceViews` als volgt een REST-API `GET` op Hallo resource-URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="14a2d-371">tooget property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on hello following resource URI:</span></span>

<span data-ttu-id="14a2d-372">/Subscriptions/ < subscription_id > /resourceGroups/ < resource_group_name > /providers/Microsoft.Compute/virtualMachineScaleSets/ < scaleset_name > / virtuele machines? $expand = instanceView & $select = instanceView</span><span class="sxs-lookup"><span data-stu-id="14a2d-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="14a2d-373">Kan ik andere uitbreiding argumenten doorgeven toodifferent virtuele machines in een virtuele-machineschaalset?</span><span class="sxs-lookup"><span data-stu-id="14a2d-373">Can I pass different extension arguments toodifferent VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="14a2d-374">Nee, u kunt niet doorgeven andere uitbreiding argumenten toodifferent virtuele machines in een virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="14a2d-374">No, you cannot pass different extension arguments toodifferent VMs in a virtual machine scale set.</span></span> <span data-ttu-id="14a2d-375">Extensies kunnen echter op basis van unieke eigenschappen Hallo Hallo VM ze worden uitgevoerd, bijvoorbeeld als u op de naam van de machine Hallo fungeren.</span><span class="sxs-lookup"><span data-stu-id="14a2d-375">However, extensions can act based on hello unique properties of hello VM they are running on, such as on hello machine name.</span></span> <span data-ttu-id="14a2d-376">Extensies ook kunnen een query metagegevens van het exemplaar op http://169.254.169.254 tooget meer informatie over Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="14a2d-376">Extensions also can query instance metadata on http://169.254.169.254 tooget more information about hello VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="14a2d-377">Waarom zijn er onderbrekingen tussen mijn namen voor machines van virtuele machine scale set VM en VM-id's?</span><span class="sxs-lookup"><span data-stu-id="14a2d-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="14a2d-378">Bijvoorbeeld: 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="14a2d-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="14a2d-379">Er onderbrekingen tussen de namen voor machines van virtuele machine scale set VM en VM-id's zijn omdat uw virtuele-machineschaalset **overprovision** eigenschap is ingesteld toohello standaardwaarde **true**.</span><span class="sxs-lookup"><span data-stu-id="14a2d-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set toohello default value of **true**.</span></span> <span data-ttu-id="14a2d-380">Als te overmatige inrichting is ingesteld**true**, meer virtuele machines dan aangevraagd worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="14a2d-380">If overprovisioning is set too**true**, more VMs than requested are created.</span></span> <span data-ttu-id="14a2d-381">Extra virtuele machines vervolgens verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14a2d-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="14a2d-382">In dit geval u krijgen hogere implementatie betrouwbaarheid, maar regels op Hallo kosten van aaneengesloten naming en aaneengesloten Network Address Translation (NAT).</span><span class="sxs-lookup"><span data-stu-id="14a2d-382">In this case, you gain increased deployment reliability, but at hello expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="14a2d-383">U kunt deze eigenschap instellen te**false**.</span><span class="sxs-lookup"><span data-stu-id="14a2d-383">You can set this property too**false**.</span></span> <span data-ttu-id="14a2d-384">Voor kleine virtuele machine-schaalsets beïnvloeden niet dit betrouwbaarheid van de implementatie aanzienlijk.</span><span class="sxs-lookup"><span data-stu-id="14a2d-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a><span data-ttu-id="14a2d-385">Wat is Hallo verschil tussen een virtuele machine in een virtuele-machineschaalset verwijderen en toewijzing Hallo VM?</span><span class="sxs-lookup"><span data-stu-id="14a2d-385">What is hello difference between deleting a VM in a virtual machine scale set and deallocating hello VM?</span></span> <span data-ttu-id="14a2d-386">Wanneer moet ik een via andere Hallo kiezen?</span><span class="sxs-lookup"><span data-stu-id="14a2d-386">When should I choose one over hello other?</span></span>

<span data-ttu-id="14a2d-387">Hallo belangrijkste verschil tussen een virtuele machine in een virtuele-machineschaalset verwijderen en toewijzing Hallo VM is dat `deallocate` Hallo virtuele harde schijven (VHD's) niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-387">hello main difference between deleting a VM in a virtual machine scale set and deallocating hello VM is that `deallocate` doesn’t delete hello virtual hard disks (VHDs).</span></span> <span data-ttu-id="14a2d-388">Er zijn kosten voor opslag die is gekoppeld aan die wordt uitgevoerd `stop deallocate`.</span><span class="sxs-lookup"><span data-stu-id="14a2d-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="14a2d-389">U mogelijk een of andere voor een van de volgende redenen Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="14a2d-389">You might use one or hello other for one of hello following reasons:</span></span>

- <span data-ttu-id="14a2d-390">U wilt toostop compute-kosten te betalen, maar u wilt dat de status van tookeep Hallo schijf Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="14a2d-390">You want toostop paying compute costs, but you want tookeep hello disk state of hello VMs.</span></span>
- <span data-ttu-id="14a2d-391">Wilt u sneller dan u een virtuele-machineschaalset kan uitbreiden toostart een set van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="14a2d-391">You want toostart a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="14a2d-392">Verwante toothis scenario wordt u mogelijk hebt gemaakt uw eigen engine voor het automatisch schalen en wilt dat een snellere end-to-end-schaal.</span><span class="sxs-lookup"><span data-stu-id="14a2d-392">Related toothis scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="14a2d-393">U hebt een virtuele-machineschaalset die ongelijkmatig verdeeld is over domeinen met fouten of update-domeinen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="14a2d-394">Dit wordt mogelijk omdat u selectief virtuele machines verwijderd, of omdat de virtuele machines zijn verwijderd na overmatige inrichting.</span><span class="sxs-lookup"><span data-stu-id="14a2d-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="14a2d-395">Met `stop deallocate` gevolgd door `start` op Hallo virtuele machine schaal instelt gelijkmatig Hallo VMs verdeelt over domeinen met fouten of update-domeinen.</span><span class="sxs-lookup"><span data-stu-id="14a2d-395">Running `stop deallocate` followed by `start` on hello virtual machine scale set evenly distributes hello VMs across fault domains or update domains.</span></span>

