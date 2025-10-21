# Enterprise Architect Oppsettguide for Mac

Denne guiden viser hvordan du setter opp Enterprise Architect på en Mac med Apple Silicon ved hjelp av Wine.


### 1. Installer Wine

Kjør disse kommandoene i Terminal:

```bash
# Oppdater Homebrew
brew update

# Installer Wine (dette vil ta flere minutter)
brew install --cask wine-stable
```

**Merk:** Du vil se advarsler om at Wine ikke passerer macOS Gatekeeper-sjekker. Wine vil bli deaktivert i september 2026, men det vil fungere fint frem til da.

### 2. Installer Rosetta 2

Wine på Apple Silicon krever Rosetta 2. Installer det med:

```bash
softwareupdate --install-rosetta --agree-to-license
```

### 3. Godkjenn Wine i macOS Sikkerhetsinnstillinger

Når du først prøver å kjøre Wine, vil macOS blokkere det med en sikkerhetsadvarsel.


1. Åpne **System Settings** → **Privacy & Security**
2. Rull ned for å finne meldingen om at "Wine Stable" er blokkert
3. Klikk **Open Anyway** eller **Allow Anyway**


### 5. Verifiser Wine-installasjonen

```bash
wine --version
```

Du skal se Wine-versjonsnummeret (f.eks. wine-10.0).

### 6. Sett opp Wine-miljø

Opprett et Wine-prefix (Windows-lignende miljø):

```bash
WINEPREFIX=~/.wine WINEARCH=win64 winecfg
```

Et Wine-konfigurasjonsvindu vil åpne seg. Du kan lukke det etter at det vises - dette initialiserer bare miljøet.

### 7. Last ned Enterprise Architect

TODO: Finn ut hvor installasjons-filen for Enterprise Architect skal leve, og oppdater readme.


### 8. Installer Enterprise Architect

Naviger til Nedlastinger-mappen og kjør installasjonsprogrammet:

```bash
cd ~/Downloads
wine EASetup.exe
```

Erstatt `EASetup.exe` med det faktiske installasjonsprogrammets filnavn.

Følg installasjonspromptene som du ville gjort på Windows.

### 9. Kjør Enterprise Architect

Etter installasjonen kan du kjøre EA med:

```bash
wine ~/.wine/drive_c/Program\ Files/Sparx\ Systems/EA/EA.exe
```

**Tips:** Opprett et alias i shell-profilen din for enklere tilgang:

```bash
echo 'alias ea="wine ~/.wine/drive_c/Program\ Files/Sparx\ Systems/EA/EA.exe"' >> ~/.zshrc
source ~/.zshrc
```

Nå kan du bare skrive `ea` for å starte Enterprise Architect.

