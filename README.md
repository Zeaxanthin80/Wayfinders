# My Favorite Engineering Tools - App Explanation (Homework Walkthrough)

## Introduction

Hello! This video will walk through the "My Favorite Engineering Tools" Android application, covering each requirement from the homework assignment step-by-step. I'll explain the relevant code, showcase the user interface design, and demonstrate the app's functionality.

---

**For this Homework:**

**1. Create a class for your collection with the appropriate class name (Model).**

- **Requirement:** Don't use generic name for a class name.
- **Requirement:** Add at least 3 attributes for your class.
- **Requirement:** Add setters (mutators) and getters (accessors) for all your attributes.
- **Requirement:** Add a constructor that initializes all your class attributes.

- **Implementation Details:**
  - **Class Name:** I've created a Kotlin `data class` named `EngineeringToolCategory`. This name is specific to the collection's content (engineering tool categories) and serves as our Model.
    - **File:** `app/src/main/java/edu/marquez/myfavoriteengineeringtools/EngineeringToolCategory.kt`
  - **Attributes (4 attributes, meeting the "at least 3" requirement):**
    - `id: Int`: A unique identifier for the tool category. (Read-only after creation)
    - `name: String`: The display name of the tool category. (Mutable)
    - `details: String`: A descriptive string listing examples or uses within this category. (Mutable)
    - `iconResId: Int?`: An optional Android resource ID for an icon representing this category. (Mutable, nullable)
  - **Setters (Mutators) and Getters (Accessors):**
    - Kotlin `data class` automatically generates:
      - **Getters** for all properties (`id`, `name`, `details`, `iconResId`).
      - **Setters** for properties declared with `var` (`name`, `details`, `iconResId`). The `id` is a `val`, making it read-only post-construction, which is appropriate for an identifier.
  - **Constructor:**
    - The primary constructor of the `EngineeringToolCategory` data class initializes all its attributes (`id`, `name`, `details`, and `iconResId` as an optional parameter with a default value).
    - Example: `EngineeringToolCategory(id = 1, name = "Measuring Tools", details = "...", iconResId = R.drawable.ic_some_icon)`

**2. Add the appropriate code to make the button on your Main Activity go to your Collection List Activity.**

- **Implementation Details (`MainActivity.kt`):**
  - In the `MainActivity`'s layout (`activity_main.xml`), there's a `Button` (e.g., with ID `R.id.toListButton`).
  - In `MainActivity.kt`, this button is retrieved using `findViewById`.
  - An `OnClickListener` is set on this button.
  - When the button is clicked, an `Intent` is created to start `ListActivity` (which serves as our Collection List Activity).
  - The `startActivity(intent)` method is then called.
  - _(During the video, I will demonstrate clicking this button on the Main Activity and showing the navigation to the List Activity)._

**3. Add the appropriate code to make the button on your Collection List Activity go to your Details Activity.**

- **Implementation Details (`ListActivity.kt`):**

  - In `ListActivity`, navigation to `DetailActivity` is primarily handled by user interaction with the `ListView` (ID `R.id.toolListView`) that displays the engineering tool categories. While not a traditional "button" for the whole activity, each list item acts as a navigational element to its respective details.
  - An `OnItemClickListener` is set on the `ListView`.
  - When a user taps on an item in the list:
    - The `EngineeringToolCategory` object corresponding to the clicked item is retrieved.
    - An `Intent` is created to start `DetailActivity`.
    - Data from the selected `EngineeringToolCategory` (like its `id`, `name`, `details`, and `iconResId`) are added as "extras" to this `Intent` using `putExtra()`. For example, `intent.putExtra("TOOL_NAME", selectedCategory.name)`.
  - _(During the video, I will demonstrate tapping a category in the List Activity and showing the navigation to the Detail Activity)._

