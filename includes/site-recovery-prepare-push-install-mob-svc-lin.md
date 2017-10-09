### <a name="prepare-for-a-push-installation-on-a-linux-server"></a>Een push-installatie voorbereiden op een Linux-server

1. Zorg ervoor dat er netwerkverbinding tussen Hallo Linux-computer en de processerver Hallo is.
2. Maak een account dat processerver Hallo tooaccess Hallo computer kunt gebruiken. Hallo-account moet een **hoofdmap** gebruiker op de bronserver Linux Hallo. (Gebruik dit account alleen voor de push-installatie Hallo en voor updates.)
3. Controleer dat bestand Hallo/etc/hosts op de bron Hallo Linux-server heeft vermeldingen die zijn toegewezen Hallo lokale hostnaam tooIP adressen die zijn gekoppeld aan alle netwerkadapters.
4. Hallo nieuwste openssh, openssh-server en openssl-pakketten op Hallo-computer die u tooreplicate wilt installeren.
5. Zorg ervoor dat SSH (Secure Shell) is ingeschakeld en wordt uitgevoerd op poort 22.
6. SFTP subsysteem voor verificatie en wachtwoord in Hallo sshd_config bestand inschakelen:
  1.  Meld u aan als **rootgebruiker**.
  2.  In Hallo bestand/etc/ssh/sshd_config-bestand, zoek Hallo regel die begint met **PasswordAuthentication**.
  3.  Hallo regel Opmerking verwijderen en het Hallo-waarde te wijzigen**Ja**.
  4.  Zoeken naar Hallo regel die met begint **subsysteem** en verwijder het commentaarteken Hallo regel.

     ![Linux](./media/site-recovery-prepare-push-install-mob-svc-lin/mobility2.png)
  5. Opnieuw opstarten Hallo **sshd** service.

7. Hallo-account die u hebt gemaakt in CSPSConfigtool toevoegen.
    1.  Meld u aan de configuratieserver tooyour.
    2.  Open **cspsconfigtool.exe**. (Dit is beschikbaar als een snelkoppeling op Hallo bureaublad en in Hallo %ProgramData%\home\svsystems\bin map).
    3.  Op Hallo **Accounts beheren** tabblad **Account toevoegen**.
    4.  U hebt gemaakt Hallo-account toevoegen. 
    5.  Geef referenties op Hallo die u gebruiken wanneer u replicatie voor een computer inschakelen.
