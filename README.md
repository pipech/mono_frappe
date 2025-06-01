# Mono-repo Setup for Frappe

- Mono repo for all frappe apps.
- Use [Git Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) to nest git inside git.
- Centerize various settings.
  - ruff for linting and formatting.
  - isort for sorting imports.
  - vscode editor settings.

## Setting-up Git Mono Repo

1. You'll need to create an app using `bench new-app your_app_name`
2. Create copied from this mono repo template
3. Add your app submodule to this mono repo template `git submodule add https://github.com/your_repo/your_app_name`

## Initial Setup

### Hot-fix Bench

Before install apps, you will need to patch bench.

https://github.com/frappe/bench/issues/1628

Before this get merge, apply hot fix by.

/home/frappe/.bench/bench/app.py
```py
def setup_details(self):
    # support for --no-git
    if not self.is_repo:
        self.on_disk = True
        self.repo = self.name
        self.tag = self.branch = None
        return
```

### Install Apps

Install apps.

```bash
bench get-app --soft-link your_app_name /home/frappe/bench/mono_frappe/your_app_name
```

### Create Symbolic Link

ERPNext and Frappe are great resource, we'll need that in our env.
This will create symbolic link to actual apps.

```bash
ln -s /home/frappe/bench/apps/erpnext /home/frappe/bench/batch_payment/erpnext
ln -s /home/frappe/bench/apps/frappe /home/frappe/bench/batch_payment/frappe
```

## Run Service

```bash
# Support service
bench start

# Web server
bench serve --port 8000
```