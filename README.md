# Hunter HQ

A modular household dashboard designed for an always-on Chromium display on Raspberry Pi 5, and responsive on phones and desktop.

## Modules
- **Andrew's Homework:** missing counter, to-do counter, and Missing / Due Tomorrow / Due This Week lists from AndrewsHWTracker.
- **Fleet:** vehicle, current status, next maintenance activity.
- **DOGZ:** morning/noon/night walked and fed tracking for Tiggy and Chikatita. Dog Log is the intended system of record; unchecked does not mean an activity did not happen.
- **Fridge:** a view of myApron's Pantry inventory filtered to the Fridge storage location, emphasizing leftover foods.

## Start
Open `index.html` in a browser, or serve the directory with `python3 -m http.server 8080`.

## Integration status
This is a UI scaffold with demonstration data. No real integrations are connected yet; demonstration items are labeled. Real write-back to Dog Log and myApron is not implemented. No secrets belong in this public repository.

## Planned adapter interfaces
- `GET /api/homework` -> `{missingCount,todoCount,missing:[],dueTomorrow:[],dueThisWeek:[]}`
- `GET /api/fleet` -> `[{id,name,status,nextMaintenance}]`
- `GET /api/dogz?date=YYYY-MM-DD` -> dog activity records; POST for new records after idempotency is implemented
- `GET /api/pantry?location=Fridge` -> inventory entries including leftover type, date, and quantity

Actual paths/auth will be finalized after reviewing source project interfaces. Avoid hard-coding credentials in frontend JavaScript.

## Data rules
Do not infer that an unrecorded dog walk was skipped. The source of truth for leftovers is myApron Pantry, where Fridge is a storage location, and leftovers are food items, not a separate storage type.
