---
title: aaaTwo stap verificatie- en AD FS - Azure MFA | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina waarop wordt beschreven hoe tooget de slag met Azure MFA en AD FS.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="1b9fe-103">Aan de slag met Azure Multi-Factor Authentication en Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="1b9fe-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="1b9fe-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="1b9fe-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="1b9fe-105">Als uw organisatie met behulp van AD FS uw on-premises Active Directory heeft gefedereerd met Azure Active Directory, zijn er twee opties voor het gebruik van Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="1b9fe-106">Cloudresources beveiligen met Azure Multi-Factor Authentication of Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="1b9fe-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="1b9fe-107">Cloudresources en on-premises resources beveiligen met behulp van de Azure Multi-Factor Authentication-server</span><span class="sxs-lookup"><span data-stu-id="1b9fe-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="1b9fe-108">Hallo volgende tabel geeft een overzicht van de verificatie-ervaring Hallo tussen het beveiligen van resources met Azure multi-factor Authentication en AD FS</span><span class="sxs-lookup"><span data-stu-id="1b9fe-108">hello following table summarizes hello verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="1b9fe-109">Verificatie-ervaring - op browser gebaseerde apps</span><span class="sxs-lookup"><span data-stu-id="1b9fe-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="1b9fe-110">Verificatie-ervaring - niet op browser gebaseerde apps</span><span class="sxs-lookup"><span data-stu-id="1b9fe-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1b9fe-111">Beveiligen van Azure AD-resources met Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="1b9fe-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="1b9fe-112">de eerste verificatiestap Hello wordt uitgevoerd on-premises met AD FS.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-112">hello first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="1b9fe-113">Hallo tweede stap bestaat uit een telefonische methode die wordt uitgevoerd met cloudverificatie.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-113">hello second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="1b9fe-114">Azure AD-resources beveiligen met behulp van Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="1b9fe-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="1b9fe-115">de eerste verificatiestap Hello wordt uitgevoerd on-premises met AD FS.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-115">hello first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="1b9fe-116">de tweede stap Hallo is on-premises uitgevoerd door Hallo claim naleven.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-116">hello second step is performed on-premises by honoring hello claim.</span></span></li> |

<span data-ttu-id="1b9fe-117">Valkuilen met app-wachtwoorden voor federatieve gebruikers:</span><span class="sxs-lookup"><span data-stu-id="1b9fe-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="1b9fe-118">App-wachtwoorden worden gecontroleerd met cloudverificatie en daarom worden federaties omzeild.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="1b9fe-119">Federatie wordt alleen actief gebruikt bij het instellen van het app-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="1b9fe-120">On-premises instellingen voor toegangsbeheer van client worden niet herkend door app-wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="1b9fe-121">U raakt on-premises mogelijkheden voor logboekregistratie bij verificatie voor app-wachtwoorden kwijt.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="1b9fe-122">Account uitschakelen/verwijderen kan duren voordat toothree uur voor directory-synchronisatie uitschakelen/verwijderen van app-wachtwoorden in de cloud-identiteit Hallo vertragen.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-122">Account disable/deletion may take up toothree hours for directory sync, delaying disable/deletion of app passwords in hello cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b9fe-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b9fe-123">Next steps</span></span>
<span data-ttu-id="1b9fe-124">Zie voor informatie over het instellen van Azure multi-factor Authentication of hello Azure multi-factor Authentication-Server met AD FS Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1b9fe-124">For information on setting up either Azure Multi-Factor Authentication or hello Azure Multi-Factor Authentication Server with AD FS, see hello following articles:</span></span>

* [<span data-ttu-id="1b9fe-125">Cloudresources beveiligen met behulp van Azure Multi-Factor Authentication en AD FS</span><span class="sxs-lookup"><span data-stu-id="1b9fe-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="1b9fe-126">Cloudresources en on-premises resources beveiligen met behulp van de Azure Multi-Factor Authentication-server met Windows Server 2012 R2 AD FS</span><span class="sxs-lookup"><span data-stu-id="1b9fe-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="1b9fe-127">Cloudresources en on-premises resources beveiligen met behulp van de Azure Multi-Factor Authentication-server met AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="1b9fe-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
