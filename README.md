# Oracle PDB Assignment II — 27713

## Student Information

* **Student Name:** Manzi Michael
* **Student ID:** 27713
* **Database:** Oracle AI Database 26ai Free
* **Operating System:** Windows 10
* **PDB Name:** `mi_pdb_27713`
* **PDB Administrator:** `Michael_plsqlauca_27713`

## Assignment Overview

This assignment focuses on practical Oracle Pluggable Database (PDB) administration. The main activities include creating and verifying a PDB, creating and verifying a PDB administrator, creating and deleting a temporary PDB, and documenting the database environment and management interface.

All database commands were executed in my Oracle database environment using SQL*Plus.

---

## Task 1 — Create and Configure the PDB

### PDB Creation

The required PDB name was created according to the assignment naming convention:

```text
mi_pdb_27713
```

The PDB was created using:

```sql
CREATE PLUGGABLE DATABASE mi_pdb_27713
ADMIN USER Michael_plsqlauca_27713
IDENTIFIED BY [password]
FILE_NAME_CONVERT = (
  'C:\APP\USER\PRODUCT\26AI\ORADATA\FREE\PDBSEED\',
  'C:\APP\USER\PRODUCT\26AI\ORADATA\FREE\MI_PDB_27713\'
);
```

The command completed successfully with:

```text
Pluggable database created.
```

The PDB was then opened using:

```sql
ALTER PLUGGABLE DATABASE mi_pdb_27713 OPEN;
```

The PDB was verified using:

```sql
SHOW PDBS;
```

The result showed:

```text
MI_PDB_27713    READ WRITE    NO
```

### User Verification

The session was changed to the new PDB:

```sql
ALTER SESSION SET CONTAINER = mi_pdb_27713;
```

The container was verified using:

```sql
SHOW CON_NAME;
```

Result:

```text
MI_PDB_27713
```

The PDB administrator was verified using:

```sql
SELECT USERNAME, ACCOUNT_STATUS
FROM DBA_USERS
WHERE USERNAME = 'MICHAEL_PLSQLAUCA_27713';
```

Result:

```text
USERNAME
--------------------------------------------------------------------------------
MICHAEL_PLSQLAUCA_27713

ACCOUNT_STATUS
--------------------------------
OPEN
```

### Evidence

The following screenshots are included in the repository:

* PDB creation
* PDB open state
* PDB container verification
* User and account-status verification

---

## Task 2 — Create and Delete a Temporary PDB

A temporary PDB was created using the required name:

```text
mi_to_delete_pdb_27713
```

The PDB was verified using:

```sql
SHOW PDBS;
```

After verification, the temporary PDB was completely removed using:

```sql
DROP PLUGGABLE DATABASE mi_to_delete_pdb_27713 INCLUDING DATAFILES;
```

Oracle returned:

```text
Pluggable database dropped.
```

A final verification was performed using:

```sql
SHOW PDBS;
```

The final output contained:

```text
PDB$SEED
FREEPDB1
MI_PDB_27713
```

The temporary PDB `MI_TO_DELETE_PDB_27713` was no longer listed.

### Evidence

Screenshots are included showing:

1. Creation and verification of the temporary PDB.
2. Successful deletion of the temporary PDB.
3. Final `SHOW PDBS` output confirming that the temporary PDB no longer exists.

---

## Task 3 — Oracle Enterprise Manager

The assignment requires Oracle Enterprise Manager (OEM) access and an OEM dashboard showing the Oracle environment and completed PDB work.

The current database environment uses Oracle AI Database 26ai Free. The database and listener are operational, and the custom PDB `MI_PDB_27713` is registered with the listener.

An OEM dashboard screenshot has **not yet been included**, because the installed Oracle 26ai environment does not provide the older EM Express interface expected by many Oracle PDB practical assignments.

This section will be updated with the required OEM evidence once the appropriate OEM environment is confirmed.

---

## Challenges and Solutions

### Challenge 1 — ORA-65016

During the initial PDB creation attempt, Oracle returned:

```text
ORA-65016: FILE_NAME_CONVERT must be specified
```

The solution was to specify the appropriate source and destination datafile locations using `FILE_NAME_CONVERT`.

### Challenge 2 — ORA-65005

A second attempt using the PDB name as the conversion pattern resulted in:

```text
ORA-65005: missing or invalid file name pattern
```

The actual Oracle datafile location was then identified from the database configuration. The PDB was successfully created using the PDB seed directory:

```text
C:\APP\USER\PRODUCT\26AI\ORADATA\FREE\PDBSEED\
```

and the destination:

```text
C:\APP\USER\PRODUCT\26AI\ORADATA\FREE\MI_PDB_27713\
```

The corrected command successfully created the PDB.

### Challenge 3 — OEM Environment

The installed Oracle AI Database 26ai Free environment does not provide the older EM Express interface. The database installation was therefore kept unchanged to avoid affecting the successfully completed PDB work.

---

## Repository Structure

```text
oracle_pdb_ass_II_27713_michael/
│
├── README.md
│
└── screenshots/
    ├── pdb_creation/
    ├── pdb_deletion/
    └── oem_dashboard/
```

The `oem_dashboard` folder will contain the genuine OEM evidence once the required management environment has been established.

---

## Database Objects Completed

| Object                    | Status                        |
| ------------------------- | ----------------------------- |
| `mi_pdb_27713`            | Created and opened            |
| `Michael_plsqlauca_27713` | Created and OPEN              |
| `mi_to_delete_pdb_27713`  | Created, verified and deleted |
| OEM dashboard             | Pending                       |

---

## Academic Integrity Statement

I confirm that the work documented in this repository represents my own practical work completed for this assignment. The screenshots and database results are based on commands executed in my Oracle database environment.

## Submission Details

* **Student Name:** Manzi Michael
* **Student ID:** 27713
* **Repository Link:** https://github.com/ManziMichael/oracle_pdb_ass_II_27713_michael
* **PDB Name Created:** MI_PDB_27713
* **Issues Encountered:** Yes — Oracle 26ai required an explicit `FILE_NAME_CONVERT` path when creating the PDB. The issue was resolved by using the correct PDB seed and destination paths.

### Integrity Statement

I confirm that the Oracle PDB work, screenshots, and documentation in this repository represent my own execution and work for this assignment.

