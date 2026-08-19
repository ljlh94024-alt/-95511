# Gemini Web2API-Go Runtime Report

Date: 2026-08-19  
Service: `gemini-web2api-go` v4.4.0  
Endpoint: `http://127.0.0.1:8083`

## Result

`PASS`

The local service was running and its admin authentication accepted the
runtime token configured for this session. Protected admin requests rejected
missing and incorrect credentials, while the login flow and session cookie
flow completed successfully.

## Checks

| Check | Result |
|---|---:|
| Process running | PASS |
| Port 8083 listening | PASS |
| Service health HTTP status | 200 |
| Protected endpoint without token | 401 |
| Protected endpoint with incorrect token | 401 |
| Protected endpoint with runtime token | 200 |
| Login endpoint with runtime token | 200 |
| Authenticated session request | 200 |
| Logout endpoint | 200 |
| Source/config modified by this validation | NO |

## Evidence handling

The original local configuration, database, cookies, session data, and raw
logs are excluded. The companion runtime log files in this directory are
redacted copies with credential material removed.
