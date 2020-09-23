# Logging guidelines


## Log levels

| Level   | Description                                                                 |
|---------|-----------------------------------------------------------------------------|
| ERROR   | Something that should not happen and needs immediately attention            |
| WARNING | Something that needs attention but does not require immediately attention   |
| INFO    | Nice to have information during normal operations                           |
| DEBUG   | Logging that is useful during development                                   |

## Format
Json logging is preferred since we can easily add more context to the logging message (structured logging), for example a trace id can be added to correlated logging messages across services.
If you run the service in a docker container the simplest thing is to just log json with one of the preferred logging frameworks to STDOUT.

## Preferred loggers
To avoid using a lot of different configurations for multiple logging framework we recommend using the same logging framework for each language.

| Language  | Logging framework |
|-----------|-------------------|
| NodeJS    | winston           |
| Java      | logback           |

## Naming conventions for structured logging
Preferred to use DataDog naming conventions: https://docs.datadoghq.com/logs/processing/attributes_naming_convention/

## Error message
When writing your log entries messages, always anticipate that there are emergency situations where the only thing you have is the log file, from which you have to understand what happened. 
The message should contain: 

* Message about what went wrong
* Information about where the error happened. E.g class name, stack trace

## HTTP status responses
To make it easier to spot issues with our services it is important to return the correct status codes from our endpoints:

| Level   | Description                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| 500     | Internal server errors, only use if the service crashed for unknown reasons                     |
| 404     | If the endpoint does not exist, this should not be used as status code when an item is not found|
| 204     | Can be returned if the item was not found by an endpoint |                                      |