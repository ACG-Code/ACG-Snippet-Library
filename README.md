# ACG TurboIntegrator Snippet Library

A collection of custom snippets for TurboIntegrator development in Planning Analytics Workspace.

## Overview

These snippets provide a standardized framework for TI process development. They are designed to work together and integrate with ACG's process logging utility (PLOG).

## Snippets Included

| Snippet | Tab | Description |
|---------|-----|-------------|
| Header | Prolog | Standardized process documentation block |
| Prolog_Framework | Prolog | Logging initialization, error handling, constants, and variable setup |
| Metadata_Framework | Metadata | Record processing header and counter |
| Data_Framework | Data | Record processing header and counter |
| Epilog_Framework | Epilog | Process completion and status logging |
| Create_Cube_View | Prolog | Dynamic view and subset creation loop |

## Installation

1. Download the JSON files from this repository
2. Open Planning Analytics Workspace
3. Open any process in the process editor
4. Click **Script** tab → **Snippet icon** → **Custom**
5. Click **Upload snippets** and select the JSON files

Once uploaded, snippets are available to all users across all databases.

## Usage

### Typical Process Structure

```
┌─────────────────────────────────────┐
│ PROLOG                              │
│  ├── Header                         │
│  ├── Prolog_Framework               │
│  └── Create_Cube_View (if needed)   │
├─────────────────────────────────────┤
│ METADATA                            │
│  └── Metadata_Framework             │
├─────────────────────────────────────┤
│ DATA                                │
│  └── Data_Framework                 │
├─────────────────────────────────────┤
│ EPILOG                              │
│  └── Epilog_Framework               │
└─────────────────────────────────────┘
```

### Snippet Details

#### Header
Inserts a documentation block at the top of the process.

**Variables:**
- `vProcess` - Process name
- `vPurpose` - Purpose description
- `vCreated` - Creation date
- `vUpdated` - Last update date

#### Prolog_Framework
Sets up logging, error handling, and standard variables.

**Variables:**
- `vProcess` - Process name
- `vPurpose` - Purpose description
- `vCreated` - Creation date
- `vUpdated` - Last update date

**Initializes:**
- `cLogProc` - Logging process name (PLOG)
- `cProc` - Current process name
- `cUser` - Current user
- `cTimestamp` - Execution timestamp
- `sView` - Unique view name for temporary objects
- `nError` - Error flag
- `nMetaHdr`, `nMeta` - Metadata counters
- `nDataHdr`, `nData` - Data counters

#### Metadata_Framework
Insert in the Metadata tab. Logs when metadata processing begins and increments the record counter.

**Requires:** Variables initialized by Prolog_Framework

#### Data_Framework
Insert in the Data tab. Logs when data processing begins and increments the record counter.

**Requires:** Variables initialized by Prolog_Framework

#### Epilog_Framework
Logs process completion with SUCCESS or ERROR status.

**Requires:** Variables initialized by Prolog_Framework

#### Create_Cube_View
Creates a view and subsets for all dimensions of a cube.

**Variables:**
- `vCube` - Cube name
- `vView` - View name
- `vTemp` - Create as temporary (1=Yes, 0=No)
- `vZero` - Skip zeroes (1=Yes, 0=No)
- `vConsol` - Skip consolidated values (1=Yes, 0=No)
- `vRules` - Skip rule-derived values (1=Yes, 0=No)
- `vType` - Description/label for the view

## Dependencies

These snippets call a logging process named `PLOG`. Ensure this process exists in your environment with the following parameters:

| Parameter | Type | Description |
|-----------|------|-------------|
| pFlag | String | INIT, MSG, or END |
| pProc | String | Process name |
| pMSG | String | Message text |

## Documentation

For more information on creating custom snippets, see IBM's documentation:  
https://www.ibm.com/docs/en/planning-analytics/2.0.0?topic=process-create-upload-custom-snippet

## License

Proprietary - ACG
