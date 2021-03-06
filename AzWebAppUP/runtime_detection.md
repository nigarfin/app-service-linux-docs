# Troubleshoot auto-detect runtime issues with `az webapp up`

The [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest) includes a set of commands to manage Web App resources ([learn more](https://docs.microsoft.com/cli/azure/webapp?view=azure-cli-latest)). Included in this set of commands `az webapp up` bundles functionality to **create** a Web App and **deploy code** from a local workspace. Current support includes apps targeting:

- [Python](#python-detection-logic)
- [Node](#node-detection-logic)
- [ASP .NET and - .NET Core](#ASP-.NET-and-.NET-Core-detection-logic)

As part of the execution of `az webapp up` command it performs a **best effort** detection to match your code (in your local directory) with a supported runtime in your Web App.

> **Important**
>
> `az webapp up` should be run from the local folder containing your code. If you see and runtime auto-detect error message, make sure the command is being executed form the from the directory containing your code and review the auto-detection logic below to ensure you comply with requirements for your stack.
>

The runtime detections logic uses the hints outlined below. Any code that doesn’t match this logic is blocked to avoid compatibility issues.

## Automatic Runtime Detection Logic `az webapp up`

### Python detection logic

Python detection looks for the existence of `requirements.txt` in the current working directory.

### Node detection logic

Node detection looks for the existence of the `package.json` or `sever.js` or `index.js` in the current working directory.

### ASP .NET and .NET Core detection logic

ASP .NET and .NET Core detection is done by looking for the existence of `*.csproj` in the current working directory.

### HTML

Static content needs to use the explicit `--html` flag to indicate that static content is being deployed. Validation is done by looking for `*.html` or `*.htm` or `*.shtml` files in the current working directory

### Manual runtime definition

The runtime is a property of the web app used to host your code. If you want to set the runtime manually you can use the [az webapp create](https://docs.microsoft.com/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.
