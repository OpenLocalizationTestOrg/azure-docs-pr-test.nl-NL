---
title: aaaGet gegevens met Azure AD rapportage-API met certificaten Hallo | Microsoft Docs
description: Legt uit hoe toouse hello Azure AD rapportage-API met referenties tooget certificaatgegevens van Directory's zonder tussenkomst van de gebruiker.
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>Gegevens hello Azure AD-rapportage-API gebruiken met certificaten ophalen
Dit artikel wordt beschreven hoe toouse hello Azure AD rapportage-API met referenties tooget certificaatgegevens van Directory's zonder tussenkomst van de gebruiker. 

## <a name="use-hello-azure-ad-reporting-api"></a>Gebruik hello Azure AD rapportage-API 
Azure AD rapportage-API is vereist dat Hallo stappen te voltooien:
 *  Vereiste onderdelen installeren
 *  Hallo-certificaat in uw app instellen
 *  Een toegangstoken opvragen
 *  Hallo access token toocall Hallo Graph API gebruiken

Zie [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Rapportage-API-module gebruiken) voor meer informatie over broncode. 

### <a name="install-prerequisites"></a>Vereiste onderdelen installeren
U moet toohave Azure AD PowerShell V2 en AzureADUtils-module geïnstalleerd.

1. Download en installeer Azure AD Powershell V2, Hallo instructies te volgen op [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).
2. Download hello Azure AD Utils module op basis van [AzureAD/azure-Active Directory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1). 
  Deze module biedt verschillende cmdlets, waaronder:
   * Hallo meest recente versie van Nuget met ADAL
   * Toegangstokens van gebruiker, toepassingssleutels en certificaten met behulp van ADAL
   * Afhandeling van pagina's met zoekresultaten door Graph API

**tooinstall hello Utils van Azure AD-module:**

1. Maken van een directory toosave Hallo hulpprogramma's-module (bijvoorbeeld c:\azureAD) en Hallo module vanuit GitHub downloaden.
2. Open een PowerShell-sessie en gaat u toohello directory die u zojuist hebt gemaakt. 
3. Hallo-module importeren en installeer het in Hallo PowerShell-module pad met de cmdlet Install-AzureADUtilsModule Hallo. 

Hallo-sessie ziet vergelijkbare toothis scherm:

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>Hallo-certificaat in uw app instellen
1. Als u een app al hebt, moet u de Object-ID ophalen van hello Azure-Portal. 

  ![Azure Portal](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. Open een PowerShell-sessie en tooAzure AD verbinding maken met de cmdlet Hallo Connect-AzureAD.

  ![Azure Portal](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. Hallo nieuw AzureADApplicationCertificateCredential cmdlet van AzureADUtils tooadd een certificaat referentie tooit gebruiken. 

>[!Note]
>U moet tooprovide Hallo toepassing Object-ID die u eerder hebt vastgelegd, evenals Hallo certificaatobject (ophalen deze met Hallo Cert: station).
>


  ![Azure Portal](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>Een toegangstoken opvragen

tooget een toegangstoken Hallo Get AzureADGraphAPIAccessTokenFromCert cmdlet van AzureADUtils gebruiken. 

>[!NOTE]
>U moet toouse Hallo toepassings-ID in plaats van de Object-ID die u hebt gebruikt in de laatste sectie Hallo Hallo.
>

 ![Azure Portal](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>Hallo access token toocall Hallo Graph API gebruiken

U kunt nu Hallo script maken. Hieronder vindt u een voorbeeld met de cmdlet Invoke-AzureADGraphAPIQuery Hallo van Hallo AzureADUtils. Deze cmdlet verwerkt met meerdere pagina's met zoekresultaten en stuurt vervolgens deze resultaten toohello PowerShell-pijplijn. 

 ![Azure Portal](./media/active-directory-report-api-with-certificates/script-completed.png)

U bent nu klaar tooexport tooa CSV en slaat tooa SIEM-systeem. U kunt ook inpakken uw script in een geplande taak tooget Azure AD-gegevens van uw tenant periodiek zonder toostore toepassing sleutels in de broncode Hallo. 

## <a name="next-steps"></a>Volgende stappen
[Hallo grondbeginselen van Azure identity management](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



