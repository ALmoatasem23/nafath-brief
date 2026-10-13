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

## Cybersecurity

## Data

## Misconception in My Track

## Open Question
