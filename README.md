# Whiplash[![Build status](https://badge.buildkite.com/73e7fa3f732bafa8bd36b8e73e6d6faff84cbe0ec72c7bc83f.svg)](https://buildkite.com/forum-one/whiplash)

- Introduction
- Development Branch Naming & Workflow
- What comes with Whiplash?
- Requirements
- Installation

## Introduction
Whiplash contains an installation profile that allows developers to quickly start a Drupal site. It includes reasonable defaults with stability, security, and the content authoring experience in mind.

## Development Branch Naming & Workflow

- Always create Feature and Bugfix branches from the `main` branch.
- When needed, create Hotfix branches from `main`.
- Merge, or submit a Pull Request, from Feature/Bugfix/Hotfix branches to `develop`.
- Submit a Pull Request from Feature/Bugfix branches to current pre-release branch `1.x`.
- Submit a Pull Request from Hotfix branches to `main`.
- Submit a Pull Request from `1.x` to `main` for all regular releases.

## What comes with Whiplash?

### Modules
Whiplash comes with the following common modules installed via Composer dependencies. For more information on the modules please follow the links provided below.

[Address](https://www.drupal.org/project/address)  
[Admin Toolbar](https://www.drupal.org/project/admin_toolbar)  
[Allowed Formats](https://www.drupal.org/project/allowed_formats)  
[CKEditor Anchor Link](https://www.drupal.org/project/anchor_link)  
[CKEditor IndentBlock](https://www.drupal.org/project/ckeditor_indentblock)  
[Components](https://www.drupal.org/project/components)  
[Configuration Split](https://www.drupal.org/project/config_split)  
[Config Direct Save](https://www.drupal.org/project/config_direct_save)  
[Contact Storage](https://www.drupal.org/project/contact_storage)  
[Devel](https://www.drupal.org/project/devel)  
[Diff](https://www.drupal.org/project/diff)  
[Entityqueue](https://www.drupal.org/project/entityqueue)  
[Facets](https://www.drupal.org/project/facets)  
[Field Group](https://www.drupal.org/project/field_group)  
[Focal Point](https://www.drupal.org/project/focal_point)  
[GoogleTagManager](https://www.drupal.org/project/google_tag)  
[Inline Entity Form](https://www.drupal.org/project/inline_entity_form)  
[Libraries API](https://www.drupal.org/project/libraries)  
[Login History](https://www.drupal.org/project/login_history)  
[MaxLength](https://www.drupal.org/project/maxlength)  
[Metatag](https://www.drupal.org/project/metatag)  
[Paragraphs](https://www.drupal.org/project/paragraphs)  
[Password Policy](https://www.drupal.org/project/password_policy)  
[Pathauto](https://www.drupal.org/project/pathauto)  
[Rabbit Hole](https://www.drupal.org/project/rabbit_hole)  
[Redirect](https://www.drupal.org/project/redirect)  
[Save & Edit](https://www.drupal.org/project/save_edit)  
[Search API](https://www.drupal.org/project/search_api)  
[Simple XML sitemap](https://www.drupal.org/project/simple_sitemap)  
[Twig Field Value](https://www.drupal.org/project/twig_field_value)  
[Twig Tweak](https://www.drupal.org/project/twig_tweak)  
[Username Enumeration Prevention](https://www.drupal.org/project/username_enumeration_prevention)  

### Configuration
Configuration occurs during site installation but can be modified and added to as needed. Config Split and Config Direct Save are included to allow for different configuration per environment and to make syncing configuration easier during development.

## Requirements
Your development and hosting environments must be capable of running Drupal 9. See Drupal's [system requirements](https://www.drupal.org/docs/system-requirements).

This project assumes that Gesso will be used as the default theme.

Whiplash needs to be installed and updated using Composer and assumes that your project includes Drupal core.

## Installation
[DDEV](https://ddev.com/) is recommended for local development.

The [drupal project](https://github.com/forumone/drupal-project) template is recommended as a starting point. You can also refer to [whiplash demo](https://github.com/forumone/whiplash-demo) for an example of how to use the drupal project with whiplash as a profile.

Once you have a starting point for development that includes Composer and Drupal core, include the necessary source repositories. The source repository section should look like:

```
"repositories": [
    {
        "type": "composer",
        "url": "https://packages.drupal.org/8"
    },
    {
        "type": "vcs",
        "url": "https://github.com/forumone/whiplash"
    },
    {
        "type": "package",
        "package": {
            "name": "ckeditor/indentblock",
            "version": "4.11.4",
            "type": "drupal-library",
            "dist": {
                "url": "https://download.ckeditor.com/indentblock/releases/indentblock_4.11.4.zip",
                "type": "zip"
            },
            "require": {
                "composer/installers": "^1.2.0"
            }
        }
    },
    {
        "type": "package",
        "package": {
            "name": "ckeditor/fakeobjects",
            "version": "4.11.4",
            "type": "drupal-library",
            "dist": {
                "url": "https://download.ckeditor.com/fakeobjects/releases/fakeobjects_4.11.4.zip",
                "type": "zip"
            },
            "require": {
                "composer/installers": "~1.0"
            }
        }
    },
    {
        "type": "package",
        "package": {
            "name": "ckeditor/link",
            "version": "4.11.4",
            "type": "drupal-library",
            "dist": {
                "url": "https://download.ckeditor.com/link/releases/link_4.11.4.zip",
                "type": "zip"
            },
            "require": {
                "composer/installers": "~1.0"
            }
        }
    }
],
```

If you are using drupal project as a starting point make sure to remove any duplicated dependencies in the composer.json. The require section in your composer.json should look similar to:

```
    "require": {
        "php": ">=7.3",
        "composer/installers": "^1.10",
        "cweagans/composer-patches": "^1.7",
        "drupal/core-composer-scaffold": "^9",
        "drupal/core-recommended": "^9",
        "drupal/core-vendor-hardening": "^9",
        "drush/drush": "^9.7.1 | ^10.0.0",
        "joachim-n/composer-manifest": "^1",
        "rvtraveller/qs-composer-installer": "^1.2",
        "vlucas/phpdotenv": "^4.0",
        "webmozart/path-util": "^2.3"
    },
```

Install Whiplash as a composer dependency

```
ddev composer require forumone/whiplash
```

Install Drupal

```
ddev drush si whiplash -y
```
