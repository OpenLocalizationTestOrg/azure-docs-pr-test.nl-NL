---
title: 'Azure Active Directory B2C: Selfservice voor wachtwoordherstel | Microsoft Docs'
description: Een onderwerp te demonstreren hoe tooset up zelf uw wachtwoord opnieuw instellen voor uw consumenten in Azure Active Directory B2C
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
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="945df-103">Azure Active Directory B2C: Selfservice voor wachtwoordherstel voor uw consumenten instellen</span><span class="sxs-lookup"><span data-stu-id="945df-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="945df-104">Hello selfservice voor wachtwoordherstel functie, uw consumenten (die zich hebben geregistreerd voor lokale accounts) kunnen hun wachtwoorden op hun eigen opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="945df-104">With hello self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="945df-105">Dit vermindert het Hallo werkbelasting van uw medewerkers, met name als uw toepassing heeft miljoenen consumenten regelmatig gebruikt.</span><span class="sxs-lookup"><span data-stu-id="945df-105">This significantly reduces hello burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="945df-106">Op dit moment wordt alleen ondersteund als een methode voor het herstellen met behulp van een geverifieerde e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="945df-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="945df-107">In de toekomst Hallo voegen we aanvullende herstelpunten methoden (geverifieerde telefoonnummer, beveiligingsvragen, enz.) toe.</span><span class="sxs-lookup"><span data-stu-id="945df-107">We will add additional recovery methods (verified phone number, security questions, etc.) in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="945df-108">In dit artikel is van toepassing tooself-service-wachtwoord opnieuw instellen in de context van een beleid voor aanmelden Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="945df-108">This article applies tooself-service password reset used in hello context of a sign-in policy.</span></span> <span data-ttu-id="945df-109">Als u volledig aanpasbare wachtwoord opnieuw instellen van beleidsregels aangeroepen vanuit uw app nodig hebt, raadpleegt u [in dit artikel](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="945df-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="945df-110">Standaard uw directory geen zelf uw wachtwoord opnieuw instellen is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="945df-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="945df-111">Gebruik Hallo volgende stappen tooturn deze op:</span><span class="sxs-lookup"><span data-stu-id="945df-111">Use hello following steps tooturn it on:</span></span>

1. <span data-ttu-id="945df-112">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) zoals Hallo Abonnementsbeheerder.</span><span class="sxs-lookup"><span data-stu-id="945df-112">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) as hello Subscription Administrator.</span></span> <span data-ttu-id="945df-113">Dit is Hallo dezelfde werken of schoolaccount of hetzelfde Microsoft-account dat u toocreate uw directory gebruikt Hallo.</span><span class="sxs-lookup"><span data-stu-id="945df-113">This is hello same work or school account or hello same Microsoft account that you used toocreate your directory.</span></span>
2. <span data-ttu-id="945df-114">Navigeer toohello Active Directory-extensie op Hallo navigatiebalk aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="945df-114">Navigate toohello Active Directory extension on hello navigation bar on hello left side.</span></span>
3. <span data-ttu-id="945df-115">Zoeken naar uw map onder Hallo **Directory** tabblad en klik erop.</span><span class="sxs-lookup"><span data-stu-id="945df-115">Find your directory under hello **Directory** tab and click it.</span></span>
4. <span data-ttu-id="945df-116">Klik op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="945df-116">Click hello **Configure** tab.</span></span>
5. <span data-ttu-id="945df-117">Schuif omlaag toohello **beleid opnieuw instellen van wachtwoorden** sectie en in-/ uitschakelen Hallo **gebruikers die zijn ingeschakeld voor wachtwoordherstel** te optie**Ja**.</span><span class="sxs-lookup"><span data-stu-id="945df-117">Scroll down toohello **User password reset policy** section and toggle hello **Users enabled for password reset** option too**YES**.</span></span> <span data-ttu-id="945df-118">U ziet dat Hallo **alternatief e-mailadres** optie is ingeschakeld; ongewijzigd laten.</span><span class="sxs-lookup"><span data-stu-id="945df-118">Notice that hello **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Self-service voor wachtwoord opnieuw instellen](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="945df-120">Klik op **opslaan** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="945df-120">Click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="945df-121">U bent nu klaar!</span><span class="sxs-lookup"><span data-stu-id="945df-121">You're done!</span></span>

<span data-ttu-id="945df-122">tootest, gebruik Hallo 'Nu uitvoeren' functie op elk beleid aanmelden met lokale accounts als een id-provider.</span><span class="sxs-lookup"><span data-stu-id="945df-122">tootest, use hello "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="945df-123">Op Hallo lokale account aanmelden pagina (waar u een e-mailadres en wachtwoord, of een gebruikersnaam en wachtwoord), klikt u op **geen toegang tot uw account?** tooverify Hallo consumer ervaring.</span><span class="sxs-lookup"><span data-stu-id="945df-123">On hello local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** tooverify hello consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="945df-124">Hallo zelf uw wachtwoord opnieuw instellen van pagina's kunnen worden aangepast met behulp van Hallo [functie huisstijl](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="945df-124">hello self-service password reset pages can be customized by using hello [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