- **Add the appropriate code to show all the attributes of your collection item on the Details Activity UI.**
  - **Implementation Details (`DetailActivity.kt` and `activity_detail.xml`):**
    - **Retrieving Attributes:** In `DetailActivity`'s `onCreate` method, the attributes passed via the `Intent`'s extras are retrieved (e.g., `intent.getStringExtra("TOOL_NAME")`, `intent.getStringExtra("TOOL_DETAILS")`).
    - **Displaying `name`:** The retrieved tool category name is set as the title of the App Bar in `DetailActivity`.
    - **Displaying `details`:**
      - The `TOOL_DETAILS` string, which can contain multiple points or sub-items for the category, is parsed.
      - It's split into individual lines/items (e.g., based on newline characters).
      - For each item, if it follows a "Title: Description" format, the "Title" part is styled as **bold** using `HtmlCompat.fromHtml()`.
      - These formatted detail items are then displayed in a `ListView` (ID `R.id.toolDetailsListView`) within `activity_detail.xml`, using an `ArrayAdapter` and a custom list item layout (`R.layout.detail_list_item`). This ensures all parts of the `details` attribute are visible.
    - **Displaying `iconResId`:** The `iconResId` is retrieved. While full display logic might involve an `ImageView` (code for which might be present or commented), the attribute _is_ successfully passed and available in `DetailActivity` to be used for displaying an icon.
    - **Displaying `id`:** The `id` is retrieved. Although not typically shown directly on the UI for the user, it's an important attribute that is passed and available if needed for any internal logic or future enhancements.
    - _(During the video, I will show a Detail Activity screen, pointing out the App Bar title (name attribute) and the list of details (details attribute), explaining how this covers showing all relevant attributes)._

**4. Add an App Bar to your project.**

- **Implementation Details:**

  - `MaterialToolbar` widgets are added to the layout XML files (`activity_main.xml`, `activity_list.xml`, `activity_detail.xml`) of all three activities to serve as App Bars.
  - In each activity's Kotlin file (`MainActivity.kt`, `ListActivity.kt`, `DetailActivity.kt`), the respective `MaterialToolbar` is found using `findViewById` and then set as the activity's official action bar using `setSupportActionBar(toolbar)`.

- **Set appropriate title to your App on the app bar.**

  - **Implementation Details:**
    - **`MainActivity`:** The App Bar title is typically set via the layout XML to the app's name (e.g., from `@string/app_name`, resulting in "My Favorite Engineering Tools").
    - **`ListActivity`:** The App Bar title is set programmatically in `ListActivity.kt` (e.g., to "Tool Categories" or a similar descriptive title loaded from string resources).
    - **`DetailActivity`:** The App Bar title is dynamically set in `DetailActivity.kt` to the `name` of the specific engineering tool category being displayed.
    - _(During the video, I will show each activity and point to its App Bar title, confirming it's appropriate for the screen's context)._

- **Set "Up buttons" for the Collection List Activity and Details Activity.**
  - **Implementation Details:**
    - **Enabling Up Button:** In `ListActivity.kt` and `DetailActivity.kt`, `supportActionBar?.setDisplayHomeAsUpEnabled(true)` is called within the `onCreate` method to show the Up button (back arrow) on the App Bar.
    - **Handling Up Navigation:**
      - The `onOptionsItemSelected` method is overridden in both `ListActivity` and `DetailActivity`.
      - Inside this method, if `item.itemId == android.R.id.home` (which corresponds to the Up button press), `finish()` is called. This action closes the current activity and returns the user to the previous activity in the back stack.
      - **`AndroidManifest.xml`:** To ensure correct "Up" navigation behavior (especially if considering task stacks for more complex apps), `android:parentActivityName` is specified for the `<activity>` declarations of `ListActivity` (pointing to `MainActivity`) and `DetailActivity` (pointing to `ListActivity`).
    - _(During the video, I will demonstrate the Up button on the List Activity, showing it returns to Main. Then, on the Detail Activity, show its Up button returns to List)._

---

## Conclusion

This walkthrough has demonstrated how each requirement for the homework assignment has been implemented in the "My Favorite Engineering Tools" Android application.
