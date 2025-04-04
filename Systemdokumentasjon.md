# Systemdokumentasjon

## Oppgave
Oppgaven er å lage en huskeliste app. Spesifiseringen ønsket å kunne lage, se, redigere og slette huskelister. Hver huskeliste er brukerspesifisert, men en skal kunne dele med andre. Det skal også være en frist, og en skal kunne be om å få notifikasjon når fristen nærmer seg. Notifikasjonen kunne være via epost / sms, eller så simpelt som noe i appen.

## Universell Utforming
Spesielt for telefon, har jeg brukt "kort" for informasjon, hvor informasjonen kommer opp i kort som skal være ganske enkle å forstå. Jeg bruker også knapper med farger som tilpasser hva knappen gjør (og tekst), for å prøve å gjøre det lett å forstå. For PC, har jeg byttet ut standarden i gridder for bit felter (check bokser) med like dynamiske knapper, for å gjøre det lettere å forstå og trykke.

## Lovverk
Jeg har gjort slik at ting blir ikke slettet. Hvis du inviterer folk til huskelista di, kan de fjerne lista, men de kan ikke slette den. Du kan lett filtrere slik at du kan finne fjernet lister, og få listen tilbake.
Som bonus, har jeg også gjort slik at, hvis du vil, kan den som har laget listen slette alt som ligger inni der. Dette ligner på "Retten til å bli glemt", men det handler hovedsaklig om personopplysninger. Dette er fortsatt viktig, siden det kan hende at noen har sensitiv informasjon i en liste.

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
Her har jeg brukt noe som vi kaller Capabilities. Jeg har to capabilities ("Can Administrate To Do Setup" og "Can Manage To Do Lists"). Disse kan du da legge til på en eller flere roller. Capabilities er tilganger til spesifikke ting. Jeg har brukt capabilities for å sjekke (hovedsaklig i triggere) om du har tilgang til å, for eksempel, jobbe med huskelister.
### Moduler
Moduler har tilganger på tabeller (Read, Edit og Delete) og apper. Da har jeg laget to moduler ("To Do Customer" og "To Do Setup Administrator").
### Roller
Disse rollene er det som gir tilgang til Capabilities og Moduler. Jeg har da to roller ("To Do Customer" og "To Do Setup Administrator", lik Modulene). Disse knytter en da på noe som heter Org Units, og en person.
### Org Units
Dette er ikke veldig viktig for denne oppgaven, men simpelt forklart er dette en slags "lokasjon." Ved hjelpen av disse kan du da knytte roller til en person på en eller flere av disse lokasjonene.
### Custom view for tilganger
Omega har innebygde views i alle Omega databaser som tillatter deg lett å sjekke hvilke capabilities noen har tilgang til. Jeg har da laget et view ("MyCapabilities") som er spesifisert mot dette systemet, som gjør sikkerheten meget lett å håndtere.
### Sikkerhets view til tabeller
Her sjekker jeg om du har tilgang til tabellen (via et annet innebygd view som returnerer alle tabeller du har tilgang til via modulene nevnt tidligere), og jeg sjekker også opp mot capabilities. Der blir det også litt mer custom basert på tabell.
### Triggere
Triggere kjører sikkerhetssjekk omtrent likt som sikkerhets viewet til tabellene. I disse triggerene kan du lage egen sikkerhetssjekker og logikk som kjøres etter INSERT, UPDATE eller DELETE av data.

## Arkitektur
### Frontend
Setup Apper (Tilgjengelig for de som har "To Do Setup Administrator" rollen):
- Severities - Her kan en legge til "Severities" som vises opp i lista når, i hovedappene, en velger en severity.

