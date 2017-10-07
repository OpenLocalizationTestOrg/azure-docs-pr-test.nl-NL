---
title: 'aaaTroubleshoot Azure Virtual Network Gateway en verbindingen: Azure CLI 2.0 | Microsoft Docs'
description: Deze pagina wordt uitgelegd hoe de Azure CLI 2.0 voor het oplossen van toouse hello Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 389e86f247722412a1d0e2e722dbf80bb7cff291
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a>Problemen met virtuele netwerkgateway en verbindingen met behulp van Azure-netwerk-Watcher Azure CLI 2.0

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

Netwerk-Watcher biedt veel mogelijkheden met betrekking toounderstanding uw netwerkbronnen in Azure. Een van deze mogelijkheden resource is het oplossen van problemen. Het oplossen van bron kan worden aangeroepen via Hallo-portal, PowerShell, CLI of REST-API. Als deze wordt aangeroepen, netwerk-Watcher Hallo status van de Gateway van een virtueel netwerk of een verbinding inspecteert en retourneert de bevindingen zijn.

In dit artikel gebruikt de volgende generatie CLI voor Hallo resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.

tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Voordat u begint

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.

Voor een lijst met ondersteunde gateway typen bezoek, [ondersteund gatewaytypen](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Overzicht

Het oplossen van resource biedt Hallo mogelijkheid oplossen van problemen die zich bij het virtuele netwerkgateways en verbindingen voordoen. Wanneer een aanvraag wordt gedaan tooresource probleemoplossing, logboeken worden opgevraagd en geïnspecteerd. Als controle voltooid is, worden Hallo resultaten geretourneerd. Resources voor probleemoplossing aanvragen zijn langlopende aanvragen die meerdere minuten tooreturn een resultaat kan krijgen. Hallo-logboeken van het oplossen van problemen worden opgeslagen in een container voor een opslagaccount die is opgegeven.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>De gatewayverbinding van een virtueel netwerk ophalen

In dit voorbeeld is het oplossen van resource wordt uitgevoerd op een verbinding. U kunt ook gebruikmaakt van een virtuele netwerkgateway. Hallo volgende cmdlet geeft een lijst Hallo vpn-verbindingen in een resourcegroep.

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

Zodra u Hallo-naam van Hallo verbinding hebt, kunt u deze opdracht tooget uitvoeren de resource-Id:

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a>Een opslagaccount maken

Gegevens over de status Hallo van Hallo resource resource probleemoplossing retourneert, Bovendien bespaart u Logboeken tooa storage account toobe gecontroleerd. In deze stap, maken we een opslagaccount, als een bestaand opslagaccount bestaat kunt u deze kunt gebruiken.

1. Hallo storage-account maken

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. Hallo opslagaccountsleutels ophalen

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. Hallo-container maken

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Netwerk-Watcher resource voor probleemoplossing uitvoert

Oplossen van resources met Hallo `az network watcher troubleshooting` cmdlet. Geven we Hallo cmdlet Hallo resourcegroep, hello naam Hallo netwerk-Watcher Hallo-Id van het Hallo-verbinding, Hallo Hallo storage-account-Id en Hallo pad toohello blob toostore Hallo oplossen resulteert in.

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

Zodra u de cmdlet Hallo uitgevoerd, controleert de netwerk-Watcher tooverify Hallo-Hallo resourcestatus. Het resultaat Hallo toohello shell en slaat logboeken van de resultaten van Hallo in Hallo storage-account opgegeven.

## <a name="understanding-hello-results"></a>Understanding Hallo resultaten

Hallo actietekst bevat algemene richtlijnen over hoe tooresolve probleem Hallo. Als een actie kan worden ondernomen voor Hallo probleem, wordt een koppeling geboden met aanvullende richtlijnen. In geval van Hallo wanneer er geen aanvullende richtlijnen, antwoord Hallo biedt Hallo url tooopen een ondersteuningsaanvraag.  Voor meer informatie over het Hallo-eigenschappen van antwoord Hallo en wat is opgenomen, gaat u naar [overzicht van netwerk-Watcher oplossen](network-watcher-troubleshoot-overview.md)

Voor instructies over het downloaden van bestanden van azure storage-accounts, Raadpleeg te[aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer. Meer informatie over Opslagverkenner vindt u hier op Hallo koppeling: [Opslagverkenner](http://storageexplorer.com/)

## <a name="next-steps"></a>Volgende stappen

Als de instellingen zijn gewijzigd die stop VPN-verbindingen, raadpleegt u [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.
