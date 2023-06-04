# Project fields

Text and number fields
In this article
Adding a text field
Adding a number field
You can add custom text and number fields to your project.

You can use text fields to include notes or any other freeform text in your project.

Text fields can be used in filters, for example: field:"exact text". Text fields and item titles will also be used if you filter for text without specifying a field.

Number fields can also be used in filters. You can use >, >=, <, <=, and .. range queries to filter by a number field. For example: field:5..15 or field:>=20.

## Adding a text field

1. In table view, in the rightmost field header, click +.
2. Click New field.
3. At the top of the dropdown, type the name of your new field.
4. Select Text.
5. Click Save.

Alternatively, open the project command palette by pressing Command+K (Mac) or Ctrl+K (Windows/Linux) and start typing "Create new field."

## Adding a number field

1. In table view, in the rightmost field header, click +.
2. Click New field.
3. At the top of the dropdown, type the name of your new field.
4. Select Number.
5. Click Save.

Alternatively, open the project command palette by pressing Command+K (Mac) or Ctrl+K (Windows/Linux) and start typing "Create new field."

## Date fields

You can create custom date fields that can be set by typing a date or using a calendar.

You can filter for date values using the YYYY-MM-DD format, for example: date:2022-07-01. You can also use operators, such as >, >=, <, <=, and ... For example, date:>2022-07-01 and date:2022-07-01..2022-07-31. You can also provide @today to represent the current day in your filter.

If your project makes use of date fields, you can use the roadmap layout to view items on a timeline.

### Adding a date field

1. In table view, in the rightmost field header, click +.
2. Click New field.
3. At the top of the dropdown, type the name of your new field.
4. Select Date
5. Click Save.

Alternatively, open the project command palette by pressing Command+K (Mac) or Ctrl+K (Windows/Linux) and start typing "Create new field."

## Single select fields

You can create single select fields with multiple options, each with a description and a color, that can be selected from a dropdown menu.

You can filter by your single select fields by specifying the option, for example: fieldname:option. You can filter for multiple values by providing a comma-separated list of options, for example: fieldname:option,option.

Single select fields can contain up to 50 options.

### Adding a single select field

1. In table view, in the rightmost field header, click +.
2. Click New field.
3. At the top of the dropdown, type the name of your new field.
4. Select Single select
5. Below "Options", type the first option.
   1. To add additional options, click Add option.
6. Click Save.

Alternatively, open the project command palette by pressing Command+K (Mac) or Ctrl+K (Windows/Linux) and start typing "Create new field."

### Editing a single select field

You can set descriptions and colors for each of your single select options.

1. Access your project's settings.
2. To the right of the single select field you want to edit, click (pencil).
3. In the modal that opens, under Label text, type the name of this option.
4. Optionally, under Color, select the color you want to use to represent this option.
5. Optionally, under Description, type a description for this option.
6. Click Save to save your changes.

## Iteration fields

You can create iterations to plan upcoming work and group items.

You can create an iteration field to associate items with specific repeating blocks of time. Iterations can be set to any length of time, can include breaks, and can be individually edited to modify name and date range. With projects, you can group by iteration to visualize the balance of upcoming work, use filters to focus on a single iteration, and sort by iteration.

You can filter for iterations by specifying the iteration name or @current for the current iteration, @previous for the previous iteration, or @next for the next iteration. You can also use operators such as >, >=, <, <=, and ... For example, iteration:>"Iteration 4" and iteration:<@current.

When you first create an iteration field, three iterations are automatically created. You can add additional iterations and make other changes on your project's settings page.
If your project makes use of iteration fields, you can use the roadmap layout to view items on a timeline.

### Adding an iteration field

1. In table view, in the rightmost field header, click +.
2. Click New field.
3. At the top of the dropdown, type the name of your new field.
4. Under "Field type", select Iteration.
5. Optionally, if you don't want the iteration to start today, select the calendar dropdown next to "Starts on" and choose a new start date.
6. To change the duration of each iteration, type a new number, then select the dropdown and click either days or weeks.
7. Click Save.

Alternatively, open the project command palette by pressing Command+K (Mac) or Ctrl+K (Windows/Linux) and start typing "Create new field."

### Adding new iterations

1. Navigate to your project.
2. In the top-right, click ... to open the menu.
3. In the menu, click Settings to access the project settings.
4. Click the name of the iteration field you want to adjust.
5. To add a new iteration of the same duration, click Add iteration.
6. Optionally, to customize the duration of the new iteration and when it will start, click (arrow-down) More options, select a starting date and duration, and click Add.
7. Click Save changes.

### Editing an iteration

You can edit iterations in your project settings. You can also access the settings for an iteration field by clicking in the table header for the field and clicking Edit values.

1. Navigate to your project.
2. In the top-right, click ... to open the menu.
3. In the menu, click (screw) Settings to access the project settings.
4. In the list on the left, click the name of the iteration field you want to adjust.
5. To change the name of an iteration, click on the name and start typing.
6. To change the date or duration of an iteration, click on the date to open the calendar. Click on the start day, then click the end day, and then click Apply.
7. Optionally, to delete an iteration, on the right of the iteration, click (trash).
8. Click Save changes.

### Inserting a break

You can insert breaks into your iterations to communicate when you are taking time away from scheduled work. The duration of a new break defaults to the length of the most recently created iteration.

1. Navigate to your project.
2. In the top-right, click ... to open the menu.
3. In the menu, click (screw) Settings to access the project settings.
4. Click the name of the iteration field you want to adjust.
5. Hover over the dividing line above an iteration, then click Insert break.
6. Optionally, to change the duration of the break, click on the date to open the calendar. Click on the start day, then click the end day, and then click Apply.
7. Click Save changes.

## About Tracks and Tracked by fields

[About tracks and tracked by fields](https://docs.github.com/en/issues/planning-and-tracking-with-projects/understanding-fields/about-tracks-and-tracked-by-fields)

## Renaming custom fields

[Renaming custom fields](https://docs.github.com/en/issues/planning-and-tracking-with-projects/understanding-fields/renaming-custom-fields)

## Deleting custom fields

[Deleting custom fields](https://docs.github.com/en/issues/planning-and-tracking-with-projects/understanding-fields/deleting-custom-fields)
