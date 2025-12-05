# homeassistant-misc
This repo is for random things related to Home Assistant that I've found, collected, built, created, whatever. Please make sure you look at the code before using them. I'm not malicious but why would you trust my word? Use any script here at your own risk.


---

## Blueprints
### [NFC Maintenance Reminder Blueprint](blueprints/nfc_maintenance_reminder.yaml)

A Home Assistant blueprint that tracks recurring maintenance tasks using NFC tags. Stick an NFC tag near something that needs periodic maintenance, scan it when you complete the task, and get reminded after a configurable number of days. Includes snooze support for when you can't get to it right away.

**Example use cases:**
- HVAC filter replacement (90 days)
- Refrigerator water filter replacement (180 days)
- Pool filter cleaning (180 days)
- Water heater draining (365 days)
- Smoke detector battery replacement (180 days)
- Dryer vent cleaning (365 days)
- Car oil change (90 days)
- Gutter cleaning (180 days)
- Water softener salt refill (60 days)
- Fish tank filter cleaning (14 days)

#### Setup

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FShakataGaNai%2Fhomeassistant-misc%2Fblob%2Fmain%2Fblueprints%2Fnfc_maintenance_reminder.yaml)

1. Settings → Automations & Scenes → Blueprints
2. Import Blueprint - https://github.com/ShakataGaNai/homeassistant-misc/blob/main/blueprints/nfc_maintenance_reminder.yaml

#### Usage

For each maintenance task:

1. **Create two helpers** (Settings → Devices & Services → Helpers → Create Helper → Date and/or time, select "Date" only):
   - `{task_name}_completed` — stores when the task was last completed
   - `{task_name}_snoozed` — stores when the reminder was snoozed

2. **Create an NFC tag** using the Home Assistant Companion app (Settings → Tags → Add Tag)

3. **Create an automation** from the blueprint (Settings → Automations → Create Automation → Use Blueprint) and fill in:
   - **NFC Tag ID** — the tag you created
   - **Completed/Snoozed Date Helpers** — the helpers you created
   - **Task Name** — displayed in notifications (e.g., "HVAC Filter", "Pool Filter")
   - **Days Until Reminder** — how long before you're reminded (default: 90)
   - **Snooze Duration** — how long snooze lasts (default: 3 days)
   - **Reminder Time** — when to check daily (default: 10:00 AM)
   - **Mobile Notify Service** — your notify service (e.g., `notify.mobile_app_my_phone`)
   - **Telegram Device ID** — optional, leave blank to skip Telegram notifications

4. **Scan the tag** to initialize the first date
