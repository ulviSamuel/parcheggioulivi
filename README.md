# Parcheggio Ulivi

> A Java 11 command-line application for managing a multi-level car park, including vehicle check-in and check-out, parking-space allocation, rental spaces, and daily revenue tracking.

![Java](https://img.shields.io/badge/Java-11-007396?style=flat-square)
![Console Application](https://img.shields.io/badge/Project-Console%20Application-555?style=flat-square)
![Academic Project](https://img.shields.io/badge/Classification-Academic%20Project-6f42c1?style=flat-square)
![Year | 2022](https://img.shields.io/badge/Year%20%7C-2022-555?style=flat-square)

> [!NOTE]
> This repository contains an academic project originally developed during earlier programming studies. It is preserved as a record of the technical knowledge, design decisions, and development experience acquired at the time.

## Overview

Parcheggio Ulivi is an interactive console program that models a multi-level parking facility. It manages cars and scooters, assigns vehicles to different types of parking spaces, persists the parking state in CSV files, and calculates parking and rental revenue during the current run.

The application is a historical educational project rather than a production-ready service. Its user-facing messages are implemented in Italian.

## Features

- Check in cars and scooters after validating their license-plate format.
- Distinguish electric and non-electric cars, including optional placement in charging spaces.
- Display all spaces, only free spaces, or rentable spaces across the configured parking levels.
- Search for a parked vehicle by license plate.
- Rent and cancel rental contracts for car spaces.
- Check vehicles out and calculate the corresponding parking charge.
- Display daily revenue, including rental revenue.
- Persist parking-space state in the repository's CSV data files.

## Technology stack

- **Language:** Java
- **Runtime level:** Java 11
- **Interface:** Console input and output through `java.util.Scanner` and standard output
- **Persistence:** CSV files read and written with Java I/O classes
- **Project tooling:** Eclipse Java project metadata

## Architecture and project structure

The code is organized as a small console application with separate domain objects, business operations, and input utilities:

```text
.
├── src/it/volta/ts/ulivisamuel/parcheggioulivi/
│   ├── Main.java                 # Application entry point
│   ├── Console.java              # Menu and interactive workflows
│   ├── bean/                     # Vehicle and parking-space objects
│   ├── business/                 # Parking, vehicle, persistence, and revenue logic
│   ├── enumerations/             # Parking and vehicle-related enum values
│   └── util/                     # Console input helpers
├── pianoA.csv                   # Rentable car spaces
├── pianoAScooter.csv            # Scooter spaces
├── pianoB.csv                   # Ordinary car spaces
├── pianoBRicarica.csv           # Charging spaces for electric cars
├── pianoC.csv                   # Ordinary car spaces
├── .classpath                   # Eclipse classpath and Java 11 level
└── .project                     # Eclipse Java project definition
```

`Main` creates a `Console` instance, which coordinates the menu and delegates parking and revenue operations to the classes in `business`. `BizDataBase` loads and rewrites the five CSV files as operations change the parking state.

## Getting started

### Prerequisites

- A Java Development Kit compatible with Java 11.
- A shell capable of running the compilation command below, or Eclipse with Java support.

### Compile

From the repository root, compile the sources into a separate output directory:

```bash
mkdir -p /tmp/parcheggioulivi-build
javac --release 11 -encoding ISO-8859-1 \
  -d /tmp/parcheggioulivi-build \
  $(find src -name '*.java' -print)
```

The explicit `ISO-8859-1` encoding matches the legacy source files, which contain non-UTF-8 Italian text.

### Run from Eclipse

The repository contains Eclipse project metadata configured for Java 11:

1. Import the repository as an existing Eclipse Java project.
2. Confirm that the project uses a Java 11 JRE.
3. Run `src/it/volta/ts/ulivisamuel/parcheggioulivi/Main.java` as a Java application.

The program opens an interactive menu. Select `0` to exit.

### Data files

The application uses the five CSV files in the repository as its parking-state data store. The implementation refers to them through Windows-style relative paths (`..\parcheggioulivi\...`). As a result, the repository does not provide a verified cross-platform command-line runtime procedure; the Eclipse project configuration and path layout should be reviewed before running it outside the original environment.

## Testing

No automated test source files, test framework configuration, or test scripts are present in the repository.

## Project status

The Git history records iterative development from November to December 2022, including parking-space listing, check-in, vehicle search, rental, check-out, and revenue functionality. A later README-only commit is dated 2026, but no current maintenance or production deployment configuration is present.

## License

No license file or explicit license declaration is present in the repository. Licensing therefore requires human review.
