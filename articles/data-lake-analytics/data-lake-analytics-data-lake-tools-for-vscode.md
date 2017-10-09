---
title: 'Azure Data Lake Tools: Gebruik Azure Data Lake Tools voor Visual Studio Code | Microsoft Docs'
description: 'Ontdek hoe toouse Azure Data Lake Tools voor Visual Studio Code toocreate, testen en U-SQL-scripts uitvoeren. '
Keywords: VScode, Azure Data Lake Tools, lokaal uitvoeren, lokale foutopsporing, lokale Debug preview opslagbestand uploaden toostorage pad
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Azure Data Lake Tools voor Visual Studio Code gebruiken

Ontdek hoe toouse Azure Data Lake Tools voor Visual Studio Code (VS-Code) toocreate, testen en U-SQL-scripts uitvoeren. Hallo-informatie wordt ook beschreven in Hallo video te volgen:

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>Vereisten

Data Lake Tools kan worden geïnstalleerd op Hallo platforms die worden ondersteund door VS-Code. Hallo ondersteunde platforms zijn Windows, Linux en Mac OS. Hallo verschillende platforms hebben Hallo volgende vereisten:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Java Runtime Environment voor SE versie 8 update 77 of hoger](https://java.com/download/manual.jsp). Hallo java.exe pad toohello system omgeving variabele pad toevoegen. Zie voor configuratie-instructies [hoe instellen of wijzigen van de padvariabele system Hallo ik?]( https://www.java.com/download/help/path.xml). Hallo-pad is vergelijkbaar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.
    - [.NET core SDK 1.0.3 of .NET Core 1.1 runtime](https://www.microsoft.com/net/download).
    
- Linux (We raden u aan Ubuntu 14.04 TNS)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx). tooinstall Hallo code, Voer Hallo volgende opdracht:

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/). 

        - tooupdate hello deb pakket bron, Voer Hallo volgende opdrachten:

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - tooinstall Mono, Voer Hallo volgende opdracht:

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Mono 4.6 wordt niet ondersteund. Versie 4.6 verwijderen volledig voordat u 4.2.x installeert.  

        - [Java Runtime Environment voor SE versie 8 update 77 of hoger](https://java.com/download/manual.jsp). Zie voor instructies voor installatie, Hallo [Linux 64-bits installatie-instructies voor Java]( https://java.com/en/download/help/linux_x64_install.xml) pagina.
        - [.NET core SDK 1.0.3 of .NET Core 1.1 runtime](https://www.microsoft.com/net/download).
- MacOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/). 
    - [Java Runtime Environment voor SE versie 8 update 77 of hoger](https://java.com/download/manual.jsp). Zie voor instructies voor installatie, Hallo [Linux 64-bits installatie-instructies voor Java](https://java.com/en/download/help/mac_install.xml) pagina.
    - [.NET core SDK 1.0.3 of .NET Core 1.1 runtime](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Installeren van Data Lake Tools

Nadat u Hallo vereisten hebt geïnstalleerd, kunt u Data Lake Tools voor VS-Code installeren.

**tooinstall Data Lake Tools**

1. Open Visual Studio Code.
2. Ctrl + P selecteren en voer vervolgens Hallo volgende opdracht:
```
ext install usql-vscode-ext
```
Hier ziet u een lijst met Visual Studio code-uitbreidingen. Een van beide is **Azure Data Lake Tools**.

3. Selecteer **installeren** volgende te**Azure Data Lake Tools**. Na enkele seconden Hallo **installeren** wijzigingen te knop**opnieuw laden**.
4. Selecteer **opnieuw laden** tooactivate Hallo-extensie.
5. Selecteer **OK** tooconfirm. U kunt Azure Data Lake Tools zien in Hallo **extensies** deelvenster.
    ![Data Lake Tools voor Visual Studio Code Extensions deelvenster](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Azure Data Lake Tools activeren
Maak een nieuw .usql-bestand of open een bestaande .usql tooactivate Hallo bestandsextensie. 

## <a name="connect-tooazure"></a>Verbinding maken met tooAzure

Voordat u kunt compileren en U-SQL-scripts in Data Lake Analytics uitvoeren, moet u verbinding maken met tooyour Azure-account.

**tooconnect tooAzure**

1.  Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet. 
2.  Voer **ADL: aanmelding**. Hallo-aanmeldingsgegevens wordt weergegeven in Hallo **uitvoer** deelvenster.

    ![Data Lake Tools voor Visual Studio Code opdracht palet](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Data Lake Tools voor Visual Studio Code aanmelding apparaatgegevens](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. Selecteer Ctrl + klikken op Hallo aanmeldings-URL: https://aka.ms/devicelogin tooopen Hallo aanmelding webpagina. Voer de code Hallo **G567LX42V** in het tekstvak Hallo en selecteer vervolgens **doorgaan**.

   ![Data Lake Tools voor Visual Studio Code aanmelding plakken code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  Volg Hallo instructies toosign in van Hallo webpagina. Wanneer u verbonden bent, de naam van uw Azure-account wordt weergegeven op de statusbalk Hallo in Hallo linkerbenedenhoek Hallo **tegenover Code** venster. 

    > [!NOTE] 
    > Als uw account twee factoren is ingeschakeld heeft, wordt u aangeraden phone verificatie in plaats van met een PINCODE te gebruiken.

toosign, Voer Hallo opdracht **ADL: afmelding**.

## <a name="list-your-data-lake-analytics-accounts"></a>Lijst van uw Data Lake Analytics-accounts

tootest hello verbinding get een lijst van uw Data Lake Analytics-accounts.

**toolist hello Data Lake Analytics-accounts onder uw Azure-abonnement**

1. Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.
2. Voer **ADL: lijst van Accounts**. Hallo-accounts worden weergegeven in Hallo **uitvoer** deelvenster.

## <a name="open-hello-sample-script"></a>Open Hallo-voorbeeldscript
Open Hallo opdracht palet (Ctrl + Shift + P) en voer de **ADL: Open voorbeeldscript**. Hiermee opent u een ander exemplaar van dit voorbeeld. U kunt bewerken, configureren en verzenden van script op basis van dit exemplaar.

## <a name="work-with-u-sql"></a>Werken met U-SQL

U moet een U-SQL-bestand of een map toowork openen met U-SQL.

**tooopen een map voor uw project U-SQL**

1. Selecteer in Visual Studio Code Hallo **bestand** menu en selecteer vervolgens **map openen**.
2. Geef een map op en selecteer vervolgens **map selecteren**.
3. Selecteer Hallo **bestand** menu en selecteer vervolgens **nieuw**. Een naamloos-1-bestand wordt toohello project toegevoegd.
4. Voer Hallo code in Hallo naamloos-1-bestand te volgen:

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    Hallo script maakt een bestand departments.csv met enkele gegevens die zijn opgenomen in Hallo/output-map.

5. Hallo bestand opslaan als **myUSQL.usql** in Hallo map geopend. Een configuratiebestand adltools_settings.json is ook toohello project toegevoegd.
4. Open en adltools_settings.json configureren met Hallo volgende eigenschappen:

    - Account: Een Data Lake Analytics-account onder uw Azure-abonnement.
    - Database: Een database onder uw account. Hallo standaardwaarde is **master**.
    - Schema: Een schema op uw database. Hallo standaardwaarde is **dbo**.
    - Optionele instellingen:
        - Prioriteit: Hallo prioriteitsbereik is 1 too1000 met 1 Hallo hoogste prioriteit. de standaardwaarde Hallo is **1000**.
        - Parallelle uitvoering: Hallo parallelle uitvoering bereik is 1 too150. de standaardwaarde Hallo is Hallo maximale parallelle uitvoering toegestaan in uw Azure Data Lake Analytics-account. 
        
        > [!NOTE] 
        > Als Hallo-instellingen ongeldige zijn, worden Hallo standaardwaarden gebruikt.

    ![Data Lake Tools voor Visual Studio Code-configuratiebestand](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Een compute Data Lake Analytics-account is nodig toocompile en voer U-SQL-taken. Voordat u deze kunt compileren en U-SQL-taken uitvoeren, moet u de computeraccount Hallo configureren.
    
Nadat het Hallo-configuratie is opgeslagen, wordt op Hallo statusbalk Hallo linkerbenedenhoek van het bijbehorende .usql bestand Hallo Hallo-account, database en schema-informatie weergegeven. 
 
 
Vergeleken tooopening een bestand, wanneer u een map die u kunt openen:

- Gebruik een code-behind-bestand. Code-behind wordt niet ondersteund in de modus Hallo één bestand.
- Gebruik een configuratiebestand. Wanneer u een map opent, delen Hallo-scripts in Hallo werkdirectory een enkel configuratiebestand.


Hallo U-SQL-script wordt gecompileerd op afstand via Hallo Data Lake Analytics-service. Wanneer u de opdracht Hallo **compileren** opdracht Hallo U-SQL-script tooyour Data Lake Analytics-account wordt verzonden. Visual Studio Code ontvangt later Hallo compilatieresultaat. Vervaldatum toohello externe compilatie vereist Visual Studio Code dat u gegevens weer te geven Hallo tooconnect tooyour Data Lake Analytics-account in het Hallo-configuratiebestand.

**toocompile een U-SQL-script**

1. Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet. 
2. Voer **ADL: compileren van Script**. Hallo compileren resultaten worden weergegeven in Hallo **uitvoer** venster. U kunt ook met de rechtermuisknop op een scriptbestand en selecteer vervolgens **ADL: compileren Script** toocompile een U-SQL-taak. Hallo compilatieresultaat wordt weergegeven in Hallo **uitvoer** deelvenster.
 

**toosubmit een U-SQL-script**

1. Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet. 
2. Voer **ADL: verzenden van taak**.  U kunt ook met de rechtermuisknop op een scriptbestand en selecteer vervolgens **ADL: Submit Job**. 

Nadat u een U-SQL-taak hebt ingediend, Hallo verzending van Logboeken worden weergegeven in Hallo **uitvoer** venster in VS-Code. Hallo taak URL wordt ook weergegeven als Hallo verzending geslaagd is. U kunt Hallo taak URL openen in een web browser tootrack Hallo realtime taakstatus.

tooenable hello uitvoer van de taakdetails hello, stel **jobInformationOutputPath** in Hallo **tegenover code voor u Hallo-sql_settings.json** bestand.
 
## <a name="use-a-code-behind-file"></a>Een code-behind-bestand gebruiken

Een code-behind-bestand is een C#-bestanden die zijn gekoppeld aan een enkel U-SQL-script. U kunt een specifiek script tooUDO, UDA, UDT en UDF definiëren in Hallo code-behind-bestand. Hallo kunnen UDO, UDA, UDT en UDF worden gebruikt rechtstreeks in Hallo script zonder Hallo assembly eerst registreren. Hallo code-behind-bestand wordt geplaatst in Hallo dezelfde map als de peering U-SQL-scriptbestand. Hallo script heet xxx.usql, heet Hallo code-behind als xxx.usql.cs. Als u Hallo code-behind-bestand voor het handmatig verwijdert, worden Hallo code-behind functie is uitgeschakeld voor de bijbehorende U-SQL-script. Zie voor meer informatie over het schrijven van code voor de U-SQL-script klant [schrijven en met behulp van aangepaste Code in de U-SQL: door de gebruiker gedefinieerde functies]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).

toosupport code-behind, moet u een werkmap openen. 

**toogenerate een code-behind-bestand**

1. Open een bronbestand. 
2. Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.
3. Voer **ADL: genereren van Code achter**. Een code-behind-bestand wordt gemaakt in Hallo dezelfde map. 

U kunt ook met de rechtermuisknop op een scriptbestand en selecteer vervolgens **ADL: Code genereren achter**. 

toocompile en het verzenden van een U-SQL-script met een code-behind-bestand is hetzelfde als het script bestand met de Hallo zelfstandige U-SQL Hallo.

Hallo na twee schermafbeeldingen weergeven een code-behind-bestand en het bijbehorende bestand van de U-SQL-script:
 
![Data Lake Tools voor Visual Studio Code code-behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools voor Visual Studio Code code-behind scriptbestand](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>Assembly's gebruiken

Zie voor meer informatie over het ontwikkelen van assembly's [ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-assemblies.md).

U kunt Data Lake Tools tooregister aangepaste code assembly's in Hallo Data Lake Analytics-catalogus.

**tooregister een assembly**

U kunt registreren assembly via Hallo Hallo **ADL: registreren Assembly** of **ADL: Assembly registreren via configuratie** opdrachten.

**tooregister via Hallo ADL: registreren Assembly-opdracht**
1.  Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.
2.  Voer **ADL: Assembly registreren**. 
3.  Hallo lokale assembly-pad opgeven. 
4.  Selecteer een Data Lake Analytics-account.
5.  Selecteer een database.

Resultaten: Hallo portal wordt geopend in een browser en Hallo assembly registratieproces wordt weergegeven.  

Een andere handige manier tootrigger hello **ADL: registreren Assembly** opdracht is tooright en klik op Hallo dll-bestand in Verkenner. 

**tooregister Hallo echter ADL: Assembly registreren via de opdracht configuratie**
1.  Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.
2.  Voer **ADL: Assembly via configuratie registreren**. 
3.  Hallo lokale assembly-pad opgeven. 
4.  Hallo JSON-bestand wordt weergegeven. Bekijk en bewerk Hallo assembly-afhankelijkheden en Resourceparameters, indien nodig. Instructies worden weergegeven in Hallo **uitvoer** venster. tooproceed toohello assembly-registratie, sla Hallo JSON-bestand (Ctrl + S).

![Data Lake Tools voor Visual Studio Code code-behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- Assembly-afhankelijkheden: een Azure Data Lake Tools of Hallo DLL eventuele afhankelijkheden heeft. Hallo afhankelijkheden worden weergegeven in de JSON-bestand Hallo nadat ze zijn gedetecteerd. 
>- Resources: U kunt uw resources dll-bestand (bijvoorbeeld, txt, PNG en CSV) als onderdeel van de registratie van assembly Hallo uploaden. 

Een andere manier tootrigger hello **ADL: Assembly registreren via configuratie** opdracht is tooright en klik op Hallo dll-bestand in Verkenner. 

Hallo volgende U-SQL-code laat zien hoe toocall een assembly. In voorbeeld Hallo Hallo assembly-naam is *testen*.

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a>Toegang tot Hallo Data Lake Analytics-catalogus

Wanneer u tooAzure hebt gekoppeld, kunt u Hallo stappen tooaccess Hallo U-SQL-catalogus te volgen.

**tooaccess hello Azure Data Lake Analytics-metagegevens**

1.  Ctrl + Shift + P selecteren en voer vervolgens **ADL: lijst met tabellen**.
2.  Selecteer een van de Hallo Data Lake Analytics-accounts.
3.  Selecteer een van de Hallo Data Lake Analytics-databases.
4.  Selecteer een van de Hallo schema's. Hier ziet u Hallo lijst met tabellen.

## <a name="view-data-lake-analytics-jobs"></a>Weergave Data Lake Analytics-taken

**tooview Data Lake Analytics-taken**
1.  Open Hallo opdracht palet (Ctrl + Shift + P) en selecteer **ADL: taak weergeven**. 
2.  Selecteer een Data Lake Analytics of lokale account. 
3.  Wacht totdat de lijst met de Hallo taken voor Hallo account tooappear.
4.  Selecteer een taak in de lijst om de taak, Data Lake Tools taakdetails Hallo in hello Azure-portal wordt geopend en toont Hallo Taakinfo-bestand in VS-Code.

![Data Lake Tools voor Visual Studio Code IntelliSense objecttypen](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Azure Data Lake Storage-integratie

U kunt Azure Data Lake Storage-gerelateerde opdrachten te gebruiken:
 - Blader door hello Azure Data Lake Storage-resources. 
 - Preview hello Azure Data Lake Storage-bestand.  
 - Hallo uploaden bestand rechtstreeks tooAzure Data Lake Storage in VS-Code. 

### <a name="list-hello-storage-path"></a>Lijst Hallo opslagpad 
Hallo opslagpad via Hallo opdracht palet of met de rechtermuisknop klikt, kunt u weergeven.

**toolist hello opslagpad via Hallo opdracht palet**

1.  Open Hallo opdracht palet (Ctrl + Shift + P) en voer de **ADL: lijst opslagpad**.

    ![Data Lake Tools voor Visual Studio Code lijst opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Selecteer uw favoriete methode voor het Hallo-opslagpad aanbieden. Maakt gebruik van deze overgang **Geef een pad** als voorbeeld.

    ![Data Lake Tools voor Visual Studio Code eenrichtingssessie toolist Hallo opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- VS-Code, blijft Hallo laatst bezochte pad in elke Data Lake Analytics-account. Bijvoorbeeld: ss tt /.
    >- Hoofdpad naar browser: pad naar de hoofdmap Hallo lijst van de geselecteerde Data Lake Analytics-account of een lokaal pad.
    >- Geef een pad op: een opgegeven pad van de geselecteerde Data Lake Analytics-account of een lokaal pad.
    
3. Selecteer een account in Hallo lokaal pad of een Data Lake Analytics-account.

    ![Data Lake Tools voor Visual Studio Code selecteren meer](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. Selecteer **meer** toolist meer Data Lake Analytics-accounts en selecteer vervolgens een Data Lake Analytics-account.

    ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Geef het pad van een Azure-opslag. Bijvoorbeeld: / uitvoer.

    ![Data Lake Tools voor Visual Studio Code invoeren opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  Resultaten: Hallo opdracht palet bevat Hallo padinformatie op basis van uw gegevens.

    ![Data Lake Tools voor Visual Studio Code weergeven opslag pad resultaten](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Een handige methode toolist Hallo relatief pad wordt via Hallo met de rechtermuisknop op contextmenu.

**toolist hello opslagpad via met de rechtermuisknop op**

1.  Met de rechtermuisknop op Hallo pad tekenreeks tooselect **lijst opslagpad**.

       ![Data Lake Tools voor Visual Studio Code met de rechtermuisknop op contextmenu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. Hallo geselecteerde relatief pad wordt weergegeven in Hallo opdracht palet.

   ![Data Lake Tools voor Visual Studio Code relatief pad zijn geselecteerd](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Selecteer een account in Hallo lokaal pad of een Data Lake Analytics-account.

       ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  Resultaten: Hallo opdracht palet bevat Hallo mappen en bestanden voor de huidige pad Hallo.

       ![Data Lake Tools voor Visual Studio Code lijst van de huidige pad Hallo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a>Hallo-opslagbestand Preview
Hallo opslagbestand via Hallo opdracht palet of met de rechtermuisknop klikt, kunt u bekijken.

**toopreview hello opslagbestand via Hallo opdracht palet**

1.  Open Hallo opdracht palet (Ctrl + Shift + P) en voer de **ADL: Preview opslagbestand**.

       ![Data Lake Tools voor Visual Studio Code preview opslagbestand](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Selecteer een account in Hallo lokaal pad of een Data Lake Analytics-account.

       ![Data Lake Tools voor Visual Studio Code lijst account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Selecteer **meer** toolist meer Data Lake Analytics-accounts en selecteer vervolgens een Data Lake Analytics-account.

       ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Voer een pad van de Azure-opslag of het bestand. Bijvoorbeeld: /output/SearchLog.txt.

       ![Data Lake Tools voor Visual Studio Code invoeren opslagpad en bestandsnaam](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  Resultaten: Hallo opdracht palet bevat Hallo padinformatie op basis van uw gegevens.

       ![Data Lake Tools voor Visual Studio Code voorbeeld bestandsresultaat](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**toolist hello opslagpad via met de rechtermuisknop op**

1.  toopreview een bestand met de rechtermuisknop op Hallo bestandspad.

   ![Data Lake Tools voor Visual Studio Code met de rechtermuisknop op contextmenu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Selecteer een account in Hallo lokaal pad of een Data Lake Analytics-account.

       ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Resultaten: VS-Code weergegeven Hallo voorbeeldresultaten van Hallo-bestand.

       ![Data Lake Tools voor Visual Studio Code voorbeeld bestandsresultaat](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>Bestand uploaden 

U kunt bestanden uploaden door te voeren Hallo opdrachten **ADL: uploaden** of **ADL:-bestand uploaden via configuratie**.

**tooupload bestanden echter Hallo ADL: de opdracht-bestand uploaden**
1. Ctrl + Shift + P tooopen Hallo opdracht palet selecteren of met de rechtermuisknop op Hallo scripteditor en voer vervolgens **-bestand uploaden**.
2.  Hallo tooupload bestand, voert u een lokaal pad.

    ![Data Lake Tools voor Visual Studio Code opgeven lokaal pad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. Selecteer een van de aanbieding Hallo opslagpad Hallo manieren. Maakt gebruik van deze overgang **Geef een pad** als voorbeeld.

    ![Data Lake Tools voor Visual Studio Code lijst opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- VS-Code, blijft Hallo laatst bezochte pad in elke Data Lake Analytics-account. Bijvoorbeeld: ss tt /.
    >- Hoofdpad naar browser: pad naar de hoofdmap Hallo lijst van de geselecteerde Data Lake Analytics-account of een lokaal pad.
    >- Geef een pad op: een opgegeven pad van de geselecteerde Data Lake Analytics-account of een lokaal pad.

4. Selecteer een account in Hallo lokaal pad of een Data Lake Analytics-account.

    ![Data Lake Tools voor Visual Studio Code met de rechtermuisknop op de opslag](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Geef het pad van een Azure-opslag. Bijvoorbeeld: / uitvoer.

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Uw Azure-opslag-pad vinden. Selecteer **de huidige map kiezen**.

    ![Selecteer een map van Data Lake Tools voor Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  Resultaten: Hallo **uitvoer** venster Hallo-bestand Uploadstatus wordt weergegeven.

       ![Data Lake Tools voor Visual Studio Code Uploadstatus](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**Hoewel Hallo ADL tooupload bestanden: configuratie opdracht-bestand uploaden**
1.  Ctrl + Shift + P tooopen Hallo opdracht palet selecteren of met de rechtermuisknop op Hallo scripteditor en voer vervolgens **-bestand uploaden via configuratie**.
2.  VS-Code wordt een JSON-bestand weergegeven. U kunt invoeren bestandspaden en meerdere bestanden op Hallo uploaden hetzelfde moment. Instructies worden weergegeven in Hallo **uitvoer** venster. tooproceed tooupload Hallo-bestand, sla Hallo JSON-bestand (Ctrl + S).

       ![Data Lake Tools voor Visual Studio Code bestandspad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  Resultaten: Hallo **uitvoer** venster Hallo-bestand Uploadstatus wordt weergegeven.

       ![Data Lake Tools voor Visual Studio Code Uploadstatus](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

Een andere manier tooupload een bestand toostorage via Hallo is met de rechtermuisknop te klikken op het volledige pad van het bestand Hallo of relatief pad in de script-editor Hallo Hallo-bestand. Geef het lokale bestandspad Hallo en selecteer vervolgens Hallo-account. Hallo **uitvoer** venster Hallo Uploadstatus weergegeven. 

### <a name="open-azure-storage-explorer"></a>Open Azure Opslagverkenner
U kunt openen **Azure Opslagverkenner** door te voeren opdracht Hallo **ADL: Open Web Azure Storage Explorer** of door deze te selecteren in de context contextmenu Hallo.

**tooopen Azure Opslagverkenner**

1. Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.
2. Voer **Open Web Azure Storage Explorer** of met de rechtermuisknop op een relatief pad of een volledig pad in de script-editor Hallo Hallo en selecteer vervolgens **Open Web Azure Storage Explorer**.
3. Selecteer een Data Lake Analytics-account.

Data Lake Tools geopend hello Azure opslagpad in hello Azure-portal. Pad en de preview-Hallo bestand Hallo van Hallo web, kunt u vinden.

### <a name="local-run-and-local-debug-for-windows-users"></a>Lokaal uitvoeren en lokaal fouten opsporen voor Windows gebruikers
U-SQL lokaal uitvoeren Test uw lokale gegevens en uw script lokaal, valideert voordat je code gepubliceerde tooData Lake Analytics is. Hallo lokale foutopsporing met het onderdeel kunt u toocomplete Hallo taken te volgen voordat uw code is tooData Lake Analytics verzonden: 
- Uw C# code-behind voor foutopsporing. 
- Doorloop Hallo-code. 
- Het script lokaal valideren.

Zie voor instructies voor lokale uitvoering en lokale foutopsporing, [U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).

## <a name="additional-features"></a>Aanvullende functies

Data Lake Tools voor VS Code ondersteunt Hallo volgende kenmerken:

-   IntelliSense automatisch aanvullen: suggesties worden weergegeven in het pop-upvensters rond items, zoals trefwoorden, methoden en variabelen. Verschillende pictogrammen verschillende typen Hallo objecten:

    - Het gegevenstype scala
    - complex gegevenstype
    - Ingebouwde UDT 's
    - .NET-verzameling en -klassen
    - C#-expressies
    - Ingebouwde C# UDF's, UDO's en UDAAGs 
    - U-SQL-functies
    - U-SQL-windowingfunctie
 
    ![Data Lake Tools voor Visual Studio Code IntelliSense objecttypen](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   IntelliSense automatisch aanvullen van Data Lake Analytics-metagegevens: Data Lake Tools Hallo Data Lake Analytics metagegevens lokaal downloadt. Hallo IntelliSense functie wordt automatisch gevuld objecten, inclusief Hallo-database, schema, tabel, weergave, tabelwaardefunctie, procedures en C#-assembly's, uit Hallo Data Lake Analytics-metagegevens.
 
    ![Data Lake Tools voor Visual Studio Code IntelliSense metagegevens](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   IntelliSense fout markering: Data Lake Tools onderstreept Hallo fouten voor de U-SQL en C# bewerken. 
-   Syntaxis licht: Data Lake Tools maakt gebruik van verschillende kleuren toodifferentiate items, zoals variabelen, trefwoorden, gegevenstype en functies. 

    ![Data Lake Tools voor Visual Studio Code syntaxis highlights](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Volgende stappen

- Zie voor U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code [U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).
- Zie voor informatie over Data Lake Analytics aan de slag [zelfstudie: aan de slag met Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Zie voor meer informatie over Data Lake Tools voor Visual Studio [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Zie voor meer informatie over het ontwikkelen van assembly's [ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-assemblies.md).



