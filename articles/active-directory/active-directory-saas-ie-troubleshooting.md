---
title: aaaTroubleshooting hello Azure Access Configuratiescherm-extensie voor IE | Microsoft Docs
description: Hoe groepeert toouse beleid toodeploy Hallo Internet Explorer-invoegtoepassing voor Hallo mijn Apps portal.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a>Hallo Configuratiescherm-uitbreiding voor toegang tot het oplossen van problemen voor Internet Explorer
In dit artikel helpt u Hallo na de problemen oplossen:

* U bent tooaccess uw apps via Hallo mijn Apps portal tijdens het gebruik van Internet Explorer.
* U ziet Hallo 'Software installeren' bericht zelfs als u al Hallo software hebt geïnstalleerd.

Als u een beheerder bent, Zie ook: [hoe tooDeploy uitbreiding voor toegang tot Configuratiescherm Hallo voor Internet Explorer met behulp van Groepsbeleid](active-directory-saas-ie-group-policy.md)

## <a name="run-hello-diagnostic-tool"></a>Hallo diagnostisch hulpprogramma uitvoeren
U kunt problemen installatie Hello Configuratiescherm-uitbreiding voor toegang door te downloaden en uitvoeren van Hallo Toegangsvenster diagnostische hulpprogramma:

1. [Klik hier toodownload Hallo diagnostische hulpprogramma.](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. Open Hallo bestands- en druk op **alle uitpakken** knop.
   
    ![Druk op alle uitpakken](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. Druk op Hallo **extraheren** knop toocontinue.
   
    ![Druk op uitpakken](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. hulpprogramma voor toorun hello, klik met de rechtermuisknop Hallo-bestand met de naam **AccessPanelExtensionDiagnosticTool**, selecteer daarna **openen met > Microsoft Windows Script Host die is gebaseerd**.
   
    ![Open met > Microsoft Windows scripthost gebaseerd](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. Vervolgens ziet u Hallo na diagnostische venster waarin wordt beschreven wat mis zijn met de installatie.
   
    ![Een voorbeeld van diagnostische Hallo-venster](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. Klik op '**Ja**' toolet Hallo programma fix Hallo problemen zijn gevonden.
7. Deze wijzigingen, toosave elke Internet Explorer-venster sluiten en open Internet Explorer opnieuw.<br />Als u nog steeds geen toegang uw apps tot, probeert u Hallo onderstaande stappen.

## <a name="check-that-hello-access-panel-extension-is-enabled"></a>Controleer dat Hallo die toegang Configuratiescherm-extensie is ingeschakeld
tooverify die Hallo uitbreiding van het Configuratiescherm toegang is ingeschakeld in Internet Explorer:

1. Klik in Internet Explorer op Hallo **Tandwielpictogram pictogram** op Hallo rechtsboven Hallo-venster. Selecteer vervolgens **Internetopties**.<br />(In oudere versies van Internet Explorer kunt u dit onder vinden **Extra > Internetopties**.
   
    ![Ga tooTools > Internetopties](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. Klik op Hallo **programma's** tabblad en klik op Hallo **invoegtoepassingen beheren** knop.
   
    ![Klik op Invoegtoepassingen beheren](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. Selecteer in dit dialoogvenster **Configuratiescherm-uitbreiding voor toegang tot** en klik vervolgens op Hallo **inschakelen** knop.
   
    ![Klik op inschakelen](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. Deze wijzigingen, toosave elke Internet Explorer-venster sluiten en open Internet Explorer opnieuw.

## <a name="enable-extensions-for-inprivate-browsing"></a>Uitbreidingen inschakelen voor InPrivate-navigatie
Als u Hallo InPrivate-navigatie-modus met:

1. Klik in Internet Explorer op Hallo **Tandwielpictogram pictogram** op Hallo rechtsboven Hallo-venster. Selecteer vervolgens **Internetopties**.<br />(In oudere versies van Internet Explorer kunt u dit onder vinden **Extra > Internetopties**.
   
    ![Een voorbeeld van diagnostische Hallo-venster](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. Ga toohello **Privacy** tabblad vervolgens **schakelt** Hallo selectievakje **werkbalken en extensies uitschakelen wanneer InPrivate-navigatie wordt gestart**</p>
   
    ![Schakel het selectievakje uitschakelen werkbalken en extensies wanneer InPrivate-navigatie wordt gestart](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. Deze wijzigingen, toosave elke Internet Explorer-venster sluiten en open Internet Explorer opnieuw.

## <a name="uninstall-hello-access-panel-extension"></a>Hallo uitbreiding van het Configuratiescherm toegang verwijderen
toouninstall hello Toegangspaneel uitbreiding van uw computer:

1. Op het toetsenbord, drukt u op Hallo **Windows-toets** tooopen Hallo startmenu. Wanneer het Hallo-menu is geopend, kunt u alles typen toodo een zoekopdracht. Typ 'Configuratiescherm' en open vervolgens Hallo **Configuratiescherm** wanneer deze wordt weergegeven in zoekresultaten Hallo.
   
    ![Zoeken naar het Configuratiescherm](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. Wijzig in Hallo rechterbovenhoek van het Configuratiescherm hello, Hallo **weergeven door** te optie**grote pictogrammen**. Vervolgens zoeken en klik op Hallo **programma's en onderdelen** knop.
   
    ![Chang Hallo weergave tooshow grote pictogrammen](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. Selecteer in de lijst Hallo **Configuratiescherm-uitbreiding voor toegang tot**, en klikt u op Hallo Hallo **verwijderen** knop.
   
    ![Klik op verwijderen](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. U kunt vervolgens tooinstall Hallo-uitbreiding opnieuw toosee als Hallo probleem opgelost is.

Als u problemen hebt met het Hallo-uitbreiding te verwijderen, kunt u ook verwijderen met behulp van Hallo [Microsoft los It](https://go.microsoft.com/?linkid=9779673) hulpprogramma.

## <a name="related-articles"></a>Verwante artikelen
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Hoe tooDeploy uitbreiding voor toegang tot Configuratiescherm Hallo voor Internet Explorer met behulp van Groepsbeleid](active-directory-saas-ie-group-policy.md)

