---
title: aaaAdd Azure Storage met behulp van verbonden Services in Visual Studio | Microsoft Docs
description: Azure Storage tooyour app toevoegen met behulp van Hallo Visual Studio verbonden dialoogvenster Services toevoegen
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Azure-opslag toe te voegen met behulp van Visual Studio verbonden Services
Met Visual Studio, kunt u een van de volgende tooAzure opslag met behulp van Hallo Hallo **verbonden Services toevoegen** dialoogvenster:

- C#-cloudservice
- .NET-back-end voor mobiele service
- ASP.NET-website of service
- ASP.NET Core-service
- Azure webtaak-service 

Hallo verbonden service functionaliteit voegt alle verwijzingen Hallo nodig en verbinding tooyour CodeProject en de configuratiebestanden op de juiste wijze wordt gewijzigd. 

Na voltooiing wordt Hallo **verbonden Services toevoegen** dialoogvenster documentatie met gedetailleerde informatie over Hallo stappen vereist toostart werken met blob-opslag, wachtrijen en tabellen automatisch weergegeven.

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a>Verbinding maken met tooAzure Storage Hallo verbonden Services met dialoogvenster
1. Open het project in Visual Studio

1. In **Solution Explorer**, klik met de rechtermuisknop Hallo **verbonden Services** knooppunt en klik in het contextmenu Hallo en selecteer **verbonden Service toevoegen**.
   
    ![Toevoegen van Azure service verbonden](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. In Hallo **verbonden Services** pagina **Cloud-opslag met Azure Storage**.
   
    ![Azure-opslag toevoegen](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. In Hallo **Azure Storage** dialoogvenster, selecteer een bestaand opslagaccount en selecteert u **toevoegen**.
   
    Als u een opslagaccount toocreate nodig hebt, gaat u toohello volgende stap. Ga anders verder toostep 6.
    
    ![Bestaande opslag account tooproject toevoegen](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. een opslagaccount toocreate: 
   
   1. Selecteer **een nieuw Opslagaccount maken** Hallo Hallo dialoogvenster onderaan in.

   1. Hallo invullen **Storage-Account maken** dialoogvenster en selecteer **maken**.
      
       ![Nieuwe Azure storage-account](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Wanneer Hallo **Azure Storage** dialoogvenster wordt weergegeven, Hallo nieuw opslagaccount wordt weergegeven in de lijst Hallo. Selecteer Nieuw opslagaccount Hallo in Hallo lijst, en selecteer **toevoegen**.

1. opslag gekoppelde service wordt weergegeven onder Hallo Hallo **Serviceverwijzingen** knooppunt van uw project.
   
## <a name="how-your-project-is-modified"></a>Hoe uw project is gewijzigd
Wanneer u klaar bent met Hallo dialoogvenster, wordt in Visual Studio verwijzingen worden toegevoegd en bepaalde configuratiebestanden wijzigt. Hallo specifieke wijzigingen, is afhankelijk van het projecttype Hallo: 

- ASP.NET-project - [wat is er gebeurd – ASP.NET-projecten](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- ASP.NET Core project - [wat is er gebeurd – ASP.NET 5-projecten](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- Cloudserviceproject (webrollen en werkrollen) - [wat is er gebeurd – Cloud Service-projecten](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- Webtaak project - [wat is er gebeurd - webtaak projecten](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>Volgende stappen
- [MSDN-Forum: Azure-opslag](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Blog van Microsoft Azure Storage-Team](http://blogs.msdn.com/b/windowsazurestorage/)
- [Documentatie bij Azure Storage](https://docs.microsoft.com/azure/storage/)
