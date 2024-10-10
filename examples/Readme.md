# Testing Guide for Fermi Trading Program [Examples]

## Prerequisites

1. **Ensure you're running the correct version of solana-cli**:

   `sh -c "$(curl -sSfL https://release.solana.com/v1.17.6/install)"`

2. **Clone this repo:**
   `git clone https://github.com/Fermi-DEX/fermi-sdk`

1. **Install dependencies**:
   Ensure that all necessary dependencies are installed. Run the following command:

   `npm install`

2. **Set up environment variables**:
   If the SDK requires any environment variables (e.g., program ID, private keys), ensure they are properly configured before executing the commands.

3. **Add the latest program ID**:
   Update your program ID in the `constants.ts` file under the `examples` directory.

   `vim examples/constants.ts`

   Update the program ID in the file to the latest value [current staging program ID: `DrgsHv79i7B9YBW5jNcgQmXWHvur3MbRGKrbCauBm79z`].

4. **Airdrop tokens**:
   Ensure you have enough tokens for testing. Use the following command to airdrop tokens:

   `npx ts-node examples/airdrop-test-keypairs.ts`

## Step-by-Step Testing Instructions

### Step 1: Create Market

1. **Create a new market**:

   `npx ts-node examples/create-market.ts`

   This script initializes a new market. After running it, note the market ID and add it to the `constants.ts` file:

   `vim examples/constants.ts`

   Add the new market ID under the `MARKET_ID` variable.

### Step 2: Create Open Orders Account

1. **Create an Open Orders account**:

   `npx ts-node examples/create-oo-account.ts`

   This step sets up an account to handle open orders in the market.

### Step 3: Execute Market Order Test

#### A. Market Order

1. **Place Bob’s limit bid**:

   `npx ts-node examples/place_bid_limit_bob.ts`

   This script places a limit order on the bid side of the order book.

2. **Place Alice’s market ask**:

   `npx ts-node examples/place_market_ask_alice.ts`

   This script places a market order on the ask side, which should match with Bob’s bid.

3. **Finalize the market**:

   `npx ts-node examples/finalise-market.ts [OrderID or Event Heap Index]`

   This finalizes the trades based on the order ID or the event heap index to ensure settlements.

#### B. Market Order Direct

1. **Execute a direct market order**:

   `npx ts-node examples/place-market-order.ts`

   Use this script to place a direct market order. This script should handle both placing and finalizing the order in a single step.

#### C. Limit Order + Market Direct

1. **Place Bob’s limit bid**:

   `npx ts-node examples/place_bid_limit_bob.ts`

2. **Place Alice’s ask and settle**:

   `npx ts-node examples/place_ask_settle_alice.ts [OrderID]`

   This will place an ask order and settle it immediately based on the order ID provided.

### Additional Commands

- **Cancel an order**:

  `npx ts-node examples/cancel-order.ts`

  Use this script if you need to cancel any outstanding orders.

- **Settle funds**:

  `npx ts-node examples/settle-funds.ts`

  Settle funds in the market to complete all pending transfers.

### Viewing Market Data and Orderbook

- **View events**:

  `npx ts-node examples/view-events.ts`

- **View open orders**:

  `npx ts-node examples/view-open-orders.ts`

- **View orderbook**:

  `npx ts-node examples/view-orderbook.ts`

  These scripts allow you to view real-time data for the events, open orders, and the current state of the orderbook.
