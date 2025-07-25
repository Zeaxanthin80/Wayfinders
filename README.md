# My Favorite Engineering Tools - App Explanation (Homework Walkthrough)

## Introduction

Hello! This video will walk through the "My Favorite Engineering Tools" Android application, covering each requirement from the homework assignment. I'll explain the relevant code, showcase the user interface design, and demonstrate the app's functionality.

## 1. Model Class: `EngineeringToolCategory`

- **Requirement:** Create a class for your collection with an appropriate class name (Model), not a generic name. Add at least 3 attributes, setters/getters, and a constructor.

- **Implementation:**
  - I've created a Kotlin data class named `EngineeringToolCategory` to serve as the model for our engineering tool categories.
  - **File:** `app/src/main/java/edu/marquez/myfavoriteengineeringtools/EngineeringToolCategory.kt`
  - **Attributes (More than 3):**
    - `id: Int`: A unique identifier for the category.
    - `name: String`: The display name of the category (e.g., "Measuring Tools").
    - `details: String`: A descriptive string listing examples or uses within this category.
    - `iconResId: Int?`: An optional Android resource ID for an icon representing this category.
  - **Constructor, Getters, and Setters:**
    - As a Kotlin `data class`, `EngineeringToolCategory` automatically receives a primary constructor that initializes all these properties (`id`, `name`, `details`, `iconResId`).
    - Kotlin also auto-generates:
      - Getters for all properties (`id`, `name`, `details`, `iconResId`).
      - Setters for `var` properties (in this class, `name`, `details`, and `iconResId` were defined as `var` initially, allowing modification, though `id` is a `val` for immutability after creation).
    - This fulfills the requirement for a constructor and accessors/mutators.

## 2. Navigation: Main Activity to Collection List Activity

- **Requirement:** Add appropriate code to make the button on your Main Activity go to your Collection List Activity.

- **Implementation (`MainActivity.kt`):**
  - In `MainActivity`, there's a button (ID: `R.id.toListButton`).
  - An `OnClickListener` is set on this button.
  - When clicked, it creates an `Intent` to start `ListActivity` (our Collection List Activity).
  - **Code Snippet (Conceptual from `MainActivity.kt`):**
