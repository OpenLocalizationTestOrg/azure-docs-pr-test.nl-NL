---
title: Azure AD Join instellen voor gebruikers | Microsoft Docs
description: Hier wordt uitgelegd hoe beheerders Azure AD Join kunnen instellen voor on-premises directory- en apparaatregistratie.
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: c37adc2654f7e931fdda22627e4a6ece2789fd86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="7d137-103">Azure AD Join instellen in uw organisatie</span><span class="sxs-lookup"><span data-stu-id="7d137-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="7d137-104">Voordat u Azure Active Directory Join (Azure AD Join) instelt, moet u uw on-premises directory van gebruikers synchroniseren met de cloud of handmatig beheerde accounts maken in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d137-104">Before you set up Azure Active Directory Join (Azure AD Join), you need to either sync up your on-premises directory of users to the cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="7d137-105">Gedetailleerde instructies voor het synchroniseren van uw on-premises gebruikers naar Azure AD zijn te vinden in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md) (Engelstalig).</span><span class="sxs-lookup"><span data-stu-id="7d137-105">Detailed instructions for syncing your on-premises users to Azure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="7d137-106">Raadpleeg [Gebruikersaccounts en wachtwoorden](https://msdn.microsoft.com/library/azure/hh967609.aspx) als u handmatig gebruikers wilt maken en beheren in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d137-106">To manually create and manage users in Azure AD, refer to [User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="7d137-107">Apparaatregistratie instellen</span><span class="sxs-lookup"><span data-stu-id="7d137-107">Set up device registration</span></span>
1. <span data-ttu-id="7d137-108">Meld u als beheerder aan bij de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7d137-108">Log on to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="7d137-109">Selecteer in het linkerdeelvenster **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d137-109">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="7d137-110">Selecteer uw directory op het tabblad **Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d137-110">On the **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="7d137-111">Selecteer de tab **Configureren**.</span><span class="sxs-lookup"><span data-stu-id="7d137-111">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="7d137-112">Ga naar de sectie **Apparaten**.</span><span class="sxs-lookup"><span data-stu-id="7d137-112">Go to the **Devices** section.</span></span>
6. <span data-ttu-id="7d137-113">Stel het volgende in op het tabblad **Apparaten**:</span><span class="sxs-lookup"><span data-stu-id="7d137-113">On the **devices** tab, set the following:</span></span>  
   * <span data-ttu-id="7d137-114">**MAXIMUMAANTAL APPARATEN PER GEBRUIKER**: selecteer het maximumaantal apparaten dat een gebruiker mag hebben in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d137-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select the maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="7d137-115">Als een gebruiker dit quotum bereikt, kan deze persoon geen apparaten meer toevoegen totdat een of meer van de bestaande apparaten zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7d137-115">If a user reaches this quota, they will not be able to add additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="7d137-116">**MEERVOUDIGE VERIFICATIE VEREISEN VOOR HET TOEVOEGEN VAN APPARATEN**: hiermee stelt u in of gebruikers een tweede verificatiefactor moeten opgeven om hun apparaat toe te voegen aan Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d137-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES**: Set whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="7d137-117">Zie [Aan de slag met Azure Multi-Factor Authentication in de cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md) voor meer informatie over meervoudige verificatie met Azure.</span><span class="sxs-lookup"><span data-stu-id="7d137-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="7d137-118">**GEBRUIKERS MOGEN APPARATEN TOEVOEGEN AAN AZURE**: selecteer de gebruikers en groepen die apparaten mogen toevoegen aan Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d137-118">**USERS MAY AZURE AD JOIN DEVICES**: Select the users and groups that are allowed to join devices to Azure AD.</span></span>
   * <span data-ttu-id="7d137-119">**EXTRA BEHEERDERS OP AZURE AD MET TOEGEVOEGDE APPARATEN**: met Azure AD Premium of de Enterprise Mobility Suite (EMS) kunt u kiezen welke gebruikers lokale beheerdersrechten ontvangen voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="7d137-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or the Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights to the device.</span></span> <span data-ttu-id="7d137-120">Globale beheerders en eigenaren van de apparaten ontvangen standaard lokale beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="7d137-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="7d137-121"><center>![Apparaatregistratie instellen](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="7d137-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="7d137-122">Nadat u Azure AD Join hebt ingesteld voor gebruikers, kunnen ze verbinding maken met Azure AD via hun bedrijfs- of persoonlijke apparaten.</span><span class="sxs-lookup"><span data-stu-id="7d137-122">After you set up Azure AD Join for your users, they can connect to Azure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="7d137-123">Met de volgende drie scenario's kunt u uw gebruikers in staat stellen Azure AD Join in te stellen:</span><span class="sxs-lookup"><span data-stu-id="7d137-123">Following are the three scenarios you can use to enable your users to set up Azure AD Join:</span></span>

* <span data-ttu-id="7d137-124">Gebruikers voegen rechtstreeks een bedrijfsapparaat toe aan Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d137-124">Users join a company-owned device directly to Azure AD.</span></span>
* <span data-ttu-id="7d137-125">Gebruikers voegen via een domein een bedrijfsapparaat toe aan de on-premises Active Directory en breiden het apparaat vervolgens uit naar Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d137-125">Users domain-join a company-owned device to the on-premises Active Directory and then extend the device to Azure AD.</span></span>
* <span data-ttu-id="7d137-126">Gebruikers voegen werk- of schoolaccounts toe aan Windows op een persoonlijk apparaat</span><span class="sxs-lookup"><span data-stu-id="7d137-126">Users add work or school accounts to Windows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="7d137-127">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="7d137-127">Additional information</span></span>
* <span data-ttu-id="7d137-128">[Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md) (Windows 10 voor de onderneming: manieren om apparaten voor werk te gebruiken)</span><span class="sxs-lookup"><span data-stu-id="7d137-128">[Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md)</span></span>
* <span data-ttu-id="7d137-129">[Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md) (Cloudmogelijkheden uitbreiden naar Windows 10-apparaten met behulp van Azure Active Directory Join)</span><span class="sxs-lookup"><span data-stu-id="7d137-129">[Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)</span></span>
* <span data-ttu-id="7d137-130">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)</span><span class="sxs-lookup"><span data-stu-id="7d137-130">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)</span></span>
* <span data-ttu-id="7d137-131">[Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md) (Apparaten die lid zijn van een domein verbinden met Azure AD voor Windows 10-ervaringen)</span><span class="sxs-lookup"><span data-stu-id="7d137-131">[Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md)</span></span>
* [<span data-ttu-id="7d137-132">Azure AD Join instellen</span><span class="sxs-lookup"><span data-stu-id="7d137-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

