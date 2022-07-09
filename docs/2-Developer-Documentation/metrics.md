# Platform Metrics

## Event List

### DEFAULT EVENTS
- `app_load` - Landing page event, always recorded on the landing page.

### AUTHENTICATION & REGISTRATION EVENTS
- `user_signup` - Whenever a new user signup
- `user_login` - Whenever a user login
- `user_logout` - Whenever a user logouts

### GENERAL PLATFORM EVENTS
- `download_file` - Downloading keys, or notebooks.
- `update_profile` - User personal section update.
- `register_hack` - Registering for the hack followed by the survey.

### HACK EVENTS

*These events require user registration*

#### Content Viewing Events

![](img/hack_events.jpg)

- These events are tabs on the hack page, an event is recorded whenever participant clicks a tab.
- `view_calendar`
- `view_notebook`
- `view_overview`
- `view_task`
- `view_post`
- `view_profile`
- `view_rules`
- `view_tutorial`

#### User Interaction Events

- `launch_hub` - Redirected to ironhub.live, jupyterlab for participant for creating their notebooks.
- `open_survey` - Filling a survey
- `submit_comment` - Submitting comment on forum
- `user_submission` - When a user clicks the submit button, event is recorded with their link to submission.

#### Results Dashboard Events (DURING HACK)
- `results_section_view` - Personal result view 
- `results_phase_view` - Peers result view
- `results_notebook_opened` - When participants look at the notebook of other participants. 
- `results_summary_expanded` - When participants look at the summary of other participants in expanded view.

### ADMIN ONLY
- `submit_post` - Admin submitting post on forum for all participants.
- `edit_forum_post` - Editing a existing post on forum.
- `overview-updated` - Overwiew of the app is updated.
- `results-published` - Publising results.
- `results-unpublished` - Redacting the published results.
- `results-updated` - Updating existing results.
- `rules-updated` - Rules created/updated.
- `tutorial-created` - Tutorials created.
- `notes-created` - Notes created for admins/admin forum.
- `task-created` - Creating a task
- `task-published` - Task for a hack is published.
- `task-unpublished` - Task for a hack is redacted.
- `task-updated` - Existing task for a hack is updated.
