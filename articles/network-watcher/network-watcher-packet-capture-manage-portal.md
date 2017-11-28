---
title: Pakket opnamen met Azure-netwerk-Watcher - Azure-portal beheren | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u de functie voor het vastleggen van pakket van netwerk-Watcher met Azure portal beheren
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 33390532cc4fc1129a4f960d589f41bc95e5a1ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-the-portal"></a><span data-ttu-id="3b735-103">Pakket opnamen beheren met Azure met behulp van de portal netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="3b735-103">Manage packet captures with Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3b735-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3b735-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="3b735-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b735-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="3b735-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3b735-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="3b735-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3b735-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="3b735-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="3b735-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="3b735-109">Netwerk-Watcher pakketopname kunt u om sessies vastleggen om bij te houden van verkeer van en naar een virtuele machine te maken.</span><span class="sxs-lookup"><span data-stu-id="3b735-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="3b735-110">Filters zijn beschikbaar voor de opnamesessie om te controleren of dat u alleen het verkeer die u wilt vastleggen.</span><span class="sxs-lookup"><span data-stu-id="3b735-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="3b735-111">Pakketopname helpt op te sporen netwerk afwijkingen reactief en proactief.</span><span class="sxs-lookup"><span data-stu-id="3b735-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="3b735-112">Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's voor foutopsporing van client-servercommunicaties en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="3b735-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="3b735-113">Door op afstand activeren pakket opnamen, deze mogelijkheid kan vergemakkelijken de last van een pakketopname handmatig en op de gewenste machine, die kostbare tijd bespaart worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3b735-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="3b735-114">In dit artikel leert u de verschillende beheertaken die momenteel beschikbaar voor pakketopname zijn.</span><span class="sxs-lookup"><span data-stu-id="3b735-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="3b735-115">**Start een pakketopname**</span><span class="sxs-lookup"><span data-stu-id="3b735-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="3b735-116">**Stop de pakketopname van een**</span><span class="sxs-lookup"><span data-stu-id="3b735-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="3b735-117">**Het vastleggen van een pakket verwijderen**</span><span class="sxs-lookup"><span data-stu-id="3b735-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="3b735-118">**Een pakketopname downloaden**</span><span class="sxs-lookup"><span data-stu-id="3b735-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="3b735-119">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="3b735-119">Before you begin</span></span>

<span data-ttu-id="3b735-120">In dit artikel wordt ervan uitgegaan dat u de volgende bronnen hebt:</span><span class="sxs-lookup"><span data-stu-id="3b735-120">This article assumes that you have the following resources:</span></span>

- <span data-ttu-id="3b735-121">Een exemplaar van netwerk-Watcher in de regio die u wilt maken van een pakketopname</span><span class="sxs-lookup"><span data-stu-id="3b735-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="3b735-122">Een virtuele machine met de pakket-capture-extensie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3b735-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b735-123">Pakketopname vereist dat de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="3b735-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="3b735-124">Voor het installeren van de extensie op een Windows-virtuele machine gaat u naar [extensie voor het virtuele machine voor Windows Azure-netwerk-Watcher Agent](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="3b735-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-the-portal"></a><span data-ttu-id="3b735-125">Pakket vastleggen agent uitbreiding via de portal</span><span class="sxs-lookup"><span data-stu-id="3b735-125">Packet Capture agent extension through the portal</span></span>

