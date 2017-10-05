---
title: Azure Active Directory-controlerapportgebeurtenissen | Microsoft Docs
description: Gebeurtenissen die beschikbaar zijn voor het weergeven en downloaden van uw Azure Active Directory controleren
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1620d917acf5a2c36767b5b03750c405f3631ee2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Auditrapport gebeurtenissen Azure Active Directory
*Deze documentatie maakt deel uit van de [Azure Active Directory-rapportagegids](active-directory-reporting-guide.md).*

Het Azure Active Directory auditrapport helpt klanten bevoorrechte acties die is opgetreden in Azure Active Directory identificeren. Bevoegdheden omvatten wijzigingen van de uitbreiding van bevoegdheden (bijvoorbeeld het maken of opnieuw instellen van wachtwoorden), veranderende beleidsconfiguraties (bijvoorbeeld wachtwoordbeleid) of wijzigingen in de directoryconfiguratie (bijvoorbeeld wijzigingen in de federation-domeininstellingen). De rapporten bevatten de controlerecord voor de naam van de gebeurtenis, de actor die de actie, de doelresource van invloed op een door de wijziging, en de datum en tijd (in UTC) wordt uitgevoerd. Klanten kunnen ophalen van de lijst van controlegebeurtenissen voor Azure Active Directory via de [Azure Portal](https://portal.azure.com/), zoals beschreven in [uw logboeken Audit](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Lijst met Controlerapportgebeurtenissen
<!--- audit event descriptions should be in the past tense --->

| Gebeurtenissen | Beschrijving van gebeurtenis |
| --- | --- |
| **Gebeurtenissen van gebruikers** | |
| Gebruiker toevoegen |Een gebruiker toegevoegd aan de directory. |
| Gebruiker verwijderen |Een gebruiker verwijderd uit de directory. |
| Licentie-eigenschappen instellen |De licentie-eigenschappen instellen voor een gebruiker in de map. |
| Gebruiker-wachtwoord opnieuw instellen |Het wachtwoord voor een gebruiker in de map opnieuw instellen. |
| Gebruiker-wachtwoord wijzigen |Het wachtwoord voor een gebruiker in de map wordt gewijzigd. |
| De gebruikerslicentie wijzigen |De licentie is toegewezen aan een gebruiker in de map wordt gewijzigd. Kijken om te zien welke licenties zijn bijgewerkt, de [Update gebruiker](#update-user-attributes) onderstaande eigenschappen |
| Gebruiker bijwerken |Een gebruiker in de directory bijgewerkt. [Zie hieronder](#update-user-attributes) voor kenmerken die kunnen worden bijgewerkt. |
| Force wijziging gebruiker-wachtwoord instellen |Stel de eigenschap dat ervoor zorgt dat een gebruiker hun wachtwoord wijzigen voor aanmelding. |
| Gebruikersreferenties updaten |Gebruiker het wachtwoord gewijzigd |
| **Gebeurtenissen groeperen** | |
| Groep toevoegen |Een groep gemaakt in de map. |
| Groep bijwerken |Een groep in Active directory bijgewerkt. Als u wilt zien welke eigenschappen zijn bijgewerkt, verwijzen naar [groep eigenschappen gecontroleerd](#update-group-attributes) in de onderstaande sectie |
| Groep verwijderen |Een groep verwijderd uit de directory. |
| CreateGroupSettings |Gemaakte groepsinstellingen |
| UpdateGroupSettings |Groepsbeleidsinstellingen bijgewerkt. Als u wilt weten welke instellingen zijn bijgewerkt, verwijzen naar [groep eigenschappen gecontroleerd](#update-group-attributes) in de onderstaande sectie |
| DeleteGroupSettings |Instellingen van de verwijderde groep |
| SetGroupLicense |Groepslicentie ingesteld. |
| SetGroupManagedBy |Groep kan worden beheerd door de gebruiker instellen |
| AddGroupMember |Lid is toegevoegd aan groep |
| RemoveGroupMember |Lid verwijderen uit groep |
| AddGroupOwner |Toegevoegde eigenaar aan groep |
| RemoveGroupOwner |Verwijderde eigenaar van groep |
| **Toepassingsgebeurtenissen** | |
| Service-principal toevoegen |Een service-principal toegevoegd aan de directory. |
| Service-principal verwijderen |Een service-principal verwijderd uit de directory. |
| Service-principal referenties toevoegen |De referenties zijn toegevoegd aan een service-principal. |
| Service-principal referenties verwijderen |De referenties van een service-principal is verwijderd. |
| Overdracht vermelding toevoegen |Gemaakt een [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) in de map. |
| Set delegering vermelding |Bijgewerkt een [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) in de map. |
| Verwijder de vermelding overdracht |Verwijderde een [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) in de map. |
| **Gebeurtenissen van de rol** | |
| Rollid toevoegen aan de rol |Een gebruiker aan een rol directory toegevoegd. |
| Rollid verwijderen uit rol |Een gebruiker verwijderd vanuit een functie directory. |
| AddRoleDefinition |Toegevoegde roldefinitie. |
| UpdateRoleDefinition |Roldefinitie bijgewerkt. Als u wilt weten welke instellingen zijn bijgewerkt, verwijzen naar [rol definitie eigenschappen gecontroleerd](#update-role-definition-attributes) in de onderstaande sectie |
| DeleteRoleDefinition |Roldefinitie verwijderd. |
| AddRoleAssignmentToRoleDefinition |De roltoewijzing is toegevoegd aan functiedefinitie. |
| RemoveRoleAssignmentFromRoleDefinition |De roltoewijzing is verwijderd van de roldefinitie. |
| AddRoleFromTemplate |De rol van sjabloon is toegevoegd. |
| UpdateRole |Bijgewerkte rol. |
| AddRoleScopeMemberToRole |Bereik lid is toegevoegd aan rol. |
| RemoveRoleScopedMemberFromRole |Bereik van lid verwijderd van de rol. |
| **Apparaatgebeurtenissen (alle nieuwe gebeurtenissen)** | |
| AddDevice |Toegevoegd apparaat. |
| UpdateDevice |Bijgewerkte apparaten. Zie de eigenschappen van welke apparaten zijn bijgewerkt, [apparaateigenschappen Audited](#update-device-attributes) in de onderstaande sectie |
| DeleteDevice |Het apparaat verwijderd. |
| AddDeviceConfiguration |Configuratie van het apparaat. |
| UpdateDeviceConfiguration |Bijgewerkte apparaatconfiguratie. Als u wilt zien welke configuratie-eigenschappen van het apparaat zijn bijgewerkt, verwijzen naar [configuratie apparaateigenschappen Audited](#update-device-configuration-attributes) in de onderstaande sectie |
| DeleteDeviceConfiguration |Apparaatconfiguratie van het verwijderd. |
| AddRegisteredOwner |Geregistreerde eigenaar toegevoegd aan het apparaat. |
| AddRegisteredUsers |Geregistreerde gebruikers toegevoegd aan apparaten. |
| RemoveRegisteredOwner |Verwijder geregistreerde eigenaar van apparaat. |
| RemoveRegisteredUsers |Verwijder geregistreerde gebruikers van apparaat. |
| RemoveDeviceCredentials |Apparaat-referenties verwijderen. |
| **B2B-gebeurtenissen** | |
| Batch nodigt geüpload. |Een beheerder kan een bestand met uitnodigingen worden verzonden naar gebruikers van de partners is geüpload. |
| Batch nodigt verwerkt. |Een bestand met uitnodigingen voor gebruikers van de partners is verwerkt. |
| Externe gebruiker uitnodigen. |Een externe gebruiker heeft uitgenodigd voor de map. |
| Externe gebruiker uitnodiging inwisselen. |De uitnodiging naar de map, een externe gebruiker is gebruikt. |
| Externe gebruiker aan groep toevoegen. |Lidmaatschap van is een externe gebruiker toegewezen aan een groep in de map. |
| Externe gebruiker toewijzen aan de toepassing. |Een externe gebruiker is toegewezen directe toegang tot een toepassing. |
| Het maken van een tenant. |Een nieuwe tenant is gemaakt in Azure AD door de inwisselcode uitnodiging. |
| Het maken van een gebruiker. |Een gebruiker is gemaakt in een bestaande tenant in Azure AD door de inwisselcode uitnodiging. |
| **Administratieve eenheden (alle nieuwe gebeurtenissen)** | |
| AddAdministrativeUnit |Administratieve eenheden toevoegen. |
| UpdateAdministrativeUnit |Administratieve eenheid bijwerken. Als u wilt zien welke eigenschappen administratieve eenheid zijn bijgewerkt, verwijzen naar [beheereigenschappen van eenheid, gecontroleerd](#update-administrative-unit-attributes) in de onderstaande sectie |
| DeleteAdministrativeUnit |Administratieve eenheden verwijderen. |
| AddMemberToAdministrativeUnit |Lid toevoegen aan de administratieve eenheid. |
| RemoveMemberFromAdministrativeUnit |Lid verwijderen uit de administratieve eenheid. |
| **Directory-gebeurtenissen** | |
| Partner toevoegen aan bedrijf |Een partner wordt toegevoegd aan de directory. |
| Partner verwijderen van bedrijf |Een partner verwijderd uit de directory. |
| DemotePartner |Partner degraderen. |
| Domein toevoegen aan de bedrijfsportal |Een domein wordt toegevoegd aan de directory. |
| Domein verwijderen van bedrijf |Een domein wordt verwijderd uit de directory. |
| Bijwerken van domein |Bijwerken van een domein in de directory. Als u wilt zien welke eigenschappen van het domein zijn bijgewerkt, verwijzen naar [Domeineigenschappen gecontroleerd](#update-domain-attributes) in de onderstaande sectie |
| Domein-verificatie instellen |De standaardinstelling voor domein voor het bedrijf wordt gewijzigd. |
| Instellen van de contactgegevens van bedrijf |Niveau van het bedrijf contactvoorkeuren ingesteld. Dit omvat de e-mailadressen voor marketing, evenals technische meldingen over de Microsoft Online Services. |
| Instellingen voor het federatieve domein |De federation-instellingen voor een domein worden bijgewerkt. |
| Domein verifiëren |Een domein op de map gecontroleerd. |
| Controleer of de geverifieerde e-maildomein |Een domein op de map met behulp van e-mailverificatie gecontroleerd. |
| DirSyncEnabled-vlag ingesteld op het bedrijf |Stel de eigenschap waarmee een map voor Azure AD Sync. |
| Wachtwoordbeleid instellen |De lengte en teken beperkingen voor wachtwoorden van gebruikers instellen. |
| Bedrijfsgegevens instellen |De gegevens van het niveau van het bedrijf zijn bijgewerkt. Zie de [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) PowerShell-cmdlet voor meer informatie. |
| SetCompanyAllowedDataLocation |Set bedrijf gegevenslocatie toegestaan. |
| SetCompanyDirSyncEnabled |DirSyncEnabled vlag worden ingesteld. |
| SetCompanyDirSyncFeature |Stel DirSync-functie. |
| SetCompanyInformation |Set-bedrijfsinformatie. |
| SetCompanyMultiNationalEnabled |Stel bedrijf meertalige functie is ingeschakeld. |
| SetDirectoryFeatureOnTenant |Functie van de directory niet instellen op de tenant. |
| SetTenantLicenseProperties |Tenant-licentie-eigenschappen worden ingesteld. |
| CreateCompanySettings |Bedrijfsinstellingen maken |
| UpdateCompanySettings |Werk de instellingen van het bedrijf. Als u wilt zien welke eigenschappen van het bedrijf zijn bijgewerkt, verwijzen naar [bedrijf eigenschappen gecontroleerd](#update-company-attributes) in de onderstaande sectie |
| DeleteCompanySettings |Bedrijfsinstellingen verwijderen |
| SetAccidentalDeletionThreshold |Drempelwaarde voor onopzettelijk verwijderen ingesteld. |
| SetRightsManagementProperties |Rights management-eigenschappen instellen. |
| PurgeRightsManagementProperties |Opschonen van rights management-eigenschappen. |
| UpdateExternalSecrets |Externe geheimen bijwerken |
| **Beleidsgebeurtenissen (alle nieuwe gebeurtenissen)** | |
| AddPolicy |Beleid toevoegen. |
| UpdatePolicy |Beleid bijwerken. |
| DeletePolicy |Beleid verwijderen. |
| AddDefaultPolicyApplication |Beleid toevoegen aan de toepassing. |
| AddDefaultPolicyServicePrincipal |Beleid toevoegen aan de service-principal. |
| RemoveDefaultPolicyApplication |Beleid van toepassing verwijderen. |
| RemoveDefaultPolicyServicePrincipal |Beleid verwijderen uit de service-principal. |
| RemovePolicyCredentials |Verwijder de beleid-referenties. |

## <a name="audit-report-retention"></a>Audit rapport bewaren

Zie voor de meest recente informatie over het bewaren van [bewaarbeleid voor Azure Active Directory-rapport](active-directory-reporting-retention.md).


Voor klanten die de bij het opslaan van de controlegebeurtenissen voor langere bewaartermijn, kan de rapportage-API worden gebruikt voor het ophalen van controlegebeurtenissen regelmatig in een afzonderlijke gegevensarchief. Zie [aan de slag met de rapportage-API](active-directory-reporting-api-getting-started.md) voor meer informatie.

## <a name="properties-included-with-each-audit-event"></a>Eigenschappen die deel uitmaakt van elke controlegebeurtenis
| Eigenschap | Beschrijving |
| --- | --- |
| Datum en tijd |De datum en tijd waarop de controlegebeurtenis heeft plaatsgevonden |
| Actor |De gebruiker of service-principal die de actie heeft uitgevoerd |
| Actie |De actie die is uitgevoerd |
| doel |De gebruiker of service-principal die de actie is uitgevoerd op |

## <a name="update-user-attributes"></a>'Gebruiker bijwerken' kenmerken
De controlegebeurtenis 'Update gebruiker' bevat aanvullende informatie over welke gebruikerskenmerken zijn bijgewerkt. Zowel de vorige waarde als de nieuwe waarde is opgenomen voor elk kenmerk.

| Kenmerk | Beschrijving |
| --- | --- |
| accountEnabled |De gebruiker zich kan aanmelden. |
| AssignedLicense |Alle licenties die zijn toegewezen aan de gebruiker. |
| AssignedPlan |Service-abonnementen die voortvloeien uit de licenties die zijn toegewezen aan de gebruiker. |
| LicenseAssignmentDetail |Informatie over licenties die zijn toegewezen aan de gebruiker. Bijvoorbeeld, als er op basis van een groep-licentieverlening is betrokken, omvat dit de groep die de licentie wordt verleend. |
| Mobiele telefoon |De gebruiker mobiele telefoon. |
| OtherMail |Alternatief e-mailadres van de gebruiker. |
| OtherMobile |Alternatieve mobiele telefoon van de gebruiker. |
| StrongAuthenticationMethod |Een lijst met verificatiemethoden die zijn geconfigureerd door de gebruiker voor meervoudige verificatie, zoals een telefoongesprek, SMS of verificatie van de code van een mobiele app. |
| StrongAuthenticationRequirement |Als multi-factor Authentication wordt afgedwongen, ingeschakeld of uitgeschakeld voor deze gebruiker. |
| StrongAuthenticationUserDetails |Alternatieve van de gebruiker-telefoonnummer en e-adres dat wordt gebruikt voor verificatie van multi-factor Authentication en het wachtwoord opnieuw instellen van telefoon. |
| StrongAuthenticationPhoneAppDetail |Detail forof phone-apps die zijn geregistreerd om uit te voeren 2FA aanmelding |
| telephoneNumber |Het telefoonnummer van de gebruiker. |
| AlternativeSecurityId |Een alternatieve beveiligings-ID voor het object. |
| CreationType |Methode voor het maken van de gebruiker (hetzij door een uitnodiging voor een). |
| InviteTicket |Lijst van tickets voor uitnodiging voor de gebruiker. |
| InviteReplyUrl |Lijst met URL's te beantwoorden na ontvangst van de uitnodiging. |
| InviteResources |Lijst met bronnen waartoe de gebruiker heeft uitgenodigd. |
| LastDirSyncTime |Laatste keer dat het object is bijgewerkt vanwege gesynchroniseerd vanaf de gezaghebbende (klant, on-premises)-directory. |
| MSExchRemoteRecipientType |Is toegewezen aan MSO geadresseerde typen. Verwijzen naar [MSO geadresseerde typen] https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx voor geadresseerden typen |
| PreferredDataLocation |De gewenste locatie voor openbare map van de gebruiker, van de groep, van de contactpersoon, of gegevens van het apparaat. |
| ProxyAddresses |Het adres waarmee een ontvanger Exchange Server-object in een extern e-mailsysteem wordt herkend. |
| StsRefreshTokensValidFrom |Uitvoert vernieuwen token intrekkingsgegevens - eventuele STS vernieuwen van tokens verleend voordat dit moment worden beschouwd als verlopen. |
| UserPrincipalName |De UPN die is een aanmeldingsnaam voor Internet-stijl voor een gebruiker. |
| UserState |Status van de gebruiker PendingApproval/PendingAcceptance/geaccepteerd/PendingVerification. |
| UserStateChangedOn |De tijdstempel van laatste wijziging voor UserState. Gebruikt voor het activeren van de levenscyclus van werkstromen. |
| UserType |Type gebruiker. Lid (0), Gast (1), Viral(2). |

## <a name="update-group-attributes"></a>De kenmerken 'Updategroep'
| Kenmerk | Beschrijving |
| --- | --- |
| Classificatie |De classificatie voor een groep Unified (HBI, MBI, enzovoort). |
| Beschrijving |Leesbare beschrijvende zinnen over het object. |
| Weergavenaam |De weergavenaam voor een object |
| DirSyncEnabled |Geeft aan of de synchronisatie van een bindende plaatsvindt (klant, on-premises)-directory. |
| GroupLicenseAssignment |De licentietoewijzing van een groep |
| groupType |Type groep, Unified (0) |
| IsMembershipRuleLocked |Geeft aan dat de eigenschap MembershipRule is ingesteld door de groepsbeheer met Self-Service management-service en kan niet worden gewijzigd door gebruikers. Alleen van toepassing op groepen waarbij GroupType GroupType.DynamicMembership bevat |
| IsPublic |Vlag waarmee wordt aangegeven of de groep openbaar/persoonlijk is. |
| LastDirSyncTime |Laatste keer dat het object is bijgewerkt als gevolg van het synchroniseren van de gezaghebbende (on-premises klant)-directory. |
| Mail |Primaire e-mailadres |
| MailEnabled |Geeft aan of deze groep e-functionaliteit. |
| mailNickname |Moniker voor een adres adresboek object, meestal het gedeelte van de voorgaande e-mailnaam de ' @ ' symbool. |
| MembershipRule |Een tekenreeks waarin de criteria die wordt gebruikt door de groepsbeheer met Self-Service management-service om te bepalen welke leden moeten deel uitmaken van deze groep. Zie ook IsMembershipRuleLocked. Alleen van toepassing op groepen waarbij GroupType GroupType.DynamicMembership bevat. |
| MembershipRuleProcessingState |Een enum-waarde die wordt gedefinieerd door de beheerservice voor groepsbeheer met Self-service voor het definiëren van de status van het lidmaatschap verwerking voor deze groep. Alleen van toepassing op groepen waarbij GroupType GroupType.DynamicMembership bevat. |
| ProxyAddresses |Het adres waarmee een ontvanger Exchange Server-object in een extern e-mailsysteem wordt herkend. |
| RenewedDateTime |De registratie van de tijdstempel van wanneer een groep voor het laatst is vernieuwd. |
| securityenabled moet |Hiermee wordt aangegeven of lidmaatschap van de groep autorisatiebeslissingen kan beïnvloeden. |
| WellKnownObject |Een Active directory-object, het toewijzen als een van de vooraf gedefinieerde als label. |

## <a name="update-device-attributes"></a>'Apparaat bijwerken' kenmerken
| Kenmerk | Beschrijving |
| --- | --- |
| accountEnabled |Hiermee wordt aangegeven of een beveiligings-principal kan worden geverifieerd. |
| CloudAccountEnabled |Hiermee wordt aangegeven of een beveiligings-principal kan worden geverifieerd. Geschreven door InTune wanneer het apparaat heeft als master on-premises. |
| CloudDeviceOSType |Type van het apparaat op basis van het besturingssysteem bijvoorbeeld Windows RT, iOS. Als de waarde door een cloudservice (zoals Intune), wordt dit kenmerk gezaghebbende in de map voor DeviceOSType. |
| CloudDeviceOSVersion |De versie van het besturingssysteem. Als de waarde door een cloudservice (zoals Intune), wordt dit kenmerk gezaghebbende in de map voor DeviceOSVersion. |
| CloudDisplayName |De waarde van het kenmerk displayName LDAP. Dit kenmerk wordt als de waarde door een cloudservice (zoals Intune), in de map voor displayName gezaghebbende. |
| CloudCreated |Hiermee wordt aangegeven of het object is gemaakt met cloudservices. |
| CompliantUntil |Tot welk tijdstip wordt apparaat als compatibel beschouwd. |
| DeviceMetadata |Aangepaste metagegevens voor het apparaat |
| DeviceObjectVersion |Dit kenmerk wordt gebruikt voor het identificeren van de versie van het schema van het apparaat. |
| DeviceOSType |Type van het apparaat op basis van het besturingssysteem bijvoorbeeld Windows RT, iOS. Geschreven door de registratieservice en bedoeld om te worden bijgewerkt door de MDM licht management-service of STS management-service. |
| DeviceOSVersion |De versie van het besturingssysteem. Geschreven door de registratieservice en bedoeld om te worden bijgewerkt door de MDM licht management-service of STS management-service. |
| DevicePhysicalIds |Kenmerk met meerdere waarden is bedoeld voor het opslaan van id's van het fysieke apparaat. Dit kan ook BIOS-id's, TPM vingerafdrukken, hardware-specifieke id's, enzovoort. |
| DirSyncEnabled |Geeft aan of de synchronisatie van een bindende (klant, on-premises plaatsvindt) directory. |
| Weergavenaam |De weergavenaam voor een object |
| IsCompliant |Dit kenmerk wordt gebruikt voor het beheren van de status van het mobiele apparaat management van het apparaat. |
| IsManaged |Dit kenmerk wordt gebruikt om aan te geven van dat het apparaat wordt beheerd door een MDM-cloud |
| LastDirSyncTime |Laatste keer dat het object is bijgewerkt vanwege gesynchroniseerd vanaf de gezaghebbende (on-premises klant)-directory. |

## <a name="update-device-configuration-attributes"></a>Kenmerken 'Bijwerken apparaatconfiguratie'
| Kenmerk | Beschrijving |
| --- | --- |
| MaximumRegistrationInactivityPeriod |Het maximum aantal dagen dat een apparaat inactieve voordat deze worden kan wordt beschouwd als voor verwijdering. |
| RegistrationQuota |Beleid wordt gebruikt voor het beperken van het aantal registraties van apparaat toegestaan voor één gebruiker. |

## <a name="update-service-principal-configuration-attributes"></a>'De configuratie van de Service-principal bijwerken' kenmerken
| Kenmerk | Beschrijving |
| --- | --- |
| accountEnabled |Hiermee wordt aangegeven of een beveiligings-principal kan worden geverifieerd. |
| AppPrincipalId |Externe, toepassingsspecifieke identiteit voor een beveiligings-principal. |
| Weergavenaam |De weergavenaam voor een object |
| ServicePrincipalName |Een service principal name "naam/authority" waarbij naam geeft u een waarde van de klasse toepassing en de autoriteit bevat ten minste met hostnaam [: poort] of 'name' die Hiermee geeft u een id voor de service-principal. |

## <a name="update-app-attributes"></a>Kenmerken 'App bijwerken'
| Kenmerk | Beschrijving |
| --- | --- |
| AppAddress |De reeks adressen (Omleidings-URL's) die zijn toegewezen aan een service-principal. |
| AppId |Toepassings-ID van de App. |
| AppIdentifierUri |Een toepassing URI die de toepassing te identificeren.  Dit is meestal de toegangs-URL van de toepassing. |
| AppLogoUrl |De url van de installatiekopie van de toepassing-logo opgeslagen in een CDN. |
| AvailableToOtherTenants |Waar de toepassing is multitenant (dat wil zeggen kunnen worden gebruikt door andere tenants). |
| Weergavenaam |De weergavenaam voor een toepassingsnaam in |
| Recht |Lijst met rechten van de toepassing. |
| ExternalUserAccountDelegationsAllowed |Markering die aangeeft of de resource-toepassing een vertrouwde is en overdrachtvermeldingen voor de externe gebruikersaccounts kunt maken. |
| GroupMembershipClaims |Het lidmaatschap van de claims van beleid. |
| PublicClient |True als de client kan geen geheime houden (d.w.z. niet-vertrouwelijke client in OAuth2.0) |
| RecordConsentConditions |Soorten toestemming voorwaarden, zoals gedefinieerd door de contractvoorwaarden: geen (0), SilentConsentForPartnerManagedApp(1). Deze waarde zal worden weergegeven in het schema Graph API en kan alleen worden ingesteld of gewijzigd door tenantbeheerders. |
| RequiredResourceAccess |XML-inhoud van een waarde van de eigenschap RequiredResourceAccess. |
| De Web-App |Indien waar, geeft aan dat deze toepassing een web-app. |
| WwwHomepage |De primaire webpagina. |

## <a name="update-role-attributes"></a>Kenmerken voor 'Rol bijwerken'
| Kenmerk | Beschrijving |
| --- | --- |
| AppAddress |De reeks adressen (Omleidings-URL's) die zijn toegewezen aan een service-principal. |
| BelongsToFirstLoginObjectSet |Indien waar, geeft u aan dat dit object bij de set objecten die zijn vereist hoort voor het inschakelen van de aanmelding van de eerste beheerder van een nieuwe tenant. |
| Ingebouwd |Hiermee wordt aangegeven of de levensduur van een object is eigendom van het systeem. |
| Beschrijving |Leesbare beschrijvende zinnen over het object. |
| Weergavenaam |De weergavenaam voor een object |
| mailNickname |Moniker voor een adres adresboek object, meestal het gedeelte van de voorgaande e-mailnaam de ' @ ' symbool. |
| RoleDisabled |Hiermee wordt aangegeven of de rol ten behoeve van de toegangscontrole moet worden genegeerd. |
| RoleTemplateId |De identiteit van de rolsjabloon. |
| ServiceInfo |Service-specifieke Inrichtingsgegevens die kan worden gebruikt door MOAC en/of andere service-exemplaren (van de met dezelfde of verschillende servicetypen). |
| TaskSetScopeReference |Identificeert een TaskSet en een set met bereiken die zijn gekoppeld aan een functie of RoleTemplate. |
| ValidationError |Gegevens die zijn gepubliceerd door een federatieve service met een beschrijving van een tijdelijke, servicespecifieke fout met betrekking tot de eigenschappen of koppeling van een object beheerdersactie om op te lossen. |
| WellKnownObject |Een Active directory-object, het toewijzen als een van de vooraf gedefinieerde als label. |

## <a name="update-role-definition-attributes"></a>Kenmerken 'Bijwerken roldefinitie'
| Kenmerk | Beschrijving |
| --- | --- |
| AssignableScopes |Verzameling van autorisatie-scopes die kan worden verwezen als u deze RoleDefinition toewijst aan een beveiligings-principal. |
| Weergavenaam |De weergavenaam voor een object |
| GrantedPermissions |Machtigingen verleend door deze RoleDefinition. |

## <a name="update-administrative-unit-attributes"></a>Kenmerken 'Bijwerken administratieve eenheid'
| Kenmerk | Beschrijving |
| --- | --- |
| Beschrijving |Deze eigenschap wordt bijgewerkt wanneer u de beschrijving van een administratieve eenheid wijzigen. |
| Weergavenaam |Deze eigenschap wordt bijgewerkt wanneer u de naam van een administratieve eenheid wijzigen. |

## <a name="update-company-attributes"></a>De kenmerken 'Bedrijf bijwerken'
| Kenmerk | Beschrijving |
| --- | --- |
| AllowedDataLocation |Een locatie waarin gebruikers het bedrijf kunnen worden ingericht. |
| AuthorizedServiceInstance |Namen van de service-exemplaren waarvoor een plan kan worden geïmplementeerd. |
| DirSyncEnabled |Geeft aan of de synchronisatie van een bindende (klant, on-premises plaatsvindt) directory. |
| DirSyncStatus |Geeft aan of de synchronisatie van adres adresboek objecten in deze context tenant van een bindende (klant, on-premises) plaatsvindt directory; een uitbreiding van de eigenschap DirSyncEnabled in bedrijf objecten. |
| DirSyncFeatures |Bits-vlag voor het bijhouden van reeks ingeschakelde als uitgeschakelde dirsync-functies voor de tenant. |
| DirectoryFeatures |Directoryfuncties voor ingeschakeld/uitgeschakeld. |
| DirSyncConfiguration |Bevat alle DirSync-configuratie die specifiek zijn voor de huidige tenant. |
| Weergavenaam |De weergavenaam voor een object |
| IsMnc |Een Boole-vlag ingesteld op 'true' iff die het bedrijf is ingeschakeld voor de functie meertalige bedrijf. |
| ObjectSettings |Een verzameling instellingen die van toepassing op het bereik van het object. |
| PartnerCommerceUrl |URL van de Partner commerce-site. |
| PartnerHelpUrl |URL van de Partner help-site. |
| PartnerSupportEmail |URL voor ondersteuning van e-mailadres van de Partner. |
| PartnerSupportTelephone |URL moet telefoon van de Partner-ondersteuning. |
| PartnerSupportUrl |URL van de Partner ondersteuningssite. |
| StrongAuthenticationDetails |Gegevens die betrekking hebben op StrongAuthentication. |
| StrongAuthenticationPolicy |Sterke verificatiebeleid voor het bedrijf. |
| TechnicalNotificationMail |E-mailadressen technische problemen met betrekking tot een bedrijf. |
| telephoneNumber |Telefoonnummers die aan de aanbeveling ITU E.123 voldoen. |
| TenantType |Het type van een tenant. Als deze waarde niet is opgegeven, is de tenant een bedrijf. Anders wordt de mogelijke waarden zijn: MicrosoftSupport (0), SyndicatePartner (1), (2) BreadthPartner BreadthPartnerDelegatedAdmin (3) ResellerPartnerDelegatedAdmin (4) ValueAddedResellerPartnerDelegatedAdmin (5). |
| VerifiedDomain |Een set van DNS-domeinnamen gebonden aan een bedrijf. |

## <a name="update-domain-attributes"></a>Kenmerken 'Bijwerken domein'
| Kenmerk | Beschrijving |
| --- | --- |
| Functionaliteit |Bits vlaggen met een beschrijving van de mogelijkheden van het domein, indien van toepassing. |
| Standaard |Hiermee wordt aangegeven of het domein de standaardwaarde; bijvoorbeeld, het standaard UserPrincipalName achtervoegsel wanneer een beheerder een nieuwe gebruiker in MOAC maakt. |
| Initiële |Hiermee wordt aangegeven of het domein het eerste domein voor het bedrijf, zoals toegewezen door OCP. Het eerste domein is een unieke subdomeinnaam van een Microsoft Online-domein. e.g.contoso3.microsoftonline.com. |
| LiveType |Type van de bijbehorende Windows Live naamruimte, indien van toepassing. |
| Naam |ID voor het eindpunt. |
| PasswordNotificationWindowDays |Het aantal dagen voordat een wachtwoord de gebruiker verloopt wordt geïnformeerd. |
| PasswordValidityPeriodDays |Het aantal dagen dat een wachtwoord is geschikt voor voordat moet worden gewijzigd. |

Controlerecords zijn vereiste besturingselement voor veel nalevingsvoorschriften. Voor klanten met behulp van het rapport in de Audit Azure Active Directory om te voldoen aan de regelgeving, wordt het aanbevolen dat de klant verzenden van een kopie van dit help-onderwerp met de kopie van de klant geëxporteerde auditrapport voor een verklaring van de details van het rapport. Als de controleur willen graag weten van de dat Azure momenteel voldoet aan regelgeving, direct de controleur naar de [naleving pagina](https://azure.microsoft.com/support/trust-center/compliance/) van Microsoft Azure Trust Center.

