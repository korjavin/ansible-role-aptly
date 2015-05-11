Ansible role to build aptly repo


Forked from Alexey Sveshnikov repo (https://github.com/alexey-sveshnikov/ansible-aptly-role)

Info about gpg:
You need a GPG public/private key pair to sign your repository.

Use the following shell commands to obtain your own key pair:

    $ sudo apt-get install gnupg
    $ gpg --gen-key

       Please select what kind of key you want:
        (1) RSA and RSA (default)
        (2) DSA and Elgamal
        (3) DSA (sign only)
        (4) RSA (sign only)
        Your selection? 3

        ... answer questions about your name, key expiration period, etc. ...

        gpg: checking the trustdb
        gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
        gpg: depth: 0  valid:   4  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 4u
        gpg: next trustdb check due at 2019-05-23

        pub   2048D/61B1BA69 2014-05-24
        ~~~~~~~~~~~~^^^^^^^^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
              Key fingerprint = 6C50 B46A 3D75 0C14 041B  6C99 FBBA 0275 61B1 BA69
              uid                  Ivan Ivanov (repository key) <ivan@example.com>

Once you have generated the key pair, you should export it to the corresponding files. Replace key ID with yours (you can find it in the end of previous command's output. In this example, the key ID is 61B1BA69)

    $ mkdir -p secrets/aptly  # (assuming you are in the directory where inventory.ini and playbooks are located. Also see 'Optional Variables' section)
    $ gpg --export-secret-keys --armor 61B1BA69 > secrets/aptly/private.key
    $ gpg --export --armor 61B1BA69 > secrets/aptly/public.key


Role Variables
--------------

#### Should be defined:

1. `aptly_secret_key_id`: ID of the GPG key
