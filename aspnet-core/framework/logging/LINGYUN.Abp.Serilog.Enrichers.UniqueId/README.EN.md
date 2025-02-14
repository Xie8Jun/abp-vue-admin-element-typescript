# LINGYUN.Abp.Serilog.Enrichers.UniqueId

[简体中文](./README.md) | English

A Serilog enricher that adds unique identifiers to log properties using the Snowflake algorithm.

## Features

* Adds unique identifier to each log event
* Uses Snowflake algorithm for distributed unique ID generation
* Supports custom Snowflake algorithm configuration
* Supports both code-based and configuration-based setup
* Seamless integration with Serilog

## Module Dependencies

```csharp
[DependsOn(typeof(AbpSerilogEnrichersUniqueIdModule))]
public class YouProjectModule : AbpModule
{
  // other
}
```

## Configuration Options

### Constants

* AbpSerilogUniqueIdConsts.UniqueIdPropertyName - Name of the unique identifier field, defaults to "UniqueId"

### Snowflake Configuration

Configure Snowflake algorithm parameters through `AbpSerilogEnrichersUniqueIdOptions`:

```json
{
  "UniqueId": {
    "Snowflake": {
      "WorkerId": 1,        // Worker machine ID
      "DatacenterId": 1,    // Datacenter ID
      "Sequence": 0,        // Sequence number
      "BaseTime": "2020-01-01 00:00:00"  // Base time
    }
  }
}
```

## Usage

### Code-based Configuration

```csharp
Log.Logger = new LoggerConfiguration()
    .Enrich.WithUniqueId()
    // ...other configuration...
    .CreateLogger();
```

### JSON Configuration

```json
{
   "Serilog": {
    "MinimumLevel": {
      "Default": "Information"
    },
    "Enrich": [ "WithUniqueId" ]
  }
}
```

## Implementation Details

This enricher uses the Snowflake algorithm to generate a unique ID for each log event. The Snowflake algorithm features:

* Generates 64-bit long integer IDs
* ID consists of timestamp, datacenter ID, worker machine ID, and sequence number
* Ensures uniqueness in distributed environments
* Time-based ordering

## Best Practices

1. Configure worker ID and datacenter ID appropriately to avoid conflicts in distributed environments:
```json
{
  "UniqueId": {
    "Snowflake": {
      "WorkerId": 1,
      "DatacenterId": 1
    }
  }
}
```

2. Set an appropriate base time to maximize the available time range for IDs:
```json
{
  "UniqueId": {
    "Snowflake": {
      "BaseTime": "2020-01-01 00:00:00"
    }
  }
}
```

3. Use the UniqueId field for precise log event location in queries.

## Notes

1. IDs generated by the Snowflake algorithm are roughly increasing but not strictly monotonic
2. Worker ID and datacenter ID must be unique within the cluster
3. Base time cannot be modified once set, as it may cause ID duplicates
4. Each log event generates a new unique ID, which may incur some performance overhead
