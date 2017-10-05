---
title: Fouten opsporen in op basis van SAML eenmalige aanmelding tot toepassingen in Azure Active Directory | Microsoft Docs
description: 'Meer informatie over fouten opsporen in op basis van SAML eenmalige aanmelding tot toepassingen in Azure Active Directory '
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
ms.openlocfilehash: 31447d597296bac57481dc2acb4a95ee3a104161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="54d9b-103">Fouten opsporen in op basis van SAML eenmalige aanmelding tot toepassingen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54d9b-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>
<span data-ttu-id="54d9b-104">Wanneer een toepassing op basis van SAML-integratie foutopsporing, is het vaak nuttig zijn voor het gebruik van een hulpprogramma zoals [Fiddler](http://www.telerik.com/fiddler) om te zien van de SAML-aanvraag, de SAML-reactie en de werkelijke SAML-token dat is uitgegeven aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="54d9b-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span></span> <span data-ttu-id="54d9b-105">Door in het SAML-token, kunt u ervoor zorgen dat alle vereiste kenmerken, de gebruikersnaam in het SAML-onderwerp en de URI van de verlener afkomstig via zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="54d9b-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="54d9b-106">Het antwoord van Azure AD met het SAML-token is doorgaans een die plaatsvindt na een HTTP 302-omleiding van https://login.windows.net en wordt verzonden naar de geconfigureerde **antwoord-URL** van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="54d9b-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span></span> 

<span data-ttu-id="54d9b-107">U kunt het SAML-token weergeven door deze regel te selecteren en vervolgens te klikken op de **Inspectors > webformulieren** tabblad in het rechterpaneel.</span><span class="sxs-lookup"><span data-stu-id="54d9b-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span></span> <span data-ttu-id="54d9b-108">Van daaruit met de rechtermuisknop op de **SAMLResponse** waarde en selecteert u **verzenden naar TextWizard**.</span><span class="sxs-lookup"><span data-stu-id="54d9b-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span></span> <span data-ttu-id="54d9b-109">Selecteer vervolgens **van Base64** van de **transformeren** menu voor het decoderen van het token en de inhoud weergeven.</span><span class="sxs-lookup"><span data-stu-id="54d9b-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span></span>

<span data-ttu-id="54d9b-110">**Opmerking**: overzicht van de inhoud van deze HTTP-aanvraag Fiddler u mogelijk gevraagd te configureren van de ontsleuteling van HTTPS-verkeer, wat u moet doen.</span><span class="sxs-lookup"><span data-stu-id="54d9b-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span></span>

## <a name="related-articles"></a><span data-ttu-id="54d9b-111">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="54d9b-111">Related Articles</span></span>
* <span data-ttu-id="54d9b-112">[Article Index for Application Management in Azure Active Directory](../active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="54d9b-112">[Article Index for Application Management in Azure Active Directory](../active-directory-apps-index.md)</span></span>
* <span data-ttu-id="54d9b-113">[Configuring single sign-on to applications that are not in the Azure Active Directory application gallery](../active-directory-saas-custom-apps.md) (Eenmalige aanmelding configureren voor toepassingen die zich niet in de Azure Active Directory-toepassingsgalerie bevinden)</span><span class="sxs-lookup"><span data-stu-id="54d9b-113">[Configuring single sign-on to applications that are not in the Azure Active Directory application gallery](../active-directory-saas-custom-apps.md)</span></span>
* [<span data-ttu-id="54d9b-114">Het aanpassen van uitgegeven Claims in het SAML-Token voor vooraf geïntegreerde Apps</span><span class="sxs-lookup"><span data-stu-id="54d9b-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png