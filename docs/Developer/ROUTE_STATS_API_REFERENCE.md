# Route Statistics API — Request & Response Reference

All endpoints are `POST`, base URL `http://localhost:4000`.  
All bodies are JSON (`Content-Type: application/json`).  
No auth required (portal-only endpoints).

---

## Common Response Envelope

Every route-stats endpoint returns the same envelope — only `metric`, `scope`/`scopeValue`, and `value` differ.

```json
{
  "success": true,
  "scope": "session" | "dateRange",
  "scopeValue": <see per-endpoint>,
  "metric": "<metricName>",
  "value": <number | object>
}
```

**Error (all endpoints):**
```json
{ "error": "Failed to compute statistics", "message": "..." }
```

---

## Session-Scoped Endpoints

**Parameter for all:** `sessionId` (number, required) in the JSON body.  
Valid pre-seeded session IDs: `18429`, `57243`, `90618`, `34790`, `62851`

### 1. Total Routes Completed

```
POST /api/route-stats/total-routes-completed-by-session
Body: { "sessionId": 18429 }
```

```json
{
  "success": true,
  "scope": "session",
  "scopeValue": 18429,
  "metric": "totalRoutesCompleted",
  "value": 42
}
```

`value`: `number` — count of completed route cycles for that session.

---

### 2. Total Connected Users

```
POST /api/route-stats/total-connected-users-by-session
Body: { "sessionId": 18429 }
```

```json
{
  "success": true,
  "scope": "session",
  "scopeValue": 18429,
  "metric": "totalConnectedUsers",
  "value": 15
}
```

`value`: `number` — count of `PlayerSession` rows for that session.

---

### 3. Users Started More Than One Route

```
POST /api/route-stats/users-started-more-than-one-route-by-session
Body: { "sessionId": 18429 }
```

```json
{
  "success": true,
  "scope": "session",
  "scopeValue": 18429,
  "metric": "usersStartedMoreThanOneRoute",
  "value": 7
}
```

`value`: `number` — count of players who started 2+ routes.

---

### 4. Users Completed More Than One Route

```
POST /api/route-stats/users-completed-more-than-one-route-by-session
Body: { "sessionId": 18429 }
```

```json
{
  "success": true,
  "scope": "session",
  "scopeValue": 18429,
  "metric": "usersCompletedMoreThanOneRoute",
  "value": 5
}
```

`value`: `number` — count of players who completed 2+ routes.

---

### 5. Users Never Started a Route

```
POST /api/route-stats/users-never-started-route-by-session
Body: { "sessionId": 18429 }
```

```json
{
  "success": true,
  "scope": "session",
  "scopeValue": 18429,
  "metric": "usersNeverStartedRoute",
  "value": 3
}
```

`value`: `number` — count of players who never started any route.

---

### 6. Users Started But Not Finished

```
POST /api/route-stats/users-started-but-not-finished-by-session
Body: { "sessionId": 18429 }
```

```json
{
  "success": true,
  "scope": "session",
  "scopeValue": 18429,
  "metric": "usersStartedButNotFinished",
  "value": 2
}
```

`value`: `number` — count of players who started at least one route but never completed any.

---

### 7. Total Replays

```
POST /api/route-stats/total-replays-by-session
Body: { "sessionId": 18429 }
```

```json
{
  "success": true,
  "scope": "session",
  "scopeValue": 18429,
  "metric": "totalReplays",
  "value": 10
}
```

`value`: `number` — count of route cycles where `cycleNumber > 1`.

---

### 8. Avg Routes Per User

```
POST /api/route-stats/avg-routes-per-user-by-session
Body: { "sessionId": 18429 }
```

```json
{
  "success": true,
  "scope": "session",
  "scopeValue": 18429,
  "metric": "avgRoutesPerUser",
  "value": 2.75
}
```

`value`: `number` — float rounded to 2 decimal places. `0` if no users.

---

