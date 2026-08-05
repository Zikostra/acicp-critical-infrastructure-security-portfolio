# Repository Security Policy

## Prohibited Content

The following must never be committed:

- private cryptographic keys;
- passwords and password hashes;
- API tokens and access tokens;
- SSH private keys;
- cloud-init credentials;
- VM disk images;
- unredacted confidential information;
- full private authentication logs;
- files belonging to systems outside the authorised laboratory.

## Permitted Evidence

The following may be committed after review:

- Markdown and text reports;
- screenshots without exposed credentials;
- public certificates;
- certificate signing requests;
- non-secret certificate extension files;
- controlled laboratory PCAP files;
- sanitised log excerpts;
- Nmap output for the assigned VM only;
- SHA-256 manifests;
- final PDF and ZIP submissions.

## Review Requirement

Every file must be reviewed before staging and committing.
