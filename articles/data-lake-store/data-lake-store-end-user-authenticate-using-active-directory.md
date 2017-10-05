---
title: 'Verificatie van de eindgebruiker: Data Lake Store met Azure Active Directory | Microsoft Docs'
description: Meer informatie over het bereiken van de eindgebruiker verificatie met Data Lake Store met Azure Active Directory
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: c20f5c39b00992d801909c8e5de292f3c2f12673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="c9390-103">Verificatie van de eindgebruiker met Data Lake Store met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9390-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9390-104">Verificatie van service-tot-service</span><span class="sxs-lookup"><span data-stu-id="c9390-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="c9390-105">Verificatie van de eindgebruiker</span><span class="sxs-lookup"><span data-stu-id="c9390-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="c9390-106">Azure Data Lake Store maakt gebruik van Azure Active Directory voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="c9390-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="c9390-107">Vóór het ontwerpen van een toepassing die met Azure Data Lake Store of Azure Data Lake Analytics werkt, moet u eerst beslissen hoe u wilt verifiëren van uw toepassing met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9390-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c9390-108">De twee belangrijkste opties zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="c9390-108">The two main options available are:</span></span>

* <span data-ttu-id="c9390-109">Verificatie van de eindgebruiker (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="c9390-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="c9390-110">Verificatie van service-tot-service</span><span class="sxs-lookup"><span data-stu-id="c9390-110">Service-to-service authentication</span></span>

<span data-ttu-id="c9390-111">Deze beide opties leiden in uw toepassing wordt geleverd met een OAuth 2.0-token, dat wordt gekoppeld aan elke aanvraag die zijn aangebracht in Azure Data Lake Store of Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c9390-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="c9390-112">Dit artikel vertelt over het maken van een **systeemeigen Azure AD-toepassing voor verificatie van de eindgebruiker**.</span><span class="sxs-lookup"><span data-stu-id="c9390-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="c9390-113">Zie voor instructies voor de configuratie van Azure AD-toepassing voor verificatie van de service to service [authentication Service-naar-service met Data Lake Store met Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c9390-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9390-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c9390-114">Prerequisites</span></span>
* <span data-ttu-id="c9390-115">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c9390-115">An Azure subscription.</span></span> <span data-ttu-id="c9390-116">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9390-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="c9390-117">Uw abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="c9390-117">Your subscription ID.</span></span> <span data-ttu-id="c9390-118">U kunt deze ophalen vanuit de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c9390-118">You can retrieve it from the Azure Portal.</span></span> <span data-ttu-id="c9390-119">Het is bijvoorbeeld beschikbaar op de blade Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="c9390-119">For example, it is available from the Data Lake Store account blade.</span></span>
  
    ![Abonnement-ID ophalen](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="c9390-121">De naam van uw Azure AD-domein.</span><span class="sxs-lookup"><span data-stu-id="c9390-121">Your Azure AD domain name.</span></span> <span data-ttu-id="c9390-122">U kunt deze ophalen door de muis in de rechterbovenhoek van de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="c9390-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure Portal.</span></span> <span data-ttu-id="c9390-123">Uit de onderstaande schermafbeelding de domeinnaam is **contoso.onmicrosoft.com**, en de GUID tussen vierkante haken is de tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="c9390-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span></span> 
  
    ![Ophalen van AAD-domein](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="c9390-125">Verificatie van de eindgebruiker</span><span class="sxs-lookup"><span data-stu-id="c9390-125">End-user authentication</span></span>
<span data-ttu-id="c9390-126">Dit is de aanbevolen aanpak als u wilt dat een eindgebruiker zich aanmelden bij uw toepassing via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9390-126">This is the recommended approach if you want an end-user to log in to your application via Azure AD.</span></span> <span data-ttu-id="c9390-127">Uw toepassing zich voor toegang tot Azure-resources met hetzelfde niveau van toegang als de eindgebruiker die in het logboek geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="c9390-127">Your application will be able to access Azure resources with the same level of access as the end-user that logged in.</span></span> <span data-ttu-id="c9390-128">U moet uw eindgebruikers hun referenties periodiek in volgorde voor uw toepassing toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="c9390-128">Your end-user will need to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="c9390-129">Het resultaat van de eindgebruiker zich aanmeldt met is dat uw toepassing een toegangstoken en een vernieuwingstoken wordt gegeven.</span><span class="sxs-lookup"><span data-stu-id="c9390-129">The result of having the end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="c9390-130">Het toegangstoken opgehaald gekoppeld aan elke aanvraag die wijzigingen in Data Lake Store of de Data Lake Analytics en het één uur standaard geldig is.</span><span class="sxs-lookup"><span data-stu-id="c9390-130">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="c9390-131">Het vernieuwingstoken dat kan worden gebruikt voor het verkrijgen van een nieuw toegangstoken en is geldig voor maximaal twee weken standaard als u regelmatig gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c9390-131">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span></span> <span data-ttu-id="c9390-132">U kunt twee verschillende benaderingen voor eindgebruikers aanmelden.</span><span class="sxs-lookup"><span data-stu-id="c9390-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-the-oauth-20-pop-up"></a><span data-ttu-id="c9390-133">Met behulp van het pop-upvenster OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="c9390-133">Using the OAuth 2.0 pop-up</span></span>
<span data-ttu-id="c9390-134">Uw toepassing kan resulteren in een OAuth 2.0 autorisatie pop-upvenster waarin de eindgebruiker hun referenties kan opgeven.</span><span class="sxs-lookup"><span data-stu-id="c9390-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end-user can enter their credentials.</span></span> <span data-ttu-id="c9390-135">Dit pop-upvenster werkt ook met het proces van Azure AD tweeledige verificatie (2FA), indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c9390-135">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="c9390-136">Nog wordt niet in de Azure AD Authentication Library (ADAL) voor Python of Java ondersteund door deze methode.</span><span class="sxs-lookup"><span data-stu-id="c9390-136">This method is not yet supported in the Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="c9390-137">Rechtstreeks doorgeven in de referenties van gebruiker</span><span class="sxs-lookup"><span data-stu-id="c9390-137">Directly passing in user credentials</span></span>
<span data-ttu-id="c9390-138">Uw toepassing krijgt u de referenties van gebruiker rechtstreeks naar Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9390-138">Your application can directly provide user credentials to Azure AD.</span></span> <span data-ttu-id="c9390-139">Deze methode werkt alleen met een gebruikersaccount voor de organisatie-ID; het is niet compatibel met persoonlijke / 'live-ID' gebruikersaccounts, met inbegrip van die eindigt op @outlook.com of @live.com.</span><span class="sxs-lookup"><span data-stu-id="c9390-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com.</span></span> <span data-ttu-id="c9390-140">Deze methode is bovendien niet compatibel zijn met een gebruikersaccount waarvoor Azure AD tweeledige verificatie (2FA)).</span><span class="sxs-lookup"><span data-stu-id="c9390-140">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-to-use-this-approach"></a><span data-ttu-id="c9390-141">Wat moet ik gebruik deze benadering?</span><span class="sxs-lookup"><span data-stu-id="c9390-141">What do I need to use this approach?</span></span>
* <span data-ttu-id="c9390-142">Azure AD-domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="c9390-142">Azure AD domain name.</span></span> <span data-ttu-id="c9390-143">Dit staat al in de vereisten van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c9390-143">This is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="c9390-144">Azure AD **systeemeigen toepassing**</span><span class="sxs-lookup"><span data-stu-id="c9390-144">Azure AD **native application**</span></span>
* <span data-ttu-id="c9390-145">Toepassings-ID voor de systeemeigen Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="c9390-145">Application ID for the Azure AD native application</span></span>
* <span data-ttu-id="c9390-146">Omleidings-URI voor de systeemeigen Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="c9390-146">Redirect URI for the Azure AD native application</span></span>
* <span data-ttu-id="c9390-147">Gedelegeerde machtigingen instellen</span><span class="sxs-lookup"><span data-stu-id="c9390-147">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="c9390-148">Stap 1: Een systeemeigen Active Directory-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="c9390-148">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="c9390-149">Maak en configureer een systeemeigen Azure AD-toepassing voor de eindgebruiker verificatie met Azure Data Lake Store met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c9390-149">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="c9390-150">Zie voor instructies [maken van een Azure AD-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9390-150">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="c9390-151">Zorg ervoor dat u selecteert bij de instructies in de bovenstaande koppeling te volgen, **systeemeigen** voor toepassingstype, zoals wordt weergegeven in de onderstaande schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="c9390-151">While following the instructions at the above link, make sure you select **Native** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="c9390-152">![Web-app maken](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "systeemeigen app maken")</span><span class="sxs-lookup"><span data-stu-id="c9390-152">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="c9390-153">Stap 2: Ophalen van toepassings-id en omleidings-URI</span><span class="sxs-lookup"><span data-stu-id="c9390-153">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="c9390-154">Zie [de toepassings-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) voor het ophalen van de toepassings-id (oftewel de client-ID in de klassieke Azure portal) van de systeemeigen Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c9390-154">See [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the application id (also called the client ID in the Azure classic portal) of the Azure AD native application.</span></span>

<span data-ttu-id="c9390-155">Volg de onderstaande stappen voor het ophalen van de omleidings-URI.</span><span class="sxs-lookup"><span data-stu-id="c9390-155">To retrieve the redirect URI, follow the steps below.</span></span>

1. <span data-ttu-id="c9390-156">Selecteer in de Azure-Portal **Azure Active Directory**, klikt u op **App registraties**, en zoeken en klikt u op de systeemeigen Azure AD-toepassing die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c9390-156">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="c9390-157">Van de **instellingen** blade voor de toepassing, klikt u op **omleidings-URI's**.</span><span class="sxs-lookup"><span data-stu-id="c9390-157">From the **Settings** blade for the application, click **Redirect URIs**.</span></span>

    ![Get omleidings-URI](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="c9390-159">Kopieer de weergegeven waarde.</span><span class="sxs-lookup"><span data-stu-id="c9390-159">Copy the value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="c9390-160">Stap 3: Machtigingen voor het instellen</span><span class="sxs-lookup"><span data-stu-id="c9390-160">Step 3: Set permissions</span></span>

1. <span data-ttu-id="c9390-161">Selecteer in de Azure-Portal **Azure Active Directory**, klikt u op **App registraties**, en zoeken en klikt u op de systeemeigen Azure AD-toepassing die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c9390-161">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="c9390-162">Van de **instellingen** blade voor de toepassing, klikt u op **vereist machtigingen**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c9390-162">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span></span>

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="c9390-164">In de **API-toegang toevoegen** blade, klikt u op **selecteert u een API**, klikt u op **Azure Data Lake**, en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="c9390-164">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="c9390-166">In de **API-toegang toevoegen** blade, klikt u op **machtigingen selecteren**, schakel het selectievakje in zodat **volledige toegang tot Data Lake Store**, en klik vervolgens op **selecteren**.</span><span class="sxs-lookup"><span data-stu-id="c9390-166">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span></span>

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="c9390-168">Klik op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="c9390-168">Click **Done**.</span></span>

5. <span data-ttu-id="c9390-169">Herhaal de laatste twee stappen voor het verlenen van machtigingen voor **Windows Azure Service Management API** ook.</span><span class="sxs-lookup"><span data-stu-id="c9390-169">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="c9390-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9390-170">Next steps</span></span>
<span data-ttu-id="c9390-171">In dit artikel een systeemeigen Azure AD-toepassing hebt gemaakt en die worden verzameld door de informatie die u nodig hebt in uw clienttoepassingen te ontwerpen met behulp van de SDK voor .NET, Java SDK, REST-API, enzovoort. U kunt nu doorgaan met de volgende artikelen die communiceren over het gebruik van de Azure AD-webtoepassing eerst worden geverifieerd met Data Lake Store en andere bewerkingen uit te voeren in de store.</span><span class="sxs-lookup"><span data-stu-id="c9390-171">In this article you created an Azure AD native application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="c9390-172">Aan de slag met Azure Data Lake Store met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c9390-172">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="c9390-173">Aan de slag met Azure Data Lake Store met Java SDK</span><span class="sxs-lookup"><span data-stu-id="c9390-173">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="c9390-174">Aan de slag met Azure Data Lake Store met REST-API</span><span class="sxs-lookup"><span data-stu-id="c9390-174">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

