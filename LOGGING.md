# Logging guidelines


## Log levels

| Level   | Description                                                                 |
|---------|-----------------------------------------------------------------------------|
| ERROR   | Something that should not happen and needs immediately attention            |
| WARNING | Something that needs attention but does not require immediately attention   |
| INFO    | Nice to have information during normal operations                           |
| DEBUG   | LLogging that is useful during development                                  |

## Format
Json logging is prefered since we can easily add more context to the logging message (structured logging), for example a trace id can be added to correlated logging messages across services.

## Prefered loggers

To avoid using a lot of different configurations for multiple logging framework we recommend using the same logging framework for each language.

| Language  | Logging framework |
|-----------|-------------------|
| NodeJS    | winston           |
| Java      | logback           |

## Naming convensions for structured logging
Prefere to use DataDog nameing convensions: https://docs.datadoghq.com/logs/processing/attributes_naming_convention/

## Error message
When writing your log entries messages, always anticipate that there are emergency situations where the only thing you have is the log file, from which you have to understand what happened. 


Try to write self healing code, for example backoff if there are a lot of errors and try again in X seconds.