---
title: beperkingen van aaaAzure Cloud Shell (Preview) | Microsoft Docs
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
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Beperkingen van de Azure-Cloud-Shell
Azure Cloud-Shell heeft Hallo bekende beperkingen:

## <a name="system-state-and-persistence"></a>Systeemstatus en persistentie
Hallo-machine waarmee u uw Cloud-Shell-sessie is tijdelijk en deze wordt gerecycled nadat uw sessie is niet actief is gedurende 20 minuten. Cloud-Shell vereist een bestandsshare toobe gekoppeld. Uw abonnement moet als gevolg hiervan kunnen tooset up opslag resources tooaccess Cloud Shell. Andere overwegingen zijn onder andere:
* Met gekoppelde opslag, alleen de wijzigingen in uw `$Home` directory of `clouddrive` directory blijven bestaan.
* Bestandsshares worden gekoppeld, alleen vanuit uw [regio toegewezen](persisting-shell-storage.md#mount-a-new-clouddrive).
* Azure Files ondersteunt alleen lokaal redundante opslag en geo-redundant storage-accounts.

## <a name="user-permissions"></a>Gebruikersmachtigingen
Machtigingen zijn ingesteld als gewone gebruikers zonder toegang tot sudo. Elke installatie buiten uw `$Home` directory niet bewaard.
Hoewel bepaalde opdrachten binnen Hallo `clouddrive` map zoals `git clone`, beschikt niet over de juiste machtigingen, uw `$Home` directory is gemachtigd.

## <a name="browser-support"></a>Browserondersteuning
Cloud-Shell ondersteunt Hallo nieuwste versies van Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox en Apple Safari. Safari in privé-modus wordt niet ondersteund.

## <a name="copy-and-paste"></a>Kopiëren en plakken
CTRL + C en Ctrl + V werken niet zoals kopiëren en plakken snelkoppelingen in de Cloud-Shell op Windows-machines, gebruikt u Ctrl + Insert en Shift + Insert toocopy- en respectievelijk plakken.

Klik met de rechtermuisknop kopiëren en plakken opties zijn ook beschikbaar, maar met de rechtermuisknop op de functie is onderwerp toobrowser-specifieke Klembord toegang.

## <a name="editing-bashrc"></a>.Bashrc bewerken
Waarschuwing nemen bij het bewerken van .bashrc, in dat geval kan leiden tot onverwachte fouten in de Cloud-Shell.

## <a name="bashhistory"></a>.bash_history
De geschiedenis van bash opdrachten mogelijk inconsistent vanwege Cloud Shell-sessie wordt onderbroken of gelijktijdige sessies.

## <a name="usage-limits"></a>Limieten voor Resourcegebruik
Cloud-Shell is bedoeld voor interactieve gebruiksvoorbeelden. Als gevolg hiervan zijn geen niet-interactieve sessies langlopende beëindigd zonder waarschuwing.

## <a name="network-connectivity"></a>Netwerkverbinding
Eventuele latentie in de Cloud-Shell onderwerp toolocal internetverbinding, Cloud Shell blijft tooattempt toocarry uit instructies die zijn verzonden.

## <a name="next-steps"></a>Volgende stappen
[Cloud-Shell Quick Start](quickstart.md)
