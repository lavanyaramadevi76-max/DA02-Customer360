# DA-02 dbt starter project

This is a starter dbt project scaffold for the DA-02 Customer 360 BigQuery work.

## Important status note

The SQL transformations and tables were created directly in BigQuery during the project.
This folder packages a dbt structure that references selected existing tables. **It has not
been executed or tested with dbt yet**, and should not be described as a completed dbt run.

The current Customer 360 and attribution tables are prototype outputs. Identity mapping is
deterministic pseudonymous mapping, and attribution uses first-user acquisition fields as a
proxy rather than full session-level journey touchpoints.

## Setup

1. Install dbt Core and the BigQuery adapter:
   `python -m pip install dbt-bigquery`
2. Replace `YOUR_GCP_PROJECT_ID` in `models/sources.yml`.
3. Copy `profiles.yml.example` to `~/.dbt/profiles.yml`.
4. Replace the project ID and BigQuery location in the profile.
5. Authenticate with Google Cloud using the OAuth method.
6. From this folder run:
   `dbt debug`
   `dbt parse`
   `dbt run`
   `dbt test`

Do not upload credentials, service-account JSON files, or access tokens to GitHub.
