# Job Portal

A browser-based job portal prototype built with **HTML, CSS, and vanilla JavaScript**. It explores job search, job-detail layouts, a job seeker dashboard, and an employer dashboard without a build tool or framework.

> **Project status:** frontend prototype with sample data. Authentication, applications, resume search, and several navigation controls are placeholders. There is no backend, database, or persistent storage in this repository. Use dummy data when trying it out.

## Quick start

With Git and Python 3 installed:

```bash
git clone https://github.com/9MidhunPM/jobportal.git
cd jobportal
python3 -m http.server 8000 --bind 127.0.0.1
```

Open **http://127.0.0.1:8000/jobseekerv2.html** for the job seeker dashboard. On Windows, use `py -3` instead of `python3` if needed. Stop the server with `Ctrl+C`.

There are no packages to install, API keys to supply, or environment variables to configure. The pages are separate prototypes, not a connected login-to-dashboard flow. Open them directly using the filenames below; there is no `index.html` default landing page.

## Explore the prototype

| Page | What it demonstrates |
| --- | --- |
| [`jobseekerv2.html`](jobseekerv2.html) | Sample job cards, title/company/location filtering, in-memory saved jobs, and sample application history. |
| [`employerv2.html`](employerv2.html) | Existing sample postings and a modal that adds a posting to the current page's in-memory list. |
| [`jobdetailsv2.html`](jobdetailsv2.html) | Detailed sample jobs selected with `?id=1` through `?id=4`; defaults to job 1. |
| [`indexv2.html`](indexv2.html) | Login/sign-up form tabs; submit buttons only display alerts. |
| [`SearchJob.html`](SearchJob.html) | A standalone list with title, location, and experience filters. |
| [`job details.html`](job%20details.html) | An alternative static job-detail layout. |

GitHub links above open the source files, not a hosted demo. To preview a page, append its filename to the local server address.

## What to expect

- Saving or posting a job changes only the current page's JavaScript data. Reloading resets it; data is not shared between pages or tabs.
- Some links point to missing files or `#`. Job applications, editing profiles/postings, and viewing applicants are not implemented.
- Each page owns its sample data; IDs and job descriptions are not consistent across all pages.
- CSS and JavaScript are inline. No external script or stylesheet CDN is required. The detailed job page requests optional placeholder logos from `placehold.co`; those images need internet access and hide on load failure.

See [Getting started](docs/GETTING_STARTED.md) for page URLs and troubleshooting, and the [Feature guide](docs/FEATURE_GUIDE.md) for a demo walkthrough, code map, and known limitations.
