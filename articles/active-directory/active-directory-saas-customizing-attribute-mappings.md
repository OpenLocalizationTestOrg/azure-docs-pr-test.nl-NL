---
title: Azure AD-kenmerktoewijzingen aaaCustomizing | Microsoft Docs
description: Meer informatie over welke kenmerktoewijzingen voor SaaS-apps in Azure Active Directory zijn hoe u kunt deze aanpassen tooaddress uw bedrijf nodig heeft.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="a719b-103">Gebruikers inrichten kenmerktoewijzingen voor SaaS-toepassingen in Azure Active Directory aanpassen</span><span class="sxs-lookup"><span data-stu-id="a719b-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="a719b-104">Microsoft Azure AD biedt ondersteuning voor gebruikers inrichten toothird derden SaaS-toepassingen zoals Salesforce en Google Apps.</span><span class="sxs-lookup"><span data-stu-id="a719b-104">Microsoft Azure AD provides support for user provisioning toothird-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="a719b-105">Als er gebruikers inrichten voor een SaaS-toepassing van derden is ingeschakeld, bepaalt hello Azure Management Portal de kenmerkwaarden weer in de vorm van een configuratie met de naam "kenmerk wordt toegewezen."</span><span class="sxs-lookup"><span data-stu-id="a719b-105">If you have user provisioning for a third-party SaaS application enabled, hello Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="a719b-106">Er is een set vooraf geconfigureerde kenmerktoewijzingen tussen Azure AD-gebruikersobjecten en gebruikersobjecten van elke SaaS-app.</span><span class="sxs-lookup"><span data-stu-id="a719b-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="a719b-107">Sommige apps beheren andere soorten objecten, zoals groepen of contactpersonen.</span><span class="sxs-lookup"><span data-stu-id="a719b-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="a719b-108">Hallo kenmerk standaardtoewijzingen volgens tooyour bedrijfsbehoeften, kunt u aanpassen.</span><span class="sxs-lookup"><span data-stu-id="a719b-108">You can customize hello default attribute mappings according tooyour business needs.</span></span> <span data-ttu-id="a719b-109">Dit houdt in dat u kunt wijzigen of verwijderen van bestaande kenmerktoewijzingen of nieuwe kenmerktoewijzingen maken.</span><span class="sxs-lookup"><span data-stu-id="a719b-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="a719b-110">In hello Azure AD-portal, opent u deze functie door te klikken op een **toewijzingen** configuratie onder **inrichten** in Hallo **beheren** gedeelte van een  **Bedrijfstoepassing**.</span><span class="sxs-lookup"><span data-stu-id="a719b-110">In hello Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in hello **Manage** section of an **Enterprise application**.</span></span>


![SalesForce][5] 

<span data-ttu-id="a719b-112">Te klikken op een **toewijzingen** configuratie, geopend Hallo gerelateerde **kenmerk toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="a719b-112">Clicking a **Mappings** configuration, opens hello related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="a719b-113">Er zijn kenmerktoewijzingen die door een SaaS-toepassing toofunction correct vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="a719b-113">There are attribute mappings that are required by a SaaS application toofunction correctly.</span></span> <span data-ttu-id="a719b-114">Voor de vereiste kenmerken Hallo **verwijderen** functie is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="a719b-114">For required attributes, hello **Delete** feature is unavailable.</span></span>


![SalesForce][6]  

<span data-ttu-id="a719b-116">Hallo bovenstaande voorbeeld ziet u dat Hallo **gebruikersnaam** kenmerk van een beheerd object in Salesforce is gevuld met Hallo **userPrincipalName** waarde van hello Azure Active Directory-Object gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a719b-116">In hello example above, you can see that hello **Username** attribute of a managed object in Salesforce is populated with hello **userPrincipalName** value of hello linked Azure Active Directory Object.</span></span>

<span data-ttu-id="a719b-117">U kunt bestaande **kenmerktoewijzingen** door te klikken op een toewijzing.</span><span class="sxs-lookup"><span data-stu-id="a719b-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="a719b-118">Hiermee opent u Hallo **kenmerk bewerken** blade.</span><span class="sxs-lookup"><span data-stu-id="a719b-118">This opens hello **Edit Attribute** blade.</span></span>

