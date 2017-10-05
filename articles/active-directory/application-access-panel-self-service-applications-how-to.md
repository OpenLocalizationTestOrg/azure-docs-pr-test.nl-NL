---
title: Het gebruik van toegang tot de toepassing zelf | Microsoft Docs
description: Toegang tot de toepassing Self-Service gebruikers kunnen hun eigen toepassingen zoeken inschakelen
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
ms.openlocfilehash: 08a05a70d976104d4e0a37b0a0dd15042b0212d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-self-service-application-access"></a><span data-ttu-id="95168-103">Toegang tot toepassingen selfservice gebruiken</span><span class="sxs-lookup"><span data-stu-id="95168-103">How to use self-service application access</span></span>

<span data-ttu-id="95168-104">Voordat uw gebruikers toepassingen van hun Toegangsvenster automatisch detecteren kunnen, moet u inschakelen **toegang tot toepassingen Self-service** naar elke toepassing die u wilt toestaan dat gebruikers zelf detecteren en aanvragen toegang tot.</span><span class="sxs-lookup"><span data-stu-id="95168-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

<span data-ttu-id="95168-105">Deze functie is een uitstekende manier om tijd en geld besparen als een IT-groep, en wordt sterk aanbevolen als onderdeel van een implementatie van moderne toepassingen met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95168-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="95168-106">Met deze functie kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="95168-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="95168-107">Kunnen gebruikers zelf detecteren toepassingen van de [toepassing Toegangsvenster](https://myapps.microsoft.com/) zonder te proberen alles van de IT-groep.</span><span class="sxs-lookup"><span data-stu-id="95168-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span></span>

-   <span data-ttu-id="95168-108">Deze gebruikers toevoegen aan een vooraf geconfigureerde groep, zodat u kunt zien wie toegang heeft aangevraagd, toegang verwijderen en de aan hen toegewezen rollen beheren.</span><span class="sxs-lookup"><span data-stu-id="95168-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span></span>

-   <span data-ttu-id="95168-109">Een zakelijke goedkeurder goed te keuren toegangsaanvragen van toepassingen zodat de IT-groep niet toestaan.</span><span class="sxs-lookup"><span data-stu-id="95168-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span></span>

-   <span data-ttu-id="95168-110">Configureer desgewenst maximaal 10 personen die toegang tot deze toepassing kunnen goedkeuren.</span><span class="sxs-lookup"><span data-stu-id="95168-110">Optionally configure up to 10 individuals who may approve access to this application.</span></span>

