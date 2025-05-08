# HA_confirmable_timer_reminder
Confirmable Timer - Tracks the number of days since a task was last done.  Lets you trigger a confirmation prompt ("Have you done the task?") from a button, automation, etc.  If the user answers Yes, the timer is reset. If No, nothing happens.  Sends an optional reminder notification after a threshold number of days.
This was built for personal use and used about 70% AI to guide the process and assist me as I'm not a (competent) programmer by any means.

Step 1: Create a Blueprint in Home Assistant

    Access Home Assistant Configuration:

        Open your Home Assistant web interface.

        Go to Settings > Automations & Scenes.

        Under the Blueprints tab, click on Add Blueprint.

    Copy the blueprint.yaml file:

        In the blueprint editor, copy the entire YAML template I provided.

    Paste into the Blueprint Editor:

        Paste the YAML template into the editor and save it. This will create a new blueprint called "Confirmable Reminder with Timer Reset."

Step 2: Create the Necessary Helper Entities

To track the task completion and enable/disable reminders, you'll need to create some helper entities. These can be created manually or via YAML configuration.

    Create input_datetime (if not already created):

        Go to Settings > Devices & Services > Entities.

        Create a new input_datetime entity for the task, such as input_datetime.task_name_last_done

    Create input_boolean (if needed for reminders):

        Go to Settings > Devices & Services > Entities.

        Create an input_boolean entity for toggling reminders, such as input_boolean.task_name_reminder_enabled.

Step 3: Use the blueprint for a specific task (e.g., Toilet Cleaning), follow these instructions:

    Navigate to the Automations Section:

        Go to Settings > Automations & Scenes > Automations.

        Click Add Automation.

    Select the Blueprint:

        Select the blueprint "Confirmable Reminder with Timer Reset" from the list of available blueprints.

    Fill in the Required Inputs:

        Task Name: Enter a name for the task, e.g., "Toilet Cleaning."

        Date/Time Entity: Select or create an input_datetime entity to track when the task was last completed (e.g., input_datetime.toilet_last_cleaned).

        Reminder Interval: Choose how many days to wait before sending the reminder (e.g., 7 days).

        Notification Target: Specify which notification service to use (e.g., notify.mobile_app_your_phone).

        Reminder Toggle (optional): If you want the ability to turn reminders on/off, create an input_boolean (e.g., input_boolean.task_name_reminder_enabled).

    Save the Automation:

        After filling out the fields, click Save to create the automation.

Step 4: Handle Task Confirmation via Automation

    Create a New Automation for Task Response:

        This automation will handle the user's response to the confirmation notification (Yes/No).

        In Automations & Scenes, create a new automation that will handle the event triggered by the mobile app action (Yes/No) using the template provide under 'Automation'.

        Save the automation to handle the response to the notification.

Step 5: Add Dashboard Card (Optional - Mine Requires the Button Card Addon from HACs or Create your Own)

To allow quick access to the task reminder and last completed date, add a dashboard card.

    Edit the Dashboard:

        Navigate to Overview.

        Click on the three dots in the top right corner and choose Edit Dashboard.

    Add the Custom Button Card:

        In the YAML section of the card configuration, copy and paste the 'Dashboard Card'.
        
    Save the Changes.

Step 6: Testing and Debugging

    Test the Automation:

        Trigger the automation by manually changing the time or by manipulating the input_datetime to simulate the task being completed.

        Check if the reminder notification sends correctly.

        Test the "Yes" and "No" responses by interacting with the notification.

    Adjust as Needed:

        Fine-tune the template or automation if anything isn't behaving as expected (e.g., adjusting triggers, conditions, or actions).
