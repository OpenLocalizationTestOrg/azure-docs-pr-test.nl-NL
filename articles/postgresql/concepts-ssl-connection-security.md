---
title: SSL-verbindingen in Azure-Database voor PostgreSQL aaaConfigure | Microsoft Docs
description: Instructies en informatie tooconfigure Azure-Database voor PostgreSQL en de bijbehorende toepassingen tooproperly gebruik van SSL-verbindingen.
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="0ff3c-103">SSL-verbindingen in de Azure-Database configureren voor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="0ff3c-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="0ff3c-104">Azure-Database voor PostgreSQL verkiest verbinding maken met uw client toepassingen toohello PostgreSQL-service met Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="0ff3c-104">Azure Database for PostgreSQL prefers connecting your client applications toohello PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="0ff3c-105">Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in Hallo middle'-aanvallen door het versleutelen van de gegevensstroom Hallo tussen Hallo-server en uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

<span data-ttu-id="0ff3c-106">Hallo PostgreSQL-database-service is standaard geconfigureerd toorequire SSL-verbinding.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-106">By default, hello PostgreSQL database service is configured toorequire SSL connection.</span></span> <span data-ttu-id="0ff3c-107">Desgewenst kunt u uitschakelen dat SSL vereist voor het verbinden van tooyour database-service als de clienttoepassing biedt geen ondersteuning voor SSL-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-107">Optionally, you can disable requiring SSL for connecting tooyour database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="0ff3c-108">Afdwingen van SSL-verbindingen</span><span class="sxs-lookup"><span data-stu-id="0ff3c-108">Enforcing SSL connections</span></span>
<span data-ttu-id="0ff3c-109">Afdwinging van SSL-verbindingen is standaard ingeschakeld voor alle Azure-Database voor PostgreSQL-servers die zijn ingericht via hello Azure-portal en CLI.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-109">For all Azure Database for PostgreSQL servers provisioned through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="0ff3c-110">Evenzo bevatten verbindingsreeksen die vooraf zijn gedefinieerd in Hallo 'Verbindingsreeksen' instellingen onder uw server in Azure-portal Hallo Hallo vereiste parameters voor algemene talen tooconnect tooyour database-server via SSL.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="0ff3c-111">Hallo SSL parameter varieert op basis van Hallo-connector, bijvoorbeeld ' ssl = true ' of ' sslmode = vereisen ' of ' sslmode = vereist ' en andere variaties.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="0ff3c-112">Afdwinging van SSL configureren</span><span class="sxs-lookup"><span data-stu-id="0ff3c-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="0ff3c-113">U kunt desgewenst uitschakelen afdwingen SSL-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="0ff3c-114">Microsoft Azure raadt tooalways inschakelen **afdwingen SSL-verbinding** instellen voor een betere beveiliging.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-114">Microsoft Azure recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="0ff3c-115">Met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0ff3c-115">Using hello Azure portal</span></span>
<span data-ttu-id="0ff3c-116">Ga naar uw Azure-Database voor PostgreSQL-server en op **verbindingsbeveiliging**.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="0ff3c-117">Hallo aan/uit-knop tooenable in- of uitschakelen van Hallo **afdwingen SSL-verbinding** instelling.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-117">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="0ff3c-118">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-118">Then click **Save**.</span></span> 

