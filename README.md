# DP Site

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**A comprehensive ecosystem of deployable services for dynamic website development**

DP Site is a collection of robust, open-source services and components that work together to provide essential functionality for dynamic websites. Instead of relying on third-party services, DP Site offers self-hosted solutions for user management, logging, metrics, email dispatching, and more.

## 🎯 Project Goals

- **Self-hosted**: Run your own services without depending on external providers
- **Open Source**: All components are open-source and freely available
- **Secure**: Opinionated security choices with first-party cookie architecture
- **Modular**: Use only the services you need
- **Technology Focused**: Built with Rust and JavaScript for reliability and modern development

## 🏗️ Architecture Overview

DP Site uses an opinionated domain structure designed for security and modularity:

```
mysite.com                     # Your main website
account.mysite.com             # User authentication and management interface for all site users
monitor.mysite.com             # Monitoring dashboard for site admins
mailer.mysite.com              # Email management interface for site admins

auth.api.mysite.com            # Authentication API
logs.api.mysite.com            # Logging API
metrics.api.mysite.com         # Metrics API
mailer.api.mysite.com          # Email API
```

### Security Architecture

The domain structure enables secure cookie sharing using first-party cookies:

- **API cookies**: Set for `.api.mysite.com` domain
- **Automatic sharing**: Available to all API subdomains without extra code
- **Isolation**: Cookies are NOT sent to non-API subdomains (e.g., `assets.mysite.com`)
- **Browser-native**: Leverages natural browser cookie behavior

## 📋 Requirements

To use DP Site, you need:

1. **A domain** (e.g., `mysite.com`)
2. **API subdomain structure** (e.g., `*.api.mysite.com`)
3. **Development stack**: Rust or JavaScript for your main site

## 🚀 Services

### Authentication Services

#### DpSiteAuthApi
- **Technology**: Rust + SQLite + GraphQL
- **Domain**: `auth.api.mysite.com` (customizable prefix)
- **Features**:
  - User sign-up and log-in
  - Password recovery
  - Email management
  - Data redaction (GDPR compliance)
  - Session management and revocation
  - OAuth integration
  - One-Time Password (OTP) support

#### DpSiteAuthWeb
- **Technology**: Vue.js
- **Domain**: `account.mysite.com` (customizable prefix)
- **Features**:
  - User sign-up and login interface
  - User profile management
  - Admin user management
  - Password recovery flows
  - OAuth authentication flows
  - OTP configuration

### Monitoring Services

#### DpSiteLogsApi
- **Technology**: Rust + SQLite + GraphQL
- **Domain**: `logs.api.mysite.com` (customizable prefix)
- **Features**:
  - Log ingestion and storage
  - Authentication via Auth layer
  - Searchable log data

#### DpSiteMetricsApi
- **Technology**: Rust + SQLite + GraphQL
- **Domain**: `metrics.api.mysite.com` (customizable prefix)
- **Features**:
  - Metrics ingestion and storage
  - Data parsing and analysis
  - Authentication via Auth layer

#### DpSiteMonitorWeb
- **Technology**: Vue.js
- **Domain**: `monitor.mysite.com` (customizable prefix)
- **Features**:
  - Log search and filtering
  - Metrics dashboards
  - Admin reporting tools
  - Connects to Logs and Metrics APIs

### Email Services

#### DpSiteMailerApi
- **Technology**: Rust + SQLite + GraphQL
- **Domain**: `mailer.api.mysite.com` (customizable prefix)
- **Features**:
  - Email payload ingestion
  - Email storage and queuing
  - Email dispatching
  - Authentication via Auth layer

#### DpSiteMailerWeb
- **Technology**: Vue.js
- **Domain**: `mailer.mysite.com` (customizable prefix)
- **Features**:
  - Email delivery monitoring
  - Email management interface
  - Connects to Mailer API

## 🧩 Components

### DpSiteConfig
- **Languages**: Rust, JavaScript
- **Usage**: Frontend and Backend
- **Purpose**: Global configuration management for all services

### DpSiteAuthSession
- **Languages**: Rust, JavaScript
- **Usage**: Backend only
- **Purpose**: Session token encoding/decoding with secret keys

### DpSiteClient
- **Languages**: Rust, JavaScript
- **Usage**: Frontend and Backend
- **Purpose**: Unified client for connecting to all DP Site APIs

## 🛠️ Technology Choices

### Languages
- **Rust**: Chosen for reliability and performance in backend services
- **JavaScript**: Popular choice for frontend development and Node.js backends
- **Future**: Additional languages like Ruby may be supported

### Database
- **SQLite**: Lightweight, reliable, and easy to deploy
  - **Scalable**: Uses multiple database files, even within the same service (e.g., the Auth API has a separate SQLite database just for current sessions)
  - **Easy to backup**: All databases support automatic backup to any S3-compatible storage
  - **PII data encrypted**: While services don't use encrypted SQLite, specific column values are encrypted via application code (e.g., email addresses) to help with security and compliance

### API Layer
- **GraphQL**: 
  - Solidified pattern for API development
  - Multi-language support
  - Advanced features (batched queries, real-time subscriptions)
  - Superior to REST for complex operations

### Frontend Framework
- **Vue.js**: Modern, reactive framework for admin interfaces

## 📈 Development Status

> **Note**: This project is in early planning stages. Most services and components are not yet implemented.

This README serves as the "ultimate goal" and development guide. Components will be developed incrementally, with each service designed to work independently while integrating seamlessly with the ecosystem.

## 🚦 Getting Started

### For Developers
1. Choose your development stack (Rust or JavaScript)
2. Set up your domain structure
3. Deploy the services you need
4. Integrate DP Site components into your application

### For Contributors
1. Check the individual service repositories for development setup
2. Follow the established patterns for new services
3. Ensure compatibility with the overall ecosystem architecture

## 🗺️ Roadmap

1. **Phase 1**: Core authentication services (DpSiteAuthApi, DpSiteAuthWeb)
2. **Phase 2**: Essential components (DpSiteConfig, DpSiteClient)
3. **Phase 3**: Monitoring services (DpSiteLogsApi, DpSiteMetricsApi, DpSiteMonitorWeb)
4. **Phase 4**: Email services (DpSiteMailerApi, DpSiteMailerWeb)
5. **Phase 5**: Additional language support and ecosystem expansion

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. As this ecosystem grows, contribution guidelines will be established for each component.

---

**DP Site** - Building robust, self-hosted web services for the modern web.
