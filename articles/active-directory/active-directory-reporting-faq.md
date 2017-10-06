---
title: Active Directory Reporting Veelgestelde vragen over aaaAzure | Microsoft Docs
description: Azure Active Directory-Veelgestelde vragen over rapportage.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="957c5-103">Azure Active Directory-Veelgestelde vragen over rapportage</span><span class="sxs-lookup"><span data-stu-id="957c5-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="957c5-104">Dit artikel bevat toofrequently van antwoorden op veelgestelde vragen (FAQ's) over Azure Active Directory-rapportage.</span><span class="sxs-lookup"><span data-stu-id="957c5-104">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="957c5-105">Zie voor meer informatie [rapportage van Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="957c5-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="957c5-106">**V: Wat is de Gegevensretentie hello om activiteitenlogboeken (Audit en aanmeldingen) in hello Azure-portal?**</span><span class="sxs-lookup"><span data-stu-id="957c5-106">**Q: What is hello data retention for activity logs (Audit and Sign-ins) in hello Azure portal?**</span></span> 

<span data-ttu-id="957c5-107">**A:** bieden We zeven dagen aan gegevens voor onze klanten gratis en door over te schakelen tooan Azure AD Premium 1 of 2 voor Premium-licentie, u toegang hebt tot gegevens voor too30 dagen.</span><span class="sxs-lookup"><span data-stu-id="957c5-107">**A:** We provide 7 days of data for our free customers and by switching tooan Azure AD Premium 1 or Premium 2 license, you can access data for up too30 days.</span></span> <span data-ttu-id="957c5-108">Zie voor meer informatie over bewaren [bewaarbeleid voor Azure Active Directory-rapport](active-directory-reporting-retention.md)</span><span class="sxs-lookup"><span data-stu-id="957c5-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="957c5-109">**V: hoe lang duurt het tot ik Hallo activiteitsgegevens zien kunt wanneer ik mijn taak hebt voltooid?**</span><span class="sxs-lookup"><span data-stu-id="957c5-109">**Q: How long does it take until I can see hello Activity data after I have completed my task?**</span></span>

<span data-ttu-id="957c5-110">**A:** controlelogboeken activiteit een latentie tussen 15 minuten tooan uur hebben.</span><span class="sxs-lookup"><span data-stu-id="957c5-110">**A:** Audit activity logs have a latency ranging from 15 mins tooan hour.</span></span> <span data-ttu-id="957c5-111">Aanmelden activiteitenlogboeken hebben een latentie tussen 15 minuten voor de meeste records en too2 uur voor een aantal records.</span><span class="sxs-lookup"><span data-stu-id="957c5-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up too2 hours for a few records.</span></span>

---

<span data-ttu-id="957c5-112">**V: moet ik een globale beheerder toosee Hallo activiteit geregistreerd in hello Azure Portal of tooget gegevens via Hallo API toobe?**</span><span class="sxs-lookup"><span data-stu-id="957c5-112">**Q: Do I need toobe a global admin toosee hello activity logs in hello Azure Portal or tooget data through hello API?**</span></span>

<span data-ttu-id="957c5-113">**A:** Nee.</span><span class="sxs-lookup"><span data-stu-id="957c5-113">**A:** No.</span></span> <span data-ttu-id="957c5-114">U kan zijn een **beveiliging lezer**, een **beveiliging Admin** of een **globale beheerder** toosee rapportagegegevens in Azure Portal of door deze te openen via Hallo API.</span><span class="sxs-lookup"><span data-stu-id="957c5-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** toosee reporting data in Azure Portal or by accessing it through hello API.</span></span>

---

<span data-ttu-id="957c5-115">**V: kan ik Office 365 activiteit logboekgegevens via hello Azure-portal krijgen?**</span><span class="sxs-lookup"><span data-stu-id="957c5-115">**Q: Can I get Office 365 activity log information through hello Azure portal?**</span></span>