![Verbindingsbeveiliging - Disable SSL afdwingen](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="0ff3c-120">U kunt Hallo instelling bevestigen door het bekijken van Hallo **overzicht** pagina toosee Hallo **SSL afdwingen status** indicator.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-120">You can confirm hello setting by viewing hello **Overview** page toosee hello **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="0ff3c-121">Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="0ff3c-121">Using Azure CLI</span></span>
<span data-ttu-id="0ff3c-122">U kunt inschakelen of uitschakelen van Hallo **ssl-afdwinging** met behulp van de parameter `Enabled` of `Disabled` waarden respectievelijk in Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-122">You can enable or disable hello **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="0ff3c-123">Zorg ervoor dat uw toepassing of framework ondersteunt SSL-verbindingen</span><span class="sxs-lookup"><span data-stu-id="0ff3c-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="0ff3c-124">Veel voorkomende toepassingsframeworks die gebruikmaken van PostgreSQL voor databaseservices, zoals Drupal en Django, doen SSL niet standaard ingeschakeld tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="0ff3c-125">Inschakelen van SSL-verbindingen moet worden uitgevoerd na de installatie of via CLI-opdrachten specifieke toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-125">Enabling SSL connectivity must be done after installation or through CLI commands specific toohello application.</span></span> <span data-ttu-id="0ff3c-126">Als uw server PostgreSQL is afdwingen van SSL-verbindingen en toepassing hello die zijn gekoppeld, is niet goed geconfigureerd, mislukken de toepassing hello tooconnect tooyour database-server.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-126">If your PostgreSQL server is enforcing SSL connections and hello associated application is not configured properly, hello application may fail tooconnect tooyour database server.</span></span> <span data-ttu-id="0ff3c-127">Hoe raadpleegt u uw toepassing documentatie toolearn tooenable SSL-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-127">Consult your application's documentation toolearn how tooenable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="0ff3c-128">Toepassingen waarvoor certificaatverificatie van het voor SSL-verbindingen</span><span class="sxs-lookup"><span data-stu-id="0ff3c-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="0ff3c-129">In sommige gevallen moet toepassingen een lokaal certificaatbestand gegenereerd op basis van een vertrouwde certificeringsinstantie (CA)-certificaat (.cer)-bestand tooconnect veilig.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) tooconnect securely.</span></span> <span data-ttu-id="0ff3c-130">Zie Hallo stappen tooobtain Hallo cer-bestand te volgen, Hallo certificaat decoderen en bindt dit tooyour toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-130">See hello following steps tooobtain hello .cer file, decode hello certificate and bind it tooyour application.</span></span>

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a><span data-ttu-id="0ff3c-131">Hallo-certificaatbestand van Hallo certificeringsinstantie (CA) downloaden</span><span class="sxs-lookup"><span data-stu-id="0ff3c-131">Download hello certificate file from hello Certificate Authority (CA)</span></span> 
<span data-ttu-id="0ff3c-132">Hallo-certificaat nodig toocommunicate via SSL met uw Azure-Database voor PostgreSQL-server zich bevindt [hier](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="0ff3c-132">hello certificate needed toocommunicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="0ff3c-133">Hallo certificaat lokaal bestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-133">Download hello certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="0ff3c-134">Download en installeer OpenSSL op uw computer</span><span class="sxs-lookup"><span data-stu-id="0ff3c-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="0ff3c-135">Hallo-certificaatbestand toodecode die nodig zijn voor uw toepassing tooconnect veilig tooyour database-server, moet u tooinstall OpenSSL op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-135">toodecode hello certificate file needed for your application tooconnect securely tooyour database server, you need tooinstall OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="0ff3c-136">Voor Linux, Unix of OS X</span><span class="sxs-lookup"><span data-stu-id="0ff3c-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="0ff3c-137">Hallo OpenSSL-bibliotheken vindt u in de broncode rechtstreeks vanuit Hallo [OpenSSL Software Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="0ff3c-137">hello OpenSSL libraries are provided in source code directly from hello [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="0ff3c-138">Hallo leiden volgende instructies u door Hallo stappen nodig tooinstall OpenSSL op uw PC Linux.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-138">hello following instructions guide you through hello steps necessary tooinstall OpenSSL on your Linux PC.</span></span> <span data-ttu-id="0ff3c-139">In dit artikel worden opdrachten bekend toowork op Ubuntu 12.04 en hoger.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-139">This article uses commands known toowork on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="0ff3c-140">Open een terminalsessie en OpenSSL installeren</span><span class="sxs-lookup"><span data-stu-id="0ff3c-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="0ff3c-141">Hallo-bestanden extraheren uit het downloadpakket Hallo</span><span class="sxs-lookup"><span data-stu-id="0ff3c-141">Extract hello files from hello download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="0ff3c-142">Voer Hallo directory waar het Hallo-bestanden zijn uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-142">Enter hello directory where hello files were extracted.</span></span> <span data-ttu-id="0ff3c-143">Standaard moet als volgt.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="0ff3c-144">OpenSSL configureren door het uitvoeren van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-144">Configure OpenSSL by executing hello following command.</span></span> <span data-ttu-id="0ff3c-145">Als u Hallo-bestanden in een map anders dan /usr/local/openssl wilt, maken of toochange Hallo na zo nodig.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-145">If you want hello files in a folder different than /usr/local/openssl, make sure toochange hello following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="0ff3c-146">Nu OpenSSL correct is geconfigureerd, moet u toocompile het tooconvert uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-146">Now that OpenSSL is configured properly, you need toocompile it tooconvert your certificate.</span></span> <span data-ttu-id="0ff3c-147">toocompile hello volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0ff3c-147">toocompile, run hello following command:</span></span>

```bash
make
```
<span data-ttu-id="0ff3c-148">Zodra de compileren is voltooid, bent u klaar tooinstall OpenSSL als een uitvoerbaar bestand door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="0ff3c-148">Once compiling is complete, you're ready tooinstall OpenSSL as an executable by running hello following command:</span></span>
```bash
make install
```
<span data-ttu-id="0ff3c-149">tooconfirm dat u hebt OpenSSL geïnstalleerd op uw systeem, Voer Hallo volgende opdracht uit en controleer zeker dat u krijgt Hallo toomake dezelfde uitvoer.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-149">tooconfirm that you've successfully installed OpenSSL on your system, run hello following command and check toomake sure you get hello same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="0ff3c-150">Als dit lukt, kunt u Hallo volgende bericht moeten zien.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-150">If successful you should see hello following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="0ff3c-151">Voor Windows</span><span class="sxs-lookup"><span data-stu-id="0ff3c-151">For Windows</span></span>
<span data-ttu-id="0ff3c-152">OpenSSL installeren op een Windows-PC kan worden uitgevoerd in de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="0ff3c-152">Installing OpenSSL on a Windows PC can be done in hello following ways:</span></span>
1. <span data-ttu-id="0ff3c-153">**(Aanbevolen)**  Hello ingebouwde Bash voor Windows-functionaliteit in Windows 10 en hoger, OpenSSL wordt standaard geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-153">**(Recommended)** Using hello built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="0ff3c-154">Instructies over hoe tooenable Bash voor Windows-functionaliteit in Windows 10 kan worden gevonden [hier](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="0ff3c-154">Instructions on how tooenable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="0ff3c-155">Via het downloaden van een toepassing Win32/64 is geleverd door het Hallo-community.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-155">Through downloading a Win32/64 application provided by hello community.</span></span> <span data-ttu-id="0ff3c-156">Terwijl Hallo OpenSSL Software Foundation biedt niet of een specifieke Windows-installatieprogramma's tekent, bieden ze een lijst met beschikbare installatieprogramma's [hier](https://wiki.openssl.org/index.php/Binaries)</span><span class="sxs-lookup"><span data-stu-id="0ff3c-156">While hello OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="0ff3c-157">Uw certificaatbestand decoderen</span><span class="sxs-lookup"><span data-stu-id="0ff3c-157">Decode your certificate file</span></span>
<span data-ttu-id="0ff3c-158">Hallo basis-CA-bestand in een versleutelde indeling is gedownload.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-158">hello downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="0ff3c-159">Certificaatbestand van OpenSSL toodecode hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-159">Use OpenSSL toodecode hello certificate file.</span></span> <span data-ttu-id="0ff3c-160">toodo worden dus deze OpenSSL-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0ff3c-160">toodo so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="0ff3c-161">TooAzure Database voor PostgreSQL verbinding te maken met SSL-verificatie</span><span class="sxs-lookup"><span data-stu-id="0ff3c-161">Connecting tooAzure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="0ff3c-162">Nu dat u hebt uw certificaat is gedecodeerd, kunt u nu verbinding databaseserver tooyour veilig via SSL.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-162">Now that you have successfully decoded your certificate, you can now connect tooyour database server securely over SSL.</span></span> <span data-ttu-id="0ff3c-163">certificaat-serververificatie met tooallow Hallo certificaat moet worden geplaatst in Hallo bestand ~/.postgresql/root.crt in Hallo basismap.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-163">tooallow server certificate verification, hello certificate must be placed in hello file ~/.postgresql/root.crt in hello user's home directory.</span></span> <span data-ttu-id="0ff3c-164">(Op Microsoft Windows hello-bestand is met de naam % APPDATA%\postgresql\root.crt.).</span><span class="sxs-lookup"><span data-stu-id="0ff3c-164">(On Microsoft Windows hello file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="0ff3c-165">Hallo hieronder vindt u instructies voor het verbinden van tooAzure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-165">hello following provides instructions for connecting tooAzure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="0ff3c-166">Er is momenteel een bekend probleem als u ' sslmode controleren volledige = ' mislukt in uw service verbinding toohello Hallo verbinding met de volgende fout Hallo: _servercertificaat voor '&lt;regio&gt;. Control.database.Windows.NET' (en 7 andere namen) niet overeenkomt met hostnaam '&lt;servername&gt;. postgres.database.azure.com '._</span><span class="sxs-lookup"><span data-stu-id="0ff3c-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection toohello service, hello connection will fail with hello following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="0ff3c-167">Als ' sslmode = controleren volledig ' is vereist, servernaamconventie Hallo gebruik  **&lt;servername&gt;. database.windows.net** als de hostnaam van uw verbinding-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-167">If "sslmode=verify-full" is required, please use hello server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="0ff3c-168">We zullen deze beperking in toekomstige Hallo tooremove.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-168">We plan tooremove this limitation in hello future.</span></span> <span data-ttu-id="0ff3c-169">Verbindingen met andere [SSL modi](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) toouse Hallo voorkeur host naamgevingsconventie moet worden voortgezet  **&lt;servername&gt;. postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue toouse hello preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="0ff3c-170">Werken met het opdrachtregelhulpprogramma psql</span><span class="sxs-lookup"><span data-stu-id="0ff3c-170">Using psql command-line utility</span></span>
<span data-ttu-id="0ff3c-171">Hallo volgende voorbeeld ziet u hoe toosuccessfully tooyour PostgreSQL-server op Hallo psql opdrachtregelprogramma met verbinding.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-171">hello following example shows you how toosuccessfully connect tooyour PostgreSQL server using hello psql command-line utility.</span></span> <span data-ttu-id="0ff3c-172">Gebruik Hallo `root.crt` -bestand gemaakt en Hallo `sslmode=verify-ca` of `sslmode=verify-full` optie.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-172">Use hello `root.crt` file created and hello `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="0ff3c-173">Gebruik Hallo PostgreSQL-opdrachtregelinterface, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0ff3c-173">Using hello PostgreSQL command-line interface, execute hello following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="0ff3c-174">Als dit lukt, wordt u Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0ff3c-174">If successful, you receive hello following output:</span></span>
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="0ff3c-175">Met behulp van pgAdmin GUI-hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="0ff3c-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="0ff3c-176">Tooset hello pgAdmin 4 tooconnect veilig configureren via SSL vereist `SSL mode = Verify-CA` of `SSL mode = Verify-Full` als volgt:</span><span class="sxs-lookup"><span data-stu-id="0ff3c-176">Configuring pgAdmin 4 tooconnect securely over SSL requires you tooset hello `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Schermopname van pgAdmin - verbinding - SSL-modus vereisen](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="0ff3c-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0ff3c-178">Next steps</span></span>
<span data-ttu-id="0ff3c-179">Bekijk verschillende toepassing connectiviteitsopties na [verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="0ff3c-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
