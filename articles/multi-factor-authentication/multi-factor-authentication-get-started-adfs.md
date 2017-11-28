---
title: Verificatie in twee stappen en AD FS - Azure MFA | Microsoft Docs
description: Dit is de Azure Multi-Factor Authentication-pagina waarop wordt beschreven hoe u met Azure MFA en AD FS aan de slag kunt gaan.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 28aede545c738137ff04257214e4a3f42792d85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="774cc-103">Aan de slag met Azure Multi-Factor Authentication en Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="774cc-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="774cc-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="774cc-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="774cc-105">Als uw organisatie met behulp van AD FS uw on-premises Active Directory heeft gefedereerd met Azure Active Directory, zijn er twee opties voor het gebruik van Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="774cc-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="774cc-106">Cloudresources beveiligen met Azure Multi-Factor Authentication of Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="774cc-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="774cc-107">Cloudresources en on-premises resources beveiligen met behulp van de Azure Multi-Factor Authentication-server</span><span class="sxs-lookup"><span data-stu-id="774cc-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="774cc-108">De volgende tabel bevat een overzicht van de verschillen tussen de verificatie-ervaring bij het beveiligen van resources met Azure Multi-Factor Authentication en AD FS</span><span class="sxs-lookup"><span data-stu-id="774cc-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="774cc-109">Verificatie-ervaring - op browser gebaseerde apps</span><span class="sxs-lookup"><span data-stu-id="774cc-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="774cc-110">Verificatie-ervaring - niet op browser gebaseerde apps</span><span class="sxs-lookup"><span data-stu-id="774cc-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="774cc-111">Beveiligen van Azure AD-resources met Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="774cc-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="774cc-112">De eerste verificatiestap wordt uitgevoerd on-premises met AD FS.</span><span class="sxs-lookup"><span data-stu-id="774cc-112">The first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="774cc-113">De tweede stap is een telefonische methode die met behulp van cloudverificatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="774cc-113">The second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="774cc-114">Azure AD-resources beveiligen met behulp van Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="774cc-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="774cc-115">De eerste verificatiestap wordt uitgevoerd on-premises met AD FS.</span><span class="sxs-lookup"><span data-stu-id="774cc-115">The first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="774cc-116">De tweede stap wordt on-premises uitgevoerd door de claim toe te kennen.</span><span class="sxs-lookup"><span data-stu-id="774cc-116">The second step is performed on-premises by honoring the claim.</span></span></li> |

<span data-ttu-id="774cc-117">Valkuilen met app-wachtwoorden voor federatieve gebruikers:</span><span class="sxs-lookup"><span data-stu-id="774cc-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="774cc-118">App-wachtwoorden worden gecontroleerd met cloudverificatie en daarom worden federaties omzeild.</span><span class="sxs-lookup"><span data-stu-id="774cc-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="774cc-119">Federatie wordt alleen actief gebruikt bij het instellen van het app-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="774cc-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="774cc-120">On-premises instellingen voor toegangsbeheer van client worden niet herkend door app-wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="774cc-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="774cc-121">U raakt on-premises mogelijkheden voor logboekregistratie bij verificatie voor app-wachtwoorden kwijt.</span><span class="sxs-lookup"><span data-stu-id="774cc-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="774cc-122">Account uitschakelen/verwijderen kan met Directory-synchronisatie tot drie uur duren, waardoor uitschakelen/verwijderen van app-wachtwoorden in de cloudidentiteit wordt vertraagd.</span><span class="sxs-lookup"><span data-stu-id="774cc-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="774cc-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="774cc-123">Next steps</span></span>
<span data-ttu-id="774cc-124">Zie voor meer informatie over het instellen van Azure Multi-Factor Authentication of van de Azure Multi-Factor Authentication-server met AD FS de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="774cc-124">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS, see the following articles:</span></span>

* [<span data-ttu-id="774cc-125">Cloudresources beveiligen met behulp van Azure Multi-Factor Authentication en AD FS</span><span class="sxs-lookup"><span data-stu-id="774cc-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="774cc-126">Cloudresources en on-premises resources beveiligen met behulp van de Azure Multi-Factor Authentication-server met Windows Server 2012 R2 AD FS</span><span class="sxs-lookup"><span data-stu-id="774cc-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="774cc-127">Cloudresources en on-premises resources beveiligen met behulp van de Azure Multi-Factor Authentication-server met AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="774cc-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
