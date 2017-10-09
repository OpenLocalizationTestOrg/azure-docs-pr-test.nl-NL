---
title: aaaEnable Microsoft Windows Hello voor bedrijven in uw organisatie | Microsoft Docs
description: Implementatie-instructies tooenable Microsoft Passport in uw organisatie.
services: active-directory
documentationcenter: 
keywords: Microsoft Passport configureren, Microsoft Windows Hello voor bedrijven-implementatie
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a>Schakel Microsoft Windows Hello voor bedrijven in uw organisatie
Na [domein Windows 10-apparaten verbinding te maken met Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), Hallo na tooenable Microsoft Windows Hello voor bedrijven in uw organisatie:

1. System Center Configuration Manager implementeren  
2. Configureren van beleidsinstellingen
3. Hallo-certificaatprofiel configureren  

## <a name="deploy-system-center-configuration-manager"></a>System Center Configuration Manager implementeren
toodeploy gebruikerscertificaten op basis van Windows Hello voor bedrijven-sleutels, moet u de volgende Hallo:

* **System Center Configuration Manager Current Branch** -u moet tooinstall versie 1606 of hoger. Zie voor meer informatie, Hallo [documentatie voor System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) en [System Center Configuration Manager-teamblog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).
* **Openbare-sleutelinfrastructuur (PKI)** -tooenable Microsoft Windows Hello voor bedrijven met behulp van gebruikerscertificaten, u moet beschikken over een PKI. Als u niet hebt of als u niet dat toouse wilt ervan voor gebruikerscertificaten u een nieuwe domeincontroller met Windows Server 2016 bouwen 10551 (of hoger) geïnstalleerd kunt implementeren. Hallo stappen te volgen[een replica-domeincontroller installeren in een bestaand domein](https://technet.microsoft.com/library/jj574134.aspx) of te[een nieuw Active Directory-forest installeren als u een nieuwe omgeving](https://technet.microsoft.com/library/jj574166). (Hallo ISO's zijn beschikbaar voor downloaden op [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)

## <a name="configure-policy-settings"></a>Configureren van beleidsinstellingen
tooconfigure hello Microsoft Windows Hello voor bedrijven-beleidsinstellingen, hebt u twee opties:

* Groepsbeleid in Active Directory 
* Hallo System Center Configuration Manager 

Via Groepsbeleid in Active Directory is Hallo aanbevolen methode tooconfigure Microsoft Windows Hello voor bedrijven-instellingen voor beleid. 

Gebruik van System Center Configuration Manager is Hallo voorkeur methode wanneer u deze ook toodeploy certificaten gebruiken. Dit scenario:

* Zorgt voor compatibiliteit met Hallo nieuwere implementatiescenario 's
* Aan de clientzijde Hallo Windows 10 versie 1607 of hoger vereist.

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a>Configureer Microsoft Windows Hello voor bedrijven via Groepsbeleid in Active Directory
**Stappen**:

1. Open Serverbeheer en te navigeren**extra** > **Group Policy Management**.
2. Navigeer via Group Policy Management toohello domeinknooppunt die overeenkomt met toohello domein waarin u Azure AD Join tooenable wilt.
3. Met de rechtermuisknop op **Group Policy Objects**, en selecteer **nieuw**. Geef uw Group Policy Object een naam, bijvoorbeeld inschakelen Windows Hello voor bedrijven. Klik op **OK**.
4. Met de rechtermuisknop op uw nieuwe groepsbeleidsobject en selecteer vervolgens **bewerken**.
5. Navigeer te**Computerconfiguratie** > **beleid** > **Beheersjablonen** > **Windows Onderdelen** > **Windows Hello voor bedrijven**.
6. Met de rechtermuisknop op **inschakelen Windows Hello voor bedrijven**, en selecteer vervolgens **bewerken**.
7. Selecteer Hallo **ingeschakeld** keuzerondje en klik vervolgens op **toepassen**. Klik op **OK**.
8. U kunt nu Hallo Group Policy Object tooa locatie van uw keuze koppelen. tooenable dit beleid voor alle Hallo domein Windows 10-apparaten in uw organisatie, koppeling Hallo Groepsbeleid toohello domein. Bijvoorbeeld:
   * Een specifieke organisatie-eenheid (OE) in Active Directory waarop Windows 10-computers domein geplaatst worden
   * Een specifieke beveiligingsgroep met Windows 10 domeincomputers die automatisch wordt geregistreerd met Azure AD

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a>Windows Hello voor bedrijven met System Center Configuration Manager configureren
**Stappen**:

1. Open Hallo **System Center Configuration Manager**, en navigeert u vervolgens te**activa en naleving > instellingen voor naleving > toegang tot bedrijfsbronnen > Windows Hello voor bedrijven-profielen**.
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. Klik in de werkbalk bovenaan Hallo Hallo op **Windows Hello voor bedrijven-profiel maken**.
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. Op Hallo **algemene** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    a. In Hallo **naam** textbox, typ een naam voor uw profiel bijvoorbeeld **mijn WHfB profiel**.
   
    b. Klik op **Volgende**.
4. Op Hallo **ondersteunde Platforms** dialoogvenster, selecteer Hallo-platforms die worden ingericht met dit Windows Hello voor bedrijven-profiel en klik vervolgens op **volgende**.
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. Op Hallo **instellingen** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    a. Als **configureren Windows Hello voor bedrijven**, selecteer **ingeschakeld**.
   
    b. Als **Trusted Platform Module (TPM) gebruiken**, selecteer **vereist**. 
   
    c. Als **verificatiemethode**, selecteer **op basis van certificaten**.
   
    d. Klik op **Volgende**.
6. Op Hallo **samenvatting** dialoogvenster, klikt u op **volgende**.
7. Op Hallo **voltooiing** dialoogvenster, klikt u op **sluiten**.
8. Klik in de werkbalk bovenaan Hallo Hallo op **implementeren**.
   
    ![Windows Hello voor bedrijven configureren](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a>Hallo-certificaatprofiel configureren
Als u verificatie op basis van certificaten voor lokale verificatie gebruikt, kunt u tooconfigure nodig en een certificaatprofiel implementeert. Deze taak moet u tooset van een NDES-server en de siterol Certificaatregistratiepunt in Hallo System Center Configuration Manager. Zie voor meer informatie, Hallo [vereisten voor Certificaatprofielen in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).

1. Open Hallo **System Center Configuration Manager**, en navigeert u vervolgens te**activa en naleving > instellingen voor naleving > toegang tot bedrijfsbronnen > Certificaatprofielen**.
2. Selecteer een sjabloon met een smartcard aanmelden uitgebreide-sleutelgebruik (EKU).

Op Hallo **SCEP-registratie** pagina Hallo certificaatprofiel, moet u toochoose **tooPassport voor Work, anders niet installeren** als Hallo **Key Storage Provider**.

## <a name="next-steps"></a>Volgende stappen
* [Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.](active-directory-azureadjoin-windows10-devices-overview.md)
* [Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden](active-directory-azureadjoin-user-upgrade.md)
* [Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren](active-directory-azureadjoin-passport.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)

