---
title: Azure AD Connect sync-service de kenmerken van | Microsoft Docs
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
ms.openlocfilehash: 0b6a7f22d744480a40a878c979986cdd7667109c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="a9a6b-103">Azure AD Connect sync-service de kenmerken</span><span class="sxs-lookup"><span data-stu-id="a9a6b-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="a9a6b-104">De meeste kenmerken worden dezelfde manier weergegeven in Azure AD omdat ze in uw lokale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-104">Most attributes are represented the same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="a9a6b-105">Maar bepaalde kenmerken sommige speciale verwerking hebben en de waarde van het kenmerk in Azure AD is mogelijk anders dan wat Azure AD Connect synchroniseert.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-105">But some attributes have some special handling and the attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="a9a6b-106">Introductie van de kenmerken</span><span class="sxs-lookup"><span data-stu-id="a9a6b-106">Introducing shadow attributes</span></span>
<span data-ttu-id="a9a6b-107">Enkele kenmerken hebben twee manieren in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="a9a6b-108">Zowel de lokale waarde en een berekende waarde worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-108">Both the on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="a9a6b-109">Deze extra kenmerken worden de kenmerken van genoemd.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="a9a6b-110">De twee meest voorkomende kenmerken waarin u zien hoe dit gedrag zijn **userPrincipalName** en **proxyAddress**.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-110">The two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="a9a6b-111">De wijziging in de kenmerkwaarden gebeurt wanneer er waarden zijn in deze kenmerken die niet-geverifieerd domeinen.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-111">The change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="a9a6b-112">Maar de synchronisatie-engine in Connect leest de waarde in het kenmerk shadow dus vanuit het perspectief, het kenmerk is bevestigd door Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-112">But the sync engine in Connect reads the value in the shadow attribute so from its perspective, the attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="a9a6b-113">U kunt de kenmerken van de schaduw met behulp van de Azure portal of met PowerShell niet zien.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-113">You cannot see the shadow attributes using the Azure portal or with PowerShell.</span></span> <span data-ttu-id="a9a6b-114">Maar het concept kennis helpt u bij het oplossen van bepaalde scenario's waarin het kenmerk verschillende waarden voor de on-premises een en in de cloud.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-114">But understanding the concept helps you to troubleshoot certain scenarios where the attribute has different values on-premises and in the cloud.</span></span>

