## Steps to create this repo

To leverage the recorder artifact from `azure-sdk-for-js` repo, we need the tests in a specific format in terms of code as well as the folder structure.

## Folder structure

```
- .gitignore (ignores `node_modules` and `.env`)
- package.json (dummy)
- rush.json (dummy)
- README.md (this file)
- sdk
  |_ service
     |_ service-sdk
        - package.json
        - package-lock.json
        - azure-tools-test-recorder-2.0.0.tgz
        - azure-test-utils-1.0.0.tgz
        - .env (Populate with `TABLES_SAS_CONNECTION_STRING` and `TEST_MODE`)
        |_ test
           - main.spec.ts (Actual test that uses the recorder with `@azure/data-tables` library)
```

## Setting up this repo & Running tests

- `cd sdk/service/service-sdk`
- Create a fresh `.env` file with `TABLES_SAS_CONNECTION_STRING` and `TEST_MODE`
- `npm install`
- `npm run test`

### Note:

`TEST_MODE` can take three values, "record", "playback" or "live"

- "live" - hits the live service, recorder is not involved
- "record" - records the requests and responses, generates recordings
- "playback" - plays the tests back using the recordings

## Refreshing "recorder" and "test-utils" artifacts

- Clone [Azure/azure-sdk-for-js](https://github.com/Azure/azure-sdk-for-js)
- `rush update`
- `cd sdk/test-utils/recorder`
- `rush build -t .`
- `rushx pack` (Generates azure-tools-test-recorder-2.0.0.tgz)
- `cd sdk/test-utils/test-utils`
- `rush build -t .`
- `rushx pack` (Generates azure-test-utils-1.0.0.tgz)
- Put them(`azure-tools-test-recorder-2.0.0.tgz` and `azure-test-utils-1.0.0.tgz`) in this repo at `sdk/service/service-sdk/`
