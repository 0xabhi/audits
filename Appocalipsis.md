# Project - Appocalipsis


#### PREPARED FOR :

Client’s name - [apocalipsis](https://github.com/apocalipsis666/) 

Client’s company name - Bestroi.io

#### PREPARED BY :

By Auditor: [0xabhi](http://github.com/0xabhi)


## 1. Summary

[Appocalipsis](https://github.com/apocalipsis666/apocalipsis/blob/master/apocalipsis.sol) smart contract security audit report performed by [Cryptoabhi](https://github.com/cryptoabhi)

Audit performed for [Bestroi.io](bestroi.io)


### Disclaimer - 

The information appearing in this audit is for general discussion purposes only and is not intended to provide legal security guarantees to any individual or entity.
Code might be subject to unidentified flaws.


## 2. Apocalipsis Ethereum Smart Contract:

### Contract description - 

Apocalipsis Smart Contract accepts payment from users only once per address.

* The user should make the payment of minimum 0.05 ETH and provide a referral address
before you specify the broadcast address of the one who invited you. 

* Accepting a payment from the user, the smart contract distributes it to five addresses in equal parts, 
the first being the referral address and 4 other addresses. 

* The user who made the payment and use the refferal for a particular address atmost 7 times. 

* For the first 8000 participants, the limit is 8 times.

* And the payment of each new participant will be distributed in the same way as yours into five equal parts - the five higher addresses of ethereum. 

* Contract can be used on bestroi.io, Each address can participate once!

### In scope

The smart contract file -
- [appocalipsis.sol](https://github.com/apocalipsis666/apocalipsis/blob/master/apocalipsis.sol)

## 3. Findings

In total, **4 issues** were reported including:

- 1 medium severity issue
- 1 low severity issues.
- 2 minor observation.

### 3.1. Naming Compatibility

#### Issue - int underflow and overflow
#### Severity: medium severity

#### Description

This issue have been regarded as one of the most severe bugs in smart contracts and resulted in big hacks like [POWH hack](https://blog.goodaudience.com/how-800k-evaporated-from-the-powh-coin-ponzi-scheme-overnight-1b025c33b530). 

An malicious user can theoritically call the contract with extreme values and make the contract value to overflow(in extreme cases in our contract's case)

#### Solution

It is recommended to use SafeMath Standard library to perform all addition operations like 

```
numMembers = numMembers + uint256(1);

_downrefs[referal].push(msg.sender);

_payments[referal] = _payments[referal] + uint256(1);

_outgoing[msg.sender] = _outgoing[msg.sender] + uint256(1);
```

#### Reference 

- [SafeMath implementation](https://github.com/OpenZeppelin/openzeppelin-solidity/blob/master/contracts/math/SafeMath.sol)

- [Safemath guide](https://medium.com/coinmonks/practicing-safemath-with-solidity-and-openzeppelin-cde4cba9ce39)

### 3.2. Contract proxy calls

#### Severity: low severity

#### Description

It is possible to make the contract call from other proxy contracts. These external smart contracts can deploy and call the contract again and again to virtually trick the contract.

#### Solution

Restrict smart contracts to call 'SendMoney' function. It can be used modifier to ensure that 

```
   // prevent contracts to call functions
    modifier isHuman() {
        address _addr = msg.sender;
        uint256 _codeLength;

        assembly {_codeLength := extcodesize(_addr)}
        require(_codeLength == 0, "sorry humans only");
        _;
    }
    
```

### 3.3. User's upref count

#### Severity: minor observation

#### Description

The self address in last index of upref is meaningless, and can be removed. Also it should be properly specified that we are using only 4 levels of upward reference count.

### 3.4. User's payment count

#### Severity: minor observation

#### Description

Noticed that a mapping is being used for managing only a single varible where the values will be changed only once. An bool can be used instead of the hashmap(mapping variable)

## 4. Conclusion

It is recommended to use more recent versions of Solidity (0.5.0 or newer)

Altought the contract is moderaltely safe and can be deployed, It would be better to deploy after resolving the issue 3.1.

However, the other highlighted issues should be taken into consideration.
