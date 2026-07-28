## REBRANDING.md

This file is an audit trail of the branding-only changes made in branch `rebrand/obsidian`.

Summary
-------
- Goal: Rebrand user-visible product name from "Void" to "Obsidian Editor" while preserving all internal technical identifiers and functionality.
- Scope: Branding-only changes to product metadata and top-level documentation. No source-level renames of classes, services, IPC channels, build tasks, or internal package names unless those fields were explicitly user-visible and safe to change.

Files changed in this branch
---------------------------
1. product.json
   - Changed fields:
     - applicationName: "obsidian-editor" (was "void")
     - dataFolderName: ".obsidian-editor" (was ".void-editor")
     - urlProtocol: "obsidian-editor" (was "void")
     - darwinBundleIdentifier: "com.mobaid.obsidian-editor" (was "com.voideditor.code")
     - win32AppUserModelId: "com.mobaid.obsidian-editor" (was "Void.Editor")
     - linuxIconName: "obsidian-editor" (was "void-editor")
     - win32DirName: "Obsidian Editor" (was "Void")
     - win32NameVersion: "Obsidian Editor" (was "Void")
     - win32RegValueName: "ObsidianEditor" (was "VoidEditor")
     - win32ShellNameShort: "O&bsidian" (was "V&oid")
     - reportIssueUrl: "https://github.com/MObaidDev/VoidEditor-Fork/issues/new" (was pointing to upstream)
   - Why: These fields are used in packaging and display of the product; changing them updates the user-visible product name and packaging identifiers while keeping internal GUIDs and non-user-visible fields unchanged.

2. README.md
   - Updated user-visible references from "Void" to "Obsidian Editor" where appropriate (welcome heading, alt text for welcome image, and reference links that advertise the product name).
   - Preserved historical references about Void's deprecation to remain transparent.
   - Why: README is user-visible documentation referencing product name.

3. .devcontainer/README.md
   - Minor edits to remove or replace a handful of visible product mentions where they referred to Void. The container docs are generic; changed only explicit visible product references.
   - Why: Top-level documentation that mentions the product name.

4. REBRANDING.md
   - New file added to explain every change and provide an audit trail for reviewers.

Important decisions and constraints
----------------------------------
- Internal names, folder names (e.g., void_icons), IPC channels, services, source-level identifiers, and build tasks were NOT renamed. This preserves code stability and avoids breaking internal references.
- Icon and image files were NOT replaced in this automated pass. A manual design pass is required to supply Obsidian Editor icons and artwork. The list of exact image files that need replacement is included below.
- License and attribution texts were NOT altered.

Remaining manual follow-ups (not in this commit)
-------------------------------------------------
- Replace icon/image assets (paths listed below).
- Search and update UI strings inside src/ and resources/ for remaining user-visible "Void" references (menus, About dialog, welcome UI). These are often in localized bundles and require careful review.
- Verify packaging/installer scripts (Inno / NSIS / Squirrel / AppX) and CI workflows reference file names and AppIDs; adjust artifact names and installer metadata if you want installer outputs to use "Obsidian Editor".

List of image files that should be replaced with Obsidian Editor assets
-----------------------------------------------------------------------
- void_icons/code.ico
- void_icons/cubecircled.png
- void_icons/logo_cube_noshadow.png
- void_icons/slice_of_void.png
- src/vs/workbench/browser/parts/editor/media/slice_of_void.png (referenced from README)

How to verify locally
---------------------
1. Checkout the branch:
   git fetch origin && git checkout rebrand/obsidian
2. Review the changed files:
   git show --name-only HEAD
3. Build & smoke test:
   npm i
   bash scripts/code.sh
   (Run platform-specific packaging steps if needed)
4. Search for remaining references:
   git grep -n -- "Void" || true
   git grep -n -- "void" || true

Contact/next steps
------------------
- After replacement artwork is provided, update the image files listed above and verify the About dialog and menus show the new brand.
- If you want internal identifiers renamed (folder names, IPC channels), request a separate, careful refactor with tests and migration steps.

