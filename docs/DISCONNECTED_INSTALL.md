# Disconnected Installation

One of the major features of Kismatic is the ability to install Kubernetes on a set of lab machines that don't necessarily have direct access to the internet.

Being disconnected means that you will not use public repositories or registries to get binaries to your nodes. Instead, you will first sync a local package repository and Docker registry with Kismatic binaries.

You must have a private Docker Registry to perform a disconnected install -- if you don't have one,  Kismatic will grab all images from DockerHub. It's strongly encouraged you install, scale and secure a Docker Registry yourself. Kismatic will install one on your behalf but it won't be scalable or secure.

There are two options in a Plan file that control disconnected installs:

**allow_package_installation**: If you want to install your own packages, set this flag to **false**. Not only will Kismatic NOT install packages for you, it will enforce that they have been installed correctly before attempting to install or upgrade Kubernetes.

**disconnected_install**: If you maintain your own docker registry, setting this flag to **true** will cause Kismatic to install a big package full of docker images needed to install Kubernetes.

... | connected install | disconnected install 
--- | --- | --- 
**allow package installation** | Most users will want this. Kismatic is fully automates and will download and install packages and docker images from public sources. This is likely the best option if you have internet access to your nodes and a wide pipe. | In this case, packages may be downloaded from the internet, but docker images will be downloaded once and installed in a docker registry that will feed your nodes.
**disallow package installation** | This is the option to choose if you do not want Kismatic to install any packages, but don't have an on-site docker registry. | In this case, you will be installing your own packages and synchronizing docker images with a local docker registry.
