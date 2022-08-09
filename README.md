# au-fsv22
Docker container for courses based on the Software Foundations book.
The container can be used for easy cross-platform Coq development using Visual Studio Code.

The image uses Coq 8.15.2 and includes *all dependencies* needed to complete the following Software Foundations volumes
* Logical Foundations (Volume 1)
* Programming Language Foundations (Volume 2)
* Verified Functional Algorithms (Volume 3)
* QuickChick: Property-Based Testing in Coq (Volume 4)
* Separation Logic Foundations (Volume 6)


## Setup
* [Install Docker](https://www.docker.com/get-started/)
* [Install Visual Studio Code](https://code.visualstudio.com/Download)
* [Install Remote - Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
* Copy the `.devcontainer` folder to your project folder

After following the above instructions open your project in Visual Studio Code and run the `Remote-Containers: Reopen in Container` command.
If the instructions are followed correctly Visual Studio Code should also automatically suggest opening the repository in container mode when the project is loaded.

## Known problems
### VSCode shows `Docker returned an error`
Make sure that Docker is installed and running.

### The `Remote-Containers: Reopen in Container` is not recoqnized by VSCode
You need to have the Remote - Containers extension VSCode extension installed and enabled.
See [here](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) for instructions on how to install it.

### Running `Remote-Containers: Reopen in Container` cannot find container
Make sure you copied the `.devcontainer` folder to your projects root folder and that it includes the `devcontainer.json` file.

### `Cannot find a physical path bound to logical path X with prefix Y` when importing file
* Make sure that the Coq files have been compiled. Run `make` to compile the project files.
* If the `_CoqProject` files is not located in the project root folder you need to either
  * Move the files to the root project folder
  * Or change the line `"coq.coqProjectRoot": "."` (in `.devcontainer/devcontainer.json` to point to the directory where `_CoqProject` is located. Restarting the docker container is required after this step.

### Docker pull rate limit hit
Docker Hub rate limits pulls of images for free accounts to 200 per six hours.
If this limit is hit you might get one of the following errors and have to wait until the rate limit resets.
* `ERROR: toomanyrequests: Too Many Requests`
* `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits`


## FAQ
### What is included in the Docker image?
The Docker image used for the devcontainer is built using the [Dockerfile](Dockerfile) in this repository, which is based on the [coqorg/coq:8.15.2-ocaml-4.14.0-flambda](https://hub.docker.com/layers/coq/coqorg/coq/8.15.2-ocaml-4.14.0-flambda/images/sha256-5bf48009faa80a0cdab45b77d5e3dcbd5ab80358e9a8923371a5959fc821f3df?context=explore) image. This image includes:
* Debian 11 Slim
* opam 2.1.2
* OCaml 4.14.0
* Coq 8.15.2
* coq-quickchick 1.6.1
* coq-ext-lib 0.11.6
* coq-equations 1.3+8.15