### 9. Avg Routes Per Session

```
POST /api/route-stats/avg-routes-per-session-by-session
Body: { "sessionId": 18429 }
```

```json
{
  "success": true,
  "scope": "session",
  "scopeValue": 18429,
  "metric": "avgRoutesPerSession",
  "value": 8.5
}
```

`value`: `number` — float rounded to 2 decimal places.

---

### 10. Replay Ratio

```
POST /api/route-stats/replay-ratio-by-session
Body: { "sessionId": 18429 }
```

```json
{
  "success": true,
  "scope": "session",
  "scopeValue": 18429,
  "metric": "replayRatio",
  "value": {
    "byPlayer": 0.4667,
    "byRoute": 0.1923
  }
}
```

`value`: **object** — the only non-scalar value across all route-stats endpoints.
- `byPlayer`: fraction of players who replayed at least once (4 decimal places)
- `byRoute`: fraction of all route cycles that were replays (4 decimal places)

---

## Date-Range-Scoped Endpoints

**Parameters for all:**

| Field | Type | Required | Notes |
|---|---|---|---|
| `startDate` | `string` | **yes** | ISO 8601 — `YYYY-MM-DD` |
| `endDate` | `string` | no | ISO 8601 — `YYYY-MM-DD`. If omitted, query runs from `startDate` to present. End is normalized to `23:59:59.999 UTC`. |

**`scopeValue` in response:**
```json
// with endDate
"scopeValue": { "startDate": "2025-01-01", "endDate": "2025-12-31" }

// without endDate (open-ended)
"scopeValue": { "startDate": "2025-01-01", "endDate": null }
```

The `metric` names and `value` types are identical to their session counterparts above.

---

### 1. Total Routes Completed

```
POST /api/route-stats/total-routes-completed-by-date-range
Body: { "startDate": "2025-01-01", "endDate": "2025-12-31" }
```

```json
{
  "success": true,
  "scope": "dateRange",
  "scopeValue": { "startDate": "2025-01-01", "endDate": "2025-12-31" },
  "metric": "totalRoutesCompleted",
  "value": 198
}
```

`value`: `number`

---

### 2. Total Connected Users

```
POST /api/route-stats/total-connected-users-by-date-range
Body: { "startDate": "2025-06-01" }
```

```json
{
  "success": true,
  "scope": "dateRange",
  "scopeValue": { "startDate": "2025-06-01", "endDate": null },
  "metric": "totalConnectedUsers",
  "value": 83
}
```

`value`: `number`

---

### 3. Users Started More Than One Route

```
POST /api/route-stats/users-started-more-than-one-route-by-date-range
Body: { "startDate": "2025-01-01", "endDate": "2025-12-31" }
```

```json
{
  "success": true,
  "scope": "dateRange",
  "scopeValue": { "startDate": "2025-01-01", "endDate": "2025-12-31" },
  "metric": "usersStartedMoreThanOneRoute",
  "value": 34
}
```

`value`: `number`

---

### 4. Users Completed More Than One Route

```
POST /api/route-stats/users-completed-more-than-one-route-by-date-range
Body: { "startDate": "2025-01-01", "endDate": "2025-12-31" }
```

```json
{
  "success": true,
  "scope": "dateRange",
  "scopeValue": { "startDate": "2025-01-01", "endDate": "2025-12-31" },
  "metric": "usersCompletedMoreThanOneRoute",
  "value": 28
}
```

`value`: `number`

---

### 5. Users Never Started a Route

```
POST /api/route-stats/users-never-started-route-by-date-range
Body: { "startDate": "2025-01-01", "endDate": "2025-12-31" }
```

```json
{
  "success": true,
  "scope": "dateRange",
  "scopeValue": { "startDate": "2025-01-01", "endDate": "2025-12-31" },
  "metric": "usersNeverStartedRoute",
  "value": 11
}
```

`value`: `number`

---

### 6. Users Started But Not Finished

