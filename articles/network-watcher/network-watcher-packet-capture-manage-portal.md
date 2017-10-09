---
title: aaaManage pakket worden vastgelegd met Azure-netwerk-Watcher - Azure-portal | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toomanage Hallo pakket vastleggen functie van netwerk-Watcher met Azure portal
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
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="c7768-103">Pakket opnamen beheren met Azure met behulp van de portal Hallo netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="c7768-103">Manage packet captures with Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c7768-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c7768-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="c7768-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7768-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="c7768-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c7768-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="c7768-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c7768-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="c7768-108">Azure REST-API</span><span class="sxs-lookup"><span data-stu-id="c7768-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="c7768-109">Netwerk-Watcher pakketopname kunt u toocreate vastleggen sessies tootrack verkeer tooand van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c7768-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="c7768-110">Filters zijn beschikbaar voor Hallo vastleggen sessie tooensure dat u alleen Hallo verkeer die u wilt vastleggen.</span><span class="sxs-lookup"><span data-stu-id="c7768-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="c7768-111">Pakketopname helpt toodiagnose netwerk afwijkingen reactief en proactief.</span><span class="sxs-lookup"><span data-stu-id="c7768-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="c7768-112">Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="c7768-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="c7768-113">Deze mogelijkheid vergemakkelijkt door kunnen tooremotely trigger pakket opnamen, Hallo last van een pakketopname handmatig en op de gewenste machine hello, die kostbare tijd bespaart worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c7768-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="c7768-114">In dit artikel leert u Hallo verschillende beheertaken uitvoeren die momenteel beschikbaar zijn voor pakketopname.</span><span class="sxs-lookup"><span data-stu-id="c7768-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="c7768-115">**Start een pakketopname**</span><span class="sxs-lookup"><span data-stu-id="c7768-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="c7768-116">**Stop de pakketopname van een**</span><span class="sxs-lookup"><span data-stu-id="c7768-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="c7768-117">**Het vastleggen van een pakket verwijderen**</span><span class="sxs-lookup"><span data-stu-id="c7768-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="c7768-118">**Een pakketopname downloaden**</span><span class="sxs-lookup"><span data-stu-id="c7768-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="c7768-119">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="c7768-119">Before you begin</span></span>

<span data-ttu-id="c7768-120">In dit artikel wordt ervan uitgegaan dat u hebt Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7768-120">This article assumes that you have hello following resources:</span></span>

- <span data-ttu-id="c7768-121">Een exemplaar van netwerk-Watcher in Hallo regio die u wilt een pakketopname toocreate</span><span class="sxs-lookup"><span data-stu-id="c7768-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="c7768-122">Een virtuele machine met hello-pakket vastleggen uitbreiding ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c7768-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7768-123">Pakketopname vereist dat de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="c7768-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="c7768-124">Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="c7768-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-hello-portal"></a><span data-ttu-id="c7768-125">Pakket vastleggen agent uitbreiding via Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="c7768-125">Packet Capture agent extension through hello portal</span></span>

