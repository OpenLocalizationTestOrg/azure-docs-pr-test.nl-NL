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
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="43e2f-103">Een Azure-bestandsshare koppelen via SMB met Mac OS</span><span class="sxs-lookup"><span data-stu-id="43e2f-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="43e2f-104">[Azure File storage](storage-dotnet-how-to-use-files.md) van Microsoft-service waarmee u toocreate en gebruik netwerkbestandsshares in hello Azure Hallo industrie-initiatief gebruikt.</span><span class="sxs-lookup"><span data-stu-id="43e2f-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="43e2f-105">Azure-bestandsshares kunnen worden gekoppeld in Mac OS Sierra (10.12) en El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="43e2f-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="43e2f-106">In dit artikel bevat twee verschillende manieren toomount een Azure-bestandsshare op Mac OS met Hallo zoeken gebruikersinterface en Hallo Terminal.</span><span class="sxs-lookup"><span data-stu-id="43e2f-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="43e2f-107">We raden u aan om het tekenen van SMB-pakketten uit te schakelen voordat u een Azure-bestandsshare koppelt via SMB.</span><span class="sxs-lookup"><span data-stu-id="43e2f-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="43e2f-108">Niet te doen kan slechte prestaties opleveren bij het openen van het Azure-bestandsshare Hallo van Mac OS.</span><span class="sxs-lookup"><span data-stu-id="43e2f-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="43e2f-109">De SMB-verbinding worden versleuteld, zodat dit heeft geen invloed op Hallo beveiliging van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="43e2f-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="43e2f-110">Van Hallo terminal, hello volgende opdrachten wordt uitgeschakeld SMB-pakketten, zoals beschreven door [Apple support-artikel over het uitschakelen van SMB-pakketten](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="43e2f-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="43e2f-111">Vereisten voor het koppelen van een Azure-bestandsshare op Mac OS</span><span class="sxs-lookup"><span data-stu-id="43e2f-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="43e2f-112">**Naam van het opslagaccount**: toomount een Azure-bestand delen, kunt u moet Hallo naam van het opslagaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="43e2f-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="43e2f-113">**Opslagaccountsleutel**: toomount een Azure-bestand delen, kunt u moet Hallo primaire (of secundaire)-opslagsleutel.</span><span class="sxs-lookup"><span data-stu-id="43e2f-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="43e2f-114">SAS-sleutels worden momenteel niet ondersteund voor koppelen.</span><span class="sxs-lookup"><span data-stu-id="43e2f-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="43e2f-115">**Zorg ervoor dat poort 445 is geopend**: SMB communiceert via TCP-poort 445.</span><span class="sxs-lookup"><span data-stu-id="43e2f-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="43e2f-116">Controleer op de clientcomputer (hello Mac) toomake ervoor dat uw firewall niet wordt geblokkeerd door TCP-poort 445.</span><span class="sxs-lookup"><span data-stu-id="43e2f-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="43e2f-117">Een Azure-bestandsshare koppelen via Finder</span><span class="sxs-lookup"><span data-stu-id="43e2f-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="43e2f-118">**Open de zoekfunctie**: zoeken is geopend op Mac OS standaard, maar u kunt ervoor zorgen dat deze toepassing door te klikken op Hallo 'Mac OS geconfronteerd pictogram' op Hallo dock Hallo momenteel geselecteerd:</span><span class="sxs-lookup"><span data-stu-id="43e2f-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="43e2f-119">![Hallo Mac OS geconfronteerd pictogram](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="43e2f-119">![hello macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="43e2f-120">**Selecteer "Connect tooServer" in hello "Ga" Menu**: Hallo UNC-pad van Hallo [vereisten](#preq), Hallo begin backslashes converteren (`\\`) te`smb://` en alle andere backslashes (`\`) tooforwards slashes (`/`).</span><span class="sxs-lookup"><span data-stu-id="43e2f-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="43e2f-121">De koppeling moet eruitzien als in de volgende Hallo: ![Hallo "Connect tooServer" dialoogvenster](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="43e2f-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="43e2f-122">**Hallo share naam- en storage-accountsleutel gebruiken wanneer u wordt gevraagd om een gebruikersnaam en wachtwoord**: wanneer u klikt op 'Verbinden' in het dialoogvenster voor Hallo "Connect tooServer", wordt u gevraagd Hallo-gebruikersnaam en wachtwoord (dit is autopopulated met uw Mac OS gebruikersnaam).</span><span class="sxs-lookup"><span data-stu-id="43e2f-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="43e2f-123">U hebt de optie Hallo van Hallo share naam/opslagaccountsleutel brengen in uw Mac OS-sleutelhanger.</span><span class="sxs-lookup"><span data-stu-id="43e2f-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="43e2f-124">**Gebruik hello Azure-bestandsshare naar wens**: na vervangen door Hallo share en de opslag accountsleutel in Hallo gebruikersnaam en wachtwoord, hello share wordt gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="43e2f-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="43e2f-125">U kunt dit gebruiken zoals u gesproken een lokale map/bestandsshare gebruikt normaal, inclusief slepen en neerzetten van bestanden naar de bestandsshare Hallo:</span><span class="sxs-lookup"><span data-stu-id="43e2f-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![Een momentopname van een gekoppelde Azure-bestandsshare](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="43e2f-127">Een Azure-bestandsshare koppelen via Terminal</span><span class="sxs-lookup"><span data-stu-id="43e2f-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="43e2f-128">Vervang `<storage-account-name>` met Hallo-naam van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="43e2f-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="43e2f-129">Geef de sleutel van het opslagaccount als wachtwoord wanneer hierom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="43e2f-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="43e2f-130">**Gebruik hello Azure-bestandsshare naar wens**: hello Azure-bestandsshare op Hallo-koppelpunt die is opgegeven door de vorige opdracht Hallo gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="43e2f-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Een momentopname van het Azure-bestandsshare Hallo gekoppeld](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="43e2f-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43e2f-132">Next steps</span></span>
<span data-ttu-id="43e2f-133">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="43e2f-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="43e2f-134">Apple Support-artikel - hoe tooconnect met het delen van bestanden op uw Mac</span><span class="sxs-lookup"><span data-stu-id="43e2f-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="43e2f-135">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="43e2f-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="43e2f-136">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="43e2f-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)