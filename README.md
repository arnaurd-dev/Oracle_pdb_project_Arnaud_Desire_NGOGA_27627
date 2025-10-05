# PL/SQL Assignment: Database Creation, Deletion & OEM

## 📝 Assignment Description

This assignment demonstrates the lifecycle management of **Pluggable Databases (PDBs)** within an **Oracle 19c Container Database (CDB)** environment. It covers the creation of a persistent PDB for class work, the creation and immediate deletion of a temporary PDB, and the configuration and verification using the **Oracle Enterprise Manager (OEM) Database Express** dashboard.

NAMES: NGOGA Desire Arnaud   
ID: 27627
-----

## ✅ Task 1: Create a New Pluggable Database (PDB)

The goal was to create a new, persistent PDB for ongoing classwork, adhering to a specific naming convention.

### ➡️ Steps Performed

1.  **PDB Creation:** Created a Pluggable Database named **`Ar_pdb_27627`** (following the format `FirstTwoLettersOfFirstName_pdb_StudentID`).
2.  **Admin User:** Created the PDB administrative user **`Arnaud_plsqIauca_27627`** with a simple password (`123`).
3.  **Datafile Conversion:** Used the `FILE_NAME_CONVERT` clause to correctly place the new PDB's datafiles.

### 💻 Command Output

The following command was successfully executed:

```sql
CREATE PLUGGABLE DATABASE Ar_pdb_27627
ADMIN USER Arnaud_plsqlauca_27627 IDENTIFIED BY 123
FILE_NAME_CONVERT=('C:\ORACLE19C\ORADATA\ORCL\PDBSEED\',
'C:\ORACLE19C\ORADATA\ORCL\Ar_Pdb_27627\');
```

<img width="610" height="168" alt="Creation of pluggable database" src="https://github.com/user-attachments/assets/148742ad-5cc8-41aa-bfc9-a5545a7dedc1" />

-----

## ✅ Task 2: Create and Delete a PDB

This task involved demonstrating the complete lifecycle of a PDB by creating and immediately dropping a temporary database.

### ➡️ Steps Performed

1.  **PDB Creation:** Created a temporary PDB named **`Ar_to_delete_pdb_27627`** (following the format `FirstTwoLettersOfName_to_delete_pdb_StudentID`).
2.  **PDB Deletion:** Immediately dropped the PDB using the `INCLUDING DATAFILES` clause to ensure all associated files were removed from the disk.
3.  **Verification:** Queried `v$pdbs` to confirm the PDB was no longer listed.

### 💻 Command Output

**Creation of PDB:**

```sql
CREATE PLUGGABLE DATABASE Ar_to_delete_pdb_27627
ADMIN USER Arn_27627 IDENTIFIED BY 123
FILE_NAME_CONVERT=('C:\ORACLE19C\ORADATA\ORCL\PDBSEED\',
'C:\ORACLE19C\ORADATA\ORCL\Arn_TO_DELETE_PDB_27627\');
```

**Deletion of PDB and Verification:**

```sql
DROP PLUGGABLE DATABASE Ar_to_delete_pdb_27627 INCLUDING DATAFILES;
SELECT name, open_mode FROM v$pdbs;
```

The verification query confirms that **`AR_TO_DELETE_PDB_27627`** is successfully removed.

<img width="645" height="145" alt="creation of pluggable database to_be_delete" src="https://github.com/user-attachments/assets/dc5e20cc-2a41-4d08-bc69-829f51409ae8" />

<img width="693" height="352" alt="Deletion OR Dropping" src="https://github.com/user-attachments/assets/bc9b03c3-d330-46d4-836a-9e02553238c6" />

-----

## ✅ Task 3: Oracle Enterprise Manager Configuration

This task focused on configuring and accessing the Oracle Enterprise Manager (OEM) Database Express dashboard.

### ➡️ Steps Performed

1.  **Select PDB:** Switched the session container to the persistent PDB, **`Ar_pdb_27627`**.
2.  **Configure HTTP Port:** Set the HTTPS port for the PDB using `DBMS_XDB_CONFIG.SETHTTPSPORT(5501)`.
3.  **Access Dashboard:** Accessed the dashboard via a web browser (`https://localhost:5501/em/shell`).

### 💻 Command Output

```sql
SQL> ALTER SESSION SET CONTAINER = Ar_pdb_27627;
Session altered.

SQL> EXEC DBMS_XDB_CONFIG.SETHTTPSPORT(5501);
PL/SQL procedure successfully completed.
```
<img width="452" height="224" alt="OEM" src="https://github.com/user-attachments/assets/9e3ea851-1524-4e97-a68c-d26622ab4ff3" />

### 🖼️ OEM Dashboard Screenshot

The screenshot below validates the configuration and shows the PDB's status and resources after completing Tasks 1 and 2. The PDB **`AR_PDB_27627`** and the system user are clearly visible.

<img width="1360" height="729" alt="Dashboard" src="https://github.com/user-attachments/assets/9a071ea8-dea5-4e92-af50-23d14de64f5f" />

-----

## 🛠️ Notes on Issues/Fixes

| Issue/Note | Description/Fix |
| :--- | :--- |
| **PDB Status** | After creation, the PDB was confirmed to be in **READ WRITE** mode (as shown in the **Deletion OR Dropping.PNG** screenshot), indicating it is ready for use. |
| **OEM Port** | The chosen port **`5501`** was used for the OEM access. If there were any firewall or port-in-use issues, a different port would have needed to be selected and configured. |
| **Datafile Location** | The `FILE_NAME_CONVERT` clause was critical for ensuring the datafiles were stored in the correct, organized directory structure (`C:\ORACLE19C\ORADATA\ORCL\Ar_Pdb_27627\`). |

-----

## 🏁 Conclusion

This assignment successfully demonstrated key **Container Database (CDB)** concepts, including the practical steps for:

1.  Creating a persistent **Pluggable Database** for development/class purposes.
2.  Managing a PDB's lifecycle by **creating and immediately dropping** a temporary PDB.
3.  Configuring and accessing the **Oracle Enterprise Manager Database Express** interface to monitor the PDB.

All objectives were met and verified with the required SQL commands and the final OEM dashboard screenshot.
