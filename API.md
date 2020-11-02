# API Specs

## Installation

Each installable app will require a manifest file accessible via backstack bot

Manifest includes:

- app.json
    - App GUID (never changes)
    - App Name
    - Author
    - Other basic info (license, github link, etc)
- install.json
    - GUID (changes with each update)
    - Timestamp
    - Basic schema
- seed.json
    - GUID (changes with each update)
    - Timestamp
    - Any data that's needed in a fresh install
- migrations.json
    - Array of state changes over time
    - State change records include
        - GUID
        - Timestamp
        - Scripts to run that mutate schema
        - Data changes

JSON may very well not be the way to go for these. Some sort of imperative "playbook" might be a better fit.

Need a way to keep local application state (and schema) in sync with user stores. Keeping track of timestamps and handling changes as "migrations" might be the way to go, however it would also be good to keep the most recent version of the schema stored with the user (or at least the timestamp and guid).

- Full "fresh install" schema and data files should always be present, representing the current state of the app.

- Partial migrations should also exist, starting form the beginning state and tracking changes and mutations over time for incremental updates.