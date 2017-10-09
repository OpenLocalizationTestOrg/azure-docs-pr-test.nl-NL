---
title: aaaCreate voor failover en herstel in de Azure Site Recovery-herstelplannen | Microsoft Docs
description: Hierin wordt beschreven hoe toocreate en plannen voor herstel in Azure Site Recovery toofail via aanpassen en virtuele machines en fysieke servers herstellen
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 72408c62-fcb6-4ee2-8ff5-cab1218773f2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 09ca7719e92460b283947fdbe752e8654e5b9cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-recovery-plans"></a>Herstelplannen maken


Dit artikel bevat informatie over het maken en aanpassen in de herstelplannen [Azure Site Recovery](site-recovery-overview.md).

Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

 Herstel plannen toodo Hallo volgende maken:

* Groepen van de machines die samen een failover en start vervolgens samen definiëren.
* Model afhankelijkheden tussen machines, door ze te groeperen samen in een recovery plan groep. Bijvoorbeeld, toofail via en online zetten van een specifieke toepassing, dat u alle Hallo VMs voor die toepassing in Hallo groeperen dezelfde groep voor gegevensherstel plannen.
* Een failover uitvoert. U kunt een test, gepland of niet-geplande failover uitvoeren op een herstelplan.


## <a name="create-a-recovery-plan"></a>Een herstelplan maken

1. Klik op **herstelplannen** > **herstelplan maken**.
   Geef een naam voor het herstelplan hello, en een bron en doel. Hallo bronlocatie moet virtuele machines hebt die zijn ingeschakeld voor failover en herstel.

    - Selecteer voor VMM tooVMM replicatie, **brontype** > **VMM**, en Hallo bron en doel van de VMM-servers. Klik op **Hyper-V** toosee clouds die zijn beveiligd.
    - Selecteer voor de VMM-tooAzure **brontype** > **VMM**.  Selecteer Hallo bron VMM-server en **Azure** als Hallo doel.
    - Voor Hyper-V-replicatie tooAzure (zonder VMM), selecteert u **brontype** > **Hyper-V-site**. Selecteer Hallo site als bron-hello, en **Azure** als Hallo doel.
    - Voor een VMware-VM of een fysieke on-premises server tooAzure, selecteert u een configuratieserver als Hallo-bron en **Azure** als Hallo doel.
    - Selecteer een Azure-regio als Hallo bron en een secundair Azure-regio als Hallo doel voor een herstelplan Azure tooAzure. Hallo secundaire Azure-regio's zijn dat alleen de toowhich virtuele machines worden beveiligd.
2. In **virtuele machines selecteren**, selecteer Hallo virtuele machines (of replicatiegroep) dat u in het herstelplan Hallo tooadd toohello standaardgroep (groep 1) wilt.

## <a name="customize-and-extend-recovery-plans"></a>Aanpassen en uitbreiden herstelplannen

U kunt aanpassen en uitbreiden herstelplannen:

- **Nieuwe groepen toevoegen**: aanvullende herstelpunten plan groepen (omhoog tooseven) toohello standaardgroep toevoegen en voeg vervolgens meer machines of replicatie groepen toothose recovery planningsgroepen. Groepen worden genummerd in Hallo-volgorde op waarin u ze toevoegt. Een virtuele machine of de replicatiegroep, kan alleen worden opgenomen in één herstelpunt plan groep.
- **Toevoegen van een handmatige actie**— u handmatige acties die worden uitgevoerd vóór of na een groep voor gegevensherstel abonnement kunt toevoegen. Wanneer Hallo herstelplan wordt uitgevoerd, wordt gestopt op Hallo punt waar u de handmatige actie Hallo ingevoegd. Een dialoogvenster wordt u gevraagd toospecify dat Hallo handmatige actie is voltooid.
- **Een script toevoegen**— u kunt scripts toevoegen die worden uitgevoerd vóór of na een groep voor gegevensherstel plannen. Wanneer u een script toevoegt, wordt een nieuwe set acties voor Hallo groep toegevoegd. Bijvoorbeeld, een reeks vooraf stappen voor het groep 1 wordt gemaakt met de naam van de Hallo: groep 1: vooraf stappen. Stappen voor alle vooraf wordt vermeld in deze set. U kunt alleen een script op de primaire site Hallo toevoegen als u een VMM-server geïmplementeerd.
- **Toevoegen van Azure-runbooks**— u kunt herstelplannen met Azure runbooks uitbreiden. Bijvoorbeeld: tooautomate taken of toocreate één stap herstel. [Meer informatie](site-recovery-runbook-automation.md).

## <a name="add-scripts"></a>Voeg scripts toe

U kunt de PowerShell-scripts gebruiken in uw plannen voor herstel.

 - Zorg dat de scripts trycatch-blokken gebruikt zodat Hallo uitzonderingen probleemloos worden afgehandeld.
    - Als er een uitzondering in Hallo script, niet meer wordt uitgevoerd en Hallo-taak wordt weergegeven als mislukt.
    - Als een fout optreedt, worden eventuele resterende deel van het Hallo-script niet uitgevoerd.
    - Als er een fout optreedt wanneer u een niet-geplande failover uitvoert, blijft Hallo herstelplan.
    - Als er een fout optreedt wanneer u een geplande failover uitvoert, stopt Hallo herstelplan. U moet toofix Hallo script, Controleer of deze wordt uitgevoerd zoals verwacht en voer vervolgens Hallo herstelplan opnieuw.
