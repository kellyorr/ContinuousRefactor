## Adding a T-Shirt Sizing Column to JIRA

<img src="https://wac-cdn.atlassian.com/dam/jcr:378c3943-e4b8-4870-9db5-7bc2773d17a3/jirasoftware_rgb_blue_updated.png?cdnVersion=ex)" width="100">

### Add the custom field
- On any screen in the upper right corner, click the Administration cog icon.
- In the pulldown menu under 'JIRA Administration', click 'Issues'.
- On the 'Adminstration' page in the menu on the left under 'Fields', click 'Custom Fields'.
- On the 'Custom fields' page in the upper right corner, click the 'Add custom field' button.
- On the 'Select a Field Type' screen under 'Standard', select 'Select List (multiple choices)' and click 'Next'.
- Specify value:
  - Name: "T-Shirt Size"
  - Options: "S", click 'Add'
  - Repeat for M, L, XL.
- Click the 'Create' button
- Back on the 'Custom fields', page scroll down and find 'T-Shirt Size'.
- Click the Settings cog.  In the pulldown menu, select 'Screens'.
- Find the screens where the field should appear and click 'Select'.
- Scroll to the bottom and click the 'Update' button.

### Add to Card Detail View
- At the top of the screen in the menu, click 'Boards'.
- Click the board where the 'T-shirt Size' field should appear
- On the board screen in the far most upper right corner, click the '...' button.
- In the pulldown menu, select 'Board settings'
- On the left under 'Settings', click 'Issue Detail View'.
- On the 'Issue Detail View' under General fields, select 'T-Shirt Size' from the drop down menu and click the 'Add' button
- Position the field at the top so it is near the 'Estimate' field which is a fixed part of the screen but not shown in this list.

### Add to Backlog View
- At the top of the screen in the menu, click 'Boards'.
- Click the board where the 'T-shirt Size' field should appear
- On the board screen in the far most upper right corner, click the '...' button.
- In the pulldown menu, select 'Board settings'.
- On the left under 'Settings', click 'Card layout'.
- Under Backlog, select 'T-Shirt Size' in the drop down menu and click 'Add'.
- Position the field.  Up moves the field left on the second row under the title in the backlog. Down moves right.
- Repeat for 'Active sprints'

