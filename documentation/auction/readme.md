# T-Bill Primary Auction API Documentation

APIs for placing bids on T-Bill Primary Auctions


#### Definitions
A **Primary Auction** is a process where government securities, such as treasury bills, are sold directly to investors. In this auction, investors can place either **competitive** or **non-competitive** bids. 

Competitive bids allow investors to specify the yield (interest rate) they are willing to accept, and if successful, they can estimate how much income they will generate from their investment. For competitive bids, the government releases a range of rates (minimum and maximum yields) that investors must bid within. These rates are usually made public on Thursdays, and until they are released, investors can only place non-competitive bids. The auction itself typically occurs on Fridays. Competitve bids are not guaranteed and may be rejected by the issuer. In Ghana, the minimum bid for a competitive auction is GHS 500,000. If MinYield or MaxYield is null in that case competitive orders are not allowed.


Non-competitive bids do not require the investor to specify a yield; instead, these bids are guaranteed to be accepted at the average yield determined by the auction, which will be made available after the auction is concluded. Non-competitive bids are the most common type, especially among retail investors who prefer the simplicity and certainty of having their bids accepted. 

#### Request Flow

Use this flow to get an idea of how the auction process works

1. #### Get Available Tenders

   Use this API to get all available tenders.

   > [see documentation](https://blackstargroup.ai/developers?folder=auction&page=getTrenders)

2. #### Calculate Estimated Interest and Maturity Amount

   This API is used to get the maturity amount and use the logic to calculate the estimated interest.

    Make a request like this
   ```json
    {
        "yield": 24,
        "orderSide": "BUY",
        "consideration": 100,
        "currencyCode": "GHS",
        "orderOfferId": "1981d8b9-3962-4048-a580-64e313b18377"
    }
   ```

   And get a response with the following fields
    ```json
    {
        "quantity": "integer",
        "indicativeConsiderationWithTransactionFees": "integer",
    }
   ```

   `quantity` is the maturity amount and
   `indicativeConsiderationWithTransactionFees` is the order amount

   **Calculate Estimated Interest**
   ```javascript
        const estimatedInterest = quantity - indicativeConsiderationWithTransactionFees.
   ```

   > [see documentation](https://blackstargroup.ai/developers?folder=auction&page=calculateMaturity)


3. #### Place Order

   Use this API to send the bid for auction

   > [see documentation](https://blackstargroup.ai/developers?folder=auction&page=placeOrder)
