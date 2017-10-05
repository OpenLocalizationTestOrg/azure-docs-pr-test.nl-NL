---
title: SSL-certificaten binding met behulp van PowerShell
description: Informatie over het SSL-certificaten binden aan uw web-app met behulp van PowerShell.
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
ms.openlocfilehash: a1fcc618fb0c68778e39cc227368a60b008f9401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>Azure App Service SSL-Certificaatbinding met behulp van PowerShell
Met de release van Microsoft Azure PowerShell versie 1.1.0 is een nieuwe cmdlet toegevoegd die krijgt de gebruiker de mogelijkheid bestaande of nieuwe SSL-certificaten te binden aan een bestaande Web-App.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Voor meer informatie over het gebruik van Azure PowerShell-cmdlets voor het beheren van de controle van uw Web-Apps op basis van Azure Resource Manager [PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>Uploaden en een nieuw certificaat voor SSL-Binding
Scenario: De gebruiker wil een SSL-certificaat binden aan een van de web-apps.

Weet de naam van de resourcegroep met de web-app, de naam van de web-app, het .pfx-bestandspad voor het certificaat op de machine van de gebruiker, het wachtwoord voor het certificaat en de aangepaste hostnaam, kunnen we de volgende PowerShell-opdracht gebruiken die SSL-binding maken:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Houd er rekening mee dat voordat u een SSL-binding aan een web-app toevoegt, moet er een hostnaam (aangepast domein) al is geconfigureerd. Als de hostnaam is niet geconfigureerd, wordt u een foutmelding krijgt 'hostnaam' bestaat niet bij het uitvoeren van nieuw AzureRmWebAppSSLBinding. U kunt een hostnaam toevoegen rechtstreeks vanuit de portal of met Azure PowerShell. Het volgende PowerShell-fragment kan zijn voor het configureren van de hostnaam voordat nieuw AzureRmWebAppSSLBinding wordt uitgevoerd.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

Het is belangrijk te weten dat de cmdlet Set-AzureRmWebApp de hostnamen voor de web-app overschrijft. Daarom wordt het bovenstaande fragment van PowerShell toevoegen aan de bestaande lijst van de hostnamen voor de web-app.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>Uploaden en voor het binden van een bestaand SSL-certificaat
Scenario: De gebruiker wil een eerder geüploade SSL-certificaat binden aan een van de web-apps.

We kunnen de lijst met certificaten al hebt geüpload naar een specifieke resourcegroep met de volgende opdracht ophalen

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Houd er rekening mee dat de certificaten die lokaal op een specifieke locatie en de resourcegroep, wordt de gebruiker moet het certificaat opnieuw te uploaden als de geconfigureerde web-app in een andere locatie en resourcegroep waarvan andere die die van het benodigde certificaat 

Weet de naam van de resourcegroep met de web-app, de naam van de web-app, vingerafdruk van het certificaat en de aangepaste hostnaam, kunnen we de volgende PowerShell-opdracht gebruiken die SSL-binding maken:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>Verwijderen van een bestaand SSL-binding
Scenario: De gebruiker wilt verwijderen van een bestaand SSL-binding.

Weet de naam van de resourcegroep met de web-app, de naam van de web-app en de aangepaste hostnaam, kunnen we de volgende PowerShell-opdracht te verwijderen die SSL-binding gebruiken:

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Houd er rekening mee dat als de verwijderde SSL-binding de laatste binding met behulp van dat certificaat in dat de locatie, standaard ingesteld op het certificaat wordt verwijderd is, als de gebruiker behouden van het certificaat dat hij de optie DeleteCertificate kunt gebruiken wilt om het certificaat

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>Verwijzingen
* [PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md)
* [Inleiding tot de App Service-omgeving](app-service-app-service-environment-intro.md)
* [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md)

