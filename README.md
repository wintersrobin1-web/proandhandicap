# Teamsport Pro- und Handicap Generator

Kompakte Web-App für den Sportunterricht: Teams erstellen, Kleinfeldspiele organisieren, Spielstand und Beteiligung grob erfassen und passende Pro-/Handicap-Regeln für die nächste Runde ausgeben.

## Funktionen

- Klassen lokal im Browser speichern
- Teams nach Anzahl/Feldlogik erstellen
- Offline-Modus ohne Internet-Datenbank
- Live-Session mit Firebase für mehrere iPads
- QR-Code/Link für iPads
- globale Uhr und Feld-Uhren
- Tore und Beteiligung synchron erfassen
- Pro-/Handicap-Karten bearbeiten, aktivieren/deaktivieren
- Sportart-Profil auswählen
- Regelübersicht für iPad/Beamer

## Dateien

- `teamsport_pro_handicap_generator_live_offline_v24.html`  
  Hauptdatei der App.

Optional:
- `teamsport_pro_handicap_generator_live_offline_v24.txt`  
  gleicher Code als Textdatei zum Kopieren/Einsehen.

## Offline nutzen

1. HTML-Datei herunterladen.
2. Datei im Browser öffnen.
3. Namen eintragen oder Klasse laden.
4. Teams/Felder erstellen.
5. Spielstände und Beteiligungen direkt auf dem Lehrkraftgerät eintragen.
6. Pro-/Handicaps auswerten.

Hinweis: Offline funktioniert nur auf dem jeweiligen Gerät. Andere iPads können dann nicht live synchronisieren.

## Live-Session mit mehreren iPads nutzen

Voraussetzung: Firebase-Projekt ist eingerichtet:

- Firestore Database erstellt
- Authentication → Anonymous aktiviert
- Firestore-Regeln veröffentlicht

Empfohlene Test-Regeln:

```js
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /teamsportSessions/{sessionId} {
      allow read, write: if request.auth != null;
    }
  }
}
```

Ablauf:

1. HTML-Datei online bereitstellen, z. B. über GitHub Pages.
2. App auf dem Lehrkraftgerät öffnen.
3. Klasse laden oder Namen eingeben.
4. Teams/Felder erstellen.
5. Live-Session erstellen.
6. QR-Code oder iPad-Link anzeigen.
7. SuS/iPads treten über QR-Code oder Raumcode bei.
8. Spielstand, Uhr und Beteiligung werden synchronisiert.
9. Nach der Stunde Session löschen.

## Einbindung über GitHub Pages

1. GitHub öffnen und neues Repository erstellen.
2. HTML-Datei in `index.html` umbenennen.
3. `index.html` ins Repository hochladen.
4. In GitHub auf `Settings` → `Pages` gehen.
5. Unter `Build and deployment` auswählen:
   - Source: `Deploy from a branch`
   - Branch: `main`
   - Folder: `/root`
6. Speichern.
7. GitHub zeigt danach eine Seiten-URL an.
8. Diese URL auf iPads öffnen oder über den QR-Code in der App nutzen.

## Unterrichtlicher Einsatz

Empfohlen für Kleinfeldspiele, z. B. 3 gegen 3 oder 4 gegen 4. Wenn Teams größer sind, werden Wechselspieler:innen/Coachrollen mitgedacht. Wechselspieler:innen bleiben bei der Beteiligung auswählbar.

Beobachtung pro Team:

- War oft beteiligt
- War auch oft beteiligt
- Kam wenig ins Spiel
- Kam auch wenig ins Spiel

Die App schlägt anschließend kompakte Pro-/Handicap-Regeln für die nächste Runde vor.

## Datenschutz-Hinweise

- Möglichst nur Vornamen, Kürzel oder Nummern verwenden.
- Keine dauerhafte Leistungsbewertung speichern.
- Session nach der Stunde löschen.
- Für Schuleinsatz Datenschutz/Schulleitung klären.
- Offline-Modus ist datensparsamer als Live-Firebase.

## Typische Fehler

**Raum erstellen klappt nicht**

Prüfen:
- Firestore erstellt?
- Anonymous Auth aktiviert?
- Regeln veröffentlicht?
- Internetverbindung vorhanden?

**QR-Code öffnet falsche Seite**

Die App muss online erreichbar sein. Bei lokaler `file://`-Datei funktioniert der QR-Link auf anderen iPads nicht zuverlässig.

**iPads synchronisieren nicht**

Alle Geräte müssen dieselbe aktuelle Version der HTML-Datei nutzen. Alte Tabs schließen und Raum neu erstellen.
