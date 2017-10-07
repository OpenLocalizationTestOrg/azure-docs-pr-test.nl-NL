---
title: Sipi testbestand | Microsoft Docs
description: Afhankelijkheden van toocheck ReadyForTest testen
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
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a>Sipi testbestand

Met behulp van deze Quickstart kunt u binnen enkele minuten een toepassing registreren in een B2C-tenant van Microsoft Azure Active Directory (Azure AD). Wanneer u klaar bent, wordt uw toepassing geregistreerd voor gebruik in hello Azure B2C-tenant.

## <a name="prerequisites"></a>Vereisten

toobuild een toepassing waarin zich kunnen registreren en aanmelden consumenten, moet u eerst tooregister Hallo toepassing met een Azure Active Directory B2C-tenant. Haal uw eigen tenant met behulp van Hallo stappen die worden beschreven in [een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md).

Toepassingen die zijn gemaakt op basis van hello Azure AD B2C-blade in hello Azure-portal moeten worden beheerd vanaf Hallo dezelfde locatie. Als u Hallo B2C-toepassingen met PowerShell of een andere portal hebt bewerkt, moet deze worden niet ondersteund en werken niet met Azure AD B2C. Zie de details in Hallo [mislukt apps](#faulted-apps) sectie. 

## <a name="navigate-toob2c-settings"></a>Navigeer tooB2C instellingen

Meld u bij toohello [Azure-portal](https://portal.azure.com/) zoals Hallo globale beheerder van Hallo B2C-tenant. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

De volgende stappen op basis van het toepassingstype Hallo die u registreert kiezen:
