---
title: Azure App Service-implementatie referenties | Microsoft Docs
description: Informatie over het gebruik van de referenties voor de Azure App Service-implementatie.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 86a2cd8ae9f97c606a378452e44eec8941700531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="18f93-103">Referenties voor implementatie configureren voor Azure App Service</span><span class="sxs-lookup"><span data-stu-id="18f93-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="18f93-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ondersteunt twee soorten referenties voor [lokale Git-implementatie](app-service-deploy-local-git.md) en [FTP-/ S implementatie](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="18f93-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="18f93-105">Deze zijn niet hetzelfde zijn als uw Azure Active Directory-referenties.</span><span class="sxs-lookup"><span data-stu-id="18f93-105">These are not the same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="18f93-106">**Beveiliging op gebruikersniveau referenties**: één set met referenties voor de volledige Azure-account.</span><span class="sxs-lookup"><span data-stu-id="18f93-106">**User-level credentials**: one set of credentials for the entire Azure account.</span></span> <span data-ttu-id="18f93-107">Het kan worden gebruikt om te implementeren in App Service voor een app, in een abonnement dat het Azure-account toegang heeft tot.</span><span class="sxs-lookup"><span data-stu-id="18f93-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span></span> <span data-ttu-id="18f93-108">Dit zijn de standaardset van de referenties die u configureert in **App Services** > **&lt;app_naam >** > **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="18f93-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="18f93-109">Dit is de standaardinstelling set die wordt opgehaald in de GUI-portal (zoals de **overzicht** en **eigenschappen** van uw app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="18f93-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="18f93-110">Wanneer u toegang tot Azure-resources via op rollen gebaseerd toegangsbeheer (RBAC) of co-beheerder machtigingen delegeren, kunt elke Azure-gebruiker die toegang tot een app ontvangt stelt zijn/haar persoonlijke op gebruikersniveau referenties gebruiken totdat de toegang is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="18f93-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="18f93-111">Deze referenties voor implementatie mag niet worden gedeeld met andere Azure-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="18f93-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="18f93-112">**App-niveau referenties**: één set met referenties voor elke app.</span><span class="sxs-lookup"><span data-stu-id="18f93-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="18f93-113">Het kan worden gebruikt om deze app alleen te implementeren.</span><span class="sxs-lookup"><span data-stu-id="18f93-113">It can be used to deploy to that app only.</span></span> <span data-ttu-id="18f93-114">De referenties publicatieprofiel voor elke app bij het maken van de app automatisch wordt gegenereerd en is gevonden in de app.</span><span class="sxs-lookup"><span data-stu-id="18f93-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span></span> <span data-ttu-id="18f93-115">U kunt handmatig de referenties niet configureren, maar u kunt ze op elk gewenst moment voor een app herstellen.</span><span class="sxs-lookup"><span data-stu-id="18f93-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="18f93-116">Om aan te geven die iemand toegang tot deze referenties via rollen gebaseerd toegangsbeheer (RBAC), moet u ze Inzender of hoger op de Web-App.</span><span class="sxs-lookup"><span data-stu-id="18f93-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span></span> <span data-ttu-id="18f93-117">Lezers zijn niet toegestaan voor het publiceren van, en daarom geen toegang tot deze referenties.</span><span class="sxs-lookup"><span data-stu-id="18f93-117">Readers are not allowed to publish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="18f93-118"><a name="userscope"></a>Instellen en de referenties op gebruikersniveau resetten</span><span class="sxs-lookup"><span data-stu-id="18f93-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="18f93-119">U kunt uw referenties op gebruikersniveau configureren in elke app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="18f93-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="18f93-120">Ongeacht in welke app configureert u deze referenties, geldt dit voor alle apps en voor alle abonnementen in uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="18f93-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="18f93-121">Uw referenties op gebruikersniveau configureren:</span><span class="sxs-lookup"><span data-stu-id="18f93-121">To configure your user-level credentials:</span></span>

1. <span data-ttu-id="18f93-122">In de [Azure-portal](https://portal.azure.com), klik op App Service >  **&lt;any_app >** > **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="18f93-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="18f93-123">U moet ten minste één app in de portal hebben voordat u toegang hebt tot de implementatie van de blade referenties.</span><span class="sxs-lookup"><span data-stu-id="18f93-123">In the portal, you must have at least one app before you can access the deployment credentials blade.</span></span> <span data-ttu-id="18f93-124">Bij de [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), kunt u de referenties op gebruikersniveau zonder een bestaande app configureren.</span><span class="sxs-lookup"><span data-stu-id="18f93-124">However, with the [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="18f93-125">Configureer de gebruikersnaam en wachtwoord en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="18f93-125">Configure the user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="18f93-126">Als u de referenties voor uw implementatie hebt ingesteld, kunt u vinden de *Git* gebruikersnaam van de implementatie in uw app **overzicht**,</span><span class="sxs-lookup"><span data-stu-id="18f93-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="18f93-127">en en *FTP* gebruikersnaam van de implementatie in uw app **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="18f93-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="18f93-128">Uw wachtwoord op gebruikersniveau implementatie wordt niet door Azure worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="18f93-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="18f93-129">Als u het wachtwoord vergeet, kunt u het niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="18f93-129">If you forget the password, you can't retrieve it.</span></span> <span data-ttu-id="18f93-130">U kunt echter uw referenties herstellen door de stappen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="18f93-130">However, you can reset your credentials by following the steps in this section.</span></span>
>
>  

## <span data-ttu-id="18f93-131"><a name="appscope"></a>Ophalen en app-niveau referenties opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="18f93-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="18f93-132">Voor elke app in App Service, de referenties van de app-niveau worden opgeslagen in het XML-profiel publiceren.</span><span class="sxs-lookup"><span data-stu-id="18f93-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span></span>

<span data-ttu-id="18f93-133">De referenties van de app-niveau ophalen:</span><span class="sxs-lookup"><span data-stu-id="18f93-133">To get the app-level credentials:</span></span>

1. <span data-ttu-id="18f93-134">In de [Azure-portal](https://portal.azure.com), klik op App Service >  **&lt;any_app >** > **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="18f93-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="18f93-135">Klik op **... Meer** > **Get publicatieprofiel**, en begint met het downloaden voor een. Bestand met publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="18f93-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="18f93-136">Open de. Met publicatie-instellingen bestand en zoek de `<publishProfile>` tag met het kenmerk `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="18f93-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="18f93-137">Haal vervolgens, de `userName` en `password` kenmerken.</span><span class="sxs-lookup"><span data-stu-id="18f93-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="18f93-138">Dit zijn de referenties van de app-niveau.</span><span class="sxs-lookup"><span data-stu-id="18f93-138">These are the app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="18f93-139">Vergelijkbaar met de referenties op gebruikersniveau, de gebruikersnaam van FTP-implementatie is in de indeling van `<app_name>\<username>`, en de gebruikersnaam Git-implementatie is zojuist `<username>` zonder de voorafgaande `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="18f93-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span></span>

<span data-ttu-id="18f93-140">Om in te stellen de referenties van de app-niveau:</span><span class="sxs-lookup"><span data-stu-id="18f93-140">To reset the app-level credentials:</span></span>

1. <span data-ttu-id="18f93-141">In de [Azure-portal](https://portal.azure.com), klik op App Service >  **&lt;any_app >** > **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="18f93-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="18f93-142">Klik op **... Meer** > **Reset publicatieprofiel**.</span><span class="sxs-lookup"><span data-stu-id="18f93-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="18f93-143">Klik op **Ja** om te bevestigen dat het opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="18f93-143">Click **Yes** to confirm the reset.</span></span>

    <span data-ttu-id="18f93-144">Reset-actie wordt een eerder gedownloade ongeldig. Bestanden met publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="18f93-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18f93-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18f93-145">Next steps</span></span>

<span data-ttu-id="18f93-146">Ontdek hoe u kunt deze referenties gebruiken voor het implementeren van uw app uit [lokale Git](app-service-deploy-local-git.md) of met behulp van [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="18f93-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