- Hallo Write-Host opdracht werkt niet in een herstelplanscript en Hallo script werkt niet. toocreate uitvoert, maak een proxyscript dat op zijn beurt uw belangrijkste script wordt uitgevoerd. Zorg ervoor dat alle uitvoer wordt doorgegeven om via Hallo >> opdracht.
  * Hallo-script wordt geblokkeerd als er binnen 600 seconden wordt niet geretourneerd.
  * Als tooSTDERR wordt uitgeschreven, ingedeeld Hallo script als mislukt. Deze informatie wordt weergegeven in Hallo scriptdetails op worden uitgevoerd.

Als u VMM in uw implementatie:

* Scripts in een herstelplan worden uitgevoerd in context Hallo Hallo VMM-serviceaccount. Zorg ervoor dat dit account heeft leesrechten nodig voor de externe share Hallo welke Hallo script zich bevindt. Test Hallo script toorun op Hallo machtigingsniveau van VMM-service-account.
* VMM-cmdlets worden in Windows PowerShell-module geleverd. Hallo-module is geïnstalleerd wanneer u Hallo VMM-console installeert. Worden kan geladen in uw script, met behulp van de volgende opdracht in de script Hallo Hallo:
   - Import-Module-naam beheer voor virtuele machines. [Meer informatie](https://technet.microsoft.com/library/hh875013.aspx).
* Zorg ervoor dat er ten minste één bibliotheekserver in uw VMM-implementatie. Hallo-bibliotheeksharepad voor een VMM-server is standaard zich lokaal op de VMM-server met de naam van de map Hallo MSCVMMLibrary Hallo.
    * Als uw bibliotheeksharepad externe (of lokale maar niet gedeeld met MSCVMMLibrary), Hallo bestandsshare als volgt configureren (met behulp van \\libserver2.contoso.com\share\ als voorbeeld):
      * Hallo Register-Editor te openen en te navigeren**HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\Azure Site Recovery\Registration**.
      * Hallo-waarde bewerken **ScriptLibraryPath** en plaats deze als \\libserver2.contoso.com\share\. Geef Hallo volledige FQDN-naam. Machtigingen verlenen toohello bestandsshare-locatie.
      * Hallo-script met een gebruikersaccount dat is dezelfde Hallo test zeker de machtigingen zoals Hallo VMM-serviceaccount. Controleert dit of zelfstandige geteste scripts uitvoeren in Hallo dezelfde manier uit als op de herstelplannen. Als volgt instellen Hallo uitvoering beleid toobypass op Hallo VMM-server:
        * Open Hallo 64-bits Windows PowerShell-console met verhoogde bevoegdheden.
        * Type: **Set-executionpolicy bypass**. [Meer informatie](https://technet.microsoft.com/library/ee176961.aspx).

## <a name="add-a-script-or-manual-action-tooa-plan"></a>Een script of een handmatige actie tooa abonnement toevoegen

U kunt een script toohello recovery plan standaardgroep toevoegen nadat u hebt toegevoegd, virtuele machines of replicatie groepen tooit en Hallo abonnement gemaakt.

1. Open Hallo herstelplan.
2. Klik op een item in Hallo **stap** lijst en klik vervolgens op **Script** of **handmatige actie**.
3. Geef aan of toowant tooadd Hallo script of actie vóór of na Hallo item geselecteerd. Gebruik Hallo **omhoog** en **omlaag** knoppen toomove Hallo positie van Hallo script omhoog of omlaag.
4. Als u een VMM-script toevoegen, selecteert u **Failover tooVMM script**. In **scriptpad**, type Hallo relatief pad toohello share. In Hallo VMM onderstaand voorbeeld u Hallo-pad: **\RPScripts\RPScript.PS1**.
5. Als u een Azure automation-boek uitvoeren toevoegt, geeft u hello Azure Automation-account in welke Hallo runbook bevindt en selecteer hello Azure runbookscript geschikt is.
6. Voer een failover van herstelplan hello, toomake ervoor Hallo script werkt zoals verwacht.


### <a name="add-a-vmm-script"></a>Een VMM-script toevoegen

Hebt u een VMM-bronsite, kunt u een script op Hallo VMM-server maken en deze opnemen in uw plan voor herstel.

1. Maak een nieuwe map in Hallo-bibliotheekshare. Bijvoorbeeld: \<VMMServerName > \MSSCVMMLibrary\RPScripts. Plaats het op Hallo bron en doel van de VMM-servers.
2. Hallo-script (bijvoorbeeld RPScript) maken en controleren van de dat test werkt zoals verwacht.
3. Hallo-script op Hallo locatie plaatsen \<VMMServerName > \MSSCVMMLibrary op Hallo bron en doel-VMM-servers.


## <a name="next-steps"></a>Volgende stappen

[Meer informatie](site-recovery-failover.md) over het uitvoeren van failovers.
