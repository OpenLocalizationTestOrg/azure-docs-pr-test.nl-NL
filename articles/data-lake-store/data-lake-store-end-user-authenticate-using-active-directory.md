---
title: 'Verificatie van de eindgebruiker: Data Lake Store met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooachieve eindgebruiker verificatie met Data Lake Store met Azure Active Directory
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
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="f4f03-103">Verificatie van de eindgebruiker met Data Lake Store met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4f03-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4f03-104">Verificatie van service-tot-service</span><span class="sxs-lookup"><span data-stu-id="f4f03-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="f4f03-105">Verificatie van de eindgebruiker</span><span class="sxs-lookup"><span data-stu-id="f4f03-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="f4f03-106">Azure Data Lake Store maakt gebruik van Azure Active Directory voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="f4f03-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="f4f03-107">Vóór het ontwerpen van een toepassing die met Azure Data Lake Store of Azure Data Lake Analytics werkt, moet u eerst beslissen hoe u tooauthenticate wilt dat uw toepassing met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4f03-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f4f03-108">Hallo twee belangrijkste opties zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="f4f03-108">hello two main options available are:</span></span>

* <span data-ttu-id="f4f03-109">Verificatie van de eindgebruiker (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="f4f03-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="f4f03-110">Verificatie van service-tot-service</span><span class="sxs-lookup"><span data-stu-id="f4f03-110">Service-to-service authentication</span></span>

<span data-ttu-id="f4f03-111">Deze beide opties leiden in uw toepassing wordt geleverd met een OAuth 2.0-token, dat gekoppelde tooeach verzoek tooAzure Data Lake Store of Azure Data Lake Analytics opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f4f03-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="f4f03-112">Dit artikel vertelt over het maken van een **systeemeigen Azure AD-toepassing voor verificatie van de eindgebruiker**.</span><span class="sxs-lookup"><span data-stu-id="f4f03-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="f4f03-113">Zie voor instructies voor de configuratie van Azure AD-toepassing voor verificatie van de service to service [authentication Service-naar-service met Data Lake Store met Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="f4f03-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4f03-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f4f03-114">Prerequisites</span></span>
* <span data-ttu-id="f4f03-115">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f4f03-115">An Azure subscription.</span></span> <span data-ttu-id="f4f03-116">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4f03-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="f4f03-117">Uw abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="f4f03-117">Your subscription ID.</span></span> <span data-ttu-id="f4f03-118">U kunt het ophalen van hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="f4f03-118">You can retrieve it from hello Azure Portal.</span></span> <span data-ttu-id="f4f03-119">Het is bijvoorbeeld beschikbaar vanuit de blade Hallo Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="f4f03-119">For example, it is available from hello Data Lake Store account blade.</span></span>
  
    ![Abonnement-ID ophalen](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="f4f03-121">De naam van uw Azure AD-domein.</span><span class="sxs-lookup"><span data-stu-id="f4f03-121">Your Azure AD domain name.</span></span> <span data-ttu-id="f4f03-122">U kunt deze ophalen door zwevende Hallo muis in Hallo rechterbovenhoek Hallo Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="f4f03-122">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure Portal.</span></span> <span data-ttu-id="f4f03-123">Van Hallo onderstaande schermafbeelding Hallo domeinnaam is **contoso.onmicrosoft.com**, en Hallo GUID tussen vierkante haken is Hallo tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="f4f03-123">From hello screenshot below, hello domain name is **contoso.onmicrosoft.com**, and hello GUID within brackets is hello tenant ID.</span></span> 
  
    ![Ophalen van AAD-domein](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="f4f03-125">Verificatie van de eindgebruiker</span><span class="sxs-lookup"><span data-stu-id="f4f03-125">End-user authentication</span></span>
<span data-ttu-id="f4f03-126">Dit is Hallo benadering wordt aanbevolen als u wilt dat een eindgebruiker toolog in tooyour toepassing via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4f03-126">This is hello recommended approach if you want an end-user toolog in tooyour application via Azure AD.</span></span> <span data-ttu-id="f4f03-127">Uw toepassing worden kunnen tooaccess Azure-resources met Hallo hetzelfde niveau van toegang als Hallo eindgebruikers die in het logboek geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="f4f03-127">Your application will be able tooaccess Azure resources with hello same level of access as hello end-user that logged in.</span></span> <span data-ttu-id="f4f03-128">De eindgebruiker moet tooprovide hun referenties periodiek in volgorde voor uw toepassing toomaintain toegang.</span><span class="sxs-lookup"><span data-stu-id="f4f03-128">Your end-user will need tooprovide their credentials periodically in order for your application toomaintain access.</span></span>

<span data-ttu-id="f4f03-129">Hallo-resultaat van het Hallo eindgebruiker zich aanmeldt met is dat uw toepassing een toegangstoken en een vernieuwingstoken wordt gegeven.</span><span class="sxs-lookup"><span data-stu-id="f4f03-129">hello result of having hello end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="f4f03-130">Hallo toegangstoken opgehaald gekoppelde tooeach verzoek tooData Lake Store of Data Lake Analytics en het één uur standaard geldig is.</span><span class="sxs-lookup"><span data-stu-id="f4f03-130">hello access token gets attached tooeach request made tooData Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="f4f03-131">Hallo-vernieuwingstoken mag gebruikte tooobtain en een nieuw toegangstoken is geldig voor up tootwo weken standaard als u regelmatig gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f4f03-131">hello refresh token can be used tooobtain a new access token, and it is valid for up tootwo weeks by default, if used regularly.</span></span> <span data-ttu-id="f4f03-132">U kunt twee verschillende benaderingen voor eindgebruikers aanmelden.</span><span class="sxs-lookup"><span data-stu-id="f4f03-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-hello-oauth-20-pop-up"></a><span data-ttu-id="f4f03-133">Met behulp van OAuth 2.0 Hallo pop-upvenster</span><span class="sxs-lookup"><span data-stu-id="f4f03-133">Using hello OAuth 2.0 pop-up</span></span>
<span data-ttu-id="f4f03-134">Uw toepassing kan resulteren in een OAuth 2.0 autorisatie pop-upvenster in welke Hallo eindgebruikers hun referenties kan opgeven.</span><span class="sxs-lookup"><span data-stu-id="f4f03-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which hello end-user can enter their credentials.</span></span> <span data-ttu-id="f4f03-135">Dit pop-upvenster werkt ook met hello Azure AD tweeledige verificatie (2FA) proces, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="f4f03-135">This pop-up also works with hello Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4f03-136">Deze methode is nog niet ondersteund in hello Azure AD Authentication Library (ADAL) voor Python of Java.</span><span class="sxs-lookup"><span data-stu-id="f4f03-136">This method is not yet supported in hello Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="f4f03-137">Rechtstreeks doorgeven in de referenties van gebruiker</span><span class="sxs-lookup"><span data-stu-id="f4f03-137">Directly passing in user credentials</span></span>
<span data-ttu-id="f4f03-138">Uw toepassing kan de gebruiker referenties tooAzure AD rechtstreeks bieden.</span><span class="sxs-lookup"><span data-stu-id="f4f03-138">Your application can directly provide user credentials tooAzure AD.</span></span> <span data-ttu-id="f4f03-139">Deze methode werkt alleen met een gebruikersaccount voor de organisatie-ID; het is niet compatibel met persoonlijke / 'live-ID' gebruikersaccounts, met inbegrip van die eindigt op @outlook.com of @live.com. Deze methode is bovendien niet compatibel zijn met een gebruikersaccount waarvoor Azure AD tweeledige verificatie (2FA)).</span><span class="sxs-lookup"><span data-stu-id="f4f03-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com. Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-toouse-this-approach"></a><span data-ttu-id="f4f03-140">Wat kan ik deze benadering toouse nodig?</span><span class="sxs-lookup"><span data-stu-id="f4f03-140">What do I need toouse this approach?</span></span>
* <span data-ttu-id="f4f03-141">Azure AD-domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="f4f03-141">Azure AD domain name.</span></span> <span data-ttu-id="f4f03-142">Dit al wordt vermeld in de vereiste Hallo van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="f4f03-142">This is already listed in hello prerequisite of this article.</span></span>
* <span data-ttu-id="f4f03-143">Azure AD **systeemeigen toepassing**</span><span class="sxs-lookup"><span data-stu-id="f4f03-143">Azure AD **native application**</span></span>
* <span data-ttu-id="f4f03-144">Toepassings-ID voor de systeemeigen toepassing hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4f03-144">Application ID for hello Azure AD native application</span></span>
* <span data-ttu-id="f4f03-145">Omleidings-URI voor Hallo systeemeigen Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="f4f03-145">Redirect URI for hello Azure AD native application</span></span>
* <span data-ttu-id="f4f03-146">Gedelegeerde machtigingen instellen</span><span class="sxs-lookup"><span data-stu-id="f4f03-146">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="f4f03-147">Stap 1: Een systeemeigen Active Directory-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="f4f03-147">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="f4f03-148">Maak en configureer een systeemeigen Azure AD-toepassing voor de eindgebruiker verificatie met Azure Data Lake Store met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4f03-148">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="f4f03-149">Zie voor instructies [maken van een Azure AD-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4f03-149">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="f4f03-150">Zorg ervoor dat u selecteert bij het Hallo-instructies op Hallo hierboven koppeling te volgen, **systeemeigen** voor toepassingstype, zoals wordt weergegeven in onderstaande schermafbeelding voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4f03-150">While following hello instructions at hello above link, make sure you select **Native** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="f4f03-151">![Web-app maken](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "systeemeigen app maken")</span><span class="sxs-lookup"><span data-stu-id="f4f03-151">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="f4f03-152">Stap 2: Ophalen van toepassings-id en omleidings-URI</span><span class="sxs-lookup"><span data-stu-id="f4f03-152">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="f4f03-153">Zie [Hallo toepassings-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve Hallo toepassings-id (ook Hallo client-ID in de klassieke Azure-portal Hallo genoemd) van systeemeigen hello Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f4f03-153">See [Get hello application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello application id (also called hello client ID in hello Azure classic portal) of hello Azure AD native application.</span></span>

<span data-ttu-id="f4f03-154">tooretrieve Hallo omleidings-URI, volgt u onderstaande stappen voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4f03-154">tooretrieve hello redirect URI, follow hello steps below.</span></span>

1. <span data-ttu-id="f4f03-155">Selecteer in Azure Portal Hallo, **Azure Active Directory**, klikt u op **App registraties**, en zoeken en klikt u op systeemeigen hello Azure AD-toepassing die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f4f03-155">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="f4f03-156">Van Hallo **instellingen** blade voor de toepassing hello, klikt u op **omleidings-URI's**.</span><span class="sxs-lookup"><span data-stu-id="f4f03-156">From hello **Settings** blade for hello application, click **Redirect URIs**.</span></span>

    ![Get omleidings-URI](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="f4f03-158">Kopieer Hallo waarde weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f4f03-158">Copy hello value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="f4f03-159">Stap 3: Machtigingen voor het instellen</span><span class="sxs-lookup"><span data-stu-id="f4f03-159">Step 3: Set permissions</span></span>

1. <span data-ttu-id="f4f03-160">Selecteer in Azure Portal Hallo, **Azure Active Directory**, klikt u op **App registraties**, en zoeken en klikt u op systeemeigen hello Azure AD-toepassing die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f4f03-160">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="f4f03-161">Van Hallo **instellingen** blade voor de toepassing hello, klikt u op **vereist machtigingen**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f4f03-161">From hello **Settings** blade for hello application, click **Required permissions**, and then click **Add**.</span></span>

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="f4f03-163">In Hallo **API-toegang toevoegen** blade, klikt u op **selecteert u een API**, klikt u op **Azure Data Lake**, en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="f4f03-163">In hello **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="f4f03-165">In Hallo **API-toegang toevoegen** blade, klikt u op **machtigingen selecteren**, selecteer het selectievakje toogive Hallo **volledige toegang tot tooData Lake Store**, en klik vervolgens op **selecteren** .</span><span class="sxs-lookup"><span data-stu-id="f4f03-165">In hello **Add API Access** blade, click **Select permissions**, select hello check box toogive **Full access tooData Lake Store**, and then click **Select**.</span></span>

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="f4f03-167">Klik op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="f4f03-167">Click **Done**.</span></span>

5. <span data-ttu-id="f4f03-168">Herhaal Hallo laatste twee stappen toogrant machtigingen voor **Windows Azure Service Management API** ook.</span><span class="sxs-lookup"><span data-stu-id="f4f03-168">Repeat hello last two steps toogrant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="f4f03-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f4f03-169">Next steps</span></span>
<span data-ttu-id="f4f03-170">In dit artikel een systeemeigen Azure AD-toepassing hebt gemaakt en die worden verzameld door Hallo-informatie die u nodig hebt in uw clienttoepassingen te ontwerpen met behulp van de SDK voor .NET, Java SDK, REST-API, enzovoort. Nu kunt u verder toohello artikelen die praten over hoe toouse hello Azure AD web application toofirst verifiëren met Data Lake Store en andere bewerkingen uit te voeren op Hallo store te volgen.</span><span class="sxs-lookup"><span data-stu-id="f4f03-170">In this article you created an Azure AD native application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="f4f03-171">Aan de slag met Azure Data Lake Store met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f4f03-171">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="f4f03-172">Aan de slag met Azure Data Lake Store met Java SDK</span><span class="sxs-lookup"><span data-stu-id="f4f03-172">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="f4f03-173">Aan de slag met Azure Data Lake Store met REST-API</span><span class="sxs-lookup"><span data-stu-id="f4f03-173">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

