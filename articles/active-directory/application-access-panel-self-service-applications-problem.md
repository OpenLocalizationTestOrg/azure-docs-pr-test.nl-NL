---
title: met behulp van de toegang tot de toepassing zelf aaaProblem | Microsoft Docs
description: Oplossen van problemen gerelateerde tooself servicetoepassing toegang
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="6f3b1-103">Probleem met toegang tot selfservice-toepassingen</span><span class="sxs-lookup"><span data-stu-id="6f3b1-103">Problem using self-service application access</span></span>

<span data-ttu-id="6f3b1-104">Toegang tot de toepassing zelf is een uitstekende manier tooallow gebruikers tooself-toepassingen detecteren, eventueel Hallo business groep toestaan tooapprove toothose toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-104">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="6f3b1-105">U kunt toestaan Hallo business groep toomanage Hallo referenties toegewezen gebruikers toothose voor wachtwoord eenmalige aanmelding op toepassingen rechtstreeks vanuit hun panelen toegang.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-105">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="6f3b1-106">Voordat u uw gebruikers kunnen toepassingen van hun Toegangsvenster automatisch detecteren, moet u tooenable **toegang tot toepassingen Self-service** tooany toepassingen die u wenst dat tooallow gebruikers tooself-detecteren en om toegang te vragen.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-106">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="6f3b1-107">Algemene problemen toocheck eerst</span><span class="sxs-lookup"><span data-stu-id="6f3b1-107">General issues toocheck first</span></span>

-   <span data-ttu-id="6f3b1-108">Zorg ervoor dat de toegang tot selfservice toepassing correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="6f3b1-109">Zie 'Hoe tooconfigure selfservice toepassing toegang krijgen tot'.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-109">See “How tooconfigure self-service application access”.</span></span>

-   <span data-ttu-id="6f3b1-110">Ervoor zorgen dat Hallo gebruiker of groep is toorequest selfservice toepassing toegang ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-110">Make sure hello user or group has been enabled toorequest self-service application access.</span></span>

-   <span data-ttu-id="6f3b1-111">Zorg ervoor dat Hallo gebruiker de juiste plaats Hallo voor toegang tot toepassingen selfservice bezoekt.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-111">Make sure hello user is visiting hello correct place for self-service application access.</span></span> <span data-ttu-id="6f3b1-112">gebruikers kunnen navigeren tootheir [toepassing Toegangspaneel](https://myapps.microsoft.com/) en klik op Hallo **+ toevoegen** knop toofind Hallo apps toowhich u access selfservicegebruikers hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-112">users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled self-service access.</span></span>

-   <span data-ttu-id="6f3b1-113">Als toegang tot de toepassing zelf onlangs is geconfigureerd, opnieuw toosign in en uit in het toegangsvenster Hallo van de gebruiker na een paar minuten toosee als Hallo access selfservicegebruikers wijzigingen hebben gestaan.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-113">If self-service application access was just recently configured, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello self-service access changes have appeared.</span></span>

## <a name="how-tooconfigure-self-service-application-access"></a><span data-ttu-id="6f3b1-114">Hoe tooconfigure selfservice toepassing openen</span><span class="sxs-lookup"><span data-stu-id="6f3b1-114">How tooconfigure self-service application access</span></span>

