# Database

This document describes the relation database used in the entire system.

## Stations

### Tables

```mermaid
erDiagram

users {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	username STRING
	password_hash STRING
	name STRING
	phone STRING
	email STRING
	confirmed BOOL
}

stations {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	user_uuid UUID
	name STRING
	description STRING
	country INT
	subdivision STRING
	latitude DOUBLE
	longitude DOUBLE
	api_key STRING
}
```

```mermaid
erDiagram

sensors {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	station_uuid UUID
	type STRING
}

sensor_registries {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	sensor_uuid UUID
	value DOUBLE
}
```

```mermaid
erDiagram

alert {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	user_uuid UUID
	name STRING
	sensor_uuid UUID
	condition INT
	value DOUBLE
}
```

### Relations

```mermaid
erDiagram

users ||--o{ stations: "Has many"
stations ||--|{ sensors: "Has many"
sensors ||--o{ sensor_registries: "Has many"

users ||--o{ alarms: "Has many"
alarms ||--|| sensors: "Has one"
```

### Table rows and their Types

#### Sensors

| Type | Number |
| ---- | ------ |
|      |        |

#### Conditions

| Type | Number |
| ---- | ------ |
| `<`  | 0      |
| `>`  | 1      |
| `<=` | 2      |
| `>=` | 3      |

## Messaging

### Tables

```mermaid
erDiagram

messages {
	uuid UUID
	created TIMESTAMP
	updated TIMESTAMP
	deleted TIMESTAMP
	type	STRING
	recipient STRING
	subject STRING
	body STRING
}
```

