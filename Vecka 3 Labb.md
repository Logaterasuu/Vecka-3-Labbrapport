###  
  # Del 2: Intro 1 – Vad kör jag egentligen?

### Varför det är viktigt för IT-säkerhet

Det första steget i all säkerhetsanalys, incidenthantering och systemhärdning är **kartläggning (** **Asset Inventory** **)**. Du måste veta vilken distribution, version och kärnversion systemet kör för att identifiera kända sårbarheter (CVE) och tillämpa rätt säkerhetsuppdateringar.

### Steg-för-steg-instruktioner

#### 1\. Identifiera distribution och version

```
cat /etc/os-release

```

* **Kodförklaring:** `cat` läser och visar innehållet i konfigurationsfilen `/etc/os-release`.

#### 2\. Kärnversion och hårdvaruarkitektur

```
uname -r
uname -m

```

* **Kodförklaring:** `uname -r` visar den aktiva Linux-kärnans version (t.ex. `6.8.0-31-generic`). `uname -m` visar maskinens hårdvaruarkitektur (t.ex. `x86_64`).

#### 3\. Datornamn och drifttid

```
hostname
uptime

```

* **Kodförklaring:** `hostname` visar maskinens nätverksnamn. `uptime` visar hur länge systemet varit igång sedan senaste start.

#### 4\. Minne och utrymme på rotfilsystemet

```
free -h
df -h /

```

* **Kodförklaring:** `free -h` visar RAM-minne. `df -h /` visar använt och ledigt utrymme på rotfilsystemet `/`. Flaggan `-h` (*human-readable*) visar värden i MB/GB.

#### 5\. Pakethanterare och distributionsfamilj

```
which apt dnf pacman

```

* **Kodförklaring:** `which` söker igenom din sökstig (`$PATH`) efter körbara program.
  
  




Mall för svar (Intro 1)

1. **Distribution och version (** **cat /etc/os-release** **):**
  * *Resultat:* [Ubuntu 26.04.1]
2. **Kodnamn och LTS-status:**
  * *Kodnamn (VERSION\_CODENAME):* [resolute]
  * *LTS-utgåva (Ja/Nej):* [Ja]
3. **Kärnversion och arkitektur:**
  * *Kärnversion (* *uname -r* *):* [7.0.0-31-generic]
  * *Arkitektur (* *uname -m* *):* [x86_64]
4. **Datornamn och drifttid:**
  * *Datornamn (* *hostname* *):* [UB-CLNT-1]
  * *Drifttid (* *uptime* *):* [3 min]
