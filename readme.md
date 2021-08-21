# OpenAI GPT-3 Chat using OpenAI API

Train OpenAI completion model using Whatsapp chat export to speak like your friend.

## Setup
Install requirements in venv
```
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Export creds environment variable
`export OPENAI_API_KEY=<insert api key from openai here>`


## Prepare data
Use notebook `create_data_from_whatsapp_export.ipynb` to parse Whatsapp chat export.

`openai tools fine_tunes.prepare_data -f data_alex.csv`
`openai tools fine_tunes.prepare_data -f data_yashodan.csv`

## Train models

`openai api fine_tunes.create -t data_alex_prepared.jsonl -m curie`
`openai api fine_tunes.create -t data_yashodan_prepared.jsonl -m curie`

Trained models:
* alex `curie:ft-user-3r7wl<...>e-2021-08-21-13-09-19`
* yashodan `curie:ft-user-3r7w<...>e-2021-08-21-13-20-04`


## Use trained model

> remember to include prompt `->`

Alex 
```
curl https://api.openai.com/v1/completions \
  -H "Authorization: Bearer sk-Ge<...>QC" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "Do you want to test it out? ->", "model": "curie:ft-user-3r7wl<...>e-2021-08-21-13-09-19"}'
  ```

Yashodan
```
curl https://api.openai.com/v1/completions \
  -H "Authorization: Bearer sk-Ge<...>QC" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "Do you want to test it out? ->", "model": "curie:ft-user-3r7w<...>e-2021-08-21-13-20-04"}'
  ```
