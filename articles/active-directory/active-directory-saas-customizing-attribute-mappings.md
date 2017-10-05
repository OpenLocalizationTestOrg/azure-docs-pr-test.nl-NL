---
title: Azure AD-kenmerktoewijzingen aanpassen | Microsoft Docs
description: Meer informatie over welke kenmerktoewijzingen voor SaaS-apps in Azure Active Directory zijn hoe u kunt deze aanpassen om de behoeften van uw bedrijf op te lossen.
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
ms.openlocfilehash: 6ca2fdc9c68ea0030d938eeaebd57aafa0e2790f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="82733-103">Gebruikers inrichten kenmerktoewijzingen voor SaaS-toepassingen in Azure Active Directory aanpassen</span><span class="sxs-lookup"><span data-stu-id="82733-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="82733-104">Microsoft Azure AD biedt ondersteuning voor gebruikersinrichting voor SaaS-toepassingen van derden zoals Salesforce en Google Apps.</span><span class="sxs-lookup"><span data-stu-id="82733-104">Microsoft Azure AD provides support for user provisioning to third-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="82733-105">Als er gebruikers inrichten voor een SaaS-toepassing van derden is ingeschakeld, bepaalt de Azure-beheerportal de kenmerkwaarden weer in de vorm van een configuratie met de naam "kenmerk wordt toegewezen."</span><span class="sxs-lookup"><span data-stu-id="82733-105">If you have user provisioning for a third-party SaaS application enabled, the Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="82733-106">Er is een set vooraf geconfigureerde kenmerktoewijzingen tussen Azure AD-gebruikersobjecten en gebruikersobjecten van elke SaaS-app.</span><span class="sxs-lookup"><span data-stu-id="82733-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="82733-107">Sommige apps beheren andere soorten objecten, zoals groepen of contactpersonen.</span><span class="sxs-lookup"><span data-stu-id="82733-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="82733-108">U kunt de standaard-kenmerktoewijzingen aanpassen volgens uw bedrijfsbehoeften.</span><span class="sxs-lookup"><span data-stu-id="82733-108">You can customize the default attribute mappings according to your business needs.</span></span> <span data-ttu-id="82733-109">Dit houdt in dat u kunt wijzigen of verwijderen van bestaande kenmerktoewijzingen of nieuwe kenmerktoewijzingen maken.</span><span class="sxs-lookup"><span data-stu-id="82733-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="82733-110">In de Azure AD-portal, opent u deze functie door te klikken op een **toewijzingen** configuratie onder **inrichten** in de **beheren** gedeelte van een **bedrijfstoepassing**.</span><span class="sxs-lookup"><span data-stu-id="82733-110">In the Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in the **Manage** section of an **Enterprise application**.</span></span>


![SalesForce][5] 

<span data-ttu-id="82733-112">Te klikken op een **toewijzingen** configuratie, de verwante geopend **kenmerk toewijzing** blade.</span><span class="sxs-lookup"><span data-stu-id="82733-112">Clicking a **Mappings** configuration, opens the related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="82733-113">Er zijn kenmerktoewijzingen die door een SaaS-toepassing vereist zijn te laten functioneren.</span><span class="sxs-lookup"><span data-stu-id="82733-113">There are attribute mappings that are required by a SaaS application to function correctly.</span></span> <span data-ttu-id="82733-114">Voor de vereiste kenmerken de **verwijderen** functie is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="82733-114">For required attributes, the **Delete** feature is unavailable.</span></span>


![SalesForce][6]  

<span data-ttu-id="82733-116">In het bovenstaande voorbeeld kunt u zien dat de **gebruikersnaam** kenmerk van een beheerd object in Salesforce is gevuld met de **userPrincipalName** waarde van de gekoppelde Azure Active Directory-Object.</span><span class="sxs-lookup"><span data-stu-id="82733-116">In the example above, you can see that the **Username** attribute of a managed object in Salesforce is populated with the **userPrincipalName** value of the linked Azure Active Directory Object.</span></span>

