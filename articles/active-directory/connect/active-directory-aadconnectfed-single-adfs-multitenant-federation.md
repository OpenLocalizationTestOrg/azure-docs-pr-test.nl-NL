---
title: "aaaFederating meerdere Azure AD met één AD FS | Microsoft Docs"
description: In dit document wordt uitgelegd hoe toofederate meerdere Azure AD met een enkel AD FS.
keywords: "federeren, ADFS, AD FS, meerdere tenants, één AD FS, één ADFS, federatie met meerdere tenants, adfs met meerdere forests, aad connect, federatie, federatie tussen tenants"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="fb5d4-104">Meerdere exemplaren van Azure AD federeren met één exemplaar van AD FS</span><span class="sxs-lookup"><span data-stu-id="fb5d4-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="fb5d4-105">Een enkele AD FS-farm met hoge beschikbaarheid kan meerdere forests federeren als er sprake is van een tweerichtingsvertrouwensrelatie.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="fb5d4-106">Deze meerdere forests kan of kunnen niet overeen met toohello dezelfde Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-106">These multiple forests may or may not correspond toohello same Azure Active Directory.</span></span> <span data-ttu-id="fb5d4-107">In dit artikel vindt u instructies voor hoe tooconfigure federatie tussen één AD FS-implementatie en meer dan één die synchronisatie toodifferent Azure AD-forests.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-107">This article provides instructions on how tooconfigure federation between a single AD FS deployment and more than one forests that sync toodifferent Azure AD.</span></span>

![Federatie tussen meerdere tenants en één AD FS-exemplaar](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="fb5d4-109">Apparaat terugschrijven en automatisch toevoegen worden niet ondersteund in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="fb5d4-110">Azure AD Connect kan gebruikte tooconfigure federation in dit scenario niet als Azure AD Connect federation voor domeinen in een enkel Azure AD kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-110">Azure AD Connect cannot be used tooconfigure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="fb5d4-111">Stappen voor het federeren van AD FS met meerdere Azure AD-exemplaren</span><span class="sxs-lookup"><span data-stu-id="fb5d4-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="fb5d4-112">U kunt dat een domein contoso.com in Azure Active Directory-contoso.onmicrosoft.com al is gefedereerd met AD FS Hallo on-premises geïnstalleerd in contoso.com on-premises Active Directory-omgeving.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with hello AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="fb5d4-113">Fabrikam.com is een domein in de Azure Active Directory fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="fb5d4-114">Stap 1: een tweerichtingsvertrouwensrelatie tot stand brengen</span><span class="sxs-lookup"><span data-stu-id="fb5d4-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="fb5d4-115">Voor AD FS in contoso.com toobe tooauthenticate kunnen gebruikers in fabrikam.com, is een wederzijdse vertrouwensrelatie tussen contoso.com en fabrikam.com nodig. Ga als volgt Hallo richtlijn in deze [artikel](https://technet.microsoft.com/library/cc816590.aspx) toocreate Hallo wederzijdse vertrouwensrelatie.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-115">For AD FS in contoso.com toobe able tooauthenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com. Follow hello guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="fb5d4-116">Stap 2: federatie-instellingen voor contoso.com wijzigen</span><span class="sxs-lookup"><span data-stu-id="fb5d4-116">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="fb5d4-117">Hallo standaard certificaatverlener is ingesteld voor een enkel domein federatieve tooAD FS is 'http://ADFSServiceFQDN/adfs/services/trust', bijvoorbeeld 'http://fs.contoso.com/adfs/services/trust'.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-117">hello default issuer set for a single domain federated tooAD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="fb5d4-118">Voor Azure Active Directory is een unieke verlener vereist voor elk federatief domein.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-118">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="fb5d4-119">Aangezien Hallo dezelfde AD FS toofederate twee domeinen gaat, moet Hallo verlener waarde toobe zodat deze uniek is voor elk domein dat AD FS federates met Azure Active Directory is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-119">Since hello same AD FS is going toofederate two domains, hello issuer value needs toobe modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="fb5d4-120">Op Hallo AD FS-server, opent u Azure AD PowerShell en Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb5d4-120">On hello AD FS server, open Azure AD PowerShell and perform hello following steps:</span></span>
 
<span data-ttu-id="fb5d4-121">Verbinding maken met Azure Active Directory met Hallo domein contoso.com Connect MsolService Update Hallo federation-instellingen voor contoso.com Update MsolFederatedDomain - domeinnaam contoso.com toohello – SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="fb5d4-121">Connect toohello Azure Active Directory that contains hello domain contoso.com Connect-MsolService Update hello federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="fb5d4-122">Certificaatverlener in de instelling voor domeinfederatie hello wordt gewijzigd te 'http://contoso.com/adfs/services/trust' en een uitgifte claim regel voor hello Azure AD Relying Party Trust tooissue Hallo juist issuerId waarde op basis van Hallo UPN-achtervoegsel wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-122">Issuer in hello domain federation setting will be changed too"http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for hello Azure AD Relying Party Trust tooissue hello correct issuerId value based on hello UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="fb5d4-123">Stap 3: fabrikam.com federeren met AD FS</span><span class="sxs-lookup"><span data-stu-id="fb5d4-123">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="fb5d4-124">In Azure AD powershell-sessie uitvoeren Hallo stappen te volgen: verbinding maken met Active Directory met Hallo domein fabrikam.com tooAzure</span><span class="sxs-lookup"><span data-stu-id="fb5d4-124">In Azure AD powershell session perform hello following steps: Connect tooAzure Active Directory that contains hello domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="fb5d4-125">Hallo fabrikam.com beheerd domein toofederated converteren:</span><span class="sxs-lookup"><span data-stu-id="fb5d4-125">Convert hello fabrikam.com managed domain toofederated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="fb5d4-126">Hallo hierboven bewerking wordt federeren Hallo domein fabrikam.com Hello dezelfde AD FS.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-126">hello above operation will federate hello domain fabrikam.com with hello same AD FS.</span></span> <span data-ttu-id="fb5d4-127">U kunt Hallo domeininstellingen controleren met behulp van Get-MsolDomainFederationSettings voor beide domeinen.</span><span class="sxs-lookup"><span data-stu-id="fb5d4-127">You can verify hello domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb5d4-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb5d4-128">Next steps</span></span>
[<span data-ttu-id="fb5d4-129">Active Directory verbinden met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb5d4-129">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