<span data-ttu-id="c7768-126">tooinstall hello pakketopname VM-agent via Hallo-portal, gaat u tooyour virtuele machine, klikt u op **extensies** > **toevoegen** en zoek naar **netwerk-Watcher-Agent voor Windows**</span><span class="sxs-lookup"><span data-stu-id="c7768-126">tooinstall hello packet capture VM agent through hello portal, navigate tooyour virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Agent weergeven][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="c7768-128">Overzicht van pakket vastleggen</span><span class="sxs-lookup"><span data-stu-id="c7768-128">Packet Capture overview</span></span>

<span data-ttu-id="c7768-129">Navigeer toohello [Azure-portal](https://portal.azure.com) en klik op **Networking** > **netwerk-Watcher** > **pakket vastleggen**</span><span class="sxs-lookup"><span data-stu-id="c7768-129">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="c7768-130">Hallo overzichtspagina bevat een lijst met alle pakketten die bestaan ongeacht Hallo status vastlegt.</span><span class="sxs-lookup"><span data-stu-id="c7768-130">hello overview page shows a list of all packet captures that exist no matter hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="c7768-131">Pakketopname vereist connectiviteit toohello storage-account via poort 443.</span><span class="sxs-lookup"><span data-stu-id="c7768-131">Packet capture requires connectivity toohello storage account over port 443.</span></span>

![scherm overzicht van pakket vastleggen][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="c7768-133">Start een pakketopname</span><span class="sxs-lookup"><span data-stu-id="c7768-133">Start a packet capture</span></span>

<span data-ttu-id="c7768-134">Klik op **toevoegen** toocreate een pakketopname.</span><span class="sxs-lookup"><span data-stu-id="c7768-134">Click **Add** toocreate a packet capture.</span></span>

<span data-ttu-id="c7768-135">Hallo-eigenschappen die kunnen worden gedefinieerd op een pakketopname zijn:</span><span class="sxs-lookup"><span data-stu-id="c7768-135">hello properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="c7768-136">**Belangrijkste instellingen**</span><span class="sxs-lookup"><span data-stu-id="c7768-136">**Main settings**</span></span>

- <span data-ttu-id="c7768-137">**Abonnement** -deze waarde is Hallo-abonnement dat wordt gebruikt, een exemplaar van netwerk-watcher nodig is in elk abonnement.</span><span class="sxs-lookup"><span data-stu-id="c7768-137">**Subscription** - This value is hello subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="c7768-138">**Resourcegroep** -Hallo brongroep van Hallo virtuele machine die wordt benaderd.</span><span class="sxs-lookup"><span data-stu-id="c7768-138">**Resource group** - hello resource group of hello virtual machine that is being targeted.</span></span>
- <span data-ttu-id="c7768-139">**Virtuele machine als doel** -Hallo virtuele machine die wordt uitgevoerd Hallo pakketopname</span><span class="sxs-lookup"><span data-stu-id="c7768-139">**Target virtual machine** - hello virtual machine that is running hello packet capture</span></span>
- <span data-ttu-id="c7768-140">**Pakketnaam vastleggen** -deze waarde is de naam Hallo van Hallo pakketopname.</span><span class="sxs-lookup"><span data-stu-id="c7768-140">**Packet capture name** - This value is hello name of hello packet capture.</span></span>

<span data-ttu-id="c7768-141">**Configuratie vastleggen**</span><span class="sxs-lookup"><span data-stu-id="c7768-141">**Capture configuration**</span></span>

- <span data-ttu-id="c7768-142">**Storage-Account** -bepaalt als pakketopname wordt opgeslagen in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c7768-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="c7768-143">**Bestand** -bepaalt als een pakketopname lokaal wordt opgeslagen op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c7768-143">**File** - Determines if a packet capture is saved locally on hello virtual machine.</span></span>
- <span data-ttu-id="c7768-144">**Storage-Accounts** -Hallo storage account toosave hello pakketopname in geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c7768-144">**Storage Accounts** - hello selected storage account toosave hello packet capture in.</span></span> <span data-ttu-id="c7768-145">Standaardlocatie is https://{storage-account-id name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription} /resourcegroups/ {name}/providers/microsoft.compute/virtualmachines/{virtual machine Resourcegroepnaam} / {jj} / {MM} / {DD} / {HH} packetcapture__{MM}_{SS} _ {XXX} Cap.</span><span class="sxs-lookup"><span data-stu-id="c7768-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="c7768-146">(Alleen beschikbaar als **opslag** is geselecteerd)</span><span class="sxs-lookup"><span data-stu-id="c7768-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="c7768-147">**Lokale bestandspad** -Hallo lokaal pad op een virtuele machine toosave Hallo-pakketopname.</span><span class="sxs-lookup"><span data-stu-id="c7768-147">**Local file path** - hello local path on a virtual machine toosave hello packet capture.</span></span> <span data-ttu-id="c7768-148">(Alleen beschikbaar als **bestand** is ingeschakeld).</span><span class="sxs-lookup"><span data-stu-id="c7768-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="c7768-149">Een geldig pad moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c7768-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="c7768-150">**Maximum aantal bytes per pakket** -Hallo aantal bytes van elk pakket die zijn vastgelegd, alle bytes zijn vastgelegd als leeg is.</span><span class="sxs-lookup"><span data-stu-id="c7768-150">**Maximum bytes per packet** - hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="c7768-151">**Maximum aantal bytes per sessie** - totaal aantal bytes die worden vastgelegd als waarde Hallo Hallo pakket vastleggen stopt is bereikt.</span><span class="sxs-lookup"><span data-stu-id="c7768-151">**Maximum bytes per session** - Total number of bytes that are captured, once hello value is reached hello packet capture stops.</span></span>
- <span data-ttu-id="c7768-152">**Tijdslimiet (seconden)** -bepaalt de tijdslimiet voor Hallo pakket vastleggen toostop.</span><span class="sxs-lookup"><span data-stu-id="c7768-152">**Time limit (seconds)** - Sets a time limit for hello packet capture toostop.</span></span> <span data-ttu-id="c7768-153">Standaard is 18000 seconden.</span><span class="sxs-lookup"><span data-stu-id="c7768-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="c7768-154">Premium storage-accounts worden momenteel niet ondersteund voor opslag van pakket worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="c7768-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="c7768-155">**Filteren (optioneel)**</span><span class="sxs-lookup"><span data-stu-id="c7768-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="c7768-156">**Protocol** -protocol toofilter voor pakketopname Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7768-156">**Protocol** - hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="c7768-157">Hallo beschikbare waarden zijn TCP, UDP en alle.</span><span class="sxs-lookup"><span data-stu-id="c7768-157">hello available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="c7768-158">**Lokaal IP-adres** -deze waarde filtert Hallo pakket vastleggen toopackets Hallo lokale IP-adres overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="c7768-158">**Local IP address** - This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>
- <span data-ttu-id="c7768-159">**Lokale poort** -deze waarde filtert Hallo pakket vastleggen toopackets Hallo lokale poort overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="c7768-159">**Local port** - This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>
- <span data-ttu-id="c7768-160">**Extern IP-adres** -deze waarde filtert Hallo pakket vastleggen toopackets Hallo externe IP overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="c7768-160">**Remote IP address** - This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>
- <span data-ttu-id="c7768-161">**Externe poort** -deze waarde filtert Hallo pakket vastleggen toopackets Hallo externe poort overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="c7768-161">**Remote port** - This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="c7768-162">Poort en IP-adres-waarden mag geen enkele waarde, bereik van waarden of een set.</span><span class="sxs-lookup"><span data-stu-id="c7768-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="c7768-163">(dat wil zeggen, 80-1024 voor poort) U kunt filters die u wilt definiëren.</span><span class="sxs-lookup"><span data-stu-id="c7768-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="c7768-164">Zodra het Hallo-waarden zijn ingevuld, klikt u op **OK** toocreate hello pakketopname.</span><span class="sxs-lookup"><span data-stu-id="c7768-164">Once hello values are filled out, click **OK** toocreate hello packet capture.</span></span>

![maken van een pakketopname][2]

<span data-ttu-id="c7768-166">Nadat de tijdslimiet Hallo ingesteld op Hallo pakketopname is verlopen, Hallo pakketopname stopt en kan worden gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="c7768-166">After hello time limit set on hello packet capture has expired, hello packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="c7768-167">U kunt ook handmatig Hallo pakket opnamen sessies stoppen.</span><span class="sxs-lookup"><span data-stu-id="c7768-167">You can also manually stop hello packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="c7768-168">Het vastleggen van een pakket verwijderen</span><span class="sxs-lookup"><span data-stu-id="c7768-168">Delete a packet capture</span></span>

<span data-ttu-id="c7768-169">Vastleggen in Hallo pakket weergeven, klikt u op Hallo **contextmenu** (...) of klik met de rechtermuisknop en klikt u op **verwijderen** toostop hello pakketopname</span><span class="sxs-lookup"><span data-stu-id="c7768-169">In hello packet capture view, click hello **context menu** (...) or right click, and click **delete** toostop hello packet capture</span></span>

![Het vastleggen van een pakket verwijderen][3]

> [!NOTE]
> <span data-ttu-id="c7768-171">Als een pakketopname, verwijdert Hallo-bestand in Hallo storage-account niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c7768-171">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

<span data-ttu-id="c7768-172">U wordt gevraagd tooconfirm gewenste toodelete hello pakketopname, klikt u op **Ja**</span><span class="sxs-lookup"><span data-stu-id="c7768-172">You are asked tooconfirm you want toodelete hello packet capture, click **Yes**</span></span>

![Bevestiging][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="c7768-174">Stop de pakketopname van een</span><span class="sxs-lookup"><span data-stu-id="c7768-174">Stop a packet capture</span></span>

<span data-ttu-id="c7768-175">Vastleggen in Hallo pakket weergeven, klikt u op Hallo **contextmenu** (...) of klik met de rechtermuisknop en klikt u op **stoppen** toostop hello pakketopname</span><span class="sxs-lookup"><span data-stu-id="c7768-175">In hello packet capture view, click hello **context menu** (...) or right click, and click **Stop** toostop hello packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="c7768-176">Een pakketopname downloaden</span><span class="sxs-lookup"><span data-stu-id="c7768-176">Download a packet capture</span></span>

<span data-ttu-id="c7768-177">Zodra de sessie van uw pakket vastleggen is voltooid, Hallo vastleggen bestand is geüpload tooblob opslag of tooa lokale op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="c7768-177">Once your packet capture session has completed, hello capture file is uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="c7768-178">Hallo-opslaglocatie van Hallo pakketopname is gedefinieerd bij het maken van Hallo-sessie.</span><span class="sxs-lookup"><span data-stu-id="c7768-178">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="c7768-179">Een handig hulpmiddel tooaccess deze bestanden vastleggen, opgeslagen tooa storage-account is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="c7768-179">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="c7768-180">Als een opslagaccount is opgegeven, worden bestanden voor pakket tooa storage-account op Hallo na locatie opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="c7768-180">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="c7768-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7768-181">Next steps</span></span>

<span data-ttu-id="c7768-182">Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="c7768-182">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="c7768-183">Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c7768-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













