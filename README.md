# homeassistant-misc
This repo is for random things related to Home Assitant that I've found, collected, built, created, whatever. Please make sure you look at the code before using them. I'm not malicious but why would you trust my word? Use any script here at your own risk.


---

## Blueprints
### [NFC Maintenance Reminder Blueprint](blueprints/nfc_maintenance_reminder.yaml)

A Home Assistant blueprint that tracks maintenance tasks using NFC tags. Scan a tag when you complete a task (like replacing a filter), and get reminded after a configurable number of days with snooze support.

#### Setup

1. Settings → Automations & Scenes → Blueprints
2. Import Blueprint - https://github.com/ShakataGaNai/homeassistant-misc/blob/main/blueprints/nfc_maintenance_reminder.yaml

#### Usage

For each maintenance task:

1. **Create two helpers** (Settings → Devices & Services → Helpers → Create Helper → Date and/or time, select "Date" only):
   - `{task_name}_replaced` — stores when the task was last completed
   - `{task_name}_snoozed` — stores when the reminder was snoozed

2. **Create an NFC tag** using the Home Assistant Companion app (Settings → Tags → Add Tag)

3. **Create an automation** from the blueprint (Settings → Automations → Create Automation → Use Blueprint) and fill in:
   - **NFC Tag ID** — the tag you created
   - **Replaced/Snoozed Date Helpers** — the helpers you created
   - **Task Name** — displayed in notifications (e.g., "HVAC Filter")
   - **Days Until Reminder** — how long before you're reminded (default: 90)
   - **Snooze Duration** — how long snooze lasts (default: 3 days)
   - **Reminder Time** — when to check daily (default: 10:00 AM)
   - **Mobile Notify Service** — your notify service (e.g., `notify.mobile_app_my_phone`)
   - **Telegram Device ID** — optional, leave blank to skip Telegram notifications

4. **Scan the tag** to initialize the first date
