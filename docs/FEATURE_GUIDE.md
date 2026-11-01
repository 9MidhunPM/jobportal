# Feature guide

[Back to README](../README.md) · [Local setup](GETTING_STARTED.md)

This guide describes the current frontend prototype, not a complete hiring service. Start the local server using the setup guide, then open each page directly. There is no required login and no working end-to-end application workflow.

## Short demo walkthrough

### 1. Search and save jobs

Open `jobseekerv2.html`.

1. Show the sample profile (John Smith) and five job cards.
2. Paste `Remote` into the search field to filter by location. Filtering also matches job title or company, ignoring case.
3. Explain that the input is recreated after each change, so its text and focus are lost. Click **Job Search** to restore the full list.
4. Click **Save** on Senior React Developer, dismiss the alert, then open **Saved Jobs**. The saved item appears alongside the initially saved Node.js Backend Engineer.
5. Open **Application History** to show the preloaded Product Manager entry marked **Under Review**. It is sample data, not a submitted application.
6. Reload to demonstrate that added saved jobs disappear.

**Do not present as functional:** View Details is a `#` link, and Edit Profile calls a missing `toggleModal()` handler. Navigation and saving also rely on an implicit global `event`, which can behave differently between browsers.

### 2. Add an employer posting

Open `employerv2.html`.

1. Show the two preloaded postings.
2. Click **Post a New Job**.
3. Fill Job Title, Company Name, Experience Needed, Skills Required, Job Type, Job Location, and Job Description with dummy values.
4. For example, use `Demo Frontend Developer`, `Demo Company`, `1`, `HTML, CSS`, `Remote`, `Other`, custom location `Kochi`, and `Build a demo interface`.
5. Click **Submit Job Posting** and dismiss the success alert. The modal closes and the new card appears first.
6. Reload: the page returns to its two original postings.

The modal can also be closed with its **×** control or by clicking the overlay. Selecting **Other** reveals the custom location input; leaving that input empty records `Not Specified`.

**Do not present as functional:** Search Resumes only alerts the entered filters; it does not search candidates. View Applicants and Edit have no handlers. The new posting is not sent anywhere and does not appear on other pages.

### 3. Browse detailed sample jobs

Open `jobdetailsv2.html?id=1` to show the job description, responsibilities, qualifications, salary, and location.

- Change the URL to `?id=2`, `?id=3`, or `?id=4` to inspect the other records.
- Open the page without a query string to see its default, ID 1.
- Try `?id=99` to demonstrate the “Job not found” state.
- The normal **Back to Search Results** link uses browser history; it does not select a specific dashboard. The not-found state's back link points to missing `jobseeker.html`.

**Apply Now** is a `#` link with no submission behavior. Placeholder company images are loaded from `placehold.co`. The detail records are separate from dashboard data: ID 3 is Digital Marketing Manager here but UI/UX Designer in the dashboard; ID 4 also differs, and dashboard ID 5 has no corresponding detail record.

### 4. Show the other layouts

- **`indexv2.html`:** switch between Login and Sign Up, including the Job Seeker / Employer selector. Both submit buttons only display alerts; neither validates credentials nor creates a session or account.
- **`SearchJob.html`:** type `Developer`, click Filters, then choose Kochi and 1-3 Years to narrow the list to Game Developer. Clear the search and reset selectors to show all five jobs. Its job links target missing `job.html`, so open the detail layouts manually instead.
- **`job details.html`:** a static Frontend Developer description with visual image placeholders. Apply Now has no handler, and Similar Jobs links also target missing `job.html`.

## Code and data map

Each HTML file owns its markup, styles, and (where present) JavaScript. There are no shared modules or backend services.

| File | Main implementation points |
| --- | --- |
| `indexv2.html` | `showForm()` switches tabs; `login()` and `signup()` are alert-only stubs. |
| `SearchJob.html` | `jobs` contains five samples; `filterJobs()` combines title, location, and experience filters; `renderJobs()` updates the list. |
| `jobseekerv2.html` | `allJobs`, `savedJobs`, and `applications` hold independent page data; render functions build views; `saveJob()` prevents duplicate saves. |
| `employerv2.html` | `postedJobs` holds sample/current-page postings; `toggleModal()` handles visibility; the form's submit listener prepends a posting and rerenders. |
| `jobdetailsv2.html` | `jobsData` maps IDs 1–4 to sample records; the DOM-ready handler reads the `id` query parameter and renders a detail or not-found view. |
| `job details.html` | Static markup and styles; no application script. |

The flow is **load HTML → initialize local sample data → render DOM → update current-page memory**. Reloading starts over. No account, job, resume, or application API contract exists to document yet.

## Known limitations and development priorities

These are follow-up ideas, not implemented features:

1. **Connect navigation and unify data.** Replace missing-file and `#` targets, reconcile IDs, and use a shared source of truth before claiming a complete search-to-details flow.
2. **Complete interactions.** Implement profile editing, applicant views, posting edits, and real application submission, with clear empty/error states.
3. **Make search and events robust.** Update only the results instead of rebuilding the search input, and pass event objects explicitly to click handlers.
4. **Add real authentication and persistence.** Define backend APIs, authorization rules, validation, and storage before accepting real users or private data. No backend or cloud deployment is included here.
5. **Harden rendering.** Form values are inserted through `innerHTML` without escaping. Use safe DOM/text APIs or appropriate sanitization before handling untrusted input; do not expose this prototype as a production service.
6. **Test accessibility and responsive layouts.** Check keyboard use, focus handling, modal behavior, small screens, and different browsers. There is no automated test suite in the repository.

## Manual smoke-check checklist

After a change, use dummy data and verify:

- [ ] All six HTML pages load through the local server.
- [ ] Login/sign-up tabs switch, with alert-only behavior clearly understood.
- [ ] Standalone search combines title, location, and experience filters; an unmatched query displays “No jobs found.”
- [ ] Employer modal opens/closes; a valid posting appears and resets after reload.
- [ ] Job seeker views switch; saving a job works once and duplicate saving shows an alert.
- [ ] Detail IDs 1–4 render; no ID defaults to 1; ID 99 shows not found.
- [ ] Missing external logos do not prevent job details from rendering.

This checklist is a suggested manual verification procedure, not a claim that all browsers or production workflows have been tested. Existing placeholder controls and broken links are documented above and are not repaired by these documentation files.
