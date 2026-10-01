# Kartverket – Hinderregistrering (Oppgave 1)

> Første versjon av gruppeprosjektet i IS-202. Den videreutviklede løsningen ligger i [kart-oppgave](https://github.com/Phiri-Madalitso/kart-oppgave).

![.NET](https://img.shields.io/badge/ASP.NET_Core_MVC-512BD4?logo=dotnet&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?logo=mariadb&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)

System for innmelding og kontroll av luftromshindringer. Applikasjonen lar piloter registrere hindringer i luftrommet. Registerfører i NRL (Nasjonalt register over luftfartshindre) kan så godkjenne eller avvise innmeldingene. Målet er bedre flysikkerhet gjennom et oppdatert register.

## Teknologi

- ASP.NET Core MVC
- Entity Framework Core
- MySQL/MariaDB
- Docker / docker-compose

## Arkitektur

Løsningen følger Model–View–Controller (MVC)-mønsteret:

- **Model**: domeneklasser og valideringslogikk
- **View**: Razor Views for skjemaer, oversiktssider, kart og tilbakemeldinger
- **Controller**: ruting og forretningslogikk
- **Database**: MySQL/MariaDB via Entity Framework Core med migrasjoner gjennom `ApplicationDbContext`

## Dataflyt

1. Brukeren åpner startsiden (Home → Index).
2. Piloten registrerer en hindring i skjemaet (Index → ObstacleData).
3. Input valideres med modellattributter.
4. Gyldige innsendelser vises på oversiktssiden (OverView).

## Drift

Applikasjonen er pakket med Docker. Med docker-compose startes webapplikasjonen og databasen i hver sin container:

- Webdelen kjører på `mcr.microsoft.com/dotnet/aspnet:9.0`
- Databasen kjører i en MariaDB-container
- Komponentene kommuniserer via et felles Docker-nettverk
