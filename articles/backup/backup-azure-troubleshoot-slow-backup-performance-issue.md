---
title: aaaTroubleshoot trage back-up van bestanden en mappen in Azure Backup | Microsoft Docs
description: Biedt richtlijnen toohelp het oplossen van problemen diagnosticeren Hallo oorzaak van prestatieproblemen met de Azure Backup
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.assetid: e379180a-db13-4e0c-90e4-28e5dd6f5b14
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 21d79bbd03c2706bc43fcc7c14020cffd6b919c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-backup-of-files-and-folders-in-azure-backup"></a>Problemen met langzame back-ups van bestanden en mappen in Azure Backup
In dit artikel bevat richtlijnen voor probleemoplossing toohelp onderzoeken Hallo oorzaak van trage prestaties van back-up voor bestanden en mappen wanneer u Azure Backup. Wanneer u de Azure Backup agent tooback Hallo van bestanden, kan back-upproces Hallo langer duren dan verwacht. Deze vertraging kan worden veroorzaakt door een of meer van de volgende Hallo:

* [Er zijn prestatieknelpunten op Hallo-computer die wordt back-up.](#cause1)
* [Een ander proces of antivirussoftware verstoort hello Azure Backup-proces.](#cause2)
* [Hallo backup-agent wordt uitgevoerd op Azure een virtuele machine (VM).](#cause3)  
* [U een back-up van een groot aantal (miljoenen) bestanden.](#cause4)

Voordat u begint met het oplossen van problemen, het is raadzaam dat u downloaden en installeren van Hallo [meest recente Azure backup-agent](http://aka.ms/azurebackup_agent). We maken regelmatig updates toohello back-up agent toofix verschillende problemen, onderdelen toevoegen en de prestaties verbeteren.

Ook wordt aangeraden dat u hello bekijkt [Veelgestelde vragen over Azure Backup-service](backup-azure-backup-faq.md) toomake zeker dat u een van de algemene configuratieproblemen Hallo niet ondervindt.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

<a id="cause1"></a>

## <a name="cause-performance-bottlenecks-on-hello-computer"></a>Oorzaak: Prestatieknelpunten op Hallo-computer
Knelpunten op Hallo-computer die wordt back-up kunnen leiden tot vertragingen. Bijvoorbeeld Hallo van de computer de mogelijkheid tooread- of schrijfbewerking toodisk of gegevens van de beschikbare bandbreedte toosend via Hallo-netwerk, kan leiden tot knelpunten.

Windows biedt een ingebouwde functie die wordt aangeroepen [Prestatiemeter](https://technet.microsoft.com/magazine/2008.08.pulse.aspx) (Perfmon) toodetect deze knelpunten.

Hier volgen enkele prestatiemeteritems en de bereiken die handig zijn bij het oplossen van knelpunten voor optimale back-ups zijn.

| Prestatiemeteritems | Status |
| --- | --- |
| Logische schijf (fysieke schijf)--% inactief |• de niet-actieve too50 100% % inactief goed =</br>• de niet-actieve too20 49% % inactief = Monitor of waarschuwing</br>• de niet-actieve too0 19% % inactief essentiële of buiten Spec = |
| Logische schijf (fysieke schijf)--% gem. Schijf per seconde lezen of schrijven |• 0,001 ms too0.015 ms goed =</br>• 0.015 ms too0.025 ms = Monitor of waarschuwing</br>• 0.026 ms of meer = essentiële of buiten Spec |
| Logische schijf (fysieke schijf)--huidige wachtrijlengte voor schijf (voor alle exemplaren) |80 aanvragen voor meer dan 6 minuten |
| Geheugen--niet wisselbaar geheugen: Bytes |• Minder dan 60% van de groep verbruikt goed =<br>• 61% too80% van de groep verbruikt = Monitor of waarschuwing</br>• Groter zijn dan 80% groep verbruikt essentiële of buiten Spec = |
| Geheugen - wisselbaar geheugen: Bytes |• Minder dan 60% van de groep verbruikt goed =</br>• 61% too80% van de groep verbruikt = Monitor of waarschuwing</br>• Groter zijn dan 80% groep verbruikt essentiële of buiten Spec = |
| Geheugen: beschikbare Megabytes |• 50% van het beschikbare geheugen beschikbaar of meer goed =</br>• 25% van het beschikbare geheugen beschikbaar = Monitor</br>• 10% van het beschikbare geheugen beschikbaar = waarschuwing</br>• Minder dan 100 MB of 5% van het beschikbare geheugen beschikbaar essentiële of buiten Spec = |
| Processor--\%processortijd (alle exemplaren) |• Minder dan 60% verbruikt goed =</br>• 61% too90% verbruikt = Monitor of waarschuwing</br>• 91% too100% verbruikt = kritiek |

> [!NOTE]
> Als u vaststelt dat Hallo infrastructuur Hallo stackpad, raden we defragmenteren u Hallo schijven regelmatig voor betere prestaties.
>
>

<a id="cause2"></a>

## <a name="cause-another-process-or-antivirus-software-interfering-with-azure-backup"></a>Oorzaak: Een ander proces of antivirussoftware interactie aangaan met Azure Backup
We hebt enkele exemplaren waarin andere processen in Windows-systeem Hallo hebben negatief worden beïnvloed prestaties van hello Azure Backup agentproces gezien. Als u zowel hello Azure backup-agent en een ander programma tooback van gegevens, of als antivirussoftware wordt uitgevoerd en heeft een vergrendeling op bestanden toobe back-up gemaakt Hallo kunnen meerdere vergrendelingen van bestanden conflicten veroorzaken. In dit geval Hallo back-up kan mislukken of Hallo taak duurt langer dan verwacht.

Hallo aanbeveling in dit scenario is tooturn uitschakelen Hallo of back-uptijd voor Azure Backup agent Hallo Hallo verandert andere toosee back-upprogramma. Normaal gesproken om ervoor te zorgen dat meerdere back-uptaken niet worden uitgevoerd op Hallo hetzelfde moment voldoende tooprevent is ze elkaar beïnvloeden.

Voor antivirusprogramma's, raden we aan dat u de volgende Hallo uitsluiten bestanden en locaties:

* C:\Program Files\Microsoft Azure Recovery Services Agent\bin\cbengine.exe als een proces
* C:\Program Files\Microsoft Azure Recovery Services Agent\ mappen
* Locatie scratchruimte (als u niet-standaardlocatie Hallo)

<a id="cause3"></a>

## <a name="cause-backup-agent-running-on-an-azure-virtual-machine"></a>Oorzaak: Back-up-agent wordt uitgevoerd op een virtuele machine van Azure
Als u Hallo backup-agent op een virtuele machine uitvoert, worden prestaties langzamer dan wanneer u deze op een fysieke computer uitvoert. Dit is normaal vanwege tooIOPS beperkingen.  U kunt echter Hallo prestaties optimaliseren door het overschakelen Hallo gegevensstations waarvan back-up tooAzure Premium-opslag wordt gemaakt. We aan het oplossen van dit probleem werkt en Hallo-oplossing is beschikbaar in een toekomstige release.

<a id="cause4"></a>

## <a name="cause-backing-up-a-large-number-millions-of-files"></a>Oorzaak: Back-ups van een groot aantal (miljoenen) bestanden
Het verplaatsen van een grote hoeveelheid gegevens duurt langer dan het verplaatsen van een kleinere hoeveelheid gegevens. In sommige gevallen kan een back-up is gerelateerd toonot Hallo alleen grootte van het Hallo-gegevens, maar ook Hallo aantal bestanden of mappen. Dit geldt met name wanneer miljoenen kleine bestanden (enkele bytes tooa enkele kilobytes) worden back-up gemaakt.

Dit probleem treedt op omdat terwijl u een back-up Hallo gegevens en tooAzure te verplaatsen, Azure uw bestanden tegelijkertijd is gecatalogiseerd. In sommige gevallen zeldzame Hallo catalogusbewerking duurt mogelijk langer dan verwacht.

Hallo na indicatoren kunt u Hallo knelpunt begrijpen en dienovereenkomstig werken op Hallo volgende stappen:

* **Gebruikersinterface wordt weergegeven voor gegevensoverdracht Hallo**. Hallo gegevens worden nog steeds overgebracht. Hallo netwerkbandbreedte Hallo grootte van gegevens kan worden veroorzaakt door of vertragingen.
* **UI wordt niet uitgevoerd voor de gegevensoverdracht Hallo weergegeven**. Logboeken openen Hallo zich bevindt op C:\Microsoft Azure Recovery Services Agent\Temp en vervolgens controleren op Hallo FileProvider::EndData-vermelding in het Hallo-Logboeken. Deze vermelding geeft aan dat Hallo gegevensoverdracht voltooid en Hallo catalogusbewerking plaatsvindt. Geen back-uptaken Hallo niet annuleren. In plaats daarvan wachten nog even Hallo catalogus bewerking toofinish. Als Hallo probleem zich blijft voordoen, neem dan contact op met [ondersteuning van Azure](https://portal.azure.com/#create/Microsoft.Support).
