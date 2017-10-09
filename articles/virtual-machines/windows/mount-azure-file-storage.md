---
title: Azure file storage vanuit een Windows Azure VM aaaMount | Microsoft Docs
description: Opslaan van het bestand in de cloud met Azure file storage Hallo en uw cloud-bestandsshare koppelen vanuit Azure een virtuele machine (VM).
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a>Azure-bestandsshares gebruiken met Windows VM 's 

U kunt Azure-bestandsshares gebruiken als een manier toostore en toegang tot de bestanden van de virtuele machine. U kunt bijvoorbeeld een script of een toepassingsconfiguratiebestand dat u wilt dat alle tooshare van uw virtuele machines opslaan. In dit onderwerp laten we zien u hoe toocreate en koppelpunten een Azure-bestandsshare en hoe bestanden tooupload en downloaden.

## <a name="connect-tooa-file-share-from-a-vm"></a>Verbinding maken met de bestandsshare tooa van een virtuele machine

Deze sectie wordt ervan uitgegaan dat u hebt al een bestand dat u wilt dat tooconnect te delen. Als u toocreate een moet, Zie [een bestandsshare maken](#create-a-file-share) verderop in dit onderwerp.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op Hallo linkermenu **opslagaccounts**.
3. Kies uw opslagaccount.
4. In Hallo **overzicht** pagina onder **Services**, selecteer **bestanden**.
5. Selecteer een bestandsshare.
6. Klik op **Connect** tooopen een pagina met de opdrachtregelsyntaxis Hallo voor het Hallo-bestandsshare koppelen van Windows of Linux.
7. Markeer Hallo syntaxis van Hallo opdracht en plak deze in Kladblok of ergens anders waar u eenvoudig toegang toe. 
8. Hallo syntaxis tooremove Hallo voorloopspaties bewerken ** > ** en vervang *[stationsaanduiding]* met Hallo stationsletter (bijvoorbeeld **Y:**) waar u wilt toomount Hallo-bestandsshare.
8. Tooyour VM sluit en open een opdrachtprompt.
9. Plakken in Hallo bewerkt u de syntaxis van de verbinding en klik op **Enter**.
10. Als het Hallo-verbinding is gemaakt, krijgt u het Hallo-bericht **Hallo-opdracht is uitgevoerd.**
11. Hallo-verbinding controleren door te typen in Hallo letter tooswitch toothat schijf en typ vervolgens **dir** toosee Hallo inhoud van de bestandsshare Hallo.



## <a name="create-a-file-share"></a>Een bestandsshare maken 
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op Hallo linkermenu **opslagaccounts**.
3. Kies uw opslagaccount.
4. In Hallo **overzicht** pagina onder **Services**, selecteer **bestanden**.
5. Hallo File Service pagina, klikt u op **+ bestandsshare** toocreate uw eerste bestandsshare. \
6. Naam van bestandsshare Hallo invullen. De namen van bestandsshares kunnen gebruiken, kleine letters, cijfers en afbreekstreepjes één. Hallo-naam kan niet beginnen met een afbreekstreepje en u kunt niet meerdere, gebruiken afbreekstreepjes achter elkaar voorkomen. 
7. Vul in een limiet op hoe groot Hallo-bestand mag up too5120 GB.
8. Klik op **OK** toodeploy Hallo-bestandsshare.
   
## <a name="upload-files"></a>Bestanden uploaden
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op Hallo linkermenu **opslagaccounts**.
3. Kies uw opslagaccount.
4. In Hallo **overzicht** pagina onder **Services**, selecteer **bestanden**.
5. Selecteer een bestandsshare.
6. Klik op **uploaden** tooopen hello **bestanden uploaden** pagina.
7. Klik op Hallo map pictogram toobrowse voor een bestand tooupload het lokale bestandssysteem.   
8. Klik op **uploaden** tooupload hello toohello bestand bestandsshare.

## <a name="download-files"></a>Bestanden downloaden
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op Hallo linkermenu **opslagaccounts**.
3. Kies uw opslagaccount.
4. In Hallo **overzicht** pagina onder **Services**, selecteer **bestanden**.
5. Selecteer een bestandsshare.
6. Met de rechtermuisknop op het Hallo-bestand en kies **downloaden** toodownload het tooyour lokale computer.
   

## <a name="next-steps"></a>Volgende stappen

U kunt ook maken en beheren van bestandsshares met behulp van PowerShell. Zie voor meer informatie [aan de slag met Azure File storage in Windows](../../storage/files/storage-dotnet-how-to-use-files.md).
