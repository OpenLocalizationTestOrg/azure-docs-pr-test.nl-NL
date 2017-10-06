---
title: aaaAzure AD Connect sync-service de kenmerken | Microsoft Docs
description: Hierin wordt beschreven hoe de kenmerken van werken in Azure AD Connect sync-service.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="b467c-103">Azure AD Connect sync-service de kenmerken</span><span class="sxs-lookup"><span data-stu-id="b467c-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="b467c-104">De meeste kenmerken worden vertegenwoordigd Hallo dezelfde manier in Azure AD omdat ze in uw lokale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b467c-104">Most attributes are represented hello same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="b467c-105">Maar bepaalde kenmerken hebben sommige speciale verwerking en Hallo-kenmerkwaarde in Azure AD mogelijk anders dan wat Azure AD Connect synchroniseert.</span><span class="sxs-lookup"><span data-stu-id="b467c-105">But some attributes have some special handling and hello attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="b467c-106">Introductie van de kenmerken</span><span class="sxs-lookup"><span data-stu-id="b467c-106">Introducing shadow attributes</span></span>
<span data-ttu-id="b467c-107">Enkele kenmerken hebben twee manieren in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b467c-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="b467c-108">Hallo lokale value- en een berekende waarde worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b467c-108">Both hello on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="b467c-109">Deze extra kenmerken worden de kenmerken van genoemd.</span><span class="sxs-lookup"><span data-stu-id="b467c-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="b467c-110">Hallo twee meest voorkomende kenmerken waarin u zien hoe dit gedrag zijn **userPrincipalName** en **proxyAddress**.</span><span class="sxs-lookup"><span data-stu-id="b467c-110">hello two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="b467c-111">Hallo wijziging in de kenmerkwaarden gebeurt wanneer er waarden zijn in deze kenmerken die niet-geverifieerd domeinen.</span><span class="sxs-lookup"><span data-stu-id="b467c-111">hello change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="b467c-112">Maar Hallo synchronisatie-engine in Connect Hallo waarde leest in Hallo shadow kenmerk dus vanuit het perspectief, Hallo-kenmerk is bevestigd door Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b467c-112">But hello sync engine in Connect reads hello value in hello shadow attribute so from its perspective, hello attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="b467c-113">U kunt hello Azure portal of met PowerShell met de kenmerken van Hallo niet zien.</span><span class="sxs-lookup"><span data-stu-id="b467c-113">You cannot see hello shadow attributes using hello Azure portal or with PowerShell.</span></span> <span data-ttu-id="b467c-114">Maar wat Hallo concept helpt u tootroubleshoot bepaalde scenario's waarin het Hallo-kenmerk een verschillende waarden voor de on-premises en in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="b467c-114">But understanding hello concept helps you tootroubleshoot certain scenarios where hello attribute has different values on-premises and in hello cloud.</span></span>

