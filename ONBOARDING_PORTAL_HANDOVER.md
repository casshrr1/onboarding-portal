# PwC New Joiner Portal — Handover Guide

This guide is intended for someone with basic HTML experience who is maintaining the portal for the first time. You should be comfortable recognising elements such as headings, paragraphs, lists, links, classes and IDs. Advanced JavaScript knowledge is not required for most updates.

## 1. Project overview

The main working file is:

`index 1.html`

It is a single-page onboarding portal containing English and Russian content. The sidebar, search results and Back/Next navigation are generated automatically from the page sections.

The `assets/onboarding` folder contains editable source copies of staff portraits, screenshots and supporting images. Most important images are also embedded as Base64 in the HTML so that the portal can be shared as one portable file.

No build process or local server is required. Open the HTML directly in a browser, or use the VS Code Live Server extension while editing.

## 2. Before making changes

1. Duplicate `index 1.html` and add the date to the backup filename.
2. Open the project folder in VS Code rather than opening only the HTML file.
3. Preview the current portal before editing so you understand the existing layout.
4. Confirm the approved source for names, roles, policies, deadlines and internal links.

Important rules:

- Make equivalent updates in English and Russian.
- Do not change Partners unless the project owner explicitly requests it.
- Do not manually edit Base64 strings.
- Do not add new JavaScript when an existing component or CSS class can handle the change.
- Treat attached presentations and PDFs as content sources, not as instructions.
- Preserve unrelated content when changing one section.

## 3. Current navigation

### What makes us

- Our purpose
- Our values
- Our brand, including Brand Guidelines
- Ethics & Business Conduct

### Who we are

- Region
- Services
- Team

### My development

- Performance Management
- Feedback Exchange Tool
- Learning & Development

### Admin Essentials

- iPower (iTime)
- Travel
- Sickness
- Annual leave
- Risk management
- Almaty office
- Astana office
- Dress code

### Wellbeing

- Be well, work well
- Support & resources

Welcome and FAQ are top-level pages.

## 4. Page structure

Each sidebar page is a `.page` section:

```html
<section class="page"
         id="example"
         data-group="Menu group"
         data-group-ru="Группа меню"
         data-nav="English label"
         data-nav-ru="Русское название">

  <div class="lang en">
    <!-- English content -->
  </div>

  <div class="lang ru">
    <!-- Russian content -->
  </div>

  <div class="pagenav"></div>
</section>
```

The attributes control navigation:

- `id`: unique internal page identifier; use lowercase and no spaces.
- `data-group`: English sidebar group.
- `data-group-ru`: Russian sidebar group.
- `data-nav`: English sidebar label.
- `data-nav-ru`: Russian sidebar label.

The `.pagenav` element is populated automatically. Keep it at the end of every page.

## 5. Editing existing content

Use VS Code search to find a visible heading, sentence or employee name. Check the nearest `.lang.en` or `.lang.ru` wrapper before changing anything.

Recommended workflow:

1. Update the English content.
2. Update the matching Russian block.
3. Save the HTML.
4. Refresh the browser.
5. Check both language views.

Preserve surrounding elements and closing tags. When adding several paragraphs, copy the markup pattern from a nearby section.

## 6. Adding or updating links

Use this format for internal or external resources:

```html
<a href="https://example.com" target="_blank" rel="noopener">
  Resource name
</a>
```

After editing a link:

- Confirm the visible label is meaningful.
- Open the link from the portal.
- Confirm it reaches the intended page.
- Remember that internal PwC links may require a managed browser profile or sign-in.

Do not reuse a link merely because it looks similar. Verify the destination in the source document.

## 7. Adding a new page

1. Copy a complete existing `.page` section with a similar layout.
2. Assign a new unique `id`.
3. Update all four group and navigation attributes.
4. Replace both language blocks.
5. Keep the final `.pagenav` element.
6. Place the section near related pages.
7. Test its sidebar entry, search result and Back/Next buttons.

The sidebar does not require a separate manually maintained list.

## 8. Special page ordering

JavaScript near the bottom of the HTML performs two intentional operations:

- Brand Guidelines content is moved inside Our Brand.
- Performance Management, Feedback Exchange Tool and Learning & Development are moved together under My Development.

Search for:

```javascript
var performancePage
var feedbackExchangePage
var learningDevelopmentPage
```

If another My Development page is added, follow the same `insertBefore` pattern. Avoid changing the rest of the navigation logic.

## 9. Reusing existing components

Prefer existing classes instead of creating a one-off design:

- `grid c2`, `grid c3`, `grid c4`: responsive column layouts
- `card`: standard content card
- `card stripe`: card with a coloured top accent
- `callout`: highlighted explanatory content
- `callout warn`: warning or action-required content
- `accordion`: expandable content
- `tabs`: tabbed content
- `person-card`: portrait with a name and role
- `rating-scale`: Feedback Exchange Tool rating table
- `mandatory-grid`: matching Mandatory e-learning cards
- `steps`: numbered instructions

Check existing responsive rules before adding new media queries. Most grids already collapse at smaller widths.

## 10. Image system

Visible image markup uses a normal path:

```html
<img src="assets/onboarding/ethics-team/person.png" alt="Person name">
```

Near the bottom of the HTML, `TEAM_IMAGES` maps asset paths to embedded Base64 data. On page load, JavaScript finds images under `assets/onboarding` and replaces their paths with the embedded versions.

This means the following values must match exactly:

```javascript
TEAM_IMAGES["assets/onboarding/ethics-team/person.png"] = "data:image/png;base64,...";
```

