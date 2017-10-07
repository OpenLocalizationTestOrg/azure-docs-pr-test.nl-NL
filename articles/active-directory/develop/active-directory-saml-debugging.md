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
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>Hoe toodebug op basis van SAML eenmalige aanmelding tooapplications in Azure Active Directory
Wanneer een toepassing op basis van SAML-integratie foutopsporing, is het vaak nuttig toouse een hulpprogramma zoals [Fiddler](http://www.telerik.com/fiddler) toosee Hallo SAML-aanvraag, Hallo SAML-reactie en Hallo werkelijke SAML-token dat is uitgegeven toohello toepassing. Door te onderzoeken Hallo SAML-token, kunt u ervoor dat alle Hallo kenmerken verplichte, Hallo gebruikersnaam in Hallo SAML onderwerp en Hallo verlener URI afkomstig zijn via zoals verwacht.

![][1]

Hallo reactie van Azure AD met Hallo SAML-token is doorgaans Hallo die na een HTTP 302-omleiding van https://login.windows.net plaatsvindt en verzonden toohello geconfigureerd **antwoord-URL** van Hallo-toepassing. 

U kunt Hallo SAML-token weergeven door deze regel te selecteren Hallo **Inspectors > webformulieren** tabblad in het rechterpaneel Hallo. Met de rechtermuisknop op Hallo van daaruit **SAMLResponse** waarde en selecteert u **tooTextWizard verzenden**. Selecteer vervolgens **van Base64** van Hallo **transformeren** menu toodecode Hallo token en de inhoud ervan bekijken.

**Opmerking**: toosee Hallo inhoud van deze HTTP-aanvragen, Fiddler u tooconfigure ontsleuteling van HTTPS-verkeer, u moet mogelijk gevraagd toodo.

## <a name="related-articles"></a>Verwante artikelen
* [Article Index for Application Management in Azure Active Directory](../active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Eenmalige aanmelding tooapplications die zich niet in de Azure Active Directory-toepassingsgalerie Hallo configureren](../active-directory-saas-custom-apps.md)
* [Hoe tooCustomize Claims uitgegeven hello SAML-Token voor Pre-Integrated Apps](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png