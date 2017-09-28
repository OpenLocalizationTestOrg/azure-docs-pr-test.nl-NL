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
# <a name="sipi-test-file"></a><span data-ttu-id="d08c5-103">Sipi testbestand</span><span class="sxs-lookup"><span data-stu-id="d08c5-103">Sipi test file</span></span>

<span data-ttu-id="d08c5-104">Met behulp van deze Quickstart kunt u binnen enkele minuten een toepassing registreren in een B2C-tenant van Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d08c5-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="d08c5-105">Wanneer u klaar bent, is de toepassing geregistreerd voor gebruik in de Azure B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="d08c5-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d08c5-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d08c5-106">Prerequisites</span></span>

<span data-ttu-id="d08c5-107">Als u een toepassing wilt maken waarin consumenten zich kunnen registreren en aanmelden, moet u de toepassing eerst registreren bij een Azure Active Directory B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="d08c5-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="d08c5-108">Haal uw eigen tenant op aan de hand van de stappen in [Een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d08c5-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="d08c5-109">Toepassingen die zijn gemaakt vanaf de blade Azure AD B2C in Azure Portal, moeten vanaf dezelfde locatie worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="d08c5-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="d08c5-110">Als u de B2C-toepassingen bewerkt met PowerShell of een andere portal, worden de toepassingen niet meer ondersteund en werken ze niet met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d08c5-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="d08c5-111">Zie voor meer informatie de sectie [Mislukte toepassingen](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="d08c5-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="d08c5-112">Navigeren naar de B2C-instellingen</span><span class="sxs-lookup"><span data-stu-id="d08c5-112">Navigate to B2C settings</span></span>

<span data-ttu-id="d08c5-113">Meld u als globale beheerder van de B2C-tenant aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d08c5-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="d08c5-114">Kies de volgende stappen op basis van het toepassingstype dat u wilt registreren:</span><span class="sxs-lookup"><span data-stu-id="d08c5-114">Choose next steps based on the application type you are registering:</span></span>
