---
title: Probleem met toegang tot de toepassing zelf | Microsoft Docs
description: Problemen met betrekking tot toegang tot de toepassing zelf oplossen
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
ms.openlocfilehash: 217726709a1fdb02275de5a76a1352ea9c350600
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="475b2-103">Probleem met toegang tot selfservice-toepassingen</span><span class="sxs-lookup"><span data-stu-id="475b2-103">Problem using self-service application access</span></span>

<span data-ttu-id="475b2-104">Toegang tot de toepassing zelf is een uitstekende manier om toestaan dat gebruikers zelf detecteren toepassingen, toestaan de bedrijfsgroep goedkeuren van toegang tot deze toepassingen.</span><span class="sxs-lookup"><span data-stu-id="475b2-104">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="475b2-105">U kunt de bedrijfsgroep voor het beheren van de referenties die zijn toegewezen aan deze gebruikers voor het recht wachtwoord eenmalige aanmelding op toepassingen van hun panelen toegang toestaan.</span><span class="sxs-lookup"><span data-stu-id="475b2-105">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="475b2-106">Voordat uw gebruikers toepassingen van hun Toegangsvenster automatisch detecteren kunnen, moet u inschakelen **toegang tot toepassingen Self-service** naar elke toepassing die u wilt toestaan dat gebruikers zelf detecteren en aanvragen toegang tot.</span><span class="sxs-lookup"><span data-stu-id="475b2-106">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="475b2-107">Algemene problemen om eerst te controleren</span><span class="sxs-lookup"><span data-stu-id="475b2-107">General issues to check first</span></span>

-   <span data-ttu-id="475b2-108">Zorg ervoor dat de toegang tot selfservice toepassing correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="475b2-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="475b2-109">Zie ' toegang tot de toepassing zelf configureren '.</span><span class="sxs-lookup"><span data-stu-id="475b2-109">See “How to configure self-service application access”.</span></span>

-   <span data-ttu-id="475b2-110">Zorg ervoor dat de gebruiker of groep is ingeschakeld voor het aanvragen van toegang tot de toepassing zelf.</span><span class="sxs-lookup"><span data-stu-id="475b2-110">Make sure the user or group has been enabled to request self-service application access.</span></span>

