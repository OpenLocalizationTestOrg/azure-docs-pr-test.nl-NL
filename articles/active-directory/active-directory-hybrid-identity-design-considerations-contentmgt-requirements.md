---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - vereisten voor inhoudsbeheer bepalen | Microsoft Docs
description: Biedt inzicht in hoe toodetermine Hallo inhoudsbeheer behoeften van uw bedrijf. Gewoonlijk wellicht wanneer een gebruiker zijn of haar eigen apparaat heeft hij ook meerdere referenties die zal worden afwisselende volgens toohello-toepassing die hij gebruikt. Het is belangrijk toodifferentiate inhoud is gemaakt met behulp van persoonlijke referenties versus Hallo die zijn gemaakt met zakelijke referenties. De oplossing van uw identiteit moet kunnen toointeract met cloud services tooprovide een naadloze ervaring voor eindgebruikers tijdens de toohello zijn privacy garanderen en het verhogen van Hallo bescherming tegen het gegevenslekken van.
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
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="37b06-106">Inhoudsbeheer vereisten bepalen voor uw oplossing voor hybride identiteit</span><span class="sxs-lookup"><span data-stu-id="37b06-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="37b06-107">Hallo inhoudsbeheer vereisten voor uw bedrijf kan directe invloed op uw beslissing over welke oplossing toouse van hybride identiteit.</span><span class="sxs-lookup"><span data-stu-id="37b06-107">Understanding hello content management requirements for your business may direct affect your decision on which hybrid identity solution toouse.</span></span> <span data-ttu-id="37b06-108">Met Hallo komst van meerdere apparaten en de mogelijkheid om Hallo van toobring gebruikers hun eigen apparaten ([BYOD](http://aka.ms/byodcg)), Hallo bedrijf moet een eigen gegevens beveiligen, maar deze ook moet ervoor zorgen dat de privacy van gebruikers behouden.</span><span class="sxs-lookup"><span data-stu-id="37b06-108">With hello proliferation of multiple devices and hello capability of users toobring their own devices ([BYOD](http://aka.ms/byodcg)), hello company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="37b06-109">Gewoonlijk wellicht wanneer een gebruiker zijn of haar eigen apparaat heeft hij ook meerdere referenties die zal worden afwisselende volgens toohello-toepassing die hij gebruikt.</span><span class="sxs-lookup"><span data-stu-id="37b06-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according toohello application that he uses.</span></span> <span data-ttu-id="37b06-110">Het is belangrijk toodifferentiate inhoud is gemaakt met behulp van persoonlijke referenties versus Hallo die zijn gemaakt met zakelijke referenties.</span><span class="sxs-lookup"><span data-stu-id="37b06-110">It is important toodifferentiate what content was created using personal credentials versus hello ones created using corporate credentials.</span></span> <span data-ttu-id="37b06-111">De oplossing van uw identiteit moet kunnen toointeract met cloud services tooprovide een naadloze ervaring voor eindgebruikers tijdens de toohello zijn privacy garanderen en het verhogen van Hallo bescherming tegen het gegevenslekken van.</span><span class="sxs-lookup"><span data-stu-id="37b06-111">Your identity solution should be able toointeract with cloud services tooprovide a seamless experience toohello end user while ensure his privacy and increase hello protection against data leakage.</span></span> 

<span data-ttu-id="37b06-112">Oplossing voor uw identiteit zal worden gebruikt door andere technische besturingselementen in volgorde tooprovide inhoudsbeheer zoals weergegeven in onderstaande afbeelding ziet Hallo:</span><span class="sxs-lookup"><span data-stu-id="37b06-112">Your identity solution will be leveraged by different technical controls in order tooprovide content management as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="37b06-113">**Beveiligingsmechanismen die zal worden gebruik van uw identiteitsbeheersysteem**</span><span class="sxs-lookup"><span data-stu-id="37b06-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="37b06-114">Vereisten voor inhoudsbeheer wordt in het algemeen gebruikmaken van uw identiteitsbeheersysteem in Hallo gebieden te volgen:</span><span class="sxs-lookup"><span data-stu-id="37b06-114">In general, content management requirements will leverage your identity management system in hello following areas:</span></span>

* <span data-ttu-id="37b06-115">Privacy: Hallo-gebruiker die eigenaar is van een bron te identificeren en Hallo juiste besturingselementen toomaintain integriteit toepassen.</span><span class="sxs-lookup"><span data-stu-id="37b06-115">Privacy: identifying hello user that owns a resource and applying hello appropriate controls toomaintain integrity.</span></span>
* <span data-ttu-id="37b06-116">Gegevensclassificatie: identificeren Hallo gebruiker of groep en niveau van toegang op basis van indeling tooits tooan-object.</span><span class="sxs-lookup"><span data-stu-id="37b06-116">Data Classification: identify hello user or group and level of access tooan object according tooits classification.</span></span> 
* <span data-ttu-id="37b06-117">Beveiliging van gegevens lekken: beveiligingsmechanismen verantwoordelijk voor het beveiligen van gegevenslekken tooavoid moet toointeract met Hallo identiteit system toovalidate Hallo gebruikers id.</span><span class="sxs-lookup"><span data-stu-id="37b06-117">Data Leakage Protection: security controls responsible for protecting data tooavoid leakage will need toointeract with hello identity system toovalidate hello user’s identity.</span></span> <span data-ttu-id="37b06-118">Dit is ook belangrijk voor de audittrail controledoeleinden.</span><span class="sxs-lookup"><span data-stu-id="37b06-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="37b06-119">Lees [gegevensclassificatie ter voorbereiding op de cloud](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) voor meer informatie over aanbevolen procedures en richtlijnen voor gegevensclassificatie.</span><span class="sxs-lookup"><span data-stu-id="37b06-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="37b06-120">Tijdens het plannen van uw oplossing voor hybride identiteit Zorg ervoor dat Hallo volgende worden vragen beantwoord de tooyour organisatievereisten op basis van:</span><span class="sxs-lookup"><span data-stu-id="37b06-120">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

