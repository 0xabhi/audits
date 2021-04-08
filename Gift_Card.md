# EOS Gift Card Signup Smart Contract Audit Report.

# 1. Summary

This document is a security audit report performed by [Cryptoabhi](https://github.com/slyon/signup) as a contributor to [Callisto Network]() where [EOS Gift Card](https://github.com/slyon/signup) has been reviewed. EOS gift card can be found at [eosgiftcard.com](https://eosgiftcard.com/)

## Contract desription:

GIFT CARD is a EOSIO based smart-contract which allows users to easily create new EOS accounts.


# 2. In scope

- [signup.cpp](https://github.com/slyon/signup/blob/master/signup.cpp)
- [signup.hpp](https://github.com/slyon/signup/blob/master/signup.hpp)
- [extra.cpp](https://github.com/slyon/signup/blob/master/extra.cpp)

# 3. Findings

**1 issues** were reported:

- 0 high severity issues.

- 0 medium severity issues.

- 2 low severity issues/recommendations.


## 3.1. EOS account format :

### Severity: low
### EOS keys format check

### Description :

Any bad actor can call the contract with invalid key format of proper length, please include proper format check for eosio keys

###  Solution - :

Need to add a check for the proper eos key format.

## 3.2. Check if new_account exist :

### Severity: low
### Check for the account's availablity, halt the execution if it exists already.

### Description :

Before calling the "newaccount" action, it is recommended to check if the account "new_name" already exists.

###  Solution - Apply the is_account assertion :

Include a check beforehand to check if the account already exist or not
We can apply a check, something like -
```
eosio::check( !is_account( new_name ), "new account already exist");
```

# 4. Conclusion

No direct exploit of the contract has been found, the audited contract can be deployed and used. however it is recommended to apply the provided checks.
