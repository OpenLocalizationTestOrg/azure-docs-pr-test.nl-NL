---
title: een Azure RemoteApp-installatiekopie op basis van een Azure VM aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een afbeelding voor Azure RemoteApp door te beginnen met een virtuele machine van Azure.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Een Azure RemoteApp-installatiekopie op basis van een virtuele machine van Azure maken
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

U kunt Azure RemoteApp-installatiekopieën (die houdt Hallo-apps die u in uw verzameling deelt) maken van een virtuele machine van Azure. Ook kunt u toouse de installatiekopie van een virtuele machine toegevoegd toohello Azure VM-installatiekopie galerie die voldoet aan alle vereisten van hello Azure RemoteApp-installatiekopie: u kunt die VM-installatiekopie gebruiken als een beginpunt voor uw eigen virtuele machine, als u wilt. Kijk voor Hallo 'Windows Server extern bureaublad-sessiehost'-installatiekopie in Hallo-bibliotheek.

Er zijn twee stappen toocreate uw eigen installatiekopie op basis van een Azure VM - Hallo installatiekopie maken en uploaden van hello Azure VM-bibliotheek tooAzure RemoteApp.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Een aangepaste installatiekopie op basis van een virtuele machine in Azure maken
Gebruik deze stappen toocreate een installatiekopie op basis van een virtuele machine in Azure.

1. Maak een virtuele machine van Azure. U kunt Hallo 'Windows Server extern bureaublad-sessiehost' of 'Windows Server Remote Desktop Session Host met Microsoft Office 365 ProPlus' Hallo-installatiekopie vanuit galerie met virtuele machine van Azure installatiekopie hello gebruiken. Deze installatiekopie voldoet aan de vereisten van de installatiekopie van het Azure RemoteApp sjabloon Hallo.
   
    Zie voor meer informatie [maken van een virtuele machine met Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Verbinding maken met toohello VM en installeren en configureren van Hallo-apps die u wilt dat tooshare via RemoteApp. Zorg ervoor dat tooperform geen aanvullende Windows-configuraties die vereist zijn voor uw apps.
   
    Zie voor meer informatie [hoe tooLog op virtuele Machine Running Windows Server tooa](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Als u van een Windows Server Remote Desktop Session Host-installatiekopieën hello gebruikmaakt, is er een opgenomen validatiescript uw virtuele machine voldoet aan Hallo RemoteApp pre-reqs. zo dat toorun script, dubbelklikt u op **ValidateRemoteAppImage** op Hallo bureaublad. Zorg ervoor dat alle fouten gerapporteerd door Hallo script worden opgelost voordat u doorgaat toohello volgende stap.
4. SYSPREP generaliseren en Hallo installatiekopie vastleggen. Zie [hoe tooCapture een tooUse virtuele Windows-computer als een sjabloon](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) voor instructies.

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Hallo afbeelding importeren in Azure RemoteApp-afbeeldingsbibliotheek Hallo
Gebruik deze stappen tooimport Hallo nieuwe installatiekopie in Azure RemoteApp:

1. In Hallo **Sjablooninstallatiekopieën** tabblad:
   
   * Als u geen bestaande afbeeldingen hebt, klikt u op **uploaden of de installatiekopie van een sjabloon importeren**.
   * Als u ten minste één installatiekopie al hebt, klikt u op  **+**  tooadd een nieuwe installatiekopie.
2. Selecteer **een afbeelding van uw virtuele Machines importeren** bibliotheek, en klik vervolgens op **volgende**.
3. Op de volgende pagina hello, selecteert u de aangepaste installatiekopie in Hallo lijst en Bevestig dat u Hallo stappen die worden vermeld bij het maken van uw installatiekopie uitgevoerd. Klik op **Volgende**.
4. Voer een naam voor de nieuwe RemoteApp-installatiekopie Hallo Hallo locatie kiezen, en klikt u op Hallo vinkje toostart Hallo-importproces.

> [!NOTE]
> U kunt afbeeldingen importeren uit een Azure-locatie wordt ondersteund door Azure Virtual Machines tooany Azure-locatie wordt ondersteund door Azure RemoteApp. Afhankelijk van Hallo locaties kan Hallo importeren too25 minuten duren.
> 
> 

U bent er nu klaar toocreate uw nieuwe verzameling, ofwel een [cloud](remoteapp-create-cloud-deployment.md) verzameling of [hybride](remoteapp-create-hybrid-deployment.md), afhankelijk van uw behoeften.