-   <span data-ttu-id="475b2-111">Zorg ervoor dat de gebruiker de juiste plaats voor toegang tot toepassingen selfservice bezoekt.</span><span class="sxs-lookup"><span data-stu-id="475b2-111">Make sure the user is visiting the correct place for self-service application access.</span></span> <span data-ttu-id="475b2-112">gebruikers kunnen navigeren naar hun [toepassing Toegangspaneel](https://myapps.microsoft.com/) en klik op de **+ toevoegen** om te zoeken van de apps waarmee u toegang tot selfservice hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="475b2-112">users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled self-service access.</span></span>

-   <span data-ttu-id="475b2-113">Als toegang tot de toepassing zelf onlangs is geconfigureerd, probeert aan te melden en afmelden opnieuw naar de gebruiker toegang deelvenster na een paar minuten om te zien als de wijzigingen access selfservicegebruikers hebben gestaan.</span><span class="sxs-lookup"><span data-stu-id="475b2-113">If self-service application access was just recently configured, try to sign in and out again into the user’s Access Panel after a few minutes to see if the self-service access changes have appeared.</span></span>

## <a name="how-to-configure-self-service-application-access"></a><span data-ttu-id="475b2-114">Toegang tot selfservice-toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="475b2-114">How to configure self-service application access</span></span>

<span data-ttu-id="475b2-115">Voor self-service toepassing toegang tot een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="475b2-115">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="475b2-116">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="475b2-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="475b2-117">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="475b2-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="475b2-118">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="475b2-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="475b2-119">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="475b2-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="475b2-120">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="475b2-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="475b2-121">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="475b2-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="475b2-122">Selecteer de toepassing die u wilt inschakelen, Self-service toegang tot in de lijst.</span><span class="sxs-lookup"><span data-stu-id="475b2-122">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="475b2-123">Nadat de toepassing wordt geladen, klikt u op **Self-service** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="475b2-123">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="475b2-124">Voor self-service toepassing toegang voor deze toepassing, schakelt u de **toestaan dat gebruikers toegang tot deze toepassing aanvragen?** in-of uitschakelen op **Ja.**</span><span class="sxs-lookup"><span data-stu-id="475b2-124">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="475b2-125">Klik vervolgens op de selector naast het label om te selecteren in de groep waartoe gebruikers die aanvragen toegang tot deze toepassing moet worden toegevoegd, **voor welke groep toegewezen gebruikers worden toegevoegd?** en selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="475b2-125">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="475b2-126">**Optioneel:** als u wilt een zakelijke goedkeuringsprocedure voordat gebruikers toegang hebben, stelt u de **moeten worden goedgekeurd voordat het verlenen van toegang tot deze toepassing?** in-of uitschakelen op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="475b2-126">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="475b2-127">**Optioneel: voor toepassingen die gebruikmaken van wachtwoord eenmalige aanmelding alleen op** als u deze bedrijven fiatteurs om op te geven van de wachtwoorden die worden verzonden naar deze toepassing voor goedgekeurde gebruikers toestaan wilt, stelt u de **fiatteurs instellen van wachtwoorden voor deze toepassing van de gebruiker toestaan?** in-of uitschakelen op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="475b2-127">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="475b2-128">**Optioneel:** om op te geven de zakelijke fiatteurs die zijn toegestaan voor het goedkeuren van toegang tot deze toepassing, klikt u op de selector naast het label **die is toegestaan voor het goedkeuren van toegang tot deze toepassing?** maximaal 10 afzonderlijke business goedkeurders selecteren.</span><span class="sxs-lookup"><span data-stu-id="475b2-128">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="475b2-129">Groepen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="475b2-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="475b2-130">**Optioneel:** **voor toepassingen die functies zichtbaar**, als u wilt Self-service goedgekeurde gebruikers toewijzen aan een rol, klikt u op de selector naast de **welke rol u gebruikers wilt toewijzen in deze toepassing?** om de rol waaraan u deze gebruikers worden toegewezen te selecteren.</span><span class="sxs-lookup"><span data-stu-id="475b2-130">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="475b2-131">Klik op de **opslaan** knop aan de bovenkant van de blade om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="475b2-131">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="475b2-132">Nadat u de configuratie van Self-Service toepassing hebt voltooid, gebruikers kunnen navigeren naar hun [toepassing Toegangspaneel](https://myapps.microsoft.com/) en klik op de **+ toevoegen** om te zoeken van de apps waarmee u toegang tot selfservice hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="475b2-132">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="475b2-133">Zakelijke goedkeurders er ook een melding in hun [Toegangspaneel toepassing](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="475b2-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="475b2-134">U kunt een melding wanneer een gebruiker heeft toegang tot een toepassing die hun goedkeuring vereist aangevraagd e-mail inschakelen.</span><span class="sxs-lookup"><span data-stu-id="475b2-134">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="475b2-135">Deze goedkeuringen ondersteuning voor één werkstromen voor goedkeuring, wat betekent dat als u meerdere goedkeurders opgeeft, een enkele fiatteur toegang tot de toepassing goedkeuren kan.</span><span class="sxs-lookup"><span data-stu-id="475b2-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="475b2-136">Als bovenstaande stappen voor probleemoplossing het probleem niet oplossen</span><span class="sxs-lookup"><span data-stu-id="475b2-136">If these troubleshooting steps do not resolve the issue</span></span> 

<span data-ttu-id="475b2-137">een ondersteuningsticket opent met de volgende informatie, indien beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="475b2-137">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="475b2-138">Correlatie fout-ID</span><span class="sxs-lookup"><span data-stu-id="475b2-138">Correlation error ID</span></span>

-   <span data-ttu-id="475b2-139">UPN (e-mailadres van de gebruiker)</span><span class="sxs-lookup"><span data-stu-id="475b2-139">UPN (user email address)</span></span>

-   <span data-ttu-id="475b2-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="475b2-140">TenantID</span></span>

-   <span data-ttu-id="475b2-141">Browsertype</span><span class="sxs-lookup"><span data-stu-id="475b2-141">Browser type</span></span>

-   <span data-ttu-id="475b2-142">Tijdzone en de tijd/tijdsbestek tijdens fout optreedt</span><span class="sxs-lookup"><span data-stu-id="475b2-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="475b2-143">Fiddler traceringen</span><span class="sxs-lookup"><span data-stu-id="475b2-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="475b2-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="475b2-144">Next steps</span></span>
[<span data-ttu-id="475b2-145">Azure Active Directory instellen voor selfservicegroepsbeheer</span><span class="sxs-lookup"><span data-stu-id="475b2-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
