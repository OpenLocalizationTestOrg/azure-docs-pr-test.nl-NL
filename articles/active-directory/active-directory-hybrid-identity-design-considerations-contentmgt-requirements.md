---
title: Azure Active Directory hybride identiteit ontwerpoverwegingen - vereisten voor inhoudsbeheer bepalen | Microsoft Docs
description: Biedt inzicht in hoe de vereisten voor beheer van de inhoud van uw bedrijf. Gewoonlijk wellicht wanneer een gebruiker zijn of haar eigen apparaat heeft hij ook meerdere referenties zal worden afwisselende volgens de toepassing die hij gebruikt. Het is belangrijk om te onderscheiden welke inhoud is gemaakt met behulp van persoonlijke referenties die gemaakt met zakelijke referenties. De oplossing van uw identiteit moet kunnen communiceren met cloud services voor een naadloze ervaring voor de eindgebruiker tijdens zijn privacy garanderen en verhoogt de beveiliging tegen het gegevenslekken van.
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 840de1e1fcba74285788d51d8f544375f0affa77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="70371-106">Inhoudsbeheer vereisten bepalen voor uw oplossing voor hybride identiteit</span><span class="sxs-lookup"><span data-stu-id="70371-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="70371-107">Inhoudsbeheer vereisten voor uw bedrijf kan een directe invloed hebben op uw beslissing over welke oplossing voor hybride identiteit moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="70371-107">Understanding the content management requirements for your business may direct affect your decision on which hybrid identity solution to use.</span></span> <span data-ttu-id="70371-108">Met de komst van meerdere apparaten en de mogelijkheid van gebruikers voor hun eigen apparaten meebrengen ([BYOD](http://aka.ms/byodcg)), het bedrijf een eigen gegevens moet beveiligen, maar deze ook moet ervoor zorgen dat de privacy van gebruikers behouden.</span><span class="sxs-lookup"><span data-stu-id="70371-108">With the proliferation of multiple devices and the capability of users to bring their own devices ([BYOD](http://aka.ms/byodcg)), the company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="70371-109">Gewoonlijk wellicht wanneer een gebruiker zijn of haar eigen apparaat heeft hij ook meerdere referenties zal worden afwisselende volgens de toepassing die hij gebruikt.</span><span class="sxs-lookup"><span data-stu-id="70371-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses.</span></span> <span data-ttu-id="70371-110">Het is belangrijk om te onderscheiden welke inhoud is gemaakt met behulp van persoonlijke referenties die gemaakt met zakelijke referenties.</span><span class="sxs-lookup"><span data-stu-id="70371-110">It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials.</span></span> <span data-ttu-id="70371-111">De oplossing van uw identiteit moet kunnen communiceren met cloud services voor een naadloze ervaring voor de eindgebruiker tijdens zijn privacy garanderen en verhoogt de beveiliging tegen het gegevenslekken van.</span><span class="sxs-lookup"><span data-stu-id="70371-111">Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.</span></span> 

<span data-ttu-id="70371-112">Oplossing voor uw identiteit zal worden gebruikt door andere technische besturingselementen om te voorzien van inhoudsbeheer, zoals wordt weergegeven in de afbeelding hieronder:</span><span class="sxs-lookup"><span data-stu-id="70371-112">Your identity solution will be leveraged by different technical controls in order to provide content management as shown in the figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="70371-113">**Beveiligingsmechanismen die zal worden gebruik van uw identiteitsbeheersysteem**</span><span class="sxs-lookup"><span data-stu-id="70371-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="70371-114">Vereisten voor inhoudsbeheer wordt in het algemeen gebruikmaken van uw identiteitsbeheersysteem in de volgende gebieden:</span><span class="sxs-lookup"><span data-stu-id="70371-114">In general, content management requirements will leverage your identity management system in the following areas:</span></span>

* <span data-ttu-id="70371-115">Privacy: de gebruiker die eigenaar is van een bron te identificeren en het toepassen van de juiste besturingselementen om integriteit te bewaren.</span><span class="sxs-lookup"><span data-stu-id="70371-115">Privacy: identifying the user that owns a resource and applying the appropriate controls to maintain integrity.</span></span>
* <span data-ttu-id="70371-116">Gegevensclassificatie: identificeren van de gebruiker of groep en het niveau van toegang tot een object volgens de classificatie.</span><span class="sxs-lookup"><span data-stu-id="70371-116">Data Classification: identify the user or group and level of access to an object according to its classification.</span></span> 
* <span data-ttu-id="70371-117">Beveiliging van gegevens lekken: beveiligingsmechanismen verantwoordelijk voor het beveiligen van gegevens om te voorkomen dat lekken moet communiceren met het identiteitssysteem om de identiteit van de gebruiker te valideren.</span><span class="sxs-lookup"><span data-stu-id="70371-117">Data Leakage Protection: security controls responsible for protecting data to avoid leakage will need to interact with the identity system to validate the user’s identity.</span></span> <span data-ttu-id="70371-118">Dit is ook belangrijk voor de audittrail controledoeleinden.</span><span class="sxs-lookup"><span data-stu-id="70371-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="70371-119">Lees [gegevensclassificatie ter voorbereiding op de cloud](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) voor meer informatie over aanbevolen procedures en richtlijnen voor gegevensclassificatie.</span><span class="sxs-lookup"><span data-stu-id="70371-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="70371-120">Wanneer uw oplossing voor hybride identiteit planning Zorg ervoor dat de volgende vragen worden beantwoord volgens de vereisten van uw organisatie:</span><span class="sxs-lookup"><span data-stu-id="70371-120">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

