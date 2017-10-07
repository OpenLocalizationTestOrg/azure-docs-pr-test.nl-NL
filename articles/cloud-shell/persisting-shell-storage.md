---
title: aaaPersist bestanden in de Azure-Cloud-Shell (Preview) | Microsoft Docs
description: Overzicht van hoe Azure Cloud Shell zich blijft bestanden voordoen.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>Bestanden in de Azure-Cloud-Shell behouden
Cloud-Shell maakt gebruik van Azure File storage toopersist bestanden over de sessies.

## <a name="set-up-a-clouddrive-file-share"></a>Instellen van een `clouddrive` bestandsshare
Op de eerste start Cloud Shell wordt u gevraagd een nieuwe of bestaande bestandsshare toopersist bestanden tussen sessies tooassociate.

### <a name="create-new-storage"></a>Maken van nieuwe opslag

Wanneer u basisinstellingen en alleen een abonnement selecteren, maakt Cloud Shell drie bronnen namens jou in Hallo ondersteund regio die zich het dichtst bij tooyou:
* Resourcegroep:`cloud-shell-storage-<region>`
* Storage-account:`cs<uniqueGuid>`
* Bestandsshare:`cs-<user>-<domain>-com-<uniqueGuid>`

![Hallo-instelling voor Cloudabonnement](media/basic-storage.png)

Hallo-bestandsshare koppelt als `clouddrive` in uw `$Home` directory. Hallo bestandsshare is ook gebruikte toostore een afbeelding 5 GB die automatisch voor u en die wordt gemaakt, bijgewerkt en zich blijft voordoen uw `$Home` directory. Dit is een eenmalige bewerking en Hallo-bestandsshare in de volgende sessies automatisch koppelt.

### <a name="use-existing-resources"></a>Bestaande bronnen gebruiken

U kunt met behulp van de geavanceerde optie Hallo bestaande resources koppelen. Wanneer Hallo opslag setup prompt wordt weergegeven, selecteert u **weergeven geavanceerde instellingen** tooview extra opties. Bestaande bestandsshares ontvangen van een afbeelding 5 GB gebruiker toopersist uw `$Home` directory. Hallo vervolgkeuzemenu's worden gefilterd voor de regio van uw Cloud-Shell en lokaal redundante & geo-redundant storage-accounts.