[//]: # (## Feilsøking)

[//]: # ()
[//]: # (### Wine-problemer)

[//]: # ()
[//]: # (**Problem:** Grafikk- eller visningsproblemer  )

[//]: # (**Løsning:** Kjør `winecfg` og juster grafikkinnstillinger under Graphics-fanen)

[//]: # ()
[//]: # (**Problem:** Manglende Windows-komponenter  )

[//]: # (**Løsning:** Installer `winetricks` og bruk det til å installere nødvendige komponenter:)

[//]: # (```bash)

[//]: # (brew install winetricks)

[//]: # (winetricks dotnet48  # eller andre nødvendige komponenter)

[//]: # (```)

[//]: # ()
[//]: # (**Problem:** EA krasjer eller vil ikke starte  )

[//]: # (**Løsning:** Sjekk Wine-logger:)

[//]: # (```bash)

[//]: # (WINEDEBUG=+all wine ~/.wine/drive_c/Program\ Files/Sparx\ Systems/EA/EA.exe)

[//]: # (```)

[//]: # ()
[//]: # (### Ytelsesproblemer)

[//]: # ()
[//]: # (Hvis EA er treg gjennom Wine:)

[//]: # (- Lukk andre applikasjoner for å frigjøre minne)

[//]: # (- Vurder å bruke en Windows VM &#40;Parallels&#41; hvis Wine-ytelsen er utilstrekkelig)

[//]: # (- Sørg for at Mac-en din har tilstrekkelig ledig diskplass)

[//]: # (## Ytterligere ressurser)

[//]: # ()
[//]: # (- [Sparx Systems Dokumentasjon]&#40;https://sparxsystems.com/enterprise_architect_user_guide/&#41;)

[//]: # (- [Wine Dokumentasjon]&#40;https://wiki.winehq.org/&#41;)

[//]: # (- [Installere Enterprise Architect for Mac]&#40;https://sparxsystems.com/enterprise_architect_user_guide/17.1/getting_started/enterprise_architect_macos.html&#41;)

### 10. Aktiver lisens

TODO: Finn ut hvordan man aktiverer lisensen/får en lisens.

# Oppdatering av implementasjonsmodellen

Dette prosjektet ble tidligere administrert med TortoiseSVN og har blitt migrert til GitHub.
Filene som blir generert er binær-filer, Github vil ikke klare å resolve merge-conflicts, så det er viktig at endringer i modellen ikke blir jobbet med av 2 samtidig.




1. **Hent siste endringer:**
   ```bash
   git pull origin main
   ```

2. **Opprett en feature branch:**
   ```bash
   git checkout -b feature/din-endringsbeskrivelse
   ```

3. **Koordiner med teamet** - Kommuniser i Slack/Teams for å unngå samtidig redigering av EA-modellen

4. **Gjør endringer i Enterprise Architect**
    - TODO: Finn ut hvordan man oppdaterer modellen med Enterprise Architect

[//]: # (    - Åpne modellen)

[//]: # (    - Gjør endringene dine)

[//]: # (    - Lagre filen)


5. **Commit endringene dine:**
   ```bash
   git add .
   git commit -m "Beskrivende melding om endringene dine"
   ```

6. **Push til GitHub:**
   ```bash
   git push origin feature/din-endringsbeskrivelse
   ```

7. **Opprett en Pull Request** på GitHub for gjennomgang


### Viktige Git-hensyn for EA-filer

**Utfordringer:**
- EA-filer (`.eap`, `.eapx`, `.qea`) er binære/komplekse XML-filer
- Git kan ikke automatisk merge disse filene som tekstfiler
- Flere som redigerer samtidig vil forårsake konflikter

**Beste praksis:**
- **Kommuniser** - Gi beskjed til teammedlemmer når du jobber med modellen
- **Bruk feature branches** - Isoler endringene dine
- **Commit ofte** - Små, fokuserte commits reduserer konfliktpotensial
- **Pull før du starter arbeid** - Jobb alltid på den nyeste versjonen
- **Koordiner redigering** - Unngå at flere personer redigerer samme EA-fil samtidig


## Oppdater matrikkel-repoet med endringene
### TODO: Oppdater denne

Nå ligger endringene dine ute, slik at andre kan hente dem ned!

Men skal de vises frem på matrikkelforsiden i neste versjon, så må de legges inn i matrikkel-repoet:

Lag en branch for endringene dine i Matrikkel-repoet.

Slett alt som ligger i mappen:
`eksternapi/api/v1/matrikkelapi-v1-wswar/src/main/webapp/dokumentasjon/implementasjonsmodellAPI`

TODO: sjekk riktig mappenavn.

Åpne filen du har endret med Enterprise Architect.

I oversikt over mappestrukturen (Project Browser menyen), så markerer man mappen "Implementasjonsmodell - MatrikkelAPI_v1, gyldig fra versjon <versjonsnummer>".

Gå så inn på Publish → HTML → Standard HTML Report

I dialogen som kommer opp:

- Dobbeltsjekk at "Package" er satt til den mappen man markerte. Dersom ingen mappe ble markert, så vil "Package" bli default satt til den øverste mappen i Project Browser menyen. Noe som vil føre til krøll i mappestrukturen når man publisher.
- Dobbeltsjekk at Output to peker på den mappen du nettopp har slettet alt i
- Under "Default Diagram", huk av for "None" (Har nok ikke så mye å si)


![Enterprise Architect publish as HTML](images/ea_publish_as_HTML.png)

Trykk Generate

Nå kan du gå inn i IntelliJ igjen, og mappen som du rensket ut, skal nå være fylt opp igjen.

Høyreklikk på mappen, og velg Git → Add, for å legge til alle de genererte filene.

Lag et pullrequest, få det inn på main, og det vil komme ut på neste versjon!

