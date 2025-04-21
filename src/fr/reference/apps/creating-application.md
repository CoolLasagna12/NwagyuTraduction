# Comment créer son application

Sur cette page, vous allez apprendre à créer votre application.

## Choix du système d'exploitation 

Avant de créer votre application, vous devez choisir le système d'exploitation sur lequel elle fonctionnera, vu que le format d'application d'Epsilon (NWA) n'est pas le même que celui d'Omega/Upsilon.

### Différences entre Omega, Upsilon et Epsilon

#### Upsilon et Omega (extapp)

Les applications externes ont été créées par Omega. À l'origine, Omega API a été conçu pour KhiCAS mais a évolué pour faire tourner d'autres applications externes.

Les applications externes d'Omega ne sont pas supprimées à l'activation du mode examen. Elles seraient plus rapides et leur API peut être modifiée et étendue.

Upsilon a été créé après la sortie d'Epsilon 16, car les mainteneurs ne voulaient pas entrer dans un jeu du chat et de la souris avec Numworks. Un autre fork d'Omega, Khi, a été créé par Bernard Parisse, le développeur de KhiCAS et xcas. Il a ajouté plusieurs fonctionnalités à l'API des applications externes, comme la possibilité d'écrire sur la Flash. Upsilon, de son côté, a continué à ajouter de nouvelles fonctionnalités, intégrant notamment les améliorations apportés par Khi.

`extapp` est le préfixe utilisé par l'API des applications externes sur Omega.

