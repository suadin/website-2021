# Table of Contents

1. [Introduction](#introduction) 
2. [Technologies](#technologies)
3. [Setup](#setup)
4. [Features](#features)

## Introduction
[suadin.de](https://suadin.de/) is a website based on [Blazor WebAssembly](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor) with aim to use it as sandbox to practise full-stack-developer topics outside of restricted job environment.

## Technologies
* [Blazor WebAssembly](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor): project template, run .NET C# code on client, less server communication
* [SignalR](https://docs.microsoft.com/en-us/aspnet/signalr/overview/getting-started/introduction-to-signalr): bidirectional communication between client and server
* [Bootstrap](https://getbootstrap.com/): responsive design

## Setup
* `choco install visualstudio2019community`
  * ensure .NET 5 is installed
  * ensure ASP.NET and .NET core features are enabled
* `choco install docker-for-windows`
  * ensure virtualization (in bios) is enabled
  * ensure `docker run -d -p 80:80 docker/getting-started` works
* `choco install gitkraken` (optional)
  * good tree-overview and diff-tool
* run this website
  * clone project
  * open visual studio
  * run as docker
  * expect browser opens with website
* build & deploy
  * push changes on main branch
  * expect [suadin.de](https://suadin.de/) website contains changes after few minutes automatically
  * details behind automatism on [suadin/infrastructure](https://github.com/suadin/infrastructure)

## Features

### Google Auth

Source documentation [here](https://code-maze.com/google-authentication-in-blazor-webassembly-hosted-applications/):
1. Login to your google account
1. Goto google [credentials](https://console.cloud.google.com/apis/credentials)
1. create credentials for `OAuth-Client-ID`, select website, enter website name, add urls [suadin.de](https://suadin.de) and www.suadin.de
1. take `Client-ID` and `Client-Secret` and add it into configuration
   * `Client-ID` into `appsettings.json`
   * `Client-Secret` into `user secrets` [how to do that?](https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-5.0&tabs=windows)
1. add google middleware:
   ```
   services.AddAuthentication()
    .AddIdentityServerJwt()
    .AddGoogle(o => 
    {
        o.ClientId = Configuration["Authentication:Google:ClientId"];
        o.ClientSecret = Configuration["Authentication:Google:ClientSecret"];
    });
   ```
1. TODO: add button into ui

* [Chatroom](https://docs.microsoft.com/de-de/azure/azure-signalr/signalr-tutorial-build-blazor-server-chat-app) to chat with other website visitors
  * [Auto-Identity](?): allows guests to chat without set a name or explicite join | :warning: **still not implemented**
* [Dark Mode](https://www.reddit.com/r/dotnet/comments/k9ryyw/blazor_webassembly_dark_mode_css_variables/) to be able to switch between dark and light mode
  * [Default Settings](?): take default setting from operating system like [here](https://docs.microsoft.com/en-us/) | :warning: **still not implemented**
