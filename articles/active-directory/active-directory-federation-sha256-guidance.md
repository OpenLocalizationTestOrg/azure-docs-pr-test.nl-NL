---
title: aaaChange handtekening hash-algoritme voor Office 365 relying-partyvertrouwensrelatie | Microsoft Docs
description: Deze pagina bevat richtlijnen voor het wijzigen van SHA-algoritme voor federatieve vertrouwensrelatie met Office 365
keywords: SHA1, SHA256, O365, Federatie, aadconnect, adfs, ad fs, wijziging sha, federatieve vertrouwensrelatie, vertrouwensrelatie van relying party
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="5eddb-104">Handtekening hash-algoritme voor Office 365 vertrouwensrelatie van relying party wijzigen</span><span class="sxs-lookup"><span data-stu-id="5eddb-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="5eddb-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5eddb-105">Overview</span></span>
<span data-ttu-id="5eddb-106">Active Directory Federation Services (AD FS), ondertekent de Azure Active Directory-tooensure voor tokens tooMicrosoft met kan worden geknoeid.</span><span class="sxs-lookup"><span data-stu-id="5eddb-106">Active Directory Federation Services (AD FS) signs its tokens tooMicrosoft Azure Active Directory tooensure that they cannot be tampered with.</span></span> <span data-ttu-id="5eddb-107">Deze handtekening kan zijn gebaseerd op SHA1 of SHA256.</span><span class="sxs-lookup"><span data-stu-id="5eddb-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="5eddb-108">Azure Active Directory biedt nu ondersteuning voor tokens die zijn ondertekend met een algoritme SHA256 en het is raadzaam Hallo token-ondertekening algoritme tooSHA256 voor Hallo hoogste niveau van beveiliging instellen.</span><span class="sxs-lookup"><span data-stu-id="5eddb-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting hello token-signing algorithm tooSHA256 for hello highest level of security.</span></span> <span data-ttu-id="5eddb-109">In dit artikel worden Hallo stappen beschreven die nodig zijn tooset Hallo token-ondertekening algoritme toohello veiliger SHA256-niveau.</span><span class="sxs-lookup"><span data-stu-id="5eddb-109">This article describes hello steps needed tooset hello token-signing algorithm toohello more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="5eddb-110">Microsoft raadt informatie over het gebruik van SHA256 als Hallo-algoritme voor het ondertekenen van tokens als het is veiliger dan SHA1 maar SHA1 nog steeds ondersteund.</span><span class="sxs-lookup"><span data-stu-id="5eddb-110">Microsoft recommends usage of SHA256 as hello algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-hello-token-signing-algorithm"></a><span data-ttu-id="5eddb-111">Hallo-algoritme voor token-ondertekening wijzigen</span><span class="sxs-lookup"><span data-stu-id="5eddb-111">Change hello token-signing algorithm</span></span>
<span data-ttu-id="5eddb-112">Nadat u de handtekeningalgoritme Hallo met een van twee processen Hallo onderstaande hebt ingesteld, ondertekent AD FS-tokens Hallo voor Office 365 relying party trust met SHA256.</span><span class="sxs-lookup"><span data-stu-id="5eddb-112">After you have set hello signature algorithm with one of hello two processes below, AD FS signs hello tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="5eddb-113">U hoeft niet toomake extra configuratiewijzigingen en deze wijziging heeft geen invloed op uw mogelijkheid tooaccess Office 365 of andere Azure AD-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5eddb-113">You don't need toomake any extra configuration changes, and this change has no impact on your ability tooaccess Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="5eddb-114">AD FS-beheerconsole</span><span class="sxs-lookup"><span data-stu-id="5eddb-114">AD FS management console</span></span>
1. <span data-ttu-id="5eddb-115">Open Hallo AD FS-beheerconsole op Hallo primaire AD FS-server.</span><span class="sxs-lookup"><span data-stu-id="5eddb-115">Open hello AD FS management console on hello primary AD FS server.</span></span>
2. <span data-ttu-id="5eddb-116">Vouw Hallo AD FS-knooppunt en klik op **Relying Party-vertrouwensrelaties**.</span><span class="sxs-lookup"><span data-stu-id="5eddb-116">Expand hello AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="5eddb-117">Met de rechtermuisknop op uw Office 365/Azure-vertrouwensrelatie voor relying party en selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="5eddb-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="5eddb-118">Selecteer Hallo **Geavanceerd** tabblad en selecteer Hallo veilige hash-algoritme SHA256.</span><span class="sxs-lookup"><span data-stu-id="5eddb-118">Select hello **Advanced** tab and select hello secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="5eddb-119">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5eddb-119">Click **OK**.</span></span>

![SHA256 ondertekeningsalgoritme--MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="5eddb-121">AD FS-PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="5eddb-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="5eddb-122">Open PowerShell onder administrator-bevoegdheden op de AD FS-server.</span><span class="sxs-lookup"><span data-stu-id="5eddb-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="5eddb-123">Set Hallo veilige hash-algoritme met behulp van Hallo **Set-AdfsRelyingPartyTrust** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5eddb-123">Set hello secure hash algorithm by using hello **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="5eddb-124">Lees ook</span><span class="sxs-lookup"><span data-stu-id="5eddb-124">Also read</span></span>
* [<span data-ttu-id="5eddb-125">Herstel van Office 365-vertrouwensrelatie met Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="5eddb-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

