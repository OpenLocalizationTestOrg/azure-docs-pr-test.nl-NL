---
title: toegang tot de toepassing zelf van de aaaHow toouse | Microsoft Docs
description: Selfservice toepassing toegang tooallow gebruikers toofind hun eigen toepassingen inschakelen
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
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a><span data-ttu-id="87986-103">Hoe toouse selfservice toepassing openen</span><span class="sxs-lookup"><span data-stu-id="87986-103">How toouse self-service application access</span></span>

<span data-ttu-id="87986-104">Voordat u uw gebruikers kunnen toepassingen van hun Toegangsvenster automatisch detecteren, moet u tooenable **toegang tot toepassingen Self-service** tooany toepassingen die u wenst dat tooallow gebruikers tooself-detecteren en om toegang te vragen.</span><span class="sxs-lookup"><span data-stu-id="87986-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="87986-105">Deze functie is een uitstekende manier voor u toosave tijd en geld als een IT-groep, en het wordt sterk aanbevolen als onderdeel van een implementatie van moderne toepassingen met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="87986-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="87986-106">Met deze functie kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="87986-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="87986-107">Kunnen gebruikers zelf detecteren toepassingen van Hallo [toepassing Toegangsvenster](https://myapps.microsoft.com/) zonder te proberen alles Hallo IT-groep.</span><span class="sxs-lookup"><span data-stu-id="87986-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="87986-108">Deze vooraf geconfigureerde groep met gebruikers tooa toevoegen zodat u kunt zien wie toegang heeft aangevraagd, toegang verwijderen en Hallo rollen toegewezen toothem beheren.</span><span class="sxs-lookup"><span data-stu-id="87986-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="87986-109">Eventueel een zakelijke goedkeurder tooapprove toepassing toegangsaanvragen toestaan zodat Hallo IT-groep niet te worden hoeven.</span><span class="sxs-lookup"><span data-stu-id="87986-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="87986-110">Configureer desgewenst up too10 personen die toegang toothis toepassing kunnen goedkeuren.</span><span class="sxs-lookup"><span data-stu-id="87986-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="87986-111">Eventueel tooset Hallo wachtwoorden toestaan een zakelijke goedkeurder die gebruikers toosign kunnen gebruiken in de toepassing toohello, rechts van Hallo zakelijke goedkeurder [Toegangspaneel toepassing](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="87986-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="87986-112">Optioneel automatisch toegewezen selfservicegebruikers tooan toepassingsrol rechtstreeks toewijzen.</span><span class="sxs-lookup"><span data-stu-id="87986-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="87986-113">Selfservice toepassing toegang tooallow gebruikers toofind hun eigen toepassingen inschakelen</span><span class="sxs-lookup"><span data-stu-id="87986-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="87986-114">Toegang tot de toepassing zelf is een uitstekende manier tooallow gebruikers tooself-toepassingen detecteren, eventueel Hallo business groep toestaan tooapprove toothose toepassingen.</span><span class="sxs-lookup"><span data-stu-id="87986-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="87986-115">U kunt toestaan Hallo business groep toomanage Hallo referenties toegewezen gebruikers toothose voor wachtwoord eenmalige aanmelding op toepassingen rechtstreeks vanuit hun panelen toegang.</span><span class="sxs-lookup"><span data-stu-id="87986-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="87986-116">tooenable selfservice toepassing toegang tooan toepassing hello stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="87986-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="87986-117">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="87986-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="87986-118">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="87986-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87986-119">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="87986-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87986-120">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="87986-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87986-121">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="87986-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="87986-122">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="87986-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="87986-123">Selecteer gewenste tooenable Self-service toofrom Hallo toegangslijst Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="87986-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="87986-124">Nadat de toepassing hello wordt geladen, klikt u op **Self-service** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="87986-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87986-125">tooenable toegang tot de toepassing Self-service voor deze toepassing, schakelt u Hallo **toorequest access toothis-toepassing voor gebruikers toestaan?** te schakelen**Ja.**</span><span class="sxs-lookup"><span data-stu-id="87986-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="87986-126">Tooselect hello toowhich gebruikers die een groep aanvragen toegang toothis toepassing moet worden toegevoegd, klik vervolgens op Hallo selector volgende toohello label **toowhich groep moet worden toegewezen gebruikers worden toegevoegd?** en selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="87986-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="87986-127">**Optioneel:** als u toorequire goedkeuring van een zakelijke wenst voordat gebruikers toegang kunt krijgen, stelt u Hallo **moeten worden goedgekeurd voordat u verleent toegang toothis toepassing?** te schakelen**Ja**.</span><span class="sxs-lookup"><span data-stu-id="87986-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="87986-128">**Optioneel: voor toepassingen die gebruikmaken van wachtwoord eenmalige aanmelding alleen op** desgewenst tooallow deze bedrijven goedkeurders toospecify Hallo wachtwoorden die worden verzonden toothis toepassingen voor goedgekeurde gebruikers instellen Hallo **toestaan goedkeurders tooset wachtwoorden van de gebruiker voor deze toepassing?**  te schakelen**Ja**.</span><span class="sxs-lookup"><span data-stu-id="87986-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="87986-129">**Optioneel:** toospecify Hallo business goedkeurders die mogen tooapprove toegang toothis toepassing, klikt u op Hallo selector volgende toohello label **die tooapprove access toothis-toepassing is toegestaan?** tooselect up too10 afzonderlijke business goedkeurders.</span><span class="sxs-lookup"><span data-stu-id="87986-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   * <span data-ttu-id="87986-130">Groepen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="87986-130">Groups are not supported.</span></span>

13. <span data-ttu-id="87986-131">**Optioneel:** **voor toepassingen die functies zichtbaar**, indien tooassign Self-service goedgekeurde gebruikers tooa rol gewenst, klikt u op Hallo selector volgende toohello **toowhich rol moeten gebruikers worden toegewezen in dit toepassing?**  tooselect Hallo rol toowhich deze gebruikers moeten worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="87986-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="87986-132">Klik op Hallo **opslaan** knop bovenaan Hallo Hallo blade toofinish.</span><span class="sxs-lookup"><span data-stu-id="87986-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="87986-133">Nadat u de configuratie van Self-Service toepassing hebt voltooid, gebruikers tootheir kunnen navigeren [toepassing Toegangspaneel](https://myapps.microsoft.com/) en klik op Hallo **+ toevoegen** knop toofind Hallo apps toowhich u hebt ingeschakeld Selfservice toegang.</span><span class="sxs-lookup"><span data-stu-id="87986-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="87986-134">Zakelijke goedkeurders er ook een melding in hun [Toegangspaneel toepassing](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="87986-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="87986-135">U kunt een melding wanneer een gebruiker toegang tooan toepassing waarvoor goedkeuring is aangevraagd e-mail inschakelen.</span><span class="sxs-lookup"><span data-stu-id="87986-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="87986-136">Deze goedkeuringen ondersteuning voor één werkstromen voor goedkeuring, wat betekent dat als u meerdere goedkeurders opgeeft, een enkele fiatteur access toohello-toepassing goedkeuren kan.</span><span class="sxs-lookup"><span data-stu-id="87986-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87986-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87986-137">Next steps</span></span>
[<span data-ttu-id="87986-138">Azure Active Directory instellen voor selfservicegroepsbeheer</span><span class="sxs-lookup"><span data-stu-id="87986-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
