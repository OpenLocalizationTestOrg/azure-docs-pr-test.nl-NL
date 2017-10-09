---
title: aaaVM opnieuw starten van onderhoud voor virtuele Linux-machines in Azure | Microsoft Docs
description: De VM opnieuw starten van onderhoud voor virtuele Linux-machines.
services: virtual-machines-linux
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: eb4b92d8-be0f-44f6-a6c3-f8f7efab09fe
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 41caa2e56740cdfa95d2ea67278e5c1d15a174c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vm-restarting-maintenance"></a>Virtuele machine opnieuw te starten onderhoud

Er zijn enkele gevallen waarbij uw virtuele machines worden opgestart vanwege tooplanned onderhoud toohello onderliggende infrastructuur. Alleen indrukwekkende toothe beschikbaarheid van uw virtuele machines die worden gehost in Azure, het volgende Hallo zijn nu beschikbaar voor u toouse:

-   Melding verzonden ten minste 30 dagen vóór het Hallo impact.

-   Zichtbaarheid toohello onderhoudsvensters per elke virtuele machine.

-   Flexibiliteit en beheer bij het instellen van Hallo precieze tijd voor het onderhoud van invloed zijn op uw virtuele machines.

In de iteraties gepland onderhoud in Microsoft Azure. Initiële iteraties hebben kleinere scope in volgorde tooreduce Hallo risico's die zijn betrokken bij het implementeren van nieuwe oplossingen en mogelijkheden. Volgende herhalingen mogelijk meerdere regio's span (nooit van Hallo dezelfde regio twee). Een virtuele machine is opgenomen in een enkel onderhoud iteratie. Als een herhaling wordt afgebroken, worden resterende virtuele machines zijn opgenomen in een andere, toekomstige, herhaling.

Hallo gepland onderhoud herhaling heeft twee fasen: onderhoudsvenster Pre-emptive en een geplande onderhoudsvenster.

Hallo **Pre-emptive onderhoudsvenster** biedt u Hallo flexibiliteit tooinitiate Hallo onderhoud op uw virtuele machines. Op deze manier kunt u zien wanneer uw virtuele machines worden beïnvloed, Hallo reeks Hallo update en Hallo tijd tussen elke VM die wordt onderhouden. U kunt elke VM toosee query of deze is gepland voor onderhoud en controleer of Hallo resultaat van uw laatste verzoek in de gestarte onderhoud.

Hallo **geplande onderhoudsvenster** is wanneer Azure heeft uw virtuele machines voor Hallo onderhoud gepland. Tijdens dit tijdvenster, die in het venster preventieve onderhoud wordt gebruikt, kunt u nog steeds een query voor het onderhoudsvenster hello, maar niet langer kunnen tooorchestrate Hallo onderhoud.

## <a name="availability-considerations-during-planned-maintenance"></a>Overwegingen voor beschikbaarheid tijdens gepland onderhoud 

### <a name="paired-regions"></a>Gekoppelde regio 's

