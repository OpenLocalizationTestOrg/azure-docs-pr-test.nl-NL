---
title: 'Azure AD Connect-synchronisatie: Directory uitbreidingen | Microsoft Docs'
description: Dit onderwerp beschrijft Hallo directory extensions functie in Azure AD Connect.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="f305b-103">Azure AD Connect-synchronisatie: Directory-uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="f305b-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="f305b-104">Directory-uitbreidingen kunt u tooextend Hallo schema in Azure AD met uw eigen kenmerken van lokale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f305b-104">Directory extensions allows you tooextend hello schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="f305b-105">Deze functie kunt u LOB-apps toobuild kenmerken u toomanage lokale blijven gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f305b-105">This feature allows you toobuild LOB apps consuming attributes you continue toomanage on-premises.</span></span> <span data-ttu-id="f305b-106">Deze kenmerken kunnen worden gebruikt via [directory-extensies voor Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) of [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="f305b-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="f305b-107">U kunt zien Hallo kenmerken beschikbaar via [explorer van Azure AD Graph](https://graphexplorer.cloudapp.net) en [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="f305b-107">You can see hello attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="f305b-108">Deze kenmerken worden op dit moment geen Office 365-werkbelasting verbruikt.</span><span class="sxs-lookup"><span data-stu-id="f305b-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="f305b-109">U welke bijkomende attributen configureren die u wilt dat toosynchronize in Hallo aangepaste instellingen pad in de installatiewizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="f305b-109">You configure which additional attributes you want toosynchronize in hello custom settings path in hello installation wizard.</span></span>
<span data-ttu-id="f305b-110">![Wizard voor schema-uitbreiding](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="f305b-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="f305b-111">Hallo installatie ziet Hallo kenmerken, die geldige kandidaten zijn te volgen:</span><span class="sxs-lookup"><span data-stu-id="f305b-111">hello installation shows hello following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="f305b-112">Gebruikers en groepen objecttypen</span><span class="sxs-lookup"><span data-stu-id="f305b-112">User and Group object types</span></span>
* <span data-ttu-id="f305b-113">Kenmerken met één waarde: String, Boolean, Integer, binair</span><span class="sxs-lookup"><span data-stu-id="f305b-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="f305b-114">Kenmerken met meerdere waarden: String, binair</span><span class="sxs-lookup"><span data-stu-id="f305b-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="f305b-115">Hallo-lijst met kenmerken worden gelezen uit de schemacache Hallo gemaakt tijdens de installatie van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f305b-115">hello list of attributes is read from hello schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="f305b-116">Als u Active Directory-schema met aanvullende kenmerken Hallo hebt uitgebreid, Hallo [schema moet worden vernieuwd](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) voordat deze nieuwe kenmerken zichtbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="f305b-116">If you have extended hello Active Directory schema with additional attributes, then hello [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="f305b-117">Een object in Azure AD kan too100 directory extensions kenmerken hebben.</span><span class="sxs-lookup"><span data-stu-id="f305b-117">An object in Azure AD can have up too100 directory extensions attributes.</span></span> <span data-ttu-id="f305b-118">Hallo maximale lengte is 250 tekens.</span><span class="sxs-lookup"><span data-stu-id="f305b-118">hello max length is 250 characters.</span></span> <span data-ttu-id="f305b-119">Als een kenmerkwaarde langer is, wordt deze afgekapt door Hallo synchronisatie-engine.</span><span class="sxs-lookup"><span data-stu-id="f305b-119">If an attribute value is longer, then it is truncated by hello sync engine.</span></span>

<span data-ttu-id="f305b-120">Tijdens de installatie van Azure AD Connect is een toepassing geregistreerd waar deze kenmerken beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="f305b-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="f305b-121">Hier ziet u deze toepassing in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f305b-121">You can see this application in hello Azure portal.</span></span>  
![Schema-uitbreiding App](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="f305b-123">Deze kenmerken zijn nu beschikbaar via de grafiek:</span><span class="sxs-lookup"><span data-stu-id="f305b-123">These attributes are now available through Graph:</span></span>  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="f305b-125">Hallo-kenmerken worden voorafgegaan door uitbreiding\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="f305b-125">hello attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="f305b-126">Hallo AppClientId heeft Hallo dezelfde voor alle kenmerken in uw Azure AD-tenant waarde.</span><span class="sxs-lookup"><span data-stu-id="f305b-126">hello AppClientId has hello same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f305b-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f305b-127">Next steps</span></span>
<span data-ttu-id="f305b-128">Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.</span><span class="sxs-lookup"><span data-stu-id="f305b-128">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="f305b-129">Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="f305b-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
