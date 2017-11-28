---
title: 'Azure Active Directory B2C: Selfservice voor wachtwoordherstel | Microsoft Docs'
description: Een onderwerp aan te tonen het instellen van de selfservice voor wachtwoordherstel voor uw consumenten in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 0508868e3b00c5771cc26038a3dd71fde6625a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="bc8ad-103">Azure Active Directory B2C: Selfservice voor wachtwoordherstel voor uw consumenten instellen</span><span class="sxs-lookup"><span data-stu-id="bc8ad-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="bc8ad-104">Uw consumenten (die zich hebben geregistreerd voor lokale accounts) kunnen hun wachtwoorden op hun eigen opnieuw instellen met de functie zelf uw wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="bc8ad-105">Dit vermindert de werkbelasting van uw medewerkers, met name als uw toepassing heeft miljoenen consumenten regelmatig gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="bc8ad-106">Op dit moment wordt alleen ondersteund als een methode voor het herstellen met behulp van een geverifieerde e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="bc8ad-107">Er wordt aanvullende herstelpunten methoden (geverifieerde telefoonnummer, beveiligingsvragen, enz.) in de toekomst toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="bc8ad-108">In dit artikel is van toepassing op zelf uw wachtwoord opnieuw instellen die worden gebruikt in de context van een beleid voor aanmelden.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="bc8ad-109">Als u volledig aanpasbare wachtwoord opnieuw instellen van beleidsregels aangeroepen vanuit uw app nodig hebt, raadpleegt u [in dit artikel](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="bc8ad-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="bc8ad-110">Standaard uw directory geen zelf uw wachtwoord opnieuw instellen is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="bc8ad-111">Gebruik de volgende stappen uit te schakelen:</span><span class="sxs-lookup"><span data-stu-id="bc8ad-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="bc8ad-112">Meld u aan bij de [klassieke Azure-portal](https://manage.windowsazure.com/) als abonnementsbeheerder.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="bc8ad-113">Dit is hetzelfde werk- of schoolaccount of hetzelfde Microsoft-account dat u gebruikt voor het maken van uw directory.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="bc8ad-114">Navigeer naar de Active Directory-extensie in de navigatiebalk aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="bc8ad-115">Zoeken naar uw map onder de **Directory** tabblad en klik erop.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="bc8ad-116">Klik op het tabblad **Configureren**.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="bc8ad-117">Schuif omlaag naar de **beleid opnieuw instellen van wachtwoorden** sectie en in-/ uitschakelen de **gebruikers die zijn ingeschakeld voor wachtwoordherstel** optie naar **Ja**.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="bc8ad-118">U ziet dat de **alternatief e-mailadres** optie is ingeschakeld; ongewijzigd laten.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Self-service voor wachtwoord opnieuw instellen](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="bc8ad-120">Klik op **Opslaan** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="bc8ad-121">U bent nu klaar!</span><span class="sxs-lookup"><span data-stu-id="bc8ad-121">You're done!</span></span>

<span data-ttu-id="bc8ad-122">Als u wilt testen, gebruikt u de functie 'Nu uitvoeren' op elk beleid aanmelden met lokale accounts als een id-provider.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="bc8ad-123">Op de lokale account aanmelden pagina (waar u een e-mailadres en wachtwoord, of een gebruikersnaam en wachtwoord), klikt u op **geen toegang tot uw account?** om te controleren of de consumer-ervaring.</span><span class="sxs-lookup"><span data-stu-id="bc8ad-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="bc8ad-124">De zelf uw wachtwoord opnieuw instellen van pagina's kunnen worden aangepast via de [functie huisstijl](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="bc8ad-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

