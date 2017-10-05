---
title: Inleiding tot verificatie in Azure Automation | Microsoft Docs
description: Dit artikel geeft een overzicht van Automation-beveiliging en de diverse verificatiemethoden die beschikbaar zijn voor Automation-accounts in Azure Automation.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: automation-beveiliging, veilige automation; automation-verificatie
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 91c98f8dda6f24c2db2730a5e0df5ea43e151c61
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-authentication-in-azure-automation"></a>Inleiding tot verificatie in Azure Automation  
Met Azure Automation kunt u taken automatiseren voor bronnen in Azure, on-premises en bij andere cloudproviders zoals Amazon Web Services (AWS).  Om een runbook in staat te stellen de vereiste acties uit te voeren, moet het machtigingen hebben om veilig toegang te krijgen tot de resources met de minimale rechten die vereist zijn binnen het abonnement.

In dit artikel worden de verschillende verificatiescenario's beschreven die door Azure Automation worden ondersteund, en wordt uitgelegd hoe u aan de slag kunt gaan afhankelijk van de omgeving(en) die u wilt beheren.  

## <a name="automation-account-overview"></a>Overzicht van Automation-account
Wanneer u Azure Automation voor het eerst start, moet u ten minste één Automation-account maken. Met Automation-accounts kunt u uw Automation-resources (runbooks, assets, configuraties) isoleren van de resources in andere Automation-accounts. U kunt Automation-accounts gebruiken om resources onder te verdelen in afzonderlijke logische omgevingen. U kunt bijvoorbeeld één account maken voor ontwikkeling, één voor productie, en één voor uw on-premises omgeving.  Een Azure Automation-account verschilt van uw Microsoft-account of de accounts die zijn gemaakt in uw Azure-abonnement.

De Automation-resources voor elk Automation-account zijn gekoppeld aan één Azure-regio, maar Automation-accounts kunnen alle resources in uw abonnement beheren. De voornaamste reden om Automation-accounts in verschillende regio's te maken zou zijn als u beleid hebt waardoor gegevens en resources moeten worden geïsoleerd in een specifieke regio.

> [!NOTE]
> Automation-accounts, en de resources die deze bevatten die in de Azure-portal worden gemaakt, zijn niet toegankelijk via de klassieke Azure-portal. Als u deze accounts of de bijbehorende resources wilt beheren met Windows PowerShell, moet u gebruikmaken van de Azure Resource Manager-modules.
>

Alle taken die u uitvoert op resources met behulp van Azure Resource Manager en de Azure-cmdlets in Azure Automation moeten worden geverifieerd bij Azure met behulp van verificatie op basis van organisatie-identiteitreferenties van Azure Active Directory.  De oorspronkelijke verificatiemethode voor de Azure Service Management-modus was gebaseerd op certificaten, maar het instellen hiervan was ingewikkeld.  Verificatie bij Azure met Azure AD-gebruiker is in 2014 geïntroduceerd, niet alleen met het doel om het proces waarmee een verificatieaccount kon worden geconfigureerd te vereenvoudigen, maar ook om de mogelijkheid te ondersteunen om op een niet-interactieve wijze bij Azure te verifiëren met één gebruikersaccount dat zowel in Azure Resource Manager als in de klassieke resources werkte.   

Wanneer u op dit moment in de Azure-portal een nieuw Automation-account maakt, wordt automatisch het volgende gemaakt:

* Uitvoeren als-account; hiermee wordt een nieuwe service-principal in Azure Active Directory gemaakt, een certificaat, en wordt het RBAC (op rollen gebaseerd toegangsbeheer) toegewezen, dat wordt gebruikt om Resource Manager-resources te beheren met runbooks.
* Klassiek uitvoeren als-account; door een beheercertificaat te uploaden, dat wordt gebruikt om Azure-servicebeheer of klassieke resources te beheren met runbooks.  

Op rollen gebaseerd toegangsbeheer is beschikbaar in Azure Resource Manager voor het toekennen van toegestane acties aan een Azure AD-gebruikersaccount en Uitvoeren als-account, en om die service-principal te verifiëren.  Lees het artikel [Op rollen gebaseerd toegangsbeheer in Azure Automation](automation-role-based-access-control.md) voor meer informatie die u helpt bij het ontwikkelen van een model voor het beheren van machtigingen in Automation.  

Runbooks die op een hybride Runbook Worker in uw datacenter of op basis van computingservices in AWS worden uitgevoerd, kunnen niet dezelfde methode gebruiken die doorgaans wordt gebruikt voor runbooks die worden geverifieerd voor Azure-resources.  Dit is omdat deze resources buiten Azure worden uitgevoerd en er daarom voor deze resources eigen beveiligingsreferenties moeten worden gedefinieerd in Automation, zodat ze kunnen worden geverifieerd voor resources waartoe ze lokaal toegang hebben.  

## <a name="authentication-methods"></a>Verificatiemethoden
De volgende tabel bevat een overzicht van de verschillende verificatiemethoden voor elke omgeving die wordt ondersteund door Azure Automation, evenals het artikel waarin wordt beschreven hoe u verificatie voor uw runbooks moet instellen.

| Methode | Omgeving | Artikel |
| --- | --- | --- |
| Azure AD-gebruikersaccount |Azure Resource Manager en Azure-servicebeheer |[Runbooks verifiëren met een Azure AD-gebruikersaccount](automation-create-aduser-account.md) |
| Azure Uitvoeren als-account |Azure Resource Manager |[Runbooks verifiëren met een Azure Uitvoeren als-account](automation-sec-configure-azure-runas-account.md) |
| Klassieke Azure Uitvoeren als-account |Azure Service Management |[Runbooks verifiëren met een Azure Uitvoeren als-account](automation-sec-configure-azure-runas-account.md) |
| Windows-verificatie |On-premises datacenter |[Runbooks verifiëren voor Hybrid Runbook Workers](automation-hybrid-runbook-worker.md) |
| AWS-referenties |Amazon Web Services |[Runbooks verifiëren met Amazon Web Services (AWS)](automation-config-aws-account.md) |
