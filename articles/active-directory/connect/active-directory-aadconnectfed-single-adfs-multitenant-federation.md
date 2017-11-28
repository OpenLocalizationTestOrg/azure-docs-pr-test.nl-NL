---
title: "Meerdere exemplaren van Azure AD federeren met één exemplaar van AD FS | Microsoft Docs"
description: "In dit document leert u hoe u meerdere exemplaren van Azure AD federeert met één exemplaar van AD FS."
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
ms.openlocfilehash: 436bf5905d2b203dc4cceea97f4fb90593df7111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="f39c6-104">Meerdere exemplaren van Azure AD federeren met één exemplaar van AD FS</span><span class="sxs-lookup"><span data-stu-id="f39c6-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="f39c6-105">Een enkele AD FS-farm met hoge beschikbaarheid kan meerdere forests federeren als er sprake is van een tweerichtingsvertrouwensrelatie.</span><span class="sxs-lookup"><span data-stu-id="f39c6-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="f39c6-106">Deze meerdere forests komen al dan niet overeen met de dezelfde Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f39c6-106">These multiple forests may or may not correspond to the same Azure Active Directory.</span></span> <span data-ttu-id="f39c6-107">In dit artikel leest u hoe u een federatie configureert tussen één AD FS-implementatie en meerdere forests die synchroniseren met verschillende exemplaren van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f39c6-107">This article provides instructions on how to configure federation between a single AD FS deployment and more than one forests that sync to different Azure AD.</span></span>

![Federatie tussen meerdere tenants en één AD FS-exemplaar](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="f39c6-109">Apparaat terugschrijven en automatisch toevoegen worden niet ondersteund in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="f39c6-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="f39c6-110">Azure AD Connect kan niet worden gebruikt om in dit scenario federatie te configureren, omdat Azure AD Connect alleen federatie kan configureren voor domeinen in één Azure AD-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f39c6-110">Azure AD Connect cannot be used to configure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="f39c6-111">Stappen voor het federeren van AD FS met meerdere Azure AD-exemplaren</span><span class="sxs-lookup"><span data-stu-id="f39c6-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="f39c6-112">Ga ervan uit dat het domein contoso.com in de Azure Active Directory contoso.onmicrosoft.com al is gefedereerd met de on-premises AD FS die is geïnstalleerd in de on-premises Active Directory-omgeving contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f39c6-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with the AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="f39c6-113">Fabrikam.com is een domein in de Azure Active Directory fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f39c6-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="f39c6-114">Stap 1: een tweerichtingsvertrouwensrelatie tot stand brengen</span><span class="sxs-lookup"><span data-stu-id="f39c6-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="f39c6-115">AD FS in contoso.com kan alleen gebruikers in fabrikam.com verifiëren als er een tweerichtingsvertrouwensrelatie tussen contoso.com en fabrikam.com bestaat.</span><span class="sxs-lookup"><span data-stu-id="f39c6-115">For AD FS in contoso.com to be able to authenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com.</span></span> <span data-ttu-id="f39c6-116">Volg de stappen in [dit artikel](https://technet.microsoft.com/library/cc816590.aspx) om een tweerichtingsvertrouwensrelatie tot stand te brengen.</span><span class="sxs-lookup"><span data-stu-id="f39c6-116">Follow the guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) to create the two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="f39c6-117">Stap 2: federatie-instellingen voor contoso.com wijzigen</span><span class="sxs-lookup"><span data-stu-id="f39c6-117">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="f39c6-118">De standaardverlener die voor een enkel met AD FS gefedereerd domein wordt ingesteld, is 'http://ADFSServiceFQDN/adfs/services/trust', bijvoorbeeld 'http://fs.contoso.com/adfs/services/trust'.</span><span class="sxs-lookup"><span data-stu-id="f39c6-118">The default issuer set for a single domain federated to AD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="f39c6-119">Voor Azure Active Directory is een unieke verlener vereist voor elk federatief domein.</span><span class="sxs-lookup"><span data-stu-id="f39c6-119">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="f39c6-120">Aangezien dezelfde AD FS twee domeinen gaat federeren, moet de waarde voor de verlener zodanig worden gewijzigd dat deze uniek is voor elk domein dat AD FS federeert met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f39c6-120">Since the same AD FS is going to federate two domains, the issuer value needs to be modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="f39c6-121">Open Azure AD PowerShell op de AD FS-server en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f39c6-121">On the AD FS server, open Azure AD PowerShell and perform the following steps:</span></span>
 
<span data-ttu-id="f39c6-122">Maak verbinding met de Azure Active Directory met het domein contoso.com
Connect-MsolService
Werk de federatie-instellingen bij voor contoso.com
Update-MsolFederatedDomain-DomainName contoso.com-SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="f39c6-122">Connect to the Azure Active Directory that contains the domain contoso.com Connect-MsolService Update the federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="f39c6-123">De verlener in de federatie-instelling van het domein wordt gewijzigd in 'http://contoso.com/adfs/services/trust' en er wordt een claimregel voor uitgifte toegevoegd voor de Relying Party Trust van Azure AD, om de juiste issuerId-waarde uit te geven op basis van het UPN-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="f39c6-123">Issuer in the domain federation setting will be changed to "http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for the Azure AD Relying Party Trust to issue the correct issuerId value based on the UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="f39c6-124">Stap 3: fabrikam.com federeren met AD FS</span><span class="sxs-lookup"><span data-stu-id="f39c6-124">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="f39c6-125">Voer de volgende stappen uit in een PowerShell-sessie in Azure AD: maak verbinding met de Azure Active Directory met het domein fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="f39c6-125">In Azure AD powershell session perform the following steps: Connect to Azure Active Directory that contains the domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="f39c6-126">Converteer het beheerde domein fabrikam.com dat u wilt federeren:</span><span class="sxs-lookup"><span data-stu-id="f39c6-126">Convert the fabrikam.com managed domain to federated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="f39c6-127">Met de bovenstaande bewerking wordt het domein fabrikam.com gefedereerd met dezelfde AD FS.</span><span class="sxs-lookup"><span data-stu-id="f39c6-127">The above operation will federate the domain fabrikam.com with the same AD FS.</span></span> <span data-ttu-id="f39c6-128">U kunt de domeininstellingen voor beide domeinen controleren met Get-MsolDomainFederationSettings.</span><span class="sxs-lookup"><span data-stu-id="f39c6-128">You can verify the domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f39c6-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f39c6-129">Next steps</span></span>
[<span data-ttu-id="f39c6-130">Active Directory verbinden met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f39c6-130">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
