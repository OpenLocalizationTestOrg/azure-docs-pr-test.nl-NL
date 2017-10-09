---
title: aaaHow toomanage Azure File storage uit hello Azure-portal | Microsoft Docs
description: Meer informatie over toouse hello Azure portal toomanage Azure File storage.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>Hoe Azure File storage toouse van hello Azure Portal
Hallo [Azure-portal](https://portal.azure.com) biedt een gebruikersinterface voor het beheren van Azure File storage. U kunt de volgende acties uit uw webbrowser Hallo uitvoeren:

* Een bestandsshare maken
* Uploaden en downloaden van bestanden tooand van de bestandsshare.
* Hallo werkelijke gebruik van elke bestandsshare controleren.
* Quotum voor de grootte van de bestandsshare Hallo aanpassen.
* Hallo koppelpunt opdrachten toouse toomount delen van het bestand kopiëren van een Windows- of Linux-client.

## <a name="create-file-share"></a>Bestandsshare maken
1. Meld u aan toohello Azure-portal.
2. Klik op Hallo navigatiemenu **opslagaccounts** of **opslagaccounts (klassiek)**.
    
    ![Schermopname die laat zien hoe toocreate-bestandsshare in Hallo-portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. Kies uw opslagaccount.

    ![Schermopname die laat zien hoe toocreate-bestandsshare in Hallo-portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. Kies de service Bestanden.

    ![Schermopname die laat zien hoe toocreate-bestandsshare in Hallo-portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. Klik op 'Bestandsshares' en volg Hallo koppeling toocreate uw eerste bestandsshare.

    ![Schermopname die laat zien hoe toocreate-bestandsshare in Hallo-portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Naam van bestandsshare Hallo en invullen Hallo grootte van Hallo file share (omhoog too5120 GB) toocreate uw eerste bestandsshare. Zodra het Hallo-bestandsshare is gemaakt, kunt u deze koppelen vanuit elk bestandssysteem dat SMB 2.1 of SMB 3.0 ondersteunt. U kunt klikken op **quotum** op Hallo toochange Hallo grootte van de bestandsshare van Hallo bestand up too5120 GB. Raadpleeg het te[Azure Prijscalculator](https://azure.microsoft.com/pricing/calculator/) tooestimate Hallo opslagkosten van het gebruik van Azure File storage.

    ![Schermopname die laat zien hoe toocreate-bestandsshare in Hallo-portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>Bestanden uploaden en downloaden
1. Kies een bestandsshare die u al hebt gemaakt.

    ![Schermopname die laat zien hoe tooupload en downloaden van bestanden van de portal Hallo](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. Klik op **uploaden** Hallo-gebruikersinterface voor het uploaden van bestanden te openen.

    ![Schermopname die laat zien hoe tooupload bestanden van Hallo-portal](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>Verbinding maken met share toofile
-  Klik op **Connect** Hallo vanaf de opdrachtregel voor koppelen Hallo bestandsshare ophalen van Windows en Linux. Voor Linux-gebruikers, kunt u ook verwijzen te[hoe toouse Azure File storage met Linux](storage-how-to-use-files-linux.md) voor montage instructies voor het andere Linux-distributies.

    ![Schermopname die laat zien hoe toomount Hallo bestandsshare](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  U kunt kopiëren Hallo opdrachten voor het koppelen van bestand delen op Windows of Linux- en virtuele machine in Azure of on-premises machine uitvoeren van u.

    ![Schermafbeelding van Hallo mount-opdrachten voor Windows en Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**Tip:**  
toofind hello toegangssleutel voor opslagaccount voor koppelen, klikt u op **toegangssleutels weergeven voor dit opslagaccount** onderin Hallo Hallo pagina verbinden.

## <a name="see-also"></a>Zie ook
Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.

* [Veelgestelde vragen](storage-files-faq.md)
* [Problemen oplossen](storage-troubleshoot-file-connection-problems.md)