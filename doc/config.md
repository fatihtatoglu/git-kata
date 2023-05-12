# Git Configuration

This document contains an overview of the Git configuration options. Understanding and configuring these options can help customize the Git environment and enhance the workflow.

The git has three configuration options that are built-in and explained in this document. The applicability of these options is from general to local. In other words, the repository-based configuration overrides the global configuration.

## System Configuration

This level of configuration affects all the users on the server. Because of this, it is suitable for the broad configuration options. The scope identifier is the `--system`.

The configuration location can be changed by the installation instruction. However, in many cases, it is located in `/etc/gitconfig` file.

## Global Configuration

This level of configuration affects the currently logged-in users. It overrides the system configuration if it has the same key. It is suitable for personal configuration options, such as username, email address, signing key, etc. The scope identifier is the `--global`.

The configuration location is in the current user's home directory path. With the following command, its content can be written on the terminal.

```bash
cat ~/.gitconfig
```

## Local Configuration

This level of configuration affects the existing git repository. It is suitable for project-specific configuration options, such as remote repository addresses. The configuration file locates in the `.git` folder.

The scope identifier is the `--local`. It overrides all the global and system configuration options if it has the same key.

## Structure of the Configuration Files

The structure has a simple and human-readable format.

```ini
[user]
        name = Fatih Tatoğlu
        email = fatihtatoglu@gmail.com
[commit]
        gpgsign = true
[color "branch"]
        remote = yellow bold
```

With that structure, editing can be easy, but using the `git config` command to manipulate the git configuration options is recommended.

## Essential Configuration

Before starting to use Git, some essential configuration options are needed to be set in the global scope. In the Git Kata, before every scenario, don't forget to arrange them.

```bash
git config --global user.name "Fatih Tatoğlu"
git config --global user.email "fatihtatoglu@gmail.com"
git config --global init.defaultBranch master
```

The `user.name` and `user.email` options are required for committing a change into the git tree.

The `init.defaultBranch` is optional, but setting it creates a standardization for the other git repositories. If not set, the first branch is named `master`.

For other configurations, the Git Kata has some scenarios. For more details, the [git-config](https://git-scm.com/docs/git-config) documentation should be visited.

## Common Configuration Commands

```bash
git config --list
```

The above commands list all the applied configuration options according to the location. Outside of a git repository, it lists the system and global configuration options. Otherwise, the repository configuration options are included.

To find out the location of the configuration options, the `--show-origin` should be added.

```bash
git config --global user.name "Fatih Tatoğlu"
```

The above command is set the `user.name` option. But the important point is using the `"` quotation mark, because the value contains a space char.

```bash
git config --global --unset user.email
```

The above command removes the configuration options in the global scope. For removing a configuration option, the `--unset` command can be used.

```bash
git config --global --edit
```

The above command opens the configuration for editing in the default text editor in the Git configuration. The default text editor can be changed by updating the `core.editor` configuration options.

If the scope isn't specified for the `--edit` command the `local` scope is used as default.

There are many other commands to manage the configuration options. However, in Git Kata, the above commands may be enough. Also, with these commands, many cases can be handled.
