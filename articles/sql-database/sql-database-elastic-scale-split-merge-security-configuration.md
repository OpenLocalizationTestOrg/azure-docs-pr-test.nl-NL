---
title: de beveiligingsconfiguratie aaaSplit samenvoegen | Microsoft Docs
description: Instellen van x409 certificaten voor versleuteling
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>Gesplitste samenvoegen Beveiligingsconfiguratie
toouse hello gesplitste/Merge-service, moet u goed beveiliging configureren. Hallo-service maakt deel uit van Hallo elastisch schalen functie van Microsoft Azure SQL Database. Zie voor meer informatie [elastische Scale splitsen en Merge-zelfstudie](sql-database-elastic-scale-configure-deploy-split-and-merge.md).

## <a name="configuring-certificates"></a>Configureren van certificaten
Certificaten worden op twee manieren geconfigureerd. 

1. [tooConfigure hello SSL-certificaat](#to-configure-the-ssl-certificate)
2. [tooConfigure clientcertificaten](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>tooobtain certificaten
Certificaten kunnen worden opgehaald van openbare certificeringsinstanties (CA's) of van Hallo [Windows certificaatservice](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx). Dit zijn Hallo voorkeur methoden tooobtain certificaten.

Als u deze opties niet beschikbaar zijn, kunt u genereren **zelfondertekende certificaten**.

## <a name="tools-toogenerate-certificates"></a>Hulpprogramma's voor toogenerate certificaten
* [MakeCert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>toorun Hallo-hulpprogramma 's
* Zie van ontwikkelaars vanaf de opdrachtprompt voor Visual Studios [Visual Studio-opdrachtprompt](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    Als u hebt geïnstalleerd, gaat u naar:
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* Ophalen van Hallo WDK van [Windows 8.1: Download kits en hulpprogramma's](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>tooconfigure hello SSL-certificaat
Een SSL-certificaat is vereist tooencrypt Hallo communicatie en Hallo server verifiëren. Kies Hallo meest toepasselijke van Hallo drie scenario's hieronder en alle bijbehorende stappen uitvoeren:

### <a name="create-a-new-self-signed-certificate"></a>Een nieuw zelfondertekend certificaat maken
1. [Een zelfondertekend certificaat maken](#create-a-self-signed-certificate)
2. [PFX-bestand voor zelfondertekende SSL-certificaat maken](#create-pfx-file-for-self-signed-ssl-certificate)
3. [SSL-certificaat tooCloud Service uploaden](#upload-ssl-certificate-to-cloud-service)
4. [SSL-certificaat in het configuratiebestand van de Service bijwerken](#update-ssl-certificate-in-service-configuration-file)
5. [SSL-certificeringsinstantie importeren](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>toouse een bestaand certificaat van Hallo certificaat opslaan
1. [SSL-certificaat exporteren uit het certificaatarchief](#export-ssl-certificate-from-certificate-store)
2. [SSL-certificaat tooCloud Service uploaden](#upload-ssl-certificate-to-cloud-service)
3. [SSL-certificaat in het configuratiebestand van de Service bijwerken](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>toouse een bestaand certificaat in een PFX-bestand
1. [SSL-certificaat tooCloud Service uploaden](#upload-ssl-certificate-to-cloud-service)
2. [SSL-certificaat in het configuratiebestand van de Service bijwerken](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>clientcertificaten tooconfigure
Clientcertificaten vereist zijn in de volgorde tooauthenticate aanvragen toohello service. Kies Hallo meest toepasselijke van Hallo drie scenario's hieronder en alle bijbehorende stappen uitvoeren:

### <a name="turn-off-client-certificates"></a>Clientcertificaten uitschakelen
1. [Op basis van certificaten clientverificatie uitschakelen](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>Nieuwe zelfondertekende certificaten uitgeven
1. [Een zelfondertekend certificeringsinstantie maken](#create-a-self-signed-certification-authority)
2. [CA-certificaat tooCloud Service uploaden](#upload-ca-certificate-to-cloud-service)
3. [CA-certificaat in het configuratiebestand van de Service bijwerken](#update-ca-certificate-in-service-configuration-file)
4. [Clientcertificaten uitgeven](#issue-client-certificates)
5. [PFX-bestanden maken voor clientcertificaten](#create-pfx-files-for-client-certificates)
6. [Client-certificaat importeren](#Import-Client-Certificate)
7. [Certificaatvingerafdrukken Client kopiëren](#copy-client-certificate-thumbprints)
8. [Clients toegestaan in Hallo serviceconfiguratiebestand configureren](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>Bestaande clientcertificaten gebruiken
1. [Vinden van openbare sleutel van CA](#find-ca-public-key)
2. [CA-certificaat tooCloud Service uploaden](#Upload-CA-certificate-to-cloud-service)
3. [CA-certificaat in het configuratiebestand van de Service bijwerken](#Update-CA-Certificate-in-Service-Configuration-File)
4. [Certificaatvingerafdrukken Client kopiëren](#Copy-Client-Certificate-Thumbprints)
5. [Clients toegestaan in Hallo serviceconfiguratiebestand configureren](#configure-allowed-clients-in-the-service-configuration-file)
6. [Controle van certificaatintrekking Client configureren](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>Toegestane IP-adressen
Toegang toohello service-eindpunten kunnen beperkte toospecific bereiken van IP-adressen zijn.

## <a name="tooconfigure-encryption-for-hello-store"></a>versleuteling voor Hallo store tooconfigure
Een certificaat is vereist tooencrypt Hallo referenties die zijn opgeslagen in Hallo metagegevensarchief. Kies Hallo meest toepasselijke van Hallo drie scenario's hieronder en alle bijbehorende stappen uitvoeren:

### <a name="use-a-new-self-signed-certificate"></a>Een nieuw zelfondertekend certificaat gebruiken
1. [Een zelfondertekend certificaat maken](#create-a-self-signed-certificate)
2. [PFX-bestand voor het versleutelingscertificaat zelfondertekend maken](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Versleutelingscertificaat tooCloud Service uploaden](#upload-encryption-certificate-to-cloud-service)
4. [Versleutelingscertificaat in het configuratiebestand van de Service bijwerken](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>Een bestaand certificaat uit het certificaatarchief hello gebruiken
1. [Versleutelingscertificaat exporteren uit het certificaatarchief](#export-encryption-certificate-from-certificate-store)
2. [Versleutelingscertificaat tooCloud Service uploaden](#upload-encryption-certificate-to-cloud-service)
3. [Versleutelingscertificaat in het configuratiebestand van de Service bijwerken](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>Een bestaand certificaat gebruiken in een PFX-bestand
1. [Versleutelingscertificaat tooCloud Service uploaden](#upload-encryption-certificate-to-cloud-service)
2. [Versleutelingscertificaat in het configuratiebestand van de Service bijwerken](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>Hallo standaardconfiguratie
Hallo standaardconfiguratie weigert u alle toegang toohello HTTP-eindpunt. Dit is Hallo aanbevolen instelling, aangezien Hallo aanvragen toothese eindpunten gevoelige informatie, zoals databasereferenties mag uitvoeren.
Hallo standaardconfiguratie kunt alle toegang toohello HTTPS-eindpunt. Deze instelling kan verder worden beperkt.

### <a name="changing-hello-configuration"></a>Hallo-configuratie wijzigen
Hallo groep toegangscontroleregels die van toepassing zijn tooand-eindpunt is geconfigureerd in Hallo  **<EndpointAcls>**  sectie in Hallo **serviceconfiguratiebestand**.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

Hallo-regels in een besturingselement toegangsgroep zijn geconfigureerd in een <AccessControl name=""> gedeelte van configuratiebestand Hallo-service. 

Hallo-indeling wordt uitgelegd in de documentatie voor Network Access Control Lists.
Bijvoorbeeld: tooallow alleen IP-adressen in Hallo bereik 100.100.0.0 too100.100.255.255 tooaccess Hallo HTTPS-eindpunt, Hallo regels eruit als volgt:

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>Denial of service te voorkomen
Er zijn twee verschillende mechanismen toodetect ondersteund en Denial of Service-aanvallen te voorkomen:

* Beperk het aantal gelijktijdige aanvragen per externe host (standaard uitgeschakeld)
* Snelheid van toegang per externe host beperken (op standaard)

Deze zijn gebaseerd op Hallo functies verder beschreven in de dynamische IP-beveiliging in IIS. Wanneer deze configuratie wijzigen pas op Hallo volgende factoren:

* Hallo-gedrag van proxy's en apparaten via Hallo externe hostinformatie Network Address Translation
* Elke aanvraag tooany resource in de Webrol hello wordt beschouwd als (bijvoorbeeld bij het laden van scripts, afbeeldingen, enzovoort)

## <a name="restricting-number-of-concurrent-accesses"></a>Het aantal gelijktijdige toegang beperken
Hallo-instellingen voor het configureren van dit probleem zijn:

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable deze beveiliging wijzigen.

## <a name="restricting-rate-of-access"></a>Snelheid van de toegang beperken
Hallo-instellingen voor het configureren van dit probleem zijn:

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>Hallo antwoord tooa configureren aanvraag geweigerd
Hallo configureert volgende instelling Hallo antwoord tooa aanvraag geweigerd:

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
Raadpleeg de documentatie toohello voor dynamische IP-beveiliging in IIS voor andere ondersteunde waarden.

## <a name="operations-for-configuring-service-certificates"></a>Bewerkingen voor het configureren van servicecertificaten
Dit onderwerp is alleen ter informatie. Volg de configuratiestappen Hallo die worden beschreven in:

* Hallo SSL-certificaat configureren
* Clientcertificaten configureren

## <a name="create-a-self-signed-certificate"></a>Een zelfondertekend certificaat maken
Uitvoeren:

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize:

* -n met Hallo service-URL. Jokertekens ("CN = * .cloudapp .net ') en alternatieve namen (CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net') worden ondersteund.
* -e met Hallo certificaat verloopt een sterk wachtwoord maken en geef hem wanneer u wordt gevraagd.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>PFX-bestand voor zelf-ondertekend SSL-certificaat maken
Uitvoeren:

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

Wachtwoord invoeren en exporteer het certificaat met deze opties:

* Ja, Hallo persoonlijke sleutel exporteren
* Alle uitgebreide eigenschappen exporteren

## <a name="export-ssl-certificate-from-certificate-store"></a>SSL-certificaat exporteren uit het certificaatarchief
* Certificaat zoeken
* Klik op Acties -> alle taken -> exporteren...
* Exporteer het certificaat in een. PFX-bestand met deze opties:
  * Ja, Hallo persoonlijke sleutel exporteren
  * Indien mogelijk exporteren met alle certificaten in het certificeringspad Hallo * alle uitgebreide eigenschappen exporteren

## <a name="upload-ssl-certificate-toocloud-service"></a>SSL-certificaat toocloud service uploaden
Upload het certificaat met de Hallo bestaande of gegenereerd. PFX-bestand met de Hallo SSL-sleutelpaar:

* Hallo-wachtwoord beveiligt persoonlijke sleutelgegevens Hallo invoeren

## <a name="update-ssl-certificate-in-service-configuration-file"></a>SSL-certificaat in het configuratiebestand van de service bijwerken
Update Hallo vingerafdrukwaarde van de volgende instelling in het serviceconfiguratiebestand met de vingerafdruk van certificaat Hallo HALLO hallo Hallo geüpload toohello cloudservice:

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>SSL-certificeringsinstantie importeren
Volg deze stappen in alle account/machine die communiceert met de Hallo-service:

* Dubbelklik op Hallo. CER-bestand in Windows Verkenner
* Klik in het dialoogvenster certificaat Hallo certificaat installeren...
* Certificaat importeren in Hallo die Trusted Root Certification Authorities opslaan

## <a name="turn-off-client-certificate-based-authentication"></a>Op basis van certificaten clientverificatie uitschakelen
Alleen op basis van certificaten clientverificatie wordt ondersteund en u dit uitschakelt wilt toestaan voor openbare toegang toohello service-eindpunten, tenzij andere beveiligingsmechanismen geïmplementeerd (zoals Microsoft Azure Virtual Network) zijn.

Deze instellingen toofalse in functie van Hallo service configuration file tooturn Hallo wijzigen uitschakelen:

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

Kopieer vervolgens Hallo die dezelfde vingerafdruk als Hallo SSL-certificaat in de instelling voor Hallo CA-certificaat:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>Een zelfondertekend certificeringsinstantie maken
Hallo te volgen stappen toocreate een zelfondertekend certificaat tooact als een certificeringsinstantie worden uitgevoerd:

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize deze

* -e met Hallo certificeringsinstantie vervaldatum

## <a name="find-ca-public-key"></a>Vinden van openbare sleutel van CA
Alle clientcertificaten zijn uitgegeven door een certificeringsinstantie wordt vertrouwd door het Hallo-service. Vinden Hallo openbare sleutel toohello certificeringsinstantie die certificaten Hallo client die toobe worden gebruikt voor verificatie in volgorde tooupload het toohello-cloudservice.

Als Hallo-bestand met de openbare sleutel Hallo niet beschikbaar is, uit het certificaatarchief Hallo exporteren:

* Certificaat zoeken
  * Zoeken naar een clientcertificaat dat is uitgegeven door Hallo dezelfde certificeringsinstantie (CA)
* Dubbelklik op Hallo certificaat.
* Selecteer Hallo certificeringspad tabblad in het dialoogvenster voor Hallo-certificaat.
* Dubbelklik op Hallo CA vermelding in het Hallo-pad.
* Notities van de certificaateigenschappen Hallo.
* Sluit Hallo **certificaat** dialoogvenster.
* Certificaat zoeken
  * Zoeken naar Hallo CA die hierboven vermeld.
* Klik op Acties -> alle taken -> exporteren...
* Exporteer het certificaat in een. CER met deze opties:
  * **Nee, Hallo persoonlijke sleutel niet exporteren**
  * Indien mogelijk exporteren met alle certificaten in het certificeringspad Hallo.
  * Alle uitgebreide eigenschappen exporteren.

## <a name="upload-ca-certificate-toocloud-service"></a>Uploaden van de CA-certificaat toocloud-service
Upload het certificaat met de Hallo bestaande of gegenereerd. CER-bestand met de openbare sleutel Hallo CA.

## <a name="update-ca-certificate-in-service-configuration-file"></a>Update-CA-certificaat in het configuratiebestand van de service
Update Hallo vingerafdrukwaarde van de volgende instelling in het serviceconfiguratiebestand met de vingerafdruk van certificaat Hallo HALLO hallo Hallo geüpload toohello cloudservice:

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Werk de waarde Hallo Hallo na instellen met Hallo dezelfde vingerafdruk:

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>Clientcertificaten uitgeven
Elke afzonderlijke geautoriseerde tooaccess Hallo-service moet een certificaat uitgegeven voor his/hers exclusieve gebruik hebben en eigenaar his/hers tooprotect sterk wachtwoord van de persoonlijke sleutel moet kiezen. 

Hallo stappen te volgen moet worden uitgevoerd in Hallo dezelfde machine waar Hallo zelfondertekend CA-certificaat is gegenereerd en worden opgeslagen:

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

Aanpassen:

* -n met een ID voor toohello-client die met dit certificaat wordt geverifieerd
* -e met Hallo certificaat verloopt
* MyID.pvk en MyID.cer met unieke bestandsnamen voor dit clientcertificaat

Met deze opdracht gevraagd een wachtwoord toobe gemaakt en vervolgens één keer worden gebruikt. Gebruik een sterk wachtwoord.

## <a name="create-pfx-files-for-client-certificates"></a>PFX-bestanden voor client-certificaten maken
Voor elk certificaat gegenereerde client uitvoeren:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Aanpassen:

    MyID.pvk and MyID.cer with hello filename for hello client certificate

Wachtwoord invoeren en exporteer het certificaat met deze opties:

* Ja, Hallo persoonlijke sleutel exporteren
* Alle uitgebreide eigenschappen exporteren
* Hallo afzonderlijke toowhom die dit certificaat wordt uitgegeven moet Hallo export wachtwoord kiezen

## <a name="import-client-certificate"></a>Client-certificaat importeren
Elke gebruiker voor wie een clientcertificaat is uitgegeven Hallo-sleutelparen moet importeren in Hallo machines gebruikt hij toocommunicate met Hallo-service:

* Dubbelklik op Hallo. PFX-bestand in Windows Verkenner
* Certificaat importeren in het persoonlijk archief met ten minste deze optie Hallo:
  * Alle uitgebreide eigenschappen ingeschakeld

## <a name="copy-client-certificate-thumbprints"></a>Certificaatvingerafdrukken client kopiëren
Elke gebruiker voor wie een clientcertificaat is uitgegeven moet deze stappen in volgorde tooobtain Hallo vingerafdruk van his/hers certificaat dat wordt toegevoegd toohello serviceconfiguratiebestand:

* Certmgr.exe uitvoeren
* Selecteer Hallo persoonlijke tabblad
* Dubbelklik op Hallo clientcertificaat toobe gebruikt voor verificatie
* Selecteer in het dialoogvenster Hallo certificaat dat wordt geopend, Hallo tabblad met Details
* Controleer of dat weergeven alle wordt weergegeven
* Selecteer Hallo veld met de naam van de vingerafdruk in Hallo lijst
* Hallo-waarde van de vingerafdruk van het Hallo kopiëren ** verwijderen van niet-zichtbare Unicode-tekens voor de eerste cijfer Hallo ** verwijdert alle spaties

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Toegestane clients in het serviceconfiguratiebestand Hallo configureren
Hallo-waarde van de volgende instelling in het serviceconfiguratiebestand een door komma's gescheiden lijst met vingerafdrukken Hallo van clientcertificaten Hallo toegestaan toohello-access-service Hallo Hallo bijwerken:

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>Controle van certificaatintrekking client configureren
de standaardinstelling Hallo controleert niet Hello certificeringsinstantie (CA) voor de clientstatus certificaat intrekken. tooturn op Hallo controleert, als certificeringsinstantie (CA) die clientcertificaten Hallo afgegeven Hallo ondersteunt deze controles, Hallo instelling na met een van Hallo-waarden die zijn gedefinieerd in Hallo X509RevocationMode opsomming wijzigen:

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>PFX-bestand voor zelfondertekende versleutelingscertificaten maken
Voor een versleutelingscertificaat uitvoeren:

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Aanpassen:

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

Wachtwoord invoeren en exporteer het certificaat met deze opties:

* Ja, Hallo persoonlijke sleutel exporteren
* Alle uitgebreide eigenschappen exporteren
* U moet Hallo wachtwoord tijdens het uploaden van Hallo certificate toohello cloud-service.

## <a name="export-encryption-certificate-from-certificate-store"></a>Versleutelingscertificaat exporteren uit het certificaatarchief
* Certificaat zoeken
* Klik op Acties -> alle taken -> exporteren...
* Exporteer het certificaat in een. PFX-bestand met deze opties: 
  * Ja, Hallo persoonlijke sleutel exporteren
  * Indien mogelijk exporteren met alle certificaten in het certificeringspad Hallo 
* Alle uitgebreide eigenschappen exporteren

## <a name="upload-encryption-certificate-toocloud-service"></a>Uploaden van de certificaatservice toocloud versleuteling
Upload het certificaat met de Hallo bestaande of gegenereerd. PFX-bestand met de Hallo versleuteling sleutelpaar:

* Hallo-wachtwoord beveiligt persoonlijke sleutelgegevens Hallo invoeren

## <a name="update-encryption-certificate-in-service-configuration-file"></a>Versleutelingscertificaat in het configuratiebestand van de service bijwerken
Update Hallo vingerafdrukwaarde van de volgende instellingen in het serviceconfiguratiebestand met de vingerafdruk van certificaat Hallo Hallo HALLO hallo geüpload toohello cloudservice:

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>Algemene bewerkingen van het certificaat
* Hallo SSL-certificaat configureren
* Clientcertificaten configureren

## <a name="find-certificate"></a>Certificaat zoeken
Volg deze stappen:

1. Mmc.exe worden uitgevoerd.
2. File -> module toevoegen/verwijderen...
3. Selecteer **certificaten**.
4. Klik op **Add**.
5. Hallo certificaat store locatie kiezen.
6. Klik op **Voltooien**.
7. Klik op **OK**.
8. Vouw **certificaten**.
9. Vouw Hallo certificaat store.
10. Vouw Hallo certificaat onderliggend knooppunt.
11. Selecteer een certificaat in de lijst Hallo.

## <a name="export-certificate"></a>Certificaat exporteren
In Hallo **Wizard Certificaat exporteren**:

1. Klik op **Volgende**.
2. Selecteer **Ja**, klikt u vervolgens **Export Hallo persoonlijke sleutel**.
3. Klik op **Volgende**.
4. Selecteer Hallo gewenste uitvoer-bestandsindeling.
5. Selectievakje Hallo gewenste opties.
6. Controleer **wachtwoord**.
7. Voer een sterk wachtwoord in en Bevestig het.
8. Klik op **Volgende**.
9. Typ of blader een bestandsnaam waar toostore certificaat Hallo (gebruik een. PFX-extensie).
10. Klik op **Volgende**.
11. Klik op **Voltooien**.
12. Klik op **OK**.

## <a name="import-certificate"></a>Certificaat importeren
Hallo in de Wizard Certificaat importeren:

1. Selecteer Hallo opslaglocatie.
   
   * Selecteer **huidige gebruiker** als alleen de processen die worden uitgevoerd onder de huidige gebruiker heeft toegang tot Hallo-service
   * Selecteer **lokale Machine** als andere processen in deze computer toegang Hallo-service tot heeft
2. Klik op **Volgende**.
3. Als importeren uit een bestand, controleert u het bestandspad Hallo.
4. Als u deze importeert een. PFX-bestand:
   1. Bescherming van persoonlijke sleutel Hallo Hallo-wachtwoord invoeren
   2. Selecteer opties voor importeren
5. Selecteer "Locatie" certificaten in Hallo na store
6. Klik op **Bladeren**.
7. Selecteer de gewenste winkel Hallo.
8. Klik op **Voltooien**.
   
   * Als Hallo vertrouwde basiscertificeringsinstanties hebt gekozen, klikt u op **Ja**.
9. Klik op **OK** op alle vensters van het dialoogvenster.

## <a name="upload-certificate"></a>Certificaat uploaden
In Hallo [Azure Portal](https://portal.azure.com/)

1. Selecteer **Cloudservices**.
2. Hallo-cloudservice selecteren.
3. Klik op het bovenste menu Hallo **certificaten**.
4. Klik op de balk onderaan hello, **uploaden**.
5. Hallo-certificaatbestand selecteren.
6. Als het is een. PFX-bestand, Hallo wachtwoord invoeren voor de persoonlijke sleutel Hallo.
7. Als voltooid, kopiëren van de certificaatvingerafdruk Hallo van Hallo nieuw item in de lijst Hallo.

## <a name="other-security-considerations"></a>Andere beveiligingsoverwegingen
Hallo SSL-instellingen in dit document beschreven versleutelen van communicatie tussen het Hallo-service en de clients wanneer Hallo HTTPS-eindpunt wordt gebruikt. Dit is belangrijk omdat de referenties voor toegang tot de database en mogelijk andere vertrouwelijke informatie zijn opgenomen in het Hallo-communicatie. Let echter op Hallo service interne status, inclusief referenties, in de interne tabellen in Hallo Microsoft Azure SQL database die u hebt opgegeven voor de metagegevensopslag van in uw Microsoft Azure-abonnement zich blijft voordoen. Deze database is gedefinieerd als onderdeel van de volgende instelling in uw serviceconfiguratiebestand hello (. CSCFG-bestand): 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

In deze database opgeslagen referenties zijn versleuteld. Echter als een best practice voor zorgen dat de web- en werkrollen rollen van uw service-implementaties up toodate blijven en veilig zijn als ze beide toegang toohello metagegevens database en het Hallo-certificaat gebruikt voor versleuteling en ontsleuteling van opgeslagen referenties hebben. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

