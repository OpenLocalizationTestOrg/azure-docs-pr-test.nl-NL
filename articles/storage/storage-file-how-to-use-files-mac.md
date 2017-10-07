---
title: aaaMount bestandsshare in Azure via SMB met Mac OS | Microsoft Docs
description: Meer informatie over hoe toomount een Azure-bestand delen via SMB met Mac OS.
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
ms.openlocfilehash: 7b4924cb42247470521c1ae8b9d03ab1756996e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>Een Azure-bestandsshare koppelen via SMB met Mac OS
[Azure File storage](storage-dotnet-how-to-use-files.md) van Microsoft-service waarmee u toocreate en gebruik netwerkbestandsshares in hello Azure Hallo industrie-initiatief gebruikt. Azure-bestandsshares kunnen worden gekoppeld in Mac OS Sierra (10.12) en El Capitan (10.11). In dit artikel bevat twee verschillende manieren toomount een Azure-bestandsshare op Mac OS met Hallo zoeken gebruikersinterface en Hallo Terminal.

> [!Note]  
> We raden u aan om het tekenen van SMB-pakketten uit te schakelen voordat u een Azure-bestandsshare koppelt via SMB. Niet te doen kan slechte prestaties opleveren bij het openen van het Azure-bestandsshare Hallo van Mac OS. De SMB-verbinding worden versleuteld, zodat dit heeft geen invloed op Hallo beveiliging van de verbinding. Van Hallo terminal, hello volgende opdrachten wordt uitgeschakeld SMB-pakketten, zoals beschreven door [Apple support-artikel over het uitschakelen van SMB-pakketten](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>Vereisten voor het koppelen van een Azure-bestandsshare op Mac OS
* **Naam van het opslagaccount**: toomount een Azure-bestand delen, kunt u moet Hallo naam van het opslagaccount Hallo.

* **Opslagaccountsleutel**: toomount een Azure-bestand delen, kunt u moet Hallo primaire (of secundaire)-opslagsleutel. SAS-sleutels worden momenteel niet ondersteund voor koppelen.

* **Zorg ervoor dat poort 445 is geopend**: SMB communiceert via TCP-poort 445. Controleer op de clientcomputer (hello Mac) toomake ervoor dat uw firewall niet wordt geblokkeerd door TCP-poort 445.

## <a name="mount-an-azure-file-share-via-finder"></a>Een Azure-bestandsshare koppelen via Finder
1. **Open de zoekfunctie**: zoeken is geopend op Mac OS standaard, maar u kunt ervoor zorgen dat deze toepassing door te klikken op Hallo 'Mac OS geconfronteerd pictogram' op Hallo dock Hallo momenteel geselecteerd:  
    ![Hallo Mac OS geconfronteerd pictogram](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)

2. **Selecteer "Connect tooServer" in hello "Ga" Menu**: Hallo UNC-pad van Hallo [vereisten](#preq), Hallo begin backslashes converteren (`\\`) te`smb://` en alle andere backslashes (`\`) tooforwards slashes (`/`). De koppeling moet eruitzien als in de volgende Hallo: ![Hallo "Connect tooServer" dialoogvenster](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)

3. **Hallo share naam- en storage-accountsleutel gebruiken wanneer u wordt gevraagd om een gebruikersnaam en wachtwoord**: wanneer u klikt op 'Verbinden' in het dialoogvenster voor Hallo "Connect tooServer", wordt u gevraagd Hallo-gebruikersnaam en wachtwoord (dit is autopopulated met uw Mac OS gebruikersnaam). U hebt de optie Hallo van Hallo share naam/opslagaccountsleutel brengen in uw Mac OS-sleutelhanger.

4. **Gebruik hello Azure-bestandsshare naar wens**: na vervangen door Hallo share en de opslag accountsleutel in Hallo gebruikersnaam en wachtwoord, hello share wordt gekoppeld. U kunt dit gebruiken zoals u gesproken een lokale map/bestandsshare gebruikt normaal, inclusief slepen en neerzetten van bestanden naar de bestandsshare Hallo:

    ![Een momentopname van een gekoppelde Azure-bestandsshare](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Een Azure-bestandsshare koppelen via Terminal
1. Vervang `<storage-account-name>` met Hallo-naam van uw opslagaccount. Geef de sleutel van het opslagaccount als wachtwoord wanneer hierom wordt gevraagd. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Gebruik hello Azure-bestandsshare naar wens**: hello Azure-bestandsshare op Hallo-koppelpunt die is opgegeven door de vorige opdracht Hallo gekoppeld.  

    ![Een momentopname van het Azure-bestandsshare Hallo gekoppeld](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Volgende stappen
Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.

* [Apple Support-artikel - hoe tooconnect met het delen van bestanden op uw Mac](https://support.apple.com/HT204445)
* [Veelgestelde vragen](storage-files-faq.md)
* [Problemen oplossen](storage-troubleshoot-file-connection-problems.md)