<span data-ttu-id="3b735-126">Voor het installeren van het pakket vastleggen VM-agent via de portal, gaat u naar de virtuele machine, klikt u op **extensies** > **toevoegen** en zoek naar **netwerk-Watcher-Agent voor Windows**</span><span class="sxs-lookup"><span data-stu-id="3b735-126">To install the packet capture VM agent through the portal, navigate to your virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Agent weergeven][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="3b735-128">Overzicht van pakket vastleggen</span><span class="sxs-lookup"><span data-stu-id="3b735-128">Packet Capture overview</span></span>

<span data-ttu-id="3b735-129">Navigeer naar de [Azure-portal](https://portal.azure.com) en klik op **Networking** > **netwerk-Watcher** > **pakket vastleggen**</span><span class="sxs-lookup"><span data-stu-id="3b735-129">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="3b735-130">De overzichtspagina ziet u een lijst met alle pakketten die bestaan ongeacht de status vastlegt.</span><span class="sxs-lookup"><span data-stu-id="3b735-130">The overview page shows a list of all packet captures that exist no matter the state.</span></span>

> [!NOTE]
> <span data-ttu-id="3b735-131">Pakketopname vereist connectiviteit met de storage-account via poort 443.</span><span class="sxs-lookup"><span data-stu-id="3b735-131">Packet capture requires connectivity to the storage account over port 443.</span></span>

![scherm overzicht van pakket vastleggen][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="3b735-133">Start een pakketopname</span><span class="sxs-lookup"><span data-stu-id="3b735-133">Start a packet capture</span></span>

<span data-ttu-id="3b735-134">Klik op **toevoegen** een pakketopname maken.</span><span class="sxs-lookup"><span data-stu-id="3b735-134">Click **Add** to create a packet capture.</span></span>

<span data-ttu-id="3b735-135">De eigenschappen die kunnen worden gedefinieerd op een pakketopname zijn:</span><span class="sxs-lookup"><span data-stu-id="3b735-135">The properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="3b735-136">**Belangrijkste instellingen**</span><span class="sxs-lookup"><span data-stu-id="3b735-136">**Main settings**</span></span>

- <span data-ttu-id="3b735-137">**Abonnement** -deze waarde is het abonnement dat wordt gebruikt, een exemplaar van netwerk-watcher nodig is in elk abonnement.</span><span class="sxs-lookup"><span data-stu-id="3b735-137">**Subscription** - This value is the subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="3b735-138">**Resourcegroep** -de resourcegroep van de virtuele machine die wordt benaderd.</span><span class="sxs-lookup"><span data-stu-id="3b735-138">**Resource group** - The resource group of the virtual machine that is being targeted.</span></span>
- <span data-ttu-id="3b735-139">**Virtuele machine als doel** -de virtuele machine die wordt uitgevoerd de pakketopname</span><span class="sxs-lookup"><span data-stu-id="3b735-139">**Target virtual machine** - The virtual machine that is running the packet capture</span></span>
- <span data-ttu-id="3b735-140">**Pakketnaam vastleggen** -deze waarde is de naam van het pakket vastleggen.</span><span class="sxs-lookup"><span data-stu-id="3b735-140">**Packet capture name** - This value is the name of the packet capture.</span></span>

<span data-ttu-id="3b735-141">**Configuratie vastleggen**</span><span class="sxs-lookup"><span data-stu-id="3b735-141">**Capture configuration**</span></span>

- <span data-ttu-id="3b735-142">**Storage-Account** -bepaalt als pakketopname wordt opgeslagen in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3b735-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="3b735-143">**Bestand** -bepaalt als een pakketopname lokaal wordt opgeslagen op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3b735-143">**File** - Determines if a packet capture is saved locally on the virtual machine.</span></span>
- <span data-ttu-id="3b735-144">**Storage-Accounts** : de storage-account op te slaan van het pakket vastleggen in geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="3b735-144">**Storage Accounts** - The selected storage account to save the packet capture in.</span></span> <span data-ttu-id="3b735-145">Standaardlocatie is https://{storage-account-id name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription} /resourcegroups/ {name}/providers/microsoft.compute/virtualmachines/{virtual machine Resourcegroepnaam} / {jj} / {MM} / {DD} / {HH} packetcapture__{MM}_{SS} _ {XXX} Cap.</span><span class="sxs-lookup"><span data-stu-id="3b735-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="3b735-146">(Alleen beschikbaar als **opslag** is geselecteerd)</span><span class="sxs-lookup"><span data-stu-id="3b735-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="3b735-147">**Lokale bestandspad** -het lokale pad op een virtuele machine op te slaan van het vastleggen van het pakket.</span><span class="sxs-lookup"><span data-stu-id="3b735-147">**Local file path** - The local path on a virtual machine to save the packet capture.</span></span> <span data-ttu-id="3b735-148">(Alleen beschikbaar als **bestand** is ingeschakeld).</span><span class="sxs-lookup"><span data-stu-id="3b735-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="3b735-149">Een geldig pad moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3b735-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="3b735-150">**Maximum aantal bytes per pakket** - het aantal bytes van elk pakket die zijn vastgelegd, alle bytes zijn vastgelegd als leeg is.</span><span class="sxs-lookup"><span data-stu-id="3b735-150">**Maximum bytes per packet** - The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="3b735-151">**Maximum aantal bytes per sessie** - totaal aantal bytes die zijn vastgelegd, zodra het pakket vastleggen gestopt door de waarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="3b735-151">**Maximum bytes per session** - Total number of bytes that are captured, once the value is reached the packet capture stops.</span></span>
- <span data-ttu-id="3b735-152">**Tijdslimiet (seconden)** -bepaalt de tijdslimiet voor de pakketopname te stoppen.</span><span class="sxs-lookup"><span data-stu-id="3b735-152">**Time limit (seconds)** - Sets a time limit for the packet capture to stop.</span></span> <span data-ttu-id="3b735-153">Standaard is 18000 seconden.</span><span class="sxs-lookup"><span data-stu-id="3b735-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="3b735-154">Premium storage-accounts worden momenteel niet ondersteund voor opslag van pakket worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="3b735-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="3b735-155">**Filteren (optioneel)**</span><span class="sxs-lookup"><span data-stu-id="3b735-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="3b735-156">**Protocol** -het protocol voor het filteren van voor het vastleggen van het pakket.</span><span class="sxs-lookup"><span data-stu-id="3b735-156">**Protocol** - The protocol to filter for the packet capture.</span></span> <span data-ttu-id="3b735-157">De beschikbare waarden zijn TCP, UDP en alle.</span><span class="sxs-lookup"><span data-stu-id="3b735-157">The available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="3b735-158">**Lokaal IP-adres** -deze waarde filtert de pakketopname voor de pakketten waar het lokale IP-adres overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="3b735-158">**Local IP address** - This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>
- <span data-ttu-id="3b735-159">**Lokale poort** -deze waarde filtert de pakketopname om pakketten van de lokale poort overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="3b735-159">**Local port** - This value filters the packet capture to packets where the local port matches this filter value.</span></span>
- <span data-ttu-id="3b735-160">**Extern IP-adres** -deze waarde filtert de pakketopname voor de pakketten waar het externe IP-adres overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="3b735-160">**Remote IP address** - This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>
- <span data-ttu-id="3b735-161">**Externe poort** -deze waarde filtert de pakketopname pakketten waarbij de externe poort overeenkomt met de waarde voor dit filter.</span><span class="sxs-lookup"><span data-stu-id="3b735-161">**Remote port** - This value filters the packet capture to packets where the remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="3b735-162">Poort en IP-adres-waarden mag geen enkele waarde, bereik van waarden of een set.</span><span class="sxs-lookup"><span data-stu-id="3b735-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="3b735-163">(dat wil zeggen, 80-1024 voor poort) U kunt filters die u wilt definiëren.</span><span class="sxs-lookup"><span data-stu-id="3b735-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="3b735-164">Nadat u de waarden zijn ingevuld, klikt u op **OK** de pakketopname maken.</span><span class="sxs-lookup"><span data-stu-id="3b735-164">Once the values are filled out, click **OK** to create the packet capture.</span></span>

![maken van een pakketopname][2]

<span data-ttu-id="3b735-166">Nadat de tijdslimiet ingesteld voor het vastleggen van het pakket is verlopen, wordt de vastlegging van het pakket wordt gestopt en kan worden gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="3b735-166">After the time limit set on the packet capture has expired, the packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="3b735-167">U kunt ook handmatig de opnamen pakket sessies stoppen.</span><span class="sxs-lookup"><span data-stu-id="3b735-167">You can also manually stop the packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="3b735-168">Het vastleggen van een pakket verwijderen</span><span class="sxs-lookup"><span data-stu-id="3b735-168">Delete a packet capture</span></span>

<span data-ttu-id="3b735-169">Klik in de weergave van de capture pakket op de **contextmenu** (...) of klik met de rechtermuisknop en klikt u op **verwijderen** de pakketopname stoppen</span><span class="sxs-lookup"><span data-stu-id="3b735-169">In the packet capture view, click the **context menu** (...) or right click, and click **delete** to stop the packet capture</span></span>

![Het vastleggen van een pakket verwijderen][3]

> [!NOTE]
> <span data-ttu-id="3b735-171">Als u het vastleggen van een pakket verwijdert, verwijdert niet het bestand in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3b735-171">Deleting a packet capture does not delete the file in the storage account.</span></span>

<span data-ttu-id="3b735-172">U wordt gevraagd om te bevestigen dat u wilt de pakketopname verwijderen, klikt u op **Ja**</span><span class="sxs-lookup"><span data-stu-id="3b735-172">You are asked to confirm you want to delete the packet capture, click **Yes**</span></span>

![Bevestiging][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="3b735-174">Stop de pakketopname van een</span><span class="sxs-lookup"><span data-stu-id="3b735-174">Stop a packet capture</span></span>

<span data-ttu-id="3b735-175">Klik in de weergave van de capture pakket op de **contextmenu** (...) of klik met de rechtermuisknop en klikt u op **stoppen** de pakketopname stoppen</span><span class="sxs-lookup"><span data-stu-id="3b735-175">In the packet capture view, click the **context menu** (...) or right click, and click **Stop** to stop the packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="3b735-176">Een pakketopname downloaden</span><span class="sxs-lookup"><span data-stu-id="3b735-176">Download a packet capture</span></span>

<span data-ttu-id="3b735-177">Zodra de sessie van uw pakket vastleggen is voltooid, wordt de capture-bestand wordt geüpload naar blob-opslag of naar een lokaal bestand op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3b735-177">Once your packet capture session has completed, the capture file is uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="3b735-178">De opslaglocatie van de pakketopname is gedefinieerd bij het maken van de sessie.</span><span class="sxs-lookup"><span data-stu-id="3b735-178">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="3b735-179">Een handig hulpmiddel voor toegang tot deze capture-bestanden opgeslagen in een opslagaccount is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="3b735-179">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="3b735-180">Als een opslagaccount is opgegeven, worden bestanden voor pakket worden opgeslagen in een opslagaccount op de volgende locatie:</span><span class="sxs-lookup"><span data-stu-id="3b735-180">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="3b735-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b735-181">Next steps</span></span>

<span data-ttu-id="3b735-182">Meer informatie over het automatiseren van pakket opnamen met waarschuwingen van de virtuele machine met weer te geven [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="3b735-182">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="3b735-183">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3b735-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













