# Phishing Email Analysis and IOC Enrichment

Practical email triage using Thunderbird, CyberChef, VirusTotal and AbuseIPDB. This project documents two training emails and reputation lookups, with evidence limits recorded alongside each verdict.

**Author** Moataz Mostafa Ali Ibrahim  
**Investigation dates** November 15–17, 2026  
**Training source** TryHackMe Phishing Analysis Fundamentals and Threat Intelligence Tools

## Investigation workflow

1. Inspect the rendered message with remote content blocked.
2. Compare From, Reply-To and Return-Path with the claimed brand.
3. Read the receiving server's SPF, DKIM and DMARC results.
4. Decode encoded header values and reconstruct quoted-printable URL line breaks.
5. Look up the domain and full URL without navigating to the suspect link directly.
6. Enrich relevant indicators and record the date, confidence and limitations.
7. Write a verdict supported by the available evidence.

## Case A — ADT-themed message

The display name claimed ADT Security Services. From, Return-Path and Reply-To used ant.anki-tech[.]com. Yahoo recorded SPF, DKIM and DMARC passes for that sending domain, with a DMARC policy of p=none.

VirusTotal showed 0/92 domain detections and 0/91 URL detections. The URL record was an existing report dated September 15, 2026. The final redirect destination and the sender domain's relationship with ADT remained unverified.

**Verdict** Inconclusive. The observed authentication and reputation results were insufficient to establish brand authorization or a safe final destination.

## Case B — Home Depot impersonation

The From display name used a MIME Base64 encoded word. Decoding its payload produced “Thank you! Home Depot”. The actual sender, reply and return addresses used support@teckbe[.]com.

The subject claimed an order had been placed successfully. HTML links pointed to t.teckbe[.]com, and images were hosted on img.teckbe[.]com. SPF, DKIM and DMARC passed for teckbe[.]com.

**Verdict** Phishing through brand impersonation in this training sample. The purchase lure, claimed brand identity and call to action on another domain support this assessment. No user interaction or final redirect was verified.

## IOC enrichment

AbuseIPDB showed 0% current abuse confidence for the sample's originating IP, 103.234.236.83. Four historical reports from one reporter concerned port scans on February 9–10, 2025. No reports appeared within the displayed last-60-days window.

**Assessment** Low current risk in the displayed reputation result. The historical port scans were not linked to the email by the available evidence.

Two separate training file records were also reviewed.

| Record | VirusTotal detections | Assessment |
|---|---:|---|
| XLS, hash prefix b8ef959a9176a | 42/62 | Malicious, with macro/downloader/dropper labels |
| Email3.eml, hash prefix f4d97603256a | 31/59 | Malicious, with Dridex/downloader labels |

The screenshots truncate the hashes. The prefixes cannot serve as full exact-match IOCs. The available evidence does not establish a relationship between these file samples and the two email cases.

## Evidence and reports

- [Email analysis report](reports/Task-13-Phishing-Email-Analysis.pdf)
- [Threat intelligence report](reports/Task-14-Threat-Intelligence-and-IOCs.pdf)

The reports include screenshots of the original headers, VirusTotal and AbuseIPDB findings and room completion. All reputation counts describe the recorded lookup results and may change.

## Learning outcomes

- Distinguish display-name impersonation from sending-domain authentication.
- Read SPF, DKIM and DMARC in the context of the domain they validate.
- Decode MIME Base64 header values and quoted-printable content.
- Treat reputation data as one source of evidence.
- Keep independent samples and uncertain associations explicit.

## Attribution

Prepared from my SOC training work, with AI assistance organizing the documentation. Training email indicators are defanged in this write-up.

