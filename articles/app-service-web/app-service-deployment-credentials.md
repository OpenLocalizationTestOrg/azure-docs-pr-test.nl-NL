---
title: aaaAzure referenties voor de implementatie van App Service | Microsoft Docs
description: Meer informatie over hoe toouse Hallo referenties voor Azure App Service-implementatie.
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
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="c5353-103">Referenties voor implementatie configureren voor Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c5353-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="c5353-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ondersteunt twee soorten referenties voor [lokale Git-implementatie](app-service-deploy-local-git.md) en [FTP-/ S implementatie](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="c5353-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="c5353-105">Deze zijn niet hetzelfde als uw Azure Active Directory-referenties Hallo.</span><span class="sxs-lookup"><span data-stu-id="c5353-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="c5353-106">**Beveiliging op gebruikersniveau referenties**: één set met referenties voor Hallo volledige Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c5353-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="c5353-107">Gebruikte toodeploy tooApp Service kan zijn voor elke app in een abonnement dat Azure-account Hallo machtiging tooaccess heeft.</span><span class="sxs-lookup"><span data-stu-id="c5353-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="c5353-108">Dit zijn Hallo referenties standaardset die u configureert in **App Services** > **&lt;app_naam >** > **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="c5353-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="c5353-109">Dit is ook Hallo standaardset die wordt opgehaald in Hallo portal GUI (zoals Hallo **overzicht** en **eigenschappen** van uw app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="c5353-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="c5353-110">Wanneer u toegang tot tooAzure bronnen via op rollen gebaseerd toegangsbeheer (RBAC) of co-beheerder machtigingen delegeren, kunt elke Azure-gebruiker die toegang tooan app ontvangt stelt zijn/haar persoonlijke op gebruikersniveau referenties gebruiken totdat de toegang is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="c5353-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="c5353-111">Deze referenties voor implementatie mag niet worden gedeeld met andere Azure-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c5353-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="c5353-112">**App-niveau referenties**: één set met referenties voor elke app.</span><span class="sxs-lookup"><span data-stu-id="c5353-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="c5353-113">Het kan gebruikte toodeploy toothat app alleen zijn.</span><span class="sxs-lookup"><span data-stu-id="c5353-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="c5353-114">Hallo-referenties publiceren voor elke app bij het maken van de app automatisch wordt gegenereerd en is gevonden in het Hallo-app profiel.</span><span class="sxs-lookup"><span data-stu-id="c5353-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="c5353-115">U kunt geen Hallo referenties handmatig configureren, maar u ze op elk gewenst moment voor een app kunt herstellen.</span><span class="sxs-lookup"><span data-stu-id="c5353-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c5353-116">In de volgorde toogive iemand toegangsreferenties toothese via rollen gebaseerd toegangsbeheer (RBAC), moet u toomake ze Inzender of hoger op Hallo Web-App.</span><span class="sxs-lookup"><span data-stu-id="c5353-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="c5353-117">Lezers zijn niet toegestaan voor toopublish en daarom geen toegang tot deze referenties.</span><span class="sxs-lookup"><span data-stu-id="c5353-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="c5353-118"><a name="userscope"></a>Instellen en de referenties op gebruikersniveau resetten</span><span class="sxs-lookup"><span data-stu-id="c5353-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="c5353-119">U kunt uw referenties op gebruikersniveau configureren in elke app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="c5353-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="c5353-120">Ongeacht in welke app configureert u deze referenties, maar apps tooall geldt voor alle abonnementen in uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c5353-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="c5353-121">tooconfigure uw referenties op gebruikersniveau:</span><span class="sxs-lookup"><span data-stu-id="c5353-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="c5353-122">In Hallo [Azure-portal](https://portal.azure.com), klik op App Service >  **&lt;any_app >** > **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="c5353-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c5353-123">U moet ten minste één app in Hallo-portal hebben voordat u toegang hebt tot blade Hallo implementatie-referenties.</span><span class="sxs-lookup"><span data-stu-id="c5353-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="c5353-124">Bij Hallo [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), kunt u de referenties op gebruikersniveau zonder een bestaande app configureren.</span><span class="sxs-lookup"><span data-stu-id="c5353-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="c5353-125">Configureer Hallo-gebruikersnaam en wachtwoord en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c5353-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="c5353-126">Als u de referenties voor uw implementatie hebt ingesteld, kunt u vinden Hallo *Git* gebruikersnaam van de implementatie in uw app **overzicht**,</span><span class="sxs-lookup"><span data-stu-id="c5353-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="c5353-127">en en *FTP* gebruikersnaam van de implementatie in uw app **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="c5353-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="c5353-128">Uw wachtwoord op gebruikersniveau implementatie wordt niet door Azure worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c5353-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="c5353-129">Als u Hallo wachtwoord vergeet, kunt u het niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="c5353-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="c5353-130">U kunt echter uw referenties herstellen door Hallo stappen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="c5353-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="c5353-131"><a name="appscope"></a>Ophalen en app-niveau referenties opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="c5353-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="c5353-132">Voor elke app in App Service, de referenties van de app-niveau worden opgeslagen in Hallo publicatieprofiel XML.</span><span class="sxs-lookup"><span data-stu-id="c5353-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="c5353-133">tooget hello app-niveau referenties:</span><span class="sxs-lookup"><span data-stu-id="c5353-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="c5353-134">In Hallo [Azure-portal](https://portal.azure.com), klik op App Service >  **&lt;any_app >** > **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="c5353-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="c5353-135">Klik op **... Meer** > **Get publicatieprofiel**, en begint met het downloaden voor een. Bestand met publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="c5353-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="c5353-136">Open hello. Bestands- en Hallo zoeken met publicatie-instellingen `<publishProfile>` code met het kenmerk Hallo `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="c5353-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="c5353-137">Haal vervolgens, de `userName` en `password` kenmerken.</span><span class="sxs-lookup"><span data-stu-id="c5353-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="c5353-138">Dit zijn Hallo app-niveau referenties.</span><span class="sxs-lookup"><span data-stu-id="c5353-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="c5353-139">Vergelijkbare toohello op gebruikersniveau referenties, Hallo FTP implementatie gebruikersnaam is in de indeling van Hallo `<app_name>\<username>`, en Hallo Git-implementatie gebruikersnaam NET `<username>` zonder Hallo voorgaande `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="c5353-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="c5353-140">tooreset hello app-niveau referenties:</span><span class="sxs-lookup"><span data-stu-id="c5353-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="c5353-141">In Hallo [Azure-portal](https://portal.azure.com), klik op App Service >  **&lt;any_app >** > **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="c5353-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="c5353-142">Klik op **... Meer** > **Reset publicatieprofiel**.</span><span class="sxs-lookup"><span data-stu-id="c5353-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="c5353-143">Klik op **Ja** tooconfirm Hallo opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="c5353-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="c5353-144">Hallo reset-actie wordt een eerder gedownloade ongeldig. Bestanden met publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="c5353-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5353-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c5353-145">Next steps</span></span>

<span data-ttu-id="c5353-146">Ontdek hoe u kunt toouse deze referenties toodeploy uw app uit [lokale Git](app-service-deploy-local-git.md) of met behulp van [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="c5353-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
