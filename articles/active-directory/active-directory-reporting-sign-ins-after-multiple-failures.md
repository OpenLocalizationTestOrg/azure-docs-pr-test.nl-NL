---
title: Aanmeldingen na meerdere mislukte pogingen
description: Een rapport dat gebruikers die zich heeft aangemeld na meerdere opeenvolgende aanmelding bij pogingen mislukte aangeeft.
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: e55e0145adbdb1f41a8b8753d5555f20e96bf161
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="16f82-103">Aanmeldingen na meerdere mislukte pogingen</span><span class="sxs-lookup"><span data-stu-id="16f82-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="16f82-104">Dit rapport geeft aan dat gebruikers die zich heeft aangemeld na meerdere opeenvolgende aanmelding bij pogingen mislukte.</span><span class="sxs-lookup"><span data-stu-id="16f82-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="16f82-105">Mogelijke oorzaken zijn:</span><span class="sxs-lookup"><span data-stu-id="16f82-105">Possible causes include:</span></span>

* <span data-ttu-id="16f82-106">Gebruiker heeft hun wachtwoord vergeten</span><span class="sxs-lookup"><span data-stu-id="16f82-106">User had forgotten their password</span></span></li><li><span data-ttu-id="16f82-107">Gebruiker is het slachtoffer van een geslaagde wachtwoord raden brute force-aanvallen</span><span class="sxs-lookup"><span data-stu-id="16f82-107">User is the victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="16f82-108">Resultaten van deze lijst ziet u het aantal opeenvolgende mislukte aanmeldpogingen gemaakt voordat de geslaagde aanmelden en een tijdstempel die is gekoppeld aan de eerste geslaagde aanmelden.</span><span class="sxs-lookup"><span data-stu-id="16f82-108">Results from this report will show you the number of consecutive failed sign-in attempts made prior to the successful sign-in and a timestamp associated with the first successful sign-in.</span></span>

<span data-ttu-id="16f82-109">**Instellingen rapporteren**: U kunt het minimum aantal opeenvolgende mislukte aanmelding configureren in pogingen dat optreden moeten voordat deze kan worden weergegeven in het rapport.</span><span class="sxs-lookup"><span data-stu-id="16f82-109">**Report Settings**: You can configure the minimum number of consecutive failed sign in attempts that must occur before it can be displayed in the report.</span></span> <span data-ttu-id="16f82-110">Wanneer u wijzigingen in deze instelling aanbrengt is het belangrijk te weten dat deze wijzigingen niet worden toegepast op alle bestaande mislukte aanmelding modules die momenteel weergegeven in het bestaande rapport.</span><span class="sxs-lookup"><span data-stu-id="16f82-110">When you make changes to this setting it is important to note that these changes will not be applied to any existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="16f82-111">Ze zullen echter worden toegepast op alle toekomstige aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="16f82-111">However, they will be applied to all future sign-ins.</span></span> <span data-ttu-id="16f82-112">Wijzigingen in dit rapport kunnen alleen worden gemaakt door de gelicentieerde beheerders.</span><span class="sxs-lookup"><span data-stu-id="16f82-112">Changes to this report can only be made by licensed admins.</span></span>

![Aanmeldingen na meerdere mislukte pogingen](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

