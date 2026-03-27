# Accessing ActiveTigger

ActiveTigger is a web application designed to be deployed on a server, but it can also run locally on your machine. Some models works better with a GPU, so hardware can be important for what you want to achieve.

There are two ways to get started:

1. **Get an account on an existing instance**
2. **Install it locally**

---

## Option 1: Use an existing instance

### Existing instance

- CREST development instance

### CREST development instance

A development instance of ActiveTigger is running on GENES servers (with GPU support), accessible [here](https://activetigger.github.io/activetigger).

!!! warning "Development instance"
    This instance is primarily intended for **testing and reporting bugs**. Service continuity is not guaranteed. We reserve the right to modify, restrict, or revoke access at any time.

#### Who can request access?

- Researchers who have textual data to annotate
- Open source contributors who want to help improve the software

#### How to get access

1. Fill this [form](https://www.css.cnrs.fr/request-an-account-on-the-crest-instance/).
2. Once your account is created, you can:
    - Upload data and annotate text
    - Train classification models
    - Report bugs or suggest features via [GitHub issues](https://github.com/activetigger/activetigger/issues)

!!! info "Account policy"
    Accounts without any activity may be deactivated after 2 months.

#### How to get in touch

- **[GitHub issues](https://github.com/activetigger/activetigger/issues)** — for bug reports and feature suggestions
- **[Discord](https://discord.gg/3uNnjw2k)** — for questions and discussions

#### User agreement

!!! warning "Terms of use"
    - Access to ActiveTigger is currently **temporary**
    - **Data storage and security are not guaranteed** — do not upload sensitive data
    - The service is hosted on **ENSAE servers** and intended **solely for research purposes**
    - We reserve the right to **modify, restrict, or revoke access** at any time without notice

---

## Option 2: Install locally

You can deploy your own instance of ActiveTigger on your machine or on a cloud server (e.g., [OVH](https://www.ovhcloud.com/fr/public-cloud)).

!!! info "GPU recommended"
    ActiveTigger can run on CPU, but a GPU will significantly speed up model training and predictions.

For installation instructions, see the [deployment guide](https://github.com/activetigger/activetigger/blob/main/DEPLOY.md).
