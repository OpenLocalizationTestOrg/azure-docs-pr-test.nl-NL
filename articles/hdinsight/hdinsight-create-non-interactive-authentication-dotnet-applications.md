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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="82439-103">Niet-interactieve verificatie .NET HDInsight-toepassingen maken</span><span class="sxs-lookup"><span data-stu-id="82439-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="82439-104">U kunt uw .NET Azure HDInsight-toepassing onder de identiteit van de van toepassing is (niet-interactieve) of onder de identiteit van de aangemelde gebruiker van de toepassing (interactief) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="82439-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under the identity of the signed-in user of the application (interactive).</span></span> <span data-ttu-id="82439-105">Zie voor een voorbeeld van de interactieve toepassing [verbinding maken met Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="82439-105">For a sample of the interactive application, see [Connect to Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="82439-106">In dit artikel laat zien hoe niet-interactieve verificatie .NET-toepassing verbinding maken met Azure en HDInsight beheren maken.</span><span class="sxs-lookup"><span data-stu-id="82439-106">This article shows you how to create non-interactive authentication .NET application to connect to Azure and manage HDInsight.</span></span>

<span data-ttu-id="82439-107">U moet van een niet-interactieve .NET-toepassing:</span><span class="sxs-lookup"><span data-stu-id="82439-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="82439-108">Uw Azure-abonnement tenant-ID (ook wel directory-ID).</span><span class="sxs-lookup"><span data-stu-id="82439-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="82439-109">Zie [tenant-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="82439-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="82439-110">De Azure Active Directory-client-id op.</span><span class="sxs-lookup"><span data-stu-id="82439-110">The Azure Active Directory application client ID.</span></span> <span data-ttu-id="82439-111">Zie [maken van een Azure Active Directory-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), en [een toepassings-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="82439-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="82439-112">De Azure Active Directory-toepassing geheime sleutel.</span><span class="sxs-lookup"><span data-stu-id="82439-112">The Azure Active Directory application secret key.</span></span> <span data-ttu-id="82439-113">Zie [verificatiesleutel Get-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="82439-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82439-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="82439-114">Prerequisites</span></span>
* <span data-ttu-id="82439-115">HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="82439-115">HDInsight cluster.</span></span> <span data-ttu-id="82439-116">Zie [zelfstudie aan de slag](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="82439-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-to-role"></a><span data-ttu-id="82439-117">Azure AD-toepassing aan rol toewijzen</span><span class="sxs-lookup"><span data-stu-id="82439-117">Assign Azure AD application to role</span></span>
<span data-ttu-id="82439-118">U moet de toepassing toewijzen aan een [rol](../active-directory/role-based-access-built-in-roles.md) deze om machtigingen te verlenen voor het uitvoeren van acties.</span><span class="sxs-lookup"><span data-stu-id="82439-118">You must assign the application to a [role](../active-directory/role-based-access-built-in-roles.md) to grant it permissions for performing actions.</span></span> <span data-ttu-id="82439-119">U kunt het bereik instellen op het niveau van het abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="82439-119">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="82439-120">De machtigingen worden overgenomen op lagere niveaus van de scope (bijvoorbeeld, het toevoegen van een toepassing met de rol Lezer voor een resourcegroep betekent dat de resourcegroep kan worden gelezen en alle resources die deze bevat).</span><span class="sxs-lookup"><span data-stu-id="82439-120">The permissions are inherited to lower levels of scope (for example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains).</span></span> <span data-ttu-id="82439-121">In deze zelfstudie wordt u het bereik instellen op het niveau van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="82439-121">In this tutorial, you will set the scope at the resource group level.</span></span> <span data-ttu-id="82439-122">Zie voor meer informatie [roltoewijzingen gebruiken voor het beheren van toegang tot de resources van uw Azure-abonnement](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="82439-122">For more information, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="82439-123">**De rol van eigenaar toevoegen aan de Azure AD-toepassing**</span><span class="sxs-lookup"><span data-stu-id="82439-123">**To add the Owner role to the Azure AD application**</span></span>

1. <span data-ttu-id="82439-124">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="82439-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="82439-125">Klik op **resourcegroep** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="82439-125">Click **Resource Group** from the left pane.</span></span>
3. <span data-ttu-id="82439-126">Klik op de resourcegroep waarin het HDInsight-cluster waar u uw Hive-query verderop in deze zelfstudie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="82439-126">Click the resource group that contains the HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="82439-127">Als er te veel resourcegroepen, kunt u het filter.</span><span class="sxs-lookup"><span data-stu-id="82439-127">If there are too many resource groups, you can use the filter.</span></span>
4. <span data-ttu-id="82439-128">Klik op **toegangsbeheer (IAM)** in het menu van de groep resource.</span><span class="sxs-lookup"><span data-stu-id="82439-128">Click **Access control (IAM)** from the resource group menu.</span></span>
5. <span data-ttu-id="82439-129">Klik op **toevoegen** van de **gebruikers** blade.</span><span class="sxs-lookup"><span data-stu-id="82439-129">Click **Add** from the **Users** blade.</span></span>
6. <span data-ttu-id="82439-130">Volg de aanwijzingen om toe te voegen de **eigenaar** role in de Azure AD-toepassing die u hebt gemaakt in de laatste procedure.</span><span class="sxs-lookup"><span data-stu-id="82439-130">Follow the instruction to add the **Owner** role to the Azure AD application you created in the last procedure.</span></span> <span data-ttu-id="82439-131">Wanneer u het met succes voltooid, ziet u de toepassing die worden vermeld in de blade gebruikers met de rol van eigenaar.</span><span class="sxs-lookup"><span data-stu-id="82439-131">When you complete it successfully, you shall see the application listed in the Users blade with the Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="82439-132">HDInsight-client-toepassing ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="82439-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="82439-133">Maak een C#-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="82439-133">Create a C# console application.</span></span>
2. <span data-ttu-id="82439-134">De volgende Nuget-pakketten toevoegen:</span><span class="sxs-lookup"><span data-stu-id="82439-134">Add the following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="82439-135">Gebruik het volgende codevoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="82439-135">Use the following code sample:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="82439-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82439-136">Next steps</span></span>
* [<span data-ttu-id="82439-137">Azure Active Directory-toepassing en service-principal maken met portal maken</span><span class="sxs-lookup"><span data-stu-id="82439-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="82439-138">Service-principal met Azure Resource Manager verifiëren</span><span class="sxs-lookup"><span data-stu-id="82439-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="82439-139">Op rollen gebaseerde toegangsbeheer van Azure</span><span class="sxs-lookup"><span data-stu-id="82439-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
