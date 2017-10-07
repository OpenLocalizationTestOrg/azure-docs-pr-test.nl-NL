---
title: een Azure-bestandsshare aaaMount en toegang Hallo delen in Windows | Microsoft Docs
description: Koppel een bestandsshare in Azure en -toegang Hallo share in Windows.
services: storage
documentationcenter: na
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
ms.openlocfilehash: eb6d58ad391adb6c06703ad694150534ccf44ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>Koppelen van een Azure-bestandsshare en -toegang Hallo share in Windows
[Azure File storage](../storage-dotnet-how-to-use-files.md) is van Microsoft easy toouse cloud-bestandssysteem. Azure-bestandsshares kunnen worden gekoppeld in Windows en Windows Server. In dit artikel bevat drie verschillende manieren toomount een Azure-bestandsshare op Windows: Hello bestand Explorer-gebruikersinterface via PowerShell en via Hallo opdrachtprompt. 

In de volgorde toomount een Azure-bestand delen buiten hello Azure-regio deze wordt gehost in, bijvoorbeeld on-premises of in een andere Azure-regio, moet de Hallo OS SMB 3.0 ondersteunen. 

Afhankelijk van de versie van het besturingssysteem kan een Azure-bestandsshare on-premises op een Windows-machine worden gekoppeld of op een virtuele Azure-machine. Onderstaande tabel ziet u Hallo 

| Windows-versie        | SMB-versie |Koppelbaar op Azure-VM|Koppelbaar on-premises|
|------------------------|-------------|---------------------|---------------------|
| Windows 7              | SMB 2.1     | Ja                 | Nee                  |
| Windows Server 2008 R2 | SMB 2.1     | Ja                 | Nee                  |
| Windows 8              | SMB 3.0     | Ja                 | Ja                 |
| Windows Server 2012    | SMB 3.0     | Ja                 | Ja                 |
| Windows Server 2012 R2 | SMB 3.0     | Ja                 | Ja                 |
| Windows 10             | SMB 3.0     | Ja                 | Ja                 |

> [!Note]  
> Aangeraden altijd nemen meest recente KB voor uw versie van Windows hello.

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>Vereisten voor het koppelen van een Azure-bestandsshare met Windows 
* **Naam van het opslagaccount**: toomount een Azure-bestand delen, kunt u moet Hallo naam van het opslagaccount Hallo.

* **Opslagaccountsleutel**: toomount een Azure-bestand delen, kunt u moet Hallo primaire (of secundaire)-opslagsleutel. SAS-sleutels worden momenteel niet ondersteund voor koppelen.

* **Zorg ervoor dat poort 445 is geopend**: Azure File Storage maakt gebruik van het SMB-protocol. Controleer de toosee SMB communiceert via TCP-poort 445 - als TCP-poort 445 van client-computer niet door uw firewall wordt geblokkeerd.

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>Hello Azure-bestandsshare met Verkenner koppelen
> [!Note]  
> Let op Hallo van instructies te volgen op Windows 10 worden weergegeven en kunnen enigszins verschillen op oudere versies. 

1. **Open de Verkenner**: dit kan worden gedaan door het openen van Hallo Menu Start of door op de snelkoppeling Win + E.

2. **Navigeer toohello 'Deze PC' item aan de linkerkant Hallo van Hallo-venster. Hiermee wijzigt u Hallo menu's beschikbaar zijn in het Hallo-lint. Selecteer onder menu Computer Hallo 'Stations toewijzen netwerk'**.
    
    ![Een schermopname van de vervolgkeuzelijst Hallo 'Netwerkverbinding maken'](./media/storage-how-to-use-files-windows/1_MountOnWindows10.png)

