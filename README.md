# Castle Windsor

## Spectra QEST fork

This is a fork of Castle Windsor that is being maintained by Spectra QEST. The original Castle Windsor project is no longer actively maintained, and this fork was necessary to implement some community-submitted pull requests which allow us to continue to use Castle Windsor in modern .NET.

### Build

This fork is not current built in DevOps, rather packages are produced locally which can be pushed to the DevOps NuGet feed.

To build, you can just use Visual Studio:
* load the top-level Castle.Windsor.sln solution
* in build\common.props, ensure:
  * `BuildVersion` is the package version you want to produce, e.g. `6.0.1-alpha`
  * `SignAssembly` is `false` (should already be in this fork)
  * `IncludeSymbols` is `false` (should already be in this fork)
* set the configuration to Release
* build the solution

NuGet artifacts will be produced in the .\build folder.

Artifacts can be pushed to the DevOps NuGet feed with, from the repository root:
```
dotnet nuget push --source qest.packages --api-key az .\build\*.nupkg
```

## Overview

<img align="right" src="docs/images/windsor-logo.png">

Castle Windsor is a best of breed, mature Inversion of Control container available for .NET.

See the [documentation](docs/README.md).

## Releases

See the [releases](https://github.com/castleproject/Windsor/releases).

## License

Castle Windsor is &copy; 2004-2023 Castle Project. It is free software, and may be redistributed under the terms of the [Apache 2.0](http://opensource.org/licenses/Apache-2.0) license.

## NuGet Preview Feed

If you would like to use preview NuGet's from our CI builds on AppVeyor, you can add the following NuGet source to your project:

```
https://ci.appveyor.com/nuget/windsor-qkry8n2r6yak
```

## Building

### Conditional Compilation Symbols

The following conditional compilation symbols are currently defined for Windsor:

Symbol                              | .NET 4.6.2         | .NET Standard / 6
----------------------------------- | ------------------ | ------------------
`FEATURE_APPDOMAIN`                 | :white_check_mark: | :no_entry_sign:
`FEATURE_ASSEMBLIES`                | :white_check_mark: | :no_entry_sign:
`FEATURE_PERFCOUNTERS`              | :white_check_mark: | :no_entry_sign:
`FEATURE_REMOTING`                  | :white_check_mark: | :no_entry_sign:
`FEATURE_SECURITY_PERMISSIONS`      | :white_check_mark: | :no_entry_sign:
`FEATURE_SERIALIZATION`             | :white_check_mark: | :no_entry_sign:
`FEATURE_SYSTEM_CONFIGURATION`      | :white_check_mark: | :no_entry_sign:

* `FEATURE_APPDOMAIN` - enables support for features that make use of an AppDomain in the host.
* `FEATURE_ASSEMBLIES` - uses `AssemblyName.GetAssemblyName()` and `Assembly.LoadFile()`.
* `FEATURE_PERFCOUNTERS` - enables code that uses Windows Performance Counters.
* `FEATURE_REMOTING` - supports remoting on various types including inheriting from `MarshalByRefObject`.
* `FEATURE_SECURITY_PERMISSIONS` - enables the use of CAS and `Security[Critical|SafeCritical|Transparent]`.
* `FEATURE_SERIALIZATION` - enables support for serialization of dynamic proxies and other types.
* `FEATURE_SYSTEM_CONFIGURATION` - enables features that use `System.Configuration` and the `ConfigurationManager`.

The following conditional compilation symbols are defined for tests only under .NET 4.6.2:
* `FEATURE_CODEDOM` - enables code that uses `System.CodeDom`.
* `FEATURE_CONSOLETRACELISTENER` - enables code that requires `System.Diagnostics.ConsoleTraceListener`.
* `FEATURE_THREADABORT` - enables code that uses `Thread.Abort()`.
* `FEATURE_WPF` - enables code that uses `PresentationCore.dll`.
