<h1 align="center">
<img src="images/icon.svg" alt="CAVAPA Icon" width="80"><br>
<b>CAVAPA</b><br>Measure the Motion of Groups from Video
</h1>

![CAVAPA Screenshot](https://raw.githubusercontent.com/gregruthenbeck/CAVAPA2019/master/GregTrackCpp/cavapa.png?token=AA2GKC5F5TPW55CLUM7CM5S7VPGJU)

[![license](https://img.shields.io/github/license/peaceiris/mkdocs-material-boilerplate.svg)](https://github.com/gregruthenbeck/cavapa_docs/blob/master/LICENSE)
[![ffmpeg](https://img.shields.io/badge/ffmpeg-v2.8.17-blue)](https://ffmpeg.org/)
![C++](https://img.shields.io/badge/c%2B%2B-11-blue)
[![boost](https://img.shields.io/badge/boost-1.72-blue)](https://www.boost.org/)
[![Visual Studio 2019](https://img.shields.io/badge/Visual%20Studio%202019%20CE-v142-blue)](https://visualstudio.microsoft.com/vs/community/)
![C#](https://img.shields.io/badge/C%23-8.0-blue)
![.Net Framework](https://img.shields.io/badge/.NET%20Framework-v4.7.2-blue)
[![Netlify Status](https://api.netlify.com/api/v1/badges/bd50eb51-4b80-4410-a59f-06394219e7ff/deploy-status)](https://app.netlify.com/sites/cavapa-docs/deploys)
<!-- [![release](https://img.shields.io/github/release/peaceiris/mkdocs-material-boilerplate.svg)](https://github.com/gregruthenbeck/cavapa_docs/releases/latest)
[![GitHub release date](https://img.shields.io/github/release-date/peaceiris/mkdocs-material-boilerplate.svg)](https://github.com/gregruthenbeck/cavapa_docs/releases) -->

CAVAPA is a new method for processing video to compute a novel metric that describes the amount of physical exertion of the moving subjects within the video frame.

## Abstract

CAVAPA aims to simplify the measurement of physical activity of groups. Sports science has long used video analysis for biomechanical insights. It requires no special devices and works on any video, with no strict requirements of camera-angle, lighting conditions, or video format.

Physical activity correlates with general wellbeing (Penedo and Dahn, 2005). Hence, measuring the physical activity of groups is an important tool for quantifying the effectiveness of interventions aimed at improving general wellbeing. School students are of particular interest since it is at this age that life-long habits are established, and schooling has a large opportunity to affect positive changes to attitudes and behaviors surrounding physical activity. Existing methods for measuring the physical activity of groups are varied and have limitations such as requiring specialized devices, requiring manual processing, or being complex to apply to common scenarios.

We are in the process of publishing details of a study in which CAVAPA results are compared with accelerometer data and observational data (manual observational measures). Once the publication is available we will add a link to it here.

## Details

Documentation build using [MkDocs Material Boilerplate].

[MkDocs Material Boilerplate]: https://github.com/gregruthenbeck/cavapa_docs

## Quick start

#### CAVAPA Video processing

```ps
git clone https://github.com/gregruthenbeck/CAVAPA2019
cd CAVAPA2019
./GregTrack.sln
```

Refer to ./README.md (in the CAVAPA2019 folder) for detailed instructions.

#### Documentation Quickstart

```sh
git clone https://github.com/gregruthenbeck/cavapa_docs.git
cd mkdocs-material-boilerplate
pipenv sync --dev
pipenv shell
inv serve --config-file cavapa_docs.yml -d localhost:8008
```

## Links

- [mkdocs/mkdocs: Project documentation with Markdown - GitHub]
- [squidfunk/mkdocs-material: A Material Design theme for MkDocs]

[mkdocs/mkdocs: Project documentation with Markdown - GitHub]: https://github.com/mkdocs/mkdocs/
[squidfunk/mkdocs-material: A Material Design theme for MkDocs]: https://github.com/squidfunk/mkdocs-material

## License

- [MIT License]
- [The graduate cap icon] made by [Freepik] from [www.flaticon.com] is licensed by [CC 3.0 BY]

[MIT License]: https://github.com/gregruthenbeck/cavapa_docs/blob/master/LICENSE
[The graduate cap icon]: https://www.flaticon.com/free-icon/graduate-cap_62627
[Freepik]: https://www.freepik.com/
[www.flaticon.com]: https://www.flaticon.com/
[CC 3.0 BY]: http://creativecommons.org/licenses/by/3.0/

## About Author

- [gregruthenbeck Homepage](https://ruthenbeck.io/)
