**Note that this method is not recommended, instead use `:call scnvim#install()` and `:call scnvim#uninstall()`**


The SuperCollider classes are located in the `sc/` directory of this repo.

This directory needs to be linked to your SuperCollider `Extensions` directory (run `Platform.userExtensionDir` in SuperCollider to see where it is located on your platform).

1. Create a directory named `scide_scnvim` in the Extensions directory. It is **important** that the directory is named `scide_scnvim` to avoid conflicts with ScIDE.

2. Create a `symlink` (symbolic link) to the `sc` directory of the plugin like in the example below.

#### Examples

* **macOS**

    ```shell
    # create scide_scnvim directory
    mkdir -p ~/Library/Application\ Support/SuperCollider/Extensions/scide_scnvim

    # create a symbolic link to 'sc' in the 'scide_scnvim' directory named 'scnvim'
    ln -s ~/.config/nvim/plugged/scnvim/sc ~/Library/Application\ Support/SuperCollider/Extensions/scide_scnvim/scnvim
    ```

* **Linux**

    It is **important** to use absolute paths. If `~` or `$HOME` or other aliases for `/home/<user>` is used the symbolic link will be "dangling" which renders a situation where sclang crashes immediately when started.

    ```shell
    # create scide_scvim directory
    mkdir -p $HOME/.local/share/SuperCollider/Extensions/scide_scnvim
    
    # create a symbolic link to 'sc' in the 'scide_scnvim' directory named 'scnvim'
    ln -s /home/<USER>/.config/nvim/plugged/scnvim/sc /home/<USER>/.local/share/SuperCollider/Extensions/scide_scnvim/scnvim
    ```

    If the above symlink does not work (you can tell this by opening up a
    SuperCollider file and running `:SCNvimStart` - if something's wrong the
    post window will contain errors about SC not being able to find the SCNvim
    class files), make sure the path to the vim plugin is correct. Depending on
    how you have configured nvim, it might be `/home/<USER>/.vim/plugged/scnvim/sc`.

