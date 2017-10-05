---
title: Probleem bij het maken van een toepassing toepassingsproxy | Microsoft Docs
description: Het oplossen van problemen met het maken van toepassingen voor toepassingsproxy in de Azure AD-beheerportal
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: fe56f56162ba7186f1b660a5b44fcef38f1dee9d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="b1991-103">Probleem bij het maken van een toepassing toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="b1991-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="b1991-104">Hieronder ziet u enkele veelvoorkomende problemen face mensen bij het maken van een nieuwe toepassing proxy-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1991-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="b1991-105">Aanbevolen documenten</span><span class="sxs-lookup"><span data-stu-id="b1991-105">Recommended documents</span></span> 

<span data-ttu-id="b1991-106">Zie voor meer informatie over het maken van een toepassing toepassingsproxy via de beheerportal, [toepassingen publiceren met Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="b1991-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="b1991-107">Als u de stappen in dit document volgt en een fout bij het maken van de toepassing krijgt, Zie de foutdetails voor informatie en suggesties voor het oplossen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1991-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="b1991-108">De meeste foutberichten bevatten een voorgestelde oplossing.</span><span class="sxs-lookup"><span data-stu-id="b1991-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="b1991-109">Specifieke wat u moet controleren</span><span class="sxs-lookup"><span data-stu-id="b1991-109">Specific things to check</span></span>

<span data-ttu-id="b1991-110">Controleer of algemene fouten te voorkomen:</span><span class="sxs-lookup"><span data-stu-id="b1991-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="b1991-111">U bent een beheerder met een machtiging voor het maken van een toepassing toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="b1991-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="b1991-112">De interne URL is uniek.</span><span class="sxs-lookup"><span data-stu-id="b1991-112">The internal URL is unique</span></span>

-   <span data-ttu-id="b1991-113">De externe URL is uniek.</span><span class="sxs-lookup"><span data-stu-id="b1991-113">The external URL is unique</span></span>

-   <span data-ttu-id="b1991-114">De URL's met http of https beginnen en eindigen met een "/"</span><span class="sxs-lookup"><span data-stu-id="b1991-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="b1991-115">De URL moet een domeinnaam zijn en niet een IP-adres</span><span class="sxs-lookup"><span data-stu-id="b1991-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="b1991-116">Het foutbericht moet worden weergegeven in de rechterbovenhoek bij het maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1991-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="b1991-117">U kunt ook het meldingspictogram voor de foutberichten selecteren.</span><span class="sxs-lookup"><span data-stu-id="b1991-117">You can also select the notification icon to see the error messages.</span></span>

   ![Prompt voor melding](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="b1991-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1991-119">Next steps</span></span>
[<span data-ttu-id="b1991-120">Toepassingsproxy inschakelen in de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b1991-120">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