* <span data-ttu-id="70371-121">Heeft uw bedrijf beveiligingsmechanismen om het afdwingen van de privacy van gegevens?</span><span class="sxs-lookup"><span data-stu-id="70371-121">Does your company have security controls in place to enforce data privacy?</span></span>
  * <span data-ttu-id="70371-122">Zo ja, deze besturingselementen voor de beveiliging kan worden geïntegreerd met de hybride identiteitsoplossing die u gaat vast te stellen?</span><span class="sxs-lookup"><span data-stu-id="70371-122">If yes, will those security controls be able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="70371-123">Maakt gebruik van uw bedrijf gegevensclassificatie?</span><span class="sxs-lookup"><span data-stu-id="70371-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="70371-124">Zo ja, kan de huidige oplossing integreren met de hybride identiteitsoplossing die u gaat vast te stellen?</span><span class="sxs-lookup"><span data-stu-id="70371-124">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="70371-125">Heeft uw bedrijf momenteel oplossing voor het lekken van gegevens?</span><span class="sxs-lookup"><span data-stu-id="70371-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="70371-126">Zo ja, kan de huidige oplossing integreren met de hybride identiteitsoplossing die u gaat vast te stellen?</span><span class="sxs-lookup"><span data-stu-id="70371-126">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="70371-127">Moet uw bedrijf toegang tot bronnen?</span><span class="sxs-lookup"><span data-stu-id="70371-127">Does your company need to audit access to resources?</span></span>
  * <span data-ttu-id="70371-128">Zo ja, welk type bronnen?</span><span class="sxs-lookup"><span data-stu-id="70371-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="70371-129">Zo ja, welk niveau van de informatie is nodig?</span><span class="sxs-lookup"><span data-stu-id="70371-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="70371-130">Zo ja, waarbij het controlelogboek moet zich bevinden?</span><span class="sxs-lookup"><span data-stu-id="70371-130">If yes, where the audit log must reside?</span></span> <span data-ttu-id="70371-131">Lokaal of in de cloud?</span><span class="sxs-lookup"><span data-stu-id="70371-131">On-premises or in the cloud?</span></span>
* <span data-ttu-id="70371-132">Heeft uw bedrijf nodig voor het versleutelen van een e-mailberichten met gevoelige gegevens (burgerservicenummers, creditcardnummers, enzovoort)?</span><span class="sxs-lookup"><span data-stu-id="70371-132">Does your company need to encrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="70371-133">Heeft uw bedrijf nodig voor het versleutelen van alle documenten/inhoud gedeeld met externe zakelijke partners?</span><span class="sxs-lookup"><span data-stu-id="70371-133">Does your company need to encrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="70371-134">Heeft uw bedrijf behoefte aan het bedrijfsbeleid op bepaalde soorten e-mailberichten (geen allen beantwoorden, niet doorsturen)?</span><span class="sxs-lookup"><span data-stu-id="70371-134">Does your company need to enforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="70371-135">Zorg ervoor dat elk antwoord noteert de logica achter het antwoord begrijpt.</span><span class="sxs-lookup"><span data-stu-id="70371-135">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="70371-136">[Definieer de strategie voor gegevensbescherming](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) gaat over de beschikbare opties en de voor-en nadelen van elke optie.</span><span class="sxs-lookup"><span data-stu-id="70371-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="70371-137">Moet door deze vragen die u selecteert welke optie het beste past bij uw bedrijf te beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="70371-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="70371-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70371-138">Next steps</span></span>
[<span data-ttu-id="70371-139">Vereisten voor toegangsbeheer bepalen</span><span class="sxs-lookup"><span data-stu-id="70371-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="70371-140">Zie ook</span><span class="sxs-lookup"><span data-stu-id="70371-140">See Also</span></span>
[<span data-ttu-id="70371-141">Overzicht ontwerpoverwegingen</span><span class="sxs-lookup"><span data-stu-id="70371-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

