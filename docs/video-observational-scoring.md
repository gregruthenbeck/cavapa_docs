<h1 align="center">
<b>VOST</b><br>Video Observational Scoring Tool<br>
<img src="../images/vost_screenshot.jpg" alt="CAVAPA screenshot" style="padding-top: 0.5rem;">
</h1>

[![license](https://img.shields.io/github/license/peaceiris/mkdocs-material-boilerplate.svg)](https://github.com/gregruthenbeck/cavapa_docs/blob/master/LICENSE)
[![FFmpeg](https://img.shields.io/badge/FFmpeg-v2.8.17-blue)](https://FFmpeg.org/)
[![Visual Studio 2019](https://img.shields.io/badge/Visual%20Studio%202019%20CE-v142-blue)](https://visualstudio.microsoft.com/vs/community/)
![C#](https://img.shields.io/badge/C%23-8.0-blue)
[![OSF Project: CAVAPA](https://img.shields.io/badge/OSF.io-CAVAPA-green)](https://osf.io/zwpy5/)
![.Net Framework](https://img.shields.io/badge/.NET%20Framework-v4.7.2-blue)

VOST simplifies manual scoring from video by synchronizing the selected row with the part of the video that is played. In loop-mode, the values are entered into the spreadsheet-view whilst the part of the video for that row is replayed. Hence you have time to consider the metric value and re-watch the relevant part of the video. No switching back and forth between programs!

Observational scoring (manual scoring) of metrics from video is very time-consuming. Approaches include pausing the video, allowing it to play whilst noting down scores, and adjusting the playback speed to allow metrics to be recorded. VOST supports all of this whilst adding a synchronized spreadsheet view. The spreadsheet view is bi-directionally coupled with the video; 1. When a row in the spreadsheet is selected, the part of the video related to that row is replayed, and 2. When part of the video is selected, the corresponding row of data is selected. This enables better scoring by removing the cumbersome clicking back and forth between a video player and a spreadsheet. The data can be exported to a CSV (Comma-Separated-Values) file, or opened directly in Microsoft Excel.

!!! note
    VOST allows data to be sorted thereby allowing easy comparison of parts of the video that are given the same score. Hence, it is easy to check if metric values are assigned consistently.

## Build Instructions

This tool is currently Windows only. It is written in C# and therefore it may be possible to use [Mono](https://www.mono-project.com/) to compile it for other operating systems. The source code is part of the CAVAPA2019 github repo.

```sh
git clone https://github.com/gregruthenbeck/CAVAPA2019
cd CAVAPA2019/Cavapa_Observation_Score
```

Then open `Cavapa_Observation_Score.csproj` in [Microsoft Visual Studio 2019 Community Edition](https://visualstudio.microsoft.com/vs/community/) or equivalent ([VS Code](https://code.visualstudio.com/) might work). 

## Install Pre-Compiled Binary

If you do not want to build the application from source code: Install the [.Net Framework 4.7.2](https://support.microsoft.com/en-us/help/4054530/microsoft-net-framework-4-7-2-offline-installer-for-windows), and use the [VOST pre-compiled binary (.zip)](dist/CAVAPA-VOST-ObservationScore-v1.zip).

## Video Pre-Processing

Video must be pre-conditioned using FFmpeg before using it with VOST (frame images are needed, it cannot work directly with video).

### Convert video into images

VOST currently requires a folder containing only images as input. To convert a video into the required format, use the following command in FFmpeg.

```sh
ffmpeg -i my_video.mp4 -q:v 1 -qmin 1 -qmax 1 ./frames/my_video_%06d.jpg
```

!!! info
    Ideally this step wouldn't be needed. We are working on a version of CAVAPA that processes the video directly. This step can be quite slow and requires enough storage space for the decoded frame images.

## About Author

- [gregruthenbeck Homepage](https://ruthenbeck.io/)
