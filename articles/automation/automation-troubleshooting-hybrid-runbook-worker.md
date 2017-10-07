---
title: Azure Automation Hybrid Runbook Worker aaaTroubleshoot | Microsoft Docs
description: Hallo symptomen, oorzaken en oplossingen voor Hallo meest voorkomende Hybrid Runbook Worker in Azure Automation problemen beschreven.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: magoedte
ms.openlocfilehash: 292af517c88d1ffd21262a286ccc079e7270bfad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-tips-for-hybrid-runbook-worker"></a>Tips voor probleemoplossing voor hybride Runbook Worker

Dit artikel vindt u hulp het oplossen van problemen die u mogelijk ondervindt met Automation Hybrid Runbook Workers en mogelijke oplossingen tooresolve stelt ze.

## <a name="a-runbook-job-terminates-with-a-status-of-suspended"></a>Een runbooktaak wordt beëindigd met de status onderbroken

Uw runbook is onderbroken kort na tooexecute probeert deze drie keer. Gelden er bepaalde voorwaarden kunnen stuiten Hallo runbook voltooid, en gerelateerde fout het Hallo-bericht bevat geen aanvullende informatie die aangeeft waarom. Dit artikel bevat stappen voor probleemoplossing voor problemen met gerelateerde toohello Hybrid Runbook Worker runbook uitvoering fouten.

Als uw Azure probleem niet wordt besproken in dit artikel, gaat u naar Azure-forums op Hallo [MSDN en Hallo Stack Overflow](https://azure.microsoft.com/support/forums/). U kunt het probleem op deze forums boeken of te[ @AzureSupport op Twitter](https://twitter.com/AzureSupport). U kunt ook een ondersteuning van Azure-aanvraag indienen door te selecteren **ondersteuning krijgen** op Hallo [ondersteuning van Azure](https://azure.microsoft.com/support/options/) site.

### <a name="symptom"></a>Symptoom
Runbook-uitvoering mislukt en Hallo fout is geretourneerd, ' hello taakactie 'Activeren' kan niet worden uitgevoerd, omdat het Hallo-proces onverwacht is gestopt. Hallo taakactie is 3 maal geprobeerd."

Er zijn verschillende mogelijke oorzaken voor Hallo-fout: 

1. Hallo hybride worker zich achter een proxy of firewall
2. Hallo computer Hallo hybride worker wordt uitgevoerd op is kleiner dan de minimale Hallo [hardwarevereisten](automation-offering-get-started.md#hybrid-runbook-worker)  
3. Hallo runbooks verifiëren niet met lokale bronnen

#### <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>1 oorzaak: Hybrid Runbook Worker wordt achter een proxy of firewall
Hallo computer Hallo die Hybrid Runbook Worker wordt uitgevoerd op zich achter een firewall of proxy-server en uitgaande netwerktoegang niet toegestaan of correct geconfigureerd.

#### <a name="solution"></a>Oplossing
Controleer of Hallo computer heeft uitgaande toegang too*.azure-automation.net op poort 443. 

#### <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>2 oorzaak: De Computer is minder dan de minimale hardwarevereisten
Computers met Hallo Hybrid Runbook Worker moet voldoen aan de minimale hardwarevereisten Hallo voordat u deze toohost deze functie. Anders Hallo computer, afhankelijk van het Resourcegebruik van andere achtergrondprocessen en conflicten veroorzaakt door runbooks tijdens het uitvoeren van Hallo, kennis wordt er meer dan worden gebruikt en ervoor zorgen dat de runbook-taak vertragingen of time-outs. 

#### <a name="solution"></a>Oplossing
Controleer eerst aangewezen toorun Hallo Hybrid Runbook Worker functie Hallo-computer voldoet aan de minimale hardwarevereisten Hallo.  Zo ja, monitor CPU en geheugen gebruik toodetermine een correlatie tussen Hallo prestaties van Hybrid Runbook Worker-processen en vensters.  Als er geheugen of CPU-belasting, dit kan wijzen op Hallo nodig tooupgrade of extra processors toevoegen of verhoging van het geheugen tooaddress resource knelpunt Hallo en los Hallo-fout. Selecteer een andere berekeningsresource die u kunt ondersteuning voor de minimale vereisten Hallo en schalen wanneer werkbelasting eisen duiden op dat een verhoging is nodig.         

#### <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>3 oorzaak: Runbooks niet verifiëren met lokale bronnen

#### <a name="solution"></a>Oplossing
Controleer Hallo **Microsoft SMA** gebeurtenislogboek voor een overeenkomstige gebeurtenis met beschrijving *Win32 proces is afgesloten met code [4294967295]*.  Hallo oorzaak van deze fout is u dit nog niet hebt geconfigureerd verificatie in uw runbooks of opgegeven Hallo Run As-referenties voor Hallo Hybrid worker-groep.  Raadpleeg [Runbook-machtigingen](automation-hrw-run-runbooks.md#runbook-permissions) tooconfirm u verificatie juist hebt geconfigureerd voor uw runbooks.  

## <a name="next-steps"></a>Volgende stappen

Zie voor informatie over het oplossen van andere problemen in Automation [het oplossen van veelvoorkomende problemen met Azure Automation](automation-troubleshooting-automation-errors.md) 