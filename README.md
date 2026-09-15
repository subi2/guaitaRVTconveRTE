<!--
  Guaita Apps - Suite of standalone tools for architecture, BIM and documentation.
  Copyright (c) 2026 Jordi Subirós
  GNU Affero General Public License v3.0
  See LICENSE file for details
-->

# GUAITA·RVT — Guaita RVT conveRTE

`User guide`

## Turn an RVT project into an RTE *template* (and back).

Guaita RVT conveRTE flips the internal type of a file —from project `.rvt` to template `.rte` or the other way round— by modifying a single marker inside the document, entirely within your browser and without sending the file anywhere.

## Contents

1. [What it is](#01--introduction)
2. [RVT and RTE](#02--project-and-template)
3. [Getting started](#03--getting-started)
4. [The interface](#04--the-interface)
5. [Detection](#05--how-it-detects-the-type)
6. [Convert and save](#06--convert-and-save)
7. [Limits and guarantees](#07--limits-and-guarantees)
8. [Troubleshooting](#08--troubleshooting)

---

## 01 · Introduction

### An RVT/RTE file type converter in a single page

The same model can be saved as a **project** (`.rvt` extension) or as a **template** (`.rte` extension). Renaming the file extension is not enough: the document holds an internal marker that determines its type, and that is what the application reads when opening it.

Guaita RVT conveRTE locates this marker and flips it. It is a single HTML file that opens in any modern browser; nothing to install.

All processing happens inside your browser. The file is never sent to any server, so you can work with confidential models and offline.

| | |
|---|---|
| 📤 **No server** | The file never leaves your computer; it is processed locally. |
| ✏️ **Minimal change** | Only the type marker is touched — four bytes. |
| ✅ **Verified** | The file is re-read after the change to confirm it. |
| 🔁 **Bidirectional** | Project to template and template to project. |

## 02 · Project and template

### What separates a .rvt from a .rte

Both share the same internal file format (an OLE2/CFBF container). The type difference lives in the **Last Save Path** stored inside the document's `BasicFileInfo` section: it contains the file extension (`.rvt` or `.rte`) and that text is what marks the nature of the document.

| Type | Extension | Use |
|---|---|---|
| **Project** | `.rvt` | The usual working model, with its content and history. |
| **Template** | `.rte` | Starting point for new projects: predefined styles, families and settings. |

> [!NOTE]
> **Why renaming is not enough**
>
> If you only change the extension of the file name in the file explorer, the application still sees the original internal type and may reject it or open it as the wrong type. This tool changes the marker inside.

## 03 · Getting started

### Two ways to load the file

1. **Drag and drop** the `.rvt` or `.rte` file onto the central upload area.
2. Or **click the upload area** ("Drag the file here, or click to select it") to open the system file picker.

Once loaded, the tool reads it instantly and shows the card with the detected type and the proposed conversion.

> [!NOTE]
> **Accepted extensions**
>
> The picker filters for `.rvt` and `.rte`. Make sure the file really is an RVT or RTE document; if it is not, the tool will warn you.

## 04 · The interface

### Where everything is

The window is a single vertical card. The map below shows its layout from top to bottom:

| Area | Content |
|---|---|
| **Header** | "Guaita RVT conveRTE" with the description |
| **Upload area** | Area to drag onto or click. Shows the `.rvt` and `.rte` extensions and reminds you everything is processed locally. |
| **Source** | The loaded file with its badge (PROJECT · RVT or TEMPLATE · RTE). |
| **Arrow and target** | The proposed conversion, with a field to edit the output name and the resulting extension fixed. |
| **Notice** | Yellow note: experimental tool, always verify the result. |
| **Footer** | Convert button · status message once the file is downloaded |

## 05 · How it detects the type

### Read before touching anything

When the file is loaded, the tool opens the internal structure of the document and looks for the extension (`.rvt` or `.rte`) inside the Last Save Path of `BasicFileInfo`. From what it finds, it deduces the type:

- If `.rvt` appears, the file is a **project**.
- If `.rte` appears, the file is a **template**.

The card shows the file **size** and, in technical mode, the exact **offsets** where the marker was found. The card automatically proposes the conversion to the opposite type.

> [!WARNING]
> **When it cannot be determined**
>
> If the file contains no recognisable extension, or contradictory ones, the tool cannot decide the type and tells you so with an error message, without modifying anything.

## 06 · Convert and save

### One click, one new file downloaded

1. **Review the output name.** In the editable field on the target side you can change the base name; the resulting extension (`.rvt` or `.rte`) is fixed by the conversion.
2. **Press the convert button.** The button text states the exact action, for example "Convert to template (.rte) → name.rte".
3. The tool makes the change, **re-reads the file to verify** the marker was updated, and **downloads** the result automatically in the browser.

When it finishes, a green confirmation message appears with the name of the downloaded file and a note that the type was verified after the change.

> [!NOTE]
> **What exactly changes**
>
> Only the extension text inside `BasicFileInfo` is replaced (four bytes), with the same length. The save history, counters and the rest of the model content are untouched and remain identical bit for bit.

## 07 · Limits and guarantees

### Use it wisely

The source file is not modified: you always get a **new downloaded file**, so you keep the original just in case. Even so, you are working with real data: keep a backup and always check the result.

> [!CAUTION]
> **Experimental tool**
>
> The application was conceived for educational purposes. Even though the change is minimal and verified, **you must open the resulting file in the authoring application** to confirm it behaves as expected before using it in production.

## 08 · Troubleshooting

### If something goes wrong

<details>
<summary>"Not a valid OLE2/CFBF file"</summary>

The loaded file does not have the internal structure of an RVT/RTE document. Check that it really is a `.rvt` or `.rte` and that it is not damaged or compressed.
</details>

<details>
<summary>"The type could not be determined"</summary>

The Last Save Path inside `BasicFileInfo` contains no recognisable extension, or contradictory ones. The tool cannot decide the type and touches nothing. Try saving the file again from the source application and retry.
</details>

<details>
<summary>The browser does not download the file</summary>

Some browsers block automatic downloads. Check the downloads bar and the site permissions. If you opened the HTML from a very restricted environment, try a standard desktop browser.
</details>

<details>
<summary>The application does not open the converted file</summary>

Remember this is an experimental tool. Double-check the conversion made sense (a real project to a template, or the reverse) and, if needed, start again from the original. Always verify the result.
</details>

---

**GUAITA RVT conveRTE**
RVT/RTE file type converter · SBS BIM Consulting
