# My Favorite Engineering Tools - App Explanation

## Introduction

Hello! This video will walk through the "My Favorite Engineering Tools" Android application. I'll cover the code structure, the user interface design, and demonstrate the app's functionality through testing.

## 1. Code Structure - The Model (Data Class)

- **Model Class:**
  - To represent our collection of engineering tools, I've created a data class named `EngineeringToolCategory`. This class acts as the model for our data.
  - **File:** `app/src/main/java/edu/marquez/myfavoriteengineeringtools/EngineeringToolCategory.kt`
- **Attributes:**
  - This class has the following attributes:
    - `id`: An `Int` to uniquely identify each tool category.
    - `name`: A `String` for the name of the tool category (e.g., "Measuring Tools").
    - `details`: A `String` containing a description or list of tools within that category.
    - `iconResId`: An optional `Int` to store the resource ID for an icon representing the category.
- **Constructor, Getters, and Setters:**
  - Being a `data class` in Kotlin, it automatically provides a constructor that initializes all these attributes.
  - Kotlin data classes also auto-generate getters for `val` properties and both getters and setters for `var` properties. In our `EngineeringToolCategory` class, since the properties are defined with `val`, they are read-only after instantiation, which is suitable for our current needs.

## 2. User Interface (UI) Design and Navigation

The app consists of three main screens (Activities):

- **Main Activity (`MainActivity.kt`, `activity_main.xml`)**

  - **UI:** This is the entry point of the app. It displays the app title and features a prominent button.
  - **App Bar:** It has an App Bar with the application's title, "My Favorite Engineering Tools".
  - **Navigation:**
    - A button (e.g., "View Tool Categories") navigates the user to the Collection List Activity.
    - The code for this is in `MainActivity.kt`, where an `Intent` is used to start `ListActivity`.

- **Collection List Activity (`ListActivity.kt`, `activity_list.xml`)**

  - **UI:** This screen displays a list of engineering tool categories (e.g., "Measuring Tools," "Hand Tools"). Each item in the list is clickable.
  - **App Bar:**
    - It features an App Bar with the title (e.g., "Tool Categories").
    - An "Up button" is present, allowing navigation back to the `MainActivity`. This is enabled in `ListActivity.kt` and defined in the `AndroidManifest.xml`.
  - **Navigation:**
    - Selecting a category name from the list takes the user to the `DetailActivity` to view the specifics of that category.
    - The code for this is in `ListActivity.kt`. When an item is clicked, an `Intent` is created, and data like the tool's ID, name, details, and icon resource ID are passed to the `DetailActivity`.

- **Details Activity (`DetailActivity.kt`, `activity_detail.xml`)**
  - **UI:** This screen shows the detailed information for a selected engineering tool category.
    - The details are displayed in a `ListView`, where each item in the details string (e.g., "Multimeters: Used to measure...") is shown.
    - The name of the tool/item within the details is displayed in **bold**, followed by its description in regular font.
  - **App Bar:**
    - The App Bar's title is dynamically set to the name of the currently displayed tool category.
    - An "Up button" is present, allowing navigation back to the `ListActivity`. This is handled in `DetailActivity.kt` and defined in the `AndroidManifest.xml`.
  - **Displaying Attributes:**
    - The `DetailActivity` retrieves the `TOOL_NAME`, `TOOL_DETAILS`, and `TOOL_ICON_RES_ID` from the `Intent`.
    - The `TOOL_NAME` is used for the App Bar title.
    - The `TOOL_DETAILS` string is parsed:
      - It's split into individual items (assuming items are separated by newlines).
      - Each item is further processed to separate the name/title from its description (assuming a colon separates them).
      - `HtmlCompat.fromHtml()` is used to style the name part as bold.
    - The parsed and styled items are then displayed in a `ListView` using an `ArrayAdapter` and a custom list item layout (`detail_list_item.xml`).
    - The `toolIconResId` is retrieved and can be used to display an icon (code for this is present but might be commented out or pending full implementation with an `ImageView`).

## 3. App Testing (Demonstration)

_(In this section of the video, you would navigate through the app)_

1.  **Launch the App:**
    - Show the `MainActivity` with the app title and the main button.
2.  **Navigate to Collection List:**
    - Click the button on `MainActivity`.
    - Observe `ListActivity` appearing, displaying the list of tool categories.
    - Point out the App Bar title and the "Up button" on `ListActivity`.
    - Test the "Up button" on `ListActivity` to ensure it goes back to `MainActivity`. Then navigate forward again.
3.  **Navigate to Details:**
    - Select a tool category from the list in `ListActivity`.
    - Observe `DetailActivity` appearing.
    - Point out that the App Bar title on `DetailActivity` correctly shows the selected category's name.
    - Show how the details of the category are displayed:
      - Each tool/item name is in bold.
      - The description follows in regular font.
      - Wrapped lines for longer descriptions correctly align.
    - Point out the "Up button" on `DetailActivity`.
    - Test the "Up button" on `DetailActivity` to ensure it goes back to `ListActivity`.
4.  **Test with Multiple Categories:**
    - Repeat selecting different categories from `ListActivity` to show that `DetailActivity` updates correctly for each one.

## Conclusion

This covers the main structure, UI, and functionality of the "My Favorite Engineering Tools" app, fulfilling the homework requirements including the data model, navigation between activities, display of all attributes, and the implementation of App Bars with titles and Up buttons.
