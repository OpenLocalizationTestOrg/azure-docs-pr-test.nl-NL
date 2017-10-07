---
title: Systeem voor het identiteitsbeheer tussen domeinen aaaUsing automatisch worden ingericht, gebruikers en groepen van Azure Active Directory-tooapplications | Microsoft Docs
description: Azure Active Directory kunnen automatisch worden ingericht, gebruikers en groepen tooany toepassing of identiteit store, die door een webservice is fronted met Hallo interface is gedefinieerd in Hallo SCIM protocol specification
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a><span data-ttu-id="5e19d-103">Met behulp van systeem voor identiteitsbeheer van verschillende domeinen tooautomatically inrichten gebruikers en groepen van Azure Active Directory-tooapplications</span><span class="sxs-lookup"><span data-stu-id="5e19d-103">Using System for Cross-Domain Identity Management tooautomatically provision users and groups from Azure Active Directory tooapplications</span></span>

## <a name="overview"></a><span data-ttu-id="5e19d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5e19d-104">Overview</span></span>
<span data-ttu-id="5e19d-105">Azure Active Directory (Azure AD) kunnen automatisch worden ingericht, gebruikers en groepen tooany toepassing of identiteit store, die door een webservice met gedefinieerd in Hallo Hallo-interface is fronted [systeem voor verschillende domeinen Identity Management (SCIM) 2.0 Protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="5e19d-105">Azure Active Directory (Azure AD) can automatically provision users and groups tooany application or identity store that is fronted by a web service with hello interface defined in hello [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="5e19d-106">Azure Active Directory kunt verzenden aanvragen toocreate, wijzigen of verwijderen van toegewezen gebruikers en groepen toohello webservice.</span><span class="sxs-lookup"><span data-stu-id="5e19d-106">Azure Active Directory can send requests toocreate, modify, or delete assigned users and groups toohello web service.</span></span> <span data-ttu-id="5e19d-107">Hallo-webservice kan vervolgens deze aanvragen worden omgezet in bewerkingen op Hallo doel identiteit store.</span><span class="sxs-lookup"><span data-stu-id="5e19d-107">hello web service can then translate those requests into operations on hello target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="5e19d-108">Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="5e19d-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="5e19d-109">![][0]
*Afbeelding 1: Inrichting van Azure Active Directory tooan identiteit store via een webservice*</span><span class="sxs-lookup"><span data-stu-id="5e19d-109">![][0]
*Figure 1: Provisioning from Azure Active Directory tooan identity store via a web service*</span></span>

<span data-ttu-id="5e19d-110">Deze mogelijkheid kan worden gebruikt in combinatie met 'bring your own app' Hallo-functionaliteit in Azure AD tooenable eenmalige aanmelding en automatisch gebruikers inrichten voor toepassingen die op of door een webservice SCIM zijn fronted.</span><span class="sxs-lookup"><span data-stu-id="5e19d-110">This capability can be used in conjunction with hello “bring your own app” capability in Azure AD tooenable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="5e19d-111">Er zijn twee gebruiksvoorbeelden voor using SCIM in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="5e19d-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="5e19d-112">**Inrichting van gebruikers en groepen tooapplications die ondersteuning bieden voor SCIM** toepassingen die ondersteuning bieden voor SCIM 2.0 en bearer-tokens van OAuth gebruiken voor verificatie met Azure AD zonder configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="5e19d-112">**Provisioning users and groups tooapplications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="5e19d-113">**Maak uw eigen inrichting oplossing voor toepassingen die ondersteuning bieden voor andere inrichting op basis van een API** voor niet-SCIM toepassingen, kunt u een SCIM eindpunt tootranslate tussen hello Azure AD SCIM eindpunt en elke API Hallo toepassing ondersteunt maken voor gebruikers inrichten.</span><span class="sxs-lookup"><span data-stu-id="5e19d-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint tootranslate between hello Azure AD SCIM endpoint and any API hello application supports for user provisioning.</span></span> <span data-ttu-id="5e19d-114">toohelp u een eindpunt SCIM ontwikkelen, bieden we Common Language Infrastructure (CLI)-bibliotheken en codevoorbeelden waarin wordt uitgelegd hoe toodo bieden een eindpunt SCIM en SCIM berichten vertalen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-114">toohelp you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how toodo provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a><span data-ttu-id="5e19d-115">Gebruikers en groepen tooapplications die ondersteuning bieden voor SCIM inrichten</span><span class="sxs-lookup"><span data-stu-id="5e19d-115">Provisioning users and groups tooapplications that support SCIM</span></span>
<span data-ttu-id="5e19d-116">Azure AD kan worden geconfigureerd tooautomatically inrichten toegewezen gebruikers en groepen tooapplications die implementeren een [systeem voor verschillende domeinen Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) webservice en accepteren OAuth bearer-tokens voor authenticatie .</span><span class="sxs-lookup"><span data-stu-id="5e19d-116">Azure AD can be configured tooautomatically provision assigned users and groups tooapplications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="5e19d-117">Toepassingen moeten voldoen aan deze vereisten binnen Hallo SCIM 2.0-specificatie:</span><span class="sxs-lookup"><span data-stu-id="5e19d-117">Within hello SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="5e19d-118">Ondersteunt het maken van gebruikers en/of groepen aan de hand van sectie 3.3 Hallo SCIM-protocol.</span><span class="sxs-lookup"><span data-stu-id="5e19d-118">Supports creating users and/or groups, as per section 3.3 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="5e19d-119">Ondersteunt het wijzigen van gebruikers en/of groepen met patch-aanvragen aan de hand van sectie 3.5.2 Hallo SCIM-protocol.</span><span class="sxs-lookup"><span data-stu-id="5e19d-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="5e19d-120">Ondersteunt het ophalen van een bekende bron volgens punt 3.4.1 Hallo SCIM-protocol.</span><span class="sxs-lookup"><span data-stu-id="5e19d-120">Supports retrieving a known resource as per section 3.4.1 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="5e19d-121">Ondersteunt het opvragen van gebruikers en/of groepen aan de hand van sectie 3.4.2 Hallo SCIM-protocol.</span><span class="sxs-lookup"><span data-stu-id="5e19d-121">Supports querying users and/or groups, as per section 3.4.2 of hello SCIM protocol.</span></span>  <span data-ttu-id="5e19d-122">Standaard door externalId aan gebruikers gevraagd en groepen worden opgevraagd met de weergavenaam.</span><span class="sxs-lookup"><span data-stu-id="5e19d-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="5e19d-123">Ondersteunt het opvragen van de gebruiker door-ID en -beheer volgens sectie 3.4.2 Hallo SCIM-protocol.</span><span class="sxs-lookup"><span data-stu-id="5e19d-123">Supports querying user by ID and by manager as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="5e19d-124">Ondersteunt het uitvoeren van query's groepen door-ID en door een lid aan de hand van sectie 3.4.2 Hallo SCIM-protocol.</span><span class="sxs-lookup"><span data-stu-id="5e19d-124">Supports querying groups by ID and by member as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="5e19d-125">OAuth-bearer-tokens voor autorisatie volgens punt 2.1 Hallo SCIM protocol accepteert.</span><span class="sxs-lookup"><span data-stu-id="5e19d-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of hello SCIM protocol.</span></span>

<span data-ttu-id="5e19d-126">Neem contact op met uw toepassingsprovider of de documentatie van uw toepassingsprovider voor overzichten van compatibiliteit met deze vereisten.</span><span class="sxs-lookup"><span data-stu-id="5e19d-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="5e19d-127">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="5e19d-127">Getting started</span></span>
<span data-ttu-id="5e19d-128">Toepassingen die ondersteuning bieden voor Hallo SCIM profiel dat wordt beschreven in dit artikel kunnen worden verbonden tooAzure Active Directory Hallo 'niet galerie application' gebruiken in hello Azure AD-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="5e19d-128">Applications that support hello SCIM profile described in this article can be connected tooAzure Active Directory using hello "non-gallery application" feature in hello Azure AD application gallery.</span></span> <span data-ttu-id="5e19d-129">Zodra de verbonden, Azure AD wordt uitgevoerd een synchronisatieproces om de 20 minuten waar query uit te voeren van de toepassing hello SCIM eindpunt voor toegewezen gebruikers en groepen uit en maakt of wijzigt volgens toohello Toewijzingsdetails.</span><span class="sxs-lookup"><span data-stu-id="5e19d-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries hello application's SCIM endpoint for assigned users and groups, and creates or modifies them according toohello assignment details.</span></span>

<span data-ttu-id="5e19d-130">**een toepassing die ondersteuning biedt voor SCIM tooconnect:**</span><span class="sxs-lookup"><span data-stu-id="5e19d-130">**tooconnect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="5e19d-131">Aanmelden te[hello Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5e19d-131">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="5e19d-132">Te bladeren ** Azure Active Directory > zakelijke toepassingen en selecteer **nieuwe toepassing > alle > niet-galerie toepassing**.</span><span class="sxs-lookup"><span data-stu-id="5e19d-132">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="5e19d-133">Voer een naam voor uw toepassing en klik op **toevoegen** pictogram toocreate een app-object.</span><span class="sxs-lookup"><span data-stu-id="5e19d-133">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span>
    
  <span data-ttu-id="5e19d-134">![][1]
  *Afbeelding 2: Azure AD-toepassingsgalerie*</span><span class="sxs-lookup"><span data-stu-id="5e19d-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="5e19d-135">Selecteer in de resulterende welkomstscherm Hallo **inrichten** tabblad in de linkerkolom Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e19d-135">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="5e19d-136">In Hallo **modus inrichting** selecteert u **automatische**.</span><span class="sxs-lookup"><span data-stu-id="5e19d-136">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="5e19d-137">![][2]
  *Afbeelding 3: Configureren in Azure-portal Hallo inrichting*</span><span class="sxs-lookup"><span data-stu-id="5e19d-137">![][2]
*Figure 3: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="5e19d-138">In Hallo **Tenant-URL** Voer Hallo-URL van de van toepassing hello SCIM eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5e19d-138">In hello **Tenant URL** field, enter hello URL of hello application's SCIM endpoint.</span></span> <span data-ttu-id="5e19d-139">Voorbeeld: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="5e19d-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="5e19d-140">Als Hallo SCIM eindpunt een OAuth bearer-token van een verlener dan Azure AD vereist, wordt de kopie Hallo OAuth bearer-token in Hallo optionele vereist **geheim Token** veld.</span><span class="sxs-lookup"><span data-stu-id="5e19d-140">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="5e19d-141">Als dit veld leeg blijft, opgenomen een OAuth-bearer-token uitgegeven vanuit Azure AD bij elke aanvraag met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e19d-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="5e19d-142">Apps die gebruikmaken van Azure AD als een id-provider kunt controleren of deze Azure AD-verleend token.</span><span class="sxs-lookup"><span data-stu-id="5e19d-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="5e19d-143">Klik op Hallo **testverbinding** knop toohave Azure Active Directory poging tooconnect toohello SCIM eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5e19d-143">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="5e19d-144">Als Hallo pogingen mislukken, wordt informatie over de fout wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5e19d-144">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="5e19d-145">Als Hallo pogingen tooconnect toohello toepassing slaagt, klikt u op **opslaan** toosave Hallo beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="5e19d-145">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="5e19d-146">In Hallo **toewijzingen** sectie, zijn er twee sets van selecteerbare Kenmerktoewijzingen: één voor gebruikersobjecten en één voor groepsobjecten.</span><span class="sxs-lookup"><span data-stu-id="5e19d-146">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="5e19d-147">Selecteer elke één tooreview Hallo kenmerken die worden gesynchroniseerd vanuit Azure Active Directory tooyour app.</span><span class="sxs-lookup"><span data-stu-id="5e19d-147">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="5e19d-148">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikers en groepen in uw app voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-148">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="5e19d-149">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-149">Select hello Save button toocommit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="5e19d-150">U kunt desgewenst uitschakelen door Hallo 'groepen' toewijzing uit te schakelen van een groepsobjecten worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="5e19d-150">You can optionally disable syncing of group objects by disabling hello "groups" mapping.</span></span> 

11. <span data-ttu-id="5e19d-151">Onder **instellingen**, Hallo **bereik** veld wordt gedefinieerd welke gebruikers en groepen worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="5e19d-151">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="5e19d-152">Alleen selecteren 'Sync alleen toegewezen gebruikers en groepen' (aanbevolen) worden gesynchroniseerd gebruikers en groepen die zijn toegewezen in Hallo **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="5e19d-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="5e19d-153">Zodra de configuratie voltooid is, verandert Hallo **inrichting Status** te**op**.</span><span class="sxs-lookup"><span data-stu-id="5e19d-153">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="5e19d-154">Klik op **opslaan** toostart Hallo inrichting Azure AD-service.</span><span class="sxs-lookup"><span data-stu-id="5e19d-154">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="5e19d-155">Als alleen synchroniseren toegewezen gebruikers en groepen (aanbevolen), moet u ervoor tooselect Hallo **gebruikers en groepen** tabblad en Hallo-gebruikers en/of groepen die u wenst dat toosync toewijzen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-155">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="5e19d-156">Nadat de initiële synchronisatie Hallo is gestart, kunt u Hallo **controlelogboeken** tabblad toomonitor voortgang, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="5e19d-156">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="5e19d-157">Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="5e19d-157">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="5e19d-158">de initiële synchronisatie Hallo duurt langer tooperform dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden, zolang het Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5e19d-158">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="5e19d-159">Uw eigen oplossing voor elke toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="5e19d-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="5e19d-160">Als u een SCIM-webservice die is gekoppeld met Azure Active Directory maakt, kunt u één gebruiker voor eenmalige aanmelding en automatische inrichting voor vrijwel elke toepassing die voorziet in een API-inrichting REST of SOAP-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5e19d-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="5e19d-161">Hier ziet u hoe het werkt:</span><span class="sxs-lookup"><span data-stu-id="5e19d-161">Here’s how it works:</span></span>

1. <span data-ttu-id="5e19d-162">Azure AD levert een algemene language infrastructure-bibliotheek met de naam [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="5e19d-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="5e19d-163">Systeemintegrators en ontwikkelaars kunnen gebruiken van deze bibliotheek toocreate en een SCIM gebaseerde webservice-eindpunt kan verbinding maken met Azure AD tooany toepassing identiteit store implementeren.</span><span class="sxs-lookup"><span data-stu-id="5e19d-163">System integrators and developers can use this library toocreate and deploy a SCIM-based web service endpoint capable of connecting Azure AD tooany application’s identity store.</span></span>
2. <span data-ttu-id="5e19d-164">Toewijzingen worden geïmplementeerd in Hallo web service toomap Hallo gestandaardiseerde gebruiker schema toohello gebruikersschema en vereist voor de toepassing hello-protocol.</span><span class="sxs-lookup"><span data-stu-id="5e19d-164">Mappings are implemented in hello web service toomap hello standardized user schema toohello user schema and protocol required by hello application.</span></span>
3. <span data-ttu-id="5e19d-165">Hallo eindpunt-URL is geregistreerd in Azure AD als onderdeel van een aangepaste toepassing in Hallo-toepassingsgalerie.</span><span class="sxs-lookup"><span data-stu-id="5e19d-165">hello endpoint URL is registered in Azure AD as part of a custom application in hello application gallery.</span></span>
4. <span data-ttu-id="5e19d-166">Gebruikers en groepen zijn toegewezen toothis toepassing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e19d-166">Users and groups are assigned toothis application in Azure AD.</span></span> <span data-ttu-id="5e19d-167">Bij toewijzing, worden ze in een wachtrij toobe gesynchroniseerd toohello-doeltoepassing geplaatst.</span><span class="sxs-lookup"><span data-stu-id="5e19d-167">Upon assignment, they are put into a queue toobe synchronized toohello target application.</span></span> <span data-ttu-id="5e19d-168">synchronisatieproces Hallo Hallo wachtrij verwerking wordt uitgevoerd om de 20 minuten.</span><span class="sxs-lookup"><span data-stu-id="5e19d-168">hello synchronization process handling hello queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="5e19d-169">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="5e19d-169">Code Samples</span></span>
<span data-ttu-id="5e19d-170">toomake dit verwerken eenvoudiger, een reeks [codevoorbeelden](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) zijn opgegeven die een SCIM webservice-eindpunt maken en Demonstreer automatische inrichting.</span><span class="sxs-lookup"><span data-stu-id="5e19d-170">toomake this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="5e19d-171">Een voorbeeld is van een provider die wordt onderhouden door een bestand met de rijen met door komma's gescheiden waarden die gebruikers en groepen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="5e19d-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="5e19d-172">Hallo andere is van een provider die wordt toegepast op Hallo Amazon Web Services Identity and Access Management-service.</span><span class="sxs-lookup"><span data-stu-id="5e19d-172">hello other is of a provider that operates on hello Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="5e19d-173">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="5e19d-173">**Prerequisites**</span></span>

* <span data-ttu-id="5e19d-174">Visual Studio 2013 of hoger</span><span class="sxs-lookup"><span data-stu-id="5e19d-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="5e19d-175">Azure-SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="5e19d-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="5e19d-176">Windows-machine die ondersteuning biedt voor Hallo ASP.NET framework 4.5 toobe gebruikt als Hallo SCIM eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5e19d-176">Windows machine that supports hello ASP.NET framework 4.5 toobe used as hello SCIM endpoint.</span></span> <span data-ttu-id="5e19d-177">Deze machine moet toegankelijk zijn vanuit de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="5e19d-177">This machine must be accessible from hello cloud</span></span>
* [<span data-ttu-id="5e19d-178">Een Azure-abonnement met een proefabonnement of een gelicentieerde versie van Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="5e19d-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="5e19d-179">Hallo Amazon AWS voorbeeld vereist bibliotheken van Hallo [AWS-Toolkit voor Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="5e19d-179">hello Amazon AWS sample requires libraries from hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="5e19d-180">Zie voor meer informatie, Hallo Leesmij bestand wordt geleverd met Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5e19d-180">For more information, see hello README file included with hello sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="5e19d-181">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="5e19d-181">Getting Started</span></span>
<span data-ttu-id="5e19d-182">Hallo gemakkelijkste manier tooimplement een SCIM-eindpunt dat kan worden geaccepteerd inrichten van Azure AD-aanvragen is toobuild en implementeert u Hallo voorbeeldcode die Hallo ingerichte gebruikers tooa door komma's gescheiden waarden (CSV)-bestand.</span><span class="sxs-lookup"><span data-stu-id="5e19d-182">hello easiest way tooimplement a SCIM endpoint that can accept provisioning requests from Azure AD is toobuild and deploy hello code sample that outputs hello provisioned users tooa comma-separated value (CSV) file.</span></span>

<span data-ttu-id="5e19d-183">**een voorbeeld SCIM eindpunt toocreate:**</span><span class="sxs-lookup"><span data-stu-id="5e19d-183">**toocreate a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="5e19d-184">Het downloadpakket Hallo code voorbeeld op [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="5e19d-184">Download hello code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="5e19d-185">Pak Hallo pakket en plaats het op uw Windows-machine op een locatie zoals C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="5e19d-185">Unzip hello package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="5e19d-186">In deze map starten Hallo FileProvisioningAgent oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5e19d-186">In this folder, launch hello FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="5e19d-187">Selecteer **Extra > Library Package Manager > Package Manager Console**, en na-opdrachten voor Hallo FileProvisioningAgent tooresolve Hallo oplossing projectverwijzingen Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5e19d-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute hello following commands for hello FileProvisioningAgent project tooresolve hello solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="5e19d-188">Hallo FileProvisioningAgent project bouwen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-188">Build hello FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="5e19d-189">Hallo opdrachtprompt toepassing in Windows (als Administrator) starten en gebruiken van Hallo **cd** opdracht toochange Hallo directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** map.</span><span class="sxs-lookup"><span data-stu-id="5e19d-189">Launch hello Command Prompt application in Windows (as an Administrator), and use hello **cd** command toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="5e19d-190">Hallo de volgende opdracht, waarbij < ip-adres > vervangt door Hallo IP-adres of domeinnaam naam van de Windows-computer Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5e19d-190">Run hello following command, replacing <ip-address> with hello IP address or domain name of hello Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="5e19d-191">In Windows onder **Windows-instellingen > netwerk- en instellingen voor Internet**, selecteer Hallo **Windows Firewall > instellingen voor geavanceerde**, en maak een **regel voor binnenkomende verbindingen** die kan de binnenkomende toegang tooport 9000.</span><span class="sxs-lookup"><span data-stu-id="5e19d-191">In Windows under **Windows Settings > Network & Internet Settings**, select hello **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access tooport 9000.</span></span>
9. <span data-ttu-id="5e19d-192">Als Windows-machine Hallo zich achter een router, Hallo router behoeften toobe geconfigureerd tooperform Network Access Translation tussen de poort 9000 die blootgestelde toohello internet en poort 9000 op Hallo Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="5e19d-192">If hello Windows machine is behind a router, hello router needs toobe configured tooperform Network Access Translation between its port 9000 that is exposed toohello internet, and port 9000 on hello Windows machine.</span></span> <span data-ttu-id="5e19d-193">Dit is vereist voor Azure AD toobe kunnen tooaccess dit eindpunt in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="5e19d-193">This is required for Azure AD toobe able tooaccess this endpoint in hello cloud.</span></span>

<span data-ttu-id="5e19d-194">**tooregister hello voorbeeld SCIM eindpunt in Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="5e19d-194">**tooregister hello sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="5e19d-195">Aanmelden te[hello Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5e19d-195">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="5e19d-196">Te bladeren ** Azure Active Directory > zakelijke toepassingen en selecteer **nieuwe toepassing > alle > niet-galerie toepassing**.</span><span class="sxs-lookup"><span data-stu-id="5e19d-196">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="5e19d-197">Voer een naam voor uw toepassing en klik op **toevoegen** pictogram toocreate een app-object.</span><span class="sxs-lookup"><span data-stu-id="5e19d-197">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span> <span data-ttu-id="5e19d-198">Hallo application-object gemaakt is beoogde toorepresent Hallo doel app u tooand implementeren van eenmalige aanmelding voor, en niet alleen Hallo SCIM eindpunt wilt inrichten.</span><span class="sxs-lookup"><span data-stu-id="5e19d-198">hello application object created is intended toorepresent hello target app you would be provisioning tooand implementing single sign-on for, and not just hello SCIM endpoint.</span></span>
4. <span data-ttu-id="5e19d-199">Selecteer in de resulterende welkomstscherm Hallo **inrichten** tabblad in de linkerkolom Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e19d-199">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="5e19d-200">In Hallo **modus inrichting** selecteert u **automatische**.</span><span class="sxs-lookup"><span data-stu-id="5e19d-200">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="5e19d-201">![][2]
  *Afbeelding 4: Configureren in Azure-portal Hallo inrichting*</span><span class="sxs-lookup"><span data-stu-id="5e19d-201">![][2]
*Figure 4: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="5e19d-202">In Hallo **Tenant-URL** Voer Hallo internet blootgesteld URL en poort van uw eindpunt SCIM.</span><span class="sxs-lookup"><span data-stu-id="5e19d-202">In hello **Tenant URL** field, enter hello internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="5e19d-203">Zou dit iets zoals http://testmachine.contoso.com:9000 of http://<ip-address>:9000/, waarbij < ip-adres > internet is Hallo blootgesteld IP adres.</span><span class="sxs-lookup"><span data-stu-id="5e19d-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is hello internet exposed IP address.</span></span>  
7. <span data-ttu-id="5e19d-204">Als Hallo SCIM eindpunt een OAuth bearer-token van een verlener dan Azure AD vereist, wordt de kopie Hallo OAuth bearer-token in Hallo optionele vereist **geheim Token** veld.</span><span class="sxs-lookup"><span data-stu-id="5e19d-204">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="5e19d-205">Als dit veld leeg laat, wordt Azure AD een OAuth-bearer-token van Azure AD bij elke aanvraag uitgegeven opnemen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="5e19d-206">Apps die gebruikmaken van Azure AD als een id-provider kunt controleren of deze Azure AD-verleend token.</span><span class="sxs-lookup"><span data-stu-id="5e19d-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="5e19d-207">Klik op Hallo **testverbinding** knop toohave Azure Active Directory poging tooconnect toohello SCIM eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5e19d-207">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="5e19d-208">Als Hallo pogingen mislukken, wordt informatie over de fout wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5e19d-208">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="5e19d-209">Als Hallo pogingen tooconnect toohello toepassing slaagt, klikt u op **opslaan** toosave Hallo beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="5e19d-209">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="5e19d-210">In Hallo **toewijzingen** sectie, zijn er twee sets van selecteerbare Kenmerktoewijzingen: één voor gebruikersobjecten en één voor groepsobjecten.</span><span class="sxs-lookup"><span data-stu-id="5e19d-210">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="5e19d-211">Selecteer elke één tooreview Hallo kenmerken die worden gesynchroniseerd vanuit Azure Active Directory tooyour app.</span><span class="sxs-lookup"><span data-stu-id="5e19d-211">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="5e19d-212">kenmerken die zijn geselecteerd als Hallo **overeenkomend** eigenschappen zijn gebruikte toomatch Hallo gebruikers en groepen in uw app voor update-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-212">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="5e19d-213">Selecteer Hallo knop toocommit wijzigingen zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-213">Select hello Save button toocommit any changes.</span></span>
11. <span data-ttu-id="5e19d-214">Onder **instellingen**, Hallo **bereik** veld wordt gedefinieerd welke gebruikers en groepen worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="5e19d-214">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="5e19d-215">Alleen selecteren 'Sync alleen toegewezen gebruikers en groepen' (aanbevolen) worden gesynchroniseerd gebruikers en groepen die zijn toegewezen in Hallo **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="5e19d-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="5e19d-216">Zodra de configuratie voltooid is, verandert Hallo **inrichting Status** te**op**.</span><span class="sxs-lookup"><span data-stu-id="5e19d-216">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="5e19d-217">Klik op **opslaan** toostart Hallo inrichting Azure AD-service.</span><span class="sxs-lookup"><span data-stu-id="5e19d-217">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="5e19d-218">Als alleen synchroniseren toegewezen gebruikers en groepen (aanbevolen), moet u ervoor tooselect Hallo **gebruikers en groepen** tabblad en Hallo-gebruikers en/of groepen die u wenst dat toosync toewijzen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-218">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="5e19d-219">Nadat de initiële synchronisatie Hallo is gestart, kunt u Hallo **controlelogboeken** tabblad toomonitor voortgang, waarin alle bewerkingen die worden uitgevoerd door het Hallo-service op uw app wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="5e19d-219">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="5e19d-220">Zie voor meer informatie over hoe tooread hello Azure AD-inrichting registreert, [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="5e19d-220">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="5e19d-221">Hallo laatste stap bij het controleren van Hallo voorbeeld is tooopen hello TargetFile.csv-bestand in Hallo \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug map op uw Windows-machine.</span><span class="sxs-lookup"><span data-stu-id="5e19d-221">hello final step in verifying hello sample is tooopen hello TargetFile.csv file in hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="5e19d-222">Zodra het inrichtingsproces hello wordt uitgevoerd, ziet u dit bestand Hallo details van alle toegewezen en ingericht gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-222">Once hello provisioning process is run, this file shows hello details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="5e19d-223">-Ontwikkelbibliotheken</span><span class="sxs-lookup"><span data-stu-id="5e19d-223">Development libraries</span></span>
<span data-ttu-id="5e19d-224">toodevelop uw eigen webservice die toohello SCIM specificatie voldoet eerst raken met Hallo volgende bibliotheken opgegeven door Microsoft toohelp Hallo ontwikkelingsproces versnellen:</span><span class="sxs-lookup"><span data-stu-id="5e19d-224">toodevelop your own web service that conforms toohello SCIM specification, first familiarize yourself with hello following libraries provided by Microsoft toohelp accelerate hello development process:</span></span> 

1. <span data-ttu-id="5e19d-225">Algemene Language Infrastructure (CLI) bibliotheken zijn beschikbaar voor gebruik met talen die op basis van die infrastructuur, zoals C#.</span><span class="sxs-lookup"><span data-stu-id="5e19d-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="5e19d-226">Een van deze bibliotheken [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declareert een interface Microsoft.SystemForCrossDomainIdentityManagement.IProvider, weergegeven in de volgende illustratie Hallo: A ontwikkelaars met Hallo bibliotheken zou implementeren die interface met een klasse die algemeen als een provider, kan worden verwezen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in hello following illustration:  A developer using hello libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="5e19d-227">Hallo-bibliotheken inschakelen Hallo developer toodeploy een webservice die toohello SCIM specificatie voldoet.</span><span class="sxs-lookup"><span data-stu-id="5e19d-227">hello libraries enable hello developer toodeploy a web service that conforms toohello SCIM specification.</span></span> <span data-ttu-id="5e19d-228">Hallo-webservice kan ofwel worden gehost in Internet Information Services of een uitvoerbaar Common Language Infrastructure-assembly.</span><span class="sxs-lookup"><span data-stu-id="5e19d-228">hello web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="5e19d-229">Aanvraag wordt omgezet in aanroepen toohello provider methoden die zou worden geprogrammeerd door Hallo developer toooperate op sommige identity-store.</span><span class="sxs-lookup"><span data-stu-id="5e19d-229">Request is translated into calls toohello provider’s methods, which would be programmed by hello developer toooperate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="5e19d-230">[Express route-handlers](http://expressjs.com/guide/routing.html) beschikbaar zijn voor het parseren van node.js aanvraagobjecten die oproepen (zoals gedefinieerd door Hallo SCIM specificatie), tooa node.js-web-service vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="5e19d-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by hello SCIM specification), made tooa node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="5e19d-231">Het bouwen van een aangepaste SCIM-eindpunt</span><span class="sxs-lookup"><span data-stu-id="5e19d-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="5e19d-232">Hallo CLI bibliotheken gebruiken, kunnen ontwikkelaars die bibliotheken met hun services in uitvoerbaar Common Language Infrastructure assembly of in Internet Information Services hosten.</span><span class="sxs-lookup"><span data-stu-id="5e19d-232">Using hello CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="5e19d-233">Hier volgt een voorbeeld van code voor het hosten van een service binnen een uitvoerbare assembly, op het Hallo-adres http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="5e19d-233">Here is sample code for hosting a service within an executable assembly, at hello address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="5e19d-234">Deze service moet een HTTP-adres en de server certificaat voor clientverificatie welke Hallo basiscertificeringsinstantie een van de volgende Hallo is hebben:</span><span class="sxs-lookup"><span data-stu-id="5e19d-234">This service must have an HTTP address and server authentication certificate of which hello root certification authority is one of hello following:</span></span> 

* <span data-ttu-id="5e19d-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="5e19d-235">CNNIC</span></span>
* <span data-ttu-id="5e19d-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="5e19d-236">Comodo</span></span>
* <span data-ttu-id="5e19d-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="5e19d-237">CyberTrust</span></span>
* <span data-ttu-id="5e19d-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="5e19d-238">DigiCert</span></span>
* <span data-ttu-id="5e19d-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="5e19d-239">GeoTrust</span></span>
* <span data-ttu-id="5e19d-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="5e19d-240">GlobalSign</span></span>
* <span data-ttu-id="5e19d-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="5e19d-241">Go Daddy</span></span>
* <span data-ttu-id="5e19d-242">VeriSign</span><span class="sxs-lookup"><span data-stu-id="5e19d-242">Verisign</span></span>
* <span data-ttu-id="5e19d-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="5e19d-243">WoSign</span></span>

<span data-ttu-id="5e19d-244">Een certificaat voor serververificatie zijn gebonden tooa poort op een Windows-host met behulp van hulpprogramma Hallo netwerk-shell:</span><span class="sxs-lookup"><span data-stu-id="5e19d-244">A server authentication certificate can be bound tooa port on a Windows host using hello network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="5e19d-245">Hallo-waarde opgegeven voor het Hallo certhash argument is hier Hallo vingerafdruk van certificaat hello, terwijl Hallo opgegeven waarde voor Hallo appid argument een globally unique identifier is.</span><span class="sxs-lookup"><span data-stu-id="5e19d-245">Here, hello value provided for hello certhash argument is hello thumbprint of hello certificate, while hello value provided for hello appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="5e19d-246">in Internet Information Services toohost Hallo-service, een ontwikkelaar zou een CLA code bibliotheek-assembly met een klasse met de naam opstarten in de standaardnaamruimte Hallo van Hallo assembly bouwen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-246">toohost hello service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in hello default namespace of hello assembly.</span></span>  <span data-ttu-id="5e19d-247">Hier volgt een voorbeeld van deze klasse:</span><span class="sxs-lookup"><span data-stu-id="5e19d-247">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="5e19d-248">Afhandeling van endpoint-verificatie</span><span class="sxs-lookup"><span data-stu-id="5e19d-248">Handling endpoint authentication</span></span>
<span data-ttu-id="5e19d-249">Aanvragen van Azure Active Directory bevatten een OAuth 2.0-bearer-token.</span><span class="sxs-lookup"><span data-stu-id="5e19d-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="5e19d-250">Een serviceaanvraag voor de ontvangende Hallo moet verifiëren Hallo verlener als Azure Active Directory namens Hallo verwacht Azure Active Directory-tenant voor toegang tot toohello Azure Active Directory Graph-webservice.</span><span class="sxs-lookup"><span data-stu-id="5e19d-250">Any service receiving hello request should authenticate hello issuer as being Azure Active Directory on behalf of hello expected Azure Active Directory tenant, for access toohello Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="5e19d-251">Hallo-token Hallo verlener wordt geïdentificeerd door een claim iss, zoals 'iss': 'https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/'.</span><span class="sxs-lookup"><span data-stu-id="5e19d-251">In hello token, hello issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="5e19d-252">In dit voorbeeld, Hallo basisadres van de claimwaarde hello, https://sts.windows.net, Azure Active Directory wordt aangemerkt als Hallo verlener, terwijl hello relatief adres segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, wordt een unieke id van Azure Active Hallo Directory-tenant namens welke Hallo token is uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="5e19d-252">In this example, hello base address of hello claim value, https://sts.windows.net, identifies Azure Active Directory as hello issuer, while hello relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of hello Azure Active Directory tenant on behalf of which hello token was issued.</span></span>  <span data-ttu-id="5e19d-253">Als het Hallo-token is uitgegeven voor toegang tot hello Azure Active Directory Graph-webservice, klikt u vervolgens Hallo-id van die service worden 00000002-0000-0000-c000-000000000000, in Hallo-waarde van het Hallo-token aud claimen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-253">If hello token was issued for accessing hello Azure Active Directory Graph web service, then hello identifier of that service, 00000002-0000-0000-c000-000000000000, should be in hello value of hello token’s aud claim.</span></span>  

<span data-ttu-id="5e19d-254">Ontwikkelaars Hallo CLA bibliotheken geleverd door Microsoft voor het bouwen van een service SCIM gebruiken kunnen verifiëren aanvragen van Azure Active Directory met Hallo Microsoft.Owin.Security.ActiveDirectory pakket met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="5e19d-254">Developers using hello CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using hello Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="5e19d-255">Implementeren in een provider Hallo Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior eigenschap doordat het retourneren van een methode toobe wordt aangeroepen wanneer het Hallo-service wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="5e19d-255">In a provider, implement hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method toobe called whenever hello service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="5e19d-256">Hallo code toothat methode toohave na elke aanvraag tooany Hallo-service-eindpunten die zijn geverifieerd als voorzien van een token dat is uitgegeven door Azure Active Directory namens een tenant opgegeven voor toegang tot toohello Azure AD Graph-webservice toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5e19d-256">Add hello following code toothat method toohave any request tooany of hello service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access toohello Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="5e19d-257">Schema voor gebruikers en groepen</span><span class="sxs-lookup"><span data-stu-id="5e19d-257">User and group schema</span></span>
<span data-ttu-id="5e19d-258">Azure Active Directory kunnen twee soorten resources tooSCIM webservices inrichten.</span><span class="sxs-lookup"><span data-stu-id="5e19d-258">Azure Active Directory can provision two types of resources tooSCIM web services.</span></span>  <span data-ttu-id="5e19d-259">Deze typen resources zijn gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="5e19d-260">User-bronnen worden geïdentificeerd door Hallo schema-id, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, die is opgenomen in deze specificatie van het protocol: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="5e19d-260">User resources are identified by hello schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="5e19d-261">de standaardtoewijzing Hallo Hallo kenmerken van gebruikers in Azure Active Directory toohello kenmerken van urn: ietf:params:scim:schemas:extension:enterprise:2.0:User resources hieronder vindt u in de tabel 1.</span><span class="sxs-lookup"><span data-stu-id="5e19d-261">hello default mapping of hello attributes of users in Azure Active Directory toohello attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="5e19d-262">Groep resources worden geïdentificeerd door Hallo schema-id, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="5e19d-262">Group resources are identified by hello schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="5e19d-263">Tabel 2 hieronder toont Hallo standaardtoewijzing Hallo kenmerken van groepen in Azure Active Directory toohello kenmerken http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span><span class="sxs-lookup"><span data-stu-id="5e19d-263">Table 2, below, shows hello default mapping of hello attributes of groups in Azure Active Directory toohello attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="5e19d-264">Tabel 1: Standaard Gebruikerskoppeling kenmerk</span><span class="sxs-lookup"><span data-stu-id="5e19d-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="5e19d-265">Azure Active Directory-gebruiker</span><span class="sxs-lookup"><span data-stu-id="5e19d-265">Azure Active Directory user</span></span> | <span data-ttu-id="5e19d-266">urn: ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="5e19d-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="5e19d-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="5e19d-267">IsSoftDeleted</span></span> |<span data-ttu-id="5e19d-268">Actieve</span><span class="sxs-lookup"><span data-stu-id="5e19d-268">active</span></span> |
| <span data-ttu-id="5e19d-269">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="5e19d-269">displayName</span></span> |<span data-ttu-id="5e19d-270">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="5e19d-270">displayName</span></span> |
| <span data-ttu-id="5e19d-271">Fax TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="5e19d-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="5e19d-272">phoneNumbers type eq 'fax'.value</span><span class="sxs-lookup"><span data-stu-id="5e19d-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="5e19d-273">Voornaam</span><span class="sxs-lookup"><span data-stu-id="5e19d-273">givenName</span></span> |<span data-ttu-id="5e19d-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="5e19d-274">name.givenName</span></span> |
| <span data-ttu-id="5e19d-275">Functie</span><span class="sxs-lookup"><span data-stu-id="5e19d-275">jobTitle</span></span> |<span data-ttu-id="5e19d-276">titel</span><span class="sxs-lookup"><span data-stu-id="5e19d-276">title</span></span> |
| <span data-ttu-id="5e19d-277">E-mail</span><span class="sxs-lookup"><span data-stu-id="5e19d-277">mail</span></span> |<span data-ttu-id="5e19d-278">e-mailberichten type eq 'werk'.value</span><span class="sxs-lookup"><span data-stu-id="5e19d-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="5e19d-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="5e19d-279">mailNickname</span></span> |<span data-ttu-id="5e19d-280">externalId</span><span class="sxs-lookup"><span data-stu-id="5e19d-280">externalId</span></span> |
| <span data-ttu-id="5e19d-281">Manager</span><span class="sxs-lookup"><span data-stu-id="5e19d-281">manager</span></span> |<span data-ttu-id="5e19d-282">Manager</span><span class="sxs-lookup"><span data-stu-id="5e19d-282">manager</span></span> |
| <span data-ttu-id="5e19d-283">mobiele</span><span class="sxs-lookup"><span data-stu-id="5e19d-283">mobile</span></span> |<span data-ttu-id="5e19d-284">phoneNumbers type eq 'mobiel'.value</span><span class="sxs-lookup"><span data-stu-id="5e19d-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="5e19d-285">object-id</span><span class="sxs-lookup"><span data-stu-id="5e19d-285">objectId</span></span> |<span data-ttu-id="5e19d-286">id</span><span class="sxs-lookup"><span data-stu-id="5e19d-286">id</span></span> |
| <span data-ttu-id="5e19d-287">Postcode</span><span class="sxs-lookup"><span data-stu-id="5e19d-287">postalCode</span></span> |<span data-ttu-id="5e19d-288">adressen type eq 'werk'.postalCode</span><span class="sxs-lookup"><span data-stu-id="5e19d-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="5e19d-289">proxy-adressen</span><span class="sxs-lookup"><span data-stu-id="5e19d-289">proxy-Addresses</span></span> |<span data-ttu-id="5e19d-290">e-mailberichten [Geef eq 'andere']. Waarde</span><span class="sxs-lookup"><span data-stu-id="5e19d-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="5e19d-291">fysieke-levering-OfficeName</span><span class="sxs-lookup"><span data-stu-id="5e19d-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="5e19d-292">adressen [Geef eq 'andere']. Indeling</span><span class="sxs-lookup"><span data-stu-id="5e19d-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="5e19d-293">StreetAddress</span><span class="sxs-lookup"><span data-stu-id="5e19d-293">streetAddress</span></span> |<span data-ttu-id="5e19d-294">adressen type eq 'werk'.streetAddress</span><span class="sxs-lookup"><span data-stu-id="5e19d-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="5e19d-295">Achternaam</span><span class="sxs-lookup"><span data-stu-id="5e19d-295">surname</span></span> |<span data-ttu-id="5e19d-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="5e19d-296">name.familyName</span></span> |
| <span data-ttu-id="5e19d-297">Telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="5e19d-297">telephone-Number</span></span> |<span data-ttu-id="5e19d-298">phoneNumbers type eq 'werk'.value</span><span class="sxs-lookup"><span data-stu-id="5e19d-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="5e19d-299">primaire gebruiker-naam</span><span class="sxs-lookup"><span data-stu-id="5e19d-299">user-PrincipalName</span></span> |<span data-ttu-id="5e19d-300">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="5e19d-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="5e19d-301">Tabel 2: Standaard kenmerk apparaatgroeptoewijzing</span><span class="sxs-lookup"><span data-stu-id="5e19d-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="5e19d-302">Azure Active Directory-groep</span><span class="sxs-lookup"><span data-stu-id="5e19d-302">Azure Active Directory group</span></span> | <span data-ttu-id="5e19d-303">http://schemas.Microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="5e19d-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="5e19d-304">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="5e19d-304">displayName</span></span> |<span data-ttu-id="5e19d-305">externalId</span><span class="sxs-lookup"><span data-stu-id="5e19d-305">externalId</span></span> |
| <span data-ttu-id="5e19d-306">E-mail</span><span class="sxs-lookup"><span data-stu-id="5e19d-306">mail</span></span> |<span data-ttu-id="5e19d-307">e-mailberichten type eq 'werk'.value</span><span class="sxs-lookup"><span data-stu-id="5e19d-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="5e19d-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="5e19d-308">mailNickname</span></span> |<span data-ttu-id="5e19d-309">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="5e19d-309">displayName</span></span> |
| <span data-ttu-id="5e19d-310">Leden</span><span class="sxs-lookup"><span data-stu-id="5e19d-310">members</span></span> |<span data-ttu-id="5e19d-311">Leden</span><span class="sxs-lookup"><span data-stu-id="5e19d-311">members</span></span> |
| <span data-ttu-id="5e19d-312">object-id</span><span class="sxs-lookup"><span data-stu-id="5e19d-312">objectId</span></span> |<span data-ttu-id="5e19d-313">id</span><span class="sxs-lookup"><span data-stu-id="5e19d-313">id</span></span> |
| <span data-ttu-id="5e19d-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="5e19d-314">proxyAddresses</span></span> |<span data-ttu-id="5e19d-315">e-mailberichten [Geef eq 'andere']. Waarde</span><span class="sxs-lookup"><span data-stu-id="5e19d-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="5e19d-316">Gebruikers inrichten en de inrichting</span><span class="sxs-lookup"><span data-stu-id="5e19d-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="5e19d-317">Hallo volgende afbeelding toont Hallo-berichten dat tooa SCIM service toomanage Hallo levenscyclus van een gebruiker in een andere identiteit store wordt verzonden naar Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5e19d-317">hello following illustration shows hello messages that Azure Active Directory sends tooa SCIM service toomanage hello lifecycle of a user in another identity store.</span></span> <span data-ttu-id="5e19d-318">Hallo diagram ziet u ook hoe een SCIM service geïmplementeerd met behulp van de CLI-bibliotheken Hallo geleverd door Microsoft voor het bouwen dat dergelijke services deze aanvragen vertalen naar aanroepen toohello methoden van een provider.</span><span class="sxs-lookup"><span data-stu-id="5e19d-318">hello diagram also shows how a SCIM service implemented using hello CLI libraries provided by Microsoft for building such services translate those requests into calls toohello methods of a provider.</span></span>  

<span data-ttu-id="5e19d-319">![][4]
*Afbeelding 5: Gebruikers inrichten en de inrichting reeks*</span><span class="sxs-lookup"><span data-stu-id="5e19d-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="5e19d-320">Azure Active Directory-query's Hallo-service voor een gebruiker met een externalId-kenmerkwaarde die overeenkomt met de Hallo mailNickname kenmerkwaarde van een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e19d-320">Azure Active Directory queries hello service for a user with an externalId attribute value matching hello mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="5e19d-321">Hallo-query wordt uitgedrukt als een aanvraag Hypertext Transfer Protocol (HTTP) zoals dit voorbeeld waarin jyoung een voorbeeld van een mailNickname van een gebruiker in Azure Active Directory is:</span><span class="sxs-lookup"><span data-stu-id="5e19d-321">hello query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="5e19d-322">Als het Hallo-service is opgebouwd Hallo Common Language Infrastructure bibliotheken geleverd door Microsoft voor het implementeren van services SCIM gebruiken, wordt Hallo aanvraag omgezet in een aanroep toohello querymethode van Hallo serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="5e19d-322">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span>  <span data-ttu-id="5e19d-323">Hier volgt Hallo handtekening van deze methode:</span><span class="sxs-lookup"><span data-stu-id="5e19d-323">Here is hello signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="5e19d-324">Hallo-definitie van Hallo Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface Ga als volgt:</span><span class="sxs-lookup"><span data-stu-id="5e19d-324">Here is hello definition of hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="5e19d-325">In Hallo voorbeeld van een query voor een gebruiker met een opgegeven waarde voor Hallo externalId kenmerk te volgen, zijn waarden van Hallo argumenten doorgegeven toohello Query-methode:</span><span class="sxs-lookup"><span data-stu-id="5e19d-325">In hello following sample of a query for a user with a given value for hello externalId attribute, values of hello arguments passed toohello Query method are:</span></span> 
  * <span data-ttu-id="5e19d-326">parameters. AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="5e19d-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="5e19d-327">parameters. AlternateFilters.ElementAt(0). AttributePath: 'externalId'</span><span class="sxs-lookup"><span data-stu-id="5e19d-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="5e19d-328">parameters. AlternateFilters.ElementAt(0). Vergelijkingsoperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="5e19d-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="5e19d-329">parameters. AlternateFilter.ElementAt(0). ComparisonValue: 'jyoung'</span><span class="sxs-lookup"><span data-stu-id="5e19d-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="5e19d-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin. RequestId"]</span><span class="sxs-lookup"><span data-stu-id="5e19d-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="5e19d-331">Als Hallo antwoord tooa query toohello webservice voor een gebruiker met een kenmerkwaarde externalId die overeenkomt met de Hallo mailNickname kenmerkwaarde van een gebruiker niet alle gebruikers, klikt u vervolgens Azure Active Directory-aanvragen die Hallo service bepaling van een gebruiker bijbehorende toohello één in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5e19d-331">If hello response tooa query toohello web service for a user with an externalId attribute value that matches hello mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that hello service provision a user corresponding toohello one in Azure Active Directory.</span></span>  <span data-ttu-id="5e19d-332">Hier volgt een voorbeeld van een aanvraag:</span><span class="sxs-lookup"><span data-stu-id="5e19d-332">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="5e19d-333">Hallo Common Language Infrastructure bibliotheken geleverd door Microsoft voor het implementeren van services SCIM zou die aanvraag vertalen naar een toohello aanroep van methode Create van Hallo serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="5e19d-333">hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call toohello Create method of hello service’s provider.</span></span>  <span data-ttu-id="5e19d-334">Hallo methode Create heeft deze handtekening:</span><span class="sxs-lookup"><span data-stu-id="5e19d-334">hello Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="5e19d-335">Hallo-waarde van Hallo resource argument is in een tooprovision aanvraag een gebruiker een exemplaar van Hallo Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="5e19d-335">In a request tooprovision a user, hello value of hello resource argument is an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="5e19d-336">Core2EnterpriseUser klasse is gedefinieerd in Hallo Microsoft.SystemForCrossDomainIdentityManagement.Schemas-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="5e19d-336">Core2EnterpriseUser class, defined in hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="5e19d-337">Als Hallo aanvraag tooprovision Hallo gebruiker slaagt, klikt u vervolgens is hello implementatie van Hallo-methode verwachte tooreturn een exemplaar van Hallo Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="5e19d-337">If hello request tooprovision hello user succeeds, then hello implementation of hello method is expected tooreturn an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="5e19d-338">Core2EnterpriseUser klasse, met het Hallo-waarde van de id-eigenschap Hallo unieke id van de toohello van Hallo nieuw ingerichte gebruiker instellen.</span><span class="sxs-lookup"><span data-stu-id="5e19d-338">Core2EnterpriseUser class, with hello value of hello Identifier property set toohello unique identifier of hello newly provisioned user.</span></span>  

3. <span data-ttu-id="5e19d-339">tooupdate bekend tooexist in een archief van de identiteit van een gebruiker fronted door een SCIM, Azure Active Directory uitgevoerd door het aanvragen van huidige status van die gebruiker Hallo van Hallo-service met een aanvraag, zoals:</span><span class="sxs-lookup"><span data-stu-id="5e19d-339">tooupdate a user known tooexist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting hello current state of that user from hello service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="5e19d-340">In een service die is gebouwd met behulp van Hallo Common Language Infrastructure bibliotheken geleverd door Microsoft voor het implementeren van services SCIM, wordt Hallo-aanvraag omgezet in een aanroep toohello ophalen-methode van Hallo serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="5e19d-340">In a service built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, hello request is translated into a call toohello Retrieve method of hello service’s provider.</span></span>  <span data-ttu-id="5e19d-341">Hier volgt Hallo handtekening van Hallo ophalen methode:</span><span class="sxs-lookup"><span data-stu-id="5e19d-341">Here is hello signature of hello Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="5e19d-342">In voorbeeld van een aanvraag tooretrieve Hallo huidige status van een gebruiker Hallo zijn Hallo waarden van Hallo-eigenschappen van Hallo-object opgegeven Hallo-waarde van argument Hallo-parameters als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="5e19d-342">In hello example of a request tooretrieve hello current state of a user, hello values of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="5e19d-343">-ID: '54D382A4-2050-4C03-94D1-E769F1D15682'</span><span class="sxs-lookup"><span data-stu-id="5e19d-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="5e19d-344">SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'</span><span class="sxs-lookup"><span data-stu-id="5e19d-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="5e19d-345">Als een verwijzingskenmerk bijgewerkt, toobe vervolgens Azure Active Directory-query's Hallo service toodetermine is al dan niet hello huidige waarde van Hallo verwijzingskenmerk in archief Hallo fronted door Hallo-service al overeenkomt met de waarde van dit kenmerk Hallo in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5e19d-345">If a reference attribute is toobe updated, then Azure Active Directory queries hello service toodetermine whether or not hello current value of hello reference attribute in hello identity store fronted by hello service already matches hello value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="5e19d-346">Voor gebruikers is de enige kenmerk Hallo welke Hallo huidige waarde op deze manier wordt opgevraagd Hallo manager kenmerk.</span><span class="sxs-lookup"><span data-stu-id="5e19d-346">For users, hello only attribute of which hello current value is queried in this way is hello manager attribute.</span></span> <span data-ttu-id="5e19d-347">Hier volgt een voorbeeld van een aanvraag toodetermine of Hallo manager kenmerk van een bepaalde gebruiker-object momenteel een bepaalde waarde is:</span><span class="sxs-lookup"><span data-stu-id="5e19d-347">Here is an example of a request toodetermine whether hello manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="5e19d-348">Hallo waarde van kenmerken queryparameter Hallo-id, betekent dat als een gebruikersobject bestaat die voldoet aan Hallo expressie opgegeven Hallo-waarde van parameter Hallo filter-query, is Hallo service verwachte toorespond met een urn: ietf:params:scim:schemas: Core: 2.0:User of urn: ietf:params:scim:schemas:extension:enterprise:2.0:User bron, met inbegrip van alleen Hallo waarde van kenmerk van de bron-id.</span><span class="sxs-lookup"><span data-stu-id="5e19d-348">hello value of hello attributes query parameter, id, signifies that if a user object exists that satisfies hello expression provided as hello value of hello filter query parameter, then hello service is expected toorespond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only hello value of that resource’s id attribute.</span></span>  <span data-ttu-id="5e19d-349">waarde van Hallo Hallo **id** kenmerk toohello aanvrager is bekend.</span><span class="sxs-lookup"><span data-stu-id="5e19d-349">hello value of hello **id** attribute is known toohello requestor.</span></span> <span data-ttu-id="5e19d-350">Het is opgenomen in het Hallo-waarde van de queryparameter Hallo-filter; Hallo-doel van deze vragen is daadwerkelijk toorequest een minimale representatie van een resource die voldoen aan de filterexpressie Hallo als indicatie van of deze object bestaat.</span><span class="sxs-lookup"><span data-stu-id="5e19d-350">It is included in hello value of hello filter query parameter; hello purpose of asking for it is actually toorequest a minimal representation of a resource that satisfying hello filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="5e19d-351">Als het Hallo-service is opgebouwd Hallo Common Language Infrastructure bibliotheken geleverd door Microsoft voor het implementeren van services SCIM gebruiken, wordt Hallo aanvraag omgezet in een aanroep toohello querymethode van Hallo serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="5e19d-351">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span> <span data-ttu-id="5e19d-352">Hallo-waarde van Hallo eigenschappen van Hallo object dat is opgegeven als Hallo-waarde van argument Hallo-parameters zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="5e19d-352">hello value of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="5e19d-353">parameters. AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="5e19d-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="5e19d-354">parameters. AlternateFilters.ElementAt(x). AttributePath: 'id'</span><span class="sxs-lookup"><span data-stu-id="5e19d-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="5e19d-355">parameters. AlternateFilters.ElementAt(x). Vergelijkingsoperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="5e19d-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="5e19d-356">parameters. AlternateFilter.ElementAt(x). ComparisonValue: '54D382A4-2050-4C03-94D1-E769F1D15682'</span><span class="sxs-lookup"><span data-stu-id="5e19d-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="5e19d-357">parameters. AlternateFilters.ElementAt(y). AttributePath: 'manager'</span><span class="sxs-lookup"><span data-stu-id="5e19d-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="5e19d-358">parameters. AlternateFilters.ElementAt(y). Vergelijkingsoperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="5e19d-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="5e19d-359">parameters. AlternateFilter.ElementAt(y). ComparisonValue: '2819c223-7f76-453a-919d-413861904646'</span><span class="sxs-lookup"><span data-stu-id="5e19d-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="5e19d-360">parameters. RequestedAttributePaths.ElementAt(0): 'id'</span><span class="sxs-lookup"><span data-stu-id="5e19d-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="5e19d-361">parameters. SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'</span><span class="sxs-lookup"><span data-stu-id="5e19d-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="5e19d-362">Hier Hallo-waarde van Hallo index x mogelijk 0 en Hallo-waarde van y voor Hallo-index is mogelijk 1, of mogelijk Hallo-waarde van x 1 en Hallo-waarde van y kan zijn ingesteld op 0, afhankelijk van het Hallo-volgorde van Hallo expressies van het Hallo-filter-queryparameter.</span><span class="sxs-lookup"><span data-stu-id="5e19d-362">Here, hello value of hello index x may be 0 and hello value of hello index y may be 1, or hello value of x may be 1 and hello value of y may be 0, depending on hello order of hello expressions of hello filter query parameter.</span></span>   

5. <span data-ttu-id="5e19d-363">Hier volgt een voorbeeld van een aanvraag van Azure Active Directory tooan SCIM service tooupdate een gebruiker:</span><span class="sxs-lookup"><span data-stu-id="5e19d-363">Here is an example of a request from Azure Active Directory tooan SCIM service tooupdate a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="5e19d-364">Hallo Microsoft Common Language Infrastructure bibliotheken voor het implementeren van services SCIM zou Hallo aanvraag vertalen naar een toohello aanroep van methode Update van Hallo serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="5e19d-364">hello Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate hello request into a call toohello Update method of hello service’s provider.</span></span> <span data-ttu-id="5e19d-365">Hier volgt Hallo handtekening Hallo updatemethode:</span><span class="sxs-lookup"><span data-stu-id="5e19d-365">Here is hello signature of hello Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="5e19d-366">In voorbeeld van een aanvraag tooupdate een gebruiker Hallo heeft Hallo object opgegeven Hallo-waarde van Hallo patch argument waarden van deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="5e19d-366">In hello example of a request tooupdate a user, hello object provided as hello value of hello patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="5e19d-367">ResourceIdentifier.Identifier: '54D382A4-2050-4C03-94D1-E769F1D15682'</span><span class="sxs-lookup"><span data-stu-id="5e19d-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="5e19d-368">ResourceIdentifier.SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'</span><span class="sxs-lookup"><span data-stu-id="5e19d-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="5e19d-369">(PatchRequest als PatchRequest2). Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="5e19d-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="5e19d-370">(PatchRequest als PatchRequest2). Operations.ElementAt(0). OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="5e19d-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="5e19d-371">(PatchRequest als PatchRequest2). Operations.ElementAt(0). Path.AttributePath: 'manager'</span><span class="sxs-lookup"><span data-stu-id="5e19d-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="5e19d-372">(PatchRequest als PatchRequest2). Operations.ElementAt(0). Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="5e19d-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="5e19d-373">(PatchRequest als PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Verwijzing: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="5e19d-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="5e19d-374">(PatchRequest als PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Waarde: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="5e19d-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="5e19d-375">toode inrichten een gebruiker uit een identity-store fronted door een SCIM-service, Azure AD verzendt een aanvraag, zoals:</span><span class="sxs-lookup"><span data-stu-id="5e19d-375">toode-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="5e19d-376">Als het Hallo-service is opgebouwd Hallo Common Language Infrastructure bibliotheken geleverd door Microsoft voor het implementeren van services SCIM gebruiken, wordt Hallo aanvraag omgezet in een aanroep toohello Delete-methode van Hallo serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="5e19d-376">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Delete method of hello service’s provider.</span></span>   <span data-ttu-id="5e19d-377">Deze methode heeft deze handtekening:</span><span class="sxs-lookup"><span data-stu-id="5e19d-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="5e19d-378">Hallo-object opgegeven Hallo-waarde van Hallo resourceIdentifier argument heeft deze eigenschapswaarden in Hallo voorbeeld van een aanvraag toode-bepaling van een gebruiker:</span><span class="sxs-lookup"><span data-stu-id="5e19d-378">hello object provided as hello value of hello resourceIdentifier argument has these property values in hello example of a request toode-provision a user:</span></span> 
  
  * <span data-ttu-id="5e19d-379">ResourceIdentifier.Identifier: '54D382A4-2050-4C03-94D1-E769F1D15682'</span><span class="sxs-lookup"><span data-stu-id="5e19d-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="5e19d-380">ResourceIdentifier.SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'</span><span class="sxs-lookup"><span data-stu-id="5e19d-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="5e19d-381">Groep inrichting en ongedaan inrichten</span><span class="sxs-lookup"><span data-stu-id="5e19d-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="5e19d-382">Hallo volgende afbeelding toont Hallo-berichten dat Azure AcD tooa SCIM service toomanage Hallo levenscyclus van een groep in een andere identiteit store verzendt.</span><span class="sxs-lookup"><span data-stu-id="5e19d-382">hello following illustration shows hello messages that Azure AcD sends tooa SCIM service toomanage hello lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="5e19d-383">Deze berichten verschillen van Hallo-berichten die deel uitmaakt van toousers op drie manieren:</span><span class="sxs-lookup"><span data-stu-id="5e19d-383">Those messages differ from hello messages pertaining toousers in three ways:</span></span> 

* <span data-ttu-id="5e19d-384">Hallo-schema van een bron wordt geïdentificeerd als http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="5e19d-384">hello schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="5e19d-385">Aanvragen tooretrieve groepen bepalen dat Hallo leden-kenmerk is uitgesloten van een resource in het antwoord toohello aanvraag toobe.</span><span class="sxs-lookup"><span data-stu-id="5e19d-385">Requests tooretrieve groups stipulate that hello members attribute is toobe excluded from any resource provided in response toohello request.</span></span>  
* <span data-ttu-id="5e19d-386">Aanvragen toodetermine aanvragen over Hallo leden kenmerk of een verwijzingskenmerk heeft voor een bepaalde waarde zijn.</span><span class="sxs-lookup"><span data-stu-id="5e19d-386">Requests toodetermine whether a reference attribute has a certain value are requests about hello members attribute.</span></span>  

<span data-ttu-id="5e19d-387">![][5]
*Afbeelding 6: Inrichting en ongedaan inrichting sequence groeperen*</span><span class="sxs-lookup"><span data-stu-id="5e19d-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="5e19d-388">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="5e19d-388">Related articles</span></span>
* <span data-ttu-id="5e19d-389">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="5e19d-389">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="5e19d-390">Gebruiker inrichten/Deprovisioning tooSaaS Apps automatiseren</span><span class="sxs-lookup"><span data-stu-id="5e19d-390">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="5e19d-391">Kenmerktoewijzingen voor gebruikers inrichten aanpassen</span><span class="sxs-lookup"><span data-stu-id="5e19d-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="5e19d-392">Expressies voor kenmerktoewijzingen schrijven</span><span class="sxs-lookup"><span data-stu-id="5e19d-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="5e19d-393">Bereikfilters voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="5e19d-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="5e19d-394">Meldingen inrichten van een account</span><span class="sxs-lookup"><span data-stu-id="5e19d-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="5e19d-395">Lijst met zelfstudies over het tooIntegrate SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="5e19d-395">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
