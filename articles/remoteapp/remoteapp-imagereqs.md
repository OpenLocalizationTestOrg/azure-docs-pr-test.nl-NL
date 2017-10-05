---
title: Azure RemoteApp image-vereisten | Microsoft Docs
description: "Meer informatie over de vereisten voor het maken van installatiekopieën moet worden gebruikt met Azure RemoteApp"
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
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Vereisten voor Azure RemoteApp-installatiekopieën
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp maakt gebruik van een Windows Server 2012 R2-afbeelding voor het hosten van alle programma's die u wilt delen met uw gebruikers. Voor het maken van een aangepaste installatiekopie die u kunt beginnen met een bestaande installatiekopie of [Maak een nieuwe](remoteapp-create-custom-image.md).

> [!TIP]
> Wist u dat uw Azure RemoteApp-abonnement hebt dat u toegang tot een Windows Server 2012 R2-installatiekopie in de galerie van Azure VM die u gebruiken kunt om uw eigen sjablooninstallatiekopie te maken? [Het uitchecken](remoteapp-image-on-azurevm.md).  
> 
> 

De vereisten voor de installatiekopie die kan worden geüpload voor gebruik met Azure RemoteApp zijn:

* Aangepaste toepassingen opslaan niet gegevens lokaal op de installatiekopie. Deze installatiekopieën staatloze zijn en mag alleen toepassingen bevatten.
* De afbeelding bevat geen gegevens die verloren kunnen gaan.
* Grootte van de afbeelding moet een veelvoud van MB. Als u probeert te uploaden van een installatiekopie die is geen exacte veelvoud, mislukt het uploaden.
* Grootte van de installatiekopie moet 127 GB of kleiner.
* Dit moet een VHD-bestand (VHDX-bestanden worden momenteel niet ondersteund).
* De VHD moet geen virtuele machines van generatie 2.
* De VHD kan een vaste grootte of dynamisch uitbreidbare zijn. Een dynamisch uitbreidbare VHD wordt aanbevolen omdat kost het minder tijd om te uploaden naar Azure dan een vaste grootte VHD-bestand.
* De schijf moet worden geïnitialiseerd met behulp van de Record MBR (Master Boot) stijl partitioneren. De partitiestijl GUID partition table (GPT) wordt niet ondersteund.
* De VHD moet één installatie van Windows Server 2012 R2 bevatten. Meerdere volumes, maar slechts één met een installatie van Windows kan bevatten.
* De functie Remote Desktop Session Host (RDSH) en de functie Bureaubladervaring moeten worden geïnstalleerd.
* De extern bureaublad Connection Broker-rol moet *niet* worden geïnstalleerd.
* Het Encrypting File System (EFS) moet worden uitgeschakeld.
* De afbeelding moet met de parameters SYSPREPed **/oobe / generalize/shutdown** (niet gebruik de **/mode:vm** parameter).
* Uploaden van uw VHD van een keten van de momentopname wordt niet ondersteund.

Zie [maken van een installatiekopie van een Azure RemoteApp](remoteapp-imageoptions.md) voor meer informatie over het maken van installatiekopieën voor Azure RemoteApp.

