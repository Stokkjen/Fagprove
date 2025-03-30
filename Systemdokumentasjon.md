# Systemdokumentasjon

## Oppgave
Oppgaven er å lage en huskeliste app. Spesifiseringen ønsket å kunne lage, se, redigere og slette huskelister. Hver huskeliste er brukerspesifisert, men en skal kunne dele med andre. Det skal også være en frist, og en skal kunne be om å få notifikasjon når fristen nærmer seg. Notifikasjonen kunne være via epost / sms, eller så simpelt som noe i appen.

## Universell Utforming
Spesielt for telefon, har jeg brukt "kort" for informasjon, hvor informasjonen kommer opp i kort som skal være ganske enkle å forstå. Jeg bruker også knapper med farger som tilpasser hva knappen gjør (og tekst), for å prøve å gjøre det lett å forstå. For PC, har jeg byttet ut standarden i gridder for bit felter (check bokser) med like dynamiske knapper, for å gjøre det lettere å forstå og trykke.

## Lovverk
Jeg har gjort slik at ting blir ikke slettet. Hvis du inviterer folk til huskelista di, kan de fjerne lista, men de kan ikke slette den. Du kan lett filtrere slik at du kan finne fjernet lister, og få listen tilbake.

## Teknologi
### Omega365 CTP (Core Technology Platform) rammeverk
- Dette er en av bedriftens standarder, og det er noe jeg har mye erfaring med.
- Det er veldig grei å bruke, fordi det finnes mange ferdig-lagte komponenter, som for eksempel grids som jeg brukte mye av.
- Dette rammeverket består da av:
  - Vue.js
  - Bootstrap
  - SQL
### Figma
- Dette er et fint værktøy for å tegne opp en skisse av en eller flere apper.
### DrawSQL
- Dette er flott for å ha en fin oversikt over en datamodell.
### Github
- Dette er et veldig greit verktøy for å dokumentere ting på, og er lett å dele.
- Det er ryddig og ser fint ut, og det er lett å få inn bilder og lignende for å illustrere.

## Sikkerhet
### Capabilities
Her har jeg brukt noe som vi kaller Capabilities. Jeg har to capabilities. Disse kan du da legge til på en eller flere roller.
### Moduler
Moduler har tilganger på tabeller og apper. Da har jeg laget to moduler. Som nevnt så kan du også gi tilgang til tabeller (Read, Edit og Delete).
### Roller
Disse rollene er det som knytter Capabilities og Moduler til ett. Jeg har da to roller (lik Modulene). Disse knytter en da på noe som heter Org Units, og en person.
### Org Units
Dette er ikke veldig viktig for denne oppgaven, men simpelt forklart er dette en slags "lokasjon." Ved hjelpen av disse kan du da knytte roller til en person på en eller flere av disse lokasjonene.
### Custom view for tilganger
I SQL er det innebygde views som tillatter deg lett å sjekke hvilke capabilities noen har tilgang til. Jeg har da laget et view som er spesifisert mot dette systemet, som gjør sikkerheten meget lett å håndtere.
### Sikkerhets view til tabeller
Her sjekker jeg om du har tilgang til tabellen (via et annet innebygd view som returnerer alle tabeller du har tilgang til via modulene nevnt tidligere), og jeg sjekker også opp mot capabilities. Der blir det også litt mer custom basert på tabell.
### Triggere
Triggere kjører sikkerhetssjekk omtrent likt som sikkerhets viewet til tabellene. Disse triggerene er da sjekker og logikk som kjører etter INSERT, UPDATE eller DELETE av data i spesifikke tabeller. Da må jeg, likt som i sikkerhets viewet til tabellene, legge til en sjekk på om du har tilgang til tabellen, men i tillegg til det, må jeg sjekke om de har Edit eller Delete permissions, kommer ann på hvilken trigger.

## Arkitektur
### Frontend
- Setup Apper
  - Severities
  - States
- Hoved Apper
  - Lists
  - Tasks
### Backend (SQL)
- Tabeller
  - 
- Views
  - 

## Avvik og hindringer
For backend holdt jeg meg godt til planen. Det ble noen ting ekstra jeg måtte gjøre, men jeg vil ikke si det var noen avvik, og det ble ikke mange hindringer. Men, i frontend, ble det mange hindringer, og ting ser helt annerledes ut for telefon enn i planen min.
- Det ble mange flere views enn planlagt i planen. Dette var nødvendig for å vise nyttig informasjon.
- I selve appen hadde jeg planlagt å alt i en app (utenom setup appene). Jeg dele hele greia i to apper, altså en for listene, og en for oppgavene.
- 

## Planen videre
