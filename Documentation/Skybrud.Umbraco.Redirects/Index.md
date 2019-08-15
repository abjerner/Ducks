# Skybrud.Umbraco.Redirects

This package features a dashboard and property editor that let's users manage inbound redirects from within the Umbraco backoffice.

URLs can be added to redirect to either a content item, media item or a custom URL.

![image](https://cloud.githubusercontent.com/assets/3634580/22441437/ac65dc6e-e737-11e6-8a5c-e89a46aea3a1.png)

## Installation

1. [**NuGet Package**][NuGetPackage]  
Install this NuGet package in your Visual Studio project. Makes updating easy.

1. [**ZIP file**][GitHubRelease]  
Grab a ZIP file of the latest release; unzip and move the contents to the root directory of your web application.

## Features

- Global dashboard for listing all redirects. Supports filtering and searching.

- Property editor that can be added to either a content item or media item to show inbound redirects

- Package only handles custom redirecs - eg. added manually by an editor. The will let Umbraco 7.5+ handle redirects for renamed pages

- Includes a `RedirectsRepository` for managing the redirects from your own code

[NuGetPackage]: https://www.nuget.org/packages/Skybrud.Umbraco.Redirects
[GitHubRelease]: https://github.com/skybrud/Skybrud.Umbraco.Redirects

## HTTP module

The package comes with a HTTP module that will kick in when Umbraco or IIS returns a response with a 404 status code. If this is the case, the module will look up the requested URL, and then redirect the user if a matching redirect is found in the database. The package will not intercept requests with any status code other than 404.