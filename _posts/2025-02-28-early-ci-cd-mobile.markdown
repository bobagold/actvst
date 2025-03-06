---
title: "Early Adoption of CI/CD in Mobile App Development"
date: 2025-02-28
layout: single
excerpt: "A practical guide to adopting CI/CD early in your mobile projects to accelerate development, enhance quality, and streamline deployments."
categories: [CI/CD, Mobile Development, Flutter]
tags: [CI/CD, Flutter, CodeMagic, GitHub Actions, GitLab CI, Automation]
---

## Introduction

Early adoption of Continuous Integration and Continuous Delivery (CI/CD) is critical for mobile projects. From my experience, adopting CI/CD early accelerates development, simplifies onboarding, and significantly enhances the development workflow. In this article, I'll share my experiences and insights into effectively integrating CI/CD using my favorite tools: **CodeMagic**, **GitHub Actions**, and **GitLab CI**.

## Why Early CI/CD Matters

Implementing CI/CD from the start provides immediate visibility into the actual state of builds and artifacts. It clearly highlights what's missing before the app can reach the store, allowing you to quickly iterate and resolve issues proactively.

## Choosing the Right CI/CD Tools

My default choice for CI/CD in mobile apps is **CodeMagic**, particularly when security constraints are minimal. However, the free plan of CodeMagic can be limiting, and migrating from its UI-based configuration to YAML isn't straightforward. 

For projects with private repositories, I've set up private runners with **GitHub Actions** and **GitLab CI** multiple times. While initially challenging, it's manageable once you're comfortable with the setup.

## Managing Private Runners and Apple Certificates

I experimented with using CodeMagic CLI tools on private runners to handle Apple certificates. However, sharing a single host machine among multiple projects often introduced complications, especially with parallel builds.

I've tried both global keychains and temporary keychains. Unfortunately, neither solution perfectly handled parallel builds. This challenge remains open-ended and continues to be an area of exploration.

## Structuring the Deployment Pipeline

My typical CI/CD pipelines include scheduled jobs, triggers on pushes, and pull requests. Each pipeline runs comprehensive checks:

- Static analysis, linting, and formatting
- Unit and integration tests
- Coverage checks (minimum 80%)
- Dependency management and validation
- License compliance
- Security checks (e.g., detection of private keys)

## Pre-commit.com

My pre-commit configurations often include tools like:

