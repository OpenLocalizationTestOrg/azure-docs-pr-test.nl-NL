---
title: wizard aaaThe Azure AD Privileged Identity Management-beveiliging
description: Hallo eerst die u hello Azure Active Directory Privileged Identity Management-extensie, gebruikt u krijgt een beveiligingswizard. Dit artikel wordt beschreven stappen voor het gebruik van de wizard Hallo Hallo.
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
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="a321d-104">Met behulp van de wizard Beveiliging Hallo in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="a321d-104">Using hello security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="a321d-105">Als u Hallo eerste persoon toorun Azure Privileged Identity Management (PIM) voor uw organisatie, u krijgt een wizard.</span><span class="sxs-lookup"><span data-stu-id="a321d-105">If you're hello first person toorun Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="a321d-106">Hallo wizard helpt u begrijpen Hallo beveiligingsrisico's van bevoegde identiteiten en hoe toouse PIM tooreduce die risico's.</span><span class="sxs-lookup"><span data-stu-id="a321d-106">hello wizard helps you understand hello security risks of privileged identities and how toouse PIM tooreduce those risks.</span></span> <span data-ttu-id="a321d-107">U hoeft niet toomake eventuele wijzigingen tooexisting roltoewijzingen in Hallo wizard als u liever toodo later.</span><span class="sxs-lookup"><span data-stu-id="a321d-107">You don't need toomake any changes tooexisting role assignments in hello wizard, if you prefer toodo it later.</span></span>

## <a name="what-tooexpect"></a><span data-ttu-id="a321d-108">Welke tooexpect</span><span class="sxs-lookup"><span data-stu-id="a321d-108">What tooexpect</span></span>
<span data-ttu-id="a321d-109">Voordat uw organisatie wordt gestart met behulp van PIM, alle roltoewijzingen zijn permanent: Hallo gebruikers bevinden zich altijd in deze rollen zelfs als ze geen momenteel hun bevoegdheden nodig.</span><span class="sxs-lookup"><span data-stu-id="a321d-109">Before your organization starts using PIM, all role assignments are permanent: hello users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="a321d-110">eerste stap van de wizard Hallo Hallo ziet u een lijst met verhoogde rollen en hoeveel gebruikers zijn momenteel in deze rollen.</span><span class="sxs-lookup"><span data-stu-id="a321d-110">hello first step of hello wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="a321d-111">U kunt inzoomen in tooa bepaalde rol toolearn meer informatie over gebruikers als een of meer van deze niet bekend bent.</span><span class="sxs-lookup"><span data-stu-id="a321d-111">You can drill in tooa particular role toolearn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="a321d-112">tweede stap van de wizard Hallo Hallo biedt u een kans toochange beheerder roltoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="a321d-112">hello second step of hello wizard gives you an opportunity toochange administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="a321d-113">Het is belangrijk dat u ten minste één globale beheerder en meer dan een beheerder met bevoorrechte rol met een organisatieaccount (dus niet door een Microsoft-account hebt).</span><span class="sxs-lookup"><span data-stu-id="a321d-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="a321d-114">Als er slechts één beheerder met bevoorrechte rol, zich Hallo organisatie niet kunnen toomanage PIM als dit account wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a321d-114">If there is only one privileged role administrator, hello organization will not be able toomanage PIM if that account is deleted.</span></span>
> <span data-ttu-id="a321d-115">Houd er ook roltoewijzingen permanente als een gebruiker heeft een Microsoft-account (een account dat ze gebruiken om toosign in tooMicrosoft services zoals Skype en Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="a321d-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use toosign in tooMicrosoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="a321d-116">Als u van plan toorequire MFA voor activering voor die functie bent, wordt die gebruiker worden vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="a321d-116">If you plan toorequire MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="a321d-117">Nadat u wijzigingen hebt aangebracht, wordt Hallo wizard niet meer weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a321d-117">After you have made changes, hello wizard will no longer show up.</span></span> <span data-ttu-id="a321d-118">Hallo ziet zodra u of een andere beheerder met bevoorrechte rol PIM, u Hallo PIM-dashboard.</span><span class="sxs-lookup"><span data-stu-id="a321d-118">hello next time you or another privileged role administrator use PIM, you will see hello PIM dashboard.</span></span>  

* <span data-ttu-id="a321d-119">Als u zou zoals tooadd of gebruikers van rollen verwijderen of toewijzingen van permanente tooeligible wijzigen, lezen meer bij [hoe tooadd of verwijderen van de rol van een gebruiker](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="a321d-119">If you would like tooadd or remove users from roles or change assignments from permanent tooeligible, read more at [how tooadd or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="a321d-120">Als u wilt toogive meer gebruikers toegang krijgen tot toomanage PIM, meer informatie op [hoe toogive toegang krijgen tot toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="a321d-120">If you would like toogive more users access toomanage PIM, read more at [how toogive access toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a321d-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a321d-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

