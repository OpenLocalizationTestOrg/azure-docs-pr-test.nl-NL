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
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="646d6-103">Azure App Service SSL-Certificaatbinding met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="646d6-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="646d6-104">Met de release van Microsoft Azure PowerShell versie 1.1.0 is een nieuwe cmdlet toegevoegd die krijgt de gebruiker de mogelijkheid bestaande of nieuwe SSL-certificaten te binden aan een bestaande Web-App.</span><span class="sxs-lookup"><span data-stu-id="646d6-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give the user the ability to bind existing or new SSL certificates to an existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="646d6-105">Voor meer informatie over het gebruik van Azure PowerShell-cmdlets voor het beheren van de controle van uw Web-Apps op basis van Azure Resource Manager [PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="646d6-105">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="646d6-106">Uploaden en een nieuw certificaat voor SSL-Binding</span><span class="sxs-lookup"><span data-stu-id="646d6-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="646d6-107">Scenario: De gebruiker wil een SSL-certificaat binden aan een van de web-apps.</span><span class="sxs-lookup"><span data-stu-id="646d6-107">Scenario: The user would like to bind an SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="646d6-108">Weet de naam van de resourcegroep met de web-app, de naam van de web-app, het .pfx-bestandspad voor het certificaat op de machine van de gebruiker, het wachtwoord voor het certificaat en de aangepaste hostnaam, kunnen we de volgende PowerShell-opdracht gebruiken die SSL-binding maken:</span><span class="sxs-lookup"><span data-stu-id="646d6-108">Knowing the resource group name that contains the web app, the web app name, the certificate .pfx file path on the user machine, the password for the certificate, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="646d6-109">Houd er rekening mee dat voordat u een SSL-binding aan een web-app toevoegt, moet er een hostnaam (aangepast domein) al is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="646d6-109">Note that before adding a SSL binding to a web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="646d6-110">Als de hostnaam is niet geconfigureerd, wordt u een foutmelding krijgt 'hostnaam' bestaat niet bij het uitvoeren van nieuw AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="646d6-110">If the host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="646d6-111">U kunt een hostnaam toevoegen rechtstreeks vanuit de portal of met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="646d6-111">You can add a hostname directly from the portal or using Azure PowerShell.</span></span> <span data-ttu-id="646d6-112">Het volgende PowerShell-fragment kan zijn voor het configureren van de hostnaam voordat nieuw AzureRmWebAppSSLBinding wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="646d6-112">The following PowerShell snippet can be to configure the hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="646d6-113">Het is belangrijk te weten dat de cmdlet Set-AzureRmWebApp de hostnamen voor de web-app overschrijft.</span><span class="sxs-lookup"><span data-stu-id="646d6-113">It is important to understand that the Set-AzureRmWebApp cmdlet overwrites the hostnames for the web app.</span></span> <span data-ttu-id="646d6-114">Daarom wordt het bovenstaande fragment van PowerShell toevoegen aan de bestaande lijst van de hostnamen voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="646d6-114">Hence the above PowerShell snippet is appending to the existing list of the host names for the web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="646d6-115">Uploaden en voor het binden van een bestaand SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="646d6-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="646d6-116">Scenario: De gebruiker wil een eerder geüploade SSL-certificaat binden aan een van de web-apps.</span><span class="sxs-lookup"><span data-stu-id="646d6-116">Scenario: The user would like to bind a previously uploaded SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="646d6-117">We kunnen de lijst met certificaten al hebt geüpload naar een specifieke resourcegroep met de volgende opdracht ophalen</span><span class="sxs-lookup"><span data-stu-id="646d6-117">We can get the list of certificates already uploaded to a specific resource group by using the following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="646d6-118">Houd er rekening mee dat de certificaten die lokaal op een specifieke locatie en de resourcegroep, wordt de gebruiker moet het certificaat opnieuw te uploaden als de geconfigureerde web-app in een andere locatie en resourcegroep waarvan andere die die van het benodigde certificaat</span><span class="sxs-lookup"><span data-stu-id="646d6-118">Note that the certificates are local to a specific location and resource group, the user need to re-upload the certificate if the configured web app is in a different location and resource group other that that of the needed certificate</span></span> 

<span data-ttu-id="646d6-119">Weet de naam van de resourcegroep met de web-app, de naam van de web-app, vingerafdruk van het certificaat en de aangepaste hostnaam, kunnen we de volgende PowerShell-opdracht gebruiken die SSL-binding maken:</span><span class="sxs-lookup"><span data-stu-id="646d6-119">Knowing the resource group name that contains the web app, the web app name, the certificate thumbprint, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="646d6-120">Verwijderen van een bestaand SSL-binding</span><span class="sxs-lookup"><span data-stu-id="646d6-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="646d6-121">Scenario: De gebruiker wilt verwijderen van een bestaand SSL-binding.</span><span class="sxs-lookup"><span data-stu-id="646d6-121">Scenario: The user would like to delete an existing SSL binding.</span></span>

<span data-ttu-id="646d6-122">Weet de naam van de resourcegroep met de web-app, de naam van de web-app en de aangepaste hostnaam, kunnen we de volgende PowerShell-opdracht te verwijderen die SSL-binding gebruiken:</span><span class="sxs-lookup"><span data-stu-id="646d6-122">Knowing the resource group name that contains the web app, the web app name, and the custom hostname, we can use the following PowerShell command to remove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="646d6-123">Houd er rekening mee dat als de verwijderde SSL-binding de laatste binding met behulp van dat certificaat in dat de locatie, standaard ingesteld op het certificaat wordt verwijderd is, als de gebruiker behouden van het certificaat dat hij de optie DeleteCertificate kunt gebruiken wilt om het certificaat</span><span class="sxs-lookup"><span data-stu-id="646d6-123">Note that if the removed SSL binding was the last binding using that certificate in that location, by default the certificate will be deleted, if the user want to keep the certificate he can use the DeleteCertificate option to keep the certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="646d6-124">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="646d6-124">References</span></span>
* [<span data-ttu-id="646d6-125">PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="646d6-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="646d6-126">Inleiding tot de App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="646d6-126">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="646d6-127">Azure PowerShell gebruiken met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="646d6-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

