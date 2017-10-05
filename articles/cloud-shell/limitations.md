---
title: Beperkingen voor Azure Cloud-Shell (Preview) | Microsoft Docs
description: Overzicht van de beperkingen van Azure Cloud Shell
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: e42841b126a9df9240bec3f489589d5ce4a6db80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Beperkingen van de Azure-Cloud-Shell
Azure Cloud-Shell heeft de volgende beperkingen:

## <a name="system-state-and-persistence"></a>Systeemstatus en persistentie
De computer waarmee u uw Cloud-Shell-sessie is tijdelijk en deze wordt gerecycled nadat uw sessie is niet actief is gedurende 20 minuten. Cloud-Shell vereist een bestandsshare te koppelen. Uw abonnement moet als gevolg hiervan kunnen storage-resources instellen voor toegang tot Cloud-Shell. Andere overwegingen zijn onder andere:
* Met gekoppelde opslag, alleen de wijzigingen in uw `$Home` directory of `clouddrive` directory blijven bestaan.
* Bestandsshares worden gekoppeld, alleen vanuit uw [regio toegewezen](persisting-shell-storage.md#mount-a-new-clouddrive).
* Azure Files ondersteunt alleen lokaal redundante opslag en geo-redundant storage-accounts.

## <a name="user-permissions"></a>Gebruikersmachtigingen
Machtigingen zijn ingesteld als gewone gebruikers zonder toegang tot sudo. Elke installatie buiten uw `$Home` directory niet bewaard.
Hoewel bepaalde opdrachten binnen de `clouddrive` map zoals `git clone`, beschikt niet over de juiste machtigingen, uw `$Home` directory is gemachtigd.

## <a name="browser-support"></a>Browserondersteuning
Cloud-Shell biedt ondersteuning voor de nieuwste versies van Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox en Apple Safari. Safari in privé-modus wordt niet ondersteund.

## <a name="copy-and-paste"></a>Kopiëren en plakken
CTRL + C en Ctrl + V niet werken als kopiëren en plakken snelkoppelingen in de Cloud-Shell op Windows-machines, gebruik Ctrl + Insert en Shift + Insert kopiëren en plakken, respectievelijk.

Klik met de rechtermuisknop kopiëren en plakken opties zijn ook beschikbaar, maar met de rechtermuisknop op de functie is onderworpen aan de browser-specifieke Klembord toegang.

## <a name="editing-bashrc"></a>.Bashrc bewerken
Waarschuwing nemen bij het bewerken van .bashrc, in dat geval kan leiden tot onverwachte fouten in de Cloud-Shell.

## <a name="bashhistory"></a>.bash_history
De geschiedenis van bash opdrachten mogelijk inconsistent vanwege Cloud Shell-sessie wordt onderbroken of gelijktijdige sessies.

## <a name="usage-limits"></a>Limieten voor Resourcegebruik
Cloud-Shell is bedoeld voor interactieve gebruiksvoorbeelden. Als gevolg hiervan zijn geen niet-interactieve sessies langlopende beëindigd zonder waarschuwing.

## <a name="network-connectivity"></a>Netwerkverbinding
Eventuele latentie in de Cloud-Shell is onderworpen aan de lokale verbinding met internet, Cloud Shell blijft proberen bij het uitvoeren van de instructies die zijn verzonden.

## <a name="next-steps"></a>Volgende stappen
[Cloud-Shell Quick Start](quickstart.md)
