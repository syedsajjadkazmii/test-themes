Alpha Test Theme (Legacy LMS)

This theme is  following OpenedX theming conventions.

## What it changes
- Primary brand color (#2458E6) and font family (Roboto) via SCSS
- Button styles via SCSS
- Header background color via SCSS
- Custom logo placement (replaces default branding_api.get_logo_url with custom-logo.png)
- One additional navigation item ("About") in authenticated navbar

## Structure

### SCSS (all under lms/static/sass/partials/lms/theme/)
- `_variables.scss`: Brand tokens (primary color, font family, header colors)
- `_buttons.scss`: Custom button styles using brand colors
- `_header.scss`: Header background, nav link styles, logo sizing
- `_extras.scss`: imports buttons and header partials

### Mako Templates (all under lms/templates/)
- `header.html`: Standard LMS header structure (includes navbar-logo-header and navbar-authenticated)
- `header/navbar-logo-header.html`: **Logo override** - uses `custom-logo.png` instead of default
- `header/navbar-authenticated.html`: **Navigation override** - adds "About" link between Programs and Discover New

### Static Assets
- `lms/static/images/custom-logo.png`: test custom logo 

## How to Enable

1. **Place your logo**:

2. **Configure LMS** to use this theme:
   ```
   THEME_NAME=alpha-test-theme
   ```
   Ensure `THEME_DIRS` includes the path to edx-themes repo.

3. **Rebuild assets**:
   ```bash
   ./manage.py lms collectstatic --noinput
   ./manage.py lms compile_sass lms --themes alpha-test-theme
   ./manage.py lms compress
   ```

4. **Restart LMS** and verify:
   - Header uses brand color background
   - Custom logo appears
   - "About" link shows in navbar (authenticated users)
   - Buttons use brand color styles

## Notes
- No inline styles; all styling is in SCSS
- Override scope is minimal and upgrade-safe
- Preserves all default LMS header functionality (hamburger menu, user dropdown, language selector, etc.)
- Variables are auto-loaded by LMS theme discovery; `_extras.scss` only imports new component partials
