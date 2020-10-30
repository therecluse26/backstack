# Notes

### Basic structure

- BackStack schema

- Config

    - Establishes basic user policies

    - Disk space and bandwidth allocations

    - Request rate limit per app

- Users - Global user store

    - Auth info

    - Extended user info (optional) - name, avatar, bio, dob, etc

    - Usage info (disk and bandwidth)

    - Other metadata necessary for basic functionality

- User.Apps

### User Flow

- User visits application and is prompted to sign in or register

- Registration prompts user for basic login info - username, email, password (x2)

- New user is saved to Users database

- Verification email is sent to user

- User follows verification link that forwards to back to API verify url, and is presented with success or error

- User logs in

- Client sends request to server to see if application is setup within their environment - sends basic application manifest (with app GUID) to API

    - Check if app is installed in User.Apps schema

- User is presented with loading screen

- If not currently installed, upload install file to API bootstrap endpoint

    - API parses file and runs install scripts to setup application database

- Else if already installed, check most recent update GUID and timestamp between client and server

    - If out of date, upload migrations file to API update endpoint

    - API parses file and runs install scripts to sync application database

- Application is presented to user for interaction


## Application flow

- State is stored locally

- Most recent state change timestamp is always kept up to date