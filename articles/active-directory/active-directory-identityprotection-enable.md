---
title: Beveiliging voor Azure Active Directory-identiteit in te schakelen | Microsoft Docs
description: 'Informatie over het inschakelen van Azure Active Directory: Identity Protection.'
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f7a7ffaf-76bf-4cc7-96a1-86c944275c82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e0683e837086ca08f4b4b3f49695bdd2b4063ea4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="bdcc9-104">Inschakelen van beveiliging voor Azure Active Directory-identiteit</span><span class="sxs-lookup"><span data-stu-id="bdcc9-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="bdcc9-105">Azure Active Directory: Identity Protection is een nieuwe mogelijkheid biedt een geconsolideerde weergave verdachte activiteiten voor aanmelden en mogelijke beveiligingsproblemen en kunt u beschermen met meldingen, herstel aanbevelingen en beleid op basis van risico uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="bdcc9-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="bdcc9-106">De service detecteert verdachte activiteiten voor eindgebruikers en identiteiten bevoegdheden (admin) op basis van signalen zoals beveiligingsaanvallen, gelekte referenties, aanmeldingen vanaf onbekende locaties, geïnfecteerde apparaten als bescherming tegen deze activiteiten in realtime.</span><span class="sxs-lookup"><span data-stu-id="bdcc9-106">The service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, to protect against these activities in real-time.</span></span> <span data-ttu-id="bdcc9-107">Belangrijker is, op basis van deze verdachte activiteiten, de ernst van een gebruiker risico wordt berekend en beleid op basis van risico's kunnen worden geconfigureerd en automatisch de identiteiten van uw organisatie te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="bdcc9-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect the identities of your organization.</span></span> <span data-ttu-id="bdcc9-108">Zie voor meer informatie [Azure Active Directory: Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="bdcc9-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="bdcc9-109">In dit onderwerp wordt beschreven hoe Azure Active Directory identiteitsbeveiliging in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="bdcc9-109">This topics shows how to enable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-to-enable-azure-active-directory-identity-protection"></a><span data-ttu-id="bdcc9-110">Stappen voor het inschakelen van Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bdcc9-110">Steps to enable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="bdcc9-111">[Eenmalige aanmelding](https://ms.portal.azure.com/) naar uw Azure-portal als globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="bdcc9-111">[Sign-on](https://ms.portal.azure.com/) to your Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="bdcc9-112">Klik in de Azure-portal op **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="bdcc9-112">In the Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="bdcc9-113">![Maak](./media/active-directory-identityprotection-enable/01.png "maken")</span><span class="sxs-lookup"><span data-stu-id="bdcc9-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="bdcc9-114">Klik in de lijst met toepassingen op **beveiliging en identiteit**.</span><span class="sxs-lookup"><span data-stu-id="bdcc9-114">In the applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="bdcc9-115">![Maak](./media/active-directory-identityprotection-enable/02.png "maken")</span><span class="sxs-lookup"><span data-stu-id="bdcc9-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="bdcc9-116">Klik op **Azure AD Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="bdcc9-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="bdcc9-117">![Maak](./media/active-directory-identityprotection-enable/03.png "maken")</span><span class="sxs-lookup"><span data-stu-id="bdcc9-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="bdcc9-118">Op de **Azure AD Identity Protection** blade, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="bdcc9-118">On the **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="bdcc9-119">![Maak](./media/active-directory-identityprotection-enable/04.png "maken")</span><span class="sxs-lookup"><span data-stu-id="bdcc9-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdcc9-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bdcc9-120">Next Steps</span></span>
* [<span data-ttu-id="bdcc9-121">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bdcc9-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

