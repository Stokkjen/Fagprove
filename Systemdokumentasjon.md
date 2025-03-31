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
- Setup Apper (Tilgjengelig for de som har "To Do Setup Administrator" rollen)
  - Severities - Her kan en legge til "Severities" som vises opp i lista når, i hovedappene, en velger en severity.
    - "Severities" er for eksempel: "Critical", "Low", "High" etc.
  - States - Det samme som "Severities", bare for "States".
    - "States" er for eksempel: "To Do", "Deleted", "Finished" etc.
- Hoved Apper (Tilgjengelig for de som har "To Do Customer" rollen)
  - Lists - Dette er appen hvor en har en oversikt over alle listene. Det er også en oversikt over folk som har tilgang til lista og hva tilgang de har. Hvis en er på telefon, vil denne informasjonen vises som "kort", som gjør det lettere å observere på telefon. For PC, vil informasjonen vises i grid. I tillegg, siden PC har mye større skjerm, få "Tasks" appen ved siden av.
  - Tasks - Her kan en lage, se, redigere og slette oppgaver. En kan også sette notifikasjoner på en oppgave (så lenge den har en frist), hvor en setter notifikasjonen til å bli aktiv så så lenge før fristen. Når notifikasjonen da er aktiv, vil den dukke opp i appen. I tillegg, vil "Lists" appen også få en notifikasjonsliste over lister som har en eller flere oppgaver som har en aktiv notifikasjon.
### Backend (SQL)
- Tabeller
  - Lists - En oversikt over lister. Den har bare tittel, og et bitfelt som sier om listen er fjernet eller ikke.
  - Subscribers - Folk som har tilgang til lister, og hvilken tilgang.
  - Tasks - Her står det informasjon om oppgaven, som tittel, beskrivelse og frist, og i tillegg kan du legge til en stat og alvorlighetsgrad.
  - States - Her kan du sette en stat, som for eksempel: "To Do", "Deleted", "Finished" etc.
  - Severities - Her ligger det alvorlighetsgrader, som for eksempel: "Critical", "Low", "High" etc.
  - Notifications - Her ligger alle notifikasjoner, altså notifikasjoner du kan legge til på en oppgave for å følge med på den.
  - NotificationSubscribers - Her kobler vi en person opp mot en notifikasjon. Så da kan flere ha samme notifikasjoner.
- Views
  - Lists - Denne velger fra "Lists" tabellen, men inkluderer for eksempel "ProgressPercentage", "IsCompleted", og noen andre kjekke ting som tilganger (i følge "Subscribers" tabellen)
  - ListsNotifications - Dette viewet velger alle aktive notifikasjoner, og simplifiserer de til en per liste. Da kan du, i "Lists" appen, se alle lister som har en aktiv notifikasjon.
  - MyCapabilities - Alt denne gjør er å sjekke hvilke capabilities du har.
  - Notifications - Velger fra "Notifications" tabellen, men den bruker også "NotificationSubscribers" for å sjekke om du følger med på notifikasjonen.
  - Subscribers - Velger fra "Subscribers" tabellen, men inkluderer sjekker for om det er du som er subscriber, eller om subscriberen er den som har laget listen.
  - Tasks - Velger rett fra "Tasks" tabellen, men inkluderer stat og alvorlighetsgrad, og har i tillegg en sjekk på om oppgaven er fjernet eller fullført.
  - TasksNotifications - Returnerer alle aktive notifikasjoner, og hvilken oppgave den tilhører.
- Prosedyrer
  - EraseList - Med tanke på "rett til å bli glemt", har jeg laget en prosedyre som sletter alt fra en liste.
  - SendNotifications - Ubrukt grunnet manglet forståelse, men virker. Denne skulle bli kjørt av en jobb hver time, som sjekker om det er noen nye notifikasjoner tilgjengelig. Hvis det er det, så sender den det ut på mail til alle som har valgt å følge med på notifikasjonen. Men igjen, hvordan ting faktisk funker bak vet jeg ikke nok av, så jeg byttet dette ut med bjellene i appen.

## Avvik og hindringer
For backend holdt jeg meg godt til planen. Det ble noen ting ekstra jeg måtte gjøre, men jeg vil ikke si det var noen avvik, og det ble ikke mange hindringer. Men, i frontend, ble det mange hindringer, og ting ser helt annerledes ut for telefon enn i planen min.
- Det ble mange flere views enn planlagt i planen. Dette var nødvendig for å vise nyttig informasjon.
- I selve appen hadde jeg planlagt å alt i en app (utenom setup appene). Jeg dele hele greia i to apper, altså en for listene, og en for oppgavene.

## Planen videre
- Hvis en person har fullført en oppgave som har en aktiv notifikasjon, vil jeg at alle som hadde meldt seg på den notifikasjonen skal få en ny notifikasjon hvor det står at noen fullførte det. Jeg hadde en ide for dette som involverer en cache tabell, men fikk ikke tid.
- Notifikasjonene som dukker opp når du trykker bjellene burde kunne trykkes (for å åpne en liste eller oppgave) for å få en mye simplere opplevelse.
- Notifikasjons systemet burde generelt sett være mer brukervennlig, altså å sende mail eller sms i stedenfor. Dette fikk jeg til å gjøre, men jeg skrudde det av, siden jeg forstår ikke helt hvordan det funker, så jeg gikk for det jeg har nå, som jeg kan "eie", siden jeg forstår det.
- Frontenden endte ikke opp med å være veldig lett å forstå. Det er noen ting på mobil som kunne bli gjort klarere, og spesielt på PC, kunne ting vært annerledes.
- Legge til tags, slik at en kan lettere filtrere og sortere ting.
