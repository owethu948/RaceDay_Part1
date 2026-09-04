
# RaceDay â€“ Part 1: System Planning and Database

## About RaceDay

South Africa has a rich road events culture â€” from the Comrades Marathon and the Cape Town
Cycle Tour to the Soweto Marathon, the Two Oceans, and hundreds of local park runs, charity
rides, and community walks held every weekend. Despite huge participation, most of these
events are still run on paper registers, spreadsheets, and disconnected WhatsApp groups,
which leaves organisers overwhelmed and participants underserved.

**RaceDay** is a full-stack event management platform built for this community. Event
Organisers can create and manage events, categories, and participant results, while
Participants can browse upcoming events, enter events, track their personal performance
history, and prepare for race day using live weather and route information.

This repository contains **Part 1** of a three-part Portfolio of Evidence: system planning
and database design. No application/API code is written in this part â€” the goal is to prove
the system is understood before it's built.

## User Roles

| Role | Capabilities |
|---|---|
| **Organiser** | Create, edit, and delete events; manage event categories; capture participant results; view all enrolments for their events. |
| **Participant** | Create an account; browse events; enter an event by selecting a category; view their own enrolments; track their personal results/performance history. |

Both roles are stored in a single `Users` table (see `docs/ERD.png`), distinguished by a
`Role` column. Role-based access will be enforced at the API level in Part 2 and reflected
in the MVC interface in Part 3.

## Contents of this Part

| File | Description |
|---|---|
| `docs/ERD.png` / `docs/ERD.pdf` | Entity Relationship Diagram for the full RaceDay data model (6 entities: Users, UserProfiles, Events, Categories, Enrolments, Results) with primary keys, foreign keys, and cardinality. |
| `docs/API-Endpoint-Plan.md` | Full planned API surface â€” every endpoint's method, route, description, required role, request body, and expected response â€” covering Auth, User Profile, Events, Categories, Enrolments, and Results. |
| `docs/RaceDay_Schema.sql` | SQL Server script that creates the full database schema matching the ERD exactly, including all constraints and seed data (2 Organisers, 2 Participants, 3 Events, categories per event, and sample enrolments/results). |

## Data Model Summary

- **Users** â€” login/auth record for both Organisers and Participants (`Role` column).
- **UserProfiles** â€” 1:1 extended profile info per user (name, phone, DOB, emergency contact).
- **Events** â€” created by an Organiser; has a date, location, and description.
- **Categories** â€” belongs to an Event (e.g. 10km, 21km, 87.7km); has a distance, fee, and capacity.
- **Enrolments** â€” links a Participant to a Category they've entered.
- **Results** â€” 1:1 with an Enrolment; the finish time, position, and status captured by the Organiser.

## Running the SQL Script

1. Open **SQL Server Management Studio (SSMS)** and connect to a local/clean SQL Server instance.
2. Open `docs/RaceDay_Schema.sql`.
3. Execute the script (F5). It will create the `RaceDayDB` database if it does not exist,
   drop/recreate the six tables in dependency order, and seed sample data.
4. Verify with `SELECT * FROM dbo.Users;` etc.

## CI/CD

A GitHub Actions workflow (`.github/workflows/`) validates the repository structure for this
part â€” confirming the `/docs` folder exists and contains the ERD, endpoint plan, and SQL
script.

**Green build screenshot:**

`[INSERT CI/CD green-check screenshot here before submission]`

## Video Walkthrough

Unlisted YouTube link (planning documents, ERD decisions, endpoint plan choices, and the SQL
script run live in SSMS):

`[INSERT UNLISTED YOUTUBE LINK HERE]`

