---
title: aaaHow tooconfigure gebruikers inrichten tooan Azure AD-galerie toepassing | Microsoft Docs
description: Hoe kunt u snel uitgebreide gebruikersaccount inrichten en tooapplications al wordt vermeld in de galerie van Azure AD-toepassing hello opheffen van inrichting configureren
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
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a><span data-ttu-id="b5fb8-103">Hoe tooconfigure gebruiker tooan Azure AD-galerie toepassing inrichten</span><span class="sxs-lookup"><span data-stu-id="b5fb8-103">How tooconfigure user provisioning tooan Azure AD Gallery application</span></span>

<span data-ttu-id="b5fb8-104">*Het inrichten van het account* wordt Hallo van maken, bijwerken en/of account gebruikersrecords in lokale opgeslagen gebruikersprofiel van de toepassing uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-104">*User account provisioning* is hello act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="b5fb8-105">De meeste cloud en SaaS-toepassingen opslaan Hallo gebruikers rollen en machtigingen die in hun eigen lokale opgeslagen gebruikersprofiel en aanwezigheid van dergelijke een gebruikersrecord in hun lokale archief is *vereist* voor eenmalige aanmelding en toegang toowork.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-105">Most cloud and SaaS applications store hello users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access toowork.</span></span>

<span data-ttu-id="b5fb8-106">Hallo in hello Azure-portal, **inrichten** tabblad in het linkernavigatievenster Hallo voor een Enterprise-App wordt weergegeven welke inrichting modi voor die app worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-106">In hello Azure portal, hello **Provisioning** tab in hello left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="b5fb8-107">Dit kan een van twee waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="b5fb8-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="b5fb8-108">Configureren van een toepassing voor handmatige inrichting</span><span class="sxs-lookup"><span data-stu-id="b5fb8-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="b5fb8-109">*Handmatige* inrichting betekent dat gebruikersaccounts handmatig met Hallo methoden van de app moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-109">*Manual* provisioning means that user accounts must be created manually using hello methods provided by that app.</span></span> <span data-ttu-id="b5fb8-110">Dit kan betekenen aan te melden bij een portal beheerdersrechten voor die app en het toevoegen van gebruikers met behulp van een webgebaseerde gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="b5fb8-111">Of het een spreadsheet met account-details met een mechanisme dat is opgegeven door de toepassing kan uploaden.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="b5fb8-112">Raadpleeg de documentatie van Hallo opgegeven door het Hallo-app of neem contact op met Hallo app developer toodetermine wat mechanismen beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-112">Consult hello documentation provided by hello app, or contact hello app developer toodetermine wat mechanisms are available.</span></span>

<span data-ttu-id="b5fb8-113">Handmatige Hallo alleen de modus weergegeven voor een bepaalde toepassing, betekent dit dat er geen automatische Azure AD connector inrichting is gemaakt voor Hallo app nog.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-113">If Manual is hello only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for hello app yet.</span></span> <span data-ttu-id="b5fb8-114">Of het Hallo-app biedt geen ondersteuning voor Hallo vereiste gebruiker management-API bij welke toobuild een geautomatiseerde inrichting connector betekent.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-114">Or it means hello app does not support hello pre-requisite user management API upon which toobuild an automated provisioning connector.</span></span>

<span data-ttu-id="b5fb8-115">Als u ondersteuning voor automatische inrichting voor een bepaalde app toorequest wilt, kunt u een van de aanvraag op invullen <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-115">If you would like toorequest support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="b5fb8-116">Een toepassing configureren voor automatische inrichting</span><span class="sxs-lookup"><span data-stu-id="b5fb8-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="b5fb8-117">*Automatische* betekent dat een Azure AD connector inrichting is ontwikkeld voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="b5fb8-118">Zie voor meer informatie over het Hallo Azure AD-service en hoe het werkt, inrichting [gebruikersaanvragen automatiseren en Deprovisioning tooSaaS toepassingen met Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="b5fb8-118">For more information on hello Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="b5fb8-119">Voor meer informatie over hoe tooprovision specifieke gebruikers en groepen tooan toepassing, Zie [het beheren van gebruikers account inrichten voor zakelijke apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="b5fb8-119">For more information on how tooprovision specific users and groups tooan application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="b5fb8-120">werkelijke stappen vereist tooenable Hallo en configureren van automatische inrichting variëren afhankelijk van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-120">hello actual steps required tooenable and configure automatic provisioning vary depending on hello application.</span></span>

>[!NOTE]
><span data-ttu-id="b5fb8-121">U moet eerst setup zelfstudie specifieke toosetting up inrichting voor uw toepassing hello en na deze stappen tooconfigure zowel Hallo-app en Azure AD toocreate Hallo inrichting verbinding vinden.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-121">You should start by finding hello setup tutorial specific toosetting up provisioning for your application, and following those steps tooconfigure both hello app and Azure AD toocreate hello provisioning connection.</span></span> 
>
>

<span data-ttu-id="b5fb8-122">App-zelfstudies kunnen worden gevonden op [lijst zelfstudies over het SaaS-Apps met Azure Active Directory tooIntegrate](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="b5fb8-122">App tutorials can be found at [List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="b5fb8-123">Een tooconsider wat belangrijk is bij het instellen van de inrichting tooreview Hallo kenmerktoewijzingen en werkstromen die welke gebruiker (of groep) eigenschappen stroom van Azure AD-toepassing voor toohello definiëren en configureren.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-123">An important thing tooconsider when setting up provisioning be tooreview and configure hello attribute mappings and workflows that define which user (or group) properties flow from Azure AD toohello application.</span></span> <span data-ttu-id="b5fb8-124">Dit omvat Hallo 'overeenkomende eigenschap' instelt met gebruikte toouniquely worden geïdentificeerd en overeen met gebruikers/groepen tussen Hallo twee systemen.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-124">This includes setting hello “matching property” that be used toouniquely identify and match users/groups between hello two systems.</span></span> <span data-ttu-id="b5fb8-125">Voor meer informatie over dit belangrijk proces.</span><span class="sxs-lookup"><span data-stu-id="b5fb8-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5fb8-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b5fb8-126">Next steps</span></span>
[<span data-ttu-id="b5fb8-127">Gebruikers inrichten kenmerktoewijzingen voor SaaS-toepassingen in Azure Active Directory aanpassen</span><span class="sxs-lookup"><span data-stu-id="b5fb8-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

