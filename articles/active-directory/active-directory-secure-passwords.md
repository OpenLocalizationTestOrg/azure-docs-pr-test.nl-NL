---
title: aaaAzure AD gelaagde wachtwoordbeveiliging | Microsoft Docs
description: Legt uit hoe u Azure AD worden afgedwongen sterke wachtwoorden en wachtwoorden van gebruikers beschermt tegen cyberbeveiliging criminelen,
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="be54f-103">Een benadering meerdere lagen tooAzure AD wachtwoordbeveiliging</span><span class="sxs-lookup"><span data-stu-id="be54f-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="be54f-104">Dit artikel worden enkele aanbevolen procedures die u kunt uw Azure Active Directory (Azure AD) of de Microsoft-Account als een gebruiker of als een beheerder tooprotect volgen.</span><span class="sxs-lookup"><span data-stu-id="be54f-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="be54f-105">Azure AD-beheerders kunnen gebruikerswachtwoorden Hallo richtlijnen in Hallo artikel met [Hallo-wachtwoord opnieuw instellen voor een gebruiker in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be54f-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="be54f-106">Gebruikers kunnen wachtwoord opnieuw instellen hun eigen met Hallo richtlijnen in Hallo artikel [Help ik mijn Azure AD-wachtwoord vergeten](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="be54f-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="be54f-107">Vereisten voor wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="be54f-107">Password requirements</span></span>

<span data-ttu-id="be54f-108">Azure AD omvat Hallo algemene benaderingen toosecuring wachtwoorden te volgen:</span><span class="sxs-lookup"><span data-stu-id="be54f-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="be54f-109">Vereisten voor de lengte van het wachtwoord</span><span class="sxs-lookup"><span data-stu-id="be54f-109">Password length requirements</span></span>
* <span data-ttu-id="be54f-110">Vereisten voor wachtwoordcomplexiteit</span><span class="sxs-lookup"><span data-stu-id="be54f-110">Password complexity requirements</span></span>
* <span data-ttu-id="be54f-111">Gepland en automatisch verlopen van wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="be54f-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="be54f-112">Zie voor informatie over het wachtwoord opnieuw instellen in Azure Active Directory, Hallo onderwerp [Azure AD selfservice voor wachtwoordherstel voor IT-professionals Hallo](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="be54f-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="be54f-113">Bescherming van Azure AD-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="be54f-113">Azure AD password protections</span></span>

<span data-ttu-id="be54f-114">Azure AD en Microsoft-Accountsysteem gebruiken bedrijfstak bewezen Hallo nadert tooensure beveiliging van gebruikers- en wachtwoorden, waaronder:</span><span class="sxs-lookup"><span data-stu-id="be54f-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="be54f-115">Dynamisch uitsluiten van wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="be54f-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="be54f-116">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="be54f-116">Smart Password Lockout</span></span>

<span data-ttu-id="be54f-117">Zie voor informatie over wachtwoordbeheer op basis van huidige research Hallo technisch document [wachtwoord richtlijnen](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="be54f-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="be54f-118">Dynamisch uitsluiten van wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="be54f-118">Dynamically banned passwords</span></span>

<span data-ttu-id="be54f-119">Azure AD en Microsoft-Accounts wachtwoordbeveiliging veiligstellen door dynamisch verboden veelgebruikte wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="be54f-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="be54f-120">Hello Azure ID Identity Protection-team analyseert regelmatig verboden wachtwoordenlijsten, voorkomen dat gebruikers wachtwoorden veelgebruikte kiezen.</span><span class="sxs-lookup"><span data-stu-id="be54f-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="be54f-121">Deze service is beschikbaar tooAzure AD en klanten van Hallo-Service van Microsoft-Account.</span><span class="sxs-lookup"><span data-stu-id="be54f-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="be54f-122">Bij het maken van wachtwoorden, is het belangrijk voor beheerders tooencourage gebruikers toochoose wachtwoord zinnen met een unieke combinatie van letters, cijfers, tekens of woorden.</span><span class="sxs-lookup"><span data-stu-id="be54f-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="be54f-123">Deze aanpak kunt toomake gebruikerswachtwoorden nagenoeg onmogelijk toobe maar gemakkelijker voor gebruikers tooremember aangetast.</span><span class="sxs-lookup"><span data-stu-id="be54f-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="be54f-124">Wachtwoord schendingen</span><span class="sxs-lookup"><span data-stu-id="be54f-124">Password breaches</span></span>

<span data-ttu-id="be54f-125">Microsoft werkt altijd één stap toostay tevoren cyberbeveiliging criminelen.</span><span class="sxs-lookup"><span data-stu-id="be54f-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="be54f-126">Hello Azure AD Identity Protection-team analyseert voortdurend wachtwoorden die vaak worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="be54f-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="be54f-127">Cyberbeveiliging criminelen ook gebruiken vergelijkbaar strategieën tooinform hun aanvallen, zoals gebouw een [Regenboog tabel](https://en.wikipedia.org/wiki/Rainbow_table) voor wachtwoord-hashes te kraken.</span><span class="sxs-lookup"><span data-stu-id="be54f-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="be54f-128">Microsoft analyseren voortdurend [gegevens schendingen](https://www.privacyrights.org/data-breaches) toomaintain een lijst met dynamisch bijgewerkte verboden wachtwoorden, die zorgt ervoor dat de wachtwoorden kwetsbaar zijn verboden voordat ze een reëel getal dreiging tooAzure AD-klanten.</span><span class="sxs-lookup"><span data-stu-id="be54f-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="be54f-129">Zie voor meer informatie over onze huidige beveiligingsinspanningen Hallo [Microsoft Intelligence beveiligingsrapport](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="be54f-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="be54f-130">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="be54f-130">Smart Password Lockout</span></span>

<span data-ttu-id="be54f-131">Als Azure AD een mogelijke poging cyberbeveiliging strafrechtelijke-toohack in het wachtwoord van een gebruiker detecteert, vergrendelen we Hallo-gebruikersaccount met slim wachtwoord vergrendeling.</span><span class="sxs-lookup"><span data-stu-id="be54f-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="be54f-132">Azure AD is ontworpen toodetermine Hallo risico dat samenhangt met specifieke aanmelding sessies.</span><span class="sxs-lookup"><span data-stu-id="be54f-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="be54f-133">Vervolgens wordt met het meest recente beveiligingsgegevens hello, accountvergrendeling semantiek toostop cyberbeveiliging bedreigingen worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="be54f-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="be54f-134">Als een gebruiker is vergrendeld buiten Azure AD, lijkt het scherm vergelijkbare toohello een die volgt op:</span><span class="sxs-lookup"><span data-stu-id="be54f-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Toegang tot Azure AD geblokkeerd](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="be54f-136">Voor andere Microsoft-accounts lijkt het scherm vergelijkbare toohello een die volgt op:</span><span class="sxs-lookup"><span data-stu-id="be54f-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Toegang tot Microsoft-account geblokkeerd](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="be54f-138">Zie voor informatie over het wachtwoord opnieuw instellen in Azure Active Directory, Hallo onderwerp [Azure AD selfservice voor wachtwoordherstel voor IT-professionals Hallo](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="be54f-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="be54f-139">Als u een Azure AD-beheerder bent, kunt u toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid dat uw gebruikers helemaal traditionele wachtwoorden maken.</span><span class="sxs-lookup"><span data-stu-id="be54f-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="be54f-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="be54f-140">Next steps</span></span>

* [<span data-ttu-id="be54f-141">Hoe tooupdate uw eigen wachtwoord</span><span class="sxs-lookup"><span data-stu-id="be54f-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="be54f-142">Hallo grondbeginselen van Azure identity management</span><span class="sxs-lookup"><span data-stu-id="be54f-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="be54f-143">Activiteit voor het rapport op wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="be54f-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


