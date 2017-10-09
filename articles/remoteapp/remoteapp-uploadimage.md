---
title: aaaUpload een aangepaste installatiekopie voor Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooupload een aangepaste installatiekopie voor Azure RemoteApp
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Een aangepaste installatiekopie uploaden voor Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Nu u de installatiekopie van uw aangepaste sjabloon hebt gemaakt of met wijzigingen bijgewerkt, moet u tooupload die afbeeldingsbibliotheek tooyour Azure RemoteApp-installatiekopie. Volg deze stappen.

## <a name="before-you-start"></a>Voordat u begint
1. Controleer of de aangepaste installatiekopie voldoet aan Hallo [afbeeldingsvereisten](remoteapp-imagereqs.md) en [toepassingsvereisten](remoteapp-appreqs.md).
2. Hallo installeren [Azure PowerShell-module](/powershell/azure/overview).

## <a name="step-by-step-on-how-tooupload-custom-image"></a>Stap voor stap voor het aangepaste installatiekopie tooupload
1. Open Azure Management Portal en navigeer van toohello RemoteApp-pagina.
2. Op Hallo **sjablooninstallatiekopieën** tabblad **uploaden** Hallo Hallo pagina onderaan in.
3. Geef een beschrijvende naam voor uw installatiekopie en Hallo opslagaccountlocatie opgeven. Zorg ervoor dat de locatie Hallo Hallo dezelfde locatie als uw RemoteApp-collectie of een locatie waar u toocreate een.
4. Wanneer u wordt gevraagd, downloaden Hallo script tooyour lokale PC.
5. Hallo opdrachtparameters in Hallo tekst vak tooyour Klembord kopiëren.
6. Open een Windows PowerShell-venster met verhoogde bevoegdheid.
7. Van Hallo met verhoogde bevoegdheden voor Windows PowerShell-venster Navigeren toohello dezelfde map waarin u Hallo script gedownload.
8. Plakken Hallo gekopieerd opdracht en druk op **Enter**.
   
   Hallo uploadproces wordt gestart en duur afhankelijk zijn van veel factoren, waaronder uw netwerksnelheid en de grootte van afbeelding Hallo
9. U kunt uw uploaden mislukt vanwege onderbreking op het netwerk of dingen die, altijd Hallo uploadproces die u begon te hervatten. tooresume een upload Voer Hallo script opnieuw uit met dezelfde Hallo vanaf de opdrachtregel.

> [!WARNING]
> Nooit Hallo uploaden script wijzigen. Specifieke controles zijn geïmplementeerd tooensure die Hallo installatiekopie voldoet aan Hallo installatiekopie van de vereisten en toepassingsvereisten.
> 
> 

## <a name="common-problems"></a>Algemene problemen
* Zorg ervoor dat u Windows PowerShell, niet Azure PowerShell gebruiken. U moet tooinstall hello Azure PowerShell-module omdat bepaalde modules nodig zijn tijdens Hallo uploaden.
* Nooit alter Hallo script, validaties zijn er voor uw gemak.
* Als Hallo vhd-bestand is vergrendeld tijdens het uploaden, Hallo bestand kopiëren of verplaatsen nieuwe locatie en probeer het uploaden van tooa opnieuw. Er is mogelijk een Windows-proces dat voorkomt uploaden dat.  

