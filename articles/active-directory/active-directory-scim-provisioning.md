---
title: Met behulp van systeem voor identiteitsbeheer van verschillende domeinen automatisch worden ingericht, gebruikers en groepen van Azure Active Directory voor toepassingen | Microsoft Docs
description: Azure Active Directory kunnen automatisch worden ingericht, gebruikers en groepen naar een toepassing of identiteit store die door een webservice is fronted met de interface die is gedefinieerd in de specificatie SCIM protocol
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
ms.openlocfilehash: 91978cee88d55c99bcb63c63cdaf01581ae84668
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="using-system-for-cross-domain-identity-management-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="460c0-103">Systeem voor het identiteitsbeheer van verschillende domeinen gebruiken voor het automatisch inrichten van gebruikers en groepen van Azure Active Directory voor toepassingen</span><span class="sxs-lookup"><span data-stu-id="460c0-103">Using System for Cross-Domain Identity Management to automatically provision users and groups from Azure Active Directory to applications</span></span>

## <a name="overview"></a><span data-ttu-id="460c0-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="460c0-104">Overview</span></span>
<span data-ttu-id="460c0-105">Azure Active Directory (Azure AD) kunnen automatisch worden ingericht, gebruikers en groepen naar een toepassing of identiteit store die door een webservice met de interface is fronted gedefinieerd in de [systeem voor verschillende domeinen Identity Management (SCIM) 2.0-protocol specificatie](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="460c0-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="460c0-106">Azure Active Directory kunt verzenden aanvragen voor het maken, wijzigen of verwijderen toegewezen gebruikers en groepen met de webservice.</span><span class="sxs-lookup"><span data-stu-id="460c0-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span></span> <span data-ttu-id="460c0-107">De webservice kan vervolgens deze aanvragen worden omgezet in bewerkingen op de doel-id-store.</span><span class="sxs-lookup"><span data-stu-id="460c0-107">The web service can then translate those requests into operations on the target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="460c0-108">Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="460c0-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="460c0-109">![][0]
*Afbeelding 1: Inrichting van Azure Active Directory naar een winkel identiteit via een webservice*</span><span class="sxs-lookup"><span data-stu-id="460c0-109">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span></span>

<span data-ttu-id="460c0-110">Deze mogelijkheid kan worden gebruikt in combinatie met de functie 'bring your own app' in Azure AD voor eenmalige aanmelding en automatisch gebruikers inrichten voor toepassingen die op of door een webservice SCIM zijn fronted.</span><span class="sxs-lookup"><span data-stu-id="460c0-110">This capability can be used in conjunction with the “bring your own app” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="460c0-111">Er zijn twee gebruiksvoorbeelden voor using SCIM in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="460c0-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="460c0-112">**Inrichting van gebruikers en groepen van toepassingen die ondersteuning bieden voor SCIM** toepassingen die ondersteuning bieden voor SCIM 2.0 en bearer-tokens van OAuth gebruiken voor verificatie met Azure AD zonder configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="460c0-112">**Provisioning users and groups to applications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="460c0-113">**Maak uw eigen inrichting oplossing voor toepassingen die ondersteuning bieden voor andere inrichting op basis van een API** voor niet-SCIM toepassingen, kunt u een eindpunt SCIM voor de omzetting tussen het eindpunt van de Azure AD SCIM en API biedt ondersteuning voor de gebruiker voor de toepassing maken inrichting.</span><span class="sxs-lookup"><span data-stu-id="460c0-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span></span> <span data-ttu-id="460c0-114">Als u een eindpunt SCIM ontwikkelen, bieden we Common Language Infrastructure (CLI)-bibliotheken en codevoorbeelden die wordt beschreven hoe u met een eindpunt SCIM bieden en vertalen SCIM berichten.</span><span class="sxs-lookup"><span data-stu-id="460c0-114">To help you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="460c0-115">Gebruikers en groepen van toepassingen die ondersteuning bieden voor SCIM inrichten</span><span class="sxs-lookup"><span data-stu-id="460c0-115">Provisioning users and groups to applications that support SCIM</span></span>
<span data-ttu-id="460c0-116">Azure AD kan worden geconfigureerd voor het automatisch inrichten toegewezen gebruikers en groepen van toepassingen die worden geïmplementeerd een [systeem voor verschillende domeinen Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) webservice en OAuth bearer-tokens voor authenticatie geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="460c0-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="460c0-117">Binnen de SCIM 2.0-specificatie toepassingen moeten voldoen aan deze vereisten voldoet:</span><span class="sxs-lookup"><span data-stu-id="460c0-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="460c0-118">Ondersteunt het maken van gebruikers en/of groepen aan de hand van sectie 3.3 van het protocol SCIM.</span><span class="sxs-lookup"><span data-stu-id="460c0-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="460c0-119">Biedt ondersteuning voor gebruikers en/of groepen met patch-aanvragen aan de hand van sectie 3.5.2 van het protocol SCIM wijzigen.</span><span class="sxs-lookup"><span data-stu-id="460c0-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="460c0-120">Ondersteunt het ophalen van een bekende bron volgens punt 3.4.1 van het protocol SCIM.</span><span class="sxs-lookup"><span data-stu-id="460c0-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="460c0-121">Biedt ondersteuning voor gebruikers en/of groepen aan de hand van sectie 3.4.2 van het protocol SCIM opvragen.</span><span class="sxs-lookup"><span data-stu-id="460c0-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="460c0-122">Standaard door externalId aan gebruikers gevraagd en groepen worden opgevraagd met de weergavenaam.</span><span class="sxs-lookup"><span data-stu-id="460c0-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="460c0-123">Ondersteunt het opvragen van de gebruiker door-ID en -beheer volgens sectie 3.4.2 van het protocol SCIM.</span><span class="sxs-lookup"><span data-stu-id="460c0-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="460c0-124">Ondersteunt het uitvoeren van query's groepen door-ID en door een lid aan de hand van sectie 3.4.2 van het protocol SCIM.</span><span class="sxs-lookup"><span data-stu-id="460c0-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="460c0-125">OAuth-bearer-tokens voor autorisatie volgens punt 2.1 van het protocol SCIM accepteert.</span><span class="sxs-lookup"><span data-stu-id="460c0-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="460c0-126">Neem contact op met uw toepassingsprovider of de documentatie van uw toepassingsprovider voor overzichten van compatibiliteit met deze vereisten.</span><span class="sxs-lookup"><span data-stu-id="460c0-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="460c0-127">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="460c0-127">Getting started</span></span>
<span data-ttu-id="460c0-128">Toepassingen die ondersteuning bieden voor het profiel SCIM is beschreven in dit artikel kunnen worden gekoppeld aan Azure Active Directory met de functie 'niet galerie application' in de galerie van Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="460c0-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span></span> <span data-ttu-id="460c0-129">Eenmaal zijn verbonden, voert Azure AD een synchronisatieproces om de 20 minuten waar deze query's van de toepassing SCIM eindpunt voor toegewezen gebruikers en groepen uit en maakt of wijzigt ze volgens de details van de toewijzing.</span><span class="sxs-lookup"><span data-stu-id="460c0-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="460c0-130">**Verbinding met het maken van een toepassing die SCIM ondersteunt:**</span><span class="sxs-lookup"><span data-stu-id="460c0-130">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="460c0-131">Aanmelden bij [de Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="460c0-131">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="460c0-132">Blader naar ** Azure Active Directory > zakelijke toepassingen en selecteer **nieuwe toepassing > alle > niet-galerie toepassing**.</span><span class="sxs-lookup"><span data-stu-id="460c0-132">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="460c0-133">Voer een naam voor uw toepassing en klik op **toevoegen** pictogram van een app-object te maken.</span><span class="sxs-lookup"><span data-stu-id="460c0-133">Enter a name for your application, and click **Add** icon to create an app object.</span></span>
    
  <span data-ttu-id="460c0-134">![][1]
  *Afbeelding 2: Azure AD-toepassingsgalerie*</span><span class="sxs-lookup"><span data-stu-id="460c0-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="460c0-135">Selecteer in het scherm voor het resulterende de **inrichten** tabblad in de linkerkolom staat.</span><span class="sxs-lookup"><span data-stu-id="460c0-135">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="460c0-136">In de **modus inrichting** selecteert u **automatische**.</span><span class="sxs-lookup"><span data-stu-id="460c0-136">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="460c0-137">![][2]
  *Afbeelding 3: Configureren in de Azure portal-inrichting*</span><span class="sxs-lookup"><span data-stu-id="460c0-137">![][2]
*Figure 3: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="460c0-138">In de **Tenant-URL** en voer de URL van de toepassing SCIM eindpunt.</span><span class="sxs-lookup"><span data-stu-id="460c0-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span></span> <span data-ttu-id="460c0-139">Voorbeeld: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="460c0-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="460c0-140">Als het eindpunt SCIM een OAuth bearer-token van een verlener dan Azure AD vereist, kopieert u de vereiste OAuth bearer-token naar de optionele **geheim Token** veld.</span><span class="sxs-lookup"><span data-stu-id="460c0-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="460c0-141">Als dit veld leeg blijft, opgenomen een OAuth-bearer-token uitgegeven vanuit Azure AD bij elke aanvraag met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="460c0-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="460c0-142">Apps die gebruikmaken van Azure AD als een id-provider kunt controleren of deze Azure AD-verleend token.</span><span class="sxs-lookup"><span data-stu-id="460c0-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="460c0-143">Klik op de **testverbinding** knop Azure Active Directory proberen te verbinden met het eindpunt SCIM hebben.</span><span class="sxs-lookup"><span data-stu-id="460c0-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="460c0-144">Als de pogingen mislukken, wordt informatie over de fout wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="460c0-144">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="460c0-145">Als de pogingen tot verbinding maken met de toepassing te voltooien, klikt u op **opslaan** om op te slaan de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="460c0-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="460c0-146">In de **toewijzingen** sectie, zijn er twee sets van selecteerbare Kenmerktoewijzingen: één voor gebruikersobjecten en één voor groepsobjecten.</span><span class="sxs-lookup"><span data-stu-id="460c0-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="460c0-147">Selecteer elke om te controleren van de kenmerken die aan uw app van Azure Active Directory zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="460c0-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="460c0-148">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikers en groepen in uw app voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="460c0-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="460c0-149">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="460c0-149">Select the Save button to commit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="460c0-150">U kunt desgewenst uitschakelen door het uitschakelen van de toewijzing 'groepen' van een groepsobjecten worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="460c0-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span></span> 

11. <span data-ttu-id="460c0-151">Onder **instellingen**, wordt de **bereik** veld wordt gedefinieerd welke gebruikers en groepen worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="460c0-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="460c0-152">Selecteren 'Sync alleen toegewezen gebruikers en groepen' (aanbevolen) synchroniseert alleen gebruikers en groepen die zijn toegewezen de **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="460c0-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="460c0-153">Zodra de configuratie voltooid is, verandert de **inrichting Status** naar **op**.</span><span class="sxs-lookup"><span data-stu-id="460c0-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="460c0-154">Klik op **opslaan** starten van de Azure AD-service inricht.</span><span class="sxs-lookup"><span data-stu-id="460c0-154">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="460c0-155">Als gebruikers en groepen (aanbevolen) synchronisatie alleen worden toegewezen, moet u selecteren de **gebruikers en groepen** tabblad en toewijzen van gebruikers en/of groepen die u wilt synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="460c0-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="460c0-156">Nadat de initiële synchronisatie is gestart, kunt u de **controlelogboeken** tabblad aan de vooruitgang van de monitor, waarin alle acties die worden uitgevoerd door de inrichting van uw app-service.</span><span class="sxs-lookup"><span data-stu-id="460c0-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="460c0-157">Zie voor meer informatie over het lezen van de Azure AD inrichting logboeken [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="460c0-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="460c0-158">De eerste synchronisatie langer duren om uit te voeren dan het volgende wordt gesynchroniseerd, die ongeveer 20 minuten optreden als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="460c0-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="460c0-159">Uw eigen oplossing voor elke toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="460c0-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="460c0-160">Als u een SCIM-webservice die is gekoppeld met Azure Active Directory maakt, kunt u één gebruiker voor eenmalige aanmelding en automatische inrichting voor vrijwel elke toepassing die voorziet in een API-inrichting REST of SOAP-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="460c0-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="460c0-161">Hier ziet u hoe het werkt:</span><span class="sxs-lookup"><span data-stu-id="460c0-161">Here’s how it works:</span></span>

1. <span data-ttu-id="460c0-162">Azure AD levert een algemene language infrastructure-bibliotheek met de naam [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="460c0-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="460c0-163">Systeemintegrators en ontwikkelaars kunnen gebruikmaken van deze bibliotheek maken en implementeren van een SCIM gebaseerde webservice-eindpunt kan verbinding maken met Azure AD voor een toepassingsarchief identiteit.</span><span class="sxs-lookup"><span data-stu-id="460c0-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="460c0-164">Toewijzingen worden geïmplementeerd in de webservice schema voor de gestandaardiseerde toewijzen aan het gebruikersschema en het protocol is vereist voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="460c0-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="460c0-165">De eindpunt-URL is geregistreerd in Azure AD als onderdeel van een aangepaste toepassing in de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="460c0-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="460c0-166">Gebruikers en groepen zijn toegewezen aan deze toepassing in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="460c0-166">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="460c0-167">Bij toewijzing, worden ze in een wachtrij moeten worden gesynchroniseerd naar de doeltoepassing geplaatst.</span><span class="sxs-lookup"><span data-stu-id="460c0-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="460c0-168">Het synchronisatieproces afhandeling van de wachtrij wordt uitgevoerd om de 20 minuten.</span><span class="sxs-lookup"><span data-stu-id="460c0-168">The synchronization process handling the queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="460c0-169">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="460c0-169">Code Samples</span></span>
<span data-ttu-id="460c0-170">Om dit proces eenvoudiger, een reeks [codevoorbeelden](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) zijn opgegeven die een SCIM webservice-eindpunt maken en Demonstreer automatische inrichting.</span><span class="sxs-lookup"><span data-stu-id="460c0-170">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="460c0-171">Een voorbeeld is van een provider die wordt onderhouden door een bestand met de rijen met door komma's gescheiden waarden die gebruikers en groepen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="460c0-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="460c0-172">Het andere type is van een provider die wordt toegepast op de Amazon Web Services Identity and Access Management-service.</span><span class="sxs-lookup"><span data-stu-id="460c0-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="460c0-173">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="460c0-173">**Prerequisites**</span></span>

* <span data-ttu-id="460c0-174">Visual Studio 2013 of hoger</span><span class="sxs-lookup"><span data-stu-id="460c0-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="460c0-175">Azure-SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="460c0-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="460c0-176">Windows-computer die ondersteuning biedt voor de ASP.NET-framework 4.5 moet worden gebruikt als het SCIM-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="460c0-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="460c0-177">Deze machine moet toegankelijk zijn vanuit de cloud</span><span class="sxs-lookup"><span data-stu-id="460c0-177">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="460c0-178">Een Azure-abonnement met een proefabonnement of een gelicentieerde versie van Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="460c0-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="460c0-179">Het voorbeeld Amazon AWS vereist bibliotheken van de [AWS-Toolkit voor Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="460c0-179">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="460c0-180">Zie het Leesmij-bestand met het voorbeeld voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="460c0-180">For more information, see the README file included with the sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="460c0-181">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="460c0-181">Getting Started</span></span>
<span data-ttu-id="460c0-182">De eenvoudigste manier voor het implementeren van een SCIM-eindpunt dat inrichting verzoeken van Azure AD kan accepteren is het bouwen en implementeren van de voorbeeldcode die de ingerichte gebruikers naar een bestand met door komma's gescheiden waarden (CSV levert).</span><span class="sxs-lookup"><span data-stu-id="460c0-182">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="460c0-183">**Een voorbeeld SCIM-eindpunt maken:**</span><span class="sxs-lookup"><span data-stu-id="460c0-183">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="460c0-184">De code voorbeeld downloaden op [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="460c0-184">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="460c0-185">Pak het pakket en plaats het op uw Windows-machine op een locatie zoals C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="460c0-185">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="460c0-186">In deze map, start u de FileProvisioningAgent oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="460c0-186">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="460c0-187">Selecteer **Extra > Library Package Manager > Package Manager Console**, en voer de volgende opdrachten voor het project FileProvisioningAgent omzetten van de oplossing verwijzingen:</span><span class="sxs-lookup"><span data-stu-id="460c0-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningAgent project to resolve the solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="460c0-188">Bouw het project FileProvisioningAgent.</span><span class="sxs-lookup"><span data-stu-id="460c0-188">Build the FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="460c0-189">Start de toepassing van de opdrachtprompt in Windows (als Administrator) en gebruiken de **cd** opdracht om te wijzigen van de directory voor uw **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** de map.</span><span class="sxs-lookup"><span data-stu-id="460c0-189">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="460c0-190">Voer de volgende opdracht, waarbij < ip-adres > vervangt door de IP-adres of domeinnaam de naam van de Windows-computer:</span><span class="sxs-lookup"><span data-stu-id="460c0-190">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="460c0-191">In Windows onder **Windows-instellingen > netwerk- en instellingen voor Internet**, selecteer de **Windows Firewall > instellingen voor geavanceerde**, en maak een **regel voor binnenkomende verbindingen** die kan inkomende toegang tot poort 9000.</span><span class="sxs-lookup"><span data-stu-id="460c0-191">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="460c0-192">Als de Windows-computer zich achter een router, moet de router worden geconfigureerd voor het uitvoeren van Network Access Translation tussen de poort 9000 die wordt blootgesteld aan internet en poort 9000 op de Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="460c0-192">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="460c0-193">Dit is vereist voor Azure AD kunnen toegang krijgen tot dit eindpunt in de cloud.</span><span class="sxs-lookup"><span data-stu-id="460c0-193">This is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="460c0-194">**Het voorbeeld SCIM eindpunt in Azure AD registreren:**</span><span class="sxs-lookup"><span data-stu-id="460c0-194">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="460c0-195">Aanmelden bij [de Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="460c0-195">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="460c0-196">Blader naar ** Azure Active Directory > zakelijke toepassingen en selecteer **nieuwe toepassing > alle > niet-galerie toepassing**.</span><span class="sxs-lookup"><span data-stu-id="460c0-196">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="460c0-197">Voer een naam voor uw toepassing en klik op **toevoegen** pictogram van een app-object te maken.</span><span class="sxs-lookup"><span data-stu-id="460c0-197">Enter a name for your application, and click **Add** icon to create an app object.</span></span> <span data-ttu-id="460c0-198">Het application-object gemaakt is bedoeld om de doel-app u zou inrichten en implementeren van eenmalige aanmelding voor, en niet alleen het eindpunt SCIM vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="460c0-198">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>
4. <span data-ttu-id="460c0-199">Selecteer in het scherm voor het resulterende de **inrichten** tabblad in de linkerkolom staat.</span><span class="sxs-lookup"><span data-stu-id="460c0-199">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="460c0-200">In de **modus inrichting** selecteert u **automatische**.</span><span class="sxs-lookup"><span data-stu-id="460c0-200">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="460c0-201">![][2]
  *Afbeelding 4: Configureren in de Azure portal-inrichting*</span><span class="sxs-lookup"><span data-stu-id="460c0-201">![][2]
*Figure 4: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="460c0-202">In de **Tenant-URL** en voer de beschikbaar gesteld op internet-URL en poort van uw eindpunt SCIM.</span><span class="sxs-lookup"><span data-stu-id="460c0-202">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="460c0-203">Zou dit iets zoals http://testmachine.contoso.com:9000 of http://<ip-address>:9000/, waarbij < ip-adres > internet is blootgesteld IP adres.</span><span class="sxs-lookup"><span data-stu-id="460c0-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
7. <span data-ttu-id="460c0-204">Als het eindpunt SCIM een OAuth bearer-token van een verlener dan Azure AD vereist, kopieert u de vereiste OAuth bearer-token naar de optionele **geheim Token** veld.</span><span class="sxs-lookup"><span data-stu-id="460c0-204">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="460c0-205">Als dit veld leeg laat, wordt Azure AD een OAuth-bearer-token van Azure AD bij elke aanvraag uitgegeven opnemen.</span><span class="sxs-lookup"><span data-stu-id="460c0-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="460c0-206">Apps die gebruikmaken van Azure AD als een id-provider kunt controleren of deze Azure AD-verleend token.</span><span class="sxs-lookup"><span data-stu-id="460c0-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="460c0-207">Klik op de **testverbinding** knop Azure Active Directory proberen te verbinden met het eindpunt SCIM hebben.</span><span class="sxs-lookup"><span data-stu-id="460c0-207">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="460c0-208">Als de pogingen mislukken, wordt informatie over de fout wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="460c0-208">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="460c0-209">Als de pogingen tot verbinding maken met de toepassing te voltooien, klikt u op **opslaan** om op te slaan de beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="460c0-209">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="460c0-210">In de **toewijzingen** sectie, zijn er twee sets van selecteerbare Kenmerktoewijzingen: één voor gebruikersobjecten en één voor groepsobjecten.</span><span class="sxs-lookup"><span data-stu-id="460c0-210">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="460c0-211">Selecteer elke om te controleren van de kenmerken die aan uw app van Azure Active Directory zijn gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="460c0-211">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="460c0-212">De kenmerken die zijn geselecteerd als **overeenkomend** eigenschappen overeenkomen met de gebruikers en groepen in uw app voor update-bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="460c0-212">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="460c0-213">Selecteer de knop Opslaan eventuele wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="460c0-213">Select the Save button to commit any changes.</span></span>
11. <span data-ttu-id="460c0-214">Onder **instellingen**, wordt de **bereik** veld wordt gedefinieerd welke gebruikers en groepen worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="460c0-214">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="460c0-215">Selecteren 'Sync alleen toegewezen gebruikers en groepen' (aanbevolen) synchroniseert alleen gebruikers en groepen die zijn toegewezen de **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="460c0-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="460c0-216">Zodra de configuratie voltooid is, verandert de **inrichting Status** naar **op**.</span><span class="sxs-lookup"><span data-stu-id="460c0-216">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="460c0-217">Klik op **opslaan** starten van de Azure AD-service inricht.</span><span class="sxs-lookup"><span data-stu-id="460c0-217">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="460c0-218">Als gebruikers en groepen (aanbevolen) synchronisatie alleen worden toegewezen, moet u selecteren de **gebruikers en groepen** tabblad en toewijzen van gebruikers en/of groepen die u wilt synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="460c0-218">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="460c0-219">Nadat de initiële synchronisatie is gestart, kunt u de **controlelogboeken** tabblad aan de vooruitgang van de monitor, waarin alle acties die worden uitgevoerd door de inrichting van uw app-service.</span><span class="sxs-lookup"><span data-stu-id="460c0-219">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="460c0-220">Zie voor meer informatie over het lezen van de Azure AD inrichting logboeken [rapportage over automatische account gebruikersaanvragen](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="460c0-220">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="460c0-221">De laatste stap bij het controleren van het voorbeeld is de TargetFile.csv-bestand te openen in de map \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug op uw Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="460c0-221">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="460c0-222">Zodra het inrichtingsproces wordt uitgevoerd, wordt dit bestand bevat de details van alle toegewezen en ingericht gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="460c0-222">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="460c0-223">-Ontwikkelbibliotheken</span><span class="sxs-lookup"><span data-stu-id="460c0-223">Development libraries</span></span>
<span data-ttu-id="460c0-224">Voor het ontwikkelen van uw eigen webservice die aan de specificatie SCIM voldoet eerst raken met de volgende bibliotheken geleverd door Microsoft te helpen het ontwikkelingsproces versnellen:</span><span class="sxs-lookup"><span data-stu-id="460c0-224">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

1. <span data-ttu-id="460c0-225">Algemene Language Infrastructure (CLI) bibliotheken zijn beschikbaar voor gebruik met talen die op basis van die infrastructuur, zoals C#.</span><span class="sxs-lookup"><span data-stu-id="460c0-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="460c0-226">Een van deze bibliotheken [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declareert een interface Microsoft.SystemForCrossDomainIdentityManagement.IProvider, weergegeven in de volgende afbeelding: A ontwikkelaar met behulp van de bibliotheken wilt implementeren die interface met een klasse die algemeen als een provider, kan worden verwezen.</span><span class="sxs-lookup"><span data-stu-id="460c0-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="460c0-227">De tapewisselaars inschakelen de ontwikkelaar voor het implementeren van een webservice die voldoet aan de SCIM-specificatie.</span><span class="sxs-lookup"><span data-stu-id="460c0-227">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span></span> <span data-ttu-id="460c0-228">De webservice kan ofwel worden gehost in Internet Information Services of een uitvoerbaar Common Language Infrastructure-assembly.</span><span class="sxs-lookup"><span data-stu-id="460c0-228">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="460c0-229">Aanvraag wordt omgezet in aanroepen van methoden van de provider, die door de ontwikkelaar zou worden geprogrammeerd bewerkingen uitvoeren op bepaalde identiteit store.</span><span class="sxs-lookup"><span data-stu-id="460c0-229">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="460c0-230">[Express route-handlers](http://expressjs.com/guide/routing.html) zijn beschikbaar voor het parseren van de aanvraag-objecten van een node.js-aanroepen (zoals gedefinieerd door de specificatie SCIM), die aangebracht aan een node.js-web-service.</span><span class="sxs-lookup"><span data-stu-id="460c0-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="460c0-231">Het bouwen van een aangepaste SCIM-eindpunt</span><span class="sxs-lookup"><span data-stu-id="460c0-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="460c0-232">Met behulp van de CLI-bibliotheken, kunnen ontwikkelaars die bibliotheken met hun services in uitvoerbaar Common Language Infrastructure assembly of in Internet Information Services host.</span><span class="sxs-lookup"><span data-stu-id="460c0-232">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="460c0-233">Hier volgt een voorbeeld van code voor het hosten van een service binnen een uitvoerbare assembly, het adres http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="460c0-233">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

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

<span data-ttu-id="460c0-234">Deze service moet een HTTP-adres en de server certificaat voor serververificatie hebben waarvan de basiscertificeringsinstantie het volgende is:</span><span class="sxs-lookup"><span data-stu-id="460c0-234">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span></span> 

* <span data-ttu-id="460c0-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="460c0-235">CNNIC</span></span>
* <span data-ttu-id="460c0-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="460c0-236">Comodo</span></span>
* <span data-ttu-id="460c0-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="460c0-237">CyberTrust</span></span>
* <span data-ttu-id="460c0-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="460c0-238">DigiCert</span></span>
* <span data-ttu-id="460c0-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="460c0-239">GeoTrust</span></span>
* <span data-ttu-id="460c0-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="460c0-240">GlobalSign</span></span>
* <span data-ttu-id="460c0-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="460c0-241">Go Daddy</span></span>
* <span data-ttu-id="460c0-242">VeriSign</span><span class="sxs-lookup"><span data-stu-id="460c0-242">Verisign</span></span>
* <span data-ttu-id="460c0-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="460c0-243">WoSign</span></span>

<span data-ttu-id="460c0-244">Een certificaat voor serververificatie kan worden gebonden aan een poort op een Windows-host met behulp van het hulpprogramma network shell:</span><span class="sxs-lookup"><span data-stu-id="460c0-244">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="460c0-245">De opgegeven waarde voor het argument certhash is hier de vingerafdruk van het certificaat, terwijl de opgegeven waarde voor het argument appid een globally unique identifier is.</span><span class="sxs-lookup"><span data-stu-id="460c0-245">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="460c0-246">Voor het hosten van de Internet Information Services-service, zou een ontwikkelaar een CLA code bibliotheek-assembly bouwen met een klasse met de naam opstarten in de standaardnaamruimte van de assembly.</span><span class="sxs-lookup"><span data-stu-id="460c0-246">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="460c0-247">Hier volgt een voorbeeld van deze klasse:</span><span class="sxs-lookup"><span data-stu-id="460c0-247">Here is a sample of such a class:</span></span> 

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

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="460c0-248">Afhandeling van endpoint-verificatie</span><span class="sxs-lookup"><span data-stu-id="460c0-248">Handling endpoint authentication</span></span>
<span data-ttu-id="460c0-249">Aanvragen van Azure Active Directory bevatten een OAuth 2.0-bearer-token.</span><span class="sxs-lookup"><span data-stu-id="460c0-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="460c0-250">Alle services die de aanvraag ontvangt, moet de verlener als Azure Active Directory namens de verwachte Azure Active Directory-tenant voor toegang tot de webservice Azure Active Directory Graph verifiëren.</span><span class="sxs-lookup"><span data-stu-id="460c0-250">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="460c0-251">In het token de certificaatverlener die wordt geïdentificeerd door een claim iss, zoals 'iss': 'https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/'.</span><span class="sxs-lookup"><span data-stu-id="460c0-251">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="460c0-252">In dit voorbeeld wordt het basisadres van de claimwaarde https://sts.windows.net, identificeert Azure Active Directory als de verlener terwijl het segment relatief adres, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is de unieke id van de Azure Active Directory tenant namens die het token is uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="460c0-252">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="460c0-253">Als het token is uitgegeven voor toegang tot de Azure Active Directory Graph-webservice, klikt u vervolgens moet de id van die service, 00000002-0000-0000-c000-000000000000, de waarde van het token aud claim.</span><span class="sxs-lookup"><span data-stu-id="460c0-253">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="460c0-254">Ontwikkelaars met behulp van de bibliotheken CLA is geleverd door Microsoft voor het bouwen van een service SCIM kunnen verifiëren aanvragen van Azure Active Directory met het pakket Microsoft.Owin.Security.ActiveDirectory met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="460c0-254">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="460c0-255">In een provider, door de eigenschap Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior te implementeren door het retourneren van een methode om te worden aangeroepen wanneer de service wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="460c0-255">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

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

2. <span data-ttu-id="460c0-256">De volgende code toevoegen aan deze methode om een aanvraag aan een van de service-eindpunten die zijn geverifieerd als een token dat is uitgegeven door Azure Active Directory namens een tenant opgegeven voor toegang tot de webservice Azure AD Graph voorzien:</span><span class="sxs-lookup"><span data-stu-id="460c0-256">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span></span> 

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
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="460c0-257">Schema voor gebruikers en groepen</span><span class="sxs-lookup"><span data-stu-id="460c0-257">User and group schema</span></span>
<span data-ttu-id="460c0-258">Azure Active Directory kunnen twee soorten resources met webservices SCIM inrichten.</span><span class="sxs-lookup"><span data-stu-id="460c0-258">Azure Active Directory can provision two types of resources to SCIM web services.</span></span>  <span data-ttu-id="460c0-259">Deze typen resources zijn gebruikers en groepen.</span><span class="sxs-lookup"><span data-stu-id="460c0-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="460c0-260">User-bronnen worden geïdentificeerd door de schema-id en urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, die is opgenomen in deze specificatie van het protocol: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="460c0-260">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="460c0-261">De standaardtoewijzing van de kenmerken van gebruikers in Azure Active Directory in de kenmerken van resources urn: ietf:params:scim:schemas:extension:enterprise:2.0:User hieronder vindt u in de tabel 1.</span><span class="sxs-lookup"><span data-stu-id="460c0-261">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="460c0-262">Groep resources worden geïdentificeerd door de schema-id en http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="460c0-262">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="460c0-263">Tabel 2 hieronder bevat de standaardtoewijzing van de kenmerken van groepen in Azure Active Directory op de kenmerken van http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span><span class="sxs-lookup"><span data-stu-id="460c0-263">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="460c0-264">Tabel 1: Standaard Gebruikerskoppeling kenmerk</span><span class="sxs-lookup"><span data-stu-id="460c0-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="460c0-265">Azure Active Directory-gebruiker</span><span class="sxs-lookup"><span data-stu-id="460c0-265">Azure Active Directory user</span></span> | <span data-ttu-id="460c0-266">urn: ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="460c0-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="460c0-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="460c0-267">IsSoftDeleted</span></span> |<span data-ttu-id="460c0-268">Actieve</span><span class="sxs-lookup"><span data-stu-id="460c0-268">active</span></span> |
| <span data-ttu-id="460c0-269">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="460c0-269">displayName</span></span> |<span data-ttu-id="460c0-270">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="460c0-270">displayName</span></span> |
| <span data-ttu-id="460c0-271">Fax TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="460c0-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="460c0-272">phoneNumbers type eq 'fax'.value</span><span class="sxs-lookup"><span data-stu-id="460c0-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="460c0-273">Voornaam</span><span class="sxs-lookup"><span data-stu-id="460c0-273">givenName</span></span> |<span data-ttu-id="460c0-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="460c0-274">name.givenName</span></span> |
| <span data-ttu-id="460c0-275">Functie</span><span class="sxs-lookup"><span data-stu-id="460c0-275">jobTitle</span></span> |<span data-ttu-id="460c0-276">titel</span><span class="sxs-lookup"><span data-stu-id="460c0-276">title</span></span> |
| <span data-ttu-id="460c0-277">E-mail</span><span class="sxs-lookup"><span data-stu-id="460c0-277">mail</span></span> |<span data-ttu-id="460c0-278">e-mailberichten type eq 'werk'.value</span><span class="sxs-lookup"><span data-stu-id="460c0-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="460c0-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="460c0-279">mailNickname</span></span> |<span data-ttu-id="460c0-280">externalId</span><span class="sxs-lookup"><span data-stu-id="460c0-280">externalId</span></span> |
| <span data-ttu-id="460c0-281">Manager</span><span class="sxs-lookup"><span data-stu-id="460c0-281">manager</span></span> |<span data-ttu-id="460c0-282">Manager</span><span class="sxs-lookup"><span data-stu-id="460c0-282">manager</span></span> |
| <span data-ttu-id="460c0-283">mobiele</span><span class="sxs-lookup"><span data-stu-id="460c0-283">mobile</span></span> |<span data-ttu-id="460c0-284">phoneNumbers type eq 'mobiel'.value</span><span class="sxs-lookup"><span data-stu-id="460c0-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="460c0-285">object-id</span><span class="sxs-lookup"><span data-stu-id="460c0-285">objectId</span></span> |<span data-ttu-id="460c0-286">id</span><span class="sxs-lookup"><span data-stu-id="460c0-286">id</span></span> |
| <span data-ttu-id="460c0-287">Postcode</span><span class="sxs-lookup"><span data-stu-id="460c0-287">postalCode</span></span> |<span data-ttu-id="460c0-288">adressen type eq 'werk'.postalCode</span><span class="sxs-lookup"><span data-stu-id="460c0-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="460c0-289">proxy-adressen</span><span class="sxs-lookup"><span data-stu-id="460c0-289">proxy-Addresses</span></span> |<span data-ttu-id="460c0-290">e-mailberichten [Geef eq 'andere']. Waarde</span><span class="sxs-lookup"><span data-stu-id="460c0-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="460c0-291">fysieke-levering-OfficeName</span><span class="sxs-lookup"><span data-stu-id="460c0-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="460c0-292">adressen [Geef eq 'andere']. Indeling</span><span class="sxs-lookup"><span data-stu-id="460c0-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="460c0-293">StreetAddress</span><span class="sxs-lookup"><span data-stu-id="460c0-293">streetAddress</span></span> |<span data-ttu-id="460c0-294">adressen type eq 'werk'.streetAddress</span><span class="sxs-lookup"><span data-stu-id="460c0-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="460c0-295">Achternaam</span><span class="sxs-lookup"><span data-stu-id="460c0-295">surname</span></span> |<span data-ttu-id="460c0-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="460c0-296">name.familyName</span></span> |
| <span data-ttu-id="460c0-297">Telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="460c0-297">telephone-Number</span></span> |<span data-ttu-id="460c0-298">phoneNumbers type eq 'werk'.value</span><span class="sxs-lookup"><span data-stu-id="460c0-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="460c0-299">primaire gebruiker-naam</span><span class="sxs-lookup"><span data-stu-id="460c0-299">user-PrincipalName</span></span> |<span data-ttu-id="460c0-300">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="460c0-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="460c0-301">Tabel 2: Standaard kenmerk apparaatgroeptoewijzing</span><span class="sxs-lookup"><span data-stu-id="460c0-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="460c0-302">Azure Active Directory-groep</span><span class="sxs-lookup"><span data-stu-id="460c0-302">Azure Active Directory group</span></span> | <span data-ttu-id="460c0-303">http://schemas.Microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="460c0-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="460c0-304">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="460c0-304">displayName</span></span> |<span data-ttu-id="460c0-305">externalId</span><span class="sxs-lookup"><span data-stu-id="460c0-305">externalId</span></span> |
| <span data-ttu-id="460c0-306">E-mail</span><span class="sxs-lookup"><span data-stu-id="460c0-306">mail</span></span> |<span data-ttu-id="460c0-307">e-mailberichten type eq 'werk'.value</span><span class="sxs-lookup"><span data-stu-id="460c0-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="460c0-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="460c0-308">mailNickname</span></span> |<span data-ttu-id="460c0-309">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="460c0-309">displayName</span></span> |
| <span data-ttu-id="460c0-310">Leden</span><span class="sxs-lookup"><span data-stu-id="460c0-310">members</span></span> |<span data-ttu-id="460c0-311">Leden</span><span class="sxs-lookup"><span data-stu-id="460c0-311">members</span></span> |
| <span data-ttu-id="460c0-312">object-id</span><span class="sxs-lookup"><span data-stu-id="460c0-312">objectId</span></span> |<span data-ttu-id="460c0-313">id</span><span class="sxs-lookup"><span data-stu-id="460c0-313">id</span></span> |
| <span data-ttu-id="460c0-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="460c0-314">proxyAddresses</span></span> |<span data-ttu-id="460c0-315">e-mailberichten [Geef eq 'andere']. Waarde</span><span class="sxs-lookup"><span data-stu-id="460c0-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="460c0-316">Gebruikers inrichten en de inrichting</span><span class="sxs-lookup"><span data-stu-id="460c0-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="460c0-317">De volgende afbeelding ziet u de Azure Active Directory voor het beheren van de levenscyclus van een gebruiker in een andere identiteit store verzendt naar een service SCIM berichten.</span><span class="sxs-lookup"><span data-stu-id="460c0-317">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span></span> <span data-ttu-id="460c0-318">Het diagram toont ook hoe een SCIM service geïmplementeerd met behulp van de CLI-bibliotheken geleverd door Microsoft voor het bouwen dat dergelijke services deze aanvragen vertalen in aanroepen van de methoden van een provider.</span><span class="sxs-lookup"><span data-stu-id="460c0-318">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="460c0-319">![][4]
*Afbeelding 5: Gebruikers inrichten en de inrichting reeks*</span><span class="sxs-lookup"><span data-stu-id="460c0-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="460c0-320">Azure Active Directory query op de service voor een gebruiker met een externalId-kenmerkwaarde die overeenkomt met de waarde van het mailNickname-kenmerk van een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="460c0-320">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="460c0-321">De query wordt uitgedrukt als een aanvraag Hypertext Transfer Protocol (HTTP) zoals dit voorbeeld waarin jyoung een voorbeeld van een mailNickname van een gebruiker in Azure Active Directory is:</span><span class="sxs-lookup"><span data-stu-id="460c0-321">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="460c0-322">Als de service is gebouwd met behulp van de Common Language Infrastructure-bibliotheken voor het implementeren van services SCIM door Microsoft geleverd, wordt de aanvraag omgezet in een aanroep van de Query-methode van de service provider.</span><span class="sxs-lookup"><span data-stu-id="460c0-322">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="460c0-323">Dit is de handtekening van deze methode:</span><span class="sxs-lookup"><span data-stu-id="460c0-323">Here is the signature of that method:</span></span> 
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
  <span data-ttu-id="460c0-324">Hier volgt de definitie van de interface Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters:</span><span class="sxs-lookup"><span data-stu-id="460c0-324">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
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
  <span data-ttu-id="460c0-325">In het volgende voorbeeld van een query voor een gebruiker met een opgegeven waarde voor het kenmerk externalId zijn de waarden van de argumenten doorgegeven aan de Query-methode:</span><span class="sxs-lookup"><span data-stu-id="460c0-325">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span></span> 
  * <span data-ttu-id="460c0-326">parameters. AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="460c0-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="460c0-327">parameters. AlternateFilters.ElementAt(0). AttributePath: 'externalId'</span><span class="sxs-lookup"><span data-stu-id="460c0-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="460c0-328">parameters. AlternateFilters.ElementAt(0). Vergelijkingsoperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="460c0-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="460c0-329">parameters. AlternateFilter.ElementAt(0). ComparisonValue: 'jyoung'</span><span class="sxs-lookup"><span data-stu-id="460c0-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="460c0-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin. RequestId"]</span><span class="sxs-lookup"><span data-stu-id="460c0-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="460c0-331">Als het antwoord op een query met de webservice voor een gebruiker met een kenmerkwaarde externalId die overeenkomt met de waarde van het mailNickname-kenmerk van een gebruiker niet alle gebruikers, klikt u vervolgens Azure Active Directory-aanvragen dat de service een gebruiker die overeenkomt met het inrichten in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="460c0-331">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="460c0-332">Hier volgt een voorbeeld van een aanvraag:</span><span class="sxs-lookup"><span data-stu-id="460c0-332">Here is an example of such a request:</span></span> 
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
  <span data-ttu-id="460c0-333">De Common Language Infrastructure-bibliotheken geleverd door Microsoft voor het implementeren van services SCIM zou die aanvraag vertalen naar een aanroep van de methode voor maken van de service provider.</span><span class="sxs-lookup"><span data-stu-id="460c0-333">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="460c0-334">De methode Create heeft deze handtekening:</span><span class="sxs-lookup"><span data-stu-id="460c0-334">The Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="460c0-335">De waarde van de resource-argument is in een aanvraag voor het inrichten van een gebruiker een exemplaar van de Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="460c0-335">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="460c0-336">Core2EnterpriseUser klasse is gedefinieerd in de bibliotheek Microsoft.SystemForCrossDomainIdentityManagement.Schemas.</span><span class="sxs-lookup"><span data-stu-id="460c0-336">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="460c0-337">Als de aanvraag voor het inrichten van de gebruiker is gelukt, wordt de implementatie van de methode verwacht een exemplaar van de Microsoft.SystemForCrossDomainIdentityManagement retourneren.</span><span class="sxs-lookup"><span data-stu-id="460c0-337">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="460c0-338">Core2EnterpriseUser klasse met de waarde van de id-eigenschap ingesteld op de unieke id van de nieuw ingerichte gebruiker.</span><span class="sxs-lookup"><span data-stu-id="460c0-338">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span></span>  

3. <span data-ttu-id="460c0-339">Voor het bijwerken van een gebruiker bekend in een archief fronted door een SCIM is Azure Active Directory wordt uitgevoerd door de huidige status van die gebruiker vraagt van de service met een aanvraag, zoals:</span><span class="sxs-lookup"><span data-stu-id="460c0-339">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="460c0-340">De aanvraag wordt in een service gemaakt met de Common Language Infrastructure-bibliotheken geleverd door Microsoft voor het implementeren van services SCIM wordt omgezet in een aanroep van de methode ophalen van de service provider.</span><span class="sxs-lookup"><span data-stu-id="460c0-340">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="460c0-341">Dit is de handtekening van de methode ophalen:</span><span class="sxs-lookup"><span data-stu-id="460c0-341">Here is the signature of the Retrieve method:</span></span> 
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
  <span data-ttu-id="460c0-342">In het voorbeeld van een aanvraag voor het ophalen van de huidige status van een gebruiker zijn de waarden van de eigenschappen van het object dat is opgegeven als de waarde van het argument parameters als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="460c0-342">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="460c0-343">-ID: '54D382A4-2050-4C03-94D1-E769F1D15682'</span><span class="sxs-lookup"><span data-stu-id="460c0-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="460c0-344">SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'</span><span class="sxs-lookup"><span data-stu-id="460c0-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="460c0-345">Als een verwijzingskenmerk is worden bijgewerkt, wordt de service om te bepalen of de huidige waarde van het verwijzingskenmerk in de store identiteit op de al fronted door de service Azure Active Directory een query overeenkomt met de waarde van dit kenmerk in Azure Active De map.</span><span class="sxs-lookup"><span data-stu-id="460c0-345">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="460c0-346">Voor gebruikers is het enige kenmerk waarvan de huidige waarde op deze manier wordt opgevraagd het kenmerk manager.</span><span class="sxs-lookup"><span data-stu-id="460c0-346">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span></span> <span data-ttu-id="460c0-347">Hier volgt een voorbeeld van een aanvraag om te bepalen of het kenmerk manager van een bepaalde gebruiker-object een bepaalde waarde heeft:</span><span class="sxs-lookup"><span data-stu-id="460c0-347">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="460c0-348">De waarde van de queryparameter kenmerken id, betekent dat als een gebruikersobject aanwezig is die voldoet aan de expressie die is opgegeven als de waarde van de queryparameter filter vervolgens de service moet reageren met een urn: ietf:params:scim:schemas:core:2.0:User of urn: ietf:params:scim:schemas:extension:enterprise:2.0:User bron, met inbegrip van alleen de waarde van kenmerk van de bron-id.</span><span class="sxs-lookup"><span data-stu-id="460c0-348">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span></span>  <span data-ttu-id="460c0-349">De waarde van de **id** kenmerk bekend is dat de aanvrager.</span><span class="sxs-lookup"><span data-stu-id="460c0-349">The value of the **id** attribute is known to the requestor.</span></span> <span data-ttu-id="460c0-350">Het is opgenomen in de waarde van de queryparameter filter; het doel van deze vragen is daadwerkelijk om aan te vragen een minimale representatie van een resource die voldoen aan de filterexpressie een indicatie van het al dan niet een dergelijk object bestaat.</span><span class="sxs-lookup"><span data-stu-id="460c0-350">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="460c0-351">Als de service is gebouwd met behulp van de Common Language Infrastructure-bibliotheken voor het implementeren van services SCIM door Microsoft geleverd, wordt de aanvraag omgezet in een aanroep van de Query-methode van de service provider.</span><span class="sxs-lookup"><span data-stu-id="460c0-351">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span> <span data-ttu-id="460c0-352">De waarde van de eigenschappen van het object dat is opgegeven als de waarde van het argument parameters zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="460c0-352">The value of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="460c0-353">parameters. AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="460c0-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="460c0-354">parameters. AlternateFilters.ElementAt(x). AttributePath: 'id'</span><span class="sxs-lookup"><span data-stu-id="460c0-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="460c0-355">parameters. AlternateFilters.ElementAt(x). Vergelijkingsoperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="460c0-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="460c0-356">parameters. AlternateFilter.ElementAt(x). ComparisonValue: '54D382A4-2050-4C03-94D1-E769F1D15682'</span><span class="sxs-lookup"><span data-stu-id="460c0-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="460c0-357">parameters. AlternateFilters.ElementAt(y). AttributePath: 'manager'</span><span class="sxs-lookup"><span data-stu-id="460c0-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="460c0-358">parameters. AlternateFilters.ElementAt(y). Vergelijkingsoperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="460c0-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="460c0-359">parameters. AlternateFilter.ElementAt(y). ComparisonValue: '2819c223-7f76-453a-919d-413861904646'</span><span class="sxs-lookup"><span data-stu-id="460c0-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="460c0-360">parameters. RequestedAttributePaths.ElementAt(0): 'id'</span><span class="sxs-lookup"><span data-stu-id="460c0-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="460c0-361">parameters. SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'</span><span class="sxs-lookup"><span data-stu-id="460c0-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="460c0-362">Hier de waarde van de x-index kan niet 0 en 1, is de waarde van de index y mogelijk of de waarde van x mogelijk 1 en de waarde van y kan zijn ingesteld op 0, afhankelijk van de volgorde van de expressies van de queryparameter filter.</span><span class="sxs-lookup"><span data-stu-id="460c0-362">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

5. <span data-ttu-id="460c0-363">Hier volgt een voorbeeld van een aanvraag van Azure Active Directory een SCIM-service voor het bijwerken van een gebruiker:</span><span class="sxs-lookup"><span data-stu-id="460c0-363">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 
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
  <span data-ttu-id="460c0-364">De Microsoft Common Language Infrastructure-bibliotheken voor het implementeren van services SCIM wordt de aanvraag worden omgezet in een aanroep van de methode Update van de service provider.</span><span class="sxs-lookup"><span data-stu-id="460c0-364">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span> <span data-ttu-id="460c0-365">Dit is de handtekening van de methode Update:</span><span class="sxs-lookup"><span data-stu-id="460c0-365">Here is the signature of the Update method:</span></span> 
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
    <span data-ttu-id="460c0-366">In het voorbeeld van een aanvraag voor het bijwerken van een gebruiker heeft het object dat is opgegeven als de waarde van de patch-argument waarden van deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="460c0-366">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="460c0-367">ResourceIdentifier.Identifier: '54D382A4-2050-4C03-94D1-E769F1D15682'</span><span class="sxs-lookup"><span data-stu-id="460c0-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="460c0-368">ResourceIdentifier.SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'</span><span class="sxs-lookup"><span data-stu-id="460c0-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="460c0-369">(PatchRequest als PatchRequest2). Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="460c0-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="460c0-370">(PatchRequest als PatchRequest2). Operations.ElementAt(0). OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="460c0-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="460c0-371">(PatchRequest als PatchRequest2). Operations.ElementAt(0). Path.AttributePath: 'manager'</span><span class="sxs-lookup"><span data-stu-id="460c0-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="460c0-372">(PatchRequest als PatchRequest2). Operations.ElementAt(0). Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="460c0-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="460c0-373">(PatchRequest als PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Verwijzing: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="460c0-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="460c0-374">(PatchRequest als PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Waarde: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="460c0-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="460c0-375">Voor het inrichten van een gebruiker uit een identiteit store fronted door een service SCIM ongedaan, verzendt Azure AD een aanvraag op, zoals:</span><span class="sxs-lookup"><span data-stu-id="460c0-375">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="460c0-376">Als de service is gebouwd met behulp van de Common Language Infrastructure-bibliotheken voor het implementeren van services SCIM door Microsoft geleverd, wordt de aanvraag omgezet in een aanroep van de Delete-methode van de service provider.</span><span class="sxs-lookup"><span data-stu-id="460c0-376">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="460c0-377">Deze methode heeft deze handtekening:</span><span class="sxs-lookup"><span data-stu-id="460c0-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="460c0-378">Het object dat is opgegeven als de waarde van het argument resourceIdentifier heeft waarden van deze eigenschappen in het voorbeeld van een aanvraag voor het inrichten van een gebruiker ongedaan:</span><span class="sxs-lookup"><span data-stu-id="460c0-378">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span></span> 
  
  * <span data-ttu-id="460c0-379">ResourceIdentifier.Identifier: '54D382A4-2050-4C03-94D1-E769F1D15682'</span><span class="sxs-lookup"><span data-stu-id="460c0-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="460c0-380">ResourceIdentifier.SchemaIdentifier: 'urn: ietf:params:scim:schemas:extension:enterprise:2.0:User'</span><span class="sxs-lookup"><span data-stu-id="460c0-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="460c0-381">Groep inrichting en ongedaan inrichten</span><span class="sxs-lookup"><span data-stu-id="460c0-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="460c0-382">De volgende afbeelding ziet u de berichten dat Azure AcD naar een service SCIM verzendt voor het beheren van de levenscyclus van een groep in een andere identiteit store.</span><span class="sxs-lookup"><span data-stu-id="460c0-382">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="460c0-383">Deze berichten verschillen van de berichten die betrekking hebben op gebruikers op drie manieren:</span><span class="sxs-lookup"><span data-stu-id="460c0-383">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="460c0-384">Het schema van een bron wordt geïdentificeerd als http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="460c0-384">The schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="460c0-385">Aanvragen voor het ophalen van groepen kunt u bepalen dat het kenmerk leden moeten worden uitgesloten van een resource in het antwoord op de aanvraag is.</span><span class="sxs-lookup"><span data-stu-id="460c0-385">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="460c0-386">Aanvragen om te bepalen of een verwijzingskenmerk een bepaalde waarde zijn aanvragen over het kenmerk leden.</span><span class="sxs-lookup"><span data-stu-id="460c0-386">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span></span>  

<span data-ttu-id="460c0-387">![][5]
*Afbeelding 6: Inrichting en ongedaan inrichting sequence groeperen*</span><span class="sxs-lookup"><span data-stu-id="460c0-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="460c0-388">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="460c0-388">Related articles</span></span>
* <span data-ttu-id="460c0-389">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="460c0-389">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="460c0-390">Automatisch gebruikers inrichten/opheffen van inrichting tot SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="460c0-390">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="460c0-391">Kenmerktoewijzingen voor gebruikers inrichten aanpassen</span><span class="sxs-lookup"><span data-stu-id="460c0-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="460c0-392">Expressies voor kenmerktoewijzingen schrijven</span><span class="sxs-lookup"><span data-stu-id="460c0-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="460c0-393">Bereikfilters voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="460c0-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="460c0-394">Meldingen inrichten van een account</span><span class="sxs-lookup"><span data-stu-id="460c0-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="460c0-395">Lijst met zelfstudies over het integreren van SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="460c0-395">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
