---
title: aaaPlanning voor de migratie van IaaS-resources van klassieke tooAzure Resource Manager | Microsoft Docs
description: Migratie van IaaS-resources van klassieke tooAzure Resource Manager plannen
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 78492a2c-2694-4023-a7b8-c97d3708dcb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 04/01/2017
ms.author: kasing
ms.openlocfilehash: 7574122d951119db4991187945739b190ef14995
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="planning-for-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Migratie van IaaS-resources van klassieke tooAzure Resource Manager plannen
Hoewel Azure Resource Manager veel mogelijkheden biedt, is het kritieke tooplan uit uw migratie reis toomake zeker dat dingen besturingssysteemupgrades soepel verlopen. Tijd besteedt over het plannen, zorgt u ervoor dat u geen problemen ondervindt tijdens het uitvoeren van de migratieactiviteiten worden bewaakt.

> [!NOTE]
> Hallo richtlijnen te volgen is zwaar ingebrachte tooby hello Azure Customer Advisory team en Cloudoplossing-architecten die werken met klanten op grote omgevingen migreren. Dit document blijft als zodanig tooget bijgewerkt naarmate nieuwe patronen van succes ontstaan, dus probeer terug in tijd tootime toosee als er geen nieuwe aanbevelingen.

Er zijn vier algemene fasen van Hallo migratie reis:<br>

![Fasen van de migratie](../media/virtual-machines-windows-migration-classic-resource-manager/plan-labtest-migrate-beyond.png)

## <a name="plan"></a>Plannen

### <a name="technical-considerations-and-tradeoffs"></a>Technische overwegingen en de voor-en nadelen

Afhankelijk van de grootte van de technische vereisten, locaties en operationele procedures, kunt u tooconsider:

1. Waarom Azure Resource Manager vereist is voor uw organisatie?  Wat zijn Hallo zakelijke redenen voor het migreren?
2. Wat zijn Hallo technische redenen voor Azure Resource Manager?  Wat (indien aanwezig) extra Azure-services wilt u tooleverage?
3. Welke toepassing (of sets van virtuele machines) is opgenomen in Hallo migratie?
4. Welke scenario's worden ondersteund met Hallo migratie API?  Bekijk Hallo [niet-ondersteunde functies en configuraties](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#unsupported-features-and-configurations).
5. Biedt uw operationele teams nu ondersteuning voor toepassingen/virtuele machines in zowel klassieke en Azure Resource Manager?
6. Hoe (als op alle) Azure Resource Manager verandert uw VM-implementatie, beheer, bewaking en rapportage van processen?  Moeten uw implementatiescripts toobe bijgewerkt?
7. Wat is er communicatie Hallo plan tooalert belanghebbenden (eindgebruikers, toepassingseigenaars en eigenaren van infrastructuur)?
8. Afhankelijk van Hallo complexiteit van het Hallo-omgeving, moet er worden een onderhoudsperiode waar Hallo toepassing niet beschikbaar tooend gebruikers en eigenaars tooapplication is?  Zo ja, hoe lang?
9. Wat is er Hallo training plan tooensure belanghebbenden zijn geïnformeerde en kundig in Azure Resource Manager?
10. Wat is Hallo programmamanagement of management projectplanning voor Hallo migratie?
11. Wat zijn Hallo tijdlijnen voor migratie van hello Azure Resource Manager en andere gerelateerde technologie weg maps?  Zijn ze optimaal uitgelijnd?

### <a name="patterns-of-success"></a>Patronen van geslaagd

Geslaagde klanten hebben gedetailleerde plannen waar hello voorgaande vragen zijn besproken, gedocumenteerd en bepaald.  Zorg ervoor dat Hallo migratieplannen zijn grote schaal wordt gecommuniceerd toosponsors en belanghebbenden.  Geef uzelf met kennis over uw opties voor de migratie; lezen door deze migratie-document dat is ingesteld onder wordt sterk aanbevolen.

