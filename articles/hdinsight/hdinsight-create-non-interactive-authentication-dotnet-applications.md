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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="597f6-103">Niet-interactieve verificatie .NET HDInsight-toepassingen maken</span><span class="sxs-lookup"><span data-stu-id="597f6-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="597f6-104">U kunt uw .NET Azure HDInsight-toepassing onder de identiteit van de van toepassing is (niet-interactieve) of onder de identiteit Hallo van Hallo aangemelde gebruiker van Hallo-toepassing (interactief) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="597f6-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under hello identity of hello signed-in user of hello application (interactive).</span></span> <span data-ttu-id="597f6-105">Zie voor een voorbeeld van de interactieve toepassing hello [tooAzure HDInsight verbinding](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="597f6-105">For a sample of hello interactive application, see [Connect tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="597f6-106">Dit artikel ziet u hoe toocreate niet-interactieve verificatie .NET application tooconnect tooAzure en HDInsight beheren.</span><span class="sxs-lookup"><span data-stu-id="597f6-106">This article shows you how toocreate non-interactive authentication .NET application tooconnect tooAzure and manage HDInsight.</span></span>

<span data-ttu-id="597f6-107">U moet van een niet-interactieve .NET-toepassing:</span><span class="sxs-lookup"><span data-stu-id="597f6-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="597f6-108">Uw Azure-abonnement tenant-ID (ook wel directory-ID).</span><span class="sxs-lookup"><span data-stu-id="597f6-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="597f6-109">Zie [tenant-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="597f6-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="597f6-110">Hello Azure Active Directory-toepassingsclient-id.</span><span class="sxs-lookup"><span data-stu-id="597f6-110">hello Azure Active Directory application client ID.</span></span> <span data-ttu-id="597f6-111">Zie [maken van een Azure Active Directory-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), en [een toepassings-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="597f6-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="597f6-112">Hello Azure Active Directory-toepassing geheime sleutel.</span><span class="sxs-lookup"><span data-stu-id="597f6-112">hello Azure Active Directory application secret key.</span></span> <span data-ttu-id="597f6-113">Zie [verificatiesleutel Get-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="597f6-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="597f6-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="597f6-114">Prerequisites</span></span>
* <span data-ttu-id="597f6-115">HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="597f6-115">HDInsight cluster.</span></span> <span data-ttu-id="597f6-116">Zie [zelfstudie aan de slag](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="597f6-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-toorole"></a><span data-ttu-id="597f6-117">Azure AD-toepassing toorole toewijzen</span><span class="sxs-lookup"><span data-stu-id="597f6-117">Assign Azure AD application toorole</span></span>
<span data-ttu-id="597f6-118">U moet toewijzen Hallo toepassing tooa [rol](../active-directory/role-based-access-built-in-roles.md) toogrant deze machtigingen voor het uitvoeren van acties.</span><span class="sxs-lookup"><span data-stu-id="597f6-118">You must assign hello application tooa [role](../active-directory/role-based-access-built-in-roles.md) toogrant it permissions for performing actions.</span></span> <span data-ttu-id="597f6-119">U kunt Hallo bereik instellen op Hallo niveau van het Hallo-abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="597f6-119">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="597f6-120">Hallo machtigingen zijn overgenomen toolower niveaus van bereik (bijvoorbeeld toevoegen van die een toepassing toohello lezersrol voor een resourcegroep betekent dat het Hallo-resourcegroep kan lezen en alle resources die deze bevat).</span><span class="sxs-lookup"><span data-stu-id="597f6-120">hello permissions are inherited toolower levels of scope (for example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains).</span></span> <span data-ttu-id="597f6-121">In deze zelfstudie wordt u Hallo bereik instellen op Hallo niveau van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="597f6-121">In this tutorial, you will set hello scope at hello resource group level.</span></span> <span data-ttu-id="597f6-122">Zie voor meer informatie [rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="597f6-122">For more information, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="597f6-123">**tooadd hello eigenaar rol toohello Azure AD-toepassing**</span><span class="sxs-lookup"><span data-stu-id="597f6-123">**tooadd hello Owner role toohello Azure AD application**</span></span>

1. <span data-ttu-id="597f6-124">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="597f6-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="597f6-125">Klik op **resourcegroep** in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="597f6-125">Click **Resource Group** from hello left pane.</span></span>
3. <span data-ttu-id="597f6-126">Klik op Hallo-resourcegroep met Hallo HDInsight-cluster waar u uw Hive-query verderop in deze zelfstudie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="597f6-126">Click hello resource group that contains hello HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="597f6-127">Als er te veel resourcegroepen, kunt u Hallo filter.</span><span class="sxs-lookup"><span data-stu-id="597f6-127">If there are too many resource groups, you can use hello filter.</span></span>
4. <span data-ttu-id="597f6-128">Klik op **toegangsbeheer (IAM)** in menu Hallo resource-groep.</span><span class="sxs-lookup"><span data-stu-id="597f6-128">Click **Access control (IAM)** from hello resource group menu.</span></span>
5. <span data-ttu-id="597f6-129">Klik op **toevoegen** van Hallo **gebruikers** blade.</span><span class="sxs-lookup"><span data-stu-id="597f6-129">Click **Add** from hello **Users** blade.</span></span>
6. <span data-ttu-id="597f6-130">Ga als volgt Hallo instructie tooadd Hallo **eigenaar** rol toohello Azure AD-toepassing die u hebt gemaakt in de laatste procedure Hallo.</span><span class="sxs-lookup"><span data-stu-id="597f6-130">Follow hello instruction tooadd hello **Owner** role toohello Azure AD application you created in hello last procedure.</span></span> <span data-ttu-id="597f6-131">Wanneer u het met succes voltooid, ziet u die worden vermeld in de blade van Hallo gebruikers met de rol van eigenaar Hallo Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="597f6-131">When you complete it successfully, you shall see hello application listed in hello Users blade with hello Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="597f6-132">HDInsight-client-toepassing ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="597f6-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="597f6-133">Maak een C#-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="597f6-133">Create a C# console application.</span></span>
2. <span data-ttu-id="597f6-134">Hallo volgende Nuget-pakketten toevoegen:</span><span class="sxs-lookup"><span data-stu-id="597f6-134">Add hello following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="597f6-135">Hallo codevoorbeeld volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="597f6-135">Use hello following code sample:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="597f6-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="597f6-136">Next steps</span></span>
* [<span data-ttu-id="597f6-137">Azure Active Directory-toepassing en service-principal maken met portal maken</span><span class="sxs-lookup"><span data-stu-id="597f6-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="597f6-138">Service-principal met Azure Resource Manager verifiëren</span><span class="sxs-lookup"><span data-stu-id="597f6-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="597f6-139">Op rollen gebaseerde toegangsbeheer van Azure</span><span class="sxs-lookup"><span data-stu-id="597f6-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