![SalesForce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="a719b-120">Kenmerk typen toewijzing</span><span class="sxs-lookup"><span data-stu-id="a719b-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="a719b-121">Met kenmerktoewijzingen, kunt u bepalen hoe kenmerken worden ingevuld in een SaaS-toepassing van derden.</span><span class="sxs-lookup"><span data-stu-id="a719b-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="a719b-122">Er zijn vier verschillende toewijzingstypen ondersteund:</span><span class="sxs-lookup"><span data-stu-id="a719b-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="a719b-123">**Directe** – Hallo target-kenmerk is gevuld met de waarde van een kenmerk van het gekoppelde object Hallo Hallo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a719b-123">**Direct** – hello target attribute is populated with hello value of an attribute of hello linked object in Azure AD.</span></span>
* <span data-ttu-id="a719b-124">**Constante** – Hallo target-kenmerk is gevuld met een specifieke tekenreeks die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a719b-124">**Constant** – hello target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="a719b-125">**Expressie** -Hallo target-kenmerk is ingevuld op basis van Hallo resultaat van een script-achtige-expressie.</span><span class="sxs-lookup"><span data-stu-id="a719b-125">**Expression** - hello target attribute is populated based on hello result of a script-like expression.</span></span> 
  <span data-ttu-id="a719b-126">Zie voor meer informatie [schrijven expressies voor kenmerktoewijzingen in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="a719b-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="a719b-127">**Geen** -Hallo doelkenmerk blijft ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a719b-127">**None** - hello target attribute is left unmodified.</span></span> <span data-ttu-id="a719b-128">Echter, als Hallo doelkenmerk ooit leeg is, wordt dit ingevuld met Hallo standaardwaarde die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="a719b-128">However, if hello target attribute is ever empty, it is populated with hello Default value that you specify.</span></span>

<span data-ttu-id="a719b-129">In de toevoeging toothese vier eenvoudige kenmerk toewijzingstypen aangepaste kenmerktoewijzingen Hallo concept van een optionele ondersteuning **standaard** waarde toewijzing.</span><span class="sxs-lookup"><span data-stu-id="a719b-129">In addition toothese four basic attribute mapping types, custom attribute mappings support hello concept of an optional **default** value assignment.</span></span> <span data-ttu-id="a719b-130">toewijzing van Hallo standaard waarde zorgt ervoor dat een target-kenmerk is gevuld met een waarde als er geen waarde in Azure AD, noch op Hallo-doelobject.</span><span class="sxs-lookup"><span data-stu-id="a719b-130">hello default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on hello target object.</span></span> <span data-ttu-id="a719b-131">meest voorkomende Hallo-configuratie is dit lege tooleave.</span><span class="sxs-lookup"><span data-stu-id="a719b-131">hello most common configuration is tooleave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="a719b-132">Understanding toewijzing kenmerkeigenschappen</span><span class="sxs-lookup"><span data-stu-id="a719b-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="a719b-133">In de vorige sectie hello, hebt u al geïntroduceerd toohello kenmerk toewijzing type-eigenschap zijn.</span><span class="sxs-lookup"><span data-stu-id="a719b-133">In hello previous section, you have already been introduced toohello attribute mapping type property.</span></span>
<span data-ttu-id="a719b-134">Bij toevoeging toothis eigenschap ondersteunen kenmerktoewijzingen ook Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="a719b-134">In addition toothis property, attribute mappings do also support hello following attributes:</span></span>

- <span data-ttu-id="a719b-135">**Bronkenmerk** -Hallo gebruikerskenmerk uit het bronsysteem hello (bijvoorbeeld: Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a719b-135">**Source attribute** - hello user attribute from hello source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="a719b-136">**Doelkenmerk** – Hallo gebruikerskenmerk in het doelsysteem hello (bijvoorbeeld: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="a719b-136">**Target attribute** – hello user attribute in hello target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="a719b-137">**Overeen met objecten met behulp van dit kenmerk** : of deze toewijzing moet worden gebruikt of niet toouniquely gebruikers tussen de bron en doel systemen Hallo identificeren.</span><span class="sxs-lookup"><span data-stu-id="a719b-137">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between hello source and target systems.</span></span> <span data-ttu-id="a719b-138">Dit is standaard ingesteld op Hallo userPrincipalName of e-mailkenmerk in Azure AD, die normaal gesproken tooa gebruikersnaam veld in een doeltoepassing toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a719b-138">This is typically set on hello userPrincipalName or mail attribute in Azure AD, which is typically mapped tooa username field in a target application.</span></span>
- <span data-ttu-id="a719b-139">**Overeenkomende voorrang** – meerdere overeenkomende kenmerken kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a719b-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="a719b-140">Wanneer er meerdere, moeten ze worden geëvalueerd in Hallo volgorde gedefinieerd door dit veld.</span><span class="sxs-lookup"><span data-stu-id="a719b-140">When there are multiple, they are evaluated in hello order defined by this field.</span></span> <span data-ttu-id="a719b-141">Als een overeenkomst is gevonden, er is geen verdere overeenkomende kenmerken worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="a719b-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="a719b-142">**Deze toewijzing is van toepassing**</span><span class="sxs-lookup"><span data-stu-id="a719b-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="a719b-143">**Altijd** : deze toewijzing is van toepassing op beide maken van een gebruikersaccount en acties bijwerken</span><span class="sxs-lookup"><span data-stu-id="a719b-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="a719b-144">**Alleen tijdens het maken van** -deze toewijzing is van toepassing alleen op gebruikersacties maken</span><span class="sxs-lookup"><span data-stu-id="a719b-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="a719b-145">Wat u moet weten</span><span class="sxs-lookup"><span data-stu-id="a719b-145">What you should know</span></span>

<span data-ttu-id="a719b-146">Microsoft Azure AD biedt een efficiënte implementatie van een synchronisatieproces.</span><span class="sxs-lookup"><span data-stu-id="a719b-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="a719b-147">In een omgeving met geïnitialiseerde worden alleen objecten die moet worden bijgewerkt verwerkt tijdens een synchronisatiecyclus.</span><span class="sxs-lookup"><span data-stu-id="a719b-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="a719b-148">Kenmerktoewijzingen bijwerken, heeft een invloed op Hallo prestaties van een synchronisatiecyclus.</span><span class="sxs-lookup"><span data-stu-id="a719b-148">Updating attribute mappings has an impact on hello performance of a synchronization cycle.</span></span> <span data-ttu-id="a719b-149">Een update toohello kenmerk toewijzing-configuratie is vereist voor alle beheerde objecten toobe opnieuw geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="a719b-149">An update toohello attribute mapping configuration requires all managed objects toobe reevaluated.</span></span> <span data-ttu-id="a719b-150">Het is een aanbevolen best practice tookeep Hallo aantal opeenvolgende wijzigingen tooyour kenmerktoewijzingen minimaal.</span><span class="sxs-lookup"><span data-stu-id="a719b-150">It is a recommended best practice tookeep hello number of consecutive changes tooyour attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a719b-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a719b-151">Next steps</span></span>

* <span data-ttu-id="a719b-152">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="a719b-152">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="a719b-153">Gebruiker inrichten/Deprovisioning tooSaaS Apps automatiseren</span><span class="sxs-lookup"><span data-stu-id="a719b-153">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="a719b-154">Expressies voor kenmerktoewijzingen schrijven</span><span class="sxs-lookup"><span data-stu-id="a719b-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="a719b-155">Bereikfilters voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="a719b-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="a719b-156">Met behulp van SCIM tooenable automatische inrichting van gebruikers en groepen van Azure Active Directory-tooapplications</span><span class="sxs-lookup"><span data-stu-id="a719b-156">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="a719b-157">Meldingen inrichten van een account</span><span class="sxs-lookup"><span data-stu-id="a719b-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="a719b-158">Lijst met zelfstudies over het tooIntegrate SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="a719b-158">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

