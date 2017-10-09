
### <a name="installation-failures"></a>Installatiefouten
| **Voorbeeld van een foutbericht** | **Aanbevolen actie** |
|--------------------------|------------------------|
|FOUT mislukt tooload Accounts. Fout: System.IO.IOException: kan geen tooread gegevens van Hallo transport verbinding bij het installeren en registreren Hallo CS-server.| Zorg ervoor dat TLS 1.0 op Hallo-computer is ingeschakeld. |

### <a name="registration-failures"></a>Registratiefouten
Registratiefouten kunnen fouten worden opgespoord aan de hand van Hallo Logboeken in Hallo **%ProgramData%\ASRLogs** map.

| **Voorbeeld van een foutbericht** | **Aanbevolen actie** |
|--------------------------|------------------------|
|**09:20:06**: InnerException.Type: SrsRestApiClientLib.AcsException,InnerException.<br>Bericht: ACS50008: SAML-token is ongeldig.<br>Traceer-id: 1921ea5b-4723-4be7-8087-a75d3f9e1072<br>Correlatie-id: 62fea7e6-2197-4be4-a2c0-71ceb7aa2d97 ><br>Tijdstempel: **2016-12-12 14:50:08Z<br>** | Zorg ervoor dat Hallo tijd op uw systeemklok niet meer dan 15 minuten uit Hallo lokale tijd. Voer Hallo installatieprogramma toocomplete Hallo registratie.|
|**09:35:27** : DRRegistrationException tijdens een poging tooget alle disaster recovery-kluis voor het geselecteerde certificaat Hallo:: Exception.Type:Microsoft.DisasterRecovery.Registration.DRRegistrationException heeft geretourneerd, Exception.Message: ACS50008: SAML-token is ongeldig.<br>Traceer-id: e5ad1af1-2d39-4970-8eef-096e325c9950<br>Correlatie-id: abe9deb8-3e64-464d-8375-36db9816427a<br>Tijdstempel: **2016-05-19 01:35:39Z**<br> | Zorg ervoor dat Hallo tijd op uw systeemklok niet meer dan 15 minuten uit Hallo lokale tijd. Voer Hallo installatieprogramma toocomplete Hallo registratie.|
|06:28:45: mislukte toocreate certificaat<br>06:28:45:Setup kan niet worden voortgezet. Een certificaat vereist tooauthenticate tooSite die herstel kan niet worden gemaakt. Setup opnieuw uitvoeren | Zorg ervoor dat u Setup uitvoert als lokale beheerder. |
