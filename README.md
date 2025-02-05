# JP-LRN-003-create-llama-fastapi

Steps
 -      poetry install (only do once)
 -      poetry shell
 -      poetry run generate (only do once or if you add new files to the /data folder)
 -      poetry run dev (run the app)
 -      http://localhost:8000 (use swagger to test the api endpoints)



# -------------------------------------------------------------------------------

## code flow

Endpoints are defined here:
 - /app/api/routers/*
 - look in each class for: @r.post("/request")
 - eg. chat.py > @r.post("") async def chat() 
 - get history of messages
 - get doc ids
 - generate filters
 - Setup callbacks
 - Calling LlamaIndex's ChatEngine to get a streamed response
 - return streamed data response


## Example request/response

send request to api:
 - POST http://localhost:8000/api/chat/request (non-streaming endpoint)

```
{
  "messages": [
    {
      "content": "What standards for letters exist?",
      "role": "user"
    }
  ]
}
```

Console logs:
```
Added user message to memory: What standards for letters exist?
=== Calling Function ===
Calling function: query_index with args: {"input":"standards for letters"}
Got output: Letter-size mail must adhere to specific dimensional standards: it should be at least 5 inches long, 3-1/2 inches high, and 0.007-inch thick, with a minimum thickness of 0.009 inches for larger dimensions. The maximum dimensions are 11-1/2 inches long, 6-1/8 inches high, and 1/4-inch thick, with a weight limit of 3.5 ounces. The mailpieces must be rectangular with square corners and parallel sides. Nonmachinable criteria include having an aspect ratio outside the range of 1.3 to 2.5, being enclosed in plastic, having closure devices like clasps or buttons, or not being made of paper.
```

Response:
```
{
  "result": {
    "role": "assistant",
    "content": "Standards for letters, particularly in the context of mail, include specific dimensional and weight requirements:\n\n1. **Minimum Dimensions**:\n   - Length: At least 5 inches\n   - Height: At least 3.5 inches\n   - Thickness: At least 0.007 inches (with a minimum thickness of 0.009 inches for larger dimensions)\n\n2. **Maximum Dimensions**:\n   - Length: Up to 11.5 inches\n   - Height: Up to 6.125 inches\n   - Thickness: Up to 0.25 inches\n\n3. **Weight Limit**: The maximum weight for letter-size mail is 3.5 ounces.\n\n4. **Shape Requirements**: Mailpieces must be rectangular with square corners and parallel sides.\n\n5. **Nonmachinable Criteria**: Letters may be considered nonmachinable if they:\n   - Have an aspect ratio outside the range of 1.3 to 2.5\n   - Are enclosed in plastic\n   - Have closure devices like clasps or buttons\n   - Are not made of paper\n\nThese standards ensure that letters can be processed efficiently by postal services.",
    "annotations": null
  },
  "nodes": [
    {
      "id": "58bb0fe2-50a2-4bcd-a81c-466b3478863a",
      "metadata": {
        "page_label": "1",
        "file_name": "101.pdf",
        "file_path": "L:\\_github\\_JP_github\\JP-LRN-003-create-llama-fastapi\\data\\101.pdf",
        "file_type": "application/pdf",
        "file_size": 47931,
        "creation_date": "2025-02-03",
        "last_modified_date": "2025-01-29",
        "private": "false"
      },
      "score": 0.541831937215857,
      "text": "Domestic Mail Manual • Updated 7-9-23\n101\n101.1.2\nRetail Mail: Physical Standards for Letters, Cards, Flats, and Parcels\n101 Physical Standards\n1.0 Physical Standards for Letters\n1.1 Dimensional Standards for Letters\nLetter-size mail is the following:\na. Not less than 5 inches long, 3-1/2 inches high, and 0.007-inch thick. For \npieces more than 6 inches long or 4-1/4 inches high, the minimum thickness \nis 0.009. (Pieces not meeting the 0.009 thickness are subject to a \nnonmachinable surcharge under 1.2f.) \nb. Not more than 11-1/2 inches long, or more than 6-1/8 inches high, or more \nthan 1/4-inch thick.\nc. Not more than 3.5 ounces. (Charge flat-size prices for First-Class Mail \nletter-size pieces over 3.5 ounces.)\nd. Rectangular, with four square corners and parallel opposite sides. \nLetter-size, card-type mailpieces made of cardstock may have finished \ncorners that do not exceed a radius of 0.125 inch (1/8 inch). See \nExhibit 201.1.1.1.\n1.2 Nonmachinable Criteria\nA letter-size piece is nonmachinable if it has one or more of the following \ncharacteristics (see 601.1.1.2 to determine the length, height, top, and bottom of \na mailpiece):\na. Has an aspect ratio (length divided by height) of less than 1.3 or more than 2.5.\nb. Is polybagged, polywrapped, enclosed in any plastic material, or has an \nexterior surface made of a material that is not paper. Windows in envelopes \nmade of paper do not make mailpieces nonmachinable. Attachments \nallowable under applicable eligibility standards do not make mailpieces \nnonmachinable. \nc. Has clasps, strings, buttons, or similar closure devices.\nOverview 1.0 Physical Standards for Letters\n2.0 Physical Standards for Flats\n3.0 Physical Standards for Parcels\n4.0 Additional Physical Standards for Priority Mail Express\n5.0 Additional Physical Standards for Priority Mail\n6.0 Additional Physical Standards for First-Class Mail and USPS Ground \nAdvantage — Retail\n7.0 Additional Physical Standards for Media Mail and Library Mail",
      "url": "http://localhost:8000/api/files/data/101.pdf"
    },
    {
      "id": "55ca2f7c-22d4-4751-844e-6e1bef03d7f9",
      "metadata": {
        "page_label": "5",
        "file_name": "101.pdf",
        "file_path": "L:\\_github\\_JP_github\\JP-LRN-003-create-llama-fastapi\\data\\101.pdf",
        "file_type": "application/pdf",
        "file_size": 47931,
        "creation_date": "2025-02-03",
        "last_modified_date": "2025-01-29",
        "private": "false"
      },
      "score": 0.5205086536686815,
      "text": "Domestic Mail Manual • Updated 7-9-23\n101\n101.6.2.9\nRetail Mail: Physical Standards for Letters, Cards, Flats, and Parcels\n6.2.3   Other Cards\nA card that does not meet the applicable standards in 6.2 must not bear the \nwords “Postcard” or “Double Postcard.” \n6.2.4   Paper or Card Stock\nA card must be of uniform thickness and made of unfolded and uncreased paper \nor cardstock of approximately the quality and weight of a stamped card (i.e., a \ncard available from USPS). A card must be formed either of one piece of paper or \ncardstock or of two pieces of paper permanently and uniformly bonded together. \nThe stock used for a card may be of any color or surface that permits the legible \nprinting of the address, postmark, and any required markings. \n6.2.5   Acceptable Attachments \nA card may bear an attachment that is the following:\na. A paper label, such as a wafer seal or decal affixed with permanent adhesive \nto the back side of the card, or within the message area on the address side \n(see Exhibit 202.2.1), or to the left of the address block.\nb. A label affixed with permanent adhesive for showing the delivery or return \naddress.\nc. A small reusable seal or decal prepared with pressure-sensitive and \nnonremovable adhesive that is intended to be removed from the first half of \na double card and applied to the reply half. \n6.2.6   Unacceptable Attachment \nA card may not bear an attachment that is the following:\na. Other than paper.\nb. Not totally adhered to the card surface.\nc. An encumbrance to postal processing. \n6.2.7   Tearing Guides\nA card may have perforations or tearing guides if they do not eliminate or \ninterfere with any address element, postage, marking, or endorsement and do \nnot impair the physical integrity of the card. \n6.2.8   Address Side of Cards\nThe address side of a card is the side bearing the delivery address and postage. \nThe address side may be formatted to contain a message area. Cards that do \nnot contain a message area on the address side are subject to the applicable \nstandards for the price claimed. For the purposes of 6.2, miscellaneous graphics \nor printing, such as symbols, logos, or characters, that appear on the address \nside of cards not containing a message area are generally acceptable provided \nthe items are not intended to convey a message. \n6.2.9   Double Cards\nA double card (a double stamped card or double postcard) consists of two \nattached cards, one of which is designed to be detached by the recipient and \nreturned by mail as a single card. Double cards are subject to these standards:",
      "url": "http://localhost:8000/api/files/data/101.pdf"
    }
  ]
}
```




# -------------------------------------------------------------------------------
# Readme file generated from template


This is a [LlamaIndex](https://www.llamaindex.ai/) project using [FastAPI](https://fastapi.tiangolo.com/) bootstrapped with [`create-llama`](https://github.com/run-llama/LlamaIndexTS/tree/main/packages/create-llama).

## Getting Started

First, setup the environment with poetry:

> **_Note:_** This step is not needed if you are using the dev-container.

```
poetry install
poetry shell
```

Then check the parameters that have been pre-configured in the `.env` file in this directory. (E.g. you might need to configure an `OPENAI_API_KEY` if you're using OpenAI as model provider).

If you are using any tools or data sources, you can update their config files in the `config` folder.

Second, generate the embeddings of the documents in the `./data` directory:

```
poetry run generate
```

Third, run the app:

```
poetry run dev
```

Open [http://localhost:8000](http://localhost:8000) with your browser to start the app.

The example provides two different API endpoints:

1. `/api/chat` - a streaming chat endpoint
2. `/api/chat/request` - a non-streaming chat endpoint

You can test the streaming endpoint with the following curl request:

```
curl --location 'localhost:8000/api/chat' \
--header 'Content-Type: application/json' \
--data '{ "messages": [{ "role": "user", "content": "Hello" }] }'
```

And for the non-streaming endpoint run:

```
curl --location 'localhost:8000/api/chat/request' \
--header 'Content-Type: application/json' \
--data '{ "messages": [{ "role": "user", "content": "Hello" }] }'
```

You can start editing the API endpoints by modifying `app/api/routers/chat.py`. The endpoints auto-update as you save the file. You can delete the endpoint you're not using.

To start the app optimized for **production**, run:

```
poetry run prod
```

## Deployments

For production deployments, check the [DEPLOY.md](DEPLOY.md) file.

## Learn More

To learn more about LlamaIndex, take a look at the following resources:

- [LlamaIndex Documentation](https://docs.llamaindex.ai) - learn about LlamaIndex.

You can check out [the LlamaIndex GitHub repository](https://github.com/run-llama/llama_index) - your feedback and contributions are welcome!
