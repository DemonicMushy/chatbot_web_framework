FROM python:3.7-slim

WORKDIR /api

COPY cosineSimilarity.py flaskApp.py requirements.txt .

RUN apt-get clean && apt-get -y update

RUN apt-get -y install python3-dev build-essential

RUN pip install -r requirements.txt

RUN python -c "import nltk; nltk.download('stopwords'); nltk.download('punkt')"

EXPOSE 5000

CMD ["python", "flaskApp.py"]
