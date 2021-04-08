# Hirevibes token Smart Contract Audit Report.

# 1. Summary

This document is a security audit report performed by [Cryptoabhi](https://github.com/cryptoabhi) as a contributor to [Callisto Network](https://callisto.network) where [Hirevibes token](https://github.com/hirevibes/token) has been reviewed. Hirevibes can be found at [hirevibes.io](https://www.hirevibes.io/)

## Contract desription:

GIFT CARD is a EOSIO based smart-contract which allows users to easily create new EOS accounts.

# 2. In scope

- [token.cpp](https://github.com/hirevibes/token/blob/master/token.cpp)
- [token.hpp](https://github.com/hirevibes/token/blob/master/token.hpp)

# 3. Findings

**1 issues** were reported:

- 0 high severity issues.

- 0 medium severity issues.

- 1 low severity issues/recommendations.

## 3.1. Use of deprecated indentifier :

### Severity: Low, Recommendation
### Use of deprecated identifiers, macros and data types, for eg - account_name and symbol_code.

### Description :

The smart contract is written for EOSIO_CDT 1.2 compatibility and 2 major changes have already been committed to the toolkit, ie latest version CDT v1.6 deprecate most of the identifier of the contract.

###  Solution - Apply the is_account assertion :

It is recommended to use updated libraries, preferably v1.6+. Detailed information about the updated libraries and macros can be reviewed at [EOSIO CDT upgrading guide](https://eosio.github.io/eosio.cdt/1.6.0/upgrading/1.5-to-1.6.html)

# 4. Conclusion

No direct exploit of the contract has been found, the audited contract can be deployed and used. The contract can be deployed and used safely.
