---
title: De beveiligingswizard voor Azure AD Privileged Identity Management
description: De eerste keer dat u de extensie Azure Active Directory Privileged Identity Management, u krijgt een beveiligingswizard. In dit artikel beschrijft de stappen voor het gebruik van de wizard.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 260d178f3d8158411b3ad266e3b0d15edbebc722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="97d57-104">Gebruik de beveiligingswizard in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="97d57-104">Using the security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="97d57-105">Als u de eerste persoon Azure Privileged Identity Management (PIM) uitvoeren voor uw organisatie, u krijgt een wizard.</span><span class="sxs-lookup"><span data-stu-id="97d57-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="97d57-106">De wizard helpt u het beveiligingsrisico van bevoegde identiteiten en hoe u PIM gebruikt om te beperken die risico's begrijpen.</span><span class="sxs-lookup"><span data-stu-id="97d57-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="97d57-107">U hoeft niet te Breng wijzigingen in bestaande roltoewijzingen in de wizard als u liever dit later doen.</span><span class="sxs-lookup"><span data-stu-id="97d57-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="97d57-108">Wat u kunt verwachten</span><span class="sxs-lookup"><span data-stu-id="97d57-108">What to expect</span></span>
<span data-ttu-id="97d57-109">Voordat uw organisatie wordt gestart met behulp van PIM, alle roltoewijzingen permanent zijn: de gebruikers zich altijd in deze rollen zelfs als ze geen momenteel hun bevoegdheden nodig.</span><span class="sxs-lookup"><span data-stu-id="97d57-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="97d57-110">De eerste stap van de wizard ziet u een lijst met verhoogde rollen en hoeveel gebruikers zijn momenteel in deze rollen.</span><span class="sxs-lookup"><span data-stu-id="97d57-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="97d57-111">U kunt inzoomen een bepaalde rol voor meer informatie over gebruikers als een of meer van deze niet bekend bent.</span><span class="sxs-lookup"><span data-stu-id="97d57-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="97d57-112">De tweede stap van de wizard hebt u de mogelijkheid om te wijzigen van roltoewijzingen van beheerder.</span><span class="sxs-lookup"><span data-stu-id="97d57-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="97d57-113">Het is belangrijk dat u ten minste één globale beheerder en meer dan een beheerder met bevoorrechte rol met een organisatieaccount (dus niet door een Microsoft-account hebt).</span><span class="sxs-lookup"><span data-stu-id="97d57-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="97d57-114">Als er slechts één beheerder met bevoorrechte rol, kunnen de organisatie zich niet PIM beheren als dit account wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="97d57-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="97d57-115">Houd er ook roltoewijzingen permanente als een gebruiker heeft een Microsoft-account (een account dat ze gebruiken om aan te melden bij Microsoft-services zoals Skype en Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="97d57-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="97d57-116">Als u van plan bent MFA voor activering voor die rol is vereist, wordt die gebruiker vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="97d57-116">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="97d57-117">Nadat u wijzigingen hebt aangebracht, wordt de wizard niet meer weergegeven.</span><span class="sxs-lookup"><span data-stu-id="97d57-117">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="97d57-118">De volgende keer dat u of een andere beheerder met bevoorrechte rol gebruiken PIM, ziet u de PIM-dashboard.</span><span class="sxs-lookup"><span data-stu-id="97d57-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="97d57-119">Als u wilt toevoegen of verwijderen van gebruikers uit functies of wijzig de toewijzingen van permanente naar in aanmerking komende, leest u meer bij [toevoegen of verwijderen van de rol van een gebruiker](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="97d57-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="97d57-120">Als u wilt meer gebruikers om toegang te geven voor het beheren van PIM, meer informatie op [geeft toegang tot het beheer in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="97d57-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="97d57-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97d57-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

