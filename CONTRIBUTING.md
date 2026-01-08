# Localization – Contribution Guide

This document explains how to add or update translations for the application.

Localization is based on YAML files and is automatically detected by the application at runtime.

---

## Where Localization Files Are Used

The application loads localization files from the `Loc` directory located in the application installation folder.

Default path:

```
C:\Program Files\Clipboard Genie\Loc
```

When this guide refers to files such as `controls.loc.yaml`,
it always means the files located in that `Loc` directory.

---

## Recommended Workflow

It is recommended to work on the **latest version of this GitHub repository**
instead of editing localization files directly inside the installed application.

Why:

* The repository may contain newer localization keys
* Application files may be outdated
* Application updates may overwrite local changes

### Suggested workflow

1. Clone or download the latest version of this repository
2. Add or update translations in the repository files
3. To test translations:

   * Copy the modified `*.loc.yaml` files
   * Paste them into the application's `Loc` directory
4. Restart the application to verify the changes

---

## Repository Structure – `app` and `sdk`

For better long-term organization, localization files in this repository are split into two logical parts:

```
app/
  Loc/
    *.loc.yaml

sdk/
  Loc/
    *.loc.yaml
```

### Purpose of this split

* **`app/Loc`** – localization used directly by the application UI
* **`sdk/Loc`** – localization for shared SDK / reusable components

This structure exists **only in the repository**.

---

## Testing Localization in the Application

⚠️ **Important**

The installed application does **not** use the `app` / `sdk` directory structure.

To test localization changes:

1. Collect **all `*.loc.yaml` files** from:

   ```
   app/Loc
   sdk/Loc
   ```
2. Copy them into the application localization directory:

   ```
   C:\Program Files\Clipboard Genie\Loc
   ```
3. Restart the application

All localization files must be placed together in a **single `Loc` directory`.
Subdirectories are **not supported at runtime**.

---

## Localization File Structure

Localization files (`*.loc.yaml`) contain nested keys.
Each final key defines translations for one or more languages.

Example:

```yaml
SettingsWindow:
  Title:
    en: Clipboard Genie Settings
    pl: Ustawienia Clipboard Genie
```

The localization key in this case is:

```
SettingsWindow.Title
```

---

## Multiline Localization Entries

Localization values can be defined using YAML multiline blocks (`|-`).

Example:

```yaml
PromptTemplateInfo:
  en: |-
    You can use the following variables in this prompt:
      - {{Clipboard.Text}}: The text of the current clipboard item.
      - {{UILanguage}}: The language selected for the user interface.
  pl: |-
    W tym szablonie promptu możesz użyć następujących zmiennych:
      - {{Clipboard.Text}}: Tekst aktualnego elementu schowka.
      - {{UILanguage}}: Język wybrany dla interfejsu użytkownika.
```

Rules:

* Preserve indentation
* Preserve all placeholders (`{{...}}`)
* Do not translate variable names inside placeholders

---

## Getting Started – Adding a New Language Translation

### Step 1: Find the language code

Open `gdsk.ui.languages.loc.yaml` and locate the language identifier.

Example:

```yaml
LanguageName:
  lang_es:
    en: Spanish
    pl: Hiszpański
```

The language code is:

```
es
```

---

### Step 2: Add translations using the language code

Open the appropriate localization file, for example `controls.loc.yaml`.

Existing entry:

```yaml
SettingsWindow:
  Title:
    en: Clipboard Genie Settings
    pl: Ustawienia Clipboard Genie
```

Add a new translation:

```yaml
SettingsWindow:
  Title:
    en: Clipboard Genie Settings
    pl: Ustawienia Clipboard Genie
    es: Configuración de Clipboard Genie
```

---

### Step 3: Restart the application (for testing)

A full application restart is required **to rebuild the language map**.

After restarting:

1. Open **Settings → Application → Language**
2. The new language (e.g. **Spanish**) should appear in the list
3. Select it and restart the application again

Result:

* The Settings window title will use the new translation
* All other untranslated entries will display their localization keys

Example fallback:

```
SomeSection.SomeKey
```

This behavior is expected and helps identify missing translations.

---

## Language Names (UI Display)

Language names are defined in `gdsk.ui.languages.loc.yaml`.

Each language must define its name in **all supported UI languages**.

Example:

```yaml
LanguageName:
  lang_en:
    en: English
    pl: Angielski

  lang_pl:
    en: Polish
    pl: Polski
```

Behavior:

* English UI → `English`, `Polish`
* Polish UI → `Angielski`, `Polski`

Language name keys always follow this format:

```
lang_<language-code>
```

Examples:

* `lang_en`
* `lang_pl`
* `lang_es`
* `lang_de-CH`
* `lang_en-GB`

---

## Regional Language Codes

Regional variants are supported.

Examples:

* `en-GB`
* `en-AU`
* `de-CH`

Rules:

* Use the same language code everywhere
* Use the same code in localization files and language name keys

---

## Missing Translations

If a translation is missing for the selected language,
the application displays the localization key instead.

Example:

```
ActivateWindowActivity.Name
```

---

## Placeholders (Variables) – IMPORTANT

Some localization values contain placeholders replaced at runtime.

Example:

```yaml
TestSuccess:
  en: "Test was successfully completed. Http Response code: {v}"
  pl: "Test został pomyślnie zakończony. Kod odpowiedzi HTTP: {v}"
```

Rules:

* Do not translate placeholders
* Do not rename placeholders
* Do not remove placeholders

---

## Formatting Rules

* Use spaces only (no tabs)
* Preserve indentation
* Keep language codes consistent
* Validate YAML before committing

---

Thank you for contributing to localization!
