# Implementation Plan - Fix Banner Rendering in README

The banner image generated via `capsule-render` is not displaying correctly on GitHub due to an XML parsing error in the generated SVG. The error is caused by a raw ampersand (`&`) in the `desc` parameter, which breaks the SVG structure.

## Proposed Changes

### 1. README.md

- Modify the `src` attribute of the banner `<img>` tag.
- Replace the ampersand (`&`) in the `desc` parameter (currently encoded as `%26`) with the word `and` or a double-escaped `&amp;`.
  - _Recommendation_: Use `and` for maximum compatibility and to avoid complex encoding issues with GitHub's image proxy.
- Remove trailing whitespaces in the first few lines of the file.
- Ensure there is a blank line between the opening `<div>` and the `<img>` tag to help some Markdown parsers, although strictly not required for all.

## Technical Details

- **File**: `/home/ibernabel/develop/ibernabel/README.md`
- **Current URL snippet**: `...desc=AI%20Solutions%20Architect%20%7C%20n8n%20%26%20LangGraph%20Specialist...`
- **New URL snippet**: `...desc=AI%20Solutions%20Architect%20%7C%20n8n%20and%20LangGraph%20Specialist...`

## Verification Plan

### Automated Tests

- Since this is a documentation fix, no unit tests are required.

### Manual Verification

- Verify the new URL in the browser to ensure the pink XML error box is gone.
- View the image in the browser and confirm the description text is visible and the waving animation works.
- (Implicitly) once pushed to GitHub, the image should render correctly.
