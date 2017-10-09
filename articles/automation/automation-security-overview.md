---
title: aaaIntro tooauthentication in Azure Automation | Microsoft Docs
description: In dit artikel biedt een overzicht van automatische beveiliging en Hallo verschillende verificatiemethoden die beschikbaar zijn voor Automation-Accounts in Azure Automation.
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
ms.openlocfilehash: 4b4409b5be010c16f7bf00a9a0f617e3617d4663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooauthentication-in-azure-automation"></a>Inleiding tooauthentication in Azure Automation  
Azure Automation kunt u tooautomate taken op basis van bronnen in Azure, on-premises en bij andere cloudproviders zoals Amazon Web Services (AWS).  Om een runbook tooperform de vereiste acties moet hebben machtigingen toosecurely toegang Hallo resources met de minimale rechten Hallo binnen Hallo abonnement vereist.

Dit artikel wordt uitgelegd Hallo verschillende scenario's voor de verificatie wordt ondersteund door Azure Automation en tonen u hoe tooget gestart op basis van Hallo omgeving(en) die u moet toomanage.  

## <a name="automation-account-overview"></a>Overzicht van Automation-account
Wanneer u Azure Automation voor Hallo eerst start, moet u ten minste één Automation-account maken. Automation-accounts kunnen u uw Automation-resources (runbooks, assets, configuraties) uit bronnen die zich bevinden in andere Automation-accounts Hallo tooisolate. U kunt Automation-accounts tooseparate resources gebruiken in afzonderlijke logische omgevingen. U kunt bijvoorbeeld één account maken voor ontwikkeling, één voor productie, en één voor uw on-premises omgeving.  Een Azure Automation-account verschilt van uw Microsoft-account of de accounts die zijn gemaakt in uw Azure-abonnement.

Hallo Automation-resources voor elk Automation-account zijn gekoppeld aan één Azure-regio, maar Automation-accounts kunnen alle Hallo resources in uw abonnement beheren. Hallo belangrijkste reden toocreate Automation-accounts in verschillende regio's zou zijn als u beleid hebt waardoor gegevens en resources toobe geïsoleerde tooa specifieke regio.

> [!NOTE]
> Automation-accounts en Hallo-resources die ze bevatten die zijn gemaakt in hello Azure-portal, niet toegankelijk in de klassieke Azure-portal Hallo. Als u toomanage deze accounts of hun resources met Windows PowerShell wilt, moet u hello Azure Resource Manager-modules.
>

Alle Hallo-taken die u uitvoert op resources met Azure Resource Manager en hello Azure-cmdlets in Azure Automation tooAzure met Azure Active Directory organisatie-id-referentie gebaseerde verificatie moet worden geverifieerd.  Verificatie op basis van certificaten is Hallo oorspronkelijke verificatiemethode Azure Service Management-modus, maar was ingewikkeld toosetup.  Verificatie van tooAzure met Azure AD-gebruiker is geïntroduceerd in 2014 toonot alleen vereenvoudigen Hallo proces tooconfigure een account voor verificatie, maar ook ondersteuning Hallo mogelijkheid toonon interactief tooAzure met één gebruikersaccount die werkten verifiëren met Azure Resource Manager en klassieke resources.   

Op dit moment als u een nieuw automatiseringsaccount in hello Azure-portal maakt, wordt automatisch gemaakt:

* Run As-account dat wordt een nieuwe service-principal gemaakt in Azure Active Directory, een certificaat en wijst Hallo Inzender op rollen gebaseerde toegangsbeheer (RBAC), die wordt gebruikt toomanage Resource Manager-resources met behulp van runbooks.
* Klassieke Run As-account door het uploaden van een beheercertificaat dat zal worden gebruikt toomanage Azure Service Management of klassieke resources met behulp van runbooks.  

Toegangsbeheer op basis van rollen is beschikbaar met Azure Resource Manager toogrant toegestane acties tooan Azure AD-gebruikersaccount en Run As-account en verifiëren van deze service-principal.  Lees [toegangsbeheer op basis van rollen in Azure Automation-artikel](automation-role-based-access-control.md) voor verdere informatie toohelp ontwikkelen van een model voor het beheren van machtigingen in Automation.  

Runbooks die worden uitgevoerd op een hybride Runbook Worker in uw datacenter of op basis van computingservices in AWS kan geen gebruik Hallo dezelfde methode die wordt doorgaans gebruikt voor runbooks tooAzure bronnen te verifiëren.  Dit is omdat deze resources buiten Azure worden uitgevoerd en daarom moet u hun eigen beveiligingsreferenties gedefinieerd in Automation tooauthenticate tooresources die ze lokaal toegang hebben.  

## <a name="authentication-methods"></a>Verificatiemethoden
Hallo volgende tabel ziet u Hallo verschillende verificatiemethoden voor elke omgeving wordt ondersteund door Azure Automation en Hallo artikel beschrijven hoe toosetup verificatie voor uw runbooks.

| Methode | Omgeving | Artikel |
| --- | --- | --- |
| Azure AD-gebruikersaccount |Azure Resource Manager en Azure-servicebeheer |[Runbooks verifiëren met een Azure AD-gebruikersaccount](automation-create-aduser-account.md) |
| Azure Uitvoeren als-account |Azure Resource Manager |[Runbooks verifiëren met een Azure Uitvoeren als-account](automation-sec-configure-azure-runas-account.md) |
| Klassieke Azure Uitvoeren als-account |Azure Service Management |[Runbooks verifiëren met een Azure Uitvoeren als-account](automation-sec-configure-azure-runas-account.md) |
| Windows-verificatie |On-premises datacenter |[Runbooks verifiëren voor Hybrid Runbook Workers](automation-hybrid-runbook-worker.md) |
| AWS-referenties |Amazon Web Services |[Runbooks verifiëren met Amazon Web Services (AWS)](automation-config-aws-account.md) |
