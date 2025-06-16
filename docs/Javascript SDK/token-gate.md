---
title: Token Gate
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Smart contract

### Get Smart contracts

Get all available smart contract addresses of the signed-in user where every smart contract has details like  `network_type`, `contract_address` and `contract_name`.

```javascript JavaScript
import { getSmartContracts } from '@livelike/javascript'

const smartContracts = await getSmartContracts()
  .then(paginatedResponse => paginatedResponse.results)

 
```
