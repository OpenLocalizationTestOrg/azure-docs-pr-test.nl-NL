---
title: aaaSSL certificaten binding met behulp van PowerShell
description: Meer informatie over hoe toobind SSL-certificaten tooyour web-app met behulp van PowerShell.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>Azure App Service SSL-Certificaatbinding met behulp van PowerShell
Hallo-versie van Microsoft Azure PowerShell versie 1.1.0 een nieuwe cmdlet is toegevoegd, die krijgt Hallo gebruiker Hallo mogelijkheid toobind bestaande of nieuwe SSL-certificaten tooan bestaande Web-App.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn over het gebruik van Azure Resource Manager gebaseerde Azure PowerShell-cmdlets toomanage de controle van uw Web-Apps [PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>Uploaden en een nieuw certificaat voor SSL-Binding
Scenario: Hallo gebruiker graag toobind een tooone SSL-certificaat van de web-apps.

Weten Hallo Resourcegroepnaam Hallo web-app, web-appnaam Hallo, Hallo pfx-bestand certificaatpad op Hallo machine gebruiker met wachtwoord voor certificaat Hallo Hallo en Hallo aangepaste hostnaam, kunnen we de volgende PowerShell-opdracht toocreate hello gebruiken die SSL-binding:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Houd er rekening mee dat voordat u een SSL-binding tooa web-app toevoegt, moet er een hostnaam (aangepast domein) al is geconfigureerd. Als Hallo hostnaam is niet geconfigureerd, wordt u een foutmelding krijgt 'hostnaam' bestaat niet bij het uitvoeren van nieuw AzureRmWebAppSSLBinding. U kunt een hostnaam toevoegen rechtstreeks vanuit het Hallo-portal of met Azure PowerShell. Hallo mag volgende PowerShell-codefragment tooconfigure Hallo hostnaam voordat nieuw AzureRmWebAppSSLBinding wordt uitgevoerd.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

Het is belangrijk toounderstand die de cmdlet Set-AzureRmWebApp Hallo Hallo hostnamen voor Hallo web-app overschreven. Daarom is het Hallo hierboven PowerShell-codefragment toohello bestaande lijst van hostnamen Hallo voor Hallo web-app toevoegen.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>Uploaden en voor het binden van een bestaand SSL-certificaat
Scenario: Hallo gebruiker graag toobind een eerder geüploade tooone van SSL-certificaat van de web-apps.

We kunnen ophalen Hallo lijst met certificaten al geüploade tooa specifieke resourcegroep met behulp van de volgende opdracht Hallo

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Houd er rekening mee dat Hallo certificaten zijn lokale tooa specifieke locatie en groep, hello gebruiker toore-upload Hallo certificaat nodig als Hallo geconfigureerd web-app in een andere locatie en resourcegroep waarvan andere die die Hallo certificaat nodig 

Weten Hallo Resourcegroepnaam Hallo-web-app met web-appnaam Hallo Hallo certificaatvingerafdruk en Hallo aangepaste hostnaam, kunnen we Hallo volgende PowerShell-opdracht toocreate die SSL-binding gebruiken:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>Verwijderen van een bestaand SSL-binding
Scenario: Hallo gebruiker graag toodelete een bestaand SSL-binding.

Weten Hallo Resourcegroepnaam Hallo-web-app met web-appnaam Hallo en Hallo aangepaste hostnaam, kunnen we Hallo volgende PowerShell-opdracht tooremove die SSL-binding gebruiken:

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Denk eraan dat als Hallo verwijderd SSL-binding is Hallo laatste binding met behulp van dat certificaat op die locatie door Hallo standaardcertificaat worden verwijderd, als de gebruiker Hallo tookeep Hallo certificaat wilt hij Hallo DeleteCertificate optie tookeep Hallo certificaat kan gebruiken

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>Verwijzingen
* [PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md)
* [Inleiding tooApp Service-omgeving](app-service-app-service-environment-intro.md)
* [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md)