-   <span data-ttu-id="95168-111">Een bedrijf toestaan goedkeurder in te stellen de wachtwoorden die gebruikers kunt gebruiken om te aan te melden aan de toepassing, rechts van de zakelijke goedkeurder [Toegangspaneel toepassing](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="95168-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="95168-112">Optioneel automatisch toewijzen self-service gebruikers rechtstreeks toegewezen aan de toepassingsrol van een.</span><span class="sxs-lookup"><span data-stu-id="95168-112">Optionally automatically assign self-service assigned users to an application role directly.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="95168-113">Toegang tot de toepassing Self-Service gebruikers kunnen hun eigen toepassingen zoeken inschakelen</span><span class="sxs-lookup"><span data-stu-id="95168-113">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="95168-114">Toegang tot de toepassing zelf is een uitstekende manier om toestaan dat gebruikers zelf detecteren toepassingen, toestaan de bedrijfsgroep goedkeuren van toegang tot deze toepassingen.</span><span class="sxs-lookup"><span data-stu-id="95168-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="95168-115">U kunt de bedrijfsgroep voor het beheren van de referenties die zijn toegewezen aan deze gebruikers voor het recht wachtwoord eenmalige aanmelding op toepassingen van hun panelen toegang toestaan.</span><span class="sxs-lookup"><span data-stu-id="95168-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="95168-116">Voor self-service toepassing toegang tot een toepassing, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="95168-116">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="95168-117">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**</span><span class="sxs-lookup"><span data-stu-id="95168-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="95168-118">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="95168-118">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="95168-119">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="95168-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="95168-120">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="95168-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="95168-121">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="95168-121">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="95168-122">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="95168-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="95168-123">Selecteer de toepassing die u wilt inschakelen, Self-service toegang tot in de lijst.</span><span class="sxs-lookup"><span data-stu-id="95168-123">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="95168-124">Nadat de toepassing wordt geladen, klikt u op **Self-service** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="95168-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="95168-125">Voor self-service toepassing toegang voor deze toepassing, schakelt u de **toestaan dat gebruikers toegang tot deze toepassing aanvragen?** in-of uitschakelen op **Ja.**</span><span class="sxs-lookup"><span data-stu-id="95168-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="95168-126">Klik vervolgens op de selector naast het label om te selecteren in de groep waartoe gebruikers die aanvragen toegang tot deze toepassing moet worden toegevoegd, **voor welke groep toegewezen gebruikers worden toegevoegd?** en selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="95168-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="95168-127">**Optioneel:** als u wilt een zakelijke goedkeuringsprocedure voordat gebruikers toegang hebben, stelt u de **moeten worden goedgekeurd voordat het verlenen van toegang tot deze toepassing?** in-of uitschakelen op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="95168-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="95168-128">**Optioneel: voor toepassingen die gebruikmaken van wachtwoord eenmalige aanmelding alleen op** als u deze bedrijven fiatteurs om op te geven van de wachtwoorden die worden verzonden naar deze toepassing voor goedgekeurde gebruikers toestaan wilt, stelt u de **fiatteurs instellen van wachtwoorden voor deze toepassing van de gebruiker toestaan?** in-of uitschakelen op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="95168-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="95168-129">**Optioneel:** om op te geven de zakelijke fiatteurs die zijn toegestaan voor het goedkeuren van toegang tot deze toepassing, klikt u op de selector naast het label **die is toegestaan voor het goedkeuren van toegang tot deze toepassing?** maximaal 10 afzonderlijke business goedkeurders selecteren.</span><span class="sxs-lookup"><span data-stu-id="95168-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

   * <span data-ttu-id="95168-130">Groepen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="95168-130">Groups are not supported.</span></span>

13. <span data-ttu-id="95168-131">**Optioneel:** **voor toepassingen die functies zichtbaar**, als u wilt Self-service goedgekeurde gebruikers toewijzen aan een rol, klikt u op de selector naast de **welke rol u gebruikers wilt toewijzen in deze toepassing?** om de rol waaraan u deze gebruikers worden toegewezen te selecteren.</span><span class="sxs-lookup"><span data-stu-id="95168-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="95168-132">Klik op de **opslaan** knop aan de bovenkant van de blade om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="95168-132">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="95168-133">Nadat u de configuratie van Self-Service toepassing hebt voltooid, gebruikers kunnen navigeren naar hun [toepassing Toegangspaneel](https://myapps.microsoft.com/) en klik op de **+ toevoegen** om te zoeken van de apps waarmee u toegang tot selfservice hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="95168-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="95168-134">Zakelijke goedkeurders er ook een melding in hun [Toegangspaneel toepassing](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="95168-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="95168-135">U kunt een melding wanneer een gebruiker heeft toegang tot een toepassing die hun goedkeuring vereist aangevraagd e-mail inschakelen.</span><span class="sxs-lookup"><span data-stu-id="95168-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="95168-136">Deze goedkeuringen ondersteuning voor één werkstromen voor goedkeuring, wat betekent dat als u meerdere goedkeurders opgeeft, een enkele fiatteur toegang tot de toepassing goedkeuren kan.</span><span class="sxs-lookup"><span data-stu-id="95168-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95168-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="95168-137">Next steps</span></span>
[<span data-ttu-id="95168-138">Azure Active Directory instellen voor selfservicegroepsbeheer</span><span class="sxs-lookup"><span data-stu-id="95168-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
