---
title: Extensies app - Azure AD B2C | Microsoft Docs
description: Hallo b2c-uitbreidingen-app herstellen
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Azure AD B2C: Extensies app

Als een Azure AD B2C-directory is gemaakt, wordt aangeroepen door een app `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` automatisch wordt gemaakt in de nieuwe map Hallo. Deze app op, waarnaar wordt verwezen tooas hello **b2c-uitbreidingen-app**, zichtbaar is in *App registraties*. Deze wordt gebruikt door hello Azure AD B2C-service toostore informatie over gebruikers en aangepaste kenmerken. Hallo-app wordt verwijderd, Azure AD B2C niet naar behoren als uw productieomgeving worden beïnvloed.

> [!IMPORTANT]
> Verwijder Hallo b2c-uitbreidingen-app niet tenzij u van plan bent tooimmediately verwijderen uw tenant. Als het Hallo-app blijft gedurende meer dan 30 dagen verwijderd, worden gebruikersgegevens permanent verloren.

## <a name="verifying-that-hello-extensions-app-is-present"></a>Controleren die Hallo extensies app aanwezig is

tooverify die Hallo b2c-uitbreidingen-app is aanwezig:

1. Binnen uw Azure AD B2C-tenant, klikt u op **meer services** in Hallo links navigatiemenu.
1. Zoeken en openen **App registraties**.
1. Een app die met begint zoeken **b2c-uitbreidingen-app**

## <a name="recover-hello-extensions-app"></a>Hallo-extensies app herstellen

Als u per ongeluk Hallo b2c-uitbreidingen-app hebt verwijderd, hebt u 30 dagen toorecover deze. Hallo-app met behulp van Hallo Graph API kunt u herstellen:

1. Te bladeren[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).
1. Toohello site aanmelden als globale beheerder voor hello Azure AD B2C-directory die u wilt dat toorestore Hallo verwijderd-app voor.
1. Uitgeven van een HTTP GET tegen Hallo URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` = met api-versie 1.6. Zorg ervoor dat tooreplace `{tenantName}` met de tenantnaam van uw. Deze bewerking wordt een lijst alle Hallo-toepassingen die zijn verwijderd binnen Hallo afgelopen 30 dagen.
1. Hallo toepassing zoeken in Hallo lijst waarbij Hallo naam met 'b2c-extensie-app' en kopieer begint de `objectid` eigenschapswaarde.
1. Uitgeven van een HTTP POST tegen Hallo URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`. Vervang Hallo `{OBJECTID}` deel van de URL Hallo Hello `objectid` uit de vorige stap Hallo. 

U moet nu mogelijk te[Zie Hallo hersteld app](#verifying-that-the-extensions-app-is-present) in hello Azure-portal.

> [!NOTE]
> Een toepassing kan alleen worden hersteld als deze is verwijderd binnen Hallo afgelopen 30 dagen. Als het meer dan 30 dagen is, worden gegevens permanent verloren. Het bestand een ondersteuningsticket voor verdere ondersteuning.
