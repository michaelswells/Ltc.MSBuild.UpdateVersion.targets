Ltc.MSBuild.UpdateVersion.targets
=================================
This is a msbuild file which will update `AssemblyInfo.cs` in your ***TFS connected VS project*** automatically on `Release` build.


How this works?
===============
It queries the history from TFS, get latest **changeset id**, then modify the existing `AssemblyVersion` and `AssemblyFileVersion` accordingly.

If ***$(UseBuildNumber) is 0 (Default)***, the version is formatted as `$(MajorVersion).$(MinorVersion).$(ChangesetId).$(MMdd)` where

* $(MajorVersion): Default is 1
* $(MinorVersion): Default is 0
* $(ChangesetId): Latest changeset id of project history queried from TFS
* $(MMdd): Latest changeset modified date in `MMdd` format
* $(BuildNumber): Default is 0 (***Ignored in this case***)

If ***$(UseBuildNumber) is 1***, the version is formatted as `$(MajorVersion).$(MinorVersion).$(BuildNumber).$(ChangesetId)` where

* $(MajorVersion): Default is 1
* $(MinorVersion): Default is 0
* $(BuildNumber): Default is 0
* $(ChangesetId): Latest changeset id of project history queried from TFS

> To prevent assembly referencing issue (strong name, version conflict, etc.), only `AssemblyFileVersion` will change all parts of revision number, `AssemblyVersion` changes only if the `MajorVersion` or `MinorVersion` have been changed.

How to install?
===============
1. Run `Install-Package Ltc.MSBuild.UpdateVersionWithOptions.targets` command in the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console).
2. Done, that's all you have to do.


What's changed by the nuget package
===================================
* Add `Build\UpdateVersion.targets` and `Build\VersionInfo.targets` files to your project.
* Add `<Import />` to your project file (`.csproj`).