5. **Minne och utrymme på** **/** **:**
  * *RAM-minne (* *free -h* *):* [Total 3.3Gi]
  * *Ledigt utrymme på* */* *(* *df -h /* *):* [8.7G]
6. **Pakethanterare och familj:**
  * *Hittad sökväg (* *which* *):* [/usr/bin/apt]
  * *Distributionsfamilj:* [apt]

#### Diskussionsfrågor (Intro 1)

* **Vad är skillnaden mellan versionsnumret i** **/etc/os-release** **och det i** **uname -r** **?**
  * *Svar:* [Första visar Ubuntu versionen och den andra visar vilken Linux version du kör.]
* **Vad betyder LTS, och varför vill en server ha det?**
  * *Svar:* [Long Term Support och betyder att versionen av operativ systemet kommer att få uppdateringar långsiktligt.]
* **Vad hade du svarat om någon frågat "vilket operativsystem kör servern"?**
  * *Svar:* [Ubuntu]  
# Del 3: Intro 2 – Första tio minuterna i terminalen

### Varför det är viktigt för IT-säkerhet

I professionella Linux-miljöer finns ofta inget grafiskt gränssnitt. Att kunna navigera, skapa, läsa och radera filer via kommandotolken är en förutsättning för effektiv administration, logganalys och felsökning.

### Steg-för-steg &amp; Kodförklaring

1. **Analysera prompten:**
  * Tolka utskriften `användare@värdnamn:katalog $` (t.ex. `student@server01:~ $`).
2. **Navigera och skapa struktur:**

```
pwd
cd /
ls
cd /home
cd ~
cd
mkdir ovning
cd ovning
touch alfa.txt beta.txt gamma.txt

```

1. **Kodförklaring:** `pwd` (*print working directory*) visar var du står. `cd /` går till mapproten. `cd ~` och `cd` utan argument tar dig båda hem till din hemkatalog. `mkdir` skapar katalogen `ovning`. `touch` skapar tre tomma filer.
2. **Jämför listningsflaggor:**

```
ls
ls -l
ls -lah

```

1. **Kodförklaring:** `ls` visar bara namn. `ls -l` visar långt format (rättigheter, ägare, storlek, datum). `ls -lah` lägger till dolda filer (`-a`) och läsbara filstorlekar (`-h`).
2. **Snabbhet med Tab och historik:**
  * Skriv `cat al` och tryck `Tab` för automatisk komplettering.
  * Tryck `↑` för att bläddra i historiken eller kör `history` för att se hela listan.
3. **Skriva till fil och läsa tillbaka:**

```
echo "hej varld" &gt; alfa.txt
cat alfa.txt

```

1. **Kodförklaring:** `echo` skriver texten. Tecknet `&gt;` (*redirection*) skickar texten till filen `alfa.txt` och skriver över befintligt innehåll.
2. **Rensa skärmen och städa upp:**

```
clear
cd ~
rm -r ovning

```

* **Kodförklaring:** `clear` rensar terminalfönstret. `rm -r` raderar katalogen `ovning` och allt dess innehåll rekursivt utan papperskorg.

---

### Mall för svar (Intro 2)

#### Diskussionsfrågor (Intro 2)

* **Vilka av kommandona ovan visade något (läsoperationer), och vilka gjorde något (skriv/ändringsoperationer)?**
  * *Svar:* [Läs: "ls" "cat"  Skriv: "echo" "touch" "rm"]
* **Vad hände när du tryckte Tab två gånger på en tom rad eller obestämbar söksträng?**
  * *Svar:* [Jag får en massa förslag]
* **Kommandot** **rm -r** **frågade inte om lov. Vad saknas i Linux som finns i Windows Utforskaren?**
  * *Svar:* [Papperskorgen]
  * 
  * # Del 4: Intro 5 – man (Manualen i maskinen)

### Varför det är viktigt för IT-säkerhet

Gissa aldrig vad ett kommando eller en flagga gör när du arbetar på en server. Att använda `man` direkt i terminalen garanterar att du får tillförlitlig dokumentation för exakt den mjukvaruversion som körs på systemet, utan att riskera felaktiga instruktioner från internet.

### Steg-för-steg &amp; Kodförklaring

1. **Navigera i manualen:**
  * Kör `man ls`. Använd `Mellanslag` (sida framåt), `b` (sida bakåt), `/sort` (sök ordet "sort"), `n` (nästa träff) och `q` (avsluta).
2. **Kommando-mönster (SYNOPSIS):**
  * Jämför: `ls [OPTION]... [FILE]...` och `cp [OPTION]... SOURCE DEST`.
  * Hakparenteser `[...]` betyder valfria argument. Tre punkter `...` betyder att flera argument kan anges. Avsaknad av hakparenteser (`SOURCE DEST`) betyder obligatoriska argument.
3. **Söka efter flaggor:**
  * Sök i `man ls` efter sortering och dolda filer.
4. **Samma namn i olika sektioner:**

```
man -f passwd
man 5 passwd

```

1. **Kodförklaring:** `man -f passwd` visar tillgängliga manualsidor. Sektion 1 är användarkommandot (`passwd`), medan sektion 5 beskriver konfigurationsfilens format (`/etc/passwd`).
2. **Söka verktyg på beskrivning:**

```
man -k "list directory"
apropos calendar

```

* **Kodförklaring:** `man -k` och `apropos` söker i alla manualers beskrivningstexter efter nyckelord.

---

### Mall för svar (Intro 5)

1. **Standardrubriker i en man-sida (i ordning):**
  * *Rubriker:* [NAME, SYNOPSIS, DESCRIPTION,OPTIONS,EXTRA,VERSION]
  * *Vilken rubrik läser du först för snabba exempel?* [Synopsis]
2. **Flaggor funna i** **man ls** **:**
  * *Sortera efter filstorlek:* [-s]
  * *Visa dolda filer:* [-a]
3. **Träffar för** **man -f passwd** **:**
  * *Antal träffar och parenteser:* [3]
  * *Vad beskriver* *man 5 passwd* *?* [passwd filer]
4. **Sektioner i manualen (från** **man man** **):**
  * Sektion 1: [Executable programs or shell commands]
  * Sektion 2: [System calls (functions provided by the kernel)]
  * Sektion 3: [Library calls (functions within program libraries)]
  * Sektion 4: [Special files (usually found in /dev)]
  * Sektion 5: [File formats and conventions, e.g. /etc/passwd]
  * Sektion 6: [Games]
  * Sektion 7: [Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7), man-pages(7)]
  * Sektion 8: [System administration commands (usually only for root)]
  * Sektion 9: [Kernel routines [Non standard]]


