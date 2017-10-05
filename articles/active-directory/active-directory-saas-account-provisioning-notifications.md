---
title: Account meldingen inrichten | Microsoft Docs
description: Informatie over het om ervoor te zorgen dat u problemen met gebruikers inrichten die uw aandacht nodig doordat account inrichten meldingen worden gewaarschuwd.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: b99037fc28eca1a3ebffefb9e99991e74f52c9a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="5ccfd-103">Meldingen over accountinrichting</span><span class="sxs-lookup"><span data-stu-id="5ccfd-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="5ccfd-104">Met gebruikers inrichten, kunt u het proces voor het beheren van gebruikers in de SaaS-toepassingen van derden automatiseren.</span><span class="sxs-lookup"><span data-stu-id="5ccfd-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="5ccfd-105">Dit is een geautomatiseerd proces, uw interactie met dit proces is van tijd tot tijd nodig.</span><span class="sxs-lookup"><span data-stu-id="5ccfd-105">While this is an automated process, your interaction with this process is from time to time required.</span></span> <br>
<span data-ttu-id="5ccfd-106">Dit is bijvoorbeeld het geval is, wanneer het wachtwoord van het account dat u hebt geconfigureerd voor het uitwisselen van gegevens met een derde partij SaaS-toepassing is verlopen.</span><span class="sxs-lookup"><span data-stu-id="5ccfd-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="5ccfd-107">Doordat het account voor het inrichten van meldingen kunt u ervoor zorgen dat u wordt gewaarschuwd van problemen met gebruikers inrichten die uw aandacht vereisen.</span><span class="sxs-lookup"><span data-stu-id="5ccfd-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span></span>

<span data-ttu-id="5ccfd-108">U activeren of deactiveren account meldingen inrichten als onderdeel van uw gebruikers inrichten van de configuratie voor een derde partij SaaS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5ccfd-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Gebruikers inrichten][1] 

<span data-ttu-id="5ccfd-110">Voor het activeren van account meldingen inrichting, selecteert u het bijbehorende selectievakje op het **bevestiging** dialoogvenster pagina en typ de e-mailalias op van de ontvanger.</span><span class="sxs-lookup"><span data-stu-id="5ccfd-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span></span>

![Meldingen over accountinrichting][2]

<span data-ttu-id="5ccfd-112">U kunt een distributielijst opgeven als recipient; het is echter belangrijk te weten dat de e-mailmelding bevat koppelingen naar rapporten die alleen toegankelijk voor de Azure AD-beheerders zijn.</span><span class="sxs-lookup"><span data-stu-id="5ccfd-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span></span>

<span data-ttu-id="5ccfd-113">Als u meldingen ingeschakeld inrichting account hebt, ontvangt u e-mailberichten over kritieke problemen die gerelateerd zijn aan gebruikers inrichten.</span><span class="sxs-lookup"><span data-stu-id="5ccfd-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span></span> <span data-ttu-id="5ccfd-114">Echter, om te voorkomen dat een e-overbelasting, alleen ontvangt u een e-mailmelding per dag voor elke SaaS-toepassing die voor de e-mailmelding is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5ccfd-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="5ccfd-115">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="5ccfd-115">Related Articles</span></span>
* <span data-ttu-id="5ccfd-116">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="5ccfd-116">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="5ccfd-117">Automatisch gebruikers inrichten/opheffen van inrichting tot SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="5ccfd-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="5ccfd-118">Kenmerktoewijzingen voor gebruikers inrichten aanpassen</span><span class="sxs-lookup"><span data-stu-id="5ccfd-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="5ccfd-119">Expressies voor kenmerktoewijzingen schrijven</span><span class="sxs-lookup"><span data-stu-id="5ccfd-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="5ccfd-120">Bereikfilters voor gebruikers inrichten</span><span class="sxs-lookup"><span data-stu-id="5ccfd-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* <span data-ttu-id="5ccfd-121">[Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications](active-directory-scim-provisioning.md) (SCIM gebruiken om in te stellen dat gebruikers en groepen van Azure Active Directory automatisch worden ingericht voor toepassingen)</span><span class="sxs-lookup"><span data-stu-id="5ccfd-121">[Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications](active-directory-scim-provisioning.md)</span></span>
* [<span data-ttu-id="5ccfd-122">Lijst met zelfstudies over het integreren van SaaS-Apps</span><span class="sxs-lookup"><span data-stu-id="5ccfd-122">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
