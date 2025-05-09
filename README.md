# 2200290100162

# Number Sequence Service

A microservice that provides access to various number sequences (prime, fibonacci, even, and random) through a REST API. The service maintains a sliding window of unique numbers and calculates their average.

## Getting Started

### Prerequisites
- Node.js (v12 or higher)
- npm (Node Package Manager)

### Installation
1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the server:
   ```bash
   npm start
   ```
The server will start running at `http://localhost:3000`.

## API Documentation

### Endpoint: `/numbers/{numberid}`

Fetches numbers based on the specified type and maintains a sliding window of unique values.

#### Parameters
- `numberid` (path parameter): Type of number sequence
  - `p` - Prime numbers
  - `f` - Fibonacci numbers
  - `e` - Even numbers
  - `r` - Random numbers

#### Response Format
```json
{
    "windowPrevState": [2, 4, 6, 8],       // Previous state of the window
    "windowCurrState": [2, 4, 6, 8, 10],   // Current state after adding new numbers
    "numbers": "[2, 4, 6, 8, 10]",         // Numbers received from the service
    "avg": 6.00                            // Average of numbers in current window
}
```

#### Example Requests
```bash
# Get even numbers
curl http://localhost:3000/numbers/e

# Get prime numbers
curl http://localhost:3000/numbers/p

# Get fibonacci numbers
curl http://localhost:3000/numbers/f

# Get random numbers
curl http://localhost:3000/numbers/r
```

## Features
- Maintains a sliding window of size 10
- Stores only unique numbers
- Automatically removes oldest numbers when window size is exceeded
- Calculates average of numbers in the current window
- Handles API timeouts (500ms limit)
- Returns both previous and current window states

## Error Handling
- Invalid number IDs return 400 Bad Request
- API timeouts and server errors return 500 Internal Server Error
- Proper error messages are included in the response

## Implementation Details
- Built with Express.js
- Uses axios for HTTP requests
- Implements sliding window algorithm
- Handles duplicate numbers
- Maintains state between requests