* <span data-ttu-id="37b06-121">Heeft uw bedrijf beveiligingsmechanismen in place tooenforce gegevensprivacy?</span><span class="sxs-lookup"><span data-stu-id="37b06-121">Does your company have security controls in place tooenforce data privacy?</span></span>
  * <span data-ttu-id="37b06-122">Zo ja, deze beveiligingsmaatregelen worden kunnen toointegrate met Hallo hybride identiteitsoplossing dat u momenteel tooadopt bent?</span><span class="sxs-lookup"><span data-stu-id="37b06-122">If yes, will those security controls be able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="37b06-123">Maakt gebruik van uw bedrijf gegevensclassificatie?</span><span class="sxs-lookup"><span data-stu-id="37b06-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="37b06-124">Zo ja, is Hallo huidige oplossing kunnen toointegrate met Hallo hybride identiteitsoplossing dat u momenteel tooadopt bent?</span><span class="sxs-lookup"><span data-stu-id="37b06-124">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="37b06-125">Heeft uw bedrijf momenteel oplossing voor het lekken van gegevens?</span><span class="sxs-lookup"><span data-stu-id="37b06-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="37b06-126">Zo ja, is Hallo huidige oplossing kunnen toointegrate met Hallo hybride identiteitsoplossing dat u momenteel tooadopt bent?</span><span class="sxs-lookup"><span data-stu-id="37b06-126">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="37b06-127">Heeft uw bedrijf behoefte aan tooaudit toegang tooresources?</span><span class="sxs-lookup"><span data-stu-id="37b06-127">Does your company need tooaudit access tooresources?</span></span>
  * <span data-ttu-id="37b06-128">Zo ja, welk type bronnen?</span><span class="sxs-lookup"><span data-stu-id="37b06-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="37b06-129">Zo ja, welk niveau van de informatie is nodig?</span><span class="sxs-lookup"><span data-stu-id="37b06-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="37b06-130">Zo ja, waarbij het controlelogboek Hallo moet zich bevinden?</span><span class="sxs-lookup"><span data-stu-id="37b06-130">If yes, where hello audit log must reside?</span></span> <span data-ttu-id="37b06-131">Lokaal of in de cloud Hallo?</span><span class="sxs-lookup"><span data-stu-id="37b06-131">On-premises or in hello cloud?</span></span>
* <span data-ttu-id="37b06-132">Heeft uw bedrijf behoefte aan tooencrypt e-mailberichten met gevoelige gegevens (burgerservicenummers, creditcardnummers, enzovoort)?</span><span class="sxs-lookup"><span data-stu-id="37b06-132">Does your company need tooencrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="37b06-133">Heeft uw bedrijf behoefte aan tooencrypt alle documenten/inhoud gedeeld met externe zakelijke partners?</span><span class="sxs-lookup"><span data-stu-id="37b06-133">Does your company need tooencrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="37b06-134">Heeft uw bedrijf behoefte tooenforce bedrijfsbeleid op bepaalde soorten e-mailberichten (geen allen beantwoorden, niet doorsturen)?</span><span class="sxs-lookup"><span data-stu-id="37b06-134">Does your company need tooenforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="37b06-135">Zorg ervoor dat tootake notities van elk antwoord en Hallo logica achter Hallo antwoord begrijpt.</span><span class="sxs-lookup"><span data-stu-id="37b06-135">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="37b06-136">[Definieer de strategie voor gegevensbescherming](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) gaat over de beschikbare opties voor Hallo en de voor-en nadelen van elke optie.</span><span class="sxs-lookup"><span data-stu-id="37b06-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="37b06-137">Moet door deze vragen die u selecteert welke optie het beste past bij uw bedrijf te beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="37b06-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="37b06-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37b06-138">Next steps</span></span>
[<span data-ttu-id="37b06-139">Vereisten voor toegangsbeheer bepalen</span><span class="sxs-lookup"><span data-stu-id="37b06-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="37b06-140">Zie ook</span><span class="sxs-lookup"><span data-stu-id="37b06-140">See Also</span></span>
[<span data-ttu-id="37b06-141">Overzicht ontwerpoverwegingen</span><span class="sxs-lookup"><span data-stu-id="37b06-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