![image](https://github.com/user-attachments/assets/6d1e4f0e-78f6-4590-952e-e40ea57c6f40)
- States - Det samme som "Severities", bare for "States". Her har jeg inkludert to bit felter, som skal hjelpe på med hvordan ting skal sorteres, filtreres osv.

![image](https://github.com/user-attachments/assets/68c5663d-bd96-400e-ba86-d6b714b21366)

Hoved Apper (Tilgjengelig for de som har "To Do Customer" rollen):
- Lists - Dette er appen hvor en har en oversikt over alle listene. Det er også en oversikt over folk som har tilgang til lista og hva tilgang de har. Hvis en er på telefon, vil denne informasjonen vises som "kort", som gjør det lettere å observere på telefon. For PC, vil informasjonen vises i grid. I tillegg, siden PC har mye større skjerm, få "Tasks" appen ved siden av.

![image](https://github.com/user-attachments/assets/b5eb1ab7-7f02-427f-8ecd-f61a8cce0eac)
- Tasks - Her kan en lage, se, redigere og slette oppgaver. En kan også sette notifikasjoner på en oppgave (så lenge den har en frist), hvor en setter notifikasjonen til å bli aktiv så så lenge før fristen. Når notifikasjonen da er aktiv, vil den dukke opp i appen. I tillegg, vil "Lists" appen også få en notifikasjonsliste over lister som har en eller flere oppgaver som har en aktiv notifikasjon.

![image](https://github.com/user-attachments/assets/3fdeb031-2390-40fa-95a9-f7a0d1aa7738)
### Backend (SQL)
- Tabeller ([DrawSQL](https://drawsql.app/teams/omega365-1/diagrams/todo-list-end))
![image](https://github.com/user-attachments/assets/53679f87-a625-4ffe-ad8f-b88b7b63139a)
  - Lists - En oversikt over lister. Den har bare tittel, og et bitfelt som sier om listen er fjernet eller ikke.
  - Subscribers - Folk som har tilgang til lister, og hvilken tilgang.
  - Tasks - Her står det informasjon om oppgaven, som tittel, beskrivelse og frist, og i tillegg kan du legge til en state og severity.
  - States - Her kan du sette en state, som for eksempel: "To Do", "Deleted", "Finished" etc.
  - Severities - Her ligger det alvorlighetsgrader, som for eksempel: "Critical", "Low", "High" etc.
  - Notifications - Her ligger alle notifikasjoner, altså notifikasjoner du kan legge til på en oppgave for å følge med på den.
  - NotificationSubscribers - Her kobler vi en person opp mot en notifikasjon. Så da kan flere ha samme notifikasjoner.
- Views
  - Lists - Denne velger fra "Lists" tabellen, men inkluderer for eksempel "ProgressPercentage", "IsCompleted", og hvilke tilganger du har for listen i følge "Subscribers" tabellen.
  - ListsNotifications - Dette viewet velger alle aktive notifikasjoner, og simplifiserer de til en per liste. Da kan du, i "Lists" appen, se alle lister som har en aktiv notifikasjon.
  - MyCapabilities - Alt denne gjør er å sjekke hvilke capabilities du har.
  - Notifications - Velger fra "Notifications" tabellen, men den bruker også "NotificationSubscribers" for å sjekke om du følger med på notifikasjonen.
  - Subscribers - Velger fra "Subscribers" tabellen, men inkluderer sjekker for om det er du som er subscriber, eller om subscriberen er den som har laget listen.
  - Tasks - Velger rett fra "Tasks" tabellen, men inkluderer state og severity, og har i tillegg en sjekk på om oppgaven er fjernet eller fullført.
  - TasksNotifications - Returnerer alle aktive notifikasjoner, og hvilken oppgave den tilhører.
- Prosedyrer
  - EraseList - Jeg har lyst at hvis folk f.eks har sensitiv informasjon på en liste kan slette det fullstendig, så jeg har laget en prosedyre som sletter alt fra en liste.
  - SendNotifications - Ubrukt grunnet manglet forståelse, men virker. Denne skulle bli kjørt av en jobb hver time, som sjekker om det er noen nye notifikasjoner tilgjengelig. Hvis det er det, så sender den det ut på mail til alle som har valgt å følge med på notifikasjonen. Men igjen, hvordan ting faktisk funker bak vet jeg ikke nok av, så jeg byttet dette ut med bjellene i appen.

## Avvik og hindringer
For backend holdt jeg meg godt til planen. Det ble noen ting ekstra jeg måtte gjøre, men jeg vil ikke si det var noen avvik, og det ble ikke mange hindringer. Men, i frontend, ble det mange hindringer, og ting ser helt annerledes ut for telefon enn i planen min.
- Det ble mange flere views enn planlagt i planen. Dette var nødvendig for å vise nyttig informasjon.
- I selve appen hadde jeg planlagt å få alt i bare en app (utenom setup appene). Jeg delte hele greia i to apper, altså en for listene, og en for oppgavene. Dette var litt for å gjøre ting simplere, og lettere spesielt på telefon, siden i stedenfor å skifte tabs eller åpne en modal eller noe greier, må de bare trykke en knapp, så kommer de der de skal.
- Jeg brukte kort i stedenfor grids for telefon. Dette er en ganske nødvendig endring da, spesielt på telefon, siden det er mye mer oversiktlig.
- Det tok altfor lang tid med frontenden. Til slutt endet jeg med et OK system, som skal virke, men som kan være forvirrende.
- Jeg tok tiden min til å lage notifikasjoner som ble sendt ut på mail til punktet hvor det virket, men siden det var hull i min forståelse rundt det, skrudde jeg dette av.
  - All tiden ble ikke bortkastet da, siden jeg tok litt av "SendNotifications" prosedyren, og gjorde det om til to views: "ListsNotifications" og "TasksNotifications", som blir brukt til notifikasjoner i appen.

## Planen videre
- Hvis en person har fullført en oppgave som har en aktiv notifikasjon, vil jeg at alle som hadde meldt seg på den notifikasjonen skal få en ny notifikasjon hvor det står at noen fullførte det. Jeg hadde en ide for dette som involverer en cache tabell, men fikk ikke tid.
- Notifikasjonene som dukker opp når du trykker bjellene burde kunne trykkes (for å åpne en liste eller oppgave) for å få en mye simplere opplevelse.
- Notifikasjons systemet burde generelt sett være mer brukervennlig, altså å sende mail eller sms i stedenfor. Dette fikk jeg til å gjøre, men jeg skrudde det av, siden jeg forstår ikke helt hvordan det funker, så jeg gikk for det jeg har nå, som jeg kan "eie", siden jeg forstår det.
- Frontenden endte ikke opp med å være veldig lett å forstå. Det er noen ting på mobil som kunne bli gjort klarere, og spesielt på PC, kunne ting vært annerledes.
- Legge til tags, slik at en kan lettere filtrere og sortere ting.
