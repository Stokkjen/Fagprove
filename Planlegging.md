# Oppgave
## Mål
Målet med oppgaven er å lage en app for å ha kontroll på reservasjoner for en restaurant, og for gjestene å legge til eller kansellere reservasjoner. Denne restauranten kan kun ha 12 gjester til gangen, men det ble ikke spesifisert noe med hvordan bordene virker. Da tar jeg og antar at de setter i sammen bord som har plass til 2 stykk sammen, slik at hvis det er 4 blir det 2 bord, hvis det er 5 blir det 3 bord. De har 6 bord, som gjør slik at 12 gjester holder maksimum. Men, det kan hende at alle bordene blir brukt og det ikke er hele 12 gjester.

# Arbeid
## Fremgangsmåte:
- Først vil jeg bruke DrawSQL for å tenke opp og illustrere en datamodell (hovedsaklig tabeller) som tilpasser selve oppgaven.
- Jeg kommer også til å tenke ut eventuelle views for å få samlet data på en sikker og fornuftig måte.
- Det samme gjelder for prosedyrer, for å få funksjonaliteten som er nødvendig.
- Så kommer jeg til å lage illustrasjoner av appene og modalene ved hjelpen av Figma.
- Når jeg har en klar idé over hvordan ting skal fungere og se ut, og har levert inn planleggingen, begynner jeg med å definere alle tabellene i SQL.
- Da lager jeg roller, moduler og capabilities for å komme i gang med sikkerhet.
- Da vil jeg begynne å implementere sikkerhet i views til tabellene og triggerne deres.
- Da begynner jeg på setup appene, siden disse er små og kjappe å lage, og en viktig del av systemet. Da følger jeg bare Figma skissen og bruker eventuelle views og prosedyrer.
- Da begynner jeg å jobbe på hovedappen.
- Hvis nødvendig kan det hende at jeg går tilbake senere å gjør småendringer hvis noe dukket opp.
- Når jeg er ferdig med det og hvis jeg får tid, er det egentlig hovedsaklig bare for meg å legge til noen bonuser hvis jeg får tid til det.
- Når presentasjonen nærmer seg begynner jeg å forberede meg.
## Timeplan
### 25.03.25 - Tirsdag (7.5t):
- Gjennomgang av fagprøve.
- Dikte opp og illustrere datamodell ved hjelp av DrawSQL.
- Dikte opp og illustrere apps ved hjelp av Figma.
- Dikte opp og notere ned views og prosedyrer som er nødvendige/fornuftig.
- Planlegge utviklingen.
- Lever inn planlegging.
### 26.03.25 - Onsdag (7.5t):
- Definere tabeller som finnes i datamodellen.
- Jobbe med sikkerhet.
### 27.03.25 - Torsdag (7.5t):
- Jobbe med views og prosedyrer.
- Lage setup apper.
### 28.03.25 - Fredag (7.5t):
- Begynne på appen ved å følge skissen laget i Figma.
### (29-30).03.25 - Helg:
- Fortsette på appen.
### 31.03.25 - Mandag (7.5t):
- Fortsette på appen.
- Hvis jeg begynner å nærme meg ferdig, legge til eventuelle nyttige ting jeg har tenkt på.
### 01.04.25 - Tirsdag (7.5t):
- Finpuss alt.
- Forberede seg til presentasjon.
### 02.04.25 - Onsdag:
- Presentasjon
### Kostnad:
- Total timekostnad: 6,975,-
  - Antall timer: 45
  - Timekostnad: 155,-
- Omega365 lisens (Per måned): 33,000,- (pluss 380,- per bruker)
  - Hosting: 8,000,-
  - Produkt: 25,000,-
  - Bruker: 380,-
- Total kostnad: 39,975,- (pluss 380,- per bruker)

# Teknologi
## Omega365:
- CTP - ellers kjent som "Core Technology Platform" er passende, siden den holder seg godt oppdatert, og bruker Vue.js, som er et rammeverk som støtter gjenbrukbare komponenter, og har mange innebygde komponenter allerede.
- Appdesigner - lar deg lage appene. Her får du mange kjekke verktøy som du kan bruke for vise frem data, og å gjøre endringer.
- Code Search - lar deg se på koden i andre apper. Dette er et meget kjekt verktøy å bruke når en ikke husker eller ikke vet hvordan en bruker spesifikke komponenter eller hvis du vil vite hvordan en gjør ting i javascript.
- Snippets - litt lik code search, men mer oversiktlig og klar. Snippets lar deg lese dokumentasjon om spesifikke komponenter, f.eks hvilken propper de har og hva de gjør.
- Data API - tillater deg å kommunisere fra frontend til backend. Ved hjelp av dataobjekter kan du koble til views. (Ikke tabeller. Hvis du bare vil ha data fra tabell kan du koble til er tabell view, et view som er designet for å vise tabellen med sikkerhet integrert.) Den kan også kjøre prosedyrer.
## Annet:
- Github - for dokumentasjon, siden det er veldig simpelt og greit.
- DrawSQL - for å lage datamodell.
- Figma - for å tegne hvordan appene skal omtrent se ut.

# Skisser
## Datamodell ([DrawSQL](https://drawsql.app/teams/omega365-1/diagrams/todo-list-planning))
INSERT IMAGE HERE
- 
## Apps ([Figma](https://www.figma.com/design/BQHHv4M9cZVGv5ZdFa2Ivm/ToDo-List---Planning?node-id=0-1&t=57C8mcIJcz8sNIPC-1))
INSERT IMAGE HERE
- 

# Views, Procedures og Triggers
## Views
- 
## Procedures
- 
## Triggers
- 

# Kilder
## Informasjonskilder:
- [ChatGPT](https://chatgpt.com/)
- [StackOverflow](https://stackoverflow.com/)
- [Vue.js](https://vuejs.org/)
- [W3Schools](https://www.w3schools.com/)
- [Bootstrap Docs](https://getbootstrap.com/docs/5.3/getting-started/introduction/)
- [Figma](https://www.figma.com/)
- [DrawSQL](https://drawsql.app/)
## Samarbeidspartnere:
- Det kan hende jeg bruker Tor, mest sannsynlig relatert til sikkerhet eller noe backend greier.
- Kolleger, sikkert for frontend greier.
