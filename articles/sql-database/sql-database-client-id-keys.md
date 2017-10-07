---
title: aaaGet-waarden voor verificatie in app - Azure SQL Database | Microsoft Docs
description: Een service-principal maken voor toegang tot SQL-Database vanuit code.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
tags: 
ms.assetid: b43e43bb-6660-49e6-b069-abde97eb5770
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: b57dc075ec9e679da9f2f5fa53e02312539cdf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-required-values-for-authenticating-an-application-tooaccess-sql-database-from-code"></a>Hallo vereiste waarden voor het verifiëren van een toepassing tooaccess SQL-Database vanuit code ophalen
toocreate en SQL Database beheren vanuit code die u moet uw app registreren in het Hallo-domein Azure Active Directory (AAD) in Hallo abonnement waar uw Azure-resources zijn gemaakt.

## <a name="create-a-service-principal-tooaccess-resources-from-an-application"></a>Een service-principal tooaccess resources van een toepassing maken
Moet u toohave Hallo nieuwste [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) geïnstalleerd en wordt uitgevoerd. Zie voor gedetailleerde informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs).

Hallo maakt volgende PowerShell-script Hallo Active Directory (AD) en -Hallo service principal dat we tooauthenticate onze C#-app moeten. Hallo script levert waarden die we nodig voor voorgaande C# Hallo steekproef. Zie voor gedetailleerde informatie [gebruik Azure PowerShell toocreate een service-principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret




## <a name="see-also"></a>Zie ook
* [Een SQL-database maken met C#](sql-database-get-started-csharp.md)
* [TooSQL Database met behulp van Azure Active Directory-verificatie verbinding te maken](sql-database-aad-authentication.md)

