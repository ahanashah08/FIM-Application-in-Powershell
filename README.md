# PowerShell File Integrity Monitor (FIM)

A **File Integrity Monitoring (FIM)** tool written in PowerShell that detects unauthorized changes in files by comparing cryptographic hashes against a saved baseline.

This script monitors a target folder and alerts when files are **created, modified, or deleted**.

---

## Overview

File Integrity Monitoring is a security control used to detect unexpected changes in files.

This project implements a simple FIM system that:

1. Generates a **baseline of file hashes**
2. Stores the baseline in `baseline.txt`
3. Continuously scans files in a monitored directory
4. Detects and reports changes

This simulates the core functionality used in **Host-Based Intrusion Detection Systems (HIDS)**.

---

## Features

* Detects **file modifications**
* Detects **newly created files**
* Detects **deleted files**
* Uses **SHA512 hashing**
* Continuous monitoring loop
* Lightweight PowerShell implementation

---

## Project Structure

```
project-folder
│
├── fim.ps1
├── baseline.txt
└── Files/
    ├── a.txt
    ├── b.txt
```

`Files/` is the directory being monitored.

---

## How It Works

### 1. Baseline Creation

The script scans all files in the monitored folder and calculates their hashes.

Example stored format in `baseline.txt`:

```
C:\Project\Files\file1.txt|HASHVALUE
C:\Project\Files\file2.txt|HASHVALUE
```

Each line contains:

```
file path | hash value
```

---

### 2. Monitoring Mode

The script:

1. Loads the baseline hashes
2. Stores them in a PowerShell **dictionary**
3. Continuously scans files
4. Compares current hashes with baseline hashes

---

## Architecture

```
Monitored Folder (Files)
        │
        ▼
PowerShell Scanner
        │
        ▼
SHA512 Hash Generator
        │
        ▼
Baseline Database (baseline.txt)
        │
        ▼
Integrity Checker
        │
        ▼
Security Alerts
```

---

## Requirements

* Windows
* PowerShell 5.1 or later

---

## Usage

### Run the script

```powershell
.\fim.ps1
```

You will be prompted with options:

```
A) Collect new Baseline
B) Begin monitoring files with saved Baseline
```

---

### Option A — Create Baseline

```
A
```

This will:

* Delete any existing baseline
* Generate hashes for all files
* Store them in `baseline.txt`

---

### Option B — Monitor Files

```
B
```

The script will begin **continuous monitoring**.

---

## Example Output

### New File Created

```
C:\Project\Files\test.txt has been created!
```

### File Modified

```
C:\Project\Files\data.txt has changed!!!
```

### File Deleted

```
C:\Project\Files\log.txt has been deleted!
```

---

## Security Concepts Demonstrated

* File integrity verification
* Cryptographic hashing
* Baseline comparison
* Host-based intrusion detection
* Security monitoring automation

---

## Future Improvements

* Real-time monitoring with `FileSystemWatcher`
* Logging to a file
* Email or webhook alerts
* GUI dashboard
* SIEM integration

---

MIT License
