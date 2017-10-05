---
title: Het configureren van gebruikers inrichten tot een galerie van Azure AD-toepassing | Microsoft Docs
description: Hoe kunt u snel uitgebreide gebruikersaccount inrichten en toepassingen die al wordt vermeld in de Azure AD-Toepassingsgalerie opheffen van inrichting configureren
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
ms.openlocfilehash: 2e38fcb30ea7632339a3ba8815a536872cfcc69e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-user-provisioning-to-an-azure-ad-gallery-application"></a><span data-ttu-id="f2e0c-103">Het configureren van gebruikers inrichten tot een toepassing die Azure AD-galerie</span><span class="sxs-lookup"><span data-stu-id="f2e0c-103">How to configure user provisioning to an Azure AD Gallery application</span></span>

<span data-ttu-id="f2e0c-104">*Het inrichten van het account* wordt het maken, bijwerken, en/of account gebruikersrecords in lokale opgeslagen gebruikersprofiel van de toepassing uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-104">*User account provisioning* is the act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="f2e0c-105">De meeste cloud en SaaS-toepassingen Sla de gebruikers, rollen en machtigingen in hun eigen lokale opgeslagen gebruikersprofiel en aanwezigheid van dergelijke een gebruikersrecord in hun lokale archief is *vereist* voor eenmalige aanmelding en toegang tot werkitems.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-105">Most cloud and SaaS applications store the users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access to work.</span></span>

<span data-ttu-id="f2e0c-106">In de Azure portal, de **inrichten** tabblad in het navigatiedeelvenster links voor een Enterprise-App wordt weergegeven welke inrichting modi voor die app worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-106">In the Azure portal, the **Provisioning** tab in the left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="f2e0c-107">Dit kan een van twee waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="f2e0c-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="f2e0c-108">Configureren van een toepassing voor handmatige inrichting</span><span class="sxs-lookup"><span data-stu-id="f2e0c-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="f2e0c-109">*Handmatige* inrichting betekent dat gebruikersaccounts handmatig met behulp van de methoden die door die app moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-109">*Manual* provisioning means that user accounts must be created manually using the methods provided by that app.</span></span> <span data-ttu-id="f2e0c-110">Dit kan betekenen aan te melden bij een portal beheerdersrechten voor die app en het toevoegen van gebruikers met behulp van een webgebaseerde gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="f2e0c-111">Of het een spreadsheet met account-details met een mechanisme dat is opgegeven door de toepassing kan uploaden.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="f2e0c-112">Raadpleeg de documentatie van de app of neem contact op met de ontwikkelaar van de app om te bepalen wat mechanismen zijn beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-112">Consult the documentation provided by the app, or contact the app developer to determine wat mechanisms are available.</span></span>

<span data-ttu-id="f2e0c-113">Als u handmatig is alleen de modus voor een bepaalde toepassing weergegeven, betekent dit dat er geen automatische Azure AD connector inrichting is gemaakt voor de app nog.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-113">If Manual is the only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for the app yet.</span></span> <span data-ttu-id="f2e0c-114">Of betekent dit dat de vereiste gebruiker management API waarop voor het bouwen van een geautomatiseerde inrichting connector biedt geen ondersteuning voor de app.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-114">Or it means the app does not support the pre-requisite user management API upon which to build an automated provisioning connector.</span></span>

<span data-ttu-id="f2e0c-115">Als u ondersteuning voor automatische inrichting voor een bepaalde app aanvragen wilt, kunt u een van de aanvraag op invullen <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-115">If you would like to request support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="f2e0c-116">Een toepassing configureren voor automatische inrichting</span><span class="sxs-lookup"><span data-stu-id="f2e0c-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="f2e0c-117">*Automatische* betekent dat een Azure AD connector inrichting is ontwikkeld voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="f2e0c-118">Zie voor meer informatie over de Azure AD-service en hoe het werkt inrichting [gebruikersaanvragen automatiseren en Deprovisioning voor SaaS-toepassingen met Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="f2e0c-118">For more information on the Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="f2e0c-119">Zie voor meer informatie over het inrichten van specifieke gebruikers en groepen naar een toepassing [het beheren van gebruikers account inrichten voor zakelijke apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="f2e0c-119">For more information on how to provision specific users and groups to an application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="f2e0c-120">Werkelijke instructies voor het inschakelen en configureren van automatische inrichting variëren afhankelijk van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-120">The actual steps required to enable and configure automatic provisioning vary depending on the application.</span></span>

>[!NOTE]
><span data-ttu-id="f2e0c-121">U moet beginnen met het vinden van de setup-zelfstudie specifiek zijn voor het instellen van de inrichting voor uw toepassing, en na deze stappen voor het configureren van de app en de Azure AD om het inrichtingsproces verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-121">You should start by finding the setup tutorial specific to setting up provisioning for your application, and following those steps to configure both the app and Azure AD to create the provisioning connection.</span></span> 
>
>

<span data-ttu-id="f2e0c-122">App-zelfstudies kunnen worden gevonden op [lijst zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="f2e0c-122">App tutorials can be found at [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="f2e0c-123">Een belangrijkste waarmee u rekening moet houden bij het instellen van de inrichting worden om te bekijken en configureren van de kenmerktoewijzingen en werkstromen die welke gebruiker (of groep) eigenschappen stroom van Azure AD voor de toepassing definiëren.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-123">An important thing to consider when setting up provisioning be to review and configure the attribute mappings and workflows that define which user (or group) properties flow from Azure AD to the application.</span></span> <span data-ttu-id="f2e0c-124">Dit omvat de 'overeenkomende eigenschap' instelt met worden gebruikt voor unieke identificatie dient en overeen met gebruikers/groepen tussen de twee systemen.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-124">This includes setting the “matching property” that be used to uniquely identify and match users/groups between the two systems.</span></span> <span data-ttu-id="f2e0c-125">Voor meer informatie over dit belangrijk proces.</span><span class="sxs-lookup"><span data-stu-id="f2e0c-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2e0c-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2e0c-126">Next steps</span></span>
[<span data-ttu-id="f2e0c-127">Gebruikers inrichten kenmerktoewijzingen voor SaaS-toepassingen in Azure Active Directory aanpassen</span><span class="sxs-lookup"><span data-stu-id="f2e0c-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

