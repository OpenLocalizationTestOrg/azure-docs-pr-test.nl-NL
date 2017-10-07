---
title: basic labbeleidsregels aaaManage in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe tooset aantal basic Hallo-beleid (instellingen) voor een testomgeving in DevTest Labs
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
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a>Basic beleid beheren voor een testomgeving in Azure DevTest Labs

Azure DevTest Labs kunt u toocontrol kosten en afval in uw labs minimaliseren door het beleid (instellingen) beheren voor elke lab. In dit artikel leert u aan de slag met beleid door te leren hoe tooset twee van de meest kritieke beleidsregels Hallo - beperken Hallo aantal virtuele machines (VM) die kan worden gemaakt of door een afzonderlijke gebruiker en automatisch afsluiten configureren geclaimd. tooview hoe tooset elk beleid lab Zie Hallo artikel [labbeleidsregels definiëren in Azure DevTest Labs](devtest-lab-set-lab-policy.md).  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a>Toegang tot een lab-beleid in Azure DevTest Labs
Hallo volgende stappen begeleiden u door het instellen van beleidsregels voor een testomgeving in Azure DevTest Labs:

tooview (en wijzigen) Hallo beleidsregels voor een testomgeving, als volgt te werk:

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.

1. Selecteer de gewenste lab Hallo in lijst Hallo van labs.   

1. Selecteer **configuratie en het beleid**.

    ![Blade beleidsinstellingen](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. Hallo **configuratie en het beleid** blade bevat een menu met instellingen die u kunt opgeven. Dit artikel behandelt alleen Hallo instellingen voor **virtuele machines per gebruiker** en **automatisch afsluiten**. toolearn over Hallo resterende instellingen, Zie [beheren van alle beleidsregels voor een testomgeving in Azure DevTest Labs](./devtest-lab-set-lab-policy.md). 
   
## <a name="set-virtual-machines-per-user"></a>Set virtuele machines per gebruiker
beleid voor Hallo **virtuele machines per gebruiker** kunt u toospecify Hallo maximum aantal VM's die kunnen worden gemaakt door een afzonderlijke gebruiker. Als een gebruiker probeert toocreate of claim een virtuele machine wanneer Hallo gebruikerslimiet is bereikt, wordt een foutbericht dat Hallo die VM kan niet worden gemaakt/geclaimd aangeeft. 

1. Op de Hallo lab **configuratie en het beleid** selecteert u **virtuele machines per gebruiker**.
   
    ![Virtuele machines per gebruiker](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Selecteer **Ja** toolimit Hallo aantal virtuele machines per gebruiker. Als u niet dat toolimit Hallo aantal virtuele machines per gebruiker wilt, schakelt u **Nee**. Als u selecteert **Ja**, Geef een numerieke waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt of door een gebruiker geclaimd. 

1. Selecteer **Ja** toolimit Hallo aantal virtuele machines met SSD (SSD-schijf). Als u niet dat toolimit Hallo aantal virtuele machines die SSD gebruiken wilt kunt, selecteert u **Nee**. Als u selecteert **Ja**, voer een waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt met SSD. 

1. Selecteer **Opslaan**.

## <a name="set-auto-shutdown"></a>Stel automatisch afsluiten
Hallo automatisch afsluiten beleid helpt toominimize lab afval doordat u toospecify Hallo wanneer dit lab VMs afgesloten.

1. Op de Hallo lab **configuratie en het beleid** blade Selecteer **automatisch afsluiten**.
   
    ![Automatisch afsluiten](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. Selecteer **op** tooenable dit beleid en **uit** toodisable deze.

1. Als u dit beleid inschakelt, geef Hallo tijd (en tijdzone) tooshut omlaag alle VM's in de huidige lab Hallo.

1. Geef **Ja** of **Nee** voor Hallo optie toosend een melding 15 minuten voorafgaande toohello automatisch afsluiten tijd opgegeven. Als u opgeeft **Ja**, voer een webhook-URL-eindpunt tooreceive Hallo melding. Zie voor meer informatie over webhooks [maken van een webhook of API-functie voor Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md). 

1. Selecteer **Opslaan**.

    Standaard eenmaal is ingeschakeld, geldt dit beleid tooall virtuele machines in de huidige lab Hallo. Deze instelling van een specifieke virtuele machine, opent u tooremove Hallo van de virtuele machine blade en wijzig de **automatisch afsluiten** instelling 

## <a name="set-auto-start"></a>Set automatisch starten
Hallo automatisch starten van beleid kunt u toospecify wanneer Hallo virtuele machines in de huidige lab Hallo moet worden gestart.  

1. Op het Hallo lab **configuratie en het beleid** blade Selecteer **automatisch starten**.
   
    ![Automatisch starten](./media/devtest-lab-set-lab-policy/auto-start.png)

2. Selecteer **op** tooenable dit beleid en **uit** toodisable deze.

3. Als u dit beleid inschakelt, geef Hallo geplande begintijd, tijdzone en Hallo dagen van de week van Hallo welke Hallo tijd van toepassing is. 

4. Selecteer **Opslaan**.

    Eenmaal is ingeschakeld, dit beleid is niet automatisch toegepast tooany virtuele machines in de huidige lab Hallo. tooapply deze instelling tooa specifieke virtuele machine, blade van open Hallo van de virtuele machine en wijzig de **automatisch starten** instelling 

## <a name="next-steps"></a>Volgende stappen

- [Labbeleidsregels definiëren in Azure DevTest Labs](devtest-lab-set-lab-policy.md) -informatie over hoe toomodify andere labbeleidsregels 
