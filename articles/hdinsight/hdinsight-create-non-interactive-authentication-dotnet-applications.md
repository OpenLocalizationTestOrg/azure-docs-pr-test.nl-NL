---
title: Maken van niet-interactieve verificatie .NET HDInsight applciations - Azure | Microsoft Docs
description: Informatie over het maken van niet-interactieve verificatie .NET HDInsight-toepassingen.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7821a9e60e60ff01cff06db2a6f216a260c1c41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>Niet-interactieve verificatie .NET HDInsight-toepassingen maken
U kunt uw .NET Azure HDInsight-toepassing onder de identiteit van de van toepassing is (niet-interactieve) of onder de identiteit van de aangemelde gebruiker van de toepassing (interactief) uitvoeren. Zie voor een voorbeeld van de interactieve toepassing [verbinding maken met Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). In dit artikel laat zien hoe niet-interactieve verificatie .NET-toepassing verbinding maken met Azure en HDInsight beheren maken.

U moet van een niet-interactieve .NET-toepassing:

* Uw Azure-abonnement tenant-ID (ook wel directory-ID). Zie [tenant-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* De Azure Active Directory-client-id op. Zie [maken van een Azure Active Directory-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), en [een toepassings-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)
* De Azure Active Directory-toepassing geheime sleutel. Zie [verificatiesleutel Get-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)

## <a name="prerequisites"></a>Vereisten
* HDInsight-cluster. Zie [zelfstudie aan de slag](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).



## <a name="assign-azure-ad-application-to-role"></a>Azure AD-toepassing aan rol toewijzen
U moet de toepassing toewijzen aan een [rol](../active-directory/role-based-access-built-in-roles.md) deze om machtigingen te verlenen voor het uitvoeren van acties. U kunt het bereik instellen op het niveau van het abonnement, resourcegroep of resource. De machtigingen worden overgenomen op lagere niveaus van de scope (bijvoorbeeld, het toevoegen van een toepassing met de rol Lezer voor een resourcegroep betekent dat de resourcegroep kan worden gelezen en alle resources die deze bevat). In deze zelfstudie wordt u het bereik instellen op het niveau van de resourcegroep. Zie voor meer informatie [roltoewijzingen gebruiken voor het beheren van toegang tot de resources van uw Azure-abonnement](../active-directory/role-based-access-control-configure.md)

**De rol van eigenaar toevoegen aan de Azure AD-toepassing**

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Klik op **resourcegroep** in het linkerdeelvenster.
3. Klik op de resourcegroep waarin het HDInsight-cluster waar u uw Hive-query verderop in deze zelfstudie wordt uitgevoerd. Als er te veel resourcegroepen, kunt u het filter.
4. Klik op **toegangsbeheer (IAM)** in het menu van de groep resource.
5. Klik op **toevoegen** van de **gebruikers** blade.
6. Volg de aanwijzingen om toe te voegen de **eigenaar** role in de Azure AD-toepassing die u hebt gemaakt in de laatste procedure. Wanneer u het met succes voltooid, ziet u de toepassing die worden vermeld in de blade gebruikers met de rol van eigenaar.

## <a name="develop-hdinsight-client-application"></a>HDInsight-client-toepassing ontwikkelen

1. Maak een C#-consoletoepassing.
2. De volgende Nuget-pakketten toevoegen:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Gebruik het volgende codevoorbeeld:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter the Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter to continue");
                    Console.ReadLine();
                }

                /// Get the access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a>Volgende stappen
* [Azure Active Directory-toepassing en service-principal maken met portal maken](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Service-principal met Azure Resource Manager verifiëren](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Op rollen gebaseerde toegangsbeheer van Azure](../active-directory/role-based-access-control-configure.md)
