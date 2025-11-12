# drawio-desktop

## About

**drawio-desktop** is a diagramming desktop app based on [Electron](https://electronjs.org/) that wraps the [core draw.io editor](https://github.com/jgraph/drawio).

Download built binaries from the [releases section](https://github.com/jgraph/drawio-desktop/releases).

**Can I use this app for free?** Yes, under the apache 2.0 license. If you don't change the code and accept it is provided "as-is", you can use it for any purpose.

## Security

draw.io Desktop is designed to be completely isolated from the Internet, apart from the update process. This checks github.com at startup for a newer version and downloads it from an AWS S3 bucket owned by Github. All JavaScript files are self-contained, the Content Security Policy forbids running remotely loaded JavaScript.

No diagram data is ever sent externally, nor do we send any analytics about app usage externally. There is a Content Security Policy in place on the web part of the interface to ensure external transmission cannot happen, even by accident.

Security and isolating the app are the primarily objectives of draw.io desktop. If you ask for anything that involves external connections enabled in the app by default, the answer will be no.

## Support

Support is provided on a reasonable business constraints basis, but without anything contractually binding. All support is provided via this repo. There is no private ticketing support for non-paying users.

Purchasing draw.io for Confluence or Jira does not entitle you to commercial support for draw.io desktop.

## Developing

**draw.io** is a git submodule of **drawio-desktop**. To get both you need to clone recursively:

`git clone --recursive https://github.com/jgraph/drawio-desktop.git`

To run this:

1. `npm install` (in the root directory of this repo)
2. `npm start` _in the root directory of this repo_ runs the app. 
   For debugging, use `npm start --enable-logging`.
   For dev mode, use `DRAWIO_ENV=dev npm start`.

Note: If a symlink is used to refer to drawio repo (instead of the submodule), then symlink the `node_modules` directory inside `drawio/src/main/webapp` also.

To release:

1. Update the draw.io sub-module and push the change. Add version tag before pushing to origin.
2. Wait for the builds to complete (<https://travis-ci.org/jgraph/drawio-desktop> and <https://ci.appveyor.com/project/davidjgraph/drawio-desktop>)
3. Go to <https://github.com/jgraph/drawio-desktop/releases>, edit the preview release.
4. Download the windows exe and windows portable, sign them using `signtool sign /a /tr http://rfc3161timestamp.globalsign.com/advanced /td SHA256 c:/path/to/your/file.exe`
5. Re-upload signed file as `draw.io-windows-installer-x.y.z.exe` and `draw.io-windows-no-installer-x.y.z.exe`
6. Add release notes
7. Publish release

_Note_: In Windows release, when using both x64 and is32 as arch, the result is one big file with both archs. This is why we split them.

Local Storage and Session Storage is stored in the AppData folder:

- macOS: `~/Library/Application Support/draw.io`
- Windows: `C:\Users\<USER-NAME>\AppData\Roaming\draw.io\`

Not open-contribution

-----

draw.io is closed to contributions (unless a maintainer permits it, which is extremely rare).

The level of complexity of this project means that even simple changes
can break a _lot_ of other moving parts. The amount of testing required
is far more than it first seems. If we were to receive a PR, we'd have
to basically throw it away and write it how we want it to be implemented.

We are grateful for community involvement, bug reports, & feature requests. We do
not wish to come off as anything but welcoming, however, we've
made the decision to keep this project closed to contributions for
the long term viability of the project.

## TODO

### Code generation and import from diagrams (En cours)

• Enable code generation from diagrams, similar to how Brainboard does for Terraform.
• Example: create a UML class diagram and automatically export the corresponding structure to Java, Python, etc. (similar to what staruml.io can do)
• Conversely, allow code import to automatically generate a diagram (similar to what Mermaid already does <https://www.drawio.com/blog/mermaid-diagrams>).

• This would allow draw.io to be used as a true bridge between visual design and implementation.

### Extension and openness of the plugin system (Pas encore commencé)

• Make plugins available not only on the web version, but also on desktop and integrated versions (Confluence, VS Code, etc.) <https://www.drawio.com/doc/faq/plugins>.

• Enable the creation and sharing of custom plugins via an integrated community marketplace.

• This openness could also be the means to implement the previous functionality (code generation/import).

• We could also add, for example, a simple system allowing users to add other icons created by the community via this menu. Furthermore, when a plugin is installed, it may require certain dependencies. This process could be managed by you through a GitHub repository, where users could submit their own plugin repositories for integration into the system.
It would also be possible to directly add a plugin by providing a link to its repository (a system similar to Terraform's providers, or inspired by Homebrew for dependency management and the marketplace).
