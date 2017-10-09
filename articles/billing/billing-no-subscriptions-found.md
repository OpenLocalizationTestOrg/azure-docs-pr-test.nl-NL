---
title: aaaNo abonnementen gevonden fout wanneer probeert toosign in tooAzure portal of Azure-accountcentrum | Microsoft Docs
description: Hallo-oplossing biedt voor een probleem waarbij geen abonnementen gevonden fout treedt op wanneer zich tooAzure portal of Azure-accountcentrum.
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="77000-103">Er zijn geen abonnementen heeft een fout gevonden in Azure portal of Azure-accountcentrum</span><span class="sxs-lookup"><span data-stu-id="77000-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="77000-104">U ontvangt mogelijk een foutbericht van de 'Geen abonnementen gevonden' wanneer u toosign in toohello probeert [Azure-portal](https://portal.azure.com/) of Hallo [Azure-accountcentrum](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="77000-104">You might receive a "No subscriptions found" error message when you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="77000-105">In dit artikel biedt een oplossing voor dit probleem.</span><span class="sxs-lookup"><span data-stu-id="77000-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="77000-106">Symptoom</span><span class="sxs-lookup"><span data-stu-id="77000-106">Symptom</span></span>

<span data-ttu-id="77000-107">Wanneer u probeert toosign in toohello [Azure-portal](https://portal.azure.com/) of Hallo [Azure-accountcentrum](https://account.windowsazure.com/Subscriptions), ontvangen van Hallo volgende foutbericht weergegeven: 'Geen abonnementen gevonden'.</span><span class="sxs-lookup"><span data-stu-id="77000-107">When you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions), you receive hello following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="77000-108">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="77000-108">Cause</span></span>

<span data-ttu-id="77000-109">Dit probleem treedt op als uw account niet voldoende machtigingen hebben.</span><span class="sxs-lookup"><span data-stu-id="77000-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="77000-110">Oplossing</span><span class="sxs-lookup"><span data-stu-id="77000-110">Solution</span></span>

<span data-ttu-id="77000-111">Zorg ervoor dat u zich als de juiste administrator Hallo aanmelden.</span><span class="sxs-lookup"><span data-stu-id="77000-111">Make sure that you log in as hello correct administrator.</span></span> <span data-ttu-id="77000-112">Een beheerder Account toegang tot alleen Hallo-Accountcentrum.</span><span class="sxs-lookup"><span data-stu-id="77000-112">An Account Administrator can access only hello Account Center.</span></span> <span data-ttu-id="77000-113">Service-beheerders (SA) en Medebeheerders (CA) hebben alleen toohello over machtigingen voor toegang tot Azure-portal of Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="77000-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only toohello Azure portal or hello Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a><span data-ttu-id="77000-114">Scenario 1: Foutbericht wordt ontvangen op Hallo [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="77000-114">Scenario 1: Error message is received in hello [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="77000-115">toofix dit probleem:</span><span class="sxs-lookup"><span data-stu-id="77000-115">toofix this issue:</span></span>

* <span data-ttu-id="77000-116">Zorg ervoor dat Hallo juiste Azure-map is geselecteerd door te klikken op uw account Hallo rechts bovenaan.</span><span class="sxs-lookup"><span data-stu-id="77000-116">Make sure that hello correct Azure directory is selected by clicking your account at hello top right.</span></span>

  ![Selecteer Hallo directory op Hallo top rechts van hello Azure-portal](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="77000-118">Als hello rechts Azure-map is geselecteerd, maar nog steeds hello foutbericht, [uw account wordt toegevoegd als een eigenaar](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="77000-118">If hello right Azure directory is selected but you still receive hello error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="77000-119">Scenario 2: Foutbericht wordt ontvangen op Hallo [Azure account center](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="77000-119">Scenario 2: Error message is received in hello [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="77000-120">Controleer of Hallo-account waarmee u Hallo accountbeheerder.</span><span class="sxs-lookup"><span data-stu-id="77000-120">Check whether hello account that you used is hello Account Administrator.</span></span> <span data-ttu-id="77000-121">tooverify wie de accountbeheerder Hallo is, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="77000-121">tooverify who hello Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="77000-122">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="77000-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="77000-123">Selecteer op de Hub-menu Hallo **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="77000-123">On hello Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="77000-124">Selecteer Hallo-abonnement dat u toocheck wilt en selecteer vervolgens **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="77000-124">Select hello subscription that you want toocheck, and then select **Settings**.</span></span>
4. <span data-ttu-id="77000-125">Selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="77000-125">Select **Properties**.</span></span> <span data-ttu-id="77000-126">de accountbeheerder Hallo van Hallo abonnement wordt weergegeven in Hallo **accountbeheerder** vak.</span><span class="sxs-lookup"><span data-stu-id="77000-126">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="77000-127">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="77000-127">Need help?</span></span> <span data-ttu-id="77000-128">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="77000-128">Contact support.</span></span>
<span data-ttu-id="77000-129">Als u nog hulp nodig hebt, [contact op met ondersteuning](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="77000-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget your issue resolved quickly.</span></span> 
