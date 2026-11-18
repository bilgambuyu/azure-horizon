# Azure Horizon | Agency Website

Single-page, multi-view website for **Azure Horizon**, a communications and marketing agency (strategy & campaigns, advocacy, PR, resource mobilization, graphic design, video editing, motion design, marketing, web development, multimedia production).

## Structure
- `index.html`: self-contained site (HTML, CSS, JS). Views are routed by URL hash: `#home`, `#about`, `#services`, `#work`, `#insights`, `#contact`, plus one page per service (e.g. `#graphic-design`).

## Images
The site ships with a cohesive local editorial image set in `img/`. Image assignments are centralized in the `IMG` object near the top of the script; update any `src` path there to customize a slot.

## Before launch
- Replace placeholder contact details (email, phone, city).
- Replace Work page sample projects with real case studies.
- Connect the contact form to a form service or backend.

## Run locally
Open `index.html` in a browser, or serve the folder: `python3 -m http.server`.
