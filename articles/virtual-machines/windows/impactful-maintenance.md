---
title: Indrukwekkende onderhoud voor Windows-machines in Azure | Microsoft Docs
description: Indrukwekkende onderhoud voor Windows virtuele machines.
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 75cd4d567deb98e5d2498dc607b43dae483f1c94
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="impactful-maintenance-for-virtual-machines"></a>Indrukwekkende onderhoud voor virtuele machines

Er zijn enkele gevallen waarbij uw virtuele machines worden opgestart vanwege gepland onderhoud aan de onderliggende infrastructuur. Alleen indrukwekkende om de beschikbaarheid van uw virtuele machines die worden gehost in Azure, zijn het volgende nu beschikbaar moet worden gebruikt:

-   Melding verzonden ten minste 30 dagen vóór de impact.

-   Zichtbaarheid van de onderhoudsvensters per elke virtuele machine.

-   Flexibiliteit en beheer bij het instellen van de precieze tijd voor het onderhoud van invloed zijn op uw virtuele machines.

In de iteraties gepland onderhoud in Microsoft Azure. Initiële iteraties hebben kleiner bereik om te reduceren het risico voor het implementeren van nieuwe oplossingen en mogelijkheden. Volgende herhalingen mogelijk meerdere regio's (nooit van dezelfde regio twee) omvatten. Een virtuele machine is opgenomen in een enkel onderhoud iteratie. Als een herhaling wordt afgebroken, worden resterende virtuele machines zijn opgenomen in een andere, toekomstige, herhaling.

De herhaling gepland onderhoud heeft twee fasen: onderhoudsvenster Pre-emptive en een geplande onderhoudsvenster.

De **Pre-emptive onderhoudsvenster** biedt u de flexibiliteit om te initiëren, het onderhoud op uw virtuele machines. Op deze manier kunt u bepalen wanneer uw virtuele machines worden beïnvloed, de volgorde van de update en de tijd tussen elke VM die wordt onderhouden. U kunt elke virtuele machine om te zien of deze is gepland voor het onderhoud van een query en controleer of het resultaat van uw laatste verzoek in de gestarte onderhoud.

De **geplande onderhoudsvenster** is wanneer Azure heeft uw virtuele machines voor het onderhoud gepland. Tijdens dit tijdvenster, die in het venster preventieve onderhoud wordt gebruikt, kunt u nog steeds een query voor het onderhoudsvenster, maar kunt u het onderhoud indeelt niet langer.

## <a name="availability-considerations-during-planned-maintenance"></a>Overwegingen voor beschikbaarheid tijdens gepland onderhoud 

### <a name="paired-regions"></a>Gekoppelde regio 's