```
POST /api/route-stats/users-started-but-not-finished-by-date-range
Body: { "startDate": "2025-01-01", "endDate": "2025-12-31" }
```

```json
{
  "success": true,
  "scope": "dateRange",
  "scopeValue": { "startDate": "2025-01-01", "endDate": "2025-12-31" },
  "metric": "usersStartedButNotFinished",
  "value": 9
}
```

`value`: `number`

---

### 7. Total Replays

```
POST /api/route-stats/total-replays-by-date-range
Body: { "startDate": "2025-01-01", "endDate": "2025-12-31" }
```

```json
{
  "success": true,
  "scope": "dateRange",
  "scopeValue": { "startDate": "2025-01-01", "endDate": "2025-12-31" },
  "metric": "totalReplays",
  "value": 47
}
```

`value`: `number`

---

### 8. Avg Routes Per User

```
POST /api/route-stats/avg-routes-per-user-by-date-range
Body: { "startDate": "2025-01-01", "endDate": "2025-12-31" }
```

```json
{
  "success": true,
  "scope": "dateRange",
  "scopeValue": { "startDate": "2025-01-01", "endDate": "2025-12-31" },
  "metric": "avgRoutesPerUser",
  "value": 3.12
}
```

`value`: `number` (float, 2 decimal places)

---

### 9. Avg Routes Per Session

```
POST /api/route-stats/avg-routes-per-session-by-date-range
Body: { "startDate": "2025-01-01", "endDate": "2025-12-31" }
```

```json
{
  "success": true,
  "scope": "dateRange",
  "scopeValue": { "startDate": "2025-01-01", "endDate": "2025-12-31" },
  "metric": "avgRoutesPerSession",
  "value": 49.5
}
```

`value`: `number` (float, 2 decimal places)

---

### 10. Replay Ratio

```
POST /api/route-stats/replay-ratio-by-date-range
Body: { "startDate": "2025-01-01", "endDate": "2025-12-31" }
```

```json
{
  "success": true,
  "scope": "dateRange",
  "scopeValue": { "startDate": "2025-01-01", "endDate": "2025-12-31" },
  "metric": "replayRatio",
  "value": {
    "byPlayer": 0.3125,
    "byRoute": 0.0952
  }
}
```

`value`: **object** `{ byPlayer: number, byRoute: number }` — same structure as session version.

---

## Quick Reference Table

| Metric | Session endpoint suffix | Date-range endpoint suffix | `value` type |
|---|---|---|---|
| `totalRoutesCompleted` | `total-routes-completed-by-session` | `total-routes-completed-by-date-range` | `number` |
| `totalConnectedUsers` | `total-connected-users-by-session` | `total-connected-users-by-date-range` | `number` |
| `usersStartedMoreThanOneRoute` | `users-started-more-than-one-route-by-session` | `users-started-more-than-one-route-by-date-range` | `number` |
| `usersCompletedMoreThanOneRoute` | `users-completed-more-than-one-route-by-session` | `users-completed-more-than-one-route-by-date-range` | `number` |
| `usersNeverStartedRoute` | `users-never-started-route-by-session` | `users-never-started-route-by-date-range` | `number` |
| `usersStartedButNotFinished` | `users-started-but-not-finished-by-session` | `users-started-but-not-finished-by-date-range` | `number` |
| `totalReplays` | `total-replays-by-session` | `total-replays-by-date-range` | `number` |
| `avgRoutesPerUser` | `avg-routes-per-user-by-session` | `avg-routes-per-user-by-date-range` | `number` (2dp) |
| `avgRoutesPerSession` | `avg-routes-per-session-by-session` | `avg-routes-per-session-by-date-range` | `number` (2dp) |
| `replayRatio` | `replay-ratio-by-session` | `replay-ratio-by-date-range` | `{ byPlayer, byRoute }` (4dp) |

All endpoint paths are prefixed with `/api/route-stats/`.
