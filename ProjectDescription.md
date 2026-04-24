# Project Description

## Summary

Pollinator Habitat is a full-stack web application developed for **Conner Prairie's** *Food, Farm, and Energy Experience*. It digitizes and enhances Conner Prairie's existing paper-based pollinator educational activity, making it accessible to all age groups and ability levels.

Visitors scan a QR code with their mobile device and are automatically connected to the active session. The app then guides them through a **dichotomous key** route walk — a series of physical characteristic clues that progressively narrow down a secretly assigned pollinator. Upon identifying their pollinator, visitors are presented with educational facts about it and can add it to their personal collection.

A companion **Admin Portal** allows Conner Prairie staff to search, review, and export participant data for grant reporting and program analysis, without collecting any personally identifiable information.

## High-Level Features

- **Route Walk (Dichotomous Key):** Visitors follow a guided route through the park, using on-screen clues to identify their randomly assigned pollinator. The app cycles through all available pollinators before repeating, ensuring variety across repeated plays.
- **Pollinator Collection:** Discovered pollinators are saved to the visitor's session. Silhouette sprites unlock into full-color images upon discovery. Completed pollinators can be replayed from the collection page.
- **Accessibility Settings:** Visitors can enable High Contrast Mode, Text-to-Speech (TTS), and adjust font size (75–150%) from the Accessibility Settings page. All settings persist across the session.
- **Optional Survey:** Visitors can optionally submit a party size survey (number of adults and children). Submissions from the same device within a 24-hour window replace the previous entry rather than creating duplicates.
- **Admin Portal — Survey Data Tool:** Staff can search party-size survey responses by date, date range, or session ID and export results to CSV.
- **Admin Portal — Route Data Tool:** Staff can search route activity statistics by date or date range, viewing Activity Overview, Positive Trends, and Missed Opportunities tables, with CSV export.
- **Admin Portal — Quick Export Tool:** Staff can generate and download a CSV report for survey or route data over a chosen time period (last month through all-time) with a single button press.
- **QR Code Access:** Visitors connect via QR code — no app download required. The system runs entirely in the mobile browser.
- **No PII Collection:** The system does not collect any personally identifiable information. Participants are tracked only via anonymous, randomly generated player IDs scoped to a single session.

## Non-Functional Requirements

- **Accessibility:** The application must be usable by visitors of all ages and ability levels, including individuals with low vision, color blindness, mobility limitations, and dyslexia. It must work on any modern smartphone browser at any screen size.
- **Performance:** The app must load and respond quickly on the Conner Prairie campus WiFi network. Route transitions and API responses must feel immediate during an active session.
- **Reliability:** The system must run continuously during Conner Prairie operating hours without manual intervention. All services run in Docker containers to simplify deployment and restarts.
- **Data Privacy:** No personally identifiable information is collected or stored. Participant data is limited to anonymous usage statistics aggregated at the session level.
- **Portability:** The system must run on the dedicated Conner Prairie workstation (Windows 10/11 with WSL2 and Docker Desktop) and be maintainable by non-developer staff following written instructions.
- **Maintainability:** New pollinator routes and facts can be added by updating the database seed file. All system configuration is controlled via environment variables. No hardcoded credentials or paths.

## Constraints

- **No App Store:** The application must run entirely in the mobile browser — visitors must not be required to install anything.
- **Single Workstation Deployment:** All services (frontend, portal, backend, database, reverse proxy) run on a single dedicated workstation at Conner Prairie using Docker Compose.
- **No PII:** The system must not collect, store, or transmit any personally identifiable information about activity participants, in keeping with Conner Prairie's privacy policy and to avoid data privacy regulatory overhead.
- **Campus WiFi Dependency:** The application requires visitors to be connected to the Conner Prairie campus WiFi network. Connectivity issues on specific campus networks are outside the application's control.
- **MySQL GPL License:** MySQL 8.4 is suitable for internal use at Conner Prairie. If this application were ever redistributed or offered as a commercial service, the MySQL GPL license would require a commercial license. PostgreSQL is included as a fully supported alternative for that scenario.
