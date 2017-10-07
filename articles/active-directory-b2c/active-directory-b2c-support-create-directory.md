---
title: 'Azure Active Directory B2C: Oplossen maken tenants | Microsoft Docs'
description: Problemen en oplossingen voor het maken van een Azure Active Directory of Azure Active Directory B2C-tenant.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a>Problemen met een Azure Active Directory of Azure Active Directory B2C-tenant maken 

## <a name="create-an-azure-ad-tenant"></a>Een Azure AD-tenant maken
Als u een tenant van Azure Active Directory (Azure AD) op de eerste poging hello maken kunt, probeer het opnieuw. Neem contact op met ondersteuning van Azure als Hallo probleem aanhoudt.

## <a name="create-an-azure-ad-b2c-tenant"></a>Een Azure AD B2C-tenant maken
Als u problemen ondervindt wanneer u [maken van een Azure Active Directory B2C-tenant (Azure AD B2C)](active-directory-b2c-get-started.md), probeer Hallo volgende opties:

* Als hello Azure AD B2C-tenant niet in de lijst met tenants weergegeven, opnieuw proberen toocreate hello tenant.
* Als hello Azure AD B2C-tenant wordt weergegeven in de lijst met tenants en u ziet Hallo volgende foutbericht wordt weergegeven, Hallo tenant verwijderen en opnieuw maken:

    "Kan maken van Hallo B2C-tenant 'contosob2c' hello niet voltooien. Ga naar dit [koppeling](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) voor meer informatie. "
* Er zijn bekende problemen bij het verwijderen van een bestaande Azure AD B2C-tenant en opnieuw maken met behulp van Hallo dezelfde domeinnaam. Wanneer u een nieuwe Azure AD B2C-tenant maakt, moet u een andere domeinnaam.
* Als deze oplossingen niet werken, moet u contact op met ondersteuning van Azure. Zie voor meer informatie [bestand ondersteuningsaanvragen voor Azure AD B2C](active-directory-b2c-support.md).

