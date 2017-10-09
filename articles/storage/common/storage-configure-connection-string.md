---
title: aaaConfigure een verbindingsreeks voor Azure Storage | Microsoft Docs
description: Configureer een verbindingsreeks voor Azure storage-account. Een verbindingsreeks bevat Hallo informatie nodig tooauthenticate toegang krijgen tot tooa storage-account van uw toepassing tijdens runtime.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: ac1d7d9bf11fa6f44243cda0c40d8faee12e513b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a>Azure Storage-verbindingsreeksen configureren

Een verbindingsreeks bevat Hallo verificatie-informatie is vereist voor uw toepassing tooaccess gegevens in een Azure Storage-account tijdens runtime. U kunt de verbindingsreeksen om te configureren:

* Verbinding maken met Azure-opslagemulator toohello.
* Toegang tot een opslagaccount in Azure.
* Toegang tot de opgegeven resources in Azure via een shared access signature (SAS).

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>Opslaan van de verbindingsreeks
Uw toepassing moet tooaccess Hallo-verbindingsreeks in runtime tooauthenticate aanvragen tooAzure opslag. U hebt verschillende mogelijkheden voor het opslaan van de verbindingsreeks:

* Hallo-verbindingsreeks in kan worden opgeslagen in een toepassing wordt uitgevoerd op Hallo bureaublad of op een apparaat een **app.config** of **web.config** bestand. Toevoegen van Hallo connection string toohello **AppSettings** sectie in deze bestanden.
* Een toepassing die wordt uitgevoerd in een Azure cloudservice Hallo verbindingsreeks kunt opslaan in Hallo [Azure-service-configuratiebestand (.cscfg) schema](https://msdn.microsoft.com/library/ee758710.aspx). Toevoegen van Hallo connection string toohello **ConfigurationSettings** gedeelte van configuratiebestand Hallo-service.
* Rechtstreeks in uw code kunt u de verbindingsreeks. We raden echter aan de verbindingsreeks op te slaan in een configuratiebestand in de meeste scenario's.

De verbindingstekenreeks opslaan in een configuratiebestand maakt het eenvoudig tooupdate Hallo connection string tooswitch tussen Hallo opslagemulator en een Azure storage-account in de cloud Hallo. U hoeft alleen tooedit Hallo connection string toopoint tooyour met doelomgeving.

U kunt Hallo [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess uw connection string tijdens runtime, ongeacht waar uw toepassing wordt uitgevoerd.

## <a name="create-a-connection-string-for-hello-storage-emulator"></a>Een verbindingsreeks voor de opslagemulator Hallo maken
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

Zie voor meer informatie over de opslagemulator hello [hello Azure-opslagemulator gebruiken voor ontwikkeling en tests](storage-use-emulator.md).

## <a name="create-a-connection-string-for-an-azure-storage-account"></a>Een verbindingsreeks voor Azure storage-account maken
toocreate een verbindingsreeks voor uw Azure storage-account, gebruik Hallo volgende-indeling. Aangeven of u wilt dat tooconnect toohello storage-account via HTTPS (aanbevolen) of HTTP-, vervangen door `myAccountName` met de naam van uw opslagaccount en vervang Hallo `myAccountKey` door uw toegangssleutel voor account:

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

De verbindingsreeks er ongeveer als:

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

Hoewel Azure Storage zowel HTTP als HTTPS in een verbindingsreeks ondersteunt *HTTPS wordt nadrukkelijk aanbevolen*.

> [!TIP]
> U vindt uw storage-account verbindingsreeksen in Hallo [Azure-portal](https://portal.azure.com). Navigeer te**instellingen** > **toegangssleutels** in uw opslagaccount menu blade toosee verbindingsreeksen voor beide primaire en secundaire toegangstoetsen.
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>Een verbindingsreeks met behulp van een shared access signature maken
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a>Een verbindingsreeks voor een eindpunt expliciete opslag maken
U kunt expliciete service-eindpunten in de verbindingsreeks in plaats van de Standaardeindpunten Hallo opgeven. Hallo volledige service-eindpunt voor elke service, inclusief Hallo protocol specification (HTTPS (aanbevolen) of HTTP) toocreate een verbindingsreeks die Hiermee geeft u een expliciete eindpunt opgeven in Hallo volgende indeling:

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

Een scenario waar u toospecify een expliciete eindpunt wilt mogelijk is wanneer u uw tooa eindpunt van Blob-opslag hebt toegewezen [aangepast domein](../blobs/storage-custom-domain-name.md). In dat geval kunt u uw aangepaste eindpunt voor Blob storage in de verbindingsreeks. U kunt eventueel opgeven Hallo Standaardeindpunten voor Hallo andere services als uw toepassing worden gebruikt.

Hier volgt een voorbeeld van een verbindingsreeks waarmee een expliciete eindpunt voor Hallo Blob-service:

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

In dit voorbeeld geeft expliciet eindpunten voor alle services, met inbegrip van een aangepast domein voor Hallo Blob-service:

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

Hallo eindpunt waarden in een verbindingsreeks zijn gebruikte tooconstruct Hallo aanvragen URI's toohello storage-services en dicteren Hallo vorm van een URI's die worden geretourneerd tooyour code.

Als u een aangepast domein voor opslag eindpunt tooa hebt toegewezen en dat eindpunt van een verbindingsreeks weglaat, wordt u niet kunt toouse tekenreeks die verbinding tooaccess gegevens in die service vanuit uw code.

> [!IMPORTANT]
> Service-eindpunt waarden in de verbindingsreeksen moeten juist opgemaakte URI's, met inbegrip van `https://` (aanbevolen) of `http://`. Omdat Azure Storage nog geen HTTPS voor aangepaste domeinen ondersteunt u *moet* Geef `http://` voor een willekeurig eindpunt-URI die het aangepaste domein tooa verwijst.
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a>Een verbindingsreeks met het achtervoegsel van een eindpunt maken
toocreate een verbinding de tekenreeks voor een service-opslag in regio's of exemplaren met verschillende eindpunt achtervoegsels, zoals voor Azure China of Azure Government, gebruik Hallo indeling voor een verbindingsreeks te volgen. Aangeven of u wilt dat tooconnect toohello storage-account via HTTPS (aanbevolen) of HTTP-, vervangen door `myAccountName` vervangen met de naam van uw opslagaccount hello `myAccountKey` met uw toegangssleutel en vervangen `mySuffix` Hello URI achtervoegsel:

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

Hier volgt een voorbeeld van de verbindingsreeks voor storage-services in Azure voor China:

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a>Een verbindingsreeks te parseren
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a>Volgende stappen
* [Hello Azure-opslagemulator gebruiken voor ontwikkeling en testen](storage-use-emulator.md)
* [Azure Storage explorers](storage-explorers.md)
* [Met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md)

