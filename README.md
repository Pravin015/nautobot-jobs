# Nautobot Jobs — Training Lab

Git-backed Nautobot Jobs for the **Nautobot 40-Hour Training Program (Techademy)**.

This repository is designed to be added as a **Git Data Source** in Nautobot so that all Jobs are automatically discovered and available in the Nautobot UI without manually copying files into the container.

## Jobs Included

| Job | File | Description |
|-----|------|-------------|
| **Device Inventory Audit** | `jobs/device_audit.py` | Checks for missing primary IPs, empty serial numbers, and unassigned roles. Supports location filtering and dry-run mode. |
| **Bulk Device Onboarding** | `jobs/bulk_onboard.py` | Import devices from a CSV file (name, role, location, status). Validates against existing data with idempotent get-or-create logic. |
| **Interface Standardization** | `jobs/interface_standardization.py` | Enforces interface description naming conventions (management, loopback, cabled, unused interfaces). |
| **IP Address Allocation** | `jobs/ip_allocation.py` | Assigns primary IPv4 addresses to devices without one, pulling from a specified management prefix. |
| **Inventory Validation Report** | `jobs/inventory_validation.py` | Cross-checks devices against 6 organizational rules (primary IP, serial, role, platform, device type, status) with severity levels. |

## Setup — Add as Git Data Source in Nautobot

### Step 1: Add the Git Repository

1. Navigate to **Extensibility > Git Repositories** in Nautobot
2. Click **Add**
3. Fill in:
   - **Name**: `Training Jobs`
   - **Remote URL**: `https://github.com/<your-username>/nautobot-jobs.git`
   - **Branch**: `main`
   - **Token** (if private repo): your GitHub personal access token
   - **Provides**: check **Jobs**
4. Click **Create**

### Step 2: Sync

1. On the Git Repository detail page, click **Sync**
2. Nautobot will clone the repo and discover all Jobs in the `jobs/` directory

### Step 3: Enable & Run

1. Navigate to **Jobs > Jobs**
2. Find the imported jobs (they appear with their `Meta.name`)
3. Click a job → **Edit** → check **Enabled** → **Save**
4. Click **Run** to execute

### Updating Jobs

When you push changes to this repository:
1. Go to **Extensibility > Git Repositories**
2. Click **Sync** on the Training Jobs repository
3. Nautobot reloads all Job files automatically

You can also set up a **webhook** for automatic sync on push.

## Job Features

All jobs follow Nautobot best practices:

- **Job Variables** — auto-generated UI forms (ObjectVar, BooleanVar, FileVar, ChoiceVar)
- **`test_*` Validation** — pre-run checks that prevent execution with invalid inputs
- **Structured Logging** — `self.logger.info/success/warning/failure` with `obj=` links
- **Dry-Run Mode** — preview changes before committing
- **Error Handling** — per-item try/except so one failure doesn't crash the entire job

## Lab Environment

| Component | Value |
|-----------|-------|
| Nautobot URL | `http://localhost:8088` |
| Credentials | `admin` / `admin` |
| API Token | `0123456789abcdef0123456789abcdef01234567` |

## License

Training materials for authorized use in Techademy programs.
