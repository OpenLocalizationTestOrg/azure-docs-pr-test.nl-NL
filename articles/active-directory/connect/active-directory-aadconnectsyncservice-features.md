---
title: service aaaAzure AD Connect-synchronisatie-functies en configuratie | Microsoft Docs
description: Beschrijving van service aan clientzijde functies voor Azure AD Connect sync-service.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="4b410-103">Azure AD Connect sync-service-functies</span><span class="sxs-lookup"><span data-stu-id="4b410-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="4b410-104">de synchronisatiefunctie Hallo van Azure AD Connect bestaat uit twee onderdelen:</span><span class="sxs-lookup"><span data-stu-id="4b410-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="4b410-105">Hallo lokale onderdeel **Azure AD Connect-synchronisatie**, ook wel **synchronisatie-engine**.</span><span class="sxs-lookup"><span data-stu-id="4b410-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="4b410-106">Hallo-service die zich in Azure AD ook wel bekend als **Azure AD Connect sync-service**</span><span class="sxs-lookup"><span data-stu-id="4b410-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="4b410-107">Dit onderwerp wordt uitgelegd hoe Hallo na functies Hallo **Azure AD Connect-synchronisatieservice** werk en hoe kunt u ze configureren met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b410-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="4b410-108">Deze instellingen zijn geconfigureerd door Hallo [Azure Active Directory-Module voor Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="4b410-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="4b410-109">Download en installeer deze afzonderlijk van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="4b410-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="4b410-110">Hallo-cmdlets die zijn beschreven in dit onderwerp zijn geïntroduceerd in Hallo [versie van de maart 2016 (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="4b410-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="4b410-111">Als u geen Hallo-cmdlets die zijn beschreven in dit onderwerp of ze geen Hallo dezelfde leiden genereren, moet u ervoor zorgen kunt u de meest recente versie Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4b410-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="4b410-112">toosee hello configuratie in uw Azure AD-directory uitvoeren `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="4b410-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="4b410-113">![Get-MsolDirSyncFeatures resultaat](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="4b410-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="4b410-114">Veel van deze instellingen kunnen alleen worden gewijzigd door Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="4b410-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="4b410-115">Hallo volgende instellingen kunnen worden geconfigureerd door `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="4b410-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="4b410-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="4b410-116">DirSyncFeature</span></span> | <span data-ttu-id="4b410-117">Opmerking</span><span class="sxs-lookup"><span data-stu-id="4b410-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="4b410-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="4b410-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="4b410-119">Hiermee maakt objecten toojoin voor userPrincipalName toevoeging tooprimary SMTP-adres.</span><span class="sxs-lookup"><span data-stu-id="4b410-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="4b410-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="4b410-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="4b410-121">Hallo sync engine tooupdate Hallo kenmerk userPrincipalName kunt u gebruikers met beheerde/een licentie (niet-gefedereerde).</span><span class="sxs-lookup"><span data-stu-id="4b410-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="4b410-122">Nadat u een functie hebt ingeschakeld, kunnen deze kan niet worden uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4b410-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="4b410-123">Hallo van 24 augustus 2016 functie *dubbel kenmerk tolerantie* is standaard ingeschakeld voor de nieuwe Azure AD-mappen.</span><span class="sxs-lookup"><span data-stu-id="4b410-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="4b410-124">Deze functie wordt ook uitgerold en ingeschakeld op de mappen die zijn gemaakt voor deze datum.</span><span class="sxs-lookup"><span data-stu-id="4b410-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="4b410-125">U ontvangt een e-mailbericht wanneer uw directory over tooget deze functie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4b410-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="4b410-126">Hallo volgende instellingen zijn geconfigureerd voor Azure AD Connect en kan niet worden gewijzigd door `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="4b410-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="4b410-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="4b410-127">DirSyncFeature</span></span> | <span data-ttu-id="4b410-128">Opmerking</span><span class="sxs-lookup"><span data-stu-id="4b410-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="4b410-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="4b410-129">DeviceWriteback</span></span> |[<span data-ttu-id="4b410-130">Azure AD Connect: Apparaat terugschrijven inschakelen</span><span class="sxs-lookup"><span data-stu-id="4b410-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="4b410-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="4b410-131">DirectoryExtensions</span></span> |[<span data-ttu-id="4b410-132">Azure AD Connect-synchronisatie: Directory-uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="4b410-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="4b410-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="4b410-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="4b410-134">Hiermee kunt een kenmerk toobe in quarantaine geplaatst wanneer dit is een duplicaat van een ander object in plaats van het gehele object Hallo mislukt tijdens het exporteren.</span><span class="sxs-lookup"><span data-stu-id="4b410-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="4b410-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="4b410-135">PasswordSync</span></span> |[<span data-ttu-id="4b410-136">Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie implementeren</span><span class="sxs-lookup"><span data-stu-id="4b410-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="4b410-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="4b410-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="4b410-138">Voorbeeld: Groep terugschrijven</span><span class="sxs-lookup"><span data-stu-id="4b410-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="4b410-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="4b410-139">UserWriteback</span></span> |<span data-ttu-id="4b410-140">Momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4b410-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="4b410-141">Dubbel kenmerk tolerantie</span><span class="sxs-lookup"><span data-stu-id="4b410-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="4b410-142">In plaats van het mislukken van tooprovision objecten met dubbele UPN's / proxyAddresses, dubbel kenmerk Hallo 'quarantaine' en een tijdelijke-waarde is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4b410-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="4b410-143">Wanneer het Hallo-adresconflict is opgelost, Hallo tijdelijke UPN is de juiste waarde toohello automatisch gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="4b410-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="4b410-144">Zie voor meer informatie [tolerantie voor synchronisatie en dubbel kenmerk](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="4b410-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="4b410-145">UserPrincipalName zachte overeen</span><span class="sxs-lookup"><span data-stu-id="4b410-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="4b410-146">Wanneer deze functie is ingeschakeld, soft-match is ingeschakeld voor de UPN in toevoeging toohello [primaire SMTP-adres](https://support.microsoft.com/kb/2641663), die altijd is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4b410-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="4b410-147">Soft-match is gebruikte toomatch bestaande cloudgebruikers in Azure AD met on-premises gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4b410-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="4b410-148">Als u moet toomatch on-premises AD-accounts met bestaande accounts die zijn gemaakt in de cloud Hallo en u geen gebruikmaakt van Exchange Online en deze functie is handig.</span><span class="sxs-lookup"><span data-stu-id="4b410-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="4b410-149">In dit scenario wordt doorgaans hebt niet u een reden tooset Hallo SMTP-kenmerk in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="4b410-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="4b410-150">Deze functie op standaard voor nieuw is Azure AD-mappen.</span><span class="sxs-lookup"><span data-stu-id="4b410-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="4b410-151">U kunt zien of deze functie is ingeschakeld voor u door te voeren:</span><span class="sxs-lookup"><span data-stu-id="4b410-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="4b410-152">Als deze functie is niet ingeschakeld voor uw Azure AD-directory, kunt klikt u inschakelen door te voeren:</span><span class="sxs-lookup"><span data-stu-id="4b410-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="4b410-153">UserPrincipalName updates synchroniseren</span><span class="sxs-lookup"><span data-stu-id="4b410-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="4b410-154">In het verleden hebben is updates toohello UserPrincipalName kenmerk met de synchronisatieservice Hallo van on-premises geblokkeerd, tenzij beide volgende voorwaarden voldaan wordt:</span><span class="sxs-lookup"><span data-stu-id="4b410-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="4b410-155">Hallo-gebruiker wordt beheerd (niet-gefedereerde).</span><span class="sxs-lookup"><span data-stu-id="4b410-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="4b410-156">Hallo gebruiker heeft geen licentie toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4b410-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="4b410-157">Zie voor meer informatie [gebruiker namen in Office 365, Azure of Intune komen niet overeen op premises UPN of de alternatieve aanmeldings-ID Hallo](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="4b410-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="4b410-158">Inschakelen van deze functie kunt Hallo sync engine tooupdate Hallo userPrincipalName, wanneer het gewijzigde lokale is en u Wachtwoordsynchronisatie gebruiken. Als u federation gebruikt, wordt deze functie wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4b410-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="4b410-159">Deze functie op standaard voor nieuw is Azure AD-mappen.</span><span class="sxs-lookup"><span data-stu-id="4b410-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="4b410-160">U kunt zien of deze functie is ingeschakeld voor u door te voeren:</span><span class="sxs-lookup"><span data-stu-id="4b410-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="4b410-161">Als deze functie is niet ingeschakeld voor uw Azure AD-directory, kunt klikt u inschakelen door te voeren:</span><span class="sxs-lookup"><span data-stu-id="4b410-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="4b410-162">Nadat u deze functie inschakelt, bestaande userPrincipalName waarden blijft-is.</span><span class="sxs-lookup"><span data-stu-id="4b410-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="4b410-163">Op de volgende wijziging van Hallo userPrincipalName kenmerk lokale Hallo normale Deltasynchronisatie op gebruikers Hallo UPN bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="4b410-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="4b410-164">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4b410-164">See also</span></span>
* [<span data-ttu-id="4b410-165">Azure AD Connect-synchronisatie</span><span class="sxs-lookup"><span data-stu-id="4b410-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="4b410-166">[Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="4b410-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

