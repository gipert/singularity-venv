# singularity-venv

Manage virtual [Singularity](https://sylabs.io) environments. Idea stolen from
[oschulz/singularity-venv](https://github.com/oschulz/singularity-venv).

### Install
```console
$ git clone https://github.com/gipert/singularity-venv ~/.singularity-venv
$ export PATH="$PATH:$HOME/.singularity-venv/bin"
```

### Quick start

1. Create a virtual environment
   ```console
   $ svenv -- create -n my-env Singularity.def
   ```
   The source can be whatever `singularity build` accepts (another image,
   remote link...).  Create a sandbox (writable) container with `create -s`.

1. List the available environments:
   ```console
   $ senv -- list
   my-env.rootfs
   my-env.sif
   ```
   The `.rootfs` extension is used to mark writable environments.

1. Spawn a shell inside an environment (read-only mode):
   ```console
   $ svenv -- shell my-env.sif
   ```
   or in write mode with `svenv -- shell -w my-env.sif`.

1. Run a a command inside the environment and exit:
   ```console
   $ svenv -- exec my-env.sif 'uname -a'
   ```

1. Specify custom commands to be executed at startup inside the environment:
   ```console
   $ echo "export VAR=value\n; alias root='root -l'" > ~/.singularity-venv/depot/my-app.env
   ```

1. Specify additional additional `singularity build` command line options:
   ```console
   $ echo "--bind /home/user/data:/data" > ~/.singularity-venv/depot/my-app.flags
   ```

1. Consult the help sections `svenv -h` or `svenv -- ACTION -h` for further documentation.

### Customization

- **`SINGULARITY_DEPOT_PATH`** : customize the storage location of the
  Sigularity containers. defaults to `~/.singularity-venv/depot`.
