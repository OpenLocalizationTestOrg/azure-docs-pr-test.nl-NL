---
title: aaaCheck connectiviteit met de Azure-netwerk-Watcher - PowerShell | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe tootest connectiviteit met de netwerk-Watcher met behulp van PowerShell
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 4bcb90a72f178445c38b7bd7fc5054c5d0c200bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="1c302-103">Controleer de verbinding met Azure met behulp van PowerShell netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="1c302-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1c302-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1c302-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="1c302-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c302-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="1c302-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1c302-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="1c302-107">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="1c302-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="1c302-108">Meer informatie over hoe toouse connectiviteit tooverify als een directe TCP-verbinding van een virtuele machine tooa opgegeven eindpunt kan worden vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="1c302-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1c302-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="1c302-109">Before you begin</span></span>

<span data-ttu-id="1c302-110">In dit artikel wordt ervan uitgegaan dat er Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c302-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="1c302-111">Een exemplaar van netwerk-Watcher in Hallo regio die u wilt toocheck connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="1c302-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="1c302-112">Virtuele machines toocheck connectiviteit met.</span><span class="sxs-lookup"><span data-stu-id="1c302-112">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="1c302-113">Controle van de verbinding zijn nodig voor de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="1c302-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="1c302-114">Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="1c302-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="1c302-115">Hallo preview mogelijkheid registreren</span><span class="sxs-lookup"><span data-stu-id="1c302-115">Register hello preview capability</span></span>

<span data-ttu-id="1c302-116">Connectiviteit is momenteel in openbare preview toouse deze functie toobe geregistreerd moet.</span><span class="sxs-lookup"><span data-stu-id="1c302-116">Connectivity is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="1c302-117">toodo deze, Voer Hallo PowerShell-voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c302-117">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="1c302-118">tooverify hello registratie is gelukt, Hallo volgende Powershell-voorbeeld uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1c302-118">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="1c302-119">Als het Hallo-functie is juist is geregistreerd, Hallo uitvoer, moet overeenkomen met Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="1c302-119">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="1c302-120">Controleer de connectiviteit tooa virtuele machine</span><span class="sxs-lookup"><span data-stu-id="1c302-120">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="1c302-121">In dit voorbeeld controleert connectiviteit tooa bestemde virtuele machine via poort 80.</span><span class="sxs-lookup"><span data-stu-id="1c302-121">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="1c302-122">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1c302-122">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"
$destVMName = "Database0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName
$VM2 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $destVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationId $VM2.Id -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="1c302-123">Antwoord</span><span class="sxs-lookup"><span data-stu-id="1c302-123">Response</span></span>