![instelling van de Resource Hallo](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>Bron maken met een Azure-resource beleid beperken
Storage-accounts die u in de Cloud-Shell maakt zijn gelabeld met `ms-resource-usage:azure-cloud-shell`. Als u wilt dat gebruikers van het storage-accounts maken in de Cloud-Shell toodisallow, maakt u een [Azure bronbeleid voor tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) die worden geactiveerd door deze specifieke tag.

## <a name="how-cloud-shell-works"></a>De werking van Cloud-Shell
Cloud-Shell aanhoudt bestanden via beide Hallo volgende methoden:
* Maken van de installatiekopie van een schijf van uw `$Home` directory toopersist alle inhoud binnen Hallo-directory. Hallo-installatiekopie wordt opgeslagen in de opgegeven bestandsshare als `acc_<User>.img` op `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, en worden wijzigingen automatisch gesynchroniseerd.

* Koppelen van de opgegeven bestandsshare als `clouddrive` in uw `$Home` map voor interactie met de share rechtstreeks bestand. `/Home/<User>/clouddrive`is toegewezen te`fileshare.storage.windows.net/fileshare`.
 
> [!NOTE]
> Alle bestanden in uw `$Home` directory, zoals SSH-sleutels worden doorgevoerd in uw schijfimage gebruiker die is opgeslagen in de gekoppelde bestandsshare. Aanbevolen procedures van toepassing wanneer u deze persistent maken informatie in uw `$Home` directory en gekoppelde bestandsshare.

## <a name="use-hello-clouddrive-command"></a>Gebruik Hallo `clouddrive` opdracht
Met Cloud-Shell, kunt u een opdracht uitvoeren `clouddrive`, dit kunt u toomanually update Hallo-bestandsshare die gekoppelde tooCloud Shell.
![Hallo 'clouddrive' opdracht uit te voeren](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>Een nieuwe koppelen`clouddrive`

### <a name="prerequisites-for-manual-mounting"></a>Vereisten voor de handmatige koppelen
U kunt bijwerken Hallo-bestandsshare die is gekoppeld aan Cloud-Shell met behulp van Hallo `clouddrive mount` opdracht.

Als u een bestaande bestandsshare koppelt, moet Hallo storage-accounts:
* Lokaal redundante opslag of geografisch redundante opslag toosupport bestandsshares.
* Bevindt zich in uw regio toegewezen. Als u de voorbereiding, Hallo regio aan u zijn toegewezen die worden vermeld in de naam van resourcegroep Hallo toois `cloud-shell-storage-<region>`.

### <a name="supported-storage-regions"></a>Ondersteunde opslagregio
Hello Azure bestanden moeten zich bevinden in Hallo dezelfde regio bevinden als Hallo Cloud Shell machine die u ze wilt koppelen. Cloud-Shell clusters is momenteel beschikbaar zijn in Hallo gebieden te volgen:
|Onderwerp|Regio|
|---|---|
|Noord- en Zuid-Amerika|VS-Oost, Zuid-centraal VS, VS-West|
|Europa|Noord-Europa, West-Europa|
|Azië en Stille Oceaan|India centraal, Zuidoost-Azië|

### <a name="hello-clouddrive-mount-command"></a>Hallo `clouddrive mount` opdracht

> [!NOTE]
> Als u een nieuwe bestandsshare koppelen wilt, een nieuwe gebruikersinstallatiekopie is gemaakt voor uw `$Home` directory, omdat uw vorige `$Home` installatiekopie wordt opgeslagen in de vorige bestandsshare Hallo.

Voer Hallo `clouddrive mount` opdracht Hello volgende parameters:

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

tooview meer details uitvoeren `clouddrive mount -h`, zoals hier wordt weergegeven:

![Actieve Hallo ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>Ontkoppelen`clouddrive`
U kunt een bestandsshare die gekoppelde tooCloud-Shell op elk gewenst moment ontkoppelen. Wanneer de bestandsshare ontkoppeld is, kunt u zich na vragen aan gebruiker toomount een nieuw bestandsshare voorafgaande tooyour volgende sessie.

een bestand tooremove delen van Cloud-Shell:
1. Voer `clouddrive unmount` uit.
2. Erkent en hello wordt u gevraagd te bevestigen.

De bestandsshare blijven tooexist tenzij u deze handmatig verwijderen. Cloud-Shell zoekt op de volgende sessies niet meer naar deze bestandsshare.

tooview meer details uitvoeren `clouddrive unmount -h`, zoals hier wordt weergegeven:

![Actieve Hallo ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> Alle resources worden niet verwijderd als u deze opdracht uit te voeren. Handmatig verwijderen van een resourcegroep, het opslagaccount of de bestandsshare die is toegewezen tooCloud Shell wordt permanent verwijderd. uw `$Home` directory installatiekopie en andere bestanden in de bestandsshare. Deze actie kan niet ongedaan worden gemaakt.

## <a name="list-clouddrive-file-shares"></a>Lijst `clouddrive` bestandsshares
welke bestandsshare is gekoppeld als toodiscover `clouddrive`, voert u de volgende Hallo `df` opdracht. 

Hallo bestand pad tooclouddrive ziet u dat de naam van het opslagaccount en bestandsshare in Hallo-URL. Bijvoorbeeld: `//storageaccountname.file.core.windows.net/filesharename`

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a>Overdracht lokale bestanden tooCloud Shell
Hallo `clouddrive` directory wordt gesynchroniseerd met Azure portal-opslag-blade Hallo. Gebruik deze blade tootransfer lokale bestanden tooor van de bestandsshare. Bijwerken van bestanden vanuit Cloud Shell wordt doorgevoerd in Hallo bestandsopslag GUI wanneer u de blade Hallo vernieuwt.

### <a name="download-files"></a>Bestanden downloaden

![Lijst van lokale bestanden](media/download.png)
1. Ga in hello Azure-portal, toohello gekoppelde bestandsshare.
2. Selecteer het doelbestand Hallo.
3. Selecteer Hallo **downloaden** knop.

### <a name="upload-files"></a>Bestanden uploaden

![Lokale bestanden toobe geüpload](media/upload.png)
1. Ga tooyour gekoppelde bestandsshare.
2. Selecteer Hallo **uploaden** knop.
3. Selecteer Hallo of bestanden die u tooupload wilt.
4. Bevestig Hallo uploaden.

U ziet nu Hallo-bestanden die toegankelijk zijn in uw `clouddrive` map in de Cloud-Shell.

## <a name="next-steps"></a>Volgende stappen
[Cloud-Shell Quick Start](quickstart.md) <br>
[Meer informatie over Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[Meer informatie over opslag labels](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
