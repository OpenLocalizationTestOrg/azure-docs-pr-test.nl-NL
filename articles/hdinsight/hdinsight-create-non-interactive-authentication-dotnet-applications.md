---
title: aaaCreate niet-interactieve verificatie .NET HDInsight applciations - Azure | Microsoft Docs
description: Meer informatie over hoe toocreate niet-interactieve verificatie .NET HDInsight-toepassingen.
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
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>Niet-interactieve verificatie .NET HDInsight-toepassingen maken
U kunt uw .NET Azure HDInsight-toepassing onder de identiteit van de van toepassing is (niet-interactieve) of onder de identiteit Hallo van Hallo aangemelde gebruiker van Hallo-toepassing (interactief) uitvoeren. Zie voor een voorbeeld van de interactieve toepassing hello [tooAzure HDInsight verbinding](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). Dit artikel ziet u hoe toocreate niet-interactieve verificatie .NET application tooconnect tooAzure en HDInsight beheren.

U moet van een niet-interactieve .NET-toepassing:

* Uw Azure-abonnement tenant-ID (ook wel directory-ID). Zie [tenant-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* Hello Azure Active Directory-toepassingsclient-id. Zie [maken van een Azure Active Directory-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), en [een toepassings-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)
* Hello Azure Active Directory-toepassing geheime sleutel. Zie [verificatiesleutel Get-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)

## <a name="prerequisites"></a>Vereisten
* HDInsight-cluster. Zie [zelfstudie aan de slag](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).



## <a name="assign-azure-ad-application-toorole"></a>Azure AD-toepassing toorole toewijzen
U moet toewijzen Hallo toepassing tooa [rol](../active-directory/role-based-access-built-in-roles.md) toogrant deze machtigingen voor het uitvoeren van acties. U kunt Hallo bereik instellen op Hallo niveau van het Hallo-abonnement, resourcegroep of resource. Hallo machtigingen zijn overgenomen toolower niveaus van bereik (bijvoorbeeld toevoegen van die een toepassing toohello lezersrol voor een resourcegroep betekent dat het Hallo-resourcegroep kan lezen en alle resources die deze bevat). In deze zelfstudie wordt u Hallo bereik instellen op Hallo niveau van de resourcegroep. Zie voor meer informatie [rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](../active-directory/role-based-access-control-configure.md)

**tooadd hello eigenaar rol toohello Azure AD-toepassing**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **resourcegroep** in het linkerdeelvenster Hallo.
3. Klik op Hallo-resourcegroep met Hallo HDInsight-cluster waar u uw Hive-query verderop in deze zelfstudie wordt uitgevoerd. Als er te veel resourcegroepen, kunt u Hallo filter.
4. Klik op **toegangsbeheer (IAM)** in menu Hallo resource-groep.
5. Klik op **toevoegen** van Hallo **gebruikers** blade.
6. Ga als volgt Hallo instructie tooadd Hallo **eigenaar** rol toohello Azure AD-toepassing die u hebt gemaakt in de laatste procedure Hallo. Wanneer u het met succes voltooid, ziet u die worden vermeld in de blade van Hallo gebruikers met de rol van eigenaar Hallo Hallo-toepassing.

## <a name="develop-hdinsight-client-application"></a>HDInsight-client-toepassing ontwikkelen

1. Maak een C#-consoletoepassing.
2. Hallo volgende Nuget-pakketten toevoegen:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Hallo codevoorbeeld volgende gebruiken:

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
                private static string secretKey = "<Enter hello Application Secret Key>";
        
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
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
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
