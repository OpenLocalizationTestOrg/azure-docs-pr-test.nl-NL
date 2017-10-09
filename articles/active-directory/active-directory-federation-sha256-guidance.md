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
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a>Handtekening hash-algoritme voor Office 365 vertrouwensrelatie van relying party wijzigen
## <a name="overview"></a>Overzicht
Active Directory Federation Services (AD FS), ondertekent de Azure Active Directory-tooensure voor tokens tooMicrosoft met kan worden geknoeid. Deze handtekening kan zijn gebaseerd op SHA1 of SHA256. Azure Active Directory biedt nu ondersteuning voor tokens die zijn ondertekend met een algoritme SHA256 en het is raadzaam Hallo token-ondertekening algoritme tooSHA256 voor Hallo hoogste niveau van beveiliging instellen. In dit artikel worden Hallo stappen beschreven die nodig zijn tooset Hallo token-ondertekening algoritme toohello veiliger SHA256-niveau.

>[!NOTE]
>Microsoft raadt informatie over het gebruik van SHA256 als Hallo-algoritme voor het ondertekenen van tokens als het is veiliger dan SHA1 maar SHA1 nog steeds ondersteund.

## <a name="change-hello-token-signing-algorithm"></a>Hallo-algoritme voor token-ondertekening wijzigen
Nadat u de handtekeningalgoritme Hallo met een van twee processen Hallo onderstaande hebt ingesteld, ondertekent AD FS-tokens Hallo voor Office 365 relying party trust met SHA256. U hoeft niet toomake extra configuratiewijzigingen en deze wijziging heeft geen invloed op uw mogelijkheid tooaccess Office 365 of andere Azure AD-toepassingen.

### <a name="ad-fs-management-console"></a>AD FS-beheerconsole
1. Open Hallo AD FS-beheerconsole op Hallo primaire AD FS-server.
2. Vouw Hallo AD FS-knooppunt en klik op **Relying Party-vertrouwensrelaties**.
3. Met de rechtermuisknop op uw Office 365/Azure-vertrouwensrelatie voor relying party en selecteer **eigenschappen**.
4. Selecteer Hallo **Geavanceerd** tabblad en selecteer Hallo veilige hash-algoritme SHA256.
5. Klik op **OK**.

![SHA256 ondertekeningsalgoritme--MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a>AD FS-PowerShell-cmdlets
1. Open PowerShell onder administrator-bevoegdheden op de AD FS-server.
2. Set Hallo veilige hash-algoritme met behulp van Hallo **Set-AdfsRelyingPartyTrust** cmdlet.
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a>Lees ook
* [Herstel van Office 365-vertrouwensrelatie met Azure AD Connect](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

