# Getting started

[Back to README](../README.md) · [Feature guide](FEATURE_GUIDE.md)

## Requirements

- A modern browser with JavaScript enabled.
- Git to clone the repository, or a downloaded/extracted repository ZIP.
- Python 3 for the optional local HTTP server below. Python is not an application dependency.

No Node.js installation, package manager, build step, database, `.env` file, or credentials are needed.

## Run locally

```bash
git clone https://github.com/9MidhunPM/jobportal.git
cd jobportal
python3 -m http.server 8000 --bind 127.0.0.1
```

On Windows, `py -3 -m http.server 8000 --bind 127.0.0.1` is an alternative. Run the command in the directory containing the HTML files. This binds the preview server to your own computer only; it is not a production hosting configuration. Stop it with `Ctrl+C`.

Open these URLs directly:

| Screen | Local URL |
| --- | --- |
| Job seeker dashboard | http://127.0.0.1:8000/jobseekerv2.html |
| Employer dashboard | http://127.0.0.1:8000/employerv2.html |
| Job details, example 1 | http://127.0.0.1:8000/jobdetailsv2.html?id=1 |
| Login/sign-up UI | http://127.0.0.1:8000/indexv2.html |
| Standalone search | http://127.0.0.1:8000/SearchJob.html |
| Static detail layout | http://127.0.0.1:8000/job%20details.html |

There is no `index.html`: opening just the server root normally shows a directory listing. The existing controls do not connect every page. In particular, login does not redirect to either dashboard; open the dashboard URL yourself.

You can also open the HTML files directly in a browser for a basic preview. A local server is recommended for predictable URLs. Preserve filename capitalization and encode the space in `job details.html` as `%20` in a URL.

## Network and data

All styles and scripts are inline. The only remote assets referenced by the application are sample company logos from `https://placehold.co` in `jobdetailsv2.html`. Without internet access, those logos may be absent; their error handler hides failed images. This does not require an API key.

All jobs, profiles, saved jobs, and application history are hardcoded samples or current-page memory. There are no API requests, server-side auth, cookies for login, or local-storage persistence in the application code. The local HTTP server only serves files.

Use made-up form inputs, not real passwords, resumes, or personal information. This prototype is not suitable for accepting real applications.

## Troubleshooting

| Symptom | Explanation / action |
| --- | --- |
| `python3` is not found | Install Python 3 or use the platform's Python 3 command (`py -3` on Windows). |
| Port 8000 is occupied | Use `8001` in the server command and in each browser URL. |
| Page returns 404 | Check the server's working directory and exact filename. `SearchJob.html` has capital letters; the static detail filename contains a space. |
| Clicking a job opens a 404 or does nothing | Several existing links are placeholders or target missing `job.html` / `jobseeker.html`. Open the documented page URLs directly. |
| A saved or posted job disappears | Reloading resets page-local sample data; nothing is saved to a database. |
| A posting does not appear on the job seeker page | The two pages use independent arrays, with no shared store or API. |
| Login does not open a dashboard | Login and sign-up only display alerts. No account is created or authenticated. |
| Job seeker search clears as you type | Its handler rebuilds the input on each change. Paste a complete query for a demo, or use the standalone search page for continuous typing. |
| Edit Profile fails | Its `toggleModal()` function is not implemented in the job seeker page. |
| Details display “Job not found” | Only IDs 1–4 exist in `jobdetailsv2.html`. Missing `id` defaults to 1. |

For a source-grounded walkthrough and development notes, continue to the [Feature guide](FEATURE_GUIDE.md).
