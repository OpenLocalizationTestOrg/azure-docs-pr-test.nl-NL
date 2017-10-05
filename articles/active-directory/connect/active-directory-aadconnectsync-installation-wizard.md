---
title: Wizard opnieuw uitvoeren van de Azure AD Connect installeren | Microsoft Docs
description: Wordt uitgelegd hoe de installatiewizard werkt de tweede keer dat u deze uitvoert.
keywords: De Azure AD Connect-installatiewizard kunt u de tweede keer dat u het uitvoeren van onderhoudsinstellingen configureren
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
ms.openlocfilehash: 42855b785c0ab334e33a622c8db912ce2438c627
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-running-the-installation-wizard-a-second-time"></a><span data-ttu-id="30e09-104">Azure AD Connect-synchronisatie: uitvoeren van de installatiewizard van een tweede keer</span><span class="sxs-lookup"><span data-stu-id="30e09-104">Azure AD Connect sync: Running the installation wizard a second time</span></span>
<span data-ttu-id="30e09-105">De eerste keer dat u de wizard Azure AD Connect-installatie uitvoert begeleidt het u bij het configureren van uw installatie.</span><span class="sxs-lookup"><span data-stu-id="30e09-105">The first time you run the Azure AD Connect installation wizard, it walks you through how to configure your installation.</span></span> <span data-ttu-id="30e09-106">Als u de installatiewizard opnieuw uitvoert, biedt opties voor onderhoud.</span><span class="sxs-lookup"><span data-stu-id="30e09-106">If you run the installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="30e09-107">U kunt de installatiewizard vinden in het startmenu met de naam **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="30e09-107">You can find the installation wizard in the start menu named **Azure AD Connect**.</span></span>

