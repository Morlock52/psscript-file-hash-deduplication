# PSScript File Hash Deduplication

This repository contains testing and documentation for the file hash deduplication feature in the PSScript platform.

## Overview

The file hash deduplication feature prevents duplicate scripts from being uploaded to the database. When a script is uploaded, the system calculates a hash of the file content and checks if a script with the same hash already exists in the database. If a match is found, the upload is rejected with a 409 Conflict response.

## Repository Contents

- **Documentation**:
  - [File Hash Implementation Report](FILE-HASH-IMPLEMENTATION-REPORT.md): Comprehensive report on implementation and testing
  - [File Hash Testing Documentation](README-FILE-HASH-TESTING.md): Detailed test results showing the feature works correctly

- **Test Scripts**:
  - [test-script-unique.ps1](test-script-unique.ps1): Original PowerShell script for testing
  - [test-script-unique-modified.ps1](test-script-unique-modified.ps1): Modified version of the script
  - [test-upload-unique-script.sh](test-upload-unique-script.sh): Shell script to upload the original script
  - [test-upload-modified-script.sh](test-upload-modified-script.sh): Shell script to upload the modified script

## Implementation Details

The file hash deduplication feature is implemented across several components:

1. **Database Schema**:
   - The `scripts` table includes a `file_hash` column to store the MD5 hash of each script.
   - An index was created on this column to speed up duplicate detection.

2. **Script Model**:
   - The Script model includes a `fileHash` field.

3. **File Integrity Utilities**:
   - Provides functions for calculating and verifying file hashes.

4. **Script Controller**:
   - Handles the logic for checking duplicate hashes and rejecting duplicate uploads.

## Testing Results

Our testing confirmed that the file hash deduplication feature is working correctly:

1. Successfully uploaded a unique script with a unique hash.
2. Rejected duplicate uploads with appropriate error messages.
3. Successfully uploaded a modified script with a different hash.
4. Rejected duplicate uploads of the modified script.

For more detailed information, please refer to the documentation files in this repository.