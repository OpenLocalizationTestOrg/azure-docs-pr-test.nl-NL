---
title: aaaHow toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure Active Directory | Microsoft Docs
description: 'Meer informatie over hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure Active Directory '
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="c43d1-103">Hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c43d1-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="c43d1-104">Wanneer een toepassing op basis van SAML-integratie foutopsporing, is het vaak nuttig toouse een hulpprogramma zoals [Fiddler](http://www.telerik.com/fiddler) toosee Hallo SAML-aanvraag, Hallo SAML-reactie en Hallo werkelijke SAML-token dat is uitgegeven toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="c43d1-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="c43d1-105">Door te onderzoeken Hallo SAML-token, kunt u ervoor dat alle Hallo kenmerken verplichte, Hallo gebruikersnaam in Hallo SAML onderwerp en Hallo verlener URI afkomstig zijn via zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="c43d1-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="c43d1-106">Hallo reactie van Azure AD met Hallo SAML-token is doorgaans Hallo die na een HTTP 302-omleiding van https://login.windows.net plaatsvindt en verzonden toohello geconfigureerd **antwoord-URL** van Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c43d1-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="c43d1-107">U kunt Hallo SAML-token weergeven door deze regel te selecteren Hallo **Inspectors > webformulieren** tabblad in het rechterpaneel Hallo.</span><span class="sxs-lookup"><span data-stu-id="c43d1-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="c43d1-108">Met de rechtermuisknop op Hallo van daaruit **SAMLResponse** waarde en selecteert u **tooTextWizard verzenden**.</span><span class="sxs-lookup"><span data-stu-id="c43d1-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="c43d1-109">Selecteer vervolgens **van Base64** van Hallo **transformeren** menu toodecode Hallo token en de inhoud ervan bekijken.</span><span class="sxs-lookup"><span data-stu-id="c43d1-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="c43d1-110">**Opmerking**: toosee Hallo inhoud van deze HTTP-aanvragen, Fiddler u tooconfigure ontsleuteling van HTTPS-verkeer, u moet mogelijk gevraagd toodo.</span><span class="sxs-lookup"><span data-stu-id="c43d1-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="c43d1-111">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="c43d1-111">Related Articles</span></span>
* <span data-ttu-id="c43d1-112">[Article Index for Application Management in Azure Active Directory](../active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="c43d1-112">[Article Index for Application Management in Azure Active Directory](../active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="c43d1-113">Eenmalige aanmelding tooapplications die zich niet in de Azure Active Directory-toepassingsgalerie Hallo configureren</span><span class="sxs-lookup"><span data-stu-id="c43d1-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="c43d1-114">Hoe tooCustomize Claims uitgegeven hello SAML-Token voor Pre-Integrated Apps</span><span class="sxs-lookup"><span data-stu-id="c43d1-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png