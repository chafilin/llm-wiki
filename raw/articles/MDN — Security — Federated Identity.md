# Federated Identity

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Authentication/Federated_identity

## Overview

**Federated identity** is an architecture where a website delegates authentication to a third party rather than managing credentials directly.

### Key Components

- **Identity Provider (IdP)**: The trusted third party that manages user credentials and authenticates users
- **Relying Party (RP)**: The website that trusts the IdP to make assertions about user identity

### Basic Flow

1. User requests to sign into the RP website
2. RP redirects user to IdP for authentication
3. User authenticates with the IdP
4. IdP returns a token confirming successful authentication
5. RP validates the token and signs the user in

## Benefits

**For Users:**
- Single credential across multiple sites (reduces password reuse risk)
- Easier sign-up process if they already have an IdP account

**For Websites:**
- Don't need to implement and secure authentication
- Reduces liability for handling user credentials

## OpenID Connect (OIDC)

The dominant standard for federated identity on the web, built on OAuth 2.0.

### Recommended Authentication Flow

**Two-Part Process:**

#### 1. Authentication Request
- RP redirects to IdP's authorization endpoint
- Parameters include:
  - `client_id`: Identifies the RP
  - `response_type`: Always `"code"` (authorization code flow)
  - `redirect_uri`: Where IdP sends the authorization code
  - `code_challenge`: Hash of a request-specific secret (PKCE)
  - `scope`: Requested user data access levels

- IdP authenticates the user (password, biometric, OTP, etc.)
- IdP generates an authorization code and redirects to RP's redirect URL

#### 2. Token Request
- RP makes POST request to IdP's token endpoint with authorization code and `code_verifier`
- IdP validates the request and responds with:
  - **Access token**: Grants user access to protected resources
  - **ID token**: Cryptographically signed JWT identifying the user

### Security Features

#### Authorization Code Flow
- Two-step process is more secure than "implicit flow"
- Prevents tokens from being exposed to the front-end

#### PKCE (Proof Key for Code Exchange)
Defends against CSRF and authorization code injection attacks:

1. RP generates unique `code_verifier` for each request
2. RP hashes it to create `code_challenge` in auth request
3. IdP stores code_challenge with authorization code
4. RP includes original `code_verifier` in token request
5. IdP verifies by hashing `code_verifier` and comparing to stored `code_challenge`

## Third-Party Cookies and Federated Identity

Many implementations depend on third-party cookie support.

**Issue:** Browsers are deprecating third-party cookies for privacy reasons.

**Recommendation:** Don't implement federated identity depending on third-party cookies.

## Federated Credential Management (FedCM) API

Browser-native API for federated identity that addresses third-party cookie dependency.

```javascript
const credential = await navigator.credentials.get({
  identity: {
    providers: [
      {
        configURL: "https://idp.example.com/fedcm.json",
        clientId: "example_client_id"
      }
    ]
  }
});
```

## Sign-Out (OIDC)

Two approaches for coordinating sign-out between RP and IdP:

### Front Channel Logout
- Browser mediates communication
- Sender embeds iframe pointing to recipient's logout URL

### Back Channel Logout
- RP and IdP communicate directly, bypassing browser
- IdP makes POST request directly to RP's logout endpoint
- More reliable than front-channel approach

## Strengths and Weaknesses

### Strengths
- Reduces sign-up friction for existing IdP users
- Lower risk of weak passwords
- More secure than password-only authentication

### Weaknesses
- Space dominated by few large providers (user lock-in)
- Still requires fallback authentication method in most cases
- Vulnerable to phishing attacks
- Users must trust the IdP with authentication
