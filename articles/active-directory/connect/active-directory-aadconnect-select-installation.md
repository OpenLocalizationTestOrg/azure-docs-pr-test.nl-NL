---
title: 'Azure AD Connect: Uw installatietype selecteren | Microsoft Docs'
description: In dit onderwerp leert u hoe tooselect Hallo installatie toouse Typ voor Azure AD Connect
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
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a><span data-ttu-id="bd848-103">Selecteer welk type installatie toouse voor Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="bd848-103">Select which installation type toouse for Azure AD Connect</span></span>
<span data-ttu-id="bd848-104">Azure AD Connect heeft twee installatietypen voor nieuwe installatie: Express en aangepast.</span><span class="sxs-lookup"><span data-stu-id="bd848-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="bd848-105">Dit onderwerp helpt u toodecide die optie toouse tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="bd848-105">This topic helps you toodecide which option toouse during installation.</span></span>

## <a name="express"></a><span data-ttu-id="bd848-106">Express</span><span class="sxs-lookup"><span data-stu-id="bd848-106">Express</span></span>
<span data-ttu-id="bd848-107">Express is de meest voorkomende optie Hallo en wordt gebruikt door ongeveer 90% van alle nieuwe installaties.</span><span class="sxs-lookup"><span data-stu-id="bd848-107">Express is hello most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="bd848-108">Was ontworpen tooprovide een configuratie die geschikt is voor Hallo meest voorkomende klant scenario's.</span><span class="sxs-lookup"><span data-stu-id="bd848-108">It was designed tooprovide a configuration that works for hello most common customer scenarios.</span></span>

<span data-ttu-id="bd848-109">Er wordt vanuit gegaan:</span><span class="sxs-lookup"><span data-stu-id="bd848-109">It assumes:</span></span>

- <span data-ttu-id="bd848-110">U hebt een enkele Active Directory lokale forest.</span><span class="sxs-lookup"><span data-stu-id="bd848-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="bd848-111">U hebt een enterprise-beheerdersaccount die voor Hallo installatie kunt u.</span><span class="sxs-lookup"><span data-stu-id="bd848-111">You have an enterprise administrator account you can use for hello installation.</span></span>
- <span data-ttu-id="bd848-112">U hebt minder dan 100.000 objecten in uw lokale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bd848-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="bd848-113">U krijgt:</span><span class="sxs-lookup"><span data-stu-id="bd848-113">You get:</span></span>

