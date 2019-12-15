# AWX Promotion Pipeline

Ansible AWX code promotion solution using Ansible playbooks and the tower modules. This can be consumed via Jenkins, GitHub Actions, GitLab and others for full code promotion and rigid tower resource definitions. This solution also allows you to audit your code promotion using native Git tools.

## Table of Contents

- [AWX Promotion Pipeline](#awx-promotion-pipeline)
  - [Table of Contents](#table-of-contents)
  - [Requirements](#requirements)
  - [Getting Started](#getting-started)
    - [Generate Base .awx-pipeline.yml](#generate-base-awx-pipelineyml)
    - [Importing Content](#importing-content)
  - [Authors](#authors)

## Requirements

## Getting Started

In order to use this pipeline we need to define a base set of variables in the `vars/` sub-directory.

We've provided a base example called `vars/NA_development.yml`.

### Generate Base .awx-pipeline.yml

If you want to generate the absolute minimum working project/job_template definitions in an .awx-pipeline.yml, use the `generate-pipeline.yml` provided playbook.

```bash
ansible-playbook generate-pipeline.yml
```

```bash
Project Name: Test
Project Description: Test Description
Project Organization Name [default]: admin-oar
Project SCM URL: https://github.com/anthonyloukinas/ping.git
Job Template Name: Testing
Job Template Playbook YML: main.yml
```

That will output the following to your directory: `awx-pipeline-Test.yml`

```yaml
---

job_templates:
  Testing:
    name: Testing
    project: Test
    playbook: main.yml
    job_type: run
    ask_inventory: yes # Set to no, if inventory: "" var set

project:
  name: Test
  description: Test Description
  organization: admin-oar
  # scm_credential: ""
  scm_url: https://github.com/anthonyloukinas/ping.git
```

You can add additional configuration to this file, and then place it in your code repository base, named `.awx-pipeline.yml`.

### Importing Content

You will need to provide the following variables to the pipeline

- `git_scm_url` - Git repository where Ansible code + .awx-pipeline.yml file exists.

These variables are covered in the lane/region specific var files in `vars/`

- `tower_lane` - Dev, UAT, Prod, etc.
- `tower_region` - NA, EU, ASIA, SA, etc.
- `tower_host_api` - Base url (localhost)
- `tower_username_api` - Tower username
- `tower_password_api` - Tower password
- `tower_proto_api` - Http or https

```bash
ansible-playbook run-pipeline.yml \ 
  -e @vars/NA_production.yml \
  -e git_scm_url=https://github.com/anthonyloukinas/ping.git
```

Project

![Project](images/project.png)

Job Template

![Template](images/template.png)

## Authors

- Anthony Loukinas <<anthony.loukinas@redhat.com>>