La documentation sur les extapp d'Omega/Upsilon est disponible sur le repo d'[Upsilon External](https://github.com/UpsilonNumworks/Upsilon-External/blob/master/docs/new-app.md).

#### Epsilon (NWA/EADK)

Epsilon 16 (la première version fermée d'Epsilon) a ajouté le support des applications externes (sous le format NWA) pour se donner bonne conscience auprès de la communauté, après avoir supprimé toute liberté sur les calculatrices Numworks (qui fut leur argument de vente).

Toutefois, leur système d'applications externes comporte de nombreuses restrictions face à celui d'Omega :
- Les applications externes ne sont pas disponibles lors du mode examen
- Les applications externes sont supprimées lors du reset de la calculatrice (crash inclus)
- L'accès au stockage n'est pas officiellement supporté (mais une réimplémentation a été créée [ici](storage.md))
- Seul Numworks a le contrôle sur l'API, donc la modifier n'est pas toujours possible (en désactivant les [boutons On/Off et Menu](onoff-home.md) par exemple)

EADK (Epsilon App Developement Kit) est donc le nom donné par Numworks à l'API utilisé par les applications NWA.

## Créer une application Upsilon

La documentation sur Omega et Upsilon (extapp) est disponible sur le repo d'[Upsilon External](https://github.com/UpsilonNumworks/Upsilon-External/blob/master/docs/new-app.md).

Les applications d'Upsilon sont, pour la plupart, rétro-compatibles avec Omega si elles n'utilisent pas l'API spécifique à Upsilon, même s'il n'y a aucune vraie raison d'utiliser Omega plutôt qu'Upsilon dans tous les cas.

## Créer une application NWA/EADK

### Choisir un langage de programmation

Les applications NWA sont écrites dans des langagés compilés, comme le C, le C++, le Rust, le Zig, et tant d'autres.

Le C et le C++ sont très similaires et leur différence principale est que le C++ est orienté-objet, avec un support des classes, permettant aux codes d'être plus organisés et plus agréables à construire. La syntaxe du C est aussi utilisable en C++, donc, sauf si vous avez une raison très spécifique de ne pas vouloir utiliser du C++, il est préférable au C.

Rust est un langage moderne et sans problèmes de mémoire, épargnant beaucoup de temps de débogage, et des performances semblables au C et au C++. Le Rust possède également un écosystème de librairie pour ne pas avoir à réinventer la roue.

### Créer votre application

:::tabs
@tab C
NumWorks a une template d'application en C sur leur repo GitHub  [numworks/epsilon-sample-app-c](https://github.com/numworks/epsilon-sample-app-c).

Pour l'utiliser, suivez les instructions dans le README.



Instructions to install the toolchain (choose the one corresponding to your
Linux distribution, or adapt the commands if it's not listed):

```bash
sudo apt install git make gcc-arm-none-eabi npm # Ubuntu/Debian
sudo pacman -S git make arm-none-eabi-gcc arm-none-eabi-newlib npm # Arch Linux
```

Here is a quick guide about it, assuming the toolchain is already installed:

```bash
git clone https://github.com/numworks/epsilon-sample-app-c
cd epsilon-sample-app-c

# To build and install the app on you calculator directly.
make run

# To simply build your app
make # make build for the full command

# To clean the build cache in case of inconsistent cache
make clean
```

If you get an error like this, it means that you are using a too recent Node
version. You can downgrade Node, or upgrade `nwlink` (see below).

```output
CC      src/main.c
src/main.c:1:10: fatal error: eadk.h: No such file or directory
    1 | #include <eadk.h>
      |          ^~~~~~~~
compilation terminated.
```

The nwa file is located under `output/app.nwa`, and is ready to be flashed from
NumWorks website just as any normal external app.

@tab C++
NumWorks is providing a C++ application template on the GitHub repo
[numworks/epsilon-sample-app-cpp](https://github.com/numworks/epsilon-sample-app-cpp)

To use it, follow the instructions on the README.

Instructions to install the toolchain (choose the one corresponding to your
Linux distribution, or adapt the commands if it's not listed):

```bash
sudo apt install git make gcc-arm-none-eabi npm # Ubuntu/Debian
sudo pacman -S git make arm-none-eabi-gcc arm-none-eabi-newlib npm # Arch Linux
```

Here is a quick guide about it, assuming the toolchain is already installed:

```bash
git clone https://github.com/numworks/epsilon-sample-app-cpp
cd epsilon-sample-app-cpp

# To build and install the app on you calculator directly.
make run

# To simply build your app
make # make build for the full command

# To clean the build cache in case of inconsistent cache
make clean
```

If you get an error like this, it means that you are using a too recent Node
version. You can downgrade Node, or upgrade `nwlink` (see below).

```output
CC      src/main.c
src/main.c:1:10: fatal error: eadk.h: No such file or directory
    1 | #include <eadk.h>
      |          ^~~~~~~~
compilation terminated.
```

The nwa file is located under `output/voord.nwa`, and is ready to be flashed
from NumWorks website just as any normal external app.

@tab Rust
NumWorks is providing a Rust application template on the GitHub repo
[numworks/epsilon-sample-app-rust](https://github.com/numworks/epsilon-sample-app-rust)

To use it, follow the instructions on the README.

To install the toolchain, simply install the toolchain using
[rustup](https://rustup.rs/) or your distributions packages.

You also need Node installed with Nwlink

For example, you can install it this way on Ubuntu (but it shouldn't be very
different on other Linux distributions like Arch Linux)

```bash
sudo apt install git rustup gcc npm
npm install -g nwlink
rustup default stable
rustup target add thumbv7em-none-eabihf
```

Here is a quick guide about it, assuming the toolchain is already installed:
<!-- TODO: Toolchain installation -->

```bash
git clone https://github.com/numworks/epsilon-sample-app-rust
cd epsilon-sample-app-rust

# To build and install the app on you calculator directly.
cargo run

# To simply build your app
cargo build

# To clean the build cache in case of inconsistent cache
cargo clean
```

The nwa file is located under
`target/thumbv7em-none-eabihf/debug/epsilon-sample-app`, and is ready to be
flashed from NumWorks website just as any normal external app.

@tab Zig

No template for Zig is available, but
[NumWolfstein](https://github.com/zenith391/numworks-wolfenstein) is an app
written in Zig so you can use it as an example.
:::

::: details Upgrading `nwlink`
Unfortunately, the NumWorks template is using an outdated `nwlink` version which
doesn't support newer Node versions.

To upgrade it, change the `NWLINK` definition in the Makefile to use at least
version 0.0.19

```makefile
NWLINK = npx --yes -- nwlink@0.0.19
```

Then, as the syntax changed, replace `eadk-cflags` with `eadk-cflags-device`

```makefile
CFLAGS += $(shell $(NWLINK) eadk-cflags-device)
```

After changing these 2 lines, you are ready to go with the newer nwlink version!
:::

Now you have built and flashed your app, you can play with the API and read the
rest of the documentation to learn things you can do.

## Adding your app to Nwagyu

To add your app to Nwagyu, you can either send a pull request to the
[repo](https://github.com/Yaya-Cout/Nwagyu) of this website, or send us directly
your app (preferably with source code available) to get it added to the website

Here are the steps to follow:

1. Fork the repository
2. Add you app to `src/.vuepress/public/assets/apps/appname-X.Y.Z.nwa`
3. Create a page for your app in `src/guide/apps/appname.md` with the same
   structure as other pages.
4. Reference you app in `src/guide/README.md` and `src/guide/apps/README.md`
5. Repeat all the steps for the french translations by replacing `src/guide` by
   `src/fr/guide` in paths.
6. Add your app to the navbar inside `src/.vuepress/config.js`, in the
   `children` list (you need to do it twice, for both french and english)
7. Open a pull request to add your app

If you can't do the french translation, it's not a big deal, but we will need to
add it before merging (out of sync translations is really bad, as syncing
everything will take time).

[Accessing storage]: storage.md
[On/Off and Home keys]: onoff-home.md
