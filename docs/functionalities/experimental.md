# Experimental features

This page lists features that are under active development and **not yet part of the main release**. They are exploratory: behavior, parameters, and even the existence of the feature can change without notice. You need to switch to the experimental mode (bottom of the main page, when available).

!!! warning

    Experimental features usually live in **dedicated branches** of the [ActiveTigger repository](https://github.com/activetigger/activetigger) rather than `main`. To try them, you will need to check out the corresponding branch and run the application from source. Hosted instances may not expose these features.

## How to try an experimental feature

1. Identify the branch where the feature is being developed (mentioned in the section below, or in the related pull request / issue).
2. Clone the repository and switch to that branch:
    ```bash
    git clone https://github.com/activetigger/activetigger.git
    cd activetigger
    git checkout <branch-name>
    ```
3. Follow the install instructions on [Install & access](../technicalities/access.md).

!!! info

    Experimental features may require database migrations or specific configuration that differs from the main release. Use a fresh project to avoid corrupting existing data.

## Current experimental features

- `image` : it allows to create image projects, to annotate images

