---
title: vereisten voor RemoteApp-installatiekopie aaaAzure | Microsoft Docs
description: "Meer informatie over het Hallo-vereisten voor het maken van installatiekopieën toobe gebruikt met Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Vereisten voor Azure RemoteApp-installatiekopieën
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp gebruikt een installatiekopie van Windows Server 2012 R2 toohost alle Hallo-programma's die u wilt de tooshare met uw gebruikers. een aangepaste installatiekopie toocreate, u kunt beginnen met een bestaande installatiekopie of [Maak een nieuwe](remoteapp-create-custom-image.md).

> [!TIP]
> Wist u dat uw Azure RemoteApp-abonnement biedt die u toegang tot Windows Server 2012 R2-afbeelding tooa in de virtuele machine van Azure-galerie waarmee u toocreate uw eigen sjablooninstallatiekopie kunt Hallo? [Het uitchecken](remoteapp-image-on-azurevm.md).  
> 
> 

Hallo-vereisten voor het Hallo-installatiekopie die kan worden geüpload voor gebruik met Azure RemoteApp zijn:

* Aangepaste toepassingen opslaan niet gegevens lokaal op Hallo-installatiekopie. Deze installatiekopieën staatloze zijn en mag alleen toepassingen bevatten.
* Hallo-afbeelding bevat geen gegevens die verbroken worden kunnen.
* Afbeeldingsgrootte Hallo moet een veelvoud van MB. Als u een installatiekopie die is geen exacte veelvoud tooupload probeert, mislukt de Hallo uploaden.
* Hallo afbeeldingsformaat moet 127 GB of kleiner.
* Dit moet een VHD-bestand (VHDX-bestanden worden momenteel niet ondersteund).
* Hallo VHD mag geen virtuele machines van generatie 2.
* Hallo VHD kan een vaste grootte of dynamisch uitbreidbare zijn. Een dynamisch uitbreidbare VHD wordt aanbevolen omdat duurt het minder tijd tooupload tooAzure dan een vaste grootte VHD-bestand.
* Hallo-schijf moet worden geïnitialiseerd met Hallo Master Boot Record (MBR) partitionering stijl. Hallo partitiestijl van GUID partition table (GPT) wordt niet ondersteund.
* Hallo VHD moet één installatie van Windows Server 2012 R2 bevatten. Meerdere volumes, maar slechts één met een installatie van Windows kan bevatten.
* Hallo Remote Desktop Session Host (RDSH)-functie en de functie Bureaubladervaring Hallo moeten worden geïnstalleerd.
* Hallo Remote Desktop Connection Broker-rol moet *niet* worden geïnstalleerd.
* Hallo Encrypting File System (EFS) moet worden uitgeschakeld.
* Hallo-installatiekopie moet SYSPREPed met Hallo parameters **/oobe / generalize/shutdown** (gebruikt Hallo **/mode:vm** parameter).
* Uploaden van uw VHD van een keten van de momentopname wordt niet ondersteund.

Zie [maken van een installatiekopie van een Azure RemoteApp](remoteapp-imageoptions.md) voor meer informatie over het maken van installatiekopieën voor Azure RemoteApp.

