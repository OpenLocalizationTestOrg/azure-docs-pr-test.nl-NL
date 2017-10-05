---
title: Er zijn geen abonnementen gevonden fout wanneer probeert aan te melden bij Azure portal of Azure-accountcentrum | Microsoft Docs
description: De oplossing biedt voor een probleem waarbij geen abonnementen gevonden fout treedt op wanneer zich bij Azure portal of Azure-accountcentrum.
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
ms.openlocfilehash: a4ce9b219c05f8469379c2aac5241fcfffd16033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="ec8dd-103">Er zijn geen abonnementen heeft een fout gevonden in Azure portal of Azure-accountcentrum</span><span class="sxs-lookup"><span data-stu-id="ec8dd-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="ec8dd-104">U ontvangt mogelijk een foutbericht van de 'Geen abonnementen gevonden' wanneer u probeert aan te melden bij de [Azure-portal](https://portal.azure.com/) of de [Azure-accountcentrum](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="ec8dd-104">You might receive a "No subscriptions found" error message when you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="ec8dd-105">In dit artikel biedt een oplossing voor dit probleem.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="ec8dd-106">Symptoom</span><span class="sxs-lookup"><span data-stu-id="ec8dd-106">Symptom</span></span>

<span data-ttu-id="ec8dd-107">Wanneer u probeert aan te melden bij de [Azure-portal](https://portal.azure.com/) of de [Azure-accountcentrum](https://account.windowsazure.com/Subscriptions), verschijnt het volgende foutbericht weergegeven: 'Geen abonnementen gevonden'.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-107">When you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions), you receive the following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="ec8dd-108">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="ec8dd-108">Cause</span></span>

<span data-ttu-id="ec8dd-109">Dit probleem treedt op als uw account niet voldoende machtigingen hebben.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="ec8dd-110">Oplossing</span><span class="sxs-lookup"><span data-stu-id="ec8dd-110">Solution</span></span>

<span data-ttu-id="ec8dd-111">Zorg ervoor dat u zich als beheerder van de juiste aanmelden.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-111">Make sure that you log in as the correct administrator.</span></span> <span data-ttu-id="ec8dd-112">Een beheerder Account toegang tot alleen de Center-Account.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-112">An Account Administrator can access only the Account Center.</span></span> <span data-ttu-id="ec8dd-113">Service-beheerders (SA) en Medebeheerders (CA) hebben toegang tot de Azure portal of de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only to the Azure portal or the Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a><span data-ttu-id="ec8dd-114">Scenario 1: Foutbericht ontvangen in de [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ec8dd-114">Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="ec8dd-115">Dit probleem oplossen:</span><span class="sxs-lookup"><span data-stu-id="ec8dd-115">To fix this issue:</span></span>

* <span data-ttu-id="ec8dd-116">Zorg ervoor dat de juiste Azure-map is geselecteerd door te klikken op uw account in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-116">Make sure that the correct Azure directory is selected by clicking your account at the top right.</span></span>

  ![Selecteer de map boven rechts van de Azure-portal](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="ec8dd-118">Als de juiste Azure-map is geselecteerd, maar u nog steeds het foutbericht ontvangen [uw account wordt toegevoegd als een eigenaar](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="ec8dd-118">If the right Azure directory is selected but you still receive the error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="ec8dd-119">Scenario 2: Foutbericht ontvangen in de [Azure account center](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="ec8dd-119">Scenario 2: Error message is received in the [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="ec8dd-120">Controleer of het account dat u gebruikt de accountbeheerder.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-120">Check whether the account that you used is the Account Administrator.</span></span> <span data-ttu-id="ec8dd-121">Om te controleren wie de accountbeheerder is, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ec8dd-121">To verify who the Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="ec8dd-122">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ec8dd-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ec8dd-123">Selecteer in het menu Hub **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-123">On the Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="ec8dd-124">Selecteer het abonnement dat u wilt controleren, en selecteer vervolgens **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-124">Select the subscription that you want to check, and then select **Settings**.</span></span>
4. <span data-ttu-id="ec8dd-125">Selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-125">Select **Properties**.</span></span> <span data-ttu-id="ec8dd-126">De accountbeheerder van het abonnement wordt weergegeven in de **accountbeheerder** vak.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-126">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="ec8dd-127">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="ec8dd-127">Need help?</span></span> <span data-ttu-id="ec8dd-128">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-128">Contact support.</span></span>
<span data-ttu-id="ec8dd-129">Als u nog hulp nodig hebt, [contact op met ondersteuning](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) ophalen van uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="ec8dd-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span></span> 
