This fork of https://github.com/MiguelAlho/MudBlazorPackFailure contains reproductions of an issue when using dotnet pack to pack a Blazor Server application into a dotnet tool package. Accessing any of the static assets from wwwroot results in a 404.

# Repro
1. Check out repo
2. `cd DotnetToolStaticFilesNotFound`
3. `dotnet pack`
4. `dotnet tool install -g --add-source .\bin\Debug\ DotnetToolStaticFilesNotFound`
5. `cd ..` - change directory so the wwwroot isn't in your current path
6. Load `localhost:5000` in a browser. No css can be found.

The diference in this version is the inclusion of MudBlazor component library. Mudblazor publishes a required `_content` folder to the `publish` directory when using `dotnet publish` but it does not get included anywhere in the tool package when using `dotnet pack`. 

![comparison between publish and pack](comparison.png)