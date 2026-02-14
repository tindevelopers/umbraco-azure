# Umbraco Azure

Umbraco CMS site with Delivery API enabled, deployed to Azure App Service.

## Live Azure installation

| Resource | Details |
|----------|---------|
| **Site** | https://umbraco-site-app.azurewebsites.net |
| **Backoffice** | https://umbraco-site-app.azurewebsites.net/umbraco |
| **Delivery API** | https://umbraco-site-app.azurewebsites.net/umbraco/delivery/api/v2/content |
| **Resource group** | `umbraco-rg` (East US) |
| **App Service** | `umbraco-site-app` |

**Azure Portal**

- [Open Web App in Azure Portal](https://portal.azure.com/#resource/subscriptions/d56a2de1-25e4-476d-bf60-13482be8f0cb/resourceGroups/umbraco-rg/providers/Microsoft.Web/sites/umbraco-site-app)
- [Open Resource Group](https://portal.azure.com/#resource/subscriptions/d56a2de1-25e4-476d-bf60-13482be8f0cb/resourceGroups/umbraco-rg)

## Important: How This Project Gets Updates

This project was created from the [Umbraco .NET templates](https://docs.umbraco.com/umbraco-cms/fundamentals/setup/install/install-umbraco-with-templates) (`dotnet new umbraco`). It is **not** a fork of the [Umbraco-CMS](https://github.com/umbraco/Umbraco-CMS) repository. The core CMS is consumed as **NuGet packages** (e.g. `Umbraco.Cms`).

**To get the latest Umbraco and .NET package updates:**

1. **Check for outdated packages**
   ```bash
   cd MyUmbracoSite
   dotnet list package --outdated
   ```

2. **Update all packages to latest compatible versions**
   ```bash
   dotnet list package --outdated --include-transitive | dotnet add package <PackageId>  # per package
   # or use:
   dotnet add package Umbraco.Cms
   dotnet add package Umbraco.Cms.DevelopmentMode.Backoffice
   ```
   Or in Visual Studio: **Right-click solution → Manage NuGet Packages → Updates**.

3. **Update to a specific Umbraco major/minor** (e.g. 17.2.x when available)
   ```bash
   dotnet add MyUmbracoSite/MyUmbracoSite.csproj package Umbraco.Cms --version 17.2.0
   dotnet add MyUmbracoSite/MyUmbracoSite.csproj package Umbraco.Cms.DevelopmentMode.Backoffice --version 17.2.0
   ```

4. **Restore and test**
   ```bash
   dotnet restore
   dotnet build
   dotnet run --project MyUmbracoSite
   ```

Do **not** try to merge from the `umbraco/Umbraco-CMS` GitHub repo into this solution—that repo is the CMS source code; this project references it via NuGet only.

## Local development

- **.NET:** 10.0 SDK (see [Umbraco setup](https://docs.umbraco.com/umbraco-cms/fundamentals/setup/install/install-umbraco-with-templates)).
- **Run:** `dotnet run --project MyUmbracoSite` (SQLite used locally via `appsettings.Development.json`).

## Deployment

- **Azure:** App Service + Azure SQL in resource group `umbraco-rg`; connection string is configured in the App Service. Publish with `dotnet publish -c Release` and deploy the output (e.g. `az webapp deploy` zip deploy or GitHub Actions).

## Delivery API

The Delivery API is enabled in `appsettings.json`. After the site is installed, content is available at:

- **Live:** https://umbraco-site-app.azurewebsites.net/umbraco/delivery/api/v2/content
