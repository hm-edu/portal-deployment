# Docker Deployment of the PKI Toolkit

This repository provides the required tools for a local docker deployment of the PKI Toolkit provided by the Munich University of Applied Sciences.

## Requirements

- Valid Sectigo Account
- Enabled API in Sectigo Cert-Manager
- Installed Docker 
- OIDC at your IDP or any other OIDC provider

## Configuration

Before building and starting the containers serveral environment variables should be configured. Therefor you should copy the `.env.example` file to `.env` and set the appropriate values.

| Variable                | Description                                                                                          | Example Value                                               |
| ----------------------- | ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| SECTIGO_USER            | Your Sectigo Username                                                                                | youruser                                                    |
| SECTIGO_PASSWORD        | Your Sectigo Password                                                                                | yourpassword                                                |
| SMIME_ORG_ID            | The Organization ID to be used for SMIME Certificates                                                | 1234                                                        |
| SSL_ORG_ID              | The Organization ID to be used for SSL Certificates                                                  | 1234                                                        |
| SSL_TERM                | The requested validity of the SSL certificate.                                                       | 365                                                         |
| SSL_PROFILE             | The requested profile of the SSL certificate                                                         | 15863                                                       |
| SMIME_TERM              | The requested validity of the SMIME certificate.                                                     | 1095                                                        |
| SMIME_STUDENT_TERM      | The requested validity of the SMIME certificate for students.                                        | 365                                                         |
| SMIME_PROFILE           | The requested profile of the SMIME certificate.                                                      | 16307                                                       |
| SMIME_KEYLENGTH         | The requested keylength of the SMIME certificate.                                                    | 3072                                                        |
| SMIME_KEYTYPE           | The requested key type of the SMIME certificate. (Currently only RSA is supported and recommended)   | RSA                                                         |
| JWKS_URI                | The URI to your JSONWebKeySet to validate the OIDC/OAuth2 Authentication                             | `https://your.idp.university.local/idp/profile/oidc/keyset` |
| AUDIENCE                | The used adiennce for OAuth2 (must be the same value as `AUTH_RESOURCE`)                             | `https://api.university.local`                              |
| NEXTAUTH_URL            | The canonical URL of your site                                                                       | `https://pki.example.edu`                                   |
| NEXT_PUBLIC_AUTH_IDP    | The IDP that shal be used for OIDC authentication                                                    | `https://sso.example.edu`                                   |
| NEXT_PUBLIC_EAB_HOST    | The API Backend host for EAB Operations                                                              | `https://eab.api.example.edu`                               |
| NEXT_PUBLIC_PKI_HOST    | The PKI Backend host for EAB Operations                                                              | `https://pki.api.example.edu`                               |
| NEXT_PUBLIC_DOMAIN_HOST | The Domain Backend host for EAB Operations                                                           | `https://domain.api.example.edu`                            |
| NEXT_PUBLIC_SENTRY_DSN  | In case of using sentry the sentry DSN to upload error reports                                       |                                                             |
| AUTH_CLIENT_ID          | The OIDC Client ID                                                                                   | `pki`                                                       |
| AUTH_CLIENT_SECRET      | The OIDC Client Secret                                                                               | `Random String`                                             |
| AUTH_IDP                | The IDP that shal be used for OIDC authentication (Should be the same as during build time)          | `https://sso.example.edu`                                   |
| AUTH_RESOURCE           | The requested OIDC resource to get OAuth2 working.                                                   | `https://api.university.local`                              |
| AUTH_SECRET             | The [Next.JS Auth Secret](https://next-auth.js.org/configuration/options#secret) used to encrypt JWT | `Random String                                              |
| NEXTAUTH_URL            | The canonical URL of your site (Should be the same as during build time)                             | `https://pki.example.edu`                                   |

## Getting Started

After setting all required values you can build the docker containers. 

```
docker compose build
```

Afterwards you should be able to start the deployment

```
docker compose up -d
```