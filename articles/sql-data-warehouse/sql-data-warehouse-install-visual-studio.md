---
title: aaaInstall Visual Studio en SSDT voor SQL Data Warehouse | Microsoft Docs
description: Visual Studio en SQL Server Development Tools (SSDT) voor Azure SQL Data Warehouse installeren
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a>Visual Studio en SSDT voor SQL datawarehouse installeren
toodevelop toepassingen voor SQL Data Warehouse, wordt u aangeraden meest recente versie van Visual Studio Hallo Hallo meest recente versie van SQL Server Data Tools (SSDT).  Visual Studio 2013 Update 5 met SSDT wordt ook ondersteund voor compatibiliteit met eerdere versies.  

Met Visual Studio met SSDT kunt u toouse Hallo SQL Server Object Explorer toovisually verkennen tabellen, weergaven, opgeslagen procedures en veel meer objecten in uw SQL Data Warehouse, evenals een query's uitvoeren.

> [!NOTE]
> SQL Data Warehouse biedt nog geen ondersteuning voor Visual Studio-Database-projecten.  Deze functie wordt in een toekomstige versie toegevoegd.
> 
> 

## <a name="step-1-install-visual-studio"></a>Stap 1: Installeer Visual Studio
Volg deze koppelingen toodownload en installeer Visual Studio. Als u al hebt Visual Studio 2013 of hoger is geïnstalleerd, kunt u overslaan tooStep 2, SSDT installeren.

1. [Visual Studio downloaden][].
2. Ga als volgt Hallo [Visual Studio installeren] [ Installing Visual Studio] leiden op MSDN en kies de standaardconfiguraties Hallo.

## <a name="step-2-install-ssdt"></a>Stap 2: SSDT installeren
tooinstall SSDT voor Visual Studio kunt u controleren voor een SSDT-update van Visual Studio met de volgende stappen.

1. Klik in Visual Studio op **extra** / **uitbreidingen en Updates...** / **Updates**
2. Selecteer **Product Updates** (Productupdates) en zoek naar **Microsoft SQL Server Update for database tooling** (Microsoft SQL Server Update voor databasehulpprogramma's)

Als een update niet wordt gevonden, moet u de meest recente versie Hallo geïnstalleerd hebben.  tooconfirm SSDT is geïnstalleerd, klikt u op **Help** / **About Microsoft Visual Studio** en zoek naar SQL Server Data Tools in Hallo-lijst.  Hallo meest recente versie van SSDT is 14.0.60525.0.  Als Hallo optie tooinstall niet beschikbaar vanuit Visual Studio is, u kunt ook kunt u bezoeken Hallo [SSDT downloaden] [ SSDT Download] toodownload pagina en SSDT handmatig installeren.

## <a name="next-steps"></a>Volgende stappen
Nu dat u hebt de nieuwste versie van SSDT hello, bent u klaar te[verbinding] [ connect] tooyour SQL Data Warehouse.

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Visual Studio downloaden]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
