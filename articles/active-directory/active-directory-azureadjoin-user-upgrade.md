---
title: aaaSet van een Windows 10-apparaat met Azure AD via instellingen | Microsoft Docs
description: Legt uit hoe gebruikers kunnen deelnemen aan tooAzure AD via het menu Hallo-instellingen.
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Instellen van een Windows 10-apparaat met Azure AD via instellingen
Als u al bent bijgewerkte tooWindows 10 met behulp van Windows 7 of Windows 8 en uw computer of apparaat is, kunt u deelnemen aan tooAzure Active Directory (Azure AD) via het menu Hallo-instellingen.

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>toojoin tooAzure AD in Hallo-instellingen
1. Van Hallo **Start** menu, klikt u op Hallo **instellingen** charm.
2. Van **instellingen**, selecteer **System**->**over**->**Azure AD Join**.
   
   <center>
   ![Deelnemen aan Azure AD in Hallo-instellingen](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Klik op **doorgaan** in hello Azure AD Join berichtvenster.
   
   <center>
   ![Azure AD join berichtvenster](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center>
4. Geef uw referenties aanmelden. Deze aanmeldingservaring bevat alle Hallo stappen die vereist toocomplete verificatie zijn. Als u deel van een federatieve tenant uitmaken, bieden de systeembeheerder u Hallo federation-ervaring bieden die wordt gehost door uw organisatie.
   <center>
   ![Geef aanmeldingsreferenties](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center>
5. Als uw organisatie heeft Azure multi-factor Authentication om lid te worden tooAzure AD geconfigureerd, bieden de tweede factor Hallo voordat u doorgaat.
6. Klik op **accepteren** op Hallo **toestaan dit apparaat toobe beheerd** scherm.
7. U ziet het Hallo-bericht 'uw apparaat is nu lid tooyour organisatie in Azure AD'.

## <a name="additional-information"></a>Aanvullende informatie
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)
* [Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren](active-directory-azureadjoin-passport.md)