Elke Azure-regio is gekoppeld aan een andere regio binnen Hallo hetzelfde Geografie, een combinatie van regionale samen te maken. Bij het uitvoeren van onderhoud wordt alleen Hallo virtuele Machine-exemplaren in één regio van het paar bijgewerkt in Azure. Bijvoorbeeld bij het bijwerken van virtuele Machines in Noordelijk Centraal, VS hello Azure worden niet bijgewerkt in Zuid-centraal VS virtuele Machines op Hallo hetzelfde moment. Deze update wordt op een ander tijdstip gepland, om failover of taakverdeling tussen regio's mogelijk te maken. Echter andere regio's, zoals Noord-Europa is in onderhoud op Hallo dezelfde tijd als VS-Oost.
Lees meer over [Azure-regio paren](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>Instellen van één exemplaar VMs versus beschikbaarheid of VM-schaalset

Wanneer u een werkbelasting gebruik van virtuele machines in Azure implementeert, kunt u Hallo virtuele machines binnen een toepassing voor hoge beschikbaarheid tooyour tooprovide beschikbaarheidsset maken. Deze configuratie zorgt ervoor dat bij een stroomstoring of een onderhoud gebeurtenissen, ten minste één virtuele machine beschikbaar is.

Afzonderlijke virtuele machines worden in een beschikbaarheidsset verdeeld over van too20 update domeinen. Tijdens gepland onderhoud één updatedomein is dit van invloed op een bepaald moment. Hallo-volgorde van update-domeinen die worden beïnvloed kan niet opeenvolgend doorgaan tijdens gepland onderhoud. Voor één exemplaar VMs (die geen deel uitmaakt van de beschikbaarheidsset), wordt er geen manier toopredict of bepalen welke en hoeveel virtuele machines tegelijk worden beïnvloed.

Virtuele-machineschaalsets zijn van een Azure compute resource waarmee u toodeploy en beheren van een set van identieke virtuele machines als één resource.
Hallo-schaalset biedt vergelijkbare garanties tooan beschikbaarheidsset in de vorm van update-domeinen. 

Zie voor meer informatie over het configureren van uw virtuele machines voor maximale beschikbaarheid [ *beheren van de beschikbaarheid van uw virtuele machines van Windows hello*](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Geplande gebeurtenissen

Azure Metadata Service kunt u toodiscover informatie over de virtuele Machine gehost in Azure. Geplande gebeurtenissen Hallo blootgesteld categorieën, bevat informatie over toekomstige gebeurtenissen (bijvoorbeeld opstarten vereist) zodat uw toepassing kunt voor ze voorbereiden en beperkt wordt onderbroken.

Raadpleeg te voor meer informatie over de geplande gebeurtenissen[Azure metagegevens Service - geplande gebeurtenissen](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Detectie van onderhoud en meldingen

Onderhoudsplanning is zichtbaar toocustomers op Hallo niveau van afzonderlijke virtuele machines. U kunt Azure-portal, API, PowerShell of CLI tooquery voor de preventieve en geplande onderhoudsvensters. Bovendien een melding te ontvangen (e-mail) in geval van Hallo verwachten wanneer (of meerdere) van uw virtuele machines worden beïnvloed tijdens het Hallo.

Zowel preventieve onderhoud en gepland onderhoud fasen beginnen met een melding. Verwacht tooreceive één melding per Azure-abonnement. Hallo-bericht verzonden van het abonnement toohello admin en co-beheerder standaard. U kunt ook configureren Hallo doelgroep voor de melding in onderhoud.

### <a name="view-hello-maintenance-window-in-hello-portal"></a>Weergave Hallo onderhoudsvenster in Hallo-portal 

U kunt gebruiken hello Azure-portal en zoek naar virtuele machines die zijn gepland voor onderhoud.

1.  Meld u aan toohello Azure-portal.

2.  Klik op en open Hallo **virtuele Machines** blade.

3.  Klik op Hallo **kolommen** knop tooopen Hallo lijst met beschikbare kolommen toochoose uit

4.  Selecteer en voeg Hallo **onderhoudsvenster** kolommen. Virtuele machines die zijn ingepland voor onderhoud hebben Hallo onderhoudsvensters opgehaald. Zodra het onderhoud is voltooid of is afgebroken voor is, wordt het onderhoudsvenster is niet meer aangeboden.

### <a name="query-maintenance-details-using-hello-azure-api"></a>Query onderhoud details met hello Azure-API

Gebruik Hallo [VM informatie API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) en zoekt u Hallo exemplaar toodiscover Hallo onderhoud details weergeven op een afzonderlijke virtuele machine. antwoord Hallo bevat Hallo volgende elementen:

  - isCustomerInitiatedMaintenanceAllowed: geeft aan of u nu preventieve opnieuw distribueren op Hallo VM kan initiëren.

  - preMaintenanceWindowStartTime: Hallo begintijd van Hallo preventieve onderhoudsvenster.

  - preMaintenanceWindowEndTime: Hallo eindtijd van Hallo preventieve onderhoudsvenster. Na deze tijd langer u niet kunnen tooinitiate onderhoud op deze virtuele machine.
    
  - maintenanceWindowStartTime: Hallo begintijd van de geplande onderhoudsvenster Hallo wanneer uw virtuele machine worden beïnvloed.

  - maintenanceWindowEndTime: Hallo eindtijd van Hallo geplande onderhoudsvenster.
  
  - lastOperationResultCode: Hallo resultaat van de laatste bewerking in de onderhoudsmodus-implementatie opnieuw uit.
 
  - lastOperationMessage: bericht met een beschrijving Hallo resultaat van de laatste bewerking in de onderhoudsmodus-implementatie opnieuw uit.


## <a name="pre-emptive-redeploy"></a>Preventieve opnieuw distribueren

Preventieve opnieuw distribueren actie biedt Hallo flexibiliteit toocontrol Hallo tijdstip waarop onderhoud toegepaste tooyour virtuele machines in Azure. Gepland onderhoud begint met een preventieve onderhoudsvenster waar u ervoor op de exacte tijd Hallo voor elk van uw virtuele machines toobe opnieuw opgestart kiezen kunt. Hier volgen gebruiksvoorbeelden waarin dergelijke functionaliteit handig is:

-   Onderhoud nodig toobe gecoördineerd met Hallo end klant.

-   geplande onderhoudsvenster Hallo die worden aangeboden door Azure is niet voldoende.
    Kan zijn dat Hallo venster toobe op Hallo drukste tijd van de week gebeurt of te lang is.

-   Voor meerdere exemplaren of -toepassingen met meerdere lagen moet u voldoende tijd tussen twee virtuele machines of een bepaalde reeks toofollow.

Als u voor preventieve opnieuw distribueren op een virtuele machine bellen, gaat de Hallo VM tooan knooppunt al is bijgewerkt en vervolgens wordt deze weer ingeschakeld, alle configuratieopties en bijbehorende bronnen behouden. Terwijl doet, Hallo tijdelijke schijf verloren en dynamische IP-adressen die zijn gekoppeld aan virtuele netwerkinterface worden bijgewerkt.

Preventieve opnieuw distribueren wordt eenmaal per VM ingeschakeld. Als er een fout opgetreden tijdens het Hallo, Hallo-bewerking is afgebroken, Hallo VM wordt niet negatief beïnvloed en het is uitgesloten van Hallo gepland onderhoud herhaling. U wordt in een later tijdstip met een nieuw schema contact en een nieuwe mogelijkheid tooschedule en volgorde Hallo invloed op uw virtuele machines worden aangeboden.