3. **Kopiëren Hallo UNC-pad vanuit Hallo 'Connect' deelvenster in hello Azure-portal**: een gedetailleerde beschrijving van hoe toofind deze informatie vindt u [hier](storage-how-to-use-files-portal.md#connect-to-file-share).

    ![Hallo UNC-pad in hello Azure File storage Connect deelvenster](./media/storage-how-to-use-files-windows/portal_netuse_connect.png)

4. **Selecteer Hallo stationsletter en Voer Hallo UNC-pad.** 
    
    ![Een schermopname van dialoogvenster voor Hallo 'Stations toewijzen netwerk'](./media/storage-how-to-use-files-windows/2_MountOnWindows10.png)

5. **Gebruik Hallo Opslagaccountnaam voorafgegaan door `Azure\` als Hallo gebruikersnaam en de sleutel van een Opslagaccount als Hallo wachtwoord.**
    
    ![Een schermopname van dialoogvenster voor gebruikersreferenties Hallo-netwerk](./media/storage-how-to-use-files-windows/3_MountOnWindows10.png)

6. **Gebruik de Azure-bestandsshare naar wens**.
    
    ![De Azure-bestandsshare is nu gekoppeld](./media/storage-how-to-use-files-windows/4_MountOnWindows10.png)

7. **Wanneer u klaar toodismount (of Verbreek de verbinding met) hello Azure-bestandsshare, kunt u doen door met de rechtermuisknop te klikken op Hallo-vermelding voor de share Hallo onder Hallo 'netwerklocaties' in Windows Verkenner en 'Verbinding verbreken'**.

## <a name="mount-hello-azure-file-share-with-powershell"></a>Hello Azure-bestandsshare met PowerShell koppelen
1. **Gebruik Hallo volgende opdracht toomount hello Azure-bestandsshare**: onthouden tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` met de juiste informatie Hallo.

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **Gebruik hello Azure-bestandsshare naar wens**.

3. **Wanneer u klaar bent, ontkoppelen Hallo bestandsshare in Azure met behulp van de volgende opdracht Hallo**.

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> U kunt op Hallo `-Persist` parameter op `New-PSDrive` toomake hello Azure File share zichtbaar toohello rest Hallo OS terwijl gekoppeld.

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>Hello Azure-bestandsshare bij de opdrachtprompt koppelen
1. **Gebruik Hallo volgende opdracht toomount hello Azure-bestandsshare**: onthouden tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` met de juiste informatie Hallo.

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **Gebruik hello Azure-bestandsshare naar wens**.

3. **Wanneer u klaar bent, ontkoppelen Hallo bestandsshare in Azure met behulp van de volgende opdracht Hallo**.

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> U kunt hello Azure File share tooautomatically opnieuw configureren op opnieuw opstarten persisting Hallo-referenties in Windows. Hallo na de opdracht bewaard Hallo referenties:
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>Volgende stappen
Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.

* [Veelgestelde vragen](../storage-files-faq.md)
* [Problemen oplossen in Windows](storage-troubleshoot-windows-file-connection-problems.md)      

### <a name="conceptual-articles-and-videos"></a>Conceptuele artikelen en video's
* [Azure File Storage: een naadloos SMB-bestandssysteem voor Windows en Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Hoe toouse Azure File storage met Linux](../storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Hulpprogramma-ondersteuning voor Azure File Storage
* [Hoe toouse AzCopy met Microsoft Azure Storage](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Hello Azure CLI gebruiken met Azure Storage](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Problemen met betrekking tot Azure File Storage oplossen - Windows](storage-troubleshoot-windows-file-connection-problems.md)
* [Problemen met betrekking tot Azure File Storage oplossen - Linux](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a>Blogberichten
* [Azure File storage is now generally available (Azure File Storage is nu algemeen beschikbaar)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File Storage (Een kijkje achter de schermen van Azure File Storage)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introducing Microsoft Azure File Service (Introductie van Microsoft Azure File-service)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migreren gegevens tooAzure bestand](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Naslaginformatie
* [Naslaginformatie over de Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Naslaginformatie over REST API voor bestandsservices](http://msdn.microsoft.com/library/azure/dn167006.aspx)
