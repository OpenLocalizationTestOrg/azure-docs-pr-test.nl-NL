---
title: Instellen van Azure Sleutelkluis met end-to-end sleutel worden gedraaid en controle | Microsoft Docs
description: Met deze procedures kunt u met de sleutel worden gedraaid en bewaking sleutelkluis-logboeken ophalen instellen.
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: 38c342802ed687985ac6f84f5a590a1a0dcc6c6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="7eddf-103">Azure Key Vault instellen met end-to-end sleutelrotatie en -controle</span><span class="sxs-lookup"><span data-stu-id="7eddf-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="7eddf-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="7eddf-104">Introduction</span></span>
<span data-ttu-id="7eddf-105">Na het maken van de sleutelkluis, kunt u zich kunt starten dat kluis gebruiken voor het opslaan van uw sleutels en geheimen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-105">After creating your key vault, you will be able to start using that vault to store your keys and secrets.</span></span> <span data-ttu-id="7eddf-106">Uw toepassingen niet langer nodig hebt voor het persistent maken van uw sleutels of geheimen, maar in plaats daarvan wordt deze aanvragen op de sleutelkluis indien nodig.</span><span class="sxs-lookup"><span data-stu-id="7eddf-106">Your applications no longer need to persist your keys or secrets, but rather will request them from the key vault as needed.</span></span> <span data-ttu-id="7eddf-107">Hiermee kunt u sleutels en geheimen bijwerken zonder het gedrag van uw toepassing, wat een groot aantal mogelijkheden om uw sleutel en geheime management wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="7eddf-107">This allows you to update keys and secrets without affecting the behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="7eddf-108">Dit artikel begeleidt bij een voorbeeld van het gebruik van Azure Key Vault voor het opslaan van een geheim in dit geval een Azure Storage-Account-sleutel die is geopend door een toepassing.</span><span class="sxs-lookup"><span data-stu-id="7eddf-108">This article walks through an example of using Azure Key Vault to store a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="7eddf-109">U ziet ook uitvoering van een geplande rotatie van de sleutel van die opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7eddf-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="7eddf-110">Ten slotte wordt begeleid bij een demonstratie van het bewaken van de controlelogboeken van de sleutelkluis en waarschuwingen genereren wanneer onverwachte aanvragen worden gedaan.</span><span class="sxs-lookup"><span data-stu-id="7eddf-110">Finally, it walks through a demonstration of how to monitor the key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="7eddf-111">Deze zelfstudie is niet bedoeld om uit te leggen in detail de eerste installatie van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7eddf-111">This tutorial is not intended to explain in detail the initial setup of your key vault.</span></span> <span data-ttu-id="7eddf-112">Zie [Aan de slag met Azure Key Vault](key-vault-get-started.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7eddf-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="7eddf-113">Zie voor instructies platformoverschrijdende opdrachtregelinterface [Key Vault beheren met CLI](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="7eddf-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="7eddf-114">Key Vault instellen</span><span class="sxs-lookup"><span data-stu-id="7eddf-114">Set up Key Vault</span></span>
<span data-ttu-id="7eddf-115">Om een toepassing een geheim ophalen uit Sleutelkluis, moet u eerst het geheim maken en uploaden naar uw kluis.</span><span class="sxs-lookup"><span data-stu-id="7eddf-115">To enable an application to retrieve a secret from Key Vault, you must first create the secret and upload it to your vault.</span></span> <span data-ttu-id="7eddf-116">Dit kunt doen met Azure PowerShell-sessie starten en het aanmelden bij uw Azure-account met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7eddf-116">This can be accomplished by starting an Azure PowerShell session and signing in to your Azure account with the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="7eddf-117">Voer in het pop-upvenster in de browser uw gebruikersnaam en wachtwoord voor uw Azure-account in.</span><span class="sxs-lookup"><span data-stu-id="7eddf-117">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="7eddf-118">PowerShell haalt alle abonnementen die gekoppeld aan dit account zijn.</span><span class="sxs-lookup"><span data-stu-id="7eddf-118">PowerShell will get all the subscriptions that are associated with this account.</span></span> <span data-ttu-id="7eddf-119">PowerShell gebruikt de eerste standaard.</span><span class="sxs-lookup"><span data-stu-id="7eddf-119">PowerShell uses the first one by default.</span></span>

<span data-ttu-id="7eddf-120">Als u meerdere abonnementen hebt, moet u wellicht opgeven die werd gebruikt voor het maken van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7eddf-120">If you have multiple subscriptions, you might have to specify the one that was used to create your key vault.</span></span> <span data-ttu-id="7eddf-121">Voer de volgende als u wilt zien van de abonnementen voor uw account:</span><span class="sxs-lookup"><span data-stu-id="7eddf-121">Enter the following to see the subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="7eddf-122">Geef het abonnement dat is gekoppeld aan de sleutelkluis die u logboekregistratie wilt inschakelen, voeren:</span><span class="sxs-lookup"><span data-stu-id="7eddf-122">To specify the subscription that's associated with the key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="7eddf-123">Omdat dit artikel wordt beschreven voor het opslaan van de sleutel van een opslagaccount als een geheim, moet u die opslagaccountsleutel ophalen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="7eddf-124">Bij het ophalen van het geheim (in dit geval wordt een sleutel van uw opslagaccount), moet u die naar een veilige tekenreeks te converteren en vervolgens een geheim maken met de waarde in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7eddf-124">After retrieving your secret (in this case, your storage account key), you must convert that to a secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="7eddf-125">Haal vervolgens de URI voor het geheim die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7eddf-125">Next, get the URI for the secret you created.</span></span> <span data-ttu-id="7eddf-126">Dit wordt gebruikt in een latere stap bij het aanroepen van de sleutelkluis voor het ophalen van het geheim.</span><span class="sxs-lookup"><span data-stu-id="7eddf-126">This is used in a later step when you call the key vault to retrieve your secret.</span></span> <span data-ttu-id="7eddf-127">Voer de volgende PowerShell-opdracht en noteer de ID-waarde de geheime URI is:</span><span class="sxs-lookup"><span data-stu-id="7eddf-127">Run the following PowerShell command and make note of the ID value, which is the secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-the-application"></a><span data-ttu-id="7eddf-128">De toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="7eddf-128">Set up the application</span></span>
<span data-ttu-id="7eddf-129">Nu dat u een geheim dat is opgeslagen hebt, kunt u code ophalen en deze gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7eddf-129">Now that you have a secret stored, you can use code to retrieve and use it.</span></span> <span data-ttu-id="7eddf-130">Er zijn een paar stappen vereist om dit te bereiken.</span><span class="sxs-lookup"><span data-stu-id="7eddf-130">There are a few steps required to achieve this.</span></span> <span data-ttu-id="7eddf-131">De eerste en belangrijkste stap is het registreren van uw toepassing met Azure Active Directory en vervolgens melding Sleutelkluis de informatie over uw toepassing zodat deze aanvragen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7eddf-131">The first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="7eddf-132">Uw toepassing moet worden gemaakt op dezelfde Azure Active Directory-tenant als uw sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7eddf-132">Your application must be created on the same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="7eddf-133">Open het tabblad toepassingen van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7eddf-133">Open the applications tab of Azure Active Directory.</span></span>

![Geopende toepassingen in Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="7eddf-135">Kies **toevoegen** een toepassing toevoegen aan uw Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7eddf-135">Choose **ADD** to add an application to your Azure Active Directory.</span></span>

![Kies toevoegen](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="7eddf-137">Laat het toepassingstype als **WEBTOEPASSING en/of WEB-API** en geef een naam op voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7eddf-137">Leave the application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![De naam van de toepassing](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="7eddf-139">Geef de toepassing een **AANMELDINGS-URL** en een **APP ID URI**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="7eddf-140">Dit kunnen van alles die voor deze demo gewenste zijn en ze kunnen later worden gewijzigd indien nodig.</span><span class="sxs-lookup"><span data-stu-id="7eddf-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Geef de vereiste URI 's](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="7eddf-142">Nadat de toepassing is toegevoegd aan Azure Active Directory, wordt u naar de pagina voor toepassingen worden gezet.</span><span class="sxs-lookup"><span data-stu-id="7eddf-142">After the application is added to Azure Active Directory, you will be brought into the application page.</span></span> <span data-ttu-id="7eddf-143">Klik op de **configureren** tabblad en klik vervolgens zoeken en kopieer de **Client-ID** waarde.</span><span class="sxs-lookup"><span data-stu-id="7eddf-143">Click the **Configure** tab and then find and copy the **Client ID** value.</span></span> <span data-ttu-id="7eddf-144">Noteer de client-ID voor de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-144">Make note of the client ID for later steps.</span></span>

<span data-ttu-id="7eddf-145">Vervolgens wordt een sleutel genereren voor uw toepassing zodat deze met uw Azure Active Directory communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="7eddf-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="7eddf-146">U kunt dit onder maken de **sleutels** sectie het **configuratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7eddf-146">You can create this under the **Keys** section in the **Configuration** tab.</span></span> <span data-ttu-id="7eddf-147">Let op het zojuist gegenereerde sleutel van uw Azure Active Directory-toepassing voor gebruik in een latere stap.</span><span class="sxs-lookup"><span data-stu-id="7eddf-147">Make note of the newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Sleutels voor Azure Active Directory-App](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="7eddf-149">Voordat er een aanroepen vanuit uw App in de sleutelkluis, moet u de sleutelkluis Vertel over uw toepassing en de bijbehorende machtigingen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-149">Before establishing any calls from your application into the key vault, you must tell the key vault about your application and its permissions.</span></span> <span data-ttu-id="7eddf-150">De volgende opdracht wordt de kluisnaam van de en de client-ID van uw Azure Active Directory-app en verleent **ophalen** toegang tot de sleutelkluis voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7eddf-150">The following command takes the vault name and the client ID from your Azure Active Directory app and grants **Get** access to your key vault for the application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="7eddf-151">Op dit moment bent u klaar om te beginnen met het bouwen van uw toepassing aanroepen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-151">At this point, you are ready to start building your application calls.</span></span> <span data-ttu-id="7eddf-152">U moet de NuGet-pakketten dat is vereist voor interactie met Azure Key Vault en Azure Active Directory installeren in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7eddf-152">In your application, you must install the NuGet packages required to interact with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="7eddf-153">Voer de volgende opdrachten vanuit de Visual Studio Package Manager-console.</span><span class="sxs-lookup"><span data-stu-id="7eddf-153">From the Visual Studio Package Manager console, enter the following commands.</span></span> <span data-ttu-id="7eddf-154">Bij het schrijven van dit artikel is de huidige versie van het pakket met Azure Active Directory 3.10.305231913, dus raadzaam om te bevestigen van de meest recente versie en dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="7eddf-154">At the writing of this article, the current version of the Azure Active Directory package is 3.10.305231913, so you might want to confirm the latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="7eddf-155">Maak een klasse voor het opslaan van de methode voor uw Azure Active Directory-verificatie in uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="7eddf-155">In your application code, create a class to hold the method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="7eddf-156">In dit voorbeeld die klasse wordt aangeroepen **Utils**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-156">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="7eddf-157">Voeg het volgende toe met de instructie:</span><span class="sxs-lookup"><span data-stu-id="7eddf-157">Add the following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="7eddf-158">Voeg vervolgens de volgende methode voor het ophalen van de JWT-token van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7eddf-158">Next, add the following method to retrieve the JWT token from Azure Active Directory.</span></span> <span data-ttu-id="7eddf-159">Voor onderhoud wilt u mogelijk verplaatsen van de vastgelegde tekenreekswaarden in de configuratie van uw website of toepassing.</span><span class="sxs-lookup"><span data-stu-id="7eddf-159">For maintainability, you may want to move the hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="7eddf-160">Voeg de benodigde code voor het aanroepen van de Sleutelkluis en uw geheime waarde wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="7eddf-160">Add the necessary code to call Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="7eddf-161">Eerst moet u het volgende toevoegen met de instructie:</span><span class="sxs-lookup"><span data-stu-id="7eddf-161">First you must add the following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="7eddf-162">Het methodeaanroepen van de invoke Sleutelkluis en ophalen van het geheim toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-162">Add the method calls to invoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="7eddf-163">Deze methode geeft u het geheim URI die u hebt opgeslagen in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="7eddf-163">In this method, you provide the secret URI that you saved in a previous step.</span></span> <span data-ttu-id="7eddf-164">Let op het gebruik van de **GetToken** methode van de **Utils** klasse eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7eddf-164">Note the use of the **GetToken** method from the **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="7eddf-165">Wanneer u uw toepassing uitvoert, nu moet u verificatie met Azure Active Directory en vervolgens uw geheime waarde ophalen van Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7eddf-165">When you run your application, you should now be authenticating to Azure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="7eddf-166">Sleutel rotatie met behulp van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7eddf-166">Key rotation using Azure Automation</span></span>
<span data-ttu-id="7eddf-167">Er zijn diverse opties voor het implementeren van een strategie worden gedraaid voor waarden die u als Azure Key Vault geheimen opslaan.</span><span class="sxs-lookup"><span data-stu-id="7eddf-167">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="7eddf-168">Geheimen kunnen worden gedraaid als onderdeel van een handmatig proces, kan programmatisch met behulp van API-aanroepen worden gedraaid of ze in een automatiseringsscript kunnen worden gedraaid.</span><span class="sxs-lookup"><span data-stu-id="7eddf-168">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="7eddf-169">Voor de doeleinden van dit artikel gaat u Azure PowerShell in combinatie met Azure Automation gebruiken een toegangssleutel voor Azure Storage-Account wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-169">For the purposes of this article, you will be using Azure PowerShell combined with Azure Automation to change an Azure Storage Account access key.</span></span> <span data-ttu-id="7eddf-170">U wordt vervolgens een geheim sleutelkluis bijwerken met deze nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="7eddf-170">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="7eddf-171">Als u Azure Automation geheime waarden instellen voor uw sleutelkluis, moet u de client-ID ophalen voor de verbinding met de naam AzureRunAsConnection die is gemaakt wanneer u uw exemplaar van Azure Automation tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="7eddf-171">To allow Azure Automation to set secret values in your key vault, you must get the client ID for the connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="7eddf-172">U kunt deze ID vinden door te kiezen **activa** van uw Azure Automation-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="7eddf-172">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="7eddf-173">Van daaruit, kiest u **verbindingen** en selecteer vervolgens de **AzureRunAsConnection** principe service.</span><span class="sxs-lookup"><span data-stu-id="7eddf-173">From there, you choose **Connections** and then select the **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="7eddf-174">Noteer de **toepassings-ID**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-174">Take note of the **Application ID**.</span></span>

![Azure Automation-client-ID](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="7eddf-176">In **activa**, kies **Modules**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-176">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="7eddf-177">Van **Modules**, selecteer **galerie**, en zoek vervolgens naar en **importeren** bijgewerkte versies van elk van de volgende modules:</span><span class="sxs-lookup"><span data-stu-id="7eddf-177">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of the following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="7eddf-178">Bij het schrijven van dit artikel wordt alleen de modules die eerder is vermeld nodig om te worden bijgewerkt in verband met het volgende script.</span><span class="sxs-lookup"><span data-stu-id="7eddf-178">At the writing of this article, only the previously noted modules needed to be updated for the following script.</span></span> <span data-ttu-id="7eddf-179">Als u merkt dat uw automation-taak is mislukt, moet u bevestigen dat u alle benodigde modules en de bijbehorende afhankelijkheden hebt geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="7eddf-179">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="7eddf-180">Nadat u hebt de toepassings-ID opgehaald voor uw Azure Automation-verbinding, moet u de sleutelkluis zien dat deze toepassing toegang heeft tot bijwerken van geheimen in uw kluis aan te geven.</span><span class="sxs-lookup"><span data-stu-id="7eddf-180">After you have retrieved the application ID for your Azure Automation connection, you must tell your key vault that this application has access to update secrets in your vault.</span></span> <span data-ttu-id="7eddf-181">Dit kan worden bewerkstelligd met de volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="7eddf-181">This can be accomplished with the following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="7eddf-182">Selecteer vervolgens **Runbooks** onder uw Azure Automation-instantie en selecteer vervolgens **een Runbook toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-182">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="7eddf-183">Selecteer **Snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-183">Select **Quick Create**.</span></span> <span data-ttu-id="7eddf-184">De naam van uw runbook en selecteer **PowerShell** als het runbooktype.</span><span class="sxs-lookup"><span data-stu-id="7eddf-184">Name your runbook and select **PowerShell** as the runbook type.</span></span> <span data-ttu-id="7eddf-185">U hebt de optie voor het toevoegen van een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="7eddf-185">You have the option to add a description.</span></span> <span data-ttu-id="7eddf-186">Tot slot op **maken**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-186">Finally, click **Create**.</span></span>

![Runbook maken](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="7eddf-188">Plak het volgende PowerShell-script in het venster editor voor uw nieuwe runbook:</span><span class="sxs-lookup"><span data-stu-id="7eddf-188">Paste the following PowerShell script in the editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get the connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in to Azure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set the following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for the storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="7eddf-189">Kies in het deelvenster editor **testvenster** voor het testen van uw script.</span><span class="sxs-lookup"><span data-stu-id="7eddf-189">From the editor pane, choose **Test pane** to test your script.</span></span> <span data-ttu-id="7eddf-190">Wanneer het script wordt uitgevoerd zonder fouten, kunt u selecteren **publiceren**, en vervolgens kunt u een planning voor het runbook terug in het deelvenster runbook configuratie toepassen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-190">Once the script is running without error, you can select **Publish**, and then you can apply a schedule for the runbook back in the runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="7eddf-191">Controle Sleutelkluis-pipeline</span><span class="sxs-lookup"><span data-stu-id="7eddf-191">Key Vault auditing pipeline</span></span>
<span data-ttu-id="7eddf-192">Wanneer u een sleutelkluis hebt ingesteld, kunt u de controle voor het verzamelen van Logboeken op toegangsaanvragen voor de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="7eddf-192">When you set up a key vault, you can turn on auditing to collect logs on access requests made to the key vault.</span></span> <span data-ttu-id="7eddf-193">Deze logboeken worden opgeslagen in een aangewezen Azure Storage-account en kunnen worden opgevraagd, bewaakt en geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="7eddf-193">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="7eddf-194">Het volgende scenario maakt gebruik van Azure functions, Azure logic apps en sleutelkluis controlelogboeken voor het maken van een pijplijn een e-mailbericht verzenden wanneer een app die overeenkomt met de app-ID van de web-app geheimen opgehaald uit de kluis.</span><span class="sxs-lookup"><span data-stu-id="7eddf-194">The following scenario uses Azure functions, Azure logic apps, and key vault audit logs to create a pipeline to send an email when an app that does match the app ID of the web app retrieves secrets from the vault.</span></span>

<span data-ttu-id="7eddf-195">Eerst moet u de sleutelkluis aanmelden inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-195">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="7eddf-196">U kunt dit doen via de volgende PowerShell-opdrachten (alle gegevens die kunnen worden weergegeven wanneer [sleutel kluis registreren](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="7eddf-196">This can be done via the following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="7eddf-197">Nadat dit is ingeschakeld, wordt de auditlogboeken start verzamelen in het opgegeven opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7eddf-197">After this is enabled, audit logs start collecting into the designated storage account.</span></span> <span data-ttu-id="7eddf-198">Deze logboeken bevatten gebeurtenissen over hoe en wanneer uw sleutelkluizen toegankelijk zijn en door wie.</span><span class="sxs-lookup"><span data-stu-id="7eddf-198">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="7eddf-199">U kunt toegang tot uw logboekgegevens 10 minuten nadat de sleutelkluis-bewerking.</span><span class="sxs-lookup"><span data-stu-id="7eddf-199">You can access your logging information 10 minutes after the key vault operation.</span></span> <span data-ttu-id="7eddf-200">Dit wordt meestal sneller worden.</span><span class="sxs-lookup"><span data-stu-id="7eddf-200">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="7eddf-201">De volgende stap is het [maken van een Azure Service Bus-wachtrij](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="7eddf-201">The next step is to [create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="7eddf-202">Dit is waar sleutelkluis controlelogboeken worden gepusht.</span><span class="sxs-lookup"><span data-stu-id="7eddf-202">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="7eddf-203">Wanneer de wachtrij de berichten voor het controlelogboek, wordt de logische app ze opneemt en uitgevoerd op deze.</span><span class="sxs-lookup"><span data-stu-id="7eddf-203">When the audit log messages are in the queue, the logic app picks them up and acts on them.</span></span> <span data-ttu-id="7eddf-204">Een servicebus Maak met de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7eddf-204">Create a service bus with the following steps:</span></span>

1. <span data-ttu-id="7eddf-205">Een Service Bus-naamruimte maken (als u al die u wilt gebruiken voor deze, gaat u verder met stap 2 hebt).</span><span class="sxs-lookup"><span data-stu-id="7eddf-205">Create a Service Bus namespace (if you already have one that you want to use for this, skip to Step 2).</span></span>
2. <span data-ttu-id="7eddf-206">Blader naar de servicebus in de Azure portal en selecteer de naamruimte die u wilt maken van de wachtrij in.</span><span class="sxs-lookup"><span data-stu-id="7eddf-206">Browse to the service bus in the Azure portal and select the namespace you want to create the queue in.</span></span>
3. <span data-ttu-id="7eddf-207">Selecteer **nieuw** en kies **Service Bus > wachtrij** en voer de vereiste gegevens.</span><span class="sxs-lookup"><span data-stu-id="7eddf-207">Select **New** and choose **Service Bus > Queue** and enter the required details.</span></span>
4. <span data-ttu-id="7eddf-208">Selecteer de Service Bus-verbindingsinformatie door de naamruimte kiezen en op **verbindingsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-208">Select the Service Bus connection information by choosing the namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="7eddf-209">U moet deze informatie gebruiken voor de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="7eddf-209">You will need this information for the next section.</span></span>

<span data-ttu-id="7eddf-210">Vervolgens [maken van een Azure-functie](../azure-functions/functions-create-first-azure-function.md) om te pollen sleutelkluis-Logboeken in het opslagaccount en nieuwe gebeurtenissen kunnen worden opgepikt.</span><span class="sxs-lookup"><span data-stu-id="7eddf-210">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) to poll key vault logs within the storage account and pick up new events.</span></span> <span data-ttu-id="7eddf-211">Dit is een functie die volgens een planning wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="7eddf-211">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="7eddf-212">Kies voor het maken van een Azure-functie **Nieuw > functie-App** in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7eddf-212">To create an Azure function, choose **New > Function App** in the Azure portal.</span></span> <span data-ttu-id="7eddf-213">U kunt tijdens het maken van een bestaand abonnement hosting gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="7eddf-213">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="7eddf-214">U kunt ook kiezen voor het hosten van dynamische.</span><span class="sxs-lookup"><span data-stu-id="7eddf-214">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="7eddf-215">Meer informatie over de functie opties host kunnen worden gevonden op [Azure Functions schalen](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="7eddf-215">More details on Function hosting options can be found at [How to scale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="7eddf-216">Wanneer de functie Azure is gemaakt, gaat u naar het en kies een timer functie en C\#.</span><span class="sxs-lookup"><span data-stu-id="7eddf-216">When the Azure function is created, navigate to it and choose a timer function and C\#.</span></span> <span data-ttu-id="7eddf-217">Klik vervolgens op **maken van deze functie**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-217">Then click **Create this function**.</span></span>

![Blade van Azure Functions starten](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="7eddf-219">Op de **ontwikkelen** tabblad, vervang de code run.csx door het volgende:</span><span class="sxs-lookup"><span data-stu-id="7eddf-219">On the **Develop** tab, replace the run.csx code with the following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting to now.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required to order by time as they may not be in the file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending to ServiceBus, use the payloadStream and set keeporiginal to true
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="7eddf-220">Zorg ervoor dat u de variabelen in de bovenstaande code verwijzen naar uw opslagaccount waarin de sleutelkluis-Logboeken geschreven, de servicebus die u eerder hebt gemaakt en het specifieke pad naar de sleutelkluis-logboeken voor opslag.</span><span class="sxs-lookup"><span data-stu-id="7eddf-220">Make sure to replace the variables in the preceding code to point to your storage account where the key vault logs are written, the service bus you created earlier, and the specific path to the key vault storage logs.</span></span>
>
>

<span data-ttu-id="7eddf-221">De functie neemt over de meest recente logboekbestand vanuit het opslagaccount waarin de sleutelkluis-Logboeken geschreven, pakt de meest recente gebeurtenissen uit dat bestand en stuurt deze naar een Service Bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7eddf-221">The function picks up the latest log file from the storage account where the key vault logs are written, grabs the latest events from that file, and pushes them to a Service Bus queue.</span></span> <span data-ttu-id="7eddf-222">Aangezien één enkel bestand meerdere gebeurtenissen hebben kan, moet u een sync.txt-bestand dat de functie wordt ook bekeken om te bepalen van de tijdstempel van de laatste gebeurtenis die is opgehaald.</span><span class="sxs-lookup"><span data-stu-id="7eddf-222">Since a single file could have multiple events, you should create a sync.txt file that the function also looks at to determine the time stamp of the last event that was picked up.</span></span> <span data-ttu-id="7eddf-223">Dit zorgt ervoor dat u geen dezelfde gebeurtenis meerdere keren pushen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-223">This ensures that you don't push the same event multiple times.</span></span> <span data-ttu-id="7eddf-224">Dit bestand sync.txt bevat een tijdstempel voor laatste gebeurtenis aangetroffen.</span><span class="sxs-lookup"><span data-stu-id="7eddf-224">This sync.txt file contains a timestamp for the last encountered event.</span></span> <span data-ttu-id="7eddf-225">De logboeken als geladen, moeten worden gesorteerd op basis van het tijdstempel om te controleren of dat ze correct zijn gerangschikt.</span><span class="sxs-lookup"><span data-stu-id="7eddf-225">The logs, when loaded, have to be sorted based on the timestamp to ensure they are ordered correctly.</span></span>

<span data-ttu-id="7eddf-226">Voor deze functie, verwijzen we naar een aantal aanvullende bibliotheken die niet beschikbaar gebruiksklaar in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="7eddf-226">For this function, we reference a couple of additional libraries that are not available out of the box in Azure Functions.</span></span> <span data-ttu-id="7eddf-227">Zodanig dat deze, moeten we Azure Functions om op te halen ze met NuGet.</span><span class="sxs-lookup"><span data-stu-id="7eddf-227">To include these, we need Azure Functions to pull them using NuGet.</span></span> <span data-ttu-id="7eddf-228">Kies de **bestanden weergeven** optie.</span><span class="sxs-lookup"><span data-stu-id="7eddf-228">Choose the **View Files** option.</span></span>

![Optie bestanden weergeven](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="7eddf-230">En toevoegen van een bestand met de naam project.json met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="7eddf-230">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="7eddf-231">Bij **opslaan**, Azure Functions vereiste binaire bestanden worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="7eddf-231">Upon **Save**, Azure Functions will download the required binaries.</span></span>

<span data-ttu-id="7eddf-232">Overschakelen naar de **integreren** tabblad en geef de parameter timer een betekenisvolle naam te gebruiken binnen de functie.</span><span class="sxs-lookup"><span data-stu-id="7eddf-232">Switch to the **Integrate** tab and give the timer parameter a meaningful name to use within the function.</span></span> <span data-ttu-id="7eddf-233">In de voorgaande code wordt ervan uitgegaan dat de timer moet worden aangeroepen *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="7eddf-233">In the preceding code, it expects the timer to be called *myTimer*.</span></span> <span data-ttu-id="7eddf-234">Geef een [CRON expressie](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) als volgt: 0 \* \* \* \* \* voor de timer waardoor de functie eenmaal een minuut uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7eddf-234">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for the timer that will cause the function to run once a minute.</span></span>

<span data-ttu-id="7eddf-235">Op dezelfde **integreren** tabblad, het toevoegen van een invoer van het type **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-235">On the same **Integrate** tab, add an input of the type **Azure Blob Storage**.</span></span> <span data-ttu-id="7eddf-236">Dit verwijst naar het sync.txt-bestand dat de tijdstempel van de laatste gebeurtenis bekeken door de functie bevat.</span><span class="sxs-lookup"><span data-stu-id="7eddf-236">This will point to the sync.txt file that contains the timestamp of the last event looked at by the function.</span></span> <span data-ttu-id="7eddf-237">Dit zijn beschikbaar binnen de functie door de parameternaam van de.</span><span class="sxs-lookup"><span data-stu-id="7eddf-237">This will be available within the function by the parameter name.</span></span> <span data-ttu-id="7eddf-238">In de vorige code de Azure Blob Storage-invoer verwacht de parameternaam moet *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="7eddf-238">In the preceding code, the Azure Blob Storage input expects the parameter name to be *inputBlob*.</span></span> <span data-ttu-id="7eddf-239">Kies het opslagaccount waarin het bestand sync.txt wordt opgeslagen (kan zijn hetzelfde of een ander opslagaccount).</span><span class="sxs-lookup"><span data-stu-id="7eddf-239">Choose the storage account where the sync.txt file will reside (it could be the same or a different storage account).</span></span> <span data-ttu-id="7eddf-240">In het padveld geeft u het pad waar het bestand zich in de notatie {container-name}/path/to/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="7eddf-240">In the path field, provide the path where the file lives in the format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="7eddf-241">Toevoegen van de uitvoer van het type *Azure Blob Storage* uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7eddf-241">Add an output of the type *Azure Blob Storage* output.</span></span> <span data-ttu-id="7eddf-242">Dit verwijst naar het sync.txt-bestand dat u hebt gedefinieerd in de invoer.</span><span class="sxs-lookup"><span data-stu-id="7eddf-242">This will point to the sync.txt file you defined in the input.</span></span> <span data-ttu-id="7eddf-243">Dit wordt gebruikt door de functie voor het schrijven van het tijdstempel van de laatste gebeurtenis bekeken.</span><span class="sxs-lookup"><span data-stu-id="7eddf-243">This is used by the function to write the timestamp of the last event looked at.</span></span> <span data-ttu-id="7eddf-244">De bovenstaande code verwacht dat deze parameter moet worden aangeroepen *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="7eddf-244">The preceding code expects this parameter to be called *outputBlob*.</span></span>

<span data-ttu-id="7eddf-245">De functie is nu klaar.</span><span class="sxs-lookup"><span data-stu-id="7eddf-245">At this point, the function is ready.</span></span> <span data-ttu-id="7eddf-246">Zorg ervoor dat u gaat u terug naar de **ontwikkelen** tabblad en de code op te slaan.</span><span class="sxs-lookup"><span data-stu-id="7eddf-246">Make sure to switch back to the **Develop** tab and save the code.</span></span> <span data-ttu-id="7eddf-247">Controleer het uitvoervenster op compilatiefouten en corrigeer deze dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="7eddf-247">Check the output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="7eddf-248">Als de code wordt gecompileerd, moet vervolgens de code nu worden elke minuut van de sleutelkluis-logboeken controleren en eventuele nieuwe gebeurtenissen naar de gedefinieerde Service Bus-wachtrij worden gepusht.</span><span class="sxs-lookup"><span data-stu-id="7eddf-248">If the code compiles, then the code should now be checking the key vault logs every minute and pushing any new events onto the defined Service Bus queue.</span></span> <span data-ttu-id="7eddf-249">U ziet logboekinformatie wegschrijven naar het logboekvenster telkens wanneer de functie wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="7eddf-249">You should see logging information write out to the log window every time the function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="7eddf-250">Azure logic app</span><span class="sxs-lookup"><span data-stu-id="7eddf-250">Azure logic app</span></span>
<span data-ttu-id="7eddf-251">Vervolgens moet u een Azure logic app die neemt over de gebeurtenissen met de functie pusht naar de Service Bus-wachtrij, parseert de inhoud en verzendt een e-mail op basis van een voorwaarde wordt aangepast maken.</span><span class="sxs-lookup"><span data-stu-id="7eddf-251">Next you must create an Azure logic app that picks up the events that the function is pushing to the Service Bus queue, parses the content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="7eddf-252">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md) door te gaan naar **Nieuw > logische App**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-252">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going to **New > Logic App**.</span></span>

<span data-ttu-id="7eddf-253">Zodra de logische app is gemaakt, gaat u naar het en kies **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-253">Once the logic app is created, navigate to it and choose **edit**.</span></span> <span data-ttu-id="7eddf-254">Kies in de editor logic app **Service Bus-wachtrij** en voer uw Service Bus-referenties om te verbinden met de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7eddf-254">Within the logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials to connect it to the queue.</span></span>

![Azure Logic App Service Bus](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="7eddf-256">Kies vervolgens **een voorwaarde toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-256">Next choose **Add a condition**.</span></span> <span data-ttu-id="7eddf-257">Overschakelen naar de geavanceerde editor in de voorwaarde, en voer de volgende code, APP_ID vervangen door de werkelijke APP_ID van uw web-app:</span><span class="sxs-lookup"><span data-stu-id="7eddf-257">In the condition, switch to the advanced editor and enter the following code, replacing APP_ID with the actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="7eddf-258">Deze expressie retourneert in wezen **false** als de *appid* van de inkomende gebeurtenis (dit is de hoofdtekst van het bericht Service Bus) is niet de *appid* van de app.</span><span class="sxs-lookup"><span data-stu-id="7eddf-258">This expression essentially returns **false** if the *appid* from the incoming event (which is the body of the Service Bus message) is not the *appid* of the app.</span></span>

<span data-ttu-id="7eddf-259">Maak nu een actie onder **zo Nee, niets doen**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-259">Now, create an action under **If no, do nothing**.</span></span>

![Azure Logic App kiezen actie](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="7eddf-261">Kies voor de actie **Office 365 - e-mailbericht verzenden**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-261">For the action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="7eddf-262">Vul de velden voor het maken van een e-mailbericht verzenden wanneer de ingestelde voorwaarde retourneert **false**.</span><span class="sxs-lookup"><span data-stu-id="7eddf-262">Fill out the fields to create an email to send when the defined condition returns **false**.</span></span> <span data-ttu-id="7eddf-263">Als u geen Office 365 hebt, kunt u alternatieven voor dezelfde resultaten bereiken bekijken.</span><span class="sxs-lookup"><span data-stu-id="7eddf-263">If you do not have Office 365, you could look at alternatives to achieve the same results.</span></span>

<span data-ttu-id="7eddf-264">U hebt op dit moment een end-to-end-pijplijn eens per minuut wordt gezocht naar de nieuwe sleutelkluis controlelogboeken.</span><span class="sxs-lookup"><span data-stu-id="7eddf-264">At this point, you have an end to end pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="7eddf-265">Deze verstuurd nieuwe logboeken vindt naar een service bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7eddf-265">It pushes new logs it finds to a service bus queue.</span></span> <span data-ttu-id="7eddf-266">De logische app wordt geactiveerd wanneer een nieuw bericht in de wachtrij terechtkomt.</span><span class="sxs-lookup"><span data-stu-id="7eddf-266">The logic app is triggered when a new message lands in the queue.</span></span> <span data-ttu-id="7eddf-267">Als de *appid* binnen de gebeurtenis komt niet overeen met de app-ID van de oproepende toepassing, zendt het een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="7eddf-267">If the *appid* within the event does not match the app ID of the calling application, it sends an email.</span></span>
