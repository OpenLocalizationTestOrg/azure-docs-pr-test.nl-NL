---
title: Opnieuw uit te voeren hello Azure AD Connect-installatiewizard | Microsoft Docs
description: Wordt uitgelegd hoe Hallo-installatiewizard werkt Hallo tweede keer dat u deze uitvoert.
keywords: Hello Azure AD Connect-installatiewizard kunt u de tweede keer dat u het uitvoeren van onderhoud instellingen Hallo configureren
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="65462-104">Azure AD Connect-synchronisatie: Hallo-installatiewizard een tweede keer uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="65462-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="65462-105">Hallo u eerste keer hello Azure AD Connect-installatiewizard uitvoert deze laat zien hoe u tooconfigure uw installatie.</span><span class="sxs-lookup"><span data-stu-id="65462-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="65462-106">Als u de installatiewizard Hallo opnieuw uitvoert, biedt opties voor onderhoud.</span><span class="sxs-lookup"><span data-stu-id="65462-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="65462-107">U vindt Hallo-installatiewizard in Hallo Startmenu met de naam **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="65462-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![Het menu Start](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="65462-109">Wanneer u Hallo-installatiewizard te starten, ziet u een pagina met deze opties:</span><span class="sxs-lookup"><span data-stu-id="65462-109">When you start hello installation wizard, you see a page with these options:</span></span>

![Pagina met een lijst van extra taken](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="65462-111">Als u AD FS hebt geïnstalleerd met Azure AD Connect, hebt u nog meer opties.</span><span class="sxs-lookup"><span data-stu-id="65462-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="65462-112">aanvullende opties die u hebt voor AD FS zijn gedocumenteerd in Hallo [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="65462-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="65462-113">Selecteer een van de Hallo taken en klikt u op **volgende** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="65462-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65462-114">Terwijl u Hallo-installatiewizard open zijn, worden alle bewerkingen in de synchronisatie-engine Hallo onderbroken.</span><span class="sxs-lookup"><span data-stu-id="65462-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="65462-115">Zorg ervoor dat u de installatiewizard Hallo sluiten als u uw wijzigingen in de configuratie hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="65462-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="65462-116">De huidige configuratie weergeven</span><span class="sxs-lookup"><span data-stu-id="65462-116">View current configuration</span></span>
<span data-ttu-id="65462-117">Deze optie biedt een overzicht van de momenteel geconfigureerde opties.</span><span class="sxs-lookup"><span data-stu-id="65462-117">This option gives you a quick view of your currently configured options.</span></span>

![Pagina met een lijst met alle opties en hun status](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="65462-119">Klik op **vorige** toogo terug.</span><span class="sxs-lookup"><span data-stu-id="65462-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="65462-120">Als u selecteert **afsluiten**, u Hallo-installatiewizard sluit.</span><span class="sxs-lookup"><span data-stu-id="65462-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="65462-121">Opties voor synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="65462-121">Customize synchronization options</span></span>
<span data-ttu-id="65462-122">Deze optie is configuratie gebruikte toomake wijzigingen toohello-synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="65462-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="65462-123">Er is een subset van de opties in het installatiepad van Hallo aangepaste configuratie.</span><span class="sxs-lookup"><span data-stu-id="65462-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="65462-124">U ziet deze optie ook als u snelle installatie in eerste instantie worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65462-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="65462-125">[Toevoegen van meer mappen](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="65462-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="65462-126">Zie voor het verwijderen van een map [verwijderen van een Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="65462-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="65462-127">[Wijzigen van domein en OE filteren](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="65462-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="65462-128">Filteren van de groep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="65462-128">Remove Group filtering.</span></span>
* <span data-ttu-id="65462-129">[Optionele functies wijzigen](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="65462-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="65462-130">Hallo andere opties van de eerste installatie Hallo kunnen niet worden gewijzigd en zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="65462-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="65462-131">Deze opties zijn:</span><span class="sxs-lookup"><span data-stu-id="65462-131">These options are:</span></span>

* <span data-ttu-id="65462-132">Hallo kenmerk toouse voor userPrincipalName en sourceAnchor wijzigen.</span><span class="sxs-lookup"><span data-stu-id="65462-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="65462-133">Lid worden van de methode voor objecten van een ander forest Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="65462-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="65462-134">Filteren op basis van een groep inschakelen.</span><span class="sxs-lookup"><span data-stu-id="65462-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="65462-135">Directory-schema vernieuwen</span><span class="sxs-lookup"><span data-stu-id="65462-135">Refresh directory schema</span></span>
<span data-ttu-id="65462-136">Deze optie wordt gebruikt als u Hallo schema hebt gewijzigd in een van uw on-premises AD DS-forests.</span><span class="sxs-lookup"><span data-stu-id="65462-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="65462-137">Bijvoorbeeld, kan ook Exchange zijn geïnstalleerd of bijgewerkt schema met apparaatobjecten tooa Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="65462-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="65462-138">In dit geval moet tooinstruct Azure AD Connect tooread Hallo schema opnieuw uit AD DS en de cache niet bijwerken.</span><span class="sxs-lookup"><span data-stu-id="65462-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="65462-139">Deze actie wordt ook Hallo Sync regels opnieuw gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="65462-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="65462-140">Als u Hallo Exchange-schema, bijvoorbeeld toevoegt, worden Hallo Sync regels voor Exchange toohello configuratie toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="65462-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="65462-141">Wanneer u deze optie selecteert, worden alle Hallo mappen in uw configuratie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="65462-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="65462-142">U kunt Hallo standaardinstelling behouden en Vernieuw alle forests of selectie ervan opheffen enkele ervan.</span><span class="sxs-lookup"><span data-stu-id="65462-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Pagina met een lijst met alle mappen in Hallo-omgeving](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="65462-144">Faseringsmodus configureren</span><span class="sxs-lookup"><span data-stu-id="65462-144">Configure staging mode</span></span>
<span data-ttu-id="65462-145">Deze optie kunt u tooenable en schakel de faseringsmodus op Hallo server uit.</span><span class="sxs-lookup"><span data-stu-id="65462-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="65462-146">Meer informatie over modus en hoe deze wordt gebruikt voor gefaseerde installatie vindt u in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="65462-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="65462-147">Hallo-optie ziet als tijdelijke momenteel is ingeschakeld of uitgeschakeld:</span><span class="sxs-lookup"><span data-stu-id="65462-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![Optie die ook Hallo huidige status van de faseringsmodus wordt weergegeven](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="65462-149">toochange Hallo status, selecteer deze optie en selecteren of selectie Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="65462-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![Optie die ook Hallo huidige status van de faseringsmodus wordt weergegeven](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="65462-151">Gebruikersaanmelding wijzigen</span><span class="sxs-lookup"><span data-stu-id="65462-151">Change user sign-in</span></span>
<span data-ttu-id="65462-152">Deze optie kunt u toochange van wachtwoord sync toofederation of Hallo andersom.</span><span class="sxs-lookup"><span data-stu-id="65462-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="65462-153">U niet te wijzigen**niet configureert**.</span><span class="sxs-lookup"><span data-stu-id="65462-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="65462-154">Zie voor meer informatie over deze optie [gebruikersaanmelding](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="65462-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65462-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65462-155">Next steps</span></span>
* <span data-ttu-id="65462-156">Meer informatie over Hallo configuratiemodel gebruikt door Azure AD Connect-synchronisatie in [Understanding declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="65462-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="65462-157">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="65462-157">**Overview topics**</span></span>

* [<span data-ttu-id="65462-158">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="65462-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="65462-159">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65462-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
