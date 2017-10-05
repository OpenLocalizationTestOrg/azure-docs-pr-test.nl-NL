---
title: Instellen van een Windows 10-apparaat met Azure AD via instellingen | Microsoft Docs
description: Legt uit hoe gebruikers kunnen toevoegen aan Azure AD via het menu instellingen.
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
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Instellen van een Windows 10-apparaat met Azure AD via instellingen
Als u al Windows 7 of Windows 8 gebruikt en uw computer of apparaat is bijgewerkt naar Windows 10, kunt u koppelen aan Azure Active Directory (Azure AD) via het menu instellingen.

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a>Koppelen aan Azure AD in het menu instellingen
1. Van de **Start** menu, klikt u op de **instellingen** charm.
2. Van **instellingen**, selecteer **System**->**over**->**Azure AD Join**.
   
   <center>
   ![Deelnemen aan Azure AD in het menu instellingen](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Klik op **doorgaan** in het venster Azure AD Join-bericht.
   
   <center>
   ![Azure AD join berichtvenster](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center>
4. Geef uw referenties aanmelden. Deze aanmeldingservaring bevat de stappen die nodig voor de volledige verificatie zijn. Als u deel van een federatieve tenant uitmaken, bieden de systeembeheerder u met de federation-ervaring die wordt gehost door uw organisatie.
   <center>
   ![Geef aanmeldingsreferenties](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center>
5. Als uw organisatie is Azure multi-factor Authentication om lid te worden naar Azure AD geconfigureerd, geeft u de tweede factor voordat u doorgaat.
6. Klik op **accepteren** op de **toestaan dat dit apparaat worden beheerd** scherm.
7. U ziet het bericht 'uw apparaat is nu lid van uw organisatie in Azure AD'.

## <a name="additional-information"></a>Aanvullende informatie
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md) (Apparaten die lid zijn van een domein verbinden met Azure AD voor Windows 10-ervaringen)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)
* [Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren](active-directory-azureadjoin-passport.md)

