# API Ethics Assignment

## Task 1 — Classify and Handle PII Fields

| Field | PII Type | Action | Justification |
|------|------|------|------|
| full_name | Direct PII | Drop | A person's full name directly identifies an individual. It is not required for research analysis. |
| email | Direct PII | Drop | Email addresses uniquely identify individuals and allow direct contact. |
| date_of_birth | Indirect PII | Mask | Exact birth dates can lead to re-identification. Converting to age groups protects privacy. |
| zip_code | Indirect PII | Mask | ZIP codes combined with other fields may reveal identity, so only partial ZIP codes should be shared. |
| job_title | Indirect PII | Generalize | Job titles may identify someone in small datasets. Converting them to broader categories reduces risk. |
| diagnosis_notes | Sensitive data | Pseudonymize | Health information is needed for research but must remove any identifying information and use a patient ID instead. |

## Task 2 — Audit the API Script for Ethical Compliance

### Violation 1: Hard-coded API Key

Problem:
The API key is written directly in the script. This is a security risk because anyone with access to the code can misuse the key.

Corrected Code:

```python
import os
import requests

API_URL = "https://healthstats-api.example.com/records"
API_KEY = os.getenv("HEALTH_API_KEY")

import time
import requests
import os

API_URL = "https://healthstats-api.example.com/records"
API_KEY = os.getenv("HEALTH_API_KEY")

records = []

for page in range(1, 101):
    response = requests.get(API_URL, params={"page": page, "key": API_KEY})
    data = response.json()
    records.extend(data["results"])

    time.sleep(1)  # Respect API rate limits
