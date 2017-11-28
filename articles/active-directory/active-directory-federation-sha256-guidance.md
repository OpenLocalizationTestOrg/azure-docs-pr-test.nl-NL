---
title: Wijziging handtekening hash-algoritme voor Office 365 relying-partyvertrouwensrelatie | Microsoft Docs
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
ms.openlocfilehash: c581b1468630a9f28204592c936360b72f42f0d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="a254a-104">Handtekening hash-algoritme voor Office 365 vertrouwensrelatie van relying party wijzigen</span><span class="sxs-lookup"><span data-stu-id="a254a-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="a254a-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a254a-105">Overview</span></span>
<span data-ttu-id="a254a-106">Active Directory Federation Services (AD FS), ondertekent de tokens in Microsoft Azure Active Directory om ervoor te zorgen dat ze met kunnen worden geknoeid.</span><span class="sxs-lookup"><span data-stu-id="a254a-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span></span> <span data-ttu-id="a254a-107">Deze handtekening kan zijn gebaseerd op SHA1 of SHA256.</span><span class="sxs-lookup"><span data-stu-id="a254a-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="a254a-108">Azure Active Directory biedt nu ondersteuning voor tokens die zijn ondertekend met een algoritme SHA256 en het is raadzaam als u het algoritme voor token-ondertekening op SHA256 voor het hoogste niveau van beveiliging.</span><span class="sxs-lookup"><span data-stu-id="a254a-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span></span> <span data-ttu-id="a254a-109">In dit artikel beschrijft de stappen die nodig zijn voor de algoritme voor token-ondertekening ingesteld op veiliger SHA256 niveau.</span><span class="sxs-lookup"><span data-stu-id="a254a-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="a254a-110">Microsoft raadt informatie over het gebruik van SHA256 als voor het ondertekenen van tokens als het is veiliger dan SHA1 maar nog steeds een ondersteunde optie SHA1-algoritme.</span><span class="sxs-lookup"><span data-stu-id="a254a-110">Microsoft recommends usage of SHA256 as the algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-the-token-signing-algorithm"></a><span data-ttu-id="a254a-111">Wijzigen van het algoritme voor token-ondertekening</span><span class="sxs-lookup"><span data-stu-id="a254a-111">Change the token-signing algorithm</span></span>
<span data-ttu-id="a254a-112">Nadat u de algoritme voor handtekening met een van de twee onderstaande processen hebt ingesteld, wordt in AD FS de tokens voor Office 365 relying party trust met SHA256 ondertekent.</span><span class="sxs-lookup"><span data-stu-id="a254a-112">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="a254a-113">U hoeft niet te worden eventuele extra configuratiewijzigingen aanbrengen en deze wijziging heeft geen invloed op uw mogelijkheid voor toegang tot Office 365 of andere Azure AD-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a254a-113">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="a254a-114">AD FS-beheerconsole</span><span class="sxs-lookup"><span data-stu-id="a254a-114">AD FS management console</span></span>
1. <span data-ttu-id="a254a-115">Open de AD FS-beheerconsole op de primaire AD FS-server.</span><span class="sxs-lookup"><span data-stu-id="a254a-115">Open the AD FS management console on the primary AD FS server.</span></span>
2. <span data-ttu-id="a254a-116">Vouw het knooppunt van de AD FS en klik op **Relying Party-vertrouwensrelaties**.</span><span class="sxs-lookup"><span data-stu-id="a254a-116">Expand the AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="a254a-117">Met de rechtermuisknop op uw Office 365/Azure-vertrouwensrelatie voor relying party en selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="a254a-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="a254a-118">Selecteer de **Geavanceerd** tabblad en selecteer het veilige hash-algoritme SHA256.</span><span class="sxs-lookup"><span data-stu-id="a254a-118">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="a254a-119">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a254a-119">Click **OK**.</span></span>

![SHA256 ondertekeningsalgoritme--MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="a254a-121">AD FS-PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="a254a-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="a254a-122">Open PowerShell onder administrator-bevoegdheden op de AD FS-server.</span><span class="sxs-lookup"><span data-stu-id="a254a-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="a254a-123">Het veilige hash-algoritme ingesteld met behulp van de **Set-AdfsRelyingPartyTrust** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a254a-123">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="a254a-124">Lees ook</span><span class="sxs-lookup"><span data-stu-id="a254a-124">Also read</span></span>
* [<span data-ttu-id="a254a-125">Herstel van Office 365-vertrouwensrelatie met Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="a254a-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