Elke Azure-regio is gekoppeld aan een andere regio binnen de dezelfde Geografie, een combinatie van regionale samen te maken. Bij het uitvoeren van onderhoud wordt alleen de virtuele Machine-exemplaren in één regio van het paar bijgewerkt in Azure. Wanneer bijvoorbeeld de virtuele machines in Noord-centraal VS worden bijgewerkt, worden er tegelijkertijd geen virtuele machines in Zuid-centraal VS bijgewerkt. Deze update wordt op een ander tijdstip gepland, om failover of taakverdeling tussen regio's mogelijk te maken. Tegelijkertijd met VS - oost kan er echter wel onderhoud plaatsvinden in andere regio's, zoals Noord-Europa.
Lees meer over [Azure-regio paren](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>Vs van één exemplaar virtuele machines. Beschikbaarheidsset of VM-schaalset

Wanneer u een werkbelasting gebruik van virtuele machines in Azure implementeert, kunt u de virtuele machines binnen een beschikbaarheidsset om maximale beschikbaarheid voor uw toepassing. Deze configuratie zorgt ervoor dat bij een stroomstoring of een onderhoud gebeurtenissen, ten minste één virtuele machine beschikbaar is.

Afzonderlijke virtuele machines worden in een beschikbaarheidsset verdeeld over maximaal 20 update-domeinen. Tijdens gepland onderhoud één updatedomein is dit van invloed op een bepaald moment. De volgorde van update-domeinen die worden beïnvloed kan niet opeenvolgend doorgaan tijdens gepland onderhoud. Voor één exemplaar virtuele machines (die geen deel uitmaakt van de beschikbaarheidsset) is er geen manier om te voorspellen of bepalen welke en hoeveel virtuele machines tegelijk worden beïnvloed.

Virtuele-machineschaalsets zijn een Azure compute resource waarmee u kunt implementeren en beheren van een set van identieke virtuele machines als één bron.
De schaalaanpassingsset biedt vergelijkbare garandeert een beschikbaarheid instellen in de vorm van update-domeinen. 

Zie voor meer informatie over het configureren van uw virtuele machines voor maximale beschikbaarheid [ *beheren van de beschikbaarheid van uw virtuele machines van Windows*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Geplande gebeurtenissen

Azure Metadata Service kunt u voor het detecteren van informatie over de virtuele Machine gehost in Azure. Geplande gebeurtenissen, een van de zichtbare categorieën, bevat informatie over toekomstige gebeurtenissen (bijvoorbeeld opstarten vereist) zodat uw toepassing kunt voor ze voorbereiden en beperkt wordt onderbroken.

Raadpleeg voor meer informatie over geplande gebeurtenissen [Azure metagegevens Service - geplande gebeurtenissen](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Detectie van onderhoud en meldingen

Onderhoudsplanning is zichtbaar voor klanten op het niveau van afzonderlijke virtuele machines. U kunt Azure-portal, API, PowerShell of CLI query voor de preventieve en geplande onderhoudsvensters. Bovendien verwacht een melding te ontvangen (e-mail) in het geval waarbij een of meer van uw virtuele machines zijn beïnvloed tijdens het proces.

Zowel preventieve onderhoud en gepland onderhoud fasen beginnen met een melding. Verwacht te ontvangen van één melding per Azure-abonnement. De melding wordt verzonden naar de beheerder van het abonnement en de co-beheerder standaard. U kunt ook de doelgroep voor de melding onderhoud configureren.

### <a name="view-the-maintenance-window-in-the-portal"></a>Het onderhoudsvenster weergeven in de portal 

U kunt de Azure portal gebruiken en zoekt u naar virtuele machines die zijn gepland voor onderhoud.

1.  Meld u aan bij Azure Portal.

2.  Klik op en open de **virtuele Machines** blade.

3.  Klik op de **kolommen** te openen van de lijst met beschikbare kolommen kiezen

4.  Selecteer en voeg de **onderhoudsvenster** kolommen. Virtuele machines die zijn ingepland voor onderhoud hebben de onderhoudsvensters opgehaald. Zodra het onderhoud is voltooid of is afgebroken voor is, wordt het onderhoudsvenster is niet meer aangeboden.

### <a name="query-maintenance-details-using-the-azure-api"></a>Query onderhoud details met de Azure-API

Gebruik de [VM informatie API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) en zoekt u de weergave exemplaar om de details van het onderhoud op een afzonderlijke virtuele machine te detecteren. Het antwoord bevat de volgende elementen:

  - isCustomerInitiatedMaintenanceAllowed: geeft aan of u nu preventieve opnieuw op de virtuele machine kan initiëren.

  - preMaintenanceWindowStartTime: de begintijd van de preventieve onderhoudsvenster.

  - preMaintenanceWindowEndTime: de eindtijd van het venster preventieve onderhoud. Na deze tijd moet zich u niet langer onderhoud op deze virtuele machine starten.
    
  - maintenanceWindowStartTime: de begintijd van uw virtuele machine zijn van invloed op het geplande onderhoudsvenster.

  - maintenanceWindowEndTime: de eindtijd van het geplande onderhoudsvenster.
  
  - lastOperationResultCode: het resultaat van de laatste bewerking in de onderhoudsmodus-implementatie opnieuw uit.
 
  - lastOperationMessage: bericht met een beschrijving van het resultaat van de laatste bewerking in de onderhoudsmodus-implementatie opnieuw uit.

## <a name="pre-emptive-redeploy"></a>Preventieve opnieuw distribueren

In dat geval preventieve actie biedt de flexibiliteit om te bepalen van de tijd wanneer de onderhoudsmodus wordt toegepast op uw virtuele machines in Azure. Gepland onderhoud begint met een preventieve onderhoudsvenster waar u kunt op de exacte tijd voor elk van uw virtuele machines opnieuw worden opgestart. Hier volgen gebruiksvoorbeelden waarin dergelijke functionaliteit handig is:

-   Onderhoud moet worden gecoördineerd met de klant.

-   Het geplande onderhoudsvenster die worden aangeboden door Azure is niet voldoende.
    Kan zijn dat het venster gebeurt op de drukste tijd van de week of te lang is.

-   Voor meerdere exemplaren of -toepassingen met meerdere lagen moet u voldoende tijd tussen twee virtuele machines of een bepaalde volgorde te volgen.

Wanneer u voor de implementatie op een virtuele machine preventieve opnieuw aanroept, wordt de virtuele machine verplaatst naar een al bijgewerkte knooppunt en vervolgens wordt het weer ingeschakeld, alle configuratieopties en bijbehorende bronnen behouden. Terwijl doet, de tijdelijke schijf verloren en dynamische IP-adressen die zijn gekoppeld aan virtuele netwerkinterface worden bijgewerkt.

Preventieve opnieuw distribueren wordt eenmaal per VM ingeschakeld. Als er een fout opgetreden tijdens het proces, de bewerking is afgebroken, de virtuele machine wordt niet negatief beïnvloed en het is uitgesloten van de herhaling gepland onderhoud. U wordt verbinding gemaakt met in een later tijdstip met een nieuw schema en krijgt een nieuwe mogelijkheid om te plannen en sequentiëren van de gevolgen voor uw virtuele machines.