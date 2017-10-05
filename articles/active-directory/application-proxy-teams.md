---
title: Toegang tot apps van Azure AD-toepassingsproxy in Teams | Microsoft Docs
description: Azure AD-toepassingsproxy gebruiken voor toegang tot uw on-premises toepassing via Microsoft-Teams.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 24e22d7314de536714a825cd7035d2cec2112278
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="de735-103">Toegang tot uw on-premises toepassingen via Microsoft-Teams</span><span class="sxs-lookup"><span data-stu-id="de735-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="de735-104">Azure Active Directory-toepassingsproxy hebt u eenmalige aanmelding tot on-premises toepassingen ongeacht waar u zich bevindt en Microsoft-Teams stroomlijnt uw gezamenlijke inspanningen op één plek.</span><span class="sxs-lookup"><span data-stu-id="de735-104">Azure Active Directory Application Proxy gives you single sign-on to on-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="de735-105">De twee samen integreren betekent dat uw gebruikers productiever te maken met hun teamleden in een situatie.</span><span class="sxs-lookup"><span data-stu-id="de735-105">Integrating the two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="de735-106">Uw gebruikers cloud-apps kunnen toevoegen aan hun kanalen Teams [tabbladen](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), maar wat er gebeurt als SharePoint-site of ze allemaal gebruik van hulpprogramma lokale gehost?</span><span class="sxs-lookup"><span data-stu-id="de735-106">Your users can add cloud apps to their Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="de735-107">Toepassingsproxy is de oplossing.</span><span class="sxs-lookup"><span data-stu-id="de735-107">Application Proxy is the solution.</span></span> <span data-ttu-id="de735-108">Ze kunnen apps die zijn gepubliceerd via toepassingsproxy in hun kanalen met de dezelfde externe URL's die ze altijd gebruiken toegang tot hun apps op afstand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="de735-108">They can add apps published through Application Proxy to their channels using the same external URLs they always use to access their apps remotely.</span></span> <span data-ttu-id="de735-109">En omdat Application Proxy worden geverifieerd via Azure Active Directory, dezelfde single sign-on-ervaring via uitvoert.</span><span class="sxs-lookup"><span data-stu-id="de735-109">And because Application Proxy authenticates through Azure Active Directory, the same single sign-on experience carries through.</span></span>


## <a name="install-the-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="de735-110">De Application Proxy connector installeert en uw app publiceren</span><span class="sxs-lookup"><span data-stu-id="de735-110">Install the Application Proxy connector and publish your app</span></span>

<span data-ttu-id="de735-111">Als u dat nog niet gedaan hebt, [Application Proxy configureren voor uw tenant en de connector installeert](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="de735-111">If you haven't already, [configure Application Proxy for your tenant and install the connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="de735-112">Vervolgens [publiceren van uw on-premises toepassing](application-proxy-publish-azure-portal.md) voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="de735-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="de735-113">Wanneer u de app publiceren wilt: Noteer de externe URL omdat uw eindgebruikers die gegevens moeten wanneer ze de app aan Teams toevoegen.</span><span class="sxs-lookup"><span data-stu-id="de735-113">When you're publishing the app, make note of the external URL because your end users need that information when they add the app to Teams.</span></span>

<span data-ttu-id="de735-114">Als u al uw Apps die zijn gepubliceerd, maar niet meer de externe URL's weet, opzoeken ze de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de735-114">If you already have your apps published but don't remember their external URLs, look them up in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="de735-115">Meld u aan en navigeert u naar **Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen** > uw app selecteren >  **Toepassingsproxy**.</span><span class="sxs-lookup"><span data-stu-id="de735-115">Sign in, then navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-to-teams"></a><span data-ttu-id="de735-116">Uw app toevoegen aan Teams</span><span class="sxs-lookup"><span data-stu-id="de735-116">Add your app to Teams</span></span>

<span data-ttu-id="de735-117">Zodra u de app via toepassingsproxy publiceert, uw gebruikers laten weten dat ze deze als een tabblad rechtstreeks in hun kanalen Teams toevoegen kunnen.</span><span class="sxs-lookup"><span data-stu-id="de735-117">Once you publish the app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="de735-118">Hebben ze deze drie stappen:</span><span class="sxs-lookup"><span data-stu-id="de735-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="de735-119">Navigeer naar de Teams kanaal waar u deze app toevoegen en selecteer  **+**  een tabblad toevoegen.</span><span class="sxs-lookup"><span data-stu-id="de735-119">Navigate to the Teams channel where you want to add this app and select **+** to add a tab.</span></span>

   ![Selecteer een tabblad toevoegen](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="de735-121">Selecteer **Website** van het tabbladopties.</span><span class="sxs-lookup"><span data-stu-id="de735-121">Select **Website** from the tab options.</span></span>

   ![Een website toevoegen](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="de735-123">Geef een naam op het tabblad en de URL ingesteld op de externe URL Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="de735-123">Give the tab a name and set the URL to the Application Proxy external URL.</span></span> 

   ![Tabbladnaam en URL configureren](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="de735-125">Zodra de tabblad van een lid van een team wordt toegevoegd, wordt deze weergegeven voor iedereen in het kanaal.</span><span class="sxs-lookup"><span data-stu-id="de735-125">Once one member of a team adds the tab, it shows up for everyone in the channel.</span></span> <span data-ttu-id="de735-126">Alle gebruikers die toegang tot de app hebben worden geopend voor één aanmelding met de referenties die ze voor Microsoft-Teams gebruiken.</span><span class="sxs-lookup"><span data-stu-id="de735-126">Any users who have access to the app get single sign-on access with the credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="de735-127">Gebruikers die u geen toegang tot de app hebt wordt het tabblad in Teams weergegeven, maar worden geblokkeerd totdat u ze machtigingen voor de lokale-app en de Azure portal gepubliceerde versie van de app geven.</span><span class="sxs-lookup"><span data-stu-id="de735-127">Any users who don't have access to the app will see the tab in Teams, but are blocked until you give them permissions to the on-premises app and the Azure portal published version of the app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="de735-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de735-128">Next steps</span></span>

- <span data-ttu-id="de735-129">Meer informatie over hoe [lokale SharePoint-sites publiceren](application-proxy-enable-remote-access-sharepoint.md) met toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="de735-129">Learn how to [publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="de735-130">Configureren van uw apps te gebruiken [aangepaste domeinen](active-directory-application-proxy-custom-domains.md) voor de externe URL.</span><span class="sxs-lookup"><span data-stu-id="de735-130">Configure your apps to use [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