* [Overzicht van de migratie van IaaS-resources van klassieke tooAzure Resource Manager-platform ondersteund](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Migratie van IaaS-resources van klassieke tooAzure Resource Manager plannen](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [PowerShell toomigrate IaaS resources van klassieke tooAzure Resource Manager gebruiken](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI toomigrate IaaS resources van klassieke tooAzure Resource Manager gebruiken](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Community-hulpprogramma's voor hulp bij de migratie van IaaS-resources van klassieke tooAzure Resource Manager](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Bekijk de meest voorkomende migratiefouten](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Bekijk Hallo veelgestelde meest vragen over migreren IaaS resources van klassieke tooAzure Resource Manager](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="pitfalls-tooavoid"></a>Valkuilen tooavoid

- Fout tooplan.  Hallo technologie stappen voor deze migratie zijn beproefde en Hallo uitkomst is voorspelbaar.
- De veronderstelling dat Hallo ondersteund platform migratie API wordt rekening houdt met alle scenario's. Lees Hallo [niet-ondersteunde functies en configuraties](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#unsupported-features-and-configurations) toounderstand welke scenario's worden ondersteund.
- Mogelijke onderbreking van deze toepassing niet van plan voor eindgebruikers.  Onvoldoende buffer plannen tooadequately waarschuwen eindgebruikers van tijd van de toepassing mogelijk niet beschikbaar.


## <a name="lab-test"></a>Test Lab

**Uw omgeving repliceren en een testmigratie uitvoeren**
  > [!NOTE]
  > Exacte replicatie van uw bestaande omgeving wordt uitgevoerd met behulp van een hulpmiddel community bijgedragen wordt niet officieel ondersteund door Microsoft Support. Daarom is het een **optionele** stap maar het is aanbevolen manier toofind Hallo uit problemen zonder dat u uw productieomgevingen. Als met een hulpprogramma community bijgedragen kan niet worden gebruikt, Lees over Hallo Prepare-valideren/afbreken vulprocedure aanbeveling hieronder.
  >

  Uitvoering van een test lab van uw exacte scenario (compute, netwerk en opslag) is Hallo aanbevolen manier tooensure een soepele migratie. Dit helpt ervoor te zorgen:

  - Een geheel afzonderlijke testomgeving of een bestaande niet-productieomgeving tootest. U wordt aangeraden een geheel afzonderlijke lab die herhaaldelijk kan worden gemigreerd en destructief kan worden gewijzigd.  Scripts toocollect/hydraat metagegevens uit Hallo echte abonnementen worden hieronder vermeld.
  - Het is een goed idee toocreate Hallo lab in een apart abonnement. Hallo reden is dat Hallo lab verwijderd herhaaldelijk en met een afzonderlijke, geïsoleerde abonnement Hallo kans verminderen dat er iets echt per ongeluk verwijderd.

  Dit kan worden bewerkstelligd met Hallo AsmMetadataParser hulpprogramma. [Lees meer over dit hulpprogramma hier](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

### <a name="patterns-of-success"></a>Patronen van geslaagd

Hallo volgende zijn problemen ontdekt in veel grotere Hallo-migraties. Dit is geen uitputtende lijst en raadpleegt u toohello [niet-ondersteunde functies en configuraties](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#unsupported-features-and-configurations) voor meer informatie.  U kan of kan geen deze technische problemen ondervinden, maar als u dit doet het oplossen van deze voordat u de migratie een soepeler ervaring zorgt ervoor.

- **Een voorbereiden-valideren/afbreken vulprocedure doen** -dit is mogelijk Hallo belangrijkste stap tooensure klassieke tooAzure Resource Manager migratie geslaagd. Hallo migratie API zijn drie stappen: valideren, voorbereiden en vastleggen. Valideren wordt Hallo status van uw omgeving klassieke lezen en een resultaat van alle problemen te retourneren. Echter, omdat sommige problemen kunnen bestaan in hello Azure Resource Manager-stack, valideren zal niet alles onderscheppen. volgende stap in het migratieproces Hallo voorbereiden kunt weergeven die problemen. Voorbereiden wordt verplaatsen Hallo van metagegevens uit klassieke tooAzure Resource Manager, maar wordt niet doorvoeren Hallo verplaatsen, en zal niet verwijderen of wijzigen iets op Hallo klassieke aan clientzijde. Hallo vulprocedure omvat het Hallo-migratie voorbereiden en vervolgens wordt afgebroken (**niet doorvoeren**) Hallo migratie voorbereiden. Hallo-doel van vulprocedure valideren/voorbereiden/afbreken is toosee alle Hallo metagegevens in Azure Resource Manager-stack hello, van het onderzoeken (*via programmacode of via de Portal*), en controleer of alles correct migreert en doorlopen technische problemen.  Ook krijgt u een idee van de duur van de migratie zodat u voor downtime dienovereenkomstig plannen kunt.  Een valideren/voorbereiden/afbreken veroorzaakt geen gebruiker uitvaltijd; Daarom is het gebruik van een ononderbroken tooapplication.
  - Hallo onderstaande items kunnen worden opgelost voordat Hallo vulprocedure toobe moet echter een test-test wordt ook gewoon uit deze voorbereidende stappen leegmaken als ze zijn gemist. Tijdens de migratie van de onderneming, hebben we Hallo test toobe voorbereiding op een veilige en waardevol zijn manier tooensure de migratie gevonden.
  - Wanneer voorbereidt wordt uitgevoerd, Hallo besturingselement vlak (Azure beheerbewerkingen) wordt vergrendeld voor de hele virtuele netwerk hello, dus er kunnen geen wijzigingen worden aangebracht tooVM metagegevens tijdens het valideren/voorbereiden/afbreken.  Maar anders een functie van de toepassing (extern bureaublad, VM-gebruik, enz.) niet worden gewijzigd.  Gebruikers van virtuele machines Hallo dan niet weet dat vulprocedure hello wordt uitgevoerd.

- **Express Route-Circuits en VPN-**. Momenteel kunnen niet Express Route-Gateways met autorisatie koppelingen worden gemigreerd zonder uitvaltijd. Zie voor een tijdelijke oplossing Hallo [migreren ExpressRoute-circuits en bijbehorende virtuele netwerken vanuit Hallo klassieke toohello Resource Manager-implementatiemodel](../../expressroute/expressroute-migration-classic-resource-manager.md).

- **VM-extensies** -extensies van virtuele Machine worden mogelijk een van de Hallo grootste problemen toomigrating VM's worden uitgevoerd. Herstel van de VM-extensies kan al 1-2 dagen duren, dus plan dienovereenkomstig.  Een werkende Azure-agent is benodigde tooreport back VM-extensie status van actieve virtuele machines. Als Hallo status weer wordt als beschadigd voor een actieve virtuele machine, is deze migratie wordt gestopt. Hallo-agent zelf wordt niet moet toobe bedrijfsklaar tooenable migratie, maar als uitbreidingen op het bestaat Hallo VM, en vervolgens zowel een agent werkt en uitgaande internetverbinding (met DNS) nodig voor migratie toomove doorsturen zijn.
  - Als verbinding tooa DNS-server verbroken tijdens de migratie alle VM-extensies, met uitzondering van BGInfo versie 1 wordt. \* moet toofirst worden verwijderd uit elke VM voordat voorbereiden voor migratie en vervolgens opnieuw toevoegen back toohello VM na de migratie van Azure Resource Manager.  **Dit is alleen voor virtuele machines die worden uitgevoerd.**  Als VMs Hallo zijn gestopt toewijzing ongedaan is gemaakt, nodig VM-extensies toobe verwijderd niet.

  > [!NOTE]
  > Veel extensies zoals Azure diagnostics en security center controle zal zichzelf opnieuw installeren na de migratie, dus te verwijderen is geen probleem.

  - Bovendien moet ervoor Netwerkbeveiligingsgroepen niet uitgaande toegang tot internet beperken. Dit kan gebeuren bij sommige configuraties Netwerkbeveiligingsgroepen. Uitgaande toegang tot internet (en DNS) nodig is voor VM-extensies toobe gemigreerd tooAzure Resource Manager.
  - Twee versies van Hallo BGInfo-extensie bestaan en versie 1 en 2 worden genoemd.  

      - Als Hallo VM Hallo BGInfo-extensie voor versie 1 gebruikt, kunt u deze extensie is. Hallo migratie API slaat deze extensie. Hallo BGInfo-extensie kan worden toegevoegd na de migratie.
      - Als Hallo VM Hallo JSON gebaseerde BGInfo versie 2-extensie gebruikt, moet door Hallo VM is gemaakt met hello Azure-portal. Hallo migratie API bevat deze extensie Hallo migratie tooAzure Resource Manager worden opgegeven Hallo agent werkt en uitgaande toegang tot internet (en DNS) heeft.

  - **Herstel optie 1**. Als u weet dat uw virtuele machines geen uitgaande internet toegang tot een werkende DNS-service, en werkt de Azure-agents op Hallo virtuele machines, verwijdert u alle VM-extensies als onderdeel van de migratie Hallo voordat voorbereiden, opnieuw installeren van de VM-extensies Hallo na de migratie.
  - **Herstel optie 2**. VM-extensies te groot is van een drempel, een andere optie is als tooshutdown/toewijzing alle VM's vóór de migratie. Hallo ongedaan van virtuele machines te migreren, start daarna deze op Hallo Azure Resource Manager-zijde. Hier Hallo voordeel is dat de VM-extensies worden gemigreerd. Hallo nadeel is dat alle openbare geconfronteerd met virtuele IP's verloren gaan (kan dit een niet-starter), en natuurlijk Hallo VMs afgesloten waardoor een veel grotere invloed op toepassingen werken.

    > [!NOTE]
    > Als een Azure Security Center-beleid is geconfigureerd op basis van Hallo uitgevoerde VM's die wordt gemigreerd, Hallo beveiligingsbeleid moet toobe gestopt voordat u uitbreidingen verwijdert, anders Hallo beveiliging controle-extensie wordt automatisch opnieuw geïnstalleerd op VM na Hallo verwijdert het.

- **Beschikbaarheidssets** : voor een virtueel netwerk (vNet) toobe gemigreerd tooAzure Resource Manager, Hallo klassieke implementatie (dat wil zeggen cloudservice) bevat virtuele machines moet deel uitmaken van één beschikbaarheidsset of Hallo VMs moet niet in een beschikbaarheidsset. Met meer dan één beschikbaarheidsset in Hallo-cloudservice is niet compatibel met Azure Resource Manager en migratie wordt gestopt.  Er kan niet ook een aantal virtuele machines in een beschikbaarheidsset en een aantal virtuele machines niet in een beschikbaarheidsset. tooresolve, of u kunt wordt tooremediate verplaatsen van de cloudservice.  Plan dienovereenkomstig dit wordt mogelijk veel tijd in beslag.

- **Implementaties van de rol web/Worker** -Cloud-Services met web-en werkrollen tooAzure Resource Manager kan niet worden gemigreerd. Hallo web/werkrollen worden eerst verwijderd van het virtuele netwerk Hallo voordat de migratie kunt starten.  Een gangbare oplossing is toojust verplaatsen web/worker-rol exemplaren tooa afzonderlijke klassiek virtueel netwerk dat ook Gekoppelde tooan ExpressRoute-circuit of toomigrate Hallo code toonewer PaaS App Services (deze bespreking valt buiten bereik Hallo van dit document). In Hallo voormalige geval implementeren, een nieuwe klassiek virtueel netwerk maken, verplaatsen/opnieuw distribueren Hallo web/worker rollen toothat nieuw virtueel netwerk en Hallo implementaties verwijderd uit Hallo virtueel netwerk worden verplaatst. Er zijn geen codewijzigingen is vereist. Hallo nieuwe [virtuele netwerk Peering](../../virtual-network/virtual-network-peering-overview.md) mogelijkheid kan gebruikte toopeer samen Hallo klassiek virtueel netwerk met Hallo web/worker rollen en andere virtuele netwerken in dezelfde Azure-regio zoals Hallo virtueel netwerk wordt Hallo gemigreerd (**nadat het virtuele netwerkmigratie is voltooid, zoals virtuele netwerken brengen kunnen niet worden gemigreerd**), dus dezelfde mogelijkheden om Hallo voorzien zonder prestatieverlies en geen sancties latentie/bandbreedte. Hallo toevoeging van gegeven [virtuele netwerk Peering](../../virtual-network/virtual-network-peering-overview.md), web/worker-rolimplementaties kunnen nu eenvoudig worden opgevangen en niet blokkeren Hallo migratie tooAzure Resource Manager.

- **Azure Resource Manager-quota** -Azure-regio's hebben afzonderlijke quota/limieten voor zowel klassieke en Azure Resource Manager. Hoewel in een migratiescenario nieuwe hardware is niet worden verbruikt *(we je bestaande virtuele machines van klassieke tooAzure Resource Manager wisselen)*, nog moeten toobe op locatie met voldoende capaciteit voor Azure Resource Manager-quota migratie kunt starten. Hieronder vindt belangrijke Hallo-limieten die we hebt gezien problemen veroorzaken.  Open een quotum ondersteuning ticket tooraise Hallo beperkt.

    > [!NOTE]
    > Deze limieten moeten toobe opgetreden in dezelfde regio Hallo als uw huidige omgeving toobe gemigreerd.
    >

    - Netwerkinterfaces
    - Taakverdelers
    - Openbare IP-adressen
    - Statische openbare IP-adressen
    - Cores
    - Netwerkbeveiligingsgroepen
    - Routetabellen

    U kunt uw huidige Azure Resource Manager-quota's Hallo Hallo meest recente versie van Azure PowerShell-opdrachten te volgen met controleren.

    **COMPUTE** *(kernen, Beschikbaarheidssets)*

    ```powershell
    Get-AzureRmVMUsage -Location <azure-region>
    ```

    **Netwerk** *(virtuele netwerken, statische openbare IP-adressen, openbare IP-adressen, de Netwerkbeveiligingsgroepen Network Interfaces, Load Balancers routetabellen)*

    ```powershell
    Get-AzureRmUsage /subscriptions/<subscription-id>/providers/Microsoft.Network/locations/<azure-region> -ApiVersion 2016-03-30 | Format-Table
    ```

    **Opslag** *(Storage-Account)*

    ```powershell
    Get-AzureRmStorageUsage
    ```

- **Azure Resource Manager-API beperking limieten** - als er een groot genoeg omgeving (bv. > 400 VM's in een VNET), kunt u Hallo standaard API beperking limieten voor schrijfacties bereikt (momenteel `1200 writes/hour`) in Azure Resource Manager. Voordat u de migratie, u moet een ticket ondersteuning tooincrease deze grens verhogen voor uw abonnement.


- **Inrichting is een time-out opgetreden van VM-Status** - als een virtuele machine Hallo status van heeft `provisioning timed out`, deze behoeften toobe opgelost vóór de migratie. Hallo alleen toodo dit is uitvaltijd door het opheffen van inrichting/reprovisioning Hallo VM (verwijderen, bewaar Hallo schijf, en maak deze opnieuw Hallo VM).

- **VM-Status RoleStateUnknown** - als de migratie wordt afgebroken vanwege tooa `role state unknown` fout bericht wordt weergegeven, inspecteren Hallo VM die gebruikmaakt van Hallo-portal en zorg ervoor dat deze wordt uitgevoerd. Deze fout wordt meestal opgeslagen gaat van de eigenaar (geen herstel mogelijk vereist) na een paar minuten en is vaak een tijdelijke type vaak zichtbaar tijdens een virtuele Machine `start`, `stop`, `restart` bewerkingen. **Aanbevolen praktijken:** migratie opnieuw na een paar minuten opnieuw proberen.

- **Fabric-Cluster bestaat niet** - In sommige gevallen bepaalde VMs oneven redenen kunnen niet worden gemigreerd. Een van deze bekende gevallen is als Hallo VM onlangs is gemaakt (binnen of dus Hallo afgelopen week) en is er gebeurd tooland een Azure-cluster die nog niet is uitgerust voor werkbelastingen met Azure Resource Manager.  U krijgt een foutmelding waarin wordt gemeld `fabric cluster does not exist` en hello VM kan niet worden gemigreerd. Wacht een paar dagen wordt doorgaans bepaald kunt dit probleem oplossen als Hallo cluster binnenkort Azure Resource Manager is ingeschakeld krijgt. Een onmiddellijke tijdelijke oplossing is echter te`stop-deallocate` Hallo VM en vervolgens doorgaan doorsturen met migratie en start Hallo VM back-up in Azure Resource Manager na de migratie.

### <a name="pitfalls-tooavoid"></a>Valkuilen tooavoid

- Sneltoetsen en weglaten Hallo valideren/voorbereiden/afbreken vulprocedure migraties niet.
- Meest, als niet alle, wordt van uw potentiële problemen surface tijdens Hallo valideren/voorbereiden/afbreken stappen.

## <a name="migration"></a>Migratie

### <a name="technical-considerations-and-tradeoffs"></a>Technische overwegingen en de voor-en nadelen

U bent nu klaar omdat u via Hallo bekende problemen met uw omgeving hebt gewerkt.

U kunt voor Hallo echte migraties, tooconsider:

1. Plan en plannen van Hallo virtueel netwerk (waarbij de kleinste eenheid van de migratie) met de prioriteit verhogen.  Eenvoudige virtuele netwerken eerst Hallo en uitgevoerd met Hallo meer gecompliceerde virtuele netwerken.
2. De meeste klanten hebben niet-productieve en productieomgevingen.  De laatste productie plannen.
3. **(OPTIONEEL)**  Plannen van een uitvaltijd onderhoud met veel van de buffer voor het geval zich onverwachte problemen voordoen.
4. Communicatie met en zijn afgestemd op uw ondersteuningsteams als zich problemen voordoen.

### <a name="patterns-of-success"></a>Patronen van geslaagd

technische richtlijnen van Hallo Hallo _Test Lab_ sectie rekening en eerdere tooa echte migratie verholpen.  Met voldoende testen, is het Hallo-migratie daadwerkelijk een gebeurtenisafhankelijke.  Voor productieomgevingen, is mogelijk handig toohave aanvullende ondersteuning, zoals een vertrouwde Microsoft-partner of Microsoft Premier-services.

### <a name="pitfalls-tooavoid"></a>Valkuilen tooavoid

Niet volledig testen kan problemen veroorzaken en vertraging in Hallo-migratie.  

## <a name="beyond-migration"></a>Na migratie

### <a name="technical-considerations-and-tradeoffs"></a>Technische overwegingen en de voor-en nadelen

Nu dat u in Azure Resource Manager, maximaliseren Hallo-platform.  Lees Hallo [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) toofind uit over extra voordelen.

Tooconsider dingen:

- Bundeling Hallo migratie met andere activiteiten.  De meeste klanten ervoor kiezen voor een onderhoudsvenster van toepassing.  Als het geval is, kunt u toouse deze uitvaltijd tooenable andere mogelijkheden van Azure Resource Manager, zoals versleuteling en migratie tooManaged schijven.
- Terugkeren naar Hallo technische en zakelijke redenen voor Azure Resource Manager; Hallo extra services alleen beschikbaar op Azure Resource Manager die van toepassing zijn tooyour omgeving inschakelen.
- Moderniseren uw omgeving met PaaS-services.

### <a name="patterns-of-success"></a>Patronen van geslaagd

Worden doelgericht op wat u nu wilt tooenable in Azure Resource Manager-services.  Veel klanten zoeken Hallo hieronder dwingende voor Azure-omgevingen:

- [Toegangsbeheer op basis van rollen](../../azure-resource-manager/resource-group-overview.md#access-control).
- [Azure Resource Manager-sjablonen voor de implementatie van eenvoudiger en meer gecontroleerde](../../azure-resource-manager/resource-group-overview.md#template-deployment).
- [Labels](../../azure-resource-manager/resource-group-using-tags.md).
- [Controle van de activiteit](../../azure-resource-manager/resource-group-audit.md)
- [Bronbeleid](../../azure-resource-manager/resource-manager-policy.md)

### <a name="pitfalls-tooavoid"></a>Valkuilen tooavoid

Houd er rekening mee waarom u deze reis klassieke tooAzure Resource Manager-migratie gestart.  Wat zijn de oorspronkelijke zakelijke redenen Hallo? U Hallo zakelijke reden bereiken?


## <a name="next-steps"></a>Volgende stappen

* [Overzicht van de migratie van IaaS-resources van klassieke tooAzure Resource Manager-platform ondersteund](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [PowerShell toomigrate IaaS resources van klassieke tooAzure Resource Manager gebruiken](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI toomigrate IaaS resources van klassieke tooAzure Resource Manager gebruiken](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Community-hulpprogramma's voor hulp bij de migratie van IaaS-resources van klassieke tooAzure Resource Manager](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Bekijk de meest voorkomende migratiefouten](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Bekijk Hallo veelgestelde meest vragen over migreren IaaS resources van klassieke tooAzure Resource Manager](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