<span data-ttu-id="1c302-124">Hallo na antwoord is van het vorige voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c302-124">hello following response is from hello previous example.</span></span>  <span data-ttu-id="1c302-125">In dit antwoord Hallo `ConnectionStatus` is **onbereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="1c302-125">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="1c302-126">U kunt zien dat alle tests verzonden mislukte Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c302-126">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="1c302-127">Hallo-connectiviteit op Hallo virtueel apparaat is mislukt vanwege tooa gebruiker geconfigureerde `NetworkSecurityRule` met de naam **UserRule_Port80**, tooblock binnenkomend verkeer op poort 80 geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1c302-127">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="1c302-128">Deze informatie kan gebruikte tooresearch verbindingsproblemen zijn.</span><span class="sxs-lookup"><span data-stu-id="1c302-128">This information can be used tooresearch connection issues.</span></span>

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "c5222ea0-3213-4f85-a642-cee63217c2f3",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurat
                   ions/ipconfig1",
                       "NextHopIds": [
                         "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa",
                       "Address": "10.1.2.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "0f1500cd-c512-4d43-b431-7267e4e67017"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "0f1500cd-c512-4d43-b431-7267e4e67017",
                       "Address": "10.1.3.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "a88940f8-5fbe-40da-8d99-1dee89240f64"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "NetworkSecurityRule",
                           "Context": [
                             {
                               "key": "RuleName",
                               "value": "UserRule_Port80"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "VnetLocal",
                       "Id": "a88940f8-5fbe-40da-8d99-1dee89240f64",
                       "Address": "10.1.4.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurati
                   ons/ipconfig1",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="validate-routing-issues"></a><span data-ttu-id="1c302-129">Problemen met routing valideren</span><span class="sxs-lookup"><span data-stu-id="1c302-129">Validate routing issues</span></span>

<span data-ttu-id="1c302-130">Hallo voorbeeld controleert de connectiviteit tussen een virtuele machine en een extern eindpunt.</span><span class="sxs-lookup"><span data-stu-id="1c302-130">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="1c302-131">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1c302-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="1c302-132">Antwoord</span><span class="sxs-lookup"><span data-stu-id="1c302-132">Response</span></span>

<span data-ttu-id="1c302-133">Hallo in Hallo voorbeeld te volgen, `ConnectionStatus` wordt weergegeven als **onbereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="1c302-133">In hello following example, hello `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="1c302-134">In Hallo `Hops` details, kunt u zien onder `Issues` dat Hallo verkeer is geblokkeerd vanwege tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="1c302-134">In hello `Hops` details, you can see under `Issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span> 

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "b4f7bceb-07a3-44ca-8bae-adec6628225f",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "3fee8adf-692f-4523-b742-f6fdf6da6584"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "UserDefinedRoute",
                           "Context": [
                             {
                               "key": "RouteType",
                               "value": "User"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "Destination",
                       "Id": "3fee8adf-692f-4523-b742-f6fdf6da6584",
                       "Address": "13.107.21.200",
                       "ResourceId": "Unknown",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-website-latency"></a><span data-ttu-id="1c302-135">Latentie van de website controleren</span><span class="sxs-lookup"><span data-stu-id="1c302-135">Check website latency</span></span>

<span data-ttu-id="1c302-136">Hallo volgende voorbeeld wordt gecontroleerd Hallo connectiviteit tooa website.</span><span class="sxs-lookup"><span data-stu-id="1c302-136">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="1c302-137">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1c302-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="1c302-138">Antwoord</span><span class="sxs-lookup"><span data-stu-id="1c302-138">Response</span></span>

<span data-ttu-id="1c302-139">In Hallo antwoord te volgen, ziet u Hallo `ConnectionStatus` wordt weergegeven als **bereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="1c302-139">In hello following response, you can see hello `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="1c302-140">Als een verbinding geslaagd is, zijn latentie waarden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1c302-140">When a connection is successful, latency values are provided.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 7
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "1f0e3415-27b0-4bf7-a59d-3e19fb854e3e",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0",
                       "Address": "204.79.197.200",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="1c302-141">Controleer de connectiviteit tooa opslag eindpunt</span><span class="sxs-lookup"><span data-stu-id="1c302-141">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="1c302-142">Hallo volgt test Hallo verbinding hebben met een virtuele machine tooa blog van storage-account.</span><span class="sxs-lookup"><span data-stu-id="1c302-142">hello following example tests hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="1c302-143">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1c302-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="1c302-144">Antwoord</span><span class="sxs-lookup"><span data-stu-id="1c302-144">Response</span></span>

<span data-ttu-id="1c302-145">Hallo is volgende json Hallo voorbeeld reactie van de vorige Hallo-cmdlet uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1c302-145">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="1c302-146">Als het Hallo-doel is bereikbaar, Hallo `ConnectionStatus` eigenschap wordt weergegeven als **bereikbaar**.</span><span class="sxs-lookup"><span data-stu-id="1c302-146">As hello destination is reachable, hello `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="1c302-147">U vindt Hallo-gegevens met betrekking tot Hallo aantal hops vereist tooreach Hallo storage-blob en latentie.</span><span class="sxs-lookup"><span data-stu-id="1c302-147">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 8
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "9e7f61d9-fb45-41db-83e2-c815a919b8ed",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "1e6d4b3c-7964-4afd-b959-aaa746ee0f15"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "1e6d4b3c-7964-4afd-b959-aaa746ee0f15",
                       "Address": "13.71.200.248",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="next-steps"></a><span data-ttu-id="1c302-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c302-148">Next steps</span></span>

<span data-ttu-id="1c302-149">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1c302-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="1c302-150">Zie als verkeer wordt geblokkeerd en mag geen [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="1c302-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<!-- Image references -->














