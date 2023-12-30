+++
title = 'SSH connection to GitLab with more than one user account.'
description = 'When switching from a personal to a company GitLab account, facing an SSH key conflict can occur. This article guides you in creating a new key for smooth connections to both accounts.'
date = 2021-02-03
tags = ["GitLab", "Muliple User Gitlab"]
draft = false
+++

Imagine you have a personal user account on GitLab with the email yourname@gmail.com, and now you've been hired by a company. You need to connect to GitLab with the email account they provided for you (yourname@company.com). If you've previously added your system's public key for your personal account and SSH connection, you may encounter an error when trying to add the same key for the company's GitLab account. This error informs you that the key has already been added because GitLab doesn't allow using a common SSH public key across two different user accounts. Therefore, you need a new key. In this article, I will guide you on how to create a new key and easily connect via SSH to each of these accounts. Stay with me.

### Steps for configuring an SSH key for connecting to GitLab
Let's assume your previous key (used for personal GitLab) has already been generated and exists with the name id_rsa.pub in the ssh directory of your system.
```bash
~/.ssh/id_rsa
```
Now, simply create a new key for your company's GitLab account using the following command in the terminal ([more details](https://docs.gitlab.com/ee/ssh/#generate-an-ssh-key-pair)):

```bash
ssh-keygen -t rsa -b 4096 -C "yourname@company.com"
```

Press Enter, and you will be prompted with the following question in the terminal:

```bash
Enter file in which to save the key (/Users/yourname/.ssh/id_rsa):
```

Enter the complete address and filename here. For example, if you want the key to be generated in a file named 'company_rsa,' you need to enter the full address and press Enter.

```bash
/Users/yourname/.ssh/company_rsa
```
Finally, two files named `company_rsa` and `company_rsa.pub` will be generated. Just add the content of `company_rsa.pub` to GitLab. [Read more details in GitLab](https://docs.gitlab.com/ee/ssh/#add-an-ssh-key-to-your-gitlab-account)

### Configuration File Setup

To connect through two different SSH keys for two separate accounts, simply create a file named 'config' in the same directory and include the following commands in it:

```bash
# Private GitLab instance
Host yournamePrivateUsername.gitlab.com
  Hostname gitlab.com
  Preferredauthentications publickey
  IdentityFile ~/.ssh/id_rsa
# Company GitLab instance
Host yournameCompanyUsername.gitlab.com
  Hostname gitlab.com
  Preferredauthentications publickey
  IdentityFile ~/.ssh/company_rsa
```

As seen in the above code, in the `Host` sections, simply define a name for each GitLab user account to use its corresponding address for the remote URL and connection with GitLab.

### Changes related to remote repository addresses

Go to GitLab and the respective repository location. Copy the address in the `Clone with SSH` section, apply the relevant changes, and ultimately clone. For example, if the remote address is as follows:

```bash
git@gitlab.com:company/repo.git
```

With regard to the host defined in the configuration file, modify it as follows:

```bash
git@yournameCompanyUsername.gitlab.com:company/repo.git
```

### Reconfiguring Git for each repository

Pay attention to your Git configuration. If you have globally set something previously, make sure to redefine it for each repository to avoid committing with a different email or name in the wrong repository/account.

To do this, go to the respective repository and execute the following two commands according to the user account:
```bash
git config user.email "your_email@example.com"
git config user.name "Your Name"

```

This ensures that the configuration is specific to each repository, preventing unintentional commits with incorrect credentials."





























