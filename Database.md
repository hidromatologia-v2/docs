# Database

This document describes the relation database used in the entire system.

## Tables

```mermaid
erDiagram

countries {
	uuid UUID
	name STRING
}

regions {
	uuid UUID
	country UUID
	name STRING
}

basins {
	uuid UUID
	region UUID
	name STRING
}
```

```mermaid
erDiagram

users {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	username STRING
	name STRING
	phone STRING
	email STRING
	password_hash STRING
}

stations {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	latitude DOUBLE
	longitude DOUBLE
	basin UUID
	user_responsible UUID
}
```

```mermaid
erDiagram

sensors {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	station UUID
	type INT
}

sensor_registries {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	sensor UUID
	value DOUBLE
}
```

```mermaid
erDiagram

alarms {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	name STRING
	user UUID
	sensor UUID
	condition INT
	value DOUBLE
}

stations_api_keys {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	key STRING
	station UUID
}
```

## Relations

### Stations organization

```mermaid
erDiagram

countries ||--o{ regions: "Has many"
regions ||--o{ basins: "Has many"
basins ||--o{ stations: "Has many"

users ||--o{ stations: "Has many"
stations ||--|{ sensors: "Has many"
sensors ||--o{ sensor_registries: "Has many"

stations ||--o{ stations_api_keys: "Has many"
```

### Alarms

```mermaid
erDiagram

users ||--o{ alarms: "Has many"
alarms ||--|| sensors: "Has one"
```

## Table rows and their Types

### Sensors

| Type | Number |
| ---- | ------ |
|      |        |

### Conditions

| Type | Number |
| ---- | ------ |
| `<`  | 0      |
| `>`  | 1      |
| `<=` | 2      |
| `>=` | 3      |

