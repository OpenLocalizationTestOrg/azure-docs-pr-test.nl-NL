---
title: Sipi testbestand | Microsoft Docs
description: Testbestand naar ReadyForTest afhankelijkheden controleren
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a>Sipi testbestand

Met behulp van deze Quickstart kunt u binnen enkele minuten een toepassing registreren in een B2C-tenant van Microsoft Azure Active Directory (Azure AD). Wanneer u klaar bent, is de toepassing geregistreerd voor gebruik in de Azure B2C-tenant.

## <a name="prerequisites"></a>Vereisten

Als u een toepassing wilt maken waarin consumenten zich kunnen registreren en aanmelden, moet u de toepassing eerst registreren bij een Azure Active Directory B2C-tenant. Haal uw eigen tenant op aan de hand van de stappen in [Een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md).

Toepassingen die zijn gemaakt vanaf de blade Azure AD B2C in Azure Portal, moeten vanaf dezelfde locatie worden beheerd. Als u de B2C-toepassingen bewerkt met PowerShell of een andere portal, worden de toepassingen niet meer ondersteund en werken ze niet met Azure AD B2C. Zie voor meer informatie de sectie [Mislukte toepassingen](#faulted-apps). 

## <a name="navigate-to-b2c-settings"></a>Navigeren naar de B2C-instellingen

Meld u als globale beheerder van de B2C-tenant aan bij [Azure Portal](https://portal.azure.com/). 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

Kies de volgende stappen op basis van het toepassingstype dat u wilt registreren:
