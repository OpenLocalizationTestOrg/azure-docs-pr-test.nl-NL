---
title: 'Azure AD Connect-synchronisatie: Directory uitbreidingen | Microsoft Docs'
description: In dit onderwerp beschrijft de functie van de extensies directory in Azure AD Connect.
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
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="9c0be-103">Azure AD Connect-synchronisatie: Directory-uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="9c0be-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="9c0be-104">Directory-uitbreidingen kunt u het schema uitbreiden in Azure AD met uw eigen kenmerken van lokale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c0be-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="9c0be-105">Deze functie kunt u kenmerken die u kunt doorgaan met het beheren van lokale verbruikt LOB-apps bouwen.</span><span class="sxs-lookup"><span data-stu-id="9c0be-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span></span> <span data-ttu-id="9c0be-106">Deze kenmerken kunnen worden gebruikt via [directory-extensies voor Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) of [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="9c0be-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="9c0be-107">U kunt zien kenmerken beschikbaar via [explorer van Azure AD Graph](https://graphexplorer.cloudapp.net) en [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="9c0be-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="9c0be-108">Deze kenmerken worden op dit moment geen Office 365-werkbelasting verbruikt.</span><span class="sxs-lookup"><span data-stu-id="9c0be-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="9c0be-109">U configureren welke extra kenmerken die u wilt synchroniseren in het pad van de aangepaste instellingen in de installatiewizard.</span><span class="sxs-lookup"><span data-stu-id="9c0be-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span></span>
<span data-ttu-id="9c0be-110">![Wizard voor schema-uitbreiding](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="9c0be-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="9c0be-111">De installatie ziet u de volgende kenmerken, die kandidaten zijn geldig:</span><span class="sxs-lookup"><span data-stu-id="9c0be-111">The installation shows the following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="9c0be-112">Gebruikers en groepen objecttypen</span><span class="sxs-lookup"><span data-stu-id="9c0be-112">User and Group object types</span></span>
* <span data-ttu-id="9c0be-113">Kenmerken met één waarde: String, Boolean, Integer, binair</span><span class="sxs-lookup"><span data-stu-id="9c0be-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="9c0be-114">Kenmerken met meerdere waarden: String, binair</span><span class="sxs-lookup"><span data-stu-id="9c0be-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="9c0be-115">De lijst met kenmerken is gelezen uit de schemacache gemaakt tijdens de installatie van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9c0be-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="9c0be-116">Als u extra kenmerken Active Directory-schema hebt uitgebreid en vervolgens de [schema moet worden vernieuwd](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) voordat deze nieuwe kenmerken zichtbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="9c0be-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="9c0be-117">Een object in Azure AD kan maximaal 100 kenmerken voor Active directory-extensies hebben.</span><span class="sxs-lookup"><span data-stu-id="9c0be-117">An object in Azure AD can have up to 100 directory extensions attributes.</span></span> <span data-ttu-id="9c0be-118">De maximale lengte is 250 tekens.</span><span class="sxs-lookup"><span data-stu-id="9c0be-118">The max length is 250 characters.</span></span> <span data-ttu-id="9c0be-119">Als een kenmerkwaarde langer is, wordt deze afgekapt door de synchronisatie-engine.</span><span class="sxs-lookup"><span data-stu-id="9c0be-119">If an attribute value is longer, then it is truncated by the sync engine.</span></span>

<span data-ttu-id="9c0be-120">Tijdens de installatie van Azure AD Connect is een toepassing geregistreerd waar deze kenmerken beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="9c0be-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="9c0be-121">Hier ziet u deze toepassing in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9c0be-121">You can see this application in the Azure portal.</span></span>  
![Schema-uitbreiding App](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="9c0be-123">Deze kenmerken zijn nu beschikbaar via de grafiek:</span><span class="sxs-lookup"><span data-stu-id="9c0be-123">These attributes are now available through Graph:</span></span>  
![Graph](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="9c0be-125">De kenmerken worden voorafgegaan door uitbreiding\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="9c0be-125">The attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="9c0be-126">De AppClientId heeft dezelfde waarde voor alle kenmerken in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="9c0be-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c0be-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9c0be-127">Next steps</span></span>
<span data-ttu-id="9c0be-128">Meer informatie over de [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.</span><span class="sxs-lookup"><span data-stu-id="9c0be-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="9c0be-129">Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9c0be-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
