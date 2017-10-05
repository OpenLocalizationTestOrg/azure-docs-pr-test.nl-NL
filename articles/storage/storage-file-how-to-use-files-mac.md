---
title: Een Azure-bestandsshare koppelen via SMB met Mac OS | Microsoft Docs
description: Informatie over het koppelen van een Azure-bestandsshare via SMB met Mac OS.
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
ms.openlocfilehash: 428086910273d10a68cb8193df377a4db267d6a3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="58519-103">Een Azure-bestandsshare koppelen via SMB met Mac OS</span><span class="sxs-lookup"><span data-stu-id="58519-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="58519-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is een service van Microsoft waarmee u netwerkbestandsshares kunt maken en gebruiken in Azure volgens de industrienorm.</span><span class="sxs-lookup"><span data-stu-id="58519-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you to create and use network file shares in the Azure using the industry standard.</span></span> <span data-ttu-id="58519-105">Azure-bestandsshares kunnen worden gekoppeld in Mac OS Sierra (10.12) en El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="58519-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="58519-106">Dit artikel behandelt twee verschillende manieren om een Azure-bestandsshare te koppelen op Mac OS met de Finder-gebruikersinterface en met Terminal.</span><span class="sxs-lookup"><span data-stu-id="58519-106">This article shows two different ways to mount an Azure File share on macOS with the Finder UI and using the Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="58519-107">We raden u aan om het tekenen van SMB-pakketten uit te schakelen voordat u een Azure-bestandsshare koppelt via SMB.</span><span class="sxs-lookup"><span data-stu-id="58519-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="58519-108">Als u dit niet doet, zorgt dit mogelijk voor slechte prestaties bij het openen van de Azure-bestandsshare in Mac OS.</span><span class="sxs-lookup"><span data-stu-id="58519-108">Not doing so may yield poor performance when accessing the Azure File share from macOS.</span></span> <span data-ttu-id="58519-109">De SMB-verbinding is versleuteld, dus dit heeft geen invloed op de beveiliging van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="58519-109">Your SMB connection will be encrypted, so this does not affect the security of your connection.</span></span> <span data-ttu-id="58519-110">Vanaf de terminal schakelen de volgende opdrachten het ondertekenen van SMB-pakketten uit, zoals beschreven door dit [ondersteuningsartikel van Apple over het uitschakelen van SMB-pakketondertekening](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="58519-110">From the terminal, the following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="58519-111">Vereisten voor het koppelen van een Azure-bestandsshare op Mac OS</span><span class="sxs-lookup"><span data-stu-id="58519-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="58519-112">**Naam van het opslagaccount**: voor het koppelen van een Azure-bestandsshare hebt u de naam van het opslagaccount nodig.</span><span class="sxs-lookup"><span data-stu-id="58519-112">**Storage account name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="58519-113">**Sleutel van het opslagaccount**: voor het koppelen van een Azure-bestandsshare hebt u de primaire (of secundaire) opslagsleutel nodig.</span><span class="sxs-lookup"><span data-stu-id="58519-113">**Storage account key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="58519-114">SAS-sleutels worden momenteel niet ondersteund voor koppelen.</span><span class="sxs-lookup"><span data-stu-id="58519-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="58519-115">**Zorg ervoor dat poort 445 is geopend**: SMB communiceert via TCP-poort 445.</span><span class="sxs-lookup"><span data-stu-id="58519-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="58519-116">Controleer op de clientcomputer (Mac) of uw firewall TCP-poort 445 niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="58519-116">On your client machine (the Mac), check to make sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="58519-117">Een Azure-bestandsshare koppelen via Finder</span><span class="sxs-lookup"><span data-stu-id="58519-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="58519-118">**Open Finder**: Finder is standaard geopend op Mac OS, maar u kunt controleren of het de geselecteerde toepassing is door te klikken op het 'gezichtspictogram van Mac OS' op de dock:</span><span class="sxs-lookup"><span data-stu-id="58519-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is the currently selected application by clicking the "macOS face icon" on the dock:</span></span>  
    <span data-ttu-id="58519-119">![Het gezichtspictogram van Mac OS](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="58519-119">![The macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="58519-120">**Selecteer 'Verbinden met server' in het menu 'Ga'**: Gebruik het UNC-pad in de [vereisten](#preq) en converteer de eerste twee backslashes (`\\`) naar `smb://` en alle andere backslashes (`\`) naar slashes (`/`).</span><span class="sxs-lookup"><span data-stu-id="58519-120">**Select "Connect to Server" from the "Go" Menu**: Using the UNC path from the [prerequisites](#preq), convert the beginning double backslash (`\\`) to `smb://` and all other backslashes (`\`) to forwards slashes (`/`).</span></span> <span data-ttu-id="58519-121">De link moet er als volgt uitzien: ![het dialoogvenster 'Verbinden met server'](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="58519-121">Your link should look like the following: ![The "Connect to Server" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="58519-122">**Gebruik de sharenaam en de sleutel van het opslagaccount wanneer u wordt gevraagd om een gebruikersnaam en wachtwoord**: Wanneer u klikt op 'Verbinden' in het dialoogvenster 'Verbinden met server', wordt u gevraagd om de gebruikersnaam en het wachtwoord (hier wordt uw Mac OS-gebruikersnaam automatisch ingevuld).</span><span class="sxs-lookup"><span data-stu-id="58519-122">**Use the share name and storage account key when prompted for a username and password**: When you click "Connect" on the "Connect to Server" dialog, you will be prompted for the username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="58519-123">U hebt de mogelijkheid om de sharenaam/sleutel van het opslagaccounts in uw Mac OS Keychain op te slaan.</span><span class="sxs-lookup"><span data-stu-id="58519-123">You have the option of placing the share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="58519-124">**Gebruik de Azure-bestandsshare naar wens**: nadat u de sharenaam en de sleutel van het opslagaccount hebt gebruikt in plaat van de gebruikersnaam en het wachtwoord, wordt de share gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="58519-124">**Use the Azure File share as desired**: After substituting the share name and storage account key in for the username and password, the share will be mounted.</span></span> <span data-ttu-id="58519-125">U kunt deze gebruiken zoals u een lokale map/bestandsshare zou gebruiken. Zo kunt u bestanden naar de bestandsshare slepen en neerzetten:</span><span class="sxs-lookup"><span data-stu-id="58519-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into the file share:</span></span>

    ![Een momentopname van een gekoppelde Azure-bestandsshare](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="58519-127">Een Azure-bestandsshare koppelen via Terminal</span><span class="sxs-lookup"><span data-stu-id="58519-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="58519-128">Vervang `<storage-account-name>` door de naam van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="58519-128">Replace `<storage-account-name>` with the name of your storage account.</span></span> <span data-ttu-id="58519-129">Geef de sleutel van het opslagaccount als wachtwoord wanneer hierom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="58519-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="58519-130">**Gebruik de Azure-bestandsshare naar wens**: de Azure-bestandsshare wordt aan het koppelpunt dat is opgegeven door de vorige opdracht gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="58519-130">**Use the Azure File share as desired**: The Azure File share will be mounted at the mount point specified by the previous command.</span></span>  

    ![Een momentopname van de gekoppelde Azure-bestandsshare](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="58519-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58519-132">Next steps</span></span>
<span data-ttu-id="58519-133">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="58519-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="58519-134">Helpartikel van Apple: Verbinding maken met Bestandsdeling op een Mac</span><span class="sxs-lookup"><span data-stu-id="58519-134">Apple Support Article - How to connect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="58519-135">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="58519-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="58519-136">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="58519-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)