<span data-ttu-id="6f3b1-115">tooenable selfservice toepassing toegang tooan toepassing hello stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="6f3b1-115">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="6f3b1-116">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="6f3b1-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="6f3b1-117">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6f3b1-118">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6f3b1-119">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6f3b1-120">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="6f3b1-121">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="6f3b1-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="6f3b1-122">Selecteer gewenste tooenable Self-service toofrom Hallo toegangslijst Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-122">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="6f3b1-123">Nadat de toepassing hello wordt geladen, klikt u op **Self-service** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-123">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6f3b1-124">tooenable toegang tot de toepassing Self-service voor deze toepassing, schakelt u Hallo **toorequest access toothis-toepassing voor gebruikers toestaan?** te schakelen**Ja.**</span><span class="sxs-lookup"><span data-stu-id="6f3b1-124">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="6f3b1-125">Tooselect hello toowhich gebruikers die een groep aanvragen toegang toothis toepassing moet worden toegevoegd, klik vervolgens op Hallo selector volgende toohello label **toowhich groep moet worden toegewezen gebruikers worden toegevoegd?** en selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-125">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="6f3b1-126">**Optioneel:** als u toorequire goedkeuring van een zakelijke wenst voordat gebruikers toegang kunt krijgen, stelt u Hallo **moeten worden goedgekeurd voordat u verleent toegang toothis toepassing?** te schakelen**Ja**.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-126">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="6f3b1-127">**Optioneel: voor toepassingen die gebruikmaken van wachtwoord eenmalige aanmelding alleen op** desgewenst tooallow deze bedrijven goedkeurders toospecify Hallo wachtwoorden die worden verzonden toothis toepassingen voor goedgekeurde gebruikers instellen Hallo **toestaan goedkeurders tooset wachtwoorden van de gebruiker voor deze toepassing?**  te schakelen**Ja**.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-127">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="6f3b1-128">**Optioneel:** toospecify Hallo business goedkeurders die mogen tooapprove toegang toothis toepassing, klikt u op Hallo selector volgende toohello label **die tooapprove access toothis-toepassing is toegestaan?** tooselect up too10 afzonderlijke business goedkeurders.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-128">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="6f3b1-129">Groepen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="6f3b1-130">**Optioneel:** **voor toepassingen die functies zichtbaar**, indien tooassign Self-service goedgekeurde gebruikers tooa rol gewenst, klikt u op Hallo selector volgende toohello **toowhich rol moeten gebruikers worden toegewezen in dit toepassing?**  tooselect Hallo rol toowhich deze gebruikers moeten worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-130">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="6f3b1-131">Klik op Hallo **opslaan** knop bovenaan Hallo Hallo blade toofinish.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-131">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="6f3b1-132">Nadat u de configuratie van Self-Service toepassing hebt voltooid, gebruikers tootheir kunnen navigeren [toepassing Toegangspaneel](https://myapps.microsoft.com/) en klik op Hallo **+ toevoegen** knop toofind Hallo apps toowhich u hebt ingeschakeld Selfservice toegang.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-132">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="6f3b1-133">Zakelijke goedkeurders er ook een melding in hun [Toegangspaneel toepassing](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="6f3b1-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="6f3b1-134">U kunt een melding wanneer een gebruiker toegang tooan toepassing waarvoor goedkeuring is aangevraagd e-mail inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-134">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="6f3b1-135">Deze goedkeuringen ondersteuning voor één werkstromen voor goedkeuring, wat betekent dat als u meerdere goedkeurders opgeeft, een enkele fiatteur access toohello-toepassing goedkeuren kan.</span><span class="sxs-lookup"><span data-stu-id="6f3b1-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="6f3b1-136">Als u deze stappen voor probleemoplossing Hallo probleem niet verhelpen</span><span class="sxs-lookup"><span data-stu-id="6f3b1-136">If these troubleshooting steps do not resolve hello issue</span></span> 

<span data-ttu-id="6f3b1-137">Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="6f3b1-137">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="6f3b1-138">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="6f3b1-138">Correlation error ID</span></span>

-   <span data-ttu-id="6f3b1-139">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="6f3b1-139">UPN (user email address)</span></span>

-   <span data-ttu-id="6f3b1-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="6f3b1-140">TenantID</span></span>

-   <span data-ttu-id="6f3b1-141">Browsertype</span><span class="sxs-lookup"><span data-stu-id="6f3b1-141">Browser type</span></span>

-   <span data-ttu-id="6f3b1-142">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="6f3b1-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="6f3b1-143">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="6f3b1-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f3b1-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6f3b1-144">Next steps</span></span>
[<span data-ttu-id="6f3b1-145">Azure Active Directory instellen voor selfservicegroepsbeheer</span><span class="sxs-lookup"><span data-stu-id="6f3b1-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
