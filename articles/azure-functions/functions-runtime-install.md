---
title: Runtime-installatie van functies aaaAzure | Microsoft Docs
description: Hoe tooInstall hello Azure Functions-Runtime
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a>Hello Azure Functions-Runtime Preview installeren

Als u tooinstall hello Azure Functions-Runtime preview wilt, moet u deze stappen volgen:

1. Zorg ervoor dat uw machine voldoet aan de minimumvereisten Hallo
1. Hallo downloaden [Azure Functions-Runtime Preview Installer](https://aka.ms/azafr). 
1. Installeer hello Azure Functions-Runtime-preview
1. Configuratie van de volledige Hallo van hello Azure Functions-Runtime-preview

## <a name="prerequisites"></a>Vereisten

Voordat u hello Azure Functions-Runtime preview installeert, moet u de volgende Hallo hebben:

1. Een computer waarop Microsoft Windows Server 2016 of Microsoft Windows 10 auteurs Update (Professional of Enterprise Edition) wordt uitgevoerd.
1. Een exemplaar van SQL Server die in uw netwerk worden uitgevoerd.  Minimale versie vereiste is SQL Server Express.

## <a name="install-hello-azure-functions-runtime-preview"></a>Hello Azure Functions-Runtime Preview installeren

Hello Azure Functions-Runtime preview installatieprogramma leidt u door het Hallo-installatie van hello Azure Functions-Runtime preview beheer- en werkrollen.  Het is mogelijk tooinstall Hallo Management en een werkrol op Hallo dezelfde machine.  Echter, als u meer functies toevoegt, moet u implementeren meer werkrollen op extra computers toobe kunnen tooscale uw functies naar meerdere werknemers.

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a>Hallo Management en een Werkrol installeren op Hallo dezelfde machine

1. Hello Azure Functions-Runtime Preview installatieprogramma worden uitgevoerd.

    ![Azure Functions-Runtime Preview-installatieprogramma][1]

1. **Klik op volgende** vooraf voorbij de eerste fase Hallo van Hallo installer
1. Zodra u Hallo Hallo gebruiksvoorwaarden hebt gelezen **overeenkomst**, **Hallo selectievakje** tooaccept Hallo voorwaarden en **Klik op volgende** tooadvance.
1. Nu Selecteer rollen Hallo gewenste tooinstall op deze machine **functies Beheerrol** en/of **functies Werkrol** en **Klik op volgende**

    ![Azure Functions-Runtime Preview Installer - selectie van Systeemrol][3]

    > [!NOTE]
    > Kunt u Hallo installeren **functies Werkrol** op veel andere machines toodo geval is, volg deze instructies en selecteer alleen de **functies Werkrol** in Hallo-installatieprogramma.

1. **Klik op volgende** toohave hello **Azure Functions-Runtime-installatieprogramma** installeren op uw computer.
1. Zodra de volledige Hallo installatieprogramma start Hallo **Azure Functions-Runtime configuratiehulpprogramma**.

    ![Azure Functions-Runtime Preview installatieprogramma voltooid][5]

    > [!NOTE]
    > Als u wilt installeren op **Windows 10** en Hallo **Container** functie is niet eerder hebt ingeschakeld, hello **Azure Functions-Runtime** Installer vraagt u tooreboot uw machine toocomplete Hallo installeren.

## <a name="configure-hello-azure-functions-runtime"></a>Hello Azure Functions-Runtime configureren

toocomplete hello Azure Functions-Runtime-installatie moet u Hallo-configuratie voltooien.

1. Hallo **Azure Functions-Runtime-configuratieprogramma** ziet u welke functies op uw computer zijn geïnstalleerd.

    ![Azure Functions-Runtime Preview Configuration Tool][6]

1. Klik op Hallo **Database** tabblad, voert u Hallo **Verbindingsdetails voor uw SQL Server-exemplaar** en **Klik op toepassen**.  Dit is vereist in de volgorde toohello Azure Functions-Runtime toocreate een database toosupport Hallo Runtime.
    
    ![Azure Functions-Runtime Preview databaseconfiguratie][7]

1. Klik op Hallo **referenties** tabblad.  In dit scherm moet u twee nieuwe referenties voor gebruik met een bestandsshare maken voor het hosten van uw Azure Functions.  **Geef een gebruikersnaam en wachtwoord** combinaties van Hallo **Share bestandseigenaar** en voor Hallo **File Share gebruiker** en klik op **toepassen**.

    ![Azure Functions-Runtime Preview referenties][8]

1. Klik op Hallo **bestandsshare** tabblad.  In dit scherm Geef details op Hallo van Hallo **bestandsshare-locatie**.  Dit kan worden gemaakt voor u of u kunt een bestaande bestandsshare gebruiken en klik op **toepassen**.  Als u een nieuwe bestandsshare-locatie selecteert, moet u een map voor gebruik door hello Azure Functions-Runtime.
    
    ![Azure Functions-Runtime Preview-bestandsshare][9]

1. Klik op Hallo **IIS** tabblad.  Op dit tabblad Hallo worden details weergegeven van Hallo websites in IIS die hello Azure Functions-Runtime-installatie maakt.  **Klik op toepassen** toocomplete.

    ![Preview van Azure Functions-Runtime IIS][10]

1. Klik op Hallo **Services** tabblad.  Dit tabblad toont Hallo status van Hallo-services in uw Azure Functions-Runtime-installatie.  Als na de initiële configuratie Hallo **Activation-Service van Azure Functions Host** wordt niet uitgevoerd Klik **Service starten**

    ![Azure Functions-Runtime Preview Configruation voltooid][11]

1. Ten slotte bladeren toohello **Azure Functions-Runtime Portal** als`https://<machinename>/`

    ![Preview-Portal voor Azure Functions-Runtime][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png