#### Diskussionsfrågor (Intro 5)

* **Vad betyder siffran i parentes efter ett namn (t.ex.** **printf(1)** **vs** **printf(3)** **)?**
  * *Svar:* [Vilken sektion den ligger i manualenl]
* **Varför har** **cd** **ingen egen man-sida, medan** **ls** **har det?**
  * *Svar:* [Eftersom cd inte är en egen fil  på disken]
* **Vad är sektionen "SEE ALSO" längst ned på sidan bra till?**
  * *Svar:* [Hitta kommandom som hör ihop]  
 

  *
* # Del 5: Övning – Kom igång med vim (VimTutor)

### Varför det är viktigt för IT-säkerhet

`vim` är en textredigerare som finns installerad på nästan alla Linux-servrar och nätverksenheter i världen. När du ansluter till en server via SSH utan grafiskt gränssnitt är `vim` ofta det enda tillgängliga verktyget för att redigera konfigurationsfiler.

### Steg-för-steg &amp; Kodförklaring

1. **Kontrollera om vim finns installerat:**

```
which vi
which vim
which vimtutor
vim --version | head -1

```

1. **Installera fullständiga vim:**

```
sudo apt update
sudo apt install -y vim

```

1. **Träna nödutgången (måste kunna!):**
  * Öppna en testfil: `vim /tmp/testfil.txt`
  * Tryck några tangenter. Avsluta sedan säkert utan att spara:
    * Tryck `Esc` (återgår till Normal mode).
    * Skriv `:q!` och tryck `Enter` (avslutar utan att spara ändringar).
2. **Kör vimtutor:**
  * Starta den interaktiva guiden i terminalen:

```
vimtutor

```

1. Genomför lektion 1 och 2 (tar ca 20 minuter).
2. **Skapa och redigera en egen fil:**

```
vim ~/anteckningar.txt

```

* Tryck `i` för att gå till **Insert mode** och skriv tre rader.
* Tryck `Esc`, skriv `:wq` och tryck `Enter` (sparar och avslutar).
* Verifiera med `cat ~/anteckningar.txt`.

---

### Mall för svar (VimTutor)

1. **Resultat från** **which** **före installation:**
  * *Vilka verktyg hittades?* [Skriv ditt svar här]
2. **Kommandon inlärda i VimTutor:**
  * `h, j, k, l`: Navigation (vänster, ned, upp, höger)
  * `i`: Gå till Insert mode
  * `Esc`: Återgå till Normal mode
  * `x`: Radera tecknet under markören
  * `dd`: Radera hela raden
  * `u`: Ångra senaste ändringen
  * `:wq`: Spara och avsluta
  * `:q!`: Avsluta utan att spara

#### Utvärderingsfrågor (VimTutor)

* **Vad är den fundamentala skillnaden mellan Normal mode och Insert mode i vim?**
  * *Svar:* [Skriv ditt svar här]
* **Du har skrivit fel i en känslig konfigurationsfil och vill lämna den helt orörd. Vad gör du?**
  * *Svar:* [Skriv ditt svar här]
* **Vad är skillnaden mellan** **:q** **och** **:q!** **?**
  * *Svar:* [Skriv ditt svar här]
* **Varför ligger** **vim** **förinstallerad på nästan alla Linux-system till skillnad från** **nano** **?**
  * *Svar:* [Skriv ditt svar här] 