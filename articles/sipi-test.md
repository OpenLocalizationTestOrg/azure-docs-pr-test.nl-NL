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
# <a name="sipi-test-file"></a><span data-ttu-id="8dc70-103">Sipi testbestand</span><span class="sxs-lookup"><span data-stu-id="8dc70-103">Sipi test file</span></span>

<span data-ttu-id="8dc70-104">Met behulp van deze Quickstart kunt u binnen enkele minuten een toepassing registreren in een B2C-tenant van Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8dc70-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="8dc70-105">Wanneer u klaar bent, wordt uw toepassing geregistreerd voor gebruik in hello Azure B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="8dc70-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8dc70-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8dc70-106">Prerequisites</span></span>

<span data-ttu-id="8dc70-107">toobuild een toepassing waarin zich kunnen registreren en aanmelden consumenten, moet u eerst tooregister Hallo toepassing met een Azure Active Directory B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="8dc70-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="8dc70-108">Haal uw eigen tenant met behulp van Hallo stappen die worden beschreven in [een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8dc70-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="8dc70-109">Toepassingen die zijn gemaakt op basis van hello Azure AD B2C-blade in hello Azure-portal moeten worden beheerd vanaf Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="8dc70-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="8dc70-110">Als u Hallo B2C-toepassingen met PowerShell of een andere portal hebt bewerkt, moet deze worden niet ondersteund en werken niet met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8dc70-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="8dc70-111">Zie de details in Hallo [mislukt apps](#faulted-apps) sectie.</span><span class="sxs-lookup"><span data-stu-id="8dc70-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="8dc70-112">Navigeer tooB2C instellingen</span><span class="sxs-lookup"><span data-stu-id="8dc70-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="8dc70-113">Meld u bij toohello [Azure-portal](https://portal.azure.com/) zoals Hallo globale beheerder van Hallo B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="8dc70-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="8dc70-114">De volgende stappen op basis van het toepassingstype Hallo die u registreert kiezen:</span><span class="sxs-lookup"><span data-stu-id="8dc70-114">Choose next steps based on hello application type you are registering:</span></span>