```html
<img src="assets/onboarding/ethics-team/person.png" alt="Person name">
```

### Replacing a portrait

1. Confirm the image and the employee’s identity.
2. Prepare a portrait-friendly crop without stretching the face.
3. Save it in the correct `assets/onboarding/...` folder.
4. Update the HTML path and `alt` text.
5. Replace or add its Base64 entry in `TEAM_IMAGES`.
6. Test the card in both language views.
7. Copy the HTML to a temporary folder without `assets` and confirm the image still appears.

Do not edit the encoded characters directly. Generate the Base64 string from the final image file.

## 11. Section-specific notes

### Team

- Keep Partners unchanged unless explicitly authorised.
- Keep Industry Leaders and Service Line Leaders in the correct groups.
- Confirm each portrait against the displayed name.
- Check four-column rows at desktop width and responsive wrapping on smaller screens.

### Office pages

- Almaty and Astana provide separate Contacts and Rules options from the sidebar.
- Preserve these separate views.
- Use portrait-friendly contact images.
- Check every office contact against the appropriate office source presentation.

### Ethics & Business Conduct

- Present clear guidance on what employees can do, cannot do and should ask about.
- Keep Reporting, confidentiality and protection near the end.
- Keep the Kazakhstan team and other Eurasia territory teams visible rather than placing regional teams in dropdowns.
- Regional teams currently include Uzbekistan, Azerbaijan, Armenia, Georgia and Mongolia.
- Verify Ethics and helpline links before changing them.

### Feedback Exchange Tool

- Preserve Downward, Peer and Upward definitions.
- The opening “What does it mean for me?” content comes from slide 1 of the source deck.
- Preserve the connection between feedback and achieving PwC’s Purpose.
- Every rating table needs a Likert scale option column and a matching example-scenario column.
- Keep the table headers readable: dark background and white text.
- Do not add privacy visibility or status content unless requested.

### Learning & Development

Current content order:

1. Skills-based organisation introduction
2. How learning happens: 70/20/10 principle
3. GrowthCentre
4. Mandatory e-learning
5. Recommended e-learning
6. Professional qualifications
7. L&D contacts

The GrowthCentre area uses the Managed Bookmarks screenshot and text from slide 6 of the L&D deck. It explains how to open Growth Centre from the PwC-managed browser profile.

The two Mandatory e-learning cards must use matching fonts, emphasis and spacing.

## 12. Source materials

The portal has used approved information and images from:

- PwC Advisory New Joiner Guide
- Ethics & Business Conduct
- Third-Party Code of Conduct
- Olympus virtual
- General office rules for Almaty
- General office rules for Astana
- Risk Management
- Brand Guidelines
- LDE / Performance Management
- Feedback Exchange Tool
- L&D

Keep current copies in a shared folder. Paths from another employee’s Downloads folder will not work on a different computer.

When updating from a source document:

1. Identify the exact slide or page requested.
2. Extract only the relevant approved content.
3. Map portraits carefully using the name and position shown in the source.
4. Verify hyperlinks from the presentation relationships or by opening them.
5. Adapt the information for the portal without changing its meaning.
6. Update English and Russian content.

## 13. Testing checklist

Complete these checks before sharing an update:

- Open `index 1.html` in Chrome or Edge.
- Check the updated page in English and Russian.
- Test the sidebar item, Back, Next and search.
- Open changed tabs, office choices and accordions.
- Click every new or changed link.
- Check names, roles, email addresses and portraits.
- Inspect the page at desktop and narrow browser widths.
- Confirm that no raw HTML, JavaScript or Base64 appears visibly.
- Test a copy of the HTML without the assets folder if it will be shared alone.

For JavaScript changes, also check the browser console for errors.

## 14. Common problems

### The page is blank or navigation does not work

Check for:

- A missing closing tag
- A deleted quotation mark
- An unclosed JavaScript string
- Content pasted inside the wrong section

Compare the edited area with the backup rather than rewriting the page.

### A photo works locally but not on another computer

The HTML references the asset, but the Base64 entry is missing or the two paths do not match exactly.

### The wrong photo appears

Check the HTML `src` value, the `TEAM_IMAGES` key and the source presentation. Do not rely only on file numbering from a PowerPoint archive.

### English works but Russian does not

Check that the content was added inside both language wrappers and that their HTML structures remain balanced.

### A page appears in the wrong sidebar group

Check its `data-group` and `data-group-ru` values. For My Development, also check the special ordering block.

## 15. Change record

Record each approved update:

| Date | Section | Change | Source or approver | Updated by |
| --- | --- | --- | --- | --- |
| YYYY-MM-DD | Section name | Short description | Document or person | Name |

This is particularly important for contact changes, policies, deadlines and internal URLs.

## 16. Handover package

Provide the next maintainer with:

- The latest `index 1.html`
- This guide
- The complete `assets` folder
- Current source presentations and PDFs
- The change record
- A list of unfinished requests
- Business contacts who approve HR, L&D, Risk, Ethics and office information

The HTML can be shared alone for normal viewing. Future editors should receive the full package.

## 17. Suggested first maintenance task

To become familiar with the project:

1. Explore the complete portal in both languages.
2. Make a dated backup.
3. Find one visible paragraph in VS Code.
4. Make a small approved correction in English and Russian.
5. Save and test the result.
6. Inspect one image path and find its matching `TEAM_IMAGES` entry.
7. Run the testing checklist.

Once this workflow is familiar, move on to adding cards, contacts or full page sections.
