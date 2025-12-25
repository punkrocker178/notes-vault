# Azure Artifacts Credential Provider
We need credential provider to able to install NuGet private packages. [Github Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider?tab=readme-ov-file#setup)
## Installation
1. Download the latest release of [Microsoft.NuGet.CredentialProvider.zip](https://github.com/Microsoft/artifacts-credprovider/releases)
2. Unzip the file
3. Copy the `netcore` (and `netfx` for nuget.exe) directory from the extracted archive to `$env:UserProfile\.nuget\plugins` or `(%UserProfile%/.nuget/plugins/)`

# Install project
`dotnet restore --interactive`

# Run dotnet app
`dotnet run`
# Development SSL certifitcates
`dotnet dev-certs https --clean`
`dotnet dev-certs https --trust`

# Upgrade dotnet 
Remove previous version
`sudo apt remove 'dotnet*' 'aspnet*' 'netstandard*'`

Install SDK
`sudo apt-get update && sudo apt-get install -y dotnet-sdk-9.0`

# Reference
https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu#supported-distributions