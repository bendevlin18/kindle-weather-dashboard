# Kindle Weather Dashboard — Planned Improvements

## Code Quality
- [ ] Replace `window.setTimeout("string")` eval-style calls with function references in `refreshData`, `clearScreen`, and the 4am cleanup timer
- [ ] Fix `clearScreen` 4am scheduling to be compatible with RTC sleep/wake timing

## Features
- [x] Display humidity, wind speed/direction, and precipitation from current weather API response (data is already returned, just not shown)
- [x] Make forecast column count configurable from the config page (currently hard-coded at 5)
- [x] Add graceful error handling when the API fails — show a message or last-known data instead of a blank screen

## New Pages / Integrations

### Home Assistant Dashboard (separate port)
- [x] Create a second Kindle-optimized page (`ha.html`) that pulls live data from Home Assistant via its REST API
- [x] Show useful home state at a glance: thermostat, lights, door sensors, presence, switches, sensors (configurable via `ha-config.js`)
- [x] Display current time prominently (large clock, same e-ink-friendly style as the weather dashboard)
- [x] Reuse the same night mode, rotation, and rem-scaling system from the weather dashboard

### Weather Quote / Remark
- [x] Add a weather-context remark line to the main dashboard — e.g. "Bring an umbrella" on rain days, "Great day for a walk" when sunny and mild, "Stay inside" on extreme heat/cold
- [x] Rules can be driven purely from the existing OWM data already fetched (weather id, temp, wind speed) — no extra API needed
- [x] Display as a small italic line below the weather description, or in the unused space on the left side beneath the main icon

## Config Page UX
- [ ] Mask the `appId` input field (type="password") to avoid exposing the API key on screen
- [ ] Add client-side validation requiring at least city or lat/lon before the form submits

## API / Compatibility
- [ ] Handle the OWM `forecast/daily` endpoint gracefully — it requires a paid plan on newer OWM accounts; show a clear error or fall back to hourly if it returns a 401/404
- [x] Removed tap-to-toggle hourly/daily from forecast area — `forecast/daily` requires a paid OWM plan and caused a crash; forecast type is now controlled via config.js only

## Done
- [x] Language fixed: `api_lang` changed from `"sk"` (Slovak) to `"en"` (English) in config.js
- [x] Forecast time font size increased from 5rem to 6.5rem
