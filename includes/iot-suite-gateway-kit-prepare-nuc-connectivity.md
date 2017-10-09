## <a name="prepare-your-intel-nuc"></a>Uw Intel NUC voorbereiden

toocomplete hello hardware-installatie, moet u:

- Verbinding maken met de Intel NUC toohello voeding opgenomen in het Hallo-pakket.
- Verbinding maken met uw Intel NUC tooyour netwerk met behulp van een Ethernet-kabel.

U hebt nu Hallo hardware-instellingen van uw gatewayapparaat Intel NUC voltooid.

### <a name="sign-in-and-access-hello-terminal"></a>Aanmelden en Hallo terminal

U hebt twee opties tooaccess een terminal-omgeving op uw NUC Intel:

- Als u een toetsenbord hebt en verbonden tooyour Intel NUC bewaken, kunt u rechtstreeks Hallo-shell openen. Hallo standaardreferenties zijn gebruikersnaam **hoofdmap** en het wachtwoord **hoofdmap**.

- Hallo-shell toegang op uw Intel NUC gebruik van SSH op uw computer.

#### <a name="sign-in-with-ssh"></a>Meld u aan met SSH

toosign met SSH, moet u Hallo IP-adres van uw NUC Intel. Als u een toetsenbord hebt en verbonden tooyour Intel NUC bewaken, gebruikt u Hallo `ifconfig` opdracht toofind Hallo IP-adres. U kunt ook verbinding maken met tooyour router toolist Hallo adressen van apparaten in uw netwerk.

Aanmelden met gebruikersnaam **hoofdmap** en het wachtwoord **hoofdmap**.

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a>Optioneel: Een map op uw NUC Intel delen

Desgewenst kunt u tooshare een map op uw NUC Intel met uw bureaublad omgeving. U toouse uw voorkeur bureaublad teksteditor delen van een map kunt (zoals [Visual Studio Code](https://code.visualstudio.com/) of [Sublime Text](http://www.sublimetext.com/)) tooedit bestanden op uw NUC Intel in plaats van `nano` of `vi`.

tooshare een map met Windows, wordt een Samba-server op Hallo Intel NUC configureren. Hallo SFTP-server ook gebruiken op Hallo Intel NUC met een SFTP-client op uw computer.