![Het menu Start](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="30e09-109">Wanneer u de installatiewizard te starten, ziet u een pagina met deze opties:</span><span class="sxs-lookup"><span data-stu-id="30e09-109">When you start the installation wizard, you see a page with these options:</span></span>

![Pagina met een lijst van extra taken](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="30e09-111">Als u AD FS hebt geïnstalleerd met Azure AD Connect, hebt u nog meer opties.</span><span class="sxs-lookup"><span data-stu-id="30e09-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="30e09-112">De aanvullende opties die u hebt voor AD FS zijn gedocumenteerd in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="30e09-112">The additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="30e09-113">Selecteer een van de taken en klik op **volgende** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="30e09-113">Select one of the tasks and click **Next** to continue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30e09-114">Terwijl u de installatiewizard open zijn, worden alle bewerkingen in de synchronisatie-engine onderbroken.</span><span class="sxs-lookup"><span data-stu-id="30e09-114">While you have the installation wizard open, all operations in the sync engine are suspended.</span></span> <span data-ttu-id="30e09-115">Zorg ervoor dat u de installatiewizard sluiten als u uw wijzigingen in de configuratie hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="30e09-115">Make sure you close the installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="30e09-116">De huidige configuratie weergeven</span><span class="sxs-lookup"><span data-stu-id="30e09-116">View current configuration</span></span>
<span data-ttu-id="30e09-117">Deze optie biedt een overzicht van de momenteel geconfigureerde opties.</span><span class="sxs-lookup"><span data-stu-id="30e09-117">This option gives you a quick view of your currently configured options.</span></span>

![Pagina met een lijst met alle opties en hun status](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="30e09-119">Klik op **vorige** om terug te gaan.</span><span class="sxs-lookup"><span data-stu-id="30e09-119">Click **Previous** to go back.</span></span> <span data-ttu-id="30e09-120">Als u selecteert **afsluiten**, u de installatiewizard sluit.</span><span class="sxs-lookup"><span data-stu-id="30e09-120">If you select **Exit**, you close the installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="30e09-121">Opties voor synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="30e09-121">Customize synchronization options</span></span>
<span data-ttu-id="30e09-122">Deze optie wordt gebruikt om de configuratie van de synchronisatie te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="30e09-122">This option is used to make changes to the sync configuration.</span></span> <span data-ttu-id="30e09-123">Er is een subset van de opties in het installatiepad van aangepaste configuratie.</span><span class="sxs-lookup"><span data-stu-id="30e09-123">You see a subset of options from the custom configuration installation path.</span></span> <span data-ttu-id="30e09-124">U ziet deze optie ook als u snelle installatie in eerste instantie worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="30e09-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="30e09-125">[Toevoegen van meer mappen](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="30e09-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="30e09-126">Zie voor het verwijderen van een map [verwijderen van een Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="30e09-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="30e09-127">[Wijzigen van domein en OE filteren](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="30e09-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="30e09-128">Filteren van de groep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="30e09-128">Remove Group filtering.</span></span>
* <span data-ttu-id="30e09-129">[Optionele functies wijzigen](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="30e09-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="30e09-130">De overige opties uit de eerste installatie kunnen niet worden gewijzigd en zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="30e09-130">The other options from the initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="30e09-131">Deze opties zijn:</span><span class="sxs-lookup"><span data-stu-id="30e09-131">These options are:</span></span>

* <span data-ttu-id="30e09-132">Het kenmerk moet worden gebruikt voor userPrincipalName en sourceAnchor wijzigen.</span><span class="sxs-lookup"><span data-stu-id="30e09-132">Change the attribute to use for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="30e09-133">Wijzig de gekoppelde methode voor objecten van ander forest.</span><span class="sxs-lookup"><span data-stu-id="30e09-133">Change the joining method for objects from different forest.</span></span>
* <span data-ttu-id="30e09-134">Filteren op basis van een groep inschakelen.</span><span class="sxs-lookup"><span data-stu-id="30e09-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="30e09-135">Directory-schema vernieuwen</span><span class="sxs-lookup"><span data-stu-id="30e09-135">Refresh directory schema</span></span>
<span data-ttu-id="30e09-136">Deze optie wordt gebruikt als u het schema hebt gewijzigd in een van uw on-premises AD DS-forests.</span><span class="sxs-lookup"><span data-stu-id="30e09-136">This option is used if you have changed the schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="30e09-137">Bijvoorbeeld, u mogelijk Exchange geïnstalleerd of bijgewerkt naar een Windows Server 2012-schema met apparaatobjecten.</span><span class="sxs-lookup"><span data-stu-id="30e09-137">For example, you might have installed Exchange or upgraded to a Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="30e09-138">In dit geval moet u instrueren Azure AD Connect opnieuw lezen van het schema van AD DS en bijwerken van de cache.</span><span class="sxs-lookup"><span data-stu-id="30e09-138">In this case, you need to instruct Azure AD Connect to read the schema again from AD DS and update its cache.</span></span> <span data-ttu-id="30e09-139">Deze actie wordt ook de synchronisatie-regels opnieuw gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="30e09-139">This action also regenerates the Sync Rules.</span></span> <span data-ttu-id="30e09-140">Als u de Exchange-schema als voorbeeld toevoegt, wordt de synchronisatie-regels voor Exchange worden toegevoegd aan de configuratie.</span><span class="sxs-lookup"><span data-stu-id="30e09-140">If you add the Exchange schema, as an example, the Sync Rules for Exchange are added to the configuration.</span></span>

<span data-ttu-id="30e09-141">Wanneer u deze optie selecteert, worden de mappen in uw configuratie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="30e09-141">When you select this option, all the directories in your configuration are listed.</span></span> <span data-ttu-id="30e09-142">U kunt de standaardinstelling behouden en Vernieuw alle forests of selectie enkele ervan.</span><span class="sxs-lookup"><span data-stu-id="30e09-142">You can keep the default setting and refresh all forests or unselect some of them.</span></span>

![Pagina met een lijst met alle mappen in de omgeving](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="30e09-144">Faseringsmodus configureren</span><span class="sxs-lookup"><span data-stu-id="30e09-144">Configure staging mode</span></span>
<span data-ttu-id="30e09-145">Deze optie kunt u inschakelen en uitschakelen van de faseringsmodus op de server.</span><span class="sxs-lookup"><span data-stu-id="30e09-145">This option allows you to enable and disable staging mode on the server.</span></span> <span data-ttu-id="30e09-146">Meer informatie over modus en hoe deze wordt gebruikt voor gefaseerde installatie vindt u in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="30e09-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="30e09-147">De optie ziet als tijdelijke momenteel is ingeschakeld of uitgeschakeld:</span><span class="sxs-lookup"><span data-stu-id="30e09-147">The option shows if staging is currently enabled or disabled:</span></span>  
![Optie dat ook de huidige status van de faseringsmodus wordt weergegeven](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="30e09-149">Selecteer deze optie om de status wijzigt, en selecteer of schakel het selectievakje uit.</span><span class="sxs-lookup"><span data-stu-id="30e09-149">To change the state, select this option and select or unselect the checkbox.</span></span>  
![Optie dat ook de huidige status van de faseringsmodus wordt weergegeven](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="30e09-151">Gebruikersaanmelding wijzigen</span><span class="sxs-lookup"><span data-stu-id="30e09-151">Change user sign-in</span></span>
<span data-ttu-id="30e09-152">Deze optie kunt u wijzigen van Wachtwoordsynchronisatie in Federatie of andersom.</span><span class="sxs-lookup"><span data-stu-id="30e09-152">This option allows you to change from password sync to federation or the other way around.</span></span> <span data-ttu-id="30e09-153">U kunt niet wijzigen naar **niet configureert**.</span><span class="sxs-lookup"><span data-stu-id="30e09-153">You cannot change to **do not configure**.</span></span>

<span data-ttu-id="30e09-154">Zie voor meer informatie over deze optie [gebruikersaanmelding](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="30e09-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="30e09-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="30e09-155">Next steps</span></span>
* <span data-ttu-id="30e09-156">Meer informatie over de configuratiemodel dat wordt gebruikt door Azure AD Connect-synchronisatie in [Understanding declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="30e09-156">Learn more about the configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="30e09-157">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="30e09-157">**Overview topics**</span></span>

* [<span data-ttu-id="30e09-158">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="30e09-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="30e09-159">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30e09-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
