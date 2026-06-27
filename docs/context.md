# Project Context

## What This Project Is
Mercy General Clinical Operations Dashboard is a frontend-only operational readout for a Clinical Operations Lead. The experience is optimized for a morning triage workflow: identify strain quickly, understand trend direction, and locate active risks.

## User and Workflow
- Primary user: Clinical Operations Lead at a mid-size hospital.
- Typical use: Morning review and operations huddles on laptop or large desktop.
- Core question: Are patient flow, occupancy, wait times, and staffing at safe levels today?

## Data Model
- Source: local mock data in src/data/metrics.json.
- Departments: ED, ICU, Med-Surg, Maternity, Pediatrics.
- Time series: 14 daily periods with latest date last.
- Each day includes per-department values for:
  - patient volume
  - bed occupancy percent
  - average wait minutes
  - staffing coverage percent
- Alerts are modeled as dated events with department, type, and severity.

## Key Decisions
- Reusable KPI tile component (MetricCard) drives consistency for all top-row metrics.
- Department filter is global and updates KPI tiles, occupancy chart, department table, and alerts.
- All Departments mode computes hospital-wide aggregate metrics from department rows.
- Theme uses clinical neutrals with deep teal accent and semantic status colors.
- Access gate is intentionally client-side and in-memory only for demo/training use.