<span data-ttu-id="b467c-115">toobetter meer inzicht in gedrag Hallo, Bekijk dit voorbeeld van Fabrikam:</span><span class="sxs-lookup"><span data-stu-id="b467c-115">toobetter understand hello behavior, look at this example from Fabrikam:</span></span>  
![Domeinen](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="b467c-117">Ze hebben meerdere UPN-achtervoegsels in hun lokale Active Directory, maar ze deze alleen hebt gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="b467c-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="b467c-118">UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="b467c-118">userPrincipalName</span></span>
<span data-ttu-id="b467c-119">Een gebruiker heeft Hallo kenmerkwaarden in een niet-geverifieerd domein te volgen:</span><span class="sxs-lookup"><span data-stu-id="b467c-119">A user has hello following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="b467c-120">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="b467c-120">Attribute</span></span> | <span data-ttu-id="b467c-121">Waarde</span><span class="sxs-lookup"><span data-stu-id="b467c-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b467c-122">lokale userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="b467c-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="b467c-123">Azure AD-shadowUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="b467c-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="b467c-124">Azure AD-userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="b467c-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="b467c-125">Hallo userPrincipalName kenmerk is Hallo waarde die wordt weergegeven wanneer u PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b467c-125">hello userPrincipalName attribute is hello value you see when using PowerShell.</span></span>

<span data-ttu-id="b467c-126">Aangezien Hallo echte lokale kenmerk-waarde wordt opgeslagen in Azure AD, wanneer u Hallo fabrikam.com domein verifiëren, werkt Azure AD Hallo userPrincipalName kenmerk Hallo waarde uit Hallo shadowUserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="b467c-126">Since hello real on-premises attribute value is stored in Azure AD, when you verify hello fabrikam.com domain, Azure AD updates hello userPrincipalName attribute with hello value from hello shadowUserPrincipalName.</span></span> <span data-ttu-id="b467c-127">U hoeft geen toosynchronize eventuele wijzigingen van Azure AD Connect voor deze waarden toobe bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b467c-127">You do not have toosynchronize any changes from Azure AD Connect for these values toobe updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="b467c-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="b467c-128">proxyAddresses</span></span>
<span data-ttu-id="b467c-129">Hallo hetzelfde proces voor het opnemen van alleen geverifieerde domeinen vindt ook plaats voor proxyAddresses, maar met een aantal extra logica.</span><span class="sxs-lookup"><span data-stu-id="b467c-129">hello same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="b467c-130">Hallo geverifieerde domeinen zoekt alleen voor gebruikers postvak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b467c-130">hello check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="b467c-131">Een e-mailfunctionaliteit gebruiker of neem contact op met vertegenwoordigen een gebruiker in een andere Exchange-organisatie en u kunt alle waarden in proxyAddresses toothese objecten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b467c-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses toothese objects.</span></span>

<span data-ttu-id="b467c-132">Voor een postvakgebruiker, on-premises of in Exchange Online, wordt alleen de waarden voor geverifieerde domeinen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b467c-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="b467c-133">Het kan er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="b467c-133">It could look like this:</span></span>

| <span data-ttu-id="b467c-134">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="b467c-134">Attribute</span></span> | <span data-ttu-id="b467c-135">Waarde</span><span class="sxs-lookup"><span data-stu-id="b467c-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b467c-136">lokale proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="b467c-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="b467c-137">Exchange Online proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="b467c-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="b467c-138">In dit geval  **smtp:abbie.spencer@fabrikam.com**  is verwijderd, omdat dat domein is niet geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="b467c-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="b467c-139">Maar ook toegevoegd Exchange  **SIP:abbie.spencer@fabrikamonline.com** . Fabrikam nog niet is gebruikt Lync/Skype lokale, maar Azure AD en Exchange Online worden voorbereid voor.</span><span class="sxs-lookup"><span data-stu-id="b467c-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="b467c-140">Deze logica voor proxyAddresses is waarnaar wordt verwezen tooas **ProxyCalc**.</span><span class="sxs-lookup"><span data-stu-id="b467c-140">This logic for proxyAddresses is referred tooas **ProxyCalc**.</span></span> <span data-ttu-id="b467c-141">ProxyCalc wordt aangeroepen met elke wijziging van een gebruiker wanneer:</span><span class="sxs-lookup"><span data-stu-id="b467c-141">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="b467c-142">Hallo-gebruiker is een service-abonnement dat Exchange Online omvat, zelfs als het Hallo-gebruiker is geen licentie voor Exchange toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b467c-142">hello user has been assigned a service plan that includes Exchange Online even if hello user was not licensed for Exchange.</span></span> <span data-ttu-id="b467c-143">Bijvoorbeeld, als Hallo gebruiker is toegewezen Hallo Office E3 SKU, maar alleen is toegewezen SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="b467c-143">For example, if hello user is assigned hello Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="b467c-144">Dit geldt zelfs als uw postvak nog steeds lokaal is.</span><span class="sxs-lookup"><span data-stu-id="b467c-144">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="b467c-145">Hallo kenmerk msExchRecipientTypeDetails heeft een waarde.</span><span class="sxs-lookup"><span data-stu-id="b467c-145">hello attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="b467c-146">U een wijziging tooproxyAddresses of userPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="b467c-146">You make a change tooproxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="b467c-147">ProxyCalc kan duren voordat sommige tooprocess tijd een wijziging van een gebruiker en is niet synchroon met hello Azure AD Connect-exportproces.</span><span class="sxs-lookup"><span data-stu-id="b467c-147">ProxyCalc might take some time tooprocess a change on a user and is not synchronous with hello Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="b467c-148">Hallo ProxyCalc logica heeft een aantal extra gedrag voor geavanceerde scenario's niet in dit onderwerp wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="b467c-148">hello ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="b467c-149">In dit onderwerp is opgegeven voor u toounderstand Hallo gedrag en niet alle interne logische-document.</span><span class="sxs-lookup"><span data-stu-id="b467c-149">This topic is provided for you toounderstand hello behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="b467c-150">In quarantaine geplaatste kenmerkwaarden</span><span class="sxs-lookup"><span data-stu-id="b467c-150">Quarantined attribute values</span></span>
<span data-ttu-id="b467c-151">De kenmerken worden ook gebruikt als er dubbele kenmerkwaarden.</span><span class="sxs-lookup"><span data-stu-id="b467c-151">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="b467c-152">Zie voor meer informatie [dubbel kenmerk tolerantie](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="b467c-152">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b467c-153">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b467c-153">See also</span></span>
* [<span data-ttu-id="b467c-154">Azure AD Connect-synchronisatie</span><span class="sxs-lookup"><span data-stu-id="b467c-154">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="b467c-155">[Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="b467c-155">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
