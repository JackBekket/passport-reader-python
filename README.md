# Simple passport reader
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Package repository](https://img.shields.io/badge/packages-repository-b956e8.svg?style=flat-square)](https://github.com/patrick-randria/passport-reader)

A very simple python backend API to extract text informations from a passport image file.

## IMPORTANT NOTICE
SCANNING IDENTITY DOCUMENTS IS IN MOST CASES RESTRICTED BY LAW. OBSERVE THE APPLICABLE LAWS USING THIS TOOL. THE COPYRIGHT HOLDER IS NOT IN ANY WAY LIABLE FOR UNLAWFUL USAGE OF THIS TOOL.
THIS APP ONLY SERVES TO DEMONSTRATE THE BASIC USE OF [PassportEye](https://pypi.org/project/PassportEye/) TO SCAN THE MACHINE READABLE ZONES (MRZ) THEN IMPROVE THE RESULT WITH [Tesseract OCR](https://github.com/tesseract-ocr/tesseract).

## Prerequisite
First of all, make sure you have [Docker](https://docs.docker.com/engine/installation/) Engine installed in your system.

For naked python run you need virtual python env (conda) with python v3.9

## Quickstart
Just clone the repo and build the app with docker compose.
```
docker-compose up --build
```

## Troubleshooting
Notes from Bekket:
1. docker-compose did not work properly, probably because bad enviroment for compose.yaml file.
2. docker build works properly most of times
3. still you can't run docker image as it says that ` http invalid host header`. I don't know how to workaround about it.
4. you still can run this without docker, as a python app.

## Run as python app
0. prepare pre-requirements. Docker file contains pkgs that should be installed in virtual enviroment. if we are not using docker, than we need to install them manually. just copy commands from docker file.
Additionally make sure you get tesseract language files installed:
```
wget https://github.com/tesseract-ocr/tessdata/raw/main/eng.traineddata
wget https://github.com/tesseract-ocr/tessdata/raw/main/rus.traineddata

sudo mv -v eng.traineddata /usr/share/tesseract-ocr/4.00/tessdata/
sudo mv -v rus.traineddata /usr/share/tesseract-ocr/4.00/tessdata/

```
1. install miniconda
```
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```
2. create virtual python enviroment
```
conda create --name p39 python=3.9
conda activate p39

```

3. install deps
`cd flask`
`pip install -r requirements.txt`

4. run in dev / production mode
in dev mode
`flask run` -- will listen at localhost only, in this case you need nginx to forward routes. 
`python3 app.py` -- will listen at all availables interfaces. if run from remote VPS will also listen to VPS public ip (port 80,5000)




## Endpoint `http://0.0.0.0:5000/process`
This is the only one endpoint of this app and accept one `POST` parameter :
- `imagefile` : An image file of the passport. For mobile app, we can use the camera.

##### A sample response:
```json
{
    "country": "Madagascar",
    "country_code": "MDG",
    "first_name": "Patrick",
    "last_name": "RANDRIA",
    "nationality": "Madagascar",
    "number": "X00X00000",
    "sex": "M"
}
```

## License

This tool is is available under the The MIT License.
Further details see LICENSE file.
