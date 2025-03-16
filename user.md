# CMS Cloud Manager: User documentation

The **CMS Cloud Manager** panel is very easy to use and features various tools for its operation.

## Supported Providers and CMS / Apps

### Providers

- Hetzner

### CMS / Apps

- TYPO3 ([GitHub](https://github.com/cmscloudmanager/typo3))
- WordPress ([GitHub](https://github.com/cmscloudmanager/wordpress))

## Access the site

This is a website, so you can access the website with the URL provided to you.

- User: `admin@admin.admin`
- Password: `password`

![Login](image/app-001.png)

## Providers setting

You can set a Provider API key. It will save the API there so you can create a Project later.

Go to the provider list and Add.

![Provider list](image/app-002.png)

Fill the form to save the Provider information.

![Create a provider](image/app-003.png)

## Project creation

You can create a Project, and get the YAML file to run it on the CLI tool.

Go to the project list and Add.

![Project list](image/app-004.png)

Fill the form about the project.

![Project information](image/app-005.png)

Fill the form about the provider and other configurations.

![Extra information](image/app-006.png)

And get the YAML file to run on the CLI tool.

![Get the YAML file](image/app-007.png)

And, run it with the CLI tool.

```bash
python3 main.py deploy ~/my_manifest.yml
```
