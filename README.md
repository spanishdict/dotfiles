# Standard dotfiles


These are the dotfiles used by default by the
[Chef dotfiles cookbook](https://github.com/spanishdict/chef-dotfiles).

We install dotfiles from an organization-wide repo so we can easily make, share,
and deploy useful updates to them. Feel free to make generally useful updates,
but for customization, please create your own dotfiles repo and point your user
data bag to it:

* Set `:enabled_custom` to true to add your custom dotfiles, specified by
`custom_dotfiles_repo` in your user data bag. See our
[Chef dotfiles](https://github.com/spanishdict/chef-dotfiles) repo for more
information on how to do this. Custom files will overwrite standard files of the
same name.

* Set `:enabled_custom` to true and set `:enabled_standard` to false to use only
custom and not standard dotfiles.

* Opt out from all of this by setting both `:enabled_standard` and
`:enabled_custom` to false. Your new accounts will receive a stock `.bashrc` and
.screenrc and nothing else, and you will not be able to update these across
instances via Chef.

The standard dotfiles in the dotfiles repo are nearly the same as what we were
already using prior to this repo, with these changes in `.bashrc`:

* Use the instance’s Chef node name in the prompt, like
  `william@aws-staging-app-c1m-01:~$`.
* Add Bash function `greplog` for searching through log files. Usage:

    greplog <log filename prefix> <pattern>.

* Add several Bash functions for counting open network connections:

  * `conns_mysql`
  * `conns_promt`
  * `conns_sdl`
  * `conns_timewait`
  * `conns_prod_mongo`
  * `conns_staging_mongo`

Whenever we want to add or change functions, we can simply add them to the
`.bashrc` in the dotfiles repo, and after a client_run they will then be
available.

Any local, per-instance bashrc stuff can go into `.bashrc_local`, which will be
sourced if it exists, and not overwritten by a client_run.
