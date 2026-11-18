# Azure Horizon | Agency Website

Single-page, multi-view website for **Azure Horizon**, a communications and marketing agency (strategy & campaigns, advocacy, PR, resource mobilization, graphic design, video editing, motion design, marketing, web development, multimedia production).

## Structure
- `index.html`: self-contained site (HTML, CSS, JS). Views are routed by URL hash: `#home`, `#about`, `#services`, `#portfolio` (plus one page per project, e.g. `#brand-identity`), `#insights`, `#contact`, plus one page per service (e.g. `#graphic-design`).

## Images
The site ships with a cohesive local editorial image set in `img/`. Image assignments are centralized in the `IMG` object near the top of the script; update any `src` path there to customize a slot.

## Before launch
- Replace placeholder contact details (email, phone, city).
- Replace Portfolio sample projects (the `PROJECTS` array) with real case studies; each project gets its own page at `#project-id`.
- Connect the contact form to a form service or backend.

## Run locally
Open `index.html` in a browser, or serve the folder: `python3 -m http.server`.

## AI assistant
A chat assistant (bottom-right "Ask Azure AI" button) answers questions about services, pricing and process, and lets visitors **book a consultation**, **request a service** or **contact the team** through forms inside the chat.

It picks the first AI backend that is available:
1. **claude.ai artifact**: when the site is viewed as a claude.ai artifact, it uses Claude through the page's `sample` capability. Nothing to configure.
2. **Your own endpoint**: set `AI_CONFIG.chatEndpoint` in `index.html` to the URL of the Cloudflare Worker in `api/`.
3. **Quick answers**: with no AI available it answers from the site's FAQ and services and still shows the forms.

### Deploy the backend (Cloudflare Worker)
```bash
cd api
npm i -g wrangler
wrangler login
wrangler secret put ANTHROPIC_API_KEY      # your Anthropic API key, never put it in index.html
# optional, to receive bookings/requests:
wrangler secret put LEAD_WEBHOOK_URL       # e.g. a Make, Zapier, Formspree or Slack webhook
# or email via Resend:
wrangler secret put RESEND_API_KEY
wrangler secret put LEAD_TO_EMAIL
wrangler deploy
```
Then in `index.html` set:
```js
const AI_CONFIG = {
  chatEndpoint: "https://azure-horizon-ai.<your-subdomain>.workers.dev/chat",
  leadEndpoint: "https://azure-horizon-ai.<your-subdomain>.workers.dev/lead",
  ...
};
```
Set `ALLOWED_ORIGIN` in `api/wrangler.toml` to your site's address so only your site can use the worker.

Until `leadEndpoint` is set, submitted forms are **not sent**: the chat tells the visitor so and offers a "Copy details" button with your email address.