<span data-ttu-id="957c5-116">**A:** Hoewel activiteit van de Office 365 en Azure AD activiteit logboeken share Hallo directory-bronnen, als u wilt een volledige weergave van veel Hallo activiteitenlogboeken Office 365, u logboekgegevens van toohello Office 365-beheercentrum tooget Office 365-activiteit moet gaan.</span><span class="sxs-lookup"><span data-stu-id="957c5-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of hello directory resources, if you want a full view of hello Office 365 activity logs, you should go toohello Office 365 Admin Center tooget Office 365 Activity log information.</span></span>

---


<span data-ttu-id="957c5-117">**V: wat API's ik tooget informatie over Office 365-activiteitenlogboeken gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="957c5-117">**Q: Which APIs do I use tooget information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="957c5-118">**A:** gebruik Hallo Office 365 Management-API's tooaccess hello [Office 365 activiteit logboeken via een API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="957c5-118">**A:** Use hello Office 365 Management APIs tooaccess hello [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="957c5-119">**V: hoe veel records die ik vanuit Azure-portal kunt downloaden?**</span><span class="sxs-lookup"><span data-stu-id="957c5-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="957c5-120">**A:** kunt u downloaden van too120K records uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="957c5-120">**A:** You can download up too120K records from hello Azure portal.</span></span> <span data-ttu-id="957c5-121">Hallo-records worden gesorteerd op *meest recente* en standaard u Hallo meest recente 120 K records.</span><span class="sxs-lookup"><span data-stu-id="957c5-121">hello records are sorted by *most recent* and by default, you get hello most recent 120K records.</span></span> 

---

<span data-ttu-id="957c5-122">**V: hoe veel records kan ik opvragen via Hallo activiteiten API?**</span><span class="sxs-lookup"><span data-stu-id="957c5-122">**Q: How many records can I query through hello activities API?**</span></span>

<span data-ttu-id="957c5-123">**A:** u kunt een query too1 miljoen records (als u geen Hallo operator top, Hallo-record te sorteren door de meeste recente).</span><span class="sxs-lookup"><span data-stu-id="957c5-123">**A:** You can query up too1 million records (if you don’t use hello top operator, which sorts hello record by most recent).</span></span> <span data-ttu-id="957c5-124">Als u Hallo 'top' operator gebruikt, kunt u een query too500K records.</span><span class="sxs-lookup"><span data-stu-id="957c5-124">If you do use hello “top” operator, you can query up too500K records.</span></span> <span data-ttu-id="957c5-125">U kunt voorbeeldquery's op hoe Hallo toouse API hier vinden [hier](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="957c5-125">You can find sample queries on how toouse hello API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="957c5-126">**V: hoe krijg ik een premium-licentie**</span><span class="sxs-lookup"><span data-stu-id="957c5-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="957c5-127">**A:** Zie [aan de slag met Azure Active Directory Premium](active-directory-get-started-premium.md) voor een antwoord toothis vraag.</span><span class="sxs-lookup"><span data-stu-id="957c5-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

<span data-ttu-id="957c5-128">**V: hoe snel moet ik activiteiten gegevens ziet nadat u een premium-licentie.**</span><span class="sxs-lookup"><span data-stu-id="957c5-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="957c5-129">**A:** als u al activiteiten gegevens als een beschikbare licentie hebt, dan kunt u zien dezelfde gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="957c5-129">**A:** If you already have activities data as a free license, then you can see hello same data.</span></span> <span data-ttu-id="957c5-130">Als u geen gegevens, duurt het een of twee dagen.</span><span class="sxs-lookup"><span data-stu-id="957c5-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="957c5-131">**V: kan ik gegevens van vorige maand nadat u een Azure AD premium-licentie zien?**</span><span class="sxs-lookup"><span data-stu-id="957c5-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="957c5-132">**A:** als u onlangs tooa Premium-versie (met inbegrip van een evaluatieversie) hebt ingeschakeld, kunt u gegevens too7 dagen in eerste instantie zien.</span><span class="sxs-lookup"><span data-stu-id="957c5-132">**A:** If you have recently switched tooa Premium version (including a trial version), you can see data up too7 days initially.</span></span> <span data-ttu-id="957c5-133">Wanneer gegevens stelt samen, ziet u too30 dagen.</span><span class="sxs-lookup"><span data-stu-id="957c5-133">When data accumulates, you will see up too30 days.</span></span>

---

<span data-ttu-id="957c5-134">**V: Er is een risicogebeurtenis in Identity Protection maar ik zie niet overeenkomende aanmelden in Hallo alle aanmeldingen. Wordt dit verwacht?**</span><span class="sxs-lookup"><span data-stu-id="957c5-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in hello all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="957c5-135">**A:** Ja, Identity Protection resulteert risico's voor alle verificatie-overdrachten of als interactieve of niet-interactieve.</span><span class="sxs-lookup"><span data-stu-id="957c5-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="957c5-136">Alle aanmeldingen alleen rapport geeft alleen Hallo echter interactieve aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="957c5-136">However, all sign-ins only report shows only hello interactive sign-ins.</span></span>

---

<span data-ttu-id="957c5-137">**V: hoe kan ik 'Gebruikers gemarkeerd voor risico' Hallo-rapport in Azure-portal downloaden?**</span><span class="sxs-lookup"><span data-stu-id="957c5-137">**Q: How can I download hello “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="957c5-138">**A:** Hallo optie toodownload *gebruikers die zijn gemarkeerd voor risico* rapport wordt binnenkort toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="957c5-138">**A:** hello option toodownload *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="957c5-139">**V: hoe u weten waarom een aanmeldingspagina of een gebruiker is gemarkeerd riskant in hello Azure-portal?**</span><span class="sxs-lookup"><span data-stu-id="957c5-139">**Q: How do I know why a sign-in or a user was flagged risky in hello Azure portal?**</span></span>

<span data-ttu-id="957c5-140">**A:** Premium edition klanten voor meer informatie over de onderliggende risico's door te klikken op Hallo-gebruiker in 'Gebruikers gemarkeerd voor risico' of door te klikken op Hallo 'Riskant aanmeldingen' Hallo.</span><span class="sxs-lookup"><span data-stu-id="957c5-140">**A:** Premium edition customers can learn more about hello underlying risk events by clicking on hello user in “Users flagged for risk” or by clicking on hello “Risky sign-ins”.</span></span> <span data-ttu-id="957c5-141">Gratis en Basic-editie klanten krijgen toosee Hallo welke gebruikers en aanmeldingen zonder Hallo onderliggende gebeurtenisgegevens risico.</span><span class="sxs-lookup"><span data-stu-id="957c5-141">Free and Basic edition customers get toosee hello at-risk users and sign-ins without hello underlying risk event information.</span></span>

---

<span data-ttu-id="957c5-142">**V: hoe IP-adressen in berekend Hallo aanmeldingen en riskant aanmeldingen rapport veldnamenrij?**</span><span class="sxs-lookup"><span data-stu-id="957c5-142">**Q: How are IP addresses calculated in hello sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="957c5-143">**A:** IP-adressen worden uitgegeven zodanig dat er is geen definitieve verbinding tussen een IP-adres en waar Hallo-computer met dit adres zich fysiek bevindt.</span><span class="sxs-lookup"><span data-stu-id="957c5-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where hello computer with that address is physically located.</span></span> <span data-ttu-id="957c5-144">Dit wordt bemoeilijkt door factoren, zoals mobiele providers en VPN-verbindingen uitgeven van IP-adressen uit de centrale pools vaak zeer ver van waar het clientapparaat Hallo daadwerkelijk wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="957c5-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where hello client device is actually used.</span></span> <span data-ttu-id="957c5-145">Hallo bovenstaande gegeven, is conversie van fysieke locatie van IP-adres tooa een zo goed mogelijke poging op basis van traceringen, registergegevens, omgekeerde uiterlijk-ups en andere informatie.</span><span class="sxs-lookup"><span data-stu-id="957c5-145">Given hello above, converting IP address tooa physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
