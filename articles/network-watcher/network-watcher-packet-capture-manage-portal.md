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
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a>Pakket opnamen beheren met Azure met behulp van de portal Hallo netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST-API](network-watcher-packet-capture-manage-rest.md)

Netwerk-Watcher pakketopname kunt u toocreate vastleggen sessies tootrack verkeer tooand van een virtuele machine. Filters zijn beschikbaar voor Hallo vastleggen sessie tooensure dat u alleen Hallo verkeer die u wilt vastleggen. Pakketopname helpt toodiagnose netwerk afwijkingen reactief en proactief. Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer. Deze mogelijkheid vergemakkelijkt door kunnen tooremotely trigger pakket opnamen, Hallo last van een pakketopname handmatig en op de gewenste machine hello, die kostbare tijd bespaart worden uitgevoerd.

In dit artikel leert u Hallo verschillende beheertaken uitvoeren die momenteel beschikbaar zijn voor pakketopname.

- [**Start een pakketopname**](#start-a-packet-capture)
- [**Stop de pakketopname van een**](#stop-a-packet-capture)
- [**Het vastleggen van een pakket verwijderen**](#delete-a-packet-capture)
- [**Een pakketopname downloaden**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Voordat u begint

In dit artikel wordt ervan uitgegaan dat u hebt Hallo resources te volgen:

- Een exemplaar van netwerk-Watcher in Hallo regio die u wilt een pakketopname toocreate
- Een virtuele machine met hello-pakket vastleggen uitbreiding ingeschakeld.

> [!IMPORTANT]
> Pakketopname vereist dat de extensie van een virtuele machine `AzureNetworkWatcherExtension`. Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).

### <a name="packet-capture-agent-extension-through-hello-portal"></a>Pakket vastleggen agent uitbreiding via Hallo-portal

tooinstall hello pakketopname VM-agent via Hallo-portal, gaat u tooyour virtuele machine, klikt u op **extensies** > **toevoegen** en zoek naar **netwerk-Watcher-Agent voor Windows**

![Agent weergeven][agent]

## <a name="packet-capture-overview"></a>Overzicht van pakket vastleggen

Navigeer toohello [Azure-portal](https://portal.azure.com) en klik op **Networking** > **netwerk-Watcher** > **pakket vastleggen**

Hallo overzichtspagina bevat een lijst met alle pakketten die bestaan ongeacht Hallo status vastlegt.

> [!NOTE]
> Pakketopname vereist connectiviteit toohello storage-account via poort 443.

![scherm overzicht van pakket vastleggen][1]

## <a name="start-a-packet-capture"></a>Start een pakketopname

Klik op **toevoegen** toocreate een pakketopname.

Hallo-eigenschappen die kunnen worden gedefinieerd op een pakketopname zijn:

**Belangrijkste instellingen**

- **Abonnement** -deze waarde is Hallo-abonnement dat wordt gebruikt, een exemplaar van netwerk-watcher nodig is in elk abonnement.
- **Resourcegroep** -Hallo brongroep van Hallo virtuele machine die wordt benaderd.
- **Virtuele machine als doel** -Hallo virtuele machine die wordt uitgevoerd Hallo pakketopname
- **Pakketnaam vastleggen** -deze waarde is de naam Hallo van Hallo pakketopname.

**Configuratie vastleggen**

- **Storage-Account** -bepaalt als pakketopname wordt opgeslagen in een opslagaccount.
- **Bestand** -bepaalt als een pakketopname lokaal wordt opgeslagen op Hallo virtuele machine.
- **Storage-Accounts** -Hallo storage account toosave hello pakketopname in geselecteerd. Standaardlocatie is https://{storage-account-id name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription} /resourcegroups/ {name}/providers/microsoft.compute/virtualmachines/{virtual machine Resourcegroepnaam} / {jj} / {MM} / {DD} / {HH} packetcapture__{MM}_{SS} _ {XXX} Cap. (Alleen beschikbaar als **opslag** is geselecteerd)
- **Lokale bestandspad** -Hallo lokaal pad op een virtuele machine toosave Hallo-pakketopname. (Alleen beschikbaar als **bestand** is ingeschakeld). Een geldig pad moet worden opgegeven.
- **Maximum aantal bytes per pakket** -Hallo aantal bytes van elk pakket die zijn vastgelegd, alle bytes zijn vastgelegd als leeg is.
- **Maximum aantal bytes per sessie** - totaal aantal bytes die worden vastgelegd als waarde Hallo Hallo pakket vastleggen stopt is bereikt.
- **Tijdslimiet (seconden)** -bepaalt de tijdslimiet voor Hallo pakket vastleggen toostop. Standaard is 18000 seconden.

> [!NOTE]
> Premium storage-accounts worden momenteel niet ondersteund voor opslag van pakket worden vastgelegd.

**Filteren (optioneel)**

- **Protocol** -protocol toofilter voor pakketopname Hallo Hallo. Hallo beschikbare waarden zijn TCP, UDP en alle.
- **Lokaal IP-adres** -deze waarde filtert Hallo pakket vastleggen toopackets Hallo lokale IP-adres overeenkomt met de filterwaarde van dit.
- **Lokale poort** -deze waarde filtert Hallo pakket vastleggen toopackets Hallo lokale poort overeenkomt met de filterwaarde van dit.
- **Extern IP-adres** -deze waarde filtert Hallo pakket vastleggen toopackets Hallo externe IP overeenkomt met de filterwaarde van dit.
- **Externe poort** -deze waarde filtert Hallo pakket vastleggen toopackets Hallo externe poort overeenkomt met de filterwaarde van dit.

> [!NOTE]
> Poort en IP-adres-waarden mag geen enkele waarde, bereik van waarden of een set. (dat wil zeggen, 80-1024 voor poort) U kunt filters die u wilt definiëren.

Zodra het Hallo-waarden zijn ingevuld, klikt u op **OK** toocreate hello pakketopname.

![maken van een pakketopname][2]

Nadat de tijdslimiet Hallo ingesteld op Hallo pakketopname is verlopen, Hallo pakketopname stopt en kan worden gecontroleerd. U kunt ook handmatig Hallo pakket opnamen sessies stoppen.

## <a name="delete-a-packet-capture"></a>Het vastleggen van een pakket verwijderen

Vastleggen in Hallo pakket weergeven, klikt u op Hallo **contextmenu** (...) of klik met de rechtermuisknop en klikt u op **verwijderen** toostop hello pakketopname

![Het vastleggen van een pakket verwijderen][3]

> [!NOTE]
> Als een pakketopname, verwijdert Hallo-bestand in Hallo storage-account niet verwijderd.

U wordt gevraagd tooconfirm gewenste toodelete hello pakketopname, klikt u op **Ja**

![Bevestiging][4]

## <a name="stop-a-packet-capture"></a>Stop de pakketopname van een

Vastleggen in Hallo pakket weergeven, klikt u op Hallo **contextmenu** (...) of klik met de rechtermuisknop en klikt u op **stoppen** toostop hello pakketopname

## <a name="download-a-packet-capture"></a>Een pakketopname downloaden

Zodra de sessie van uw pakket vastleggen is voltooid, Hallo vastleggen bestand is geüpload tooblob opslag of tooa lokale op Hallo VM. Hallo-opslaglocatie van Hallo pakketopname is gedefinieerd bij het maken van Hallo-sessie. Een handig hulpmiddel tooaccess deze bestanden vastleggen, opgeslagen tooa storage-account is Microsoft Azure Storage Explorer, die u kunt hier downloaden: http://storageexplorer.com/

Als een opslagaccount is opgegeven, worden bestanden voor pakket tooa storage-account op Hallo na locatie opgeslagen:
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooautomate pakket worden vastgelegd met waarschuwingen van de virtuele machine door [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)

Als bepaalde verkeer is toegestaan in of buiten uw virtuele machine in via vinden [controleren IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