- `trailing-whitespace`
- `end-of-file-fixer`
- `check-yaml`
- `check-added-large-files`
- `check-merge-conflict`
- `check-json`, `check-xml`
- `fix-byte-order-marker`
- `detect-private-key`
- `mixed-line-ending`
- [`codespell`](https://github.com/codespell-project/codespell)
- Dart and Flutter-specific checks (format, analyze, test, license checks, dependency validation)

I strongly recommend using [pre-commit.com](https://pre-commit.com/) to quickly and easily integrate all these quality checks. It simplifies managing hooks and ensures consistent quality across teams.

Here is a snippet from one of my projects:
```yaml
# See https://pre-commit.com for more information
# See https://pre-commit.com/hooks.html for more hooks
default_install_hook_types: [pre-commit, pre-push, commit-msg]
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v5.0.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-added-large-files
      - id: check-merge-conflict
      - id: check-json
      - id: check-xml
      - id: fix-byte-order-marker
      - id: detect-private-key
      - id: mixed-line-ending
  - repo: https://github.com/codespell-project/codespell
    rev: v2.3.0
    hooks:
      - id: codespell
        exclude: (^api-client/|_de\.\w+$)
  - repo: local
    hooks:
      - id: check-format
        name: Check format
        entry: dart format --line-length 80 --set-exit-if-changed
        language: system
        files: \.dart$
        exclude: \.(gen|g|mocks)\.dart$
      - id: get-packages-app
        name: Get packages in app
        entry: bash -c 'cd app && flutter pub get'
        pass_filenames: false
        language: system
        files: ^app/pubspec.yaml$
      - id: check-packages
        name: Update packages in app
        entry: bash -c 'cd app && flutter pub upgrade'
        pass_filenames: false
        language: system
        files: ^app/pubspec.yaml$
      - id: generate-l10n
        name: Run flutter gen-l10n in app
        entry: bash -c 'cd app && flutter gen-l10n'
        pass_filenames: false
        language: system
        files: (^app/lib/config/l10n/app_.*\.arb$|\.dart$)
      - id: check-analyze-app
        name: Run dart analyze in app
        entry: bash -c 'cd app && dart analyze'
        pass_filenames: false
        language: system
        files: ^app/.*\.dart$
      - id: check-test
        name: Run flutter test in app
        entry: bash -c 'cd app && flutter test'
        pass_filenames: false
        language: system
        files: ^app/.*\.dart$
      - id: check-test-coverage
        name: Check test coverage treshold in app
        stages: [pre-push]
        entry: bash -c 'cd app && flutter test --coverage && lcov --summary coverage/lcov.info --fail-under-lines 80'
        pass_filenames: false
        language: system
        files: ^app/.*\.dart$
```

Integration of pre-commit with action runners requires some boilerplate, but it is worth it - you will have a single set of checks locally and on CI/CD.


## GitLab CI/CD

Here is a short snippet that enables flutter quality checks on GitLab CI/CD:

```yaml
# You can copy and paste this template into a new `.gitlab-ci.yml` file.
# You should not add this template to an existing `.gitlab-ci.yml` file by using the `include:` keyword.
#
# To contribute improvements to CI/CD templates, please follow the Development guide at:
# https://docs.gitlab.com/ee/development/cicd/templates.html
# This specific template is located at:
# https://gitlab.com/gitlab-org/gitlab/-/blob/master/lib/gitlab/ci/templates/Flutter.gitlab-ci.yml

code_quality:
  stage: test
  image: "ghcr.io/cirruslabs/flutter:3.10.3"
  before_script:
    - flutter pub global activate dart_code_metrics
    - export PATH="$PATH:$HOME/.pub-cache/bin"
  script:
    - cd app
    - metrics lib -r codeclimate  > gl-code-quality-report.json
  artifacts:
    reports:
      codequality: app/gl-code-quality-report.json

test:
  stage: test
  image: "ghcr.io/cirruslabs/flutter:3.10.3"
  before_script:
    - flutter pub global activate junitreport
    - export PATH="$PATH:$HOME/.pub-cache/bin"
  script:
    - cd app
    - flutter test --machine --coverage | tojunit -o report.xml
    - lcov --summary coverage/lcov.info --fail-under-lines 80
    - genhtml coverage/lcov.info --output=coverage
  coverage: '/lines\.*: \d+\.\d+\%/'
  artifacts:
    name: coverage
    paths:
      - $CI_PROJECT_DIR/app/coverage
    reports:
      junit: app/report.xml

deploy:
  stage: deploy
  script: echo "Define your deployment script!"
  environment: production
```

## Useful links

Here is a couple of handy actions that would help to deploy your app:
- [upload-google-play - GitHub Action](https://github.com/r0adkll/upload-google-play)
- [Codemagic CLI tools](https://docs.codemagic.io/knowledge-codemagic/codemagic-cli-tools/)
- [Dart license checker](https://pub.dev/packages/license_checker)
- [Dart Dependency Validator](https://pub.dev/packages/dependency_validator)

## Code Generation in Team Projects

When working in a team, consistency is key regarding generated files. Clearly decide early whether all generated files should be committed or excluded completely. Avoid mixing both approaches—consistency significantly simplifies development and CI/CD management.

## Smooth Transition from Development to Publishing

To streamline deployments and ensure consistency, I rely heavily on Flutter flavors to manage builds for different environments (development, staging, production). Publishing should always be an integrated part of your CI/CD pipeline, not a manual step.

### Flutter Flavors and Dart Defines

Rather than creating multiple entry points, I use Flutter flavors primarily for platform-specific assets and configurations. Dart-level configurations are managed via Dart defines, which should remain orthogonal to flavor settings. 

The best practice here is:

- Configure Dart defines through environment variables and secrets.
- Provide sensible defaults for local development, allowing the project to run easily with just `flutter run`.

## Secure Management of Secrets

My preferred method is using built-in CI/CD secrets. Ensure the runners are managed by trusted team members and configured to execute jobs only from trusted branches and projects.

## Key Takeaway: Short Feedback Loops

The most valuable lesson from early adoption of CI/CD is maintaining the shortest possible loop from commit to end-user devices. This short loop greatly benefits:

- Testing and quality assurance
- Developer onboarding
- Quick store feedback (App Store, Play Store)
- Increased developer engagement and productivity

Implementing this approach has consistently provided clear value in all my mobile projects.

## Conclusion

Adopting CI/CD early in mobile app development streamlines processes, significantly improves app quality, and ensures faster and smoother deployments. It pays off not only in technical quality but also by fostering better collaboration and developer experience.

What have been your experiences with early CI/CD adoption? Share your thoughts and insights below!

