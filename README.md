# GTIFF2TILES

Analogue of [gdal2tiles.py](https://github.com/OSGeo/gdal/blob/master/gdal/swig/python/scripts/gdal2tiles.py) on C#. Currently support any GEOTIFF, but creates **EPSG:4326** **geodetic** tiles on output in [**tms**](https://wiki.osgeo.org/wiki/Tile_Map_Service_Specification) structure.

Solution is build in VS2017, .NET Framework 4.7.2, targeting Windows x64 systems.

[![Build status](https://ci.appveyor.com/api/projects/status/wp5bbi08sgd4i9bh?svg=true)](https://ci.appveyor.com/project/Gigas002/gtiff2tiles)

## Table of contents

- [GTIFF2TILES](#gtiff2tiles)
  * [Table of contents](#table-of-contents)
  * [Current version](#current-version)
  * [Examples](#examples)
  * [GTiff2Tiles.Core](#gtiff2tilescore)
    + [Dependencies](#dependencies)
  * [GTiff2Tiles.Console](#gtiff2tilesconsole)
    + [Usage](#usage)
  * [Detailed options description](#detailed-options-description)
    + [Dependencies](#dependencies-1)
  * [GTiff2Tiles.GUI](#gtiff2tilesgui)
    + [Dependencies](#dependencies-2)
  * [GTiff2Tiles.Tests](#gtiff2tilestests)
    + [Dependencies](#dependencies-3)
  * [TODO](#todo)
  * [Contributing](#contributing)

Table of contents generated with [markdown-toc](http://ecotrust-canada.github.io/markdown-toc/ ).

## Current version

Current stable can be found here: [![Release](https://img.shields.io/github/release/Gigas002/GTiff2Tiles.svg)](https://github.com/Gigas002/GTiff2Tiles/releases/latest), or on NuGet: [![NuGet](https://img.shields.io/nuget/v/GTiff2Tiles.svg)](https://www.nuget.org/packages/GTiff2Tiles/).

Information about changes since previous releases can be found in [changelog](https://github.com/Gigas002/GTiff2Tiles/blob/master/CHANGELOG.md). This project supports [SemVer 2.0.0](https://semver.org/).

Previous versions can be found on [releases](https://github.com/Gigas002/GTiff2Tiles/releases) and [branches](https://github.com/Gigas002/GTiff2Tiles/branches) pages.

## Examples

In [Examples](https://github.com/Gigas002/GTiff2Tiles/tree/master/Examples/Input) directory you can find **GEOTIFF** for some tests.

## GTiff2Tiles.Core 

**GTiff2Tiles.Core** is a core library. [Here’s](https://github.com/Gigas002/GTiff2Tiles/wiki) the API documentation. 

Library uses 2 different algorithms to create tiles:

- **Crop** - crops all the zooms from input file;
- **Join** - crops the lowest zoom from input file and then join the upper images from built tiles.

Also I should mention, that if your input .tif is not **EPSG:4326**, it will be converted by **GdalWarp** to that projection, and saved in **temp** directory before cropping tiles.

### Dependencies

- [GDAL](https://www.nuget.org/packages/GDAL/) - 2.3.3;
- [GDAL.Native](https://www.nuget.org/packages/GDAL.Native/) - 2.3.3;
- [NetVips](https://www.nuget.org/packages/NetVips/) - 1.0.7;
- [System.Threading.Tasks.Extensions](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/) - 4.5.2;
- [System.Runtime.CompilerServices.Unsafe](https://www.nuget.org/packages/System.Runtime.CompilerServices.Unsafe/) - 4.5.2;

## GTiff2Tiles.Console

**GTiff2Tiles.Console** is a console application, that uses methods from core to create tiles. 

### Usage

| Short |    Long     |          Description          | Required? |
| :---: | :---------: | :---------------------------: | :-------: |
|  -i   |   --input   |    Full path to input file    |    Yes    |
|  -o   |  --output   | Full path to output directory |    Yes    |
|  -t   |   --temp    |  Full path to temp directory  |    Yes    |
|       |   --minz    |     Minimum cropped zoom      |    Yes    |
|       |   --maxz    |     Maximum cropped zoom      |    Yes    |
|  -a   | --algorithm |   Algorithm to create tiles   |    Yes    |
|       |  --threads  |         Threads count         |    No     |
|       |  --version  |        Current version        |           |
|       |   --help    | Message about console options |           |

## Detailed options description

**input** is `string`, representing full path to input **GEOTIFF** file.

**output** is `string`, representing full path to directory, where tiles in tms structure will be created. Should be empty.

**temp** is `string`, representing full path to temporary directory. Inside will be created directory, which name is a **timestamp** in format `yyyyMMddHHmmssfff`.

**minz** is `int` parameter, representing minimum zoom, which you want to crop.

**maxz** is `int` parameter, representing minimum zoom, which you want to crop.

**algorithm** is `string`, representing cropping algorithm. Can be **crop** or **join**. When using **crop**, the input image will be cropped for each zoom. When using **join**, the input image will be cropped for the lowest zoom, and the upper tiles created by joining lowest ones.

**threads** is `int` parameter, representing threads count. By default (if not set) uses 5 threads.

### Dependencies

- [GDAL](https://www.nuget.org/packages/GDAL/) - 2.3.3;
- [GDAL.Native](https://www.nuget.org/packages/GDAL.Native/) - 2.3.3;
- [NetVips](https://www.nuget.org/packages/NetVips/) - 1.0.7;
- [System.Threading.Tasks.Extensions](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/) - 4.5.2;
- [System.Runtime.CompilerServices.Unsafe](https://www.nuget.org/packages/System.Runtime.CompilerServices.Unsafe/) - 4.5.2;
- [CommandLineParser](https://www.nuget.org/packages/CommandLineParser/) - 2.4.3;

## GTiff2Tiles.GUI

**GTiff2Tiles.GUI** is a very simple (and ugly!) GUI, that has the same methods and parameters, as **GTiff2Tiles.Console**.

### Dependencies

- [GDAL](https://www.nuget.org/packages/GDAL/) - 2.3.3;
- [GDAL.Native](https://www.nuget.org/packages/GDAL.Native/) - 2.3.3;
- [NetVips](https://www.nuget.org/packages/NetVips/) - 1.0.7;
- [System.Threading.Tasks.Extensions](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/) - 4.5.2;
- [System.Runtime.CompilerServices.Unsafe](https://www.nuget.org/packages/System.Runtime.CompilerServices.Unsafe/) - 4.5.2;
- [Caliburn.Micro](https://www.nuget.org/packages/Caliburn.Micro) - 3.2.0;
- [Ookii.Dialogs.Wpf](https://www.nuget.org/packages/Ookii.Dialogs.Wpf/) - 1.0.0;

## GTiff2Tiles.Tests

**GTiff2Tiles.Tests** is a unit test project for **GTiff2Tiles.Core**.

### Dependencies

- [GDAL](https://www.nuget.org/packages/GDAL/) - 2.3.3;
- [GDAL.Native](https://www.nuget.org/packages/GDAL.Native/) - 2.3.3;
- [NetVips](https://www.nuget.org/packages/NetVips/) - 1.0.7;

## TODO

You can track, what’s planned to do in future releases on [projects](https://github.com/Gigas002/GTiff2Tiles/projects) page.

## Contributing

Feel free to contribute, make forks, change some code, add [issues](https://github.com/Gigas002/GTiff2Tiles/issues), etc.
