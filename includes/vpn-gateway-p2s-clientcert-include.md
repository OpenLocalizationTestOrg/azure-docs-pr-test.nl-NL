Elke clientcomputer die verbinding tooa maakt VNet met punt-naar-Site moet beschikken over een clientcertificaat dat is geïnstalleerd. Hallo-clientcertificaat is gegenereerd op basis van het basiscertificaat Hallo en geïnstalleerd op elke clientcomputer. Als een geldig clientcertificaat niet is geïnstalleerd en Hallo client tooconnect toohello VNet probeert, mislukt de verificatie.

Kunt u een uniek certificaat genereren voor elke client kunt, of u Hallo hetzelfde voor meerdere clients certificaat. Hallo voordeel toogenerating unieke clientcertificaten Hallo mogelijkheid toorevoke één certificaat is. Als meerdere clients met behulp van dezelfde clientcertificaat Hallo en moet u toorevoke, u toogenerate en nieuwe certificaten installeren voor alle clients die gebruikmaken van dat certificaat tooauthenticate Hallo.

U kunt met behulp van de volgende methoden Hallo clientcertificaten genereren:

- **Commercieel certificaat**

  - Als u een commerciële certificeringsoplossing gebruikt, genereert u een certificaat met de algemene indeling van de naam van waarde Hallo 'name@yourdomain.com', in plaats van Hallo "domeinnaam\gebruikersnaam" indeling.
  - Zorg ervoor dat het Hallo-clientcertificaat is gebaseerd op Hallo 'User' certificaatsjabloon met als eerste item in de lijst gebruik Hallo Hallo 'Client Authentication' in plaats van slimme smartcardaanmelding, enzovoort. U kunt Hallo certificaat controleren door te dubbelklikken op Hallo-clientcertificaat en het weergeven van **Details > Enhanced Key Usage**.

- **Zelfondertekende basiscertificaat:** is het belangrijk dat u Hallo in een van onderstaande Hallo P2S-certificaat-artikelen stappen. Anders Hallo-clientcertificaten die u maakt is niet compatibel met P2S-verbindingen en clients een foutbericht ontvangt bij het tooconnect. Hallo-stappen op een van de volgende artikelen Hallo een compatibel clientcertificaat genereren: 

  * [Instructies voor Windows 10 PowerShell](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert): deze instructies zijn Windows 10 en PowerShell toogenerate certificaten vereist. Hallo-certificaten die zijn gegenereerd kunnen worden geïnstalleerd op alle ondersteunde P2S-client.
  * [MakeCert instructies](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): MakeCert gebruiken als u geen toegang tot Windows 10 tooa toouse toogenerate computercertificaten. MakeCert afgeschaft, maar u kunt nog steeds MakeCert toogenerate certificaten gebruiken. Hallo-certificaten die zijn gegenereerd kunnen worden geïnstalleerd op alle ondersteunde P2S-client.

  Wanneer u een clientcertificaat uit een zelfondertekend basiscertificaat met behulp van de voorgaande instructies hello genereren, is deze automatisch geïnstalleerd op Hallo computer die u hebt gebruikt toogenerate deze. Als u wilt dat een clientcertificaat op een andere clientcomputer tooinstall, moet u tooexport als een .pfx-bestand, samen met de volledige certificaatketen Hallo. Hiermee maakt u een .pfx-bestand met Hallo root certificaatinformatie die is vereist voor de Hallo client toosuccessfully verifiëren. Zie voor stappen tooexport een certificaat, [certificaten - exporteren een clientcertificaat](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientexport).
