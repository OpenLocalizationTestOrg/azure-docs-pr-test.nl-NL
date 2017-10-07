---
title: 'Azure Active Directory B2C: Aangepaste kenmerken | Microsoft Docs'
description: Hoe toouse aangepaste kenmerken in Azure Active Directory B2C toocollect informatie over uw consumenten
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a>Azure Active Directory B2C: Gebruik aangepaste kenmerken toocollect informatie over uw consumenten
Uw Azure Active Directory (Azure AD) B2C-directory wordt geleverd met een ingebouwde verzameling gegevens (kenmerken): voornaam, achternaam, plaats, postcode en andere kenmerken. Elke consumentgerichte toepassing heeft echter unieke vereisten op welke toogather kenmerken van consumenten. Met Azure AD B2C, kunt u Hallo set kenmerken die zijn opgeslagen op elke consumentenaccount uitbreiden. U kunt aangepaste kenmerken maken op Hallo [Azure-portal](https://portal.azure.com/) en deze gebruiken in uw registratie-beleid, zoals hieronder wordt weergegeven. U kunt ook lezen en schrijven van deze kenmerken met behulp van Hallo [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Gebruik van aangepaste kenmerken [Azure AD Graph API Directory-Schemauitbreidingen](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Een aangepast kenmerk maken
1. [Volg deze stappen toonavigate toohello B2C-functiesblade op Hallo Azure-portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Klik op **gebruikerskenmerken**.
3. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
4. Geef een **naam** voor Hallo aangepast kenmerk (bijvoorbeeld ' ShoeSize') en eventueel een **beschrijving**. Klik op **Create**.
   
   > [!NOTE]
   > Alleen Hallo 'String' **gegevenstype** is momenteel beschikbaar.
   > 
   > 

Hallo aangepast kenmerk is nu beschikbaar in de lijst met Hallo **gebruikerskenmerken**, en voor gebruik in uw registratie-beleid.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Gebruik een aangepast kenmerk in het registratiebeleid
1. [Volg deze stappen toonavigate toohello B2C-functiesblade op Hallo Azure-portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Klik op **Registratiebeleid**.
3. Klik op uw tooopen registratiebeleid (bijvoorbeeld ' B2C_1_SiUp') deze. Klik op **bewerken** Hallo boven aan het Hallo-blade.
4. Klik op **registratiekenmerken** en selecteer Hallo aangepast kenmerk (bijvoorbeeld ' ShoeSize'). Klik op **OK**.
5. Klik op **toepassingsclaims** en selecteer Hallo aangepast kenmerk. Klik op **OK**.
6. Klik op **opslaan** Hallo boven aan het Hallo-blade.

Hallo 'Nu uitvoeren' functie kunt u op Hallo beleid tooverify Hallo consumer ervaring. U moet nu Zie 'ShoeSize' in Hallo-lijst met kenmerken die zijn verzameld tijdens consumenten registreren en deze in Hallo token verzonden back tooyour toepassing.

## <a name="notes"></a>Opmerkingen
* Samen met aanmelding beleid kunnen ook aangepaste kenmerken worden gebruikt in beleid voor het registreren of aanmelden en profiel bewerken van beleid.
* Er is een bekende beperking van aangepaste kenmerken. Het is alleen Hallo eerste keer dat deze wordt gebruikt in een beleid gemaakt en niet wanneer u deze lijst met toohello toevoegen **gebruikerskenmerken**.

