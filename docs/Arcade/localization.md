---
title: Localization
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

# Localization Guide for Arcade CMS

## Description

Localization in Arcade CMS allows you to manage and deliver content in multiple languages for your games and experiences. This feature ensures that users from different regions can interact with your product in their preferred language, improving accessibility and engagement.

## Usage

* **Accessing Localization:**
  * Navigate to the Localization section in the CMS dashboard.
  * Select the desired locale (language) from the dropdown menu.
  * Choose the screen or module you wish to localize.
  * Edit the text fields for each screen and save your changes.
* **Supported Locales:**
  * The CMS supports all standard language codes (e.g., `en` for English, `es` for Spanish).
  * You can add new locales as needed.

## How to Add Localization Using CMS

1. **Add a New Locale:**
   * Go to the Localization section.
   * Click "Add Locale" and enter the language code (e.g., `fr` for French).
2. **Set Default Language:**
   * Once you prepare your desired set of supported locales, you can select which one will be the default language. English (`en`) is the default if no changes are made.
3. **Configure Screens:**
   * For each locale, select the screens/modules to localize.
   * Enter translations for each field (e.g., button labels, messages).
4. **Save and Preview:**
   * Save your changes.
   * Use the preview feature to see how the localized content appears in the app.

## Localization Configuration Options

* **Locale List:**
  * Displays all available languages. You can reorder or remove locales.
  * The first locale in the list (usually 'en') is used as the default language for your app. To set a different default, reorder the locales so your preferred default is first.
* **Screen Selection:**
  * Choose which screens/modules to localize for each language.
* **Field Editing:**
  * Edit individual text fields for each screen and locale.
* **Bulk Upload:**
  * Upload CSV files to update multiple translations at once.
* **Download Template:**
  * Download a CSV template to help you prepare your localization data for bulk upload. The template includes all required fields and headers.

## Synchronization

* **Automatic Sync:**
  * Changes made in the step wise copies are automatically synced to the localization step after saving.
* **Manual Sync:**
  * Any further changes made in the localization step will also sync to the step wise copies but the producer will have to manually trigger the sync by saving that step again.

## Troubleshooting

* **Missing Translations:**
  * If a field is not translated, the app will display the default language (English).
* **Locale Not Appearing:**
  * Ensure the desired locale is properly set and part of supported locales list in the CMS.
* **Sync Issues:**
  * Try manual sync if found unexpected behavior or the data is out of sync.
* **CSV Upload Errors:**
  * Make sure your CSV file matches the required template format.
  * Check for missing headers or invalid characters.
