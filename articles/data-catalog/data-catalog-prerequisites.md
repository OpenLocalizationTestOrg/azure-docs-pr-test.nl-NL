---
title: vereisten voor aaaAzure Data Catalog | Microsoft Docs
description: Meer informatie over Hallo vereisten moet u de slag met Azure Data Catalog tooget.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="363af-103">Vereisten voor Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="363af-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="363af-104">U moet tootake antwoord leest voordat u Azure Data Catalog kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="363af-104">You need tootake care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="363af-105">Maak je geen zorgen, dit proces is niet lang duren.</span><span class="sxs-lookup"><span data-stu-id="363af-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="363af-106">Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="363af-106">Azure subscription</span></span>
<span data-ttu-id="363af-107">tooset van Data Catalog, moet u de eigenaar van het Hallo of mede-eigenaar van een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="363af-107">tooset up Data Catalog, you must be hello owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="363af-108">Azure-abonnementen kunnen u toegang tot toocloud service bronnen zoals Data Catalog indelen.</span><span class="sxs-lookup"><span data-stu-id="363af-108">Azure subscriptions help you organize access toocloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="363af-109">Abonnementen kunnen u ook bepalen hoe Resourcegebruik is gerapporteerd, kosten in rekening gebracht en betaald.</span><span class="sxs-lookup"><span data-stu-id="363af-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="363af-110">Elk abonnement kan een afzonderlijke facturerings- en -instellingen hebben, zodat u kunt abonnementen en schema's die per afdeling, project en regionaal kantoor verschillen.</span><span class="sxs-lookup"><span data-stu-id="363af-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="363af-111">Elke cloudservice tooa abonnement behoort en moet u een abonnement toohave voordat u Data Catalog instellen.</span><span class="sxs-lookup"><span data-stu-id="363af-111">Every cloud service belongs tooa subscription, and you need toohave a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="363af-112">toolearn meer, Zie [beheren van accounts, abonnementen en beheerdersrollen](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="363af-112">toolearn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="363af-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="363af-113">Azure Active Directory</span></span>
<span data-ttu-id="363af-114">tooset van Data Catalog, als u bent aangemeld met een gebruikersaccount van Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="363af-114">tooset up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="363af-115">Azure AD biedt een eenvoudige manier voor uw zakelijke toomanage identiteits- en toegangsbeheer, zowel in Hallo cloud en on-premises.</span><span class="sxs-lookup"><span data-stu-id="363af-115">Azure AD provides an easy way for your business toomanage identity and access, both in hello cloud and on-premises.</span></span> <span data-ttu-id="363af-116">Gebruikers kunnen één werk- of schoolaccount gebruiken voor eenmalige aanmelding tooany cloud en lokale webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="363af-116">Users can use a single work or school account for single sign-in tooany cloud and on-premises web application.</span></span> <span data-ttu-id="363af-117">Data Catalog gebruikt Azure AD tooauthenticate aanmelden.</span><span class="sxs-lookup"><span data-stu-id="363af-117">Data Catalog uses Azure AD tooauthenticate sign-in.</span></span> <span data-ttu-id="363af-118">toolearn meer, Zie [wat is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="363af-118">toolearn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="363af-119">Met behulp van Hallo [Azure-portal](http://portal.azure.com/), kunt u zich aanmelden met een persoonlijk Microsoft-account of een Azure Active Directory werk- of schoolaccount.</span><span class="sxs-lookup"><span data-stu-id="363af-119">By using hello [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="363af-120">tooset van Data Catalog via ofwel hello Azure portal of Hallo [Data Catalog-portal](http://www.azuredatacatalog.com), moet u zich aanmelden met een Azure Active Directory-account, niet een persoonlijk account.</span><span class="sxs-lookup"><span data-stu-id="363af-120">tooset up Data Catalog by using either hello Azure portal or hello [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="363af-121">Configuratie van Active Directory-beleid</span><span class="sxs-lookup"><span data-stu-id="363af-121">Active Directory policy configuration</span></span>
<span data-ttu-id="363af-122">U kunt een situatie tegenkomen wanneer u zich kunt aanmelden toohello Data Catalog-portal, maar wanneer u probeert toosign in hulpprogramma voor registratie van gegevensbronnen toohello, u ontvangt een foutmelding dat u niet aanmelden.</span><span class="sxs-lookup"><span data-stu-id="363af-122">You might encounter a situation where you can sign in toohello Data Catalog portal, but when you attempt toosign in toohello data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="363af-123">Dit probleem kan gebeuren wanneer je op Hallo bedrijfsnetwerk of het optreden alleen wanneer u verbinding maakt vanaf externe Hallo-netwerk van bedrijf.</span><span class="sxs-lookup"><span data-stu-id="363af-123">This problem behavior might occur only when you're on hello company network, or it might occur only when you're connecting from outside hello company network.</span></span>

<span data-ttu-id="363af-124">hulpprogramma voor registratie van gegevensbronnen Hallo gebruikt formulierverificatie toovalidate uw gebruikersreferenties op basis van Active Directory.</span><span class="sxs-lookup"><span data-stu-id="363af-124">hello data source registration tool uses Forms Authentication toovalidate your user credentials against Active Directory.</span></span> <span data-ttu-id="363af-125">toohelp die het aanmelden is gelukt, een Active Directory-beheerder moet formulierverificatie inschakelen in algemeen verificatiebeleid Hallo.</span><span class="sxs-lookup"><span data-stu-id="363af-125">toohelp you sign in successfully, an Active Directory administrator must enable Forms Authentication in hello Global Authentication Policy.</span></span>

<span data-ttu-id="363af-126">In het globale verificatiebeleid Hallo mag verificatiemethoden ingeschakeld afzonderlijk voor intranet en extranet-verbindingen, zoals wordt weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="363af-126">In hello Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in hello following screenshot.</span></span> <span data-ttu-id="363af-127">Aanmelden fouten optreden als formulierverificatie niet is ingeschakeld voor het Hallo-netwerk van waaruit u verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="363af-127">Sign-in errors might occur if Forms Authentication is not enabled for hello network from which you're connecting.</span></span>

 ![Het globale verificatiebeleid Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="363af-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="363af-129">Next steps</span></span>
<span data-ttu-id="363af-130">Zie voor meer informatie [Authenticatiebeleid configureren](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="363af-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
