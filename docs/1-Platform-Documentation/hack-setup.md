# Hack Admin

> Admin users must be manually added by a developer.

Platform admins can create and manage hacks from the administrator portal at `/admin`.

## Hack Settings

![](./img/ironhacks-admin.jpg)

The hack settings page allows you to update content for a hack including

- name - The title of the hack
- slug - the hacks url path
- description - a brief description of the hack
- banner image - the image displayed at the top of the overview page
- thumbnail image - a small image displayed in the hack selection screen
- publish and unpublish - determines if the hack is visible in the selection screen
- registration open - manually sets the registration open or closed
- display options - sets which pages will be visible in the hack navigation
- registration survey - if this is filled in then participants will be required to fill in the survey when registering
- difficulty - sets the hack difficulty category  

## Hack Content

Content for the hack can be added in several places in the admin area using the integrated markdown editor.

__Overview Page__

The hack overview page is the landing page for the hack. This content is also displayed on the hack registration page.

__Rules Page__

If `rules enabled` is checked in the hack display settings then the content here will be displayed on the rules page.

__Task Page__

The task page has a unique property that allows you create multiple task documents which can be shown to specific cohorts (managed in the cohort settings area). You should set the default task document if you do not intend to use this feature, which will be shown to any user not in a cohort or if that participants cohort does not have a set task.

Only one task can ever be shown to the participant.

Each task may enable the a survey url to be included before the task is viewable by the user (this must be manually enabled for each task).

To include the task page in the hack navigation area `task enabled` you must click `publish task` in the admin task editor view. This feature was created to help track the specific event timing between the start of the hack, registration, and when the task is made avaiable (when users can actually start working on their submission).

__Tutorials Page__

You can create multiple tutorials which will be displayed in the hack tutorials list.

## Hack Submissions

Submissions have the following properties:

- Name
- Submission Id
- Deadline
- Survey Url
- Description
- Submisison Options
  - Submission Summary
  - Submission Tags
- Additional Fields
- Submission Files
- Submission Enabled
- Solution File
