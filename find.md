> find . ! -name 'file.txt' -type f -exec rm -f {} +

will remove all regular files (recursively, including hidden ones) except file.txt. To remove directories, change -type f to -type d and add -r option to rm.

In bash, to use rm -- !(file.txt), you must enable extglob:

> shopt -s extglob 
> rm -- !(file.txt)

(or calling bash -O extglob)

Note that extglob only works in bash and Korn shell family. And using rm -- !(file.txt) can cause an Argument list too long error.

In zsh, you can use ^ to negate pattern with extendedglob enabled:

> setopt extendedglob
> rm -- ^file.txt

or using the same syntax with ksh and bash with options ksh_glob and no_bare_glob_qual enabled.
