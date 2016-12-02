#### errors
* [Console output](https://gist.github.com/spboyer/3984b735bc4a59cfa642b5bfd01e8264#file-console-output-txt)
* [Log streaming](https://gist.github.com/spboyer/3984b735bc4a59cfa642b5bfd01e8264#file-log-streaming-output-txt)

# Prerequisites
* azure-cli 
* dotnet-cli Preview 3

## Install the latest azure-cli using npm

```bash
$ npm install azure-cli -g
```

## Configure azure-cli

### Login to Azure

```bash
$ azure login
```

The cli prompts you to go to a url and enter a specific code to login to the portal. 

### Enable Azure CLI Service Management mode commands

```bash
$ azure config mode asm
``` 

## dotnet-cli Preview 3

* Linux/macOS - Download from [github/dotnet/core](https://github.com/dotnet/core/blob/master/release-notes/preview3-download.md)
* Visual Studio 2017 - included


# Create the Web app using the dotnet-cli

```bash
# create the destinatation directory
$ mkdir preview3web

# change directory
$ cd preview3web

# create new application with template option of web
$ dotnet new -t web

# restore nuget packages
$ dotnet restore
```

**Console Output**
```bash
  Restoring packages for .../preview3web/preview3web.csproj...
  Writing lock file to disk. Path: .../preview3web/obj/project.assets.json
  Generating MSBuild file .../preview3web/obj/preview3web.csproj.nuget.g.targets.
  Generating MSBuild file .../preview3web/obj/preview3web.csproj.nuget.g.props.
  Restore completed in 1657.5765ms for .../preview3web/preview3web.csproj.

  NuGet Config files used:
      /Users/shayneboyer/.nuget/NuGet/NuGet.Config

  Feeds used:
      https://api.nuget.org/v3/index.json
```


# Creating the Web site using the azure-cli

`--location` sets the Azure region for the site to be created, and the `--git` option set that we will be using git deploy to deploy the application.

```bash
$ azure site create 'preview3web' --location 'East US' --git
```

**Console Output**
```bash
info:    Executing command site create
+ Getting sites
+ Getting locations
info:    Creating a new web site at preview3web.azurewebsites.net
\info:    Created website at preview3web.azurewebsites.net
+
+ Getting locations
info:    Executing `git init`
info:    Initializing remote Azure repository
+ Updating site information
info:    Remote azure repository initialized
+ Getting site information
+ Getting user information
info:    Executing `git remote add azure https://shayneboyer@preview3web.scm.azurewebsites.net/preview3web.git`
info:    A new remote, 'azure', has been added to your local git repository
info:    Use git locally to make changes to your site, commit, and then use 'git push azure master' to deploy to Azure
info:    site create command OK
```

Add the site contents and push to azure.

```bash
$ git add .

$ git commit -m 'init'
```

Push to Azure 

```bash
$ git push azure master
```

