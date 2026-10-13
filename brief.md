Version: NAFATH-V1
Track: AI

## Overview

The authority wants one login that citizens can use from a mobile app or a website to reach many government services.
All six fields meet at that login.
Software picks the protocol, and OpenID Connect fits best for confirming who the user is.
Cybersecurity decides how users prove it, and passkeys are far safer than SMS codes.
Mobile sets what the Android app may access on the phone.
Networking protects the connection, including the DNS lookup that finds the login site.
Data covers the legal duties for the personal data the service stores.
AI adds a model that watches logins and flags suspicious ones.
If one part is weak, the whole service is weak.

## Software

OAuth 2.0 was built for delegated access: it lets an app get an access token to call an API for the user.
It has no standard way to tell the app who the user is.
OpenID Connect adds that identity layer on top of OAuth 2.0 and is designed for login.
Its ID Token is a signed JWT with claims about how the user authenticated.
So the service should use OpenID Connect.

Resource: OpenID Connect Core 1.0 incorporating errata set 2 - https://openid.net/specs/openid-connect-core-1_0.html

## AI

Using the NIST AI Risk Management Framework, the authority should govern, map, measure and manage the model's risks before launch.
The main ones are false positives that lock real citizens out, false negatives that let attackers in, unfair flagging of groups like citizens abroad, privacy of login and location data, attackers fooling or poisoning the model, and blocks nobody can explain.
Monitoring has to continue after launch.

Resource: Artificial Intelligence Risk Management Framework (AI RMF 1.0), NIST AI 100-1 - https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf

## Mobile

On Android, low-risk install-time permissions are granted automatically.
Anything that touches private data or sensitive hardware, like location or the camera, needs a runtime permission that the user can refuse.
The login app should only ask when a feature needs it, for example the camera when scanning an ID card, and explain why.
It must check before every use and keep working if the user says no.

Resource: Permissions on Android (Android Developers) - https://developer.android.com/guide/topics/permissions/overview

## Networking

DNS over HTTPS (DoH) sends a device's DNS lookups, like the one that finds the login site, inside HTTPS.
The traffic is encrypted and the resolver is authenticated, so attackers on the network cannot easily spy on lookups or divert them to a rogue server.
But the DoH resolver itself still sees every lookup, DoH does not replace DNSSEC, and the login still needs its own TLS.

Resource: RFC 8484: DNS Queries over HTTPS (DoH) - https://www.rfc-editor.org/rfc/rfc8484.html

## Cybersecurity

NIST calls a method phishing-resistant when a fake site cannot get the user's secrets, even if the user is fooled.
This works through verifier name binding, as with WebAuthn passkeys, or channel binding, as with smart cards using client-authenticated TLS.
Passwords, SMS codes, authenticator app codes and push approvals do not qualify, because a fake site can capture or relay them.
At AAL2, services must offer at least one phishing-resistant option.

Resource: NIST SP 800-63B-4, Digital Identity Guidelines: Authentication and Authenticator Management - https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63B-4.pdf

## Data

Under Oman's Personal Data Protection Law (Royal Decree 6/2022), a controller needs explicit consent and must inform citizens in writing first, protect the data, keep records, appoint a data protection officer, report breaches to the ministry and affected people, follow rules for transfers abroad, and get a permit for biometric data.
One surprise: Article 3 excludes processing by state administrative units within their legal powers, so the authority should confirm which duties apply.

Resource: Royal Decree 6/2022 Issuing the Personal Data Protection Law (English translation, Decree.om) - https://decree.om/2022/rd20220006/

## Misconception in My Track

Many people think that if the suspicious-login model scores high accuracy in testing, it is ready to go live.
That is not true.
The NIST AI RMF lists seven characteristics of trustworthy AI: valid and reliable, safe, secure and resilient, accountable and transparent, explainable and interpretable, privacy-enhanced, and fair with harmful bias managed.
They have to be balanced for the context of use.
A model that catches attackers but cannot explain why it blocked a citizen, or that keeps flagging people who log in from abroad, is still not ready.
Section 3, "AI Risks and Trustworthiness", says accurate but opaque systems are undesirable.

## Open Question

How many false positives can the authority accept, and should a flagged login be blocked or just trigger a second check, like a passkey prompt?
I would test both in a small pilot, because this decides how many real citizens get locked out.
