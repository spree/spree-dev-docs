# General guidelines

## Overview

Proper application design, intelligent programming, and secure infrastructure are all essential in creating a secure e-commerce store using any software (Spree included). The Spree team has done its best to provide you with the tools to create a secure and profitable web presence, but it is up to you to take these tools and put them in good practice. We highly recommend reading and understanding the [Rails Security Guide](http://guides.rubyonrails.org/security.html).

## Supported Versions

This is a list of all Spree versions currently being supported by the Spree team.

| Version | Supported? | Release date | EOL date   |
| ------- | ---------- | ------------ | ---------- |
| 4.3     | **Yes**    | 14.09.2021   | 14.09.2023 |
| 4.2     | **Yes**    | 23.02.2021   | 23.02.2023 |
| 4.1     | **Yes**    | 02.03.2020   | 02.03.2022 |
| 4.0     | **Yes**    | 09.10.2019   | 09.10.2021 |
| 3.7 LTS | **Yes**    | 04.02.2019   | 04.02.2022 |

LTS means [Long-term support releases](https://en.wikipedia.org/wiki/Long-term\_support), usually the last release in the major release cycle.

If you're using an older version [please upgrade](../upgrades/upgrades/). Have trouble upgrading? [Contact us for support](https://spreecommerce.org/contact/).

## Reporting Security Issues

Please do not announce potential security vulnerabilities in public. We have a dedicated email address [security@spreecommerce.org](mailto:security@spreecommerce.org). We will work quickly to determine the severity of the issue and provide a fix for the appropriate versions. We will credit you with the discovery of this patch by naming you in a blog post.

If you would like to provide a patch yourself for the security issue **do not open a pull request for it**. Instead, create a commit on your fork of Spree and run this command:

```bash
git format-patch HEAD~1..HEAD --stdout > patch.txt
```

This command will generate a file called `patch.txt` with your changes. Please email a description of the patch along with the patch itself to our [dedicated email address](mailto:hi@spreecommerce.org).
