# Daglig logg
## 25.03.25 - Tirsdag:
- Gikk gjennom informasjon om fagprøven.
- Tegnet skisser med DrawSQL (datamodell) og Figma (apper).
- Skrevet planleggingen.
- Satt på plass basic sikkerhet med roller, moduler og capabilities.
- Definert tabeller i DrawSQL skissen.
## 26.03.25 - Onsdag
- Fått på plass sikkerhet i tabell views og triggere.
- Laget views spesifisert.
- Laget setup apps.
- Begynt på hoved app.
- Laget alle grids.
  - Avvik: I figma skissene brukte jeg checkbokser for å endre bit felter. Grunnet universell utforming og mobil i tanken har jeg gjort slik at du trykker på en klar og farget knapp (med dynamisk tekst for å gjøre det lett å forstå). Det kan hjelpe ikke bare med forståelse, men siden knappen er relativt stor, mens checkboksen liten, er det også lettere å trykke på.
## 27.03.25 - Torsdag
- Jobbet med hovedappen.
  - Hindring: Jeg har hatt store utfordringer med å få appen til å ha et intuitivt design, og jeg har også brukt mye tid på å finne ut av hvordan jeg skriver frontenden for å tilpasse det. Dette er noe som har tatt mesteparten av dagen, og jeg er fortsatt langt fra ferdig.
- Laget 2 tabeller. Disse står ikke i planleggingen min, men de er nødvendige tabeller for å få notifikasjoner på plass. (ToDo_Notifications og ToDo_NotificationSubscribers.)
  - Sikkerhet er på plass også.
- Laget en prosedyre for å få funksjonaliteten til notifikasjoner til å virke. (ToDo_SendNotifications.) Denne inserter informasjon om en epost inn i en tabell, som da blir sendt videre til mail via en jobb som aktiverer et c# skript.
- Til slutt har jeg lagt til en grid for notifikasjonene.
## 28.03.25 - Fredag
- Begynt å endre hvordan appen ser ut. Oppgave vinduet er nå kort i stedenfor grids, for å få det til å se mer intuitivt ut.
  - Laget en modal som popper opp når du trykker på en oppgave, hvor du kan redigere oppgaven (og slette den).
- For mobil har jeg gjort lister om til kort for samme grunn.
- Begynt med å endre hvordan notifikasjoner virket. Har laget 2 views, som ikke sto i planleggingen, som er nødvendig for å vise notifikasjoner i appen.
## (29-30).03.25 - Helg
- Jobbet mye med frontend delen.
  - Gjort slik at alt på mobil bruker cards.
  - Lagt til all krevende funksjonalitet, lik som det var i griddene.
    - Det er noen mangler her jeg vil fikse de neste to dagene.
  - Har lagt til notifikasjonsbjeller for oversikt over lister og oversikt over oppgaver.
## 31.03.25 - Mandag
- Fikset mange bugs / feil.
- Lagt til ting som kan være nyttig.
  - Hovedgreia her er "Erase," en ny knapp jeg har lagt til grunnet lovverk. En skal ha "retten til å bli glemt," så jeg har gjort slik at den som lager en liste får nå muligheten til å ta en full slett av hele lista. (Det kommer opp advarsel.)
- Ryddet opp i koden.
- Gjort en del testing.
- Begynt litt på systemdokumentasjon.
