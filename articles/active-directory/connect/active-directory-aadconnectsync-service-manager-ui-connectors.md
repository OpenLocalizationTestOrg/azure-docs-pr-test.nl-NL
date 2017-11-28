---
title: aaaConnectors in hello Azure AD Synchronization Service Manager UI | Microsoft-Docs
description: Hallo Connectors tabblad in Hallo Synchronization Service Manager begrijpen voor Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="9fb6e-103">Met behulp van connectors met hello Azure AD Connect Sync-Service Manager</span><span class="sxs-lookup"><span data-stu-id="9fb6e-103">Using connectors with hello Azure AD Connect Sync Service Manager</span></span>

![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="9fb6e-105">Hallo Connectors tabblad is gebruikte toomanage alle systemen Hallo synchronisatie-engine is verbonden met.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-105">hello Connectors tab is used toomanage all systems hello sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="9fb6e-106">Connector-acties</span><span class="sxs-lookup"><span data-stu-id="9fb6e-106">Connector actions</span></span>
| <span data-ttu-id="9fb6e-107">Actie</span><span class="sxs-lookup"><span data-stu-id="9fb6e-107">Action</span></span> | <span data-ttu-id="9fb6e-108">Opmerking</span><span class="sxs-lookup"><span data-stu-id="9fb6e-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="9fb6e-109">Maken</span><span class="sxs-lookup"><span data-stu-id="9fb6e-109">Create</span></span> |<span data-ttu-id="9fb6e-110">Gebruik geen.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-110">Do not use.</span></span> <span data-ttu-id="9fb6e-111">Gebruik de wizard Hallo voor het verbinden van tooadditional AD-forests.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-111">For connecting tooadditional AD forests, use hello installation wizard.</span></span> |
| <span data-ttu-id="9fb6e-112">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="9fb6e-112">Properties</span></span> |<span data-ttu-id="9fb6e-113">Gebruikt voor het domein en OE filteren.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="9fb6e-114">Verwijderen</span><span class="sxs-lookup"><span data-stu-id="9fb6e-114">Delete</span></span>](#delete) |<span data-ttu-id="9fb6e-115">Gebruikte tooeither Hallo-gegevens in Hallo connector ruimte of toodelete verbinding forest tooa verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-115">Used tooeither delete hello data in hello connector space or toodelete connection tooa forest.</span></span> |
| [<span data-ttu-id="9fb6e-116">Profielen uitvoeren configureren</span><span class="sxs-lookup"><span data-stu-id="9fb6e-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="9fb6e-117">Met uitzondering van domein filteren, niets tooconfigure hier.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-117">Except for domain filtering, nothing tooconfigure here.</span></span> <span data-ttu-id="9fb6e-118">U kunt deze actie uitvoeringsprofielen toosee al is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-118">You can use this action toosee already configured run profiles.</span></span> |
| <span data-ttu-id="9fb6e-119">Voer</span><span class="sxs-lookup"><span data-stu-id="9fb6e-119">Run</span></span> |<span data-ttu-id="9fb6e-120">Een ad-hoc uitvoeren van een profiel toostart gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-120">Used toostart a one-off run of a profile.</span></span> |
| <span data-ttu-id="9fb6e-121">Stoppen</span><span class="sxs-lookup"><span data-stu-id="9fb6e-121">Stop</span></span> |<span data-ttu-id="9fb6e-122">Een Connector die momenteel wordt uitgevoerd een profiel stopt.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="9fb6e-123">Exporteren van de Connector</span><span class="sxs-lookup"><span data-stu-id="9fb6e-123">Export Connector</span></span> |<span data-ttu-id="9fb6e-124">Gebruik geen.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-124">Do not use.</span></span> |
| <span data-ttu-id="9fb6e-125">Connector importeren</span><span class="sxs-lookup"><span data-stu-id="9fb6e-125">Import Connector</span></span> |<span data-ttu-id="9fb6e-126">Gebruik geen.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-126">Do not use.</span></span> |
| <span data-ttu-id="9fb6e-127">Update-Connector</span><span class="sxs-lookup"><span data-stu-id="9fb6e-127">Update Connector</span></span> |<span data-ttu-id="9fb6e-128">Gebruik geen.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-128">Do not use.</span></span> |
| <span data-ttu-id="9fb6e-129">Schema vernieuwen</span><span class="sxs-lookup"><span data-stu-id="9fb6e-129">Refresh Schema</span></span> |<span data-ttu-id="9fb6e-130">In de cache schema Hallo vernieuwt.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-130">Refreshes hello cached schema.</span></span> <span data-ttu-id="9fb6e-131">Het is aanbevolen toouse Hallo optie in de installatiewizard Hallo in plaats daarvan sinds die updates ook regels synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-131">It is preferred toouse hello option in hello installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="9fb6e-132">Connectorgebied zoeken</span><span class="sxs-lookup"><span data-stu-id="9fb6e-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="9fb6e-133">Gebruikte toofind objecten en te[volgen op een object en de gegevens via Hallo systeem](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="9fb6e-133">Used toofind objects and too[Follow an object and its data through hello system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="9fb6e-134">Verwijderen</span><span class="sxs-lookup"><span data-stu-id="9fb6e-134">Delete</span></span>
<span data-ttu-id="9fb6e-135">Hallo verwijderingsactie wordt gebruikt voor twee verschillende dingen.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-135">hello delete action is used for two different things.</span></span>  
![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="9fb6e-137">Hallo optie **alleen connectorruimte verwijderen** Hiermee verwijdert u alle gegevens, maar houd Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-137">hello option **Delete connector space only** removes all data, but keep hello configuration.</span></span>

<span data-ttu-id="9fb6e-138">Hallo optie **Connector verwijderen en connector ruimte** Hallo gegevens en configuratie van de Hallo verwijdert.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-138">hello option **Delete Connector and connector space** removes hello data and hello configuration.</span></span> <span data-ttu-id="9fb6e-139">Deze optie wordt gebruikt wanneer u niet dat tooconnect tooa forest niet meer wilt.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-139">This option is used when you do not want tooconnect tooa forest anymore.</span></span>

<span data-ttu-id="9fb6e-140">Beide opties alle objecten synchroniseren en Hallo metaverse objecten bijwerken.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-140">Both options sync all objects and update hello metaverse objects.</span></span> <span data-ttu-id="9fb6e-141">Deze actie is een langdurige bewerking.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="9fb6e-142">Profielen uitvoeren configureren</span><span class="sxs-lookup"><span data-stu-id="9fb6e-142">Configure Run Profiles</span></span>
<span data-ttu-id="9fb6e-143">Deze optie kunt u toosee hello uitvoeringsprofielen geconfigureerd voor een Connector.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-143">This option allows you toosee hello run profiles configured for a Connector.</span></span>

![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="9fb6e-145">Connectorgebied zoeken</span><span class="sxs-lookup"><span data-stu-id="9fb6e-145">Search Connector Space</span></span>
<span data-ttu-id="9fb6e-146">connector Hallo-ruimte zoekactie is nuttig toofind objecten en gegevensproblemen oplossen.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-146">hello search connector space action is useful toofind objects and troubleshoot data issues.</span></span>

![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="9fb6e-148">Begin met het selecteren een **bereik**.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="9fb6e-149">U kunt zoeken op basis van gegevens (RDN, DN-naam, anker substructuur), of de status van Hallo-object (voor alle opties).</span><span class="sxs-lookup"><span data-stu-id="9fb6e-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of hello object (all other options).</span></span>  
<span data-ttu-id="9fb6e-150">![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="9fb6e-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="9fb6e-151">Als u bijvoorbeeld substructuur zoeken wilt, krijgt u alle objecten in een organisatie-eenheid.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="9fb6e-152">![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="9fb6e-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="9fb6e-153">Vanaf dit raster kunt u een object selecteert, selecteert u **eigenschappen**, en [hieraan](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) van Hallo bron connectorgebied overgebracht via het Hallo-metaverse en toohello doel connectorgebied overgebracht.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from hello source connector space, through hello metaverse, and toohello target connector space.</span></span>

### <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="9fb6e-154">Hallo AD DS accountwachtwoord wijzigen</span><span class="sxs-lookup"><span data-stu-id="9fb6e-154">Changing hello AD DS account password</span></span>
<span data-ttu-id="9fb6e-155">Als u het accountwachtwoord Hallo wijzigt, Hallo-synchronisatieservice niet langer kunnen tooimport/exporteren wijzigingen tooon lokale AD.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-155">If you change hello account password, hello Synchronization Service will no longer be able tooimport/export changes tooon-premises AD.</span></span>   <span data-ttu-id="9fb6e-156">Hallo volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9fb6e-156">You may see hello following:</span></span>

- <span data-ttu-id="9fb6e-157">Hallo voor importeren/exporteren stap voor AD-connector Hallo mislukt met fout 'geen start referenties'.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-157">hello import/export step for hello AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="9fb6e-158">Onder de functie Logboeken van Windows bevat hello logboek voor toepassingsgebeurtenissen een fout met 6000 van gebeurtenis-ID en het bericht "hello management agent 'contoso.com' kan niet toorun omdat Hallo referenties ongeldig zijn."</span><span class="sxs-lookup"><span data-stu-id="9fb6e-158">Under Windows Event Viewer, hello application event log contains an error with Event ID 6000 and message “hello management agent “contoso.com” failed toorun because hello credentials were invalid.”</span></span>

<span data-ttu-id="9fb6e-159">tooresolve hello uitgeeft, update gebruikersaccount in AD DS Hallo Hallo volgende met:</span><span class="sxs-lookup"><span data-stu-id="9fb6e-159">tooresolve hello issue, update hello AD DS user account using hello following:</span></span>


1. <span data-ttu-id="9fb6e-160">Hallo Synchronization Service Manager (START → Synchronization Service) starten.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-160">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="9fb6e-161">![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="9fb6e-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="9fb6e-162">Ga toohello **Connectors** tabblad.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-162">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="9fb6e-163">Selecteer Hallo AD-Connector die geconfigureerde toouse Hallo AD DS-account.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-163">Select hello AD Connector which is configured toouse hello AD DS account.</span></span>
4. <span data-ttu-id="9fb6e-164">Selecteer onder acties **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="9fb6e-165">Selecteer in het pop-upvenster hello, Connect tooActive Directory-Forest:</span><span class="sxs-lookup"><span data-stu-id="9fb6e-165">In hello pop-up dialog, select Connect tooActive Directory Forest:</span></span>
6. <span data-ttu-id="9fb6e-166">Hallo-forestnaam geeft Hallo bijbehorende on-premises AD.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-166">hello Forest name indicates hello corresponding on-prem AD.</span></span>
7. <span data-ttu-id="9fb6e-167">Hallo-gebruikersnaam geeft Hallo AD DS-account voor synchronisatie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-167">hello User name indicates hello AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="9fb6e-168">Geef de nieuwe wachtwoord Hallo Hallo AD DS-account in Hallo wachtwoordtekstvak ![Azure AD Connect-synchronisatie versleuteling sleutel hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="9fb6e-168">Enter hello new password of hello AD DS account in hello Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="9fb6e-169">Klik op OK toosave Hallo nieuwe wachtwoord en start opnieuw Hallo synchronisatieservice tooremove Hallo oude wachtwoord uit cachegeheugen.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-169">Click OK toosave hello new password and restart hello Synchronization Service tooremove hello old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="9fb6e-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9fb6e-170">Next steps</span></span>
<span data-ttu-id="9fb6e-171">Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.</span><span class="sxs-lookup"><span data-stu-id="9fb6e-171">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="9fb6e-172">Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9fb6e-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
