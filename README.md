# jamf-api-client-go

This repository contains an unoffical Go API client for Jamf REST API's.
  
  - [Jamf Classic API](https://www.jamf.com/developers/apis/classic/overview/)
    - [API Reference](https://www.jamf.com/developers/apis/classic/reference/)
    - [Code Samples](https://www.jamf.com/developers/apis/classic/code-samples/)
  - [Jamf Pro API](https://www.jamf.com/developers/apis/jamf-pro/overview/) **(TBD)**
    - [API Reference](https://www.jamf.com/developers/apis/jamf-pro/reference/)
    - **Note:** Development on the pro client has not been started, if any work is to be added here please keep in mind that the endpoints are prefaced with `v1` per the API Reference below and therfore the file structure should reflect `/pro/v1/*.go`

To see what functionality is available in the current API client release, please see the [API Coverage](https://github.com/DataDog/jamf-api-client-go/blob/main/docs/api_coverage.md) doc.
## Disclaimers

- The API client remains in active development and has no affiliation to [Jamf](https://github.com/jamf)
- This is **not** an official [Jamf](https://github.com/jamf) API client
- The client is **not** formally supported by Datadog and the code is available as-is

[Contribution](https://github.com/DataDog/jamf-api-client-go/blob/main/CONTRIBUTING.md) is welcome and appreciated! 🚀 💜
## Usage

```go
import  jamf "github.com/trustero/jamf-api-client-go/classic"

// You can optionally setup a custom HTTP client to use which can
// include any settings you desire. If you would like to use the 
// default client configuration just pass nil. This will default 
// to a client that is simply configured with a timeout of 1 minute
myCustomHTTPClient := &http.Client{
  Timeout: time.Minute,
}

// Create a client instance to interact with API
j, err := jamf.NewClient("https://jamf.example.com", "YOUR_API_USER", "YOUR_USERS_PASSWORD_HERE", myCustomHTTPClient)
if err != nil {
  fmt.Println(err.Error())
  os.Exit(1)
}

// Example: Get All Computers
computers, err := j.Computers()
if err != nil {
  os.Exit(1)
}

// Example: Create Script
newScript := &jamf.ScriptContents{
  Name: "Script with API Creation",
}
s, err := j.CreateScript(newScript)
if err != nil {
  os.Exit(1)
}

// Example: Get Script Details
scriptDetails, err := j.ScriptDetails(37)
if err != nil {
  os.Exit(1)
}
```

More examples available [here](https://github.com/DataDog/jamf-api-client-go/tree/main/examples)
### Tests

Unit tests should exist for all endpoints and pass successfully prior to being checked into the `main` branch

 `go test -v ./...` or `make test`

 Alternatively, `make pr-prep` can be run to execute all tests, formatting, and linting
