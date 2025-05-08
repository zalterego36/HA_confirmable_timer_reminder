# HA Confirmable Timer Reminder

This project lets you track how many days it's been since a task was completed (like cleaning the toilet). It can:

- Send you a confirmation prompt asking if the task has been done.
- Reset the timer if you confirm "Yes."
- Send reminder notifications if the task hasn't been done in a set number of days.
- Optionally enable/disable reminders with a toggle.

> ⚠️ This blueprint was created for personal use with the help of AI (~70%). It’s meant for Home Assistant users who are comfortable setting up blueprints, helpers, and automations.

---

## Step 1: Import the Blueprint into Home Assistant

1. Go to **Settings > Automations & Scenes > Blueprints**.
2. Click **"Import Blueprint"** or **"Add Blueprint"**.
3. Paste the raw GitHub URL of the `blueprint.yaml` file and import it.

   > If importing manually:
   - Open the `blueprint.yaml` file.
   - Copy the full contents.
   - Paste it into the blueprint editor in Home Assistant.
   - Save it. You should now see the blueprint titled **"Confirmable Reminder with Timer Reset."**

---

## Step 2: Create Required Helper Entities

You’ll need some helper entities to track task completion and (optionally) toggle reminders.

### ✅ input_datetime (Required)

Used to store the last time the task was completed.

- Go to **Settings > Devices & Services > Helpers**.
- Create a new `input_datetime`, such as:

input_datetime.toilet_last_cleaned

### ✅ input_boolean (Optional)

Used to enable or disable reminder notifications.

- Go to **Settings > Devices & Services > Helpers**.
- Create a new `input_boolean`, such as:

input_boolean.toilet_reminder_enabled


---

## Step 3: Create an Automation Using the Blueprint

1. Go to **Settings > Automations & Scenes > Automations**.
2. Click **"Add Automation"**, then choose **"Start with a Blueprint."**
3. Select **"Confirmable Reminder with Timer Reset."**

Fill in the fields:

- **Task Name**: e.g., `Toilet Cleaning`
- **Date/Time Entity**: e.g., `input_datetime.toilet_last_cleaned`
- **Reminder Interval**: e.g., `7` days
- **Notification Target**: e.g., `notify.mobile_app_your_phone`
- **Reminder Toggle** *(optional)*: e.g., `input_boolean.toilet_reminder_enabled`

Click **Save** when done.

---

## Step 4: Handle Notification Responses ("Yes"/"No")

The blueprint sends a mobile notification with Yes/No buttons. You need a separate automation to respond to the “Yes” button, this can be found under 'Automation'.

---

## Step 5: Optional — Add a Dashboard Card

You can use a custom card to view and trigger reminders from your dashboard.

Requires the Button Card from HACS (https://github.com/custom-cards/button-card).

Go to Overview > Edit Dashboard > Add Card.

Choose Manual or YAML.

Paste your button card configuration (see example in the repo).

Save the dashboard.

---

## Step 6: Testing and Debugging

Manually change the input_datetime to simulate the task being done.

Wait for the scheduled reminder time (e.g., 9:00 AM).

Check if the notification is sent.

Tap “Yes” and verify the timer is reset.

Review Home Assistant’s Trace if things don’t work as expected.
