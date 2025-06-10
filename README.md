# @synthra-swap/sdk-core

[![npm version](https://img.shields.io/npm/v/@synthra-swap/sdk-core.svg)](https://www.npmjs.com/package/@synthra-swap/sdk-core)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

⚒️ **Core SDK for building applications on top of Synthra-swap V3**

A robust and type-safe TypeScript SDK that provides the fundamental entities, utilities, and types needed to interact with the Synthra-swap protocol. This package serves as the foundation layer for all other Synthra-swap SDKs.

## 🚀 Features

- **Core Entities**: Classes for Token, Currency, CurrencyAmount, Price, Fraction, and Percent
- **Trading Utilities**: Functions for price calculations, address validation, and impact analysis
- **Type Safety**: Complete TypeScript typing for enhanced development safety
- **Multi-Chain Support**: Support for Ethereum and compatible networks
- **Precise Mathematics**: Accurate decimal handling and financial calculations
- **Tree Shakable**: Modular imports for optimized bundle sizes

## 📦 Installation

```bash
npm install @synthra-swap/sdk-core
```

```bash
yarn add @synthra-swap/sdk-core
```

```bash
pnpm add @synthra-swap/sdk-core
```

## 🛠️ Basic Usage

### Importing Entities

```typescript
import {
  Token,
  CurrencyAmount,
  Price,
  Percent,
  Fraction
} from '@synthra-swap/sdk-core'
```

### Creating a Token

```typescript
import { Token, ChainId } from '@synthra-swap/sdk-core'

const USDC = new Token(
  ChainId.MAINNET,
  '0xA0b86a33E6441c8442a4F5d4c6d8dcFc7a3e9dc5',
  6,
  'USDC',
  'USD Coin'
)
```

### Working with Amounts

```typescript
import { CurrencyAmount, Token } from '@synthra-swap/sdk-core'

// Create an amount of 100.5 USDC
const amount = CurrencyAmount.fromRawAmount(USDC, '100500000')

// Or from a decimal string
const amountFromString = CurrencyAmount.fromFractionalAmount(
  USDC,
  '100.5',
  '1'
)

console.log(amount.toFixed()) // "100.500000"
```

### Price Calculations

```typescript
import { Price, Token } from '@synthra-swap/sdk-core'

const price = new Price(
  tokenA,
  tokenB,
  '1000000000000000000', // 1 tokenA
  '2000000000000000000'  // = 2 tokenB
)

console.log(price.toFixed(4)) // "2.0000"
```

### Working with Percentages

```typescript
import { Percent } from '@synthra-swap/sdk-core'

// Create a 2.5% percentage
const slippage = new Percent('25', '1000') // 25/1000 = 2.5%

// Or from basis points
const fee = new Percent('30', '10000') // 30 basis points = 0.3%
```

## 📚 API Reference

### Core Entities

#### `Token`
Represents an ERC20 token with its essential properties.

```typescript
constructor(
  chainId: number,
  address: string,
  decimals: number,
  symbol?: string,
  name?: string
)
```

#### `CurrencyAmount`
Represents an amount of a specific currency with decimal precision.

```typescript
static fromRawAmount(currency: Currency, rawAmount: JSBI): CurrencyAmount
static fromFractionalAmount(currency: Currency, numerator: JSBI, denominator: JSBI): CurrencyAmount
```

#### `Price`
Represents the price of one currency in terms of another.

```typescript
constructor(
  baseCurrency: Currency,
  quoteCurrency: Currency,
  denominator: JSBI,
  numerator: JSBI
)
```

#### `Percent`
Extends the Fraction class to represent percentages.

```typescript
constructor(numerator: JSBI, denominator: JSBI)
```

### Utilities

#### `validateAndParseAddress`
Validates and normalizes an Ethereum address.

```typescript
function validateAndParseAddress(address: string): string
```

#### `computePriceImpact`
Calculates the price impact of a swap.

```typescript
function computePriceImpact(
  midPrice: Price,
  inputAmount: CurrencyAmount,
  outputAmount: CurrencyAmount
): Percent
```

## 🔗 Chain Support

The SDK supports the following chains:

- **Ethereum Mainnet** (ChainId: 1)
- **Polygon** (ChainId: 137)
- **Arbitrum One** (ChainId: 42161)
- **Optimism** (ChainId: 10)
- **Base** (ChainId: 8453)

## 🧪 Testing

```bash
npm test
```

The project includes comprehensive tests for all core functionality.

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is released under the MIT License. See the [LICENSE](LICENSE) file for more details.

## 🔗 Related Resources

- [Synthra-swap Protocol Documentation](https://docs.synthra-swap.com)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [Ethereum Development](https://ethereum.org/developers/)

---

**Disclaimer**: This software is provided "as is" without warranty of any kind. Use at your own risk.wap/sdk-core - Now at `Uniswap/sdks`

All versions after 4.2.0 of this SDK can be found in the [SDK monorepo](https://github.com/Uniswap/sdks/tree/main/sdks/sdk-core)! Please file all future issues, PR’s, and discussions there.

### Old Issues and PR’s

If you have an issue or open PR that is still active on this SDK in this repository, please recreate it in the new repository. Some existing issues and PR’s may be automatically migrated by the Uniswap Labs team.
