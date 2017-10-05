---
title: Azure AD gelaagde wachtwoordbeveiliging | Microsoft Docs
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
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a><span data-ttu-id="543bb-103">Een benadering meerdere lagen van beveiliging voor Azure AD-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="543bb-103">A multi-tiered approach to Azure AD password security</span></span>

<span data-ttu-id="543bb-104">Dit artikel worden enkele aanbevolen procedures kunt u als een gebruiker of als een beheerder om uw Azure Active Directory (Azure AD) of de Microsoft-Account te beschermen.</span><span class="sxs-lookup"><span data-stu-id="543bb-104">This article discusses some best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="543bb-105">Azure AD-beheerders kunnen gebruikerswachtwoorden met behulp van de instructies in het artikel [opnieuw instellen van het wachtwoord voor een gebruiker in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="543bb-105">Azure AD administrators can reset user passwords using the guidance in the article [Reset the password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="543bb-106">Gebruikers kunnen hun eigen wachtwoord met behulp van de instructies in het artikel in opnieuw instellen [Help ik mijn Azure AD-wachtwoord vergeten](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="543bb-106">Users can reset their own password using the guidance in the article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="543bb-107">Vereisten voor wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="543bb-107">Password requirements</span></span>

<span data-ttu-id="543bb-108">In Azure AD worden de volgende algemene benaderingen gebruikt om wachtwoorden te beveiligen:</span><span class="sxs-lookup"><span data-stu-id="543bb-108">Azure AD incorporates the following common approaches to securing passwords:</span></span>

* <span data-ttu-id="543bb-109">Vereisten voor de lengte van het wachtwoord</span><span class="sxs-lookup"><span data-stu-id="543bb-109">Password length requirements</span></span>
* <span data-ttu-id="543bb-110">Vereisten voor wachtwoordcomplexiteit</span><span class="sxs-lookup"><span data-stu-id="543bb-110">Password complexity requirements</span></span>
* <span data-ttu-id="543bb-111">Gepland en automatisch verlopen van wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="543bb-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="543bb-112">Zie het onderwerp voor informatie over het wachtwoord opnieuw instellen in Azure Active Directory, [Azure AD selfservice voor wachtwoordherstel voor IT-professionals](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="543bb-112">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="543bb-113">Bescherming van Azure AD-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="543bb-113">Azure AD password protections</span></span>

<span data-ttu-id="543bb-114">Azure AD en de Microsoft-Accountsysteem bedrijfstak bewezen benaderingen gebruiken om te controleren of de beveiliging van gebruikers- en wachtwoorden, waaronder:</span><span class="sxs-lookup"><span data-stu-id="543bb-114">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="543bb-115">Dynamisch uitsluiten van wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="543bb-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="543bb-116">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="543bb-116">Smart Password Lockout</span></span>

<span data-ttu-id="543bb-117">Zie voor informatie over wachtwoordbeheer op basis van huidige research in dit technisch document [wachtwoord richtlijnen](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="543bb-117">For information about password management based on current research, see the whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="543bb-118">Dynamisch uitsluiten van wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="543bb-118">Dynamically banned passwords</span></span>

<span data-ttu-id="543bb-119">Azure AD en Microsoft-Accounts wachtwoordbeveiliging veiligstellen door dynamisch verboden veelgebruikte wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="543bb-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="543bb-120">Het Azure AD Identity Protection-team maakt regelmatig analyses van lijsten met uitgesloten wachtwoorden, om te voorkomen dat gebruikers wachtwoorden selecteren die regelmatig worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="543bb-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="543bb-121">Deze service is beschikbaar voor klanten van Azure AD en de Microsoft-accountservice.</span><span class="sxs-lookup"><span data-stu-id="543bb-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span>

<span data-ttu-id="543bb-122">Bij het maken van wachtwoorden, is het belangrijk zijn voor beheerders om aan te raden gebruikers kiezen wachtwoord zinnen met een unieke combinatie van letters, cijfers, tekens of woorden.</span><span class="sxs-lookup"><span data-stu-id="543bb-122">When creating passwords, it is important for administrators to encourage users to choose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="543bb-123">Deze aanpak kunt u gebruikerswachtwoorden nagenoeg onmogelijk waarmee is geknoeid, maar gebruikers te onthouden gemakkelijker te maken.</span><span class="sxs-lookup"><span data-stu-id="543bb-123">This approach helps to make user passwords nearly impossible to be compromised but easier for users to remember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="543bb-124">Wachtwoord schendingen</span><span class="sxs-lookup"><span data-stu-id="543bb-124">Password breaches</span></span>

<span data-ttu-id="543bb-125">Microsoft werkt altijd om te blijven van één stap tevoren cyberbeveiliging criminelen.</span><span class="sxs-lookup"><span data-stu-id="543bb-125">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="543bb-126">Het Azure AD Identity Protection-team analyseert voortdurend wachtwoorden die vaak worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="543bb-126">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="543bb-127">Cybercriminelen maken gebruik van vergelijkbare strategieën voor hun aanvallen, zoals het samenstellen van een [rainbow-tabel](https://en.wikipedia.org/wiki/Rainbow_table) om wachtwoord-hashes te kraken.</span><span class="sxs-lookup"><span data-stu-id="543bb-127">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="543bb-128">Microsoft analyseert voortdurend [gegevensschendingen](https://www.privacyrights.org/data-breaches) om een dynamisch bijgewerkte lijst met uitgesloten wachtwoorden te onderhouden die ervoor zorgt dat kwetsbare wachtwoorden worden uitgesloten voordat ze een echte bedreiging kunnen vormen voor klanten van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="543bb-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="543bb-129">Raadpleeg het [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx) voor meer informatie over onze inspanningen op dit gebied. Dit rapport is alleen in het Engels beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="543bb-129">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="543bb-130">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="543bb-130">Smart Password Lockout</span></span>

<span data-ttu-id="543bb-131">Als Azure AD vaststelt dat een mogelijke cybercrimineel probeert om het wachtwoord van een gebruiker te achterhalen, wordt het gebruikersaccount vergrendeld met Smart Password Lockout.</span><span class="sxs-lookup"><span data-stu-id="543bb-131">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="543bb-132">Azure AD bevat logica om het risico te bepalen dat samenhangt met specifieke aanmeldingssessies.</span><span class="sxs-lookup"><span data-stu-id="543bb-132">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> <span data-ttu-id="543bb-133">Vervolgens wordt met de meest recente beveiligingsgegevens toegepast accountvergrendeling, zodat u cyberbeveiliging bedreigingen te stoppen.</span><span class="sxs-lookup"><span data-stu-id="543bb-133">Then using the most up-to-date security data, we apply lockout semantics to stop cyber threats.</span></span>

<span data-ttu-id="543bb-134">Als een gebruiker is vergrendeld buiten Azure AD, wordt het scherm op de link die erna lijkt:</span><span class="sxs-lookup"><span data-stu-id="543bb-134">If a user is locked out of Azure AD, their screen looks similar to the one that follows:</span></span>

  ![Toegang tot Azure AD geblokkeerd](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="543bb-136">Voor andere Microsoft-accounts lijkt het scherm op de link die erna:</span><span class="sxs-lookup"><span data-stu-id="543bb-136">For other Microsoft accounts, their screen looks similar to the one that follows:</span></span>

  ![Toegang tot Microsoft-account geblokkeerd](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="543bb-138">Zie het onderwerp voor informatie over het wachtwoord opnieuw instellen in Azure Active Directory, [Azure AD selfservice voor wachtwoordherstel voor IT-professionals](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="543bb-138">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="543bb-139">Als u een Azure AD-beheerder bent, kunt u [Windows Hello](https://www.microsoft.com/windows/windows-hello) gebruiken om ervoor te zorgen dat uw gebruikers helemaal geen traditionele wachtwoorden meer hoeven te maken.</span><span class="sxs-lookup"><span data-stu-id="543bb-139">If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="543bb-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="543bb-140">Next steps</span></span>

* [<span data-ttu-id="543bb-141">Uw eigen wachtwoord bijwerken</span><span class="sxs-lookup"><span data-stu-id="543bb-141">How to update your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* <span data-ttu-id="543bb-142">[The fundamentals of Azure identity management](fundamentals-identity.md) (De grondbeginselen van Azure-identiteitsbeheer)</span><span class="sxs-lookup"><span data-stu-id="543bb-142">[The fundamentals of Azure identity management](fundamentals-identity.md)</span></span>
* [<span data-ttu-id="543bb-143">Activiteit voor het rapport op wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="543bb-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


