# .NET Hello World (Deploy to Azure)

This repository contains a minimal ASP.NET Core **Hello World** web application and a GitHub Actions workflow configured to deploy to an Azure Web App.

## Files included
- `Program.cs` — minimal ASP.NET Core app (returns "Hello, world!" on `/`)
- `HelloWorld.csproj` — project file targeting .NET 8.0
- `.github/workflows/azure-webapps.yml` — GitHub Actions workflow to build and deploy
- `.gitignore`
- `README.md` — this file

## Quick local run
1. Install .NET 8 SDK: https://dotnet.microsoft.com/download (choose SDK for your OS).
2. From repo root:
   ```bash
   dotnet restore
   dotnet run
   ```
3. Open `http://localhost:5000` (or the console output URL).

## GitHub → Azure deployment (workflow)
The workflow expects two GitHub repository secrets:

1. `AZURE_WEBAPP_NAME` — the exact name of your Azure Web App.
2. `AZURE_WEBAPP_PUBLISH_PROFILE` — the publish profile XML from the Azure Portal.

How to get the publish profile:
- In the Azure Portal, open your Web App.
- In the left menu choose **Get publish profile** and download the `.PublishSettings` file.
- Open the file in a text editor and copy its contents into the `AZURE_WEBAPP_PUBLISH_PROFILE` secret in GitHub.

Push this repository to GitHub. On push to the default branch the workflow will:
- restore and publish the project
- deploy the published output to the Azure Web App

## Notes
- The workflow uses `actions/setup-dotnet` to install .NET 8.
- If you prefer using an Azure Service Principal instead of publish profile, modify the workflow to use `azure/login` and the `azure/webapps-deploy` action with appropriate inputs.
