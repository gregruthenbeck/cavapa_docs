<h1 align="center">
<img src="https://cavapa.ruthenbeck.io/images/icon.svg" alt="CAVAPA Icon" width="80" style="margin-left: 32px;"><br>
<b>CAVAPA</b><br>
Measure the Motion of Groups from Video<br>
<img src="https://cavapa.ruthenbeck.io/images/cavapa.png" alt="CAVAPA screenshot" style="padding-top: 0.5rem;">
</h1>

[![license](https://img.shields.io/github/license/peaceiris/mkdocs-material-boilerplate.svg)](https://github.com/gregruthenbeck/cavapa_docs/blob/master/LICENSE)
[![FFmpeg](https://img.shields.io/badge/FFmpeg-v2.8.17-blue)](https://FFmpeg.org/)
[![Visual Studio 2019](https://img.shields.io/badge/Visual%20Studio%202019%20CE-v142-blue)](https://visualstudio.microsoft.com/vs/community/)
![C#](https://img.shields.io/badge/C%23-8.0-blue)
[![OSF Project: CAVAPA](https://img.shields.io/badge/OSF.io-CAVAPA-green)](https://osf.io/zwpy5/)
![.Net Framework](https://img.shields.io/badge/.NET%20Framework-v4.7.2-blue)
[![Netlify Status](https://api.netlify.com/api/v1/badges/bd50eb51-4b80-4410-a59f-06394219e7ff/deploy-status)](https://app.netlify.com/sites/cavapa-docs/deploys)

CAVAPA is a new method for processing video to compute a novel metric that describes the amount of physical exertion of the moving subjects within the video frame.

!!! note
    CAVAPA's motion-metric has been validated compared with HR + accelerometer data and manual observational scoring. Full details will be added once the paper is published. In the meantime, see the [Quantitative Validation](#quantitative_validation) section.

This is part of a research project with [Greg Ruthenbeck PhD](https://ruthenbeck.io), Heidi Pasi, [Prof. Taru Lintunen](https://www.researchgate.net/profile/Taru_Lintunen), [Prof. Martin Hagger](https://sites.ucmerced.edu/martinhagger/people/martin-hagger) (and others) at [Jyväskylä University](https://www.jyu.fi/en/), Finland.

This documentation and the CAVAPA source code is written and maintained by [Greg Ruthenbeck](https://ruthenbeck.io) and [contributors tba].

Test data is available via the [CAVAPA Project page](https://osf.io/zwpy5/) at the [Open Science Foundation](https://osf.io). This includes: video samples (input and output), accelerometer data, heart-rate monitor data for all participants of the validation study.

## Abstract

CAVAPA simplifies the measurement of physical activity of groups. Sports science has long used video analysis for biomechanical insights. Other methods rely on specialist hardware like accelerometers or special cameras and motion-tracking markers. CAVAPA works on any video, with no strict requirements of camera-angle, lighting conditions, or video format.

Physical activity correlates with general wellbeing[^1]. Hence, measuring the physical activity of groups is an important tool for quantifying the effectiveness of interventions aimed at improving general wellbeing. Existing methods for measuring the physical activity of groups are varied and have limitations such as requiring specialized devices, requiring manual processing, or being complex to apply to common scenarios.

We are in the process of publishing details of a study in which CAVAPA results are compared with accelerometer data and observational data (manual observational measures, using the [VOST tool](video-observational-scoring)). Once the publication is available we will add a link to it here.

## Quantitative Validation

CAVAPA has been compared with other methods of estimating/measuring physical-activity-levels for an indoor and an outdoor video. The data analyses were conducted using a Python [Jupyter Notebook](https://jupyter.org/). The data-analyses compare manually-observed scoring, accelerometers, hear-rate monitors, with CAVAPA output.

- CAVAPA Validation Data Analysis [CSV data & code on GitHub](https://github.com/gregruthenbeck/cavapa-data)
- CAVAPA Validation Data Analysis live Jupyter Notebook [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/gregruthenbeck/cavapa-data/HEAD?filepath=cavapa_data_jupyter_notebook.ipynb) on [binder.org](https://binder.org))

In summary, the indoor test resulted in a ~0.75 correlation with manually-observed scores of physical activity, and the outdoor test a ~0.65 correlation. A subjective "eye-balling" of the time-series shows that physical-activity is measured by CAVAPA and is arguably better than manual observation (much easier and could actually be more accurate than other measures).

## Installation

- [CAVAPA v1.0.81 Windows Installer msi](https://github.com/gregruthenbeck/cavapa/releases/download/v1.0.81/CavapaInstaller-v1.0.81.msi) 56.7MB.
- [CAVAPA v1.0.81 Windows Installer zip](https://github.com/gregruthenbeck/cavapa/releases/download/v1.0.81/Cavapa-v1.0.81.zip) 51.9MB.

<img src="https://cavapa.ruthenbeck.io/images/cavapa2.png" alt="CAVAPA screenshot" style="padding-top: 0.5rem;">

## Video Pre-Processing

It may be necessary to pre-process video in order to garauntee the best-possible output from CAVAPA.

### Interlaced Video

Many video cameras use interlaced video compression codecs. This will reduce the accuracy of CAVAPA if it is not removed. Fortunately, decoding the frames of the video can be done in [FFmpeg](https://FFmpeg.org/) with some additional command-line parameters via the [YADIF - Yet Another De-Interlacing Filter](http://avisynth.nl/index.php/Yadif).

```sh
ffmpeg -i input.mp4 -vf yadif=parity=auto output.mp4
```

| <img src="https://cavapa.ruthenbeck.io/images/ball_drop_interlace_stripes.png" alt="interlacing striping" style="height:200px;"/> | <img src="images/ball_drop_de-interlaced.png" alt="de-interlaced" style="height:200px;"/> |
| ----------------------------------------------------- | ----------------------------------- |
| Interlacing causes striping                              | Properly decoded de-interlaced frame |

### Consistent Frame-rate

To simplify calculations, all of our videos were processed at 25fps. Videos can be de-interlaced and converted to 25fps with a single command in FFmpeg. The command below also re-encodes the video using the HEVC codec with NVidia's GPU accelerated encoding for smaller files and minimal picture degradation.

```sh
ffmpeg -i in.mp4 -c:v hevc_nvenc -vf yadif=parity=auto -r:v 25 -c:a copy out.mp4
```

If only 25fps conversion is needed, use this command:

```sh
ffmpeg -i in.mp4 -r:v 25 -c:a copy out.mp4
```

### Convert video into images

CAVAPA currently requires a folder containing only images as input. To convert a video into the required format, use the following command in FFmpeg.

```sh
ffmpeg -i my_video.mp4 -q:v 1 -qmin 1 -qmax 1 ./frames/my_video_%06d.jpg
```

!!! info
    Ideally this step wouldn't be needed. We are working on a version of CAVAPA that processes the video directly. This step can be quite slow and requires enough storage space for the decoded frame images.

## Post-Processing

Since CAVAPA processes videos as a squence of images (aka. frames), the output of CAVAPA is also frames (and a .csv data file). The output frame images can be converted to a video using the following commands.

### Encoding CAVAPA output frames into a video

```sh
ffmpeg -i ./cavapa_frames/my_video_%06d.jpg my_video.mp4 -loglevel error
```

### Combining Videos Side-by-Side

![CAVAPA Screenshot](https://cavapa.ruthenbeck.io/images/cavapa.png)

Test videos can be generated that show the input video alongside the CAVAPA-processed video.

```sh
ffmpeg -i videos/original.mpg -i cavapa_output.mp4 -filter_complex '[0:v]pad=iw*2:ih[int];[int][1:v]overlay=W/2:0[vid]' -map [vid] output-sxs.mp4
```

## Documentation

This documentation is built using [MkDocs Material Boilerplate].

[MkDocs Material Boilerplate]: https://github.com/gregruthenbeck/cavapa_docs

### Quick start

```sh
git clone https://github.com/gregruthenbeck/cavapa_docs.git
cd cavapa_docs
pipenv sync --dev
pipenv shell
inv serve --config-file cavapa_docs.yml -d localhost:8008
```

### Dependencies

- Python 3.6 or higher
- pip
- pipenv
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

[^1]:
    Penedo, F.J., Dahn, J.R., 2005. [Exercise and well-being: a review of mental and physical health benefits associated with physical activity](https://journals.lww.com/co-psychiatry/Abstract/2005/03000/Exercise_and_well_being__a_review_of_mental_and.13.aspx). Curr. Opin. Psychiatry 18, 189–193.
