---
title: Toepassingsproxy van Azure AD-apps in Teams aaaAccess | Microsoft Docs
description: Azure AD-toepassingsproxy tooaccess uw on-premises toepassing via Microsoft-Teams gebruiken.
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
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="6b8fa-103">Toegang tot uw on-premises toepassingen via Microsoft-Teams</span><span class="sxs-lookup"><span data-stu-id="6b8fa-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="6b8fa-104">Azure Active Directory-toepassingsproxy hebt u één aanmelding tooon-premises toepassingen ongeacht waar u zich bevindt en Microsoft-Teams stroomlijnt uw gezamenlijke inspanningen op één plek.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-104">Azure Active Directory Application Proxy gives you single sign-on tooon-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="6b8fa-105">Hallo integreren betekent twee samen dat uw gebruikers productiever te maken met hun teamleden in een situatie.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-105">Integrating hello two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="6b8fa-106">Uw gebruikers kunnen toevoegen cloud-apps tootheir Teams kanalen [tabbladen](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), maar wat er gebeurt als SharePoint-site of ze allemaal gebruik van hulpprogramma lokale gehost?</span><span class="sxs-lookup"><span data-stu-id="6b8fa-106">Your users can add cloud apps tootheir Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="6b8fa-107">Toepassingsproxy is Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-107">Application Proxy is hello solution.</span></span> <span data-ttu-id="6b8fa-108">Ze kunnen apps toevoegen gepubliceerd via toepassingsproxy tootheir Hallo kanalen met dezelfde externe URL's die ze altijd tooaccess hun apps op afstand gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-108">They can add apps published through Application Proxy tootheir channels using hello same external URLs they always use tooaccess their apps remotely.</span></span> <span data-ttu-id="6b8fa-109">En omdat Application Proxy worden geverifieerd via Azure Active Directory, Hallo dezelfde single sign-on-ervaring via uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-109">And because Application Proxy authenticates through Azure Active Directory, hello same single sign-on experience carries through.</span></span>


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="6b8fa-110">Hallo Application Proxy connector installeert en uw app publiceren</span><span class="sxs-lookup"><span data-stu-id="6b8fa-110">Install hello Application Proxy connector and publish your app</span></span>

<span data-ttu-id="6b8fa-111">Als u dat nog niet gedaan hebt, [Application Proxy configureren voor uw tenant en het Hallo-connector installeert](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="6b8fa-111">If you haven't already, [configure Application Proxy for your tenant and install hello connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="6b8fa-112">Vervolgens [publiceren van uw on-premises toepassing](application-proxy-publish-azure-portal.md) voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="6b8fa-113">Wanneer u Hallo app publiceert, noteer de externe URL Hallo omdat uw eindgebruikers die gegevens moeten wanneer ze Hallo app tooTeams toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-113">When you're publishing hello app, make note of hello external URL because your end users need that information when they add hello app tooTeams.</span></span>

<span data-ttu-id="6b8fa-114">Als u al uw Apps die zijn gepubliceerd maar weet niet meer van de externe URL's, ze in opzoeken Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b8fa-114">If you already have your apps published but don't remember their external URLs, look them up in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6b8fa-115">Meld u aan en vervolgens te navigeren**Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen** > uw app selecteren > **Toepassingsproxy**.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-115">Sign in, then navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-tooteams"></a><span data-ttu-id="6b8fa-116">Uw app tooTeams toevoegen</span><span class="sxs-lookup"><span data-stu-id="6b8fa-116">Add your app tooTeams</span></span>

<span data-ttu-id="6b8fa-117">Zodra u Hallo app via toepassingsproxy publiceert, uw gebruikers laten weten dat ze deze als een tabblad rechtstreeks in hun kanalen Teams toevoegen kunnen.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-117">Once you publish hello app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="6b8fa-118">Hebben ze deze drie stappen:</span><span class="sxs-lookup"><span data-stu-id="6b8fa-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="6b8fa-119">Navigeer toohello Teams channel waar u tooadd deze app en selecteer  **+**  tooadd een tabblad.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-119">Navigate toohello Teams channel where you want tooadd this app and select **+** tooadd a tab.</span></span>

   ![Selecteer een tabblad toevoegen](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="6b8fa-121">Selecteer **Website** uit Hallo tabbladopties.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-121">Select **Website** from hello tab options.</span></span>

   ![Een website toevoegen](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="6b8fa-123">Geef een naam op Hallo tabblad en Hallo URL toohello toepassingsproxy externe URL ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-123">Give hello tab a name and set hello URL toohello Application Proxy external URL.</span></span> 

   ![Tabbladnaam en URL configureren](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="6b8fa-125">Wanneer een lid van een team Hallo tabblad wordt toegevoegd, wordt deze weergegeven voor iedereen in Hallo-kanaal.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-125">Once one member of a team adds hello tab, it shows up for everyone in hello channel.</span></span> <span data-ttu-id="6b8fa-126">Alle gebruikers die toegang toohello app worden geopend voor één aanmelding met Hallo-referenties die ze voor Microsoft-Teams gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-126">Any users who have access toohello app get single sign-on access with hello credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="6b8fa-127">Alle gebruikers die geen toegang tot toohello app Hallo-tabblad in Teams wordt weergegeven, maar worden geblokkeerd totdat u hen machtigingen toohello lokale app geven en de Azure portal de gepubliceerde versie van de app Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-127">Any users who don't have access toohello app will see hello tab in Teams, but are blocked until you give them permissions toohello on-premises app and hello Azure portal published version of hello app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6b8fa-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6b8fa-128">Next steps</span></span>

- <span data-ttu-id="6b8fa-129">Meer informatie over hoe te[lokale SharePoint-sites publiceren](application-proxy-enable-remote-access-sharepoint.md) met toepassingsproxy.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-129">Learn how too[publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="6b8fa-130">Configureren van uw apps toouse [aangepaste domeinen](active-directory-application-proxy-custom-domains.md) voor de externe URL.</span><span class="sxs-lookup"><span data-stu-id="6b8fa-130">Configure your apps toouse [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
