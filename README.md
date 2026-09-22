# Oracle PDB Assignment II

## Student Information

- **Student Name:** Mutamba Alice
- **Student ID:** 27688
- **Repository Name:** `oracle_pdb_ass_II_27688_Alice`

## Overview

This project documents the Oracle Database 19c Pluggable Database (PDB) practical assignment. The work includes creating a permanent PDB, creating and deleting a temporary PDB, verifying the PDB environment, and accessing Oracle Enterprise Manager Database Express.

## Environment

- **Database:** Oracle Database 19c Enterprise Edition
- **Database Name:** ORCL
- **Operating System:** Microsoft Windows x86 64-bit
- **PDB Seed:** PDB$SEED
- **Permanent PDB:** AL_PDB_27688
- **PDB User:** ALICE_PLSQLAUCA_27688
- **OEM Express HTTPS Port:** 5500

## Task 1: Create a New Pluggable Database

The required naming convention was:

`FirstTwoLettersOfFirstName_pdb_StudentID`

For this student:

`Al_pdb_27688`

Oracle displays the PDB name as:

`AL_PDB_27688`

The required user naming convention was:

`FirstName_plsqlauca_StudentID`

The created user is:

`ALICE_PLSQLAUCA_27688`

The PDB was verified as `READ WRITE`, and the user was given an unlimited quota on the `USERS` tablespace.

### Verification

The permanent PDB was verified with:

```sql
SHOW PDBS;

SELECT name, open_mode
FROM v$pdbs
WHERE name = 'AL_PDB_27688';
```

The user quota was verified with:

```sql
SELECT username, tablespace_name, max_bytes
FROM dba_ts_quotas
WHERE username = 'ALICE_PLSQLAUCA_27688';
```

## Task 2: Create and Delete a Temporary PDB

The temporary PDB used the required naming convention:

`Al_to_delete_pdb_27688`

Oracle displayed it as:

`AL_TO_DELETE_PDB_27688`

The temporary PDB was created, opened, closed, and removed completely using:

```sql
DROP PLUGGABLE DATABASE AL_TO_DELETE_PDB_27688 INCLUDING DATAFILES;
```

Final verification confirmed that it no longer existed:

```sql
SELECT name, open_mode
FROM v$pdbs
WHERE name = 'AL_TO_DELETE_PDB_27688';
```

The result was:

```text
no rows selected
```

## Task 3: Oracle Enterprise Manager

Oracle Enterprise Manager Database Express was accessed through the configured HTTPS port:

`https://localhost:5500/em`

The OEM dashboard confirmed the Oracle 19c environment and database `ORCL`. The dashboard was accessed using the Oracle administrative account.

## Screenshots

The screenshots are organized into the following folders:

```text
screenshots/
├── pdb_creation/
├── pdb_deletion/
└── oem_dashboard/
```

Place the actual screenshots from the completed practical work into the appropriate folders.

## Challenges and Solutions

### 1. Correct PDB datafile location

The PDB seed datafiles were located under:

`C:\ORACLE19C\ORADATA\ORCL\PDBSEED\`

This path was used with `FILE_NAME_CONVERT` when creating the PDBs.

### 2. USERS tablespace quota

The permanent PDB already had a `USERS` tablespace. The user was therefore assigned an unlimited quota instead of attempting to recreate the tablespace.

### 3. Temporary PDB already existed

During Task 2, Oracle reported that `AL_TO_DELETE_PDB_27688` already existed. Its state was checked with `SHOW PDBS` and `v$pdbs`, then it was closed and removed. A final query confirmed that no such PDB remained.

### 4. SQL*Plus command formatting

Some initial SQL*Plus errors were caused by missing spaces or by entering database object names directly at the SQL prompt. The commands were corrected and the database state was re-verified.

## Final Database State

The final PDB list contained:

- `PDB$SEED` — READ ONLY
- `ORCLPDB` — READ WRITE
- `AL_PDB_27688` — READ WRITE

The temporary PDB `AL_TO_DELETE_PDB_27688` was successfully deleted.

## Integrity Statement

I, **Mutamba Alice (Student ID 27688)**, confirm that the work documented in this repository represents the practical Oracle PDB assignment work completed in my Oracle 19c environment. The screenshots included in the repository should be the original evidence captured from my own environment.


