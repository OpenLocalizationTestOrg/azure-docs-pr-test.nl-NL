---
title: Beheer van basic lab-beleid in Azure DevTest Labs | Microsoft Docs
description: Informatie over het aantal basic-beleid (instellingen) voor een testomgeving instellen in DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: ed35d081b191ec41ed9e5970515057a4715c0d59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a>Basic beleid beheren voor een testomgeving in Azure DevTest Labs

Azure DevTest Labs kunt u kosten te beheren en afval in uw labs minimaliseren door het beleid (instellingen) voor elke lab beheren. In dit artikel leert u aan de slag met beleid door leren hoe u kunt twee van de meest kritieke beleidsregels instellen - het aantal virtuele machines (VM) die kan worden gemaakt of door een enkele gebruiker geclaimd beperken en automatisch afsluiten te configureren. Om weer te geven hoe elk lab beleid instelt, Zie het artikel [labbeleidsregels definiëren in Azure DevTest Labs](devtest-lab-set-lab-policy.md).  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a>Toegang tot een lab-beleid in Azure DevTest Labs
De volgende stappen begeleiden u bij het instellen van beleidsregels voor een testomgeving in Azure DevTest Labs:

Als u wilt weergeven (en wijzigen) op het beleid voor een testomgeving, de volgende stappen uit:

1. Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecteer **Meer services** en selecteer in de lijst vervolgens **DevTest Labs**.

1. Selecteer de gewenste testomgeving uit de lijst van labs.   

1. Selecteer **configuratie en het beleid**.

    ![Blade beleidsinstellingen](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. De **configuratie en het beleid** blade bevat een menu met instellingen die u kunt opgeven. Dit artikel behandelt alleen de instellingen voor **virtuele machines per gebruiker** en **automatisch afsluiten**. Zie voor meer informatie over de overige instellingen, [beheren van alle beleidsregels voor een testomgeving in Azure DevTest Labs](./devtest-lab-set-lab-policy.md). 
   
## <a name="set-virtual-machines-per-user"></a>Set virtuele machines per gebruiker
Het beleid voor **virtuele machines per gebruiker** kunt u het maximum aantal VM's die kunnen worden gemaakt door een afzonderlijke gebruiker opgeven. Als een gebruiker probeert te maken of een virtuele machine wanneer de gebruikerslimiet is bereikt, wordt een foutbericht geeft aan dat de virtuele machine kan niet gemaakt/geclaimd worden. 

1. Op de testomgeving **configuratie en het beleid** selecteert u **virtuele machines per gebruiker**.
   
    ![Virtuele machines per gebruiker](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Selecteer **Ja** beperken het aantal virtuele machines per gebruiker. Als u niet beperken het aantal virtuele machines per gebruiker wilt, schakelt u **Nee**. Als u selecteert **Ja**, Geef een numerieke waarde die aangeeft van het maximum aantal VM's die kunnen worden gemaakt of door een gebruiker geclaimd. 

1. Selecteer **Ja** beperken het aantal virtuele machines met SSD (SSD-schijf). Als u niet wilt beperken het aantal virtuele machines die gebruik van SSD **Nee**. Als u selecteert **Ja**, voer een waarde die het maximum aantal VM's die kunnen worden gemaakt met SSD aangeeft. 

1. Selecteer **Opslaan**.

## <a name="set-auto-shutdown"></a>Stel automatisch afsluiten
Het beleid voor automatisch afsluiten helpt te minimaliseren lab verspilling doordat u de tijd die dit lab virtuele machines afsluiten opgeven.

1. Op de testomgeving **configuratie en het beleid** blade Selecteer **automatisch afsluiten**.
   
    ![Automatisch afsluiten](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. Selecteer **op** waarmee dit beleid en **uit** dat u deze uitschakelt.

1. Als u dit beleid inschakelt, geef de tijd (en tijdzone) de alle VM's in het huidige lab af te sluiten.

1. Geef **Ja** of **Nee** voor de optie een melding te verzenden 15 minuten voordat de tijd opgegeven automatisch afsluiten. Als u opgeeft **Ja**, voer een webhook-URL-eindpunt voor het ontvangen van de melding. Zie voor meer informatie over webhooks [maken van een webhook of API-functie voor Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md). 

1. Selecteer **Opslaan**.

    Eenmaal is ingeschakeld, geldt dit beleid voor alle VM's in het huidige lab. Als deze instelling uit een specifieke virtuele machine verwijderen, de VM-blade open en wijzig de **automatisch afsluiten** instelling 

## <a name="set-auto-start"></a>Set automatisch starten
Het beleid voor automatisch starten, kunt u opgeven wanneer de virtuele machines in het huidige lab moeten worden gestart.  

1. Op de testomgeving **configuratie en het beleid** blade Selecteer **automatisch starten**.
   
    ![Automatisch starten](./media/devtest-lab-set-lab-policy/auto-start.png)

2. Selecteer **op** waarmee dit beleid en **uit** dat u deze uitschakelt.

3. Als u dit beleid inschakelt, geeft u het geplande begintijdstip, tijdzone en de dagen van de week waarop de tijd van toepassing is. 

4. Selecteer **Opslaan**.

    Eenmaal is ingeschakeld, wordt dit beleid niet automatisch toegepast op alle virtuele machines in het huidige lab. Als u wilt deze instelling toepast op een specifieke virtuele machine, van de VM-blade open en wijzig de **automatisch starten** instelling 

## <a name="next-steps"></a>Volgende stappen

- [Labbeleidsregels definiëren in Azure DevTest Labs](devtest-lab-set-lab-policy.md) -informatie over het aanpassen van andere labbeleidsregels 
