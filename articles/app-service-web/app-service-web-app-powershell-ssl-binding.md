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
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="bd248-103">Azure App Service SSL-Certificaatbinding met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd248-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="bd248-104">Hallo-versie van Microsoft Azure PowerShell versie 1.1.0 een nieuwe cmdlet is toegevoegd, die krijgt Hallo gebruiker Hallo mogelijkheid toobind bestaande of nieuwe SSL-certificaten tooan bestaande Web-App.</span><span class="sxs-lookup"><span data-stu-id="bd248-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give hello user hello ability toobind existing or new SSL certificates tooan existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="bd248-105">toolearn over het gebruik van Azure Resource Manager gebaseerde Azure PowerShell-cmdlets toomanage de controle van uw Web-Apps [PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="bd248-105">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="bd248-106">Uploaden en een nieuw certificaat voor SSL-Binding</span><span class="sxs-lookup"><span data-stu-id="bd248-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="bd248-107">Scenario: Hallo gebruiker graag toobind een tooone SSL-certificaat van de web-apps.</span><span class="sxs-lookup"><span data-stu-id="bd248-107">Scenario: hello user would like toobind an SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="bd248-108">Weten Hallo Resourcegroepnaam Hallo web-app, web-appnaam Hallo, Hallo pfx-bestand certificaatpad op Hallo machine gebruiker met wachtwoord voor certificaat Hallo Hallo en Hallo aangepaste hostnaam, kunnen we de volgende PowerShell-opdracht toocreate hello gebruiken die SSL-binding:</span><span class="sxs-lookup"><span data-stu-id="bd248-108">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate .pfx file path on hello user machine, hello password for hello certificate, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="bd248-109">Houd er rekening mee dat voordat u een SSL-binding tooa web-app toevoegt, moet er een hostnaam (aangepast domein) al is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="bd248-109">Note that before adding a SSL binding tooa web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="bd248-110">Als Hallo hostnaam is niet geconfigureerd, wordt u een foutmelding krijgt 'hostnaam' bestaat niet bij het uitvoeren van nieuw AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="bd248-110">If hello host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="bd248-111">U kunt een hostnaam toevoegen rechtstreeks vanuit het Hallo-portal of met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd248-111">You can add a hostname directly from hello portal or using Azure PowerShell.</span></span> <span data-ttu-id="bd248-112">Hallo mag volgende PowerShell-codefragment tooconfigure Hallo hostnaam voordat nieuw AzureRmWebAppSSLBinding wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bd248-112">hello following PowerShell snippet can be tooconfigure hello hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="bd248-113">Het is belangrijk toounderstand die de cmdlet Set-AzureRmWebApp Hallo Hallo hostnamen voor Hallo web-app overschreven.</span><span class="sxs-lookup"><span data-stu-id="bd248-113">It is important toounderstand that hello Set-AzureRmWebApp cmdlet overwrites hello hostnames for hello web app.</span></span> <span data-ttu-id="bd248-114">Daarom is het Hallo hierboven PowerShell-codefragment toohello bestaande lijst van hostnamen Hallo voor Hallo web-app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bd248-114">Hence hello above PowerShell snippet is appending toohello existing list of hello host names for hello web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="bd248-115">Uploaden en voor het binden van een bestaand SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="bd248-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="bd248-116">Scenario: Hallo gebruiker graag toobind een eerder geüploade tooone van SSL-certificaat van de web-apps.</span><span class="sxs-lookup"><span data-stu-id="bd248-116">Scenario: hello user would like toobind a previously uploaded SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="bd248-117">We kunnen ophalen Hallo lijst met certificaten al geüploade tooa specifieke resourcegroep met behulp van de volgende opdracht Hallo</span><span class="sxs-lookup"><span data-stu-id="bd248-117">We can get hello list of certificates already uploaded tooa specific resource group by using hello following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="bd248-118">Houd er rekening mee dat Hallo certificaten zijn lokale tooa specifieke locatie en groep, hello gebruiker toore-upload Hallo certificaat nodig als Hallo geconfigureerd web-app in een andere locatie en resourcegroep waarvan andere die die Hallo certificaat nodig</span><span class="sxs-lookup"><span data-stu-id="bd248-118">Note that hello certificates are local tooa specific location and resource group, hello user need toore-upload hello certificate if hello configured web app is in a different location and resource group other that that of hello needed certificate</span></span> 

<span data-ttu-id="bd248-119">Weten Hallo Resourcegroepnaam Hallo-web-app met web-appnaam Hallo Hallo certificaatvingerafdruk en Hallo aangepaste hostnaam, kunnen we Hallo volgende PowerShell-opdracht toocreate die SSL-binding gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bd248-119">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate thumbprint, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="bd248-120">Verwijderen van een bestaand SSL-binding</span><span class="sxs-lookup"><span data-stu-id="bd248-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="bd248-121">Scenario: Hallo gebruiker graag toodelete een bestaand SSL-binding.</span><span class="sxs-lookup"><span data-stu-id="bd248-121">Scenario: hello user would like toodelete an existing SSL binding.</span></span>

<span data-ttu-id="bd248-122">Weten Hallo Resourcegroepnaam Hallo-web-app met web-appnaam Hallo en Hallo aangepaste hostnaam, kunnen we Hallo volgende PowerShell-opdracht tooremove die SSL-binding gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bd248-122">Knowing hello resource group name that contains hello web app, hello web app name, and hello custom hostname, we can use hello following PowerShell command tooremove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="bd248-123">Denk eraan dat als Hallo verwijderd SSL-binding is Hallo laatste binding met behulp van dat certificaat op die locatie door Hallo standaardcertificaat worden verwijderd, als de gebruiker Hallo tookeep Hallo certificaat wilt hij Hallo DeleteCertificate optie tookeep Hallo certificaat kan gebruiken</span><span class="sxs-lookup"><span data-stu-id="bd248-123">Note that if hello removed SSL binding was hello last binding using that certificate in that location, by default hello certificate will be deleted, if hello user want tookeep hello certificate he can use hello DeleteCertificate option tookeep hello certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="bd248-124">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="bd248-124">References</span></span>
* [<span data-ttu-id="bd248-125">PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bd248-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="bd248-126">Inleiding tooApp Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="bd248-126">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="bd248-127">Azure PowerShell gebruiken met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bd248-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