- <span data-ttu-id="bd848-114">[Wachtwoordsynchronisatie](active-directory-aadconnectsync-implement-password-synchronization.md) van lokale tooAzure AD voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="bd848-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises tooAzure AD for single sign-on.</span></span>
- <span data-ttu-id="bd848-115">Een configuratie die wordt gesynchroniseerd [gebruikers, groepen, contactpersonen en Windows 10-computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="bd848-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="bd848-116">Synchronisatie van alle in aanmerking komende objecten in alle domeinen en alle OE's.</span><span class="sxs-lookup"><span data-stu-id="bd848-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="bd848-117">[Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is ingeschakeld toomake zeker dat u altijd Hallo meest recente versie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bd848-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled toomake sure you always use hello latest available version.</span></span>

<span data-ttu-id="bd848-118">Opties voor waar u Express nog steeds kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bd848-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="bd848-119">Als u niet dat toosynchronize alle OE's wilt, u kunt nog steeds gebruiken Express en op de laatste pagina hello, het vakje **Start het synchronisatieproces Hallo...** *.</span><span class="sxs-lookup"><span data-stu-id="bd848-119">If you do not want toosynchronize all OUs, you can still use Express and on hello last page, unselect **Start hello synchronization process...***.</span></span> <span data-ttu-id="bd848-120">Vervolgens Hallo-installatiewizard opnieuw uitvoeren en wijzigen van Hallo OE's in [configuratieopties](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) en geplande synchronisatie inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bd848-120">Then run hello installation wizard again and change hello OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="bd848-121">Wilt u tooenable een Hallo-functies in Azure AD Premium, zoals wachtwoord terugschrijven.</span><span class="sxs-lookup"><span data-stu-id="bd848-121">You want tooenable one of hello features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="bd848-122">Ga eerst via snelle tooget Hallo initiële installatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="bd848-122">First go through express tooget hello initial installation completed.</span></span> <span data-ttu-id="bd848-123">Vervolgens Hallo-installatiewizard opnieuw uitvoeren en wijzigen van Hallo [configuratieopties](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="bd848-123">Then run hello installation wizard again and change hello [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="bd848-124">Aangepast telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="bd848-124">Custom</span></span>
<span data-ttu-id="bd848-125">Hallo aangepaste pad kunt veel meer opties dan express.</span><span class="sxs-lookup"><span data-stu-id="bd848-125">hello customized path allows many more options than express.</span></span> <span data-ttu-id="bd848-126">Het moet worden gebruikt in alle gevallen waarbij Hallo-configuratie wordt beschreven in de vorige sectie voor snelle niet representatief is voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="bd848-126">It should be used in all cases where hello configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="bd848-127">Gebruiken wanneer:</span><span class="sxs-lookup"><span data-stu-id="bd848-127">Use when:</span></span>

- <span data-ttu-id="bd848-128">U hebt geen toegang tot tooan enterprise-beheerdersaccount in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bd848-128">You do not have access tooan enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="bd848-129">U hebt meer dan één forest of u van plan bent toosynchronize meer dan één forest in toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd848-129">You have more than one forest or you plan toosynchronize more than one forest in hello future.</span></span>
- <span data-ttu-id="bd848-130">U kunt domeinen hebt in uw forest niet bereikbaar is vanaf Hallo Connect-server.</span><span class="sxs-lookup"><span data-stu-id="bd848-130">You have domains in your forest not reachable from hello Connect server.</span></span>
- <span data-ttu-id="bd848-131">U van plan bent toouse federation of Pass through-verificatie voor de gebruiker zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="bd848-131">You plan toouse federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="bd848-132">U hebt meer dan 100.000 objecten en moet toouse een volledige SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bd848-132">You have more than 100,000 objects and need toouse a full SQL Server.</span></span>
- <span data-ttu-id="bd848-133">U van plan bent toouse filteren op basis van een groep en niet alleen domein of filteren op basis van organisatie-eenheid.</span><span class="sxs-lookup"><span data-stu-id="bd848-133">You plan toouse group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="bd848-134">Upgraden van DirSync</span><span class="sxs-lookup"><span data-stu-id="bd848-134">Upgrade from DirSync</span></span>
<span data-ttu-id="bd848-135">Als u momenteel DirSync gebruikt, stappen Hallo in [Upgrade van DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade uw bestaande configuratie.</span><span class="sxs-lookup"><span data-stu-id="bd848-135">If you are currently using DirSync, then follow hello steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade your existing configuration.</span></span> <span data-ttu-id="bd848-136">Er zijn twee verschillende upgrade-opties:</span><span class="sxs-lookup"><span data-stu-id="bd848-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="bd848-137">In-place upgrade tooinstall verbinding maken op Hallo dezelfde server.</span><span class="sxs-lookup"><span data-stu-id="bd848-137">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="bd848-138">Parallelle implementatie tooinstall Connect op een nieuwe server tijdens het Hallo bestaande DirSync-server nog steeds operationeel is.</span><span class="sxs-lookup"><span data-stu-id="bd848-138">Parallel deployment tooinstall Connect on a new server while hello existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="bd848-139">Upgrade uitvoeren vanaf Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="bd848-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="bd848-140">Als u Azure AD Sync momenteel gebruikt, wordt u Hallo volgen kunt [dezelfde stappen](active-directory-aadconnect-upgrade-previous-version.md) als wanneer u een van de nieuwere versie tooa één verbinding maken upgrade.</span><span class="sxs-lookup"><span data-stu-id="bd848-140">If you are currently using Azure AD Sync, then you can follow hello [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version tooa newer.</span></span> <span data-ttu-id="bd848-141">Er zijn twee verschillende upgrade-opties:</span><span class="sxs-lookup"><span data-stu-id="bd848-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="bd848-142">In-place upgrade tooinstall verbinding maken op Hallo dezelfde server.</span><span class="sxs-lookup"><span data-stu-id="bd848-142">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="bd848-143">Swing migratie tooinstall Connect op een nieuwe server tijdens het Hallo bestaande Azure AD Sync-server nog steeds operationeel is.</span><span class="sxs-lookup"><span data-stu-id="bd848-143">Swing-migration tooinstall Connect on a new server while hello existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="bd848-144">Migreren van FIM 2010 wachtwoordherstelextensies of MIM2016</span><span class="sxs-lookup"><span data-stu-id="bd848-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="bd848-145">Als u momenteel Forefront Identity Manager 2010 of Microsoft Identity Manager 2016 Hello Azure AD-Connector gebruikt, is de enige optie een migratie.</span><span class="sxs-lookup"><span data-stu-id="bd848-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with hello Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="bd848-146">Volg de stappen Hallo in [swing migratie](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="bd848-146">Follow hello steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="bd848-147">FIM 2010 wachtwoordherstelextensies/MIM2016 in stappen van hello, vervangen een melding van Azure AD Sync.</span><span class="sxs-lookup"><span data-stu-id="bd848-147">In hello steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd848-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bd848-148">Next steps</span></span>
<span data-ttu-id="bd848-149">Afhankelijk van de optie Hallo u toouse hebt geselecteerd, Hallo tabel gebruiken van inhoud toohello links toofind uw artikel Hello gedetailleerde stappen.</span><span class="sxs-lookup"><span data-stu-id="bd848-149">Depending on hello option you have selected toouse, use hello table of content toohello left toofind your article with hello detailed steps.</span></span>
