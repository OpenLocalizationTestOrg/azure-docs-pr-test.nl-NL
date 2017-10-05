---
title: Azure AD Connect sync-service-functies en configuratie | Microsoft Docs
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
ms.openlocfilehash: c2873510c280a2683c235cfdce3d2617c3b665cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="c256f-103">Azure AD Connect sync-service-functies</span><span class="sxs-lookup"><span data-stu-id="c256f-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="c256f-104">De synchronisatiefunctie van Azure AD Connect bestaat uit twee onderdelen:</span><span class="sxs-lookup"><span data-stu-id="c256f-104">The synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="c256f-105">Lokale onderdeel **Azure AD Connect-synchronisatie**, ook wel **synchronisatie-engine**.</span><span class="sxs-lookup"><span data-stu-id="c256f-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="c256f-106">De service zich in Azure AD, ook wel bekend als **Azure AD Connect sync-service**</span><span class="sxs-lookup"><span data-stu-id="c256f-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="c256f-107">Dit onderwerp wordt uitgelegd hoe u de volgende functies van de **Azure AD Connect-synchronisatieservice** werk en hoe kunt u ze configureren met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c256f-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="c256f-108">Deze instellingen zijn geconfigureerd door de [Azure Active Directory-Module voor Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="c256f-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="c256f-109">Download en installeer deze afzonderlijk van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c256f-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="c256f-110">De cmdlets die zijn beschreven in dit onderwerp zijn geïntroduceerd in de [versie van de maart 2016 (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="c256f-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="c256f-111">Als u niet de cmdlets in dit onderwerp wordt beschreven hebt of ze geen hetzelfde resultaat genereren, Controleer of dat u de meest recente versie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="c256f-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span></span>

<span data-ttu-id="c256f-112">Als u wilt zien van de configuratie in uw Azure AD-directory, `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="c256f-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="c256f-113">![Get-MsolDirSyncFeatures resultaat](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="c256f-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="c256f-114">Veel van deze instellingen kunnen alleen worden gewijzigd door Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c256f-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="c256f-115">De volgende instellingen kunnen worden geconfigureerd door `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="c256f-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="c256f-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="c256f-116">DirSyncFeature</span></span> | <span data-ttu-id="c256f-117">Opmerking</span><span class="sxs-lookup"><span data-stu-id="c256f-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="c256f-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="c256f-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="c256f-119">Hiermee kunt objecten die u wilt deelnemen aan op userPrincipalName naast het primaire SMTP-adres.</span><span class="sxs-lookup"><span data-stu-id="c256f-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span></span> |
| [<span data-ttu-id="c256f-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="c256f-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="c256f-121">Hiermee kunt de synchronisatie-engine voor het bijwerken van het kenmerk userPrincipalName voor gebruikers met beheerde/een licentie (niet-gefedereerde).</span><span class="sxs-lookup"><span data-stu-id="c256f-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="c256f-122">Nadat u een functie hebt ingeschakeld, kunnen deze kan niet worden uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c256f-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="c256f-123">Vanaf 24 augustus 2016 de functie *dubbel kenmerk tolerantie* is standaard ingeschakeld voor de nieuwe Azure AD-mappen.</span><span class="sxs-lookup"><span data-stu-id="c256f-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="c256f-124">Deze functie wordt ook uitgerold en ingeschakeld op de mappen die zijn gemaakt voor deze datum.</span><span class="sxs-lookup"><span data-stu-id="c256f-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="c256f-125">U ontvangt een e-mailbericht wanneer uw directory wordt deze functie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c256f-125">You will receive an email notification when your directory is about to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="c256f-126">De volgende instellingen zijn geconfigureerd voor Azure AD Connect en kan niet worden gewijzigd door `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="c256f-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="c256f-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="c256f-127">DirSyncFeature</span></span> | <span data-ttu-id="c256f-128">Opmerking</span><span class="sxs-lookup"><span data-stu-id="c256f-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="c256f-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="c256f-129">DeviceWriteback</span></span> |[<span data-ttu-id="c256f-130">Azure AD Connect: Apparaat terugschrijven inschakelen</span><span class="sxs-lookup"><span data-stu-id="c256f-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="c256f-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="c256f-131">DirectoryExtensions</span></span> |[<span data-ttu-id="c256f-132">Azure AD Connect-synchronisatie: Directory-uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="c256f-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="c256f-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="c256f-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="c256f-134">Hiermee kunt een kenmerk in quarantaine geplaatst wanneer dit is een duplicaat van een ander object in plaats van het gehele object mislukt tijdens het exporteren.</span><span class="sxs-lookup"><span data-stu-id="c256f-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span></span> |
| <span data-ttu-id="c256f-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="c256f-135">PasswordSync</span></span> |[<span data-ttu-id="c256f-136">Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie implementeren</span><span class="sxs-lookup"><span data-stu-id="c256f-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="c256f-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="c256f-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="c256f-138">Voorbeeld: Groep terugschrijven</span><span class="sxs-lookup"><span data-stu-id="c256f-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="c256f-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="c256f-139">UserWriteback</span></span> |<span data-ttu-id="c256f-140">Momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c256f-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="c256f-141">Dubbel kenmerk tolerantie</span><span class="sxs-lookup"><span data-stu-id="c256f-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="c256f-142">Objecten in plaats van het mislukken te richten met dubbele UPN's / proxyAddresses, het gedupliceerde kenmerk 'quarantaine' en een tijdelijke-waarde is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c256f-142">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="c256f-143">Als het conflict is opgelost, wordt de tijdelijke UPN automatisch gewijzigd in de juiste waarde.</span><span class="sxs-lookup"><span data-stu-id="c256f-143">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span></span> <span data-ttu-id="c256f-144">Zie voor meer informatie [tolerantie voor synchronisatie en dubbel kenmerk](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="c256f-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="c256f-145">UserPrincipalName zachte overeen</span><span class="sxs-lookup"><span data-stu-id="c256f-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="c256f-146">Wanneer deze functie is ingeschakeld, soft-match is ingeschakeld voor de UPN in aanvulling op de [primaire SMTP-adres](https://support.microsoft.com/kb/2641663), die altijd is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c256f-146">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="c256f-147">Soft-match wordt gebruikt voor bestaande cloudgebruikers in Azure AD overeen met on-premises gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c256f-147">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="c256f-148">Als u wilt vergelijken lokale AD-accounts met bestaande accounts die zijn gemaakt in de cloud en u geen gebruikmaakt van Exchange Online en deze functie is handig.</span><span class="sxs-lookup"><span data-stu-id="c256f-148">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="c256f-149">In dit scenario wordt doorgaans er geen reden is om de SMTP-kenmerk ingesteld in de cloud.</span><span class="sxs-lookup"><span data-stu-id="c256f-149">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span></span>

<span data-ttu-id="c256f-150">Deze functie op standaard voor nieuw is Azure AD-mappen.</span><span class="sxs-lookup"><span data-stu-id="c256f-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="c256f-151">U kunt zien of deze functie is ingeschakeld voor u door te voeren:</span><span class="sxs-lookup"><span data-stu-id="c256f-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="c256f-152">Als deze functie is niet ingeschakeld voor uw Azure AD-directory, kunt klikt u inschakelen door te voeren:</span><span class="sxs-lookup"><span data-stu-id="c256f-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="c256f-153">UserPrincipalName updates synchroniseren</span><span class="sxs-lookup"><span data-stu-id="c256f-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="c256f-154">In het verleden hebben updates voor het kenmerk UserPrincipalName met behulp van de synchronisatieservice van on-premises is geblokkeerd, tenzij beide volgende voorwaarden wordt voldaan:</span><span class="sxs-lookup"><span data-stu-id="c256f-154">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="c256f-155">De gebruiker wordt beheerd (niet-gefedereerde).</span><span class="sxs-lookup"><span data-stu-id="c256f-155">The user is managed (non-federated).</span></span>
* <span data-ttu-id="c256f-156">De gebruiker heeft geen licentie toegewezen.</span><span class="sxs-lookup"><span data-stu-id="c256f-156">The user has not been assigned a license.</span></span>

<span data-ttu-id="c256f-157">Zie voor meer informatie [gebruikersnamen in Office 365, Azure of Intune komen niet overeen met de lokale UPN of de alternatieve aanmeldings-ID](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="c256f-157">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="c256f-158">Deze functie inschakelt, kunt de synchronisatie-engine de userPrincipalName bijwerken wanneer het gewijzigde lokale is en u Wachtwoordsynchronisatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c256f-158">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password sync.</span></span> <span data-ttu-id="c256f-159">Als u federation gebruikt, wordt deze functie wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c256f-159">If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="c256f-160">Deze functie op standaard voor nieuw is Azure AD-mappen.</span><span class="sxs-lookup"><span data-stu-id="c256f-160">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="c256f-161">U kunt zien of deze functie is ingeschakeld voor u door te voeren:</span><span class="sxs-lookup"><span data-stu-id="c256f-161">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="c256f-162">Als deze functie is niet ingeschakeld voor uw Azure AD-directory, kunt klikt u inschakelen door te voeren:</span><span class="sxs-lookup"><span data-stu-id="c256f-162">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="c256f-163">Nadat u deze functie inschakelt, bestaande userPrincipalName waarden blijft-is.</span><span class="sxs-lookup"><span data-stu-id="c256f-163">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="c256f-164">Op de volgende wijziging van de userPrincipalName kenmerk on-premises, wordt de normale Deltasynchronisatie op gebruikers de UPN bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c256f-164">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="c256f-165">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c256f-165">See also</span></span>
* [<span data-ttu-id="c256f-166">Azure AD Connect-synchronisatie</span><span class="sxs-lookup"><span data-stu-id="c256f-166">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="c256f-167">[Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="c256f-167">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

