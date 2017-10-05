---
title: Aan de slag met Azure AD Privileged Identity Management | Microsoft Docs
description: Informatie over het beheren van bevoegde identiteiten met de Azure Active Directory Privileged Identity Management-toepassing in de Azure Portal.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 17cdff033cc3dbb199d11c3b8ac1acbc92499877
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a><span data-ttu-id="86959-103">Aan de slag met Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="86959-103">Start using Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="86959-104">Met Azure Active Directory (AD) Privileged Identity Management kunt u toegang binnen de organisatie beheren, controleren en bewaken.</span><span class="sxs-lookup"><span data-stu-id="86959-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="86959-105">Dit bereik is inclusief toegang tot resources in Azure AD en andere Microsoft-onlineservices zoals Office 365 en Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="86959-105">This scope includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="86959-106">In dit artikel leest u hoe u de PIM-app van Azure AD toevoegt aan uw Azure Portal-dashboard.</span><span class="sxs-lookup"><span data-stu-id="86959-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="86959-107">De Privileged Identity Management-toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="86959-107">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="86959-108">Voordat u Azure AD Privileged Identity Management gebruikt, moet u de toepassing toevoegen aan uw Azure Portal-dashboard.</span><span class="sxs-lookup"><span data-stu-id="86959-108">Before you use Azure AD Privileged Identity Management, you need to add the application to your Azure portal dashboard.</span></span>

1. <span data-ttu-id="86959-109">Meld u aan bij de [Azure Portal](https://portal.azure.com/) als globale beheerder van uw directory.</span><span class="sxs-lookup"><span data-stu-id="86959-109">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="86959-110">Als uw organisatie meerdere directory's heeft, selecteert u uw gebruikersnaam rechtsboven in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="86959-110">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="86959-111">Selecteer de map waar u PIM gaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="86959-111">Select the directory where you want to use PIM.</span></span>
3. <span data-ttu-id="86959-112">Selecteer **Meer services** en gebruik het tekstvak Filteren om te zoeken naar **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="86959-112">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="86959-113">Schakel **Vastmaken aan dashboard** in en klik op de knop **Maken**.</span><span class="sxs-lookup"><span data-stu-id="86959-113">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="86959-114">De Privileged Identity Management-toepassing wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="86959-114">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="86959-115">Als u de eerste persoon bent die het gebruik van Azure AD Privileged Identity Management in uw map gebruikt, krijgt u automatisch de wollen **Beveiligingsbeheerder** en **Beheerder met bevoegdheid** toegewezen in de map.</span><span class="sxs-lookup"><span data-stu-id="86959-115">If you're the first person to use Azure AD Privileged Identity Management in your directory, you are automatically assigned the **Security administrator** and **Privileged role administrator** roles in the directory.</span></span> <span data-ttu-id="86959-116">Alleen beheerders met bevoegdheid kunnen roltoewijzingen van gebruikers beheren.</span><span class="sxs-lookup"><span data-stu-id="86959-116">Only privileged role administrators can manage role assignments of users.</span></span> <span data-ttu-id="86959-117">Bovendien kunt u de [beveiligingswizard](active-directory-privileged-identity-management-security-wizard.md) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="86959-117">In addition, you may choose to run the [security wizard.](active-directory-privileged-identity-management-security-wizard.md)</span></span> <span data-ttu-id="86959-118">Deze helpt u bij de eerste ervaring met detectie en toewijzing.</span><span class="sxs-lookup"><span data-stu-id="86959-118">that walks you through the initial discovery and assignment experience.</span></span>

## <a name="navigate-to-your-tasks"></a><span data-ttu-id="86959-119">Navigeer naar uw taken</span><span class="sxs-lookup"><span data-stu-id="86959-119">Navigate to your tasks</span></span>
<span data-ttu-id="86959-120">Nadat Azure AD Privileged Identity Management is ingesteld, ziet u de navigatieblade telkens wanneer u de toepassing opent.</span><span class="sxs-lookup"><span data-stu-id="86959-120">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span> <span data-ttu-id="86959-121">Gebruik deze blade om de taken voor identiteitsbeheer te voltooien.</span><span class="sxs-lookup"><span data-stu-id="86959-121">Use this blade to accomplish your identity management tasks.</span></span>

![Taken op het hoogste niveau voor PIM - schermopname](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* <span data-ttu-id="86959-123">**Mijn rollen**: hiermee gaat u naar de lijst met functies die aan u zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="86959-123">**My Roles** takes you to a list of roles that are assigned to you.</span></span> <span data-ttu-id="86959-124">Dit gedeelte is waar u alle functies activeert waarvoor u in aanmerking komt.</span><span class="sxs-lookup"><span data-stu-id="86959-124">This section is where you activate any roles that you are eligible for.</span></span>
* <span data-ttu-id="86959-125">**Aanvragen goedkeuren (preview)**: hiermee geeft u een lijst weer met openstaande activeringsaanvragen van gebruikers in uw map.</span><span class="sxs-lookup"><span data-stu-id="86959-125">**Approve Requests (Preview)** displays a list of pending activation requests from users in your directory.</span></span> [<span data-ttu-id="86959-126">Meer informatie.</span><span class="sxs-lookup"><span data-stu-id="86959-126">Learn more.</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* <span data-ttu-id="86959-127">**Aanvragen in behandeling (preview)**: hiermee geeft u alle huidige aanvragen voor activering weer.</span><span class="sxs-lookup"><span data-stu-id="86959-127">**Pending Requests (Preview)** displays any current requests to have made to activate.</span></span>
* <span data-ttu-id="86959-128">**Toegang beoordelen**: hiermee gaat u naar eventuele in behandeling zijnde toegangsbeoordelingen die u moet voltooien, of u nu de toegang beoordeelt voor uzelf of voor iemand anders.</span><span class="sxs-lookup"><span data-stu-id="86959-128">**Review Access** takes you to any pending access reviews that you need to complete, whether you're reviewing access for yourself or someone else.</span></span>
* <span data-ttu-id="86959-129">**Azure AD Directory-rollen**: dit dashboard bevindt zich onder het gedeelte 'Beheren’. Hiermee kunnen beheerders met bevoorrechte rollen roltoewijzingen beheren, instellingen voor rolactivering wijzigen, toegangsbeoordelingen starten en meer.</span><span class="sxs-lookup"><span data-stu-id="86959-129">**Azure AD Directory Roles** located under the 'Manage' section is the dashboard for privileged role admins to manage role assignments, change role activation settings, start access reviews, and more.</span></span> <span data-ttu-id="86959-130">De opties in dit dashboard zijn uitgeschakeld voor iedereen die geen beheerder met een bevoorrechte rol is.</span><span class="sxs-lookup"><span data-stu-id="86959-130">The options in this dashboard are disabled for anyone who isn't a privileged role administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86959-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="86959-131">Next steps</span></span>
<span data-ttu-id="86959-132">Het [overzicht van Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) bevat meer informatie over het beheren van beheerderstoegang in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="86959-132">The [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) includes more details on how you can manage administrative access in your organization.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