<span data-ttu-id="82733-117">U kunt bestaande **kenmerktoewijzingen** door te klikken op een toewijzing.</span><span class="sxs-lookup"><span data-stu-id="82733-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="82733-118">Hiermee opent u de **kenmerk bewerken** blade.</span><span class="sxs-lookup"><span data-stu-id="82733-118">This opens the **Edit Attribute** blade.</span></span>

![SalesForce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="82733-120">Kenmerk typen toewijzing</span><span class="sxs-lookup"><span data-stu-id="82733-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="82733-121">Met kenmerktoewijzingen, kunt u bepalen hoe kenmerken worden ingevuld in een SaaS-toepassing van derden.</span><span class="sxs-lookup"><span data-stu-id="82733-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="82733-122">Er zijn vier verschillende toewijzingstypen ondersteund:</span><span class="sxs-lookup"><span data-stu-id="82733-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="82733-123">**Directe** : het kenmerk target is gevuld met de waarde van een kenmerk van het gekoppelde object in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82733-123">**Direct** – the target attribute is populated with the value of an attribute of the linked object in Azure AD.</span></span>
* <span data-ttu-id="82733-124">**Constante** : het kenmerk target is gevuld met een specifieke tekenreeks die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="82733-124">**Constant** – the target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="82733-125">**Expressie** -het kenmerk target is ingevuld op basis van het resultaat van een script-achtige-expressie.</span><span class="sxs-lookup"><span data-stu-id="82733-125">**Expression** - the target attribute is populated based on the result of a script-like expression.</span></span> 
  <span data-ttu-id="82733-126">Zie voor meer informatie [schrijven expressies voor kenmerktoewijzingen in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="82733-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="82733-127">**Geen** -het kenmerk target blijft ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="82733-127">**None** - the target attribute is left unmodified.</span></span> <span data-ttu-id="82733-128">Echter, als het kenmerk target ooit leeg is, wordt dit ingevuld met de standaardwaarde die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="82733-128">However, if the target attribute is ever empty, it is populated with the Default value that you specify.</span></span>

<span data-ttu-id="82733-129">Naast deze vier eenvoudige kenmerk toewijzingstypen aangepaste kenmerktoewijzingen ondersteuning voor het concept van een optionele **standaard** waarde toewijzing.</span><span class="sxs-lookup"><span data-stu-id="82733-129">In addition to these four basic attribute mapping types, custom attribute mappings support the concept of an optional **default** value assignment.</span></span> <span data-ttu-id="82733-130">De toewijzing van de standaard waarde zorgt ervoor dat een target-kenmerk is gevuld met een waarde als er geen waarde in Azure AD en ook op het doelobject.</span><span class="sxs-lookup"><span data-stu-id="82733-130">The default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on the target object.</span></span> <span data-ttu-id="82733-131">De meest voorkomende configuratie is leeg laten.</span><span class="sxs-lookup"><span data-stu-id="82733-131">The most common configuration is to leave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="82733-132">Understanding toewijzing kenmerkeigenschappen</span><span class="sxs-lookup"><span data-stu-id="82733-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="82733-133">In de vorige sectie hebt u al is kennis met de eigenschap type van kenmerk toewijzing.</span><span class="sxs-lookup"><span data-stu-id="82733-133">In the previous section, you have already been introduced to the attribute mapping type property.</span></span>
<span data-ttu-id="82733-134">Naast deze eigenschap ondersteunen kenmerktoewijzingen ook de volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="82733-134">In addition to this property, attribute mappings do also support the following attributes:</span></span>

- <span data-ttu-id="82733-135">**Bronkenmerk** -gebruikerskenmerk uit het bronsysteem (bijvoorbeeld: Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="82733-135">**Source attribute** - The user attribute from the source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="82733-136">**Doelkenmerk** – het gebruikerskenmerk in het doelsysteem (bijvoorbeeld: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="82733-136">**Target attribute** – The user attribute in the target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="82733-137">**Overeen met objecten met behulp van dit kenmerk** : of deze toewijzing moet worden gebruikt als unieke identificatie van gebruikers tussen de bron en doel-systemen of niet.</span><span class="sxs-lookup"><span data-stu-id="82733-137">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between the source and target systems.</span></span> <span data-ttu-id="82733-138">Dit is standaard ingesteld op het kenmerk userPrincipalName of e-mail in Azure AD, die meestal naar een veld username in een doeltoepassing is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="82733-138">This is typically set on the userPrincipalName or mail attribute in Azure AD, which is typically mapped to a username field in a target application.</span></span>
- <span data-ttu-id="82733-139">**Overeenkomende voorrang** – meerdere overeenkomende kenmerken kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="82733-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="82733-140">Wanneer er meerdere, moeten ze worden geëvalueerd in de volgorde gedefinieerd door dit veld.</span><span class="sxs-lookup"><span data-stu-id="82733-140">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="82733-141">Als een overeenkomst is gevonden, er is geen verdere overeenkomende kenmerken worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="82733-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="82733-142">**Deze toewijzing is van toepassing**</span><span class="sxs-lookup"><span data-stu-id="82733-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="82733-143">**Altijd** : deze toewijzing is van toepassing op beide maken van een gebruikersaccount en acties bijwerken</span><span class="sxs-lookup"><span data-stu-id="82733-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="82733-144">**Alleen tijdens het maken van** -deze toewijzing is van toepassing alleen op gebruikersacties maken</span><span class="sxs-lookup"><span data-stu-id="82733-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="82733-145">Wat u moet weten</span><span class="sxs-lookup"><span data-stu-id="82733-145">What you should know</span></span>

<span data-ttu-id="82733-146">Microsoft Azure AD biedt een efficiënte implementatie van een synchronisatieproces.</span><span class="sxs-lookup"><span data-stu-id="82733-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="82733-147">In een omgeving met geïnitialiseerde worden alleen objecten die moet worden bijgewerkt verwerkt tijdens een synchronisatiecyclus.</span><span class="sxs-lookup"><span data-stu-id="82733-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="82733-148">Kenmerktoewijzingen bijwerken, heeft een invloed op de prestaties van een synchronisatiecyclus.</span><span class="sxs-lookup"><span data-stu-id="82733-148">Updating attribute mappings has an impact on the performance of a synchronization cycle.</span></span> <span data-ttu-id="82733-149">Een update voor de configuratie van de toewijzing is vereist voor alle beheerde objecten die opnieuw worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="82733-149">An update to the attribute mapping configuration requires all managed objects to be reevaluated.</span></span> <span data-ttu-id="82733-150">Het is aanbevolen om het aantal opeenvolgende wijzigingen tot uw kenmerktoewijzingen minimaal te beperken.</span><span class="sxs-lookup"><span data-stu-id="82733-150">It is a recommended best practice to keep the number of consecutive changes to your attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82733-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82733-151">Next steps</span></span>

* <span data-ttu-id="82733-152">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="82733-152">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="82733-153">Automatisch gebruikers inrichten/opheffen van inrichting tot SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="82733-153">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="82733-154">Expressies voor kenmerktoewijzingen schrijven</span><span class="sxs-lookup"><span data-stu-id="82733-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="82733-155">Bereikfilters voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="82733-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* <span data-ttu-id="82733-156">[Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications](active-directory-scim-provisioning.md) (SCIM gebruiken om in te stellen dat gebruikers en groepen van Azure Active Directory automatisch worden ingericht voor toepassingen)</span><span class="sxs-lookup"><span data-stu-id="82733-156">[Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications](active-directory-scim-provisioning.md)</span></span>
* [<span data-ttu-id="82733-157">Meldingen inrichten van een account</span><span class="sxs-lookup"><span data-stu-id="82733-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="82733-158">Lijst met zelfstudies over het integreren van SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="82733-158">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

