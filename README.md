# Localization Repository

This repository contains localization files used by the application and SDK.

Localization is YAML-based and languages are detected automatically at runtime.
Adding a new language does not require code changes in the application.

---

## What Is Localized

- Application UI (windows, dialogs, controls)
- Activities and actions
- Exceptions and validation messages
- SDK-related UI resources

Installer localization will be added in the future.

---

## How Localization Works

- Localization files are stored as `*.loc.yaml`
- Each file contains nested localization keys
- Each key can define translations for multiple languages using language codes (`en`, `pl`, `es`, etc.)
- Language names displayed in the UI are defined in `gdsk.ui.languages.loc.yaml`

If a translation is missing, the application displays the localization key instead.

---

## Where Files Are Used

The application loads localization files from the `Loc` directory in the installation folder.

Default location:
```

C:\Program Files\Clipboard Genie\Loc

```

---

## Adding or Updating Translations

If you want to contribute translations, please read:

➡ **`CONTRIBUTING.md`**

---

## Testing Changes

To test translations locally:
1. Copy modified `*.loc.yaml` files to the application `Loc` directory
2. Restart the application
3. Select the language in **Settings → Application → Language**
4. Restart the application again to apply the change

