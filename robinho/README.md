# Robinho

## JSON API endpoints

The JSON API is currently running under the url https://robinho.fakenewsdetector.org/

### Predictions

You can predict the category of a news by calling:

`GET /predict?title=string&content=string`

Response format:

```
{
  predictions: {
    fake_news: float,
    extremely_biased: float,
    clickbait: float
  },
  keywords: [ string ]
}
```

### Postman

Postman is an app that helps you make requests when developing APIs.

We have a postman collection ready for you to use for debugging the API, just [download postman](https://www.getpostman.com/) and import the `dev/postman_collection.json` file.

<img width="303" alt="Postman Collection" src="https://user-images.githubusercontent.com/792201/34436375-8c11a10a-ec7c-11e7-8319-a567613701e4.png">

## Running

### With Docker

#### Running

```sh
make build
make run
```

#### Test Suite

```sh
make test
```

### Without Docker

You will need Python 3 with pip, then you can install the dependencies:

```sh
pip3 install -r requirements.txt
python3 -m nltk.downloader stopwords
```

Now you can retrain the model:

```sh
rm links.csv; python3 . --retrain
```

Then use the saved model to do predictions, by passing the news title and body:

```sh
python3 . "Chora bandidagem" "Chora turma dos direitos humanos. Michel Temer acaba de sancionar..."
>> Extremely Biased

python3 . "Pato rebate provocação de Neymar com foto" "Neymar e Alexandre Pato resolveram brincar com os cabelos um do outro..."
>> Legitimate
```

#### Running

To run the server:

```sh
python3 . --server
```

#### Test Suite

You can run all tests with:

```sh
python3 -m unittest
```

## Deploy

The deploy is made by CircleCI using docker on heroku.

Read more about deploying docker with heroku [on the oficial docs](https://devcenter.heroku.com/articles/container-registry-and-runtime).
