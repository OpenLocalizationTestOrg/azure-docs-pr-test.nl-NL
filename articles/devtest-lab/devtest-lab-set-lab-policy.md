---
title: labbeleidsregels aaaManage in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe toodefine labbeleidsregels zoals VM-groottes, maximum aantal virtuele machines per gebruiker, en automatisering afsluiten.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a>Alle beleidsregels voor een testomgeving in Azure DevTest Labs beheren

Azure DevTest Labs kunt u de kosten te beheren en afval in uw labs minimaliseren door het beleid (instellingen) beheren voor elke lab. In dit artikel wordt stapsgewijs gedetailleerd uitgelegd hoe tooset elk beleid.  

## <a name="set-allowed-virtual-machine-sizes"></a>Set toegestane grootten van virtuele machines
Hallo toegestaan-beleid voor instelling Hallo VM-grootten helpt toominimize lab afval doordat u toospecify welke VM-grootten zijn toegestaan in Hallo lab. Als dit beleid is geactiveerd, zijn alleen VM-grootten uit deze lijst gebruikte toocreate virtuele machines.

1. Op de Hallo lab **configuratie en het beleid** blade Selecteer **toegestane grootten voor virtuele machines**.
   
    ![Grootten van de toegestane virtuele machines](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. Selecteer **op** tooenable dit beleid en **uit** toodisable deze.

1. Als u dit beleid inschakelt, selecteert u een of meer VM-grootten die kunnen worden gemaakt in uw testomgeving.

1. Selecteer **Opslaan**.

## <a name="set-virtual-machines-per-user"></a>Set virtuele machines per gebruiker
beleid voor Hallo **virtuele machines per gebruiker** kunt u toospecify Hallo maximum aantal VM's die kunnen worden gemaakt door een afzonderlijke gebruiker. Als een gebruiker probeert toocreate of claim een virtuele machine wanneer Hallo gebruikerslimiet is bereikt, wordt een foutbericht dat Hallo die VM kan niet worden gemaakt/geclaimd aangeeft. 

1. Op de Hallo lab **configuratie en het beleid** selecteert u **virtuele machines per gebruiker**.
   
    ![Virtuele machines per gebruiker](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Selecteer **Ja** toolimit Hallo aantal virtuele machines per gebruiker. Als u niet dat toolimit Hallo aantal virtuele machines per gebruiker wilt, schakelt u **Nee**. Als u selecteert **Ja**, Geef een numerieke waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt of door een gebruiker geclaimd. 

1. Selecteer **Ja** toolimit Hallo aantal virtuele machines met SSD (SSD-schijf). Als u niet dat toolimit Hallo aantal virtuele machines die SSD gebruiken wilt kunt, selecteert u **Nee**. Als u selecteert **Ja**, voer een waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt met SSD. 

1. Selecteer **Opslaan**.

## <a name="set-virtual-machines-per-lab"></a>Set virtuele machines per lab
beleid voor Hallo **virtuele machines per lab** kunt u toospecify Hallo maximum aantal VM's die kunnen worden gemaakt voor de huidige lab Hallo. Als een gebruiker een virtuele machine toocreate probeert wanneer Hallo lab limiet is bereikt, geeft een foutbericht weergegeven dat Hallo die VM kan niet worden gemaakt. 

1. Op de Hallo lab **configuratie en het beleid** selecteert u **virtuele machines per lab**.
   
    ![Virtuele machines per lab](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. Selecteer **Ja** toolimit Hallo aantal virtuele machines per lab. Als u niet dat toolimit Hallo aantal virtuele machines per lab wilt, selecteert u **Nee**. Als u selecteert **Ja**, Geef een numerieke waarde die aangeeft Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt of door een gebruiker geclaimd. 

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

## <a name="set-expiration-date"></a>Verloopdatum instellen
U kunt een vervaldatum instellen datum wanneer u [Hallo VM maken](devtest-lab-add-vm.md). In **geavanceerde instellingen**, kies Hallo kalender pictogram toospecify een datum waarop Hallo VM automatisch worden verwijderd.  Standaard Hallo VM nooit verloopt.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Volgende stappen
Zodra u hebt gedefinieerd en toegepast Hallo van verschillende instellingen voor virtuele machine voor uw testomgeving, Hier vindt u enkele dingen tootry volgende:

* [Gedeelde IP-adressen begrijpen](devtest-lab-shared-ip.md) -wordt uitgelegd hoe gedeelde IP adressen worden gebruikt in DevTest Labs toominimize Hallo aantal openbare IP-adressen vereist tooconnect tooyour lab virtuele machines.
* [Kostenbeheer van configureren](devtest-lab-configure-cost-management.md) -illustreert hoe toouse hello **maandelijkse geschatte kosten Trend** grafiek  
  tooview Hallo maand geschatte kosten-to-date en Hallo geprojecteerd einde van de maand kosten.
* [Maken van aangepaste installatiekopie](devtest-lab-create-template.md) : wanneer u een virtuele machine, maakt u een basis, kan dit een aangepaste installatiekopie of een Marketplace-installatiekopie opgeven. In dit artikel ziet u hoe toocreate een aangepaste installatiekopie van een VHD-bestand.
* [Configureren van installatiekopieën van Marketplace](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs ondersteunt het maken van virtuele machines op basis van Azure Marketplace-installatiekopieën. Dit artikel wordt beschreven hoe toospecify die, indien aanwezig, Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van virtuele machines in een testomgeving.
* [Een virtuele machine maken in een testomgeving](devtest-lab-add-vm-with-artifacts.md) -ziet u hoe een virtuele machine uit een basisinstallatiekopie toocreate (ofwel aangepaste of Marketplace), en hoe toowork met artefacten in uw virtuele machine.

