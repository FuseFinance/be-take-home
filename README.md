## Fuse take home

The goal of this challenge is to develop a back-end service for stock trading operations. The service should integrate with a mock vendor API (provided by Fuse) to:

1. List available stocks and user portfolios
2. Execute stock purchase transactions
3. Generate and email daily reports including successful and failed transactions

## Requirements

- The service should be written in Node.js ( any framework is allowed )
- The service has to run locally and should be able to be started in simple steps ( if it doesn't run, it doesn't pass the challenge )
- Feel free to create and use any kind of architecture / db / infrastructure you want

## Considerations

- The stock vendor changes the stock price every 5 minutes
- The stock vendor doesn't work all the time, sometimes it fails

## Deliverables

- The source code of the service in private repository, add the user `@skaznowiecki` / `@sebastian-alvarez-fuse-finance` / `@danielruizr` as a collaborator
- A `README.md` file with instructions on how to run the service and any other information you think is relevant
- A `REPORT.md` file with a description of the architecture and the decisions you made
- Clean commits with clear messages

## API Endpoints

### Base URL

`https://api.challenge.fusefinance.com`

### API-KEY

You should add the `x-api-key` header with the value `nSbPbFJfe95BFZufiDwF32UhqZLEVQ5K4wdtJI2e`

### GET /stocks

The endpoint should return a list of stocks from the vendor and nextToken to get the next page. To get the next page, you should add the `nextToken` as a query parameter.

```
{
    "status": 200,
    "data": {
        "items": [
         ...stock data
        ],
         "nextToken": "string"
    }
}
```

### POST /stocks/:symbol/buy

The endpoint should allow the user to buy a stock. The request should have the following body:

```
{
    "price": 220.67,
    "quantity": 1
}
```

You get the stock price from the previous endpoint, if the price is more/less than 2% from the current stock price, the transaction should fail.

For example:

- If the stock price is 100, and the user tries to buy it for 95, the transaction should fail because it's more than 2% of the stock price
- If the stock price is 100, and the user tries to buy it for 98.5, the transaction should succeed because it's less than 2% of the stock price

## Bonus

- Deploy the service in a cloud provider is a plus ( not required )
