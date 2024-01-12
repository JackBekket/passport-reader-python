FROM python:3.9

RUN export DEBIAN_FRONTEND=noninteractive && apt-get update && apt-get install -y make

RUN apt-get -y install tesseract-ocr && apt-get -y install tesseract-ocr-fra
RUN apt install -y libsm6 libxext6
RUN apt-get update && apt-get install ffmpeg libsm6 libxext6  -y

COPY . /flask
WORKDIR /flask

RUN mkdir /uploads

RUN pip install -r requirements.txt

# Set the environment variable
#ENV FLASK_APP=app.py
#CMD [ "flask", "run"]
CMD ["python", "app.py","--host=0.0.0.0"]