<span data-ttu-id="a9a6b-115">Bekijk voor meer informatie over het gedrag, in dit voorbeeld van Fabrikam:</span><span class="sxs-lookup"><span data-stu-id="a9a6b-115">To better understand the behavior, look at this example from Fabrikam:</span></span>  
![Domeinen](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="a9a6b-117">Ze hebben meerdere UPN-achtervoegsels in hun lokale Active Directory, maar ze deze alleen hebt gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="a9a6b-118">UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="a9a6b-118">userPrincipalName</span></span>
<span data-ttu-id="a9a6b-119">Een gebruiker heeft de volgende kenmerkwaarden in een niet-geverifieerd domein:</span><span class="sxs-lookup"><span data-stu-id="a9a6b-119">A user has the following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="a9a6b-120">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="a9a6b-120">Attribute</span></span> | <span data-ttu-id="a9a6b-121">Waarde</span><span class="sxs-lookup"><span data-stu-id="a9a6b-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a9a6b-122">lokale userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="a9a6b-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="a9a6b-123">Azure AD-shadowUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="a9a6b-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="a9a6b-124">Azure AD-userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="a9a6b-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="a9a6b-125">Het kenmerk userPrincipalName is de waarde die u ziet wanneer met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-125">The userPrincipalName attribute is the value you see when using PowerShell.</span></span>

<span data-ttu-id="a9a6b-126">Omdat de waarde van het kenmerk echte lokaal wordt opgeslagen in Azure AD, wanneer u het fabrikam.com-domein verifiëren, Azure AD-het kenmerk userPrincipalName updates met de waarde van de shadowUserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-126">Since the real on-premises attribute value is stored in Azure AD, when you verify the fabrikam.com domain, Azure AD updates the userPrincipalName attribute with the value from the shadowUserPrincipalName.</span></span> <span data-ttu-id="a9a6b-127">U hebt geen Synchroniseer eventuele wijzigingen van Azure AD Connect voor deze waarden moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-127">You do not have to synchronize any changes from Azure AD Connect for these values to be updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="a9a6b-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="a9a6b-128">proxyAddresses</span></span>
<span data-ttu-id="a9a6b-129">Hetzelfde proces voor het opnemen van alleen geverifieerde domeinen vindt ook plaats voor proxyAddresses, maar met een aantal extra logica.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-129">The same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="a9a6b-130">De controle op geverifieerde domeinen alleen voor gebruikers postvak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-130">The check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="a9a6b-131">Een e-mailfunctionaliteit gebruiker of neem contact op met vertegenwoordigen een gebruiker in een andere Exchange-organisatie en u kunt alle waarden in proxyAddresses toevoegen aan deze objecten.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses to these objects.</span></span>

<span data-ttu-id="a9a6b-132">Voor een postvakgebruiker, on-premises of in Exchange Online, wordt alleen de waarden voor geverifieerde domeinen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="a9a6b-133">Het kan er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="a9a6b-133">It could look like this:</span></span>

| <span data-ttu-id="a9a6b-134">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="a9a6b-134">Attribute</span></span> | <span data-ttu-id="a9a6b-135">Waarde</span><span class="sxs-lookup"><span data-stu-id="a9a6b-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a9a6b-136">lokale proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="a9a6b-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="a9a6b-137">Exchange Online proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="a9a6b-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="a9a6b-138">In dit geval  **smtp:abbie.spencer@fabrikam.com**  is verwijderd, omdat dat domein is niet geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="a9a6b-139">Maar ook toegevoegd Exchange  **SIP:abbie.spencer@fabrikamonline.com** .</span><span class="sxs-lookup"><span data-stu-id="a9a6b-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**.</span></span> <span data-ttu-id="a9a6b-140">Fabrikam nog niet is gebruikt Lync/Skype lokale, maar Azure AD en Exchange Online worden voorbereid voor.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-140">Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="a9a6b-141">Deze logica voor proxyAddresses wordt aangeduid als **ProxyCalc**.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-141">This logic for proxyAddresses is referred to as **ProxyCalc**.</span></span> <span data-ttu-id="a9a6b-142">ProxyCalc wordt aangeroepen met elke wijziging van een gebruiker wanneer:</span><span class="sxs-lookup"><span data-stu-id="a9a6b-142">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="a9a6b-143">De gebruiker is een service-abonnement dat Exchange Online omvat, zelfs als de gebruiker is geen licentie voor Exchange toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-143">The user has been assigned a service plan that includes Exchange Online even if the user was not licensed for Exchange.</span></span> <span data-ttu-id="a9a6b-144">Bijvoorbeeld als de gebruiker de Office E3-SKU is toegewezen, maar is alleen SharePoint Online toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-144">For example, if the user is assigned the Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="a9a6b-145">Dit geldt zelfs als uw postvak nog steeds lokaal is.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-145">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="a9a6b-146">Het kenmerk msExchRecipientTypeDetails heeft een waarde.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-146">The attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="a9a6b-147">U aanbrengt een wijziging in proxyAddresses of userPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-147">You make a change to proxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="a9a6b-148">ProxyCalc kan even duren voor het verwerken van een gebruiker wordt gewijzigd en is niet synchroon met de Azure AD Connect-exportproces.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-148">ProxyCalc might take some time to process a change on a user and is not synchronous with the Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="a9a6b-149">De logica ProxyCalc heeft een aantal extra gedrag voor geavanceerde scenario's niet in dit onderwerp wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-149">The ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="a9a6b-150">In dit onderwerp is beschikbaar voor u meer inzicht in het gedrag en niet alle interne logische-document.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-150">This topic is provided for you to understand the behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="a9a6b-151">In quarantaine geplaatste kenmerkwaarden</span><span class="sxs-lookup"><span data-stu-id="a9a6b-151">Quarantined attribute values</span></span>
<span data-ttu-id="a9a6b-152">De kenmerken worden ook gebruikt als er dubbele kenmerkwaarden.</span><span class="sxs-lookup"><span data-stu-id="a9a6b-152">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="a9a6b-153">Zie voor meer informatie [dubbel kenmerk tolerantie](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="a9a6b-153">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a9a6b-154">Zie ook</span><span class="sxs-lookup"><span data-stu-id="a9a6b-154">See also</span></span>
* [<span data-ttu-id="a9a6b-155">Azure AD Connect-synchronisatie</span><span class="sxs-lookup"><span data-stu-id="a9a6b-155">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="a9a6b-156">[Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="a9a6b-156">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
